# A2_Antipatrones

**Versión:** 2.3.0 | **Estado:** Definitivo | **Audiencia:** Practitioners, Arquitectos, Security, Product/UX, Data/AI Engineers

---

## §1. TAXONOMÍA EJECUTIVA

```yaml
Inventario: 52 antipatrones (AP01-AP52) en 10 categorías

Categorías:
  Estructurales (AP01-AP06): Org design, teams, roles
  Procesuales (AP07-AP12): Workflows, coordinación
  Tecnológicos (AP13-AP18): Arquitectura, infraestructura
  Decisionales (AP19-AP24): OKRs, roadmaps, priorización
  IA (AP25-AP30): Delegación incorrecta, bias algorítmico
  Crisis & Transformation (AP31-AP33): Emergency governance, readiness
  Seguridad (AP34-AP37): Security by design, incident response
  Customer Experience (AP38-AP40): Customer-centricity, value stream
  Tech Especializados (AP41-AP50): Enterprise/Data/AI/Process
  Multi-Tenant (AP51-AP52): Isolation, data leaks

Distribución Severidad:
  🔴 Crítico: 24 (46%) - Fix <30 días, sponsor ejecutivo mandatory
  🟡 Alto: 24 (46%) - Fix <90 días, roadmap remediation
  🟢 Moderado: 4 (8%) - Backlog, fix oportunista

Navegación:
  §2: Catálogo completo (tablas por categoría)
  §3: Análisis transversal (severidad, dominios, top 10)
  §4: Herramientas operativas (detección, mitigación, costos)
  §5: Referencias cruzadas KERNEL
```

---

## §2. CATÁLOGO DE ANTIPATRONES

### §2.1. Estructurales (AP01-AP06)

| ID | Nombre | Síntoma | Causa Raíz | Consecuencia | Fix | Sev |
|---|---|---|---|---|---|---|
| **AP01** | **Matrix sin Governance** | Dual reporting, nadie decide conflictos | Matrix sin ARB/escalation | Paralysis decisional, IN1<40 | Governance explícito: ARB semanal, RACI claro, escalation path | 🔴 |
| **AP02** | **Reorg Perpetuo** | Cambio estructura cada 3-6 meses | No diagnosticar root cause, "reorg como magia" | IN2 colapsa (fatigue), no learning | Diagnosticar antes reorg, pilot 1-2 teams, max 1 reorg/18 meses | 🔴 |
| **AP03** | **Silos Profundos** | Departments no colaboran, handoffs eternos | Especialización sin interfaces, "not my job" | Cycle time >14 días, handoff_ratio >40% | Cross-functional squads, shared OKRs, interfaces claras | 🟡 |
| **AP04** | **Span of Control Extremo** | Manager 25+ reports directos | Growth sin management layer | No 1:1s, IN2 cae, development nulo | Target 5-9 reports/manager, split teams, promote leads | 🟡 |
| **AP05** | **Conway Inverse Fallacy** | Cambiar org para forzar arquitectura tech deseada | Malinterpretar Conway (org→tech, no tech→org) | Resistance, fracaso adoption | Alinear org con tech actual, evolucionar ambos coordinadamente | 🟡 |
| **AP06** | **Teams Proyecto** | Teams formados para proyecto, disueltos post-completion | Project thinking vs Asset thinking | Knowledge loss, ramp-up perpetuo | Teams estables long-term, trabajo fluye a través team | 🟡 |

---

### §2.2. Procesuales (AP07-AP12)

| ID | Nombre | Síntoma | Causa Raíz | Consecuencia | Fix | Sev |
|---|---|---|---|---|---|---|
| **AP07** | **Scrum Zombi** | Ceremonies sin valor, rituales vacíos | Scrum by-the-book sin entender principios | Fatigue meetings, velocity estancada | Retrospectiva: ¿Qué ceremonies aportan valor? Eliminar waste | 🟢 |
| **AP08** | **WIP Sin Límite** | 30+ items "In Progress" simultáneamente | No entender cost context switching | Cycle time >14 días, nada completa | WIP limits explícitos (1.5× team size), finish antes start nuevo | 🟡 |
| **AP09** | **Handoff Hell** | 8+ handoffs en proceso deploy | Silos funcionales + process design malo | Cycle time >21 días, flow efficiency <10% | Value stream map, eliminar handoffs innecesarios, automation | 🔴 |
| **AP10** | **Estimation Theater** | 4 horas estimating 2-week sprint | Precisión falsa, planning poker eterno | Waste tiempo, estimates inaccurate anyway | #NoEstimates O cycle time historical data + Monte Carlo | 🟢 |
| **AP11** | **Meeting Overload** | >30% tiempo en meetings | Falta clarity ownership, over-communication | Productivity <50%, burnout | Audit meetings (¿valor agregado?), async-first, clear DRI | 🟡 |
| **AP12** | **Retro Sin Acción** | Retrospectivas sin implementar action items | No ownership, no follow-up | Learning 0, mismos problemas repiten | Max 3 action items, assign owner, review next retro (mandatorio) | 🟢 |

