# T23_Customer_Journey_Map (KERNEL-Native)

**Versión:** 2.2.1  
**Última Actualización:** 2025-11-03  
**Compatibilidad:** KERNEL v2.2.x  
**Audiencia:** Product Managers, UX, Customer Success, Engineering  
**Patterns Aplicables:** P_CX01 (Flujo Valor Cliente), P_CX02 (Eventos Señales CX), P_CX03 (Touchpoint Ownership)

---

## ⚠️ PREREQUISITOS

**Capacidades Técnicas Requeridas:**
- ✅ **Instrumentación básica** (analytics web/app, event tracking)
- ✅ **Observable O2 tracked** (NPS, CSAT, o equivalente medido actualmente)
- ✅ **Ownership claro touchpoints** (al menos RACI draft existe)
- ✅ **Data infrastructure** (warehouse, dashboards, o capacidad implementar en 3-6 meses)

**Nivel Madurez Mínimo:**
- ✅ **D2 Percepción ≥50** (observables básicos funcionando)
- ✅ **Product-market fit alcanzado** (no pre-PMF startups)
- ✅ **Customer base >100 activos** (statistically significant)

**Señales de Alerta - NO USAR si:**
- 🚫 **No tracking actual** → Implementar analytics básico primero (3-6 meses)
- 🚫 **Pre-PMF startup** → Usar journey map tradicional (qualitative), demasiado early para instrumentación
- 🚫 **No data team/capability** → Journey será insights sin acción, build capability primero
- 🚫 **Customer base <50** → Sample size insuficiente, grow primero
- 🚫 **Crisis churn** → Firefighting mode, no es momento para journey mapping estratégico

**MVP Alternativo (si no cumples full prerequisites):**
1. **Fase 1 (Manual):** Journey map cualitativo tradicional (workshops, sticky notes)
2. **Fase 2 (Hybrid):** Instrumentar 2-3 touchpoints críticos solamente
3. **Fase 3 (Full KERNEL):** Expandir a journey completo instrumentado

**Timing Óptimo:**
- Post-PMF, pre-scale (50-500 customers)
- Cuando O2 (NPS/CSAT) ya se mide (aunque sea manualmente)
- Budget disponible para tooling ($10K-50K típico)

**Si Dudas:**
- Empezar con journey map tradicional, migrar a KERNEL cuando maduro
- Ver `A1_Patrones.md` §6.6 P_CX01-03 para entender patterns primero
- Considerar contratar CX expert si team no tiene experiencia journey mapping

---

## Propósito Template

**KERNEL Customer Journey Map** traduce journey tradicional (visual, empathy-driven) a **instrumentación ejecutable** usando primitivos KERNEL:

- **Flujos F**: Customer journey como flujo valor end-to-end
- **Observables O2**: NPS/CSAT instrumentado por touchpoint
- **Señales S**: Friction points como alertas automáticas
- **Actores A**: Ownership explícito touchpoints (RACI)

**Diferencia vs Journey Map tradicional**:
- ✅ KERNEL: Operacionalizable (metrics, alerts, ownership)
- ❌ Tradicional: Insights cualitativos (workshops, sticky notes)

---

## PASO 1: Identificar Flujo Valor Cliente (F1)

### Definir Trigger & Outcome

```yaml
Customer_Job_To_Be_Done:
  Trigger: [¿Qué evento inicia el journey?]
    Ejemplo: "Usuario busca producto X en Google"
  
  Outcome_Deseado: [¿Qué valor busca cliente?]
    Ejemplo: "Comprar producto X con confianza (quality assurance, precio competitivo)"
  
  Success_Criteria: [¿Cómo medir outcome alcanzado?]
    Ejemplo: "Compra completada + NPS >7 post-compra"
```

**Tu Implementación**:
```yaml
Trigger: _________________________________
Outcome_Deseado: _________________________________
Success_Criteria: _________________________________
```

---

## PASO 2: Mapear Touchpoints (Flujo F End-to-End)

### Estructura Flujo Cliente

**Touchpoint** = Interacción cliente ↔ organización (digital, humano, físico).

