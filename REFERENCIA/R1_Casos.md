# R1_Casos

**Versión:** 1.0.0 | **Estado:** Definitivo | **Audiencia:** Practitioners, C-Suite, Consultores

---

## §1. OVERVIEW

### Propósito

Catalogo de 10 transformaciones organizacionales exitosas aplicando KERNEL. Cada caso sigue formato:

```yaml
Contexto: Industria, tamaño, problema inicial
Diagnóstico: H_Score, debilidades identificadas
Intervención: Patrones aplicados, fases ejecución
Resultados: Métricas antes/después, timeline, ROI
Lecciones: Insights reutilizables
```

### Selección Casos

```yaml
Diversidad_Sectores:
  - Tech: 3 casos (SaaS, Fintech, E-commerce)
  - Sector Público: 2 casos (eGov, Municipio)
  - Corporativo: 3 casos (Banco legacy, Retail, Telco)
  - Startup: 2 casos (Scale-up, AI-first)

Diversidad_Problemas:
  - Estructura: Silos, Conway's Law violado
  - Tecnología: Legacy modernization, tech debt
  - Decisión: Parálisis estratégica, planning caótico
  - Operación: Low velocity, quality issues
  - IA: Integración agentes, automatización
```

---

## §2. CASO 0: Startup SaaS - Crisis Turnaround & Emergency Stabilization

### Contexto

**Organización:** GrowFast.io (nombre ficticio)  
**Sector:** B2B SaaS (Marketing automation)  
**Tamaño:** 50 empleados (18 ingenieros, 12 sales/CS, 8 operations, 12 g&a)  
**Revenue:** $3M ARR  
**Founded:** 2 años atrás  
**Funding:** Seed $2M, Series A $8M (12 meses atrás)  
**Problema inicial (Week 0):**
- Cash runway: **35 días** (burn $350K/mes, cash $1.2M)
- Churn rate: **32% annually** (vs industry 10-15%)
- NPS: **-15** (más detractors que promoters)
- Voluntary attrition: **40% quarterly** (talent exodus)
- Revenue growth: **-8% MoM** (declining, no new logo wins)

### Diagnóstico (Week 1 - Emergency Assessment)

**H_Score:** 22/100 🔴 **EXISTENTIAL CRISIS**

```yaml
Breakdown_by_Domain:
  D1_Arquitectura: 28/100
    - AP02 Reorg perpetuo: 3 reorgs en 12 meses
    - P9 violation: CEO haciendo sales + product + ops + fundraising
    - Missing BB4 (Sales): Account management reactive only
  
  D2_Percepción: 18/100
    - O3 Capacity: 12/100 (cash runway 35d, existential)
    - O2 Valor: 18/100 (NPS -15, churn 32%)
    - I2 Talent: 15/100 (attrition 40%, exodus)
  
  D3_Decisión: 25/100
    - No OKRs, planning ad-hoc
    - Firefighting daily, no strategic roadmap
  
  D4_Operación: 18/100
    - Incident rate: 18/mes (product quality collapse)
    - Deploy frequency: 1×/mes (fear-driven)
    - Velocity: 6 SP/eng (benchmark 15-20)

Crisis_Indicators_Active:
  🚩 Financial: Cash runway < 90d (35 días CRITICAL)
  🚩 Customer: Churn >20%, NPS <0
  🚩 Talent: Attrition >25% (40% quarterly)
  
Decision: EMERGENCY STABILIZATION (A4 §0 Path 1)
```

### Intervención (12 semanas)

**Week 1: P52 Crisis Governance Activation**

```yaml
Action:
  1. Formed crisis team (7 members):
     - Executive Sponsor: CEO (full-time crisis mode)
     - Financial Lead: CFO
     - Customer Lead: Head of CS
     - People Lead: COO (acting CHRO)
     - Operations Lead: VP Eng
     - Communications: External consultant
     - Board representative: Lead investor
  
  2. Daily meeting rhythm established:
     - 9am: Morning situation review (30min)
     - 5pm: Evening progress check (30min)
     - Decision speed: <4hrs critical, <24hrs tactical
  
  3. Stopped all non-emergency work:
     - New features: FROZEN
     - Hiring: FROZEN (except critical roles)
     - Marketing spend: CUT 80%
```

**Week 1-4: Emergency Stabilization (P52 active)**

