# 03_Arquitectura

**Versión:** 2.1.0 | **Estado:** Definitivo | **Audiencia:** Arquitectos, Líderes, Security

---

## Invariante

**Toda organización ejecutable se estructura en exactamente 4 dominios funcionales ortogonales: Arquitectura, Percepción, Decisión, Operación.**

---

## §1. LOS 4 DOMINIOS

### Definición

Los **4 dominios** son subsistemas organizacionales con responsabilidades únicas y sin overlap.

```
┌─────────────────────────────────────────────────────┐
│                  ORGANIZACIÓN                       │
├─────────────────────────────────────────────────────┤
│                                                     │
│  ┌──────────────┐        ┌──────────────┐         │
│  │ ARQUITECTURA │───────▶│  PERCEPCIÓN  │         │
│  │  (Estructura)│        │   (Sensado)  │         │
│  └──────┬───────┘        └──────┬───────┘         │
│         │                       │                  │
│         │                       │                  │
│         ▼                       ▼                  │
│  ┌──────────────┐        ┌──────────────┐         │
│  │   DECISIÓN   │───────▶│  OPERACIÓN   │         │
│  │ (Estrategia) │        │  (Ejecución) │         │
│  └──────────────┘        └──────────────┘         │
│                                                     │
└─────────────────────────────────────────────────────┘
```

---

### D1. ARQUITECTURA

```yaml
Responsabilidad: Definir ESTRUCTURA organizacional
Función: Quién hace qué, cómo se organizan, límites autoridad

Actividades:
  - Diseñar topología (jerarquía, equipos, roles)
  - Asignar responsabilidades (RACI)
  - Definir dominios de decisión
  - Establecer interfaces entre unidades
  - Resolver conflictos estructurales

Output:
  - Org chart ejecutable
  - RACI matrices
  - Team charters
  - Governance model

Pregunta clave: "¿Cómo nos organizamos para lograr objetivos?"
```

**Ver detalle:** `DOMINIOS/D1_Arquitectura.md`

---

### D2. PERCEPCIÓN

```yaml
Responsabilidad: DETECTAR estado interno/externo
Función: Sensado continuo, observables, health monitoring

Actividades:
  - Instrumentar 16 observables (O1-O8, I1-I3, SO1-SO5)
  - Detectar anomalías y drift
  - Generar insights desde datos
  - Proyectar tendencias futuras
  - Alertar cuando thresholds violados

Output:
  - Health Dashboard (H score 0-100)
  - Alertas tempranas
  - Reports estado
  - Forecasts

Pregunta clave: "¿Cuál es nuestro estado actual y hacia dónde vamos?"
```

**Ver detalle:** `DOMINIOS/D2_Percepcion.md`

---

### D3. DECISIÓN

```yaml
Responsabilidad: PLANIFICAR evolución organizacional
Función: Estrategia, priorización, roadmaps, portfolio

Actividades:
  - Definir OKRs (outcomes, no outputs)
  - Priorizar iniciativas (valor/riesgo/costo)
  - Construir roadmaps capability-based
  - Gestionar portfolio activo
  - Preparar transformaciones (R1-R5)

Output:
  - OKRs cascadeados
  - Roadmap 3-12 meses
  - Portfolio priorizado
  - Investment allocation

Pregunta clave: "¿Qué debemos construir/cambiar y en qué orden?"
```

**Ver detalle:** `DOMINIOS/D3_Decision.md`

---

### D4. OPERACIÓN

```yaml
Responsabilidad: EJECUTAR flujos valor
Función: Delivery continuo, teams, excelencia técnica

Actividades:
  - Operar teams estables (5-9 personas)
  - Ejecutar flujos trabajo (Kanban, Scrum)
  - Desplegar continuamente (CI/CD)
  - Mantener activos (tech debt management)
  - Iterar con feedback loops

Output:
  - Valor entregado a clientes
  - Features deployed
  - Incidentes resueltos
  - Métricas flow (cycle time, throughput)

Pregunta clave: "¿Cómo entregamos valor de forma continua y sostenible?"
```

**Ver detalle:** `DOMINIOS/D4_Operacion.md`

---

## §2. ORTOGONALIDAD DE DOMINIOS

### Prueba de No-Overlap

