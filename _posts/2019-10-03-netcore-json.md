---
layout: post
title: "Novas ferramentas de JSON para .NET Standard"
date: 2019-10-03 08:54:00 -0300
tags: net netcore json
---

O .NET Core 3.0 trouxe novos recursos para manipulação de JSON. Mais precisamente uma nova biblioteca para leitura, criação e serialização de dados nesse formato que tem o objetivo de substituir o onipresente JSON.NET. A princípio eu achei isso um esforço desnecessário, por que mexer em um padrão já estabelecido, eficiente e com uma grande base instalada? Porém, sempre há espaço para melhorias, e a issue [**The future of JSON in .NET Core 3.0**](https://github.com/dotnet/corefx/issues/33115) no repositório do .NET Core me trouxe uma explicação convicente das motivações para criação dessa nova biblioteca:

* **Performance**: o JSON.NET sempre foi referência de performance JSON no .NET, sendo superior as implementações nativas do Framework. Isso prevaleceu em um período em que o .NET não tinha ferramentas como o `Span<T>` que trouxeram um espaço para otimização de implementações de algoritimos em CLR.
* **Remover do ASP.NET a dependência do JSON.NET**: o JSON.NET é bom mas é código proprietário do qual a Microsoft não tem controle. Ao criar sua prórpia biblioteca para um tipo de operação tão fundamental quanto manipulação de JSON eles passam a ter mais flexibilidade para otimizar e evoluir esse workload.
* **Mantendo compatibilidade com o JSON.NET**: ele já esta tão entranhado na maioria das a aplicações .NET que seria um erro absurdo simplesmente substitui-lo, até por ele ter recursos bem específicos que não são o foco das novas bibliotecas, então foram mantidos mecanismos para continuar usando o JSON.NET.

>Essa é uma interpretação pessoal do que o Immo escreveu originalmente na [issue](https://github.com/dotnet/corefx/issues/33115), se desejar saber mais detalhes consulte a página.

Esclarecidas as motivações, meu objetivo aqui é trazer uma referência de uso da nova biblioteca. Pessoalmente estou migrando todos os meus projetos para utilziação dela ao invés do JSON.NET. Explico: em meus projetos procuro sempre reduzir ao máximo o uso de dependências externas à plataforma, que em sí tem um suporte e continuidade. Não é que o JSON.NET vá simplesmente ser descontinuado do dia pra noite, mas se puder não te-lo mais como dependencia e usar um mecanismo embutido no Framework, eu prefiro. Além disso os ganhos de performance são significativos o suficiente para um upgrade.

Vale ressaltar que, **apesar da nova biblioteca ter nascido com o .NET Core 3.0 e fazer parte de sua distribuição básica, ela também é distribuida através do pacote [`System.Text.Json`](https://www.nuget.org/packages/System.Text.Json) sendo retrocompatível com a maioria dos monikers .NET, incluindo .NET Standard 2.0 e consequentemente o Xamarin**.

## Serialização e Deserialização de Objetos em JSON
Essas são as operações básicas em projetos que consumam e gerem JSON sob um modelo de dados pré-definido. Tomemos por exemplo a classe:

```csharp
class Person
{
    public string Name { get; set; }
    public string Email { get; set; }
    public DateTime DateOfBirth { get; set; }
}
```

Para serializar um objeto usamos a classe `JsonSerializer` que contém diversos métodos estáticos para serialização e deserialização. Na prática o API acaba sendo muito semelhante ao do próprio JSON.NET:

```csharp
using System.Text.Json;
using System.Text.Json.Serialization;

var person = new Person
{
    Name = "Pessoa da Silva",
    Email = "pessoa@silva.com",
    DateOfBirth = new DateTime(1983, 2, 25, 10, 30, 0),
};
var personJson = JsonSerializer.Serialize(person);
```

Produz o seguinte JSON como resultado:

```json
{
  "Name": "Pessoa da Silva",
  "Email": "pessoa@silva.com",
  "DateOfBirth": "1983-02-25T10:30:00"
}
```

Que pode ser facilmente transformado de volta em objeto:

```csharp
var deserializedPerson = JsonSerializer.Deserialize<Person>(personJson);
```

Ambos métodos `Serialize` e `Deserialize` aceitam um objeto do tipo `JsonSerializerOptions` que controla seu comportamento. Essa classe tem uma propriedade `PropertyNamingPolicy` que permite por exemplo serializar ou deserializar os nomes das propriedades como _Camel Case_, que é um padrão mais comum.

Além disso, ainda temos os atributos que podem ser aplicados aos elementos da classe e que também modificam o comportamento do serializador. O mais comum deles é o `JsonPropertyName`, que nos permite definir um nome específico para uma determinada propriedade:

```csharp
class Person
{
    public string Name { get; set; }
    public string Email { get; set; }

    [JsonPropertyName("birthday")]
    public DateTime DateOfBirth { get; set; }
}
```

Fará com que o serializador produza o seguinte JSON:

```json
{
  "name": "Pessoa da Silva",
  "email": "pessoa@silva.com",
  "birthday": "1983-02-25T10:30:00"
}
```

E por fim temos o atributo `JsonIgnore`, que faz com que o Serializador ignore completamente aquela propriedade. Podemos aplicar isso a uma nova propriedade computada em nosso modelo:

```csharp
[JsonIgnore]
public int Age => (int)((DateTime.Now - DateOfBirth).TotalDays / 365);
```

Com isso o resultado final será o mesmo JSON anterior.

Além dessas operações básicas, a nova biblioteca também conta com uma série de API's para criação e manipulação de JSON dinamicamente, e para trabalhar com Streams de maneira assíncrona. Consulte a documentação para ver todas as possibilidades.

## Referências

* [What's New in .NET Core 3 - Fast Built-in JSON Support](https://docs.microsoft.com/en-us/dotnet/core/whats-new/dotnet-core-3-0#fast-built-in-json-support)
* [The future of JSON in .NET Core 3.0](https://github.com/dotnet/corefx/issues/33115)
* [System.Text.Json and new built-in JSON support in .NET Core](https://www.hanselman.com/blog/SystemTextJsonAndNewBuiltinJSONSupportInNETCore.aspx)
* [Pacote `System.Text.Json`](https://www.nuget.org/packages/System.Text.Json)