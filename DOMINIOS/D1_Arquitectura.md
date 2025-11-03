# D1_Arquitectura

**Versión:** 1.0.0 | **Estado:** Definitivo | **Audiencia:** Arquitectos Empresariales, Líderes Organizacionales

---

## Responsabilidad

**ARQUITECTURA define ESTRUCTURA organizacional:** Quién hace qué, cómo se organizan, límites de autoridad, interfaces entre unidades.

**Pregunta clave:** ¿Cómo nos organizamos para lograr objetivos?

---

## §0. QUICK START: ARQUITECTURA MÍNIMA VIABLE (MVA)

**Objetivo**: 80% valor con 20% esfuerzo - implementar lo esencial primero.

### MVA Checklist (4-6 semanas)

```yaml
Week_1-2: Estructura Básica
  ☐ Org chart documentado (tool: Lucidchart, Miro, o Excel)
  ☐ Teams identificados (5-9 personas each si posible)
  ☐ Managers asignados (span-of-control: target 5-9 reports)
  
Week_3-4: Claridad Decisional
  ☐ RACI matriz top 10 procesos críticos
  ☐ Decision rights documentados (Type 1 vs Type 2)
  ☐ Escalation path definido (quién decide qué, cuándo escalar)
  
Week_5-6: Interfaces
  ☐ Team boundaries claros (ownership products/services)
  ☐ Handoff points identificados (max 3-5 handoffs críticos)
  ☐ Communication cadence (standups, syncs, reviews)

Output_MVA:
  - Clarity: 70%+ personas saben quién decide qué
  - A_Score baseline: Típicamente 60-70 (good starting point)
  - Foundation para improvement continuo

Next_Steps_Post_MVA:
  - Implement 1-2 patrones (P01 Feature Teams o P10 SRE)
  - Measure A_Score trimestral
  - Iterate basado en gaps (use §2 Diagnóstico)
```

---

### Principios MVA (3 esenciales de 10)

```yaml
P1_Autoridad_Única:
  - CRÍTICO: Cada decisión 1 owner único
  - Quick implementation: RACI con single "A" (Accountable)
  - Skip si no posible: P2, P3 (menos crítico short-term)

P2_Límites_Claros:
  - CRÍTICO: Boundaries entre teams explícitos
  - Quick implementation: Service ownership map
  
P6_Autonomy_with_Alignment:
  - IMPORTANTE: Teams autónomos "cómo", alineados "qué"
  - Quick implementation: OKRs shared, implementation delegated

P4,P5,P7-P10: Defer a post-MVA (6+ meses)
```

---

### Cuando Skip MVA

```yaml
Ya_Tienes_MVA_Si:
  - Org chart updated <3 meses
  - RACI existe y usado para decisiones
  - <10% conflictos autoridad escalados semanalmente
  - A_Score >70
  
  → Skip to full implementation (§1-§6 completo)

MVA_No_Suficiente_Si:
  - Org >200 personas (requiere más estructura)
  - Highly regulated (compliance requiere más documentation)
  - M&A recent (integration complexity mayor)
  
  → Use full D1 desde inicio
```

---

## §1. LOS 10 PRINCIPIOS ESTRUCTURALES

### P1. Autoridad Única

```yaml
Principio: Cada decisión tiene exactamente 1 owner
Rationale: Autoridad fragmentada → Parálisis decisional
Test_Violación: ¿Hay decisiones donde 2+ personas tienen veto pero ninguna es accountable?

Ejemplo_Correcto:
  Decisión: "Priorizar Feature X en roadmap"
  Owner: Product Manager (ÚNICO accountable)
  Consulted: Eng Lead, Design Lead, PM
  Informed: Stakeholders
  
Ejemplo_Violación:
  Decisión: "Aprobar arquitectura microservices"
  Owner: CTO + VP Eng + Architect (3 vetos, nadie accountable único)
  → PROBLEMA: Si falla, ¿quién es responsable?
```

---

### P2. Límites Claros

```yaml
Principio: Boundaries entre unidades explícitos y mínimos
Rationale: Handoffs costosos, interfaces reducen friction
Test_Violación: ¿Equipos no saben dónde termina su responsabilidad?

Ejemplo_Correcto:
  Team_A: Ownership API /orders (incluyendo DB, deployment)
  Team_B: Ownership API /payments (incluyendo DB, deployment)
  Interface: AsyncAPI contract (events Order_Created, Payment_Completed)
  
Ejemplo_Violación:
  Team_A: "Nosotros hacemos frontend, pero backend también a veces"
  Team_B: "Nosotros backend, pero tocamos frontend si urgente"
  → PROBLEMA: Ownership difuso, nadie mantiene code quality
```

---

### P3. Specialization at Scale

