# D2_Percepcion

**Versión:** 3.0.0 | **Estado:** Definitivo | **Audiencia:** Líderes, Analistas, Data Engineers

## INVARIANTE DOMINIO

**Percepción = Aplicación sistemática de Sense (S1-S3) sobre 16 observables organizacionales → H_Score.**

**Propiedad:** D2 NO decide qué hacer (eso es D3), solo detecta, comprende y proyecta estado actual/futuro.

## REFERENCIAS RÁPIDAS

```yaml
Observables_16:
  Externos_8: O1-O8 (Demanda, Valor, Capacidad, Eventos, Restricciones, Competencia, Dependencias, Calidad)
  Internos_3: IN1-IN3 (Velocidad Decisional, Salud Talento, Eficiencia Flujo)
  Security_5: SO1-SO5 (Vulnerabilidades, Secretos, Acceso, Cumplimiento, Respuesta)

Métrica_Agregada:
  H_Score: §3 - Health organizacional (0-100, ponderado)
  Crisis_Thresholds: H<45 (emergency), H<30 (existential)

Niveles_Awareness:
  S1_Detectar: §4.1 - Raw facts (M1 Monitor)
  S2_Comprender: §4.2 - Patterns + context (M2-M3 Inform/Enable)
  S3_Proyectar: §4.3 - Forecasts + scenarios (M3-M4 Enable/Control)

Patrones:
  MVO: §5.1 - 3 observables → H_Score baseline (2-4 semanas)
  Drift_Detection: §5.2 - H_Score Δ >5pts/trimestre → escalate
  Anomaly_Detection: §5.3 - ML patterns (M4-M5)

Cross-References:
  CORE/02_Ciclo_Fundamental.md §2: Fase Sense (S1-S3 formal)
  CORE/01_Primitivos.md §3A: Primitivo Señal (alertas)
  CORE/03_Arquitectura.md §6: Security como límite transversal
  D1_Arquitectura.md §5: A_Score, IN1, IN2 vinculados
  D3_Decision.md §1: OKRs consumen observables
  D4_Operacion.md §2: IN3 Eficiencia Flujo detallado
```

## Responsabilidad

**PERCEPCIÓN detecta ESTADO organizacional interno/externo mediante 16 observables + 3 niveles awareness (S1-S3).**

**Pregunta clave:** ¿Cuál es nuestro estado actual y hacia dónde vamos?

**NO pregunta:** ¿Qué hacemos al respecto? (eso es D3 Decisión)

## §0. QUICK START: PERCEPCIÓN MÍNIMA VIABLE (MVO)

**Objetivo**: H_Score baseline en 2-4 semanas con 3 observables críticos.

### MVO Checklist

```yaml
Week_1-2: Instrumentar 3 Observables Críticos
  ☐ O2_Valor: NPS/CSAT/Churn (customer satisfaction)
  ☐ IN2_Salud_Talento: Turnover rate (employee retention)
  ☐ IN3_Eficiencia_Flujo: Cycle time (delivery speed)
  
  Tool: Qualtrics (O2), HR system (IN2), Jira/Linear (IN3)
  Frecuencia: Mensual O2/IN2, Semanal IN3

Week_3: Calcular H_Score MVO
  ☐ Fórmula simplificada: H ≈ 0.70*avg(3 observables) + 30 (baseline otros)
  ☐ Interpretación: >70 OK, 60-70 atención, <60 crisis
  ☐ Dashboard básico: Excel/Metabase/Tableau (3 gráficas)

Week_4: Expansión Planificada
  ☐ Identificar próximos 3 observables (típico: O1, O3, IN1)
  ☐ Timeline: +1 observable cada 2-4 semanas
  ☐ Target: 11 observables (base) en 6 meses, 16 (full) en 12 meses

Output_MVO:
  - H_Score baseline (~aproximado, accionable)
  - Momentum: 2 semanas → visibilidad
  - Foundation: Expansión incremental clara

Saltar_MVO_Si:
  - Ya tienes dashboards KPIs + H_Score >60
  - Data collection automated
  → Ir directo §1-§4 completo
```

