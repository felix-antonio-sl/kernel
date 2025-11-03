# 03_Arquitectura v2.0.0

## §0. INVARIANTE

**Toda organización ejecutable se estructura en exactamente 4 dominios funcionales ortogonales con responsabilidades no solapadas:**

**Arquitectura • Percepción • Decisión • Operación**

**Propiedad I2 (Ortogonalidad):** Responsabilidad(Di) ∩ Responsabilidad(Dj) = ∅ para i≠j.

## §1. LOS 4 DOMINIOS

### Estructura Conceptual

```
┌─────────────────────────────────────┐
│         ORGANIZACIÓN                │
├─────────────────────────────────────┤
│  ┌──────────┐      ┌──────────┐   │
│  │ARQUITECT.│─────▶│PERCEPCIÓN│   │
│  │(Diseña)  │      │(Detecta) │   │
│  └────┬─────┘      └────┬─────┘   │
│       │                 │          │
│       ▼                 ▼          │
│  ┌──────────┐      ┌──────────┐   │
│  │DECISIÓN  │─────▶│OPERACIÓN │   │
│  │(Planifica│      │(Ejecuta) │   │
│  └──────────┘      └──────────┘   │
└─────────────────────────────────────┘
```

### Comparativa Dominios

| Dominio | Responsabilidad | Pregunta Clave | Outputs | Ver Detalle |
|---------|----------------|----------------|---------|-------------|
| **D1 Arquitectura** | Diseñar ESTRUCTURA organizacional | ¿Cómo nos organizamos? | Org chart, RACI, team charters, governance model | `D1_Arquitectura.md` |
| **D2 Percepción** | Detectar ESTADO interno/externo | ¿Cuál es nuestro estado actual? | H_Score, dashboards, alertas, forecasts | `D2_Percepcion.md` |
| **D3 Decisión** | Planificar EVOLUCIÓN | ¿Qué construir y en qué orden? | OKRs, roadmap, portfolio, investment allocation | `D3_Decision.md` |
| **D4 Operación** | Ejecutar FLUJOS valor | ¿Cómo entregamos valor continuo? | Features deployed, incidentes resueltos, métricas flow | `D4_Operacion.md` |

### Actividades por Dominio

**D1 ARQUITECTURA:**

```yaml
Actividades:
  - Diseñar topología (jerarquía, equipos, roles)
  - Asignar responsabilidades (RACI)
  - Definir dominios decisión
  - Establecer interfaces entre unidades
  - Resolver conflictos estructurales
```

**D2 PERCEPCIÓN:**

```yaml
Actividades:
  - Instrumentar 16 observables (11 base + 5 security)
  - Detectar anomalías y drift
  - Generar insights desde datos
  - Proyectar tendencias futuras
  - Alertar thresholds violados
```

**D3 DECISIÓN:**

```yaml
Actividades:
  - Definir OKRs (outcomes, no outputs)
  - Priorizar iniciativas (valor/riesgo/costo)
  - Construir roadmaps capability-based
  - Gestionar portfolio activo
  - Preparar transformaciones (R1-R5)
```

**D4 OPERACIÓN:**

```yaml
Actividades:
  - Operar teams estables (5-9 personas)
  - Ejecutar flujos trabajo (Kanban, Scrum)
  - Desplegar continuamente (CI/CD)
  - Mantener activos (tech debt management)
  - Iterar con feedback loops
```

## §2. ORTOGONALIDAD DE DOMINIOS

### Prueba Formal

```
∀ i,j ∈ {1,2,3,4}, i≠j:
  Responsabilidad(Di) ∩ Responsabilidad(Dj) = ∅
```

### Tabla Responsabilidades Únicas

| Pregunta | Dominio Owner | Otros NO deciden |
|----------|---------------|------------------|
| ¿Cómo estructurarnos? | **D1 Arquitectura** | D2/D3/D4 no diseñan org |
| ¿Cuál es nuestro estado? | **D2 Percepción** | D1/D3/D4 no miden |
| ¿Qué priorizamos? | **D3 Decisión** | D1/D2/D4 no planifican strategy |
| ¿Cómo ejecutamos hoy? | **D4 Operación** | D1/D2/D3 no deliveren |

**Violaciones típicas:**

- ❌ Operación decide cambiar estructura → Viola D1
- ❌ Arquitectura decide qué feature priorizar → Viola D3
- ❌ Decisión ejecuta deploys → Viola D4

## §3. INTERACCIONES ENTRE DOMINIOS

### Flujos de Información

