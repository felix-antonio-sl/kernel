# A5_Medicion

**Versión:** 1.0.0 | **Estado:** Definitivo | **Audiencia:** Data Teams, Engineering Managers, Executives

---

## §1. FRAMEWORK MEDICIÓN KERNEL

### Principios

```yaml
P1_Outside_In:
  Filosofía:
    - Métricas externas (O1-O8) primero
    - Métricas internas (I1-I3) segundo
    - Optimizar primero valor entregado, luego eficiencia interna
  
  Conexión_Composición:
    - Métricas O1 (Demanda) miden necesidades destinatarios
    - Métricas O2 (Valor) miden outcomes productos_servicios
    - Ver `CORE/01_Primitivos.md` §7 para composición formal
      Unidad_Trabajo con outputs/destinatarios/entorno explícitos
  
  Implicación_Práctica:
    - Antes de medir eficiencia interna (cycle time, utilization)
    - Validar que estamos entregando valor a destinatarios correctos
    - "Doing the right thing" > "Doing things right"
    - Product-market fit primero, optimización operacional después

P2_Leading_and_Lagging:
  - Leading indicators: Predicen futuro (ej: NPS → churn futuro)
  - Lagging indicators: Confirman resultado (ej: revenue)
  - Balance ambos (no solo lagging)

P3_Actionable:
  - Si métrica no cambia comportamiento → No medir
  - Target claro (ej: >80, no "mejorar")
  - Owner asignado por métrica

P4_Automated:
  - Manual tracking no escala
  - Dashboards real-time o near-real-time
  - Alerts automáticos cuando threshold
```

---

## §2. KPIs POR DOMINIO

### ARQUITECTURA (A_Score, 0-100)

| KPI | Definición | Fórmula | Target | Frecuencia | Owner |
|-----|-----------|---------|--------|------------|-------|
| **A1_Team_Stability** | % teams sin cambios roster últimos 6m | (Teams_Sin_Cambios / Total_Teams) × 100 | >70% | Trimestral | HR / CTO |
| **A2_Decision_Clarity** | % decisiones Type 1/Type 2 clasificadas | (Decisiones_Clasificadas / Total) × 100 | >90% | Mensual | COO |
| **A3_Handoff_Efficiency** | Avg handoff ratio procesos críticos | Avg(Handoffs / Steps) × 100 | <25% | Trimestral | Process Owner |
| **A4_Span_of_Control** | Avg reports directos per manager | Avg(Reports_Directos) | 5-9 | Trimestral | HR |
| **A5_Org_Complexity** | # layers jerárquicos | Count(Layers CEO → IC) | <5 (org <500) | Anual | CTO |
| **A6_RACI_Clarity** | % procesos críticos con RACI documentado | (Procesos_RACI / Total_Críticos) × 100 | >95% | Trimestral | COO |

**A_Score Agregado:**  

```
A_Score = (A1 + A2 + A3 + (100 - (A4-5)*10) + (100 - A5*10) + A6) / 6
```

**Disclaimer calibración**: Ponderaciones iguales (1/6 cada componente) asumen importancia balanceada. Organizaciones pueden ajustar según contexto (ej: si span-of-control crítico, aumentar peso A4). Ver `DOMINIOS/D2_Percepcion.md` §4 para metodología calibración.

---

### PERCEPCIÓN (H_Score, 0-100)

**Ver fórmula completa:** `DOMINIOS/D2_Percepcion.md` §4

| KPI | Definición | Target | Frecuencia | Data Source | Owner |
|-----|-----------|--------|------------|-------------|-------|
| **O1_Demanda** | Backlog growth rate % trimestral | +5-10% | Trimestral | Jira, Salesforce | Product |
| **O2_Valor** | NPS score | >50 | Mensual | Qualtrics | Customer Success |
| **O3_Capacidad** | Utilization rate % | 70-85% | Semanal | Jira, HR system | Engineering |
| **O4_Eventos** | # incidents críticos sin resolver >30d | 0 | Semanal | PagerDuty | SRE |
| **O5_Restricciones** | Compliance score % | 100% | Mensual | Compliance system | Legal |
| **O6_Competencia** | Win rate % (deals won / total deals) | >60% | Trimestral | Salesforce | Sales |
| **O7_Dependencias** | Vendor health score avg | >80 | Trimestral | Vendor mgmt | Procurement |
| **O8_Calidad_Info** | Data quality score % | >90% | Mensual | DBT, Alation | Data |
| **I1_Velocidad_Decisional** | Time-to-decision avg (días) | <7 | Mensual | Decision log | COO |
| **I2_Salud_Talento** | Engagement score | >75 | Trimestral | Culture Amp | HR |
| **I3_Eficiencia_Flujo** | Flow efficiency % | >40% | Semanal | Jira | Engineering |