## §1. ARQUITECTURA SENSING: 16 OBSERVABLES

### Estructura Ontológica

```
┌─────────────────────────────────────────┐
│     ENTORNO EXTERNO (8 observables)     │
├──────────────────────────────────────────┤
│ O1: Demanda         │ O5: Restricciones │
│ O2: Valor           │ O6: Competencia   │
│ O3: Capacidad       │ O7: Dependencias  │
│ O4: Eventos         │ O8: Calidad Info  │
└──────────────────────────────────────────┘
              ↓
┌──────────────────────────────────────────┐
│   ORGANIZACIÓN INTERNA (3 observables)   │
├──────────────────────────────────────────┤
│ IN1: Velocidad Decisional                │
│ IN2: Salud Talento                       │
│ IN3: Eficiencia Flujo                    │
└──────────────────────────────────────────┘
              ↓
┌──────────────────────────────────────────┐
│  SEGURIDAD TRANSVERSAL (5 observables)   │
├──────────────────────────────────────────┤
│ SO1: Vulnerabilidades │ SO4: Cumplimiento│
│ SO2: Secretos         │ SO5: Respuesta   │
│ SO3: Acceso           │                  │
└──────────────────────────────────────────┘
              ↓
        H_Score (0-100)
```

### Propiedades Invariantes

```yaml
Ortogonalidad:
  - O1-O8: Externos (sensores entorno)
  - IN1-IN3: Internos (sensores org)
  - SO1-SO5: Transversales (Security como Límite L3, ver CORE/03 §6)
  
  NO hay overlap: Cada observable mide dimensión única

Completitud:
  - 16 observables suficientes modelar health organizacional
  - Validado: 10 casos diversos (REFERENCIA/R1_Casos.md)
  - NO agregar más → Violaría I1 Minimalidad

Composability:
  - Cada observable vincula a primitivos KERNEL:
    * O1 Demanda → productos_servicios + destinatarios (Outside-In)
    * O2 Valor → métricas_valor outcomes (Unidad_Trabajo)
    * IN3 Flujo → Estados + transiciones (Ciclo WSLC)
  - Ver CORE/01_Primitivos.md §7 para estructura completa
```

## §2. DEFINICIÓN OBSERVABLES (MINIMALISTA)

**Nota:** Definiciones completas con ejemplos extensos → `APLICACION/A5_Medicion.md`. Aquí solo esencia.

### O1. DEMANDA

```yaml
Qué_Mide: Necesidad mercado por productos_servicios
Indicadores: Backlog features, Support tickets, Sales pipeline, Market size
Score_0-100:
  90-100: Demanda creciendo 5-10%/trimestre
  50-70: Demanda estancada
  0-40: Demanda cayendo >15%/trimestre
Crisis: <30 → Emit(Señal: "Product_Market_Fit_Loss")
```

### O2. VALOR

```yaml
Qué_Mide: Percepción valor por destinatarios
Indicadores_Private: NPS, CSAT, Churn, Revenue/customer
Indicadores_Public: Citizen satisfaction, Service delivery, Trust indices
Score_0-100:
  90-100: NPS >50, Churn <5%
  45-70: NPS 20-50, Churn 5-15%
  0-45: NPS <20, Churn >15%
Crisis: <30 → Emit(Señal: "Customer_Defection_Crisis")
       <15 → Emit(Señal: "Market_Rejection_Existential")
```

### O3. CAPACIDAD

```yaml
Qué_Mide: Recursos vs demanda (workforce, financial, infrastructure)
Indicadores: Headcount vs backlog, Utilization, Cash runway, Time-to-hire
Score_0-100:
  90-100: Capacity surplus >15%, utilization 70-85%, cash >180d
  50-70: Capacity matches demand, cash 30-180d
  0-45: Capacity deficit >30%, utilization >95%, cash <30d
Crisis: <30 → Emit(Señal: "Capacity_Crisis_Protocol")
       <15 → Emit(Señal: "Existential_Capacity_Threat", cash <7d)
```

