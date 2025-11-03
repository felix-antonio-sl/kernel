# D4_Operacion

**Versión:** 3.0.0 | **Estado:** Definitivo | **Audiencia:** Engineering Managers, Tech Leads

## INVARIANTE DOMINIO

**Operación = Aplicación sistemática de Act (A1-A3) sobre inputs D3 (roadmap) → Delivery continuo de valor.**

**Propiedad:** D4 NO decide qué hacer (eso es D3), solo ejecuta CÓMO entregar valor sosteniblemente.

## REFERENCIAS RÁPIDAS

```yaml
Métricas_Flow_4:
  Cycle_Time: §2 - Start→done (target <5d excelente, <10d MVO)
  WIP: §2 - In Progress (target <1.5× team size)
  Throughput: §2 - Items/semana completados
  Flow_Efficiency: §2 - % value-add vs wait (>25% good, >40% world-class)

Métricas_DORA_4:
  Deploy_Frequency: §3 - Elite multiple/día, High daily
  Lead_Time: §3 - Commit→prod (Elite <1hr, High <1d)
  Change_Failure: §3 - % deploys con incident (Elite <5%)
  Time_to_Restore: §3 - Incident→resolved (Elite <1hr)

Principios_Core:
  Teams_as_Assets: §1 - Permanentes (NOT proyectos temporales)
  Two-Pizza_Teams: §1 - 5-9 personas (communication O(n²))
  20%_Rule: §4 - Mínimo 20% capacity → health (tech debt, automation)
  No_Commitment_Culture: §5 - Schedules = forecasts (NO promesas rígidas)

Act_Levels (CORE/02 §4):
  A1_Plan: Orchestration (workflow, dependencies)
  A2_Specify: Configuration (policies, resources)
  A3_Execute: Actions (atomic operations)

Métricas:
  O_Score: §6 - Excelencia operacional (0-100)
  Tech_Debt_Score: §4 - 0-100 lower better (<15 excellent, >50 crisis)
  Típico_MVO: 60-70

Cross-References:
  CORE/02_Ciclo_Fundamental.md §4: Fase Act (A1-A3 formal)
  CORE/01_Primitivos.md §2: Primitivo Flujo
  D2_Percepcion.md §3.3: IN3 Eficiencia Flujo (observable)
  D3_Decision.md §3: Probabilistic forecasts (input D4)
  D1_Arquitectura.md §3: Patrones org (P01 Feature Teams)
```

## Responsabilidad

**OPERACIÓN ejecuta FLUJOS DE VALOR mediante teams estables, delivery continuo y excelencia técnica sostenible.**

**Pregunta clave:** ¿Cómo entregamos valor de forma continua y predecible?

**NO pregunta:** ¿Qué construimos? (eso es D3 Decisión)

## §0. QUICK START: OPERACIÓN MÍNIMA VIABLE (MVO)

**Objetivo**: Delivery continuo funcionando en 6-8 semanas.

### MVO Checklist

```yaml
Week_1-2: Teams Setup
  ☐ Teams 5-9 personas (two-pizza rule)
  ☐ Cross-functional minimum (Eng + Product)
  ☐ Ownership claro (products/services)
  ☐ Manager/Tech Lead identificado

Week_3-4: Flow Basics
  ☐ Methodology: Scrum O Kanban (elige 1)
  ☐ WIP limits: <1.5× team size
  ☐ Cycle time tracking (Jira/Linear)
  ☐ Daily standups (15 min)

Week_5-6: CI/CD Básico
  ☐ Automated tests (>60% coverage MVO target)
  ☐ CI pipeline (lint + test cada commit)
  ☐ Deployment staging automated
  ☐ Deployment prod manual (con checklist)

Week_7-8: Tech Debt Governance
  ☐ 20% rule adopted (1 día/sprint health)
  ☐ Tech debt score baseline
  ☐ Quality gates (tests pass, coverage >60%)

Output_MVO:
  - Teams estables operando
  - Cycle time <10d (functional)
  - Deploy staging automated
  - Tech debt managed
  - O_Score típico: 60-70

Saltar_MVO_Si:
  - Teams estables >6M
  - Cycle time <7d consistent
  - CI/CD operational
  - O_Score >70
  → Ir directo §1-§6 avanzado
```

## §1. TEAMS ESTABLES (ASSET THINKING)

### Principio Manifiesto P4

