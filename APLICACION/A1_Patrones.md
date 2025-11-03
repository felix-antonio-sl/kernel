# A1_Patrones

**Versión:** 2.3.0 | **Estado:** Definitivo | **Audiencia:** Practitioners, Arquitectos, Security, Product/UX, Data/AI Engineers

---

## §1. TAXONOMÍA DE PATRONES

```yaml
Total: 72 patrones en 8 categorías ortogonales

Estructura:
  Base (P01-P56):           56 patrones fundamentales
  Especializados (P57-P72): 16 patrones dominio-específicos

Categorías:
  1. Estructurales (P01-P12):       Organización, equipos, roles
  2. Procesuales (P13-P20):         Workflows, coordinación, ceremonias
  3. Tecnológicos (P21-P28):        Arquitectura, infra, deployment
  4. Decisionales (P29-P36):        Strategy, prioritization, roadmaps
  5. IA_Base (P37-P50):             Automatización, ML, copilots
  6. Emergentes (P51-P56):          Crisis, orquestación, evolución
  7. Seguridad (P57-P61):           Defense, compliance, IR
  8. Datos_IA_Avanzado (P62-P72):   Data products, RAG, multi-agent, CX

Renumeración (v2.3.0):
  # Consolidación para eliminar esquemas múltiples
  P_SEC01-05 → P57-P61  (Seguridad)
  P57-P64    → P62-P69  (Datos/IA/Procesos)
  P_CX01-03  → P70-P72  (Customer Experience)

Evolución:
  v1.0:   50 patrones base (P01-P50)
  v1.1:   +3 emergentes (P51-P53)
  v1.4:   +3 desarrollo evolutivo (P54-P56)
  v2.1:   +5 seguridad (P_SEC01-05 → P57-P61)
  v2.2:   +3 customer experience (P_CX01-03 → P70-P72)
  v2.2.1: +7 datos/IA, +1 multi-tenant (P57-P64 → P62-P69)
  v2.3.0: Renumeración unificada, taxonomía ortogonal
```

---

## §2. PATRONES ESTRUCTURALES (P01-P12)

**Propósito**: Diseño organizacional que habilita entrega de valor. Aplica Inverse Conway (P06) para alinear estructura con arquitectura target.

**Primitivos KERNEL**: Actor (A1-A3 roles), Límite (L1 boundaries organizacionales), Flujo (F1 coordinación)

| ID | Nombre | Problema | Solución | Cuándo Usar | Evitar Si |
|---|---|---|---|---|---|
| **P01** | **Feature Teams** | Silos funcionales causan handoffs | Teams cross-functional E2E ownership | Org 20-200, producto digital, velocity crítico | Especialización profunda requerida |
| **P02** | **Platform Teams** | Product teams reinventan infra | Platform teams construyen productos internos self-service | >5 product teams, infra compartida compleja | Org <50 personas |
| **P03** | **Two-Pizza Teams** | Teams grandes → overhead O(n²) | Max 5-9 personas por team, split si >9 | Escala >50, velocity crítico | Trabajo requiere >9 skills distintas |
| **P04** | **Guilds & Chapters** | Feature teams → silos conocimiento | Squads (delivery) + Chapters (expertise) + Guilds (comunidad) | Org 100-500, need expertise + delivery | Org <100 o cultura inmadura |
| **P05** | **Enabling Teams** | Teams luchan con nueva tech | Experts temporales enseñan (no hacen), 8-12 semanas | Adoption nueva tech, upskilling | Dependencia permanente aceptable |
| **P06** | **Inverse Conway** | Org actual no soporta arquitectura target | Diseñar org para forzar arquitectura deseada | Migration deliberada (monolito→microservices) | No tienes mandate C-level |
| **P07** | **Business-within-Business** | Dependencies cross-stream ralentizan | Mini-empresas autónomas E2E + platforms compartidas | >200 personas, value streams independientes | Value streams altamente acoplados |
| **P08** | **Federated Model** | Central vs Local tension global | Central: Strategy/governance, Geo: Execution/hiring | Org >500, múltiples geos, needs locales difieren | Single geography |
| **P09** | **Product Trios** | PM solo decide → suboptimal | PM + Eng Lead + Design Lead co-own roadmap | Product-led growth, discovery intenso | Decisiones deben ser muy rápidas |
| **P10** | **SRE Model** | Dev features vs Ops firefighting perpetuo | SRE: 50% automation, 50% toil; error budget balancea | Sistemas críticos 99.9%+, escala >100K users | No tienes SREs seniors |
| **P11** | **Squad-Chapter Matrix** | Autonomía sin expertise profundo | Matrix: Squads (delivery) con Chapters (functional expertise) | 50-500 personas, need both velocity + quality | <50 personas o >500 |
| **P12** | **Pods Rotacionales** | Expertise profundo + flexibility | 3-5 expertos ultra-especializados rotan entre pods | Producto premium, org pequeña elite | Org >100 o turnover alto |

