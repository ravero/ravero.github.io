---
layout: post
title: "Xcode 11 - Enviando um IPA para a App Store"
date: 2019-10-23 13:37:00 -0300
tags: ios xcode
---

Com o Xcode 11 perdemos o utilitário "Application Loader" que vinha embutido em sua instalação e servia para fazer upload dos pacotes de apps para a App Store, e que fazia parte do fluxo de desenvolvimento de Xamarin.iOS já que ao gerarmos um pacote exportavamos o arquivo `.ipa` para upload por esse utilitário. Felizmente foram oferecidas soluções simples para contornar esse problema.

## Upload através do Transporter
A Apple liberou recentemente o app [Transporter na Mac App Store](https://developer.apple.com/news/?id=10152019a), que seria um substituto do Application Loader com uma interface um pouco mais elaborada (e compatível com o macOS Catalina). Se procura um substituto gráfico ele é sua melhor opção.

![Screenshot do Transporter](/assets/images/transporter.png){:class="img-responsive" width="300"}

## Upload através de linha de comando
Agora é possível fazer o upload através de linha de comando. Uso essa opção quando tenho arquivos `.ipa` compilados em algum serviço de Build como o [Visual Studio App Center](appcenter.ms). Tendo o arquivo em mãos basta usar o comando:

```bash
xcrun altool --upload-app --type ios --file "/path/to/app.ipa" --username "[conta-apple]" --password "[senha]"
```

>**Importante**: se seu Apple ID é protegido por 2FA é necessário usar uma [Senha de Aplicativo](https://support.apple.com/en-in/HT204397). Caso não tenha use a senha padrão.

Caso tenha algum problema com esse comando não se esqueça de usar `xcode-select -s /Applications/Xcode.app` para disponibilizar as ferramentas de linha de comando do Xcode (supondo que você o tenha instalado através da App Store, onde esse seria o path padrão).

## Referências
* [Transporter Mac App](https://developer.apple.com/news/?id=10152019a&utm_campaign=Weekly%2BXamarin&utm_medium=email&utm_source=Weekly_Xamarin_229)
* [Xcode 11 and upload IPA file without Application Loader](https://forums.xamarin.com/discussion/170085/xcode-11-and-upload-ipa-file-without-application-loader)