---

### DECISIÓN (D_Score, 0-100)

| KPI | Definición | Fórmula | Target | Frecuencia | Owner |
|-----|-----------|---------|--------|------------|-------|
| **D1_OKR_Quality** | % OKRs outcome-based (no output) | (OKRs_Outcome / Total) × 100 | >90% | Trimestral | Product |
| **D2_OKR_Achievement** | % OKRs alcanzados >70% | (OKRs_>70% / Total) × 100 | >75% | Trimestral | C-level |
| **D3_Roadmap_Predictability** | % roadmap items delivered on-time | (On_Time / Total_Planned) × 100 | >70% | Trimestral | Product |
| **D4_Portfolio_Balance** | % initiatives by type (STEP/GROWTH/DELAYED) | Mix: 50/30/20 | Target mix | Trimestral | CPO |
| **D5_Decision_Velocity** | Avg time decisión Type 2 (días) | Avg(Decision_Date - Problem_Date) | <7 | Mensual | COO |
| **D6_Preparación_Score** | Avg R1-R5 score transformaciones | Avg(R_Score) | >70 | Per initiative | PMO |

**D_Score Agregado:**  

```
D_Score = (D1 + D2 + D3 + D4_Quality + (100 - D5*10) + D6) / 6
```

**Disclaimer calibración**: Ponderaciones iguales (1/6) asumen balance. Context-specific adjustments recomendados (ej: org strategic planning critical → aumentar D6 weight). Calibrar localmente según correlation con outcomes.

---

### OPERACIÓN (O_Score, 0-100)

| KPI | Definición | Fórmula | Target | Frecuencia | Owner |
|-----|-----------|---------|--------|------------|-------|
| **O1_Cycle_Time** | Avg días start → done | Avg(Done_Date - Start_Date) | <5 días | Semanal | Engineering |
| **O2_Throughput** | Items completados / semana | Count(Done_Items) / Week | Trend ↑ | Semanal | Engineering |
| **O3_WIP** | # items "In Progress" simultáneos | Count(Status = "In Progress") | <1.5 × Team_Size | Semanal | Engineering |
| **O4_Flow_Efficiency** | % tiempo value-add vs wait | (Work_Time / Total_Time) × 100 | >40% | Semanal | Engineering |
| **O5_Deploy_Frequency** | Deploys to prod per día | Count(Deploys) / Day | >1/día (elite) | Diario | SRE |
| **O6_Lead_Time** | Tiempo commit → production | Avg(Deploy_Time - Commit_Time) | <1 hr (elite) | Diario | SRE |
| **O7_Change_Failure_Rate** | % deploys causan incident | (Incidents / Deploys) × 100 | <5% (elite) | Semanal | SRE |
| **O8_MTTR** | Tiempo detectar → resolver incident | Avg(Resolve_Time - Detect_Time) | <1 hr (elite) | Per incident | SRE |
| **O9_Tech_Debt_Score** | Weighted score (coverage, complexity, vulns) | Formula §5 DOMINIOS/D4 | <30 | Mensual | Engineering |
| **O10_Test_Coverage** | % code covered by tests | (Lines_Covered / Total_Lines) × 100 | >80% | Diario | Engineering |

**O_Score Agregado (DORA + Flow):**  

```
O_Score = (
  (100 - O1_Cycle*10) + O2_Normalized + (100 - O3_Excess*10) + O4 +
  O5_Normalized + (100 - O6_LeadTime*10) + (100 - O7_ChangeFailure*2) +
  (100 - O8_MTTR*10) + (100 - O9_TechDebt) + O10
) / 10
```

**Disclaimer calibración**: Fórmula compleja integra DORA metrics (O5-O8) con Flow metrics (O1-O4) y quality (O9-O10). Pesos derivados de State of DevOps Report correlations pero ajustables. Organizaciones high-reliability (finance, health) pueden aumentar O7-O8 weights. Ver calibración methodology `DOMINIOS/D2_Percepcion.md` §4.

