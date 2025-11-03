# KERNEL v2.2 - Índice de Navegación

**Estado:** ✅ Production Ready | **Versión:** 2.2.0 | **Release:** 2025-11-03

---

## 🚀 Resumen Global

- **Versión Actual:** 2.2.0 (Production Ready)
- **Documentos Totales:** 55 archivos
  - CORE: 9 docs
  - DOMINIOS: 4 docs
  - APLICACION: 5 docs
  - DOMINIOS_ESPECIALIZADOS: 8 docs (E1-E8, donde E2 = 4 archivos)
  - REFERENCIA: 14 docs (R1-R7, R6 contiene 15 templates)
  - META: 5 docs (README, INDEX, LEARNING_PATH, VERSIONING, CONTRIBUTING, QUICK_REFERENCE)
- **Patterns:** 64 (50 base + 3 emergentes + 3 evolutivos + 5 security + 3 CX)
- **Observables:** 16 (O1-O8, I1-I3, SO1-SO5)
- **Templates:** 15 (T01-T14, T23)
- **Líneas Código:** ~17,000 líneas markdown total
- **Idiomas:** Español (completo), Inglés (roadmap v2.3)

**Versión v2.2.0 (2025-11-03)**: Ver `VERSIONING.md` para changelog completo y roadmap.

**Highlights v2.2**:
- ✅ Positioning Statement (CORE/00 §0): Elevator pitch + diferenciadores
- ✅ LEARNING_PATH.md: 4 tracks (Executive, Architect, AI Engineer, Full)
- ✅ Customer Experience KERNEL-native (P_CX01-03 + T23)
- ✅ E2 Gobierno Digital refactored (internacional-first: Base + Chile + Template)
- ✅ Security integration complete (SO1-SO5, P_SEC01-05, CORE/03 §6)

---

## 🗺️ Navegación por Sección


### 📚 META-DOCUMENTOS (Nuevos v2.2)

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

**[QUICK_REFERENCE.md](./QUICK_REFERENCE.md)** - Cheat sheet 1 página (imprimible):
- 7 Primitivos, 4 Dominios, H_Score fórmula, 6 Modos Delegación, 6 Smartness
- Top 10 Patterns quick wins, 3 Invariantes, Decision/Awareness Modes
- ROI example ($8.3M value, 1,561% ROI), Learning Paths tabla, Links rápidos

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
- **[07_Validacion.md](./CORE/07_Validacion.md):** Pruebas formales de los 3 invariantes (Completitud, Minimalidad, Consistencia).
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
- **[E3_Manufactura.md](./DOMINIOS_ESPECIALIZADOS/E3_Manufactura.md):** Para producción, SCM e IoT.
- **[E4_Salud.md](./DOMINIOS_ESPECIALIZADOS/E4_Salud.md):** Para sistemas clínicos y regulación.
- **[E5_Financiero.md](./DOMINIOS_ESPECIALIZADOS/E5_Financiero.md):** Para gestión de riesgo y compliance.
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
  - `README.md` → `CORE/00_Manifiesto.md` §0 (Positioning) → `QUICK_REFERENCE.md` (cheat sheet)

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

