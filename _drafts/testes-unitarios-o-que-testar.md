---
title: "Testes Unitários - O que testar?"
---

Sempre que tentei integrar testes unitários ao meu projeto, a primeira pergunta que surgia era: "o que testar?". Embora isso pareça ser uma pergunta idiota, a verdade é que a sensação que temos quando começamos a escrever testes é de que o teste que esta sendo escrito é tão óbvio que parece irrelevante. Isso sempre me gerou um sentimento de frustração pois sempre via os grandes nomes da engenharia de software defendo a prática do TDD e os testes unitários como uma prática fundamental de qualquer bom programador.

Com um pouco de insistência comecei a enxergar alguns padrões, e o que parecia irrelevante começa a se tornar indispensável!

Primeiro é importante entender que o simples conhecimento de um framework de testes unitários e de suas funções básicas, não vai te trazer nenhum insight sobre o que é relevante ser testado em seu projeto. Isso porque os escritores desses frameworks muitas vezes tentam chamar mais atenção para os recursos da ferramenta do que para o problema que eles se propõem a resolver. Eis nossa primeira lição:

>Não baseie seu aprendizado sobre testes unitários em guias de introdução rápida e documentações dos frameworks de testes unitários

Essa fonte de referência nunca traz exemplos próximos da realidade, pelas seguintes razões:

* Esses frameworks são carregados de funcionalidades que extrapolam as necessidades de um bom teste unitário
* Pra demonstrar todas as capacidades da ferramenta não são aplicadas boas práticas
* Misturam os conceitos de Teste Unitário e Teste de Integração
* Misturam os conceitos de Mocks e Stubs

Uma outra barreira comum no entendimento do que é relevante ser testado é a confusão que se faz entre testes unitários e TDD (Test-Driven Design). Vamos desmistificar esses conceitos:

>Teste Unitário é uma técnica de escrita de testes automáticos no c