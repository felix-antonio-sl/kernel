# D4_Operacion

**Versión:** 1.0.0 | **Estado:** Definitivo | **Audiencia:** Engineering Managers, Tech Leads, Teams

---

## REFERENCIAS RÁPIDAS

```yaml
Métricas_Flow_Core:
  Cycle_Time: §2 - Días start→done (target <5d excelente, <10d MVO)
  WIP: §2 - Items In Progress (target <1.5× team size)
  Throughput: §2 - Items/semana completados (track trend)
  Flow_Efficiency: §2 - % tiempo value-add vs wait (target >25%, >40% world-class)

Métricas_DORA:
  Deploy_Frequency: §4 - Elite multiple/día, High daily, Medium weekly
  Lead_Time_for_Changes: §4 - Commit→prod (Elite <1hr, High <1d)
  Change_Failure_Rate: §4 - % deploys con incident (Elite <5%)
  Time_to_Restore: §4 - Incident→resolved (Elite <1hr)

Conceptos_Core:
  Two-Pizza_Teams: §1 - 5-9 personas (communication overhead O(n²))
  Teams_as_Assets: §1 - Permanentes, no proyectos temporales
  20%_Rule: §5 - Mínimo 20% capacity a health (tech debt, automation)
  70/20/10_Mix: §7 - 70% planificado, 20% reactivo, 10% exploración
  Carry-Over_Work: §7.1 - Permitir flow entre sprints (no commitment culture)

Prácticas_Esenciales:
  CI/CD_Pipeline: §4 - Lint→test(≥60% MVO, ≥80% post-MVO)→build→deploy
  Blue-Green_Deployment: §4 - Instant rollback via switch
  Canary_Deployment: §4 - Gradual rollout 5%→25%→50%→100%
  Feature_Flags: P23 - Deploy código desacoplado de release
  On-Call_Rotation: §9 - 1 semana shifts, runbooks, 4+ personas mínimo

Antipatrones:
  Deseconomías_Escala: §1.1 - Más personas ≠ más rápido (communication O(n²))
  Project_Thinking: §1 - Teams temporales → conocimiento perdido
  Tech_Debt_Acumulación: §5 - Score >50 requiere 50% capacity remediation

Métricas:
  O_Score: §8 - Excelencia operacional (Cycle 30% + WIP 20% + Deploy 30% + Complete 20%)
  Tech_Debt_Score: §5 - 0-100 lower better (<15 excelente, >50 crítico)
  Typical_MVO: 60-70
  Excellence: 80-90

Patrones:
  P52_Crisis_Management: CORE/08 - Estabilización emergencia (H<45)
  P55_Walking_Skeleton: §12.1 - Sistema E2E mínimo funcional
  P23_Feature_Flags: APLICACION/A1 - Deployment sin release

Cross-References:
  D2_Percepcion.md §3.3: IN3 Eficiencia Flujo (observable vinculado)
  D3_Decision.md §3.1: Schedules as forecasts (no commitment)
  CORE/02_Ciclo_Fundamental.md §4: Fase Act (A1 Plan, A2 Specify, A3 Execute)
  APLICACION/A1_Patrones.md §4: Patrones DevOps detallados
```

---

## Responsabilidad

**OPERACIÓN ejecuta FLUJOS DE VALOR:** Delivery continuo, teams estables, excelencia técnica, activos que evolucionan.

**Pregunta clave:** ¿Cómo entregamos valor de forma continua y sostenible?

---

## §0. QUICK START: OPERACIÓN MÍNIMA VIABLE (MVO)

**Objetivo**: Delivery continuo funcionando en 6-8 semanas.

### MVO Checklist (6-8 semanas)

```yaml
Week_1-2: Teams Setup
  ☐ Teams 5-9 personas (two-pizza rule)
  ☐ Cross-functional si posible (Eng + Product + Design minimum)
  ☐ Ownership claro (products/services asignados)
  ☐ Manager/Tech Lead identificado
  
Week_3-4: Flow Basics
  ☐ Methodology: Scrum O Kanban (elige 1, no híbrido yet)
  ☐ WIP limits: <1.5× team size (ej: team 7 → WIP max 10)
  ☐ Cycle time tracking (Jira, Linear configuration)
  ☐ Daily standups (15 min strict)

Week_5-6: CI/CD Básico
  ☐ Automated tests (minimum unit tests, target >60% coverage)
  ☐ CI pipeline (lint + test en cada commit)
  ☐ Deployment pipeline staging (automated push staging)
  ☐ Manual deployment prod (con checklist)

Week_7-8: Tech Debt Governance
  ☐ 20% rule adopted (min 1 día/sprint para health work)
  ☐ Tech debt score baseline calculado
  ☐ Quality gates básicos (tests must pass, coverage >60%)

Output_MVO:
  - Teams estables operando
  - Cycle time <10 días (not great but functional)
  - Deploy staging automated
  - Tech debt managed (not growing)
  - Typical O_Score post-MVO: 60-70

Next_Steps_Post_MVO:
  - Reduce cycle time <5 días (optimize flow)
  - Automate deployment prod (CI/CD complete)
  - Add feature flags (P23)
  - Improve tech debt <30 (refactoring continuous)
```

---

### Métricas MVO (4 esenciales)

```yaml
Cycle_Time:
  - CRÍTICO: Avg días start → done
  - Target MVO: <10 días (good), <5 días (excellent post-MVO)
  - Tool: Jira, Linear analytics
  
Throughput:
  - IMPORTANTE: Items/week completados
  - Target: Stable or growing (trend más important que absolute)
  
WIP:
  - CRÍTICO: Items "In Progress" simultáneos
  - Target: <1.5× team size
  - Enforcement: Kanban board WIP limits o sprint commitment
  
Deploy_Frequency:
  - IMPORTANTE: Deploys to staging (prod manual OK initially)
  - Target MVO: Daily staging, Weekly prod minimum
  - Target post-MVO: Daily prod (DORA high performer)

Defer_Post-MVO:
  - Flow efficiency (calculate después que tienes data 3+ meses)
  - DORA full (lead time, change failure rate, MTTR)
  - Advanced: Auto-scaling, auto-rollback
```

---

### Ceremonies MVO (3 esenciales)

```yaml
Daily_Standup (15 min):
  - CRÍTICO: Yesterday, Today, Blockers
  - Skip: Problem-solving in standup (use parking lot)
  
Weekly_Planning (1-2 hrs):
  - CRÍTICO: Prioritize top items, commitment sprint/week
  - Skip initially: Estimation poker (use historical cycle time)
  
Bi-Weekly_Retrospectiva (1 hr):
  - CRÍTICO: What worked, what didn't, max 3 action items
  - Skip initially: Deep-dive analysis (save para post-MVO)

Defer_Post-MVO:
  - Backlog refinement (si backlog crece >50 items, agregar)
  - Sprint review (si stakeholders demandan demos)
  - Quarterly planning (si roadmap estable)
```

