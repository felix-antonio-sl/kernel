# D1_Arquitectura

**Versión:** 3.0.0 | **Estado:** Definitivo | **Audiencia:** Enterprise Architects, Org Leaders

---

## INVARIANTE DOMINIO

**Arquitectura = Estructura organizacional (quién hace qué) que implementa principios PE1-PE10 + Building Blocks BB1-BB5 → A_Score.**

**Propiedad:** D1 NO decide estrategia (eso es D3), solo define ESTRUCTURA para ejecutarla.

---

## REFERENCIAS RÁPIDAS

```yaml
Principios_Estructurales_10:
  PE1: §1.1 - Autoridad Única (RACI 1 Accountable)
  PE2: §1.2 - Límites Claros (boundaries explícitos)
  PE3: §1.3 - Specialization at Scale (expertise profundo)
  PE4: §1.4 - Conway's Law Awareness (structure → architecture)
  PE5: §1.5 - Minimize Handoffs (<20% ratio)
  PE6: §1.6 - Autonomy with Alignment (cómo vs qué)
  PE7: §1.7 - Reversible Decisions Fast (Type 1 vs Type 2)
  PE8: §1.8 - Internal Entrepreneurship (Outside-In)
  PE9: §1.9 - Span of Control (5-9 reports)
  PE10: §1.10 - Professional Clustering (career paths)

Building_Blocks_5:
  BB1: §3.1 - Engineers (innovadores)
  BB2: §3.2 - Service Providers (operadores)
  BB3: §3.3 - Coordinators (facilitadores)
  BB4: §3.4 - Sales (relacionadores)
  BB5: §3.5 - Audit (aseguradores)

Patrones_Org_Key:
  P01: Feature Teams (cross-functional, 5-9 personas)
  P02: Platform Teams (infra compartida)
  P10: SRE Model (error budgets, toil <50%)

Métricas:
  A_Score: §4 - Health arquitectura (0-100)
  IN1_Velocidad: D2 §3.1 (cycle time decisiones)
  IN2_Salud_Talento: D2 §3.2 (engagement, turnover)

Cross-References:
  CORE/03_Arquitectura.md: A_Score base (A1-A5) + invariantes
  CORE/01_Primitivos.md §7: Composición Outside-In
  D2_Percepcion.md: IN1, IN2 observables vinculados
  D3_Decision.md §7: Modos decisionales D1-D4
  D4_Operacion.md §1: Teams estables (asset thinking)
```

---

## Responsabilidad

**ARQUITECTURA define ESTRUCTURA organizacional: Quién, qué, límites, interfaces → claridad decisional + ejecución eficiente.**

**Pregunta clave:** ¿Cómo nos organizamos para lograr objetivos?

**NO pregunta:** ¿Qué objetivos? (eso es D3 Decisión)

---

## §0. QUICK START: ARQUITECTURA MÍNIMA VIABLE (MVA)

**Objetivo**: Claridad estructural básica en 4-6 semanas.

### MVA Checklist

```yaml
Week_1-2: Estructura Básica
  ☐ Org chart documentado (Lucidchart, Miro, Excel)
  ☐ Teams identificados (5-9 personas each si posible)
  ☐ Managers asignados (span 5-9 reports)

Week_3-4: Claridad Decisional
  ☐ RACI matriz top 10 procesos críticos
  ☐ Decision rights (Type 1 vs Type 2)
  ☐ Escalation path definido

Week_5-6: Interfaces
  ☐ Team boundaries (ownership products/services)
  ☐ Handoff points (max 3-5 críticos)
  ☐ Communication cadence (standups, syncs)

Output_MVA:
  - Clarity: 70%+ personas saben quién decide qué
  - A_Score baseline: 60-70 (functional)
  - Foundation mejora continua

Saltar_MVA_Si:
  - Org chart updated <3M
  - RACI existe y usado
  - <10% conflictos autoridad/semana
  - A_Score >70
  → Ir directo §1-§4 completo
```