### O4. EVENTOS

```yaml
Qué_Mide: Disrupciones externas no planificadas
Indicadores: Incidents críticos, Regulación nueva, Tech breakthrough, Competitor moves
Score_0-100:
  90-100: Sin eventos críticos 3 meses
  70-85: 1-2 eventos menores gestionados
  0-65: 3+ eventos o 1 catastrófico no resuelto
```

### O5. RESTRICCIONES

```yaml
Qué_Mide: Límites regulatorios, legales, contractuales
Indicadores: Compliance %, Audit findings, SLA breaches, Legal risks
Score_0-100:
  95-100: 100% compliance, 0 findings críticos
  80-90: >95% compliance, <5 findings menores
  0-75: <95% compliance, findings críticos, breaches
```

### O6. COMPETENCIA

```yaml
Qué_Mide: Alternativas disponibles para destinatarios
Indicadores: Market share, Feature parity, Win/loss rate, Churn to competitor
Score_0-100:
  85-100: Market leader, feature parity >90%, Win rate >60%
  60-80: Market follower, parity 70-90%, Win rate 40-60%
  0-55: Laggard, parity <70%, Win rate <40%
```

### O7. DEPENDENCIAS

```yaml
Qué_Mide: Proveedores, partners, integraciones críticas
Indicadores: Vendor health, SLA compliance vendors, SPOFs, Integration failures
Score_0-100:
  90-100: Vendors estables, <2 SPOFs, <1% integration failures
  70-85: Vendors OK, 2-5 SPOFs, 1-3% failures
  0-65: Vendor risk alto, >5 SPOFs, >3% failures
```

### O8. CALIDAD INFORMACIÓN

```yaml
Qué_Mide: Confiabilidad y disponibilidad datos para decisiones
Indicadores: Data accuracy %, Coverage %, Freshness, Governance
Score_0-100:
  90-100: Accuracy >95%, coverage >90%, freshness <24h
  70-85: Accuracy 80-95%, coverage 70-90%, freshness 24-72h
  0-65: Accuracy <80%, coverage <70%, freshness >72h
```

### Observables Internos (IN1-IN3)

### IN1. VELOCIDAD DECISIONAL

```yaml
Qué_Mide: Rapidez y calidad toma decisiones
Indicadores:
  - Cycle time decisiones (Type 1 <14d, Type 2 <3d)
  - Decision quality (% correctas retrospectiva 6M)
  - Delegation rate (% delegadas vs centralizadas C-level)
  - Decision backlog (ARB = Architecture Review Board)

Score_0-100:
  90-100: Type 2 <3d, quality >75%, delegation >80%, backlog <10
  70-85: Type 2 3-7d, quality 60-75%, delegation 60-80%, backlog 10-30
  0-65: Type 2 >7d, quality <60%, delegation <60%, backlog >30

Type_1_vs_Type_2:
  Type 1 (Irreversible): M&A, reorg mayor → C-level, lento OK (<14d)
  Type 2 (Reversible): Features, tech stack → Delegar teams, rápido (<3d)
  Ver: D1_Arquitectura.md §1.7 (PE7), D3_Decision.md §10 para framework completo
```

### IN2. SALUD TALENTO

```yaml
Qué_Mide: Engagement, retención, desarrollo talento
Indicadores:
  - Turnover total (% anualizado)
  - Regretted attrition (% pérdidas críticas)
  - Engagement score (survey)
  - Time-to-fill vacantes
  - Promotion rate (% progresión interna)

Score_0-100:
  90-100: Turnover <10%, regretted <5%, engagement >75
  70-85: Turnover 10-15%, regretted 5-10%, engagement 60-75
  0-65: Turnover >15%, regretted >10%, engagement <60
```

### IN3. EFICIENCIA FLUJO

