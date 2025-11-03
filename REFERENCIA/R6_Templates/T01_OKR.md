# T01: OKR Template (Quarterly)

**Versión:** 2.2.1  
**Última Actualización:** 2025-11-03  
**Compatibilidad:** KERNEL v2.2.x

**Propósito:** Framework OKRs trimestre siguiente (13 semanas)  
**Ciclo:** Q1: Ene-Mar | Q2: Abr-Jun | Q3: Jul-Sep | Q4: Oct-Dic

---

## ORGANIZATIONAL OKRs (Top-Level)

### Objective 1: [Estratégico, inspirador, cualitativo]
**Por qué importa:** [Conexión estrategia empresa]

| KR | Métrica | M0 | M3 | Owner | Status |
|----|---------|----|----|-------|--------|
| KR1.1 | [Cuantificable] | [Baseline] | [Target] | [Nombre] | 🟢/🟡/🔴 |
| KR1.2 | [Cuantificable] | [Baseline] | [Target] | [Nombre] | 🟢/🟡/🔴 |
| KR1.3 | [Cuantificable] | [Baseline] | [Target] | [Nombre] | 🟢/🟡/🔴 |

**Ejemplo Real:**
```yaml
Objective: Convertirse en plataforma más confiable del mercado
KR1.1: Uptime 99.5% → 99.95% (P10 SRE Model)
KR1.2: MTTR incidents 4hrs → 30min (SRE Lead)
KR1.3: NPS clientes enterprise 45 → 70 (Product VP)
```

---

### Objective 2: [Segundo objetivo org]

| KR | Métrica | M0 | M3 | Owner | Status |
|----|---------|----|----|-------|--------|
| KR2.1 | ... | ... | ... | ... | ... |

---

## TEAM OKRs (Aligned)

### Team: [Nombre Team]

**Team Objective 1:** [Contribuye a Org Obj 1]

| KR | Métrica | M0 | M3 | Sprint Breakdown |
|----|---------|----|----|------------------|
| KR1.1 | Deploy frequency | 1/semana | 5/día | S1: CI/CD, S2-4: Automation, S5-6: Monitoring |
| KR1.2 | Test coverage | 45% | 80% | S1-2: Unit tests, S3-4: Integration, S5-6: E2E |
| KR1.3 | Cycle time | 3 semanas | 5 días | S1: Baseline, S2-4: Bottlenecks, S5-6: Optimization |

**Initiatives (What):**
1. [Específico, ejecutable] - Owner: [Nombre] - Esfuerzo: [Story points]
2. [Específico, ejecutable] - Owner: [Nombre] - Esfuerzo: [Story points]
3. [Específico, ejecutable] - Owner: [Nombre] - Esfuerzo: [Story points]

**Dependencies:**
- Blocker: [Team X debe entregar API Auth] - ETA: S2
- Input needed: [Designs de UX team] - ETA: S1

---

## SCORING & TRACKING

### Weekly Check-in (Viernes 4pm)

```markdown
## Week [N]/13 - [Fecha]

### Progress
- KR1.1: [Actual value] (Target: [Value]) - Confidence: 🟢/🟡/🔴
- KR1.2: [Actual value] (Target: [Value]) - Confidence: 🟢/🟡/🔴

### Blockers
1. [Descripción blocker] - Owner: [Quien resuelve] - ETA: [Fecha]

### Learnings
- [Insight semanal]

### Next Week Focus
- [Top 3 priorities]
```

### Mid-Quarter Review (S7)

**Re-forecast si:**
- Confianza KR <40% en 3+ KRs
- External factors changed (mercado, regulación)
- Dependencies fallaron

**No cambiar Objectives. Ajustar KRs targets si necesario (excepcional).**

---

## GRADING (End Quarter)

```python
# Scoring individual KR
def grade_kr(actual, target, baseline):
    achievement = (actual - baseline) / (target - baseline)
    if achievement >= 1.0:
        return 1.0, "✅ Exceeds"
    elif achievement >= 0.7:
        return achievement, "🟢 On Track"
    elif achievement >= 0.4:
        return achievement, "🟡 Behind"
    else:
        return achievement, "🔴 At Risk"

# Objective score = promedio KRs
objective_score = sum(kr_scores) / len(krs)

# Interpretación
# 0.7-1.0: Success (stretch goals bien calibrados)
# 0.4-0.69: Partial (over-ambitious o execution issues)
# <0.4: Miss (fundamental problems)
```

**Nota:** OKRs bien escritos logran 0.6-0.8. Score 1.0 constante indica targets muy conservadores.

---

## BEST PRACTICES

### Writing Good Objectives
✅ **Good:** "Transformar experiencia cliente digital"  
❌ **Bad:** "Implementar feature X" (es initiative, no objective)

✅ **Good:** "Convertirse en employer of choice tech talent"  
❌ **Bad:** "Mejorar cosas" (vago, no inspirador)

### Writing Good Key Results
✅ **Good:** "NPS 45 → 70" (cuantificable, time-bound)  
❌ **Bad:** "Mejorar satisfacción" (no medible)

✅ **Good:** "Deploy frequency 1/semana → 5/día" (outcome)  
❌ **Bad:** "Implementar CI/CD" (output, no outcome)

### Common Mistakes
1. **Demasiados OKRs:** Max 3 objectives, 3 KRs cada uno
2. **Business-as-usual como OKRs:** "Responder tickets" no es OKR
3. **No conectar team→org:** Teams deben laderar a org objectives
4. **Set & forget:** Review semanal mandatory
5. **100% achievement:** Indica sandbaggin, no stretch goals

---

## TEMPLATE EN BLANCO

```yaml
Q[X] [Year] OKRs

ORGANIZATIONAL:
  Objective 1: [Inspirador]
    KR1.1: [Métrica] [M0]→[M3]
    KR1.2: [Métrica] [M0]→[M3]
    KR1.3: [Métrica] [M0]→[M3]

TEAM: [Nombre]
  Objective 1: [Contribuye Org Obj]
    KR1.1: [Métrica] [M0]→[M3]
    KR1.2: [Métrica] [M0]→[M3]
    Initiatives:
      - [Específico] - [Owner] - [SP]
    Dependencies:
      - [Blocker] - [ETA]
```
