---
layout: post
title: "Novas ferramentas de JSON para .NET Standard"
date: 2019-10-03 08:54:00 -0300
tags: net netcore json
---

O .NET Core 3.0 trouxe novos recursos para manipulação de JSON. Mais precisamente uma nova biblioteca para leitura, criação e serialização de dados nesse formato que tem o objetivo de substituir o onipresente JSON.NET. A princípio eu achei isso um esforço desnecessário, por que mexer em um padrão já estabelecido, eficiente e com uma grande base instalada? Sempre há espaço para melhorias, e a issue [**The future of JSON in .NET Core 3.0**](https://github.com/dotnet/corefx/issues/33115) no repositório do .NET Core me trouxe uma explicação convicente das motivações para criação dessa nova biblioteca:

* **Performance**: o JSON.NET sempre foi referência de performance JSON no .NET, sendo superior as implementações nativas do Framework. Isso prevaleceu em um período em que o .NET não tinha ferramentas como o `Span<T>` que trouxeram um espaço para otimização de implementações de algoritimos em CLR.
* **Remover do ASP.NET a dependência do JSON.NET**: o JSON.NET é bom mas é código proprietário do qual a Microsoft não tem controle. Ao criar sua prórpia biblioteca para um tipo de operação tão fundamental quanto manipulação de JSON eles passam a ter mais flexibilidade para otimizar e evoluir esse workload.
* **Mantendo compatibilidade com o JSON.NET**: ele já esta tão entranhado na maioria das a aplicações .NET que seria um erro absurdo simplesmente substitui-lo, até por ele ter recursos bem específicos que não são o foco das novas bibliotecas, então foram mantidos mecanismos para continuar usando o JSON.NET.

>Essa é uma interpretação pessoal do que o Immo escreveu originalmente na [issue](https://github.com/dotnet/corefx/issues/33115), se desejar saber mais detalhes consulte a página.

Esclarecidas as motivações, meu objetivo aqui é trazer uma referência de uso da nova biblioteca. Pessoalmente estou migrando todos os meus projetos para utilziação dela ao invés do JSON.NET. Explico: em meus projetos procuro sempre reduzir ao máximo o uso de depdências externas a plataforma, que em sí tem um suporte e continuidade. Não é que o JSON.NET vá simplesmente ser descontinuado do dia pra noite, mas se puder não te-lo mais como dependencia eu prefiro. Além disso os ganhos de performance são significativos o suficiente para um upgrade.

Vale ressaltar que apesar da nova biblioteca ter nascido com o .NET Core 3.0 e fazer parte de sua distribuição básica, ela também é distribuida através do pacote [`System.Text.Json`](https://www.nuget.org/packages/System.Text.Json) sendo retrocompatível com a maioria dos monikers .NET, **incluindo .NET Standard 2.0 e consequentemente o Xamarin**.

## Serialização e Deserialização de Objetos em JSON
Uma das operações mais triviais com JSON é a serialização e deserialização de objetos .NET para JSON. 