```
Responsabilidad(Arquitectura) ∩ Responsabilidad(Percepción) = ∅
Responsabilidad(Arquitectura) ∩ Responsabilidad(Decisión) = ∅
Responsabilidad(Arquitectura) ∩ Responsabilidad(Operación) = ∅
Responsabilidad(Percepción) ∩ Responsabilidad(Decisión) = ∅
Responsabilidad(Percepción) ∩ Responsabilidad(Operación) = ∅
Responsabilidad(Decisión) ∩ Responsabilidad(Operación) = ∅
```

### Tabla de Responsabilidades Únicas

| Pregunta | Dominio Responsable | Otros NO deciden |
|----------|---------------------|------------------|
| ¿Cómo nos estructuramos? | **Arquitectura** | Percepción/Decisión/Operación no diseñan org |
| ¿Cuál es nuestro estado? | **Percepción** | Arquitectura/Decisión/Operación no miden |
| ¿Qué priorizamos? | **Decisión** | Arquitectura/Percepción/Operación no planifican strategy |
| ¿Cómo ejecutamos hoy? | **Operación** | Arquitectura/Percepción/Decisión no deliveren |

**Violación ejemplo:**
- Equipo Operación decide cambiar estructura org → Viola dominio Arquitectura
- Arquitectura decide qué feature priorizar → Viola dominio Decisión

---

## §3. INTERACCIONES ENTRE DOMINIOS

### Flujos de Información

```
PERCEPCIÓN → DECISIÓN:
  Input: Health score bajo (H=65), O2 (Valor) decayendo
  Output: Decisión priorizar iniciativa mejora valor

DECISIÓN → ARQUITECTURA:
  Input: Roadmap requiere nueva capability "ML Platform"
  Output: Arquitectura diseña team MLOps

DECISIÓN → OPERACIÓN:
  Input: OKRs Q4, portfolio priorizado
  Output: Operación ejecuta top 5 iniciativas

OPERACIÓN → PERCEPCIÓN:
  Input: Métricas flow (cycle time, throughput, WIP)
  Output: Percepción actualiza I3 (Eficiencia flujo)

ARQUITECTURA → TODOS:
  Input: Nueva estructura organizacional
  Output: Percepción/Decisión/Operación operan con nueva topología

PERCEPCIÓN → ARQUITECTURA:
  Input: I1 (Velocidad decisional) muy baja
  Output: Arquitectura diagnostica governance bottleneck
```

### Ciclo OODA Organizacional

```
Observe  (Percepción)  → Estado detectado
   ↓
Orient   (Arquitectura) → Contexto estructural
   ↓
Decide   (Decisión)     → Curso acción elegido
   ↓
Act      (Operación)    → Valor entregado
   ↓
→ Loop back to Observe
```

---

## §4. NIVELES DE ABSTRACCIÓN

### L1. Estratégico (3-5 años)

```yaml
Horizonte: 3-5 años
Ciclo refresh: Anual
Foco: Visión, misión, posicionamiento

Por dominio:
  Arquitectura: Target org model, capabilities estratégicas
  Percepción: Trends macro (mercado, tech, regulación)
  Decisión: Strategic intents, North Star metrics
  Operación: Platforms y tech stack target
```

---

### L2. Táctico (3-12 meses)

```yaml
Horizonte: 3-12 meses
Ciclo refresh: Trimestral
Foco: Roadmaps, OKRs, portfolios

Por dominio:
  Arquitectura: Cambios estructurales planificados (reorgs, new teams)
  Percepción: 11 observables monitoreados, H score target
  Decisión: OKRs anuales, roadmap capability-based
  Operación: Capacity planning, tech debt budget
```

---

### L3. Operacional (1-4 semanas)

```yaml
Horizonte: 1-4 semanas (sprints)
Ciclo refresh: Sprint (2 semanas típico)
Foco: Ejecución, delivery, resolución problemas

Por dominio:
  Arquitectura: Ajustes menores roles, resolución conflictos
  Percepción: Dashboards real-time, alertas
  Decisión: Sprint planning, backlog priorization
  Operación: Daily work, features deployed, bugs fixed
```

---

### L4. Inmediato (minutos-horas)

```yaml
Horizonte: Minutos-horas
Ciclo refresh: Continuo
Foco: Respuesta inmediata, automatización

Por dominio:
  Arquitectura: (Poco activo en este nivel)
  Percepción: Sensores 24/7, detección anomalías real-time
  Decisión: Decisiones tácticas (incident response, hotfixes)
  Operación: CI/CD deploys, incident management, on-call
```

