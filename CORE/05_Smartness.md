# 05_Smartness v2.0.0

## §0. INVARIANTE

**La inteligencia organizacional (Smartness) se estructura como matriz 4×6: 4 dominios × 6 niveles de capacidad = 24 células medibles.**

**Propiedad:** C6 (Adaptativo) es el máximo nivel alcanzable bajo Principio P8 (Herramienta no Oráculo). Sistemas C6 auto-optimizan dentro de objetivos y límites definidos por humanos, pero no definen sus propios objetivos estratégicos.

## §1. DEFINICIÓN Y ESTRUCTURA

### Concepto

**Smartness:** Capacidad de un sistema para **percibir** entorno y estado interno, **decidir** cursos de acción efectivos, y **actuar** para alcanzar objetivos de forma adaptativa y eficiente.

**No es binario:** Espectro de madurez progresivo C1→C6.

### Estructura 4×6

**4 Dominios (Filas):**

- D1 Arquitectura
- D2 Percepción  
- D3 Decisión
- D4 Operación

**6 Niveles Capacidad (Columnas):**

- C1 Manual
- C2 Documentado
- C3 Medido
- C4 Automatizado
- C5 Proactivo
- C6 Adaptativo

**Total:** 24 células de capacidad medibles

## §2. LOS 6 NIVELES DE CAPACIDAD

| Nivel | Características | Delegación | Latencia | Escalabilidad | Uso Típico |
|-------|----------------|-----------|----------|---------------|------------|
| **C1 Manual** | Procesos ad-hoc, hero-dependent, variabilidad alta | M1 (Monitor) | Alta | Nula | Startups nascentes, exploración |
| **C2 Documentado** | Procesos escritos, repetibilidad media, requiere training | M1 + Docs | Alta | Baja | Post-PMF, estructuración inicial |
| **C3 Medido** | KPIs tracked, dashboards automated, parcialmente data-driven | M1-M2 | Media | Media | Scale-ups, mejora continua emergente |
| **C4 Automatizado** | Tasks rutinarias scripteadas, humano configura | M3-M4 | Baja | Alta | Empresas maduras, DevOps culture |
| **C5 Proactivo** | Predicción problemas, prevención automated, forecasting | M4-M5 | Muy baja | Muy alta | Elite tech, ML production |
| **C6 Adaptativo** | Auto-optimización bounded, closed-loop dentro policies | M5-M6 | Mínima | Extrema | Vanguardia, IA avanzada + governance |

**Nota C7 eliminado:** Versiones anteriores incluían "C7 Soberano". Eliminado por violar **P8 (Herramienta no Oráculo)**. C6 es máximo nivel bajo gobernanza humana responsable.

## §3. MATRIZ SMARTNESS 4×6

| Dominio ↓ / Nivel → | C1 Manual | C2 Documentado | C3 Medido | C4 Automatizado | C5 Proactivo | C6 Adaptativo |
|--------------------|-----------|----------------|-----------|-----------------|--------------|---------------|
| **D1 Arquitectura** | Diseño en pizarra | Diagramas estáticos | A_Score trimestral | Code generation (scaffolding) | Drift detection arquitectónico | Refactoring autónomo supervisado |
| **D2 Percepción** | Reporte verbal | Dashboards estáticos | Alertas threshold | Log aggregation automated | Anomaly detection | Root cause analysis automático |
| **D3 Decisión** | Intuición líder | Roadmaps en PPT | Progreso OKRs tracked | Auto-prioritization backlog | Scenario simulation | Portfolio optimization dinámica |
| **D4 Operación** | Deploys manuales | Runbooks escritos | DORA metrics | CI/CD, IaC | Self-healing (restart pods) | Adaptive deployment + auto-remediation |

**Límite C6:** Todas capacidades C6 operan bajo **bounded autonomy** (M5-M6 con límites explícitos). Sistema optimiza CÓMO, humano define QUÉ y POR QUÉ.

## §4. C1: MANUAL (Ad-hoc, Hero-Dependent)