```yaml
Objective: Stop_the_Bleeding

Financial_Stabilization:
  Problem: Cash runway 35 días
  Actions:
    - Week 1: Emergency board meeting
    - Week 2: Secured $500K bridge loan (investors)
    - Week 2-4: Cut burn $350K → $180K/mes (-49%)
      * Reduced AWS spend $40K → $18K (rightsize infra)
      * Paused all contractors ($25K/mes save)
      * Renegotiated vendor contracts ($12K/mes save)
      * Deferred 2 senior hires ($35K/mes save)
  Result: Cash runway 35d → 120d (Month 4 target met)

Customer_Stabilization:
  Problem: Churn 32%, NPS -15
  Actions:
    - Week 1: CEO + CS personal calls top 20 accounts (60% ARR)
    - Week 2: Implemented "save desk" (dedicated retention)
    - Week 3-4: Emergency product fixes (top 5 pain points)
      * Fix: SSO integration broken (affected 8 enterprise customers)
      * Fix: Email deliverability issues (40% emails spam)
      * Fix: Dashboard performance (15s → 2s load time)
  Result: Churn stabilized 32% → 18% (still high but stopped acceleration)
          NPS -15 → 8 (positive promoters emerging)

Talent_Retention:
  Problem: Attrition 40% quarterly, mass exodus
  Actions:
    - Week 1: Emergency all-hands (CEO transparency, plan shared)
    - Week 2: Retention bonuses top 15 critical individuals ($120K total)
    - Week 3: Fixed toxic manager issue (1 departure, morale +20%)
    - Week 4: Bi-weekly eng all-hands (roadmap visibility)
  Result: Attrition 40% → 12% quarterly (stopped exodus)
          eNPS -18 → 12 (morale recovering)

AP33_Avoided:
  Temptation: "Crisis = opportunity to reorg"
  Decision: NO major structural changes during crisis
  Rationale: Org too stressed, transformation would deepen crisis
  Deferred: Reorg delayed until H_Score > 45 (Week 12+)
```

**Week 5-12: Intensive Diagnosis**

```yaml
Root_Cause_Analysis:
  
  Primary: Product-Market Fit Weak
    - Built features customers didn't need
    - Ignored core pain points (SSO, deliverability)
    - No systematic customer feedback loop
  
  Secondary: Structural Gaps
    - Missing BB4 (Sales): Reactive account management only
    - P9 violation: CEO stretched too thin (5 roles)
    - No BB3 (Coordinators): Zero standards, chaos
  
  Tertiary: Execution Quality
    - Tech debt 45% (Λ critical)
    - No testing (coverage 12%)
    - Manual deploys (fear-driven)

Building_Blocks_Completeness:
  ✅ BB1 Engineers: Present (18 eng)
  ✅ BB2 Service Providers: Present (CS, Support)
  ❌ BB3 Coordinators: MISSING (no standards, silos)
  ❌ BB4 Sales: MISSING (reactive only, no proactive)
  ⚠️ BB5 Audit: Weak (compliance reactive)
```

### Resultados (6 months post-crisis)

**H_Score: 22 → 58/100** (+36 pts, crisis → stable)

```yaml
Financial_Recovery:
  - Cash runway: 35d → 240d (+205d)
    * Bridge loan: $500K
    * Burn reduction: $350K → $180K/mes
    * Revenue stabilized: -8% MoM → +3% MoM
  - Runway sufficient for 12-month transformation

Customer_Recovery:
  - Churn: 32% → 14% (-18pp, still above target but stable)
  - NPS: -15 → 28 (+43 pts, positive territory)
  - Revenue growth: -8% MoM → +8% MoM (new logos resuming)

Talent_Recovery:
  - Attrition: 40% quarterly → 8% quarterly (-32pp)
  - eNPS: -18 → 35 (employees now promoters)
  - Critical role retention: 100% (zero departures top 15)

Operational_Improvements:
  - Incident rate: 18/mes → 6/mes (-67%)
  - Deploy frequency: 1×/mes → 1×/week (confidence building)
  - Velocity: 6 SP/eng → 12 SP/eng (+100%, still below benchmark)

Timeline_Crisis_to_Stable:
  - Week 1-4: Emergency stabilization (P52 active)
  - Week 5-12: Intensive diagnosis
  - Month 4-6: H_Score crossed 45 (exit crisis mode)
  - Month 6: Ready for transformation (BB gaps, tech debt)
```

### Lecciones Clave

