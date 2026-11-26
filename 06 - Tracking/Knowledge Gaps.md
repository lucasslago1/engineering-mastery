# Lacunas
Hipóteses ainda a avaliar: closures, event loop, mutabilidade, concorrência e React. Níveis abaixo provisórios, não certificação de retenção.

| Conceito | Evidência | Nível | Próxima prática |
|---|---|---|---|
| Escopo de bloco, shadowing, hoisting e TDZ | Diagnóstico: acertos isolados, erros combinados; escopo léxico explicado corretamente | 2 | Problema inédito sem consulta |
| Funções como valores e referências | Erros em typeof e identidade; melhora após feedback | 2 | Recuperação independente |
| Exceções | D+1: distinguiu propriedade inexistente de TypeError, errou referência não declarada | 2 | Prever execução |
| Declarações e escopo na prática | calculateTotal e processOrder corretos por inspeção; segundo sem var | 3 provisório | Implementação inédita |
| Busca binária | D+1: implementação correta independente após rastreamento, 98/100 estático; execução não confirmada | 3 | Reimplementar sem consulta |
| Complexidade temporal | Identificou O(n) e O(log n) com justificativa | 3 | Analisar algoritmo inédito |
| Complexidade espacial | D+1: confusões persistentes, explicação final correta para busca binária | 2 | Comparar memória auxiliar |
| Truthy/falsy e operadores && e \|\| | Confundiu zero com truthy e retorno com concatenação; acertos após orientação | 2 | Prever valor e tipo; transferência inédita |
| Renderização condicional JSX com && | Omitiu condição; após demonstração aplicou comparação e interpolação com erro de tag | 2 | Implementar condição sem consulta, testar zero |
| Aritmética de duração | Corrigiu divisão com Math.floor e resto após feedback | 2 | Conversão inédita |
| JSX, fragments e ternário | Exercícios simples corretos | 3 provisório | Nova implementação |
| Componentes, composição e props | Exercícios 06/07 independentes por relato; avaliação estática 92/100 no 07 | 3 provisório | Componente inédito |
| Imutabilidade de props | Identificou pai responsável; confundiu efeito de reatribuição local com mutação compartilhada | 2 | Explicar primitivos e referências |
| Requisitos funcionais | Classificação 6/6 e transferência para consultas | 4 provisório | Novo domínio |
| RNF e levantamento | Métricas incompletas, boa percepção de custo e elasticidade | 3 | Definir carga, percentil e critérios |
| Invariantes e estados | Confundiu regras operacionais com invariantes; precisou de orientação | 2 | Formular condições distintas e verificáveis |
| Atomicidade e idempotência | Combinou UNIQUE e transação após orientação; reconheceu limite local | 3 provisório | Simular falhas e retries |
| Condição de corrida | Diagnóstico inicial guiado; variação correta independente | 3 provisório | Simular interleaving inédito |

D+1 (26/11): escopo/TDZ e referências permanecem nível 2; índices/valores nível 3 provisório, com erro aritmético inicial corrigido. Tempo nível 3, ainda com erro isolado em soma linear.