---

## §5. GOBERNANZA CROSS-DOMAIN

### Modelo de Gobernanza

```yaml
Nivel_Ejecutivo:
  Responsabilidad: Alignment cross-domain
  Composición: C-level (CEO, CTO, CFO, COO)
  Frecuencia: Mensual
  Decisiones:
    - Estrategia (L1)
    - Budget allocation major
    - Reorgs estructurales
    - M&A, partnerships

Nivel_Táctico:
  Responsabilidad: Coordinación roadmaps
  Composición: VPs, Directors
  Frecuencia: Quincenal
  Decisiones:
    - Priorización portfolio (Decisión)
    - Resource allocation (Arquitectura)
    - Escalation de blockers (Operación)

Nivel_Operacional:
  Responsabilidad: Ejecución diaria
  Composición: Teams, Tech Leads, Product Owners
  Frecuencia: Daily (standups)
  Decisiones:
    - Sprint planning (Decisión táctica)
    - Task assignment (Operación)
    - Technical choices (Operación)
```

---

## §6. SECURITY COMO LÍMITE TRANSVERSAL

**Concepto**: Security no es dominio independiente, sino **límite transversal** (L3) que permea los 4 dominios organizacionales.

### Límite L3 Security

```yaml
Definición:
  Security = Constraints operacionales, regulatorios, reputacionales
  que restringen decisiones/acciones en todos los dominios.

Naturaleza_Transversal:
  - NO es dominio separado (no hay "D5 Security")
  - ES límite que aplica a D1-D4 simultáneamente
  - Análogo a compliance, ética, legal (también límites L3)

Diferencia_vs_Dominios:
  Dominios (D1-D4): Tienen responsabilidad funcional única
  Límites (L1-L3): Restricciones aplicables a múltiples dominios
  
  Security cruza:
    - D1 Arquitectura: Secure by design, threat modeling
    - D2 Percepción: Security observables SO1-SO5
    - D3 Decisión: Risk assessment en roadmap
    - D4 Operación: Secure deployment, IR
```

---

### Security en cada Dominio

**D1 ARQUITECTURA (Security by Design)**:
```yaml
Responsabilidad: Diseñar seguridad en estructura organizacional y técnica

Actividades:
  - Threat modeling (STRIDE, DREAD) en arquitectura
  - Define security roles (CISO, SecOps, AppSec)
  - Establece security governance (policies, standards)
  - Diseña security architecture (Defense in Depth, Zero Trust)
  - Define security boundaries (network segmentation, data classification)

Patterns_Aplicables:
  - P_SEC01: Defense in Depth
  - P_SEC02: Zero Trust Architecture
  - P_SEC03: Security as Code

Output:
  - Security architecture diagrams
  - Threat models documentados
  - Security standards/policies
  - Data classification schemes
```

**D2 PERCEPCIÓN (Security Observability)**:
```yaml
Responsabilidad: Detectar estado security interno/externo

Actividades:
  - Instrumentar 5 security observables (SO1-SO5)
  - Monitorear vulnerabilities (CVE tracking)
  - Detectar anomalías security (SIEM, EDR)
  - Proyectar security posture trends
  - Alertar security thresholds violados

Observables_Security:
  - SO1: Vulnerabilidades (MTTP, CVE count)
  - SO2: Gestión Secretos (vault adoption, rotation)
  - SO3: Control Acceso (MFA, privileged accounts)
  - SO4: Cumplimiento (certifications, audit findings)
  - SO5: Incident Response (MTTD, MTTC)

Patterns_Aplicables:
  - P38: Anomaly Detection (security events)
  - P48: Root Cause Analysis (security incidents)

Output:
  - Security dashboards (SO1-SO5 scores)
  - Vulnerability reports
  - Incident alerts
  - Security posture H_Score extended
```

