# CONTRIBUTING (Guía Contribuciones KERNEL)

**Versión:** 2.2.0  
**Estado:** Open for Contributions  
**Última Actualización:** 2025-11-03

---

## Bienvenido

Gracias por tu interés en contribuir a KERNEL. Este documento establece guidelines claros para submissions (patterns, templates, fixes, expansiones).

**Tipos de Contribuciones Aceptadas**:
1. **Bug fixes** (typos, links rotos, inconsistencias menores)
2. **New Patterns Base** (P72+, cross-domain en A1)
3. **New Patterns Domain-Specific** (P_SECTOR# en E3-E5, E9+)
4. **New Templates** (T24+)
5. **Dominios Especializados** (E9+, nuevas industrias)
6. **Traducciones** (español → inglés, otros idiomas)
7. **Casos Estudio** (R1, nuevos casos organizaciones)
8. **Mejoras Documentación** (clarificaciones, ejemplos)

**NO Aceptamos**:
- Cambios invariantes I1-I3 (core inmutable)
- Remoción primitivos (breaking changes requieren v3.0)
- Marketing content (KERNEL es técnico, pragmático)
- Propuestas sin evidencia empírica (al menos 1 caso real)

---

## Proceso Contribución

### 1. Antes de Contribuir

**Lee primero**:
- `README.md`: Entender KERNEL básico
- `CORE/00_Manifiesto.md` §0-§1: Positioning + Invariantes
- `VERSIONING.md`: Estrategia versioning, qué es breaking change
- Este documento completo

**Verifica**:
- [ ] Tu propuesta no existe ya (buscar en A1_Patrones.md para patterns base, E3-E5 para domain-specific, R6_Templates)
- [ ] Tu propuesta alineada con invariantes I1-I3
- [ ] Tienes evidencia empírica (al menos 1 caso aplicación real)
- [ ] Tu propuesta no duplica antipatrón existente (A2_Antipatrones.md para base, E3-E5 §10 para domain-specific)

---

### 2. Tipos Contribución Detallados

#### A. Bug Fixes (Minor)

**Qué califica**:
- Typos, gramática
- Links rotos
- Inconsistencias menores (ej: H_Score descrito diferente en 2 docs)
- Formatting markdown (tablas rotas)

**Proceso**:
1. Identifica bug específico (file + line number)
2. Propón fix (exact text change)
3. Submit issue/PR con:
   - **Title**: `[BUG] Brief description`
   - **Body**: File, line, current text, proposed fix, rationale
4. Review: <7 días
5. Merge: Patch release (v2.2.Z)

**Ejemplo Issue**:
```markdown
**Title**: [BUG] Cross-reference a sección inexistente en A1

**File**: APLICACION/A1_Patrones.md, line 693
**Current**: "Patrones extraídos de `DOMINIOS/D4_Operacion.md` §11.1"
**Proposed**: "Patrones fundamentados en `DOMINIOS/D4_Operacion.md` §11 Continuous Learning"
**Rationale**: Sección §11.1 no existe en D4, solo §11 (sin subsecciones numeradas)

Nota: Este issue fue corregido en v2.2.1
```

---

#### B. New Patterns Base (P72+)

**Qué califica**:
- Pattern aplicado ≥2 organizaciones exitosamente
- Cross-domain (aplica múltiples industrias, no sector-specific)
- Resuelve problema recurrente no cubierto P01-P71
- Evidencia ROI medible (ej: -30% cycle time)

**Nota Domain-Specific**: Si pattern es sector-specific (manufacturing, healthcare, financial), contribuir a E3-E5 §4-§9 (no A1). Ver §B2 abajo.

**Formato Template**:
```markdown
## Pattern P72: [Nombre Pattern]

**Categoría**: [Estructural/Procesal/Tecnológico/Decisional/IA/Security/CX/Otro]

**Problema**: [Descripción problema común, contexto]

**Solución**: [Cómo resolver, implementación pragmática]

**Cuándo Usar**: [Condiciones aplicabilidad, org size, madurez]

**Evitar Si**: [Contextos donde contraproducente]

**Evidencia Empírica**:
- Org 1: [Nombre anonimizado], [Industry], [Size], [Outcome metrics]
- Org 2: [Nombre anonimizado], [Industry], [Size], [Outcome metrics]

**Primitivos KERNEL Involucrados**: [A, F, D, S, E, L, R - cuáles usa]

**Observables Impactados**: [O1-O8, I1-I3, SO1-SO5 - cuáles mejora]

**Relación Patterns Existentes**:
- Complementa: [P01, P23, etc.]
- Conflicts: [Ninguno / P45 si...]
- Prerequisitos: [P18 IaC debe existir antes]

**Autor**: [Tu nombre/org], [Contacto opcional]
**Fecha Submission**: YYYY-MM-DD
**Validado por**: [Maintainer asigna post-review]
```

**Proceso**:
1. Draft pattern usando template arriba
2. Submit issue con draft
3. Review community (feedback 14 días)
4. Revisions (iterate based feedback)
5. Approval: Maintainer valida invariantes I1-I3, minimalidad, evidencia, cross-domain applicability
6. Merge: Minor release (v2.3.0), agregado A1_Patrones.md §[nueva sección] (si pattern base general)

**Criterios Aprobación**:
- ✅ Evidencia empírica ≥2 orgs
- ✅ Cross-domain applicability (no sector-specific)
- ✅ No duplica P01-P71 existentes ni P_SEC/P_CX
- ✅ Respeta minimalidad I1 (irreducible)
- ✅ Format correcto (tabla compatible A1)
- ✅ Primitivos claramente mapeados

**Criterios Rechazo**:
- ❌ Solo 1 caso aplicación (no generalizable)
- ❌ Duplica pattern existente (usar existente)
- ❌ Sector-specific (debe ir en E3-E5 o E9+, no A1)
- ❌ Demasiado específico tech (ej: "P_AWS_Lambda_Deploy" → usar P27 CI/CD genérico)
- ❌ Sin evidencia ROI (anecdótico)

---

#### B2. New Patterns Domain-Specific (P_SECTOR#)

**Qué califica**:
- Pattern específico sector (manufacturing, healthcare, financial, retail, etc.)
- Aplicado ≥2 orgs mismo sector exitosamente
- Evidencia ROI sector-specific

**Formato Template** (similar a P72+ pero con nomenclatura sector):
```markdown
## Pattern P_[SECTOR]#: [Nombre Pattern]

**Sector**: [Manufacturing/Healthcare/Financial/Retail/etc.]

**Problema**: [Específico sector]

**Solución**: [Implementación sector-specific]

**Cuándo Usar**: [Contexto sector]

**Evitar Si**: [Condiciones sector]

**Evidencia Empírica**:
- Org 1: [Sector-specific caso]
- Org 2: [Sector-specific caso]

**Conexión KERNEL**: [Primitivos + Observables + Patterns base relacionados]

**Métricas Sector**: [KPIs específicos sector]
```

**Proceso**:
1. Identificar sector target (E3 Manufacturing, E4 Healthcare, E5 Financial, E9+ nuevo)
2. Draft pattern usando template arriba
3. Submit issue/PR con evidencia ≥2 casos sector
4. Review: Maintainer valida relevancia sector, no-duplicación
5. Approval: Merge a documento sector (ej: E3_Manufactura.md §4-§9)
6. Merge: Minor release (v2.3.0), agregado E# §[patterns]

**Ejemplos**:
- E3_Manufactura: P_MFG1-8 (Digital Twin, Predictive Maintenance, etc.)
- E4_Salud: P_HEALTH1-8 (FHIR Interop, HIPAA, Telemedicine, etc.)
- E5_Financiero: P_FIN1-8 (Fraud Detection, KYC/AML, HFT, etc.)

**Nuevos Sectores** (E9+):
- E9_Retail: P_RETAIL1-10
- E9_Education: P_EDU1-8
- E9_Logistics: P_LOG1-12

---

#### C. New Templates (T24+)

**Qué califica**:
- Template usado ≥5 veces diferentes contextos
- Formato estructurado (YAML, Markdown, etc.)
- Complementa templates T01-T23 sin duplicar

**Formato Template**:
```markdown
# T24_[Nombre_Template]

**Versión:** 1.0.0
**Audiencia:** [Roles específicos]
**Patterns Aplicables:** [P01, P23, etc.]

---

## Propósito Template

[¿Qué problema resuelve? ¿Cuándo usar?]

---

## Estructura

[Secciones template, campos obligatorios/opcionales]

---

## Ejemplo Completado

[Ejemplo concreto llenado con datos ficticios pero realistas]

---

## Instrucciones Uso

[Step-by-step cómo completar template]

---

## Referencias KERNEL

[Links a CORE, DOMINIOS, APLICACION relevantes]
```

**Proceso**:
1. Draft template T24+
2. Submit con ≥1 ejemplo real (anonimizado si sensible)
3. Review: ¿Duplica T01-T23? ¿Útil genérico?
4. Approval: Minor release (v2.3.0), agregado REFERENCIA/R6_Templates/

---

#### D. Dominios Especializados (E9+)

**Qué califica**:
- Industria no cubierta E1-E8 (Digital, Gobierno, Manufactura, Salud, Financiero, E6 Template, E7 Enterprise Tech, E8 AI/Data)
- ≥300 líneas contenido específico sector
- Patrones específicos ≥5 (ej: E9_Retail → P_RETAIL1-10)
- Antipatrones específicos ≥3 (ej: AP_RETAIL1-5)
- Casos sector ≥2 documentados
- Mapping claro a CORE/DOMINIOS/APLICACION

**Formato Base** (usar E6_Template.md como starting point):
```markdown
# E9_[Sector] (Descripción breve)

**Versión:** 1.0.0
**Audiencia:** [Roles sector-specific]
**Dependencias**: CORE/01-08, DOMINIOS/D1-D4, APLICACION/A1-A5

---

## §0. QUICK START MV[Sector]

[Minimum Viable implementación sector, 4-8 semanas]

---

## §1. FUNDAMENTOS [SECTOR]

[Context sector, challenges específicos, frameworks relevantes]

---

## §2-§N. [SECCIONES SECTOR-SPECIFIC]

[Patterns, observables, casos sector]

---

## §FINAL. INTEGRACIÓN KERNEL

[Mapping D1-D4, primitivos sector, métricas específicas]

---

## Referencias Cruzadas

[Links a CORE, otros E1-E8 relevantes]
```

**Proceso**:
1. Draft E9+ usando E6_Template.md
2. Submit outline + §0 Quick Start (review feasibility)
3. Develop full content (iterar con maintainer)
4. Review community (30 días feedback período)
5. Approval: Minor release (v2.3.0), agregado DOMINIOS_ESPECIALIZADOS/

**Ejemplos E9+ Candidates**:
- E9_Retail: Omnichannel, inventory, CRM
- E9_Education: LMS, student lifecycle, accreditation
- E9_Logistics: Supply chain, fleet management, last-mile
- E9_Energy: Grid management, renewable integration, IoT sensors
- E9_Construction: Project management, safety, subcontractors

---

#### E. Traducciones

**Idiomas Prioritarios**:
1. **Inglés** (universal, highest priority)
2. Español (ya existe)
3. Francés
4. Portugués (Brasil)
5. Alemán

**Proceso**:
1. Identifica documento traducir (empezar README, CORE/00, INDEX)
2. Submit translation pull request
3. Review: Native speaker valida calidad
4. Merge: Patch release (v2.2.Z)
5. Maintain: Traducciones actualizan con cada minor release

**Estructura Folders**:
```
/KERNEL/
  README.md (español, default)
  README.en.md (inglés)
  README.fr.md (francés)
  CORE/
    00_Manifiesto.md (español)
    00_Manifiesto.en.md (inglés)
  ...
```

**Guidelines Traducción**:
- Mantener términos técnicos en inglés si no hay equivalente claro (ej: "pattern", "observable")
- Ejemplos adaptar a contexto cultural (ej: empresas US → empresas locales)
- Links mantener a versión español (cambiar solo si existe versión idioma destino)

---

#### F. Casos Estudio (R1)

**Qué califica**:
- Transformación completa org usando KERNEL
- Timeline ≥6 meses (no pilotos cortos)
- H_Score before/after documentado
- ROI medible (savings, revenue, risk mitigation)
- Org dispuesta compartir learnings (anonimizado OK)

**Formato Caso** (usar R1_Casos.md estructura existente):
```markdown
### Caso [N]: [Org Anonimizada] - [Industry]

**Context**:
- Industry: [Tech, Finance, Gobierno, etc.]
- Size: [Headcount, revenue]
- Problem: [H_Score inicial, gaps críticos]

**Solution Applied**:
- KERNEL version: v2.2
- Implementation: [Fases, timeline]
- Patterns key: [P01, P23, P_SEC01, etc.]
- Observables instrumentados: [O1-O8, I1-I3, SO1-SO5]

**Results**:
- H_Score: [Before] → [After] (change: +X points)
- ROI: [Savings + Revenue + Risk = $Y]
- Timeline: [Months start→finish]
- Lessons Learned: [3-5 bullets pragmatic]

**Quotes** (opcional):
> "[CTO/CEO testimonial anonimizado]"

**Evidence**:
- Screenshots dashboards (anonimizados)
- Métricas before/after (graphs)
- Architecture diagrams
```

**Proceso**:
1. Contact maintainer (email/GitHub)
2. NDA si sensible (mantener confidencialidad org)
3. Draft caso con data anonymized
4. Review: Validate H_Score calculation, ROI claims
5. Approval: Minor release (v2.3.0), agregado R1_Casos.md
6. Opcional: Case study spotlight (blog, conference talk)

---

### 3. Submission Process (GitHub/Email)

**Opción A: GitHub Pull Request** (preferido si público)
1. Fork repository KERNEL
2. Create branch: `feature/pattern-p65-name` o `fix/typo-d2-line-142`
3. Make changes following templates arriba
4. Commit: Descriptive message (ej: `Add P65 Circuit Breaker pattern with 2 case studies`)
5. Push to fork
6. Open Pull Request:
   - Title: `[PATTERN/TEMPLATE/FIX/DOMAIN] Brief description`
   - Description: Template completado, rationale, evidence
7. Wait review (7-30 días depending complexity)
8. Address feedback (iterate)
9. Approval → Merge → Credited in CHANGELOG

**Opción B: Email Submission** (si preferencia privacidad)
1. Email: kernel-contributions@[domain] (replace with actual)
2. Subject: `[CONTRIBUTION] Type - Brief description`
3. Attachment: Draft markdown file(s)
4. Body: Brief intro, rationale, evidence
5. Response: <7 días acknowledgment, 7-30 días review
6. Iterate via email
7. Approval → Published próximo release

---

### 4. Review Criteria

**Maintainer Checklist**:

**Invariantes (Obligatorio)**:
- [ ] **I1 Minimalidad**: ¿Propuesta irreducible? ¿Agrega complejidad innecesaria?
- [ ] **I2 Ortogonalidad**: ¿Overlap con existente? ¿Responsabilidad única clara?
- [ ] **I3 Trazabilidad**: ¿Conexión propósito → valor explicitable?

**Principios (Recomendado)**:
- [ ] **P1 Parsimonia**: ¿Solución minimal viable? ¿Evita over-engineering?
- [ ] **P2 Pragmatismo**: ¿Ejecutable realista? ¿No solo teoría?
- [ ] **P3 Evidencia**: ¿Data empírico ≥2 casos? ¿ROI medible?

**Quality**:
- [ ] Markdown formatting correcto (tablas, YAML, links)
- [ ] Typos mínimos (spell-check pass)
- [ ] Cross-references actualizadas (si nueva sección, update INDEX.md)
- [ ] Versioning correcto (PATCH vs MINOR vs MAJOR)

**Documentation**:
- [ ] Changelog entry (VERSIONING.md)
- [ ] References updated (README, INDEX si aplica)
- [ ] Glosario updated (R5 si nuevos términos)

---

### 5. Recognition & Credits

**Contributors Reconocidos**:
- **CHANGELOG**: Mention `Contributors: @username1, @username2` en cada release
- **CREDITS.md**: Lista acumulativa todos contributors (agregado futuro)
- **Case Studies**: Autor citado en R1_Casos.md (opcional, si desean visibilidad)

**Tipos Contribución Value**:
- Bug fixes: Small recognition (thank you mention)
- New Patterns: Medium recognition (author field, changelog)
- New Domains E9+: High recognition (author field, case study spotlight, opcional blog post)
- Major refactors: Highest recognition (co-author próximo paper/book si KERNEL se publica)

**No Compensation Monetary**:
- KERNEL es open framework (si aplica), contribuciones voluntarias
- Recognition es reputational (portfolio, LinkedIn, conferences)

---

### 6. Code of Conduct

**Expectations**:
- **Respectful**: Feedback constructivo, no personal attacks
- **Evidence-based**: Claims con data, no opinions sin fundamento
- **Collaborative**: Iterate based feedback, no defensive
- **Pragmatic**: Focus business value, no academic debates estériles

**Unacceptable**:
- Harassment, discrimination, toxic behavior
- Spam, self-promotion excesiva (1 mention OK, repeated no)
- Plagiarism (citar fuentes, no copiar sin attribution)
- Bad faith arguments (trolling, sabotage)

**Enforcement**:
- Warning (first offense)
- Ban temporal (repeat offense)
- Ban permanente (severe violations)

---

### 7. FAQ Contributions

**Q1: ¿Puedo proponer cambio a invariantes I1-I3?**  
**A**: No en v2.X. Invariantes son core inmutable. Cambios requieren v3.0 (MAJOR breaking), y deben tener consenso community amplio (≥80% support). Proposal debe demostrar fallo fundamental I1-I3 con evidencia ≥10 casos.

**Q2: ¿Cuánto tiempo toma review?**  
**A**: Bug fixes: <7 días. Patterns: 14-30 días. Domains E9+: 30-60 días (más complejo, requiere community feedback amplio).

**Q3: ¿Qué pasa si mi propuesta rechazada?**  
**A**: Feedback explicativo con rationale. Opciones: (1) Iterate based feedback, re-submit. (2) Fork KERNEL, create variant (respectar license). (3) Publicar independently como extension (ej: "KERNEL+ Retail by Company X").

**Q4: ¿Puedo contribuir si no soy experto KERNEL?**  
**A**: Sí. Bug fixes bienvenidos cualquier nivel. Patterns/Domains requieren entender CORE (read LEARNING_PATH Executive o Architect track primero).

**Q5: ¿KERNEL acepta contribuciones empresas consultoras?**  
**A**: Sí, pero no marketing content. Patterns basados experiencia cliente real OK (anonimizar). Self-promotion explícita no (ej: "Use our consulting services" → no).

**Q6: ¿Cómo manejo IP/confidencialidad al contribuir caso cliente?**  
**A**: Anonimizar org (Org A, Tech Startup 200p, etc.). Métricas OK si aggregated/disguised. NDA disponible si necesario. Maintainer respeta confidencialidad.

---

### 8. Roadmap Contributions Prioritarias

**v2.3 (Q1 2026) - Looking For**:
- **Translations**: README + CORE/00 a inglés (highest priority)
- **E9 Retail**: Domain especializado retail (P_RETAIL1-10: omnichannel, inventory, personalization, etc.)
- **Patterns Base**: P72+ cross-domain (si aplicables múltiples sectores)
- **Patterns Manufacturing**: P_MFG9+ expansion (E3)
- **Templates Financial**: T24 Budget Template, T25 ROI Calculator (Excel/Google Sheets)

**v3.0 (Q3 2026) - Research Phase**:
- **M7-M8 Delegation**: Swarm Intelligence, Autonomous Org (requiere research, no aceptar aún)
- **Observables Expansion**: 30+ observables sector-specific (prepare proposals, no merge hasta v3.0)

---

## Contact

**Maintainer**: [KERNEL Core Team]  
**Email Contributions**: kernel-contributions@[domain]  
**GitHub**: [Repository URL si público]  
**Community**: [Discord/Slack/Forum si existe]

---

## Changelog CONTRIBUTING.md

**v1.0.0** (2025-11-03): Initial CONTRIBUTING.md
- Guidelines types contributions (bugs, patterns, templates, domains, translations, cases)
- Submission process (GitHub PR / Email)
- Review criteria (invariantes, principios, quality)
- Recognition policy
- Code of Conduct
- FAQ

---

**Gracias por contribuir a KERNEL. Juntos construimos el framework más minimal, ejecutable y evidence-based para organizaciones adaptativas.** 🚀