---

### Cuando Skip MVO

```yaml
Ya_Tienes_MVO_Si:
  - Teams estables >6 meses
  - Cycle time <7 días consistent
  - CI/CD operational
  - O_Score >70
  
  → Skip to optimization (§5-§12 avanzado)

MVO_No_Suficiente_Si:
  - Org >100 personas (requiere platform teams P02)
  - SaaS crítico 99.9%+ uptime (requiere SRE P10)
  - Deploy frequency target >5/día (requiere advanced CI/CD)
  
  → Use full D4 desde inicio
```

---

## §1. TEAMS ESTABLES

### Principio P4 Aplicado

```yaml
Asset_Thinking:
  - Teams son activos de largo plazo, NO proyectos temporales
  - Team permanece, trabajo fluye a través del team
  - Acumulación conocimiento, mejora continua

Project_Thinking (anti-patrón):
  - Teams se forman para proyecto, se disuelven al completar
  - Conocimiento se pierde en cada disolución
  - Ramp-up perpetuo, nunca alto rendimiento sostenible
```

---

### Configuración Team Óptimo

```yaml
Tamaño: 5-9 personas (Two-Pizza Team)
  - <5: Insuficiente diversidad skills, vulnerable bus factor
  - >9: Coordination overhead crece O(n²)

Composición_Cross-Functional:
  - Eng Backend: 2-3 personas
  - Eng Frontend: 1-2 personas
  - QA/SDET: 1 persona (idealmente automation)
  - Product Manager: 0.5-1 persona (puede shared)
  - Designer: 0.3-0.5 persona (shared OK)

Ownership:
  - E2E: Desde ideación hasta producción + mantenimiento
  - On-call: Team rotación on-call propio servicio
  - Metrics: Team responsable OKRs específicos

Estabilidad:
  - Cambios roster <20%/año
  - No reassignments frecuentes (cada 3-6 meses)
  - Si team crece >9 → Split en 2 teams (no diluir)
```

---

### §1.1. DESECONOMÍAS DE ESCALA

#### Principio Fundamental

```yaml
Ley_Contraintuitiva: En desarrollo software, más personas ≠ más rápido
                      Agregar personas puede hacer trabajo MENOS eficiente

Razón: Software development tiene deseconomías de escala
       (opposite a manufactura, que tiene economías de escala)
```

---

#### Causa 1: Comunicación Exponencial

```yaml
Fórmula_Brooks:
  Communication_Paths = n(n-1)/2
  donde n = team size

Ejemplos:
  Team_5: 5(4)/2 = 10 paths
  Team_9: 9(8)/2 = 36 paths (+260% vs team 5)
  Team_15: 15(14)/2 = 105 paths (+950% vs team 5)

Efecto:
  - Más tiempo en meetings, sincronización, alignment
  - Menos tiempo en trabajo productivo (coding, testing, design)
  - Información degradada en cada handoff

Consecuencia:
  Team de 15 NO es 3x más productivo que team de 5
  Frecuentemente es MENOS productivo en total
  (overhead > beneficio de headcount adicional)
```

---

#### Causa 2: Especialización y Colas

```yaml
Anti-Patrón_Especialización:
  División trabajo: Analyst → Designer → Coder → Tester → DevOps
  
  Problemas:
    1. Queues: Cada especialista tiene backlog propio
       - Analyst termina análisis → espera en queue Designer
       - Designer termina → espera en queue Coder
       - ...
       - Resultado: 80% tiempo esperando, 20% trabajando
    
    2. Handoffs: Cada transición pierde información
       - Analyst → Designer: Matices contextuales perdidos
       - Designer → Coder: Intención design no capturada
       - Knowledge loss acumulativo ~10-20% por handoff
    
    3. Rework: Descubrimientos tardíos requieren volver atrás
       - Tester descubre problema arquitectural semana 4
       - Requiere re-analysis, re-design, re-code
       - Costo 5-10x vs descubrimiento temprano

Alternativa_T-Shaped:
  - Miembros con depth en especialidad + breadth en otras áreas
  - Engineer puede hacer design básico, testing propio
  - Designer puede escribir HTML/CSS
  - Reduce handoffs, elimina colas, acelera flow
```

---

#### Causa 3: Large Batches = Large Risk

```yaml
Proyecto_Grande:
  - Más scope → Más puede ir mal
  - Más tiempo → Más cambios externos (mercado, tech, regulación)
  - Más personas → Más communication overhead
  - Más riesgo técnico, mercado, ejecución

Proyecto_Pequeño:
  - Poco scope → Poco riesgo
  - Poco tiempo → Entorno estable
  - Pocas personas → Low overhead
  - Fail fast, fail cheap (si falla, pérdida pequeña)

Ejemplo:
  Proyecto_$10M_50_personas_18_meses:
    - Riesgo técnico: Alto (muchas integraciones, incógnitas)
    - Riesgo mercado: Alto (18 meses → competencia puede cambiar)
    - Riesgo ejecución: Alto (50 personas → coordination nightmare)
    - Si falla: Pérdida $10M + 18 meses + 50 personas
  
  10_Proyectos_$1M_5_personas_3_meses:
    - Riesgo por proyecto: Bajo
    - Si 1 falla: Pérdida $1M (no $10M)
    - Aprendizaje rápido: Feedback cada 3 meses, pivotes posibles
    - Portfolio effect: 7 de 10 exitosos → ROI superior
```

---

#### Small Teams, Small Batches: The Solution

```yaml
Recomendación_KERNEL:
  Team_Size: 5-9 personas (Two-Pizza Team)
  Batch_Size: Features deliverable en <2 semanas
  WIP_Limit: <15 items simultáneos para team 7 personas

Justificación:
  - Minimiza communication overhead (manageable paths)
  - Minimiza handoffs (cross-functional teams)
  - Minimiza riesgo (small batches, fast feedback)
  - Maximiza flow efficiency (poco tiempo waiting)

Contraejemplo_Clásico:
  "Contratar 20 developers más para acelerar proyecto"
  
  Realidad:
    - Mes 1-2: Ramp-up (productivity cae mientras aprenden)
    - Mes 3-6: Overhead sube (meetings, coordination, conflicts)
    - Mes 6+: Velocity puede ser MENOR que team original pequeño
    - Tech debt sube (inconsistencias de 20 personas sin alignment)

Alternativa_Correcta:
  - Mantener team pequeño (7-9 max)
  - Reducir scope (focus en 70% más valioso)
  - Incrementar quality (reduce rework futuro)
  - Resultado: Más rápido, mejor quality, menor costo
```

