---
layout: post
title: "Ferramentas para Testes de API's e Webhooks"
date: 2019-11-08 9:52:00 -0300
tags: api
---

Recentemente descobri algumas ferramentas bem úteis para o desenvolvimento de API's, em especial quando é necessário responder a chamados externos ou de webhooks.

## Capturando e recebendo chamadas externas com o ngrok
O [ngrok](https://ngrok.com) é um utilitário que cria um tunel com sua máquina local e um endpoint público. Isso permite que você direcione chamadas de um URL pública para um servidor HTTP local em sua máquina.

A ferramenta não poderia ser mais crua! Um executável de linha de comando. É necessário criar uma conta no serviço para poder usá-lo, após isso é possível fazer sua configuração:

```bash
./ngrok authtoken [token-da-conta]
```

Esse token pode ser obtido no [Dashboard da sua conta](https://dashboard.ngrok.com/get-started), item 3 (Connect your account). Para direcionar um fluxo para seu servidor local basta usar o comando:

```bash
./ngrok http 80
```

Isso irá criar um endpoint e direcionar o fluxo para a porta 80 local. Seu terminal ficará travado durante a execução da ferramenta e você poderá acompanhar um resumo dos chamados.

![](/assets/images/ngrok-summary.png)

Caso direcionar para uma outra porta ou se estiver um https local use:

```bash
./ngrok http https://localhost:5001
```

Todas as chamadas capturadas podem ser monitoradas pelo seu browser no endereço http://127.0.0.1:4040/. Por essa interface você consegue verificar todos os detalhes do Request/Response, incluindo headers, body, códigos de erro, etc.

A versão gratuita permite apenas uma conexão aberta e cria uma URL randomizada cada vez que você o inicia, o que as vezes pode ser incoveniente, mas é suficiente para fluxos básicos de desenvolvimento. Existem planos pagos onde é possível reservar uma URL ou subir mais de um endpoint ao mesmo tempo.

Há diversos casos de uso para o ngrok, desde testes de API's, chamadas de Webhooks, até publicar versões temporárias de testes ou apresentações para clientes, sendo uma ferramenta fundamental para desenvolvedores web.

## Simulando um API com o Beeceptor
Já o [Beeceptor](https://beeceptor.com) é uma ferramenta totalmente online e serve para criarmos um servidor "mockado", onde podemos regras que geram respostas padrões para determinados chamados naquele endpoint. O que mais me agrada no Beeceptor é sua facilidade de uso, não sendo necessário criação de conta para prototipar rapidamente um API.

![](/assets/images/beeceptor.png)

Todas as chamadas são capturadas e é possível verificar todos os detalhes do Request, o que pode ajudar a entender a montagem de algumas integrações.

Outra ótima função do Beeceptor é capacidade de atuar como um Proxy. Com isso você pode configurar um endereço para onde as chamadas serão redirecionadas, e também criar regras para alguns endpoints específicos.


