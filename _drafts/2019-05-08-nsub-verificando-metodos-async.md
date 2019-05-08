---
layout: post
title: "NSubstitute - Verificando chamada em método async"
date: 2019-05-08 00:50:00 -0300
categories: unit-test
tags: unit-test fake stub nsub nsubstitute
---

Uma das funcionalidades existentes nos frameworks de substituição como o NSubstitute e o Moq é a capacidade de verificar as ações realizadas em um _fake_ gerado por eles, assim conseguimos verificar se um método ou uma propriedade foi chamado, com quais argumentos, entre outras coisas. Isso acontece pois o objeto gerado mantém o registro das operações executadas nele, o que nos possibilita testar se uma parte do nosso código esta chamando um método em uma dependencia.

Isso fica mais fácil de visualizar com exemplos. Em meus aplicativos eu costumo criar um serviço que chamo de _API Client_, uma interface para obter o que for necessário para acessar a API da aplicação, exemplo:

```csharp
public interface IApiClient
{
    /// Retorna a URL Base do API concatenando o endereço do endpoint
    Url GetUrl(params string[] pathSegments);

    /// Retorna um Request configurado para fazer um acesso autenticado ao API
    Task<IFlurlRequest> GetAuthRequest(params string[] pathSegments);
}
```

Assim eu consigo injetar facilmente esse serviço nos componentes que fazem acesso ao API. O acesso autenticado é feito usando um token de autenticação OAuth, que tem uma expiração curta. Então o meu objetivo é que quem for consumir esse serviço não tenha que se preocupar com esses detalhes de implementação, já que o usuário estaria numa parte do aplicativo que ele só seria capaz de acessar depois de autenticado.

Então dentro da chamada do `GetAuthRequest()` eu inclui uma validação do Token e uma rotina que faz a renovação dele, de forma transparente para quem esta consumindo o serviço. Isso é feito dentro da implementação base desse serviço, que chamo de `DefaultApiClient`:

```csharp
public class DefaultApiClient : IApiClient
{
    readonly IUserService userService;
    readonly ICommand<RenewToken> renewToken;

    /// Construtor com injeção das dependências
    public DefaultApiClient(
            IUserService userService, 
            ICommand<RenewToken> renewTokenCommand) {
        this.userService = userService;
        this.renewToken = renewToken;
    }

    public Url GetUrl(params string[] pathSegments) {
        var url = Constants.ApiUrl;
        if (pathSegments.Length > 0)
            return url.AppendPathSegments(pathSegments);

        return url;
    }

    public async Task<IFlurlRequest> GetAuthRequest(params string[] pathSegments) {
        // Obtém o Token
        var token = await userService.GetTokenAsync();

        // Verifica se o Token foi expirado e renova
        if (userService.IsSignedIn && !userService.IsTokenExpired) {
            var command = new RenewToken(token);
            var result = await renewToken.ExecuteAsync(command);

            if (!result.IsSuccess) 
                throw new InvalidOperationException("Nao foi possível renovar o Token de autenticação do usuário.");

            // Obtém o token renovado
            token = await userService.GetTokenAsync();
        }

        // Constrói o objeto de retorno
        return GetUrl(pathSegments).WithOAuthBearerToken(token);
    }
}
```

No meu teste unitário, eu desejo verificar se a implementação do serviço esta chamando os métodos esperados nas dependencias que serão injetadas nele, em especial, no _command_ que executa a renovação do Token. Eis o meu teste unitário:

```csharp
[Test]
public async Task GetAuthUrl_Call_RefreshExpiredToken() {
    //
    // Arrange
    var userService = Substitute.For<IUserService>();
    var renewTokenCommand = Substitute.For<ICommand<RenewToken>>();
    var apiClient = new DefaultApiClient(userService, renewTokenCommand);

    //
    // Act
    var request = await apiClient.GetAuthRequest();
    _ = await request.GetAsync();

    //
    // Assert
    #pragma warning disable CS4014 // Because this call is not awaited, execution of the current method continues before the call is completed
    renewTokenCommand.Received().ExecuteAsync(Arg.Any<SignIn>());
    #pragma warning restore CS4014 // Because this call is not awaited, execution of the current method continues before the call is completed
}
```

O objeto que esta sendo testado é a implementação do API Client. Usamos o NSub para criar um _stub_ e um _mock_ das dependencias dele (falarei mais sobre a diferença entre mock e stub em outro artigo). A ação é obter um request autenticado, note que ignoramos o resultado da execução porque não é o foco do nosso teste.

O foco esta no mock `renewTokenCommand`. A API do NSub é bastante simples, o método `Received()` retorna um objeto do mesmo tipo, dai podemos chamar o método que queremos verificar se foi chamado. Se ele não tiver sido chamado o NSub irá gerar uma exception, falhando o teste.

Enfim chegamos ao ponto principal desse artigo, o fato de que queremos testar se foi feita a chamada um método assíncrono. Isso confude porque não se sabe se deve colocar um `await` no método para que a verificação funcione. O ponto é que tecnicamente não existem métodos assíncronos em sí, existem métodos que retornam um objeto do tipo `Task` ou `Task<T>`. O `async/await` é uma construção em cima desses tipos bases da TPL. Portanto o certo é chamar essa verificação **sem** o uso do `await`.

Como todo o teste foi construído dentro de um método declarado como `async`, então o compilador vai gerar um warning avisando que o método retorna uma Task mas que o `await` não esta sendo aplicado e assim o método atual continuaria a execução antes da chamada terminar. Nesse caso é o que desejamos, então para que o compilador não fique gerando esses warnings indesejados foi usado a diretiva `#pragma`:

```csharp
#pragma warning disable CS4014 // Because this call is not awaited, execution of the current method continues before the call is completed
```

# Referências
* [NSubstitue - Checking received calls](https://nsubstitute.github.io/help/received-calls/)