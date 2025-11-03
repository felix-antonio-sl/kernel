# R5: Glosario de Términos

**Versión:** 2.2.0 | **Estado:** Definitivo | **Audiencia:** Todos

---

## A

- **Actor:** (Primitivo) Una entidad que puede ejecutar una acción. Puede ser un humano (ej. un ingeniero), una máquina (ej. un servidor) o un agente de IA (ej. un chatbot).

- **Agente de IA:** (Subtipo de Actor) Un actor computacional con un grado de autonomía (M1-M6) para realizar tareas.

- **Antipatrón:** Una solución común pero ineficaz a un problema recurrente. KERNEL documenta 35 antipatrones en `A2_Antipatrones.md`.

- **Awareness Levels (S1-S3):** Tres niveles cognitivos de percepción: S1 Detect (captura facts), S2 Comprehend (síntesis meaningful), S3 Project (predice estados futuros). Ver `D2_Percepcion.md` §5.

- **Arquitectura (Dominio D1):** Uno de los cuatro dominios de KERNEL, responsable de definir la estructura, los límites y los principios del sistema.

## C

- **Capacidad de Negocio:** Una habilidad o pericia que la organización posee para lograr un propósito específico (ej. "Marketing por correo electrónico"). Se modelan en el Mapa de Capacidades (`T02`).

- **Ciclo Sense-Decide-Act (SDA):** El ciclo de feedback fundamental de KERNEL. Es el proceso continuo de percibir el entorno, decidir una acción y actuar.

- **Crisis Threshold:** Umbral H_Score <45 que activa emergency response patterns (P52 Crisis Governance). Indica disfunción organizacional severa requiriendo intervención inmediata. Ver `CORE/08_Crisis_Management.md`.

- **CX_Score:** Variante H_Score específica customer experience. Weighted avg observables O2 (valor) por touchpoint. Ver `T23_Customer_Journey_Map.md`.

## D

- **Dato:** (Primitivo D) Información que reduce la incertidumbre. Puede ser una métrica, un log, un evento o un modelo de datos.

- **Decisión (Dominio D3):** Uno de los cuatro dominios de KERNEL, responsable de la planificación, la priorización y la definición de objetivos (OKRs).

- **Decision Modes (D1-D4):** Cuatro modos decisionales por complejidad cognitiva: D1 Direct Feedback (automático), D2 Rule-Based (condicional), D3 Associative (pattern fuzzy), D4 Analytical (investigación iterativa). Ver `D3_Decision.md` §6.

- **Delegación (Modos M1-M6):** Los seis niveles de autonomía que se pueden delegar a un agente de IA: M1 Monitor (observa), M2 Inform (alerta), M3 Enable (sugiere), M4 Control (humano valida), M5 Co-produce (colabora), M6 Execute (autónomo). Ver `CORE/04_Delegacion.md`.

## E

- **Estado:** (Primitivo) Una "fotografía" de la configuración de un sistema en un punto específico en el tiempo. Es un snapshot de los Actores, Flujos, Datos y Recursos en un instante `t`. Ver `CORE/01_Primitivos.md` §5.

- **Evento:** (Concepto) La causa de una transición entre dos estados (`Estado(t0) -> Estado(t1)`). Un evento es instantáneo y no es un primitivo, sino el mecanismo de cambio que es notificado por una `Señal`.

## F

- **Flujo:** (Primitivo F) Una secuencia de acciones que transforma inputs en outputs para entregar valor. Puede ser un proceso de negocio, un pipeline de CI/CD o un flujo de datos.

## H

- **H_Score (Health Score):** Métrica compuesta (0-100) que mide salud organizacional. Fórmula base: weighted avg 11 observables (O1-O8, I1-I3). Fórmula extended: 70% O1-O8 + 20% I1-I3 + 10% SO1-SO5 (security). Interpretación: >90 Excelente, 75-89 Bueno, 60-74 Aceptable, 45-59 Pobre, <45 Crisis. Ver `D2_Percepcion.md` §4.

## I