---

## §3. PATRONES PROCESUALES (P13-P20)

**Propósito**: Optimizar flujo de trabajo mediante WIP limits, ceremonies y discovery. Implementa Principio P4 (Flujo Continuo).

**Primitivos KERNEL**: Flujo (F2 workflow), Límite (L2 WIP limits), Estado (ST1 work items)

| ID | Nombre | Problema | Solución | Cuándo Usar | Evitar Si |
|---|---|---|---|---|---|
| **P13** | **Dual-Track Agile** | Features nadie usa (no discovery) | Track 1: Discovery (PM/Design), Track 2: Delivery (Eng), parallel | Product teams maduros, B2C, discovery crítico | Resources limitados |
| **P14** | **Value Stream Mapping** | No sabemos dónde están bottlenecks | Mapear flujo completo, medir wait time cada paso | Cycle time alto (>7 días), muchos handoffs | Proceso ya optimizado |
| **P15** | **WIP Limits Kanban** | Context switching, cycle time alto | Límite explícito items "In Progress" por columna/persona | Flow continuo, trabajo impredecible >40% | Trabajo 100% planificado |
| **P16** | **Scrumban Híbrido** | Scrum rígido O Kanban sin estructura | Sprints + ceremonies Scrum + WIP limits Kanban | Teams maduros, mix planificado/reactivo 60/40 | Team nuevo necesita estructura pura |
| **P17** | **Mob Programming** | Knowledge silos, bus factor alto | 3-5 personas trabajan simultáneamente mismo código | Problema complejo novel, upskilling, bus factor crítico | Tareas rutinarias o independientes |
| **P18** | **Spike Time-Boxed** | Incertidumbre técnica bloquea decisión | Time-box 2-5 días para explorar, deadline forzado | Alta incertidumbre, múltiples alternativas | Ya sabes cómo implementar |
| **P19** | **Backlog Refinement Continuo** | Backlog desactualizado en planning | Weekly refinement session 1hr, groom próximos 3 sprints | Scrum teams, backlog >50 items | Kanban puro |
| **P20** | **Retrospectiva Accionable** | Retros sin cambio real | Max 3 action items, assign owner, review next retro | Toda metodología ágil | No hay commitment hacer cambios |

---

## §4. PATRONES TECNOLÓGICOS (P21-P28)

**Propósito**: Arquitectura técnica resiliente y evolutiva. Habilita deployment continuo y separación deploy/release.

**Primitivos KERNEL**: Recurso (R2-R3 infra/datos), Límite (L2-L3 constraints técnicos), Evento (E1 deployment events)

| ID | Nombre | Problema | Solución | Cuándo Usar | Evitar Si |
|---|---|---|---|---|---|
| **P21** | **Strangler Fig Migration** | Big-bang rewrite riesgoso | Migración incremental: nuevo sistema rodea legacy, replacement gradual | Legacy monolito crítico, no puedes parar | Greenfield project |
| **P22** | **Circuit Breaker** | Cascading failures dependencies | Auto-detecta fallas dependency, circuit abierto evita llamadas | Microservices, dependencias externas críticas | Monolito sin dependencies |
| **P23** | **Feature Flags** | Deploy ≠ Release, rollback lento | Deploy código disabled, activate remotamente, A/B test, rollback instant | Despliegue continuo, A/B testing, canary | Overhead config no justificado |
| **P24** | **Blue-Green Deployment** | Rollback deployment lento | Dos entornos idénticos, switch instantáneo | Downtime 0 requerido, rollback <1 min crítico | Infra cost prohibitivo (2x) |
| **P25** | **Database per Service** | Microservices comparten DB → coupling | Cada microservice ownership DB propia | Microservices true independence, escala diferenciada | Necesitas transactions cross-service |
| **P26** | **API Gateway Pattern** | Clients hablan N microservices → complejidad | Single entry point (gateway), routing, auth, rate limit centralizados | Microservices >5, múltiples clients | Monolito o 1-2 services |
| **P27** | **Event Sourcing** | Estado actual sin historia, debugging difícil | Store events (no state final), rebuild state replaying events | Audit trail crítico, temporal queries necesarios | CRUD simple suficiente |
| **P28** | **CQRS** | Read/Write mixed → optimization difícil | Separate models: Write optimized differently than Read | High read:write ratio (100:1+), complex queries | Read:write ratio balanceado |

---

## §5. PATRONES DECISIONALES (P29-P36)

**Propósito**: Frameworks para priorización objetiva y portfolio management. Reduce política, maximiza ROI.