```yaml
Asset_Thinking:
  - Teams = activos largo plazo (NOT proyectos temporales)
  - Trabajo fluye A TRAVÉS del team
  - Acumulación conocimiento + mejora continua

Project_Thinking (antipatrón):
  - Teams temporales → disolución al terminar
  - Conocimiento perdido cada disolución
  - Ramp-up perpetuo, nunca alto rendimiento

Tamaño_Óptimo: 5-9 personas (Two-Pizza Team)
  <5: Insuficiente diversidad skills
  >9: Coordination overhead O(n²)

Composición_Cross-Functional:
  Eng Backend: 2-3
  Eng Frontend: 1-2
  QA/SDET: 1 (automation)
  PM: 0.5-1 (puede shared)
  Designer: 0.3-0.5 (shared OK)

Ownership_E2E:
  - Ideación → producción → mantenimiento
  - On-call: Team rota propio servicio
  - Metrics: Team responsable OKRs

Estabilidad:
  - Cambios roster <20%/año
  - NO reassignments frecuentes
  - Si crece >9 → Split en 2 (NO diluir)
```

### Deseconomías Escala

```yaml
Ley_Contraintuitiva: Más personas ≠ más rápido en software

Causa_1_Communication:
  Paths = n(n-1)/2
  Team_5: 10 paths
  Team_9: 36 paths (+260%)
  Team_15: 105 paths (+950%)
  
  Efecto: Overhead meetings > beneficio headcount

Causa_2_Colas:
  Especialización → Queues cada fase
  80% tiempo esperando, 20% trabajando
  
  Fix: T-Shaped (depth + breadth)

Ver: D1_Arquitectura.md §3.1 (P01 Feature Teams) para patterns detallados
```

## §2. MÉTRICAS FLOW (4 CORE)

### Cycle Time

```yaml
Definición: Días desde start → done
Target_MVO: <10d (functional)
Target_Excellence: <5d
Tool: Jira, Linear analytics

Cálculo:
  Avg últimas 20-50 stories completadas
  Exclude outliers >3σ (análisis separate)

Vinculación:
  - D2 IN3_Eficiencia_Flujo observable
  - D3 forecasting input (velocity)
```

### WIP (Work In Progress)

```yaml
Definición: Items "In Progress" simultáneos
Target: <1.5× team size
Ejemplo: Team 7 → WIP max 10

Razón:
  Multitasking → context switching → efficiency ↓
  Flow theory: Limit WIP → optimize throughput

Enforcement:
  Kanban: Column WIP limits
  Scrum: Sprint commitment (NO overload)
```

### Throughput

```yaml
Definición: Items/semana completados
Target: Stable or growing (trend > absolute)

Uso:
  - Forecasting (expected throughput próximas N weeks)
  - Capacity planning (cuántos items caben roadmap)
```

### Flow Efficiency

```yaml
Definición: % tiempo value-add vs wait
Fórmula: (Active_Time / Total_Cycle_Time) × 100

Ejemplo:
  Story: 10 días total cycle
  Active work: 3 días coding/testing
  Waiting: 7 días (code review queue, deploy queue)
  Flow Efficiency = 3/10 = 30%

Target:
  >25%: Good (típico org)
  >40%: World-class (elite performers)
  <15%: Crítico (proceso broken)

Fix_Low_Efficiency:
  - Reduce handoffs (PE5, D1 §1.5)
  - Automate queues (CI/CD, auto-deploy)
  - Cross-functional teams (reduce waits)
```

## §3. MÉTRICAS DORA (4 ELITE)

### Deploy Frequency

```yaml
Qué_Mide: Frecuencia deploys to production
Elite: Multiple/día
High: Daily
Medium: Weekly
Low: <Monthly

Vinculación: D2 O_Score componente (30%)
```

### Lead Time for Changes

```yaml
Qué_Mide: Commit → production
Elite: <1 hora
High: <1 día
Medium: 1 semana
Low: >1 mes

Requiere: CI/CD automated full
```

### Change Failure Rate

```yaml
Qué_Mide: % deploys con incident
Elite: <5%
High: 5-15%
Medium: 15-30%
Low: >30%

Mitigación:
  - Automated testing (>80% coverage)
  - Canary deploys (gradual rollout)
  - Feature flags (P23)
```

### Time to Restore

```yaml
Qué_Mide: Incident → resolved
Elite: <1 hora
High: <1 día
Medium: <1 semana
Low: >1 semana

Requiere:
  - On-call rotation (§7)
  - Runbooks automated
  - Rollback instant (blue-green)
```

## §4. TECH DEBT GOVERNANCE

### 20% Rule

```yaml
Principio: Mínimo 20% capacity → health work
Health_Work:
  - Tech debt paydown
  - Automation improvements
  - Refactoring
  - Tool upgrades
  - Learning

Enforcement:
  - 1 día/sprint (team 5d sprint)
  - NOT negotiable (protegido C-level)

Anti-Pattern_Skip_Health:
  "Este sprint emergencia, 0% health"
  → Debt acumula → velocity ↓ → más "emergencias"
  → Death spiral
```

### Tech Debt Score

