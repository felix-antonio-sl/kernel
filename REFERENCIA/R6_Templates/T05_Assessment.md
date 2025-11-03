# T05: Assessment Interview Guide

**Versión:** 2.2.1  
**Última Actualización:** 2025-11-03  
**Compatibilidad:** KERNEL v2.2.x

**Propósito:** Guía estructurada entrevistas diagnóstico organizacional (Fase 0)  
**Duración:** 60-90 min por stakeholder  
**Audiencia:** C-Suite, VPs, Team Leads, IC contributors

---

## ⚠️ PREREQUISITOS

**Nivel Madurez Mínimo:**
- ✅ **Sponsor ejecutivo comprometido** (C-level con mandate y budget)
- ✅ **Acceso a stakeholders clave** (al menos 8-12 entrevistas cross-functional)
- ✅ **Tiempo disponible** (4-6 semanas para diagnóstico completo)
- ✅ **Apertura a cambio** (org dispuesta a actuar sobre findings)

**Señales de Alerta - NO USAR si:**
- 🚫 **Crisis activa** → Ir directo a `A4_Implementacion.md` §0 Path 1-2 (estabilización)
- 🚫 **No hay sponsor real** → Assessment será ignorado, waste of time
- 🚫 **Resistencia cultural alta** → Hacer readiness building primero (3-6 meses)
- 🚫 **Org <20 personas** → Assessment too heavy, usar diagnóstico simplificado

**Si Dudas:**
- Ver `A4_Implementacion.md` §0 para determinar path correcto (crisis vs transformation)
- Ver `A1_Patrones.md` §9 P35 Preparación R1-R5 para score readiness
- Considerar assessment MVP (solo 4-5 entrevistas, 2 semanas) si recursos limitados

---

## BLOQUE 0: PRE-ASSESSMENT TRIAGE - 10 min

**⚠️ CRITICAL: Completar ANTES de diagnóstico detallado para evitar AP33 (Transforming During Crisis)**

### P0.1 Crisis Indicators Check

> "¿La organización enfrenta actualmente crisis financiera, de clientes o de talento?"

**Buscar señales críticas:**

🚩 **Financial Crisis:**
- Cash runway < 90 días
- Burn rate acelerado (>20% MoM)
- Payroll at risk próximos 2 meses
- Credit lines agotadas

🚩 **Customer/Citizen Crisis:**
- Churn rate > 20% annually
- NPS < 0 (más detractors que promoters)
- Key account losses (top 20% revenue)
- Service delivery failures > 20% (sector público)

🚩 **Talent Crisis:**
- Voluntary attrition > 25% annually
- High-performer exodus > 20%
- Leadership team departures (3+ in last quarter)
- eNPS < -10

**Decision Tree:**

```yaml
IF ANY crisis indicator present:
  Path: EMERGENCY STABILIZATION (A4 §0 Path 1-2)
  Action:
    1. STOP transformation assessment
    2. Activate P52 (Crisis Governance Pattern)
    3. Focus: Week 1-4 stabilization
    4. Re-assess H_Score Week 5
  Next_Step: Skip to crisis stabilization protocol
  
ELSE IF No crisis indicators:
  Path: STANDARD ASSESSMENT
  Action: Proceed to P0.2 Readiness Assessment
```

---

### P0.2 Change Readiness Assessment (if no crisis)

> "Evalúe 5 dimensiones de readiness para transformación (escala 1-5)"

**Dimensiones:**

1. **Leadership Alignment:** ¿Executive team unificado sobre necesidad y approach?
   - 5: 100% alineados, total buy-in
   - 3: Mayoría support, algunos skeptics
   - 1: Fragmentados, no consensus

2. **Urgency Level:** ¿Existe caso compelling para cambiar AHORA?
   - 5: Burning platform claro OR opportunity window cerrando
   - 3: Change deseable pero no urgente
   - 1: Status quo aceptable

3. **Resource Availability:** ¿Tiempo, dinero, personas disponibles?
   - 5: Resources totalmente allocated
   - 3: Resources disponibles pero constrained
   - 1: Zero capacity, org at limit