```yaml
Características_Generales:
  - Procesos no documentados (residen en cabezas)
  - Variabilidad alta (cada quien hace diferente)
  - Escalabilidad nula (pierde persona clave → colapsa)
  - Delegación: 100% humano (M1 si acaso)

Por_Dominio:
  D1_Arquitectura:
    Descripción: Diseño org pizarra, decisiones ad-hoc CEO
    Problema: Cambio persona → org desestabiliza
  
  D2_Percepción:
    Descripción: Reportes verbales, "feeling" sin datos
    Problema: Blind spots, decisiones sin evidencia
  
  D3_Decisión:
    Descripción: Intuición líder sin framework
    Problema: Inconsistente, no explicable, high-risk
  
  D4_Operación:
    Descripción: Deploys manuales, scripts personales
    Problema: Errores frecuentes, MTTR alto, no escala
```

## §5. C2: DOCUMENTADO (Definido, Repetible)

```yaml
Características_Generales:
  - Procesos escritos (wikis, runbooks, checklists)
  - Repetibilidad media (sigue docs, pero execution manual)
  - Escalabilidad baja (requiere training cada persona)
  - Delegación: Humano execution, docs M1 reference

Por_Dominio:
  D1_Arquitectura:
    Descripción: Diagramas estáticos (Lucidchart), RACI matrices
    Mejora_vs_C1: Visibility, onboarding +50% rápido
  
  D2_Percepción:
    Descripción: Dashboards estáticos, Excel reports
    Mejora_vs_C1: Métricas visibles, trends posibles
  
  D3_Decisión:
    Descripción: Roadmaps PPT, planning templates
    Mejora_vs_C1: Plan compartido, alignment visible
  
  D4_Operación:
    Descripción: Runbooks escritos, deployment checklists
    Mejora_vs_C1: Consistencia, errores -50%
```

## §6. C3: MEDIDO (KPIs Capturados)

```yaml
Características_Generales:
  - Métricas key tracked sistemáticamente
  - Dashboards automated básicos
  - Decisiones parcialmente data-driven
  - Delegación: M1 monitoring automated, M2 emerging

Por_Dominio:
  D1_Arquitectura:
    Descripción: A_Score calculado trimestral
    KPIs: Team stability, handoff ratio, span-of-control
    Mejora_vs_C2: Objectivity decisiones, data-driven
  
  D2_Percepción:
    Descripción: Alertas threshold-based (CPU >80%)
    KPIs: 11 observables tracked (O1-O8, IN1-IN3)
    Mejora_vs_C2: Real-time awareness, alertas reactivas
  
  D3_Decisión:
    Descripción: Progreso OKRs en dashboards
    KPIs: OKR achievement, decision velocity
    Mejora_vs_C2: Transparency, accountability visible
  
  D4_Operación:
    Descripción: DORA metrics (lead time, deploy freq)
    KPIs: Cycle time, throughput, WIP
    Mejora_vs_C2: Performance visible, bottlenecks identificables
```

## §7. C4: AUTOMATIZADO (Tasks Repetitivas Scripteadas)

```yaml
Características_Generales:
  - Automation tasks rutinarias (CI/CD, pipelines)
  - Humano configura, sistema ejecuta
  - Escalabilidad media (requiere infra management)
  - Delegación: M3-M4 (enable/control)

Por_Dominio:
  D1_Arquitectura:
    Descripción: Code generation (scaffolding, boilerplate)
    Ejemplo: Cookiecutter templates
    Beneficio: New service 10 min vs 2h manual
  
  D2_Percepción:
    Descripción: Log aggregation automated (ELK)
    Ejemplo: Fluentd → Elasticsearch
    Beneficio: Centralized, searchable, MTTD <5min
  
  D3_Decisión:
    Descripción: Auto-prioritization backlog (RICE, WSJF)
    Ejemplo: Script scores backlog items
    Beneficio: Objectivity, save PM 2h/week
  
  D4_Operación:
    Descripción: CI/CD pipelines, IaC
    Ejemplo: GitHub Actions: test → build → deploy
    Beneficio: Deploy frequency 10×, lead time <1h
```

## §8. C5: PROACTIVO (Anticipación, Prevención)

