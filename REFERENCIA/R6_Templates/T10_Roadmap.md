# T10: Transformation Roadmap Template

**Versión:** 2.2.1  
**Última Actualización:** 2025-11-03  
**Compatibilidad:** KERNEL v2.2.x

**Propósito:** Planificar transformación 12-24 meses basada en H_Score diagnóstico

---

## ⚠️ PREREQUISITOS

**Nivel Madurez Requerido:**
- ✅ **H_Score baseline confirmado** (diagnóstico completo D1-D4)
- ✅ **No crisis activa** (H_Score ≥45, no observables <30)
- ✅ **Sponsor ejecutivo comprometido** (budget aprobado, mandate claro)
- ✅ **Readiness Score R1-R5 ≥3.0** promedio (ver P35 Preparación)
- ✅ **Capacidad ejecución** (al menos 1-2 FTEs dedicados a transformación)

**Señales de Alerta - NO USAR si:**
- 🚫 **Crisis mode** (H<45) → Ir a `A4_Implementacion.md` §0 Path 1-2 (estabilización)
- 🚫 **H_Score no calculado** → Completar assessment primero (T05)
- 🚫 **Budget no aprobado** → Roadmap será papel mojado, conseguir funding primero
- 🚫 **Resistencia cultural crítica** → Hacer readiness building antes (6-12 meses)
- 🚫 **Multiple transformations paralelas** → Risk overload, priorizar una sola

**Timing Óptimo:**
- Post-assessment (T05 completado)
- Post-stabilization si hubo crisis
- Budget cycle aligned (Q4 para planning año siguiente)
- Leadership stable (no reorganizaciones inminentes)

**Si Dudas:**
- Ver `A4_Implementacion.md` para determinar si estás en Path correcto
- Considerar roadmap incremental 6 meses (vs 12-24) si incertidumbre alta
- Consultar con KERNEL expert si R1-R5 score <3.0

---

## METADATA

```yaml
Organización: [Nombre]
H_Score_Inicial: [0-100]
Fecha_Diagnóstico: [YYYY-MM-DD]
Sponsor_Ejecutivo: [Nombre + Cargo]
Budget_Total: [USD]
Timeline: [Meses]
```

---

## FASE 1: ESTABILIZACIÓN (M1-M3)

**Objetivo:** Detener degradación, crear fundación observable

| ID | Iniciativa | Patrón | Owner | Budget | Success Metric |
|----|-----------|--------|-------|--------|----------------|
| S1 | Deploy observability stack | O3 | SRE Lead | $50K | Dashboards 4 dominios |
| S2 | Formar platform team | P01 | CTO | $300K | Team 5-8 operacional M2 |
| S3 | Baseline métricas current state | - | PMO | $20K | H_Score confirmado |
| S4 | Executive alignment workshop | - | Sponsor | $15K | OKRs Q1 aprobados |

**Gate Crítico M3:** H_Score estable (no decreciente) + dashboards operacionales

---

## FASE 2: ARQUITECTURA (M4-M9)

**Objetivo:** Resolver antipatrones estructurales críticos

| ID | Iniciativa | Patrón | Owner | Budget | Success Metric |
|----|-----------|--------|-------|--------|----------------|
| A1 | Reestructurar equipos Conway-compliant | P01 | CTO | - | 0 handoffs cross-team |
| A2 | Extraer bounded contexts top-3 | P07 | Arch Lead | $400K | 3 servicios prod M9 |
| A3 | Implementar IaC | P_SEC03 | Platform | $120K | 80% infra Terraform |
| A4 | Tech debt paydown 20% | P14 | All teams | $600K | Λ de 45%→25% |

**Gate Crítico M9:** D1_Score ≥60 + arquitectura modular desplegada

---

## FASE 3: ACELERACIÓN (M10-M15)

**Objetivo:** Aumentar velocity y quality

| ID | Iniciativa | Patrón | Owner | Budget | Success Metric |
|----|-----------|--------|-------|--------|----------------|
| AC1 | CI/CD pipelines inteligentes | P42 | DevOps | $80K | Deploy frequency 5x/día |
| AC2 | Automated testing >80% coverage | P28 | QA + Eng | $200K | Coverage 45%→80% |
| AC3 | OKR framework implementación | P35 | Product | $50K | 100% teams con OKRs |
| AC4 | MLOps pipeline para IA agents | P37 | ML Eng | $150K | Models en prod <2 días |

**Gate Crítico M15:** D4_Score ≥70 + velocity +100%

---

## FASE 4: OPTIMIZACIÓN (M16-M21)

**Objetivo:** Automatización IA, platform excellence

| ID | Iniciativa | Patrón | Owner | Budget | Success Metric |
|----|-----------|--------|-------|--------|----------------|
| O1 | Integrar agentes IA equipos (M4-M5) | P45,P37 | AI Lead | $250K | 6 agentes prod |
| O2 | Self-healing systems | P44 | SRE | $100K | 70% incidents auto-resolved |
| O3 | Platform-as-Product mindset | P50 | Platform | $80K | NPS interno >40 |
| O4 | Predictive analytics negocio | P39 | Data Sci | $180K | Forecasts 85% accuracy |

**Gate Crítico M21:** H_Score ≥75 + ROI positivo verificado

---

## FASE 5: MADUREZ (M22-M24)

**Objetivo:** Consolidar, documentar, escalar

| ID | Iniciativa | Patrón | Owner | Budget | Success Metric |
|----|-----------|--------|-------|--------|----------------|
| M1 | Runbooks + playbooks completos | - | Tech Writing | $40K | 100% procesos doc |
| M2 | Onboarding automatizado nuevos | P49 | HR Tech | $60K | Time-to-productive -50% |
| M3 | Benchmark externo (DORA, OHI) | - | PMO | $25K | Top quartile 2+ métricas |
| M4 | Retrospectiva + lessons learned | - | Sponsor | $10K | Report público |

**Outcome Final:** H_Score ≥75, ROI ≥300%, capabilities sostenibles

---

## RISKS & MITIGATIONS

| Riesgo | Probabilidad | Impacto | Mitigation |
|--------|--------------|---------|------------|
| Resistance cambio >40% org | ALTA | ALTO | Change mgmt desde M1, pilots voluntarios |
| Budget cuts mid-program | MEDIA | CRÍTICO | ROI quick wins M6, board updates mensuales |
| Key talent turnover | MEDIA | ALTO | Retention plan, knowledge transfer, docs |
| Tech debt mayor de estimado | ALTA | MEDIO | Buffer 20% timeline, re-scope si Λ>50% |
| IA adoption slower than expected | MEDIA | MEDIO | Training programa, IA CoE desde M1 |

---

## GOVERNANCE

**Steering Committee (Mensual):**
- Sponsor Ejecutivo (Chair)
- CTO, CFO, COO
- Transformation Lead

**Working Group (Semanal):**
- Domain Leads (D1-D4)
- PMO
- Change Management Lead

**Metrics Review (Quincenal):**
- H_Score evolution
- Budget vs Actuals
- Timeline vs Plan
- Top risks heatmap

---

**Este template debe customizarse basado en H_Score específico y contexto organizacional. Ver R1_Casos.md para ejemplos reales.**
