---
layout: post
title: "XAML Styler para Visual Studio for Mac"
date: 2019-05-28 20:35:00 -0300
categories: programação git
tags: programação git
---

Na semana passada o [Xamarin Show](https://channel9.msdn.com/Shows/XamarinShow) publicou um episódio falando sobre o [**XAML Styler**](https://github.com/Xavalon/XamlStyler), um plugin para formatação de arquivos XAML que foi ressucitado recentemente. O que ele não cita nesse vídeo, e que por coicidencia eu descobri momentos antes de assist-lo, é que existe uma versão desse plugin para o Visual Studio for Mac. Ele pode ser encontrado na galeria de plugins:

![](/assets/images/xaml-styler/gallery.png)

Legal! Mas o que eu ganho com essa extensão? Quem já trabalhou bastante com XAML sabe o quanto esse tipo de arquivo pode ser chato de formatar de um jeito que fique legível, afinal XML já não é la uma das linguagens mais simpáticas a leitura pelo seu excesso de repetições e pontuações, mas ainda há diversas extensões no XAML que podem tornar a leitura ainda mais confusa. Na versão para, o XAML Styler instala um novo comando no meu _Edit_, o _Format XAML_:

![](/assets/images/xaml-styler/menu.png)

Esse comando aciona a formatação do XAML Styler, veja que lindo o resultado num arquivo de uma `ContentPage` nova, que tem um template que já vem com uma formatação desgraçada:

![](/assets/images/xaml-styler/applying.gif)

Só que o ponto chave é que essa formatação é totalmente personalizável como você pode conferir na tela de preferências:

![](/assets/images/xaml-styler/options.png)

Nesse menu há algumas opções herdadas do XAML para WPF, já que o projeto do plugin vem dessa época. Pessoalmente esse plugin me caiu como uma luva, pois eu sempre me pego gastando um tempo razoável fazendo esse tipo de formatação. Talvez seja apenas um chilique meu, mas eu realmente sinto que consigo ler com mais facilidade e velocidade um código que esteja com uma formatação adequada, e esse é um conceito que levo para todas as linguagens que trabalho, desde do C# até o CSS e à forma como escrevo queries do SQL.

# Referências
* [XAML Styler no GitHub](https://github.com/Xavalon/XamlStyler)