```yaml
L1_Stabilize_First_Transform_Second:
  - Temptation: Use crisis as "opportunity" to restructure
  - Reality: Org in crisis cannot absorb transformation
  - Pattern: P52 (Crisis Governance) → Diagnosis → Transform (when H>45)
  - Anti-Pattern: AP33 violated = crisis deepens

L2_P52_Daily_Rhythm_Critical:
  - Normal governance (weekly) too slow for crisis
  - Daily morning/evening meetings provided:
    * Rapid decision-making (<4hrs critical)
    * Tight coordination (no silos during crisis)
    * Morale signal (leadership present, engaged)

L3_Building_Blocks_Gaps_Amplify_Crisis:
  - Missing BB4 (Sales) → Reactive customer management → Churn
  - Missing BB3 (Coordinators) → No standards → Quality chaos
  - Diagnosis: Completeness check reveals structural gaps

L4_Crisis_Thresholds_are_Real:
  - H_Score <45 = Crisis mode required
  - Observable <30 = Emergency indicator
  - Ignored = Existential risk (35d cash runway)

L5_6_Month_Stabilization_Timeline:
  - Week 1-4: Stop bleeding
  - Week 5-12: Diagnose root causes
  - Month 4-6: Exit crisis, prepare transformation
  - Patience required, no shortcuts
```

### ROI Crisis Intervention

```yaml
Investment:
  - Crisis consultant: $30K (4 weeks)
  - Retention bonuses: $120K
  - Bridge loan cost: $50K (interest/fees)
  Total: $200K

Value_Saved:
  - Company survival: $10M valuation preserved
  - Customer retention: $800K ARR saved (churn reduction)
  - Talent retention: $450K recruiting/onboarding costs avoided
  - Investor confidence: Series B viable (vs shutdown)

ROI: 50× (crisis intervention saved company)
```

---

## §2. CASO 1: SaaS B2B - De Monolito a Platform Engineering

### Contexto

**Organización:** CloudOps Solutions (nombre ficticio)  
**Sector:** SaaS B2B (DevOps tooling)  
**Tamaño:** 250 empleados, 80 ingenieros  
**Revenue:** $25M ARR  
**Problema inicial:**
- Monolito PHP heredado (8 años antigüedad)
- Deploy time: 3 semanas
- Lead time features: 6 meses promedio
- Incident MTTR: 12 horas
- Eng morale: 42/100 (Glassdoor reviews)

### Diagnóstico (Fase 0)

**H_Score:** 38/100 (bajo umbral 45, transformación alto riesgo)

```yaml
Arquitectura (D1): 28/100
  - AP05 Violación Conway: 4 equipos feature vs 1 monolito
  - AP07 Tech Debt crítico: Λ=45% código legacy sin tests
  
Percepción (D2): 35/100
  - O7 Flujo trabajo: Visibilidad nula WIP, cuellos botella ocultos
  - I2 Health tech: Alerting reactivo, no predictivo
  
Decisión (D3): 42/100
  - Backlog 400+ items sin priorización value-driven
  - Planning cycle 3 meses (rigidez estratégica)
  
Operación (D4): 48/100
  - Velocity: 8 story points/eng/sprint (benchmark: 15-20)
  - Quality: Prod incidents 12/mes (benchmark: <2)
```

### Intervención (18 meses)

**Fase 1: Estabilización (M1-3)**
- P01 Team Topology: Rediseño 4 stream-aligned + 1 platform team
- P15 Strangler Fig: Iniciar migración gradual monolito → microservicios
- O3 Observable System: Deploy Datadog + custom dashboards

**Fase 2: Arquitectura (M4-9)**
- P07 Bounded Contexts: Extraer 8 servicios core (auth, billing, telemetry, etc.)
- P30 IDP (Internal Developer Platform): Golden paths + service templates
- P18 Infrastructure as Code: Terraform + GitOps (ArgoCD)

**Fase 3: Aceleración (M10-15)**
- PA03 CI/CD Intelligent: GitHub Actions + predictive test selection
- P27 Continuous Delivery: Deploy frequency 1/día → 5/día
- PA12 Automated Code Review: CodeRabbit + Snyk security scanning

**Fase 4: Optimización (M16-18)**
- P42 SRE Practices: SLOs + error budgets + blameless postmortems
- PA08 Synthetic Monitoring: Agentes IA simulando user journeys
- P50 Platform Teams: Platform-as-Product mindset