```yaml
Cálculo_Componentes:
  - Test coverage (weight 30%)
  - Code duplication (20%)
  - Complexity (cyclomatic) (20%)
  - Documentation gaps (15%)
  - Security vulnerabilities (15%)

Score_0-100 (lower better):
  <15: Excelente (minimal debt)
  15-30: Good (manageable)
  30-50: Atención (dedicate 30% capacity)
  >50: Crisis (dedicate 50% capacity hasta <30)

Tools: SonarQube, CodeClimate, custom scripts
```

## §5. NO COMMITMENT CULTURE

### Schedules as Forecasts

```yaml
Principio_Manifiesto_P6: Estimación ≠ Compromiso

❌ Malo: "Prometo entregar 15-Mayo"
✅ Bueno: "80% probabilidad 10-20 Mayo"

Consecuencias_Commitments:
  - Teams sandbag (estimates conservadores)
  - NO transparency issues
  - Pressure unhealthy (burnout)
  - Gaming metrics

Fix:
  - Communicate ranges (D3 §3 probabilistic)
  - NO penalizar forecasts incorrectos
  - Track accuracy, learn, improve

Carry-Over_Work_OK:
  - Sprint ≠ deadline rígido
  - Items carry over next sprint (flow continuo)
  - Focus: Throughput promedio, NO "100% sprint commitment"
```

## §6. O_SCORE (0-100)

### Fórmula Operacional

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
    <3d: 95-100
    3-7d: 75-90
    7-14d: 50-70
    >14d: 0-45
  
  WIP_Compliance_Score (0-100):
    WIP <1.5× team: 90-100
    WIP 1.5-2.0×: 70-85
    WIP >2.0×: 0-65
  
  Deploy_Frequency_Score (0-100):
    DORA Elite (multiple/día): 95-100
    DORA High (daily): 75-90
    DORA Medium (weekly): 50-70
    DORA Low (<monthly): 0-45
  
  Completion_Rate_Score (0-100):
    >80% stories started completadas: 90-100
    70-80%: 75-85
    <70%: 0-70

Interpretación:
  >75: Operación excelente (flow rápido, predecible)
  60-75: Operación funcional (gaps menores)
  <60: Operación débil (blockers sistémicos)

Típico_MVO: 60-70
Típico_excelencia: 80-90

Vinculación_D2:
  O_Score alimenta IN3_Eficiencia_Flujo (D2 §3.3)
```

## §7. ON-CALL & INCIDENT RESPONSE

### Rotation

```yaml
Team_Size_Mínimo: 4+ personas (para rotación sostenible)
Shift_Duration: 1 semana (Monday-Monday)
Responsibilities:
  - Monitor alerts 24/7
  - Respond incidents SEV1/SEV2
  - Execute runbooks
  - Escalate if needed

Runbooks_Required:
  - Database connection issues
  - Service outage
  - High latency
  - Security incident
  
  Format: IF symptom X THEN action Y (M6 executable)

Compensation:
  - On-call pay differential OR comp time
  - NOT "part of job" sin recognition
```

## §8. CEREMONIES (3 ESSENTIAL)

### Daily Standup (15 min)

```yaml
Format: Yesterday, Today, Blockers
NO: Problem-solving (use parking lot)
Skip: Status report to manager (anti-pattern)
```

### Planning (1-2 hrs/week)

```yaml
Actividad: Prioritize top items, commitment sprint
NO: Estimation poker (use historical cycle time)
```

### Retrospectiva (1 hr bi-weekly)

```yaml
Actividad: What worked, what didn't, max 3 action items
NO: Blame game (psychological safety crítica)
```

## §9. CONTINUOUS LEARNING (PIECEMEAL GROWTH)

### Walking Skeleton (P55)

```yaml
Concepto: Sistema E2E mínimo funcional
Ejemplo_Web_App:
  - 1 página HTML
  - 1 API endpoint
  - 1 DB table
  - Deploy pipeline
  → Funciona E2E, luego expand

Rationale:
  - Validate integration points early
  - Infrastructure desde día 1
  - Iteración sobre base working

Ver: D1 §1 para MVA, D2 §0 para MVO, D3 §0 para MVD pattern similar
```

## §10. ACT LEVELS (CORE/02 §4)

### A1: PLAN (Orchestration)

```yaml
Definición: Workflow, dependencies, conditional logic

Ejemplos:
  - Deployment plan (canary → gradual rollout → validate)
  - Incident response (detect → contain → remediate)
  - Crisis stabilization (P52 protocols)

Complejidad: Alta (strategic planning)
Delegación: M2-M4 (humano plans, IA assists OR orchestrator)
```

### A2: SPECIFY (Configuration)

```yaml
Definición: Policies, resources, parameters

Ejemplos:
  - CI/CD specs (instance type, timeout, replicas)
  - Quality gates (coverage >60%, tests pass)
  - Resource limits (CPU, memory, budget)