---

## §3. DASHBOARDS RECOMENDADOS

### Dashboard Ejecutivo (C-level)

```yaml
Refresh: Daily
Audience: CEO, CTO, CPO, COO

Widgets:
  1. H_Score Overall (0-100):
     - Gauge chart grande
     - Trend últimos 4 trimestres
     - Color: Verde >80, Amarillo 60-80, Rojo <60
  
  2. Observables Breakdown (Radar chart):
     - 11 observables (O1-O8, I1-I3)
     - Actual vs Target
  
  3. Top 3 Risks (Table):
     - Observable bajo + Impact + Mitigación
  
  4. OKRs Progress (Bar chart):
     - % completion cada OKR
     - On-track vs At-risk vs Off-track
  
  5. Deployment Frequency (Line chart):
     - Deploys/día últimos 30 días
     - Target line (elite = 1/día)

Tools: Tableau, Looker, Metabase
```

---

### Dashboard Managers

```yaml
Refresh: Hourly
Audience: Engineering Managers, Product Managers

Widgets:
  1. Team Health (Table):
     - Por team: Cycle time, Throughput, WIP, Satisfaction
     - Color-coded vs targets
  
  2. Flow Metrics (Line chart):
     - Cycle time últimos 8 semanas
     - Throughput últimas 8 semanas
  
  3. Blockers & Dependencies (Kanban board):
     - Items bloqueados >3 días
     - Dependencies unresolved
  
  4. Tech Debt Trend (Line chart):
     - Tech debt score últimos 6 meses
     - Target line (30)
  
  5. Incident Log (Table):
     - Últimos 10 incidents
     - Severity, MTTR, Status

Tools: Jira dashboards, Linear, Jellyfish
```

---

### Dashboard Team (ICs)

```yaml
Refresh: Real-time
Audience: Engineers, Designers, PMs

Widgets:
  1. Sprint Progress (Burndown):
     - Items remaining vs ideal
     - Velocity trend
  
  2. WIP Visualization (Kanban):
     - Todo / In Progress / Done
     - WIP limits highlighted
  
  3. CI/CD Pipeline Status:
     - Build status (green/red)
     - Test coverage %
     - Deployment queue
  
  4. Personal Metrics (Individual):
     - My items this sprint
     - My avg cycle time
     - My PR review time
  
  5. Team OKRs (Progress bars):
     - Team-level OKRs progress
     - Contribution this week

Tools: Jira, GitHub, CircleCI dashboards
```

---

## §4. ALERTAS & THRESHOLDS

### Alerts Automáticos

```yaml
Alert_1_H_Score_Drop:
  Condition: H_Score cae >5 pts vs mes anterior
  Severity: Yellow
  Action: Diagnóstico root cause (1 semana)
  Recipient: CTO, COO

Alert_2_H_Score_Critical:
  Condition: H_Score <60
  Severity: Red
  Action: Emergency QBR, transformación urgente
  Recipient: CEO, Board

Alert_3_Cycle_Time_Spike:
  Condition: Cycle time >10 días por 2 semanas consecutivas
  Severity: Yellow
  Action: Value stream mapping, identify bottlenecks
  Recipient: Engineering Manager

Alert_4_Deploy_Failure_Rate:
  Condition: Change failure rate >10% por 1 semana
  Severity: Red
  Action: Feature freeze, fix quality gates
  Recipient: CTO, SRE Lead

Alert_5_Tech_Debt_Critical:
  Condition: Tech debt score >50
  Severity: Red
  Action: Allocate 50% capacity health work
  Recipient: VP Engineering

Alert_6_Churn_Spike:
  Condition: Churn rate sube >3pp vs Q anterior
  Severity: Yellow
  Action: Customer feedback deep-dive
  Recipient: CEO, CPO

Alert_7_Turnover_Spike:
  Condition: Turnover >5% en 1 mes (annualized >60%)
  Severity: Red
  Action: Retention program urgente, exit interviews
  Recipient: CEO, CHRO
```

---

## §5. BENCHMARKS INDUSTRY

### DevOps (DORA)

