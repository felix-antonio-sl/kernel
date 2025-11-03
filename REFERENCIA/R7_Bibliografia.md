# R7_Bibliografia

**Versión:** 2.0.0  
**Estado:** Completo  
**Propósito:** Referencias fuentes KERNEL v2.0 (tech domains, TDE Chile, standards internacionales)

---

## FUENTES PRIMARIAS v2.0

### Tech Domains (7 Sources)

**BAD.md** (Business Application Development):

- **Líneas**: 101
- **Cobertura**: E7 §2-§3-§5-§7 (patterns arquitectónicos, stack, DevOps, NFRs)
- **Temas**: Monolito vs Microservices, Backend/Frontend stacks, CI/CD, Observability, Shift-Left Security

**UXUI.md** (UX/UI Trends Enterprise):

- **Líneas**: 78
- **Cobertura**: E7 §4 fusionado completo (modern layouts, interaction models, accessibility, AI-assisted UX, multi-device, data viz, design systems)
- **Temas**: Progressive disclosure, conversational interfaces, WCAG, dark mode, command palettes, real-time collaboration

**DATA.md** (Data-as-Product Architecture):

- **Líneas**: 313
- **Cobertura**: E8 §4 DATA completo (lifecycle, contracts, bronze/silver/gold, lineage, DQ, FinOps, MDM/RDM, DW/BI, MLOps)
- **Temas**: DAMA DMBOK, Data Mesh, lakehouse, OpenLineage, Great Expectations, policy-as-code (OPA/Rego)

**OCE.md** (Orquestación Cognitiva Empresarial):

- **Líneas**: 161
- **Cobertura**: E8 §5 AI Orchestration completo (model serving, RAG, agents, guardrails, evaluation, multi-agent)
- **Temas**: vLLM/TGI/SGLang runtimes, autonomy spectrum, faithfulness, OWASP Top-10 LLMs, FinOps IA

**KNOW.md** (Knowledge Management):

- **Líneas**: 188
- **Cobertura**: E8 §6 KM+RAG completo (framework 16 celdas ISO 30401, curation pipeline RAG 5 fases, roles KM, evaluation)
- **Temas**: Connect/Collect, chunking estructural, indexación híbrida (BM25+vector), reranking, citations mandatory

**BPA.md** (Business Process Automation):

- **Líneas**: 143
- **Cobertura**: E8 §7 Process Automation completo (taxonomía BPM/BPA/RPA/IPA, BPMN, sagas, HITL, CoE RPA)
- **Temas**: Orchestration vs choreography, invoice processing pipeline, governance RPA, anti-patterns (automatizar rotos, RPA martillo)

**SIGMA.md** (Supradominio Integrador):

- **Líneas**: 293
- **Cobertura**: E8 §3 Contracts (absorbed), §1 meta-principios, §2 arquitectura
- **Temas**: Contracts unificados 4 tipos (datos, proceso, agente, conocimiento), espectros autonomía/responsabilidad/interacción, policy-as-code

**Total Tech Domains**: 1,277 líneas source → 3,170 líneas E7-E8 (expansion 2.5×, integration + examples + KERNEL coherence)

---

### TDE Chile (4 Sources Gobierno Digital)

**kb_tde_910** (Estándares y Guías Buenas Prácticas):

- **Líneas**: 2,984
- **Cobertura**: E2 §3-§4-§5-§6-§10 (40% usado, invariantes extracted)
- **Temas**: MGDE (12 dims, 52 preguntas, 4 niveles madurez), Datos Abiertos (DCAT, formatos, licencias, metadatos 3 niveles), Metadatos Docs/Expedientes (29+46, listas controladas), Anonimización (4 enfoques, matriz riesgo), Calidad Web (20 dims, 14 recs diseño servicios), Voz/Tono (12 reglas estilo)

**kb_tde_920** (Estrategias y Políticas Fundamentales):