- **Invariante:** Uno de los tres principios no negociables de KERNEL: Minimalidad, Ortogonalidad y Trazabilidad. (Ver `CORE/00_Manifiesto.md`).

## K

- **KERNEL:** El nombre del framework, que significa "núcleo" en alemán. Representa la idea de un sistema operativo central para la organización.

## L

- **Límite:** (Primitivo L) La interfaz que separa dos componentes del sistema. Define qué se expone y qué se oculta, gobernando la interacción y el acoplamiento. Tres tipos: L1 Recursos, L2 Autoridad, L3 Constraints (ej: security, compliance).

## M

- **MVDG (Minimum Viable Digital Government):** Quick start gobierno digital 90 días (governance, diagnóstico, plataformas, infraestructura, datos, plan, capacitación, compliance). Ver `E2_Gov_Digital_Base.md` §0.

- **MVTD (Minimum Viable Transformación Digital):** Variante Chile-specific MVDG para Órganos Administración del Estado cumplir Ley 21.180. Ver `E2_Chile_TDE.md` §0.

## O

- **Observable:** Métrica instrumentada que captura estado sistema. KERNEL define 16 observables canónicos: O1-O8 (externos), IN1-IN3 (internos), SO1-SO5 (security). Cada observable score 0-100, contribuye a H_Score. Ver `D2_Percepcion.md` §1-§4, §8.

- **Operación (Dominio D4):** Uno de los cuatro dominios de KERNEL, responsable de la ejecución de flujos, la gestión de equipos y la entrega de valor.

- **Ortogonalidad:** (Invariante I2) El principio de que los componentes del sistema deben tener responsabilidades únicas y no solapadas.

- **OT1-OT3 (Tech Observables):** Observables tecnológicos especializados: OT1 Data Health, OT2 AI Performance, OT3 Process Effectiveness. Definidos `E8_Intelligent_Data_AI_Systems.md`. Renombrados de T1-T3 para evitar namespace collision con Templates T01-T22.

## P

- **Patrón:** Una solución reutilizable y probada a un problema común en un contexto determinado. KERNEL documenta 64 patrones en `A1_Patrones.md`: 50 base (P01-P50), 3 emergentes (P51-P53), 3 evolutivos (P54-P56), 5 security (P_SEC01-05), 3 CX (P_CX01-03).

- **Percepción (Dominio D2):** Uno de los cuatro dominios de KERNEL, responsable de observar, medir y entender el estado del sistema y su entorno.

- **Primitivo:** Uno de los 7 bloques de construcción fundamentales e irreducibles del modelo KERNEL: Actor (A), Flujo (F), Dato (D), Señal (S), Límite (L), Estado y Recurso (R). Ver `CORE/01_Primitivos.md`.

- **P_CX Patterns:** Patterns Customer Experience KERNEL-native: P_CX01 Flujo Valor Cliente, P_CX02 Eventos como Señales CX, P_CX03 Touchpoint Ownership. Operan sobre primitivos F, S, O2 (no inventa conceptos nuevos). Ver `A1_Patrones.md` §6.6.

- **P_GOV Patterns:** Patterns Gobierno Digital universales: P_GOV01 Life Events Approach, P_GOV02 Once-Only Principle, P_GOV03 Proactive Government. Ver `E2_Gov_Digital_Base.md` §5.

- **P_SEC Patterns:** Patterns Security enterprise-grade: P_SEC01 Defense in Depth, P_SEC02 Zero Trust, P_SEC03 Security as Code, P_SEC04 Shift-Left Security, P_SEC05 Incident Response Automation. Implementan mejoras SO1-SO5. Ver `A1_Patrones.md` §6.5.

## R

- **Readiness (R1-R5):** Framework evaluación preparación transformación: R1 Momentum (desire change), R2 Capabilities (skills), R3 Forces (stakeholder support), R4 Drivers (business case), R5 Catalysts (leadership). Score 0-5 cada, total 0-25. Ver `A4_Implementacion.md` §0.

- **Recurso:** (Primitivo R) Un activo necesario para que un flujo se ejecute. Puede ser tangible (dinero, servidores) o intangible (tiempo, conocimiento, software).