---

#### Implicaciones para KERNEL

```yaml
Diseño_Organizacional:
  - Preferir múltiples teams pequeños vs pocos teams grandes
  - 4 teams de 7 personas > 2 teams de 14
  - Autonomía por team (minimize dependencies)

Portfolio_Management:
  - Preferir muchas initiatives pequeñas vs pocas grandes
  - 10 proyectos $500K > 1 proyecto $5M
  - Permite fail fast, learning rápido, pivotes

Planning:
  - NO "agregar más gente" para acelerar
  - SÍ "reducir scope" o "aceptar timeline realista"
  - Ley Brooks: "Adding people to late project makes it later"
```

---

## §2. FLOW METRICS

### Métricas Core (4)

```yaml
1. CYCLE_TIME:
   Definición: Tiempo desde "start work" hasta "done"
   Cálculo: Avg(fecha_done - fecha_start) para items completados
   Target: <5 días para user stories, <2 días para bugs
   Interpretación:
     - <3 días: Excelente
     - 3-7 días: Bueno
     - >7 días: Attention (likely blockers)

2. THROUGHPUT:
   Definición: # items completados por unidad tiempo
   Cálculo: Count(items_done) / periodo (típicamente semana)
   Target: Variable por team, track trend
   Interpretación:
     - Creciendo: Mejora capacidad
     - Estable: Predictable delivery
     - Cayendo: Investigar (tech debt? dependencies?)

3. WIP (Work in Progress):
   Definición: # items activos simultáneamente
   Cálculo: Count(items estado "In Progress")
   Target: <15 items para team 7 personas
   Interpretación:
     - WIP alto → Context switching, cycle time sube
     - WIP bajo → Foco, flow óptimo

4. FLOW_EFFICIENCY:
   Definición: % tiempo value-add vs tiempo wait
   Cálculo: (Tiempo_work / Tiempo_total) × 100
   Target: >40% (world-class), >25% (good)
   Interpretación:
     - <15%: Mayoría tiempo esperando (handoffs, blockers)
     - 25-40%: Saludable
     - >40%: Excelente
```

---

### Ejemplo Cálculo Flow Efficiency

```yaml
Item: User_Story_123
Timeline:
  - Lunes 10:00: Priorizado (start)
  - Lunes 14:00: Waiting for design (4 hrs)
  - Martes 09:00: Design ready, dev starts (wait 19 hrs)
  - Martes 15:00: Coding (work 6 hrs)
  - Miércoles 10:00: Waiting code review (wait 19 hrs)
  - Miércoles 12:00: Review (work 2 hrs)
  - Miércoles 15:00: Waiting QA (wait 3 hrs)
  - Miércoles 18:00: QA (work 3 hrs)
  - Jueves 09:00: Done (wait 15 hrs)

Totales:
  - Tiempo_total: 47 hrs (lunes 10:00 → jueves 09:00)
  - Tiempo_work: 11 hrs (4+6+2+3)
  - Tiempo_wait: 36 hrs
  - Flow_Efficiency: 11/47 = 23% (borderline)

Mejora:
  - Reducir wait code review (19 hrs → CI auto-review partial)
  - Reducir wait QA (automation en vez de manual handoff)
  - Target efficiency: 40% (necesita reducir waits 50%)
```

---

## §3. KANBAN VS SCRUM

### Comparación

| Dimensión | Kanban | Scrum |
|-----------|---------|-------|
| **Iteraciones** | Continuo | Sprints time-boxed (1-4 semanas) |
| **Roles** | No roles prescritos | PO, SM, Dev Team |
| **Commitment** | No compromiso sprint | Compromiso sprint backlog |
| **Cambios** | Pueden entrar mid-flow | Solo entre sprints |
| **WIP Limits** | Explícito, por columna | Implícito (sprint capacity) |
| **Métricas** | Cycle time, throughput | Velocity, burndown |
| **Mejor para** | Support, mantenimiento, flow continuo | Features grandes, roadmap planificado |

---

### Cuándo Usar Cada Uno

```yaml
Scrum_Ideal:
  - Trabajo planificado >70%
  - Features multi-semana
  - Need ceremonies (planning, retro, review)
  - Team nuevo necesita estructura

Kanban_Ideal:
  - Trabajo impredecible >40%
  - Support/bugs frecuentes
  - Cycle time corto (<3 días)
  - Team maduro, auto-organizado

Scrumban (Híbrido):
  - Sprints de Scrum + WIP limits de Kanban
  - Ceremonies Scrum pero flow continuo Kanban
  - Usado por 60% teams maduros
```

---

## §4. CI/CD (CONTINUOUS INTEGRATION/DEPLOYMENT)

### Pipeline Mínimo Viable

```yaml
Stage_1_CI (Continuous Integration):
  Trigger: Cada push a branch
  Steps:
    1. Lint (code style, formato)
    2. Unit tests (>80% coverage target)
    3. Build (compilar, empaquetar)
    4. Integration tests
    5. Security scan (SAST, dependency check)
  Duration: <10 min (si >10 min, split o paralelizar)
  Output: Artifact versionado + test report

Stage_2_CD_Staging (Continuous Deployment):
  Trigger: CI passed + merge a main branch
  Steps:
    1. Deploy to staging environment
    2. Smoke tests (critical paths)
    3. Performance tests (load, stress)
  Duration: <15 min
  Output: Staging environment updated

Stage_3_CD_Production:
  Trigger: Manual approval O automated (si confidence alta)
  Steps:
    1. Deploy canary (5% traffic)
    2. Monitor metrics 15 min (error rate, latency, business KPIs)
    3. IF metrics OK: Deploy 25% → 50% → 100%
    4. IF metrics NOK: Rollback automático
  Duration: 30-60 min (gradual rollout)
  Output: Production updated O rollback

Rollback_Strategy:
  - Blue-Green: Instant rollback (switch DNS/load balancer)
  - Canary: Stop rollout, revert canary instances
  - Feature flags: Disable feature remotely sin redeploy
```

---

### Métricas DevOps (DORA)

```yaml
4_Métricas_DORA (DevOps Research & Assessment):

1. Deployment_Frequency:
   Definición: ¿Qué tan seguido deployamos a prod?
   Elite: Multiple deploys per day
   High: Weekly-Daily
   Medium: Monthly-Weekly
   Low: <Monthly

2. Lead_Time_for_Changes:
   Definición: Tiempo commit → production
   Elite: <1 hr
   High: 1 día - 1 semana
   Medium: 1 semana - 1 mes
   Low: >1 mes

3. Change_Failure_Rate:
   Definición: % deploys que causan incident
   Elite: <5%
   High: 5-15%
   Medium: 15-30%
   Low: >30%

4. Time_to_Restore_Service:
   Definición: Tiempo detectar incident → resolver
   Elite: <1 hr
   High: <1 día
   Medium: 1 día - 1 semana
   Low: >1 semana
```