**Formato KERNEL**:
```yaml
Touchpoint_ID: [T1, T2, T3...]
Descripción: [¿Qué hace cliente aquí?]
Recursos_R: [¿Qué recursos usa? Website, app, call center]
Actores_A: [¿Quiénes intervienen? Customer, CSR, chatbot]
Duración_Avg: [Tiempo típico en este touchpoint]
Friction_Típica: [¿Qué puede fallar/frustrar?]
```

### Ejemplo: E-commerce Purchase Journey

```yaml
T1_Discover:
  Descripción: Usuario busca producto Google, llega a website
  Recursos_R: SEO, Google Ads, Website homepage
  Actores_A: A1_Customer (busca), A3_Google (search engine)
  Duración_Avg: 2-5 minutos
  Friction_Típica: Website slow (>3 sec load), no aparece en resultados

T2_Explore:
  Descripción: Usuario navega catálogo, compara productos
  Recursos_R: Product catalog, filters, recommendations AI
  Actores_A: A1_Customer (explora), A3_Recommendation_Engine (sugiere)
  Duración_Avg: 10-15 minutos
  Friction_Típica: Filters confusos, no encuentra product fit

T3_Decide:
  Descripción: Usuario lee reviews, specs técnicas, agrega a cart
  Recursos_R: Product details page, reviews, cart
  Actores_A: A1_Customer (evalúa)
  Duración_Avg: 5-10 minutos
  Friction_Típica: Reviews negativas (>30%), out of stock

T4_Purchase:
  Descripción: Usuario completa checkout (payment, shipping)
  Recursos_R: Checkout flow, payment gateway, shipping calculator
  Actores_A: A1_Customer (paga), A3_Payment_Processor
  Duración_Avg: 3-5 minutos
  Friction_Típica: Payment fails, shipping cost surprise

T5_Receive:
  Descripción: Usuario recibe producto, inspecciona calidad
  Recursos_R: Logistics (shipping), product packaging
  Actores_A: A1_Customer (recibe), A2_Courier (entrega)
  Duración_Avg: 2-5 días
  Friction_Típica: Delivery delayed, producto damaged

T6_Support:
  Descripción: Usuario contacta soporte si issue (returns, questions)
  Recursos_R: Support portal, chatbot, call center
  Actores_A: A1_Customer (reporta), A2_CSR (resuelve), A3_Chatbot
  Duración_Avg: 10-30 minutos
  Friction_Típica: Wait time >10 min, no resolution
```

**Tu Journey Map** (completar tabla):

| Touchpoint ID | Descripción | Recursos R | Actores A | Duración Avg | Friction Típica |
|---------------|-------------|------------|-----------|--------------|-----------------|
| T1 | | | | | |
| T2 | | | | | |
| T3 | | | | | |
| T4 | | | | | |
| T5 | | | | | |

---

## PASO 3: Instrumentar Observables O2 (Valor por Touchpoint)

### Definir Métricas O2 por Touchpoint

**Observable O2 (Valor)**: NPS, CSAT, conversion rate, abandonment rate, time-to-value.

**Formato**:
```yaml
Touchpoint: [T1, T2, etc.]
Observable_O2: [Métrica específica]
Target: [Threshold objetivo]
Alerting_Rule: [IF métrica < threshold THEN Señal S]
```

### Ejemplo: E-commerce Observables

```yaml
T1_Discover:
  O2_Metric: Bounce rate (% usuarios leave sin navegar)
  Target: <40%
  Alerting: IF bounce_rate >50% THEN S_High_Bounce_Alert

T2_Explore:
  O2_Metric: Product views per session
  Target: >3 productos vistos
  Alerting: IF avg_views <2 THEN S_Low_Engagement

T3_Decide:
  O2_Metric: Add-to-cart rate (% que agregan cart)
  Target: >15%
  Alerting: IF add_to_cart <10% THEN S_Low_Conversion

T4_Purchase:
  O2_Metric: Checkout completion rate
  Target: >70%
  Alerting: IF completion <60% THEN S_Cart_Abandonment

T5_Receive:
  O2_Metric: On-time delivery rate
  Target: >95%
  Alerting: IF on_time <90% THEN S_Logistics_Issue

T6_Support:
  O2_Metric: CSAT support
  Target: >80%
  Alerting: IF CSAT <70% THEN S_Support_Quality_Drop
```