| Métrica | Elite | High | Medium | Low |
|---------|-------|------|--------|-----|
| **Deploy Frequency** | Multiple per day | Weekly-Daily | Monthly-Weekly | <Monthly |
| **Lead Time** | <1 hr | 1 día - 1 semana | 1 semana - 1 mes | >1 mes |
| **Change Failure Rate** | <5% | 5-15% | 15-30% | >30% |
| **MTTR** | <1 hr | <1 día | 1 día - 1 semana | >1 semana |

**Fuente:** State of DevOps Report 2023

---

### Flow Metrics (Kanban)

| Métrica | World-Class | Good | Average | Poor |
|---------|-------------|------|---------|------|
| **Cycle Time** | <3 días | 3-7 días | 7-14 días | >14 días |
| **Flow Efficiency** | >40% | 25-40% | 15-25% | <15% |
| **WIP per Person** | <2 items | 2-3 items | 3-5 items | >5 items |
| **Throughput Variability** | CV <30% | CV 30-50% | CV 50-100% | CV >100% |

**Fuente:** Kanban Maturity Model, David Anderson

---

### Org Health (McKinsey OHI)

| Dimensión | Top Quartile | Median | Bottom Quartile |
|-----------|--------------|--------|-----------------|
| **Employee Engagement** | >85/100 | 65-75 | <55 |
| **Turnover (Tech)** | <8%/año | 12-18% | >25% |
| **Time-to-Fill (Engineering)** | <30 días | 45-60 días | >90 días |
| **Internal Mobility** | >50% promotions internal | 30-40% | <20% |

**Fuente:** McKinsey Organizational Health Index

---

## §6. DATA COLLECTION AUTOMATION

### Stack Técnico Recomendado

```yaml
Layer_1_Data_Sources:
  - Jira / Linear (work tracking)
  - GitHub / GitLab (code, PRs, commits)
  - CircleCI / GitHub Actions (CI/CD)
  - PagerDuty / Opsgenie (incidents)
  - Salesforce (customer data, pipeline)
  - Qualtrics / Typeform (surveys NPS, engagement)
  - Culture Amp / Lattice (employee feedback)

Layer_2_ETL:
  - Fivetran / Airbyte: Extract data sources
  - dbt: Transform data (quality, aggregations)
  - Airflow: Orchestrate pipelines (daily refresh)

Layer_3_Data_Warehouse:
  - Snowflake / BigQuery / Redshift
  - Schema: KERNEL metrics (11 observables, A/D/O scores)

Layer_4_BI_Tools:
  - Tableau / Looker / Metabase
  - Dashboards pre-built (Ejecutivo, Managers, Teams)
  - Alerts automated (Slack, email cuando thresholds)

Layer_5_ML_Analytics (Opcional):
  - Anomaly detection (O4)
  - Churn prediction (O2)
  - Capacity forecasting (O3)
```

---

### Data Model KERNEL

```sql
-- Tabla maestra H_Score
CREATE TABLE h_score_history (
  date DATE PRIMARY KEY,
  h_score DECIMAL(5,2),
  o1_demanda DECIMAL(5,2),
  o2_valor DECIMAL(5,2),
  o3_capacidad DECIMAL(5,2),
  o4_eventos DECIMAL(5,2),
  o5_restricciones DECIMAL(5,2),
  o6_competencia DECIMAL(5,2),
  o7_dependencias DECIMAL(5,2),
  o8_calidad_info DECIMAL(5,2),
  i1_velocidad_decisional DECIMAL(5,2),
  i2_salud_talento DECIMAL(5,2),
  i3_eficiencia_flujo DECIMAL(5,2)
);

-- Tabla team metrics
CREATE TABLE team_metrics (
  team_id VARCHAR(50),
  date DATE,
  cycle_time_days DECIMAL(5,2),
  throughput INT,
  wip INT,
  flow_efficiency DECIMAL(5,2),
  deploy_frequency DECIMAL(5,2),
  tech_debt_score DECIMAL(5,2),
  satisfaction_score DECIMAL(5,2),
  PRIMARY KEY (team_id, date)
);

-- Tabla OKRs
CREATE TABLE okrs (
  okr_id VARCHAR(50) PRIMARY KEY,
  objective TEXT,
  key_result_1 TEXT,
  key_result_2 TEXT,
  key_result_3 TEXT,
  kr1_progress DECIMAL(5,2),
  kr2_progress DECIMAL(5,2),
  kr3_progress DECIMAL(5,2),
  quarter VARCHAR(10),
  owner VARCHAR(100)
);
```

