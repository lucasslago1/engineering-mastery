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

### Comparação de strings

- O javascript é case sensitive ao comparar strings e segue a tabela unicode. Por exemplo, a maiúcula `A` é menor que a minúscula `a`, pois minúsculas tem um indíce maior na tabela unicode.

### Comparação de diferentes tipos

- Ao comparar valores de diferentes tipos o javascript converte os valores em números.

```javascript
alert('2' > 1); //true, string '2' vira number 2
alert('01' == 1); //true, string '01' vira number 1
```

- O operador de igualdade estrita verifica a igualdade sem conversão de tipo.
- Porque null == 0 é false se deveria converter null para 0? A verificação de igualdade para undefined e null é definida de uma forma que sem quaisquer conversões eles são iguais entre si e não são iguais a mais nada. 

## Operadores lógicos

- `||` retorna o primeiro valor true.
- `&&` retorna o primeiro valor false. Se o primeiro operando for truthy, retorna o segundo operando, quando todos os valores são verdadeiros, retorna o último valor.

```javascript
alert(1 && 0); //0
alert(1 && 5); //5
alert(1 && 2 && 3) //3
```

- A precedência do operador AND é maior que a do operador OR.
- `!!` converte um valor para o tipo booleano.
- `!` converte para booleano e retorna o resultado inverso. Tem a maior precedência entre todos os operadores.