Complejidad: Media (policy-driven)
Delegación: M4-M5 (configured by human, executed by system)
```

### A3: EXECUTE (Actions)

```yaml
Definición: Atomic operations (deploy, test, notify, log)

Ejemplos:
  - Deploy artifact
  - Send notification
  - Update database
  - Scale instances

Complejidad: Baja (bounded operations)
Delegación: M5-M6 (automated con oversight o full autonomy)

Separación_Concerns:
  ✅ Actions reusables (NO mix orchestration)
  ✅ Testable aislado
  ✅ Composable en diferentes workflows
```

### Progresión A1→A2→A3

```yaml
Delegation_Mapping:
  A1_Plan → M2-M4:
    IF plan standard (runbook): M4 (orchestrator executes)
    ELSE IF plan novel: M2-M3 (human plans, IA assists)
  
  A2_Specify → M4-M5:
    Policies configured by human
    System executes con policies
  
  A3_Execute → M5-M6:
    IF bounded AND reversible: M6 (full autonomy)
    ELSE IF significant: M5 (human oversight)
```

## §11. ANTI-PATRONES OPERACIONALES

```yaml
AP_D4_1_Project_Thinking:
  Síntoma: Teams temporales, disolución perpetua
  Fix: Teams permanentes (§1 Asset Thinking)

AP_D4_2_Tech_Debt_Ignored:
  Síntoma: 0% capacity health, velocity decay
  Fix: 20% rule protected (§4)

AP_D4_3_Commitment_Culture:
  Síntoma: "Prometemos X fecha", sandbagging
  Fix: Schedules = forecasts (§5)

AP_D4_4_Manual_Toil:
  Síntoma: Manual deploys, manual testing
  Fix: CI/CD automated (§3, M6 delegation)

AP_D4_5_Hero_Culture:
  Síntoma: 1 persona "saves the day" repeatedly
  Fix: Runbooks, rotation, NO single points (§7)

Ver: APLICACION/A2_Antipatrones.md §4 para 20+ operacionales
```

## §12. VALIDACIÓN DOMINIO

**Validación Formal:** Ver `CORE/07_Validacion.md` para pruebas completas de Invariantes I1-I3, Completitud y Consistencia.

**Checklist Rápido D4 (5 min):**

```yaml
✓ Ortogonalidad: D4 ∩ {D1, D2, D3} = ∅
  - D4 ejecuta/opera, D1 organiza, D2 mide, D3 decide
  - Sin solapamiento: D4 consume roadmap D3, produce métricas para D2

✓ Trazabilidad: Flujo causal verificable
  - D3 roadmap → D4 execution → D2 metrics (O_Score, IN3) → D3 adjust (loop)
  - Métricas alimentan ciclo de feedback continuo

✓ Completitud: Métricas suficientes
  - Flow: Lead Time, Cycle Time, Throughput, WIP
  - DORA: Deployment Freq, Lead Time Changes, MTTR, Change Fail Rate
  - Calidad: Tech Debt %, Bug Escape Rate

✓ Parsimonia: Elementos mínimos
  - Todas las métricas necesarias para predictibilidad y control
  - Cycle Time: Predictibilidad
  - WIP: Control de flujo
  - Deploy Freq: Velocidad de entrega
  - MTTR: Confiabilidad del sistema

✓ Alineamiento CORE:
  - A4 (Ciclo SDA) → A1-A3 es el Act del ciclo
  - P4 (Flujo Continuo) → Flow Metrics, WIP limits
  - P7 (Parsimonia) → Solo métricas accionables
  - Primitivo Flujo → Lead Time, Cycle Time, Throughput
```

**Para revisión formal:** Aplicar pruebas de `CORE/07_Validacion.md` §2 (Ortogonalidad), §3 (Trazabilidad)

## Referencias Cruzadas

- **Ciclo SDA Act:** `CORE/02_Ciclo_Fundamental.md` §4 (A1-A3 formal)
- **Manifiesto P4:** `CORE/00_Manifiesto.md` §3.4 (Flujo Continuo)
- **Primitivo Flujo:** `CORE/01_Primitivos.md` §2
- **IN3 Eficiencia:** `D2_Percepcion.md` §3.3 (observable flow)
- **Probabilistic:** `D3_Decision.md` §3 (forecasts input)
- **PE7 Type 1/2:** `D1_Arquitectura.md` §1.7 (decisiones reversibles)
- **P01 Feature Teams:** `D1_Arquitectura.md` §3.1 (teams estables)
- **Delegación:** `CORE/04_Delegacion.md` (M2-M6)
- **Smartness D4:** `CORE/05_Smartness.md` matriz D4 row
- **Crisis P52:** `CORE/08_Crisis_Management.md` (orchestration example)
- **Implementación:** `APLICACION/A4_Implementacion.md`

**Fin D4_Operacion v3.0.0**