4. **Capability:** ¿Skills para diseñar/implementar?
   - 5: Expertise in-house OR budget consultants
   - 3: Some skills, need upskilling
   - 1: No capability, no budget

5. **Organizational Bandwidth:** ¿Capacidad absorber change?
   - 5: Utilization <80%, can absorb change
   - 3: Utilization 80-90%, tight but manageable
   - 1: Utilization >95%, overloaded

**Scoring & Decision:**

```yaml
Total_Score: [Sum of 5 dimensions] / 5 = [Average]

IF ALL dimensions >= 4:
  Recommendation: PROCEED full transformation
  Approach: A4 §1-§6 playbook standard
  Timeline: 12-18 months

ELSE IF MOST dimensions >= 3:
  Recommendation: PROCEED pilot/phased
  Approach: Start 1-2 teams, 3-month pilot
  Timeline: 6 months pilot, then re-assess

ELSE IF ANY dimension < 3:
  Recommendation: BUILD READINESS first
  Action: Address gaps (workshops, capacity, hiring)
  Re-assess: 3-6 months
  Risk: 70% failure if force now (AP32)

ELSE IF ANY dimension = 1:
  Recommendation: DELAY transformation
  Action: Prerequisites work only
  Timeline: 6-12 months readiness building
```

---

### P0.3 Building Blocks Completeness Check

> "¿La organización tiene las 5 funciones organizacionales críticas?"

**Checklist (D1 §4 Building Blocks):**

☐ **BB1 - Engineers (Innovadores):**  
   ¿Quién diseña productos/servicios nuevos? ¿Capacity innovation?
   - ✅ Presente: Dedicated eng teams, R&D capacity
   - ⚠️ Débil: Solo maintenance, zero innovation
   - ❌ Ausente: No engineering, todo outsourced

☐ **BB2 - Service Providers (Operadores):**  
   ¿Quién opera sistemas day-to-day? ¿Service delivery?
   - ✅ Presente: Ops teams, SRE, service desk
   - ⚠️ Débil: Reactive only, firefighting
   - ❌ Ausente: No operations capability

☐ **BB3 - Coordinators (Facilitadores):**  
   ¿Quién coordina standards, governance cross-org?
   - ✅ Presente: Architecture, PMO, standards bodies
   - ⚠️ Débil: Informal coordination only
   - ❌ Ausente: Zero coordination, silos totales

☐ **BB4 - Sales/Stakeholder Engagement:**  
   ¿Quién construye relationships, descubre opportunities?
   - Private: Sales, marketing, business development
   - Public: Stakeholder engagement, citizen services
   - ✅ Presente: Dedicated function
   - ⚠️ Débil: Reactive only
   - ❌ Ausente: Disconnect from customers/stakeholders

☐ **BB5 - Audit (Aseguradores):**  
   ¿Oversight independent, compliance, risk?
   - ✅ Presente: Internal audit, compliance team
   - ⚠️ Débil: Compliance-only, no proactive
   - ❌ Ausente: No controls, compliance failures

**Gap Analysis:**

```yaml
Missing_BB → Structural gap diagnosis in D1 Arquitectura

Common_Gaps:
  - Startup sin BB5 (Audit): Común early-stage, acceptable si <50 personas
  - Public sector sin BB4 formal: Stakeholder engagement diluido en silos
  - Scale-up sin BB3: Coordination chaos, cada team su standard
```

---

## BLOQUE 1: ARQUITECTURA (D1) - 15 min

### P1.1 Estructura Organizacional
> "Describe cómo están organizados los equipos. ¿Cuántos equipos? ¿Qué tamaño? ¿Qué poseen?"

**Buscar:**
- ✅ Teams 5-8 personas, cross-funcionales, ownership producto/servicio
- ⚠️ Teams >12 personas, especializados por función, ownership ambiguo
- 🚩 Silos departamentales, handoffs múltiples, ownership nulo

**Scoring:**
- 80-100: Team Topologies aplicado, Conway's Law respetado
- 50-79: Estructura razonable, algunos silos
- 0-49: Silos críticos, AP05 violación Conway