---

### §2.3. Tecnológicos (AP13-AP18)

| ID | Nombre | Síntoma | Causa Raíz | Consecuencia | Fix | Sev |
|---|---|---|---|---|---|---|
| **AP13** | **Monolito Distribuido** | Microservices pero deployments acoplados | Split tech sin split org (viola Conway) | Peor de ambos mundos: complejidad microservices + rigidez monolito | Inverse Conway: reorg teams primero O consolidar a monolito modular | 🔴 |
| **AP14** | **Tech Debt Perpetuo** | >50% tiempo apagando fuegos | 0% capacity dedicado a health, solo features | Velocity cae 60%, incident rate crece 200% | 20% min capacity health (refactor, tests, automation) | 🔴 |
| **AP15** | **Big Bang Rewrite** | Replace legacy system completo en 1 deploy | "Empezar desde cero es más fácil" (falso) | 80% failures, 24+ meses, budget overrun 3× | Strangler Fig pattern: replacement incremental | 🔴 |
| **AP16** | **Not Invented Here** | Re-implementar lo que existe open source | NIH syndrome, arrogancia | Waste tiempo, calidad inferior, maintenance burden | Use open source maduro, contribute upstream | 🟢 |
| **AP17** | **Resume-Driven Development** | Adoptar tech porque "cool" sin business case | Engineers quieren aprender X, no porque resuelve problema | Tech stack fragmentado, complexity sin ROI | Tech radar: Adopt/Trial/Assess/Hold, business case mandatorio | 🟡 |
| **AP18** | **Deploy = Release** | Deploy a prod = feature visible a todos usuarios | No separar deployment de release | Rollback lento (30+ min), no A/B testing, blast radius 100% | Feature flags: deploy disabled, gradual rollout, instant rollback | 🟡 |

---

### §2.4. Decisionales (AP19-AP24)

| ID | Nombre | Síntoma | Causa Raíz | Consecuencia | Fix | Sev |
|---|---|---|---|---|---|---|
| **AP19** | **Output Disguised as Outcome** | OKR "Launch 10 features" | No entender diferencia output vs outcome | Delivery sin impacto, vanity metrics | OKRs outcome-based: "Aumentar retention +15%", no "launch X" | 🟡 |
| **AP20** | **HiPPO Decisions** | Highest Paid Person's Opinion gana siempre | Autoridad basada en seniority, no en data | Suboptimal decisions, team disengagement | Data-driven decision making, delegación por expertise | 🟡 |
| **AP21** | **Analysis Paralysis** | Decisiones tardan >4 semanas análisis | Perfectionism, risk-aversion extremo | Velocity decisional <30, competitors avanzan | Type 1 vs Type 2 decisions, bias hacia action reversible | 🟢 |
| **AP22** | **Roadmap Wish List** | Roadmap = todo lo que alguien pidió alguna vez | No priorización real, "todos felices" | Focus 0, delivery 0, nada completa | Ruthless prioritization: RICE, WSJF, top 5 solo | 🔴 |
| **AP23** | **Planning Fallacy** | Estimates 50% del tiempo real consistentemente | Optimism bias, no histórico | Missed deadlines perpetuos, credibility loss | #NoEstimates O historical cycle time + confidence intervals | 🟢 |
| **AP24** | **Sunk Cost Fallacy** | Continuar proyecto fracasado porque "ya invertimos $X" | Emotional attachment, loss aversion | Bueno dinero tras malo, opportunity cost | Kill criteria up-front, review quarterly: continuar/pivot/kill | 🟡 |

---

### §2.5. IA (AP25-AP30)