```yaml
Características_Generales:
  - Sistema predice problemas antes de ocurrir
  - Forecasting, anomaly detection
  - Acciones preventivas automated
  - Delegación: M4-M5 (control/co-produce)

Por_Dominio:
  D1_Arquitectura:
    Descripción: Drift detection arquitectónico
    Ejemplo: ML detecta coupling creciendo entre services
    Beneficio: Prevenir monolito distribuido antes solidificar
  
  D2_Percepción:
    Descripción: Anomaly detection (spikes, dips inusuales)
    Ejemplo: ML detecta traffic anomalía 30 min antes crash
    Beneficio: Prevenir incidents (proactive vs reactive)
  
  D3_Decisión:
    Descripción: Scenario simulation (Monte Carlo, what-if)
    Ejemplo: "If Feature A, 70% prob $1M en 6 meses"
    Beneficio: Risk-informed decisions, surprises -50%
  
  D4_Operación:
    Descripción: Self-healing (auto-restart failing pods)
    Ejemplo: K8s liveness probe failed → restart pod
    Beneficio: MTTR <1 min (vs 15 min manual)
```

## §9. C6: ADAPTATIVO (Auto-Optimización Bounded)

```yaml
Características_Generales:
  - Sistema ajusta strategy/parameters dinámicamente
  - Closed-loop optimization dentro bounds
  - Humano define objetivos y límites, sistema optimiza cómo
  - Delegación: M5-M6 (co-produce/execute), máxima autonomía bajo P8

Por_Dominio:
  D1_Arquitectura:
    Descripción: Refactoring autónomo supervisado
    Ejemplo: Bot detecta code smell → genera PR → tests pass → merge
    Límites: Solo refactorings behavior-preserving, cambios mayores requieren human ADR
    Delegación: M5 Co-produce
  
  D2_Percepción:
    Descripción: Root cause analysis automático
    Ejemplo: Incident → system correlates logs/metrics → suggests RCA
    Límites: Sugiere causas, human valida postmortem
    Delegación: M4 Control
  
  D3_Decisión:
    Descripción: Portfolio optimization dinámica
    Ejemplo: System re-prioriza backlog basado en CoD + velocity changes
    Límites: Optimiza dentro OKRs fijos (human-defined), pivots requieren human
    Delegación: M5 Co-produce
  
  D4_Operación:
    Descripción: Adaptive deployment + auto-remediation multi-dimensional
    Ejemplo:
      - Detecta latency spike región APAC
      - Reduce canary rollout 10%→5% esa región
      - Extiende monitoring 10min→20min
      - Notifica SRE (no bloquea)
      - Si metrics OK, continues rollout adapted
    Límites: Bounded autonomy policies (max rollout %, error thresholds)
    Delegación: M6 Execute (within bounds) + M4 Control (escalate exceptions)

Requisitos_Universales_C6:
  - Objetivos definidos por humanos (OKRs, policies)
  - Bounded autonomy explícita (limits, thresholds)
  - Human oversight (monitoring, circuit breakers)
  - Escalation protocols (exception handling)
  - Auditability (decision logs, explainability)
```

## §10. PATHS DE MADUREZ POR DOMINIO

### Progresión Típica

| Transición | Duración | Foco | Quick Win |
|-----------|----------|------|-----------|
| **C1→C2** | 3-6 meses | Documentación procesos críticos | Visibility, onboarding 50% más rápido |
| **C2→C3** | 6 meses | Instrumentación KPIs, dashboards | Objectivity, data-driven decisions |
| **C3→C4** | 6-12 meses | Automation tasks repetitivas | Escalabilidad horizontal, velocity 10× |
| **C4→C5** | 12 meses | ML/analytics, predictive capabilities | Proactive vs reactive, incidents -50% |
| **C5→C6** | 18+ meses | Advanced ML, adaptive systems, governance | Auto-optimization, human focuses strategy |

### D1 Arquitectura: C1→C6

```yaml
C1→C2 (6 meses):
  - Documentar org chart, RACI matrices, team charters
  Quick_Win: Clarity roles, onboarding +50%

C2→C3 (6 meses):
  - Calcular A_Score trimestral
  - Track team stability, handoff ratio
  Quick_Win: Objectivity reorg decisions

C3→C4 (12 meses):
  - Code generation templates
  - Org chart automated sync
  Quick_Win: New services 10× más rápido

C4→C5 (12 meses):
  - Architectural drift detection
  - Dependency analysis automated
  Quick_Win: Prevenir monolito distribuido

C5→C6 (18+ meses):
  - Refactoring bots
  - Self-organizing teams suggestions
  Quick_Win: Tech debt auto-remediation

Prerequisitos:
  C4: CI/CD platform, code repos structured
  C5: ML/analytics platform, metrics comprehensive
  C6: Advanced ML, XAI, governance robust
```

### D2 Percepción: C1→C6