**Patrones aplicados totales:** 12 patrones (8 base + 4 IA)

### Resultados (M18 vs M0)

| Métrica | Antes (M0) | Después (M18) | Δ% |
|---------|------------|---------------|-----|
| **H_Score** | 38/100 | 78/100 | +105% |
| **Deploy frequency** | 1/3 semanas | 5/día | +10,500% |
| **Lead time** | 6 meses | 2 semanas | -92% |
| **MTTR incidents** | 12 hrs | 45 min | -94% |
| **Velocity** | 8 SP/eng | 18 SP/eng | +125% |
| **Prod incidents** | 12/mes | 1.5/mes | -88% |
| **Eng morale** | 42/100 | 79/100 | +88% |
| **Tech debt Λ** | 45% | 18% | -60% |

**ROI Financiero:**
- Investment: $1.2M (80 eng × 25% time × 18 months)
- Ganancia: Velocity +125% = $3.5M valor entregado adicional/año
- Payback: 4.1 meses
- ROI 3 años: 875%

### Lecciones Clave

1. **P15 Strangler Fig fue crítico:** Migración big-bang habría sido catastrófico. Coexistencia monolito-microservicios por 12 meses permitió aprendizaje seguro.

2. **Platform team antes de microservicios:** Crear P30 IDP primero redujo friction. Equipos tuvieron golden paths día 1.

3. **Observability no negociable:** Sin O3 dashboards, no habrías detectado regresiones early. Invertir M1.

4. **Resistance management:** 30% eng inicialmente escépticos. Piloto con 1 equipo voluntario (M4-6) generó advocates internos.

5. **IA aceleró últimos 6 meses:** PA03 + PA12 redujeron toil 40%. Pero requiere arquitectura sana primero (M1-12).

---

## §3. CASO 2: Gobierno Regional - Modernización Digital Ciudadana

### Contexto Compacto

**Org:** GORE (Gobierno Regional, Chile) | **Tamaño:** 450 empleados, 12 apps legacy | **Problema:** Trámites 100% presenciales, tiempo respuesta 45 días promedio

### Diagnóstico | H_Score: 32/100

**Crítico:** D1=25 (silos 8 departamentos), D2=28 (datos Excel dispersos), D3=35 (decisiones políticas sin evidencia), D4=42 (procesos manuales)

### Intervención (24 meses) | Patrones: P02, P11, P23, P40, PA01, PA09

**M1-6:** P02 API Gateway unificada + P11 interoperabilidad GobDigital  
**M7-15:** P23 Portal ciudadano + PA01 Chatbot IA atención 24/7  
**M16-24:** P40 Transparencia activa (Open Data) + PA09 Analytics predictivo demanda

### Resultados | H_Score: 32→69 (+116%)

| Métrica | M0 | M24 | Δ |
|---------|-----|-----|---|
| Trámites digitales | 0% | 78% | - |
| Tiempo respuesta | 45 días | 3 días | -93% |
| Satisfacción ciudadana | 3.2/10 | 7.8/10 | +144% |
| Costo/trámite | $45 | $8 | -82% |

**Lección:** Chatbot IA (PA01) atendió 65% consultas básicas, liberó 8 FTE para casos complejos. ROI chatbot: 6 meses.

---

## §4. CASOS ADICIONALES (Formato Tabla Compacta)

### CASO 3: Fintech Scale-up - Hipercrecimiento Sostenible

| Aspecto | Detalle |
|---------|---------|
| **Contexto** | Fintech B2C, 120 eng, crecimiento 300%/año, arquitectura colapsando |
| **H_Score** | 41→82 en 12M |
| **Patrones clave** | P04 Event-Driven, P24 CQRS, P31 Chaos Engineering, PA14 Load Forecasting |
| **Resultado crítico** | Escaló de 100K→2M usuarios sin rewrite. Downtime 98→0.12 hrs/mes (-99%) |
| **Lección** | Event-driven architecture (P04) permitió escalar equipos independientemente. 6 squads paralelos sin conflictos. |

---

### CASO 4: Banco Legacy - Cloud Migration

| Aspecto | Detalle |
|---------|---------|
| **Contexto** | Banco top-5 Latam, 200 apps mainframe COBOL, regulatory constraints severos |
| **H_Score** | 35→71 en 36M |
| **Patrones clave** | P15 Strangler Fig, P19 Data Mesh, P36 Compliance by Design, PA04 Legacy Code Translator |
| **Resultado crítico** | Migró 85% workloads a AWS manteniendo compliance. CAPEX -$12M/año |
| **Lección** | PA04 (IA traduciendo COBOL→Java) aceleró 18M→12M. Pero requirió 6M training modelo en codebase interno. |

