# A1_Patrones

**Versión:** 1.1.0 | **Estado:** Definitivo | **Audiencia:** Practitioners, Arquitectos

---

## §1. TAXONOMÍA DE PATRONES

```yaml
Total: 56 patrones (50 base + 3 emergentes v1.1 + 3 refactored v1.4)

Categorías_Base (v1.0):
  - Estructurales (P01-P12): Organización, equipos, responsabilidades
  - Procesuales (P13-P20): Workflows, flujos, coordinación
  - Tecnológicos (P21-P28): Arquitectura técnica, infra, datos
  - Decisionales (P29-P36): Estrategia, roadmaps, planning
  - IA (P37-P50): Delegación, agentes, automatización

Patrones_Emergentes (v1.1):
  - P51: Carry-Over Management (§11)
  - P52: Crisis Governance (§12, consolidado CORE/08)
  - P53: Orchestration Agent (§13)

Patrones_Desarrollo_Evolutivo (v1.4):
  - P54: Piecemeal Growth (§14 - refactored desde D4)
  - P55: Walking Skeleton (§14 - refactored desde D4)
  - P56: Continuous Refactoring (§14 - refactored desde D4)
```

---

## §2. PATRONES ESTRUCTURALES (P01-P12)

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

| ID | Nombre | Problema | Solución | Cuándo Usar | Evitar Si |
|---|---|---|---|---|---|---|
| **P21** | **Strangler Fig Migration** | Big-bang rewrite riesgoso | Migración incremental: nuevo sistema rodea legacy, replacement gradual | Legacy monolito crítico, no puedes parar | Greenfield project |
| **P22** | **Circuit Breaker** | Cascading failures dependencies | Auto-detecta fallas dependency, circuit abierto evita llamadas | Microservices, dependencias externas críticas | Monolito sin dependencies |
| **P23** | **Feature Flags** | Deploy ≠ Release, rollback lento | Deploy código disabled, activate remotamente, A/B test, rollback instant | Despliegue continuo, A/B testing, canary | Overhead config no justificado |
| **P24** | **Blue-Green Deployment** | Rollback deployment lento | Dos entornos idénticos, switch instantáneo | Downtime 0 requerido, rollback <1 min crítico | Infra cost prohibitivo (2x) |
| **P25** | **Database per Service** | Microservices comparten DB → coupling | Cada microservice ownership DB propia | Microservices true independence, escala diferenciada | Necesitas transactions cross-service |
| **P26** | **API Gateway Pattern** | Clients hablan N microservices → complejidad | Single entry point (gateway), routing, auth, rate limit centralizados | Microservices >5, múltiples clients | Monolito o 1-2 services |
| **P27** | **Event Sourcing** | Estado actual sin historia, debugging difícil | Store events (no state final), rebuild state replaying events | Audit trail crítico, temporal queries necesarios | CRUD simple suficiente |
| **P28** | **CQRS (Command Query Separation)** | Read/Write mixed → optimization difícil | Separate models: Write optimized differently than Read | High read:write ratio (100:1+), complex queries | Read:write ratio balanceado |

---

## §5. PATRONES DECISIONALES (P29-P36)

| ID | Nombre | Problema | Solución | Cuándo Usar | Evitar Si |
|---|---|---|---|---|---|---|
| **P29** | **OKRs Bottom-Up** | Top-down goals no ownership | Teams proponen OKRs, alignment via negotiation | Org >50, autonomía teams alta | Startup <20, need strong direction |
| **P30** | **Capability-Based Roadmap** | Project-based planning → no evolution continua | Roadmap por capabilities (evolucionan), no projects (terminan) | Asset thinking, producto continuo | Projects realmente discretos |
| **P31** | **RICE Scoring** | Priorización subjetiva, politics | Score = (Reach × Impact × Confidence) / Effort, rank descending | Backlog >30 items, need objective prioritization | Factors cualitativos críticos |
| **P32** | **Time-Value Profiles** | No consideras cuándo se captura valor | Classify initiatives: SPIKE/STEP/GROWTH/DELAYED, portfolio mix | Portfolio planning, value timing crítico | Todos initiatives similar profile |
| **P33** | **WSJF (Weighted Shortest Job First)** | Priorización ignora cost of delay | Score = (Business Value + Time Criticality + Risk) / Job Size | SAFe, Lean portfolio management | Todos items similar urgencia |
| **P34** | **North Star Metric** | Múltiples métricas → dilución focus | Single metric empresa optimiza (ej: Weekly Active Users) | Product-led growth, need alignment | Negocio multi-faceted no reducible |
| **P35** | **Preparación R1-R5** | Transformación falla por no preparar | Score 5 dimensiones (Momentum, Capabilities, Forces, Drivers, Catalysts), go/no-go decision | Cambio mayor (>6 meses, >$500K), riesgo alto | Cambio pequeño reversible |
| **P36** | **Portfolio Balancing** | Solo short-term O solo long-term bets | 70% Core (STEP), 20% Adjacent (GROWTH), 10% Transformational (DELAYED) | Portfolio >5 initiatives, horizons 1-2-3 | Startup pre-PMF (100% core) |

