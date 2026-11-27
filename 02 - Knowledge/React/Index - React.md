# React

## Props

- `children`: conteúdo passado entre as tags de um componente.
- Rest reúne as props restantes; spread repassa propriedades a outro componente.
- Props são somente leitura: não devem ser modificadas pelo componente.

```jsx
function Card({ children, ...rest }) {
  return <section {...rest}>{children}</section>;
}
```

## Recuperação ativa

- Qual a diferença entre rest e spread nesse exemplo?
- Como passar conteúdo JSX para um componente?
- Por que não devemos modificar props?
