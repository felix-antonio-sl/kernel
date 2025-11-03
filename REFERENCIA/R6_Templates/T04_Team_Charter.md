# T04: Team Formation Checklist

**Propósito:** Formar equipos efectivos 5-8 personas, cross-funcionales, ownership claro

---

## TEAM DESIGN

### Tamaño & Composición

☐ **Tamaño:** 5-8 personas (sweet spot: 6)
☐ **Cross-funcional:** Habilidades para entregar end-to-end sin handoffs
☐ **T-shaped skills:** Profundidad especialista + amplitud generalista

**Composición típica:**
```yaml
Stream-Aligned_Team:
  - 1 Product Owner (customer voice)
  - 3-4 Engineers (backend, frontend, full-stack)
  - 1 Designer (UX/UI)
  - 0.5 QA (embedded, no silo)
  - 0.5 Data Analyst (optional)
```

**Building Blocks Mapping (D1 §4):**

```yaml
Team_Type → Building_Block_Function:

Stream-Aligned_Team:
  → BB1 (Engineers) si focus en innovación/productos nuevos
  → BB2 (Service Providers) si focus en operations/delivery
  Ejemplo BB1: Feature teams building new products
  Ejemplo BB2: Support team operating existing services

Platform_Team:
  → BB2 (Service Providers) + BB3 (Coordinators)
  Function: Proveen servicios shared (BB2: infra, auth, observability)
            + Standards governance (BB3: how to use platform)
  Ejemplo: Platform Eng team (Kubernetes cluster + standards)

Enabling_Team:
  → BB3 (Coordinators)
  Function: Facilitan, coordinan, no ejecutan permanente
  Temporal: Coaching teams en new tech/practices
  Ejemplo: DevOps enablement, Security champions program

Sales/Customer_Success_Team:
  → BB4 (Sales/Stakeholder Engagement)
  Private_Context: Account sales, marketing, BD
  Public_Context: Citizen services, stakeholder relations
  Ejemplo Private: Enterprise sales team
  Ejemplo Public: Citizen engagement office

Audit/Compliance_Team:
  → BB5 (Audit)
  Function: Independent oversight, compliance, risk
  Ejemplo: Internal audit, InfoSec compliance, Risk management

Completeness_Check:
  Organization should have teams covering all 5 BB
  Missing BB → Structural gap (see D1 §4 diagnostic)
```

---

## OWNERSHIP

☐ **Producto/Servicio completo:** Team posee feature de punta a punta
☐ **P&L responsability:** Entienden impacto negocio
☐ **"You build it, you run it":** On-call rotation, incidents
☐ **Metrics ownership:** Team define y trackea KPIs propios

**Anti-patrón:**
❌ Team "backend" + Team "frontend" + Team "QA" separados
✅ Team "Checkout" posee backend+frontend+tests+deploy checkout flow

---

## DEPENDENCIES

☐ **Máx 1-2 dependencias externas** para delivery
☐ **APIs bien definidas** para interacción otros teams
☐ **Platform team** provee servicios compartidos (auth, observability)
☐ **Enabling teams** proveen coaching temporal (no permanente)

---

## TEAM CHARTER (Template)

```markdown
# Team: [Nombre]

## Mission
[1-2 frases: Qué problema resuelven para clientes]

## Ownership
- **Productos:** [Lista productos/servicios]
- **Métricas clave:** [3-5 KPIs core]
- **Stakeholders:** [Clientes internos/externos]

## Team Members
| Nombre | Rol | Skills | Availability |
|--------|-----|--------|--------------|
| [Nombre] | PO | Product, UX research | 100% |
| [Nombre] | Eng | Backend (Python, Go) | 100% |

## Working Agreements
- **Sprint:** 2 semanas
- **Ceremonies:** Planning Mon 9am, Review Fri 2pm, Retro Fri 3pm, Daily 10am
- **Core hours:** 10am-3pm timezone [X]
- **On-call:** Rotation semanal, escalation <15min
- **Decision-making:** Consensus-driven, PO tiebreaker

## Interfaces
- **Depends on:** [Team X] para [API Y]
- **Provides to:** [Team Z] servicio [W]
- **Platform team:** [Servicios consumidos]

## OKRs (Current Quarter)
[Ver T03_OKR_Template.md]
```

---

## TOPOLOGY TYPE

☐ **Stream-Aligned (80% teams):** Feature teams owning customer-facing products
☐ **Platform (10%):** Internal products (IDP, CI/CD, observability)
☐ **Enabling (5%):** Coaching/upskilling (temporal)
☐ **Complicated Subsystem (5%):** Algoritmos especializados (ML, fraud detection)

**Referencia:** Team Topologies (Skelton & Pais)

---

## CHECKLIST LAUNCH

### Week -2: Preparación
☐ Team charter draft completo
☐ Members identificados y confirmados
☐ Stakeholders alineados en mission
☐ Tooling/accesos configurados (Jira, GitHub, AWS, etc.)

### Week -1: Onboarding
☐ Kickoff meeting: Mission, charter, working agreements
☐ Codebase tour + arquitectura overview
☐ Setup dev environments
☐ Primer sprint planificado

### Week 1-4: Formación (Tuckman: Forming)
☐ Daily standups establecidos
☐ First sprint completado
☐ Retrospectiva realizada
☐ Working agreements ajustados

### Week 5-12: Normalización (Storming → Norming)
☐ Velocity estabilizada
☐ Dependencies resueltas
☐ Ownership claro sin ambigüedades
☐ Team morale >70/100

### Week 13+: Performance
☐ Velocity objetivo alcanzada
☐ OKRs on track
☐ Team autónomo, mínima intervención management

---

## RED FLAGS

🚩 **Team >10 personas:** Split en 2 teams
🚩 **Dependencies >3:** Arquitectura problem, reevaluar boundaries
🚩 **Handoffs frecuentes:** No cross-funcional, añadir skills
🚩 **Morale <50:** Burnout risk, intervención urgente
🚩 **Velocity decreciente 3+ sprints:** Retro profunda, tech debt?

---

**Ver también:**
- D4_Operacion.md (KERNEL) para detalles completos
- P01_Team_Topologies (A1_Patrones.md)