| ID | Nombre | Síntoma | Causa Raíz | Consecuencia | Fix | Sev |
|---|---|---|---|---|---|---|
| **AP25** | **M6 Prematuro** | Implementar M6 sin validar M1-M4 | "Move fast" sin considerar riesgos | Fallos catastróficos, pérdida confianza IA | Siempre progresar M1→M2→M3→M4→M6, validar cada etapa | 🔴 |
| **AP26** | **Automation Bias** | Confiar ciegamente en M6, no validar | "Computer said so" syndrome | Errores sistemáticos no detectados | Monitoring activo + auditoría periódica resultados M6 | 🔴 |
| **AP27** | **No Escalation Path** | M6 sin mecanismo rollback a M4/M2 | Diseño asume "IA nunca falla" | Cuando falla, no escape hatch, incident 4+ hrs | Siempre implementar circuit breaker + escalation humano | 🔴 |
| **AP28** | **Bias Algorítmico Ignorado** | ML discrimina grupos sin detectar | No auditar bias en training data | Violaciones legales (EEOC, GDPR), daño reputacional | Bias detection audits, diverse training data, XAI mandatorio | 🔴 |
| **AP29** | **M1 Perpetuo** | Nunca evolucionar de M1 después años | Risk-aversion extrema, falta skills IA | No capturar valor IA, competitors avanzan | Roadmap progresión modos, upskilling team, quick wins M2 | 🟡 |
| **AP30** | **Mode Mismatch** | Usar M3 cuando necesitas M4 | No entender diferencia modos | Humano saturado requests manuales, scalability limit | Decision tree CORE/04_Delegacion.md: volumen/latencia→modo | 🟡 |

---

### §2.6. Crisis & Transformation (AP31-AP33)

| ID | Nombre | Síntoma | Causa Raíz | Consecuencia | Fix | Sev |
|---|---|---|---|---|---|---|
| **AP31** | **Crisis Theater** | Declarar "crisis" sin cambiar governance, meetings siguen weekly no daily, no crisis team | Leadership quiere urgency sin accountability | Burnout +40%, attrition +15%, credibility loss, "crisis fatigue" | Si H<45 AND (O3<30 OR O2<30 OR IN2<30) → P52 Crisis Governance. Si H≥45 → No declarar crisis | 🔴 |
| **AP32** | **Forcing Transformation Unprepared** | Transformation con readiness <3/5 en dimensiones críticas (leadership, resources, capability, bandwidth) | Executive impatience, ignoring prerequisites | 70% failure rate, $500K-$2M waste, morale damage, competitive position worsens | Build readiness: alignment workshops, free 20% capacity, hire/upskill. Re-assess 3-6 meses | 🔴 |
| **AP33** | **Transforming During Crisis** | Major reorg mientras H<45, cash runway <60d, churn >25% | "Never waste crisis" mal interpretado | Crisis deepens (H: 35→22), transformation fails, dual disruption, talent exodus | Stabilize FIRST (P52 crisis governance Weeks 1-4), transform AFTER H>45 stable 3 meses | 🔴 |

**Detalle operativo**: Ver `CORE/08_Crisis_Management.md` para playbooks completos P52, readiness dimensions (R1-R5), H_Score thresholds.

---

### §2.7. Seguridad (AP34-AP37)

| ID | Nombre | Síntoma | Causa Raíz | Consecuencia | Fix | Sev |
|---|---|---|---|---|---|---|
| **AP34** | **Perímetro Confiable** | Foco exclusivo en seguridad perimetral (firewalls) | Mentalidad "fortaleza", ignorar amenazas internas | Brechas insiders, movimiento lateral atacantes | P_SEC02 Zero Trust: verificar todo, nunca confiar implícitamente | 🔴 |
| **AP35** | **Seguridad Manual** | Configs seguridad hechas a mano, no versionadas | Falta IaC para seguridad, silos Sec-Ops | Errores, drift, inconsistencia entre entornos | P_SEC03 Security as Code: políticas versionadas, IaC, GitOps | 🟡 |
| **AP36** | **Seguridad como Gate Final** | Security se revisa solo pre-producción | Cascada tradicional, "departamento del no" | Fixes costosos, lentitud, devs vs security | P_SEC04 Shift-Left: integrar security todo el ciclo (design, code, CI/CD) | 🔴 |
| **AP37** | **Respuesta a Incidentes Lenta** | MTTD y MTTR >24 horas | Playbooks manuales, falta automatización SOAR | Daño extendido, pérdida confianza, multas | P_SEC05 Incident Response Automation: playbooks automáticos, runbooks | 🔴 |