```yaml
Principio: A mayor escala, mayor especialización requerida
Rationale: World-class expertise requiere focus profundo
Test_Violación: ¿Generalistas cuando org >100 personas?

Progresión típica:
  <10 personas: Full-stack generalists OK
  10-50: Especialización leve (Backend/Frontend/Data)
  50-200: Teams especializados (Platform, Product, Data, ML)
  200-1000: Departments + chapters (Eng dept con Backend/Frontend/Mobile/ML/Data chapters)
  >1000: Business units + platforms centralizadas

Ejemplo_Violación:
  Org 500 personas con "everyone does everything"
  → PROBLEMA: Nadie es world-class en nada
```

---

### P4. Conway's Law Awareness

```yaml
Principio: Org structure determina system architecture
Conway's Law: "Systems mirror communication structure of org"

Implicación: Si quieres microservices, necesitas teams autónomos
           Si quieres monolito modular, necesitas coordination fuerte

Ejemplo_Correcto:
  Objetivo: Microservices architecture
  Org: 8 teams pequeños (5-9 personas), cada uno ownership 1-3 services
  Resultado: Loose coupling natural (cada team evoluciona su service independiente)

Ejemplo_Violación:
  Objetivo: Microservices architecture
  Org: 1 team grande 40 personas, todos tocan todos los services
  Resultado: Monolito distribuido (coupling alto, deploys coordinados)
```

---

### P5. Minimize Handoffs

```yaml
Principio: Reducir handoffs entre equipos al mínimo necesario
Rationale: Cada handoff agrega latencia, fricción, errores

Métrica: Handoff_Ratio = # Handoffs / # Pasos_Proceso
Target: <20% para procesos críticos

Ejemplo_Correcto:
  Proceso: "Deploy feature to production" (5 pasos)
  - Developer escribe código → Deploy staging (1 team)
  - QA automation valida (1 team)
  - Security scan (automated, 0 handoff humano)
  - Deploy prod (automated)
  - Monitor (mismo team developer)
  Handoffs: 1 (Dev → QA) / 5 pasos = 20%

Ejemplo_Violación:
  Proceso: "Deploy feature" (12 pasos, 8 handoffs)
  Dev → Code review team → QA manual → Security review → Change board → Ops deploy → Monitoring team → Support handoff
  Handoffs: 8 / 12 = 67%
  Cycle time: 14 días (vs 2 días con <20% handoffs)
```

---

### P6. Autonomy with Alignment

```yaml
Principio: Teams autónomos en "cómo", alineados en "qué" y "por qué"
Rationale: Autonomía sin alignment → Chaos
           Alignment sin autonomía → Micromanagement

Balance:
  Centralizado: Estrategia, OKRs, principles, platforms
  Descentralizado: Implementación, tech choices (dentro de guardrails), priorización micro

Ejemplo_Correcto:
  Central define: "Reducir churn a 5%" (OKR)
  Team A autónomo: Decide implementar feature "Proactive outreach" (cómo)
  Team B autónomo: Decide implementar "Churn prediction ML" (cómo diferente)
  Resultado: Ambos contribuyen a mismo OKR, approaches distintos

Ejemplo_Violación:
  Central define: "Reducir churn" + "Usar Python" + "Desplegar Kubernetes" + "3 sprints" + "Arquitectura X"
  Team: Solo ejecuta, 0 autonomía
  → PROBLEMA: No ownership, no innovación, low morale
```

---

### P7. Reversible Decisions Fast

```yaml
Principio: Decisiones reversibles → delegar rápido
           Decisiones irreversibles → escalar con cuidado

Type 1 (Irreversible): Cambio legal entity, M&A, reorg mayor
  → Requiere C-level approval, análisis profundo
  
Type 2 (Reversible): Tech stack choice, feature prioritization, hiring 1 persona
  → Delegar a teams, decidir rápido, ajustar si falla

Ejemplo_Correcto:
  Team decide: "Vamos a usar PostgreSQL en vez de MySQL"
  Si falla: Migrar en 2 semanas (reversible)
  → Decisión delegada, rápida

Ejemplo_Violación:
  Team debe escalar a ARB: "¿Usamos PostgreSQL or MySQL?"
  ARB tarda 3 semanas en decidir
  → PROBLEMA: Overhead decisional excesivo en Type 2 decision
```

---

### P8. Internal Entrepreneurship

```yaml
Principio: Cada unidad organizacional opera como negocio interno con clientes y value proposition
Rationale: Entrepreneurship driving innovation y customer focus
Test_Violación: ¿Unidad puede identificar clientes específicos y valor entregado?

Conexión: Formaliza Outside-In (P3 Manifiesto) en estructura organizacional
          Conecta con composición Unidad_Trabajo (productos_servicios, destinatarios)

Ejemplo_Correcto:
  Platform Team:
    Clientes: Product teams internos (15 teams)
    Productos_Servicios: CI/CD self-service, K8s clusters managed
    Value_Proposition: Reduce deploy time 80%, uptime 99.9%
    Métricas_Valor: Adoption rate 95%, developer satisfaction 4.5/5
  → Entrepreneurship claro, accountability por valor

Ejemplo_Violación:
  "Architecture Team":
    Función: "Hacer arquitectura" (vago)
    Cliente: ¿? (no identificado)
    Output: Documentos que nadie lee
    Métricas: Lines of documentation produced
  → PROBLEMA: No entrepreneurship, no customer focus, no value measurable
```

