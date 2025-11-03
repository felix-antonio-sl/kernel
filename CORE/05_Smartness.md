# 05_Smartness

**Versión:** 1.0.0 | **Estado:** Definitivo | **Audiencia:** Arquitectos, Estrategas, AI/ML Leads

---

## §1. EL MODELO DE INTELIGENCIA ORGANIZACIONAL (SMARTNESS)

### Definición

La "Smartness" o Inteligencia Organizacional es la capacidad de un sistema para **percibir** su entorno y su estado interno, **decidir** cursos de acción efectivos y **actuar** para alcanzar sus objetivos de forma adaptativa y eficiente. No es un estado binario, sino un espectro de madurez.

### El Framework 4x6

El modelo de Smartness de KERNEL se estructura como una matriz de 4x6, donde las 4 filas son los dominios operacionales y las 6 columnas son niveles de capacidad progresiva. Esto genera un total de 24 "células" de capacidad medibles.

- **4 Dominios (Filas):**
  - **D1. Arquitectura:** La capacidad de diseñar y evolucionar la estructura del sistema.
  - **D2. Percepción:** La capacidad de observar y entender el estado y el entorno.
  - **D3. Decisión:** La capacidad de planificar y priorizar acciones.
  - **D4. Operación:** La capacidad de ejecutar acciones y entregar valor.

- **6 Niveles de Capacidad (Columnas):**
  - **C1. Manual:** Procesos ad-hoc, dependientes de héroes.
  - **C2. Documentado:** Procesos definidos y repetibles.
  - **C3. Medido:** Se capturan KPIs básicos sobre los procesos.
  - **C4. Automatizado:** Tareas repetitivas son ejecutadas por scripts o software.
  - **C5. Proactivo:** El sistema anticipa problemas y actúa para prevenirlos.
  - **C6. Adaptativo:** El sistema se auto-optimiza en respuesta a cambios.

**Nota sobre C7 eliminado**: Versiones anteriores incluían "C7. Soberano: Sistema define objetivos emergentes propios". Este nivel se eliminó por **contradicción con Principio P8** (Herramienta no Oráculo - humano siempre en control meta-nivel). Un sistema que define objetivos sin supervisión humana viola el axioma fundamental de delegación explícita (A3). C6 Adaptativo es el **máximo nivel alcanzable** bajo gobernanza humana responsable.

---

## §2. LA MATRIZ DE CAPACIDADES DE SMARTNESS (4x6)

| | C1: Manual | C2: Documentado | C3: Medido | C4: Automatizado | C5: Proactivo | C6: Adaptativo |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **D1. Arquitectura** | Diseño en pizarra | Diagramas estáticos | Métricas de acoplamiento | Generación de código (scaffolding) | Detección de deriva arquitectónica | Refactorización autónoma supervisada |
| **D2. Percepción** | Reporte verbal | Dashboards estáticos | Alertas basadas en umbrales | Recolección de logs y métricas | Detección de anomalías | Análisis de causa raíz automático |
| **D3. Decisión** | Intuición del líder | Roadmaps en PPT | Progreso de OKRs | Priorización de backlog (RICE) | Simulación de escenarios (what-if) | Optimización dinámica portfolio (con oversight humano) |
| **D4. Operación** | Deploys manuales | Runbooks y checklists | Métricas DORA (lead time, etc.) | CI/CD, IaC | Self-healing (ej. reinicio de pods) | Auto-escalado + auto-remediation (bounded autonomy) |

**Límite C6**: Todas las capacidades C6 operan bajo **delegación M5-M6 con bounded autonomy**. El sistema puede auto-optimizarse dentro de límites y políticas definidas por humanos, pero no puede redefinir sus propios objetivos estratégicos (eso requeriría C7, eliminado por violar P8).

---

## §3. DESARROLLO CAPACIDADES POR NIVEL

### C1: Manual (Ad-hoc, Hero-Dependent)

**Características**:

- Procesos no documentados, residen en cabezas de personas
- Variabilidad alta (cada quien hace diferente)
- Escalabilidad nula (pierde persona clave → colapsa proceso)
- Delegación: 100% humano (M1 monitoring si acaso)

**Por Dominio**:

```yaml
D1_Arquitectura_C1:
  Descripción: Diseño org en pizarra, decisiones ad-hoc CEO
  Ejemplo: CEO decide estructura en reunión, no documentado
  Problema: Cambio persona → org se desestabiliza
  
D2_Percepción_C1:
  Descripción: Reportes verbales, "feeling" sin datos
  Ejemplo: Manager reporta "team está bien" sin métricas
  Problema: Blind spots, decisiones sin evidencia
  
D3_Decisión_C1:
  Descripción: Intuición líder sin framework
  Ejemplo: CEO decide roadmap based on "gut feeling"
  Problema: Inconsistente, no explicable, high-risk
  
D4_Operación_C1:
  Descripción: Deploys manuales, scripts personales
  Ejemplo: DevOps engineer SSH a servidor, run commands manualmente
  Problema: Errores frecuentes, MTTR alto, no escala
```

---

### C2: Documentado (Definido, Repetible)

**Características**:

- Procesos escritos (wikis, runbooks, checklists)
- Repetibilidad media (sigue docs, pero manual execution)
- Escalabilidad baja (requiere training cada persona nueva)
- Delegación: Humano execution, docs son M1 reference

**Por Dominio**:

```yaml
D1_Arquitectura_C2:
  Descripción: Diagramas estáticos (Lucidchart, Miro)
  Ejemplo: Org chart documentado, RACI matrices en Confluence
  Problema: Docs desactualizados (no enforzados)
  Mejora_vs_C1: Visibility, onboarding más rápido
  
D2_Percepción_C2:
  Descripción: Dashboards estáticos, Excel reports
  Ejemplo: Weekly report con métricas manuales copy-paste
  Problema: Latency alta (report semanal), manual effort
  Mejora_vs_C1: Métricas visibles, trends posibles
  
D3_Decisión_C2:
  Descripción: Roadmaps en PPT, planning templates
  Ejemplo: Roadmap trimestral en slides, reviewed mensual
  Problema: Estático, no linked a execution real-time
  Mejora_vs_C1: Plan compartido, alignment visible
  
D4_Operación_C2:
  Descripción: Runbooks escritos, deployment checklists
  Ejemplo: Deploy checklist 20 pasos, engineer sigue manual
  Problema: Slow (30+ min deploy), error-prone
  Mejora_vs_C1: Consistencia, reducción errores 50%
```

---

### C3: Medido (KPIs Básicos Capturados)

**Características**:

- Métricas key tracked sistemáticamente
- Dashboards automated básicos
- Decisiones parcialmente data-driven
- Delegación: M1 monitoring automated, M2 emerging

**Por Dominio**:

```yaml
D1_Arquitectura_C3:
  Descripción: Métricas acoplamiento, span-of-control
  Ejemplo: A_Score calculado trimestral (ver A5 §2)
  KPIs: Team stability, handoff ratio, decision clarity
  Mejora_vs_C2: Objectivity, trends cuantificados
  
D2_Percepción_C3:
  Descripción: Alertas threshold-based (CPU >80%)
  Ejemplo: PagerDuty alerts cuando SLA breach
  KPIs: 11 observables tracked (O1-O8, I1-I3)
  Mejora_vs_C2: Real-time awareness, reactive alerts
  
D3_Decisión_C3:
  Descripción: Progreso OKRs tracked en dashboards
  Ejemplo: OKR dashboard muestra % completion KRs
  KPIs: OKR achievement, decision velocity
  Mejora_vs_C2: Transparency, accountability visible
  
D4_Operación_C3:
  Descripción: Métricas DORA capturadas (lead time, deploy freq)
  Ejemplo: Jira analytics cycle time, throughput
  KPIs: Cycle time, deploy frequency, WIP
  Mejora_vs_C2: Performance visible, bottlenecks identificables
```

---

### C4: Automatizado (Tareas Repetitivas Scripteadas)

**Características**:

- Automation tasks rutinarias (CI/CD, data pipelines)
- Humano configura, sistema ejecuta
- Escalabilidad media (requiere infra management)
- Delegación: M3-M4 (enable/control), automation bounded

**Por Dominio**:

```yaml
D1_Arquitectura_C4:
  Descripción: Code generation (scaffolding, boilerplate)
  Ejemplo: Cookiecutter templates, Yeoman generators
  Beneficio: New service en 10 min vs 2 hrs manual
  Delegación: M3 Enable (developer invokes, tool generates)
  
D2_Percepción_C4:
  Descripción: Log collection automated (ELK, Splunk)
  Ejemplo: Fluentd/Filebeat ship logs → Elasticsearch
  Beneficio: Centralized, searchable, retention automated
  Delegación: M6 Execute (data pipelines autonomous)
  
D3_Decisión_C4:
  Descripción: Backlog auto-prioritization (RICE, WSJF)
  Ejemplo: Script scores backlog items, ranks por priority
  Beneficio: Objectivity, save PM 2hrs/week
  Delegación: M4 Control (human validates top 10)
  
D4_Operación_C4:
  Descripción: CI/CD pipelines, IaC (Terraform)
  Ejemplo: GitHub Actions: test → build → deploy staging
  Beneficio: Deploy frequency 10×, lead time <1hr
  Delegación: M5-M6 (co-produce staging, human approve prod)
```

---

### C5: Proactivo (Anticipación, Prevención)

**Características**:

- Sistema predice problemas antes de ocurrir
- Forecasting, anomaly detection
- Acciones preventivas automated
- Delegación: M4-M5 (control/co-produce), ML models

**Por Dominio**:

```yaml
D1_Arquitectura_C5:
  Descripción: Drift detection arquitectónico
  Ejemplo: ML detecta coupling creciendo entre services
  Acción: Alerta architects "Services X-Y coupling 0.7→0.85"
  Beneficio: Prevenir monolito distribuido antes de solidificar
  Delegación: M2 Inform (alert, human decides refactor)
  
D2_Percepción_C5:
  Descripción: Anomaly detection (spikes, dips inusuales)
  Ejemplo: ML detecta traffic pattern anomalía 30 min antes crash
  Acción: Alert on-call "Traffic spike predicted, suggest pre-scale"
  Beneficio: Prevenir incidents (proactive vs reactive)
  Delegación: M2-M3 Inform/Enable (suggest, human validates)
  
D3_Decisión_C5:
  Descripción: Scenario simulation (Monte Carlo, what-if)
  Ejemplo: "If we prioritize Feature A, 70% prob $1M in 6 months"
  Acción: Portfolio optimizer sugiere prioritization
  Beneficio: Risk-informed decisions, less surprises
  Delegación: M3 Enable (human requests simulation)
  
D4_Operación_C5:
  Descripción: Self-healing (auto-restart failing pods)
  Ejemplo: Kubernetes liveness probe failed → restart pod
  Acción: Service auto-recovers sin human intervention
  Beneficio: MTTR <1 min (vs 15 min manual)
  Delegación: M6 Execute (bounded: restart only, escalate if persist)
```

---

### C6: Adaptativo (Auto-Optimización Bounded)

**Características**:

- Sistema ajusta strategy/parameters dinámicamente
- Closed-loop optimization dentro de bounds
- Humano define objetivos y límites, sistema optimiza cómo
- Delegación: M5-M6 (co-produce/execute), máxima autonomía bajo P8

**Por Dominio**:

```yaml
D1_Arquitectura_C6:
  Descripción: Refactoring autónomo supervisado
  Ejemplo: Bot detecta code smell, genera PR refactor, tests pass → merge
  Límites: Solo refactorings que preserve behavior (tests green)
          Cambios arquitectónicos mayores requieren human ADR
  Beneficio: Tech debt reducción continua sin human bottleneck
  Delegación: M5 Co-produce (bot refactors, human reviews weekly)
  
D2_Percepción_C6:
  Descripción: Root cause analysis automático
  Ejemplo: Incident → system correlates logs/metrics → suggests RCA
  Límites: Sugiere causas, human valida y documenta postmortem
  Beneficio: RCA 80% automated, human adds context
  Delegación: M4 Control (system analyzes, human validates)
  
D3_Decisión_C6:
  Descripción: Portfolio optimization dinámica
  Ejemplo: System re-prioriza backlog basado en CoD + velocity changes
  Límites: Optimiza dentro OKRs fijos (human-defined)
          Strategic pivots require human decision
  Beneficio: Backlog siempre optimal, PM focuses strategy
  Delegación: M5 Co-produce (system suggests, human adjusts weights)
  
D4_Operación_C6:
  Descripción: Auto-scaling + auto-remediation multi-dimensional
  Ejemplo: System ajusta deployment strategy real-time:
    - Detecta latency spike región APAC
    - Reduce canary rollout 10%→5% esa región
    - Extiende monitoring 10min→20min
    - Notifica SRE (no bloquea)
    - Si metrics OK, continues rollout adapted
  Límites: Bounded autonomy policies (max rollout %, error thresholds)
          Human can pause/override anytime
  Beneficio: Deployment safety + velocity optimal
  Delegación: M6 Execute (within bounds) + M4 Control (escalate exceptions)
```