```yaml
Qué_Mide: Velocidad y predictibilidad entrega valor
Indicadores:
  - Cycle time (días start → done)
  - WIP (work in progress vs team size)
  - Throughput (items/semana completed)
  - Flow efficiency (% tiempo value-add vs wait)

Score_0-100:
  90-100: Cycle <5d, WIP <1.5× team, efficiency >40%
  70-85: Cycle 5-10d, WIP 1.5-2.0× team, efficiency 25-40%
  0-65: Cycle >10d, WIP >2.0× team, efficiency <25%

Vinculación: Ver D4_Operacion.md §2 para métricas DORA + flow detalladas
```

### Security Observables (SO1-SO5)

**Nota:** Security es **límite transversal L3**, NO dominio independiente. Ver CORE/03_Arquitectura.md §6.

### SO1. VULNERABILIDADES

```yaml
Qué_Mide: Exposición a vulnerabilidades técnicas
Indicadores: MTTP (Mean Time to Patch), CVE count critical/high, Scan coverage
Score_0-100:
  90-100: MTTP <7d, 0 CVEs critical, coverage >95%
  70-85: MTTP 7-30d, <5 CVEs critical, coverage 80-95%
  0-65: MTTP >30d, >5 CVEs critical, coverage <80%
```

### SO2. GESTIÓN SECRETOS

```yaml
Qué_Mide: Seguridad credentials, API keys, certificates
Indicadores: Vault adoption %, Rotation frequency, Hardcoded secrets detected
Score_0-100:
  90-100: 100% vaulted, rotation <90d, 0 hardcoded
  70-85: >80% vaulted, rotation 90-180d, <5 hardcoded
  0-65: <80% vaulted, rotation >180d, >5 hardcoded
```

### SO3. CONTROL ACCESO

```yaml
Qué_Mide: Identity governance (quién puede acceder qué)
Indicadores: MFA adoption %, Privileged accounts, Access reviews, Least-privilege
Score_0-100:
  90-100: MFA >95%, privileged <5% headcount, reviews 100%
  70-85: MFA 80-95%, privileged 5-10%, reviews >80%
  0-65: MFA <80%, privileged >10%, reviews <80%
```

### SO4. CUMPLIMIENTO NORMATIVO

```yaml
Qué_Mide: Adherencia regulaciones security/privacy (SOC2, ISO27001, GDPR)
Indicadores: Certifications activas, Controls compliance %, Audit findings, Fines
Score_0-100:
  90-100: ≥2 certs, >95% controls, 0 findings críticos, 0 fines
  70-85: 1 cert, 80-95% controls, <5 findings críticos, 0 fines
  0-65: 0 certs, <80% controls, >5 findings críticos, fines
```

### SO5. RESPUESTA INCIDENTES

```yaml
Qué_Mide: Capacidad detectar, contener, remediar security incidents
Indicadores: MTTD (Mean Time to Detect), MTTC (Contain), IR drills/año, Actions completed
Score_0-100:
  90-100: MTTD <1hr, MTTC <4hrs, ≥4 drills/año, actions 100%
  70-85: MTTD 1-24hrs, MTTC 4-24hrs, 2-3 drills/año, actions >80%
  0-65: MTTD >24hrs, MTTC >24hrs, <2 drills/año, actions <80%
```

## §3. H_SCORE: MÉTRICA AGREGADA HEALTH

### Fórmula Base (11 Observables)

```yaml
H_Score_Base = (
  0.70 * avg_ponderado(O1-O8) +
  0.20 * avg_ponderado(IN1-IN3) +
  0.10 * baseline_security
)

Pesos_Externos (O1-O8, suman 1.0):
  O1_Demanda: 0.12
  O2_Valor: 0.15        # Crítico
  O3_Capacidad: 0.10
  O4_Eventos: 0.08
  O5_Restricciones: 0.10
  O6_Competencia: 0.10
  O7_Dependencias: 0.08
  O8_Calidad_Info: 0.07

Pesos_Internos (IN1-IN3, suman 1.0):
  IN1_Velocidad_Decisional: 0.40
  IN2_Salud_Talento: 0.40
  IN3_Eficiencia_Flujo: 0.20

Baseline_Security: 75 (si SO1-SO5 no disponibles, asumir razonable)
```

