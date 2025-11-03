# E2_Template_Gov (Guía Adaptación Gobierno Digital por País)

**Versión:** 2.1.0  
**Estado:** Template  
**Audiencia:** CDOs Gobierno, Arquitectos SI Públicos, Consultores Internacionales  
**Dependencias**: `E2_Gov_Digital_Base.md` (fundamentos universales), `E2_Chile_TDE.md` (ejemplo implementación)

---

## Propósito Template

Este documento guía adaptación de `E2_Gov_Digital_Base.md` (principios universales) a implementación específica por país, usando `E2_Chile_TDE.md` como referencia.

---

## PASO 1: Identificar Marco Legal & Regulatorio

### Checklist Marco Legal

**Pregunta**: ¿Qué leyes/regulaciones aplican gobierno digital en tu jurisdicción?

**Aspectos Mapear**:

1. **Digital Transformation Law** (equivalente Ley 21.180 Chile):
   - ¿Existe mandato legal gobierno digital?
   - Fecha promulgación, vigencia gradual o inmediata
   - Plazos compliance (ej: Chile 2027-12-31)
   - Sanciones incumplimiento

2. **Data Protection & Privacy** (equivalente GDPR EU, LGPD Brasil):
   - Regulación protección datos personales
   - Derechos ciudadanos (access, rectification, erasure)
   - Data Protection Authority (DPA)
   - Multas/sanciones breaches

3. **Cybersecurity Standards** (equivalente NT DS 7/2023 Chile):
   - Normas técnicas seguridad gobierno
   - Frameworks obligatorios (ISO 27001, NIST CSF, local)
   - Incident reporting requirements
   - Roles security (CISO, security officers)

4. **E-Signature & E-Documents** (equivalente NT DS 10/2023 Chile):
   - Validez legal firma electrónica
   - PKI infrastructure (Public Key Infrastructure)
   - Document retention policies (años almacenamiento)
   - Archiving standards (formato, metadata)

5. **Open Data Regulation**:
   - Mandato publicación datos abiertos
   - Licencias datos (CC0, CC-BY)
   - Excepciones (national security, privacy)
   - Portal datos centralizado (data.gov.xx)

6. **Interoperability Standards**:
   - Estándares técnicos intercambio datos inter-agencias
   - API specifications (REST, SOAP)
   - Metadata standards (DCAT, Dublin Core)
   - Semantic interoperability (ontologies sector)

**Ejemplo Chile** (extraído E2_Chile_TDE.md §1):
```yaml
Ley_TDE: Ley 21.180 (2019)
Privacy: Ley 19.628 (pendiente actualización GDPR-like)
Cybersecurity: NT DS 7/2023
E-Documents: NT DS 10/2023
Open_Data: Política Datos Abiertos Gobierno Chile
Interoperability: Guía API v3.0 SGD
```

**Template Tu País**:
```yaml
Ley_TDE: [Nombre ley/decreto, año]
Privacy: [GDPR local equivalent, año]
Cybersecurity: [Standard obligatorio]
E-Documents: [Regulación e-signature]
Open_Data: [Política datos abiertos]
Interoperability: [Standards técnicos]
```

---

## PASO 2: Identificar Plataformas Nacionales

### Checklist Plataformas Gobierno

**Pregunta**: ¿Qué plataformas digitales compartidas existen (o deben crearse)?

**Plataformas Esenciales** (basado §3 E2_Gov_Digital_Base.md):

1. **Identity & Authentication**:
   - Chile: ClaveÚnica (SAML, OAuth)
   - Estonia: e-ID (PKI smartcard)
   - UK: GOV.UK Verify (federated identity)
   - **Tu País**: _____________________

2. **Digital Signature**:
   - Chile: FirmaGob (PKI government)
   - EU: eIDAS (cross-border signatures)
   - India: Aadhaar eSign
   - **Tu País**: _____________________

3. **Document Management**:
   - Chile: DocDigital (inter-agency communications)
   - Estonia: X-Road (document exchange)
   - Brazil: gov.br (unified portal + docs)
   - **Tu País**: _____________________

