---
layout: post
title: "Criando uma Imagem de Disco Criptografada no macOS"
date: 2019-06-11 15:42:00 -0300
categories: macos dicas
tags: macos dicas
---

Recentemente comecei a fazer uso de imagens de disco criptografadas para guardar arquivos sensíveis dos projetos de meus clientes. Esse é um recurso bem simples de usar, e em conjunto com o [1Password](https://1password.com) vira uma combinação perfeita para guardar e armazenar esse tipo de arquivo.

A criação de uma nova imagem de disco é uma receita de pão:

1. Abra o Utilitário de Disco (Disk Utility), geralmente encontrado na pasta `/Applications/Utilities`. Você também consegue acessá-lo facilmente pelo Finder digitando Command+Espaço.
2. No menu do aplicativo selecione **File > New Image > Blank Image**, a janela de seleção de arquivo será exibida.
3. Preencha as informações da janela:
    * **Save As**: nome do arquivo da imagem (será um arquivo com extensão `.dmg`).
    * **Name**: nome da imagem, geralmente deixo com o mesmo nome do arquivo.
    * **Size**: tamanho máximo que a imagem terá, isso vai depender do que você pretende armazenar nela. Eu geralmente guardo documentos bem pequenos, logo o tamanho sugerido de 100 MB é mais que suficiente.
    * **Format**: deixo como _Mac OS Extended (Journaled)_.
    * **Encryption**: uso a opção `256-bit AES encryption`. Ela é mais segura e mais lenta, mas em Macs modernos isso não deve ser um problema, então vou na opção mais segura.
    * **Partition**: mantenho a opção padrão `Single partition - GUID Partition Map`, para nosso propósito esta adequado.
    * **Image Format**: `read/write disk image`, já que iremos usá-lo como se fosse um pen-drive gravando e lendo arquivos.
4. Ao selecionar a opção de Encryption, será solicitada que seja digitada uma senha para proteger a imagem. Sugiro criar uma senha forte usando o 1Password e armazená-la em seu cofre, assim não correrá o risco de não conseguir acessar seus arquivos posteriormente.
5. Clique no botão `Save` para criar o arquivo, ele será automaticamente "montado" no seu Finder.

Uma imagem de disco do macOS quando aberta aparece como se fosse um drive qualquer. Você copiar arquivos para essa pasta normalmente como se fosse um drive qualquer. Ao desmontar a imagem, clicando na setinha ao lado direito dela, o acesso a imagem será fechado e só será possível abri-lo novamente com a senha determinada durante a criação.