---

## §6. PATRONES IA (P37-P50)

| ID | Nombre | Problema | Solución | Cuándo Usar | Evitar Si |
|---|---|---|---|---|---|---|
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

## §7. MATRIZ PATRONES × DOMINIOS

| Patrón | Arquitectura | Percepción | Decisión | Operación |
|--------|-------------|------------|----------|-----------|
| **P01-P12 (Estructurales)** | ✅✅✅ | ◐ | ◐ | ◐ |
| **P13-P20 (Procesuales)** | ◐ | ◐ | ◐ | ✅✅✅ |
| **P21-P28 (Tecnológicos)** | ◐ | — | — | ✅✅✅ |
| **P29-P36 (Decisionales)** | — | ◐ | ✅✅✅ | ◐ |
| **P37-P50 (IA)** | ◐ | ✅✅ | ✅✅ | ✅✅✅ |

**Leyenda:** ✅✅✅ Primario | ✅✅ Secundario | ◐ Terciario | — No aplica

---

## §8. COMBINACIONES DE PATRONES

### Combo 1: Startup Scaling (20→100 personas)

```yaml
Patrones:
  - P01 (Feature Teams) - Estructura base
  - P03 (Two-Pizza) - Límite tamaño
  - P13 (Dual-Track) - Discovery + Delivery
  - P23 (Feature Flags) - Deploy continuo
  - P29 (OKRs Bottom-Up) - Alignment
  - P37 (Copilot) - Velocity código

Resultado: Velocity 2-3× vs baseline, H_Score >80
```

---

### Combo 2: Legacy Modernization

```yaml
Patrones:
  - P06 (Inverse Conway) - Reorg para microservices
  - P21 (Strangler Fig) - Migration incremental
  - P23 (Feature Flags) - A/B old vs new
  - P35 (R1-R5) - Preparación transformación
  - P41 (Auto-Prioritization) - Backlog migration

Resultado: Migration 12-18 meses, downtime <1hr total
```

---

### Combo 3: Platform Engineering Excellence

```yaml
Patrones:
  - P02 (Platform Teams) - Infra como producto
  - P10 (SRE) - Reliability + automation
  - P22 (Circuit Breaker) - Resilience
  - P24 (Blue-Green) - Deployment safety
  - P43 (Auto-Scaling) - Efficiency
  - P44 (Auto-Rollback) - MTTR <5 min

Resultado: Uptime 99.95%+, Deploy frequency >10×/día
```

---

### Combo 4: Product-Led Growth

```yaml
Patrones:
  - P09 (Product Trios) - Discovery excellence
  - P13 (Dual-Track) - Build only validated
  - P31 (RICE Scoring) - Objective prioritization
  - P34 (North Star Metric) - Alignment total
  - P39 (Churn Prediction) - Retention proactiva
  - P50 (A/B Analyzer) - Data-driven iterations

Resultado: Activation rate +40%, Churn -60%
```

---

## §9. ADOPCIÓN PROGRESIVA

### Fase 1: Fundamentos (Meses 1-3)

```yaml
Esenciales (implementar primero):
  - P01 o P03: Estructura teams
  - P29: OKRs básicos
  - P23: Feature flags
  - P42: Quality gates CI/CD

Quick wins visibles, bajo riesgo
```

---

