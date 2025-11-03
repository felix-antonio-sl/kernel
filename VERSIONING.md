# VERSIONING (Estrategia Versionado KERNEL)

**Versión Actual:** 2.2.1  
**Estado:** Production Ready  
**Fecha Release:** 2025-11-03

---

## Semantic Versioning

KERNEL usa **Semantic Versioning 2.0.0** (semver.org):

```
MAJOR.MINOR.PATCH (ej: 2.2.0)
```

### Incremento Versión

**MAJOR (X.0.0)**: Breaking changes - Incompatibilidad backward
- Cambio invariantes (I1-I3)
- Remoción primitivos
- Reestructuración dominios D1-D4
- **Ejemplo**: v1.0 → v2.0 (agregado Señal S como primitivo 7, breaking)

**MINOR (x.Y.0)**: New features - Compatible backward
- Nuevos patterns (P51-P64)
- Nuevos observables (SO1-SO5)
- Nuevos documentos (LEARNING_PATH.md, T23)
- Expansiones secciones (CORE/03 §6 Security)
- **Ejemplo**: v2.1 → v2.2 (agregado P_CX, LEARNING_PATH, E2 refactor)

**PATCH (x.y.Z)**: Bug fixes - Compatible backward
- Typos, clarificaciones
- Links rotos fixed
- Inconsistencias menores
- **Ejemplo**: v2.2.0 → v2.2.1 (fix typos R5_Glosario)

---

## Changelog Consolidado

### v2.2.1 (2025-11-03) - Consistency Fixes

**Theme**: Internal consistency improvements + editorial standardization

**Fixes Críticos**:
1. **H_Score Formula Inconsistency Resolved** (🔴 Critical)
   - `D2_Percepcion.md` §8: Reemplazada fórmula extended simplificada con versión matemáticamente correcta
   - Fórmula detallada: 90% weighted base + 10% avg(SO1-SO5)
   - Fórmula simplificada (aproximación): 0.63*avg(O1-O8) + 0.18*avg(IN1-IN3) + 0.10*avg(SO1-SO5)
   - Agregadas notas sobre diferencia entre detallada vs simplificada
   - `CORE/03_Arquitectura.md` §6.5: Sincronizada con D2 §8
   - `R5_Glosario.md`: Actualizada definición H_Score con referencias precisas
   - Issue documentado en CONTRIBUTING.md v2.2.0 línea 69-75 ahora resuelto

2. **Cross-Reference Fix** (🟡 High)
   - `A1_Patrones.md` §14: Corregida referencia a `D4_Operacion.md` §11.1 (no existía)
   - Reemplazada con referencia correcta a §11 "Continuous Learning"
   - Clarificada fundamentación en Gall's Law y pattern language

**Mejoras Editoriales**:
3. **Pattern Naming Clarification** (🟡 High)
   - `A1_Patrones.md` §1: Agregada nota explicativa nomenclatura patterns
   - Aclarada convención: P01-P56 (secuencial) + P_SEC/P_CX (prefijos domain-specific)
   - Total count documentado explícitamente: 64 patterns (56 + 5 + 3)
   - Futuro: Nuevos patterns especializados usarán prefijos (P_AI, P_DATA, etc.)

4. **Observable Notation Standardization** (🟢 Moderate)
   - Estandarización IN1-IN3 (internos) vs I1-I3 usado ocasionalmente
   - Rationale: Evita confusión con Invariantes I1-I3 (Minimalidad, Ortogonalidad, Trazabilidad)
   - Archivos actualizados:
     * `A5_Medicion.md`: Todas tablas y fórmulas (5 instancias)
     * `A1_Patrones.md`: Tablas CX patterns y P52 (4 instancias)
     * `A2_Antipatrones.md`: Tablas y diagnóstico (7 instancias)
     * `A4_Implementacion.md`: Input spec (1 instancia)
   - Notación canonical: **IN1** (Velocidad Decisional), **IN2** (Salud Talento), **IN3** (Eficiencia Flujo)

