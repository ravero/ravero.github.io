---
layout: post
title: "Registrando chamados HTTP no ASP.NET Core"
date: 2019-12-09 14:38:00 -0300
tags: asp.net core api
---

Recentemente passei por uma situação onde precisava entender a sequência de chamados que estava acontecendo a uma API feita em ASP.NET Core que já estava publicada. Minha idéia era registrar isso temporariamente na forma de um _trace_ em um banco de dados onde pudesse fazer as analises que fossem necessárias nos dados estruturados dessas chamadas. Sem conhecimento de algum recurso ou componente que me trouxesse isso automaticamente, resolvi criar um componente de Middleware que pudesse capturar os requests e fazer os devidos registros.

A estrutura de middlewares do ASP.NET Core é bastante flexível e extensível, e nos permite executar uma lógica personalizada em qualquer ponto de um request. Com conhecimento disso parti para a escrita da classe `RequestResponseLoggingMiddleware`, dentro da pasta `Middlewares` do projeto em questão. O código resumido da classe:
