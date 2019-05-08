---
layout: post
title: "NSubstitute - Verificando chamada em método async"
date: 2019-05-08 00:50:00 -0300
categories: unit-test
tags: unit-test fake stub nsub nsubstitute
---

Uma das funcionalidades existentes nos frameworks de substituição como o NSubstitute e o Moq, é a capacidade de verificar se um método de um _fake_ gerado por eles foi chamado. Isso acontece pois eles mantém um registro de todas as chamadas que são feitas áquele objeto. Isso nos possibilita testar se uma parte do nosso código esta chamando um método em uma dependencia.