**Implicación práctica:** Cada manager debe poder responder: "¿Quiénes son mis clientes?" y "¿Qué valor específico les entrego?"

---

### P9. Avoid Conflicts of Interest

```yaml
Principio: Roles no deben requerir optimizar objectives opuestos simultáneamente
Rationale: Conflictos de interés hacen jobs imposibles
           Protege moral obligation (no culpar personas por mal diseño)
Test_Violación: ¿Role requiere maximizar A y B donde A contradice B?

Ejemplo_Violación_1 (Operations Director):
  Accountable_Por: Stability (uptime 99.99%, no disruptions)
  Accountable_Por: Innovation (implement new technologies)
  Conflicto: Innovation inevitablemente disrupts stability
  Resultado: Innovation managers fired consecutivamente (3 en 6 años)
  Causa_Real: Diseño de role imposible, no incompetencia personas
  
Ejemplo_Violación_2 (Sales + Coordination):
  Job_1: Sales (requires outbound energy, focus externo, persuasión)
  Job_2: Internal Coordination (requires facilitation, consensus building)
  Conflicto: Skill sets y temperamentos completamente diferentes
  Resultado: Excel en sales, fail en coordination → fired
  Causa_Real: Expecting one person master two opposing competencies

Ejemplo_Correcto:
  Split role Operations Director en 2:
    - SRE Lead: Accountable stability únicamente
    - Innovation Lead: Accountable new tech adoption únicamente
    - Coordination: ARB resuelve tensiones stability vs innovation
  → Ambos pueden excel en roles coherentes
```

**Moral imperative:** Antes de culpar performance, verificar si role design contiene conflictos inherentes.

---

### P10. Professional Clustering

```yaml
Principio: Agrupar especialistas bajo manager con expertise similar
Rationale: Knowledge sharing, mentorship efectivo, career paths claros
Test_Violación: ¿Especialistas reportan a manager sin domain expertise?

Ejemplo_Correcto (Matrix Organization):
  Dimensión_Horizontal (Delivery):
    - Product Teams: Cross-functional squads para delivery
  
  Dimensión_Vertical (Craft/Career):
    - Backend Chapter: 40 engineers → Backend Engineering Lead
    - Frontend Chapter: 30 engineers → Frontend Engineering Lead
    - Data Chapter: 25 engineers → Data Engineering Lead
    - ML Chapter: 15 engineers → ML Engineering Lead
  
  Beneficios:
    - Knowledge sharing within chapter (tech talks, pair programming)
    - Career progression visible (junior → mid → senior → staff → principal)
    - Manager can evaluate technical work (domain expertise)
    - Standards consistency (code style, testing practices)

Ejemplo_Violación:
  Org 200 engineers en product teams únicamente:
    - 20 product teams, cada uno con mix especialistas
    - Todos reportan a Product Manager (no technical background)
  
  Problemas:
    → Backend engineer no tiene mentor backend
    → Career path unclear (¿cómo progresar sin senior backend reference?)
    → Quality standards divergen (cada team reinventa prácticas)
    → Knowledge silos (learnings no cross-polinate)

Resolución_Matrix:
  Dual_Reporting:
    - Product Manager: Accountable delivery, velocity, outcomes
    - Chapter Lead: Accountable craft quality, career development, standards
  
  No_Conflict: PM focuses "what" (roadmap), Chapter focuses "how" (technical excellence)
```

**Escala:** <50 personas clustering opcional, >100 personas clustering mandatorio, >500 clustering + formal chapters.

---

## §2. DIAGNÓSTICO ARQUITECTURAL

### Framework Diagnóstico

```yaml
Síntoma_Observado (11 observables):
  ↓
Hipótesis_Root_Cause (violación 10 principios):
  ↓
Validación (datos, entrevistas):
  ↓
Recomendación_Estructural:
  ↓
Implementación (reorg, redefinición boundaries):
  ↓
Medición_Post (A_Score, I1, I2)
```

---

### Síntomas Comunes

#### S1. Decisiones Lentas (I1 bajo)