**Primitivos KERNEL**: Dato (D1 métricas), Decisión (modo M2-M3), Límite (L1 constraints portfolio)

| ID | Nombre | Problema | Solución | Cuándo Usar | Evitar Si |
|---|---|---|---|---|---|
| **P29** | **OKRs Bottom-Up** | Top-down goals no ownership | Teams proponen OKRs, alignment via negotiation | Org >50, autonomía teams alta | Startup <20, need strong direction |
| **P30** | **Capability-Based Roadmap** | Project-based planning → no evolution continua | Roadmap por capabilities (evolucionan), no projects (terminan) | Asset thinking, producto continuo | Projects realmente discretos |
| **P31** | **RICE Scoring** | Priorización subjetiva, politics | Score = (Reach × Impact × Confidence) / Effort, rank descending | Backlog >30 items, need objective prioritization | Factors cualitativos críticos |
| **P32** | **Time-Value Profiles** | No consideras cuándo se captura valor | Classify initiatives: SPIKE/STEP/GROWTH/DELAYED, portfolio mix | Portfolio planning, value timing crítico | Todos initiatives similar profile |
| **P33** | **WSJF** | Priorización ignora cost of delay | Score = (Business Value + Time Criticality + Risk) / Job Size | SAFe, Lean portfolio management | Todos items similar urgencia |
| **P34** | **North Star Metric** | Múltiples métricas → dilución focus | Single metric empresa optimiza (ej: Weekly Active Users) | Product-led growth, need alignment | Negocio multi-faceted no reducible |
| **P35** | **Preparación R1-R5** | Transformación falla por no preparar | Score 5 dimensiones (Momentum, Capabilities, Forces, Drivers, Catalysts), go/no-go | Cambio mayor (>6 meses, >$500K), riesgo alto | Cambio pequeño reversible |
| **P36** | **Portfolio Balancing** | Solo short-term O solo long-term bets | 70% Core (STEP), 20% Adjacent (GROWTH), 10% Transformational (DELAYED) | Portfolio >5 initiatives, horizons 1-2-3 | Startup pre-PMF (100% core) |

---

## §6. PATRONES IA BASE (P37-P50)

**Propósito**: Delegación cognitiva humano-IA mediante Modes M2-M6. Ver `CORE/04_Delegacion.md` para fundamentos.

**Primitivos KERNEL**: Actor (A3 agente), Dato (D1 training data), Señal (S1-S2 alertas/predictions), Límite (L2 autonomy boundaries)

| ID | Nombre | Problema | Solución | Cuándo Usar | Evitar Si |
|---|---|---|---|---|---|
| **P37** | **Copilot Coding (M3)** | Boilerplate code lento | IA genera código bajo demanda, humano revisa | Tareas coding rutinarias, languages popular | Código crítico seguridad |
| **P38** | **Anomaly Detection (M2)** | Humano no detecta patterns anomalías en tiempo real | ML detecta spikes/dips, alerta automática | Datos masivos (>1M events/día), patterns sutiles | Datos <1K events/día |
| **P39** | **Churn Prediction (M2)** | React a churn post-facto | ML predice churn 30 días anticipado, proactive outreach | >1K customers, histórico 12+ meses | <100 customers |
| **P40** | **Sentiment Analysis (M2)** | Manual review NPS comments imposible escala | LLM analiza text feedback, categoriza sentiments | >100 responses/día, qualitative insights críticos | <50 responses/día |
| **P41** | **Auto-Prioritization Backlog (M4)** | Backlog prioritization manual consume tiempo PM | Reglas defined, agente rankea automático, humano ajusta excepciones | Backlog >100 items, reglas claras | Reglas cambian constantemente |
| **P42** | **Quality Gates Automated (M4)** | Manual code review bottleneck | CI/CD auto-rechaza si coverage <80%, vulns high, tests fail | Deploy frequency >daily, quality non-negotiable | Team <5, low volume commits |
| **P43** | **Auto-Scaling Infra (M6)** | Manual scaling lento, over/under-provisioned | Reglas CPU/memory → auto-scale instances | Tráfico variable (>2x swing), cloud-native | Traffic predictable |
| **P44** | **Auto-Rollback (M6)** | Deploy bad code, manual rollback 30+ min | Monitor error_rate/latency, auto-rollback si threshold | Despliegue continuo, MTTR <5 min crítico | No tienes monitoring robusto |
| **P45** | **Chatbot FAQ (M4)** | Support agents responden FAQs repetitivas | LLM responde FAQs, escalate a humano si confidence <70% | >50 tickets/día FAQ, knowledge base existe | FAQ muy dinámicos |
| **P46** | **Pair Programming IA (M5)** | Complex problems, humano + IA complementarios | Humano diseña approach, IA implementa, humano revisa, iterate | Problema novel, neither humano ni IA puede solo | Problema trivial o muy complejo |
| **P47** | **Portfolio Optimizer (M2)** | Multi-objective optimization manual suboptimal | IA optimiza valor/riesgo/costo constraints, humano ajusta weights | Portfolio >10 initiatives, constraints múltiples | Portfolio <5 initiatives |
| **P48** | **Root Cause Analysis Auto (M2)** | RCA manual post-incident consume horas | IA correlaciona logs/metrics/events, sugiere root cause | >100K events/día, incidents frecuentes | Incidents <1/mes |
| **P49** | **Documentation Auto-Generate (M3)** | Docs desactualizados, nadie escribe | IA genera docs desde código/comments, humano revisa | Codebase >50K LOC, turnover alto | Codebase <10K LOC |
| **P50** | **A/B Test Analyzer (M2)** | Análisis estadístico A/B test manual error-prone | IA calcula significance, detects early winners, recomienda stop | >10 A/B tests/mes, statistical rigor crítico | <2 tests/mes |

