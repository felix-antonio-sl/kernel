# E7_Enterprise_Technology_Integration

**Versión:** 2.0.0  
**Estado:** Production  
**Audiencia:** CTOs, Arquitectos SI, Tech Leads, Platform Engineers  
**Dependencias**: CORE/01-08, DOMINIOS/D1-D4, APLICACION/A1-A5

---

## §1. PROPÓSITO Y SCOPE

### Definición

Este dominio especializado cubre el **desarrollo de aplicaciones empresariales end-to-end** y la habilitación tecnológica de plataformas (DevOps, security, observability, UX/UI). Integra patrones arquitectónicos modernos, stacks tecnológicos, ingeniería de plataformas y experiencia de usuario como capa transversal.

### Alcance

**INCLUYE**:

- Patrones arquitectónicos (Monolito Modular, Microservicios, EDA, Serverless)
- Stack tecnológico enterprise (backend, frontend, databases, infra)
- Experience Layer (UX/UI patterns, AI-assisted UX, design systems, multi-device)
- DevOps & Platform Engineering (CI/CD, IaC, containerization, observability)
- Security shift-left (autenticación, autorización, OWASP, secrets management)
- NFRs & SLOs (latency, throughput, availability, C4, ADRs)

**EXCLUYE** (cubiertos por otros dominios):

- Data-as-Product, AI Orchestration, Process Automation, Knowledge Management → **E8_Intelligent_Systems**
- Dominio-específico (gobierno, manufactura, salud, finanzas) → **E2-E5**
- Foundation concepts → **CORE** (Recurso, Flujo, Actor, Límite en CORE/01-03)

### Conexión KERNEL

**Primitivos especializados**:

- **Recurso**: Applications, tech stack, infrastructure, platform services
- **Flujo**: CI/CD pipelines, user workflows, data flows, deployment flows
- **Actor**: Developers, SRE/DevOps Engineers, Platform Engineers, End-users
- **Límite**: NFRs, SLOs, API contracts, regulatory constraints, error budgets

**Dominios extendidos**:

- **D1_Arquitectura**: Stack patterns, Conway's Law, ADRs, bounded contexts
- **D2_Percepción**: Tech observability (DORA metrics, tech health, uptime)
- **D3_Decisión**: Stack selection framework, trade-offs analysis, build vs buy
- **D4_Operación**: CI/CD execution, deployment strategies, SRE practices

**Delegación tech-specific**:

- **M2-M3**: AI copilots en UX (inform users, enable capabilities) → §4.5
- **M4-M6**: Automated testing, quality gates, automated deployments → §5

---

## §2. PATRONES ARQUITECTÓNICOS

### Trade-Offs Matrix

La elección arquitectónica es la decisión con mayor impacto a largo plazo. No existe solución única; la clave es entender los **trade-offs**.

| Patrón | Ideal Para | Ventajas Clave | Desventajas/Consideraciones |
|:---|:---|:---|:---|
| **Monolito Modular** | Startups, MVPs, equipos <15, dominios acotados | • Simplicidad inicial desarrollo/deploy<br>• Rendimiento optimizado (in-process)<br>• Refactorización interna fácil | • Acoplamiento tecnológico<br>• Escalado granular difícil<br>• Ciclos deploy lentos al crecer |
| **Microservicios** | Sistemas complejos, equipos >30 distribuidos, escalabilidad granular | • Escalabilidad por componente<br>• Autonomía equipos<br>• Deploys independientes frecuentes | • Complejidad operacional (orchestration, service discovery)<br>• Consistencia eventual (Sagas, Outbox)<br>• Latencia de red, tracing distribuido (OpenTelemetry) |
| **EDA (Event-Driven)** | Procesos asíncronos, alta desacoplación, sistemas reactivos (IoT, finanzas) | • Desacoplamiento máximo<br>• Escalabilidad masiva<br>• Resiliencia a picos de carga | • Debugging flujos complejo<br>• Requiere message broker robusto (Kafka, Pulsar)<br>• Idempotencia, orden de eventos críticos |
| **Serverless (FaaS)** | Cargas intermitentes, event-driven, APIs bajo tráfico, prototipos | • Coste cero en reposo (pay-per-use)<br>• Escalado automático gestionado<br>• Abstracción infra total | • Cold starts (latencia)<br>• Límites tiempo/recursos ejecución<br>• Vendor lock-in, testing local complejo |

### Principio Rector

**Start monolito modular bien estructurado** → Extract microservicios cuando **dolor del acoplamiento > complejidad de la distribución**.

**Domain-Driven Design (DDD)**: Define **Bounded Contexts** como límites naturales para módulos/servicios.

**Conexión KERNEL**:

- **P06 Inverse Conway's Law** (APLICACION/A1): Org structure → System architecture
- **D1_Arquitectura §1 P4**: Conway's Law awareness explícito
- **Límite** (CORE/03): Bounded contexts como límites semánticos