```yaml
Síntoma: I1 (Velocidad decisional) <50/100
Observable: Decisiones tardan >2 semanas promedio

Root_Causes_Posibles:
  - Viola P1: Autoridad fragmentada (3+ personas con veto)
  - Viola P7: Todas decisiones escaladas a C-level (Type 2 tratadas como Type 1)
  - Estructura: Demasiados layers jerárquicos (>5 para org <500)

Diagnóstico:
  1. Mapear últimas 20 decisiones: Owner, tiempo decisión, # aprobaciones requeridas
  2. Clasificar Type 1 vs Type 2
  3. Identificar bottlenecks (ej: ARB se reúne 1 vez/mes, backlog 30 decisiones)

Recomendación:
  - Si P1 violado: Asignar DRI (Directly Responsible Individual) única por decisión
  - Si P7 violado: Delegar Type 2 decisions a teams, ARB solo Type 1
  - Si layers excesivos: Flatten org, eliminar approval layers innecesarios
```

---

#### S2. Silos Patológicos

```yaml
Síntoma: Handoffs excesivos, teams no colaboran, "not my job" culture
Observable: Handoff_Ratio >40%, cycle time alto

Root_Causes_Posibles:
  - Viola P2: Boundaries difusos o demasiado rígidos
  - Viola P5: Proceso diseñado con handoffs innecesarios
  - Estructura: Functional silos sin cross-functional teams

Diagnóstico:
  1. Value Stream Map: Identificar handoffs en proceso crítico
  2. Medir: Tiempo en handoff / Total cycle time
  3. Identificar: ¿Handoffs necesarios (especialización) o fricción?

Recomendación:
  - Crear cross-functional squads (reduce handoffs 60-80%)
  - Implementar "You build it, you run it" (ownership E2E)
  - Shared OKRs entre teams que deben colaborar
```

---

#### S3. Scaling Bottlenecks

```yaml
Síntoma: No pueden escalar headcount sin colapsar velocidad
Observable: Duplicar team size → Velocity cae 40%

Root_Causes_Posibles:
  - Viola P3: No especialización suficiente (coordination overhead)
  - Viola P4: Monolito + team grande (Conway's Law)
  - Estructura: Span of control extremo (1 manager con 20+ reports)

Diagnóstico:
  1. Medir: Velocity per capita vs headcount (¿correlación negativa?)
  2. Analizar: Dependencies entre teams (¿todos tocan mismo código?)
  3. Identificar: ¿Architecture permite paralelismo?

Recomendación:
  - Split monolito → Microservices (requiere split teams)
  - Crear platform teams (infra compartida, product teams independientes)
  - Management layers: 1 manager per 5-9 reports (no más)
```

---

#### S4. Conflicts de Autoridad

```yaml
Síntoma: Conflictos frecuentes "quién decide", escalations diarias
Observable: >10 escalaciones/semana a C-level

Root_Causes_Posibles:
  - Viola P1: RACI con múltiples "A" (Accountable)
  - Estructura: Matrix sin governance claro

Diagnóstico:
  1. Audit RACI: ¿Decisiones con 2+ Accountable?
  2. Interview teams: "¿Sabes quién decide X?" (si <80% sabe, problema)

Recomendación:
  - RACI strict: 1 Accountable por decisión, N Consulted/Informed
  - Si Matrix: Definir escalation explícito (ej: Functional manager decide people, Product manager decide roadmap)
```

---

## §3. PATRONES ESTRUCTURALES (12 PATRONES)

### Patrón 1: Feature Teams

```yaml
Nombre: Feature Teams
Contexto: Org 20-200 personas, producto digital
Problema: Functional silos (Frontend/Backend/QA separados) causan handoffs excesivos

Solución:
  - Teams cross-functional 5-9 personas (Eng, Product, Design)
  - Cada team ownership features E2E (desde ideación hasta producción)
  - Minimal dependencies entre teams

Estructura:
  Team_A: Login & Auth (Backend + Frontend + DB + Deploy)
  Team_B: Payments (Backend + Frontend + DB + Deploy)
  Team_C: Catalog (Backend + Frontend + DB + Deploy)

Ventajas:
  - Cycle time bajo (no handoffs)
  - Ownership claro
  - Autonomía alta

Desventajas:
  - Requiere multi-skilled engineers (no todos pueden)
  - Duplicación cross-team (cada team su pipeline)
  - Platforms necesitan governance

Cuándo_Usar:
  - Producto digital
  - Velocity es crítico
  - Equipos pueden ser full-stack
```

---

### Patrón 2: Platform Teams

```yaml
Nombre: Platform Teams
Contexto: Org >100 personas, infra compartida crítica
Problema: Product teams reinventan wheel (CI/CD, monitoring, auth)

Solución:
  - 1-3 Platform teams que construyen "products for internal teams"
  - Product teams son "customers" de platforms
  - Platforms exponen APIs/herramientas self-service

Estructura:
  Platform_DevEx: CI/CD, deployment, local dev environment
  Platform_Data: Data warehouse, pipelines, governance
  Platform_Auth: SSO, RBAC, OAuth flows
  
  Product_Teams (10 teams): Consumen platforms, focus en features

Ventajas:
  - No duplicación esfuerzo
  - Standards consistentes
  - Product teams más rápidos

Desventajas:
  - Platform puede volverse bottleneck si no self-service
  - Requiere product thinking en platform teams

Cuándo_Usar:
  - >5 product teams
  - Infra común compleja
  - Standards críticos (compliance, security)
```