**Límite Universal C6**: Todas capacidades C6 requieren:

- Objetivos definidos por humanos (OKRs, policies)
- Bounded autonomy explícita (limits, thresholds)
- Human oversight (monitoring, circuit breakers)
- Escalation protocols (exception handling)
- Auditability (decision logs, explainability)

---

## §4. CÓMO MEDIR Y MEJORAR LA SMARTNESS

1. **Assessment Inicial:** Evalúa cada una de las 24 capacidades de la matriz en una escala de 1 a 6, usando la columna correspondiente como guía. Esto te dará un "heatmap" de la madurez de inteligencia de tu organización.
2. **Identificar Cuellos de Botella:** Las columnas con las puntuaciones más bajas son tus principales inhibidores de agilidad. Una organización no puede ser C6 (Adaptativa) en Operaciones si su Arquitectura es C1 (Manual).
3. **Definir un Roadmap de Madurez:** No intentes saltar de C1 a C6. Define un plan realista para mover las capacidades críticas una columna a la derecha cada 6-12 meses. La progresión típica es: C1→C2 (6 meses), C2→C3 (6 meses), C3→C4 (12 meses), C4→C5 (12 meses), C5→C6 (18+ meses).
4. **Invertir en Plataforma:** Las capacidades de C4 en adelante requieren una plataforma de datos y automatización robusta. La inversión en DevOps, MLOps y plataformas de datos es un pre-requisito. C6 adicionalmente requiere IA/ML avanzado con governance sólida (bounded autonomy, human oversight, circuit breakers).
5. **Límite de Autonomía:** C6 es el máximo nivel bajo Principio P8. Sistemas C6 se auto-optimizan pero dentro de objetivos y límites definidos por humanos. No evolucionan a "autonomía total" sin supervisión.

---

## §5. PATHS DE MADUREZ POR DOMINIO

### D1 Arquitectura: C1 → C6

```yaml
Progresión_Típica:
  
  C1→C2 (6 meses):
    - Documentar org chart actual en tool (Lucidchart, Miro)
    - Escribir RACI matrices procesos críticos
    - Publish team charters (ownership, responsibilities)
    Quick_Win: Clarity roles, onboarding 50% más rápido
  
  C2→C3 (6 meses):
    - Calcular A_Score trimestral (A5 §2 KPIs arquitectura)
    - Track team stability, handoff ratio, span-of-control
    - Alerts: Si A_Score <70 → Diagnóstico estructural
    Quick_Win: Objectivity decisiones reorg, data-driven
  
  C3→C4 (12 meses):
    - Code generation templates (service scaffolding)
    - Org chart automated sync (HR system → diagram tool)
    - RACI enforcement automated (approval workflows)
    Quick_Win: New services 10× más rápido, consistency
  
  C4→C5 (12 meses):
    - Architectural drift detection (coupling metrics)
    - Dependency analysis automated (service maps)
    - Alerts proactive: "Coupling trend suggests split Service X"
    Quick_Win: Prevenir monolito distribuido, refactor proactive
  
  C5→C6 (18+ meses):
    - Refactoring bots (automated PR generation)
    - Self-organizing teams (rebalance load automated suggestions)
    - Bounded autonomy: Human approves architectural decisions
    Quick_Win: Tech debt auto-remediation, architecture self-healing

Prerequisitos_Cada_Nivel:
  C4: CI/CD platform, code repositories structured
  C5: ML/analytics platform, metric collection comprehensive
  C6: Advanced ML, explainability (XAI), governance robust
```

---

### D2 Percepción: C1 → C6

