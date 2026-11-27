# JavaScript

## Escopo e variáveis

- Escopo léxico: funções acessam variáveis dos escopos externos; o inverso não ocorre.
- `var`: escopo de função; não respeita blocos comuns.
- `let` e `const`: escopo de bloco.
- `const` impede reatribuição, não mutação de objetos.
- Atribuir a um identificador não declarado pode criar uma global em modo não estrito; em modo estrito gera `ReferenceError`.

**Recuperação ativa**
- Por que `const` não torna um objeto imutável?
- Qual a diferença entre escopo de função e de bloco?

## Hoisting

- Declarações de função podem ser chamadas antes da declaração.
- `var` é inicializada com `undefined`; `let` e `const` ficam na TDZ até a inicialização.

**Recuperação ativa**
- O que acontece ao acessar `let` antes da inicialização?

## Conversões de tipo

### Conversão numérica

- `undefined` é convertido em `NaN`, enquanto `null` é convertido em `0`.

```javascript
Number(undefined); // NaN
Number(null);      // 0
```

**Atenção:** igualdade e conversão numérica não são a mesma coisa.

```javascript
undefined == null;  // true
undefined === null; // false
```

### Conversão booleana

- Toda string não vazia é truthy.
- `true` e `false` são valores booleanos; truthy e falsy classificam o comportamento de valores em contextos booleanos.
- Um valor truthy não precisa ser do tipo booleano.

```javascript
Boolean("false"); // true
Boolean("");      // false
```

**Recuperação ativa**
- Qual a diferença entre converter `null` e `undefined` em número?
- Por que `undefined == null` retorna true?
- Qual a diferença entre truthy e true?
- Por que a string "false" é truthy?

**Fonte:** [JavaScript.info — Conversões de tipo](https://javascript.info/type-conversions)
