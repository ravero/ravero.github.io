---
layout: post
title: "Conectando a um emulador Android a partir de uma VM"
date: 2019-05-09 15:16:00 -0300
categories: android
tags: android emulator parallels vm
---

Um cenário típico para desenvolvedores Xamarin que usam Mac (meu caso), mas gostam do Visual Studio para Windows, é usar um Mac como máquina de desenvolvimento carregando o Windows com Parallels Desktop. Ao testar um aplicativo Android é preferível usar o emulador nativo no macOS ao invés de tentar rodar ele dentro da VM do Windows, o que costuma ser bem problemático.

O setup para isso ficou bastante simples nos últimos tempos:
1. Executar o Emulador do Android no macOS
2. Configurar o netcat (`nc`) para direcionar as conexões de rede para o emulador
3. Usar o `adb` no Windows para se conectar ao emulador

Eu criei alguns scripts para facilitar:

_Script para iniciar o emulador:_

```bash
#!/bin/bash

# Start Android Emulator
cd $ANDROID_HOME/tools
emulator -avd <NomeDoEmulador> &
```

Note o uso da variável `$ANDROID_HOME`, ela foi declarada no `.bash_profile` para ficar disponível nas chamadas de Terminal e do Script. A mudança de pasta é necessária pois se chamar o comando `emulator` em uma pasta diferente dará um erro.

_Script para direcionar os pacotes para o adb:_

```bash
#!/bin/bash

# Open up the Android Emulator to be accessed through network
adb kill-server

# Allow remote connection to the Emulator
cd /tmp
mkfifo backpipe
nc -kl 5555 0<backpipe | nc 127.0.0.1 5555 > backpipe
```

No Windows, deixo no Desktop um batch (connect-emu.bat) para conectar ao emulador da máquina principal:
```bat
"c:\Program Files (x86)\Android\android-sdk\platform-tools\adb.exe" connect localhost.mac:5555
PAUSE
```

>Note o uso do endereço `localhost.mac` para se referenciar a máquina host (rodando o macOS). Minha VM esta configurada para usar _Shared Network_, que cria uma subrede no próprio computador com um DHCP local, e o endereço do host geralmente é o primeiro (10.211.55.2).
>
>Para esse nome se tornar acessível na VM, adicionei a seguinte entrada no arquivo `"C:\Windows\System32\drivers\etc\hosts"`:
>
>```
>10.211.55.2     localhost.mac
>```
>
>Com isso fica bastante simples referenciar o macOS.

Além disso, o artigo que usei como referência lista mais duas formas de fazer isso caso esses passos não funcionem, mas eu fiquei com essa primeira opção por ser a mais simples.

>Algumas pessoas me perguntam porque usar um Mac para emular o Windows. Trata-se de um misto de preferência pessoa com praticidade. Para criar aplicativos iOS no Xamarin é obrigatório passar por um macOS para compilação, então trabalhando em um Mac não preciso me preocupar em ter uma máquina de build.
>
>Mas esse ainda não é meu motivo principal. Pessoalmente eu tenho o macOS como meu sistema operacional "base", onde realizo todas as minhas tarefas computacionais, a parte das ferramentas que uso especificamente para desenvolvimento de apps.

# Referências

* [Is it possible to connect to Android emulators running on a Mac from a Windows VM?](https://docs.microsoft.com/en-us/xamarin/android/troubleshooting/questions/connect-android-emulator-mac-windows)
* [Start the emulator from the command line](https://developer.android.com/studio/run/emulator-commandline)
* [Network modes in Parallels Desktop for Mac](https://kb.parallels.com/4948#section5)
* [Access macOS localhost from IE or Edge within Parallels Desktop](https://gist.github.com/ernsheong/23c00e65219b10db7bc072772ea509d4)