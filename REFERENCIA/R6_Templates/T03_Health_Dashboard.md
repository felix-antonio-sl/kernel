# T03: Weekly Executive Dashboard

**Propósito:** Vista ejecutiva salud organizacional (actualización semanal)  
**Audiencia:** C-Suite, Board  
**Formato:** 1 página, lectura <5 min

---

## 📊 HEALTH SCORE (Semana [N])

```
┌────────────────────────────────────────────┐
│  H_SCORE: [72/100] ▲+3 vs semana anterior │
├────────────────────────────────────────────┤
│  D1 Arquitectura:  [68/100] 🟢 ▲+2        │
│  D2 Percepción:    [75/100] 🟢 →          │
│  D3 Decisión:      [70/100] 🟡 ▼-1        │
│  D4 Operación:     [76/100] 🟢 ▲+5        │
└────────────────────────────────────────────┘

Tendencia 13 semanas: ████████████░░ +12 pts
Target Q[X]: 75/100 - On track para alcanzar
```

**Status:** 🟢 HEALTHY - Transformation mode  
**Next Review:** Weekly monitoring continues

---

## 🚨 CRISIS MODE ASSESSMENT (if H_Score < 45)

**⚠️ Template applies when H_Score drops below 45 - Replace normal section with this:**

```
┌──────────────────────────────────────────────────┐
│  H_SCORE: [38/100] 🔴 CRISIS MODE - Week [N]    │
├──────────────────────────────────────────────────┤
│  D1 Arquitectura:  [42/100] 🟡                   │
│  D2 Percepción:    [28/100] 🔴 CRÍTICO           │
│  D3 Decisión:      [45/100] 🟡                   │
│  D4 Operación:     [38/100] 🔴                   │
└──────────────────────────────────────────────────┘

🚨 CRISIS INDICATORS ACTIVE:
├─ O3 Capacity:      [22/100] Cash runway 18 días
├─ O2 Valor:         [25/100] Churn 28%, NPS -8
├─ I2 Talent Health: [28/100] Attrition 32% annual
└─ Observable < 30 threshold crossed

┌──────────────────────────────────────────────────┐
│ ✅ P52 CRISIS GOVERNANCE ACTIVATED - Week 2      │
├──────────────────────────────────────────────────┤
│ Crisis Team: 7 members (see below)               │
│ Meeting Cadence: Daily 9am + 5pm                 │
│ Decision Speed: <4hrs critical, <24hrs tactical  │
│                                                   │
│ STABILIZATION TARGETS (Week 4):                  │
│ • Cash runway: 18d → >60d (bridge financing)     │
│ • Stop churn: Freeze top 20 accounts            │
│ • Talent retention: Emergency bonuses            │
│                                                   │
│ EXIT CRITERIA (to resume transformation):        │
│ • H_Score > 45 for 3 consecutive months          │
│ • All observables > 30                           │
│ • Cash runway > 180 días                         │
└──────────────────────────────────────────────────┘

Crisis Team Roles:
  • Executive Sponsor: [Name] (CEO/COO)
  • Financial Lead: [Name] (CFO) - O3 focus
  • Customer Lead: [Name] (VP CS) - O2 focus
  • People Lead: [Name] (CHRO) - I2 focus
  • Operations Lead: [Name] (VP Eng)
  • Communications: [Name] (CCO)
  • Legal/Compliance: [Name] (as needed)

⚠️ NO MAJOR REORG during crisis (AP33 violation)
   Focus: Stabilize → Diagnose → Transform (when H>45)
```

**Reference:** See `A4_Implementacion.md` §0 Path 1-2 for crisis protocols

---

## 🎯 OKRs PROGRESS (Q[X] - Week [N]/13)

### Org Objective 1: [Nombre]

| KR | Target | Actual | Δ | Confidence | Trend |
|----|--------|--------|---|------------|-------|
| KR1.1 | 99.95% uptime | 99.87% | -0.08pp | 🟡 70% | ▲ |
| KR1.2 | MTTR 30min | 45min | +15min | 🟢 85% | ▲ |
| KR1.3 | NPS 70 | 62 | -8 pts | 🟡 75% | → |

**Status:** 🟡 Parcialmente on track. KR1.1 requiere atención.

### Org Objective 2: [Nombre]
[Similar structure]

---

## 📊 AWARENESS & DECISION MATURITY (v1.3)

### Widget 5: Awareness Levels (S1-S3)

```
┌────────────────────────────────────────────┐
│  AWARENESS MATURITY: [73/100] 🟢 ▲+5 vs Q  │
├────────────────────────────────────────────┤
│  S1 Detect:      [88/100] ✓ Excellent     │
│    Monitoring coverage: 96%                │
│    Dashboard uptime: 99.9%                 │
│    Telemetry latency: 18s (P95)            │
│                                            │
│  S2 Comprehend:  [75/100] ✓ Good          │
│    H_Score automated: ✓ Yes                │
│    Alert quality: 82% actionable           │
│    Pattern detection: ✓ Deployed           │
│                                            │
│  S3 Project:     [58/100] ⚠ Developing    │
│    Forecast accuracy: 12% MAPE ✓           │
│    Crisis monitoring: ✓ H<45 alerts        │
│    Predictive models: 3 (target 5-10)     │
└────────────────────────────────────────────┘

Trend 12 weeks: ████████░░░░ +18 pts
Gap: S3 requires more predictive models in prod
```

---

### Widget 6: Decision Automation