---

### §2.8. Customer Experience (AP38-AP40)

| ID | Nombre | Síntoma | Causa Raíz | Consecuencia | Fix | Sev |
|---|---|---|---|---|---|---|
| **AP38** | **Diseño Inside-Out** | Servicios diseñados según estructura interna empresa | Foco en silos org, no en cliente | Experiencia fragmentada, NPS bajo, churn 20%+ | P_CX01 Flujo Valor Cliente: mapear journey outside-in | 🔴 |
| **AP39** | **Fricción del Cliente Invisible** | Puntos de dolor no medidos, opera a ciegas | Falta instrumentación journey (telemetry) | Churn inesperado, quejas reactivas, oportunidades perdidas | P_CX02 Eventos como Señales CX: convertir fricción en alertas | 🟡 |
| **AP40** | **"Tragedia de los Comunes" en CX** | CX es "responsabilidad de todos", nadie owner E2E | Falta ownership explícito por touchpoint | Handoffs dolorosos, "no es mi problema", cliente sufre | P_CX03 Touchpoint Ownership: asignar owner por etapa | 🟡 |

---

### §2.9. Tech Especializados (AP41-AP50)

**Enterprise Tech (AP41-AP43)**

| ID | Nombre | Síntoma | Causa Raíz | Consecuencia | Fix | Sev |
|---|---|---|---|---|---|---|
| **AP41** | **Premature Microservices** | Startup 5 engineers comienza con 15 microservicios sin justificar | Hype-driven architecture, no pain real con monolito | Complejidad operacional >10×, velocity -70%, cognitive load insostenible | Start monolito modular → Extract microservicios cuando dolor > complejidad. P54 Piecemeal Growth | 🟡 |
| **AP42** | **Frontend-Backend Coupling** | Frontend directamente acopla a backend DB schemas/internal APIs | No BFF layer, no API contracts estables | Deploy dependencies, violates team autonomy, API versioning imposible | API Gateway con contracts (OpenAPI), BFF layer, semantic versioning | 🟡 |
| **AP43** | **Big Design Up Front (BDUF)** | 6 meses diseño arquitectónico detallado antes escribir código | Waterfall mindset, fear of refactoring | Requirements drift, sunk cost fallacy, time-to-market delay massive | P54 Piecemeal Growth + P55 Walking Skeleton: iterate con feedback real | 🟡 |

**Data/AI/Process (AP44-AP50)**

| ID | Nombre | Síntoma | Causa Raíz | Consecuencia | Fix | Sev |
|---|---|---|---|---|---|---|
| **AP44** | **RPA Universal Hammer** | Usar RPA para toda automatización, incluso cuando APIs/ETL existen | RPA vendor hype, falta expertise APIs | Bots frágiles (UI changes→break), maintenance >60%, no escala, security risk | Audit APIs disponibles (99% sistemas tienen), API-first, RPA solo legacy absoluto | 🟡 |
| **AP45** | **Data Sin Contrato** | Datos compartidos sin schema documentado, SLO, ownership | "Move fast" cultura, no data governance | Breaking changes silent (consumers crash), quality unknown, no lineage | P57, P62 Data Contracts: schema registry, ownership RACI, lineage tools | 🔴 |
| **AP46** | **RAG Sin Curation** | RAG sobre corpus sin curate (fuentes no oficiales, vigencia unknown, calidad baja) | "Quick win" LLM without data quality investment | Hallucinations >20%, citas inválidas, info desactualizada, compliance risk | P58 RAG Auditable: curation pipeline, authority validation, vigencia tracking, ACL | 🔴 |
| **AP47** | **Observabilidad Mínima IA** | LLM en producción sin monitoring faithfulness, cost, latency | Treat LLM como "black box", no ML observability | Degradation silent, cost overruns, incidents slow resolution | Evaluation harness (offline+online), metrics dashboards, alerts, OpenTelemetry | 🟡 |
| **AP48** | **Automatizar Procesos Rotos** | Automatizar proceso ineficiente as-is (no optimize primero) | Urgencia delivery, no process mining, "digitize≠optimize" confusion | "Mal pero rápido" (inefficiency amplified), frustration, ROI bajo | Process mining (Celonis, Disco) → redesign → THEN automate optimized | 🟡 |
| **AP49** | **Dual Write Pattern** | Write simultáneamente a dos DBs sin coordinación (DB1, DB2 parallel updates) | No event sourcing, no CDC, "just sync both" naive | Inconsistency inevitable, no rollback coordination, race conditions | Single source truth, CDC (Change Data Capture), Outbox Pattern. P57 Data Product | 🔴 |
| **AP50** | **Prompt Injection Undefended** | LLM sin input validation, user prompts ejecutan instrucciones maliciosas | No security awareness LLMs, treat como traditional apps | Data exfiltration, privilege escalation, jailbreak (bypass guardrails) | Input guardrails (rewrite, injection defense), sandboxed input, allowlist tools, output validation. OWASP Top-10 LLMs | 🔴 |