---

### Patrón 3: Business-within-Business

```yaml
Nombre: Business-within-Business
Contexto: Org >200 personas, múltiples value streams independientes
Problema: Dependencies entre value streams ralentizan todos

Solución:
  - Cada "business" es mini-empresa autónoma
  - Tiene Eng + Product + Design + Data + Marketing
  - P&L propio (puede ser)
  - Minimal dependencies con otros businesses

Estructura:
  Business_Streaming: Todo lo relacionado video streaming
  Business_Content: Todo lo relacionado producción contenido
  Business_Growth: Todo lo relacionado adquisición usuarios
  
  Shared_Platforms: Infra, Auth, Payments (servicios a businesses)

Ventajas:
  - Autonomía máxima
  - Velocity alta (no coordination overhead)
  - Accountability clara (P&L)

Desventajas:
  - Duplicación algunas funciones
  - Requiere businesses realmente independientes

Cuándo_Usar:
  - >200 personas
  - Value streams independientes (pueden fallar uno sin afectar otro)
  - Ejemplo: Netflix (Streaming, Content, Growth como "businesses")
```

---

### Patrón 4: Guilds & Chapters

```yaml
Nombre: Guilds & Chapters (Spotify model)
Contexto: Org 100-500 personas, necesita especialización + cross-pollination
Problema: Feature teams → Silos de conocimiento, no sharing

Solución:
  - Squads: Feature teams (estructura primaria)
  - Chapters: Agrupación especialistas mismo dominio (ej: Backend chapter)
  - Guilds: Comunidades práctica cross-chapter (ej: Security guild)

Estructura:
  Squads: Unidades delivery (5-9 personas cross-functional)
  Chapters: Managers funcionales (Backend, Frontend, Data)
    → Chapter lead hace 1:1s, career development, standards
  Guilds: Voluntarios, share conocimiento, sin autoridad formal

Ventajas:
  - Autonomía squads (delivery)
  - Especialización chapters (expertise)
  - Cross-pollination guilds (innovación)

Desventajas:
  - Complejidad (dual structure)
  - Requiere cultura madura

Cuándo_Usar:
  - Org media (100-500)
  - Necesitas expertise profundo + delivery rápido
```

---

### Patrón 5: Two-Pizza Teams

```yaml
Nombre: Two-Pizza Teams (Amazon)
Contexto: Org escala rápido, necesita mantener velocity
Problema: Teams grandes → Coordination overhead O(n²)

Solución:
  - Team size: 5-9 personas (pueden comer con 2 pizzas)
  - Full ownership producto/servicio
  - APIs como interfaces entre teams

Regla: Si team >9 personas → Split en 2 teams

Ventajas:
  - Communication overhead mínimo
  - Decision making rápido
  - Ownership claro

Desventajas:
  - Requiere arquitectura que soporte (microservices)
  - Puede generar muchos teams (coordination cross-team)

Cuándo_Usar:
  - Org >50 personas
  - Velocity crítico
  - Arquitectura permite autonomía
```

---

### Patrón 6: Enabling Teams

```yaml
Nombre: Enabling Teams
Contexto: Stream-aligned teams necesitan upskilling
Problema: Teams luchan con nueva tech (ej: Kubernetes, ML)

Solución:
  - Enabling team: Expertos temporales que ayudan otros teams
  - NO hacen el trabajo, ENSEÑAN
  - Time-boxed engagement (8-12 semanas)

Ejemplo:
  Stream_Team_A: Quiere adoptar Kubernetes
  Enabling_Team_SRE: Pair programming 4 semanas, luego Team_A autónomo
  
  Diferencia vs Platform: Platform provee servicio, Enabling enseña

Ventajas:
  - Upskilling orgánico
  - No dependencia permanente
  - Expertise compartido

Desventajas:
  - Requiere personas con skills teaching
  - Temporal (no sustentable long-term)

Cuándo_Usar:
  - Adoption nueva tech
  - Teams heterogéneos en skills
```

---

### Patrón 7: Inverse Conway Maneuver

```yaml
Nombre: Inverse Conway Maneuver
Contexto: Quieres arquitectura específica (ej: microservices)
Problema: Org actual no soporta arquitectura deseada

Solución:
  - Diseñar org structure para forzar arquitectura deseada
  - Split teams primero, arquitectura emerge después

Proceso:
  1. Target architecture: 8 microservices independientes
  2. Crear 8 teams pequeños (1 team per service)
  3. Dar ownership E2E a cada team
  4. Arquitectura microservices emerge (Conway's Law)

Ventajas:
  - Arquitectura sigue org (natural)
  - Ownership claro desde día 1

Desventajas:
  - Disruptivo (reorg)
  - Requiere commitment leadership

Cuándo_Usar:
  - Migration deliberada (monolito → microservices)
  - Tienes mandate C-level
```