| Flujo | Input | Output |
|-------|-------|--------|
| **D2 → D3** | H_Score bajo (65), O2 decayendo | Priorizar iniciativa mejora valor |
| **D3 → D1** | Roadmap requiere "ML Platform" | Diseñar team MLOps |
| **D3 → D4** | OKRs Q4, portfolio priorizado | Ejecutar top 5 iniciativas |
| **D4 → D2** | Métricas flow (cycle time, WIP) | Actualizar IN3 (Eficiencia flujo) |
| **D1 → All** | Nueva estructura org | D2/D3/D4 operan con nueva topología |
| **D2 → D1** | IN1 (Velocidad decisional) muy baja | Diagnosticar governance bottleneck |

### Ciclo OODA Organizacional

```
Observe  (D2 Percepción)  → Estado detectado
   ↓
Orient   (D1 Arquitectura) → Contexto estructural
   ↓
Decide   (D3 Decisión)     → Curso acción elegido
   ↓
Act      (D4 Operación)    → Valor entregado
   ↓
Loop back → Observe
```

## §4. NIVELES DE ABSTRACCIÓN

| Nivel | Horizonte | Refresh | D1 Arquitectura | D2 Percepción | D3 Decisión | D4 Operación |
|-------|-----------|---------|-----------------|---------------|-------------|--------------|
| **L1 Estratégico** | 3-5 años | Anual | Target org model, capabilities | Trends macro (mercado, tech) | Strategic intents, North Star | Platforms, tech stack target |
| **L2 Táctico** | 3-12 meses | Trimestral | Reorgs planificados | 11 observables, H_Score | OKRs, roadmap capability | Capacity planning, tech debt budget |
| **L3 Operacional** | 1-4 semanas | Sprint | Ajustes roles, conflictos | Dashboards real-time, alertas | Sprint planning, backlog | Daily work, features, bugs |
| **L4 Inmediato** | min-horas | Continuo | (Poco activo) | Sensores 24/7, anomalías | Incident response, hotfixes | CI/CD deploys, on-call |

## §5. GOBERNANZA CROSS-DOMAIN

| Nivel | Composición | Frecuencia | Responsabilidad | Decisiones Típicas |
|-------|-------------|-----------|-----------------|-------------------|
| **Ejecutivo** | C-level (CEO, CTO, CFO, COO) | Mensual | Alignment cross-domain | Estrategia, budget major, reorgs, M&A |
| **Táctico** | VPs, Directors | Quincenal | Coordinación roadmaps | Priorización portfolio, resource allocation, blockers |
| **Operacional** | Teams, Tech Leads, POs | Daily | Ejecución diaria | Sprint planning, task assignment, technical choices |

## §6. SECURITY COMO LÍMITE TRANSVERSAL

### Concepto

**Security NO es dominio independiente (no hay "D5").** Es **límite transversal** (Límite L3) que permea D1-D4.

```yaml
Definición:
  Security = Constraints operacionales, regulatorios, reputacionales
             que restringen decisiones/acciones en todos los dominios

Naturaleza:
  - Análogo a compliance, ética, legal (también límites L3)
  - Cruza los 4 dominios simultáneamente
  - NO tiene responsabilidad funcional única

Diferencia_Dominios_vs_Límites:
  Dominios (D1-D4): Responsabilidad funcional única
  Límites (L1-L3): Restricciones cross-domain
```

### Security por Dominio

| Dominio | Foco Security | Patterns | Outputs |
|---------|---------------|----------|---------|
| **D1 Arquitectura** | Security by Design | P_SEC01 (Defense in Depth)<br>P_SEC02 (Zero Trust)<br>P_SEC03 (Security as Code) | Threat models, security architecture, policies, data classification |
| **D2 Percepción** | Security Observability | P38 (Anomaly Detection)<br>P48 (Root Cause Analysis) | SO1-SO5 dashboards, vulnerability reports, incident alerts, H_Score Extended |
| **D3 Decisión** | Risk-Informed Planning | P31 (RICE + risk)<br>P35 (Readiness R1-R5) | Security-informed roadmaps, risk registers, security OKRs, budget allocation |
| **D4 Operación** | Secure Execution | P_SEC04 (Shift-Left)<br>P_SEC05 (Incident Response Automation)<br>P42 (Quality Gates)<br>P44 (Auto-Rollback) | Secure deployments, patched systems (<7d MTTP), IR playbooks executed |

### Security Observables (SO1-SO5)