### Fase 2: Optimización (Meses 4-9)

```yaml
Mejoras (si Fase 1 exitosa):
  - P13: Dual-track agile
  - P31: RICE scoring
  - P37: Copilot coding
  - P38: Anomaly detection

Requiere Fase 1 estable
```

---

### Fase 3: Avanzado (Meses 10-18)

```yaml
Transformacionales:
  - P06: Inverse Conway (si reorg necesaria)
  - P10: SRE model
  - P21: Strangler fig (si legacy)
  - P46-P47: IA colaborativa avanzada

Alto impacto, alto riesgo, requiere madurez
```

---

## §10. ANTI-PATRONES RELACIONADOS

**Ver:** `APLICACION/A2_Antipatrones.md` para patologías que estos patrones mitigan.

**Mapeo común:**

- P01 mitiga AP05 (Silos funcionales)
- P29 mitiga AP12 (Top-down sin ownership)
- P23 mitiga AP18 (Deploy = Release sin control)
- P35 mitiga AP02 (Transformación sin preparar)

---

## §11. PATRONES EMERGENTES (v1.1+)

**Nota:** Patrones identificados post-release v1.0, basados en integración con fuentes fundacionales y práctica operacional.

### P51: Carry-Over Management

| ID | Nombre | Problema | Solución | Cuándo Usar | Evitar Si |
|---|---|---|---|---|---|
| **P51** | **Carry-Over Management** | Scrum rígido prohibe carry-over entre sprints → stories forzadas pequeñas pierden valor | Permitir trabajo fluir entre sprints con governance (max 30-40% capacity carry-over, re-priorizar cada sprint, track age >3 sprints) | Teams maduros, stories naturalmente multi-sprint, dominios complejos (embedded, sistemas críticos) | Work 100% completable en sprint único, team nuevo necesita estructura rígida |

**Detalles completos:** Ver `DOMINIOS/D4_Operacion.md` §7.1 para:

- Probabilistic delivery (no commitment "todo o nada")
- Métricas governance (Carry-Over Rate, Completion Rate, Avg Story Age)
- Yellow Cards (suspended work para incidents)
- Contraste con Scrum estricto

**Relación con otros patrones:**

- Complementa P16 (Scrumban Híbrido)
- Mitiga rigidez ceremonial de Scrum puro
- Habilita P17 (Mob Programming) en stories complejas

---

## §12. P52: CRISIS GOVERNANCE PATTERN (v1.1)

**Patrón consolidado en:** `CORE/08_Crisis_Management.md`

### Quick Reference

| Aspecto | Descripción |
|---------|-------------|
| **Activación** | H_Score < 45 OR any(O1-O8, I1-I3) < 30 sustained |
| **Problema** | Governance normal demasiado lento para crisis |
| **Solución** | Crisis team 5-7 personas, daily meetings, decision protocols <4hrs critical |
| **Cuándo Usar** | Financial (O3<30), Customer (O2<30), Talent (I2<30), Multiple observables <30 |
| **Evitar Si** | H_Score > 60, crisis artificial (AP31), no sponsor, team unavailable |
| **Duration** | 4-12 semanas típico (hasta H>45 stable 3 months) |
| **Exit Criteria** | H>45 for 3 months + all observables >30 + specific domain stability |

**Detalles completos**: Ver `CORE/08_Crisis_Management.md` para:

- §2: Activation triggers por tipo de crisis
- §3: Crisis team structure + dynamics (daily meetings)
- §4: Exit criteria + transition process
- §5: Antipatrones (AP31-33)
- §6: Stabilization actions by crisis type
- §9: Case study financial crisis

---

## §13. P53: ORCHESTRATION AGENT PATTERN

### Contexto

```yaml
Activación: Sistema requiere coordinar múltiples agents especializados

Problema:
  - N agents especializados en cognitive functions distintas
  - Cada agent opera independently (sensing, decision, execution)
  - User necesita interface unificado para supervisar/intervenir
  - Agents deben collaborate coherentemente sin conflicts
```

---

### Estructura