```
┌────────────────────────────────────────────┐
│  DECISION AUTOMATION: [42%] 🟡 ▲+8pp vs Q  │
├────────────────────────────────────────────┤
│  D1 Direct Feedback:                       │
│    Automation rate: 67% (12 of 18 loops)   │
│    Examples: Autoscaling, circuit breakers │
│    Status: ✓ Excellent                     │
│                                            │
│  D2 Rule-Based:                            │
│    Rules documented: 45% (18 of 40 types)  │
│    Rules automated: 72% (13 of 18 docs)    │
│    Status: ⚠ Coverage gaps                 │
│                                            │
│  D3 ML-Assisted:                           │
│    Models in prod: 4 (churn, fraud, etc.)  │
│    Avg accuracy: 87% ✓                     │
│    Human validation: 92% ✓                 │
│    Status: ✓ Good                          │
│                                            │
│  D4 Strategic:                             │
│    Decision latency: 5.2 days ✓ (<7d)     │
│    Simulation tools: ✓ Monte Carlo         │
│    OKR linkage: 78% ⚠ (target 80%)        │
│    Status: ✓ Good                          │
└────────────────────────────────────────────┘

Target Q4: 50% automation rate (need +8pp)
Priority: Document remaining D2 rules, deploy 2 more D3 models
```

---

## 🚨 ALERTS (Top 3 This Week)

### 🔴 CRÍTICO
**A1: Deploy frequency cayó 40%**  
- Root cause: Jenkins cluster inestable desde martes  
- Impact: 12 deploys delayed, 3 features blocked  
- Owner: SRE Lead (Jane)  
- ETA fix: Viernes EOD  
- Mitigation: Manual deploys para P0, cluster upgrade programado

### 🟡 ATENCIÓN
**A2: Cycle time aumentó S1→S3**  
- Métrica: 5 días → 8 días promedio  
- Cause: Code review bottleneck (2 reviewers de vacaciones)  
- Owner: Eng Manager (Carlos)  
- Action: Expanded reviewer pool +3 personas

### 🟢 WATCH
**A3: Churn rate subió 0.3%**  
- Métrica: 2.1% → 2.4% MoM  
- Cause: Pricing change inicio mes  
- Owner: Product VP  
- Action: Monitoring close next 2 weeks

---

## 💰 TRANSFORMATION ROI

```yaml
Investment_to_date: $2.4M (vs $2.6M budget)
Value_delivered: $4.2M (velocity gains + incident reduction)
ROI: 175%
Payback_achieved: Month 14 (target was M18)

Breakdown_value:
  - Velocity +120% = $2.8M/año adicional features
  - Incidents -85% = $1.1M/año costo operacional ahorrado
  - Churn -1.2% = $0.3M/año revenue retained
```

---

## 👥 TEAM HEALTH

| Métrica | This Week | Δ | Benchmark |
|---------|-----------|---|-----------|
| **Velocity** | 18 SP/eng | ▲+2 | 15-20 |
| **Quality** | 1 incident | → | <2/mes |
| **Morale** | 78/100 | ▲+3 | >75 |
| **Turnover** | 8% anual | ▼-2pp | <10% |

🟢 **Morale improvement:** Nuevo home office policy bien recibida  
🟡 **Watch:** Backend team velocity -10% (2 members sick)

---

## 📈 KEY METRICS TRENDS (13 weeks)

```
Deploy Frequency (target: 5/día)
Week: 1  2  3  4  5  6  7  8  9 10 11 12 13
      █  █  ██ ██ ███ ███ ████ ████ ████ ████ █████ █████ ████
      1  1  2  2  3   3   4    4    4    4    5     5     4

MTTR (target: <30min)
Week: 1  2  3  4  5  6  7  8  9 10 11 12 13
      ████████████████ ████ ████ ██ ██ █ █ █ █ █ █
      240min 180  120   90   75  60 50 40 35 32 31 30 45
```

---

## 🎬 INITIATIVES IN FLIGHT

| Initiative | Phase | %Complete | On Track | ETA | Blocker |
|-----------|-------|-----------|----------|-----|---------|
| Cloud Migration | Execute | 65% | 🟢 Yes | M21 | None |
| MLOps Platform | Build | 40% | 🟡 Risk | M18 | GPU quota |
| OKR Rollout | Scale | 80% | 🟢 Yes | M15 | None |
| API Gateway | Done | 100% | ✅ | M14 | - |

---

## 📅 NEXT WEEK PRIORITIES

### Executive Actions Needed
1. **Approve:** GPU quota increase $50K (MLOps blocker)
2. **Review:** Q4 budget allocation (due Friday)
3. **Attend:** All-hands transformation update (Thursday 10am)

### Key Milestones
- Monday: Sprint 26 starts (6 teams)
- Wednesday: Mid-quarter OKR review
- Friday: Platform team demo (API versioning)

---

## 💬 QUOTES (Pulse Survey)

> "Deploy process mejoró dramáticamente. Puedo pushear features sin miedo." - Backend Eng

> "OKRs dieron claridad que no teníamos antes. Sé por qué mi trabajo importa." - Product Designer

> "Dashboards son game changer. Veo problemas antes que users." - SRE

---

## 📎 DEEP DIVES AVAILABLE

- [Link] Detailed H_Score breakdown por dominio
- [Link] OKRs confidence analysis por team
- [Link] Incident postmortem Week 12
- [Link] Tech debt paydown progress report

---

**Next Update:** [Fecha] | **Questions:** [Slack channel] | **Prepared by:** [PMO Team]