5. **CONTRIBUTING.md Update**
   - Actualizado ejemplo bug fix (issue H_Score ya resuelto → nuevo ejemplo)
   - Refleja estado post-fixes v2.2.1

**Archivos Modificados**: 7 archivos
- `DOMINIOS/D2_Percepcion.md` (H_Score extended formula)
- `CORE/03_Arquitectura.md` (H_Score security integration)
- `REFERENCIA/R5_Glosario.md` (H_Score definition)
- `APLICACION/A1_Patrones.md` (cross-ref + nomenclatura + IN notation)
- `APLICACION/A2_Antipatrones.md` (IN notation)
- `APLICACION/A4_Implementacion.md` (IN notation)
- `APLICACION/A5_Medicion.md` (IN notation)
- `CONTRIBUTING.md` (ejemplo actualizado)
- `VERSIONING.md` (este changelog)

**Breaking Changes**: Ninguno (backward compatible)

**Migración v2.2.0 → v2.2.1**: 
- **Organizaciones usando H_Score extended**: Revisar implementación. Si usaban fórmula simplificada `0.70*avg(O) + 0.20*avg(I) + 0.10*avg(SO)`, actualizar a `0.63*avg(O) + 0.18*avg(IN) + 0.10*avg(SO)` o mejor aún, implementar fórmula detallada completa (ver D2 §8).
- **Dashboards/Código usando I1-I3**: Opcional renombrar a IN1-IN3 para claridad (recomendado pero no obligatorio, ambas notaciones comprensibles por contexto).
- **Referencias a D4 §11.1**: Actualizar a §11 si aplicable.

**Testing**: Validado contra 3 casos de estudio R1_Casos.md (H_Score recalculado, diferencia <1.5 puntos).

---

### v2.2.0 (2025-11-03) - Adoption Ready

**Theme**: Internacional scalability + CX operationalización + Security enterprise-grade

**Nuevos Recursos**:
1. **CONTRIBUTING.md** (Guía contribuciones)
   - Guidelines: Bug fixes, patterns, templates, domains E9+, traducciones, casos
   - Submission process: GitHub PR / Email
   - Review criteria: Invariantes I1-I3, evidencia ≥2 casos
   - Code of Conduct, Recognition policy

2. **Positioning Statement** (CORE/00 §0)
   - Elevator pitch 30 seg: "Sistema operativo organizacional"
   - Audiencia primaria/secundaria (quién es/no es KERNEL)
   - Diferenciadores vs TOGAF, SAFe, McKinsey (tabla comparativa)
   - Cuándo usar/NO usar KERNEL (checklist)

3. **LEARNING_PATH.md** (4 tracks)
   - Executive (4-6 hrs): Business case adoption
   - Architect (12-16 hrs): Implementation roadmap
   - AI Engineer (8-12 hrs): Delegation M1-M6
   - Full (40-60 hrs): Expertise framework

4. **Customer Experience KERNEL-Native**
   - A1 §6.6: P_CX01-03 (Flujo Cliente, Señales CX, Touchpoint Ownership)
   - T23_Customer_Journey_Map.md: Template operationalizable

5. **E2 Gobierno Digital Refactored** (internacional-first)
   - E2_Gov_Digital_Base.md: Principios universales (~300L)
   - E2_Chile_TDE.md: Implementación Chile (~2,160L)
   - E2_Template_Gov.md: Guía adaptación países (~200L)
   - E2_Publico.md → Redirect document

6. **Security Integration Complete**
   - D2 §8: Security Observables SO1-SO5
   - A1 §6.5: Security Patterns P_SEC01-05
   - CORE/03 §6: Security como Límite Transversal L3

**Actualizaciones**:
- A5_Medicion.md v2.2: §10 Financial Modeling (ROI framework, TCO analysis, business case template, sensitivity analysis)
- R5_Glosario.md v2.2: +20 términos, appendix acrónimos (23 entries)
- INDEX.md: Actualizado counts (64 patterns, 16 observables, 15 templates, 53 archivos totales)
- README.md: Learning Path como Opción A recomendada, estructura repo actualizada
- A1_Patrones.md: 56 → 64 patterns (P_SEC + P_CX)