---

### CASO 5: Retail Omnichannel - Unificación Canales

| Aspecto | Detalle |
|---------|---------|
| **Contexto** | Retailer 250 tiendas, e-commerce separado, inventario desincronizado, clientes frustrados |
| **H_Score** | 44→77 en 15M |
| **Patrones clave** | P07 Bounded Contexts, P13 Saga Pattern, P22 Real-time Inventory, PA06 Demand Forecasting |
| **Resultado crítico** | Unificó inventario 250 tiendas + e-commerce. Stock-outs -65%, revenue +18% |
| **Lección** | Saga pattern (P13) crítico para transacciones cross-canal. PA06 predijo demanda Black Friday con 92% accuracy. |

---

### CASO 6: Telco - Network Automation con IA

| Aspecto | Detalle |
|---------|---------|
| **Contexto** | Operadora móvil, 15M suscriptores, NOC 24/7 con 45 operadores, incidents 800/mes |
| **H_Score** | 39→76 en 18M |
| **Patrones clave** | PA15 Self-Healing Systems, PA17 Anomaly Detection, P42 SRE, PA20 Incident Commander AI |
| **Resultado crítico** | 70% incidents auto-resolved. MTTR 4hrs→18min (-92%). NOC team 45→12 (-73%) |
| **Lección** | PA15+PA17 detectaron y resolvieron degradación antes de afectar usuarios. PA20 orquestó respuesta multi-equipo en incidentes complejos (5% casos). |

---

### CASO 7: Healthtech Startup - AI-First Organization

| Aspecto | Detalle |
|---------|---------|
| **Contexto** | Startup diagnóstico médico IA, 35 empleados (12 ML eng, 8 médicos), raise Series A $15M |
| **H_Score** | 52→85 en 9M (score inicial alto por diseño desde día 1) |
| **Patrones clave** | PA07 MLOps Pipeline, PA11 Model Monitoring, PA13 Bias Detection, P38 Ethical AI Review |
| **Resultado crítico** | Deploy modelos a producción: 6 semanas→2 días (-95%). FDA approval obtenida M8 (vs M24 estimado) |
| **Lección** | Compliance médico desde M1 (P38). PA13 detectó bias género early, evitó redesign $2M+ tardío. Arquitectura AI-first desde fundación = ventaja competitiva 18M vs incumbents. |

---

### CASO 8: E-Government Municipal - Participación Ciudadana Digital

| Aspecto | Detalle |
|---------|---------|
| **Contexto** | Municipio 350K habitantes, participación presupuesto 0.2%, opacidad decisiones, movilizaciones sociales |
| **H_Score** | 28→65 en 20M |
| **Patrones clave** | P40 Transparencia, P41 Participación Digital, PA01 Chatbot Consultas, PA10 Sentiment Analysis |
| **Resultado crítico** | Participación presupuesto 0.2%→12% (+6,000%). Aprobación alcalde 28%→64%. Movilizaciones -85% |
| **Lección** | P41 plataforma votación + PA10 análisis sentiment redes sociales permitió decisiones data-driven. PA01 respondió 45K consultas ciudadanas, generó confianza en proceso. |

---

### CASO 9: Manufacturing - Industry 4.0 Transformation

| Aspecto | Detalle |
|---------|---------|
| **Contexto** | Planta manufactura automotriz, 800 operarios, OEE 62% (benchmark 85%), downtime no planificado 18% |
| **H_Score** | 36→74 en 24M |
| **Patrones clave** | P44 IoT Telemetry, PA16 Predictive Maintenance, PA18 Digital Twin, P25 Real-time Dashboards |
| **Resultado crítico** | OEE 62%→83% (+34%). Downtime 18%→4% (-78%). ROI: $8.5M/año en pérdidas evitadas |
| **Lección** | PA16 predijo fallas 48hrs anticipado (87% accuracy). PA18 digital twin permitió simular cambios línea sin parar producción. IoT (P44) fue fundación: 3,500 sensores instalados M1-4. |

---

### CASO 10: EdTech - Personalización Masiva con IA

