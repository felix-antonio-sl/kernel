# KERNEL v2.2 - Índice de Navegación

**Estado:** ✅ Production Ready | **Versión:** 2.2.3 | **Release:** 2025-11-03

---

## 🚀 Resumen Global

- **Versión Actual:** 2.2.3 (Production Ready)
- **Documentos Totales:** 54 archivos
  - CORE: 9 docs
  - DOMINIOS: 4 docs
  - APLICACION: 5 docs
  - DOMINIOS_ESPECIALIZADOS: 8 docs (E1-E8, donde E2 = 4 archivos)
  - REFERENCIA: 14 docs (R1-R7, R6 contiene 15 templates)
  - META: 4 docs (README, INDEX, LEARNING_PATH, VERSIONING, CONTRIBUTING)
- **Patterns:** 72 base (A1) + 27 domain-specific (E2-E5) = 99 total
  - A1: 72 patterns (50 base + 3 emergentes + 3 evolutivos + 5 security + 3 CX + 7 data/AI + 1 multi-tenant)
  - E2 Gov: 3 patterns (P_GOV01-03)
  - E3 Manufacturing: 8 patterns (P_MFG1-8), 7 antipatterns (AP_MFG1-7)
  - E4 Healthcare: 8 patterns (P_HEALTH1-8), 5 antipatterns (AP_HEALTH1-5)
  - E5 Financial: 8 patterns (P_FIN1-8), 5 antipatterns (AP_FIN1-5)
- **Antipatrones:** 52 base (A2: 50 general + 2 multi-tenant) + 17 domain-specific (E3-E5) = 69 total
- **Observables:** 16 (O1-O8, IN1-IN3, SO1-SO5)
- **Templates:** 15 (T01-T14, T23)
- **Líneas Código:** ~18,500 líneas markdown total
- **Idiomas:** Español (completo), Inglés (roadmap v2.3)

**Versión v2.2.3 (2025-11-03)**: Ver `VERSIONING.md` para changelog completo y roadmap.

**Highlights v2.2.3**:
- ✅ Sistema de Validación Distribuido (CORE/07 §7): Central + Local, Métricas M1-M4, AP_VAL1-3
- ✅ Índice de Referencias Cruzadas Global (§"🔗"): 100+ conceptos mapeados, tiempo búsqueda 90% ↓
- ✅ 5 Correcciones Coherencia Críticas: H_Score canónico (suma 1.00), AS1-AS5, P7 Parsimonia
- ✅ Validaciones Locales Optimizadas (D1-D4): Checklists 5 min + referencias formales
- ✅ v2.2.2: Multi-Tenant (P64, AP51-52), Positioning Statement, Learning Path, Security

---

## 🗺️ Navegación por Sección


### 📚 META-DOCUMENTOS

**[VERSIONING.md](./VERSIONING.md)** - Estrategia versionado KERNEL:
- Semantic versioning 2.0.0 (MAJOR.MINOR.PATCH)
- Changelog consolidado v1.0 → v2.2
- Policies: Deprecation, backward compatibility, release cadence
- Roadmap preview: v2.3 (Q1 2026), v3.0 (Q3 2026)

**[LEARNING_PATH.md](./LEARNING_PATH.md)** - Guía adoption progresiva KERNEL (4 tracks especializados):
- **Executive Track** (4-6 hrs): Business case, decisión adopt/no-adopt
- **Architect Track** (12-16 hrs): Implementation roadmap, architecture design
- **AI Engineer Track** (8-12 hrs): Delegation M1-M6, agents specs
- **Full Track** (40-60 hrs): Lectura exhaustiva completa framework

**[CONTRIBUTING.md](./CONTRIBUTING.md)** - Guía contribuciones (open collaboration):
- Tipos contribuciones: Bug fixes, new patterns, templates, domains E9+, traducciones, casos
- Submission process: GitHub PR / Email
- Review criteria: Invariantes I1-I3, principios, quality, evidence ≥2 casos
- Recognition policy, Code of Conduct, FAQ

---

### 核心 CORE (9 Documentos)

*La fundación teórica e inmutable del framework.*