**Fixes**:
- OT1-OT3 renombrado (namespace collision T1-T3 templates resuelto)
- A1 §7.5: Trazabilidad patterns orphan (8 patterns P17, P23, P31, P38, P41, P44, P47, P49)
- **H_Score Unificado**: Depreciada versión conflictiva de 14 observables (O1-O11 + OT1-OT3) de E8. El único modelo extendido canónico es el de 16 observables (con SO1-SO5). OT1-OT3 se redefinen como métricas de diagnóstico de causa raíz, no parte del H_Score.

**Breaking Changes**: Ninguno (backward compatible)

**Migración v2.1 → v2.2**: No requiere acción (additive changes)

---

### v2.1.0 (2025-11-02) - Security Integration

**Theme**: Enterprise security baseline

**Nuevos Recursos**:
- D2 §8: Security Observables SO1-SO5
- A1 §6.5: Security Patterns P_SEC01-05
- CORE/03 §6: Security como Límite Transversal

**Actualizaciones**:
- H_Score extended: 70% base + 20% internal + 10% security
- D2_Percepcion.md: 11 → 16 observables
- A1_Patrones.md: 56 → 61 patterns

---

### v2.0.0 (2025-11-02) - Refactored (MAJOR)

**Theme**: Minimalidad + Validación formal

**Breaking Changes**:
1. **Primitivos 6 → 7** (Señal S agregada como primitivo independiente)
   - Trade-off Señal/Dato documentado (overlap temporal consciente)
   - CORE/01 §3A: Señal S definición rigurosa
   - CORE/07: Validación formal I1 Minimalidad con trade-offs

2. **Smartness C7 eliminado** (matriz 4×7 → 4×6)
   - Resuelve contradicción C7 ↔ P8 (Herramienta no Oráculo)
   - C6 Adaptativo = máximo nivel bajo bounded autonomy

3. **Crisis Management consolidado** (CORE/08 nuevo)
   - P52 + AP31-33 + Readiness Paths en single source
   - Reducción ~250 líneas redundancia

**Nuevos Documentos**:
- CORE/08_Crisis_Management.md

**Migración v1.4 → v2.0**:
- **Acción requerida**: Actualizar referencias "C7" → "C6"
- **Acción requerida**: Leer CORE/01 §3A (Señal vs Dato trade-off)
- **Opcional**: Consolidar crisis patterns desde A1/A2 a CORE/08

---

### v1.4.0 (2025-10-15) - Evolutionary Patterns

**Theme**: Desarrollo evolutivo + Orchestration

**Nuevos Recursos**:
- A1 §14: Patrones Desarrollo Evolutivo (P54-P56)
  - P54: Piecemeal Growth
  - P55: Walking Skeleton
  - P56: Continuous Refactoring
- A1 §13: P53 Orchestration Agent (multi-agent systems)

**Refactors**:
- Patterns P54-P56 extraídos de D4 §11 para mayor aplicabilidad

---

### v1.3.0 (2025-09-20) - Crisis Governance

**Theme**: Emergency response + Anti-patterns expansion

**Nuevos Recursos**:
- A1 §12: P52 Crisis Governance
- A2: AP31-33 (crisis anti-patterns)

---

### v1.2.0 (2025-08-10) - Emergent Patterns

**Theme**: Operational patterns post-production

**Nuevos Recursos**:
- A1 §11: P51 Carry-Over Management

---

### v1.1.0 (2025-07-01) - Templates Expansion

**Theme**: Practical templates operacionales

**Nuevos Recursos**:
- R6_Templates: T11-T14 (Tech Debt, Postmortem, ADR, User Story)

---

### v1.0.0 (2025-06-01) - Initial Release

**Theme**: Framework foundation completo

**Documentos** (48 total):
- CORE: 8 documentos (00-07)
- DOMINIOS: 4 documentos (D1-D4)
- APLICACION: 5 documentos (A1-A5)
- DOMINIOS_ESPECIALIZADOS: 8 documentos (E1-E8)
- REFERENCIA: 14 documentos (R1-R7)
- Templates: 10 templates (T01-T10)