---

## §5. TECH DEBT MANAGEMENT

### 20% Rule

```yaml
Regla: Minimum 20% capacity dedicado a health (no solo features)

Health_Work_Includes:
  - Tech debt remediation (refactoring, modernización)
  - Automation (tests, CI/CD, monitoring)
  - Performance optimization
  - Security hardening
  - Developer experience (tooling, docs)

Ejemplo_Team_10_Eng:
  Capacity_Total: 10 eng × 40 hrs/semana × 2 semanas sprint = 800 hrs
  Capacity_Features: 640 hrs (80%)
  Capacity_Health: 160 hrs (20%)
  
  Health_Sprint_Backlog:
    - Refactor legacy module X (60 hrs)
    - Add integration tests service Y (40 hrs)
    - Upgrade framework Z (30 hrs)
    - Fix performance bottleneck (20 hrs)
    - Docs API endpoint W (10 hrs)
```

---

### Tech Debt Score

```yaml
Debt_Score (0-100, lower is better):
  Componentes:
    - Code_Coverage: 100 - coverage% (target <20)
    - Code_Duplication: % duplicated code (target <5%)
    - Complexity: Avg cyclomatic complexity (target <10)
    - Vulnerabilities: # critical + high vulns (target 0)
    - Legacy_Dependencies: % dependencies >2 years old (target <20%)

  Fórmula:
    Debt_Score = 0.25*Coverage_Gap + 0.20*Duplication + 0.20*Complexity + 
                 0.25*Vulns + 0.10*Legacy

  Interpretación:
    <15: Excelente (health bajo mantenimiento OK)
    15-30: Bueno (monitorear, 20% rule suficiente)
    30-50: Atención (incrementar a 30% capacity health)
    >50: Crítico (50% capacity debt remediation urgente)
```

---

## §6. ACTIVOS CONTINUOS

### Software-as-Asset

```yaml
Asset_Lifecycle:
  1. INCEPTION (0-6 meses):
     - Build MVP
     - Product-market fit search
     - Metrics: User adoption, feedback

  2. GROWTH (6 meses - 3 años):
     - Scale users, features
     - Optimize performance, UX
     - Metrics: Revenue, retention, NPS

  3. MATURITY (3-10 años):
     - Maintain, optimize costs
     - Incremental features
     - Metrics: TCO, uptime, efficiency

  4. DECLINE O MODERNIZATION (10+ años):
     - Opción A: Retire (migrate users a alternativa)
     - Opción B: Modernize (rebuild, refactor mayor)
     - Metrics: Migration success, cost savings

Anti-Patrón: "Sunset sin plan"
  - App deployed, team disuelto
  - 3 años después: App legacy crítica, nadie entiende
  - Costo mantenimiento 10x vs si hubiera team continuo
```

---

### Asset Decay Detection

```yaml
Señales_Decay:
  - Deployment frequency cae >50% vs año anterior
  - Tech debt score sube >20 puntos
  - Bus factor = 1 (solo 1 persona entiende sistema)
  - Vulnerabilities críticas sin fix >30 días
  - Time-to-fix bugs crece >100%

Ejemplo_App_Decaying:
  2022: Deploy frequency 2×/semana, Tech debt 18
  2023: Deploy frequency 1×/mes (-90%), Tech debt 42 (+24)
  2024: Deploy frequency 1×/trimestre, Tech debt 68 (+26)
  → Acción: Assign 2 eng full-time O sunset planificado
```

---

## §7. WORK MIX (70/20/10)

### Regla Composición Backlog

```yaml
70% Planificado (OKRs, Roadmap):
  - Features alineadas a OKRs
  - Tech debt planificado
  - Initiatives estratégicas

20% No-Planificado Reactivo:
  - Bugs production
  - Support escalations
  - Hotfixes
  - Quick wins oportunistas

10% Exploración/Innovación:
  - Experiments, spikes técnicos
  - Learning new tech
  - Innovation time (ej: Google 20%)

Ejemplo_Sprint_Team:
  Capacity: 100 hrs
  Planificado: 70 hrs (4 features roadmap + 2 tech debt items)
  Buffer_Reactivo: 20 hrs (asumimos ~3 bugs + 1 escalation)
  Exploración: 10 hrs (1 engineer experimenta tech X)

Si_Reactivo_Excede_20%:
  - Síntoma: Planning deficiente o entorno volátil
  - Acción: Root cause analysis
    - ¿Bugs porque quality baja? → Incrementar 20% a health (tests)
    - ¿Escalations porque missing features? → Re-priorizar roadmap
```

---

### §7.1. CARRY-OVER WORK: Flow Between Iterations

#### Principio Anti-Scrum

```yaml
Scrum_Estricto:
  - Prohibe carry-over: Trabajo debe completarse en sprint
  - Si no se completa → Vuelve a backlog, re-estimado próximo sprint
  - Sprint commitment es "sagrado"

KERNEL/Xanpan_Approach:
  - Permite carry-over: Trabajo fluye entre sprints
  - Si no se completa → Continúa en próximo sprint
  - No hay commitment rígido, hay forecast probabilístico

Justificación_Carry-Over:
  1. Evita forzar stories demasiado pequeñas que pierden valor negocio
  2. Permite features multi-sprint sin artificial splitting
  3. Refleja realidad: Algunos dominios (embedded, C++) requieren stories grandes
  4. Reduce "dry-stone walling" (buscar task pequeña para llenar sprint final)
```

---

#### Probabilistic Delivery

```yaml
Concepto: No commitment "todo o nada", sino probabilidades decrecientes

Modelo:
  Sprint_Planning_Capacity: 80 points
  
  Backlog_Priorizado:
    - Story 1 (priority 1): 13 points → 95% probabilidad delivery
    - Story 2 (priority 2): 21 points → 85% probabilidad
    - Story 3 (priority 3): 18 points → 70% probabilidad
    - Story 4 (priority 4): 15 points → 50% probabilidad
    - Story 5 (priority 5): 13 points → 30% probabilidad
    - Total: 80 points
  
  Resultado_Real (sprint ends):
    - Story 1: ✅ Done
    - Story 2: ✅ Done
    - Story 3: ⏳ 60% complete → Carry over
    - Story 4: ⏳ 20% started → Carry over
    - Story 5: ❌ Not started → Back to backlog
  
  Próximo_Sprint:
    - Story 3 (carry, 40% resta): Priority 1
    - Story 4 (carry, 80% resta): Priority 2
    - New Story 6: Priority 3
    - ...

Ventaja:
  - Team siempre trabaja en highest priority
  - No artificial completion forzado (shortcuts, tech debt)
  - Flow smooth, no hard boundaries sprint
```