```yaml
SO1_Vulnerabilidades:
  Métrica: MTTP (Mean Time to Patch), CVE count
  Target: MTTP <7 días, Critical CVEs = 0

SO2_Gestión_Secretos:
  Métrica: Vault adoption %, rotation frequency
  Target: 100% vaulted, rotation <90 días

SO3_Control_Acceso:
  Métrica: MFA adoption %, privileged accounts audit
  Target: MFA 100%, privileged <5% headcount

SO4_Cumplimiento:
  Métrica: Certifications current, audit findings open
  Target: SOC2/ISO27001 current, findings <3 open

SO5_Incident_Response:
  Métrica: MTTD (Detect), MTTC (Contain), MTTR (Resolve)
  Target: MTTD <1h, MTTC <4h, MTTR <24h
```

### H_Score Extended (16 Observables)

```yaml
Base_Formula (11 observables):
  H_Score = weighted_avg(O1-O8, IN1-IN3)
  
Extended_Formula (16 observables):
  H_Score = 0.90 * H_Score_Base + 0.10 * avg(SO1-SO5)
  # Aproximación rápida (pesos normalizados):
  H_Score = 0.72*avg(O1-O8) + 0.18*avg(IN1-IN3) + 0.10*avg(SO1-SO5)
  # Donde: 0.72 + 0.18 = 0.90 (base), +0.10 (security) = 1.00 total

Ajuste_Industry:
  - Financial/Healthcare: 15-20% security (base 80-85%)
  - SaaS B2B: 12-15% security (base 85-88%)
  - B2C low-sensitivity: 5-8% security (base 92-95%)

Crisis_Threshold:
  IF avg(SO1-SO5) < 30 OR any(SO1-SO5) < 20:
    → Activate Security Crisis Mode
    → Apply P_SEC emergency patterns
    → Escalate CISO + C-level
    → Daily security standup hasta SO > 30
```

**Detalle completo:** `DOMINIOS/D2_Percepcion.md` §8

### Governance Security

```yaml
Security_Champions (Distributed):
  - Embedded en cada team (D1-D4)
  - 20% time security-focused
  - Training by central SecOps

Central_Security_Team (Platform):
  - CISO + SecOps + AppSec
  - Build platforms/tools, monitor posture, define roadmap
  - Opera en los 4 dominios

Security_Review_Board:
  - CISO + CTO + Legal + Risk
  - Monthly: Review SO1-SO5, incidents, roadmap
  - Approve high-risk changes

Anti-Pattern:
  AP_Security_Silo: Security como departamento aislado
  Fix: Security Champions + Shift-Left + SO observables
```

## §7. PATRONES ESTRUCTURALES

| Patrón | Estructura | Aplicable | Arquitectura | Ejemplo |
|--------|-----------|-----------|--------------|---------|
| **Federación** | Unidades autónomas con governance central mínima | >500 personas, multi-producto | Business units con P&L propio. Central: estrategia, governance, platforms. Federadas: execution, delivery, hiring. | Amazon (BUs como "países") |
| **Centralizado** | Single hierarchy, decisiones top-down | <50 personas, alta urgencia alignment | CEO/CTO decide mayoría. Teams con autonomía limitada. Coordinación fácil, escalabilidad limitada. | Startup pre-PMF |
| **Matricial** | Dual reporting (funcional + proyecto/producto) | 100-500 personas, multi-proyecto | Functional departments (Eng, Product, Design) + Cross-functional teams/squads. Conflicts requieren governance. | Spotify (Squads + Chapters) |
| **Business-within-Business** | Mini-empresas end-to-end por value stream | >200 personas, value streams independientes | Cada "business" tiene Eng+Product+Design+Data. Minimal dependencies. Platforms compartidas. | Netflix (Content, Streaming, Growth) |

## §8. EVOLUCIÓN ARQUITECTURAL

### Triggers de Cambio

| Trigger | Condición | Acción |
|---------|-----------|--------|
| **T1 Crecimiento** | Duplicar headcount en 12 meses | Split teams, create management layer |
| **T2 Performance** | IN1 (Velocidad decisional) <50 persistente | Reducir governance layers, delegar autoridad |
| **T3 Strategy** | Pivote estratégico (nuevo mercado/producto) | Crear nueva business unit o squad |
| **T4 Merger** | M&A completa | Integration organizacional (6-18 meses) |
| **T5 Tech Debt** | O3 (Capacidad) estancada, no escala | Platform teams para reducir dependencies |

### Ciclo de Vida

```yaml
1. ESTABLE (60-80% tiempo):
   - Estructura fija, roles claros, processes establecidos

2. TENSIÓN (señales):
   - IN1 bajo, conflicts autoridad, silos, scalability limits

3. DISEÑO (2-8 semanas):
   - Diagnosticar root cause (D1_Arquitectura §2)
   - Diseñar target state, preparar transición (R1-R5)

4. TRANSICIÓN (4-12 semanas):
   - Anuncio, reassignments, handoffs, training
   - Monitoreo IN2 (resistance)

5. ESTABILIZACIÓN (4-8 semanas):
   - Nueva estructura opera, ajustes menores, retrospectiva
```