### Decisión Framework

**Inputs**: NFRs + Team skills + Ecosystem maturity  
**Proceso**: Evaluar trade-offs tabla → Piloto pequeño → Iterar  
**Output**: ADR documentado (T13_ADR template, REFERENCIA/R6_Templates)

**Ejemplo aplicación**: Startup 10 eng → 50 eng:

1. Año 1: Monolito modular (velocidad máxima)
2. Año 2-3: Identificar bounded contexts con dolor (deploy freq bottleneck)
3. Año 3: Extraer 2-3 microservicios críticos (pagos, autenticación)
4. Año 4: Deploy freq 1 cada 3 semanas → 5/día (DORA improvement)

---

## §3. STACK TECNOLÓGICO

### Decision Framework

**Criterios**: Ecosistema + Talento disponible + NFRs + Madurez

### Backend

| Lenguaje/Framework | Ideal Para | Justificación |
|:---|:---|:---|
| **Java (Spring Boot, Quarkus)** | Apps enterprise robustas, alto rendimiento, arquitecturas complejas | Ecosistema maduro, tipado fuerte, tooling excepcional, talent pool amplio |
| **C# (.NET)** | Ecosistemas Microsoft, integración Azure nativa | Alto rendimiento, unificado (web/desktop/mobile), excelente DX |
| **Python (Django, FastAPI)** | Apps data-intensive, servicios IA/ML | Rapidez desarrollo, FastAPI performance comparable Go/Node, ecosistema ML/AI |
| **Node.js (Express, NestJS)** | Apps I/O-bound, real-time (websockets) | Event loop non-blocking, ecosistema NPM masivo, NestJS estructura modular |
| **Go** | Microservicios alto rendimiento, CLI/infra tools | Concurrencia nativa simple, binarios estáticos, footprint bajo |

### Frontend

| Framework | Trade-off | Cuándo Usar |
|:---|:---|:---|
| **React** | Flexibilidad vs Estructura | Equipos que prefieren componer su framework (routing, state management custom) |
| **Angular** | Estructura vs Flexibilidad | Apps enterprise grandes, estructura robusta, DI, tipado fuerte desde inicio |
| **Vue.js** | Equilibrio | Curva aprendizaje suave, balance React flexibility + Angular structure |
| **Svelte/SolidJS** | Performance vs Ecosystem | Interfaces altamente interactivas, performance máximo (compiladores, minimal JS) |

### Databases

| Tipo | Tecnología | Uso Principal |
|:---|:---|:---|
| **SQL (OLTP)** | PostgreSQL (default), MySQL | Datos transaccionales, ACID, extensibilidad (JSONB, PostGIS) |
| **NoSQL Documental** | MongoDB, DynamoDB | Datos semi-estructurados, esquemas flexibles, escalabilidad horizontal |
| **Cache** | Redis | Caché in-memory, pub/sub, colas, latency reduction |
| **Search** | Elasticsearch, OpenSearch | Búsqueda full-text, analytics, observability (logs, metrics) |

### Conexión KERNEL

**Recurso (CORE/01)**: Stack como capacidad habilitadora (tech capacity R3)  
**Flujo (CORE/02)**: CI/CD como flujo automatizado (F2 Automated)  
**Actor (CORE/03)**: Developers, SRE como actores especializados  
**D3_Decisión §3**: Stack selection como decisión arquitectónica bajo incertidumbre

---

## §4. EXPERIENCE LAYER (UX/UI Integrado)

### §4.1 Modern Layouts & Design Patterns

**Modular, Card-Based Interfaces**:

- Dashboards modulares con widgets movibles (personalización usuario)
- Drill-down sin overhead cognitivo (progressive disclosure)
- Beneficio: Updates componentes no disrumpten sistema completo

**Progressive Disclosure & Contextual Help**:

- Opciones avanzadas ocultas hasta necesarias (reduce cognitive load)
- Tooltips contextuales, info panels on-demand
- **Ejemplo**: Analytics app muestra summary simple → "Show Advanced Filters" expande

**Micro-Interactions for Feedback**:

- Animaciones sutiles (buttons hover, loaders, checkmarks post-save)
- Instant feedback usuarios (acción registrada)
- **Ejemplo enterprise**: Field validations shake/color-highlight on error

**Established UI Patterns**:

- Leverage consumer patterns (left-side menus, top search bars)
- Reducen training time (users recognize behavior)
- **Principio**: Consistency builds trust (mission-critical tools)

**Minimalist Aesthetics**:

- Whitespace amplio, typography clara, color deliberado
- **Dark mode** default (reduce eye strain, hours-in-dashboards use case)
- **Filosofía**: Less is more → Data y acciones destacan