**Conexión KERNEL**: Ver `DOMINIOS_ESPECIALIZADOS/E7_Enterprise_Technology.md` §10 y `E8_Intelligent_Data_AI_Systems.md` §11 para ejemplos concretos implementación.

---

### §2.10. Multi-Tenant (AP51-AP52)

| ID | Nombre | Síntoma | Causa Raíz | Consecuencia | Fix | Sev |
|---|---|---|---|---|---|---|
| **AP51** | **Noisy Neighbor** | Tenant A spike CPU/IOPS → Tenant B degraded performance (latency +300%, timeouts) | No resource quotas per-tenant, shared compute sin límites | Tenant B churn (SLA breach), reputation damage, revenue loss | P64 Level 2+ isolation: K8s ResourceQuota, per-tenant throttling, circuit breakers, monitoring per-tenant | 🔴 |
| **AP52** | **Cross-Tenant Data Leak** | Tenant A users see Tenant B data (bug WHERE tenant_id filter) | Application-level isolation sin DB-level enforcement, no unit tests isolation | Data breach (€20M GDPR fines), trust loss, churn 80%+, lawsuits | P64 Level 2+: Postgres RLS, ORM scopes mandatory, unit tests 100% isolation, quarterly pen-test | 🔴 |

**Detalle técnico AP51**: Resource quotas (CPU, memory, DB connections, IOPS), circuit breakers (>90% CPU 5min → 503), monitoring per-tenant (dashboards, alerting >80% quota), billing alignment (usage-based pricing).

**Detalle técnico AP52**: Defense-in-depth (Layer 1: App middleware inject tenant_id, Layer 2: Postgres RLS policies, Layer 3: API Gateway JWT validation, Layer 4: Network VPC isolation), automated testing (unit tests 100% coverage tenant isolation, integration tests cross-tenant access forbidden, quarterly security pen-test), audit trail (immutable logs tenant_id+user_id+query, 7yr retention, SOC2/ISO27001 controls), incident response (<1h containment, <72h GDPR notification, <7d remediation).

**Conexión**: Ver `APLICACION/A1_Patrones.md` P64 Multi-Tenant Architecture para patterns preventivos.

---

## §3. ANÁLISIS TRANSVERSAL

### §3.1. Matriz Severidad × Dominio

| Dominio ↓ / Severidad → | 🔴 Crítico | 🟡 Alto | 🟢 Moderado |
|------------------------|-----------|--------|------------|
| **D1 Arquitectura** | AP01, AP02, AP13, AP15, AP51, AP52 | AP03, AP04, AP05, AP17, AP41 | AP06, AP16 |
| **D2 Percepción** | AP34, AP36, AP37 | AP35 | — |
| **D3 Decisión** | AP22 | AP19, AP20, AP24 | AP21, AP23 |
| **D4 Operación** | AP09, AP14, AP25, AP26, AP27, AP28, AP31, AP45, AP46, AP49, AP50 | AP08, AP11, AP18, AP29, AP30, AP42, AP44, AP47, AP48 | AP07, AP10, AP12, AP43 |
| **Transversal Crisis** | AP32, AP33 | — | — |
| **Transversal CX** | AP38 | AP39, AP40 | — |

**Leyenda Dominios**:

- **D1 Arquitectura**: Estructura org, teams, roles, org design
- **D2 Percepción**: Observables, monitoring, security, metrics
- **D3 Decisión**: OKRs, roadmaps, prioritization, strategy
- **D4 Operación**: Workflows, deployment, processes, execution, AI delegation
- **Transversal**: Aplican múltiples dominios