- **[00_Manifiesto.md](./CORE/00_Manifiesto.md):** §0 Positioning Statement (elevator pitch, diferenciadores) + 3 invariantes + 10 principios.
- **[01_Primitivos.md](./CORE/01_Primitivos.md):** Los 7 primitivos fundamentales (Actor, Flujo, Dato, Señal, Límite, Estado, Recurso) con clarificación trade-offs.
- **[02_Ciclo_Fundamental.md](./CORE/02_Ciclo_Fundamental.md):** El ciclo Sense-Decide-Act y WSLC.
- **[03_Arquitectura.md](./CORE/03_Arquitectura.md):** Los 4 dominios ortogonales.
- **[04_Delegacion.md](./CORE/04_Delegacion.md):** Los 6 modos de delegación Humano-IA + 4 propósitos.
- **[05_Smartness.md](./CORE/05_Smartness.md):** La matriz de madurez de inteligencia 4x6 (C1-C6).
- **[06_Trazabilidad.md](./CORE/06_Trazabilidad.md):** El grafo causal de 10 capas.
- **[07_Validacion.md](./CORE/07_Validacion.md):** Pruebas formales de los 3 invariantes (Completitud, Minimalidad, Consistencia) + Sistema de Validación Distribuido.
- **[08_Crisis_Management.md](./CORE/08_Crisis_Management.md):** P52 Crisis Governance + AP31-33 consolidados.

### 域 DOMINIOS (4 Documentos)

*La implementación de los 4 subsistemas operacionales.*

- **[D1_Arquitectura.md](./DOMINIOS/D1_Arquitectura.md):** Principios y patrones para el diseño estructural.
- **[D2_Percepcion.md](./DOMINIOS/D2_Percepcion.md):** Los 16 observables (11 base + 5 security) y la construcción de agentes sensoriales.
- **[D3_Decision.md](./DOMINIOS/D3_Decision.md):** OKRs, planificación y optimización de portafolio.
- **[D4_Operacion.md](./DOMINIOS/D4_Operacion.md):** Gestión de equipos, flujo de valor y ejecución.

### 应用 APLICACION (5 Documentos)

*Guías prácticas, playbooks y herramientas para la ejecución.*

- **[A1_Patrones.md](./APLICACION/A1_Patrones.md):** Catálogo de 64 patrones (50 base + 3 emergentes + 3 evolutivos + 5 security + 3 CX).
- **[A2_Antipatrones.md](./APLICACION/A2_Antipatrones.md):** Catálogo de 35 antipatrones (30 base + 5 v1.3: crisis & orchestration).
- **[A3_Diagnostico.md](./APLICACION/A3_Diagnostico.md):** El framework para calcular el H_Score.
- **[A4_Implementacion.md](./APLICACION/A4_Implementacion.md):** El playbook de transformación de 6 fases.
- **[A5_Medicion.md](./APLICACION/A5_Medicion.md):** KPIs, dashboards y métricas para cada dominio.

### 专科 DOMINIOS_ESPECIALIZADOS (8 Documentos)

*Adaptaciones de KERNEL para contextos industriales específicos.*

- **[E1_Digital.md](./DOMINIOS_ESPECIALIZADOS/E1_Digital.md):** Para Sistemas de Información, DevOps y MLOps.
- **E2 Gobierno Digital** (3 documentos especializados):
  - **[E2_Gov_Digital_Base.md](./DOMINIOS_ESPECIALIZADOS/E2_Gov_Digital_Base.md):** Principios universales eGovernment (cualquier país)
  - **[E2_Chile_TDE.md](./DOMINIOS_ESPECIALIZADOS/E2_Chile_TDE.md):** Implementación específica Chile (Ley 21.180 TDE)
  - **[E2_Template_Gov.md](./DOMINIOS_ESPECIALIZADOS/E2_Template_Gov.md):** Guía adaptación otros países
  - **[E2_Publico.md](./DOMINIOS_ESPECIALIZADOS/E2_Publico.md):** ⚠️ Redirect (ver documentos arriba)
- **[E3_Manufactura.md](./DOMINIOS_ESPECIALIZADOS/E3_Manufactura.md):** 8 patterns (P_MFG1-8: Digital Twin, Predictive Maintenance, Supply Chain, Computer Vision, OEE, AGV, Energy, Blockchain) + 7 antipatterns (AP_MFG1-7).
- **[E4_Salud.md](./DOMINIOS_ESPECIALIZADOS/E4_Salud.md):** 8 patterns (P_HEALTH1-8: Patient Journey, AI Diagnosis, FHIR Interop, HIPAA, Telemedicine, CDS, Drug Interaction, Readmission Prevention) + 5 antipatterns (AP_HEALTH1-5).
- **[E5_Financiero.md](./DOMINIOS_ESPECIALIZADOS/E5_Financiero.md):** 8 patterns (P_FIN1-8: Fraud Detection, Backtesting, Algo Trading, Compliance, KYC/AML, Portfolio Optimization, Market Making, HFT) + 5 antipatterns (AP_FIN1-5).
- **[E6_Template.md](./DOMINIOS_ESPECIALIZADOS/E6_Template.md):** Plantilla para crear nuevos dominios.

