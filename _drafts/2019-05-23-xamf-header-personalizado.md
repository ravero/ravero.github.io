---
layout: post
title: "Xamarin.Forms - Barra de Navegação Personalizada"
date: 2019-05-16 12:41:00 -0300
categories: programação git
tags: programação git
---

O Xamarin.Forms a partir da versão 3.2.0 introduziu um recurso muito útil, a capacidade de personalizar a barra da navegação com qualquer View. Em vários projetos que atendi era bem comum o cliente querer colocar o logo do seu aplicativo na barra de navegação. Em alguns casos até escondia a barra de navegação e criava uma própria a fim de conseguir personalizar ela do jeito que o cliente desejava.

Felizmente com esse novo recurso, modificar a apresentação da barra de navegação é tão simples quanto desenhar qualquer layout no XAML da página:

```xml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="NavigationPageTitleView.TitleViewPage">
    <NavigationPage.TitleView>
        <Image Source="caeno_logo" />
    </NavigationPage.TitleView>
    ...
</ContentPage>
```

No exemplo acima eu substituo o título textual padrão pelo logo da minha antiga empresa. O resultado é o seguinte:



O mesmo resultado pode ser facilmente atingido via código, o que possibilita a criação de algumas rotinas para facilitar a inclusão da barra personalizada em mais de uma página:

```csharp

```


# Referencias
* [Displaying Views in the Navigation Bar](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/app-fundamentals/navigation/hierarchical#displaying-views-in-the-navigation-bar)