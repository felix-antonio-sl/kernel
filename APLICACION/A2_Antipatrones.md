# A2_Antipatrones

**Versión:** 2.2.1 | **Estado:** Definitivo | **Audiencia:** Practitioners, Arquitectos, Security, Product/UX, Data/AI Engineers

---

## §1. TAXONOMÍA ANTIPATRONES

```yaml
Total: 50 antipatrones organizados en 9 categorías

Categorías:
  - Estructurales (AP01-AP06): Org design, teams, roles
  - Procesuales (AP07-AP12): Workflows, coordinación
  - Tecnológicos (AP13-AP18): Arquitectura, infra
  - Decisionales (AP19-AP24): OKRs, roadmaps
  - IA (AP25-AP30): Delegación incorrecta, bias
  - Crisis & Transformation (AP31-AP33): Emergency governance, readiness
  - Seguridad (AP34-AP37): Security by design, response
  - Customer Experience (AP38-AP40): Customer-centricity, value stream
  - Tecnológicos Especializados (AP41-AP50): Tech/Data/AI/Process (v2.2.1)
    - AP41: Premature Microservices (§8)
    - AP42: Frontend-Backend Coupling (§8)
    - AP43: Big Design Up Front (BDUF) (§8)
    - AP44: RPA Universal Hammer (§8)
    - AP45: Data Sin Contrato (§8)
    - AP46: RAG Sin Curation (§8)
    - AP47: Observabilidad Mínima IA (§8)
    - AP48: Automatizar Procesos Rotos (§8)
    - AP49: Dual Write Pattern (§8)
    - AP50: Prompt Injection Undefended (§8)
Severidad: 🔴 Crítico | 🟡 Alto | 🟢 Moderado
```

---

## §2. ANTIPATRONES ESTRUCTURALES (AP01-AP06)

| ID | Nombre | Síntoma | Causa Raíz | Consecuencia | Fix | Severidad |
|---|---|---|---|---|---|---|
| **AP01** | **Matrix sin Governance** | Dual reporting, nadie decide conflictos | Implementar matrix sin ARB/escalation | Paralysis decisional, IN1<40 | Governance explícito: ARB semanal, RACI claro, escalation path | 🔴 |
| **AP02** | **Reorg Perpetuo** | Cambio estructura cada 3-6 meses | No diagnosticar root cause, "reorg como magia" | IN2 colapsa (fatigue), no learning | Diagnosticar antes reorg, pilot 1-2 teams, max 1 reorg/18 meses | 🔴 |
| **AP03** | **Silos Profundos** | Departments no colaboran, handoffs eternos | Especialización sin interfaces, "not my job" | Cycle time >14 días, handoff_ratio >40% | Cross-functional squads, shared OKRs, interfaces claras | 🟡 |
| **AP04** | **Span of Control Extremo** | Manager 25+ reports directos | Growth sin crear management layer | No 1:1s, IN2 cae, development nulo | Target 5-9 reports/manager, split teams, promote leads | 🟡 |
| **AP05** | **Conway Inverse Fallacy** | Cambiar org para forzar arquitectura tech deseada | Malinterpretar Conway (org→tech, no tech→org) | Resistance, fracaso adoption | Alinear org con tech actual, evolucionar ambos coordinadamente | 🟡 |
| **AP06** | **Teams Proyecto** | Teams formados para proyecto, disueltos post-completion | Project thinking vs Asset thinking | Knowledge loss, ramp-up perpetuo | Teams estables long-term, trabajo fluye a través team | 🟡 |

---

## §3. ANTIPATRONES PROCESUALES (AP07-AP12)

| ID | Nombre | Síntoma | Causa Raíz | Consecuencia | Fix | Severidad |
|---|---|---|---|---|---|---|
| **AP07** | **Scrum Zombi** | Ceremonies sin valor, rituales vacíos | Scrum by-the-book sin entender principios | Fatigue meetings, velocity estancada | Retrospectiva: ¿Qué ceremonies aportan valor? Eliminar waste | 🟢 |
| **AP08** | **WIP Sin Límite** | 30+ items "In Progress" simultáneamente | No entender cost context switching | Cycle time >14 días, nada completa | WIP limits explícitos (1.5× team size), finish antes start nuevo | 🟡 |
| **AP09** | **Handoff Hell** | 8+ handoffs en proceso deploy | Silos funcionales + process design malo | Cycle time >21 días, flow efficiency <10% | Value stream map, eliminar handoffs innecesarios, automation | 🔴 |
| **AP10** | **Estimation Theater** | 4 horas estimating 2-week sprint | Precisión falsa, planning poker eterno | Waste tiempo, estimates inaccurate anyway | #NoEstimates O cycle time historical data + Monte Carlo | 🟢 |
| **AP11** | **Meeting Overload** | >30% tiempo en meetings | Falta clarity ownership, over-communication | Productivity <50%, burnout | Audit meetings (¿valor agregado?), async-first, clear DRI | 🟡 |
| **AP12** | **Retro Sin Acción** | Retrospectivas sin implementar action items | No ownership, no follow-up | Learning 0, mismos problemas repiten | Max 3 action items, assign owner, review next retro (mandatorio) | 🟢 |