### Fórmula Extended (16 Observables)

```yaml
H_Score_Extended = (
  0.90 * H_Score_Base_Renormalized +
  0.10 * avg(SO1-SO5)
)

Donde H_Score_Base_Renormalized = (
  0.90 * (
    0.72 * avg_ponderado(O1-O8) +   # 0.70 * 0.90 / (0.70+0.20) ≈ 0.72
    0.18 * avg_ponderado(IN1-IN3)   # 0.20 * 0.90 / (0.70+0.20) ≈ 0.18
  )
)

# Simplificación práctica (usar solo si precisión no crítica):
H_Score ≈ 0.72*avg_ponderado(O1-O8) + 0.18*avg_ponderado(IN1-IN3) + 0.10*avg(SO1-SO5)
```

### Interpretación

```yaml
Rangos:
  90-100: Excelencia organizacional (todos observables >85)
  75-89: Health bueno (operación sostenible)
  60-74: Atención requerida (gaps menores)
  45-59: Crítico (intervención necesaria)
  30-44: Emergency mode (P52 Crisis Management)
  0-29: Existential threat (survival protocols)

Crisis_Thresholds:
  IF H_Score < 45:
    → Emit(Señal: "Health_Crisis_Emergency")
    → Activate: CORE/08_Crisis_Management.md protocols
  
  IF H_Score < 30:
    → Emit(Señal: "Existential_Org_Threat")
    → Escalate: CEO/Board immediately
    → Freeze: All non-survival activities

Drift_Detection:
  IF H_Score drops >5 pts in 1 trimestre:
    → Emit(Señal: "Health_Drift_Alert")
    → Investigate: Qué observable(s) cayeron
    → Action: D3 debe priorizar remediation
```

### Customización Industry

```yaml
Financial/Healthcare (highly regulated):
  Security weight: 15-20% (renormalize base to 80-85%)
  
SaaS B2B (security-critical):
  Security weight: 12-15% (renormalize base to 85-88%)
  
B2C low-sensitivity:
  Security weight: 5-8% (renormalize base to 92-95%)
  
Default standard:
  Security weight: 10% (base 90%)
```

## §4. AWARENESS COGNITIVA: NIVELES S1-S3

**Fundamento:** Ciclo SDA (CORE/02 §2) define Sense en 3 niveles. D2 implementa estos niveles sobre 16 observables.

### §4.1. S1: DETECTAR (Raw Facts)

```yaml
Definición: Capturar señales crudas sin interpretar
Output: Datos raw (0-100 por observable)
Latencia: Real-time a diaria
Capacidad_IA: Extrema (sensores 24/7, M1 Monitor)

Implementación_Por_Observable:
  O2_Valor (NPS):
    S1: "NPS score = 42" (dato crudo)
    Tool: Qualtrics API → Database
    Frecuencia: Post-transaction + mensual survey
  
  IN3_Flujo (Cycle Time):
    S1: "Story-12345: 8.3 días" (dato crudo)
    Tool: Jira webhook → Metrics DB
    Frecuencia: Cada story transición a Done

Delegación:
  M1_Monitor: Sensores automated (APIs, webhooks, scrapers)
  Humano: Solo configuración inicial + validación spot-check

Antipatrón:
  ❌ Humano calcula manualmente cada semana (no escala, error-prone)
  ✅ Sistema emite dato, humano solo interpreta agregados
```

### §4.2. S2: COMPRENDER (Patterns + Context)