---

### Patrón 8: Pods (Apple)

```yaml
Nombre: Pods
Contexto: Producto complejo, múltiples especialidades
Problema: Necesitas deep expertise + collaboration cercana

Solución:
  - Pod: 3-5 expertos ultra-especializados
  - Trabajan juntos iteraciones cortas
  - Rotan entre pods según proyecto

Ejemplo_Apple_iOS:
  Pod_Camera: 1 HW engineer + 1 SW engineer + 1 ML engineer
  → Trabajan 6 meses en camera feature
  → Luego rotan a otros pods

Ventajas:
  - Expertise profundo
  - Collaboration intensa
  - Flexibility (rotan)

Desventajas:
  - No escala >100 personas bien
  - Requiere high-performers

Cuándo_Usar:
  - Producto premium
  - Expertise crítico
  - Org pequeña elite
```

---

### Patrón 9: Federated Model

```yaml
Nombre: Federated Model
Contexto: Org global, múltiples geografías
Problema: Central vs Local tension

Solución:
  - Central: Estrategia, governance, platforms
  - Federado (geo): Execution, hiring, adaptación local

Estructura:
  Central_HQ: CTO, architects, platform core
  Geo_LATAM: Eng teams, product managers, local execution
  Geo_EU: Eng teams, product managers, local execution
  Geo_APAC: Eng teams, product managers, local execution

Governance:
  - Central define: OKRs, tech radar, security standards
  - Geo decide: Priorización local, hiring, implementations

Ventajas:
  - Escala global
  - Adaptación local
  - Time zones (follow-the-sun)

Desventajas:
  - Coordination complejo
  - Duplicación esfuerzos

Cuándo_Usar:
  - Org >500 personas
  - Múltiples geos
  - Local needs difieren
```

---

### Patrón 10: Dual-Track Agile

```yaml
Nombre: Dual-Track Agile
Contexto: Discovery + Delivery en paralelo
Problema: Teams construyen features nadie usa (no discovery)

Solución:
  - Track 1 (Discovery): PMs + Designers validan problems, prototipos
  - Track 2 (Delivery): Eng construye features validados
  - Parallel tracks, mismas personas rotan

Ciclo:
  Week 1-2: PM/Design discover problema (Track 1)
  Week 3-4: Eng build feature validado (Track 2)
  Week 5-6: PM/Design discover siguiente problema (Track 1 para próximo)

Ventajas:
  - Reduce waste (solo builds validados)
  - Velocity alta (parallel)

Desventajas:
  - Requiere PM/Design strong
  - Complexity gestión 2 tracks

Cuándo_Usar:
  - Product teams maduros
  - Discovery crítico (B2C)
```

---

### Patrón 11: SRE Model (Google)

```yaml
Nombre: SRE (Site Reliability Engineering)
Contexto: Operación sistemas críticos escala
Problema: Dev build features, Ops apaga fuegos perpetuo

Solución:
  - SRE: 50% tiempo en automation, 50% en toil
  - Si toil >50% → Rechaza trabajo, fuerza Devs fix root cause
  - Error budget: SLO 99.9% → 0.1% budget errors usado para velocity

Reglas:
  - SRE solo acepta services con SLO claro
  - Si error budget agotado → Feature freeze, solo reliability work
  - Automation mandatorio (no manual toil perpetuo)

Ventajas:
  - Reliability cuantificado
  - Incentivos alineados (Dev quiere features, SRE quiere uptime, error budget balancea)

Desventajas:
  - Requiere engineers seniors
  - Cultural shift grande

Cuándo_Usar:
  - Sistemas críticos (99.9%+ uptime)
  - Escala (>100K users)
```

---

### Patrón 12: Product Trios

```yaml
Nombre: Product Trios
Contexto: Product discovery intenso
Problema: PM solo decide features → Suboptimal

Solución:
  - Trio: PM + Eng Lead + Design Lead
  - Co-own roadmap, discovery, prioritization
  - Decisiones consensus (no PM dictator)

Meetings:
  - Weekly trio sync (90 min)
  - Discovery sessions (user interviews, data análisis)
  - Roadmap refinement continuo

Ventajas:
  - Expertise complementario
  - Buy-in desde diseño
  - Better decisions

Desventajas:
  - Slower (3 personas consensus)
  - Requiere high-trust

Cuándo_Usar:
  - Product-led growth
  - Expertise balanceado PM/Eng/Design
```

---

## §4. ANTI-PATRONES ARQUITECTURALES

### AP1. Matrix sin Governance

**Ver:** `CORE/03_Arquitectura.md` §10

---

### AP2. Reorg como Solución Mágica