---

## §4. ANTIPATRONES TECNOLÓGICOS (AP13-AP18)

| ID | Nombre | Síntoma | Causa Raíz | Consecuencia | Fix | Severidad |
|---|---|---|---|---|---|---|
| **AP13** | **Monolito Distribuido** | Microservices pero deployments acoplados | Split tech sin split org (viola Conway) | Peor de ambos mundos: complejidad microservices + rigidez monolito | Inverse Conway: reorg teams primero O consolidar a monolito modular | 🔴 |
| **AP14** | **Tech Debt Perpetuo** | >50% tiempo apagando fuegos | 0% capacity dedicado a health, solo features | Velocity cae 60%, incident rate crece 200% | 20% min capacity health (refactor, tests, automation) | 🔴 |
| **AP15** | **Big Bang Rewrite** | Replace legacy system completo en 1 deploy | "Empezar desde cero es más fácil" (falso) | 80% failures, 24+ meses, budget overrun 3× | Strangler Fig pattern: replacement incremental | 🔴 |
| **AP16** | **Not Invented Here** | Re-implementar lo que existe open source | NIH syndrome, arrogancia | Waste tiempo, calidad inferior, maintenance burden | Use open source maduro, contribute upstream | 🟢 |
| **AP17** | **Resume-Driven Development** | Adoptar tech porque "cool" sin business case | Engineers quieren aprender X, no porque resuelve problema | Tech stack fragmentado, complexity sin ROI | Tech radar: Adopt/Trial/Assess/Hold, business case mandatorio | 🟡 |
| **AP18** | **Deploy = Release** | Deploy a prod = feature visible a todos usuarios | No separar deployment de release | Rollback lento (30+ min), no A/B testing, blast radius 100% | Feature flags: deploy disabled, gradual rollout, instant rollback | 🟡 |

---

## §5. ANTIPATRONES DECISIONALES (AP19-AP24)

| ID | Nombre | Síntoma | Causa Raíz | Consecuencia | Fix | Severidad |
|---|---|---|---|---|---|---|
| **AP19** | **Output Disguised as Outcome** | OKR "Launch 10 features" | No entender diferencia output vs outcome | Delivery sin impacto, vanity metrics | OKRs outcome-based: "Aumentar retention +15%", no "launch X" | 🟡 |
| **AP20** | **HiPPO Decisions** | Highest Paid Person's Opinion gana siempre | Autoridad basada en seniority, no en data | Suboptimal decisions, team disengagement | Data-driven decision making, delegación por expertise | 🟡 |
| **AP21** | **Analysis Paralysis** | Decisiones tardan >4 semanas análisis | Perfectionism, risk-aversion extremo | Velocity decisional <30, competitors avanzan | Type 1 vs Type 2 decisions, bias hacia action reversible | 🟢 |
| **AP22** | **Roadmap Wish List** | Roadmap = todo lo que alguien pidió alguna vez | No priorización real, "todos felices" | Focus 0, delivery 0, nada completa | Ruthless prioritization: RICE, WSJF, top 5 solo | 🔴 |
| **AP23** | **Planning Fallacy** | Estimates 50% del tiempo real consistentemente | Optimism bias, no histórico | Missed deadlines perpetuos, credibility loss | #NoEstimates O historical cycle time + confidence intervals | 🟢 |
| **AP24** | **Sunk Cost Fallacy** | Continuar proyecto fracasado porque "ya invertimos $X" | Emotional attachment, loss aversion | Bueno dinero tras malo, opportunity cost | Kill criteria up-front, review quarterly: continuar/pivot/kill | 🟡 |

---

## §6. ANTIPATRONES IA (AP25-AP30)