### 参考 REFERENCIA (14 Documentos)

*Casos de estudio, plantillas y recursos de apoyo para acelerar la adopción.*

- **[R1_Casos.md](./REFERENCIA/R1_Casos.md):** 10 casos de estudio de transformaciones reales.
- **[R2_Capacidades_Plataforma.md](./REFERENCIA/R2_Capacidades_Plataforma.md):** Las 20 capacidades de una plataforma de EA "KERNEL-compliant".
- **[R3_Comparacion_Frameworks.md](./REFERENCIA/R3_Comparacion_Frameworks.md):** KERNEL vs. TOGAF, Zachman, SAFe.
- **[R4_FAQ.md](./REFERENCIA/R4_FAQ.md):** Preguntas Frecuentes.
- **[R5_Glosario.md](./REFERENCIA/R5_Glosario.md):** Definiciones precisas de todos los términos.
- **[R6_Templates/](./REFERENCIA/R6_Templates/):** Carpeta con 15 plantillas ejecutables:
  - `T01_OKR.md`
  - `T02_Capability_Map.md`
  - `T03_Health_Dashboard.md`
  - `T04_Team_Charter.md`
  - `T05_Assessment.md`
  - `T06_Agente_Spec.md`
  - `T07_Delegacion_Matriz.md`
  - `T08_Ethics_Checklist.md`
  - `T09_Pattern_Application.md`
  - `T10_Roadmap.md`
  - `T11_Technical_Debt_Register.md`
  - `T12_Incident_Postmortem.md`
  - `T13_Architecture_Decision_Record.md`
  - `T14_User_Story_Template.md`
  - `T23_Customer_Journey_Map.md` ✨ (v2.2)
- **[R7_Bibliografia.md](./REFERENCIA/R7_Bibliografia.md):** Lecturas recomendadas.

---

## 🧭 Navegación por Caso de Uso

### Primeros Pasos (New to KERNEL)

- **"Entender KERNEL en 30 minutos"**
  - `README.md` → `CORE/00_Manifiesto.md` §0 (Positioning) → `LEARNING_PATH.md` (elige tu track)

- **"Elevator pitch C-suite (5 min)"**
  - `CORE/00_Manifiesto.md` §0 → Tabla comparativa KERNEL vs TOGAF/SAFe/McKinsey
  - `A5_Medicion.md` §10: Business case template (ROI 1,561%, payback <1 mes)

- **"Implementar rápido (Quick Wins en 4-8 semanas)"**
  - `DOMINIOS/D1_Arquitectura.md` §0 (MVA) - Estructura básica
  - `DOMINIOS/D2_Percepcion.md` §0 (MVP) - Health monitoring
  - `DOMINIOS/D3_Decision.md` §0 (MVD) - OKRs básicos
  - `DOMINIOS/D4_Operacion.md` §0 (MVO) - Delivery continuo

### Diagnóstico & Transformación

- **"Diagnosticar mi organización"**
  - `APLICACION/A3_Diagnostico.md` → Calcular H_Score → Identificar gaps
  - Templates: `R6_Templates/T05_Assessment.md`

- **"Transformación digital end-to-end"**
  - `APLICACION/A4_Implementacion.md` §0 (Readiness Triage)
  - Playbook 6 fases → `R1_Casos.md` ejemplos

- **"Crisis mode (H_Score < 45)"**
  - `CORE/08_Crisis_Management.md` (P52 activation, stabilization)

### Especialización

- **"Integrar agentes IA"**
  - `CORE/04_Delegacion.md` (M1-M6 modes + 4 purposes)
  - `APLICACION/A1_Patrones.md` §6 (P37-P50 IA patterns)
  - Templates: `T06_Agente_Spec.md`, `T07_Delegacion_Matriz.md`

- **"Mejorar madurez organizational"**
  - `CORE/05_Smartness.md` (matriz 4×6, paths C1→C6)