### P1.2 Deuda Técnica
> "¿Cómo medirían la salud técnica del sistema? ¿Qué % código es legacy sin tests?"

**Buscar:**
- ✅ Λ<15%, tests coverage >80%, refactoring continuo
- ⚠️ Λ=15-35%, tests 50-80%, refactoring ocasional
- 🚩 Λ>35%, tests <50%, "don't touch, it works"

**Scoring:**
- 80-100: Tech debt gestionado, Λ<15%
- 50-79: Tech debt moderado, Λ=15-35%
- 0-49: Tech debt crítico, Λ>35%

### P1.3 Dependencies
> "¿Cuántos otros equipos debe coordinar su equipo para entregar una feature?"

**Buscar:**
- ✅ 0-1 dependencias, equipos autónomos
- ⚠️ 2-3 dependencias, coordinación manejable
- 🚩 >3 dependencias, coordinación constante

---

## BLOQUE 2: PERCEPCIÓN (D2) - 15 min

### P2.1 Observabilidad
> "¿Cómo saben que el sistema está sano? ¿Qué dashboards existen? ¿Quién los usa?"

**Buscar:**
- ✅ Dashboards tiempo real, alertas proactivas, SLOs definidos
- ⚠️ Logs centralizados, alertas básicas, revisión manual
- 🚩 Logs dispersos, alertas reactivas, "users report bugs"

### P2.2 Datos de Negocio
> "¿Cómo miden satisfacción cliente? ¿Frecuencia? ¿Accionabilidad?"

**Buscar:**
- ✅ NPS/CSAT continuo, analytics real-time, decisiones data-driven
- ⚠️ Surveys trimestrales, analytics batch, intuición + datos
- 🚩 Sin medición sistemática, decisiones basadas en anecdotes

### P2.3 Flujo Trabajo
> "¿Dónde están los cuellos de botella? ¿Cómo lo saben?"

**Buscar:**
- ✅ WIP limits, cycle time tracked, bottlenecks identificados/resueltos
- ⚠️ Tracking manual, bottlenecks conocidos pero no resueltos
- 🚩 Sin visibilidad WIP, "siempre estamos ocupados"

---

## BLOQUE 2.5: AWARENESS & AUTOMATION MATURITY - 15 min

**⚡ Nuevo en v1.3:** Evaluar madurez en niveles awareness (S1-S3) y automation (D1-D4)

### P2.5.1 Awareness Levels Evaluation (S1-S3)

> "Evalúe capacidad organizacional para percibir, comprender y proyectar estado del sistema"

**S1 - DETECT (Percibir):**

```yaml
Checklist:
  ☐ ¿Dashboards con métricas básicas disponibles 24/7?
  ☐ ☐ ¿Alerting automated para eventos críticos?
  ☐ ¿Telemetry real-time o near-real-time (<1 min)?
  ☐ ¿Logs aggregated y searchable (últimos 30 días)?
  ☐ ¿Monitoring coverage >90% systems críticos?

Scoring (1-5):
  5: Full coverage, real-time, automated
  3: Partial coverage, gaps en monitoring
  1: Manual tracking, dashboards stale

Score_S1: [___] / 5
```

**S2 - COMPREHEND (Comprender):**

```yaml
Checklist:
  ☐ ¿H_Score u otra métrica composite calculada automáticamente?
  ☐ ¿Alerting context-aware (no solo raw thresholds)?
  ☐ ¿Observables O1-O8, IN1-IN3 tracked y visibles?
  ☐ ¿Pattern recognition automated (anomaly detection)?
  ☐ ¿Alert quality >80% (actionable, no noise)?

Scoring (1-5):
  5: H_Score automated, intelligent alerting, pattern detection
  3: Some synthesis, alerts basic pero functional
  1: Solo raw metrics, mucho noise en alerts

Score_S2: [___] / 5
```

**S3 - PROJECT (Proyectar):**