```yaml
Definición: Extraer patrones, correlaciones, contexto
Output: Insights ("NPS cayó 20pts, correlaciona con release buggy")
Latencia: Minutos a horas
Capacidad_IA: Alta (pattern recognition, clustering, M2-M3 Inform/Enable)

Implementación:
  Anomaly_Detection:
    IF observable Δ >2 std deviations from trend:
      → Emit(Señal: "Anomaly_Detected", observable, magnitude)
      → Dashboard: Highlight in red
  
  Correlation_Analysis:
    IF O2_Valor drops AND IN3_Cycle_Time spikes:
      → Insight: "Velocity cayó → Quality bajó → Customer sat cayó"
      → Suggest: "Investigate release X (deployed 2 weeks ago)"
  
  Cohort_Analysis:
    Segment: Customers por acquisition channel
    Pattern: "Channel A: NPS 65, Channel B: NPS 35"
    → Insight: "Channel B customers expect feature X que no tenemos"

Delegación:
  M2_Inform: IA sugiere insights, humano valida
  M3_Enable: IA genera dashboards automáticos, humano explora
  Humano: Interpreta contexto cualitativo (customer interviews, team feedback)

Output_Ejemplo:
  "H_Score cayó 62 → 58 últimas 4 semanas.
   Root cause: O2_Valor cayó 80 → 65 (NPS down).
   Correlation: IN3_Cycle_Time subió 6d → 12d (velocity dropped).
   Hypothesis: Release 2.8 introdujo bugs, customer frustration up."
```

### §4.3. S3: PROYECTAR (Forecasts + Scenarios)

```yaml
Definición: Predecir evolución futura, simular escenarios
Output: Forecasts ("Si trend continúa, H<45 en 2 meses")
Latencia: Horas a días
Capacidad_IA: Emergente (forecasting cuantitativo excelente, escenarios cualitativos requieren humano)

Implementación:
  Time_Series_Forecast:
    Model: ARIMA, Prophet, o ML (LSTM)
    Input: H_Score últimos 12 meses
    Output: "H_Score forecast: 55 (50% conf), 48-62 (80% conf) para Q4"
    → IF forecast <45: Emit(Señal: "Future_Crisis_Predicted")
  
  Scenario_Simulation:
    Scenario_1_Baseline: "Si no cambios, H → 52 en 3 meses"
    Scenario_2_Intervention: "Si hiring +10 engineers, H → 68 en 3 meses"
    Scenario_3_Crisis: "Si churn sigue, H → 38 en 3 meses (crisis)"
    → D3 usa estos escenarios para priorizar roadmap

Delegación:
  M3_Enable: IA genera forecasts + confidence intervals
  M4_Control: IA simula escenarios bounded (dentro parámetros conocidos)
  Humano: Define escenarios qualitativos (ej: "¿Qué si competitor lanza feature X?")
  
Output_Ejemplo:
  "Projection 3 meses:
   - Baseline: H_Score 58 → 52 (declining)
   - Root cause projected: O2_Valor continuará cayendo (churn rate increasing)
   - Intervention needed: O2 recovery (ver D3 para priorizar Customer Experience OKRs)
   - Risk: Si no actuar, H<45 (crisis) en 8-12 semanas"

Vinculación_D3:
  S3 provee forecasts → D3_Decision.md §3 (R1-R5 Readiness) consume para go/no-go
  S3 provee scenarios → D3 portfolio optimization (Cost of Delay analysis)
```

## §5. PATRONES SENSING

### §5.1. MVO (Mínimo Viable Observability)

```yaml
Objetivo: H_Score baseline en 2-4 semanas con 3 observables

Observables_Tier1 (Pareto 80/20):
  1. O2_Valor: Customer satisfaction (NPS/CSAT/Churn)
  2. IN2_Salud_Talento: Employee retention (turnover/engagement)
  3. IN3_Eficiencia_Flujo: Delivery speed (cycle time)

Rationale:
  - Estos 3 predicen viabilidad org mejor que cualquier otro subconjunto
  - Validado: 10 casos, correlación H_Score_Full vs H_Score_MVO >0.85

Fórmula_MVO:
  H_Score_MVO ≈ 0.70 * avg(O2, IN2, IN3) + 30
  # 30 = baseline otros observables (asumir razonable 75 * 0.30 ≈ 22.5, ajustar a 30 conservador)

Expansión_Path:
  Week 1-2: O2, IN2, IN3 → H_Score_MVO
  Week 3-8: Agregar O1, O3, IN1 (Tier 2) → H_Score representativo
  Week 9-24: Agregar O4-O8 (Tier 3) → H_Score completo
  Month 12+: Agregar SO1-SO5 (Security) → H_Score Extended

Skip_MVO_Si:
  - Ya tienes dashboards con KPIs tracked
  - Data collection automated
  - H_Score >60 (aunque no todos observables)
```