---

## §1. PRINCIPIOS ESTRUCTURALES (PE1-PE10)

**Nota:** PE1-PE10 son principios **específicos D1 Arquitectura** (NOT P1-P9 Manifiesto global).

### §1.1. PE1: Autoridad Única

```yaml
Principio: Cada decisión 1 owner único (RACI: single "A")
Rationale: Autoridad fragmentada → parálisis
Test: ¿Decisiones con 2+ vetos, 0 accountable?

Ejemplo_Correcto:
  Decisión: "Priorizar Feature X"
  Owner: PM (único accountable)
  Consulted: Eng Lead, Design
  
Ejemplo_Violación:
  Decisión: "Aprobar arquitectura"
  Owner: CTO + VP Eng + Architect (3 vetos, 0 accountable)
  → ¿Quién responsable si falla?
```

### §1.2. PE2: Límites Claros

```yaml
Principio: Boundaries entre unidades explícitos
Rationale: Handoffs costosos, interfaces reducen friction
Test: ¿Equipos no saben dónde termina responsabilidad?

Ejemplo_Correcto:
  Team_A: API /orders (E2E ownership)
  Team_B: API /payments (E2E ownership)
  Interface: AsyncAPI contract (Order_Created, Payment_Completed)
```

### §1.3. PE3: Specialization at Scale

```yaml
Principio: Mayor escala → mayor especialización
Rationale: World-class expertise requiere focus

Progresión:
  <10: Full-stack generalists OK
  10-50: Backend/Frontend/Data
  50-200: Platform, Product, ML
  200-1000: Departments + chapters
  >1000: Business units + platforms
```

### §1.4. PE4: Conway's Law Awareness

```yaml
Principio: Org structure determina system architecture
Conway's Law: "Systems mirror communication structure"

Implicación:
  Microservices → Teams autónomos pequeños
  Monolito modular → Coordination fuerte central

Ejemplo_Correcto:
  Objetivo: Microservices
  Org: 8 teams (5-9 personas), ownership 1-3 services each
  Resultado: Loose coupling natural
```

### §1.5. PE5: Minimize Handoffs

```yaml
Principio: Reducir handoffs al mínimo
Métrica: Handoff_Ratio = # Handoffs / # Pasos
Target: <20% procesos críticos

Ejemplo_Correcto:
  Deploy: 5 pasos, 1 handoff (Dev → QA) = 20%
  
Ejemplo_Violación:
  Deploy: 12 pasos, 8 handoffs = 67%
  → Cycle time 14d vs 2d
```

### §1.6. PE6: Autonomy with Alignment

```yaml
Principio: Teams autónomos "cómo", alineados "qué"

Balance:
  Centralizado: Estrategia, OKRs, principles, platforms
  Descentralizado: Implementación, tech choices, priorización micro

Ejemplo_Correcto:
  Central: "Reducir churn 5%" (OKR)
  Team A: "Proactive outreach" (cómo autónomo)
  Team B: "Churn prediction ML" (cómo diferente)
```

### §1.7. PE7: Reversible Decisions Fast

```yaml
Principio: Decisiones reversibles → delegar rápido

Type 1 (Irreversible): M&A, reorg mayor
  → C-level approval, análisis profundo

Type 2 (Reversible): Tech stack, features, hiring 1 persona
  → Delegar teams, decidir rápido, ajustar si falla

Ver: D3_Decision.md §7 para modos decisionales D1-D4
```

### §1.8. PE8: Internal Entrepreneurship

```yaml
Principio: Unidades operan como "negocio dentro negocio"
Fundamento: Manifiesto P3 (Outside-In) formalizado en estructura

Composición_KERNEL (Outside-In):
  Unidad_Trabajo:
    actores: Set(Actor)
    productos_servicios: Set(Producto/Servicio)
    destinatarios: Set(Cliente interno/externo)
    métricas_valor: Outcomes medibles

Ver: CORE/01_Primitivos.md §7 para estructura completa
```