- **"Capability-based planning"**
  - `DOMINIOS/D3_Decision.md` §4 (Roadmaps)
  - `CORE/06_Trazabilidad.md` (Objetivos → Capacidades → Valor)

---

## 🔗 Índice de Referencias Cruzadas

*Mapa exhaustivo de conceptos clave con todas sus ubicaciones en el framework.*

### Invariantes y Axiomas

- **I1 Minimalidad**
  - *Definición:* `CORE/00_Manifiesto.md` §2.1
  - *Validación:* `CORE/07_Validacion.md` §1
  - *Aplicación:* `CORE/01_Primitivos.md` §6 (test 7 primitivos)

- **I2 Ortogonalidad**
  - *Definición:* `CORE/00_Manifiesto.md` §2.2
  - *Validación:* `CORE/07_Validacion.md` §2
  - *Aplicación dominios:* `CORE/03_Arquitectura.md` §2
  - *Verificación:* `D1_Arquitectura.md` §7, `D2_Percepcion.md` §8, `D3_Decision.md` §10, `D4_Operacion.md` §12

- **I3 Trazabilidad**
  - *Definición:* `CORE/00_Manifiesto.md` §2.3
  - *Validación:* `CORE/07_Validacion.md` §3
  - *Sistema completo:* `CORE/06_Trazabilidad.md` (10 capas)
  - *Implementación:* `D3_Decision.md` §2.4, `APLICACION/A5_Medicion.md` §7

- **A1 Unidad de Trabajo**
  - *Definición:* `CORE/00_Manifiesto.md` §3.1, `CORE/01_Primitivos.md` §2
  - *Construcción:* `CORE/01_Primitivos.md` §2.8 (composición 7 primitivos)
  - *Aplicación:* `D1_Arquitectura.md` §1.8 (PE8)

- **A2 Actor Dual**
  - *Definición:* `CORE/00_Manifiesto.md` §3.2
  - *Tipos:* `CORE/01_Primitivos.md` §2.1 (Actor Humano, Actor Algorítmico)
  - *Delegación:* `CORE/04_Delegacion.md` §1-6 (M1-M6)

- **A3 Delegación Explícita**
  - *Definición:* `CORE/00_Manifiesto.md` §3.3
  - *Modos:* `CORE/04_Delegacion.md` §1-6 (M1: Monitorear → M6: Ejecutar)
  - *Propósitos:* `CORE/04_Delegacion.md` §7 (Assistant, Tool, Orchestrator, Automation)
  - *Mapeo dominios:* `CORE/04_Delegacion.md` §8

- **A4 Ciclo SDA Universal**
  - *Definición:* `CORE/00_Manifiesto.md` §3.4
  - *Detalle:* `CORE/02_Ciclo_Fundamental.md` §1 (Sense-Decide-Act)
  - *Niveles:* §1.1 (S1-S3), §1.2 (D1-D4), §1.3 (A1-A3)
  - *Implementación dominios:* `D2_Percepcion.md` (Sense), `D3_Decision.md` (Decide), `D4_Operacion.md` (Act)

- **A5 Evolución Continua**
  - *Definición:* `CORE/00_Manifiesto.md` §3.5
  - *Smartness:* `CORE/05_Smartness.md` (C1→C6)
  - *Versioning:* `VERSIONING.md`

### Principios (P1-P9)

- **P1 Autoridad = Responsabilidad**
  - *Definición:* `CORE/00_Manifiesto.md` §4.1
  - *Aplicación:* `D1_Arquitectura.md` §1.1 (PE1: Ownership Explícito)

- **P2 Especialización + Colaboración**
  - *Definición:* `CORE/00_Manifiesto.md` §4.2
  - *Estructura:* `D1_Arquitectura.md` §2 (Building Blocks)

- **P3 Outside-In**
  - *Definición:* `CORE/00_Manifiesto.md` §4.3
  - *Trazabilidad:* `CORE/06_Trazabilidad.md` §3
  - *OKRs:* `D3_Decision.md` §1.1

- **P4 Flujo Continuo**
  - *Definición:* `CORE/00_Manifiesto.md` §4.4
  - *Métricas:* `D4_Operacion.md` §1 (Lead Time, Cycle Time, Throughput, WIP)
  - *DORA:* `D4_Operacion.md` §2

- **P5 Outcomes > Outputs**
  - *Definición:* `CORE/00_Manifiesto.md` §4.5
  - *Decisiones:* `D3_Decision.md` §1 (OKRs orientados a impacto)