4. **Citizen Portal**:
   - Chile: ChileAtiende (gov.cl)
   - Singapore: MyGov.sg
   - France: service-public.fr
   - **Tu País**: _____________________

5. **Payment Gateway**:
   - Chile: Portal Pagos Gobierno
   - UK: GOV.UK Pay
   - India: Bharat Bill Payment System
   - **Tu País**: _____________________

6. **Interoperability Platform**:
   - Chile: Red Interoperabilidad SGD (reemplazo PISEE)
   - Estonia: X-Road
   - EU: CEF eDelivery
   - **Tu País**: _____________________

7. **Open Data Portal**:
   - Chile: datos.gob.cl
   - USA: data.gov
   - EU: data.europa.eu
   - **Tu País**: _____________________

**Template Plataformas**:
```yaml
Plataformas_Existentes:
  Identity: [Nombre, URL, adoption %]
  Signature: [Nombre, URL, adoption %]
  Portal: [gov.xx, features]
  Payments: [Gateway, métodos soportados]
  Interop: [Platform, standards]
  Open_Data: [Portal, datasets count]

Plataformas_Faltantes:
  - [Lista plataformas por construir]
  - [Prioridad: Alta/Media/Baja]
  - [Timeline estimado]
```

---

## PASO 3: Adaptar MVDG Checklist (90 días)

### Personalización Quick Start

**Basado**: §0 E2_Gov_Digital_Base.md + §0 E2_Chile_TDE.md

**Adaptaciones Necesarias**:

1. **Governance (Semana 1-2)**:
   - ¿Rol CDO existe? Si no, ¿cómo se llamará? (Coordinador TD, Director Digital)
   - ¿Requiere aprobación legislativa/ejecutiva?
   - ¿Presupuesto asignado?

2. **Diagnóstico (Semana 3-6)**:
   - ¿Existe herramienta nacional madurez digital? Si no, usar OCDE eGov Maturity Model
   - ¿Inventario servicios ciudadanos disponible? Si no, crear desde cero
   - ¿Auditoría web accesibilidad/security? Standards locales (WCAG 2.1, ISO 27001)

3. **Plataformas (Semana 4-10)**:
   - Priorizar según disponibilidad: Usar existentes vs construir
   - Si no hay Identity nacional → Evaluar opciones:
     * Build in-house (costly, 12-18 meses)
     * Adopt SaaS (Auth0, Okta Government)
     * Federated identity (allow Google, Facebook login - controversial gov)

4. **Infraestructura (Semana 3-8)**:
   - Cloud: ¿Restricciones data residency? (algunos países requieren data sovereignty)
   - Budget: Adjust costo estimado según país (Chile $15-30M CLP = $20-40K USD)

5. **Datos Abiertos (Semana 6-10)**:
   - ¿Policy open data existe? Si no, draft basado OECD 8 principles
   - Portal: Usar CKAN (open source) o propietario (Socrata, OpenDataSoft)

6. **Plan TD (Semana 8-12)**:
   - Horizonte: 3-5 años typical
   - KPIs: Adaptar §6 E2_Gov_Digital_Base.md (12 métricas universales)
   - Budget: % PIB government IT spending (benchmark OCDE 1-3% budget público)

7. **Capacitación (Semana 1-12)**:
   - Language training materials (traducir si es necesario)
   - Cultural adaptation: Ejemplos locales, no foráneos

8. **Compliance (Semana 10-12)**:
   - Policies: Template usando frameworks internacionales + requirements locales
   - Roles: Adaptar títulos (CISO, DPO) a nomenclatura local

**Template MVDG Adaptado**:
```yaml
MVDG_[PAÍS]:
  Duration: 90 días (ajustar si capacity limitada)
  Budget: $______ USD (basado contexto local)
  Team: [Roles específicos país]
  Legal: [Leyes aplicables por paso]
  Platforms: [Usar existentes, construir faltan]
  Language: [Idioma oficial, minorías]
  Timeline_Adjusted: [Si regulación tiene plazos específicos]
```