---

## §7. MÉTRICAS IA ESPECÍFICAS

### Por Modo Delegación

| Modo | Métrica Clave | Definición | Target | Frecuencia |
|------|--------------|-----------|--------|------------|
| **M1** | Coverage % | % procesos monitoreados | >95% | Mensual |
| **M2** | Precision/Recall | Accuracy recomendaciones | >90% | Semanal |
| **M3** | Adoption Rate | % sugerencias aceptadas | >60% | Semanal |
| **M4** | Override Rate | % decisiones IA revertidas | <10% | Semanal |
| **M5** | Collaboration Quality | Human satisfaction colaboración | >75/100 | Mensual |
| **M6** | Automation Success | % executions exitosas sin intervención | >95% | Diario |

---

### Bias Detection

```yaml
Metrics_Fairness:
  - Demographic parity (ej: hiring IA no discrimina género)
  - Equal opportunity (ej: churn prediction igual recall por segmento)
  - Calibration (ej: confidence scores well-calibrated)

Audit_Frequency: Trimestral
Tools: Fairlearn, AI Fairness 360
Owner: Data Ethics Lead
```

---

### §7.1 KPIs AWARENESS LEVELS (S1-S3)

```yaml
Contexto: Métricas para niveles percepción (CORE/02 §2, D2 §5)

S1_DETECT_Metrics:

  | KPI | Definición | Fórmula | Target | Owner |
  |-----|-----------|---------|--------|-------|
  | S1_Monitoring_Coverage | % systems críticos con monitoring básico | (Systems_Monitored / Total_Critical) × 100 | >95% | DevOps |
  | S1_Dashboard_Availability | Uptime dashboards observabilidad | % tiempo dashboards disponibles | >99.9% | SRE |
  | S1_Telemetry_Latency | Lag entre evento → visualización dashboard | P95 latency (seconds) | <30s | Platform |
  | S1_Log_Retention | Días logs searchable disponibles | Min(retention_days) | >30d | Data |

S2_COMPREHEND_Metrics:

  | KPI | Definición | Fórmula | Target | Owner |
  |-----|-----------|---------|--------|-------|
  | S2_H_Score_Automated | ¿H_Score calculado automáticamente? | Boolean (Yes/No) | Yes | Analytics |
  | S2_Alert_Quality | % alerts actionable (no false positives) | (Valid_Alerts / Total_Alerts) × 100 | >80% | SRE |
  | S2_Observable_Coverage | % observables O1-O8, I1-I3 tracked | (Obs_Tracked / 11) × 100 | 100% | Product |
  | S2_Anomaly_Detection | ¿Pattern recognition automated? | Boolean + accuracy | >85% acc | ML Eng |

S3_PROJECT_Metrics:

  | KPI | Definición | Fórmula | Target | Owner |
  |-----|-----------|---------|--------|-------|
  | S3_Forecast_Accuracy | MAPE (mean abs % error) forecasts | Avg(\|Actual - Forecast\| / Actual) | <15% | Data Sci |
  | S3_Crisis_Monitoring | ¿Threshold H<45 monitored w/ alerts? | Boolean | Yes | COO |
  | S3_Scenario_Planning | # scenario analyses per quarter | Count (strategic decisions) | ≥3 | Strategy |
  | S3_Predictive_Models_Prod | # ML models serving predictions | Count (active models) | 5-10 | ML Lead |

Awareness_Maturity_Score:
  Formula: (S1_avg × 0.4) + (S2_avg × 0.35) + (S3_avg × 0.25)
  Benchmark:
    >80: Excelente
    60-80: Bueno
    40-60: Atención
    <40: Crítico
```

---

### §7.2 KPIs DECISION MODES (D1-D4)