- **P6 Probabilístico**
  - *Definición:* `CORE/00_Manifiesto.md` §4.6
  - *Framework:* `D3_Decision.md` §1.3 (Decisiones bajo incertidumbre)

- **P7 Parsimonia**
  - *Definición:* `CORE/00_Manifiesto.md` §4.7
  - *Aplicación:* `CORE/01_Primitivos.md` §6 (7 primitivos irreducibles)

- **P8 Herramienta no Oráculo**
  - *Definición:* `CORE/00_Manifiesto.md` §4.8
  - *IA como herramienta:* `CORE/04_Delegacion.md` §0

- **P9 Explicabilidad Causal**
  - *Definición:* `CORE/00_Manifiesto.md` §4.9
  - *Trazabilidad:* `CORE/06_Trazabilidad.md` §6
  - *IA:* `CORE/04_Delegacion.md` §7.4, `APLICACION/A1_Patrones.md` P47 (Explicabilidad)

### Primitivos (7)

- **Actor**
  - *Definición:* `CORE/01_Primitivos.md` §2.1
  - *Tipos:* Humano, Algorítmico
  - *Axioma relacionado:* A2 Actor Dual

- **Flujo**
  - *Definición:* `CORE/01_Primitivos.md` §2.2
  - *Métricas:* `D4_Operacion.md` §1

- **Señal**
  - *Definición:* `CORE/01_Primitivos.md` §2.3
  - *Trade-off con Dato:* `CORE/01_Primitivos.md` §3A
  - *Eventos:* `D2_Percepcion.md` §6 (Sensing patterns)

- **Dato**
  - *Definición:* `CORE/01_Primitivos.md` §2.4
  - *Trade-off con Señal:* `CORE/01_Primitivos.md` §3A
  - *Capa trazabilidad:* `CORE/06_Trazabilidad.md` §2.5

- **Límite**
  - *Definición:* `CORE/01_Primitivos.md` §2.5
  - *Tipos:* Temporal, Recurso, Autoridad, Alcance
  - *Security:* `CORE/03_Arquitectura.md` §6, `D2_Percepcion.md` §1.2 (SO1-SO5)

- **Estado**
  - *Definición:* `CORE/01_Primitivos.md` §2.6
  - *Tipos:* Conocido, Inferido, Proyectado

- **Recurso**
  - *Definición:* `CORE/01_Primitivos.md` §2.7
  - *Gestión:* `D1_Arquitectura.md` §1.5 (PE5: Resource Efficiency)

### Dominios (4)

- **D1 Arquitectura**
  - *Definición:* `CORE/03_Arquitectura.md` §2.1
  - *Documento:* `DOMINIOS/D1_Arquitectura.md`
  - *Métrica:* A_Score (§4), A_Score_Extended (§4.1)
  - *Principios:* PE1-PE10 (§1)
  - *Building Blocks:* BB1-BB5 (§2)

- **D2 Percepción**
  - *Definición:* `CORE/03_Arquitectura.md` §2.2
  - *Documento:* `DOMINIOS/D2_Percepcion.md`
  - *Métrica:* H_Score (§3), H_Score_Extended (§3.1 con SO1-SO5)
  - *Observables:* O1-O8 (§1.1 externos), IN1-IN3 (§1.1 internos), SO1-SO5 (§1.2 security)
  - *Niveles Awareness:* S1-S3 (§4)
  - *Patterns:* §6

- **D3 Decisión**
  - *Definición:* `CORE/03_Arquitectura.md` §2.3
  - *Documento:* `DOMINIOS/D3_Decision.md`
  - *Métrica:* D_Score (§6)
  - *Frameworks:* OKRs (§1.1), Time-Value (§1.2), Probabilístico (§1.3)
  - *Frameworks avanzados:* Cost of Delay (§2.1), Readiness (§2.2), Portfolio (§2.3)
  - *Modos decisión:* D1-D4 (§7)

- **D4 Operación**
  - *Definición:* `CORE/03_Arquitectura.md` §2.4
  - *Documento:* `DOMINIOS/D4_Operacion.md`
  - *Métrica:* O_Score (§6)
  - *Flow Metrics:* §1 (Lead Time, Cycle Time, Throughput, WIP)
  - *DORA Metrics:* §2 (Deployment Freq, Lead Time, MTTR, Change Fail Rate)
  - *Tech Debt:* §3
  - *Cultura:* §4 (No commitment culture)
  - *On-call:* §5
  - *Niveles Act:* A1-A3 (§10)