```yaml
Checklist:
  ☐ ¿Forecasting trends implemented? (revenue, churn, capacity)
  ☐ ¿Crisis thresholds monitoreados con alerts? (H_Score<45)
  ☐ ¿Scenario planning tools available? (Monte Carlo, what-if)
  ☐ ¿Predictive models en production? (≥3 models)
  ☐ ¿Forecast accuracy <15% MAPE?

Scoring (1-5):
  5: Multiple forecasts, scenario planning, high accuracy
  3: Basic forecasting, emergent predictive capability
  1: No prediction, purely reactive

Score_S3: [___] / 5
```

**Awareness_Maturity_Overall:**
```
Score = (S1 × 20) + (S2 × 20) + (S3 × 20) = [___] / 100

Interpretación:
  >80: Excelente - Full spectrum awareness
  60-80: Bueno - S1+S2 strong, S3 developing
  40-60: Atención - Solo S1, gaps significativos
  <40: Crítico - Awareness básica insuficiente
```

---

### P2.5.2 Decision Automation Evaluation (D1-D4)

> "Evalúe qué decisiones están automated vs requieren humanos"

**D1 - DIRECT FEEDBACK (Automática):**

```yaml
Question: "Liste 5-10 decisiones que ocurren automáticamente sin intervención humana"

Ejemplos_Esperados:
  - Autoscaling (CPU>80% → add instances)
  - Circuit breakers (error rate>10% → open circuit)
  - Auto-remediation (pod crash → restart)
  - Fraud rules básicas (amount>$10K → flag)

Count_D1: [___] decisiones automated

Automation_D1_Rate:
  = Count_D1 / Total_D1_Opportunities
  Estimate: [___]% (target >60%)
```

**D2 - RULE-BASED (Condicional):**

```yaml
Question: "¿Qué business rules están documentadas? ¿Automated?"

Checklist:
  ☐ Approval workflows documented (>$X require VP)
  ☐ Compliance rules automated (GDPR, SOX)
  ☐ Quality gates CI/CD (coverage>80%, security scan)
  ☐ Triage rules (severity → priority mapping)
  ☐ Rules engine deployed (Drools, decision tables)

Rules_Coverage:
  = # rules_documented / # critical_decision_types
  Estimate: [___]% (target >90%)

Rules_Automation:
  = # rules_automated / # rules_documented
  Estimate: [___]% (target >75%)
```

**D3 - ASSOCIATIVE (ML-based):**

```yaml
Question: "¿Qué ML models están en producción sirviendo decisiones?"

List_Models:
  1. [Model name] - [Decision served] - [Accuracy]
  2. ...
  3. ...

Count_D3: [___] ML models in production (target 5-10)

Human_Validation_Rate:
  ¿Qué % decisiones D3 validated by human?
  Estimate: [___]% (target >90% si high-risk)

Model_Monitoring:
  ☐ Drift detection active?
  ☐ Accuracy tracking automated?
  ☐ Explainability available (SHAP, LIME)?
```

**D4 - KNOWLEDGE-BASED (Analítica):**

```yaml
Question: "¿Cuánto tardan decisiones estratégicas/tácticas?"

Decision_Latency:
  - Strategic (portfolio, roadmap): [___] días (target <7d)
  - Tactical (feature prioritization): [___] horas (target <24h)

Simulation_Tools:
  ☐ Monte Carlo simulation available?
  ☐ Scenario planning structured process?
  ☐ What-if analysis tools deployed?

OKR_Structure:
  ☐ Strategic decisions linked to OKRs?
  Estimate: [___]% decisions con OKR linkage (target >80%)
```

**Decision_Automation_Overall:**
```
Automation_Rate = % decisiones repeatables que están automated

Estimate: [___]% (based on D1-D3 counts above)

Benchmark:
  >50%: Excelente - Alta automation apropiada
  30-50%: Bueno - Balance automation/human
  15-30%: Atención - Underautomated, opportunities
  <15%: Crítico - Manual decision overload
```

---

## BLOQUE 3: DECISIÓN (D3) - 20 min

### P3.1 Planning
> "Describan su proceso planificación. ¿Freuencia? ¿Quién participa? ¿Cómo priorizan?"

**Buscar:**
- ✅ OKRs trimestrales, bottom-up + top-down, value-driven prioritization
- ⚠️ Planning semestral, top-down, priorización mixta
- 🚩 Planning anual, cascada, "todo es prioridad 1"