**Tu Instrumentación O2**:

| Touchpoint | Observable O2 | Target | Alerting Rule |
|------------|---------------|--------|---------------|
| T1 | | | |
| T2 | | | |
| T3 | | | |
| T4 | | | |
| T5 | | | |

---

## PASO 4: Identificar Señales S (Friction Alerts)

### Convertir Friction → Señal S

**Señal S** = Evento detectable que indica problema customer experience.

**Formato**:
```yaml
Señal_ID: [S1, S2...]
Touchpoint: [Dónde ocurre]
Trigger: [¿Qué evento dispara señal?]
Severity: [High/Medium/Low]
Action: [¿Qué hacer cuando señal activa?]
Owner_A2: [¿Quién responsible responder?]
```

### Ejemplo: E-commerce Friction Signals

```yaml
S1_High_Bounce:
  Touchpoint: T1_Discover
  Trigger: Bounce rate >50% last 24hrs
  Severity: High
  Action: Urgent review landing page (SEO team)
  Owner: A2_SEO_Lead

S2_Cart_Abandonment:
  Touchpoint: T4_Purchase
  Trigger: Checkout completion <60% last 7 días
  Severity: High
  Action: Analyze checkout flow (UX + Eng)
  Owner: A2_Product_Manager

S3_Logistics_Issue:
  Touchpoint: T5_Receive
  Trigger: On-time delivery <90% last 30 días
  Severity: Medium
  Action: Escalate to logistics partner
  Owner: A2_Operations_Manager

S4_Support_Overload:
  Touchpoint: T6_Support
  Trigger: Support tickets >100/día
  Severity: Medium
  Action: Scale support capacity (hire, chatbot)
  Owner: A2_Customer_Success_Lead
```

**Tus Señales S**:

| Señal ID | Touchpoint | Trigger | Severity | Action | Owner A2 |
|----------|------------|---------|----------|--------|----------|
| S1 | | | | | |
| S2 | | | | | |
| S3 | | | | | |

---

## PASO 5: Asignar Ownership RACI por Touchpoint

### RACI Matrix Touchpoints

**Purpose**: Clarificar quién responsible customer experience cada touchpoint (evitar "nadie es responsible").

**Formato**:
```yaml
Touchpoint: [T1, T2...]
Responsible: [Owner primario touchpoint, accountable O2 metric]
Accountable: [Exec sponsor, escalation point]
Consulted: [Teams input decisions touchpoint]
Informed: [Stakeholders notificados cambios]
```

### Ejemplo: E-commerce RACI

```yaml
T1_Discover:
  Responsible: A2_SEO_Lead (owns bounce rate, landing page quality)
  Accountable: A2_VP_Marketing (budget SEO, strategy)
  Consulted: A2_UX_Designer (landing page design), A2_Data_Analyst (metrics)
  Informed: A2_CEO (if crisis: bounce >70%)

T2_Explore:
  Responsible: A2_Product_Manager (owns catalog experience, filters)
  Accountable: A2_VP_Product
  Consulted: A2_Eng_Lead (catalog infrastructure), A2_UX_Designer
  Informed: A2_CEO

T3_Decide:
  Responsible: A2_Product_Manager (owns product details, reviews)
  Accountable: A2_VP_Product
  Consulted: A2_Eng_Lead, A2_Customer_Success (reviews quality)
  Informed: A2_CEO

T4_Purchase:
  Responsible: A2_Eng_Lead (owns checkout flow technical reliability)
  Accountable: A2_CTO
  Consulted: A2_Product_Manager (UX checkout), A2_Finance (payment gateway)
  Informed: A2_CEO

T5_Receive:
  Responsible: A2_Operations_Manager (owns logistics, delivery quality)
  Accountable: A2_COO
  Consulted: A2_Logistics_Partner (external), A2_Customer_Success
  Informed: A2_CEO

T6_Support:
  Responsible: A2_Customer_Success_Lead (owns CSAT support)
  Accountable: A2_VP_Customer_Success
  Consulted: A2_Eng_Lead (technical issues), A2_Product_Manager (product issues)
  Informed: A2_CEO
```