## S

- **Señal:** (Primitivo S) Interpretación meaningful de evento/dato. Ejemplo: S_High_Churn (interpretación de dato churn_rate >15%). Difiere de Evento E (ocurrencia cruda) y Dato D (measurement). Ver `CORE/01_Primitivos.md` §3A.

- **Security Observables (SO1-SO5):** Observables seguridad: SO1 Vulnerabilidades, SO2 Gestión Secretos, SO3 Control Acceso, SO4 Cumplimiento Normativo, SO5 Respuesta Incidentes. Complementan O1-O8, I1-I3. Peso 10% H_Score extended (ajustable por industry). Ver `D2_Percepcion.md` §8.

- **Smartness (C1-C6):** Modelo madurez inteligencia organizacional, estructurado en matriz 4 dominios × 6 niveles capacidad (24 celdas): C1 Opaco, C2 Reactivo, C3 Predecible, C4 Diagnóstico, C5 Prescriptivo, C6 Adaptativo. Ver `CORE/05_Smartness.md`.


## T

- **Touchpoint:** Punto interacción cliente ↔ organización en customer journey. Ejemplos: website landing page, checkout flow, support call. Cada touchpoint instrumentado con observable O2 (NPS/CSAT). Ver `T23_Customer_Journey_Map.md`.

- **Trazabilidad:** (Invariante I3) El principio de que cada elemento en el sistema debe estar conectado en una cadena causal desde el propósito estratégico hasta el valor entregado.

- **Track (Learning Path):** Ruta aprendizaje KERNEL especializada por rol: Executive (4-6 hrs), Architect (12-16 hrs), AI Engineer (8-12 hrs), Full (40-60 hrs). Ver `LEARNING_PATH.md`.

---

---

## Appendix: Acrónimos Frecuentes

| Acrónimo | Significado | Referencia |
|----------|-------------|------------|
| **ADR** | Architecture Decision Record | T13_Architecture_Decision_Record.md |
| **CDO** | Chief Digital Officer | E2_Gov_Digital_Base.md |
| **CISO** | Chief Information Security Officer | CORE/03_Arquitectura.md §6 |
| **CX** | Customer Experience | A1_Patrones.md §6.6 |
| **EA** | Enterprise Architecture | — |
| **GaaP** | Government as Platform | E2_Gov_Digital_Base.md §2 |
| **IR** | Incident Response | SO5, P_SEC05 |
| **MTTC** | Mean Time to Contain | SO5 (post-detection containment) |
| **MTTD** | Mean Time to Detect | SO5 (security incident detection) |
| **MTTP** | Mean Time to Patch | SO1 (vulnerabilities críticas) |
| **MVA** | Minimum Viable Architecture | D1_Arquitectura.md §0 |
| **MVD** | Minimum Viable Decision | D3_Decision.md §0 |
| **MVDG** | Minimum Viable Digital Government | E2_Gov_Digital_Base.md §0 |
| **MVO** | Minimum Viable Operations | D4_Operacion.md §0 |
| **MVP** | Minimum Viable Perception | D2_Percepcion.md §0 |
| **MVTD** | Minimum Viable Transformación Digital | E2_Chile_TDE.md §0 |
| **NPS** | Net Promoter Score | Observable O2 (Valor) |
| **OGD** | Open Government Data | E2_Gov_Digital_Base.md §3 |
| **RACI** | Responsible, Accountable, Consulted, Informed | P_CX03, T04_Team_Charter.md |
| **RICE** | Reach, Impact, Confidence, Effort | P31 (prioritization framework) |
| **SDA** | Sense-Decide-Act | CORE/02_Ciclo_Fundamental.md |
| **SIEM** | Security Information and Event Management | P_SEC05, SO5 |
| **SOAR** | Security Orchestration, Automation, Response | P_SEC05 |
| **TDE** | Transformación Digital del Estado (Chile) | E2_Chile_TDE.md |

---

*Este glosario v2.2 se actualiza con cada release KERNEL. Última actualización: 2025-11-03 (iteraciones 1-10 incorporadas).*