### Métricas Clave

- **H_Score (Health Score)**
  - *Definición:* `D2_Percepcion.md` §3
  - *Fórmula:* Weighted average de 16 observables (O1-O8, IN1-IN3, SO1-SO5)
  - *Diagnóstico:* `APLICACION/A3_Diagnostico.md`
  - *Umbrales crisis:* `CORE/08_Crisis_Management.md` §2 (H < 45)
  - *Template:* `REFERENCIA/R6_Templates/T03_Health_Dashboard.md`

- **A_Score (Architecture Score)**
  - *Definición:* `D1_Arquitectura.md` §4
  - *Extended:* §4.1 (incluye IN1 velocidad decisional, IN2 salud talento)

- **D_Score (Decision Score)**
  - *Definición:* `D3_Decision.md` §6
  - *Componentes:* OKR Progress, Decision Velocity, Resource Allocation

- **O_Score (Operational Score)**
  - *Definición:* `D4_Operacion.md` §6
  - *Componentes:* Flow Metrics + DORA Metrics + Tech Debt

- **DORA Metrics**
  - *Definición:* `D4_Operacion.md` §2
  - *4 métricas:* Deployment Frequency, Lead Time for Changes, MTTR, Change Fail Rate
  - *Benchmarks:* Elite/High/Medium/Low performers

### Delegación y Smartness

- **Modos Delegación (M1-M6)**
  - *Framework completo:* `CORE/04_Delegacion.md`
  - *M1 Monitorear:* §1 (human-in-the-loop pasivo)
  - *M2 Informar:* §2 (detección + alerta)
  - *M3 Habilitar:* §3 (propuestas + decisión humana)
  - *M4 Controlar:* §4 (human-on-the-loop, intervención excepcional)
  - *M5 Coproducir:* §5 (colaboración negociada)
  - *M6 Ejecutar:* §6 (human-out-the-loop, autonomía total)
  - *Template:* `REFERENCIA/R6_Templates/T06_Agente_Spec.md`, `T07_Delegacion_Matriz.md`

- **Niveles Smartness (C1-C6)**
  - *Framework completo:* `CORE/05_Smartness.md`
  - *C1 Manual:* §2.1
  - *C2 Documentado:* §2.2
  - *C3 Medido:* §2.3
  - *C4 Automatizado:* §2.4
  - *C5 Proactivo:* §2.5
  - *C6 Adaptativo:* §2.6
  - *Matriz 4x6:* §3 (ejemplos por dominio)
  - *Paths:* §4 (rutas madurez C1→C6)

### Trazabilidad (10 Capas)

- **Sistema completo:** `CORE/06_Trazabilidad.md` §2
  - *L1:* Objetivos Estratégicos → Capacidades (§2.1)
  - *L2:* Capacidades → Procesos (§2.2)
  - *L3:* Procesos → Aplicaciones (§2.3)
  - *L4:* Aplicaciones → Datos (§2.4)
  - *L5:* Datos → Tecnología (§2.5)
  - *L6:* Tecnología → Controles (§2.6)
  - *L7:* Controles → Riesgos (§2.7)
  - *L8:* Riesgos → Iniciativas (§2.8)
  - *L9:* Iniciativas → Resultados (§2.9)
  - *L10:* Resultados → Valor (§2.10)

- **Queries Críticas:** §5 (Impact Analysis, Orphan Detection, Value Trace, Compliance Gap)
- **Tooling:** §6
- **Template:** `REFERENCIA/R6_Templates/T02_Capability_Map.md`

### Crisis Management

- **P52 Crisis Governance Pattern**
  - *Definición:* `CORE/08_Crisis_Management.md`
  - *Activación:* §2 (H_Score < 45, umbrales observables críticos)
  - *Estructura:* §3 (Crisis Commander, Core Team, Work Streams)
  - *Ritmos:* §4 (War Room diario, Status Updates, Stakeholder Comms)
  - *Derechos decisión:* §5
  - *Protocolos comunicación:* §6
  - *Salida:* §7 (criterios exit)
  - *Antipatrones:* AP31 (crisis permanente), AP32 (heroics), AP33 (ausencia post-mortem)
  - *Estabilización:* §9 (acciones por tipo crisis)