**Distribución por Dominio**:

- D1 Arquitectura: 12 AP (6 🔴 + 5 🟡 + 1 🟢)
- D2 Percepción: 4 AP (3 🔴 + 1 🟡)
- D3 Decisión: 6 AP (1 🔴 + 3 🟡 + 2 🟢)
- D4 Operación: 27 AP (11 🔴 + 13 🟡 + 3 🟢)
- Transversal: 3 AP (3 🔴)

---

### §3.2. Top 10 Antipatrones Más Críticos

| Rank | ID | Nombre | Dominio | Impacto Típico | MTTR Target |
|------|----|---------|---------|-----------------|--------------|
| 1 | AP52 | Cross-Tenant Data Leak | D1 | GDPR €20M fines, churn 80%+ | <7 días |
| 2 | AP25 | M6 Prematuro | D4 | Fallos catastróficos IA, pérdida confianza | <14 días |
| 3 | AP28 | Bias Algorítmico Ignorado | D4 | Violaciones legales, daño reputacional | <30 días |
| 4 | AP15 | Big Bang Rewrite | D1 | 80% failures, budget 3×, 24+ meses waste | <30 días (stop) |
| 5 | AP02 | Reorg Perpetuo | D1 | IN2 colapso, turnover 40%+, learning 0 | <60 días |
| 6 | AP14 | Tech Debt Perpetuo | D4 | Velocity -60%, incident rate +200% | <90 días |
| 7 | AP22 | Roadmap Wish List | D3 | Focus 0, delivery 0, opportunity cost alto | <30 días |
| 8 | AP31 | Crisis Theater | D4 | Burnout +40%, credibility loss, fatigue | <7 días (stop) |
| 9 | AP38 | Inside-Out Design | CX | Churn 20%+, NPS <0, revenue loss 20%+ | <90 días |
| 10 | AP51 | Noisy Neighbor | D1 | SLA breach, churn, reputation damage | <30 días |

**Nota**: MTTR = Mean Time To Remediate (tiempo típico fix desde detection). Estos antipatrones representan amenazas existenciales para health organizacional, customer trust y compliance legal. Requieren sponsor ejecutivo y fix prioritario.

---

## §4. HERRAMIENTAS OPERATIVAS

### §4.1. Patrones Mitigadores

| Antipatrón | Mitigado por Patrón(es) | Efectividad |
|-----------|-------------------------|-------------|
| AP01 (Matrix sin Governance) | P01 Feature Teams, P11 Squad-Chapter | Alta |
| AP02 (Reorg Perpetuo) | P35 R1-R5 Preparación | Alta |
| AP03 (Silos) | P01 Feature Teams, P13 Dual-Track | Alta |
| AP08 (WIP Sin Límite) | P15 WIP Limits Kanban | Alta |
| AP09 (Handoff Hell) | P14 Value Stream Mapping, P01 Feature Teams | Alta |
| AP13 (Monolito Distribuido) | P06 Inverse Conway, P25 DB per Service | Media |
| AP14 (Tech Debt Perpetuo) | P20 Retrospectiva Accionable + 20% rule | Alta |
| AP15 (Big Bang Rewrite) | P21 Strangler Fig | Alta |
| AP18 (Deploy=Release) | P23 Feature Flags | Alta |
| AP19 (Output as Outcome) | P29 OKRs Bottom-Up + filosofía correcta | Alta |
| AP22 (Roadmap Wish List) | P31 RICE Scoring, P33 WSJF | Media |
| AP23 (Planning Fallacy) | Forecasts probabilísticos (D3 §3.1) | Media |
| AP25 (M6 Prematuro) | Progresión M1→M6 disciplinada | Alta |
| AP27 (No Escalation) | Circuit breakers, resilience design | Alta |
| AP34 (Perímetro Confiable) | P_SEC02 Zero Trust Architecture | Alta |
| AP35 (Seguridad Manual) | P_SEC03 Security as Code | Alta |
| AP36 (Seguridad como Gate Final) | P_SEC04 Shift-Left Security | Alta |
| AP37 (Respuesta Incidentes Lenta) | P_SEC05 Incident Response Automation | Alta |
| AP38 (Diseño Inside-Out) | P_CX01 Flujo Valor Cliente | Alta |
| AP39 (Fricción Invisible) | P_CX02 Eventos como Señales CX | Alta |
| AP40 (Tragedia Comunes CX) | P_CX03 Touchpoint Ownership Explícita | Alta |
| AP41 (Premature Microservices) | P54 Piecemeal Growth | Alta |
| AP42 (Frontend-Backend Coupling) | API Gateway + BFF, Contract-first design | Media |
| AP43 (BDUF) | P54 Piecemeal, P55 Walking Skeleton, P56 Continuous Refactoring | Alta |
| AP44 (RPA Universal Hammer) | API-first architecture review | Media |
| AP45 (Data Sin Contrato) | P57 Data Product, P62 Contract-Driven Evolution | Alta |
| AP46 (RAG Sin Curation) | P58 RAG Auditable | Alta |
| AP47 (Observabilidad Mínima IA) | Evaluation harness (E8 §5.5), Observability-first | Alta |
| AP48 (Automatizar Procesos Rotos) | Process mining, optimize-first principle | Media |
| AP49 (Dual Write Pattern) | P57 Data Product single source, CDC/Outbox | Alta |
| AP50 (Prompt Injection) | Input/output guardrails (E8 §5.3), OWASP Top-10 LLMs | Alta |
| AP51 (Noisy Neighbor) | P64 Multi-Tenant Level 2+, Resource Quotas | Alta |
| AP52 (Cross-Tenant Data Leak) | P64 Multi-Tenant Level 2+, Postgres RLS, Unit Tests 100% | Alta |