---

## §7. PATRONES EMERGENTES (P51-P56)

**Propósito**: Patrones identificados post-v1.0 basados en práctica operacional y fuentes fundacionales (Gall's Law, Alexander, Agile Manifesto).

**Primitivos KERNEL**: Combinaciones complejas multi-dominio (crisis governance, meta-agents, evolutionary design)

| ID | Nombre | Problema | Solución | Cuándo Usar | Evitar Si |
|---|---|---|---|---|---|
| **P51** | **Carry-Over Management** | Scrum rígido prohibe carry-over → stories artificialmente pequeñas | Permitir flujo entre sprints con governance (max 30-40% capacity, track age >3 sprints) | Teams maduros, dominios complejos (embedded, critical systems) | Work completable en sprint único |
| **P52** | **Crisis Governance** | Governance normal lento en crisis (H<45, any O<30 sustained) | Crisis team 5-7 personas, daily sync, decisions <4hrs critical, exit H>45 stable 3 months | Financial/Customer/Talent crisis, multiple observables <30 | H_Score >60, crisis artificial |
| **P53** | **Orchestration Agent** | N agents especializados sin coordinación → conflicts, inconsistencies | Meta-agent coordina: registry, delegation, intervention points, conflict resolution | Sistema ≥3 agents, collaboration needed, user needs unified interface | Single agent suffices, overhead > benefit |
| **P54** | **Piecemeal Growth** | Big bang design → fracaso (Gall's Law: complex system designed from scratch never works) | Sistema simple funcional → crecer incrementalmente con stable intermediate forms | Todo sistema complejo (>3 meses), alta incertidumbre | Sistema trivial (<4 semanas) |
| **P55** | **Walking Skeleton** | Integration risk descubierto tarde (mes 6+ en vez de week 1) | Build versión mínima E2E (todas capas, 1 feature trivial) para validar arquitectura | Proyecto greenfield, arquitectura no validada, multiple layers | Arquitectura probada, single layer |
| **P56** | **Continuous Refactoring** | Design upfront especulativo → rigidez o inadecuado cuando realidad conocida | Design emerge de refactoring post-código funcional (TDD cycle, Boy Scout Rule) | Codebase evolutionary, tech debt managed proactively | Codebase frozen, no tests |

**Referencias Detalladas**:
- **P51**: `DOMINIOS/D4_Operacion.md` §7.1 (metrics: Carry-Over Rate, Completion Rate, Yellow Cards)
- **P52**: `CORE/08_Crisis_Management.md` (activation triggers, decision protocols, exit criteria, case studies)
- **P53**: Ejemplos concretos en `DOMINIOS_ESPECIALIZADOS/E8_Intelligent_Data_AI_Systems.md` §5.6
- **P54-P56**: Fundamentos en `DOMINIOS/D4_Operacion.md` §11 (Continuous Learning, Gall's Law)

---

## §8. PATRONES SEGURIDAD (P57-P61)

**Propósito**: Security by design mediante defense-in-depth, zero trust y shift-left. Implementa observables SO1-SO5 (`D2_Percepcion.md` §8).

**Primitivos KERNEL**: Límite (L3 security boundaries), Señal (S2 security events), Recurso (R3 security controls)

| ID | Nombre | Problema | Solución | Cuándo Usar | Evitar Si |
|---|---|---|---|---|---|
| **P57** | **Defense in Depth** | Single security layer vulnerable | Múltiples capas defensa independientes (network, app, data, identity) | Org enterprise, alto impacto breach | Org <20 personas, low-risk data |
| **P58** | **Zero Trust Architecture** | Perimeter security insufficient | Verify explícitamente every access (never trust, always verify), least privilege | Remote workforce, cloud-native, high-value assets | Legacy systems no soportan auth granular |
| **P59** | **Security as Code** | Manual security configs error-prone, no versionados | Security policies, firewall rules, access controls en IaC (versionado, testeable) | DevOps maduro, multi-environment, compliance | Sin IaC básico |
| **P60** | **Shift-Left Security** | Security descubierta tarde → costoso fix (10-100× más caro en prod vs design) | Security integrado desde design: threat modeling, SAST/DAST en CI/CD | Deploy frequency >semanal, regulated industry | Security team inexistente |
| **P61** | **Incident Response Automation** | Manual IR lento (MTTD >24hrs, MTTC >24hrs) | SOAR platform: automated detection (SIEM), containment playbooks | >5 incidents/mes, 24/7 operations | <1 incident/trimestre |

**Impacto Observables**:

| Pattern | Observable Mejorado | Impacto Típico |
|---------|---------------------|----------------|
| P57 | SO1 Vulnerabilities, SO5 IR | MTTP -40%, MTTC -50% |
| P58 | SO3 Access Control, SO2 Secrets | Breach risk -70%, over-provisioning -60% |
| P59 | SO4 Compliance, SO1 Vulnerabilities | Audit findings -50%, config drift 0% |
| P60 | SO1 Vulnerabilities, SO5 IR | Vulnerabilities found design -80% cost |
| P61 | SO5 IR | MTTD -70% (<1hr), MTTC -65% (<4hrs) |

---

## §9. PATRONES DATOS/IA AVANZADO (P62-P72)

**Propósito**: Data-as-Product, RAG auditable, process automation, multi-agent orchestration y customer experience. Ver `DOMINIOS_ESPECIALIZADOS/E8_Intelligent_Data_AI_Systems.md` para casos concretos.

**Primitivos KERNEL**: Dato (D2 contracts), Actor (A3 agents), Flujo (F3 pipelines complejos), Límite (L1-L3 governance)

| ID | Nombre | Problema | Solución | Cuándo Usar | Evitar Si |
|---|---|---|---|---|---|
| **P62** | **Data Product** | Datos subproducto → Calidad baja, no reusable, undiscoverable | Treat data as product: Contract (schema, SLO, DQ), Owner, Lineage, Serving | Multi-team org, data reuse alto, compliance | Single-team app, data uso único |
| **P63** | **RAG Auditable** | LLMs alucinan, no citan → No confiables, compliance risk | RAG: Curation + Hybrid index + Mandatory citations (exactness ≥0.95) | Legal, medical, gov (high-authority domains) | Creative content, brainstorming |
| **P64** | **Saga Compensation** | Transacción distribuida → Partial failures, inconsistency | Orchestrated saga: Forward + Compensation steps idempotent, BPMN engine | Distributed transactions, eventual consistency OK | Single DB (use ACID) |
| **P65** | **HITL Checkpoint** | Full automation high-stakes → Errors costosos, compliance risk | Pause workflow + human decision + resume (triggers: confidence <0.85, $>10K) | High-stakes (financial, medical, legal) | Low-risk, AI confidence >0.95 |
| **P66** | **Multi-Agent Orchestration** | Single agent limitado (capabilities, context window) | Router/Supervisor coordinates specialized agents (domain-experts) | Multi-domain queries, task decomposition beneficial | Simple queries, single-domain |
| **P67** | **Contract-Driven Evolution** | Schema changes break consumers silently → Production outages | Semver + Backward compat + Deprecation windows (90-120 días coexist v1+v2) | Shared data/APIs, multiple consumers | Internal single-team |
| **P68** | **Hybrid Search** | Keyword misses semantic, vector misses exact → Suboptimal recall/precision | BM25 + Vector + Reranking + ACL filters (dual index, fusion) | Heterogeneous corpus, diverse query styles | Homogeneous corpus |
| **P69** | **Multi-Tenant Architecture** | Single-tenant → Cost prohibitivo ($500-$5K/tenant), scaling impossible | Shared infra + isolation (Levels 1-4) + per-tenant config | >5 tenants, requirements similar (80%+ overlap) | <3 tenants, highly heterogeneous |
| **P70** | **Flujo Valor Cliente** | Org diseña inside-out → No fit customer needs | Mapear Flujo F completo, instrumentar O2 (valor) por touchpoint (outside-in) | B2C, B2B múltiples touchpoints, NPS <30 | B2B simple (1 touchpoint) |
| **P71** | **Eventos como Señales CX** | Customer friction invisible → Reactive fixes | Friction points → Señales S explícitas, alertas proactivas threshold violated | Digital products, journey complejo (>5 pasos), churn >15% | Offline sin telemetry |
| **P72** | **Touchpoint Ownership** | Nadie responsible E2E → Handoff hell, blame game | Actor A2 owner por touchpoint crítico, RACI, dashboards O2 (NPS/CSAT) | Product-led growth, multi-team, complaints >50/mes | Single team, touchpoints <3 |

**Referencias Detalladas**:
- **P62-P69**: `DOMINIOS_ESPECIALIZADOS/E8_Intelligent_Data_AI_Systems.md` §3-§7 (ejemplos billing_invoices, RAG normativa, invoice pipeline)
- **P69 Multi-Tenant**: Decision tree isolation levels (L1 Shared Everything → L4 Dedicated Infra), H_Score per-tenant, noisy neighbor mitigation
- **P70-P72 CX**: Diferencia vs Design Thinking tradicional (cuantitativo vs cualitativo, instrumentado vs manual)

**Templates Asociados**:
- **T15_Contrato_Datos.yaml**: P62, P67 (data contracts, schema evolution)
- **T17_Contrato_Agente.yaml**: P65, P66 (HITL section, multi-agent coordination)
- **T18_Contrato_Conocimiento.yaml**: P63, P68 (RAG indexing, hybrid search)
- **T16_Contrato_Proceso.yaml**: P64 (BPMN saga compensation)

---

## §10. MATRIZ PATRONES × DOMINIOS

**Leyenda**: ✅✅✅ Primario | ✅✅ Secundario | ◐ Terciario | — No aplica

| Categoría | Arquitectura (D1) | Percepción (D2) | Decisión (D3) | Operación (D4) |
|-----------|-------------------|-----------------|---------------|----------------|
| P01-P12 (Estructurales) | ✅✅✅ | ◐ | ◐ | ◐ |
| P13-P20 (Procesuales) | ◐ | ◐ | ◐ | ✅✅✅ |
| P21-P28 (Tecnológicos) | ✅✅ | — | — | ✅✅✅ |
| P29-P36 (Decisionales) | — | ◐ | ✅✅✅ | ◐ |
| P37-P50 (IA Base) | ◐ | ✅✅ | ✅✅ | ✅✅✅ |
| P51-P56 (Emergentes) | ✅✅ | ✅✅ | ✅✅ | ✅✅✅ |
| P57-P61 (Seguridad) | ✅✅ | ✅✅✅ | ◐ | ✅✅✅ |
| P62-P72 (Datos/IA/CX) | ✅✅ | ✅✅✅ | ✅✅ | ✅✅✅ |

**Notas**:
- **Seguridad**: Transversal. D2 primario (observables SO1-SO5), D1/D4 secundarios (design + execution)
- **Emergentes**: Multi-dominio por naturaleza (crisis governance afecta D1-D4, orchestration agent es meta-level)
- **Datos/IA/CX**: D2 primario (instrumentación valor, telemetry), D4 secundario (execution), D1/D3 secundarios (architecture + roadmap)

---

## §11. TRAZABILIDAD DETALLADA PATTERNS SELECCIONADOS

**Propósito**: Mapeo explícito dominio primario y primitivos involucrados para patterns representativos de cada categoría.

| ID | Nombre | Dominio Primario | Primitivos Involucrados |
|---|---|---|---|
| **P01** | Feature Teams | D1 Arquitectura | A1 (Actor: team cross-functional), L1 (Límite: team boundary E2E) |
| **P15** | WIP Limits Kanban | D4 Operación | L2 (Límite: WIP per column), F2 (Flujo: work items) |
| **P23** | Feature Flags | D4 Operación | R1 (Recurso: feature toggle config), L2 (Límite: activation control) |
| **P31** | RICE Scoring | D3 Decisión | D1 (Dato: métricas RICE), F2 (Flujo: scoring process) |
| **P38** | Anomaly Detection | D2 Percepción | D1 (Dato: events stream), E1 (Evento: anomaly), S1 (Señal: alert), A3 (Actor: ML agent M2) |
| **P41** | Auto-Prioritization | D3 Decisión | D1 (Dato: backlog metadata), A3 (Actor: agent M4), L1 (Límite: reglas prioritization) |
| **P44** | Auto-Rollback | D4 Operación | E1 (Evento: error threshold), A3 (Actor: rollback agent M6), L2 (Límite: error budget SLO) |
| **P52** | Crisis Governance | Multi-dominio | ST1 (Estado: H_Score crisis), A1 (Actor: crisis team), F1 (Flujo: daily sync), L1 (Límite: decision protocols) |
| **P53** | Orchestration Agent | D4 Operación | A3 (Actor: orchestrator meta-level), F3 (Flujo: coordination), S2 (Señal: escalations), L2 (Límite: delegation policies) |
| **P62** | Data Product | D1 Arquitectura | D2 (Dato: contract), A2 (Actor: data product owner), R3 (Recurso: lakehouse), L1 (Límite: SLO) |
| **P70** | Flujo Valor Cliente | D2 Percepción | F1 (Flujo: customer journey), R1 (Recurso: touchpoints), O2 (Observable: valor entregado) |

**Nota**: Patterns no listados tienen trazabilidad implícita vía §10 Matriz Patrones × Dominios.

---

## §12. COMBINACIONES DE PATRONES

### Combo 1: Startup Scaling (20→100 personas)

```yaml
Stack:
  - P01 (Feature Teams) - Estructura base
  - P03 (Two-Pizza) - Límite tamaño
  - P13 (Dual-Track) - Discovery + Delivery
  - P23 (Feature Flags) - Deploy continuo
  - P29 (OKRs Bottom-Up) - Alignment
  - P37 (Copilot) - Velocity código

Resultado: Velocity 2-3× baseline, H_Score >80
Timeline: 6-12 meses implementación progresiva
```

### Combo 2: Legacy Modernization

```yaml
Stack:
  - P06 (Inverse Conway) - Reorg para microservices
  - P21 (Strangler Fig) - Migration incremental
  - P23 (Feature Flags) - A/B old vs new
  - P35 (R1-R5) - Preparación transformación
  - P54 (Piecemeal Growth) - Stable intermediate forms

Resultado: Migration 12-18 meses, downtime <1hr total
Antipatrón Mitigado: AP15 (Big Bang Rewrite)
```

### Combo 3: Platform Engineering Excellence

```yaml
Stack:
  - P02 (Platform Teams) - Infra como producto
  - P10 (SRE) - Reliability + automation
  - P22 (Circuit Breaker) - Resilience
  - P24 (Blue-Green) - Deployment safety
  - P43 (Auto-Scaling) - Efficiency
  - P44 (Auto-Rollback) - MTTR <5 min

Resultado: Uptime 99.95%+, Deploy frequency >10×/día
```

### Combo 4: Product-Led Growth

```yaml
Stack:
  - P09 (Product Trios) - Discovery excellence
  - P13 (Dual-Track) - Build only validated
  - P31 (RICE Scoring) - Objective prioritization
  - P34 (North Star Metric) - Alignment total
  - P39 (Churn Prediction) - Retention proactiva
  - P50 (A/B Analyzer) - Data-driven iterations
  - P70-P72 (CX Patterns) - Outside-in instrumentation

Resultado: Activation rate +40%, Churn -60%
```

### Combo 5: Data/AI Platform

```yaml
Stack:
  - P62 (Data Product) - Contracts, ownership, lineage
  - P63 (RAG Auditable) - Citations mandatory
  - P66 (Multi-Agent) - Specialized domain agents
  - P67 (Contract-Driven) - Schema evolution governance
  - P68 (Hybrid Search) - BM25 + Vector fusion
  - P69 (Multi-Tenant) - Isolation + shared infra

Resultado: Data reuse 5×, AI accuracy >95%, Cost per tenant -70%
```

---

## §13. ADOPCIÓN PROGRESIVA

### Fase 1: Fundamentos (Meses 1-3)

```yaml
Esenciales:
  - P01 o P03: Estructura teams
  - P29: OKRs básicos
  - P23: Feature flags
  - P42: Quality gates CI/CD

Criterio_Exit: H_Score >60, Velocity stable 3 sprints
Risk: Bajo, Quick wins visibles
```

### Fase 2: Optimización (Meses 4-9)

```yaml
Mejoras (requiere Fase 1 exitosa):
  - P13: Dual-track agile
  - P31: RICE scoring
  - P37: Copilot coding
  - P38: Anomaly detection
  - P70-P72: CX instrumentation

Criterio_Exit: H_Score >70, Customer satisfaction >75
Risk: Medio, Requiere madurez cultural
```

### Fase 3: Avanzado (Meses 10-18)

```yaml
Transformacionales:
  - P06: Inverse Conway (si reorg necesaria)
  - P10: SRE model
  - P21: Strangler fig (si legacy)
  - P46-P47: IA colaborativa avanzada
  - P62-P69: Data/AI platform patterns

Criterio_Exit: H_Score >80, Capabilities strategic automated
Risk: Alto, Alto impacto, Requiere executive sponsorship
```

---

## §14. ANTIPATRONES RELACIONADOS

**Ver**: `APLICACION/A2_Antipatrones.md` para patologías detalladas que estos patrones mitigan.

**Mapeo Común**:

| Antipatrón | Patterns Mitigadores | Mecanismo |
|------------|---------------------|-----------|
| AP02 (Transformación sin preparar) | P35 (R1-R5), P52 (Crisis Governance) | Assessment readiness, governance adaptativo |
| AP05 (Silos funcionales) | P01 (Feature Teams), P06 (Inverse Conway) | Cross-functional ownership E2E |
| AP12 (Top-down sin ownership) | P29 (OKRs Bottom-Up), P09 (Product Trios) | Negotiated alignment, co-ownership |
| AP15 (Big Bang Rewrite) | P21 (Strangler Fig), P54 (Piecemeal Growth) | Incremental migration, stable forms |
| AP18 (Deploy = Release) | P23 (Feature Flags), P24 (Blue-Green) | Decouple deploy/release, instant rollback |
| AP31 (Crisis Artificial) | P52 (Crisis Governance) | Exit criteria explicit (H>45 stable 3 months) |
| AP37 (Data Sin Contrato) | P62 (Data Product), P67 (Contract-Driven) | Schema contracts, SLO, deprecation governance |
| AP38 (RAG Sin Curation) | P63 (RAG Auditable) | Authority validation, mandatory citations |
| AP39 (Observabilidad Mínima IA) | P65 (HITL Checkpoint), P38 (Anomaly Detection) | Confidence monitoring, human-in-loop |
| AP41 (Dual Write) | P64 (Saga Compensation) | Orchestrated compensation idempotent |

---

## §15. REFERENCIAS CRUZADAS

**Documentos Core**:
- **Primitivos**: `CORE/01_Primitivos.md` (Actor, Dato, Flujo, Señal, Límite, Recurso, Estado)
- **Ciclo SDA**: `CORE/02_Ciclo_Fundamental.md` (Sense → Decide → Act)
- **Principios**: `CORE/00_Manifiesto.md` (P1-P7 fundacionales)
- **Delegación**: `CORE/04_Delegacion.md` §8 (Modes M1-M6, Purpose Orchestration)
- **Crisis**: `CORE/08_Crisis_Management.md` (P52 consolidado completo)

**Dominios**:
- **D1 Arquitectura**: `DOMINIOS/D1_Arquitectura.md` (Patterns estructurales P01-P12)
- **D2 Percepción**: `DOMINIOS/D2_Percepcion.md` §4 (H_Score), §8 (SO1-SO5 Security Observables)
- **D3 Decisión**: `DOMINIOS/D3_Decision.md` §6 (Decision Modes 1-6)
- **D4 Operación**: `DOMINIOS/D4_Operacion.md` §7.1 (Carry-Over), §11 (Continuous Learning), §12 (Execution Levels)

**Especializados**:
- **E8 Intelligent Data/AI Systems**: `DOMINIOS_ESPECIALIZADOS/E8_Intelligent_Data_AI_Systems.md` (P62-P69 ejemplos concretos, casos billing_invoices, RAG normativa, invoice pipeline)

**Templates**:
- **OKR/Roadmap**: `REFERENCIA/R6_Templates/T01_OKR.md`, `T10_Roadmap_Capability.yaml`
- **Contratos**: `T15_Contrato_Datos.yaml`, `T16_Contrato_Proceso.yaml`, `T17_Contrato_Agente.yaml`, `T18_Contrato_Conocimiento.yaml`
- **Specs**: `T19_App_Inventory.yaml`, `T20_Data_Product_Spec.yaml`, `T22_Process_Model_BPMN.yaml`

**Antipatrones**: `APLICACION/A2_Antipatrones.md` (AP01-AP52 patologías organizacionales/técnicas)

---

## Cambios v2.3.0

```yaml
Breaking_Changes:
  - Renumeración patterns especializados para taxonomía unificada
  - P_SEC01-05 → P57-P61 (Seguridad)
  - P57-P64 (Datos/IA v2.2.1) → P62-P69
  - P_CX01-03 → P70-P72 (Customer Experience)

Improvements:
  - Taxonomía ortogonal 8 categorías (vs 6+ ad-hoc)
  - Formato tabular consistente (vs mix tablas/YAML extenso)
  - Referencias cruzadas explícitas (vs contenido duplicado)
  - Trazabilidad primitivos KERNEL por pattern
  - Combinaciones patterns por use case
  - Roadmap adopción progresiva 3 fases

Deprecated:
  - Ejemplos verbosos inline (movidos a E8_Intelligent_Data_AI_Systems.md)
  - P64 Multi-Tenant como standalone (consolidado contexto P62-P69)

Migration_Guide:
  - Actualizar referencias P_SEC* → P57-P61
  - Actualizar referencias P_CX* → P70-P72
  - Ver E8 para ejemplos detallados P62-P69
```

---

**Fin del documento. Total: 72 patrones en estructura ortogonal, mínima y trazable.**