| ID | Nombre | Síntoma | Causa Raíz | Consecuencia | Fix | Severidad |
|---|---|---|---|---|---|---|
| **AP25** | **M6 Prematuro** | Implementar M6 sin validar M1-M4 | "Move fast" sin considerar riesgos | Fallos catastróficos, pérdida confianza IA | Siempre progresar M1→M2→M3→M4→M6, validar cada etapa | 🔴 |
| **AP26** | **Automation Bias** | Confiar ciegamente en M6, no validar | "Computer said so" syndrome | Errores sistemáticos no detectados | Monitoring activo + auditoría periódica resultados M6 | 🔴 |
| **AP27** | **No Escalation Path** | M6 sin mecanismo rollback a M4/M2 | Diseño asume "IA nunca falla" | Cuando falla, no escape hatch, incident 4+ hrs | Siempre implementar circuit breaker + escalation humano | 🔴 |
| **AP28** | **Bias Algorítmico Ignorado** | ML discrimina grupos sin detectar | No auditar bias en training data | Violaciones legales (EEOC, GDPR), daño reputacional | Bias detection audits, diverse training data, XAI mandatorio | 🔴 |
| **AP29** | **M1 Perpetuo** | Nunca evolucionar de M1 después años | Risk-aversion extrema, falta skills IA | No capturar valor IA, competitors avanzan | Roadmap progresión modos, upskilling team, quick wins M2 | 🟡 |
| **AP30** | **Mode Mismatch** | Usar M3 cuando necesitas M4 | No entender diferencia modos | Humano saturado requests manuales, scalability limit | Decision tree §12 CORE/04_Delegacion.md: volumen/latencia→modo | 🟡 |

---

## §7. MATRIZ SEVERIDAD × DOMINIO

| Dominio ↓ / Severidad → | 🔴 Crítico | 🟡 Alto | 🟢 Moderado |
|------------------------|-----------|--------|------------|
| **Arquitectura** | AP01, AP02, AP34 | AP03, AP04, AP05 | AP06 |
| **Percepción** | AP39 | AP38 | — |
| **Decisión** | AP22, AP40 | AP19, AP20, AP24 | AP21, AP23 |
| **Operación** | AP09, AP13, AP14, AP15, AP36, AP37 | AP08, AP11, AP17, AP18, AP35 | AP07, AP10, AP12, AP16 |
| **IA** | AP25, AP26, AP27, AP28 | AP29, AP30 | — |
| **Seguridad** | AP34, AP36, AP37 | AP35 | — |
| **Customer Experience** | AP38, AP39, AP40 | — | — |

**Total críticos:** 17 (42.5%)  
**Total altos:** 15 (37.5%)  
**Total moderados:** 8 (20%)

---

## §8. PATRONES QUE MITIGAN ANTIPATRONES

| Antipatrón | Mitigado por Patrón(es) | Efectividad |
|-----------|-------------------------|-------------|
| AP01 (Matrix sin Governance) | P01 (Feature Teams), P11 (Squad-Chapter) | Alta |
| AP02 (Reorg Perpetuo) | P35 (R1-R5 Preparación) | Alta |
| AP03 (Silos) | P01 (Feature Teams), P13 (Dual-Track) | Alta |
| AP08 (WIP Sin Límite) | P15 (WIP Limits Kanban) | Alta |
| AP09 (Handoff Hell) | P14 (Value Stream Mapping), P01 (Feature Teams) | Alta |
| AP13 (Monolito Distribuido) | P06 (Inverse Conway), P25 (DB per Service) | Media |
| AP14 (Tech Debt Perpetuo) | P20 (Retrospectiva Accionable) + 20% rule | Alta |
| AP15 (Big Bang Rewrite) | P21 (Strangler Fig) | Alta |
| AP18 (Deploy=Release) | P23 (Feature Flags) | Alta |
| AP19 (Output as Outcome) + variantes OKR | P29 (OKRs Bottom-Up) + filosofía correcta | Alta |
| AP22 (Roadmap Wish List) | P31 (RICE Scoring), P33 (WSJF) | Media |
| AP23 (Planning Fallacy) | Forecasts probabilísticos (ver D3 §3.1) | Media |
| AP25 (M6 Prematuro) | Progresión M1→M6 disciplinada | Alta |
| AP27 (No Escalation) | Diseño resilience (circuit breakers) | Alta |
| AP34 (Perímetro Confiable) | P_SEC02 (Zero Trust Architecture) | Alta |
| AP35 (Seguridad Manual) | P_SEC03 (Security as Code) | Alta |
| AP36 (Seguridad como Gate Final) | P_SEC04 (Shift-Left Security) | Alta |
| AP37 (Respuesta a Incidentes Lenta) | P_SEC05 (Incident Response Automation) | Alta |
| AP38 (Diseño Inside-Out) | P_CX01 (Flujo Valor Cliente) | Alta |
| AP39 (Fricción Invisible) | P_CX02 (Eventos como Señales CX) | Alta |
| AP40 (Tragedia Comunes CX) | P_CX03 (Touchpoint Ownership Explícita) | Alta |
| AP41 (Premature Microservices) | P54 (Piecemeal Growth) | Alta |
| AP42 (Frontend-Backend Coupling) | API Gateway + BFF Pattern, Contract-first design | Media |
| AP43 (BDUF) | P54 (Piecemeal), P55 (Walking Skeleton), P56 (Continuous Refactoring) | Alta |
| AP44 (RPA Universal Hammer) | API-first architecture review | Media |
| AP45 (Data Sin Contrato) | P57 (Data Product), P62 (Contract-Driven Evolution) | Alta |
| AP46 (RAG Sin Curation) | P58 (RAG Auditable) | Alta |
| AP47 (Observabilidad Mínima IA) | Evaluation harness (E8 §5.5), Observability-first design | Alta |
| AP48 (Automatizar Procesos Rotos) | Process mining (optimize-first principle) | Media |
| AP49 (Dual Write Pattern) | P57 (Data Product single source), CDC/Outbox Pattern | Alta |
| AP50 (Prompt Injection) | Input/output guardrails (E8 §5.3), OWASP Top-10 LLMs | Alta |

