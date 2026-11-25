# JavaScript

Variáveis

- Hoisting
- Escopo
	- Escopo de função: Variáveis declaradas dentro de funções não são acessadas fora das mesmas.
	- Declarar variáveis sem let, const ou var fará uma variável global, isso é um erro. O 'use strict' resolve isso.
	- Variáveis declaradas no escopo pai da função, conseguem ser acessadas pelas funções.
	- Escopo de bloco: ocorre dentro das chaves. var vaza o bloco, let e const não.
	- Const mantém o escopo no bloco, impede redeclaração e impede a modificação do valor da variável.