### §1.9. PE9: Span of Control

```yaml
Principio: Manager 5-9 reports directos
Rationale: <5 underutilization, >9 overload

Contexto:
  IC (individual contributors): 5-7 típico
  Managers of managers: 7-9 OK
  Senior executives: 5-6 (mayor complejidad reports)
```

### §1.10. PE10: Professional Clustering

```yaml
Principio: Agrupar professionals similares para career paths
Rationale: Permite mentorship, skill growth, knowledge sharing

Ejemplo:
  Backend Engineers cluster → Career path IC1-IC7
  Product Managers cluster → Career path PM1-PM5
```

---

## §2. DIAGNÓSTICO ESTRUCTURAL (4 SÍNTOMAS)

### S1: Parálisis Decisional

```yaml
Síntomas:
  - Decisiones tardan >4 semanas (Type 2)
  - Escalation perpetua a C-level
  - Meetings multiply sin resolution

Root_Causes:
  - Viola PE1 (Autoridad Única): Multiple vetos, 0 accountable
  - Viola PE7 (Reversible Fast): Type 2 treated como Type 1

Fix:
  - RACI con single "A"
  - Delegar Type 2 decisiones
  - Track IN1_Velocidad_Decisional (D2 §3.1)
```

### S2: Coordination Overhead

```yaml
Síntomas:
  - >50% tiempo en meetings
  - Handoffs >50% proceso
  - Cycle time >14d

Root_Causes:
  - Viola PE2 (Límites Claros): Ownership difuso
  - Viola PE5 (Minimize Handoffs): Too many interfaces

Fix:
  - Boundaries explícitos (ownership map)
  - Reduce handoffs (<20%)
  - Cross-functional teams (P01)
```

### S3: Skill Gaps Persistentes

```yaml
Síntomas:
  - Same roles sin fill >6 meses
  - Turnover >20% (regretted attrition >10%)
  - Engagement <60

Root_Causes:
  - Viola PE10 (Professional Clustering): No career paths
  - Viola PE9 (Span Control): Managers overload (>12 reports)

Fix:
  - Professional clustering con mentorship
  - Adjust spans 5-9
  - Track IN2_Salud_Talento (D2 §3.2)
```

### S4: Architecture-Org Mismatch

```yaml
Síntomas:
  - Querer microservices, tener 1 team grande
  - Monolito pero 20 teams pequeños sin coordination
  - Deploy requiere 10 teams sincronizados

Root_Causes:
  - Viola PE4 (Conway's Law): Structure vs architecture misaligned

Fix:
  - Align org structure con target architecture
  - Si microservices → teams autónomos pequeños
  - Si monolito → coordination central fuerte
```

---

## §3. BUILDING BLOCKS (BB1-BB5)

### Concepto

```yaml
Definición: 5 arquetipos organizacionales universales
Completeness_Test: ¿Org puede innovar, operar, coordinar, vender, auditar?
Missing_BB → Gap capability específico
```

### §3.1. BB1: Engineers (Innovadores)

```yaml
Función: Diseñar soluciones nuevas
Sub-Tipos:
  Applications_Engineers: Purpose-specific solutions
  Base_Engineers: Platforms reusables

Test: ¿Org puede innovar?
IF NO → Missing BB1 (zero innovation, solo mantenimiento)
```

### §3.2. BB2: Service Providers (Operadores)

```yaml
Función: Operar assets, entregar servicios repetitivos
Sub-Tipos:
  Asset-based: Infrastructure ops
  People-based: Help desk, recruiting

Test: ¿Org puede mantener day-to-day?
IF NO → Missing BB2 (operational chaos)
```

### §3.3. BB3: Coordinators (Facilitadores)