---

#### No Commitment Culture

```yaml
Scrum_Tradicional:
  - Team "commits" a sprint backlog
  - No cumplir = "failure", presión social
  - Incentiva sandbagging (aceptar poco trabajo)

KERNEL_Approach:
  - Team forecasts, no commits
  - "Planeamos 80 points, probablemente haremos 60-70"
  - No completion = Normal (reflected en velocity histórico)
  - Incentiva ambición (no penalty por intentar más)

Comunicación_Stakeholder:
  ❌ Malo: "Commitimos a Story 1, 2, 3, 4"
           → Sprint termina, solo Story 1, 2 completadas
           → "Team falló commitment" (percepción negativa)
  
  ✅ Bueno: "Story 1 casi segura (95%), Story 2 muy probable (80%),
            Story 3 probable (70%), Story 4 posible (50%)"
           → Sprint termina, Story 1, 2 completadas
           → "Within expected range" (percepción realista)
```

---

#### Carry-Over Governance

```yaml
Regla_1_Re-Prioritize:
  - Carry-over NO tiene prioridad automática
  - Al inicio próximo sprint, re-evaluar contra nuevo trabajo
  - Posible que carry-over baje prioridad si surge urgencia mayor

Regla_2_Max_Carry_Over:
  - Max 30-40% capacity puede ser carry-over
  - Si >40% → Señal problema (stories demasiado grandes o blockers sistémicos)

Regla_3_Track_Age:
  - Monitorear "age" de work items
  - Si item >3 sprints sin completar → Red flag
  - Posibles causas:
    - Scope creep (story creciendo)
    - Blockers no resueltos
    - Underestimated effort
  - Acción: Split story O re-scope O escalate blocker

Ejemplo_Unhealthy_Carry_Over:
  Sprint_1: Story X (50 points) started
  Sprint_2: Story X (30% complete, carry over)
  Sprint_3: Story X (50% complete, carry over)
  Sprint_4: Story X (70% complete, carry over)
  Sprint_5: Story X FINALLY done
  
  Problema:
    - 5 sprints = 10 semanas para 1 story
    - Bloqueó capacity 5 sprints
    - Probablemente scope creció durante desarrollo
  
  Solución_Retrospectiva:
    - ¿Por qué story tan grande? → Necesita splitting pattern
    - ¿Hubo blockers ocultos? → Make visible, escalate faster
    - ¿Estimación muy optimista? → Calibrate future estimates
```

---

#### Suspended Work (Yellow Cards)

```yaml
Concepto: Permitir suspender trabajo si surge urgencia

Xanpan_Yellow_Cards:
  - Work no planificado (incident, escalation, oportunidad)
  - Puede interrumpir trabajo planificado
  - Team member suspend blue card → Atiende yellow card

Ejemplo:
  Developer trabajando Story 3 (blue, planned)
  Production incident SEV2 ocurre (yellow, unplanned)
  → Suspend Story 3, work yellow card 4 hrs
  → Resolve incident
  → Resume Story 3
  
  Efecto_Carry_Over:
    - Story 3 toma más tiempo (interruption)
    - Probablemente carry over a próximo sprint
    - Normal, esperado, trackeable

Tracking:
  - Count yellow card hours
  - If yellows >20% capacity → Investigate root causes
    - ¿Calidad baja? → Más testing, reduce bugs
    - ¿Proceso roto? → Arreglar handoffs
    - ¿Falta features? → Re-prioritize roadmap
```

---

#### Metrics for Carry-Over

```yaml
Metric_1_Carry_Over_Rate:
  Fórmula: (Points_Carried / Total_Points_Planned) × 100
  Target: <30%
  Interpretation:
    - <20%: Excellent (planificación accurate)
    - 20-30%: Good (normal variation)
    - 30-50%: Attention (posible overcommitment o blockers)
    - >50%: Problem (systemic issue)

Metric_2_Completion_Rate:
  Fórmula: (Stories_Done / Stories_Started) × 100
  Target: >70%
  Interpretation:
    - >80%: Excellent
    - 70-80%: Good
    - <70%: Attention (demasiados starts, pocos finishes)

Metric_3_Avg_Story_Age:
  Fórmula: Avg(days desde start hasta done) para stories completadas
  Target: <10 días (2 sprints de 1 semana)
  Interpretation:
    - <7 días: Excellent (flow rápido)
    - 7-14 días: Good
    - >14 días: Attention (stories demasiado grandes o blockers)

Dashboard_Example:
  Sprint_10_Metrics:
    - Planned: 75 points (5 stories)
    - Completed: 53 points (3 stories)
    - Carried: 22 points (2 stories)
    - Carry-Over Rate: 29% ✅ (within target)
    - Completion Rate: 60% ⚠️ (below target, investigate)
    - Avg Age: 8 días ✅
```

---

## §8. O_SCORE (0-100)

### Fórmula Operación

```yaml
O_Score: Métrica agregada excelencia operacional

Fórmula:
  O_Score = (
    0.30 * Cycle_Time_Score +
    0.20 * WIP_Compliance_Score +
    0.30 * Deploy_Frequency_Score +
    0.20 * Completion_Rate_Score
  )

Componentes:

  Cycle_Time_Score (0-100):
    <3 días: 95-100
    3-7 días: 75-90
    7-14 días: 50-70
    >14 días: 0-45
  
  WIP_Compliance_Score (0-100):
    WIP <1.5× team size: 90-100
    WIP 1.5-2.0×: 70-85
    WIP >2.0×: 0-65
  
  Deploy_Frequency_Score (0-100):
    DORA Elite (multiple/día): 95-100
    DORA High (weekly-daily): 75-90
    DORA Medium (monthly-weekly): 50-70
    DORA Low (<monthly): 0-45
  
  Completion_Rate_Score (0-100):
    >80% stories started completadas: 90-100
    70-80%: 75-85
    <70%: 0-70

Interpretación:
  >75: Operación excelente (flow rápido, predecible)
  60-75: Operación funcional (gaps menores)
  <60: Operación débil (blockers sistémicos)

Típico post-MVO: 60-70
Típico excelencia: 80-90
```

---

## §9. ON-CALL & INCIDENT MANAGEMENT

### On-Call Rotation