**Nota OKRs Adicionales**: Para anti-patrones OKR (Top-Down Imposition, Linked to Compensation, Estimating OKRs, 100% Expected) ver `DOMINIOS/D3_Decision.md` §1 Anti-Patrones AP6-AP9. Todos mitigados por P29 + claridad filosófica OKRs.

---

### §4.2. Detección Temprana

**Señales por Categoría**

```yaml
Estructurales:
  IN1 (Velocidad decisional) <40: AP01, AP02 probables
  Handoff_ratio >40%: AP03 confirmado
  Avg reports/manager >12: AP04 confirmado
  Reorg frequency >1/18 meses: AP02 crítico

Procesuales:
  Cycle time >14 días: AP08, AP09 probables
  Flow efficiency <15%: AP09 confirmado
  WIP >2× team size: AP08 confirmado
  Meeting time >30%: AP11 confirmado

Tecnológicos:
  Deploy frequency <1/mes: AP14, AP18 probables
  Tech debt score >50: AP14 crítico
  Incident rate creciendo >50%/trimestre: AP14, AP15
  Microservices count >3× team count: AP13, AP41 probable

Decisionales:
  Time-to-decision >21 días: AP20, AP21
  % OKRs output-based >60%: AP19
  Backlog >100 items no priorizados: AP22
  Projects killed >30%: AP24 probable

IA:
  Incidents causados por IA >5%: AP25, AP26, AP27
  Bias detection audit nunca hecho: AP28 riesgo alto
  M1 usage >90% después 18 meses: AP29
  Human escalation requests >50/día: AP30 mode mismatch

Crisis:
  H_Score <45 pero no crisis governance: AP31 probable
  Transformation iniciado con readiness <3/5: AP32
  Major reorg durante H<45: AP33

Seguridad:
  MTTD >24h: AP34, AP37
  Security configs manual: AP35
  Security reviews solo pre-prod: AP36

CX:
  NPS <0: AP38 probable
  Customer complaints trending +20%/trimestre: AP39
  Touchpoints sin owner: AP40

Multi-Tenant:
  Tenant performance complaints >10/mes: AP51
  Cross-tenant access bugs encontrados: AP52 crítico
```

---

### §4.3. Cost of Delay

**Disclaimer Metodológico**

```yaml
Nota_Validación:
  - Costos derivados de research industry pública (citada)
  - Estimaciones para org 100 engineers como baseline
  - Escala aproximadamente lineal (200 eng ≈ 2× cost)
  - Contexto específico puede variar significativamente
  - Use como order-of-magnitude, no precisión absoluta
  
Cobertura:
  - 11 antipatrones cuantificados (de 52 total, 21%)
  - Research sources citadas donde disponible
  - 41 antipatrones: Impacto significativo pero requiere case-by-case quantification
  
Recomendación_Uso:
  - Priorización relativa (AP14 > AP07 en costo típico)
  - No usar para ROI preciso sin validación local
  - Complementar con diagnóstico específico (A3)
```