---

## PASO 4: Mapear Casos Uso Prioritarios

### Servicios Digitales Alta Demanda

**Pregunta**: ¿Qué servicios ciudadanos tienen mayor volumen/impacto?

**Categorías Universales** (basado Life Events):

1. **Citizen Identity**:
   - Register birth/death
   - ID card issuance/renewal
   - Change address

2. **Tax & Payments**:
   - Income tax filing
   - Property tax payment
   - Business tax (VAT, corporate)

3. **Business**:
   - Business registration (incorporate)
   - Permits (construction, operation)
   - Licenses (professional, trade)

4. **Social Services**:
   - Unemployment benefits
   - Pensions (calculate, apply)
   - Social assistance (housing, food)

5. **Health**:
   - Appointment booking
   - Medical records access
   - Prescription refills

6. **Education**:
   - School enrollment
   - Student financial aid
   - Certificate requests (diplomas)

7. **Justice**:
   - Police reports (theft, accident)
   - Court case status
   - Legal aid request

**Priorización**:
```yaml
Criterios:
  - Volume: Trámites/año
  - Impact: Tiempo/costo ciudadano ahorrado
  - Complexity: Bajo (quick win) vs Alto (largo plazo)
  - Legal_Mandate: Obligatorio por ley vs opcional

Top_5_Servicios_Digitalizar:
  1. [Servicio #1]: Volume X, Impact Y, Timeline Z
  2. [Servicio #2]: ...
  3. [Servicio #3]: ...
  4. [Servicio #4]: ...
  5. [Servicio #5]: ...
```

**Chile Top 5** (inferido E2_Chile_TDE.md):
1. SIMPLE: Trámites municipales (permisos, certificados)
2. Tax filing: Declaración impuestos (SII)
3. ClaveÚnica: Identidad digital (transversal)
4. Subsidios sociales: Registro Social Hogares
5. Salud: Agendamiento atención primaria

**Tu País Top 5**:
1. ___________
2. ___________
3. ___________
4. ___________
5. ___________

---

## PASO 5: Definir Métricas Éxito

### KPIs Adaptados (basado §6 E2_Gov_Digital_Base.md)

**KPIs Universales con Targets Locales**:

```yaml
Digital_Adoption:
  - % servicios online: Target __% (Chile 2027: 100%)
  - % transacciones digitales vs presencial: Target __% (benchmark 70%)
  - Mobile usage: Target __% (tendencia global >50%)

Citizen_Satisfaction:
  - NPS ciudadanos: Target >__ (benchmark >50)
  - CSAT servicios digitales: Target >__% (benchmark >75%)
  - Trust government digital: Survey __% (benchmark >60%)

Efficiency:
  - Cost per transaction digital vs analog: Ratio __:1 (benchmark 10:1)
  - Time savings per citizen: __ horas/año (benchmark 10-20hrs)
  - Government productivity: Staff hours saved __% (benchmark +20%)

Security_Privacy:
  - Incidents security: Target 0 breaches materiales
  - Compliance rate: Target 100% regulations
  - GDPR/Privacy requests response: <30 días (benchmark EU)

Inclusion:
  - Digital divide: __% población sin acceso digital (target minimize)
  - Accessibility: __% servicios WCAG 2.1 AA compliant (target 100%)
  - Language support: # idiomas soportados (si país multilingüe)
```

**Baseline Actual vs Target**:
```yaml
Año_0 (Baseline Today):
  Servicios_Online: __%
  Transacciones_Digitales: __%
  NPS: __
  Cost_Ratio: __:1

Año_3 (Target):
  Servicios_Online: __%
  Transacciones_Digitales: __%
  NPS: __
  Cost_Ratio: __:1

Año_5 (Aspiracional):
  Servicios_Online: 100%
  Transacciones_Digitales: >70%
  NPS: >50
  Cost_Ratio: >10:1
```

