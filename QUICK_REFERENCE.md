# KERNEL Quick Reference Card (Cheat Sheet)

**Versión:** 2.2.0 | **1 página** | **Imprimir/guardar para consulta rápida**

---

## 7 Primitivos Universales

| Primitivo | Símbolo | Definición | Ejemplo |
|-----------|---------|------------|---------|
| **Actor** | A | Entidad ejecuta acción | Humano, máquina, IA agent |
| **Flujo** | F | Secuencia transforma inputs → outputs | CI/CD pipeline, customer journey |
| **Dato** | D | Información reduce incertidumbre | Métrica, log, evento |
| **Señal** | S | Interpretación meaningful dato/evento | S_High_Churn (>15%) |
| **Evento** | E | Ocurrencia discreta cambia estado | E_Deploy_Completed |
| **Límite** | L | Interfaz separa componentes | L1 Recursos, L2 Autoridad, L3 Constraints |
| **Recurso** | R | Activo necesario para flujo | Dinero, servidores, tiempo, conocimiento |

---

## 4 Dominios Ortogonales

| Dominio | Responsabilidad | Output Clave | Métricas |
|---------|-----------------|--------------|----------|
| **D1 Arquitectura** | Estructura (quién, qué, cómo organizamos) | Org chart, RACI | A_Score (clarity, balance, authority) |
| **D2 Percepción** | Sensado (detectar estado interno/externo) | H_Score, dashboards | 16 observables (O1-O8, I1-I3, SO1-SO5) |
| **D3 Decisión** | Estrategia (planificar, priorizar, OKRs) | Roadmaps, portfolio | D_Score (alignment, prioritization) |
| **D4 Operación** | Ejecución (flujos valor, delivery) | Features shipped, CI/CD | O_Score (velocity, quality, efficiency) |

---

## H_Score (0-100) - Health Organizacional

**Fórmula Base**: Weighted avg 11 observables (O1-O8, I1-I3)

**Fórmula Extended**: 70% O1-O8 + 20% I1-I3 + 10% SO1-SO5 (security)

### 11 Observables Base

**Externos (O1-O8)**:
1. O1 Satisfacción Cliente (NPS)
2. O2 Valor Entregado (revenue, adoption)
3. O3 Sostenibilidad Financiera (runway, profitability)
4. O4 Eventos Críticos (incidents, outages)
5. O5 Market Position (competidores, share)
6. O6 Regulaciones (compliance, audits)
7. O7 Alianzas (partners, ecosistema)
8. O8 Reputación (brand, glassdoor)

**Internos (I1-I3)**:
- I1 Velocidad Decisional (cycle time decisions)
- I2 Salud Talento (retention, engagement)
- I3 Eficiencia Flujo (lead time, throughput)

### 5 Security Observables (SO1-SO5)

- SO1 Vulnerabilidades (MTTP <7 días)
- SO2 Gestión Secretos (vault adoption, rotation)
- SO3 Control Acceso (MFA, privileged accounts)
- SO4 Cumplimiento (certifications, audit findings)
- SO5 Incident Response (MTTD, MTTC)

### Interpretación H_Score

- **90-100**: Excelente (NPS >50, churn <5%)
- **75-89**: Bueno (NPS 30-50, churn 5-10%)
- **60-74**: Aceptable (NPS 10-30, churn 10-15%)
- **45-59**: Pobre (NPS <10, churn >15%)
- **<45**: Crisis (activar P52 Crisis Governance)

---

## 6 Modos Delegación (M1-M6)

| Modo | Nombre | IA Role | Human Role | Ejemplo |
|------|--------|---------|------------|---------|
| **M1** | Monitor | Observa | Actúa 100% | Dashboard metrics |
| **M2** | Inform | Alerta | Decide + actúa | Anomaly detection |
| **M3** | Enable | Sugiere | Valida + actúa | Copilot coding |
| **M4** | Control | Decide | Valida + actúa | Auto-prioritization |
| **M5** | Co-produce | Colabora | Co-crea | Pair programming IA |
| **M6** | Execute | Autónomo | Supervisa | Auto-scaling, rollback |

---

## 6 Niveles Smartness (C1-C6)

| Nivel | Nombre | Capacidad | Ejemplo D2 Percepción |
|-------|--------|-----------|----------------------|
| **C1** | Opaco | No visibilidad | Sin dashboards |
| **C2** | Reactivo | Responde post-crisis | Alertas manuales |
| **C3** | Predecible | Patrones históricos | Dashboards básicos |
| **C4** | Diagnóstico | Root cause | Anomaly detection |
| **C5** | Prescriptivo | Recomienda acción | IA sugiere fixes |
| **C6** | Adaptativo | Auto-ajuste | IA auto-remedia |

---

## Patterns Top 10 (Quick Wins)

