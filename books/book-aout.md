---
layout: page
title: The Art of Unit Testing (2nd Edition)
permalink: /books/aout
exclude: true
---

Resumo do livro _The Art of Unit Testing_ de Roy Osherove, segunda edição.

## Parte 1 - Getting Started

### Capítulo 1 - The Basics of Unit Testing 

### Capítulo 2 - A first unit test

## Parte 2 - Core Techniques

### Capítulo 3 - Using stubs to break dependencies

### Capítulo 4 - Interaction testing using mock objects

### Capítulo 5 - Isolation (mock object) frameworks

### Capítulo 6 - Digging Deeper into Isolation Frameworks

## Parte 3 - Test the code

### Capítulo 7 - Test Hierarquies and Organization

### Capítulo 8 - The Pillars of good tests

## Parte 4 - Design and Process

### Capítulo 9 - Integrate unit testing into organization

### Capítulo 10 - Working with legacy code
Esse capítulo apresenta conceitos importantes sobre a aplicação de testes unitários em código legado. O fato é que o mundo ideal onde qualquer código produzido nasce a partir de um teste unitário, no bom e velho TDD é completamente distante do mundo real onde a maioria dos desenvolvedores estão sempre correndo para entregar novos releases e apagando o incendio dos códigos que não foram produzidos com a qualidade adequada.

Somos humanos e infelizmente ainda somos assim, não conseguimos enxergar o valor das ações de longo prazo, sendo muito imediatistas. Essa responsabilidade não é exclusiva da programador, talvez até ele seja a ponta mais fraca da corda que puxa os profissionais para agendas de entrega cada vez mais insanas (já repararam como no mundo do software vivemos um eterno beta?).

O resultado disso:

O autor apresenta uma metodologia bem interessante para identificar no código legado o que é importante ser testado. Para isso elenca alguns critérios para os quais você da nota e que vão balizar a priorização de onde começar a escrever seus testes:

* Complexidade lógica
* Nível de dependência
* Prioridade

Para cada um desses critérios de uma classificação de 1 (baixa prioridade) a 10 (alta prioridade). Isso pode ser colocado em uma tabela que o autor chama de _"Tabela de Viabilidade"_.

### Capítulo 11 - Design and Testability