```yaml
Progresión_Típica:
  
  C1→C2 (3 meses):
    - Setup dashboards básicos (Datadog, Grafana)
    - Document 11 observables tracking plan
    - Weekly manual report → dashboard
    Quick_Win: Real-time visibility, elimina report manual
  
  C2→C3 (6 meses):
    - Calcular H_Score mensual automated
    - Alerts threshold (O2<60, I2<60, etc.)
    - Data pipelines para 11 observables
    Quick_Win: H_Score tracking continuo, alertas proactivas
  
  C3→C4 (6 meses):
    - Log aggregation comprehensive (ELK stack)
    - Metrics collection automated (Prometheus, StatsD)
    - Distributed tracing (Jaeger, Zipkin)
    Quick_Win: Observability 360°, MTTD (mean time to detect) <5min
  
  C4→C5 (12 meses):
    - Anomaly detection ML (Prophet, Isolation Forest)
    - Predictive alerts (forecast CPU 90% en 30 min)
    - Churn prediction model (O2 proactive)
    Quick_Win: Prevent incidents, proactive vs reactive
  
  C5→C6 (18+ meses):
    - Auto-RCA (root cause analysis correlating signals)
    - Self-diagnosis systems (suggest fixes)
    - Continuous learning (models adapt to org changes)
    Quick_Win: RCA 80% automated, learning organizational

Prerequisitos_Cada_Nivel:
  C4: Data warehouse (Snowflake, BigQuery), ETL pipelines
  C5: ML platform (feature store, model registry), data scientists
  C6: MLOps mature (A/B testing models, drift detection), governance
```

---

### D3 Decisión: C1 → C6

```yaml
Progresión_Típica:
  
  C1→C2 (6 meses):
    - Documentar OKRs en template standard
    - Roadmap en tool compartido (Productboard, Aha!)
    - Planning process definido (quarterly OKRs, monthly review)
    Quick_Win: Alignment visible, strategy communicable
  
  C2→C3 (6 meses):
    - OKR progress tracking automated (integración Jira)
    - Decision velocity measured (D5 en A5 §2)
    - Portfolio dashboard (initiatives, status, ROI)
    Quick_Win: Transparency, accountability enforcement
  
  C3→C4 (12 meses):
    - Auto-prioritization backlog (RICE, WSJF scoring)
    - Workflow approval automated (>$10K require VP)
    - Roadmap sync automated (OKRs → Jira epics)
    Quick_Win: PM time saved 30%, objectivity increased
  
  C4→C5 (12 meses):
    - Monte Carlo simulations roadmap (probabilistic forecasts)
    - What-if scenario tools (portfolio optimizer)
    - Churn prediction informing prioritization
    Quick_Win: Risk-informed decisions, surprises -50%
  
  C5→C6 (18+ meses):
    - Dynamic portfolio rebalancing (CoD + velocity changes)
    - Auto-adjust OKRs tactics (strategy fixed, how optimized)
    - Bounded: Human defines OKRs, system optimizes execution
    Quick_Win: Portfolio siempre optimal, strategic agility

Prerequisitos_Cada_Nivel:
  C4: Project management tool (Jira, Linear), workflow automation
  C5: Analytics platform, forecasting models, simulation tools
  C6: Advanced optimization (linear programming, reinforcement learning)
```

---

### D4 Operación: C1 → C6

```yaml
Progresión_Típica:
  
  C1→C2 (3 meses):
    - Runbooks written (deployment, incident response)
    - Checklists para procesos críticos
    - Document flow (value stream mapping)
    Quick_Win: Consistency, onboarding 2× más rápido
  
  C2→C3 (6 meses):
    - DORA metrics tracked (deploy freq, lead time, MTTR)
    - Flow metrics tracked (cycle time, throughput)
    - Dashboards teams real-time
    Quick_Win: Performance visibility, bottleneck identification
  
  C3→C4 (6 meses):
    - CI/CD pipeline (GitHub Actions, CircleCI)
    - IaC (Terraform, CloudFormation)
    - Automated testing (unit, integration, E2E)
    Quick_Win: Deploy frequency 10×, lead time <1hr
  
  C4→C5 (12 meses):
    - Self-healing (Kubernetes auto-restart pods)
    - Auto-scaling (CPU/memory threshold → instances)
    - Predictive scaling (forecast load, pre-scale)
    Quick_Win: Uptime 99.9%+, MTTR <5min
  
  C5→C6 (18+ meses):
    - Adaptive deployment strategies (adjust rollout real-time)
    - Multi-dimensional auto-scaling (cost + performance optimized)
    - Self-remediation (auto-rollback, auto-patch, auto-rebalance)
    Bounded: Policies strict (error thresholds, cost limits)
    Quick_Win: Deployment velocity + safety maximized simultaneously

Prerequisitos_Cada_Nivel:
  C4: Cloud infrastructure, containerization (Docker, K8s)
  C5: Observability platform (Datadog, New Relic), ML basic
  C6: MLOps platform, chaos engineering, advanced ML (RL)
```