| ID | Patrón | Problema | Solución | ROI Típico |
|----|--------|----------|----------|------------|
| **P01** | Single Source of Truth | Docs dispersos | Central repo (Notion, Confluence) | -50% tiempo búsqueda |
| **P18** | Infrastructure as Code | Configs manuales | Terraform/Pulumi versionado | -40% deploy time |
| **P27** | Continuous Delivery | Deploy manual | CI/CD automatizado | +300% deploy frequency |
| **P31** | RICE Scoring | Priorización subjetiva | (Reach × Impact × Confidence) / Effort | +40% value delivered |
| **P38** | Anomaly Detection | Incidents reactivos | ML detecta early | MTTD -70% |
| **P42** | Quality Gates Automated | Bugs prod | SAST/DAST CI/CD blocks | -60% bugs escaped |
| **P_SEC01** | Defense in Depth | Single layer vulnerable | Múltiples capas defensa | Breach risk -70% |
| **P_SEC04** | Shift-Left Security | Security late | Security desde design | Vuln cost -80% |
| **P_CX01** | Flujo Valor Cliente | Inside-out design | Outside-in journey | NPS +20 points |
| **P52** | Crisis Governance | Crisis caos | War room, daily standups | Recovery time -50% |

---

## 3 Invariantes NO NEGOCIABLES

1. **I1 Minimalidad**: Todo elemento irreducible (eliminar cualquiera destruye capacidades)
2. **I2 Ortogonalidad**: Dominios sin overlap (responsabilidad única clara)
3. **I3 Trazabilidad**: Todo conecta propósito → valor (no islas información)

---

## Decision Modes (D1-D4)

| Mode | Nombre | Complejidad | Ejemplo |
|------|--------|-------------|---------|
| **D1** | Direct Feedback | Automático | Thermostat |
| **D2** | Rule-Based | Condicional | IF-THEN rules |
| **D3** | Associative | Pattern fuzzy | ML classification |
| **D4** | Analytical | Investigación iterativa | Strategic planning |

---

## Awareness Levels (S1-S3)

| Level | Nombre | Capacidad |
|-------|--------|-----------|
| **S1** | Detect | Captura facts crudos |
| **S2** | Comprehend | Síntesis meaningful |
| **S3** | Project | Predice estados futuros |

---

## Quick Start (30 min)

1. **Lee Positioning** (5 min): `CORE/00_Manifiesto.md` §0
2. **Calcula H_Score** (15 min): `T05_Assessment.md` self-assessment
3. **Identifica 3 Patterns** (10 min): `A1_Patrones.md` según gaps H_Score

---

## Learning Paths

| Rol | Track | Tiempo | Output |
|-----|-------|--------|--------|
| **CEO, C-level** | Executive | 4-6 hrs | Business case |
| **CTO, Arquitecto** | Architect | 12-16 hrs | Roadmap 12m |
| **ML Engineer** | AI Engineer | 8-12 hrs | Delegation strategy |
| **Consultor** | Full | 40-60 hrs | Expertise completo |

Ver: `LEARNING_PATH.md`

---

## ROI KERNEL (Example Org 50-200p)

**Investment**: $500K Year 1, $250K/year ongoing

**Annual Value**: $8.3M/year
- Cost Savings: $5.34M (downtime, productivity, rework, infra, consultants)
- Revenue Increase: $1.755M (time-to-market, churn reduction, upsell)
- Risk Mitigation: $1.21M (breach, compliance, project failure, tech debt)

**ROI Year 1**: 1,561% | **Payback**: <1 month | **NPV 3-year**: $19.76M

Ver: `A5_Medicion.md` §10

---

## Recursos Clave (Links Rápidos)

- **README**: Portal principal, quick start
- **INDEX**: Navegación completa 53 archivos
- **CORE/00**: Manifiesto + positioning
- **A1_Patrones**: 64 patterns catálogo
- **A3_Diagnostico**: Framework assessment
- **A4_Implementacion**: Playbook 6 fases
- **VERSIONING**: Changelog + roadmap v2.3, v3.0
- **CONTRIBUTING**: Guidelines contribuciones
- **LEARNING_PATH**: 4 tracks adoption

---

## Support & Community

- **Email Contributions**: kernel-contributions@[domain]
- **Issues/PRs**: [GitHub URL]
- **Documentation**: Leer `R4_FAQ.md` (60 preguntas)
- **Glosario**: `R5_Glosario.md` (43 términos + 23 acrónimos)

---

## Version Info

- **Current**: v2.2.0 (2025-11-03)
- **Next Minor**: v2.3.0 (Q1 2026) - Translations, E9 Retail, Financial templates
- **Next Major**: v3.0.0 (Q3 2026) - AI-Native v2 (M7-M8, 30+ observables)

---

**Imprime esta página y mantenla cerca durante implementación KERNEL.** 📋

*Quick Reference v2.2.0 - Para detalle completo, consultar documentos fuente.*