---

## PASO 6: Roadmap Implementación

### Fases Transformación Digital (3-5 años)

**Basado**: E2_Gov_Digital_Base.md principios + E2_Chile_TDE.md timeline

**Fase 1: Foundations (Año 1)**:
- MVDG 90 días (§0 E2_Gov_Digital_Base.md)
- Plataformas core: Identity + Portal + Payments
- Digitalizar 5 servicios alta demanda
- Team: CDO + 5-10 personas

**Fase 2: Scale (Año 2)**:
- Digitalizar 20-30 servicios adicionales
- Interoperability platform deployed
- Open data portal con 50+ datasets
- Team: CDO + 20-30 personas

**Fase 3: Optimization (Año 3)**:
- Mayoría servicios digitales (>70%)
- Proactive government (life events, AI notifications)
- Data analytics platform (dashboards C-level)
- Team: CDO + 30-50 personas

**Fase 4: Leading (Año 4-5)**:
- 100% servicios digitales
- AI integration (chatbots, recommendations)
- Cross-border interoperability (si regional block existe)
- Benchmark internacional top 20%

**Timeline Tu País**:
```yaml
Año_1_[YYYY]:
  - [Milestone 1]
  - [Milestone 2]
  - [Budget $__]

Año_2_[YYYY]:
  - [Milestone 1]
  - [Milestone 2]
  - [Budget $__]

Año_3_[YYYY]:
  - [Milestone 1]
  - [Milestone 2]
  - [Budget $__]
```

---

## PASO 7: Budget & Financing

### Estimation Costs

**Basado**: E2_Chile_TDE.md §0 ($15-30M CLP MVTD = $20-40K USD)

**Cost Drivers**:

1. **Platforms** (60-70% budget):
   - Identity: $100K-500K (build) vs $10K-50K/yr (SaaS)
   - Portal: $200K-1M (build) vs $20K-100K/yr (SaaS)
   - Interop: $500K-2M (build) vs $50K-200K/yr (SaaS)
   - Cloud IaaS: $50K-500K/yr depending scale

2. **Services Digitalization** (20-30% budget):
   - Per service: $10K-100K (depends complexity)
   - 50 services × $30K avg = $1.5M

3. **Team** (10-20% budget):
   - CDO: $__K/yr (benchmark local executive salaries)
   - IT staff: $__K/yr × __ personas
   - Consultants: $__K (short-term needs)

4. **Training & Change Management** (5-10%):
   - Executive workshops: $__K
   - Staff training: $__K
   - Citizen communication: $__K

**Total Budget Estimado**:
```yaml
Año_1: $____K-____K USD
Año_2: $____K-____K USD
Año_3: $____K-____K USD

Total_3_Años: $____K-____K USD

Financing:
  - Government budget allocation: __% ($__)
  - International donors (World Bank, IDB, EU): __% ($__)
  - Public-private partnerships: __% ($__)
```

**Benchmark Internacional** (% PIB o % Budget Público IT):
- Estonia: 3.5% budget público IT
- OCDE avg: 1-2% budget público IT
- Tu país baseline: __% → Target __% (año 3)

---

## PASO 8: Risks & Mitigation

### Risks Comunes Gobierno Digital

**Basado**: Lecciones E2_Chile_TDE.md + internacional

**Risk Matrix**:

| Risk | Probability | Impact | Mitigation |
|------|-------------|--------|------------|
| **Legal delays** (leyes no aprobadas) | Alta | Alto | Start pilot sin mandato formal, lobby legislativo paralelo |
| **Budget cuts** (austerity) | Media | Alto | Priorizar MVDG (ROI quick), defer nice-to-have features |
| **Resistance change** (funcionarios) | Alta | Medio | Change management, training, incentivos adoption |
| **Technical debt legacy** (sistemas obsoletos) | Alta | Medio | Strangler Fig pattern (P21), no big-bang rewrite |
| **Cybersecurity breach** | Baja | Muy Alto | Security by design, ISO 27001, incident response plan |
| **Vendor lock-in** | Media | Medio | Open standards, avoid proprietary, exit clauses contracts |
| **Low citizen adoption** | Media | Alto | UX testing, marketing campaigns, support centers |
| **Data quality poor** | Alta | Alto | Data governance program, stewardship roles, quality metrics |