---

## §6. INTEGRACIÓN CON KERNEL

### Conexión Modos Delegación (M1-M6)

```yaml
Mapping_Smartness_to_Delegation:
  
  C1_Manual → M1 Monitor:
    - Sistema solo observa, humano hace todo
    - Ejemplo: Dashboard muestra metrics, PM analiza
  
  C2_Documentado → M1 Monitor + Docs:
    - Docs como reference, execution manual
    - Ejemplo: Runbook, engineer sigue pasos
  
  C3_Medido → M1-M2:
    - Monitoring automated, alerts basic
    - Ejemplo: Threshold alerts (CPU >80%)
  
  C4_Automatizado → M3-M4:
    - Automation tasks bounded, human configures
    - Ejemplo: CI/CD pipeline, quality gates
  
  C5_Proactivo → M2-M4:
    - Prediction + automated response bounded
    - Ejemplo: Anomaly detection + alert, auto-restart pod
  
  C6_Adaptativo → M5-M6:
    - Self-optimization dentro policies
    - Ejemplo: Dynamic portfolio rebalancing, adaptive deployment
    - Requiere bounded autonomy estricta (P8 compliance)

Principio_Delegación:
  Mayor Smartness level → Mayor delegation mode permitido
  PERO: Siempre bounded por P8 (human meta-level control)
  
  C6 permite M6, PERO:
    - Human define objetivos (OKRs)
    - Human define bounds (policies, thresholds)
    - Human puede override siempre
    - System optimiza CÓMO, not WHAT ni WHY
```

---

### Conexión Observables (D2)

```yaml
Smartness_Habilita_Observables:
  
  O8_Calidad_Información:
    - C1-C2: Data quality manual, inconsistente
    - C3-C4: Data quality measured, pipelines automated
    - C5-C6: Data quality self-healing (auto-fix, auto-validate)
  
  I1_Velocidad_Decisional:
    - C1-C2: Decisiones lentas (manual analysis)
    - C3-C4: Decisiones data-informed (dashboards, scoring)
    - C5-C6: Decisiones automated (M4-M6 modes)
  
  I3_Eficiencia_Flujo:
    - C1-C2: Flow manual, bottlenecks invisibles
    - C3-C4: Flow measured, bottlenecks identificables
    - C5-C6: Flow self-optimizing (auto-rebalance, auto-remove blockers)

Feedback_Loop:
  Higher Smartness → Better observables → Better decisions
  Better decisions → Investment in automation → Higher Smartness
  → Virtuous cycle (requires initial investment trigger)
```

---

### Métricas Smartness (A5 Integration)

```yaml
Smartness_Score_Overall (0-100):
  
  Por_Dominio:
    S_D1_Arquitectura = Avg(C_level across 24 capabilities D1 row)
    S_D2_Percepción = Avg(C_level across 24 capabilities D2 row)
    S_D3_Decisión = Avg(C_level across 24 capabilities D3 row)
    S_D4_Operación = Avg(C_level across 24 capabilities D4 row)
  
  Agregado:
    Smartness_Score = (S_D1 + S_D2 + S_D3 + S_D4) / 4
  
  Normalización (C1-C6 → 0-100):
    C1 = 0, C2 = 20, C3 = 40, C4 = 60, C5 = 80, C6 = 100
    
    Ejemplo:
      Org con D1=C3, D2=C4, D3=C3, D4=C5
      → S_D1=40, S_D2=60, S_D3=40, S_D4=80
      → Smartness_Score = (40+60+40+80)/4 = 55/100

Benchmarks:
  >70: Elite (C4-C5 avg, alta automation + proactividad)
  50-70: Mature (C3-C4 avg, medición + automation básica)
  30-50: Developing (C2-C3 avg, documentación + medición emergente)
  <30: Nascent (C1-C2 avg, ad-hoc + documentación básica)

Tracking_Frequency:
  - Assessment full: Anual (24 celdas evaluar)
  - Score calculation: Trimestral (track progress)
  - Dashboard: Heatmap 4×6 visible a C-level

Integration_A3_Diagnostico:
  - Agregar Smartness assessment a diagnóstico (after H_Score)
  - Identifica dominios low maturity (opportunities automation)
  
Integration_A4_Implementacion:
  - Maturity roadmap: "Move D4 from C3 to C4 in 6 months"
  - Initiatives priorizadas por Smartness gaps

Integration_A5_Medicion:
  - Dashboard Smartness heatmap (color: Red C1-C2, Yellow C3-C4, Green C5-C6)
  - KPI: "Smartness Score" alongside H_Score
```