```yaml
Orchestration_Agent:
  
  Responsabilidades:
    1. Agent_Network_Management:
       - Registry de agents disponibles (capabilities catalog)
       - Health monitoring (cada agent reporta status)
       - Lifecycle management (start, stop, restart agents)
    
    2. Delegation_Management:
       - User configura policies: ¿qué delegar a qué agent?
       - Mapea user intent → agent capability
       - Routes tasks a agents apropiados (load balancing)
    
    3. Intervention_Points:
       - Define cuándo human debe intervenir (thresholds, exceptions)
       - Escalation logic: agent → orchestrator → human
       - Override mechanisms (human can take control anytime)
    
    4. Coordination:
       - Sincroniza agents (orchestrates Sense → Decide → Act pipeline)
       - Manages handoffs entre agents (output de uno → input de otro)
       - Conflict resolution si agents disagree on action

  Posición_Arquitectural:
    - Meta-level sobre domain agents
    - User-facing (provee supervision interface)
    - Purpose: Orchestration (ver 04_Delegacion §8 Purpose 3)
    - Autonomy: Típicamente M4-M5 (control, co-produce)

Conexión_Primitivos:
  orchestrator: Actor (algorítmico tipo meta)
  managed_agents: Set(Actor) (domain-specific specialists)
  coordination_flow: Flujo (orchestrator ↔ agents messaging)
  intervention_signals: Set(Señal) (escalations, overrides, alerts)
  delegation_policies: Set(Límite) (boundaries, thresholds)
  network_state: Estado (agents health, current assignments)
```

---

### Ejemplos

#### Ejemplo 1: Self-Driving Car Orchestrator

```yaml
Orchestrator: Main vehicle controller (supervises specialized agents)

Managed_Agents:
  Perception_Agent:
    - Capabilities: Camera, LIDAR, radar fusion
    - Function: Sense environment (L1 Detect + L2 Comprehend)
    - Output: Object detection, classification, tracking
  
  Localization_Agent:
    - Capabilities: GPS, mapping, SLAM
    - Function: Determine vehicle position
    - Output: Current position, map alignment
  
  Planning_Agent:
    - Capabilities: Route planning, behavior planning
    - Function: Decide trajectory (Mode 2-3 decisions)
    - Output: Path, speed profile, lane changes
  
  Control_Agent:
    - Capabilities: Steering, throttle, brakes actuation
    - Function: Execute maneuvers (L1-L2 execution)
    - Output: Vehicle control commands

User_Interface:
  - Set destination (delegates navigation to orchestrator)
  - Set driving mode (aggressive vs cautious vs eco)
  - Monitor status (dashboard shows agents health)
  - Intervention: Take steering wheel → Full override

Coordination_Logic:
  Normal_Flow:
    1. Perception detects pedestrian crossing
    2. Orchestrator alerts Planning
    3. Planning decides "slow down to stop"
    4. Orchestrator commands Control
    5. Control executes braking
    6. Orchestrator monitors success (perception feedback)
  
  Emergency_Escalation:
    IF Perception detects imminent collision:
      → Orchestrator bypasses Planning (too slow)
      → Direct command to Control: "Emergency brake"
      → Alert user with audio/visual warning
      → User can override (take control)
```

---

#### Ejemplo 2: Multi-Agent Business Process

```yaml
Orchestrator: Order fulfillment workflow engine

Managed_Agents:
  Order_Taking_Agent:
    - Function: Receives customer orders (Sense L1)
    - Output: Validated order (payment OK, stock check)
  
  Inventory_Agent:
    - Function: Allocates stock from warehouses (Decide Mode 2)
    - Output: Reserved inventory, warehouse assignment
  
  Warehouse_Agent:
    - Function: Schedules picking tasks (Execute L2-L3)
    - Output: Pick list, worker assignments
  
  Shipping_Agent:
    - Function: Books carriers, optimizes routes (Decide Mode 2-3)
    - Output: Carrier booking, tracking number
  
  Notification_Agent:
    - Function: Sends customer updates (Execute L1)
    - Output: Email/SMS confirmations

User_Interface (Operations Manager):
  - Configure policies (SLA, shipping rules, escalations)
  - Monitor workflow dashboard (orders in-flight, bottlenecks)
  - Intervene: Manual override for VIP orders, exceptions

Coordination_Logic:
  Standard_Flow:
    1. Order arrives → Order_Taking validates
    2. Orchestrator routes to Inventory
    3. Inventory allocates stock → Warehouse schedules pick
    4. Orchestrator routes to Shipping (parallel with picking)
    5. Shipping books carrier → Notification sends confirmation
  
  Exception_Handling:
    IF Inventory allocation fails (out of stock):
      → Orchestrator escalates to human buyer
      → Options: Backorder, Cancel order, Alternative product
      → Human decides → Orchestrator resumes workflow
```