**D3 DECISIÓN (Risk-Informed Planning)**:
```yaml
Responsabilidad: Incorporar security risk en decisiones estratégicas/tácticas

Actividades:
  - Risk assessment en roadmap features
  - Security vs velocity tradeoffs explícitos
  - Budget allocation security initiatives
  - Priorización tech debt security
  - Compliance deadline planning

Decision_Modes_Security:
  - Mode D2 (Rule-Based): Compliance automático (SOC2 controls)
  - Mode D3 (Associative): Risk scoring ML (threat intelligence)
  - Mode D4 (Analytical): Strategic security planning

Patterns_Aplicables:
  - P31: RICE Scoring (incluir security risk)
  - P35: Readiness R1-R5 (security readiness dimension)

Output:
  - Security-informed roadmaps
  - Risk registers actualizados
  - Security OKRs
  - Budget allocation security
```

**D4 OPERACIÓN (Secure Execution)**:
```yaml
Responsabilidad: Ejecutar operaciones seguras día-a-día

Actividades:
  - Secure SDLC (SAST, DAST, code scanning)
  - Secrets management (vault, rotation)
  - Secure deployment (image scanning, signing)
  - Incident response execution (SOAR playbooks)
  - Security drills/exercises

Delegation_Modes:
  - M4-M5: Automated security gates (CI/CD blocks)
  - M6: Auto-remediation (patch automation, auto-scaling blockers)

Patterns_Aplicables:
  - P_SEC04: Shift-Left Security
  - P_SEC05: Incident Response Automation
  - P42: Quality Gates Automated (incluye security)
  - P44: Auto-Rollback (triggered por security threshold)

Output:
  - Security-compliant deployments
  - Patched systems (<7 días MTTP)
  - Incident response playbooks executed
  - Post-incident action items
```

---

### Integration H_Score Extended

```yaml
Security_Impact_H_Score:
  Base_Formula (11 observables):
    H_Score = weighted_avg(O1-O8, I1-I3)
  
  Extended_Formula (16 observables):
    H_Score = 0.70 * avg(O1-O8) + 0.20 * avg(I1-I3) + 0.10 * avg(SO1-SO5)
  
  Rationale:
    - Security NO es dominio aparte (no "D5")
    - Security observables (SO1-SO5) complementan base observables
    - Peso 10% refleja criticality security enterprise
    - Adjustable por industry (financial 15-20%, B2C 5-8%)

Crisis_Threshold_Security:
  IF SO_avg < 30 OR any SO individual < 20:
    → Activate Security Crisis Mode
    → Apply P_SEC emergency patterns
    → Escalate to CISO + C-level
    → Daily security standup until SO > 30
```

---

### Governance Security Cross-Domain

```yaml
Security_Governance_Model:
  
  Security_Champions (Distributed):
    - Embedded en cada team (D1-D4)
    - 20% time security-focused
    - Training by central SecOps
    - Represent security in team decisions
  
  Central_Security_Team (Platform):
    - CISO + SecOps + AppSec (D1 Arquitectura)
    - Build security platforms/tools (D4 Operación)
    - Monitor security posture (D2 Percepción)
    - Define security roadmap (D3 Decisión)
  
  Security_Review_Board (Governance):
    - CISO + CTO + Legal + Risk
    - Monthly: Review SO1-SO5, incidents, roadmap
    - Approve high-risk changes (M&A, new markets)
    - Set security OKRs

Anti-Pattern_Avoid:
  AP_Security_Silo:
    - Security como departamento aislado
    - "No es mi responsabilidad" actitud devs
    - Security discovered late (post-deployment)
    → Fix: Security Champions + Shift-Left + SO observables
```

---

### Conexión Primitivos KERNEL

```yaml
Security_Through_Primitives:
  
  Límite_L3 (Security Constraint):
    - Security policies restrict actions
    - Compliance requirements bound decisions
    - Ejemplos: "No PII en logs", "MFA mandatory", "SOC2 required"
  
  Actor_A (Security Roles):
    - A2_CISO: Chief Information Security Officer
    - A2_SecOps: Security Operations team
    - A2_Security_Champion: Embedded en teams
  
  Evento_E (Security Events):
    - E_CVE_Published: Nueva vulnerabilidad disclosed
    - E_Security_Incident: Breach o attempt detected
    - E_Audit_Finding: Compliance gap identified
  
  Señal_S (Security Alerts):
    - S_Vulnerability_Threshold: CVE count >threshold
    - S_Access_Anomaly: Unusual login pattern
    - S_Compliance_Risk: Audit due, gaps exist
  
  Dato_D (Security Data):
    - D_Vulnerability_DB: CVE database
    - D_Audit_Logs: Security events stream
    - D_Threat_Intelligence: Known attack patterns
```