```yaml
Síntoma: Cada 6 meses nueva estructura
Causa: No diagnóstico root cause, "reorg fixes all"
Consecuencia: Fatigue, I2 colapsa, no learning

Ejemplo:
  Q1: Functional silos
  Q2: Reorg a feature teams
  Q3: Feature teams no funciona, reorg a platform teams
  Q4: Platform bottleneck, reorg a matrix
  
  → Nadie aprende por qué falló cada modelo

Fix:
  - Diagnosticar antes de reorg (§2)
  - Pilot nueva estructura (1-2 teams, 3 meses)
  - Retrospectiva pre-scaling
  - Reorg no más de 1 vez cada 18-24 meses
```

---

### AP3. Team Topology Mismatch

```yaml
Síntoma: Quieres microservices, tienes 1 team 40 personas
Causa: Ignorar Conway's Law
Consecuencia: Monolito distribuido (peor de ambos mundos)

Fix:
  - Si monolito OK → 1-2 teams grandes, coordination fuerte
  - Si microservices → N teams pequeños (1-2 services cada uno)
  - Inverse Conway: Reorg teams primero, arquitectura sigue
```

---

### AP4. Span of Control Extremo

```yaml
Síntoma: Manager 25+ reports directos
Causa: Growth sin crear management layer
Consecuencia: No 1:1s, development nulo, I2 cae

Fix:
  - Target: 5-9 reports per manager
  - Si >10 → Split team, promote lead
```

---

## §5. MÉTRICAS ARQUITECTURA

### A_Score (0-100)

**Ver:** `CORE/03_Arquitectura.md` §9

Componentes adicionales:

```yaml
A6_Decision_Clarity:
  Métrica: % decisiones Type 1 vs Type 2 clasificadas
  Target: >90%
  Cálculo: Audit últimas 50 decisiones, ¿están clasificadas?

A7_Handoff_Efficiency:
  Métrica: Avg handoff ratio procesos críticos
  Target: <25%
  Cálculo: (# Handoffs / # Steps) para top 10 procesos

A8_Team_Stability:
  Métrica: % teams sin cambios miembros últimos 6 meses
  Target: >70%
  Cálculo: ¿Cuántos teams tienen mismo roster 6 meses?
```

---

## §6. IMPLEMENTACIÓN CAMBIO ESTRUCTURAL

### Ciclo Reorg (20 semanas)

```yaml
Semanas 1-4: DIAGNÓSTICO
  - Measure: A_Score, I1, I2, I3
  - Interview: 20 personas clave
  - Identify: Root causes (§2)
  - Output: Diagnóstico report

Semanas 5-8: DISEÑO
  - Design: Target structure (elegir patrón §3)
  - Model: RACI nuevo
  - Prepare: Team charters
  - Output: Target state blueprint

Semanas 9-10: COMUNICACIÓN
  - Announce: Town hall + FAQ
  - 1:1s: Cada persona afectada
  - Address: Concerns, resistance
  - Output: Commitment leadership + teams

Semanas 11-16: TRANSICIÓN
  - Reassign: Personas a nuevos teams
  - Handoff: Responsabilidades
  - Train: New processes
  - Monitor: I2 (Salud talento) intensivo
  - Output: Nueva estructura operando

Semanas 17-20: ESTABILIZACIÓN
  - Adjust: Issues menores
  - Retro: ¿Qué funcionó/no funcionó?
  - Measure: A_Score, I1, I2, I3 post-reorg
  - Output: Lessons learned

Post-Week-20: SOSTENIBILIDAD
  - Maintain: Nueva estructura mínimo 18 meses
  - Evolve: Ajustes menores OK, no reorg mayor
```

---

## §4. BUILDING BLOCKS PATTERN

### Concepto

```yaml
Definición:
  5 arquetipos organizacionales universales que toda org completa debe contener
  NO son primitivos (son patrones arquitecturales)
  SON composiciones de Actor + productos_servicios + destinatarios
  
Fundamento:
  Completeness test: ¿Organización puede innovar, operar, coordinar, vender, auditar?
  Missing building block → Gap capability específico
```

---

### BB1: Engineers (Innovadores)

```yaml
Función: Diseñar soluciones nuevas (productos, servicios, sistemas)

Composición_KERNEL:
  actores: Set(Actor) con skill_type = "Design/Engineering"
  productos_servicios: Nuevos productos, servicios, features
  destinatarios: Customers (external) o Business units (internal)
  
Sub-Tipos:
  Applications_Engineers:
    - Diseñan soluciones purpose-specific para customer needs
    - Ejemplos: Product teams, Solution architects
    
  Base_Engineers:
    - Diseñan componentes reusables y platforms
    - Ejemplos: Platform teams, Infrastructure engineers

Test_Completeness:
  ¿Organización puede innovar y crear productos nuevos?
  IF NO → Missing BB1 (Engineers)
  Síntoma: Zero innovation, solo mantenimiento
```

---

### BB2: Service Providers (Operadores)

