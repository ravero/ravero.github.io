---
layout: post
title: "Xcode 11 - Enviando um IPA para a App Store"
date: 2019-10-07 08:51:00 -0300
tags: ios xcode
---

Com o Xcode 11 perdemos o utilitário "Application Loader" que vinha embutido em sua instalação e servia para fazer upload dos pacotes de apps para a App Store, e que fazia parte do fluxo de desenvolvimento de Xamarin.iOS já que ao gerarmos um pacote exportavamos o arquivo `.ipa` para upload por esse utilitário. Felizmente foram oferecidas soluções simples para contornar esse problema.

## Upload através de linha de comando
Também é possível fazer o upload através de linha de comando. Uso essa opção quando tenho arquivos `.ipa` compilados em algum serviço de Build como o [Visual Studio App Center](appcenter.ms). Tendo o arquivo em mãos basta usar o comando:

```bash
xcrun altool --upload-app --type ios --file "/path/to/app.ipa" --username "[conta-apple]" --password "[senha]"
```

>**Importante**: se seu Apple ID é protegido por 2FA é necessário usar uma [Senha de Aplicativo](https://support.apple.com/en-in/HT204397). Caso não tenha use a senha padrão.

Caso tenha algum problema com esse comando não se esqueça de usar `xcode-select -s /Applications/Xcode.app` para disponibilizar as ferramentas de linha de comando do Xcode (supondo que você o tenha instalado através da App Store, onde esse seria o path padrão).

## Upload através do próprio Xcode


## Referências
* [Xcode 11 and upload IPA file without Application Loader](https://forums.xamarin.com/discussion/170085/xcode-11-and-upload-ipa-file-without-application-loader)
