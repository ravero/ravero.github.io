---
layout: post
title: "Xamarin.Forms - Barra de Navegação Personalizada"
date: 2019-05-23 20:31:00 -0300
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

![](/assets/images/xaml-headers/ios-titleview.png){:class="img-responsive" width="300"}
![](/assets/images/xaml-headers/android-titleview.png){:class="img-responsive" width="300"}

O mesmo resultado pode ser facilmente atingido via código, o que possibilita a criação de algumas rotinas para facilitar a inclusão da barra personalizada em mais de uma página:

```csharp
var titleView = new Image { Source = ImageSource.FromFile("caeno_logo") };
NavigationPage.SetTitleView(this, titleView);
```

Use esse código no construtor da página, logo após o `InitializeComponents()`.

## Limitações
Embora seja um recurso prático e fácil de usar, ele deve ser configurado para cada página que fizer parte da stack de navegação do `NavigationPage`, não é uma forma global de atribuir essa view. Nesse caso pode ser interessante criar uma página base e no construtor dela criar essa view personalizada de navegação.

Outro problema que encontrei foi com a centralização de elementos no Android quando se esta em uma subpágina e há o botão voltar. Nesse caso o logo será centralizado de acordo com o restante do espaço disponível na barra, deslocando assim o ícone da posição original quando estava na página anterior e causando uma sensação estranha na navegação. Veja o exemplo abaixo:

![](/assets/images/xaml-headers/header-offset1.png){:class="img-responsive" width="300"}
![](/assets/images/xaml-headers/header-offset2.png){:class="img-responsive" width="300"}


Não há um jeito muito simples de calcular esse offset, então é bom ter isso em mente quando for desenhar uma estrutura de navegação dessas para incluir componentes nessa barra de navegação apenas quando for acrescentar algo a funcionalidade daquela tela.

# Referencias
* [Código fonte do app usado nos exemplos](https://github.com/ravero/XamSamples/tree/master/TitleViewTest)
* [Displaying Views in the Navigation Bar](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/app-fundamentals/navigation/hierarchical#displaying-views-in-the-navigation-bar)