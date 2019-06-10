---
layout: post
title: "Obtendo o Fingerprint de um Keystore do Android"
date: 2019-06-10 12:44:00 -0300
categories: android
tags: android
---

Aplicativos Android usam uma chave para assinar seus APK's afim de identificar os desenvolvedores na hora da publicação. Quem já trabalhou com Android sabe como o gerenciamento dessas chaves pode ser trabalhoso e as vezes é dificil identificar as informações de uma chave em questão bem como quais as chaves usadas em um aplicativo já publicado.

Certificados digitais são identificados através de um hash, uma assinatura individual conhecida como **Fingerprint**, ou _impressão digital_ em tradução livre. No mundo Java/Android, esses certificados digitais vivem dentro dos _Keystores_, arquivos criptogrados e protegidos por senha que podem conter uma ou mais entradas e geralmente tem a extensão `.jks` ou `.keystore`.

Para extrair essas _impressões digitais_ há um utilitário de linha de comando instalado por padrão junto com o Android Studio chamado `keytool`. O comando é o seguinte:

```bash
keytool -list -v -keystore [arquivo.keystore|jks]
```

O comando irá solicitar a senha do Keystore e irá listar as informações de todos os certificados contidos nesse arquivo. Na minha experiência, dificilmente mais de um certificado é hospedado em um arquivo, mas caso deseje ser mais específico você também pode especificar de qual certificado deseja saber a respeito através de seu alias com o seguinte comando:

```bash
keytool -list -v -keystore [arquivo.keystore|jks] -alias [nome-do-alias]
```

## Verificando a assinatura das chaves de debug
Durante o desenvolvimento de um app é comum usar as chaves de debug que são geradas automaticamente pelo Android Studio ou pelo Visual Studio durante sua instalação. Ambos ambientes assinam os pacotes com essa chave temporária quando você executa o app em debug. As vezes é útil obter essas chaves para configurar o uso de serviços como o Google Maps SDK durante o desenvolvimento do app.

O comando é o mesmo, o que muda é o local onde esse arquivo é gerado. No Android Studio para Windows:

```bash
C:\Users\USERNAME\.android\debug.keystore
```

No Android Studio para macOS:

```bash
~/.android/debug.keystore
```

No Visual Studio para Windows:

```bash
C:\Users\USERNAME\AppData\Local\Xamarin\Mono for Android\debug.keystore
```

No Visual Studio para Mac esse arquivo fica em:

```bash
~/.local/share/Xamarin/Mono for Android/debug.keystore
```


## Verificando a assinatura de um APK
Supondo que você precise identificar com qual certificado um APK publicado foi assinado anteriormente, baixe um pacote de qualquer versão desse app (todos devem ser assinado sempre com o mesmo certificado), descompate e localize o arquivo `.RSA` na pasta `META-INF`, então execute o comando a abaixo:

```bash
keytool -printcert -file [ANDROID_].RSA
```

# Referências

* [SHA-1 fingerprint of keystore certificate](https://stackoverflow.com/questions/15727912/sha-1-fingerprint-of-keystore-certificate)
* [How do I find out which keystore was used to sign an app?](https://stackoverflow.com/questions/11331469/how-do-i-find-out-which-keystore-was-used-to-sign-an-app)
* [Where is debug.keystore in Android Studio](https://stackoverflow.com/questions/16965058/where-is-debug-keystore-in-android-studio/39330177)
* [Finding your Keystore's Signature](https://docs.microsoft.com/en-us/xamarin/android/deploy-test/signing/keystore-signature?tabs=macos)