```yaml
Configuración_Mínima:
  - Team size mínimo: 4 personas (para rotation sustainable)
  - Shift duration: 1 semana (balance freshness vs handoff overhead)
  - Escalation: Primary on-call → Secondary → Manager → CTO

Compensación:
  - Pay: $X por día on-call + $Y por incident resuelto
  - Time off: 1 día off post on-call week pesada (>3 incidents)

Runbooks:
  - Cada alert tiene runbook asociado
  - Runbook: Diagnosis steps + remediation actions + escalation
  - Update runbook después cada incident (continuous learning)

Ejemplo_Alert:
  Alert: "DB Connections >90% pool"
  Runbook:
    1. Check: ¿Spike legítimo tráfico o leak connections?
    2. If spike: Scale read replicas (click button X)
    3. If leak: Restart service Y, monitor 5 min
    4. If persists: Escalate to DB team (Slack #db-oncall)
```

---

### Incident Severity

```yaml
SEV1 (Critical):
  - Impacto: Servicio core down, revenue loss
  - Response SLA: <15 min acknowledge, <1 hr resolve
  - Postmortem: Mandatorio, dentro 48 hrs

SEV2 (High):
  - Impacto: Feature degradada, subset usuarios afectados
  - Response SLA: <1 hr acknowledge, <4 hrs resolve
  - Postmortem: Recomendado

SEV3 (Medium):
  - Impacto: Minor issue, workaround existe
  - Response SLA: <4 hrs acknowledge, <1 día resolve
  - Postmortem: Opcional

SEV4 (Low):
  - Impacto: Cosmético, no functionality loss
  - Response SLA: Best effort
  - Postmortem: No
```

---

## §10. AGENTES EJECUCIÓN IA

### Modos Delegación Operación

```yaml
M3_Copilot_Coding:
  Función: Genera código bajo demanda (GitHub Copilot, Codeium)
  Input_Humano: Comment "// función que valida email"
  Output_IA: Código completo función
  Humano: Revisa, acepta/modifica
  Modo: M3 (Habilitar)
  Aceleración: 30-50% velocity (según estudios)

M4_Quality_Gates_Automated:
  Función: Bloquea merge si quality thresholds no cumplidos
  Input: PR con código nuevo
  Checks_Automáticos:
    - Coverage <80% → Block
    - Vulnerabilities high/critical → Block
    - Lint errors → Block
    - Tests failing → Block
  Humano: Fix issues, puede override con justificación (exceptional)
  Modo: M4 (Controlar)

M6_Auto_Deploy_CI_CD:
  Función: Deploy automático si tests passed
  Trigger: Merge to main branch
  Pipeline:
    1. Run CI tests
    2. IF all green: Deploy staging
    3. Run smoke tests staging
    4. IF pass: Deploy canary prod (5%)
    5. Monitor 15 min
    6. IF metrics OK: Rollout 100%
  Humano: Monitorea dashboards, puede pausar deploy manualmente
  Modo: M6 (Ejecutar)
  Beneficio: Lead time <1 hr (vs días manual)

M6_Auto_Scaling:
  Función: Escala infra según demanda
  Input: CPU >80% durante 5 min
  Acción: +2 instances
  Input: CPU <30% durante 30 min
  Acción: -1 instance (min 2)
  Humano: Define reglas, monitorea costs
  Modo: M6 (Ejecutar)

M6_Auto_Rollback:
  Función: Rollback automático si metrics degradan
  Trigger: Error rate >5% O latency p99 >2× baseline
  Acción:
    1. Stop rollout canary
    2. Revert canary instances to previous version
    3. Alert on-call engineer (Slack + PagerDuty)
  Humano: Investiga root cause, fix, re-deploy
  Modo: M6 (Ejecutar)
  Beneficio: MTTR <5 min (vs 30 min manual)
```

---

## §11. CEREMONIES

### Weekly Cadence (Scrum)

```yaml
Lunes_09:00_Sprint_Planning (2 hrs):
  - Review OKRs, roadmap
  - Priorizar backlog top 20
  - Commitment sprint (X story points o Y items)
  - Break down features en tasks
  - Assign ownership

Diario_09:30_Daily_Standup (15 min):
  - Cada persona: Yesterday, Today, Blockers
  - Update board (Jira, Linear, etc.)
  - No problem-solving (parking lot)

Miércoles_14:00_Backlog_Refinement (1 hr):
  - Groom próximos 3 sprints
  - Clarificar acceptance criteria
  - Estimar effort (planning poker)

Viernes_15:00_Sprint_Review (1 hr):
  - Demo features deployed
  - Stakeholder feedback
  - Update roadmap si necesario

Viernes_16:00_Retrospectiva (1 hr):
  - What went well
  - What didn't
  - Action items próximo sprint (max 3)
  - Review action items sprint anterior
```

---

## §12. CONTINUOUS LEARNING

### 10% Time Innovation

```yaml
Concepto: 10% capacity dedicado a aprendizaje/innovación

Actividades:
  - Learn new tech (ej: engineer aprende Rust)
  - Experiments (ej: spike IA generativa para feature X)
  - Open source contributions
  - Internal tools (mejora developer experience)

Governance:
  - No requiere approval manager (dentro 10%)
  - Share learnings (demo, blog post, tech talk)
  - Some experiments → production (si valuable)

Ejemplo_Google_Gmail:
  - Gmail nació de 20% time engineer Paul Buchheit
  - Investment: ~40 hrs (1 semana 20% × 2 eng)
  - Return: $X billion product

Ejemplo_Team_Weekly:
  Team 8 eng × 40 hrs × 10% = 32 hrs/semana
  → 4 engineers dedican 1 día cada uno O 1 engineer dedica full week
  → Output: 2-3 experiments/mes, 20% se vuelven features
```

---

### §12.1. DESARROLLO EVOLUTIVO (Piecemeal Growth)

**Contexto operacional**: Esta sección mantiene perspectiva **operación continua** de cómo teams aplican desarrollo evolutivo day-to-day.

#### Principios Operacionales

```yaml
Gall's_Law_Applied:
  "Complex system that works evolved from simple system that worked"
  
  Implicación_Operacional:
    - Initiatives nuevas: Start walking skeleton (P55)
    - Features: Agregar incrementalmente (P54)
    - Código: Refactor continuo (P56), no big rewrites
    - Teams: Empezar pequeños 2-3, grow a 5-7 si validated

Stable_Intermediate_Forms:
  - Cada sprint entrega sistema deployable completo
  - NO: Componentes aislados integrados al final
  - SÍ: Vertical slices end-to-end cada iteración
  
  Operacionalmente:
    - Sprint planning: Priorizar stories que atraviesan capas
    - Definition of Done: Deployed to staging, E2E test passing
    - Demo: Sistema funcional mostrado, not slides

Walking_Skeleton_Week_1:
  - New initiative: Primera semana es skeleton técnico
  - Validación: Architecture funciona antes business logic
  - CI/CD: Establecido día 1 (no "add later")
  - Operacionalmente: Foundation para work subsecuente

Refactoring_Daily:
  - 20% capacity health incluye refactoring continuo
  - Boy Scout Rule: Each code touch → small improvement
  - Operacionalmente: Diseño emerge, no precede
  - NO big refactor projects (except tech debt crítico)
```