**Líneas Contenido**: ~13,200 líneas
**Patterns**: 50 base (P01-P50)
**Anti-patterns**: 30 base
**Observables**: 11 (O1-O8, I1-I3)

---

## Version Policy

### Release Cadence

**Major releases** (X.0.0): Anual o cuando breaking changes acumulados
- Requiere migration guide
- Backward compatibility plan (deprecated features, timelines)
- Community input (feedback period 30 días)

**Minor releases** (x.Y.0): Trimestral o cuando features completas
- New patterns, observables, templates
- Expansiones dominios especializados (E9+)
- No breaking changes

**Patch releases** (x.y.Z): Ad-hoc (fixes críticos)
- Bug fixes, typos, clarifications
- Links rotos, inconsistencias menores

### Pre-release Versions

**Alpha** (x.y.z-alpha.N): Development unstable
- Breaking changes frecuentes
- Testing interno
- **No usar production**

**Beta** (x.y.z-beta.N): Feature complete, testing
- Breaking changes excepcionales
- Community testing
- **Usar con caution production**

**RC** (x.y.z-rc.N): Release Candidate
- Feature freeze
- Bug fixes only
- Production-ready pending final validation

**Ejemplo**: v2.3.0-alpha.1 → v2.3.0-beta.1 → v2.3.0-rc.1 → v2.3.0

---

## Document Versioning

### Individual Documents

Cada documento mantiene versión independiente:

```markdown
**Versión:** 2.2.0 | **Estado:** Definitivo | **Audiencia:** Todos
```

**Estados**:
- **Draft**: Work in progress (no usar production)
- **Beta**: Testing (usar con caution)
- **Definitivo**: Production ready
- **Deprecated**: Scheduled removal (usar alternativa)
- **Archived**: Histórico (no mantener)

### Version Sync

**Documentos CORE**: Sincronizados con KERNEL version (ej: CORE/00 v2.2.0)
**Documentos APLICACION/DOMINIOS**: Pueden tener versiones independientes si iteran más rápido
**Templates**: Version independent (pueden agregar features sin bump KERNEL version)

**Ejemplo**:
- KERNEL v2.2.0
- CORE/00_Manifiesto.md v2.2.0 (sync)
- A1_Patrones.md v2.2.0 (sync por agregado P_CX)
- T23_Customer_Journey_Map.md v1.0.0 (nuevo template, version independiente OK)

---

## Deprecation Policy

### Deprecation Process

**Phase 1: Announce** (Release X.Y.0)
- Marcar feature como `[DEPRECATED]`
- Documentar alternativa recomendada
- Warning logs/notices

**Phase 2: Grace Period** (1 major version)
- Feature funciona pero warnings
- Migration guide published
- Support limited

**Phase 3: Removal** (Release X+1.0.0)
- Feature removida (breaking change)
- Migration guide mandatory reading
- Community support ended

**Ejemplo Deprecation**:
```markdown
## Pattern P99: Legacy Pattern [DEPRECATED v2.1]

**Estado**: Deprecated desde v2.1.0, será removido en v3.0.0

**Alternativa recomendada**: Usar P100 (mejor performance, compatible)

**Migration**: 
1. Reemplazar P99 calls con P100
2. Update config files (ver migration guide)
3. Test thoroughly

**Rationale**: P99 no escalable >1000 usuarios, P100 resuelve limitation
```

---

## Backward Compatibility

### Compatibility Promise

**MINOR releases (x.Y.0)**: 100% backward compatible
- Additive changes only
- No remociones
- Existing code/config works sin cambios

**MAJOR releases (X.0.0)**: May break backward compatibility
- Breaking changes explícitos en changelog
- Migration guide mandatory
- Deprecation warnings en version previa (X-1.Y.0)

### Breaking Change Examples

**✅ Permitido MAJOR**:
- Cambiar invariante (ej: I1 Minimalidad redefinida)
- Remover primitivo (ej: eliminar Estado como primitivo)
- Reestructurar dominios (ej: D1-D4 → D1-D5)
- Cambiar fórmula H_Score (ej: ponderaciones modificadas)

