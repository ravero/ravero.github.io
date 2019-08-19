---
layout: post
title: "Dica de Xamarin.Forms - Quebra de Linha no XAML"
date: 2019-08-09 12:33:00 -0300
tags: xamarin xamarin.forms
---

Um cenário comum no Xamarin.Forms é precisar inserir uma quebra de linha em um `Label` dentro do XAML. Isso pode ser conseguido facilmente usando o código de escape: **`&#x0a;`** como no exemplo abaixo:

```xml
<Label Text="Primeira linha&#x0a;Segunda Linha." />
```

## Referências

* [How to add line breaks in a label in Xamarin Forms using XAML](https://forums.xamarin.com/discussion/24179/how-to-add-line-breaks-in-a-label-in-xamarin-forms-using-xaml)