---

#### Ejemplo 3: Crisis Governance (P52 as Orchestrator)

```yaml
Orchestrator: Crisis team + system (hybrid human-AI orchestration)

Managed_Agents:
  Financial_Agent:
    - Function: Monitors cash runway, burn rate (Sense L2-L3)
    - Alerts: Cash < 90 días, burn rate spike
  
  Customer_Agent:
    - Function: Tracks churn, NPS, retention (Sense L2-L3)
    - Alerts: Churn > 20%, NPS < 0, key account losses
  
  Talent_Agent:
    - Function: Monitors attrition, engagement (Sense L2)
    - Alerts: Attrition > 25%, eNPS < -10
  
  Operations_Agent:
    - Function: Tracks incidents, velocity (Sense L2)
    - Alerts: Incident rate spike, velocity drop

User_Interface (Crisis Team):
  - Daily morning meeting: All agents report status
  - Decision protocols: <4hrs critical, <24hrs tactical
  - Intervention: Crisis team makes decisions, agents execute

Coordination_Logic:
  Week_1_4_Stabilization:
    1. Financial_Agent: "Cash runway 18 días" (alert)
    2. Orchestrator: Escalates to crisis team (daily meeting)
    3. Crisis team: Decides "secure bridge loan + cut burn"
    4. Orchestrator: Delegates actions
       - Financial_Agent: Execute loan application
       - Operations_Agent: Implement cost cuts
    5. Orchestrator: Monitors daily progress
    6. IF H_Score > 45: Transition to normal governance
```

---

### Cuándo Usar

```yaml
Indicadores_Activación:
  - Sistema tiene ≥3 agents especializados
  - Agents deben collaborate para complete task end-to-end
  - User necesita single point of control/visibility
  - Delegation dinámica (varies by situation, trust, complexity)
  - Safety-critical OR high-value (requires human oversight)

Ejemplos_Aplicables:
  ✓ Self-driving vehicle (perception + planning + control)
  ✓ Multi-agent workflows (order fulfillment, incident response)
  ✓ Crisis management (multiple sensing agents + human decisions)
  ✓ Smart home (multiple devices coordinated)
  ✓ DevOps automation (CI/CD pipeline orchestration)
```

---

### Evitar Si

```yaml
No_Necesario_Si:
  - Single agent suffices (no coordination needed)
  - Agents fully independent (no interdependencies, can work isolated)
  - User wants direct control cada agent (no meta-interface desired)
  - System simple enough for hardcoded workflow (no dynamic routing)
  - Overhead > benefit (small-scale, trivial coordination)
```

---

### Antipatrones Relacionados

```yaml
AP34_No_Orchestration:
  Síntoma: N agents compiten, conflicts, inconsistent actions
  Causa: Cada agent optimiza locally sin global view
  Ejemplo_Real:
    - Autoscaling agent adds servers
    - Cost-optimization agent removes servers
    - Conflict: Thrashing (add/remove loops)
  Fix: Introduce orchestration agent para resolve conflicts
       → Coordina decisions (capacity vs cost trade-off)

AP35_Over_Orchestration:
  Síntoma: Orchestrator becomes bottleneck, agents wait for approval
  Causa: Orchestrator micro-manages, no delega apropiadamente
  Ejemplo_Real:
    - Every agent decision requires orchestrator approval
    - Orchestrator becomes single point of failure
    - Latency: <1s agents → 10s orchestration overhead
  Fix: Empoderar agents con bounded autonomy
       → Orchestrator sets policies, agents execute within bounds
       → Orchestrator intervenes only on exceptions/conflicts
```

---

### Conexión KERNEL

