---
layout: page
title: Ambiente
permalink: /dev-env
---

Eu descobri a utilidade de manter uma documentação dos passos que eu sigo sempre que eu configuro um novo computador para trabalho. Como tenho pelo menos duas estações de trabalho (a principal e a reserva), e de tempos em tempos me da a louca de formata-los quando acho que o sistema ficou muito bagunçado, a criação de um roteiro com tudo que eu preciso para deixar a máquina pronta para qualquer situação acelera muito as coisas, já que fazendo tudo de cabeça sempre sentia falta de alguma coisa no dia-a-dia.

Eu considero a preparação do ambiente como a manutenção da caixa de ferramentas. Um cozinheiro é sempre eficiente quando suas ferramentas de trabalho estão sempre afiadas e ao seu fácil alcance. O trabalho como desenvolvedor só se torna realmente produtivo quando estabelecemos um ambiente otimizado para nossas atividades diárias.

De tempos em tempos gosto de revisar esse roteiro, tanto para acrescentar descobertas como para rever ferramentas que talvez tenha esquecido. São tantos os recursos a nosso dispor que não é raro esquecermos que já temos facilitadores de uma tarefa.

## Preparação do Ambiente macOS
A preparação do ambiente macOS segue os passos abaixo:

### 1. Formatar o computador e Instalar o Sistema Operacional
Para formatar o computador é necessário criar um disco de instalação. Primeiro é preciso baixar o macOS na App Store, depois inserir um pen-drive com pelo menos 8GB de espaço (que será limpado nesse processo). Basta executar o comando abaixo:

```bash
sudo /Applications/Install\ macOS\ Mojave.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume
```

**Referência**: [How to create a bootable installer for macOS](https://support.apple.com/en-us/HT201372)

### 2. Instalar os aplicativos da App Store
Com o sistema operacional recém instalado a primeira coisa que faço é instalar os aplicativos da app store. Sempre começo pelo _Amphetamine_, para deixar o computador ativo durante o download e instalação dos componentes que as vezes é demorado. Na sequência baixo o _Xcode_, esse mamute da Apple com seus mais de 6.5GB de download e um tempo incompreensível de instalação. Os demais podem vir sem ordem específica.

* Amphetamine
* [Xcode](https://itunes.apple.com/br/app/xcode/id497799835?l=en&mt=12)
* Microsoft Office ([Word](https://itunes.apple.com/br/app/microsoft-word/id462054704?l=en&mt=12), [Excel](https://itunes.apple.com/br/app/microsoft-excel/id462058435?l=en&mt=12), [PowerPoint](https://itunes.apple.com/br/app/microsoft-powerpoint/id462062816?l=en&mt=12), [Outlook](https://itunes.apple.com/br/app/microsoft-outlook/id985367838?l=en&mt=12), [OneNote](https://itunes.apple.com/br/app/microsoft-onenote/id784801555?l=en&mt=12))
* [OneDrive](https://itunes.apple.com/br/app/onedrive/id823766827?l=en&mt=12)
* iWork Suite (Pages, Numbers, Keynote)
* Yoink
* Pocket
* Kindle
* PixelMator
* TweetBot 3
* MacTracker
* DaisyDisk
* Asset Catalog Creator
* Display Menu
* Evernote
* Disconnect Premium
* Scrivener
* Telegram
* Cocoa JSON Editor
* Helium

### 3. Instalar o SetApp


### 4. Instalar os aplicativos de outras fontes
Lista dos outros softwares que baixo diretamente de seus fabricantes, que não estão disponíveis na loja ou no Setapp, ou que adquiri diretamente.

* [1Password](https://1password.com/downloads/mac/): meu gerenciador de senhas, a primeira ferramenta que instalo.
* [Alfred](https://www.alfredapp.com): esse é o que o Spotlight deveria ser, e substitui ele devidamente.
* [Dropbox](https://www.dropbox.com/downloading): Apenas para manter as configurações do Alfredo sincronizadas. As vezes também uso par acompartilhar alguma coisa ou acessar aquivos de algum projeto.
* [Visual Studio for Mac](https://visualstudio.microsoft.com/downloads/): minha principal ferramenta de desenvolvimento.
* [Visual Studio Code](https://code.visualstudio.com/download): fora dos projetos específicos para o Visual Studio, o Code é meu editor padrão para arquivos texto.
* [GitKraken](https://www.gitkraken.com/download): meu cliente Git favorito. Acabo centralizando todos os meus projetos na ferramenta depois que adquiri a versão pro.
* [Azure Data Studio](https://docs.microsoft.com/en-us/sql/azure-data-studio/download): cliente multiplataforma de SQL Server da Microsoft. Acabo usando mais o SQLPro Studio, mas deixo essa ferramenta como um backup.
* [Azure Storage Explorer](https://azure.microsoft.com/en-us/features/storage-explorer/): cliente multiplataforma do Azure Storage. Utilizo em alguns projetos.
* [Postman](https://www.getpostman.com/downloads/): costumava ser minha principal ferramenta para manipular API's. Hoje esta um pouco de lado, já que outros recursos como Swagger tornou essa interação mais fácil. Mas ainda tenho alguns projetos na nuvem deles.
* [Gorilla Player](https://github.com/UXDivers/Gorilla-Player-Support/releases/download/v1.5.0.0/Gorilla.Player-1.5.0.dmg): 
* [Charles](https://www.charlesproxy.com/download/): Ferramenta de Debug de HTTP multiplataforma. Indispensável para desenvolvimento web e mobile.
* [Reflection 3](https://www.airsquirrels.com/reflector/try): Geralmente uso esse utilitário para espelhar a tela do celular no meu computador durante uma aula ou demonstração de algum app.
* [Parallels Desktop](https://www.parallels.com/products/desktop/download/): uso para virtualizar o Windows (desenvolver com Visual Studio ou fazer alguma coisa específica de Windows) e o Linux (desenvolver para Android). Hoje é a melhor ferramenta de virtualização para Mac, mas esta ficando muito cara.
* [Docker](https://hub.docker.com/editions/community/docker-ce-desktop-mac): uso o community edition para baixar imagens do SQL Server ou Postgree para desenvolvimento. Estou com livros para estudar mais.
* [Skype](https://www.skype.com/en/get-skype/): a Microsoft estragou o Skype, é fato, mas os clientes ainda usam para comunicação.
* Spectacle
* Itsycal
* Screenflow
* iMazing
* Node.js
* Python
* Firefox
* Google Chrome
* [Musixmatch](http://about.musixmatch.com/desktop-app): porque é gostoso cantar! Esse client Desktop funciona muito bem com o iTunes/Apple Music, apesar de estar em Beta.

### 5. Instalar os plugins do QuickLook
### 6. Instalar e configurar as fontes
### 7. Configurar o Visual Studio
### 8. Configurar o ambiente do Bash/Terminal
### 9. Configurar os papéis de parede
### 10. Configurações e Extensões do Safari