# Lacunas
Hipóteses ainda a avaliar: closures, event loop, mutabilidade, concorrência e React. Níveis abaixo provisórios, não certificação de retenção.

| Conceito | Evidência | Nível | Próxima prática |
|---|---|---|---|
| Escopo de bloco, shadowing, hoisting e TDZ | Diagnóstico: acertos isolados, erros combinados; escopo léxico explicado corretamente | 2 | Problema inédito sem consulta |
| Funções como valores e referências | Erros em typeof e identidade; melhora após feedback | 2 | Recuperação independente |
| Exceções | Confusão ReferenceError/TypeError e interrupção do fluxo | 1 | Prever execução |
| Declarações e escopo na prática | calculateTotal e processOrder corretos por inspeção; segundo sem var | 3 provisório | Implementação inédita |
| Busca binária | Três tentativas; confusão índice/valor; solução guiada e debugger | 2 | Reimplementar sem consulta |
| Complexidade temporal | Identificou O(n) e O(log n) com justificativa | 3 | Analisar algoritmo inédito |
| Complexidade espacial | Confundiu com tempo; feedback O(1) auxiliar | 1 | Comparar memória auxiliar |
| Truthy/falsy e operadores && e \|\| | Confundiu zero com truthy e retorno com concatenação; acertos após orientação | 2 | Prever valor e tipo; transferência inédita |
| Renderização condicional JSX com && | Omitiu condição; após demonstração aplicou comparação e interpolação com erro de tag | 2 | Implementar condição sem consulta, testar zero |
| Aritmética de duração | Corrigiu divisão com Math.floor e resto após feedback | 2 | Conversão inédita |
| JSX, fragments e ternário | Exercícios simples corretos | 3 provisório | Nova implementação |
| Componentes, composição e props | Exercícios 06/07 independentes por relato; avaliação estática 92/100 no 07 | 3 provisório | Componente inédito |
| Imutabilidade de props | Identificou pai responsável; confundiu efeito de reatribuição local com mutação compartilhada | 2 | Explicar primitivos e referências |
