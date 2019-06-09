---
layout: post
title: "Dica de Xamarin.Forms — Personalização rápida por plataforma"
date: 2019-06-09 13:41:00 -0300
categories: programação xamarin xamarin.forms dicas
tags: programação xamarin xamarin.forms dicas
---

O Xamarin.Forms permite personalizar os componentes de acordo com a plataforma em que a interface esta sendo renderizada. Isso é feito usando a tag `<OnPlatform x:TypeArguments="[Tipo]">`, onde o atributo `x:TypeArguments` determina o tipo de dado que estamos personalizando.

Por exemplo, é possível determinar o tamanho de um botão de acordo com a plataforma usando a sintaxe:

```xml
<Button Text="OK">  
    <Button.WidthRequest>  
        <OnPlatform x:TypeArguments="x:Double">  
            <On Platform="iOS">200</On>  
            <On Platform="Android">150</On>  
        </OnPlatform>  
    </Button.WidthRequest>  
</Button>
```

Também é possível definir mais de uma plataforma em uma condição, separando os nomes por virgula, como exemplificado abaixo:

```xml
<Button Text="Ok">  
    <Button.WidthRequest>  
        <OnPlatform x:TypeArguments="x:Double">  
            <On Platform="iOS,Android">200</On>  
            <On Platform="UWP">120</On>  
        </OnPlatform>  
    </Button.WidthRequest>  
</Button>
```

>**Nota**: O intellisense do Visual Studio for Mac não reconhece direito essa construção, por isso não estranhe se as opções não aparecem a medida que você digita.

A partir do Xamarin.Forms versão 3.2.0 essa sintaxe foi ainda mais simplificada com a inclusão de uma _markup extension_ para o _OnPlatform_ (e também para o OnIdiom, que não estou tratando nesse artigo). Com isso é possível fazer essa personalização em linha, direto no XAML, assim os primeiros exemplos podem ser simplificados da seguinte forma:

```xml
<Button 
    WidthRequest="{OnPlatform Android=150,iOS=200}"
    Text="OK (Markup Ext)" /> 
```

No code-behind também é possível verificar a plataforma para executar códigos persoanlizados usando um Switch:

```csharp
double width;  
switch (Device.RuntimePlatform) {  
    case Device.iOS:  
    case Device.Android:  
        width = 200;  
        break;  
    case Device.UWP:  
        width = 120;  
        break;  
}
```

Essa sintaxe foi introduzida Xamarin.Forms 2.3.4, com o objetivo de facilitar a entrada das novas plataformas que estão sendo suportadas pelo Forms (macOS, Tizen, tvOS, etc.), já que usamos uma string para descreve-la e não mais uma enumeração. Ela facilita por um lado mas acabamos perdendo duas construções que eram bastante úteis:

* `public static T Device.OnPlatform<T>(T iOS, T Android, T WinPhone);`, que permitia personalizar o retorno de um valor por plataforma facilmente e;
* `public static void Device.OnPlatform(Action iOS = null, Action Android = null, Action WinPhone = null, Action Default = null);` que permitia executar uma ação específica de acordo com a plataforma.

Tomei a liberdade de re-criar essas funções com recursos modernos do C# 7.0. Usando tuplas podemos declarar um método OnPlatform para retornar valores da seguinte forma:

```csharp
static T OnPlatform<T>(T defValue, params (string, T)[] platformValues) {  
    foreach (var pv in platformValues) {  
        if (pv.Item1 == Device.RuntimePlatform)  
            return pv.Item2;  
    }
    return defValue;  
}
```

Esse método recebe um valor padrão que é retornado quando o app esta rodando em uma plataforma não listada, e uma lista de tuplas que representa o nome da plataforma e o valor associado a ela. O uso dela seria semelhante a esse:

```csharp
double width2 = OnPlatform(200.0, (Device.iOS, 200), (Device.Android, 150), (Device.UWP, 120));
```

Mais simples do que um Switch certo? Podemos fazer o mesmo para resgatar o OnPlatform que executa um Action por plataform:

```csharp
static void OnPlatform(params (string, Action)[] platformActions) =>  
    platformActions.ToList().ForEach(pa => {  
        if (pa.Item1 == Device.RuntimePlatform)  
            pa.Item2();  
    });
```

E podemos usar esse método por exemplo para chamar ações específicas para cada plataforma:

```csharp
OnPlatform(
	(Device.iOS, () => CustomiOSAction()), 
	(Device.Android, () => CustomAndroidAction())
);
```

Você pode incluir esses dois métodos em uma classe utilitário para facilitar seu dia-a-dia com o Xamarin.Forms. No código de exemplo inclui isso numa classe chamada `PlatformUtils`.

# Referências
* [Código fonte dos exemplos](https://github.com/ravero/XamSamples/tree/master/OnPlatform)
* [Redesign OnPlatform](https://forums.xamarin.com/discussion/84632/redesign-onplatform)
* [New OnPlatform mechanism](https://github.com/xamarin/Xamarin.Forms/pull/658)
* [OnPlatform/OnIdiom markup extensions](https://github.com/xamarin/Xamarin.Forms/issues/2608)