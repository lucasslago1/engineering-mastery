---
cssclasses:
  - engineering-dashboard
---
# Engineering Mastery
> [!important] Missão
> Recolocação profissional, autonomia técnica e construção de sistemas complexos em 90 dias.

## Painel de acompanhamento

```dataviewjs
const root = dv.el("div", "", {cls:"em-dashboard"});
const add = (parent, tag, value, cls) => {
  const e = document.createElement(tag);
  if (cls) e.className = cls;
  if (value !== null && value !== undefined) e.textContent = String(value);
  parent.appendChild(e); return e;
};
const css = add(root,"style","");
css.textContent = `
.em-dashboard { --em-accent: var(--interactive-accent); }
.em-grid { display:grid; grid-template-columns:repeat(auto-fit,minmax(135px,1fr)); gap:10px; }
.em-card { border:1px solid var(--background-modifier-border); border-radius:12px; padding:14px; background:var(--background-secondary); min-width:0; }
.em-label { color:var(--text-muted); font-size:.82em; }
.em-value { font-size:1.7em; font-weight:700; margin:5px 0; color:var(--text-normal); }
.em-track { height:6px; border-radius:8px; background:var(--background-modifier-border); overflow:hidden; margin-top:8px; }
.em-fill { height:100%; background:var(--em-accent); border-radius:8px; }
.em-chart { display:grid; grid-template-columns:repeat(7,minmax(0,1fr)); gap:8px; align-items:end; }
.em-bar { height:100px; display:flex; align-items:end; background:var(--background-modifier-border); border-radius:6px; overflow:hidden; }
.em-bar > div { width:100%; background:var(--em-accent); border-radius:5px; }
.em-day { text-align:center; font-size:.75em; color:var(--text-muted); }
.em-heat { display:grid; grid-template-rows:repeat(7,14px); grid-auto-flow:column; grid-auto-columns:14px; gap:4px; overflow-x:auto; padding:5px 0; }
.em-cell { border-radius:3px; background:var(--background-modifier-border); }
.em-section { margin:18px 0 8px; font-weight:650; font-size:1.1em; }
.em-row { display:flex; justify-content:space-between; gap:12px; padding:8px 0; border-bottom:1px solid var(--background-modifier-border); }
`;
const today = dv.date("today").startOf("day");
const sessions = dv.pages('"06 - Tracking/Daily Logs"').array().filter(p => p.type === "session" && p.date && p.file.name !== "Template - Session");
const valid = sessions.filter(p => typeof p.minutes === "number" && Number.isFinite(p.minutes) && p.minutes >= 0);
const sum = a => a.reduce((s,p)=>s+p.minutes,0);
const hours = n => (n/60).toLocaleString("pt-BR",{maximumFractionDigits:1})+" h";
const ids = k => new Set(sessions.flatMap(p=>p[k] ? Array.from(dv.array(p[k])) : []).filter(x=>typeof x==="string" || typeof x==="number")).size;
const days = new Set(sessions.map(p=>p.formation_day).filter(n=>Number.isInteger(n)&&n>=1&&n<=90)).size;
const byDate = new Map();
for (const p of valid) { const d=dv.date(p.date); if(d && d.isValid) {const k=d.toISODate(); byDate.set(k,(byDate.get(k)||0)+p.minutes);} }
const week = Array.from({length:7},(_,i)=>today.minus({days:6-i}));
const weekMinutes=week.reduce((s,d)=>s+(byDate.get(d.toISODate())||0),0);
const reviews=dv.page("06 - Tracking/Spaced Repetition")?.file.tasks ?? [];
const pending=Array.from(reviews).filter(t=>!t.completed && t.due && dv.date(t.due).toMillis()<=today.endOf("day").toMillis());
const grid=add(root,"div",null,"em-grid");
function card(label,value,n,max) {
 const c=add(grid,"div",null,"em-card"); add(c,"div",label,"em-label"); add(c,"div",value,"em-value");
 if(max){const track=add(c,"div",null,"em-track"); const fill=add(track,"div",null,"em-fill"); fill.style.width=Math.min(100,100*n/max)+"%";}
}
card("Horas acumuladas",hours(sum(valid)));
card("Últimos 7 dias",hours(weekMinutes));
card("Dias registrados",days+" / 90",days,90);
card("LeetCode",ids("leetcode_solved")+" / 100",ids("leetcode_solved"),100);
card("System Design",ids("system_design_completed")+" / 12",ids("system_design_completed"),12);
card("Simulados",ids("mock_completed")+" / 12",ids("mock_completed"),12);
card("Revisões até hoje",pending.length);
card("Sessões registradas",sessions.length);
add(root,"div","Atividade · últimos 7 dias","em-section");
const chart=add(root,"div",null,"em-chart");
const max=Math.max(480,...week.map(d=>byDate.get(d.toISODate())||0));
for(const d of week){const n=byDate.get(d.toISODate())||0;const col=add(chart,"div",null,"em-day");add(col,"div",hours(n));const bar=add(col,"div",null,"em-bar");const fill=add(bar,"div");fill.style.height=100*n/max+"%";add(col,"div",d.setLocale("pt-BR").toFormat("ccc dd"));}
add(root,"div","Consistência · últimos 84 dias","em-section");
const heat=add(root,"div",null,"em-heat");
for(let i=83;i>=0;i--){const d=today.minus({days:i});const n=byDate.get(d.toISODate())||0;const cell=add(heat,"div",null,"em-cell");cell.title=d.toFormat("dd/MM/yyyy")+" — "+hours(n);if(n>0){cell.style.background="var(--em-accent)";cell.style.opacity=String(Math.min(1,.25+.75*n/480));}}
add(root,"div","Tempo por disciplina","em-section");
const areas=new Map();for(const p of valid){const a=String(p.area||"Sem área");areas.set(a,(areas.get(a)||0)+p.minutes);}
if(!areas.size)add(root,"div","Nenhuma sessão registrada ainda.","em-label");
for(const [a,n] of [...areas].sort((a,b)=>b[1]-a[1])){const r=add(root,"div",null,"em-row");add(r,"span",a);add(r,"strong",hours(n));}
add(root,"div","Domínio por disciplina","em-section");
const assessments=dv.pages('"06 - Tracking"').array().filter(p=>p.type==="assessment"&&p.date&&p.area&&p.evidence&&Number.isInteger(p.level)&&p.level>=0&&p.level<=5);
const latest=new Map();
for(const p of assessments){const k=String(p.area)+" / "+String(p.concept||p.file.name);const prev=latest.get(k);if(!prev||dv.date(p.date).toMillis()>dv.date(prev.date).toMillis())latest.set(k,p);}
if(!latest.size)add(root,"div","Sem avaliações estruturadas. Domínio ainda não medido.","em-label");
for(const [k,p] of latest){const r=add(root,"div",null,"em-row");add(r,"span",k);add(r,"strong",p.level+" / 5");}
add(root,"div","Revisões pendentes","em-section");
if(!pending.length)add(root,"div","Nenhuma revisão com prazo até hoje.","em-label");
else dv.taskList(pending,false);
```

> [!note] Critérios
> Dias registrados não equivalem a dias concluídos. Horas são minutos efetivos confirmados. Domínio exige avaliação com evidência. A meta diária de 8h é referência, não obrigação de compensação.

## Retomar formação
![[CURRENT_STATE]]

## Projetos e carreira
- [ ] MVP [[Learning OS]]
- [ ] MVP [[CineGraph]] com recomendação avaliada
- [[Career|Candidaturas e entrevistas]]

## Sessões recentes
```dataview
TABLE date AS "Data", area AS "Área", minutes AS "Minutos"
FROM "06 - Tracking/Daily Logs"
WHERE type = "session" AND date
SORT date DESC, file.name DESC
LIMIT 10
```

## Central de navegação
- [[Roadmap.canvas|Roadmap visual]] · [[ROADMAP]] · [[CURRICULUM]] · [[METHODOLOGY]]
- [[CURRENT_STATE]] · [[AGENTS]]
- [[Assessments]] · [[Knowledge Gaps]] · [[Spaced Repetition]]
- [[Books]] · [[Courses]]
- [[LeetCode]] · [[System Design]]
- [[Template - Session|Modelo de sessão]]