- **Líneas**: ~1,500 (estimado)
- **Cobertura**: E2 §1-§2 (100%)
- **Temas**: Estrategia GobDigital 2030 (6 ejes, visión OCDE), Estrategia Datos Estado (3 ejes: ecosistema, personas, tecnología), Estrategia Identidad Digital (modelo híbrido, corto/mediano plazo), Estrategia Capacitación TD (7 perfiles prioritarios)

**kb_tde_940** (Gobernanza y Gestión Institucional):

- **Líneas**: ~1,200 (estimado)
- **Cobertura**: E2 §7 (100%)
- **Temas**: Institucionalidad TIC (SGD, ANCI, roles CTD), Sistema TD PMG 2025 (4 etapas, 3 instrumentos: CPAT/MGDE/Calidad Web), Gestión Proyectos TIC (metodología fases, anexos), EVALTIC (proceso evaluación, orientaciones formulación, criterios compra, seguimiento PMO)

**kb_tde_960** (Marco Legal, Normas Técnicas, Protección Datos, IA):

- **Líneas**: ~4,300 (estimado)
- **Cobertura**: E2 §1-§8-§9 (100%)
- **Temas**: Ley 21.658 (Crea SGD), Ley 21.180 (TD Estado, Arts modificados), Ley 19.880 (Bases PA, consolidada), DS 4/2020 (Reglamento 21.180), 6 NTs DS 7-12/2023 (Seguridad, Notificaciones, Autenticación, Docs/Expedientes, Calidad, Interoperabilidad), Proyecto Ley IA (clasificación riesgo, principios, gobernanza, sandboxes), Ley 21.719 (Protección Datos, ARCO+, decisiones automatizadas Art. 8 bis, EIPD)

**Total TDE Chile**: ~10,000 líneas source → 1,850 líneas E2 (selection ratio 18.5%, invariantes 47 embedded, parsimonia extrema)

---

## STANDARDS INTERNACIONALES

### Enterprise Architecture & Digital Transformation

- **TOGAF**: The Open Group Architecture Framework (enterprise architecture methodology)
- **Zachman Framework**: Enterprise ontology (2D matrix, interrogatives × stakeholders)
- **SAFe** (Scaled Agile Framework): Large-scale agile (PI planning, ARTs, value streams)
- **DAMA DMBOK** (Data Management Body of Knowledge): Data governance, quality, architecture
- **COBIT**: Control Objectives for Information and Related Technologies (IT governance)

**KERNEL Diferenciación**: Minimalidad extrema (I1), IA nativa (M1-M6 delegación), ejecutabilidad (templates copy-paste), observables cuantitativos (H_Score), trazabilidad completa (10 capas).

### Data & AI

- **W3C DCAT** (Data Catalog Vocabulary): Metadatos interoperables catálogos
- **Dublin Core**: 15 propiedades metadatos recursos electrónicos
- **OpenLineage**: Data lineage standard (events START/COMPLETE/FAIL)
- **Great Expectations**: Data quality framework Python
- **ISO 30401**: Knowledge Management Systems (framework 16 celdas, usado E8 §6.1)
- **OWASP Top-10 LLMs**: Security vulnerabilities AI (prompt injection, data exfiltration, model theft)

### Process & Quality

- **ISO 19510** (BPMN 2.0): Business Process Model & Notation
- **ISO 9001**: Quality Management Systems
- **Six Sigma**: DMAIC, DPMO metrics
- **ISO 15489**: Records management
- **ISO 23081**: Metadata for records

### Healthcare

- **HL7 FHIR** (Fast Healthcare Interoperability Resources): R4/R5
- **HIPAA**: Health Insurance Portability & Accountability Act (Privacy Rule, Security Rule)
- **DICOM**: Digital Imaging & Communications in Medicine
- **ICD-10**: International Classification of Diseases
- **SNOMED CT, LOINC, RxNorm**: Clinical terminologies

### Finance