---

## §7. ANTI-PATRONES SMARTNESS

### AP_S1: Skipping Levels

```yaml
Síntoma: Intentar saltar C1 → C5 sin pasar por C2-C4
Causa: Impatience, FOMO ("everyone does ML, we must too")
Consecuencia: Fracaso implementation, investment wasted
Ejemplo:
  - Org C1 (manual) quiere C5 (ML predictive)
  - Falta C2 (docs), C3 (metrics), C4 (pipelines)
  - ML model sin data quality → garbage in, garbage out

Fix: Respect progression, build foundation first
  - C1→C2: Document (3-6 meses)
  - C2→C3: Measure (6 meses)
  - C3→C4: Automate (6-12 meses)
  - C4→C5: Predict (12+ meses)
```

---

### AP_S2: Unbalanced Maturity

```yaml
Síntoma: 1 dominio C5-C6, otros dominios C1-C2
Causa: Over-investment un área, neglect others
Consecuencia: Bottleneck en dominios low maturity
Ejemplo:
  - D4_Operación C5 (CI/CD elite, deploy 20×/día)
  - D3_Decisión C1 (CEO intuition, no OKRs)
  - Result: Deliver features rápido, pero wrong features

Fix: Balance investment across dominios
  - Target: Max gap 2 levels entre dominios
  - Si D4=C5 → D1,D2,D3 minimum C3
  - Holistic improvement, not siloed excellence
```

---

### AP_S3: Automation Without Foundation

```yaml
Síntoma: C4 automation sin C3 measurement
Causa: "Automate first, measure later" (backwards)
Consecuencia: Automation ineficaz, automated wrong things
Ejemplo:
  - CI/CD pipeline automated
  - Pero no tracking DORA metrics (don't know if improving)
  - Automation exists, value unclear

Fix: Measure BEFORE automate
  - C3 establece baseline (cycle time manual 45 min)
  - C4 automates (cycle time automated 5 min)
  - Improvement quantified (9× faster)
```

---

## §8. CONEXIÓN PRINCIPIOS MANIFIESTO

### Smartness Implementa Principios

```yaml
P4_Flujo_Continuo:
  - C1-C2: Flow interrumpido (manual handoffs)
  - C4-C6: Flow continuous (automation removes friction)
  - Smartness habilita P4 operacionalmente

P6_Probabilístico:
  - C1-C2: Deterministic thinking (estimates as commitments)
  - C3-C5: Probabilistic (forecasts with confidence intervals)
  - C5-C6 requiere probabilistic para scenario planning

P7_Parsimonia:
  - Smartness mismo es parsimonioso (6 levels, not 10)
  - 24 celdas (4×6) mínimo para completitud
  - Trade-off: Comprehensiveness vs Simplicity

P8_Herramienta_No_Oráculo:
  - C6 es máximo level (bounded autonomy)
  - C7 eliminated porque violaría P8
  - Smartness respeta human oversight siempre

P10_Culture_Emergent:
  - Culture NO es nivel Smartness
  - Culture EMERGE de Smartness sustained
  - C5-C6 org → innovation culture (porque experimentation safe)
```

---

## Referencias Cruzadas

- **Manifiesto P8:** `CORE/00_Manifiesto.md` §3 (C6 limit justification)
- **Delegación M1-M6:** `CORE/04_Delegacion.md` (mapping to Smartness levels)
- **Observables:** `DOMINIOS/D2_Percepcion.md` (enabled by Smartness)
- **KPIs Smartness:** `APLICACION/A5_Medicion.md` §X (to be added)
- **Assessment Smartness:** `APLICACION/A3_Diagnostico.md` §X (to be integrated)
- **Implementation roadmap:** `APLICACION/A4_Implementacion.md` (maturity paths)

---

**Fin de Smartness**
