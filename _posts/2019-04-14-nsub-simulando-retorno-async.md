---
layout: post
title: "NSubstitute - Simulando retorno de um método async"
date: 2019-04-14 20:20:00 -0300
categories: unit-test
tags: unit-test fake stub nsub nsubstitute
---

Em testes unitários um _stub_ é um tipo de _fake_ usado para simular o código de uma dependência do objeto ou tema que esta sendo testado (subject under test ou _sut_). Em meus projetos adotei o NSubstitute como ferramenta para criação de fakes. Ele possibilita configurar de maneira bem simples um objeto para que ele tenha retorno específicos as chamadas de seus métodos.

A API do NSub é bem simples. Para criar um _stub_ de uma interface por exemplo, basta chamar o método `For<T>` da classe Substitute, que se escreve de maneira fluente:

```csharp
var stub = Substitute.For<IUserService>();
```

A interface em questão tem a seguinte declaração:

```csharp
public interface IUserService
{
    Task<string> GetTokenAsync(bool legacy = true);
    Task<User> GetUserAsync();
    bool IsSignedIn { get; }
}
```

O NSub vai criar um objeto com um classe anonima implementando a interface, com uma implementação padrão para cada um dos seus elementos. Supondo que você queira que a propriedade `IsSignedIn` retorne `true` quando for chamada, bastaria configurar dessa forma:

```csharp
stub.IsSignedIn.Returns(true);
```

A mesma técnica se aplica para métodos, porém note que a interface de exemplo tem uma particularidade: seus métodos assíncronos. Então me deparei com um cenário onde o método precisava retornar um valor específico em uma chamada com `await`. Como simular isso?

Como métodos assíncronos na verdade retornam um objeto do tipo `Task<T>`, é necessário um pequeno ajuste no método `Returns` para que ele receba uma Task com o resultado desejado inserido:

```csharp
stub.GetTokenAsync(Arg.Any<bool>())
    .Returns(
        Task.FromResult("TEST TOKEN")
    );
```

Essa técnica funcionará independente do framework de testes que estiver usando (xUnit, NUnit, MSTest, etc.), pois é própria do NSubstitute. Creio que seja simples transcrever para outros frameworks de fakes como o Moq.