```yaml
Contexto: Métricas para modos decisionales (CORE/02 §3, D3 §6)

D1_DIRECT_FEEDBACK_Metrics:

  | KPI | Definición | Fórmula | Target | Owner |
  |-----|-----------|---------|--------|-------|
  | D1_Automation_Rate | % decisiones D1 automated | (Auto_D1 / Total_D1_Opportunities) × 100 | >60% | Ops |
  | D1_Loop_Latency | Tiempo sense → decide → act (D1) | P95 latency (ms) | <1s | DevOps |
  | D1_Bounded_Autonomy | % D1 agents con limits explícitos | (Agents_Bounded / Total_D1) × 100 | 100% | SRE |

D2_RULE_BASED_Metrics:

  | KPI | Definición | Fórmula | Target | Owner |
  |-----|-----------|---------|--------|-------|
  | D2_Rule_Coverage | % business rules documentadas | (Rules_Doc / Critical_Dec_Types) × 100 | >90% | Product |
  | D2_Workflow_Automation | % approval workflows automated | (Workflows_Auto / Total) × 100 | >75% | Ops |
  | D2_Rule_Engine_Usage | ¿Rules engine deployed? | Boolean (tool name) | Yes | Eng |
  | D2_Edge_Case_Rate | % decisions sin rule match | (No_Match / Total_D2) × 100 | <5% | Product |

D3_ASSOCIATIVE_Metrics:

  | KPI | Definición | Fórmula | Target | Owner |
  |-----|-----------|---------|--------|-------|
  | D3_ML_Models_Production | # ML models serving decisions | Count (active, monitored) | 5-10 | ML Lead |
  | D3_Model_Accuracy | Avg accuracy models en prod | Avg(accuracy_per_model) | >85% | ML Eng |
  | D3_Human_Validation_Rate | % D3 decisions validated by human | (Validated / Total_D3) × 100 | >90% | PM |
  | D3_Model_Drift_Detection | ¿Drift monitoring active? | Boolean + alert frequency | Yes, weekly | ML Ops |

D4_KNOWLEDGE_BASED_Metrics:

  | KPI | Definición | Fórmula | Target | Owner |
  |-----|-----------|---------|--------|-------|
  | D4_Decision_Latency_Strategic | Tiempo problem → strategic decision | P50 latency (days) | <7d | CPO |
  | D4_Decision_Latency_Tactical | Tiempo problem → tactical decision | P50 latency (hours) | <24h | VP Eng |
  | D4_Simulation_Availability | ¿Simulation tools available? | Boolean (tool list) | Yes | Strategy |
  | D4_OKR_Structure | % strategic decisions con OKR linkage | (Decisions_OKR / Total_D4) × 100 | >80% | Product |

Decision_Automation_Overall:
  Formula: % decisiones repeatables que están automated
  Benchmark:
    >50%: Excelente
    30-50%: Bueno
    15-30%: Atención
    <15%: Crítico
```

---

### §7.3 KPIs EXECUTION LEVELS (A1-A3)

```yaml
Contexto: Métricas para niveles ejecución (CORE/02 §4, D4 §12)

A3_ACTION_Metrics (Level 1):

  | KPI | Definición | Fórmula | Target | Owner |
  |-----|-----------|---------|--------|-------|
  | A3_Deploy_Frequency | Deployments/day (atomic actions) | Count(deploys) / days | >10/day | DevOps |
  | A3_Action_Idempotency | % actions idempotent (safe retry) | (Idempotent / Total_Actions) × 100 | >95% | Eng |
  | A3_Action_Audit | % actions logged con timestamp+actor | (Logged / Total) × 100 | 100% | Security |
  | A3_Rollback_Success_Rate | % rollbacks exitosos <5 min | (Success_Rollback / Total) × 100 | >98% | SRE |

A2_SPECIFICATION_Metrics (Level 2):

  | KPI | Definición | Fórmula | Target | Owner |
  |-----|-----------|---------|--------|-------|
  | A2_Config_Drift | % infra con config drift vs IaC | (Drifted / Total_Resources) × 100 | <5% | Platform |
  | A2_Environment_Parity | Similarity dev/staging/prod configs | Config_Match_Score | >90% | DevOps |
  | A2_Policy_Coverage | % actions con policies explícitas | (With_Policy / Total_Actions) × 100 | >85% | Ops |
  | A2_Resource_Optimization | Avg cost per action (efficiency) | $ / action (trend) | ↓ 10%/yr | FinOps |

A1_PLANNING_Metrics (Level 3):

  | KPI | Definición | Fórmula | Target | Owner |
  |-----|-----------|---------|--------|-------|
  | A1_Workflow_Complexity | Avg steps en workflows critical | Avg(steps_per_workflow) | <15 | Arch |
  | A1_Orchestration_Success | % workflows completados sin errors | (Success / Total_Runs) × 100 | >95% | Ops |
  | A1_Parallel_Efficiency | % workflow steps parallelizables executed parallel | (Parallel / Parallelizable) × 100 | >80% | Eng |
  | A1_Human_Intervention_Rate | % workflows requiring manual intervention | (Manual / Total) × 100 | <10% | PM |

Execution_Maturity_Score:
  Formula: (A3_avg × 0.4) + (A2_avg × 0.35) + (A1_avg × 0.25)
  Benchmark:
    >85: Excelente
    70-85: Bueno
    50-70: Atención
    <50: Crítico
```