### §5.2. Drift Detection

```yaml
Pattern: Detectar degradación health antes que crisis

Regla_Core:
  IF H_Score drops >5 pts in 1 trimestre:
    → Emit(Señal: "Health_Drift_Alert", magnitude, affected_observables)
    → Investigate: ¿Qué observable(s) específicos cayeron?
    → Action: D3 debe priorizar remediation en próximo OKR cycle

Refinamiento_Por_Observable:
  IF any(O1-O8, IN1-IN3, SO1-SO5) drops >15 pts:
    → Emit(Señal: "Observable_Collapse", observable_id, severity)
    → Priority: Critical (investigate within 24h)
  
  IF O2_Valor < 30 OR O3_Capacidad < 30:
    → Emit(Señal: "Crisis_Imminent", trigger CORE/08)

Frecuencia_Check:
  - Real-time: Anomaly detection (M2)
  - Weekly: Trend analysis (M3)
  - Monthly: Executive H_Score review + drift report
```

### §5.3. Anomaly Detection (ML-Powered)

```yaml
Pattern: Detectar cambios súbitos no capturados por drift gradual

Técnica:
  - Statistical: Z-score >2σ from rolling mean
  - ML: Isolation Forest, Autoencoders (para multidimensional)
  - Seasonal: SARIMA para detectar deviaciones vs patterns esperados

Delegación:
  M4_Control: Sistema detecta anomalías, sugiere investigación
  M5_Co-produce: Sistema genera hypothesis root cause
  Humano: Valida hypothesis, ejecuta investigación cualitativa

Ejemplo:
  Observable: O2_Valor
  Baseline: NPS 65 ± 5 (stable 6 meses)
  Anomaly: NPS drop to 42 in 1 semana (Z-score = 4.6σ)
  → Emit(Señal: "Anomaly_Critical", O2, magnitude=23pts)
  → ML Hypothesis: "Correlates with Release 2.8.0 (deployed 5 days ago)"
  → Human Action: Rollback + RCA
```

## §6. ANTI-PATRONES SENSING

```yaml
AP_D2_1_Vanity_Metrics:
  Síntoma: Medir actividad, no outcomes (ej: "100 features shipped" vs "NPS +12")
  Fix: Medir O2_Valor (outcomes), no outputs
  Vinculación: Manifiesto P5 (Outcomes > Outputs)

AP_D2_2_Analysis_Paralysis:
  Síntoma: Dashboards perfectos pero sin decisiones
  Causa: D2 decide (viola ortogonalidad, eso es D3)
  Fix: D2 solo Sense → D3 Decide → D4 Act

AP_D2_3_Stale_Data:
  Síntoma: Observables actualizados cada 6 meses
  Causa: Manual collection, no automation
  Fix: ETL pipelines (M1), freshness <24h para críticos

AP_D2_4_Boiling_Frog:
  Síntoma: H_Score cae 70→50 gradual, nadie reacciona
  Causa: No drift detection
  Fix: §5.2 alerts automáticos >5pts/trimestre

AP_D2_5_Data_Without_Action:
  Síntoma: Observables tracked, pero H_Score ignorado por C-level
  Causa: No accountability D3 (OKRs no vinculados a observables)
  Fix: D3 OKRs deben referenciar explícito observables target
```

## §7. DELEGACIÓN IA SENSING (M1-M6)