**Nota:** Para anti-patrones OKR adicionales (Top-Down Imposition, Linked to Compensation, Estimating OKRs, 100% Expected) ver `D3_Decision.md` §1 Anti-Patrones AP6-AP9. Todos mitigados por P29 + claridad filosófica OKRs.

---

## §9. DETECCIÓN TEMPRANA

### Señales por Categoría

```yaml
Estructurales:
  - IN1 (Velocidad decisional) <40: AP01, AP02 probables
  - Handoff_ratio >40%: AP03 confirmado
  - Avg reports/manager >12: AP04 confirmado

Procesuales:
  - Cycle time >14 días: AP08, AP09 probables
  - Flow efficiency <15%: AP09 confirmado
  - WIP >2× team size: AP08 confirmado

Tecnológicos:
  - Deploy frequency <1/mes: AP14, AP18 probables
  - Tech debt score >50: AP14 crítico
  - Incident rate creciendo >50%/trimestre: AP14, AP15

Decisionales:
  - Time-to-decision >21 días: AP20, AP21
  - % OKRs output-based >60%: AP19
  - Backlog >100 items no priorizados: AP22

IA:
  - Incidents causados por IA >5%: AP25, AP26, AP27
  - Bias detection audit nunca hecho: AP28 riesgo alto
```

---

## §10. COST OF DELAY

**Ver también:** `DOMINIOS/D3_Decision.md` §2.1 para uso de Cost of Delay como herramienta de priorización de portfolio (perspectiva prospectiva vs retrospectiva aquí).

### Disclaimer Validación

```yaml
Nota_Metodológica:
  - Costos derivados de research industry pública (citada)
  - Estimaciones para org 100 engineers como baseline
  - Escala aproximadamente lineal (200 eng ≈ 2× cost)
  - Contexto específico puede variar significativamente
  - Use como order-of-magnitude, no precision absoluta
  
Validación_Status:
  - 11 antipatrones cuantificados (de 35 total, 31%)
  - Research sources citadas donde disponible
  - 24 antipatrones: Impacto significativo pero requiere case-by-case quantification
  - Organizaciones deben calibrar según su contexto específico

Recomendación_Uso:
  - Priorización relativa (AP14 > AP07 en costo típico)
  - No usar para ROI preciso sin validación local
  - Complementar con diagnóstico específico (A3)
```

---

### Impacto Financiero Estimado