---

## §8. REPORTING CADENCE

### Frecuencias Recomendadas

```yaml
Daily:
  - CI/CD metrics (deploy frequency, build status)
  - Incident log (if any)
  - WIP levels

Weekly:
  - Cycle time, throughput
  - Sprint progress
  - Tech debt score

Monthly:
  - H_Score full calculation
  - Team satisfaction surveys
  - OKRs progress (mid-quarter check)

Quarterly:
  - QBR presentation (H_Score, top wins/challenges)
  - OKRs finales + planning próximo Q
  - Strategy adjustments

Annual:
  - Retrospectiva full año
  - H_Score trend análisis
  - Benchmarking external (si disponible)
```

---

## §9. MÉTRICAS QUE EVITAR (VANITY METRICS)

### Anti-Patterns Medición

```yaml
AP_M1_Lines_of_Code:
  - Por qué malo: Más código ≠ mejor (puede ser bloat)
  - Mejor usar: Value delivered (features shipped, NPS)

AP_M2_Hours_Worked:
  - Por qué malo: Hours ≠ productivity (puede ser ineficiencia)
  - Mejor usar: Throughput, cycle time

AP_M3_Story_Points:
  - Por qué malo: Puntos no comparable cross-team, gaming
  - Mejor usar: Cycle time (días reales)

AP_M4_Bugs_Found:
  - Por qué malo: Incentiva crear bugs para luego "find"
  - Mejor usar: Bugs escaped to prod (quality outcome)

AP_M5_Code_Reviews_Count:
  - Por qué malo: Cantidad ≠ calidad review
  - Mejor usar: Time-to-review, thoroughness (comments constructivos)

AP_M6_Meeting_Hours:
  - Por qué malo: Solo mide tiempo, no effectiveness
  - Mejor usar: Decision velocity, alignment surveys

AP_M7_Features_Shipped:
  - Por qué malo: Output no outcome, puede ser features nadie usa
  - Mejor usar: Feature adoption rate, NPS impact
```

---

## ✅ SPRINT 3 COMPLETADO

**Documentos APLICACION generados (5 de 5):**

1. ✅ A1_Patrones.md (250 líneas) - 50 patrones tabulados, combos
2. ✅ A2_Antipatrones.md (269 líneas) - 30 antipatrones, remediation
3. ✅ A3_Diagnostico.md (577 líneas) - Framework assessment 5 fases, caso TechCorp
4. ✅ A4_Implementacion.md (762 líneas) - Playbook transformación 6 fases, gates
5. ✅ A5_Medicion.md (actual) - KPIs por dominio, dashboards, benchmarks

**Total generado Sprint 3:** ~1,900 líneas

**Progreso acumulado:**

- Sprint 1 (CORE): ~3,900 líneas
- Sprint 2 (DOMINIOS): ~2,650 líneas
- Sprint 3 (APLICACION): ~1,900 líneas
- **Total: ~8,450 líneas (~70% del objetivo 12,000)**

**Estado KERNEL:** Toolkit completo practitioners disponible ✅

**Próximo:** Sprint 4 (DOMINIOS_ESPECIALIZADOS) o Sprint 5 (REFERENCIA) según preferencia

---

## Referencias Cruzadas

- **11 Observables:** `DOMINIOS/D2_Percepcion.md`
- **H_Score fórmula:** `DOMINIOS/D2_Percepcion.md` §4
- **Flow metrics:** `DOMINIOS/D4_Operacion.md` §2
- **DORA metrics:** `DOMINIOS/D4_Operacion.md` §4.2
- **Tech debt score:** `DOMINIOS/D4_Operacion.md` §5.2
- **Diagnóstico framework:** `APLICACION/A3_Diagnostico.md`