```yaml
Purpose_Dimension (04_Delegacion §8):
  - Orchestration Agent = Purpose 3
  - Distinct from Assistant, Augment, Automate
  - Manages other agents (meta-level function)

Execution_Levels (D4_Operacion §12):
  - Orchestrator opera en Level 3 (Action Planning)
  - Manages workflow, dependencies, parallelization
  - Delegates Level 1-2 (specification, action) to domain agents

Decision_Modes (D3_Decision §6):
  - Orchestrator típicamente Mode 2-3
  - Rule-based routing (simple cases)
  - Associative mapping (complex coordination)

Awareness_Levels (D2_Percepcion §5):
  - Orchestrator requiere Level 2-3
  - Comprehend: Agent status, health, conflicts
  - Project: Predict bottlenecks, resource needs

Building_Blocks (D1_Arquitectura §4):
  - Orchestrator puede ser BB3 (Coordinator) function
  - Especializado en coordination, no en domain work
```

---

---

## §14. PATRONES DESARROLLO EVOLUTIVO (P54-P56)

**Nota**: Patrones extraídos de `DOMINIOS/D4_Operacion.md` §11.1 para mayor aplicabilidad cross-domain. Fundamentados en Gall's Law y Christopher Alexander's pattern language.

### P54: Piecemeal Growth

| ID | Nombre | Problema | Solución | Cuándo Usar | Evitar Si |
|---|---|---|---|---|---|
| **P54** | **Piecemeal Growth** | Big bang design → fracaso (complex system from scratch never works) | Empezar sistema simple que funciona, crecer incrementalmente con stable intermediate forms | Todo sistema complejo (>3 meses build), alta incertidumbre requirements | Sistema trivial (<4 semanas), requirements 100% conocidos upfront |

**Detalles**:

```yaml
Gall's_Law_Foundation:
  "Complex system that works evolved from simple system that worked.
   Complex system designed from scratch never works."

Proceso:
  1. Start: Sistema mínimo end-to-end funcional (walking skeleton)
  2. Iterate: Agregar features incrementalmente (1-2 semanas cada)
  3. Validate: Cada iteración deployable, testeable, demostreable
  4. Grow: Sistema crece orgánicamente según feedback real

Drivers:
  Commercial:
    - Reduced risk (fail small, fail cheap)
    - Earlier ROI (value desde iteración 1)
    - Sponsor optionality (cancel anytime con valor capturado)
  
  Technical:
    - Simpler start (menos overwhelm)
    - Easier debug (pequeño = fácil aislar)
    - Devolved decisions (emergen del trabajo, no upfront committee)
    - Incorporates learning (feedback informa próximas iteraciones)

Anti-Pattern_Relacionado: Big Design Up Front (BDUF)
  - Meses 1-6: Design completo upfront
  - Meses 7-14: Implementation + integration
  - Mes 15: Descubrir que assumptions incorrectas
  - Costo: 10× vs piecemeal (change cost architectural late >> early)
```

**Conexión KERNEL**:

- Principio P4 (Flujo Continuo): Piecemeal permite evolution continua
- Outside-In (P3): Cada iteración entrega valor a destinatarios reales
- Probabilístico (P6): Cada iteración ajusta forecast basado en velocity real

---

### P55: Walking Skeleton

| ID | Nombre | Problema | Solución | Cuándo Usar | Evitar Si |
|---|---|---|---|---|---|
| **P55** | **Walking Skeleton** | Uncertainty arquitectural → integration risk al final | Build versión mínima end-to-end (todas capas) con 1 feature trivial, validate arquitectura funciona, luego grow | Proyecto nuevo (greenfield), arquitectura no validada, multiple layers (UI/API/DB/Infra) | Arquitectura probada (similar a proyecto anterior), single layer (solo backend o solo UI) |

**Detalles**:

