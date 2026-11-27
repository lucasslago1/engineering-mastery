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

## Comparações

### Strings

- Comparações relacionais entre strings são lexicográficas, por unidades de código UTF-16, e distinguem maiúsculas de minúsculas.

```javascript
"A" < "a"; // true
```

### Igualdade e coerção

- `a === b` compara sem coerção de tipos.
- `a == b` pode realizar coerção, conforme os tipos envolvidos.
- `null` e `undefined` são iguais entre si com `a == b`, mas não são iguais a zero.
- Em comparações relacionais com números, `null` é convertido em zero.

```javascript
"2" > 1;       // true
"01" == 1;     // true
null == 0;     // false
null >= 0;     // true
undefined == null; // true
```

**Recuperação ativa**
- Por que `null == 0` é false, mas `null >= 0` é true?

**Fonte:** [JavaScript.info — Comparações](https://javascript.info/comparison)

## Operadores lógicos

### OR e AND

- `||`: retorna o primeiro operando truthy ou o último se todos forem falsy.
- `&&`: retorna o primeiro operando falsy ou o último se todos forem truthy.
- Ambos retornam operandos, não necessariamente booleanos.

```javascript
1 && 0;      // 0
1 && 5;      // 5
1 && 2 && 3; // 3
0 || "Ana";  // "Ana"
```

### NOT e precedência

- `!`: converte para booleano e inverte o resultado.
- `!!`: converte para booleano.
- Entre esses operadores, a precedência é: `!`, depois `&&`, depois `||`.

### Curto-circuito

- A avaliação para assim que o resultado pode ser determinado; os operandos restantes não são avaliados.

```javascript
"Maria" || getName(); // não chama getName
0 && getName();       // não chama getName
"" || getName();      // chama getName
```

**Risco:** confundir truthy/falsy com true/false ou presumir que todas as funções de uma expressão serão executadas.

**Recuperação ativa**
- O que `||` retorna quando todos os operandos são falsy?
- Por que `0 && getName()` não executa a função?
- Qual a diferença entre `!` e `!!`?

**Fonte:** [JavaScript.info — Operadores lógicos](https://javascript.info/logical-operators)

## Referências e cópias de objetos

- Uma variável que contém um objeto armazena uma referência a ele. Atribuir essa variável a outra ou passá-la como argumento copia a referência, não o objeto.
- Alterações nas propriedades por referências compartilhadas afetam o mesmo objeto.
- Cópia rasa: spread e `Object.assign` permitem criar um novo objeto, mas preservam as referências dos objetos aninhados.
- Cópia profunda: `structuredClone` clona estruturas compatíveis, incluindo objetos aninhados, mas não suporta funções. Alternativas incluem implementações personalizadas e [Lodash cloneDeep](https://lodash.com/docs#cloneDeep).

```javascript
const original = { address: { city: "Recife" } };
const shallow = { ...original };
const deep = structuredClone(original);

shallow.address === original.address; // true
deep.address === original.address;    // false
```

**Recuperação ativa**
- O que é copiado ao passar um objeto como argumento?
- Por que uma cópia rasa pode permitir mutações no objeto original?
- Quando uma cópia profunda é necessária?

**Fonte:** [JavaScript.info — Referências e cópias de objetos](https://javascript.info/object-copy)
