---
layout: post
title: "Criando Arquivos .gitignore"
date: 2019-05-16 12:41:00 -0300
categories: programação git
tags: programação git
---

A configuração de um repositório de código para seu projeto para boa convivência com seu time, passa pela criação de um bom arquivo `.gitignore`. Nesse arquivo configuramos uma lista de exclusões, arquivos que não serão incluidos nem rastreados pelo git dentro do repositório. Mas qual a finalidade, o repositório não é justamente o espaço onde temos uma cópia completa do código fonte para que o projeto possa ser acessado e recompilado em qualquer ambiente?

Tanto o sistema operacional quanto as ferramentas de desenvolvimento, compiladores, etc, produzem uma série de arquivos temporários ou de configurações que são específicas para nosso usuário ou ambiente. Alguns exemplos disso:

* **.DS_Store**: é uma pasta oculta que o macOS cria com metadados do Finder. É completamente descartável.
* **._**: arquivos de thumbnails no macOS, também para uso específico no Finder e totalmente descartável.
* **Desktop.ini**: metadados do Windows Explorer, criado como arquivo oculto a medida que você vai ajustando os parâmetros de visualização de uma pasta.
* **Thumbs.db**: gerado como arquivo oculto pelo Windows para fazer cache das thumbnails de imagens que existam na pasta.

Além disso, algumas IDE's como o Visual Studio e o Android Studio, geram os arquivos intermediários de compilação e os binários dos projetos em subpastas do próprio projeto. Esses arquivos são re-criados a todo momento no processo de desenvolvimento e, incluí-los no repositório, só aumentaria seu tamanho desnecessariamente e geraria mais conflitos ao fazer merges. Por esses motivos a configuração adequada de um `.gitignore` se faz importante!

Mas como determinar quais as exclusões necessárias para meu projeto? Entra o [`gitignore.io`](https://www.gitignore.io), um projeto open source extremamente simples que organiza as exclusões por tags de sistemas operacionais, IDE's ou linguagens de programação, e o melhor, sem gerar duplicidades no resultado final.

![Site do gitignore.io](/assets/images/gitignore-io.png)

O funcionamento é extremamente simples, basta digitar as tags dos sistemas operacionais, linguagens ou ambientes de desenvolvimento que você. Por exemplo, quando vou criar o repositório para um novo projeto do Xamarin uso as seguintes tags: `Windows`, `macOS`, `Csharp`, `VisualStudio`, `XamarinStudio`, `xcode`, `Android`, `AndroidStudio`. O racional é o seguinte: o repositório será usado por programadores nos 2 sistemas operacionais, então eu não quero que sejam incluídos arquivos específicos dessas plataformas. O projeto sera feito com C#, usando o Visual Studio para Windows ou macOS (antes Xamarin Studio). Também incluo o `Xcode`, `Android` e `AndroidStudio` pois como o projeto terá Android e iOS isso exclui alguns arquivos específicos dessas plataformas.

O mais legal é que o `gitignore.io` gera usa URL's amigáveis, então você pode compartilhar facilmente com o time ou até mesmo passar batido pelo site chamando direto a url. Veja o endereço com as tags que defini anteriormente:

```
https://www.gitignore.io/api/xcode,macos,csharp,android,windows,visualstudio,androidstudio,xamarinstudio
```

Basta colocar as tags que você deseja após o `api/` separadas por vírgula.

## Bonus - dotnet-giio

O [`dotnet giio`](https://github.com/liammoat/dotnet-giio/blob/master/README.md) é uma ferramenta global do .NET Core que facilita a criação de arquivos `.gitignore` direto pelo terminal ou linha de comando. Ele tem comandos para consultar as tags e gerar o arquivo. Sua instalação é bastante simples:

```
dotnet tool install --global dotnet-giio
```

Serei repetitivo pois essas informações estão na documentação do utilitário, mas como é tão simples reproduzo aqui traduzidas! Para gerar um novo gitignore usando as tags para Windows e Visual Studio:

```
dotnet giio generate visualstudio windows
```

Para consultar as tags disponíveis no serviço, use o comando list:

```
dotnet giio list --query visualstudio
```

Passe as palavras chave para o parâmetro query para filtrar o resultado. Nesse caso ira retornar `VisualStudio` e `VisualStudioCode`. Sem o parâmetro query retorna todas as tags disponíveis.

Por fim, é possível dar preview no arquivo que seria gerado com um conjunto de tags:

```
donet giio preview visualstudio windows macos
```

# Conclusão
Embora a criação de repositórios não seja uma tarefa tão frequente, é certamente recorrente e ajustar esses arquivos de configuração sempre foi uma dor de cabeça. Depois que eu comecei a usar esse serviço nunca mais tive problemas.