**Conexión KERNEL**:

- **D2_Percepción O1**: UX clarity como observable (P1 Perceptualidad CORE/05 §3)
- **A3_Diagnóstico §4**: UX friction assessment

### §4.2 Interaction Models

**Real-Time Collaboration**:

- Multi-user live editing (cursors, edits real-time como Google Docs/Figma)
- **Baseline expectation 2024**: Project mgmt, analytics tools con co-editing
- **Ejemplo**: Joint annotation de dashboards durante meetings

**Conversational & Chatbot Interfaces**:

- Natural language requests vs menu hunting
- **Ejemplo**: "What was Q3 revenue growth?" → AI-driven answer
- **CRM use case**: Chatbot retrieve customer info, draft emails (speed workflows)

**Voice & Screen-Free Controls**:

- VUI para field workers (hands-free, mobility)
- **Ejemplo**: Warehouse app usa "next item" voice command
- **Emergente**: AR glasses maintenance/training (hands-free data viz)

**Keyboard Shortcuts & Command Palettes**:

- Power-users efficiency (Ctrl+K universal search)
- **Inspired by**: VS Code, Slack command palettes
- **Ejemplo**: Type "inv" → Suggests "Invite User", "Invoice Settings"

**Non-Linear Workflows**:

- Expert users no siguen "happy path" preset
- Save draft workflows, resume later, multiple paths to function
- **Ejemplo**: Edit dos records side-by-side (parallel workstreams)

**Delightful UX & Gamification**:

- Progress indicators celebrate completion (reduce stress)
- **Ejemplo**: Asana unicorn animation task completion, confetti milestones
- **Beneficio**: Boost morale, positive emotional connection (Zoom fatigue mitigation)

**Conexión KERNEL**:

- **M2-M3 Delegación** (CORE/04 §8): AI copilots como M3 Enable (conversational interfaces)
- **D4_Operación A2**: User workflows como ejecución especificada
- **P55 Conversational Interface** (APLICACION/A1): Pattern relacionado

### §4.3 Accessibility & Inclusive Design

**Accessibility as Standard (WCAG Baseline)**:

- WCAG AA baseline, AAA aspirational
- **Valor amplio**: No solo discapacidad permanente, sino temporal, situacional, aging workforce
- Bake-in desde día 1 (no retrofit)

**Keyboard-First & Assistive Tech**:

- Full functionality via keyboard (power users + motor impairments)
- Visible focus indicators, logical tab order, shortcut keys
- **Screen readers**: ARIA labels, summary statistics read aloud
- **Ejemplo**: Dashboard widgets navegables vía ARIA, stats spoken

**Inclusive Visual Design**:

- **Dark mode, high-contrast modes** out-of-box
- Color palettes color-blind friendly (texture/patterns en charts)
- Plain language, clear labels (no jargon → non-native speakers, cognitive differences)

**Resultado**: Universal design = good design → Overall satisfaction ↑, competitive edge

**Conexión KERNEL**:

- **Límite L3** (CORE/03 §3): WCAG como límite regulatorio
- **D2_Percepción O1**: Accessibility score como observable
- **E2_Público §6**: Gov-specific accessibility requirements (reference)

### §4.4 AI-Assisted UX

**Copilots Embedded**:

- LLM-powered assistants in-UI (chat, voice)
- **Ejemplo**: Microsoft 365 Copilot draft emails, summarize docs on command
- **Funciones**: Contextual help, domain Q&A, content generation, process guidance

**Predictive UX & Smart Automation**:

- Auto-suggest likely actions, pre-fill based on context
- **Ejemplo ERP**: "End-of-quarter → Generate finance report now?"
- **Ejemplo CRM**: Auto-fill customer location from phone number

**Personalization ML**:

- Dashboards reorder to surface relevant metrics per user
- Learn visit patterns → Bubble up frequent spaces
- **Hyper-personalization**: Role + habits adaptation (like consumer apps)
- **Ethics**: User control, transparency, opt-out

**Augmented Decision-Making**:

- AI crunch large datasets → Present insights/recommendations in-UI
- **Ejemplo procurement**: Highlight best supplier (past performance, cost data)
- **Ejemplo HR**: Flag team burnout risk (workload, time-off patterns analysis)
- **UX challenge**: Transparent AI (confidence levels, reasoning shown)

**Conexión KERNEL**:

- **CORE/04 Delegación §8**: Purpose 1 Assistant (M3 Enable mode explícito)
- **M3 Enable**: AI copilots enable user capabilities (contextual, bounded)
- **E8_Intelligent_Systems §5**: AI Orchestration patterns (reference, no duplicar)
- **P53 Orchestration Agent** (CORE/04 §8): Pattern AI agents

### §4.5 Multi-Device & Cross-Platform

**Responsive & Mobile-Friendly**:

- Responsive web design standard 2024 (desktop/tablet/mobile)
- Redesign workflows for mobile (not cramped desktop copy)
- **Resultado**: Employees accomplish key tasks on-the-go

**Companion Apps & Second-Screen**:

- **Ejemplo**: Google Meet Companion Mode (second device, no echo)
- Desktop deep exploration, mobile alerts + key metrics
- Tailor experience to device strengths (phone camera scan QR, PC bulk data analysis)

**Seamless Continuity**:

- Cloud sync, state preservation cross-device
- **Ejemplo**: Email draft phone → Continue laptop right where left off
- Design systems ensure familiarity each device (no relearn)

**Offline Capability**:

- PWAs, local caching (poor connectivity resilience)
- **Ejemplo**: Sales rep CRM offline, data syncs later
- **Beneficio**: Productivity no halt when network fails

**Conexión**: D4_Operación §6 Resilience patterns

### §4.6 Data Visualization

**Interactive Dashboards**:

- Click chart elements → Filter/drill-down
- **Ejemplo**: Click sales bar → See per-region details
- Adjust time ranges via sliders, hover granular tooltips

**Real-Time Data & Alerts**:

- Live operations metrics, IoT sensor data (seconds refresh)
- AI highlight anomalies: "This week output 15% below avg" (red flag)
- **Beneficio**: Transform dashboards → Decision support tools

**Story-Focused Visuals**:

- Reduce clutter, clear purpose per chart
- Curated dashboards (cada chart tiene contexto: titles, captions, dynamic explanations)
- **Ejemplo**: Few key KPIs + trendlines + annotations (good/bad vs goal) + text blurb

**Data Democratization**:

- BI capabilities in everyday apps (no export to specialized tools)
- Self-service: drag-drop, natural language queries ("show sales by region as pie chart")
- **Resultado**: Insights no bottlenecked with analysts, data-savvy workforce

**Conexión**: A5_Medición §3 Dashboard structures (reference)

### §4.7 Design Systems

**Unified Component Library**:

- Centralized design system as mission-critical product
- Reusable components (buttons, icons, interactions) shared across apps
- **Beneficio**: Consistency (HR portal = B2B tool feel), accelerate dev, propagate updates

**Design Tokens & Theming**:

- Variables for colors, spacing, typography (design attributes)
- **Enable**: Multi-brand support (white-label SaaS), light/dark mode swap minimal effort
- **W3C Design Tokens spec**: Standardizing token formats (Figma ↔ code sync)

**Dev Workflow Integration**:

- Living style libraries (Storybook, Figma integration)
- **Source of truth**: Coded component library (design ≡ reality, no drift)
- Governance boards: Evaluate new components, manage updates, usage metrics

**Scalable & Future-Proof**:

- Enterprise software lives decades → Update system (not rebuild from scratch)
- **Extensibility**: Bake-in i18n, accessibility, multi-device from start
- **Resultado**: Large app ecosystems agile, resilient to change

**Conexión KERNEL**:

- **CORE/06 Capacidades §4**: Design system como capacidad habilitadora C7
- **D1_Arquitectura**: Component architecture patterns
- **A4_Implementación §3**: Design system governance

---

## §5. DEVOPS & PLATFORM ENGINEERING

### CI/CD Pipelines

**Automated Build, Test, Deploy**:

- **Tools**: GitHub Actions, GitLab CI, Jenkins, CircleCI
- **Pipeline stages**: Build → Unit tests → Integration tests → Security scans → Deploy
- **Principio**: Every commit triggers pipeline (fail fast)

**Testing Pyramid**:

- **Base sólida**: Unit tests (70%)
- **Complemento**: Integration tests (20%)
- **Capa fina**: E2E tests (10%) - Cypress, Playwright

**Contract Testing**:

- Pact para microservicios (compatibility sin entorno integración completo)
- Valida consumer-provider contracts aisladamente

**Performance Testing**:

- k6, JMeter para simular carga
- Validate NFRs pre-producción (latency p95, throughput)

**Conexión KERNEL**:

- **D4_Operación §4**: CI/CD detallado (reference, no duplicar)
- **Flujo F2** (CORE/02): Automated flow como primitivo
- **P23 Feature Flags** (APLICACION/A1): Decouple deploy/release

### Infrastructure-as-Code

**Declarative Infra**:

- **Tools**: Terraform (cloud-agnostic), Pulumi (code-native), CloudFormation (AWS)
- **Beneficio**: Infra versionada Git, reproducible, auditable

**Containerization & Orchestration**:

- **Docker**: Package apps + dependencies (consistency dev → prod)
- **Kubernetes**: Orchestration standard de-facto (scheduling, scaling, self-healing)

**Deployment Strategies**:

- **Blue-Green**: Two identical envs, instant switch, instant rollback
- **Canary**: Gradual rollout (5% → 50% → 100%), monitor metrics, auto-rollback
- **Rolling**: Update instances incrementally (zero downtime)

**Conexión**: P24 Blue-Green Deployment (APLICACION/A1)

### Observability (3 Pillars)

**No es solo monitoreo** → Es capacidad de entender internal states desde outputs externos.

**Pilar 1: Logs**:

- **Structured logs** (JSON) para procesamiento automático
- **Tools**: ELK Stack (Elasticsearch, Logstash, Kibana), Loki + Grafana
- **Campos estándar**: timestamp, level, service, trace_id, message, context

**Pilar 2: Metrics**:

- **Time-series** para dashboards y alertas
- **Tools**: Prometheus (scraping, storage), Grafana (visualization)
- **Golden signals**: Latency, Traffic, Errors, Saturation (Google SRE)

**Pilar 3: Traces**:

- **Distributed tracing** para debugging bottlenecks en sistemas complejos
- **Tools**: Jaeger, Zipkin, OpenTelemetry (vendor-agnostic standard)
- **Beneficio**: End-to-end request flow visibility (microservices)

**Unified Observability**:

- **OpenTelemetry**: Single SDK for logs/metrics/traces (vendor-neutral)
- **Correlation**: trace_id links logs + metrics + spans (holistic debugging)

**Conexión KERNEL**:

- **D2_Percepción §2**: Observables técnicos (O2-O4)
- **A5_Medición §5**: DORA metrics (reference)
- **CORE/05 Smartness §4**: Observability como smartness habilitador

### Feature Flags

**Decouple Deploy ↔ Release**:

- Deploy código production (flag OFF) → Enable feature runtime (flag ON)
- **Beneficio**: Canary releases, A/B testing, instant kill switch

**Tools**: LaunchDarkly, Unleash, ConfigCat, custom (Redis-backed)

**Conexión**: P23 Feature Flags (APLICACION/A1)

---

## §6. SECURITY SHIFT-LEFT

### Principio

**Integrar seguridad desde inicio** del ciclo de vida (no post-hoc).

### Autenticación & Autorización

**Autenticación**:

- **Standards**: OAuth 2.1 / OIDC (industry standard)
- **JWT**: Stateless APIs (token-based, no server sessions)
- **MFA**: Multi-factor (algo tienes + algo sabes + algo eres)

**Autorización**:

- **RBAC** (Role-Based): Permisos por roles (simple, mayoría casos)
- **ABAC** (Attribute-Based): Permisos granulares por atributos (contexto, tiempo, recurso)
- **Principio**: Least privilege (mínimo necesario)

**Conexión KERNEL**:

- **Actor A4** (CORE/03 §4): Roles y permisos como actor capabilities
- **Límite L4** (CORE/03 §5): Authorization policies como límites de acceso

### OWASP Top 10 & Automated Detection

**SAST** (Static Application Security Testing):

- Analiza código fuente en CI pipeline (pre-commit hooks, PR gates)
- Tools: SonarQube, Checkmarx, Semgrep

**DAST** (Dynamic Application Security Testing):

- Escanea app running en staging/pre-prod
- Tools: OWASP ZAP, Burp Suite

**SCA** (Software Composition Analysis):

- Analiza dependencias terceros (vulnerabilities conocidas)
- Tools: Dependabot, Snyk, Trivy

**Principio**: Automatizar detección (no manual reviews post-deploy)

### Secrets Management

**Vault Centralizado**:

- **Tools**: HashiCorp Vault, AWS Secrets Manager, GCP Secret Manager, Azure Key Vault
- **Principio absoluto**: **NEVER hardcode secrets** (código, env vars Git, configs)

**Just-In-Time Credentials**:

- Apps/bots autentican → Obtain credentials runtime (time-bounded tokens)
- **Rotation automática**: Secrets rotan periódicamente (reduce blast radius)

**Conexión**: D4_Operación §8 Security practices

---

## §7. NFRs Y SLOs

### Non-Functional Requirements

**Performance**:

- **Latency**: p50, p95, p99 targets (ms)
- **Throughput**: Requests/sec, transactions/sec
- **Example**: API p95 latency <200ms, throughput >1000 req/s

**Availability**:

- **Uptime SLO**: 99.9% (8.76h downtime/año), 99.99% (52.6min/año)
- **Error budget**: (1 - SLO) × time_window → Budget errors/downtime permitidos

**Scalability**:

- Horizontal scaling capacity (add instances, not vertical resize)
- Auto-scaling triggers (CPU >70%, queue length >100)

### Architecture Decision Records (ADRs)

**Propósito**: Documentar decisiones arquitectónicas clave y justificaciones para futuro.

**Estructura ADR**:

1. **Context**: Problem/situation
2. **Decision**: What we decided
3. **Consequences**: Positive/negative outcomes expected
4. **Alternatives considered**: Why rejected
5. **Status**: Proposed, Accepted, Deprecated, Superseded

**Storage**: Git-versioned (markdown en `/docs/adr/`)

**Template**: T13_ADR (REFERENCIA/R6_Templates) - existente v1.4

### C4 Diagrams

**Architecture as Code** (4 niveles abstracción):

1. **Context**: System ↔ Users/External systems
2. **Containers**: High-level tech stack (apps, databases, message buses)
3. **Components**: Internal structure containers
4. **Code**: Classes/interfaces (opcional, low-level)

**Tools**: PlantUML, Structurizr, Mermaid

---

## §8. CONEXIÓN KERNEL

### Primitivos Especializados

| Primitivo KERNEL | Manifestación E7 | Ejemplo Concreto |
|:---|:---|:---|
| **Recurso** | Applications, tech stack, infrastructure, platform | API Gateway (R3), PostgreSQL cluster (R3), K8s cluster (R3) |
| **Flujo** | CI/CD pipelines, user workflows, data flows | GitLab CI pipeline (F2 Automated), User checkout flow (F1 Manual) |
| **Actor** | Developers, SRE, DevOps Eng, Platform Eng, End-users | DevOps Engineer (A3 Specialized), End-user (A1 Principal) |
| **Límite** | NFRs, SLOs, API contracts, regulatory, error budgets | API p95 <200ms (L1 Performance), WCAG AA (L3 Regulatory) |

### Dominios KERNEL Extendidos

**D1_Arquitectura**:

- Stack patterns (§2 E7) extend D1 architecture thinking
- Conway's Law aplicado (D1 §1 P4)
- ADRs como architectural decisions traceable

**D2_Percepción**:

- Tech observables: DORA metrics (deploy freq, lead time, MTTR, change failure rate)
- Uptime %, error rate %, latency p95
- **Extension**: D2 + §8 Tech Observables (Week 6)

**D3_Decisión**:

- Stack selection framework (§3 decision framework)
- Trade-offs analysis explicit (tabla §2)
- Build vs Buy decisions

**D4_Operación**:

- CI/CD practices (D4 §4 existing, reference)
- Deployment strategies (blue-green, canary, rolling)
- SRE on-call rotations, incident response

### Delegación M1-M6 en UX Layer

| Modo Delegación | Manifestación UX/Tech | Ejemplo E7 |
|:---|:---|:---|
| **M1 Monitor** | Dashboards pasivos, alertas | Grafana dashboard operations (human monitors) |
| **M2 Inform** | Chatbots info-only, knowledge bases | FAQ bot (inform, no execute) |
| **M3 Enable** | AI copilots, predictive UX, auto-suggest | Microsoft Copilot draft email (enable user, user approves) |
| **M4 Control** | Automated testing gates, quality checks | CI pipeline auto-reject PR (fails tests, human fixes) |
| **M5 Co-produce** | AI-assisted coding, pair programming | GitHub Copilot code suggestions (human edits, approves) |
| **M6 Execute** | Automated deployments, self-healing infra | K8s auto-restart failed pods, auto-scale (bounded, monitored) |

**Conexión**: CORE/04 Delegación §3-§8 (matriz completa)

---

## §9. CASOS DE USO

### Caso 1: Startup Monolito → Microservicios (Migration)

**Contexto**:

- Startup SaaS B2B, 10 engineers → 50 engineers en 3 años
- Monolito Ruby on Rails (150K LOC)
- **Pain points**: Deploy freq 1 cada 3 semanas (bottleneck), merge conflicts daily, testing suite 45 min (slow feedback)

**Approach (Pattern P06 Inverse Conway)**:

1. **Año 1**: Mantener monolito, agregar **modularización interna** (bounded contexts DDD)
   - 3 contexts: Authentication, Billing, Analytics
   - Refactor internal APIs claras entre contexts