---

## PASO 9: Governance & Organization

### Estructura Gobierno Digital

**Modelo Recomendado** (basado OECD + E2_Chile_TDE §7):

```yaml
Executive_Level:
  CDO (Chief Digital Officer):
    - Reports to: President/PM or Minister Modernization
    - Budget authority: Yes (% PIB asignado)
    - Team size: 50-200 personas (depends country size)
    - Mandate: Digital transformation strategy, platforms, oversight

Coordination_Bodies:
  Comité_TD (Digital Transformation Committee):
    - Members: CDO + Ministers key (Finance, Interior, Economy)
    - Frequency: Monthly
    - Decisions: Budget major, priorities, regulations

  Technical_Committee:
    - Members: CDO + CIOs agencies
    - Frequency: Bi-weekly
    - Decisions: Standards, interop, platform roadmap

Agency_Level:
  CIO (Chief Information Officer) per Agency:
    - Reports to: Agency head + matrix to CDO
    - Mandate: Implement digital services agency-specific
    - Budget: Agency allocation + platform budget central CDO

Citizen_Participation:
  Advisory_Council:
    - Members: Civil society, private sector, academia
    - Frequency: Quarterly
    - Role: Feedback UX, accountability, transparency
```

---

## PASO 10: Success Stories Celebrate

### Communication & Adoption

**Change Management** (crítico success):

1. **Quick Wins** (first 6 meses):
   - Launch 1 high-visibility service (tax filing, ID renewal)
   - Communicate savings: "Citizens saved X hours/year"
   - Media coverage: National newspapers, TV, social media

2. **Champions** (continuous):
   - Identify early adopters (agencies, citizens)
   - Showcase testimonials: "Before 3 days, now 10 minutes"
   - Awards: Best digital service, most innovative agency

3. **Metrics Dashboard** (transparency):
   - Public dashboard: servicios.digital.gob.xx/metrics
   - Show progress: % services online, transactions, satisfaction
   - Update monthly: Build momentum, accountability

4. **International Recognition** (año 2-3):
   - Apply UN eGov Survey, OCDE eGov reviews
   - Present conferences: eGov conferences, regional forums
   - Benchmarking: Position country regional top 5

---

## Checklist Final Adaptación

**Antes Launch Tu País**:

- [ ] Marco legal mapeado completamente
- [ ] Plataformas nacionales identificadas/construidas
- [ ] MVDG checklist personalizado
- [ ] Top 5 servicios priorizados + roadmap
- [ ] KPIs definidos + baseline medido
- [ ] Budget 3 años estimado + financing secured
- [ ] Risks identificados + mitigation plans
- [ ] Governance structure approved
- [ ] Team recruited (CDO + core)
- [ ] Communication plan defined
- [ ] Pilot service launched (first 90 días)

**Recursos Adicionales**:
- `E2_Gov_Digital_Base.md`: Fundamentos universales
- `E2_Chile_TDE.md`: Ejemplo implementación completa Chile
- `CORE/03_Arquitectura.md`: Dominios KERNEL aplicables gobierno
- `APLICACION/A1_Patrones.md`: Patterns útiles gobierno (P_GOV01-03, P01-P56)
- `REFERENCIA/R6_Templates`: Templates adapt (OKR, Roadmap, Assessment)

---

## Contact & Support

**¿Necesitas ayuda adaptación?**

- Consulta comunidad KERNEL (si existe)
- OECD Digital Government Unit
- Regional organizations (CLAD LATAM, EU eGov, ASEAN eGov)
- Inter-American Development Bank (IDB) - Digital Government Division

**¡Éxito en tu transformación digital gubernamental!** 🚀