```yaml
M1_Monitor (Detectar S1):
  - Sensores automated: APIs, webhooks, scrapers
  - Ejemplos: Jira API (IN3), NPS surveys (O2), HR system (IN2)
  - Delegación: 100% automatizable
  - Smartness: D2 C1-C3 (ver CORE/05)

M2_Inform (Comprender S2 básico):
  - Dashboards automated
  - Alertas threshold-based
  - Ejemplos: "O2 <30 → Alert", "H_Score weekly report"
  - Delegación: 80% automatizable (humano configura thresholds)
  - Smartness: D2 C3-C4

M3_Enable (Comprender S2 avanzado):
  - Pattern recognition (anomalies, correlations)
  - Ejemplos: "O2 drop correlates with release X"
  - Delegación: 60% automatizable (humano valida patterns)
  - Smartness: D2 C4-C5

M4_Control (Proyectar S3 básico):
  - Time series forecasts (ARIMA, Prophet)
  - Bounded scenarios ("Si hiring +10, H → 68")
  - Delegación: 50% automatizable (humano define scenarios)
  - Smartness: D2 C5

M5_Co-produce (Proyectar S3 avanzado):
  - ML forecasts complejos (LSTM, ensemble)
  - Root cause hypothesis generation
  - Delegación: 30% automatizable (humano decide acción)
  - Smartness: D2 C5-C6

M6_Execute (NO aplica D2):
  - D2 NO ejecuta acciones, solo Sense
  - Ejecución es D4 Operación
  - Mantener ortogonalidad I2
```

## §8. VALIDACIÓN DOMINIO

**Validación Formal:** Ver `CORE/07_Validacion.md` para pruebas completas de Invariantes I1-I3, Completitud y Consistencia.

**Checklist Rápido D2 (5 min):**

```yaml
✓ Ortogonalidad: D2 ∩ {D1, D3, D4} = ∅
  - D2 mide/observa, D1 diseña estructura, D3 decide, D4 ejecuta
  - Sin solapamiento: D2 provee información, otros consumen

✓ Trazabilidad: Flujo causal verificable
  - Observable → H_Score → D3 OKRs → D4 Execution → Observable (loop)
  - Ejemplo: O2↓ → H<60 → D3 prioriza CX → D4 fixes → O2↑

✓ Completitud: Observables suficientes
  - 16 observables (O1-O8, IN1-IN3, SO1-SO5) validados en 10 casos
  - MVO (O2, IN2, IN3) suficiente para 80/20 coverage

✓ Parsimonia: Elementos mínimos
  - Todos los observables necesarios (ninguno eliminable)
  - S1-S3 (Detectar, Contextualizar, Proyectar) mínimo cognitivo

✓ Alineamiento CORE:
  - A4 (Ciclo SDA) → S1-S3 es el Sense del ciclo
  - I3 (Trazabilidad) → H_Score conecta observables con decisiones
  - P6 (Probabilístico) → S3 forecasting
```

**Para revisión formal:** Aplicar pruebas de `CORE/07_Validacion.md` §2 (Ortogonalidad), §3 (Trazabilidad)

## Referencias Cruzadas

- **Ciclo SDA Sense:** `CORE/02_Ciclo_Fundamental.md` §2 (S1-S3 formal)
- **Primitivo Señal:** `CORE/01_Primitivos.md` §3A (alertas, triggers)
- **Outside-In:** `CORE/01_Primitivos.md` §7 (productos_servicios, destinatarios)
- **Security Límite L3:** `CORE/03_Arquitectura.md` §6
- **Crisis Management:** `CORE/08_Crisis_Management.md` (H<45 protocols)
- **Smartness D2:** `CORE/05_Smartness.md` matriz D2 row (C1-C6)
- **A_Score vinculado:** `D1_Arquitectura.md` §5 (IN1, IN2 componentes)
- **OKRs consumen observables:** `D3_Decision.md` §1
- **Métricas flujo:** `D4_Operacion.md` §2 (IN3 detallado, DORA)
- **Implementación práctica:** `APLICACION/A5_Medicion.md`
- **Security patterns:** `APLICACION/A1_Patrones.md` §6.5 (P_SEC01-P_SEC05)

**Fin D2_Percepcion v3.0.0**