**Impacto Financiero Estimado**

| Antipatrón | Cost of Delay ($/mes por 100 eng) | Fuente/Rationale | Sev |
|-----------|-----------------------------------|------------------|-----|
| **AP02** (Reorg Perpetuo) | $200K (IN2 churn 15%, productivity -30%) | Google re:Work study | 🔴 |
| **AP03** (Silos Profundos) | $180K (handoff overhead, cycle time 2×) | Lean Enterprise research | 🟡 |
| **AP08** (WIP Sin Límite) | $120K (context switching, cycle time +80%) | Personal Kanban studies | 🟡 |
| **AP09** (Handoff Hell) | $150K (cycle time 3×, flow efficiency <15%) | State of DevOps Report | 🔴 |
| **AP13** (Monolito Distribuido) | $180K (complexity without modularity benefits) | ThoughtWorks Technology Radar | 🔴 |
| **AP14** (Tech Debt Perpetuo) | $250K (velocity -60%, incidents +200%) | Stripe Developer Coefficient | 🔴 |
| **AP15** (Big Bang Rewrite) | $500K (opportunity cost 18+ meses no delivery) | Gartner research | 🔴 |
| **AP20** (HiPPO Decisions) | $100K (suboptimal decisions, team disengagement) | McKinsey decision quality | 🟡 |
| **AP22** (Roadmap Wish List) | $140K (no focus, nada completa, thrashing) | Pragmatic Marketing research | 🔴 |
| **AP25** (M6 Prematuro) | $100K-$1M (incident severity dependent) | Industry case studies IA failures | 🔴 |
| **AP26** (Automation Bias) | $80K-$500K (systematic errors undetected) | Algorithm bias research (O'Neil) | 🔴 |

**Total potencial críticos:** $2.18M/mes para org 100 eng si 6+ antipatrones críticos presentes simultáneamente.

**Efectos No Lineales:**

- AP14 (Tech Debt) + AP09 (Handoffs) = 1.5× cost individual (compounding effect)
- AP02 (Reorg) + AP33 (Transform During Crisis) = 2× cost (dual disruption)
- AP25 (M6 Prematuro) + AP28 (Bias Algorítmico) = Riesgo legal exponencial

**Antipatrones sin cuantificar:** 41 de 52 (79%) tienen impacto significativo pero requieren análisis case-by-case según contexto organizacional específico.

---

## §5. REFERENCIAS CRUZADAS KERNEL

**Patrones Mitigadores:**

- `APLICACION/A1_Patrones.md`: P01-P64 patterns completos
- `CORE/04_Delegacion.md`: Modos M1-M6 (mitiga AP25-AP30)
- `CORE/08_Crisis_Management.md`: P52 Crisis Governance (mitiga AP31-AP33)

**Diagnóstico:**

- `APLICACION/A3_Diagnostico.md`: Assessment tools, health score, readiness
- `APLICACION/A4_Implementacion.md` §0: Readiness Triage

**Observables & Thresholds:**

- `DOMINIOS/D2_Percepcion.md`: O1-O8, IN1-IN3, SO1-SO5
- `CORE/08_Crisis_Management.md` §2: H_Score thresholds crisis

**Dominios Especializados:**

- `DOMINIOS_ESPECIALIZADOS/E7_Enterprise_Technology.md` §10: Ejemplos AP41-AP43
- `DOMINIOS_ESPECIALIZADOS/E8_Intelligent_Data_AI_Systems.md` §11: Ejemplos AP44-AP50

**Decision Making:**

- `DOMINIOS/D3_Decision.md` §1: OKR Anti-Patrones adicionales (AP6-AP9 OKR-specific)
- `DOMINIOS/D3_Decision.md` §2.1: Cost of Delay como herramienta priorización

**Principios Fundamentales:**

- `CORE/00_Manifiesto.md` §3: Principios violados por antipatrones
- `CORE/01_Primitivos.md`: Building blocks (E1-E5), violaciones generan antipatrones

**Security:**

- P_SEC02 Zero Trust Architecture
- P_SEC03 Security as Code
- P_SEC04 Shift-Left Security
- P_SEC05 Incident Response Automation

**Customer Experience:**

- P_CX01 Flujo Valor Cliente
- P_CX02 Eventos como Señales CX
- P_CX03 Touchpoint Ownership Explícita

---

**Fin documento A2_Antipatrones.md v2.3.0**