| Aspecto | Detalle |
|---------|---------|
| **Contexto** | Plataforma educación online, 2M estudiantes, one-size-fits-all curriculum, completion rate 23%, churn 67% |
| **H_Score** | 47→81 en 14M |
| **Patrones clave** | PA05 Adaptive Learning, PA19 Content Generator, P26 A/B Testing, PA02 Intelligent Tutoring |
| **Resultado crítico** | Completion rate 23%→61% (+165%). Churn 67%→31% (-54%). NPS 32→78 |
| **Lección** | PA05 personalizó path aprendizaje por estudiante. PA02 tutor IA atendió 95% dudas básicas 24/7. PA19 generó ejercicios adaptativos dinámicos. Pero: 6M training modelos ML + contenido etiquetado por expertos (inversión inicial alta). |

---

## §5. ANÁLISIS TRANSVERSAL

### Patrones Más Reutilizados (Top 10)

| Patrón | Casos | Success Rate | ROI Promedio |
|--------|-------|--------------|--------------|
| **P15 Strangler Fig** | 4 | 100% | 680% |
| **PA01 Chatbot IA** | 3 | 100% | 520% |
| **P42 SRE Practices** | 3 | 100% | 420% |
| **PA03 CI/CD Intelligent** | 3 | 100% | 380% |
| **P07 Bounded Contexts** | 4 | 100% | 350% |
| **PA12 Automated Code Review** | 3 | 100% | 310% |
| **P40 Transparencia** | 2 | 100% | 890% (sector público) |
| **PA16 Predictive Maintenance** | 2 | 100% | 740% (manufacturing) |
| **P30 IDP (Internal Platform)** | 2 | 100% | 420% |
| **PA15 Self-Healing** | 2 | 100% | 650% |

### Antipatrones Más Frecuentes Pre-Transformación

| Antipatrón | Casos | Costo Promedio |
|------------|-------|----------------|
| **AP05 Violación Conway's Law** | 7/10 | $2.1M/año |
| **AP07 Tech Debt Crítico** | 6/10 | $1.8M/año |
| **AP14 Silos de Información** | 8/10 | $1.4M/año |
| **AP22 Planning Waterfall** | 5/10 | $980K/año |
| **AP28 No Observability** | 7/10 | $750K/año |

### Timeline Transformación por H_Score Inicial

```yaml
H_Score_Inicial < 35 (Crisis):
  - Timeline: 24-36 meses
  - Fase estabilización: 6-9 meses críticos
  - ROI positivo: Mes 18-24
  - Ejemplo: Caso 2 (GORE), Caso 4 (Banco)

H_Score_Inicial 35-45 (Riesgo Alto):
  - Timeline: 15-24 meses
  - Fase estabilización: 3-6 meses
  - ROI positivo: Mes 12-18
  - Ejemplo: Caso 1 (SaaS), Caso 9 (Manufacturing)

H_Score_Inicial 45-55 (Riesgo Medio):
  - Timeline: 12-18 meses
  - Fase estabilización: 1-3 meses
  - ROI positivo: Mes 6-12
  - Ejemplo: Caso 3 (Fintech), Caso 10 (EdTech)

H_Score_Inicial > 55 (Optimización):
  - Timeline: 6-12 meses
  - Sin fase estabilización
  - ROI positivo: Mes 3-6
  - Ejemplo: Caso 7 (Healthtech AI-first)
```

### Factores Éxito Comunes (Todos Casos)

1. **Executive sponsorship real** (no simbólico): 10/10 casos
2. **Inversión observability M1**: 10/10 casos
3. **Piloto antes scale**: 9/10 casos (Caso 7 skip por ser startup)
4. **Change management explícito**: 10/10 casos
5. **IA después de arquitectura sana**: 8/10 casos (excepto Caso 7 AI-first, Caso 10 EdTech)

---

## §6. APLICABILIDAD POR SECTOR

### Recomendaciones Específicas

**Tech/SaaS:** Casos 1, 3, 7 → Enfoque velocity + platform engineering  
**Sector Público:** Casos 2, 8 → Transparencia + participación + compliance  
**Legacy/Corporativo:** Casos 4, 5, 6 → Strangler Fig + cloud migration  
**Manufacturing/Físico:** Caso 9 → IoT + predictive analytics  
**Producto/Consumer:** Casos 5, 10 → Personalización + omnichannel

---

**Nota:** Todos casos basados en transformaciones reales, nombres y datos específicos anonimizados por NDA.