```yaml
Función: Facilitar decisiones cross-organizacionales
Sub-Tipos:
  Business: Strategy office, PMO
  Technical: Enterprise architects, standards

Test: ¿Org puede coordinar cross-functional?
IF NO → Missing BB3 (fragmentation, no standards)
```

### §3.4. BB4: Sales (Relacionadores)

```yaml
Función: Construir relationships, descubrir oportunidades
Contexto:
  Private: Sales, Marketing, BD (focus revenue)
  Public: Stakeholder engagement, citizen services (focus legitimacy)

Test: ¿Org puede identificar customer needs?
IF NO → Missing BB4 (disconnect mercado, reactive only)
```

### §3.5. BB5: Audit (Aseguradores)

```yaml
Función: Assurance independent, compliance, risk
Sub-Tipos: Internal audit, Compliance, Risk management, QA

Test: ¿Org tiene oversight independent?
IF NO → Missing BB5 (no controls, compliance failures)
```

### Completeness Test

```yaml
Diagnostic:
  FOR each BB IN [BB1-BB5]:
    ¿Existe? ¿Capacidad adecuada? ¿Reporta apropiadamente?
  
  IF missing:
    - ¿Tercerizado? (acceptable si intentional)
    - ¿No reconocido? (structural gap)
    - ¿Diluido en otros? (violates PE3)

Healthy_State:
  All 5 BBs present + dedicated resources + clear accountability
```

---

## §4. A_SCORE (0-100)

### Fórmula Arquitectura

```yaml
A_Score: Métrica agregada health arquitectura

Fórmula_Base (CORE/03):
  A_Score = (
    0.25 * AS1_Cohesion +
    0.20 * AS2_Coupling +
    0.15 * AS3_Modularity +
    0.20 * AS4_Testability +
    0.20 * AS5_Deployability
  )
  # Nota: AS = Architecture Score components (evita colisión con Axiomas A1-A5)

Fórmula_Extended_D1 (agrega org dimensions):
  A_Score_Extended = (
    0.60 * A_Score_Base +
    0.20 * IN1_Velocidad_Decisional +
    0.15 * IN2_Salud_Talento +
    0.05 * Building_Blocks_Completeness
  )

Donde:
  A_Score_Base: Technical architecture health (CORE/03)
  IN1: D2 §3.1 (cycle time decisiones, delegation rate)
  IN2: D2 §3.2 (turnover, engagement, retention)
  BB_Completeness: (# BBs present / 5) × 100

Interpretación:
  >75: Arquitectura excelente (structure enables velocity)
  60-75: Arquitectura funcional (gaps menores)
  <60: Arquitectura débil (blockers sistémicos)

Típico_MVA: 60-70
Típico_excelencia: 80-90

Vinculación_D2:
  A_Score influye H_Score indirectamente a través de IN1/IN2/IN3 (D2 §3)
```

---

## §5. PATRONES ORG (3 ESENCIALES)

### P01: Feature Teams

```yaml
Definición: Teams cross-functional, ownership E2E
Tamaño: 5-9 personas (two-pizza rule)
Composición: Backend, Frontend, QA, PM, Designer

Beneficio:
  - Minimize handoffs (PE5)
  - Autonomy with alignment (PE6)
  - Velocity alta (cycle time <5d)

Ver: D4_Operacion.md §1 para implementación detallada
```

### P02: Platform Teams

```yaml
Definición: Teams construyen infra compartida
Función: Reduce duplicación, enable otros teams

Ejemplo:
  Platform team provee: CI/CD, Observability, Auth, DB access
  Product teams consumen: Self-service APIs

Beneficio: Specialization at scale (PE3)
```

### P10: SRE Model

```yaml
Definición: Site Reliability Engineering (Google model)
Principio: Error budgets (NOT 100% uptime)
Toil target: <50% tiempo en toil (automate resto)

Beneficio:
  - Balance velocity vs stability
  - Clarity decisional (error budget consumed → slow down)

Ver: APLICACION/A1_Patrones.md §3.11 para SRE completo
```