| Antipatrón | Cost of Delay ($/mes por 100 eng) | Fuente/Rationale | Severidad |
|-----------|-----------------------------------|------------------|-----------|
| **AP02 (Reorg Perpetuo)** | $200K (IN2 churn 15%, productivity -30%) | Google re:Work study | 🔴 |
| **AP03 (Silos Profundos)** | $180K (handoff overhead, cycle time 2×) | Lean Enterprise research | 🟡 |
| **AP08 (WIP Sin Límite)** | $120K (context switching, cycle time +80%) | Personal Kanban studies | 🟡 |
| **AP09 (Handoff Hell)** | $150K (cycle time 3×, flow efficiency <15%) | State of DevOps Report | 🔴 |
| **AP13 (Monolito Distribuido)** | $180K (complexity without modularity benefits) | ThoughtWorks Technology Radar | 🔴 |
| **AP14 (Tech Debt Perpetuo)** | $250K (velocity -60%, incidents +200%) | Stripe Developer Coefficient | 🔴 |
| **AP15 (Big Bang Rewrite)** | $500K (opportunity cost 18+ meses no delivery) | Gartner research | 🔴 |
| **AP20 (HiPPO Decisions)** | $100K (suboptimal decisions, team disengagement) | McKinsey decision quality | 🟡 |
| **AP22 (Roadmap Wish List)** | $140K (no focus, nada completa, thrashing) | Pragmatic Marketing research | 🔴 |
| **AP25 (M6 Prematuro)** | $100K-$1M (incident severity dependent) | Industry case studies IA failures | 🔴 |
| **AP26 (Automation Bias)** | $80K-$500K (systematic errors undetected) | Algorithm bias research (O'Neil) | 🔴 |

**Total potencial críticos:** $2.18M/mes para org 100 eng si 6+ antipatrones críticos presentes simultáneamente.

**Nota importante**: Los costos son **acumulativos y no lineales**. Múltiples antipatrones interactúan:

- AP14 (Tech Debt) + AP09 (Handoffs) = 1.5× cost individual (compounding effect)
- AP02 (Reorg) + AP33 (Transform During Crisis) = 2× cost (dual disruption)

**Antipatrones sin cuantificar**: 24 de 35 (69%) tienen impacto significativo pero requieren analysis case-by-case. Esto incluye AP07 (Scrum Zombi), AP11 (Meeting Overload), AP16 (Not Invented Here), etc. El impacto es real pero depende fuertemente de contexto organizacional específico.

---

## §11. PLAYBOOK REMEDIATION

### Template Remediation

```yaml
Antipatrón_ID: APXX
Severidad: 🔴/🟡/🟢
Detectado_En: [Fecha]

Síntomas_Observados:
  - [Métrica X = Y, threshold Z]
  - [Feedback teams: "..."]

Root_Cause_Analysis (5 Whys):
  1. ¿Por qué ocurre síntoma?
  2. ¿Por qué ocurre causa 1?
  3. ¿Por qué ocurre causa 2?
  4. ¿Por qué ocurre causa 3?
  5. ¿Por qué ocurre causa 4? → ROOT CAUSE

Plan_Remediation:
  Fase_1_Stop_Bleeding (0-2 semanas):
    - [Acción inmediata para contener]
  
  Fase_2_Fix_Root_Cause (2-8 semanas):
    - [Implementar patrón mitigador]
  
  Fase_3_Prevent_Recurrence (8-12 semanas):
    - [Proceso/governance para prevenir]

Métricas_Success:
  - [Métrica X de Y a Z en N semanas]
  
Owner: [Nombre]
Review_Date: [Fecha +4 semanas]
```

---

### Ejemplo Completo: AP14 (Tech Debt Perpetuo)

```yaml
Antipatrón_ID: AP14
Severidad: 🔴
Detectado_En: 2024-10-15

Síntomas_Observados:
  - Tech debt score: 68 (threshold <30)
  - Velocity: 15 pts/sprint (vs 40 pts hace 12 meses, -62%)
  - Incident rate: 12/mes (vs 4/mes hace 12 meses, +200%)
  - Deployment frequency: 1×/mes (vs 2×/semana target)

Root_Cause_Analysis:
  1. ¿Por qué velocity cayó? → 60% tiempo apagando fuegos
  2. ¿Por qué tantos incidents? → Tech debt crítico (tests <40%, legacy code)
  3. ¿Por qué tech debt alto? → 0% capacity dedicado a health
  4. ¿Por qué 0% health? → PM prioriza solo features (presión revenue)
  5. ¿Por qué presión revenue? → KPIs solo features shipped, no quality
  → ROOT CAUSE: Incentivos desalineados, no visibility cost tech debt

Plan_Remediation:
  Fase_1_Stop_Bleeding (Semanas 1-2):
    - Freeze features nuevas 2 sprints
    - Fix top 5 incidents root causes
    - Upgrade 3 dependencies críticas vulnerables
  
  Fase_2_Fix_Root_Cause (Semanas 3-8):
    - Implementar 20% rule: Min 20% capacity health cada sprint
    - Quality gates CI/CD: coverage >80%, 0 vulns high/critical
    - Refactor módulos top 3 tech debt (cyclomatic complexity >15)
  
  Fase_3_Prevent_Recurrence (Semanas 9-12):
    - Dashboard tech debt visible a C-level
    - OKR: "Tech debt score <30 by EOY"
    - PM compensation: 20% basado en quality metrics

Métricas_Success:
  - Tech debt score: 68 → <30 en 12 semanas
  - Velocity: 15 → 35 pts/sprint
  - Incident rate: 12 → <5/mes
  - Deployment frequency: 1×/mes → 2×/semana

Owner: CTO
Review_Date: 2024-11-15 (check progress), 2025-01-15 (final)
```

---

--- 

## §6.5. ANTIPATRONES DE SEGURIDAD (AP34-AP37)

| ID | Nombre | Síntoma | Causa Raíz | Consecuencia | Fix | Severidad |
|---|---|---|---|---|---|---|
| **AP34** | **Perímetro Confiable** | Foco exclusivo en seguridad perimetral (firewalls) | Mentalidad de "fortaleza", ignorar amenazas internas | Brechas por insiders, movimiento lateral atacantes | P_SEC02 (Zero Trust): verificar todo, nunca confiar | 🔴 |
| **AP35** | **Seguridad Manual** | Configs de seguridad hechas a mano, no versionadas | Falta de IaC para seguridad, silos Sec-Ops | Errores, drift, inconsistencia entre entornos | P_SEC03 (Security as Code): políticas como código | 🟡 |
| **AP36** | **Seguridad como Gate Final** | Security se revisa solo pre-producción | Cascada tradicional, "departamento del no" | Fixes costosos, lentitud, devs ven security como enemigo | P_SEC04 (Shift-Left): integrar seguridad en todo el ciclo | 🔴 |
| **AP37** | **Respuesta a Incidentes Lenta** | MTTD y MTTR > 24 horas | Playbooks manuales, falta de automatización (SOAR) | Daño extendido, pérdida de confianza, multas | P_SEC05 (Incident Response Automation): playbooks automáticos | 🔴 |

---

## §6.6. ANTIPATRONES DE EXPERIENCIA DE CLIENTE (AP38-AP40)

| ID | Nombre | Síntoma | Causa Raíz | Consecuencia | Fix | Severidad |
|---|---|---|---|---|---|---|
| **AP38** | **Diseño Inside-Out** | Servicios diseñados según estructura interna de la empresa | Foco en silos organizacionales, no en el cliente | Experiencia de cliente fragmentada, NPS bajo | P_CX01 (Flujo Valor Cliente): mapear journey outside-in | 🟡 |
| **AP39** | **Fricción del Cliente Invisible** | Puntos de dolor del cliente no medidos, se opera a ciegas | Falta de instrumentación del journey (telemetry) | Churn inesperado, quejas reactivas, oportunidades perdidas | P_CX02 (Eventos como Señales CX): convertir fricción en alertas | 🔴 |
| **AP40** | **"Tragedia de los Comunes" en CX** | CX es "responsabilidad de todos", pero nadie es dueño E2E | Falta de ownership explícito por touchpoint | Handoffs dolorosos, "no es mi problema", cliente sufre | P_CX03 (Touchpoint Ownership): asignar owner por etapa | 🔴 |

---

## §8. ANTIPATRONES TECNOLÓGICOS ESPECIALIZADOS (AP41-AP50)

**Nota**: Antipatrones especializados para aplicaciones enterprise, data products, AI systems y process automation. Ver `DOMINIOS_ESPECIALIZADOS/E7_Enterprise_Technology.md` y `E8_Intelligent_Data_AI_Systems.md` para ejemplos concretos de implementación.

### Antipatrones Tech Enterprise (AP41-AP43)

| ID | Nombre | Síntoma | Causa Raíz | Consecuencia | Fix | Severidad |
|---|---|---|---|---|---|---|
| **AP41** | **Premature Microservices** | Startup 5 engineers comienza con 15 microservicios sin justificar | Hype-driven architecture, no pain real con monolito | Complejidad operacional >10×, dev velocity -70%, cognitive load insostenible | Start monolito modular → Extract microservicios cuando dolor > complejidad. P54 Piecemeal Growth | 🟡 |
| **AP42** | **Frontend-Backend Coupling** | Frontend directamente acopla a backend DB schemas/internal APIs | No BFF (Backend-for-Frontend) layer, no API contracts estables | Deploy dependencies, violates team autonomy, API versioning imposible | API Gateway con contracts estables (OpenAPI), BFF layer, semantic versioning | 🟡 |
| **AP43** | **Big Design Up Front (BDUF)** | 6 meses diseño arquitectónico detallado antes de escribir código | Waterfall mindset, fear of refactoring, architecture astronauts | Requirements drift, sunk cost fallacy, time-to-market delay massive | P54 Piecemeal Growth + P55 Walking Skeleton: iterate con feedback real, P56 Continuous Refactoring | 🟡 |

### Antipatrones Data/AI/Process (AP44-AP50)

| ID | Nombre | Síntoma | Causa Raíz | Consecuencia | Fix | Severidad |
|---|---|---|---|---|---|---|
| **AP44** | **RPA Universal Hammer** | Usar RPA para toda automatización, incluso cuando APIs/ETL existen | RPA vendor hype, falta expertise APIs, "quick win" presión | Bots frágiles (UI changes → break), maintenance overhead alto (>60%), no escala, security risk | Audit APIs disponibles (99% sistemas tienen), API-first design, RPA solo legacy absoluto sin APIs | 🟡 |
| **AP45** | **Data Sin Contrato** | Datos compartidos sin schema documentado, SLO, ownership | "Move fast" cultura, no data governance, silos | Breaking changes silent (consumers crash), quality unknown, no ownership, no lineage | Implementar data contracts (P57, P62), schema registry, ownership RACI, lineage tools | 🔴 |
| **AP46** | **RAG Sin Curation** | RAG sobre corpus sin curate (fuentes no oficiales, vigencia unknown, calidad baja) | "Quick win" LLM without data quality investment | Hallucinations altas (>20%), citas inválidas, info desactualizada, compliance risk | Curation pipeline (E8 §6.3), authority validation, vigencia tracking, ACL enforcement. P58 RAG Auditable | 🔴 |
| **AP47** | **Observabilidad Mínima IA** | LLM en producción sin monitoring faithfulness, cost, latency | Treat LLM como "black box", no ML observability expertise | Degradation silent, cost overruns (no budgets), incidents slow resolution | Evaluation harness (offline + online), metrics dashboards, alerts critical thresholds, OpenTelemetry traces | 🟡 |
| **AP48** | **Automatizar Procesos Rotos** | Automatizar proceso ineficiente as-is (no optimize primero) | Urgencia delivery, no time process mining, "digitize ≠ optimize" confusion | "Mal pero rápido" (inefficiency amplified), user frustration, ROI bajo | Process mining (Celonis, Disco) → Identify bottlenecks, redesign process, THEN automate optimized | 🟡 |
| **AP49** | **Dual Write Pattern** | Write simultaneously a dos databases sin coordinación (DB1, DB2 parallel updates) | No event sourcing, no CDC, "just sync both" naive | Inconsistency inevitable (partial state), no rollback coordination, race conditions | Single source truth, CDC (Change Data Capture), Outbox Pattern (transactional). P57 Data Product | 🔴 |
| **AP50** | **Prompt Injection Undefended** | LLM sin input validation, user prompts ejecutan instrucciones maliciosas | No security awareness LLMs, treat como traditional apps | Data exfiltration, privilege escalation, jailbreak (bypass guardrails) | Input guardrails (prompt rewrite, injection defense), user input sandboxed, allowlist tools, output validation. OWASP Top-10 LLMs | 🔴 |

**Conexión KERNEL**:
- **E7 §10**: Ejemplos tech enterprise concretos (AP41-AP43)
- **E8 §11**: Ejemplos data/AI/process concretos (AP44-AP50)
- **P54-P56**: Patterns desarrollo evolutivo (previenen AP43)
- **P57-P63**: Patterns Data/AI especializados (previenen AP44-AP50)

---

## §7. ANTIPATRONES CRISIS & TRANSFORMATION (AP31-AP33)

| ID | Nombre | Síntoma | Causa Raíz | Consecuencia | Fix | Severidad |
|---|---|---|---|---|---|---|
| **AP31** | **Crisis Theater** | Declarar "crisis" sin cambiar governance | Leadership quiere urgency sin accountability | Staff burnout, credibility loss, no mejora real | Si crisis real (H<45) → Activate P52. Si no crisis → Don't declare crisis | 🔴 |
| **AP32** | **Forcing Transformation Unprepared** | Iniciar transformation con readiness score <3/5 en dimensiones críticas | Executive impatience, ignoring prerequisites | 70% failure rate transformations, wasted resources, damaged morale | Build readiness first (leadership alignment, resources, bandwidth), re-assess in 3-6 months | 🔴 |
| **AP33** | **Transforming During Crisis** | Major reorg mientras H_Score <45, financials/talent en crisis | "Never waste a crisis" mal interpretado, impaciencia | Crisis deepens, transformation fails, double disruption | Stabilize FIRST using P52 (crisis governance), transform AFTER H>45 stable 3 months | 🔴 |

**Detalles:**

### AP31: Crisis Theater

```yaml
Síntoma_Específico:
  - Executives declaran "all-hands crisis mode"
  - Pero meetings siguen siendo weekly, no daily
  - Decision rights no cambian
  - No crisis team formado
  - Staff trabaja overtime sin estructura emergency
  
Diagnóstico:
  H_Score: Típicamente 50-65 (no es crisis real)
  Motivación: Create urgency artificial, politics
  
Consecuencia_12_Meses:
  - Burnout rate +40%
  - Attrition +15% (IN2 collapse)
  - "Crisis fatigue" - next real crisis ignored
  - Credibility leadership destroyed
  
Fix_Pattern:
  IF H_Score < 45 AND (O3<30 OR O2<30 OR IN2<30):
    → Real crisis → Activate P52 (Crisis Governance)
    → Daily meetings, stop bleeding (cash, customers, talent)
    → NO structural changes
    
  ELSE IF H_Score >= 45:
    → Not crisis → Don't declare crisis
    → Use normal urgency mechanisms (OKRs, roadmap prioritization)
```

---

### AP32: Forcing Transformation Unprepared

```yaml
Síntoma_Específico:
  - Transformation kicked off sin readiness assessment
  - Leadership fragmented (algunos support, otros resist)
  - No resources allocated (team at 95% utilization)
  - No skills in-house, no budget consultants
  - Urgency artificial ("competitors doing it")
  
Diagnóstico:
  Readiness_Dimensions (rate 1-5):
    - Leadership Alignment: 2 (fragmented)
    - Urgency Level: 2 (no compelling case)
    - Resource Availability: 1 (no capacity)
    - Capability: 1 (no skills)
    - Org Bandwidth: 1 (overloaded)
  
  Decision_Matrix: ANY dimension <3 → BUILD READINESS
  
Consecuencia_24_Meses:
  - 70% probability complete failure
  - $500K-$2M wasted (consulting, tools, time)
  - Morale damage (cynicism next transformation)
  - Competitive position worsens (distraction)
  
Fix_Prerequisites:
  1. Leadership_Alignment:
     - Facilitated workshops, alignment sessions
     - Get 100% exec team buy-in or don't proceed
  
  2. Resource_Availability:
     - Free up 20% capacity (stop other initiatives)
     - Allocate budget ($200K-$1M depending scale)
  
  3. Capability:
     - Hire transformation expertise OR
     - Engage consultants with transfer knowledge plan
  
  Re-Assess: 3-6 months, verify all dimensions >=3
```

---

### AP33: Transforming During Crisis

```yaml
Síntoma_Específico:
  - H_Score 20-40 (crisis mode)
  - Cash runway <60 days OR Churn >25% OR Attrition >25%
  - Executive decides "now is time to reorg" (crisis = opportunity)
  - Major structural changes while firefighting
  
Diagnóstico:
  Confusion: "Never waste crisis" misunderstood
  Reality: Crisis needs STABILIZATION first, transformation second
  
  Correct_Sequence:
    Week 1-4: Emergency stabilization (P52 crisis governance)
    Week 5-12: Intensive diagnosis (root causes)
    Month 4+: IF H>45 THEN structural transformation
  
Consecuencia_Dual_Disruption:
  - Crisis worsens (attention diverted to reorg)
  - Transformation fails (organization too stressed to absorb)
  - H_Score drops further: 35 → 22 (existential)
  - Talent exodus accelerates (uncertainty × crisis)
  
Fix_Pattern:
  Current_State: H_Score = 35 (crisis)
  
  WRONG_Path:
    Week 1: Announce major reorg
    Week 2-8: Restructure while firefighting
    → Result: H_Score 35 → 22, crisis deepens
  
  CORRECT_Path:
    Week 1-4: Activate P52 (crisis governance only)
      - Daily meetings, stop bleeding (cash, customers, talent)
      - NO structural changes
    
    Week 5-12: Diagnosis
      - Root cause analysis
      - Energy/conflict mapping
      - Building blocks completeness test
    
    Month 4: Check H_Score
      IF H_Score > 45 for 3 consecutive months:
        → NOW safe to transform
        → Follow A4 §1-§6 playbook
      
      ELSE:
        → Continue stabilization
        → Delay transformation
```

---

---

**Conexión v1.4:**

- AP31-33 consolidados en single source of truth: `CORE/08_Crisis_Management.md` §5
- Detalles completos: Structure, diagnosis, consequences, fixes, prevention
- Case study financial crisis: `CORE/08_Crisis_Management.md` §9

---

## Referencias Cruzadas

- **Patrones mitigadores:** `APLICACION/A1_Patrones.md`
- **Crisis Governance (P52):** `CORE/08_Crisis_Management.md` (consolidado)
- **Crisis Antipatrones (AP31-33):** `CORE/08_Crisis_Management.md` §5
- **Readiness Triage:** `APLICACION/A4_Implementacion.md` §0
- **Crisis Thresholds:** `DOMINIOS/D2_Percepcion.md` (O2, O3, IN2) + `CORE/08_Crisis_Management.md` §2
- **Diagnóstico antipatrones:** `APLICACION/A3_Diagnostico.md`
- **11 Observables:** `DOMINIOS/D2_Percepcion.md`
- **Principios violados:** `CORE/00_Manifiesto.md` §3