```yaml
Definición:
  Implementación mínima que atraviesa TODAS las capas tech
  Implementa 1 feature trivial (casi sin business logic)
  Propósito: Validar plumbing, not business value yet

Ejemplo_E-commerce:
  Week_1_Skeleton:
    - UI: 1 página hardcoded "Product: Widget $10"
    - API: GET /products returns fixture JSON
    - DB: Tabla products con 1 row dummy
    - Auth: Login fake (username "admin", no validation)
    - Payment: Stub (always returns "success")
    - Deploy: CI/CD pipeline to staging
    - Tests: 1 E2E test (user sees product)
  
  Validación:
    - ✓ UI → API → DB → Deploy funciona
    - ✓ CI/CD pipeline operational
    - ✓ All layers integrated
    - ✗ Business value zero (hardcoded)
  
  Week_2_Real_Data:
    - Replace fixtures con DB real (seed 10 products)
    - API query DB instead of return fixture
    - Deploy to prod (minimal but real)
  
  Weeks_3-10_Growth:
    - Add search, filters, cart, checkout step-by-step
    - Cada semana: Sistema más capaz, siempre deployable

Beneficios:
  - De-risk arquitectura temprano (week 1, not month 6)
  - CI/CD desde día 1 (no "integrate later")
  - Framework growth (structure probada)
  - Momentum team (deployable week 1 vs month 3)
```

**Conexión KERNEL**:

- Composición Unidad_Trabajo (CORE/01 §7): Skeleton define actores/flujos mínimos
- Ciclo WSLC (CORE/02 §5): Skeleton es Development → Implementation rápido
- Mitigates AP15 (Big Bang Rewrite): Skeleton valida approach antes full investment

---

### P56: Continuous Refactoring

| ID | Nombre | Problema | Solución | Cuándo Usar | Evitar Si |
|---|---|---|---|---|---|
| **P56** | **Continuous Refactoring** | Design upfront especulativo → rigidez o design inadecuado descubierto tarde | Design emerge de refactoring continuo post-código funcional (make it work → make it right), Boy Scout Rule cada touch | Codebase evolutionary (learning ongoing), tech debt managed proactively | Codebase frozen (legacy untouchable), no tests (refactor sin tests = riesgo alto) |

**Detalles**:

```yaml
Principio:
  "El mejor momento para diseñar es DESPUÉS de tener código funcional"
  
  Razón:
    - Pre-code: Speculation (qué pensamos que necesitamos)
    - Post-code: Knowledge (qué sabemos que necesitamos)
    - Refactor con knowledge >> Design con speculation

TDD_Cycle:
  Red: Write failing test (define interface deseada)
  Green: Write simplest code passes (make it work, ignore elegance)
  Refactor: Improve design preserving tests (make it right)
  
  → Design emerge de refactoring, no precede coding

Boy_Scout_Rule:
  "Leave code better than you found it"
  
  Cada touch: Pequeña mejora (rename variable, extract function, etc.)
  Accumulate: 100 small improvements > 1 big refactor project
  Continuous: Diseño mejora constantemente, no decay

Límites:
  - Refactor >2 días → Considerar si es rewrite (ROI analysis)
  - Legacy code: A veces mejor dejar "as-is" (touch = risk)
  - No tests: Refactor = dangerous (add tests first)

20%_Rule_Integration:
  - 20% capacity health work incluye refactoring
  - NO: "Código malo ahora, refactor después" (tech debt intencional)
  - SÍ: "Código simple ahora, refactor cuando aprendemos" (informed improvement)
```

**Conexión KERNEL**:

- 20% Rule (D4 §5): Capacity para refactoring continuo
- Tech Debt Score (A5): Refactoring reduce debt incrementalmente
- P42 Quality Gates: Tests requieren para safe refactoring

---

## Referencias Cruzadas

- **Dominios detallados:** `DOMINIOS/D1-D4_*.md`
- **Purpose dimension:** `CORE/04_Delegacion.md` §8 (Orchestration Agent = Purpose 3)
- **Execution levels:** `DOMINIOS/D4_Operacion.md` §12 (Level 3 Planning)
- **Decision modes:** `DOMINIOS/D3_Decision.md` §6
- **Crisis Management:** `CORE/08_Crisis_Management.md` (P52 consolidado)
- **H_Score calculation:** `DOMINIOS/D2_Percepcion.md` §4
- **Antipatrones:** `APLICACION/A2_Antipatrones.md`
- **Ciclo SDA fundamental:** `CORE/02_Ciclo_Fundamental.md`
- **Templates OKR/Roadmap:** `REFERENCIA/R6_Templates/`
- **Piecemeal Growth detalle:** `DOMINIOS/D4_Operacion.md` §11 (context operacional)
