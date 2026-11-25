# Engineering Mastery
> [!important] Missão
> Recolocação profissional, autonomia técnica e construção de sistemas complexos em 90 dias.

## Retomar formação
![[CURRENT_STATE]]

## Indicadores de estudo
> [!note] Dados reais
> Sem registros, as consultas podem mostrar nenhuma linha. Isso significa ausência de dados, não avaliação de domínio. Metas: 100 problemas, 12 casos de System Design e 12 simulados.

### Tempo acumulado e dias registrados
```dataview
TABLE WITHOUT ID round(sum(rows.minutes)/60, 2) AS "Horas", length(unique(rows.formation_day)) AS "Dias registrados (meta: 90)", length(rows) AS "Sessões"
FROM "06 - Tracking/Daily Logs"
WHERE type = "session" AND date AND minutes != null AND formation_day != null
GROUP BY true
```

### Últimos sete dias (incluindo hoje)
```dataview
TABLE WITHOUT ID key AS "Data", round(sum(rows.minutes)/60, 2) AS "Horas"
FROM "06 - Tracking/Daily Logs"
WHERE type = "session" AND date >= date(today) - dur(6 days) AND date <= date(today) AND minutes != null
GROUP BY date
SORT key DESC
```

### Tempo por disciplina
```dataview
TABLE WITHOUT ID key AS "Área", round(sum(rows.minutes)/60, 2) AS "Horas"
FROM "06 - Tracking/Daily Logs"
WHERE type = "session" AND date AND area AND minutes != null
GROUP BY area
SORT sum(rows.minutes) DESC
```

### Prática concluída (itens únicos)
```dataview
TABLE WITHOUT ID length(unique(flat(rows.leetcode_solved))) AS "LeetCode / 100", length(unique(flat(rows.system_design_completed))) AS "System Design / 12", length(unique(flat(rows.mock_completed))) AS "Simulados / 12"
FROM "06 - Tracking/Daily Logs"
WHERE type = "session" AND date
GROUP BY true
```

### Sessões recentes
```dataview
TABLE date AS "Data", area AS "Área", minutes AS "Minutos"
FROM "06 - Tracking/Daily Logs"
WHERE type = "session" AND date
SORT date DESC, file.name DESC
LIMIT 10
```

## Domínio e retenção
- [[Assessments|Avaliações com evidência e níveis 0–5]]
- [[Knowledge Gaps|Lacunas técnicas]]
- [[Spaced Repetition|Revisões espaçadas]]
- [[METHODOLOGY|Critérios de domínio]]

### Revisões pendentes com prazo
```dataview
TASK
FROM "06 - Tracking/Spaced Repetition"
WHERE !completed AND due AND due <= date(today)
SORT due ASC
```

## Projetos e carreira
- [ ] MVP [[Learning OS]]
- [ ] MVP [[CineGraph]] com recomendação avaliada
- [[Career|Candidaturas e entrevistas]]
- [[LeetCode]] · [[System Design]]

## Central de navegação
- [[Roadmap.canvas|Roadmap visual]]
- [[ROADMAP]] · [[CURRICULUM]] · [[METHODOLOGY]]
- [[CURRENT_STATE]] · [[AGENTS]]
- [[Books]] · [[Courses]]
- [[Template - Session|Modelo de registro de sessão]]