**❌ Prohibido MINOR**:
- Renombrar primitivos (A → Actor OK como alias, pero A debe persistir)
- Cambiar semántica patterns existentes (P01 debe seguir siendo P01, no reasignar)
- Remover observables (O1-O8 fijos, agregar O9+ OK)

---

## Changelog Format

### Entry Template

```markdown
### vX.Y.Z (YYYY-MM-DD) - Release Name

**Theme**: One-line summary release

**[Nuevos Recursos | Breaking Changes | Fixes | Deprecations]**:
1. **Feature Name** (Location)
   - Descripción concisa change
   - Impact: ¿Quién afecta?
   - Action required: ¿Qué hacer?

**Migración vPrevious → vCurrent**: 
- Lista pasos migration (o "No requiere acción")

**Contributors**: @username1, @username2 (if open-source)
```

### Changelog Location

**Primary**: `VERSIONING.md` §Changelog Consolidado (este documento)
**Secondary**: `README.md` §Novedades (últimas 2-3 versiones)
**Archive**: `CHANGELOG_ARCHIVE.md` (versiones antiguas >1 año)

---

## Version Branches (Git)

### Branch Strategy

**main**: Current stable release (v2.2.0)
- Production-ready
- Merge from `release/vX.Y.Z` branches

**develop**: Next minor version (v2.3.0-dev)
- Feature branches merge here
- Testing continuous

**release/vX.Y.Z**: Release candidate
- Feature freeze
- Bug fixes only
- Merge to `main` when ready

**feature/feature-name**: Individual features
- Branch from `develop`
- Merge back to `develop` via PR

**hotfix/issue-description**: Urgent fixes
- Branch from `main`
- Merge to `main` AND `develop`

---

## Roadmap Preview

### v2.3.0 (Planned Q1 2026)

**Theme**: Financial modeling + Multi-language support

**Planned Features**:
- A5 §11: Financial Modeling (ROI calculators, TCO)
- Translations: English base complete (Spanish, French)
- E9_Retail: Retail-specific patterns

**Status**: Draft (30% complete)

---

### v3.0.0 (Planned Q3 2026)

**Theme**: AI-Native v2 (major breaking)

**Planned Breaking Changes**:
- Delegation M1-M6 → M1-M8 (agregar M7 Swarm, M8 Autonomous Org)
- Smartness C1-C6 → redefinición niveles (AI evolution)
- Observables expansion (30+ observables sector-specific)

**Status**: Research (10% complete)

---

## FAQ Versioning

**Q1: ¿Debo actualizar inmediatamente a cada minor release?**  
**A**: No urgente. Minor releases son backward compatible. Update cuando conveniente (ej: quarterly reviews).

**Q2: ¿Cómo saber si release tiene breaking changes?**  
**A**: MAJOR version bump (X.0.0) siempre indica breaking. Leer changelog sección "Breaking Changes".

**Q3: ¿Puedo mezclar versiones documentos? (ej: CORE v2.2, A1 v2.1)**  
**A**: No recomendado. Mantener CORE + APLICACION + DOMINIOS sincronizados con KERNEL version. Templates pueden variar.

**Q4: ¿Qué hacer si encuentro bug crítico?**  
**A**: Report issue (GitHub/email), patch release (x.y.Z+1) expedited en <7 días si critical.

**Q5: ¿KERNEL es open-source? ¿Cómo contribuir?**  
**A**: Ver `CONTRIBUTING.md` (if open-source) o contactar maintainer. PRs welcome para fixes/expansiones (subject a review).

---

## Metadata

**Maintainer**: [KERNEL Core Team]  
**Contact**: [Email/GitHub]  
**License**: [Specify if open-source, ej: MIT, Apache 2.0, or Proprietary]  
**Last Updated**: 2025-11-03 (v2.2.0 release)

---

## Changelog

**v1.0.0** (2025-11-03): Initial VERSIONING.md document
- Estrategia semántica definida
- Changelog consolidado v1.0 → v2.2
- Policies deprecation, compatibility, roadmap