**Principio P7 (Parsimonia):** No reorganizar sin causa estructural clara. Reorgs son costosas (IN2 sufre).

## §9. INTEGRACIÓN CON CICLO SDA

```yaml
Arquitectura_en_SDA:
  
  Sense (D2 Percepción):
    - Detecta: IN1 bajo, conflicts autoridad, silos
    - Comprende: Root cause estructura inadecuada
    - Proyecta: Sin cambio, velocidad seguirá cayendo
  
  Decide (D3 Decisión):
    - Evalúa: ¿Reorg ahora o esperar?
    - Considera: R1-R5, costo-beneficio, riesgo IN2
    - Elige: Proceder con patrón "Business-within-Business"
  
  Act (D4 Operación):
    - Planifica: 12 semanas transición
    - Especifica: Nuevo org chart, RACI, team charters
    - Ejecuta: Anuncio → Reassignments → Stabilization
    - Monitorea: IN1, IN2, IN3 durante/post transición
```

## §10. MÉTRICAS DE ARQUITECTURA

### A_Score (0-100)

```yaml
Componentes:
  A1_Clarity: % roles con RACI claro (target >90%)
  A2_Balance: Distribución carga work - Gini <0.3
  A3_Authority_Alignment: % decisiones con owner único (>95%)
  A4_Span_Control: Avg reports per manager (target 5-9)
  A5_Layers: # niveles jerárquicos (<5 para <500 personas)

Fórmula:
  A_Score = 0.3*A1 + 0.2*A2 + 0.25*A3 + 0.15*A4 + 0.1*A5

Interpretación:
  >85: Excelente
  70-85: Bueno
  50-70: Atención requerida
  <50: Crítico - reorg necesaria
```

## §11. ANTI-PATRONES

| Anti-Pattern | Síntoma | Causa | Fix |
|--------------|---------|-------|-----|
| **AP_A1: Matrix sin Governance** | Dual reporting sin resolución conflictos | Matricial sin ARB o escalation clara | Governance explícito (ARB semanal, RACI actualizado) |
| **AP_A2: Silos Profundos** | Departments no colaboran, handoffs eternos | Especialización sin interfaces (viola P2) | Cross-functional teams temporales, shared OKRs |
| **AP_A3: Span-of-Control Extremo** | Manager con 20+ reports | Growth sin management layer | Split team, promote leads |
| **AP_A4: Reorg Perpetuo** | Cambio estructura cada 3-6 meses | Falta diagnóstico root cause | Diagnosticar antes de reorg (D1 §2) |
| **AP_A5: Conway Inverse Fallacy** | "Cambiar org para forzar arquitectura tech" | Malinterpretar Conway's Law | Alinear org con tech actual, evolucionar ambos coordinadamente |

## §12. VALIDACIÓN

### Completitud

```
¿Toda función org cae en 1 de 4 dominios? → SÍ
  D1: Estructura | D2: Sensing | D3: Planning | D4: Execution

¿Algo falta? → NO (validado 10 casos, R1_Casos.md)
```

### Ortogonalidad

```
¿Overlaps entre dominios? → NO
  Test: Cada responsabilidad asignable unívocamente a 1 dominio ✓
```

### Suficiencia

```
¿4 dominios suficientes modelar org completa? → SÍ
  Evidencia: 10 casos diversos (insurance, airline, gov, tech) modelados exitosamente
```

## Referencias Cruzadas

- **Manifiesto (I1-I3, A1-A5, P1-P9):** `CORE/00_Manifiesto.md`
- **Primitivos (7):** `CORE/01_Primitivos.md`
- **Ciclo SDA + WSLC:** `CORE/02_Ciclo_Fundamental.md`
- **Delegación (M1-M6):** `CORE/04_Delegacion.md`
- **D1 Arquitectura detallado:** `DOMINIOS/D1_Arquitectura.md`
- **D2 Percepción detallado + SO1-SO5:** `DOMINIOS/D2_Percepcion.md` §8
- **D3 Decisión detallado:** `DOMINIOS/D3_Decision.md`
- **D4 Operación detallado:** `DOMINIOS/D4_Operacion.md`
- **Security Patterns:** `APLICACION/A1_Patrones.md` §6.5 (P_SEC01-P_SEC05)
- **Security practices:** `DOMINIOS_ESPECIALIZADOS/E7_Enterprise_Technology.md` §6
- **Patrones org:** `APLICACION/A1_Patrones.md` §7
- **Casos aplicados:** `REFERENCIA/R1_Casos.md`

**Fin 03_Arquitectura v2.0.0**