**Patrones completos**: Ver `APLICACION/A1_Patrones.md` §14:

- P54: Piecemeal Growth (Gall's Law, drivers, anti-pattern BDUF)
- P55: Walking Skeleton (definición, ejemplo E-commerce, beneficios)
- P56: Continuous Refactoring (TDD cycle, Boy Scout Rule, límites)

**Por qué refactorizado**: Estos son **patrones aplicables cross-domain** (arquitectura, producto, procesos), no solo operación. Mayor visibilidad en APLICACION/A1_Patrones permite reuso fuera contexto engineering teams.

---

## §13. NIVELES EXECUTION COGNITIVA

### Estratificación Ejecución

```yaml
Concepto:
  Execution NO es monolítica
  Opera en 3 niveles de abstracción desde actions atómicas hasta orchestration
  Separar qué hacer (orchestration) de cómo hacerlo (specification) de hacerlo (action)

Conexión_Ciclo_SDA:
  Act phase (CORE/02 §4) se subdivide en:
    Level 1 = A3 EJECUTAR → Ejecución atómica individual
    Level 2 = A2 ESPECIFICAR → Detalle operacional (recursos, params)
    Level 3 = A1 PLANIFICAR → Orchestration multi-step con dependencies

Nomenclatura:
  Este documento usa "Level 1-3" bottom-up (concrete → abstract)
  02_Ciclo_Fundamental.md usa "A1-A3" top-down (plan → specify → execute)
  Orden inverso pero conceptos equivalentes:
    - Level 1 (Action) = A3 (Ejecutar)
    - Level 2 (Specification) = A2 (Especificar)
    - Level 3 (Planning) = A1 (Planificar)
```

---

### Level 1: Action (Ejecutar) = A3

```yaml
Referencia: A3 EJECUTAR en CORE/02_Ciclo_Fundamental.md §4

Definición: Implementación directa de acción individual atómica

Características:
  - Granularidad: Single atomic operation
  - Contexto: Totalmente especificado (no ambiguity)
  - Autonomía: Puede ser fully automated
  - Reversibilidad: Depende del tipo de action

Ejemplos_Concretos:
  Communication:
    - Send email notification
    - Post message to Slack channel
    - Trigger webhook HTTP POST
    - Push notification to mobile app
  
  Data_Operations:
    - Update database record
    - Insert row to table
    - Delete file from S3
    - Write log entry
  
  Infrastructure:
    - Deploy artifact to server
    - Restart service
    - Scale instance count +1
    - Execute SQL script
  
  Business:
    - Block financial transaction
    - Approve purchase order
    - Create support ticket
    - Refund customer payment

Complejidad_Cognitiva: Mínima (execution determinística)
Agente_Típico: M6 Execute (action agents)
Human_Control: Out-of-loop si action bounded y reversible

Design_Principle:
  Actions deben ser:
    - Atómicas: Indivisible (all-or-nothing)
    - Idempotent: Safe to retry (mismo resultado)
    - Bounded: Scope claro, impact limited
    - Auditable: Logged con timestamp + actor
```

---

### Level 2: Action Specification (Especificar) = A2

```yaml
Referencia: A2 ESPECIFICAR en CORE/02_Ciclo_Fundamental.md §4

Definición: Detalle operacional de cómo ejecutar (resources, parameters, timing)

Características:
  - Granularidad: Action + contexto operacional
  - Contexto: Requiere micro-decisions sobre resources/config
  - Autonomía: Requires domain knowledge
  - Optimización: Trade-offs (cost, speed, quality)

Ejemplos_Concretos:
  Deployment_Specification:
    Action: Deploy service
    Specification:
      - Region: us-east-1 (proximity to users)
      - Instance type: t3.medium (cost vs performance)
      - Replicas: 3 (availability vs cost)
      - Deployment strategy: Blue-green (zero-downtime)
      - Rollback threshold: Error rate >5%
  
  Email_Specification:
    Action: Send notification
    Specification:
      - Channel: Email vs SMS vs push (user preference)
      - Template: Personalized content (user segment)
      - Timing: Immediate vs scheduled (timezone awareness)
      - Retry logic: 3 attempts with exponential backoff
  
  Transaction_Specification:
    Action: Process payment
    Specification:
      - Payment method: Credit card vs ACH (user choice)
      - Currency conversion: Real-time rate (if international)
      - Fraud check level: Standard vs enhanced (transaction size)
      - Settlement timing: Immediate vs batch (cost optimization)
  
  Backup_Specification:
    Action: Backup database
    Specification:
      - Storage tier: S3 Standard vs Glacier (access frequency)
      - Retention policy: 30 days daily, 12 months monthly
      - Compression: gzip level 6 (speed vs size)
      - Encryption: AES-256 (compliance requirement)

Complejidad_Cognitiva: Media (resource optimization, policy application)
Agente_Típico: M5 Co-produce (execution con human-configured policies)
Human_Control: On-loop (policies set a priori, system executes)

Design_Principle:
  Specification separada de action permite:
    - Reusable actions con different specs
    - Policy-driven execution (compliance, cost, performance)
    - A/B testing de specifications
    - Adaptation to context sin cambiar action logic

Ejemplo_Pattern:
  CI/CD Pipeline:
    - Action: "Deploy artifact" (Level 1, generic)
    - Specification: Environment-specific (dev, staging, prod)
      * Dev: t3.micro, 1 replica, no blue-green
      * Prod: t3.large, 5 replicas, blue-green, health checks
```

---

### Level 3: Action Planning (Orchestrar) = A1

```yaml
Referencia: A1 PLANIFICAR en CORE/02_Ciclo_Fundamental.md §4

Definición: Orchestration de múltiples actions en workflow coherente con dependencies

Características:
  - Granularidad: Multi-step plan con conditional logic
  - Contexto: Requiere strategic decisions sobre approach
  - Autonomía: High-level orchestration
  - Complejidad: Sequencing, parallelization, error handling

Ejemplos_Concretos:
  Incident_Response_Plan:
    Orchestration:
      1. Detect (sensing agent alerts)
      2. Diagnose (analyze logs, metrics)
      3. Mitigate (rollback OR scale OR patch)
      4. Communicate (status page, stakeholders)
      5. Document (postmortem)
    
    Dependencies:
      - Diagnose BEFORE mitigate
      - Communicate IN PARALLEL with mitigate
      - Document AFTER mitigate confirmed
    
    Conditional_Logic:
      IF severity SEV1:
        → Page on-call immediately
        → Update status page every 15min
      ELSE IF SEV2:
        → Slack notification
        → Update status page hourly
  
  Order_Fulfillment_Plan:
    Orchestration:
      1. Validate order (payment, inventory)
      2. Allocate inventory (nearest warehouse)
      3. Schedule picking (warehouse queue)
      4. Book carrier (optimize route)
      5. Dispatch shipment
      6. Notify customer (tracking info)
    
    Dependencies:
      - Allocate AFTER validate
      - Schedule AFTER allocate
      - Book carrier IN PARALLEL with picking
      - Notify AFTER dispatch
    
    Error_Handling:
      IF inventory allocation fails:
        → Backorder OR Cancel order (policy-driven)
      IF carrier booking fails:
        → Retry with alternative carrier
  
  Deployment_Strategy_Plan:
    Orchestration:
      1. Run tests (unit, integration, E2E)
      2. Deploy to canary (5% traffic)
      3. Monitor metrics (error rate, latency)
      4. IF metrics OK:
           → Gradual rollout (25%, 50%, 100%)
         ELSE:
           → Rollback canary
      5. Final validation
      6. Cleanup old version
    
    Parallelization:
      - Tests run in parallel (speed)
      - Monitoring runs continuously during rollout
    
    Rollback_Trigger:
      - Error rate >5% → Automatic rollback
      - Latency P95 >500ms → Automatic rollback
      - Manual intervention → Pause or rollback
  
  Crisis_Stabilization_Plan (P52):
    Orchestration:
      Week 1-4: Emergency stabilization
        - Daily morning situation (9am)
        - Priority actions execution (throughout day)
        - Daily evening progress (5pm)
        - Decision protocols (<4hrs critical)
      
      Week 5-12: Intensive diagnosis
        - Root cause analysis
        - Building blocks completeness
        - Energy/conflict mapping
      
      Dependencies:
        - Stabilization BEFORE diagnosis
        - Diagnosis BEFORE transformation
        - Exit criteria: H_Score >45 for 3 months

Complejidad_Cognitiva: Alta (strategic planning, coordination)
Agente_Típico: M3-M4 (human plans, AI assists OR orchestration agent)
Human_Control: In-loop (human approves plan) OR On-loop (orchestrator executes)

Design_Principle:
  Planning separado de specification/action permite:
    - Reusable plans para situations similares (playbooks)
    - Adaptation to context (conditional logic)
    - Parallel execution donde posible
    - Graceful degradation on failures
    - Human intervention points explícitos
```

---

### Progresión Execution & Delegación

```yaml
Mapping_to_M1_M6:
  
  Level_1_Action → M5-M6:
    IF action bounded AND reversible:
      → M6 Execute (fully autonomous)
      Ejemplo: Send notification, log entry
    ELSE IF action significant:
      → M5 Co-produce (human oversight)
      Ejemplo: Refund payment, delete data
  
  Level_2_Specification → M4-M5:
    Policies configured by human
    System executes con policies
    Ejemplo: CI/CD specs, backup policies
  
  Level_3_Planning → M2-M4:
    IF plan standard (playbook):
      → M4 Control (orchestrator executes, human monitors)
      Ejemplo: Incident response runbook
    ELSE IF plan novel:
      → M2-M3 Enable (human plans, AI assists)
      Ejemplo: Crisis stabilization custom plan

Cross-Level_Autonomy:
  Orchestration agent puede:
    - Plan workflow (Level 3, human-designed)
    - Specify resources (Level 2, policy-driven)
    - Execute actions (Level 1, autonomous)
  
  Ejemplo_Self_Driving_Car:
    - Planning: Route navigation (user sets destination)
    - Specification: Lane changes, speed adjustments (policy: cautious vs aggressive)
    - Action: Steering, braking, acceleration (fully autonomous)
```

---

### Separación Concerns: Orchestration vs Execution

```yaml
Anti-Pattern_Monolithic:
  ❌ Malo: Action que hace todo (orchestrate + specify + execute)
  
  Ejemplo_Problema:
    deploy_function():
      # Orchestration logic mixed with action
      if environment == "prod":
        replicas = 5
        run_tests()
        deploy_canary()
        monitor_metrics()
        if errors > threshold:
          rollback()
        else:
          gradual_rollout()
      cleanup()
    
    Problemas:
      - Cannot reuse deployment logic para different orchestrations
      - Cannot A/B test specifications easily
      - Cannot parallelize where possible
      - Hard to add human intervention points

Pattern_Separated:
  ✅ Bueno: Separar orchestration, specification, action
  
  Ejemplo_Solution:
    # Level 3: Orchestration
    deployment_plan = Plan([
      Step("run_tests", parallel=True),
      Step("deploy_canary", spec=canary_spec),
      Step("monitor", duration="10min"),
      Decision("metrics_ok",
        if_true=["gradual_rollout"],
        if_false=["rollback"]),
      Step("cleanup")
    ])
    
    # Level 2: Specifications
    canary_spec = {
      "traffic_percent": 5,
      "instance_type": "t3.large",
      "health_check_interval": "30s"
    }
    
    # Level 1: Actions (reusable)
    def deploy(artifact, spec):
      # Pure execution, no orchestration logic
      ...
    
    Beneficios:
      - Reusable actions
      - Testable specifications
      - Flexible orchestrations
      - Clear intervention points
```

---

### Conexión Patterns KERNEL

```yaml
P52_Crisis_Governance:
  - Opera en Level 3 (orchestration)
  - Daily meetings, decision protocols (planning)
  - Crisis team executes actions (Level 1)
  - Policies guide resource allocation (Level 2)

CI_CD_Pipelines:
  - Pipeline definition (Level 3 orchestration)
  - Environment configs (Level 2 specification)
  - Deploy, test, rollback (Level 1 actions)

Incident_Response:
  - Runbook (Level 3 plan)
  - Severity-based specs (Level 2)
  - Mitigations (Level 1 actions)

Piecemeal_Growth (§11.1):
  - Walking skeleton (Level 1, minimal actions)
  - Iteration planning (Level 3, orchestration)
  - Resource allocation (Level 2, specs grow over time)
```

---

## Referencias Cruzadas

- **Ciclo SDA (Act):** `CORE/02_Ciclo_Fundamental.md` §4
- **Primitivo Flujo:** `CORE/01_Primitivos.md` §2
- **Observable I3 (Eficiencia flujo):** `DOMINIOS/D2_Percepcion.md` §3.3
- **Delegación IA operacional:** `CORE/04_Delegacion.md` (M3, M4, M6)
- **Métricas operación:** `APLICACION/A5_Medicion.md`
- **Patrones DevOps:** `APLICACION/A1_Patrones.md` §4