### P3.2 Adaptabilidad
> "¿Qué pasa si aparece oportunidad urgente mid-quarter? ¿Pueden pivotar?"

**Buscar:**
- ✅ 30% capacidad emergente, re-planificación 2 semanas
- ⚠️ 10-20% buffer, re-planificación mensual
- 🚩 0% buffer, "committed for the year"

### P3.3 Alignment
> "¿Todos entienden el 'por qué' de su trabajo? ¿Conexión con objetivos empresa?"

**Buscar:**
- ✅ Transparencia completa OKRs, todos explican why
- ⚠️ OKRs compartidos, entendimiento variable
- 🚩 "Work comes from backlog, don't ask why"

---

## BLOQUE 4: OPERACIÓN (D4) - 20 min

### P4.1 Velocity
> "¿Cuánto tardan features typical de concebir a producción?"

**Buscar:**
- ✅ Lead time <2 semanas, velocity estable/creciente
- ⚠️ Lead time 2-8 semanas, velocity errática
- 🚩 Lead time >8 semanas, velocity decreciente

### P4.2 Quality
> "¿Cuántos incidents producción/mes? ¿MTTR?"

**Buscar:**
- ✅ <2 incidents/mes, MTTR <1hr
- ⚠️ 2-5 incidents/mes, MTTR 1-4hrs
- 🚩 >5 incidents/mes, MTTR >4hrs

### P4.3 Morale
> "En escala 1-10, ¿qué tan satisfecho está el equipo? ¿Por qué?"

**Buscar:**
- ✅ 8-10: Energía alta, ownership, aprendizaje
- ⚠️ 5-7: Neutral, algunas frustraciones
- 🚩 1-4: Burnout, síntomas turnover

---

## BLOQUE 5: IA & AUTOMATIZACIÓN - 10 min

### P5.1 Nivel Madurez IA
> "¿Qué procesos tienen automatización IA? ¿Agentes digitales en equipos?"

**Buscar:**
- ✅ Agentes M4-M6, automatización 30%+ tareas, MLOps maduro
- ⚠️ Pilots IA, automatización 10-30%, MLOps incipiente
- 🚩 Sin IA, automatización <10%, scripts manuales

### P5.2 Delegación Humano-IA
> "¿Cómo deciden qué delegar a agentes IA vs humanos?"

**Buscar:**
- ✅ Matriz delegación definida, evaluación sistemaática
- ⚠️ Ad-hoc, basado en disponibilidad
- 🚩 "No usamos IA" o "IA hace todo"

---

## CÁLCULO H_SCORE

```python
# Scoring por dominio (0-100)
D1_Arquitectura = (P1.1 + P1.2 + P1.3) / 3
D2_Percepcion = (P2.1 + P2.2 + P2.3) / 3
D3_Decision = (P3.1 + P3.2 + P3.3) / 3
D4_Operacion = (P4.1 + P4.2 + P4.3) / 3

# H_Score total (promedio ponderado)
H_Score = (
    D1_Arquitectura * 0.30 +  # Más peso: fundación
    D2_Percepcion * 0.20 +
    D3_Decision * 0.25 +
    D4_Operacion * 0.25
)

# Interpretación
if H_Score >= 75:
    nivel = "EXCELENTE - Optimización continua"
elif H_Score >= 60:
    nivel = "BUENO - Mejora incremental"
elif H_Score >= 45:
    nivel = "ACEPTABLE - Transformación viable"
else:
    nivel = "CRÍTICO - Estabilización urgente"
```

---

## NOTAS PARA INTERVIEWER

1. **Triangular datos:** Entrevistar 3-5 personas por dominio (C-level, middle mgmt, ICs)
2. **Buscar evidencia:** No aceptar claims sin métricas/ejemplos
3. **Detectar deseabilidad social:** Preguntar "cómo", no "si hacen X"
4. **Observar lenguaje:** "We should..." vs "We do..." indica gaps
5. **Capturar quotes:** Usar verbatims en reporte final

---

**Output esperado:** Report 5-10 páginas con H_Score, breakdown por dominio, top 5 hallazgos críticos, roadmap sugerido.