### Patterns y Antipatterns

- **Patterns Base (50):** `APLICACION/A1_Patrones.md`
  - *Arquitectura:* P01-P12 (§1)
  - *Percepción:* P13-P21 (§2)
  - *Decisión:* P22-P36 (§3)
  - *Operación:* P37-P50 (§4)
  - *Emergentes:* P51-P53 (§5: P51 Digital Twin, P52 Crisis Governance, P53 Platform Teams)
  - *Evolutivos:* P54-P56 (§6: P54 Capability Evolution, P55 Tech Radar, P56 Architectural Fitness)
  - *Security:* P_SEC01-05 (§7: Zero Trust, DevSecOps, Incident Response, Identity Governance, Security Observability)
  - *Customer Experience:* P_CX01-03 (§8: Journey-Driven Design, Omnichannel Orchestration, Voice of Customer)

- **Antipatrones Base (50):** `APLICACION/A2_Antipatrones.md`
  - *Arquitectura:* AP01-AP10 (§1)
  - *Percepción:* AP11-AP20 (§2)
  - *Decisión:* AP21-AP30 (§3)
  - *Operación:* AP40-AP50 (§4)
  - *Crisis:* AP31-AP33 (§5)
  - *Multi-tenant:* AP_MT1-MT2 (§6)

- **Patterns Especializados:**
  - *Gobierno:* P_GOV01-03 (`E2_Gov_Digital_Base.md` §3)
  - *Manufactura:* P_MFG1-8 (`E3_Manufactura.md` §2)
  - *Salud:* P_HEALTH1-8 (`E4_Salud.md` §2)
  - *Financiero:* P_FIN1-8 (`E5_Financiero.md` §2)

### Observables

- **Externos (O1-O8):** `D2_Percepcion.md` §1.1.1
  - O1: Net Promoter Score (NPS)
  - O2: Revenue Growth
  - O3: Customer Acquisition Cost (CAC)
  - O4: Customer Lifetime Value (CLTV)
  - O5: Market Share
  - O6: Time to Market (TTM)
  - O7: Digital Adoption Rate
  - O8: Brand Perception Index

- **Internos (IN1-IN3):** `D2_Percepcion.md` §1.1.2
  - IN1: Velocidad Decisional
  - IN2: Salud Talento (eNPS, Retention, Bench Strength)
  - IN3: Eficiencia Flujo (Flow Efficiency)

- **Security (SO1-SO5):** `D2_Percepcion.md` §1.2, `CORE/03_Arquitectura.md` §6
  - SO1: Security Posture Score
  - SO2: Incident Response Time
  - SO3: Vulnerability Remediation Rate
  - SO4: Compliance Coverage
  - SO5: Identity Governance Score

### Ciclos

- **SDA (Sense-Decide-Act):** `CORE/02_Ciclo_Fundamental.md` §1
  - *Niveles Sense:* S1-S3 (§1.1)
  - *Modos Decide:* D1-D4 (§1.2)
  - *Subfases Act:* A1-A3 (§1.3)
  - *Universalidad temporal:* §1.4

- **WSLC (Work System Life Cycle):** `CORE/02_Ciclo_Fundamental.md` §2
  - *Fases:* Operation & Maintenance, Initiation, Development, Implementation
  - *Integración con SDA:* §2.3

### Templates (15)

- **Directorios:** `REFERENCIA/R6_Templates/`
  - T01: OKRs
  - T02: Capability Map
  - T03: Health Dashboard
  - T04: Team Charter
  - T05: Assessment Questionnaire
  - T06: Agente Spec
  - T07: Delegación Matriz
  - T08: Ethics Checklist
  - T09: Pattern Application Guide
  - T10: Transformation Roadmap
  - T11: Technical Debt Register
  - T12: Incident Postmortem
  - T13: Architecture Decision Record (ADR)
  - T14: User Story Template
  - T23: Customer Journey Map

### Documentos Meta

- **VERSIONING.md:** Estrategia versionado, changelog v1.0→v2.2, roadmap v2.3-v3.0
- **LEARNING_PATH.md:** 4 tracks adopción (Executive, Architect, AI Engineer, Full)
- **CONTRIBUTING.md:** Guía contribuciones, review criteria, recognition policy
- **README.md:** Intro framework, quick start
- **INDEX.md:** Este documento (navegación completa)

---

**Fin INDEX.md v2.2.0**