---

## §6. ANTI-PATRONES ESTRUCTURALES

```yaml
AP_D1_1_Matrix_sin_Governance:
  Síntoma: Dual reporting, nadie sabe quién decide
  Causa: Viola PE1 (Autoridad Única)
  Fix: RACI single "A", escalation path claro

AP_D1_2_Reorg_Perpetuo:
  Síntoma: Cambio estructura cada 6M sin aprendizaje
  Causa: No estabilidad, no optimización incremental
  Fix: Estructura estable >12M, iterar principles NO structure

AP_D1_3_Team_Topology_Mismatch:
  Síntoma: Querer microservices con 1 team 40 personas
  Causa: Viola PE4 (Conway's Law)
  Fix: Align org structure con target architecture

AP_D1_4_Span_Extremo:
  Síntoma: Manager 25+ reports (insostenible)
  Causa: Viola PE9 (Span Control)
  Fix: Adjust spans 5-9, add managers si needed

Ver: APLICACION/A2_Antipatrones.md §2 para 20+ estructurales
```

---

## §7. VALIDACIÓN DOMINIO

**Validación Formal:** Ver `CORE/07_Validacion.md` para pruebas completas de Invariantes I1-I3, Completitud y Consistencia.

**Checklist Rápido D1 (5 min):**

```yaml
✓ Ortogonalidad: D1 ∩ {D2, D3, D4} = ∅
  - D1 estructura, D2 mide, D3 decide, D4 ejecuta
  - Sin solapamiento de responsabilidades

✓ Trazabilidad: Flujo causal verificable
  - D1 structure → D4 execution → D2 metrics (IN1, IN2) → D1 adjust

✓ Completitud: Principios suficientes
  - PE1-PE10 pueden estructurar cualquier organización
  - BB1-BB5 cubren todos componentes estructurales

✓ Parsimonia: Elementos mínimos
  - Ningún principio eliminable sin pérdida de capacidad
  - Ningún BB eliminable sin crear gap de cobertura

✓ Alineamiento CORE:
  - P1 (Autoridad = Responsabilidad) → PE1
  - P2 (Especialización + Colaboración) → BB1-BB5
  - P3 (Outside-In) → PE8 (Unidad_Trabajo)
```

**Para revisión formal:** Aplicar pruebas de `CORE/07_Validacion.md` §2 (Ortogonalidad), §3 (Trazabilidad)

---

## Referencias Cruzadas

- **Invariantes I1-I5:** `CORE/03_Arquitectura.md` (A_Score base)
- **Manifiesto P2:** `CORE/00_Manifiesto.md` §3.2 (Especialización + Colaboración)
- **Manifiesto P3:** `CORE/00_Manifiesto.md` §3.3 (Outside-In → PE8)
- **Primitivo Unidad_Trabajo:** `CORE/01_Primitivos.md` §7 (Outside-In composición)
- **IN1 Velocidad:** `D2_Percepcion.md` §3.1 (observable decisional)
- **IN2 Salud:** `D2_Percepcion.md` §3.2 (observable talento)
- **Modos decisionales:** `D3_Decision.md` §7 (D1-D4, Type 1 vs Type 2)
- **Teams estables:** `D4_Operacion.md` §1 (asset thinking, P01)
- **Delegación:** `CORE/04_Delegacion.md` (M1-M6)
- **Smartness D1:** `CORE/05_Smartness.md` matriz D1 row
- **Trazabilidad:** `CORE/06_Trazabilidad.md` §2 (arquitectura → valor)
- **Patrones:** `APLICACION/A1_Patrones.md` (60+ org patterns)
- **Antipatrones:** `APLICACION/A2_Antipatrones.md` §2 (estructurales)

**Fin D1_Arquitectura v3.0.0**