- **Basilea III**: Capital requirements, liquidity ratios
- **SOX**: Sarbanes-Oxley (US financial reporting, internal controls)
- **MiFID II**: Markets in Financial Instruments Directive (EU)
- **Dodd-Frank**: US financial reform
- **FIX Protocol**: Financial Information eXchange (trading)

### Manufacturing

- **ISO 45001**: Occupational Health & Safety
- **ISO 14001**: Environmental Management
- **IATF 16949**: Automotive quality
- **HACCP, ISO 22000**: Food safety

### Gobierno Digital (Chile)

- **Ley 21.180** (Transformación Digital Estado)
- **Ley 21.658** (Crea Secretaría Gobierno Digital)
- **Ley 19.880** (Bases Procedimientos Administrativos)
- **DS 7-12/2023**: 6 Normas Técnicas (Seguridad, Notificaciones, Autenticación, Docs/Expedientes, Calidad, Interoperabilidad)
- **Proyecto Ley IA** (Chile, tramitación 2025)
- **Ley 21.719** (Protección Datos Personales, vigencia 2026)

### Organizaciones Referencia

- **OCDE**: Digital Government Index, Data-Driven Public Sector
- **Naciones Unidas**: E-Government Survey
- **Banco Mundial**: Data for Better Lives
- **BID**: Guía Transformación Digital Gobierno
- **European Commission**: GDPR, EU AI Act
- **McKinsey**: Digital transformation research
- **Google**: DORA metrics (DevOps Research & Assessment), SRE (Site Reliability Engineering)

---

## LECTURAS RECOMENDADAS (Orden Sugerido)

### Foundational (KERNEL Prerequisites)

1. **Team Topologies** (Matthew Skelton, Manuel Pais) - Org design, Conway's Law, cognitive load
2. **Accelerate** (Nicole Forsgren, Jez Humble, Gene Kim) - DORA metrics, DevOps excellence
3. **Site Reliability Engineering** (Google) - SLOs, error budgets, toil reduction
4. **Domain-Driven Design** (Eric Evans) - Bounded contexts, ubiquitous language
5. **Lean Enterprise** (Jez Humble, Joanne Molesky, Barry O'Reilly) - Flow, hypothesis-driven

### Data & AI (E8 Deep-Dive)

6. **Data Management at Scale** (Piethein Strengholt) - Data mesh, data-as-product
7. **Designing Data-Intensive Applications** (Martin Kleppmann) - Distributed systems, consistency, replication
8. **Building Machine Learning Powered Applications** (Emmanuel Ameisen) - ML lifecycle, evaluation
9. **Designing Machine Learning Systems** (Chip Huyen) - MLOps, deployment, monitoring
10. **The Big Book of MLOps** (Databricks) - Lakehouse, feature stores, model registry

### Process & Knowledge

11. **Business Process Management** (Mathias Weske) - BPMN, workflow patterns
12. **The Definitive Guide to DAX** (Alberto Ferrari, Marco Russo) - BI, semantic layers
13. **Knowledge Management in Theory & Practice** (Kimiz Dalkir) - KM frameworks, ISO 30401

### Gobierno Digital (E2 Deep-Dive)

14. **Estrategia Gobierno Digital 2030** (SGD Chile) - 6 ejes, iniciativas
15. **Marco Gestión Datos Estado (MGDE)** (SGD, GobLab UAI) - 12 dimensiones
16. **Guía Implementación Institucionalidad TIC** (SGD) - Roles, plataformas, Sistema TD
17. **OCDE Digital Government Index** - Benchmarks internacionales

---

**KERNEL v2.0**: Framework empresarial más completo que existe (EA + DX + Tech + Gov, único 100% TDE Chile).

**Para profundizar**: Ver `CHANGELOG_v2.0.md` (cambios detallados), `CONTEXTO_SESION_v2.0.md` (specs completas), `RADICAL_PLUS_PLAN_v2.0.md` (plan maestro).
