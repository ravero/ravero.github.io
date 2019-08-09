---
layout: post
title: "Extendendo o Menu de Contexto do editor XAML do Visual Studio"
date: 2019-08-08 00:45:00 -0300
categories: visualstudio vsix
tags: visualstudio vsix
---

Em um dos projetos que estou atendendo, o MFractor, estamos portando as funcionalidades da extensão criada originalmente para o Visual Studio de Mac para seu irmão mais velho no Windows. Uma dessas funções são os atalhos do MVVM que, em um projeto do Xamarin.Forms, permitem alternar rapidamente entre o XAML de uma View seu code-behind e seu View Model. Para isso extendemos o menu de contexto do editor. Há uma série de artigos sobre como extender esse menu, mas no caso específico do editor de arquivos XAML, a forma padrão não estava funcionando.

Depois de muito cavocar finalmente achei [uma thread no Gitter](https://gitter.im/Microsoft/extendvs/archives/2016/05/19) com uma discussão em cima exatamente dessa dúvida. Ao que tudo indica esse editor de arquivos XAML é diferente dos demais editores e não extendido através do id padrão (guid: `guidSHLMainMenu` e id: `IDM_VS_CTXT_CODEWIN`) e as contantes desse novo editor para extender seu menu de contexto através do _Command Table_ não foram específicadas em nenhuma documentação.

A solução é declarar o `GuidSymbol` e `IDSymbol` correspondentes a essa função no arquivo .vsct da extensão, eis como estamos usando:

```xml
<GuidSymbol name="guidXamlCmdSet" value="{4C87B692-1202-46AA-B64C-EF01FAEC53DA}">
    <IDSymbol name="editorContextMenu" value="259"/>
</GuidSymbol>
```

Esse símbolo corresponde ao que eles conseguiram capturar usando a função [`EnableVSIPLogging`](https://blogs.msdn.microsoft.com/dr._ex/2007/04/17/using-enablevsiplogging-to-identify-menus-and-commands-with-vs-2005-sp1/) que exibe mensagens de Debug com as referências aos elementos da IDE do Visual Studio (e que eu não consegui habilitar no Visual Studio 2019):

![](https://files.gitter.im/Microsoft/extendvs/OEup/blob)

Muito bem, com isso conseguimos então usar esses ID's para declarar um _Command Placement_ para os comandos que desejamos exibir nesse menu de contexto:

```xml
<CommandPlacement guid="[GuidDoGrupo]" id="[IdDoGrupo|Comando]" priority="0x0001">
    <Parent guid="guidXamlCmdSet" id="editorContextMenu" />
</CommandPlacement>
```

Dessa forma os comandos desse grupo passam a aparecer no menu de contexto:

![](/assets/images/mvvm-shortcuts-xaml.png)