2. **Año 2**: Split teams por context (3 teams × 10-15 eng)
   - Architecture follows org (Conway's Law)
3. **Año 3**: Extract 2 microservicios críticos
   - **Billing** (alta volatilidad reglas negocio, deploy frecuente necesario)
   - **Authentication** (security isolation, independent scaling)
   - Mantener Analytics en monolito (stable, bajo cambio)

**Stack**:

- Monolito: Ruby on Rails (legacy)
- Microservicios: Node.js (NestJS) - team preference, faster iteration
- Infra: K8s (GKE), PostgreSQL (cada microservicio su DB), Redis (cache shared), Kafka (event bus)
- Observability: OpenTelemetry + Jaeger + Prometheus + Grafana

**Métricas**:

- **Deploy frequency**: 1 cada 3 semanas → 5/día (DORA Elite)
- **Lead time**: 15 días → 2 días
- **MTTR**: 4 horas → 45 min
- **Change failure rate**: 15% → 8%

**Timeline**: 18 meses (modularización 6m, split teams 6m, extract 6m)

**Conexión KERNEL**:

- **P06 Inverse Conway** (A1): Pattern aplicado explícitamente
- **D4 §4 CI/CD**: Execution practices
- **A5 §5 DORA**: Metrics framework

### Caso 2: Enterprise Multi-Product Design System

**Contexto**:

- Enterprise 5 productos B2B SaaS
- **Pain**: Inconsistencia UX (cada producto UI diferente), Dev velocity bajo (reinvent components cada vez)

**Solución** (§4.7 Design System):

1. **Audit**: Inventario components 5 productos → 347 componentes, 89% duplicados
2. **Design**: Unified component library (42 core components)
3. **Governance**: Design System team (3 designers, 2 FE engineers)
4. **Adoption**: Migrate producto por producto (6 meses cada)

**Stack**:

- Component library: React + TypeScript + Storybook
- Design tokens: JSON format (W3C spec)
- Distribution: NPM private registry

**Métricas**:

- **Dev velocity**: +40% (time-to-market new features)
- **Consistency score**: 35% → 95% (automated UI tests)
- **Component reuse**: 12% → 78%
- **Design-dev handoff time**: 5 días → 1 día

**Timeline**: 24 meses (design 6m, build 6m, adoption 12m)

### Caso 3: SaaS Multi-Tenant Architecture

**Contexto**: Single-tenant app → Multi-tenant migration (scale 50 customers → 5000)

**Patterns**:

- **DB per tenant** (isolation máxima, compliance)
- **Feature flags per tenant** (gradual rollout, A/B testing)
- **Tenant-aware observability** (metrics per tenant)

**Resultado**:

- **Onboarding**: 2 semanas → 2 horas (automated provisioning)
- **Cost per tenant**: -60% (shared infra)
- **Compliance**: Tenant isolation garantizada (GDPR, SOX)

**Conexión**: P23 Feature Flags, D4 §7 Multi-tenancy patterns

---

## §10. ANTIPATRONES TECH ENTERPRISE

**IMPORTANTE**: Definiciones canónicas de antipatrones AP41-AP43 viven en `APLICACION/A2_Antipatrones.md` §8 (single source of truth). Esta sección provee **ejemplos concretos E7-specific** y detalles de implementación.

**Ver A2 §8 para**: Síntoma, Causa Raíz, Consecuencia, Fix, Severidad.

---

### AP41: Premature Microservices - Implementación E7

**Reference**: `A2_Antipatrones.md` §8 AP41 (definición completa)

**Ejemplo E7**: Startup 10 engineers, arquitectura target

**Anti-pattern observado**:
```yaml
Startup_Real_Case:
  Engineers: 10
  Microservices: 18 (cada bounded context = service)
  Overhead:
    - Service discovery: Consul setup 2 semanas
    - Distributed tracing: Jaeger + instrumentation 3 semanas
    - API gateway: Kong config 1 semana
    - Local dev: Docker-compose 25 services, 32GB RAM
  
  Velocity_Impact:
    - Feature delivery: 2 weeks → 6 weeks
    - Onboarding: 1 semana → 4 semanas (cognitive load)
    - Debug session: 30min → 4 horas (trace across services)
```

**Fix aplicado (retrospective)**:
```yaml
Refactor_Journey:
  Month_0: Collapse 18 services → 3 módulos monolito
  Month_3: Velocity recovery +200%
  Month_12: Extract 2 services críticos (payments, auth)
  Month_18: Arquitectura óptima: 1 monolito + 2 microservices
```

**Conexión**: §2 Trade-Offs Matrix (cuando microservices correcto), P54 Piecemeal Growth

---

### AP42-AP43: Ver A2 §8 + Ejemplos E7

**AP42: Frontend-Backend Coupling** (`A2_Antipatrones.md` §8 AP42)  
**Ejemplo E7**: SPA React acopla directamente a Django ORM schemas - Breaking changes cada backend migration, frontend rewrites 3× en 18 meses.

**AP43: Big Design Up Front (BDUF)** (`A2_Antipatrones.md` §8 AP43)  
**Ejemplo E7**: 6 meses UML/C4 diagrams detallados → Requirements cambió 40% → 4 meses diseño desperdicio. Fix: P55 Walking Skeleton implementado (skeleton funcional semana 1).

---

## §11. PLANTILLAS RELACIONADAS

### Plantillas Técnicas

**T19_App_Inventory** (REFERENCIA/R6_Templates, nuevo v2.0):

- Metadatos de la aplicación (stack, observabilidad, NFRs, salud)
- Trazabilidad KERNEL (primitivos, dominios, delegación)
- Puntuación de deuda técnica, instantánea de métricas DORA

**T13_ADR** (existente v1.4):

- Registro de Decisión de Arquitectura
- Referencia para decisiones de stack y arquitectura

### Plantillas de Contratos

**T15_Contrato_Datos** (nuevo v2.0):

- Contratos de datos para aplicaciones intensivas en datos (referencia E8 §3)

**T20_Data_Product_Spec** (nuevo v2.0):

- Para aplicaciones que son productos de datos (referencia E8 §4)

**Conexión**: E8_Intelligent_Systems para contratos detallados (no duplicar aquí)

---

## §12. MÉTRICAS

### Métricas DORA

**4 Métricas Clave** (investigación DORA de Google, estándar de la industria):

| Métrica | Élite | Alto | Medio | Bajo |
|:---|:---|:---|:---|:---|
| **Frecuencia de Despliegue** | Bajo demanda (>1/día) | 1/semana - 1/mes | 1/mes - 6/mes | <1 cada 6 meses |
| **Tiempo de Entrega para Cambios** | <1 día | 1 día - 1 semana | 1 semana - 1 mes | 1-6 meses |
| **Tiempo de Restauración (MTTR)** | <1 hora | <1 día | 1 día - 1 semana | >1 semana |
| **Tasa de Fallos en Cambios** | 0-15% | 16-30% | 31-45% | 46-60% |

**Conexión KERNEL**:

- **A5_Medición §5**: Métricas DORA detalladas (referencia, no duplicar)
- **D2_Percepción**: DORA como observables técnicos

### Puntuación de Salud Técnica

**Formula**:

```
Puntuacion_Salud_Tecnica = (Salud_Infraestructura + Salud_Seguridad + Salud_Observabilidad + Madurez_DevOps) / 4
```

**Componentes** (cada uno de 0 a 100):

1. **Salud_Infraestructura**:
   - % de tiempo de actividad (peso 0.4)
   - Efectividad del autoescalado (0.3)
   - Utilización óptima de recursos (0.3)

2. **Salud_Seguridad**:
   - Vulnerabilidades críticas = 0 (0.5)
   - Cumplimiento de la gestión de secretos (0.3)
   - % de adopción de MFA (0.2)

3. **Salud_Observabilidad**:
   - % de cobertura de logs/métricas/trazas (0.4)
   - Cobertura de alertas en rutas críticas (0.3)
   - Tiempo medio de detección (MTTD) <5min (0.3)

4. **Madurez_DevOps**:
   - Puntuación compuesta de DORA (0.6)
   - % de cobertura de IaC (0.2)
   - Cobertura de pruebas automatizadas (0.2)

**Benchmarks**:

- **>85**: Excellent (world-class)
- **70-85**: Good (industry standard)
- **<70**: Needs attention

### Tech Debt Score

**Reference**: D4_Operación §5 Tech Debt detallado (no duplicar)

**Integración**: TH_Score complementa H_Score (CORE/05) para dimensión tech.

**Conexión**: A5_Medición §10 Tech Metrics (extension v2.0 Week 7)

---

## REFERENCIAS CRUZADAS

### CORE

- **CORE/01 Recurso**: Stack como recurso habilitador
- **CORE/02 Flujo**: CI/CD como flujo automatizado
- **CORE/03 Actor**: Developers, SRE como actores especializados
- **CORE/03 Límite**: NFRs, SLOs como límites operacionales
- **CORE/04 Delegación §8**: Purpose 1 Assistant (AI copilots UX)
- **CORE/05 Smartness**: Observability como smartness habilitador

### DOMINIOS

- **D1_Arquitectura §1 P4**: Conway's Law awareness
- **D1 §14** (extension v2.0): Tech Stack Patterns detallado
- **D2_Percepción §2**: Observables base O1-O11
- **D2 §8** (extension v2.0): Tech Observables OT1-OT3
- **D3_Decisión §3**: Decision modes arquitectónicos
- **D4_Operación §4**: CI/CD detallado (primary reference)
- **D4 §5**: Tech debt management
- **D4 §8**: Security practices

### APLICACION

- **A1_Patrones**:
  - P06 Inverse Conway's Law
  - P23 Feature Flags
  - P24 Blue-Green Deployment
  - P54 Piecemeal Growth
  - P55 Walking Skeleton
  - P56 Continuous Refactoring
- **A2_Antipatrones**: AP_TECH1-3 cross-reference
- **A3_Diagnóstico §4**: UX friction assessment
- **A4_Implementación §3**: Design system governance
- **A5_Medición §5**: DORA metrics framework (primary reference)

### DOMINIOS_ESPECIALIZADOS

- **E8_Intelligent_Systems**: Data/AI/Process/Knowledge (orthogonal, minimal overlap infra K8s/OpenTelemetry)
- **E2_Público §6**: Gov UX requirements (sector-specific)
