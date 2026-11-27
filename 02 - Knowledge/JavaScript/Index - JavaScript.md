# JavaScript

## Escopo e variáveis

- Escopo léxico: funções acessam variáveis dos escopos externos; o inverso não ocorre.
- `var`: escopo de função; não respeita blocos comuns.
- `let` e `const`: escopo de bloco.
- `const` impede reatribuição, não mutação de objetos.
- Atribuir a um identificador não declarado pode criar uma global em modo não estrito; em modo estrito gera ReferenceError.

## Hoisting

- Declarações de função podem ser chamadas antes da declaração.
- `var` é inicializada com undefined; `let` e `const` ficam na TDZ até a inicialização.

## Recuperação ativa

- Por que const não torna um objeto imutável?
- O que acontece ao acessar let antes da inicialização?
- Qual a diferença entre escopo de função e de bloco?

## Coversões de tipo

- undefined é NaN em conversão numérica e não 0.
- Qualquer string é considerada verdadeira como um valor booleano, exceto uma string vazia.
- Diferença de truthy e falsy para true e false?