---

## §7. PATRONES ESTRUCTURALES

### P1. Federación

```yaml
Patrón: Federación
Estructura: Unidades autónomas con governance central mínima
Aplicable: Organizaciones >500 personas, multi-producto

Arquitectura:
  - Business units con P&L propio
  - Central: Estrategia, governance, platforms compartidas
  - Federadas: Execution, delivery, hiring

Ejemplo: Amazon (Business units como "países independientes")
```

---

### P2. Centralizado

```yaml
Patrón: Centralizado
Estructura: Single hierarchy, decisiones top-down
Aplicable: Startups <50 personas, alta urgencia alignment

Arquitectura:
  - CEO/CTO decide mayoría decisiones
  - Teams ejecutan con autonomía limitada
  - Coordinación fácil, escalabilidad limitada

Ejemplo: Startup pre-product-market-fit
```

---

### P3. Matricial

```yaml
Patrón: Matricial
Estructura: Dual reporting (funcional + proyecto/producto)
Aplicable: Organizaciones 100-500 personas, multi-proyecto

Arquitectura:
  - Functional departments (Eng, Product, Design)
  - Cross-functional teams/squads
  - Conflicts de prioridad requieren governance

Ejemplo: Spotify (Squads + Chapters + Guilds)
```

---

### P4. Business-within-Business

```yaml
Patrón: Business-within-Business
Estructura: Mini-empresas end-to-end por value stream
Aplicable: >200 personas, value streams independientes

Arquitectura:
  - Cada "business" tiene Eng+Product+Design+Data
  - Minimal dependencies entre businesses
  - Platforms compartidas (infra, data, auth)

Ejemplo: Netflix (Content, Streaming, Growth as mini-businesses)
```

---

## §8. EVOLUCIÓN ARQUITECTURAL

### Triggers de Cambio Estructural

```yaml
Trigger_1_Crecimiento:
  Condición: Duplicar headcount en 12 meses
  Acción: Split teams, create new layer management

Trigger_2_Performance:
  Condición: I1 (Velocidad decisional) <50/100 persistente
  Acción: Reducir governance layers, delegar autoridad

Trigger_3_Strategy:
  Condición: Pivote estratégico (nuevo mercado, nuevo producto)
  Acción: Crear nueva business unit o squad

Trigger_4_Merger:
  Condición: M&A completa
  Acción: Integration organizacional (puede tomar 6-18 meses)

Trigger_5_Tech_Debt:
  Condición: O3 (Capacidad) estancada, no puede escalar
  Acción: Platform teams para reducir dependencies
```

---

### Ciclo de Vida Arquitectural

```
1. ESTABLE (60-80% del tiempo)
   - Estructura fija
   - Roles claros
   - Processes establecidos

2. TENSIÓN (señales)
   - I1 bajo (decisiones lentas)
   - Conflicts frecuentes autoridad
   - Silos patológicos
   - Scalability limits

3. DISEÑO (2-8 semanas)
   - Diagnosticar root cause (DOMINIOS/D1_Arquitectura §2)
   - Diseñar target state
   - Preparar transición (R1-R5)
   - Comunicar cambio

4. TRANSICIÓN (4-12 semanas)
   - Anuncio formal
   - Reassignments
   - Handoffs
   - Training
   - Monitoreo I2 (Salud talento) - resistance

5. ESTABILIZACIÓN (4-8 semanas)
   - Nueva estructura opera
   - Ajustes menores
   - Retrospectiva
   - → Volver a ESTABLE
```

**Principio P7 (Parsimonia):** No reorganizar sin causa estructural clara. Reorgs son costosas (I2 sufre).

---

## §9. INTEGRACIÓN CON CICLO SDA

### Arquitectura en SDA

```yaml
Sense (Percepción):
  - Detecta: I1 bajo, conflicts de autoridad, silos
  - Comprende: Root cause es estructura inadecuada
  - Proyecta: Si no cambiamos, velocidad seguirá cayendo

Decide (Decisión):
  - Evalúa: ¿Reorg ahora o esperar?
  - Considera: R1-R5 (preparación), costo-beneficio, riesgo I2
  - Elige: Proceder con patrón "Business-within-Business"

Act (Operación):
  - Planifica: 12 semanas de transición
  - Especifica: Nuevo org chart, RACI, team charters
  - Ejecuta: Anuncio → Reassignments → Stabilization
  - Monitorea: I1, I2, I3 durante/post transición
```