```yaml
C1→C2 (3 meses):
  - Setup dashboards básicos
  Quick_Win: Real-time visibility

C2→C3 (6 meses):
  - H_Score mensual automated
  - Alertas threshold
  Quick_Win: H_Score tracking continuo

C3→C4 (6 meses):
  - Log aggregation (ELK)
  - Metrics collection (Prometheus)
  Quick_Win: Observability 360°

C4→C5 (12 meses):
  - Anomaly detection ML
  - Predictive alerts
  Quick_Win: Prevent incidents

C5→C6 (18+ meses):
  - Auto-RCA
  - Self-diagnosis systems
  Quick_Win: RCA 80% automated

Prerequisitos:
  C4: Data warehouse, ETL pipelines
  C5: ML platform, data scientists
  C6: MLOps mature, governance
```

### D3 Decisión: C1→C6

```yaml
C1→C2 (6 meses):
  - Documentar OKRs, roadmap en tool
  Quick_Win: Alignment visible

C2→C3 (6 meses):
  - OKR progress tracking automated
  - Decision velocity measured
  Quick_Win: Transparency, accountability

C3→C4 (12 meses):
  - Auto-prioritization backlog
  - Workflow approval automated
  Quick_Win: PM time saved 30%

C4→C5 (12 meses):
  - Monte Carlo simulations
  - What-if scenario tools
  Quick_Win: Risk-informed decisions

C5→C6 (18+ meses):
  - Dynamic portfolio rebalancing
  - Auto-adjust OKRs tactics
  Quick_Win: Portfolio siempre optimal

Prerequisitos:
  C4: PM tool, workflow automation
  C5: Analytics platform, forecasting
  C6: Advanced optimization (LP, RL)
```

### D4 Operación: C1→C6

```yaml
C1→C2 (3 meses):
  - Runbooks written
  - Checklists procesos críticos
  Quick_Win: Consistency, onboarding 2×

C2→C3 (6 meses):
  - DORA metrics tracked
  - Flow metrics tracked
  Quick_Win: Performance visibility

C3→C4 (6 meses):
  - CI/CD pipeline
  - IaC (Terraform)
  Quick_Win: Deploy frequency 10×

C4→C5 (12 meses):
  - Self-healing (K8s)
  - Auto-scaling
  Quick_Win: Uptime 99.9%+

C5→C6 (18+ meses):
  - Adaptive deployment strategies
  - Multi-dimensional auto-scaling
  Quick_Win: Velocity + safety maximized

Prerequisitos:
  C4: Cloud infra, K8s
  C5: Observability platform, ML basic
  C6: MLOps, chaos engineering, RL
```

## §11. MEDICIÓN SMARTNESS

### Smartness Score (0-100)

```yaml
Por_Dominio:
  S_D1 = Avg(C_level across D1 row)
  S_D2 = Avg(C_level across D2 row)
  S_D3 = Avg(C_level across D3 row)
  S_D4 = Avg(C_level across D4 row)

Agregado:
  Smartness_Score = (S_D1 + S_D2 + S_D3 + S_D4) / 4

Normalización (C1-C6 → 0-100):
  C1=0, C2=20, C3=40, C4=60, C5=80, C6=100

Ejemplo:
  Org con D1=C3, D2=C4, D3=C3, D4=C5
  → S_D1=40, S_D2=60, S_D3=40, S_D4=80
  → Smartness_Score = 55/100

Benchmarks:
  >70: Elite (C4-C5 avg, alta automation + proactividad)
  50-70: Mature (C3-C4 avg, medición + automation básica)
  30-50: Developing (C2-C3 avg, documentación + medición emergente)
  <30: Nascent (C1-C2 avg, ad-hoc + docs básica)

Tracking:
  - Assessment full: Anual (24 celdas)
  - Score calculation: Trimestral
  - Dashboard: Heatmap 4×6 visible C-level
```

### Integración con KERNEL