**Tu RACI Matrix**:

| Touchpoint | Responsible | Accountable | Consulted | Informed |
|------------|-------------|-------------|-----------|----------|
| T1 | | | | |
| T2 | | | | |
| T3 | | | | |
| T4 | | | | |
| T5 | | | | |

---

## PASO 6: Construir Dashboard O2 (Customer Experience Health)

### Dashboard Metrics

**Purpose**: Visualizar health customer experience en tiempo real (similar H_Score pero para journey).

**Fórmula CX_Score** (0-100):
```yaml
CX_Score = weighted_avg(O2_T1, O2_T2, O2_T3, O2_T4, O2_T5, O2_T6)

Pesos_Sugeridos:
  T1_Discover: 10% (acquisition critical pero no loyalty)
  T2_Explore: 15% (product discovery key)
  T3_Decide: 20% (conversion moment crítico)
  T4_Purchase: 25% (transaction success esencial)
  T5_Receive: 20% (post-purchase experience)
  T6_Support: 10% (minority users contact support)

Nota: Ajustar pesos según negocio (B2C vs B2B, product type)
```

**Interpretación CX_Score**:
```yaml
90-100: Excellent CX (NPS >50, churn <5%)
75-89: Good CX (NPS 30-50, churn 5-10%)
60-74: Acceptable CX (NPS 10-30, churn 10-15%)
45-59: Poor CX (NPS <10, churn >15%)
<45: Crisis CX (NPS negative, churn >25%, emergency patterns)
```

### Dashboard Example (Datadog, Grafana, Tableau)

```yaml
Panel_1_CX_Score:
  Metric: CX_Score 0-100
  Visualization: Gauge
  Update: Real-time (5 min refresh)
  Threshold_Colors: Red <60, Yellow 60-75, Green >75

Panel_2_Touchpoint_O2:
  Metrics: O2_T1, O2_T2, O2_T3, O2_T4, O2_T5, O2_T6
  Visualization: Bar chart
  Target_Lines: Show target per touchpoint
  Update: Daily

Panel_3_Friction_Signals:
  Metrics: Active S1, S2, S3, S4 (count alerts)
  Visualization: Alert list (sortable by severity)
  Actions: Link to owner A2, incident ticket
  Update: Real-time

Panel_4_Trends:
  Metrics: CX_Score last 30 días (time series)
  Visualization: Line chart
  Annotations: Major changes (product launches, incidents)
  Update: Daily
```

**Tu Dashboard Config** (tool-agnostic spec):
```yaml
Dashboard_Name: [Customer Experience Health - {Product}]
Panels:
  - CX_Score_Gauge: [Config...]
  - Touchpoint_Metrics: [Config...]
  - Friction_Signals: [Config...]
  - Trends: [Config...]
Update_Frequency: [Real-time / Hourly / Daily]
Access: [Teams con acceso dashboard]
```

---

## PASO 7: Implementar Mejoras (Iterative)

### Priorización Friction Fixes

**Criterios**:
1. **Impact**: ¿Cuántos customers afecta? (volume touchpoint)
2. **Severity**: ¿Qué tan crítico? (S High vs Low)
3. **Effort**: ¿Cuánto cuesta fix? (Eng days, $)

**Framework Priorización** (RICE adaptado CX):
```yaml
Priority_Score = (Impact × Severity) / Effort

Impact: # customers affected/mes (scale 1-10)
Severity: High=10, Medium=5, Low=1
Effort: Eng days (scale 1-10, inverse: 1=mucho, 10=poco)
```

### Ejemplo Priorización