---

## §10. MÉTRICAS DE ARQUITECTURA

### Health Score Arquitectural

```yaml
A_Score (0-100):
  Componentes:
    - A1_Clarity: % roles con RACI claro (target >90%)
    - A2_Balance: Distribución carga work (Gini <0.3)
    - A3_Authority_Alignment: % decisiones con owner único (target >95%)
    - A4_Span_Control: Avg reports per manager (target 5-9)
    - A5_Layers: # niveles jerárquicos (target <5 para <500 personas)

  Fórmula:
    A_Score = 0.3*A1 + 0.2*A2 + 0.25*A3 + 0.15*A4 + 0.1*A5

  Interpretación:
    >85: Excelente
    70-85: Bueno
    50-70: Atención requerida
    <50: Crítico - reorg necesaria
```

---

## §11. ANTI-PATRONES

### AP1. "Matrix sin Governance"

```yaml
Síntoma: Dual reporting sin mecanismo resolución conflictos
Causa: Implementar matricial sin ARB o clear escalation
Consecuencia: Paralysis decisional, I1 colapsa
Fix: Establecer governance explícito (ARB semanal, RACI actualizado)
```

### AP2. "Silos Profundos"

```yaml
Síntoma: Departments no colaboran, handoffs eternos
Causa: Especialización sin interfaces (viola P2)
Fix: Cross-functional teams temporales, shared OKRs
```

### AP3. "Span-of-Control Extremo"

```yaml
Síntoma: Manager con 20+ reports directos
Causa: Growth sin crear management layer
Consecuencia: No hay 1:1s, desarrollo talento nulo, I2 cae
Fix: Split team, promote leads
```

### AP4. "Reorg Perpetuo"

```yaml
Síntoma: Cambio estructura cada 3-6 meses
Causa: Falta diagnóstico root cause, "reorg como solución mágica"
Consecuencia: I2 colapsa (fatiga cambio), no learning organizacional
Fix: Diagnosticar antes de reorg (DOMINIOS/D1_Arquitectura §2)
```

### AP5. "Conway Inverse Fallacy"

```yaml
Síntoma: "Cambiar org para forzar arquitectura tech deseada"
Causa: Malinterpretar Conway's Law (org → tech, no tech → org)
Consecuencia: Resistance, fracaso adoption
Fix: Alinear org con tech actual, evolucionar ambos coordinadamente
```

---

## §12. VALIDACIÓN

### Completitud

```
¿Toda función organizacional cae en 1 de 4 dominios? → SÍ
  Arquitectura: Estructura
  Percepción: Sensing
  Decisión: Planning
  Operación: Execution

¿Algo falta? → NO (validado con 10 casos, ver REFERENCIA/R1_Casos.md)
```

### Ortogonalidad

```
¿Overlaps entre dominios? → NO
  Test: Cada responsabilidad asignable unívocamente a 1 dominio
```

### Suficiencia

```
¿4 dominios suficientes para modelar org completa? → SÍ
  Evidencia: 10 casos diversos (insurance, airline, gov, tech) modelados exitosamente
```

---

## Referencias Cruzadas

- **Dominio Arquitectura detallado:** `DOMINIOS/D1_Arquitectura.md`
- **Dominio Percepción detallado:** `DOMINIOS/D2_Percepcion.md` (incluye §8 Security Observables SO1-SO5)
- **Dominio Decisión detallado:** `DOMINIOS/D3_Decision.md`
- **Dominio Operación detallado:** `DOMINIOS/D4_Operacion.md`
- **Ciclo SDA:** `CORE/02_Ciclo_Fundamental.md`
- **Security como límite transversal:** Este documento §6
- **Security Patterns:** `APLICACION/A1_Patrones.md` §6.5 (P_SEC01-P_SEC05)
- **Security practices detalladas:** `DOMINIOS_ESPECIALIZADOS/E7_Enterprise_Technology.md` §6
- **Patrones org:** `APLICACION/A1_Patrones.md` §7 (patrones estructurales)
- **Casos aplicados:** `REFERENCIA/R1_Casos.md`