```yaml
Conexión_Delegación (M1-M6):
  C1 → M1 Monitor
  C2 → M1 + Docs
  C3 → M1-M2 (monitoring automated, alerts)
  C4 → M3-M4 (automation bounded)
  C5 → M2-M4 (prediction + automated response)
  C6 → M5-M6 (self-optimization, bounded autonomy)
  
  Principio: Mayor Smartness → Mayor delegation mode
  PERO: Siempre bounded por P8 (human meta-level control)

Conexión_Observables:
  O8_Calidad_Información:
    C1-C2: Manual, inconsistente
    C3-C4: Measured, pipelines automated
    C5-C6: Self-healing (auto-fix, auto-validate)
  
  I1_Velocidad_Decisional:
    C1-C2: Lentas (manual analysis)
    C3-C4: Data-informed (dashboards)
    C5-C6: Automated (M4-M6)
  
  I3_Eficiencia_Flujo:
    C1-C2: Manual, bottlenecks invisibles
    C3-C4: Measured, identificables
    C5-C6: Self-optimizing (auto-rebalance)

Integración_Diagnóstico (A3):
  - Agregar Smartness assessment después H_Score
  - Identifica dominios low maturity (opportunities)

Integración_Implementación (A4):
  - Maturity roadmap: "Move D4 from C3 to C4 in 6 months"
  - Initiatives priorizadas por Smartness gaps
```

## §12. ANTI-PATRONES SMARTNESS

| Anti-Pattern | Síntoma | Causa | Consecuencia | Fix |
|--------------|---------|-------|--------------|-----|
| **AP_S1: Skipping Levels** | Intentar C1→C5 sin C2-C4 | Impatience, FOMO | Fracaso implementation, investment wasted | Respect progression: C1→C2→C3→C4→C5→C6 |
| **AP_S2: Unbalanced Maturity** | 1 dominio C5-C6, otros C1-C2 | Over-investment un área | Bottleneck dominios low maturity | Balance investment: max gap 2 levels entre dominios |
| **AP_S3: Automation Without Foundation** | C4 automation sin C3 measurement | "Automate first" (backwards) | Automation ineficaz, automated wrong things | Measure BEFORE automate: C3 baseline → C4 automate → quantify improvement |

## §13. CONEXIÓN PRINCIPIOS MANIFIESTO

```yaml
P4_Flujo_Continuo:
  - C1-C2: Flow interrumpido (manual handoffs)
  - C4-C6: Flow continuous (automation removes friction)
  - Smartness habilita P4 operacionalmente

P6_Probabilístico:
  - C1-C2: Deterministic thinking
  - C3-C5: Probabilistic (forecasts con confidence intervals)
  - C5-C6 requiere probabilistic para scenario planning

P7_Parsimonia:
  - Smartness mismo es parsimonioso (6 levels, not 10)
  - 24 celdas (4×6) mínimo para completitud

P8_Herramienta_No_Oráculo:
  - C6 es máximo level (bounded autonomy)
  - C7 eliminado porque violaría P8
  - Smartness respeta human oversight siempre

Valor_Guía_Culture (Emergent):
  - Culture NO es nivel Smartness
  - Culture EMERGE de Smartness sustained
  - C5-C6 org → innovation culture (experimentation safe)
```

## §14. VALIDACIÓN

### Completitud

```
¿24 celdas (4×6) suficientes modelar inteligencia org? → SÍ
  Evidencia: 10 casos diversos modelados (R1_Casos.md)
```

### Ortogonalidad

```
¿Overlaps entre niveles? → NO
  C1-C6 progresión lineal sin saltos
  
¿Overlaps entre dominios? → NO
  D1-D4 responsabilidades únicas (ver 03_Arquitectura)
```

### Suficiencia

```
¿Se necesitan más de 6 niveles? → NO
  C6 es máximo bajo P8
  C7 violaría human oversight
  
¿Se necesitan más de 4 dominios? → NO
  D1-D4 cobertura completa (ver 03_Arquitectura §12)
```

## Referencias Cruzadas

- **Manifiesto (P8: No Oráculo):** `CORE/00_Manifiesto.md` §3
- **4 Dominios (D1-D4):** `CORE/03_Arquitectura.md`
- **Delegación (M1-M6):** `CORE/04_Delegacion.md`
- **Observables (O1-O8, IN1-IN3):** `DOMINIOS/D2_Percepcion.md`
- **A_Score (métricas arquitectura):** `CORE/03_Arquitectura.md`
- **Assessment Smartness:** `APLICACION/A3_Diagnostico.md` (to be integrated)
- **Implementation roadmap:** `APLICACION/A4_Implementacion.md`
- **KPIs Smartness:** `APLICACION/A5_Medicion.md` (to be added)
- **Casos aplicados:** `REFERENCIA/R1_Casos.md`

**Fin 05_Smartness v2.0.0**