```yaml
Fix_1_Reduce_Bounce_T1:
  Impact: 10 (100% usuarios pass T1)
  Severity: 10 (High signal S1)
  Effort: 7 (2-3 eng days landing page optimization)
  Score: (10 × 10) / 7 = 14.3
  Priority: #1

Fix_2_Improve_Checkout_T4:
  Impact: 8 (80% reach T4)
  Severity: 10 (High signal S2 cart abandonment)
  Effort: 4 (5-7 eng days UX redesign)
  Score: (8 × 10) / 4 = 20.0
  Priority: #0 (highest!)

Fix_3_Support_CSAT_T6:
  Impact: 3 (30% contact support)
  Severity: 5 (Medium signal S4)
  Effort: 6 (3-4 eng days chatbot improvements)
  Score: (3 × 5) / 6 = 2.5
  Priority: #3

Fix_4_Logistics_T5:
  Impact: 10 (100% receive product)
  Severity: 5 (Medium signal S3)
  Effort: 2 (complex, logistics partner coordination)
  Score: (10 × 5) / 2 = 25.0
  Priority: #0 (tie highest, external dependency warning)
```

**Tus Fixes Priorizados** (top 5):

| Fix ID | Touchpoint | Impact | Severity | Effort | Priority Score | Ranking |
|--------|------------|--------|----------|--------|----------------|---------|
| 1 | | | | | | |
| 2 | | | | | | |
| 3 | | | | | | |
| 4 | | | | | | |
| 5 | | | | | | |

---

## PASO 8: Validación Post-Implementation

### Before/After Metrics

**Purpose**: Demostrar ROI mejoras CX (justificar inversión).

**Formato**:
```yaml
Fix_Implemented: [Descripción mejora]
Date_Deployed: [YYYY-MM-DD]
Touchpoint: [T1, T2, etc.]

Metrics_Before (baseline 30 días pre):
  O2_Metric: [Valor baseline]
  CX_Score: [Score baseline]
  Customer_Complaints: [Count baseline]

Metrics_After (30 días post):
  O2_Metric: [Valor post]
  CX_Score: [Score post]
  Customer_Complaints: [Count post]

Impact:
  O2_Delta: [+X% improvement]
  CX_Score_Delta: [+Y points]
  Complaints_Delta: [-Z%]
  
ROI_Estimated:
  Churn_Reduction: [-X customers/mes × $LTV]
  NPS_Increase: [+Y points → referrals → $Z acquisition saved]
  Total_Annual_Impact: [$__K/year]
```

### Ejemplo: Checkout Improvement

```yaml
Fix: Simplified checkout flow (reduce steps 5→3)
Date: 2024-06-01
Touchpoint: T4_Purchase

Before (May 2024):
  Checkout_Completion: 62%
  CX_Score: 68
  Cart_Abandonment_Complaints: 120/mes

After (July 2024):
  Checkout_Completion: 78%
  CX_Score: 75
  Cart_Abandonment_Complaints: 40/mes

Impact:
  Completion_Rate: +16% (62%→78%)
  CX_Score: +7 points
  Complaints: -67% (120→40)

ROI:
  Revenue_Increase: +16% orders × $50 avg order × 10K visitors/mes = +$80K/mes
  Annual_Impact: $960K/year
  Eng_Cost: 7 days × $1K/day = $7K
  ROI: 137× (payback <1 week)
```

---

## Referencias KERNEL

**Patterns**:
- `A1_Patrones.md` §6.6: P_CX01-03
- `A1_Patrones.md` §5: P31 RICE Scoring (priorización)
- `A1_Patrones.md` §6: P38 Anomaly Detection, P50 A/B Test Analyzer

**Primitivos**:
- `CORE/01_Primitivos.md` §1: F (Flujos), R (Recursos), A (Actores)
- `CORE/01_Primitivos.md` §3A: S (Señales), E (Eventos)

**Observables**:
- `DOMINIOS/D2_Percepcion.md` §2: O2 Valor (NPS, CSAT)
- `DOMINIOS/D2_Percepcion.md` §4: IN3 Eficiencia Flujo

**Dominios**:
- `CORE/03_Arquitectura.md`: D1-D4 mapping CX
- `DOMINIOS/D4_Operacion.md`: Ejecución mejoras flujo

---

## Changelog Template

**v2.2.0** (2025-11-03):
- Initial release T23_Customer_Journey_Map
- KERNEL-native approach (Flujos F, Observables O2, Señales S, Actores A)
- Diferenciación vs Design Thinking tradicional
- Dashboard CX_Score (similar H_Score)
- Priorización RICE adaptada CX