```yaml
Función: Operar assets y entregar servicios repetitivos

Composición_KERNEL:
  actores: Set(Actor) con skill_type = "Operations"
  productos_servicios: Servicios operacionales continuos
  destinatarios: Internal users o customers
  
Sub-Tipos:
  Asset-based_Providers:
    - Operan shared infrastructure
    - Ejemplos: Network ops, Data center ops, Production facilities
    
  People-based_Providers:
    - Proveen expertise y labor services
    - Ejemplos: Help desk, Training, Recruiting, Accounting

Test_Completeness:
  ¿Organización puede mantener operaciones day-to-day?
  IF NO → Missing BB2 (Service Providers)
  Síntoma: Operational chaos, no reliability
```

---

### BB3: Coordinators (Facilitadores)

```yaml
Función: Facilitar decisiones shared cross-organizacionales

Composición_KERNEL:
  actores: Set(Actor) con skill_type = "Coordination/Governance"
  productos_servicios: Standards, policies, coordination
  destinatarios: Toda la organización (cross-cutting)
  
Sub-Tipos:
  Business_Coordinators:
    - Strategic planning, Budget coordination, Org design
    - Ejemplos: Strategy office, PMO, Business continuity
    
  Technical_Coordinators:
    - Standards coordination, Architecture governance
    - Ejemplos: Enterprise architects, Tech standards committee

Test_Completeness:
  ¿Organización puede coordinar decisions cross-functional?
  IF NO → Missing BB3 (Coordinators)
  Síntoma: Fragmentation, inconsistency, no standards
```

---

### BB4: Sales (Relacionadores)

```yaml
Función: Construir relationships y descubrir oportunidades

Composición_KERNEL:
  actores: Set(Actor) con skill_type = "Relationship/Sales"
  productos_servicios: Relationships, opportunities, demand generation
  destinatarios: External customers o stakeholders
  
Sector_Context:
  Private:
    - Account sales, Marketing, Business development
    - Focus: Revenue, customer acquisition
  
  Public:
    - Stakeholder engagement, Citizen services, Partner relations
    - Focus: Legitimacy, stakeholder satisfaction, participation

Test_Completeness:
  ¿Organización puede identificar customer needs y opportunities?
  IF NO → Missing BB4 (Sales)
  Síntoma: Disconnect from market/stakeholders, reactive only
```

---

### BB5: Audit (Aseguradores)

```yaml
Función: Assurance independent, compliance, risk management

Composición_KERNEL:
  actores: Set(Actor) con skill_type = "Audit/Compliance"
  productos_servicios: Assurance reports, compliance verification
  destinatarios: Board, Regulators, Leadership
  
Sub-Tipos:
  - Internal audit
  - Compliance monitoring
  - Risk management
  - Quality assurance

Test_Completeness:
  ¿Organización tiene oversight independent?
  IF NO → Missing BB5 (Audit)
  Síntoma: No controls, compliance failures, risk blindness
```

---

### Completeness Test Framework

```yaml
Diagnostic_Process:
  
  FOR each building_block IN [BB1, BB2, BB3, BB4, BB5]:
    ASSESS: ¿Existe en org?
    ASSESS: ¿Tiene capacidad adecuada?
    ASSESS: ¿Reporta apropiadamente?
  
  IF any_missing:
    Diagnose_Gap:
      - ¿Función tercerizada? (acceptable if intentional)
      - ¿Función no reconocida? (structural gap)
      - ¿Función diluida en otros roles? (violates specialization)
  
  Healthy_State:
    All 5 building blocks present
    Each with dedicated resources
    Each with clear accountability (P8 Entrepreneurship)
    Each clustered professionally (P10 Professional Clustering)
```

---

### Conexión Principios

```yaml
Building_Blocks implementan:
  
  P2 (Specialization + Teamwork):
    - Cada BB es specialist domain
    - Cross-BB teamwork para deliverables complejos
  
  P8 (Internal Entrepreneurship):
    - Cada BB opera como "business within business"
    - BB1 entrega innovation a BB2/customers
    - BB4 descubre opportunities para BB1
  
  P10 (Professional Clustering):
    - BB agrupa professionals similares
    - Engineers cluster, Sales cluster, etc.
```

---

## Referencias Cruzadas

- **Principios detallados:** `CORE/00_Manifiesto.md` §3
- **Invariante I2 Ortogonalidad:** `CORE/03_Arquitectura.md`
- **Composición Outside-In:** `CORE/01_Primitivos.md` §7
- **Trazabilidad arquitectural:** `CORE/06_Trazabilidad.md`
- **Antipatrones estructurales:** `APLICACION/A2_Antipatrones.md` §2
- **Patrones org:** `APLICACION/A1_Patrones.md`amental.md` §6
- **Observable I1 (Velocidad decisional):** `DOMINIOS/D2_Percepcion.md` §3.1
- **Observable I2 (Salud talento):** `DOMINIOS/D2_Percepcion.md` §3.2
- **Casos estructurales:** `REFERENCIA/R1_Casos.md`
