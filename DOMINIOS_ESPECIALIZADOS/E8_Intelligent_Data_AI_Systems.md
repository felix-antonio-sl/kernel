# E8_Intelligent_Data_AI_Systems

**Versión:** 2.0.0  
**Estado:** Production (Week 1 - Parcial §1-§3)  
**Audiencia:** Data Architects, AI/ML Engineers, BPA Specialists, Knowledge Engineers  
**Dependencias**: CORE/01-08, DOMINIOS/D1-D4, APLICACION/A1-A5, E7_Enterprise_Technology

---

## §1. PROPÓSITO & METAMODELO

### Definición

Este dominio especializado cubre **sistemas integrados de Datos, IA, Procesos y Conocimiento** como un todo coherente. Integra Data-as-Product, AI Orchestration, Business Process Automation y Knowledge Management bajo un metamodelo unificado de **contratos, observabilidad y governance embebida**.

### Alcance

**INCLUYE**:

- **Data-as-Product** (lifecycle, contracts, quality, lakehouse, lineage, MDM, FinOps)
- **AI Orchestration** (model serving, RAG, agents, guardrails, evaluation, multi-agent)
- **Knowledge Management** (curation, indexación híbrida, RAG auditable, ISO 30401)
- **Process Automation** (BPM, BPA, RPA, BPMN ejecutable, Sagas, HITL)
- **Contratos Unificados** (4 tipos: Datos, Proceso, Agente, Conocimiento)
- **Observabilidad Unificada** (data + AI + process end-to-end)
- **Governance & Compliance** (policy-as-code, zero-trust, FinOps, ethics)

**EXCLUYE** (cubiertos por E7 o CORE):

- App development, UX/UI, DevOps básico → **E7_Enterprise_Technology**
- Foundation concepts → **CORE** (Delegación M1-M6 en CORE/04 §3-§8)
- Generic patterns → **APLICACION/A1** (P57-P63 tech patterns allí, aquí referenced)

### Conexión KERNEL

**Primitivos especializados**:

- **Dato** → ProductoDeDatos, Documento, Chunk, Feature
- **Actor** → LLM_Agent, RPA_Bot, Data_Engineer, Knowledge_Engineer, BPMN_Orchestrator
- **Flujo** → BPMN_Process, ETL_Pipeline, RAG_Pipeline, Saga_Flow
- **Recurso** → Lakehouse, Model_Endpoint, Vector_DB, Knowledge_Base, Workflow_Engine
- **Señal** → Evento (EDA), DQ_Violation, Process_Exception, AI_Guardrail_Trigger

**Dominios extendidos**:

- **D1**: Tech stack patterns (reference E7), data architecture (lakehouse)
- **D2**: Se introducen Observables Técnicos de Diagnóstico (OT1-OT3) que sirven como métricas de causa raíz para los 16 observables canónicos.
- **D3**: Algorithmic decision modes D5-D7 (RAG, ReAct, Plan) - extension v2.0
- **D4**: Tech execution E4-E6 (Orquestada, Reactiva, Asistida) - extension v2.0

**Delegación M1-M6 en Intelligent Systems**:

- **RAG** → M3-M4 (Enable/Control: Augment human, bounded)
- **ReAct** → M4-M5 (Control/Co-produce: Tool calling, HITL checkpoints)
- **Plan & Execute** → M5-M6 (Co-produce/Execute: Multi-step autonomy, supervised)

### Meta-Principios E8

1. **Contratos como cimiento**: Todo artefacto (data, process, agent, knowledge) opera bajo contrato semántico
2. **Governance embebida**: Guardrails éticos/técnicos/operacionales desde diseño → operación
3. **Observabilidad como requisito**: Métricas, traces, lineage activo para auditar decisiones humanas y de IA
4. **HITL por defecto en riesgo**: Human-in-the-loop checkpoints en alta incertidumbre/impacto
5. **Federación con guardrails**: Dominios autónomos, estándares comunes, policy-as-code

**Conexión**: CORE/04 Delegación §5 C6 Bounded Autonomy (autonomía acotada por guardrails)

---

## §2. ARQUITECTURA REFERENCIA 6 CAPAS

### Metamodelo Integrado

**Arquitectura modular por capas** que integra experiencia, orquestación, inteligencia, datos, integración y plataforma en un stack coherente.

```
┌─────────────────────────────────────────────────────────────────────┐
│ Layer 1: EXPERIENCE & AGENTS                                        │
│ • Copilots, Chatbots, Dashboards, APIs, Voice Interfaces            │
│ • Delegation: M2-M4 (Inform, Enable, Control)                       │
└─────────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────────┐
│ Layer 2: ORCHESTRATION                                              │
│ • Workflow Engines (BPMN: Camunda, Temporal)                        │
│ • Multi-Agent Orchestration (Router, Supervisor-Worker)             │
│ • Event Bus (Kafka, RabbitMQ, NATS)                                 │
│ • Rules Engine (Drools, decision tables)                            │
│ • Delegation: M4-M5 (Control, Co-produce)                           │
└─────────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────────┐
│ Layer 3: INTELLIGENCE & PROCESSING                                  │
│ • LLMs (OpenAI-compatible endpoints, vLLM, TGI, SGLang)             │
│ • RAG (Retrieval-Augmented Generation)                              │
│ • IDP/OCR (Intelligent Doc Processing: Tesseract, Azure Form)       │
│ • Rules Engines, RPA (UI automation: UiPath, Automation Anywhere)   │
│ • Delegation: M3-M6 (Enable → Execute según autonomy)               │
└─────────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────────┐
│ Layer 4: DATA PLATFORM                                              │
│ • Lakehouse (Delta Lake, Iceberg, Hudi - ACID, time-travel)         │
│ • Feature Store (Feast, Tecton - offline/online parity)             │
│ • Vector DB (Qdrant, Milvus, Weaviate, pgvector)                    │
│ • Semantic Cache (Redis - prompt+retrieval hash)                    │
│ • OLAP (Clickhouse, Druid - analytics queries)                      │
│ • Knowledge Base (curated documents, chunks indexed)                │
└─────────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────────┐
│ Layer 5: INTEGRATION                                                │
│ • API Gateway (Kong, Apigee - rate limits, auth, versioning)        │
│ • Message Bus (Kafka, RabbitMQ - async, event-driven)               │
│ • MDM/RDM (Master/Reference Data Mgmt - golden records)             │
│ • Data Catalog (Unity, DataHub, Amundsen - discovery, lineage)      │
│ • Schema Registry (Confluent, Apicurio - schema evolution)          │
└─────────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────────┐
│ Layer 6: PLATFORM ENGINEERING                                       │
│ • Containers (Docker) + Orchestration (Kubernetes)                  │
│ • IaC (Terraform, Pulumi - declarative infra)                       │
│ • Observability (OpenTelemetry, Prometheus, Grafana, Jaeger)        │
│ • Security (RBAC/ABAC, secrets vault, mTLS, JWT/OIDC)               │
│ • FinOps (Showback/chargeback, rightsizing, cost allocation)        │
└─────────────────────────────────────────────────────────────────────┘
```

### Fuentes Arquitectura

- **OCE metamodelo 6 capas**: Base structure (layers 1-3, 6)
- **BPA arquitectura**: Layer 2 orchestration overlay (BPMN, sagas)
- **DATA platform**: Layer 4 expanded (lakehouse, feature store, catalogs)
- **KNOW curation**: Layer 4 knowledge base + Layer 3 RAG
- **E7 platform engineering**: Layer 6 referenced (no duplicar, cross-ref)

### Orthogonality E7-E8

| Aspecto | E7 Coverage | E8 Coverage | Overlap |
|:---|:---|:---|:---|
| **Apps/UX/Frontend** | ✓ Primary | — | 0% |
| **DevOps/CI/CD** | ✓ Primary | Reference | 5% (pipelines data) |
| **Platform Infra (K8s)** | ✓ Primary | Reference | 10% (shared) |
| **Observability (OTel)** | ✓ Foundation | ✓ Extended (data/AI) | 15% (shared stack) |
| **Data Platform** | — | ✓ Primary | 0% |
| **AI/ML Systems** | — | ✓ Primary | 0% |
| **Process Automation** | — | ✓ Primary | 0% |
| **Knowledge Mgmt** | — | ✓ Primary | 0% |

**Overlap total**: ~10% (inevitable infra compartida K8s, OpenTelemetry)  
**Orthogonality**: 90% ✓ (superior a target 85%)

**Conexión KERNEL**:

- **I2 Ortogonalidad** (CORE/00_Manifiesto.md §1): E7-E8 satisface invariante
- **P7 Separation of Concerns**: Capas ortogonales (cada una responsabilidad única)

---

## §3. CONTRATOS UNIFICADOS (SIGMA Core Absorbed)

### Principio Contract-Driven

**Todo artefacto inteligente opera bajo contrato semántico** que define:

- Qué promete (interfaces, schema, SLO)
- Cómo evoluciona (semver, deprecation windows, backward compatibility)
- Cómo se observa (lineage, metrics, alertas)
- Cómo se gobierna (ownership, policies, access control)

**Beneficios**:

- **Clarity**: Expectations explícitas (producer-consumer)
- **Evolution**: Cambios controlados (no breaking changes silenciosos)
- **Observability**: Contracts activan monitoring automático
- **Governance**: Policy-as-code enforce contracts

**Origen**: SIGMA.md §5 Contratos Canónicos (absorbed como E8 §3, no domain separado)

### §3.1 Contract Base Structure

**Estructura común** (4 tipos heredan):

```yaml
# METADATA
type: [data|process|agent|knowledge]_contract
id: "<domain>_<entity>_<version>"
version: "X.Y.Z"  # Semantic versioning
owner: ["<team>", "<email>"]

# SEMANTICS
glossary_refs: ["<term1>", "<term2>"]  # Business terms canonical
business_rules:
  - name: "<rule_name>"
    rule: "<validation_logic>"
    severity: [error|warn]

# INTERFACES
endpoints: ["<uri1>", "<uri2>"]  # SQL, REST, GraphQL, gRPC
schema_ref: "<schema_registry_url>"  # Schema versionado externo

# SLO (Service-Level Objectives)
slo:
  availability_pct: 99.9
  latency_p95_ms: 200
  throughput_min_rps: 100

# QUALITY
quality:
  checks:
    - {name: "<check_name>", rule: "<validation>", severity: [error|warn]}
  error_budget_pct: 0.1  # (1 - SLO availability)

# SECURITY
security:
  classification: [P0|P1|P2|P3]  # Criticality
  pii: [true|false]
  access_control: {roles: ["<role1>", "<role2>"], policy: "<OPA_policy_ref>"}

# CHANGES (Evolution)
changes:
  policy: semver  # Major (breaking), Minor (backward-compat), Patch (fixes)
  deprecation_window_days: 90
  coexistence_strategy: [dual-write|adapter|migration]

# OPERATIONS
operations:
  lineage: ["<upstream1> -> <transform> -> <downstream1>"]
  observability:
    metrics: ["<metric1>", "<metric2>"]
    alerts: ["<alert_rule1>"]
  runbook: "<wiki_url_or_repo_path>"
```

**Conexión KERNEL**:

- **Límite L2** (CORE/03 §3): Contracts como límites semánticos explícitos
- **D3_Decisión §6**: Contracts como decisiones cristalizadas
- **P62 Contract-Driven Evolution** (APLICACION/A1 v2.0): Pattern derivado

### §3.2 Contrato Datos (Data Contract)

**Extensión específica** (base + DATA specialization):

```yaml
type: data_contract
product: billing_invoices  # Data product name
version: 2.1.0

# METADATA (inherited)
owner: ["dom-finanzas", "dp-owner@empresa.cl"]
interfaces:
  - "sql:warehouse.gold.billing_invoices"
  - "rest:/api/v1/invoices"

# SEMANTICS (inherited + extended)
semantics:
  glossary_refs: ["Factura", "Nota de crédito", "Cliente"]
  business_rules:
    - name: valid_invoice_status
      rule: "status in [ISSUED, PAID, VOID, CANCELLED]"
      severity: error
    - name: amount_positive
      rule: "amount_total >= 0"
      severity: error
  data_domain: "Finanzas"  # Domain ownership

# SCHEMA (data-specific)
schema:
  primary_key: [invoice_id]
  partition_key: [issue_date]  # For lakehouse optimization
  fields:
    - {name: invoice_id, type: string, required: true, description: "Unique ID"}
    - {name: customer_id, type: string, required: true}
    - {name: amount_total, type: "decimal(18,2)", unit: CLP, required: true}
    - {name: issued_at, type: timestamp, timezone: "America/Santiago", required: true}
    - {name: status, type: string, enum: [ISSUED, PAID, VOID, CANCELLED], required: true}
  scd_type: 2  # Slowly Changing Dimension Type 2 (history preserved)

# SLO (data-specific)
slo:
  freshness_p95_minutes: 30  # Data freshness
  availability_pct: 99.9
  accuracy_variance_pct: 0.3  # vs source-of-truth (ERP)

# QUALITY (data-specific)
quality:
  dimensions: [exactitud, completitud, validez, unicidad, consistencia, frescura]
  checks:
    - {name: pk_unique, rule: "unique(invoice_id)", severity: error}
    - {name: status_domain, rule: "in_domain(status)", severity: error}
    - {name: late_arrival, rule: "event_time_diff < 24h", severity: warn}
  dq_framework: great_expectations  # or Deequ, Soda
  error_budget_violations_per_1k: 0.8  # Max violations tolerable

# SECURITY (data-specific)
security:
  classification: P1  # Business-critical
  pii: false
  phi: false  # Protected Health Information
  access_control:
    roles: [billing_analyst, finance_engineer, auditor_readonly]
    rls_policy: "opa://policies/billing_rls"  # Row-Level Security
    cls_enabled: false  # Column-Level Security

# OPERATIONS (data-specific)
operations:
  lineage:
    as_designed: "kafka.billing.events -> bronze.billing -> silver.billing -> gold.billing_invoices"
    as_implemented_tool: openlineage  # Harvest runtime lineage
    column_level: true
  observability:
    metrics: [freshness_p95, dq_violations_per_1k, latency_query_p95, error_budget_consumption]
    alerts:
      - {rule: "freshness_p95 > 45min", severity: warn, channel: slack}
      - {rule: "dq_violations_per_1k > 1.0", severity: error, channel: pagerduty}
  serving_interfaces:
    - {type: sql, endpoint: "warehouse.gold.billing_invoices", slo_latency_p95_ms: 500}
    - {type: rest, endpoint: "/api/v1/invoices", slo_latency_p95_ms: 200}
```

**Fuente**: DATA.md §5 completo (contracts estructura base)

**Conexión KERNEL**:

- **P57 Data Product Pattern** (APLICACION/A1 v2.0): Pattern aplicado
- **T15_Contrato_Datos** (REFERENCIA v2.0): Template detallado
- **T20_Data_Product_Spec** (REFERENCIA v2.0): Product-level spec

### §3.3 Contrato Proceso (Process Contract)

**Extensión específica** (base + BPA + SIGMA specialization):

```yaml
type: process_contract
process: invoice_approval_workflow
version: 1.3.0

# METADATA (inherited)
owner: ["finanzas-ops", "process-owner@empresa.cl"]

# SEMANTICS (inherited + process-specific)
semantics:
  glossary_refs: ["Factura", "Aprobación", "Workflow", "Excepción"]
  business_rules:
    - name: approval_required_threshold
      rule: "invoice.amount_total > 10000 CLP"
      severity: error

# SLA (process-specific, not SLO)
sla:
  cycle_time_p95_minutes: 180  # p95 end-to-end duration
  stp_target_pct: 80  # Straight-Through Processing (no human intervention)
  hitl_queue_slo_minutes: 30  # Human-in-the-Loop response time

# SAGA (compensations for distributed transactions)
saga:
  pattern: orchestrated  # vs choreographed
  compensations:
    - {step: "post_to_ERP", compensation_action: "revert_posting", idempotent: true}
    - {step: "notify_approver", compensation_action: "cancel_notification", idempotent: true}

# HITL (Human-in-the-Loop checkpoints)
hitl:
  queues:
    - {name: "exceptions.approval", escalation_sla_hours: 48, escalation_to: "supervisor"}
    - {name: "exceptions.validation_failed", escalation_sla_hours: 24, escalation_to: "data_steward"}
  triggers:
    - {condition: "amount_total > 10000", route_to: "exceptions.approval"}
    - {condition: "validation_score < 0.85", route_to: "exceptions.validation_failed"}

# EVENTS (process publishes/consumes)
events:
  consumes:
    - {name: "invoice.received", schema_ref: "avro://billing/invoice/v1", delivery: at_least_once}
  publishes:
    - {name: "invoice.approved", schema_ref: "avro://billing/approval/v1", delivery: exactly_once}
    - {name: "invoice.rejected", schema_ref: "avro://billing/rejection/v1", delivery: at_least_once}

# IDEMPOTENCY (critical for retries)
idempotency:
  keys: [invoice_id]
  deduplication_window_hours: 72

# RPA FALLBACK (last resort if API fails)
rpa_fallback:
  enabled: true
  triggers: ["erp_api_timeout", "erp_api_500_error"]
  guardrails:
    - credential_vault_required: true
    - screen_selector_stability_check: true
    - max_retries: 3

# OPERATIONS (process-specific)
operations:
  orchestrator: camunda  # or Temporal, Airflow
  bpmn_model_uri: "repo://processes/invoice_approval_v1.3.bpmn"
  observability:
    metrics: [cycle_time_p95, stp_pct, error_rate, hitl_backlog_size, compensation_rate]
    alerts:
      - {rule: "cycle_time_p95 > 240min", severity: warn}
      - {rule: "stp_pct < 75%", severity: error}
      - {rule: "hitl_backlog_size > 50", severity: warn}
```

**Fuente**: BPA.md §2 + SIGMA.md §5.2 (process contracts)

**Conexión KERNEL**:

- **P59 Saga Compensation Pattern** (A1 v2.0): Compensations deterministas
- **P60 HITL Checkpoint Pattern** (A1 v2.0): Human checkpoints
- **T16_Contrato_Proceso** (REFERENCIA v2.0): Template detallado
- **T22_Process_Model_BPMN** (REFERENCIA v2.0): BPMN spec

### §3.4 Contrato Agente (Agent Contract)

**Extensión específica** (base + OCE + SIGMA specialization):

```yaml
type: agent_contract
agent: invoice_pre_reviewer
version: 2.0.0

# METADATA (inherited)
owner: ["ai-eng-team", "ai-owner@empresa.cl"]

# AUTONOMY & ROLE (agent-specific)
autonomy_level: PLAN_AND_EXECUTE  # RAG < ReAct < Plan&Execute
role: COPRODUCIR  # Maps to CORE/04 Delegation M5
delegation_mode: M5  # Explicit KERNEL mapping

# CAPABILITIES (agent-specific)
capabilities:
  - extract_invoice_data  # IDP capability
  - validate_business_rules  # Rules engine
  - query_knowledge_base  # RAG capability
  - interact_erp_api  # Tool calling

# TOOLS (functions agent can call)
tools:
  - {name: kb_search_secure, endpoint: "/api/kb/search", permissions: read, quota_calls_per_hour: 1000}
  - {name: erp_api_post, endpoint: "/api/erp/invoices", permissions: write, quota_calls_per_hour: 100}
  - {name: doc_parser_vision, endpoint: "/api/vision/parse", permissions: read, quota_calls_per_hour: 500}

# RAG POLICY (knowledge retrieval)
rag_policy:
  retrieval:
    hybrid: true  # BM25 + vector
    filters: ["vigente:true", "confidencialidad<=role"]
    reranking: cross_encoder  # Autoridad, entidades, proximity
    top_k: 10
  context_assembly:
    max_tokens: 4000
    by: "articulo/seccion"  # Chunk boundaries
    add_hierarchy: true  # Document path context
  citations:
    required: true
    granularity: "articulo/pagina"  # Citation precision
  mode: extractive  # vs abstractive (for normative content)

# GUARDRAILS (4 types)
guardrails:
  input:  # Pre-LLM
    - prompt_rewrite  # Sanitize, structure
    - pii_detection  # Redact sensitive
    - injection_defense  # Prompt injection prevention
  output:  # Post-LLM
    - schema_validation: json  # Validate output structure
    - faithfulness_check: true  # vs retrieved context
    - toxicity_scan: true  # Content moderation
    - citation_validation: true  # All claims cited
  operational:  # Runtime limits
    - max_iterations: 5  # For ReAct/Plan loops
    - timeout_seconds: 120
    - token_cost_limit_usd: 2.0  # FinOps
  ethical:  # Bias, fairness
    - bias_detection: true
    - fairness_constraints: demographic_parity  # For sensitive decisions

# QUALITY METRICS (agent-specific)
quality_metrics:
  faithfulness_min: 0.9  # Grounding to context
  citation_exactness_min: 0.95  # Citation accuracy
  hallucination_rate_max: 0.05  # 5% max
  ttft_p95_ms: 1200  # Time-to-First-Token
  cost_per_resolution_usd_max: 0.50

# HITL CHECKPOINTS (agent-specific)
hitl_checkpoints:
  - {condition: "confidence_score < 0.85", action: "pause_for_human_review"}
  - {condition: "conflict_detected", action: "escalate_to_expert"}
  - {condition: "amount_total > 50000", action: "require_supervisor_approval"}

# STATE & MEMORY (agent-specific)
state_management:
  short_term:
    - session_context  # Conversation history
    - tool_context  # Intermediate results
  long_term:
    - entity_memory  # Customer facts, TTL 30 days
    - knowledge_base  # Shared, persistent
  consistency: event_sourcing  # For multi-agent coordination

# EVALUATION HARNESS (offline + online)
evaluation:
  offline:
    golden_set: "test_cases/invoice_approval_v1.json"
    metrics: [faithfulness, citation_exactness, task_success_rate]
    frequency: pre_deploy
  online:
    sampling_rate: 0.10  # 10% traffic
    metrics: [latency_p95, cost_per_task, user_satisfaction_csat]
    frequency: continuous

# OPERATIONS (agent-specific)
operations:
  model_serving:
    runtime: vllm  # or TGI, SGLang
    model: "gpt-4o-mini"  # or local LLM
    endpoint: "https://api.openai.com/v1/chat/completions"
    autoscaling:
      min_replicas: 1
      max_replicas: 10
      target_queue_length: 5
  observability:
    metrics: [ttft_p95, faithfulness, citation_exactness, cost_per_task, gpu_utilization]
    traces: opentelemetry  # Spans per agent invocation
```

**Fuente**: OCE.md completo + SIGMA.md §5.3

**Conexión KERNEL**:

- **CORE/04 Delegación §8**: Purpose 1 Assistant (M3-M5 agent roles)
- **C6 Bounded Autonomy** (CORE/04 §5): Guardrails implement bounded autonomy
- **P53 Orchestration Agent** (CORE/04 §8): Pattern agente orquestador
- **P61 Multi-Agent Orchestration** (A1 v2.0): Pattern multi-agent
- **T17_Contrato_Agente** (REFERENCIA v2.0): Template detallado
- **T21_AI_Agent_Spec** (REFERENCIA v2.0): Deployment spec

### §3.5 Contrato Conocimiento (Knowledge Contract)

**Extensión específica** (base + KNOW + SIGMA specialization):

```yaml
type: knowledge_contract
collection: normativa_interna_rrhh
version: 1.2.0

# METADATA (inherited)
owner: ["legal-team", "knowledge-eng@empresa.cl"]

# AUTHORITY (knowledge-specific)
authority: official_only  # Only authoritative sources
sources:
  - {type: "resolutions", repo: "documental/resoluciones", vigente: true}
  - {type: "instructivos", repo: "documental/instructivos", vigente: true}

# DOCUMENT UNITS (knowledge-specific)
doc_units: [expediente, documento, seccion, articulo, clausula]

# METADATA MINIMUM (knowledge-specific, per document)
metadata_min:
  - id_doc
  - tipo_documental
  - emisor
  - fecha_emision
  - vigencia_desde
  - vigencia_hasta
  - estado_normativo  # vigente, derogado, en_tramite
  - materia
  - hash_sha256
  - version
  - acl  # Access Control List

# INDEXING (hybrid)
indexing:
  lexical:
    method: bm25
    fields: [titulo, sumario, articulado, anexos]
    boost: {titulo: 2.0, articulado: 1.5}  # Field importance
  vector:
    model: text-embedding-3-large  # or sentence-transformers
    model_version: "v3"
    dimensions: 1024
    fields: [titulo, sumario, articulado]
  filters:
    query_time:
      - {field: estado_normativo, value: vigente}
      - {field: confidencialidad, operator: "<=", value: user_role}
  reranking:
    enabled: true
    method: cross_encoder
    features: [entidad_match, fecha_match, proximidad_estructural, autoridad_score]

# CHUNKING (knowledge-specific)
chunking:
  strategy: structural  # Respect semantic boundaries
  by: [articulo, clausula, seccion]
  context_hierarchy: true  # Add document path, article number
  overlap_strategy: sliding_window  # For multi-context reasoning
  chunk_size_tokens: 512
  overlap_tokens: 50

# SERVING (RAG-specific)
serving:
  context_assembly:
    by: "articulo/seccion"
    add_hierarchy: true
    max_chunks: 10
    diversity_balance: 0.3  # Multiple sources vs single-source depth
  citation_policy: required_exact  # Mandatory, article-level precision
  response_mode: extractive_default  # For normative, abstractive for summaries
  ambiguity_handling: explicit_versions  # Disambiguate vigente vs anterior

# AUDIT (knowledge-specific)
audit:
  chain_of_custody: true  # Track document→chunk→retrieval→response
  snapshots: true  # Immutable index snapshots (reproducibility)
  retention_days: 2555  # 7 years (compliance)

# SLO (knowledge-specific)
slo:
  retrieval_latency_p95_ms: 300
  citation_exactness_min: 0.95
  no_answer_correctness_min: 0.90  # Correctly refuses non-answerable
  availability_pct: 99.9

# QUALITY (knowledge-specific)
quality:
  dimensions: [recall, precision, citation_accuracy, vigencia_correctness]
  evaluation:
    frozen_corpus: "test_cases/normativa_rrhh_v1.json"
    metrics: [recall_at_10, precision_at_10, mrr, ndcg, citation_f1]
    frequency: weekly

# OPERATIONS (knowledge-specific)
operations:
  curation_pipeline:
    ingesta: {sources: official_repos, ocr: tesseract_confident, dedup: structural_hash}
    enrichment: {classification: taxonomy, ner: entities, resolution: cross_refs}
    chunking: {method: structural, metadata_rich: true}
    indexing: {lexical: bm25, vector: embeddings_v3, filters: acl_rls}
  observability:
    metrics: [corpus_coverage_pct, ingestion_lag_hours, pct_responses_cited, cache_hit_rate]
    alerts:
      - {rule: "pct_responses_cited < 0.90", severity: error}
```

**Fuente**: KNOW.md §10 Content Curation RAG + SIGMA.md §5.4

**Conexión KERNEL**:

- **P58 RAG Auditable Pattern** (A1 v2.0): Pattern aplicado
- **P63 Hybrid Search Pattern** (A1 v2.0): Indexing strategy
- **T18_Contrato_Conocimiento** (REFERENCIA v2.0): Template detallado
- **E2_Público §9-§12**: Gov-specific RAG normativa (reference)

### §3.6 Unificación SIGMA

**Decisión arquitectónica**: SIGMA NO es dominio separado, es **pattern P62 + E8 §3 Contracts**.

**Razón**:

- SIGMA intentaba ser "supradominio" (framework dentro framework) → Redundante con KERNEL
- Contenido valioso: 100% preservado en:
  - **E8 §3**: Contratos unificados (4 tipos detallados arriba)
  - **A1 P62**: Contract-Driven Evolution (pattern composition)
  - **§2**: Arquitectura 6 capas (metamodelo integrado)

**Beneficio**:

- **Minimalidad I1**: Reduce 1 doc (SIGMA domain) → absorb en E8 §3
- **Clarity**: Contracts como section E8 (not separate confusing "supradomain")
- **Coherencia**: Single voice KERNEL (no framework-within-framework)

**Contenido SIGMA migrado**:

- §1-§4 SIGMA: Principios → E8 §1 Meta-Principios
- §5 SIGMA: Contratos → E8 §3 (este §)
- §6 SIGMA: Arquitectura → E8 §2 (6 capas)
- §7-§9 SIGMA: Métricas, anti-patterns, roadmap → E8 §8, §11, §16

**Conexión KERNEL**:

- **I1 Minimalidad** (CORE/07 §1): Eliminar redundancia (SIGMA absorbed)
- **P7 Separation of Concerns**: Contracts como concern cross-cutting (no domain)

---

## §4. DATA-AS-PRODUCT

### §4.1 Operating Model Federado

**Estructura organizacional** (socio-técnica):

```
┌────────────────────────────────────────────────────────────┐
│ CONSEJO GOBERNANZA DATOS (CDO, Data Council)              │
│ • Políticas, prioridades, resolución conflictos            │
└────────────────────────────────────────────────────────────┘
         ↓ Define policies        ↓ Escalations
┌──────────────────────┐    ┌────────────────────────────────┐
│ PLATFORM TEAM        │    │ DOMAIN TEAMS (Federados)       │
│ • Enablement         │←───│ • Product Owners               │
│ • Lakehouse, tools   │    │ • Data Engineers               │
│ • Standards, templates│    │ • Ownership data products      │
└──────────────────────┘    └────────────────────────────────┘
         ↓ Provides infra         ↓ Build products
┌────────────────────────────────────────────────────────────┐
│ GUARDRAILS CENTRALIZADOS (Policy-as-Code)                  │
│ • OPA/Rego policies (Git-versioned, CI-tested)             │
│ • Quality gates, Security policies, FinOps budgets         │
└────────────────────────────────────────────────────────────┘
```

**Roles DAMA-aligned**:

- **CDO** (Chief Data Officer): Visión estratégica, owner gobernanza
- **Data Product Owner**: Responsable producto datos específico (SLO, quality, roadmap)
- **Data Engineer**: Build/maintain pipelines, servicing interfaces
- **Data Steward**: Domain expert, metadata curator, quality monitor
- **Platform Team**: Enablement (no ownership products, provee capacidad)

**Conexión KERNEL**:

- **D1_Arquitectura §2**: Org structure patterns
- **Actor A3** (CORE/03 §4): Specialized actors (Data Engineer, DPO)

### §4.2 Lifecycle Producto Datos

**6 Fases end-to-end**:

**1. Descubrimiento**:

- **Outcome**: ¿Qué problema de negocio resuelve?
- **Usuarios**: ¿Quiénes consumen? (personas, roles, use cases)
- **KPIs**: ¿Cómo medir éxito? (adoption, query volume, satisfaction)
- **Riesgos**: Privacy, security, compliance constraints

**2. Semántica**:

- **Glosario**: Términos de negocio canónicos (no ambigüedad)
- **Entidades**: Customer, Product, Invoice, etc. (domain model)
- **Reglas negocio**: Validaciones, constraints, invariantes

**3. Contrato**:

- **Schema**: Campos, tipos, PKs, cardinalidades
- **SLO**: Freshness, availability, accuracy targets
- **DQ**: Dimensiones quality (6: exactitud, completitud, validez, unicidad, consistencia, frescura)
- **Seguridad**: Clasificación (P0-P3), PII/PHI flags, ACLs

**4. Implementación**:

- **Ingesta**: CDC, batch, streaming (bronze zone)
- **Transform**: Cleaning, SCD2, enrichment (silver zone)
- **Serving**: Metrics, views, APIs (gold zone)

**5. Operación**:

- **Observability**: Freshness p95, DQ violations/1k, latency p95
- **SRE**: On-call, runbooks, incident response
- **FinOps**: Cost allocation, showback/chargeback

**6. Evolución**:

- **Semver**: Major/Minor/Patch (backward compatibility)
- **Deprecation**: Notice period, coexistence, adapters
- **Retirement**: Sunset plan, data migration/archival

**Conexión KERNEL**:

- **Flujo F3** (CORE/02 §4): Data pipeline como flujo complejo multi-stage
- **P57 Data Product Pattern** (A1 v2.0): Lifecycle operationalizado

### §4.3 Arquitectura Bronze/Silver/Gold (Medallion)

**Lakehouse moderno** (Delta Lake, Iceberg, Hudi):

```
┌─────────────────────────────────────────────────┐
│ BRONZE (Raw, Immutable)                         │
│ • Ingesta sin transform (append-only)           │
│ • Formato: Parquet/ORC (columnar compressed)    │
│ • Partición: Por fecha ingesta (time-travel)    │
│ • Schema: Flexible, schema-on-read              │
│ • Retention: 90 días → Archive cold storage     │
└─────────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────────┐
│ SILVER (Cleaned, Conformed)                     │
│ • Cleaned: Nulls handled, types validated       │
│ • Deduplication: Business keys únicos           │
│ • SCD Type 2: History preserved (valid_from/to) │
│ • Schema: Enforced, schema-on-write             │
│ • DQ checks: 6 dimensions validated             │
│ • Retention: 2 años → Archive                   │
└─────────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────────┐
│ GOLD (Business-Level, Curated)                  │
│ • Aggregations: Metrics pre-computed            │
│ • Star/Snowflake schemas: OLAP-optimized        │
│ • Data Products: Contract-governed              │
│ • Views: Business-semantic layer                │
│ • Retention: Indefinido (core business asset)   │
└─────────────────────────────────────────────────┘
```

**ACID Transactions**: Delta Lake garantiza (Atomicity, Consistency, Isolation, Durability)

**Time-Travel**: Queryable snapshots históricos (`SELECT * FROM tabla VERSION AS OF timestamp`)

**OPTIMIZE**: Compaction automático (small files → large files, Z-ordering clustering)

**Conexión KERNEL**:

- **Recurso R3** (CORE/01 §3): Lakehouse como recurso capacity storage
- **Flujo F2** (CORE/02): Automated ETL pipelines

### §4.4 Contratos Datos Detalle

**Ver §3.2** para estructura completa base.

**Ejemplo completo billing_invoices** (ya en §3.2, no duplicar).

**Ejemplo 2: customer_360** (data product analítico):

```yaml
type: data_contract
product: customer_360
version: 1.0.0
owner: ["dom-marketing", "customer-analytics@empresa.cl"]

semantics:
  glossary_refs: ["Cliente", "Segmento", "Lifetime_Value", "Churn_Risk"]
  business_rules:
    - {name: ltv_positive, rule: "lifetime_value_clp >= 0", severity: warn}

schema:
  primary_key: [customer_id]
  fields:
    - {name: customer_id, type: string, required: true}
    - {name: segment, type: string, enum: [VIP, Standard, New, Churned]}
    - {name: lifetime_value_clp, type: "decimal(18,2)"}
    - {name: churn_risk_score, type: float, range: [0.0, 1.0]}
    - {name: last_interaction_at, type: timestamp}

slo:
  freshness_p95_minutes: 60  # Hourly refresh
  availability_pct: 99.5

operations:
  lineage:
    as_designed: "crm.customers + billing.invoices + support.tickets -> customer_360"
  serving_interfaces:
    - {type: sql, endpoint: "warehouse.gold.customer_360"}
    - {type: graphql, endpoint: "/api/graphql/customer"}
```

**Conexión**: T15_Contrato_Datos, T20_Data_Product_Spec (templates v2.0)

### §4.5 Linaje Activo

**Dos dimensiones**:

**As-Designed** (intención):

- Mapeos semánticos fuente → destino
- Documentado en contracts (`operations.lineage`)
- Mantenido por Data Engineers/Architects

**As-Implemented** (realidad):

- **OpenLineage** harvesting automático (runtime instrumentation)
- **Column-level lineage**: Campo_A.tabla_1 → Campo_B.tabla_2 (transformaciones rastreadas)
- **Impact analysis**: ¿Qué downstream afecta cambio a upstream?

**Herramientas**:

- **OpenLineage**: Standard events (START, COMPLETE, FAIL) con inputs/outputs
- **Tools**: Marquez (lineage UI), DataHub, Amundsen (catalog + lineage integrated)

**Ejemplo OpenLineage event**:

```json
{
  "eventType": "COMPLETE",
  "job": {"name": "silver.billing.transform", "namespace": "etl"},
  "inputs": [{"namespace": "lake/bronze", "name": "billing_raw"}],
  "outputs": [{"namespace": "lake/silver", "name": "billing_clean"}],
  "run": {"runId": "uuid-123", "facets": {"execution_time_ms": 45000}}
}
```

**Conexión KERNEL**:

- **I3 Trazabilidad** (CORE/07 §3): Lineage como trazabilidad datos
- **P57 Data Product Pattern** (A1 v2.0): Lineage component

### §4.6 Data Quality System

**6 Dimensiones DQ** (DAMA standard):

| Dimensión | Definición | Check Example | Tool |
|:---|:---|:---|:---|
| **Exactitud** | Datos reflejan realidad correctamente | `amount_total` matches source invoice | Reconciliation |
| **Completitud** | Campos críticos no-null | `customer_id IS NOT NULL` | Great Expectations |
| **Validez** | Valores en dominios permitidos | `status IN (ISSUED, PAID, VOID)` | Schema validation |
| **Unicidad** | PKs únicos, no duplicados | `UNIQUE(invoice_id)` | Deduplication |
| **Consistencia** | Formatos estandarizados | `fecha ISO 8601, moneda CLP` | Format validators |
| **Frescura** | Data actualizada según SLO | `event_time_diff < 30min` | Lag monitoring |

**Framework Implementation**:

**Great Expectations** (Python-based):

```yaml
expectations:
  - expect_column_values_to_be_in_set:
      column: status
      value_set: [ISSUED, PAID, VOID, CANCELLED]
  - expect_column_values_to_not_be_null:
      column: invoice_id
  - expect_column_values_to_be_unique:
      column: invoice_id
```

**Deequ** (Scala/Spark-based):

- Scala API para Spark (big data scale)
- Anomaly detection (z-score, statistical profiling)

**Error Budgets por Producto**:

- **Formula**: `Error_Budget = (1 - SLO_DQ) × Total_Rows`
- **Ejemplo**: SLO = 99.9% quality → Error budget = 0.1% × 1M rows = 1,000 violations permitidas/mes
- **Alertas**: `violations/1k > threshold` → PagerDuty

**Conexión KERNEL**:

- **CORE/05 Smartness §3**: Quality como smartness dimension
- **Límite L1** (CORE/03): DQ thresholds como límites performance

### §4.7 FinOps Datos

**Showback/Chargeback por Domain**:

- **Showback**: Informar costos (visibility, no cobro)
- **Chargeback**: Cobro interno (accountability, budget ownership)

**Modelo**:

```
Cost_Domain = (Storage_TB × Price_TB) + (Compute_Hours × Price_Compute) + (Query_Count × Price_Query)
```

**Storage Tiering** (hot/warm/cold):

- **Hot**: SSD, <30 días, acceso frecuente (alto costo)
- **Warm**: HDD, 30-365 días, acceso ocasional (medio costo)
- **Cold**: S3 Glacier, >365 días, acceso raro (bajo costo, retrieval delay)

**Optimizaciones**:

- **Compaction**: Small files → Large files (reduce metadata overhead)
- **Partition Pruning**: Query solo particiones necesarias (skip irrelevant)
- **Z-Ordering**: Co-locate related data (clustering, cache-friendly)

**KPIs FinOps**:

- Cost/TB stored
- Cost/query executed
- Cost/data product
- Waste % (unused tables, zombie pipelines)

**Conexión**: D4_Operación §9 FinOps practices

### §4.8 Otras Capacidades DATA

**Semántica** (Glosario, SHACL):

- Glosario controlado términos negocio
- SHACL constraints (validaciones semánticas)
- **Ejemplo**: `ex:Factura sh:property [ sh:path ex:status ; sh:in ("ISSUED" "PAID" "VOID") ]`

**Integration** (CDC, Outbox):

- **CDC** (Change Data Capture): Log-based (Debezium), minimal coupling
- **Outbox Pattern**: Transactional messaging (dual-write prevention)

**Security** (ABAC, RLS/CLS):

- **ABAC**: Attribute-Based Access Control (context-aware)
- **RLS**: Row-Level Security (filter rows by user role)
- **CLS**: Column-Level Security (mask columns sensitive)

**MDM/RDM**:

- **Master Data Mgmt**: Golden records (customers, products)
- **Reference Data Mgmt**: Códigos, catálogos (países, categorías)

**DW/BI**:

- Star/Snowflake schemas (OLAP)
- Semantic layer (metrics declarativas, ver §3.2 contracts)

**MLOps**:

- Feature Store (offline/online parity, point-in-time joins)
- Model registry (versioning, A/B testing, shadow traffic)

**Fuente**: DATA.md §6-§21 completo

---

## §5. AI ORCHESTRATION

### §5.1 Model Serving

**OpenAI-Compatible Endpoints** (standard de-facto):

- API compatible con OpenAI (drop-in replacement)
- **Beneficio**: Cambiar provider sin cambiar client code

**Runtimes LLM**:

| Runtime | Strengths | Use Case |
|:---|:---|:---|
| **vLLM** | Continuous batching, PagedAttention (alta throughput) | Production serving high-load |
| **TGI** (Text Generation Inference) | HuggingFace native, rápido setup | HF models serving |
| **SGLang** | Structured generation (JSON, grammar-constrained) | Structured outputs guaranteed |
| **Triton** | Multi-framework (TensorFlow, PyTorch, ONNX) | Heterogeneous model zoo |
| **Ray Serve** | Distributed, autoscaling built-in | Large-scale, multi-model |

**Continuous Batching**:

- Traditional: Espera llenar batch completo → Process → Repeat (latency alta)
- **Continuous**: Procesa requests a medida que llegan, batch dinámico (latency baja, throughput alto)

**Autoscaling Triggers**:

- **Queue length**: >10 requests waiting → Scale up
- **GPU memory**: >80% utilization → Scale up
- **Batch occupancy**: <30% → Scale down
- **Cold-start pre-warm**: Mantener 1 replica mínima (avoid cold start)
- **Scale-to-zero**: Para workloads intermitentes (cost optimization)

**Ejemplo config** (Kubernetes HPA):

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: llm-serving
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: vllm-gpt4o
  minReplicas: 1
  maxReplicas: 10
  metrics:
  - type: External
    external:
      metric:
        name: queue_length
      target:
        type: AverageValue
        averageValue: "5"
```

**Conexión KERNEL**:

- **Recurso R3** (CORE/01 §3): Model endpoint como capacity resource
- **D4_Operación §10**: Autoscaling strategies

### §5.2 Autonomy Spectrum

**3 Niveles Autonomía** (menos → más):

**Nivel 1: RAG (Retrieval-Augmented)**:

- **Definición**: LLM augmented con context retrieved de knowledge base
- **Autonomy**: Baja (responde con info recuperada, no toma acciones)
- **Delegation mapping**: **M3 Enable** (augment human capabilities)
- **Ejemplo**: Chatbot normativa responde con citas exactas
- **Guardrails**: Citation mandatory, modo extractivo, no ejecuta tools

**Nivel 2: ReAct (Reasoning-Action)**:

- **Definición**: LLM razona → Llama tool → Observa resultado → Repite (loop)
- **Autonomy**: Media (ejecuta tools, pero bounded iterations)
- **Delegation mapping**: **M4-M5** (Control/Co-produce - human reviews outputs)
- **Ejemplo**: Agent extrae factura (IDP tool) → Valida (rules tool) → Si >$10K HITL → Post ERP (API tool)
- **Guardrails**: Max iterations, cost limits, HITL checkpoints scores <0.85

**Nivel 3: Plan & Execute**:

- **Definición**: LLM planifica multi-step → Ejecuta plan → Checkpoints validation → Compensate on failure
- **Autonomy**: Alta (multi-step autonomous, supervised)
- **Delegation mapping**: **M5-M6** (Co-produce/Execute - meta-supervisión)
- **Ejemplo**: Agent orquesta workflow facturación (8 pasos, sagas, HITL conditional)
- **Guardrails**: Comprehensive (input/output/ops/ethical), supervisor agent meta-level

**Conexión KERNEL**:

- **CORE/04 Delegación §3-§8**: M1-M6 spectrum (mapeo explícito)
- **C6 Bounded Autonomy** (CORE/04 §5): Autonomía acotada por guardrails
- **D3 §8** (extension v2.0): Algorithmic Decision Modes D5-D7

### §5.3 Guardrails Architecture

**4 Tipos Guardrails** (defensa en profundidad):

**Input Guardrails** (pre-LLM):

- **Prompt rewrite**: Sanitize, structure user input (prevent injection)
- **PII detection**: Redact sensitive (NER models, regex patterns)
- **Injection defense**: Detect prompt injection attempts (adversarial patterns)
- **Tools**: NeMo Guardrails, Guardrails AI, LlamaGuard

**Output Guardrails** (post-LLM):

- **Schema validation**: JSON output conforms to expected schema (Pydantic)
- **Faithfulness check**: Output grounded en retrieved context (NLI models)
- **Toxicity scan**: Content moderation (Perspective API, custom classifiers)
- **Citation validation**: All claims have valid citations (regex + lookup)

**Operational Guardrails** (runtime):

- **Max iterations**: Límite loops ReAct (prevent infinite loops)
- **Timeout**: Max execution time (prevent hangs)
- **Token cost limit**: FinOps budget per task (prevent runaway costs)
- **Concurrency limit**: Max parallel invocations (resource protection)

**Ethical Guardrails** (fairness, bias):

- **Bias detection**: Demographic parity checks (protected attributes)
- **Fairness constraints**: Equalized odds, calibration checks
- **Transparency**: Explain decisions (SHAP, LIME for ML, prompt templates for LLM)
- **Human oversight**: HITL mandatory para decisiones high-stakes (hiring, credit, medical)

**Ejemplo OPA Policy** (operational guardrail):

```rego
package agent.guardrails

deny[msg] {
  input.iterations > 5
  msg := "Max iterations exceeded (5)"
}

deny[msg] {
  input.cost_usd > 2.0
  msg := "Cost limit exceeded ($2.00)"
}
```

**Conexión KERNEL**:

- **C6 Bounded Autonomy** (CORE/04 §5): Guardrails implement bounds
- **Límite L1-L4** (CORE/03): Guardrails como límites operacionales multi-dimensión

### §5.4 State & Memory Management

**Short-Term Memory** (session-scoped):

- **Session context**: User ID, preferences, permissions
- **Conversation history**: Last N messages (sliding window)
- **Tool context**: Intermediate results tools (ephemeral, task-scoped)
- **TTL**: Session end (~30 min inactivity)

**Long-Term Memory** (persistent):

- **Knowledge base**: Shared, curated documents (ver §6)
- **Vector store**: Embeddings previous conversations (semantic search)
- **Entity memory**: Facts about entities (Customer X prefers Y) - TTL 30-90 días
- **Storage**: PostgreSQL + pgvector, Qdrant, Weaviate

**Consistency Multi-Agent**:

- **Event Sourcing**: Immutable event log (state reconstructed from events)
- **CRDTs** (Conflict-Free Replicated Data Types): Eventual consistency multi-agent writes
- **Coordination**: Supervisor agent arbitra conflictos

**Privacy**:

- **Scoping por tenant**: Datos segregados (multi-tenant SaaS)
- **PII redaction**: Mask/tokenize antes storage
- **Encryption**: At-rest (AES-256), in-transit (TLS 1.3)

**Conexión KERNEL**:

- **Dato D2** (CORE/01 §2): State como dato persistent
- **Señal S2** (CORE/01 §2): Events como señales state changes

### §5.5 Evaluation Harness

**Offline Evaluation** (pre-deploy):

**Golden Sets**:

- Curated test cases (input, expected output, citations)
- Version-controlled (Git), frozen corpus (reproducibility)

**Metrics Offline**:

- **Faithfulness**: ≥0.9 (output grounded in retrieved context)
- **Citation exactness**: ≥0.95 (citations valid, precise)
- **Hallucination rate**: <5% (claims sin soporte context)
- **Task success rate**: % tasks completed correctly

**Tools**: Ragas (RAG metrics), DeepEval, LangSmith

**Online Evaluation** (production):

**Sampling**:

- 10% traffic sampled para evaluation (cost-performance balance)
- A/B testing (model A vs B, 50/50 split)

**Metrics Online**:

- **TTFT** (Time-to-First-Token): p95 <1200ms
- **TPOT** (Time-per-Output-Token): p95 <50ms
- **Cost per Resolution**: $0.50 target
- **User satisfaction**: CSAT score (thumbs up/down)

**LLM-as-a-Judge**:

- GPT-4 evalúa outputs otros modelos (rúbricas, scoring)
- **Ventaja**: Scalable vs human eval
- **Limitación**: Judge model bias, requiere calibration con human eval

**Regression Tests**:

- Frozen test set ejecuta cada deploy
- **Alarm**: Degradation >5% cualquier métrica → Block deploy

**Conexión KERNEL**:

- **A5_Medición §7**: Evaluation frameworks
- **CORE/05 Smartness §5**: Quality metrics validation

### §5.6 Multi-Agent Patterns

**4 Patterns Orquestación**:

**Pattern 1: Router**:

- **Descripción**: Agent router selecciona specialized agent por query type
- **Ejemplo**: User query → Router classifies → Route to {Billing_Agent, Support_Agent, Product_Agent}
- **Delegation**: M4 Control (router controls, no ejecuta)

**Pattern 2: Supervisor-Worker**:

- **Descripción**: Supervisor agent asigna tasks a worker agents, agrega resultados
- **Ejemplo**: Research task → Supervisor asigna sub-queries a 3 workers → Aggregate findings
- **Delegation**: M5 Co-produce (supervisor + workers co-produce outcome)

**Pattern 3: Planner-Executor**:

- **Descripción**: Planner agent crea plan multi-step → Executor agent ejecuta steps
- **Ejemplo**: "Book viaje" → Planner: [buscar vuelos, reservar, confirmar pago] → Executor: ejecuta c/u
- **Delegation**: M5-M6 (Planner M5, Executor M6 bounded)

**Pattern 4: Critic-Refiner**:

- **Descripción**: Generator agent crea output → Critic agent evalúa → Refiner mejora iteratively
- **Ejemplo**: Draft legal document → Critic flags issues → Refiner corrige → Loop hasta quality threshold
- **Delegation**: M5 Co-produce (human-like review loop)

**Coordination Mechanisms**:

- **Shared memory**: Vector store, PostgreSQL (state coordination)
- **Message passing**: Event bus (async coordination)
- **Locking**: Distributed locks (prevent conflicts, e.g., Redis locks)

**Conexión KERNEL**:

- **P53 Orchestration Agent** (CORE/04 §8): Pattern supervisor
- **P61 Multi-Agent Orchestration** (A1 v2.0): Pattern detallado
- **C6 Bounded Autonomy**: Multi-agent bounded colectivamente

### §5.7 Security OWASP LLMs

**OWASP Top-10 for LLMs** (2025):

1. Prompt Injection (malicious instructions embedded)
2. Insecure Output Handling (LLM output executed unsafe)
3. Training Data Poisoning (contaminated training sets)
4. Model Denial of Service (resource exhaustion attacks)
5. Supply Chain Vulnerabilities (compromised dependencies)
6. Sensitive Information Disclosure (leak PII, secrets)
7. Insecure Plugin Design (tools vulnerables)
8. Excessive Agency (over-privileged agents)
9. Overreliance (humans trust LLM blindly)
10. Model Theft (extraction attacks)

**Mitigaciones**: Ver §3.4 Guardrails (comprehensive defense)

**Conexión**: E7_Enterprise_Technology §6 Security (foundation)

---

## §6. KNOWLEDGE MANAGEMENT + RAG

### §6.1 Framework 16 Celdas (ISO 30401)

**Matriz 4×4** (Transacciones × Habilitadores):

| Transacción ↓ / Habilitador → | **Personas** | **Procesos** | **Tecnología** | **Gobernanza** |
|:---|:---|:---|:---|:---|
| **Discutir** | CoP meetings, expert networks | Agendas estructuradas, facilitación | Wikis, forums, Slack | Charters CoP, participation KPIs |
| **Documentar** | Document owners, curadores | Capture templates, standards | ECM, Git, Confluence | Retention policies, quality gates |
| **Sintetizar** | Knowledge engineers, analistas | Synthesis workflows, peer review | NLP summarization, clustering | Authority designation, IP policies |
| **Encontrar/Revisar** | End-users, researchers | Search protocols, tagging | Search engines, vector DB, RAG | Access policies (ABAC), audit trails |

**ISO 30401 Compliance**:

- Todas 16 celdas cubiertas (completitud framework)
- Ciclo KM: Descubrir → Capturar → Compartir → Aplicar
- Rutas: **Connect** (personas ↔ personas, tácito) + **Collect** (contenido codificado, explícito)

**Conexión KERNEL**:

- **CORE/06 Capacidades §2**: KM como capacidad organizacional C3
- **Actor A3** (CORE/03): Knowledge Engineers como specialized actors

### §6.2 Roles KM

| Rol | Responsabilidad | KERNEL Mapping |
|:---|:---|:---|
| **Knowledge Engineers** | Curation pipelines, quality, indexing | Actor A3 Specialized |
| **Document Owners** | Autoridad content, aprobación publicación | Actor A3 |
| **CoP Leaders** | Facilitate communities, socialización tácito | Actor A2 Organizational |
| **Curadores/Documentalistas** | QA content, metadata enrichment, taxonomies | Actor A3 |
| **Data Stewards** | Metadata data products (overlap KM-Data) | Actor A3 |

**Conexión**: D1_Arquitectura §2 Org structure (roles como estructura)

### §6.3 Content Curation Pipeline RAG (Government/Enterprise)

**5 Fases** (Normativa/Admin use case, high-authority required):

**Fase 1: Ingesta & Normalización**:

**Fuentes Oficiales**:

- Repositorios oficiales (Diario Oficial, boletines, ECM institucional)
- **Verificación integridad**: SHA-256 hash validation
- **OCR confiable**: Tesseract, Azure Form Recognizer (confidence >0.95)
- **Detección idioma**: langdetect, fastText

**Deduplicación**:

- **Structural hash**: texto + metadatos clave (no solo content hash)
- **Fuzzy matching**: SimHash para near-duplicates (>95% similarity)

**Redacción PII Selectiva**:

- NER models (spaCy, Presidio) detectan PII
- Redact según políticas (nombres, RUTs, direcciones)
- **Marcas de agua**: Digital fingerprints rastreabilidad

**Fase 2: Enriquecimiento Semántico**:

**Clasificación Taxonomía**:

- Controlled vocabulary (materias: Laboral, Tributario, Contractual, etc.)
- Multi-label classification (documento puede tener >1 materia)

**Entity Recognition**:

- Organismos (Ministerio X, GORE Y)
- Cargos (Director, Jefe Departamento)
- Montos (CLP, UF, UTM)
- Fechas vigencia (desde, hasta)
- Referencias normativas (Ley N° X, Decreto Y)

**Resolución Referencias**:

- ¿Qué documento deroga/modifica a cuál?
- Enlaces cruzados (artículo X refiere artículo Y)
- **Graph construction**: Documents como nodos, references como edges

**Quality Gates**:

- Schema validation (metadatos obligatorios completos)
- Vigencia dates coherentes (desde < hasta)
- Exception reports (docs sin clasificar, referencias rotas)

**Fase 3: Chunking Estructural**:

**Por Límites Semánticos**:

- **Artículo** (unidad mínima normativa)
- **Cláusula** (contratos)
- **Sección** (informes, guías)

**Contexto Jerárquico**:

- Ruta documento: `Ley_21180 > Título_II > Artículo_18`
- Número artículo, epígrafe
- **Benefit**: LLM entiende posición chunk en documento (context-aware)

**Ventanas Solapadas**:

- Overlap 10-20% tokens entre chunks consecutivos
- **Razón**: Reasoning requiere multi-context (artículo N referencia N-1)

**Metadatos Chunk** (ricos):

```json
{
  "chunk_id": "ley21180_art18_uuid",
  "doc_id": "ley_21180",
  "tipo": "Ley",
  "numero_articulo": "18",
  "epigrafe": "Expediente Electrónico",
  "vigencia_desde": "2022-06-09",
  "vigencia_hasta": null,
  "estado": "vigente",
  "acl": ["public"],
  "chunk_text": "...",
  "chunk_index": 12,
  "total_chunks_doc": 45
}
```

**Fase 4: Indexación Híbrida**:

**Doble Índice** (best of both):

**Lexical (BM25/TF-IDF)**:

- Exact keyword matching (nombres propios, códigos, fechas)
- **Boost fields**: `titulo: 2.0×`, `articulado: 1.5×`, `anexos: 1.0×`

**Vector (Embeddings)**:

- Semantic similarity (conceptually related, not keyword match)
- **Models**: text-embedding-3-large (OpenAI), sentence-transformers (local)
- **Dimensiones**: 1024-1536 (trade-off precision vs speed)

**Filters Query-Time**:

- `estado = vigente` (no derogados)
- `vigencia_desde <= today <= vigencia_hasta` (aplicable hoy)
- `confidencialidad <= user_role` (ACL)
- `materia IN user_allowed_materias`

**Reranking (Cross-Encoder)**:

- Top-K (20-50) from hybrid → Rerank top-10
- **Features**: Entity match, fecha match, proximidad estructural (mismo título/sección), autoridad score
- **Model**: Cross-encoder fine-tuned (domain-specific)

**Fase 5: Serving Seguro**:

**Búsqueda ACL Pre-Filters**:

- Apply filters ANTES retrieval (security by design)
- Never retrieve restricted → Filter post-hoc (leak risk)

**Context Assembly**:

- Ensamblar top-10 chunks con **citas exactas** (doc, artículo, página)
- **Desambiguar versiones**: Vigente vs anterior explícito
- **Balancear diversidad**: Múltiples fuentes vs single-source depth (parámetro)

**LLM Template**:

```
Eres un asistente experto en normativa [DOMINIO].

CONTEXTO RECUPERADO:
{chunks_con_citas}

INSTRUCCIONES:
1. Responde SOLO con información del contexto recuperado
2. SIEMPRE cita: [Documento, Artículo/Página]
3. Si no hay info suficiente: "No encuentro información específica en la normativa vigente sobre..."
4. Nota vigencia si relevante: "Según Ley X (vigente desde YYYY-MM-DD)..."
5. Modo extractivo para pasajes normativos (cita textual)

PREGUNTA USUARIO:
{user_query}

RESPUESTA:
```

**Defensas Prompt Injection**:

- User input en sección separada (no mezclado con system instructions)
- Allowlist orígenes retrieval (solo knowledge base oficial)
- Bloqueo "ejecutar código", "ignorar instrucciones previas" (pattern matching)

**Conexión KERNEL**:

- **P58 RAG Auditable Pattern** (A1 v2.0): Pipeline completo operationalizado
- **P63 Hybrid Search Pattern** (A1 v2.0): Indexación strategy
- **T18_Contrato_Conocimiento** (REFERENCIA v2.0): Contract template

### §6.4 Evaluación Calidad RAG

**Retrieval Evaluation**:

- **Recall@K**: % relevant docs en top-K
- **Precision@K**: % top-K que son relevant
- **MRR** (Mean Reciprocal Rank): 1/rank_first_relevant
- **Cobertura normativa**: % materias cubiertas corpus

**Reranking Evaluation**:

- **NDCG** (Normalized Discounted Cumulative Gain): Ranking quality
- **Consistencia autoridad**: Docs oficiales ranked higher

**Generation Evaluation**:

- **Citation exactness**: ≥0.95 (all citations valid, traceable)
- **Faithfulness**: ≥0.90 (claims supported by context)
- **No-answer rate correctness**: ≥0.90 (correctly refuses non-answerable)
- **Readability**: Flesch-Kincaid grade level <12 (accessible)

**Security Testing**:

- **Injection attacks suite**: Adversarial prompts (jailbreak attempts)
- **PII leakage simulated**: Intentar extraer PII training data
- **Version confusion**: Verify derogado NO retrieved

**Regression**:

- **Frozen corpora**: 100 golden Q&A pairs
- **Drift alarms**: Citation exactness drop >5% → Alert

**HITL Curation**:

- Panel curadores/documentalistas review edge cases
- Accept/reject suggestions, corregir metadatos
- Promote canonical examples (fine-tuning, few-shot)

**Conexión KERNEL**:

- **A5_Medición §7**: Evaluation harness general
- **CORE/05 Smartness §5**: Quality validation systematic

### §6.5 Operación Continua KM

**Monitoreo**:

- **Métricas uso**: Queries/day, users activos, temas top
- **Cobertura corpus**: % documents indexed vs total oficial
- **Lag ingestión**: Time desde publicación oficial → Available search
- **% respuestas cited**: ≥90% target (mandatory citations)

**Mantenimiento Índice**:

- **Re-embedding**: Cuando cambio model embeddings (migration v2 → v3)
- **Re-sharding**: Growth corpus requiere partition re-balance
- **Pruning**: Docs derogados archive (soft-delete, keep retrievable historical queries)

**MLOps Curation**:

- **Pipelines versionados**: Git (ingesta, enrichment, indexing)
- **Feature stores**: Authority scores, entity importance (signals reranking)
- **Canary deployments**: New embedding model (10% traffic → 100% gradual)

**Catálogo Conocimiento** (data products de docs):

- **Producto**: "Normativa_RRHH_Vigente"
- **Owner**: Legal team
- **SLO**: Actualización <24h desde publicación oficial
- **Contacto**: <legal-team@empresa.cl>

**Playbooks**:

- **Alta colección nueva** (ej. contratos): Mapeo campos, política vigencia, ontología, pruebas, publicación
- **Derogación masiva**: Regla negocio (`Ley X deroga Y`), migración vigencia flags, reindexación, comunicación users
- **Incidente** (doc sensible expuesto): Freeze serving, revoke ACL, purge caches, impact report

**Fuente**: KNOW.md §10 completo (Content Curation RAG)

**Conexión KERNEL**:

- **D4_Operación §11**: KM operations (playbooks, runbooks)
- **A4_Implementación §5**: KM implementation roadmap

---

## §7. PROCESS AUTOMATION

### §7.1 Taxonomía BPA

**Clarificación conceptual** (crítica, often confused):

| Término | Alcance | Nivel | Analogía Técnica |
|:---|:---|:---|:---|
| **BPM** (Business Process Management) | Disciplina gestión estratégica | Estratégico | Como SDLC/Agile (metodología, no tool) |
| **BPA** (Business Process Automation) | Orquestación procesos end-to-end | Táctico | Como K8s (orchestrator workflows completos) |
| **RPA** (Robotic Process Automation) | Automatización tareas UI | Operacional | Como Selenium en producción (UI scripts, último recurso) |
| **DPA** (Digital Process Automation) | BPA + modern tech (low-code, AI, cloud) | Táctico-Tech | BPA con DevOps + UX + Cloud-Native |
| **IPA** (Intelligent Process Automation) | BPA + IA/ML (cognitive tasks) | Táctico-AI | BPA + LLM/ML services (IDP, NLP, decisiones) |

**Principio**: **BPA orquesta**, **RPA es último recurso** (API-first always).

**Conexión KERNEL**:

- **Flujo F3** (CORE/02 §4): BPMN process como flujo complejo
- **D4_Operación §2**: Process execution modes

### §7.2 BPMN Ejecutable

**Elementos BPMN** (standard ISO 19510):

**Tasks**:

- **User Task**: Humano ejecuta (HITL)
- **Service Task**: Llamada API automatizada
- **Script Task**: Código ejecuta (transformaciones ligeras)
- **Send/Receive Task**: Messaging async
- **Business Rule Task**: Rules engine (Drools, decision tables)

**Gateways**:

- **Exclusive (XOR)**: Solo un path (decisión binaria)
- **Parallel (AND)**: Todos paths simultáneamente
- **Inclusive (OR)**: Uno o más paths (conditional parallelism)
- **Event-Based**: Espera evento(s) para continuar

**Events**:

- **Start**: Inicia proceso (message received, timer, signal)
- **Intermediate**: Durante proceso (timer espera, message catch, error boundary)
- **End**: Termina proceso (success, error, compensation)

**Sagas (Compensaciones)**:

- **Problema**: Transacción distribuida (multi-systems, no 2PC disponible)
- **Solución**: Cada step tiene **compensation action** determinista
- **Ejemplo**: Post_ERP → Compensation: Revert_Posting (idempotent)

**HITL Queues**:

- **Exception queues**: Casos automación no puede manejar
- **Escalation rules**: `>48h in queue → Escalate supervisor`
- **UI**: Low-code tools (form-based human task completion)

**Ejemplo BPMN** (invoice approval):

```xml
<process id="invoice_approval">
  <startEvent id="start" />
  <serviceTask id="classify" name="Classify Document (AI)" />
  <exclusiveGateway id="is_invoice" />
  <serviceTask id="extract_idp" name="Extract Data (IDP)" />
  <businessRuleTask id="validate" name="Validate Rules" />
  <exclusiveGateway id="amount_check" />
  <userTask id="hitl_approval" name="Human Approval (>$10K)" />
  <serviceTask id="post_erp" name="Post to ERP API" />
  <boundaryEvent id="api_error" attachedToRef="post_erp">
    <errorEventDefinition />
  </boundaryEvent>
  <serviceTask id="rpa_fallback" name="RPA Post (Fallback)" />
  <endEvent id="end_success" />
</process>
```

**Métricas Process**:

- **Cycle time p95**: 180 min target
- **STP %** (Straight-Through Processing): 80% target (no human intervention)
- **Error rate**: <5%
- **HITL backlog**: <50 items

**Conexión KERNEL**:

- **Flujo F3** (CORE/02 §4): Process flow multi-stage
- **P59 Saga Compensation** (A1 v2.0): Pattern compensations
- **P60 HITL Checkpoint** (A1 v2.0): Pattern human checkpoints

### §7.3 Pipeline Típico: Invoice Processing

**Pseudocódigo anotado** (delegation modes explicit):

```python
def process_invoice(invoice_document):
    # 1. Ingesta & Clasificación (M4 Control - AI classifies, system proceeds)
    doc_type = AI.classify_document(invoice_document)  # M4 AI
    if doc_type != "INVOICE":
        raise UnprocessableDocumentError()
    
    # 2. Extracción Datos IDP (M5 Co-produce - AI extracts, human validates edge cases)
    extracted_data = IDP.extract(invoice_document)  # M5 AI (Intelligent Doc Processing)
    confidence = extracted_data.confidence_score
    
    # 3. Validación Reglas Negocio (M6 Execute - automated rules)
    validation_result = BusinessRules.validate(extracted_data)  # M6 Rules Engine
    
    if not validation_result.isValid or confidence < 0.85:
        # 4. HITL para excepciones (M1 Monitor - human reviews, decides)
        human_resolution = HumanTaskQueue.assign(
            queue="exceptions.approval",
            data=extracted_data,
            errors=validation_result.errors,
            timeout_hours=48
        )  # M1 Human
        if human_resolution.isRejected:
            return "REJECTED"
        update(extracted_data, human_resolution.changes)
    
    # 5. Integración ERP API-First (M6 Execute - automated integration)
    try:
        ERP_API.post_invoice(extracted_data)  # M6 API
    except APIError as e:
        # Fallback RPA si API falla (M6 Execute bounded - ultimo recurso)
        RPA_Bot.enter_invoice_legacy_erp(
            data=extracted_data,
            guardrails=["credential_vault", "screen_selector_stable"]
        )  # M6 RPA (bounded, monitored)
    
    # 6. Notificación & Archive (M6 Execute - automated ops)
    Notifier.send_success(extracted_data.invoice_id)  # M6
    DocumentStore.archive(invoice_document, extracted_data)  # M6
    
    return "PROCESSED"
```

**Métricas Pipeline**:

- **Cycle time**: 45 min (was 4h manual) - 82% improvement
- **STP %**: 82% (AI+rules handle, 18% HITL)
- **Cost per invoice**: $0.45 (was $8.50 manual) - 95% reduction
- **Error rate**: 2.3%

**Conexión KERNEL**:

- **CORE/04 Delegación §3-§8**: M1-M6 aplicados explícitamente cada step
- **Caso integrado**: Ver §12 Caso 1 (detallado)

### §7.4 RPA Governance (CoE)

**Center of Excellence RPA** (mandatory governance):

**Credential Vault**:

- **NEVER hardcode** credentials bots
- HashiCorp Vault, CyberArk (enterprise-grade)
- JIT credentials (bots fetch runtime, time-bounded)

**Screen Selector Stability**:

- **Problem**: UI changes → Bots break (selectors XPath/CSS frágiles)
- **Mitigation**:
  - AI-powered selectors (self-healing, computer vision)
  - Contract con app owners (notify UI changes 30 días advance)
  - Selector validation tests (daily smoke tests)

**Orchestrator Central**:

- **UiPath Orchestrator**, Automation Anywhere Control Room
- **Functions**: Scheduling, queueing, monitoring, credential management
- **Benefit**: Centralized visibility, policy enforcement

**Audit Trail Inmutable**:

- Cada ejecución bot logged (timestamp, user, actions, screenshots, errors)
- **Retention**: 7 años (compliance SOX, GDPR)
- **Immutability**: Write-once storage (WORM, blockchain optional)

**Conexión KERNEL**:

- **D4_Operación §12**: RPA operations best practices
- **AP36 RPA Universal Hammer** (A2 v2.0): Anti-pattern evitar

### §7.5 Anti-Patterns BPA

**AP_BPA1: Automatizar Proceso Roto**:

- **Síntoma**: Automatizar proceso ineficiente sin optimizar primero
- **Consecuencia**: "Hacer mal las cosas, pero más rápido"
- **Fix**: **Process Mining** primero (Celonis, UiPath Process Mining) → Optimize → Automate
- **Conexión**: AP40 (A2 v2.0)

**AP_BPA2: RPA como Martillo Universal**:

- **Síntoma**: Usar RPA cuando existe API o ETL más robusto
- **Consecuencia**: Frágil (UI changes), costoso mantener, no escala
- **Fix**: **API-first always** → RPA solo legacy sin APIs
- **Conexión**: AP36 (A2 v2.0)

**AP_BPA3: Ignorar Larga Cola Excepciones**:

- **Síntoma**: Automatizar happy path (80%), ignorar edge cases (20%)
- **Consecuencia**: 20% casos bloquean, manual intervention >80% esfuerzo total
- **Fix**: **Design para excepciones** (HITL queues, escalation, logging comprehensive)

**Fuente**: BPA.md §5 Anti-Patterns

**Conexión KERNEL**:

- **APLICACION/A2 §11** (v2.0): Tech anti-patterns (cross-reference)
- **CORE/08 Crisis Management**: Exception handling como crisis prevention

---

## §8. OBSERVABILIDAD UNIFICADA

### Data Observability

**Golden Signals Data**:

- **Freshness p95**: Time desde event_time → Available query (target <30min)
- **DQ violations/1k rows**: Violations error-level per 1000 rows (target <0.8)
- **Latency p95**: Query response time (target <500ms OLAP, <50ms OLTP)
- **Error budget consumption**: % error budget used (SLO tracking)

**OpenLineage** (lineage as-implemented):

- Runtime instrumentation pipelines
- Column-level lineage automático
- Impact analysis queries (¿qué afecta cambio X?)

**Tools**: Monte Carlo Data, Datafold, custom (dbt tests + Airflow sensors)

**Dashboards**:

- **Executive**: DH_Score trend, products at-risk
- **Manager**: Per-product freshness, DQ, cost
- **Engineer**: Pipeline execution logs, data diffs, schema changes

### AI Observability

**Golden Signals AI**:

- **Faithfulness**: ≥0.9 (grounding to context)
- **Citation exactness**: ≥0.95 (valid, traceable)
- **Hallucination rate**: <5% (unsupported claims)
- **TTFT p95**: <1200ms (user perception snappy)
- **TPOT p95**: <50ms (streaming smooth)
- **GPU utilization**: 60-80% sweet spot (under → waste, over → queue)
- **Cache hit rate**: >40% (semantic cache effectiveness)

**Cost per Task** (FinOps):

- **Formula**: `CpT = (Input_Tokens × Price_In + Output_Tokens × Price_Out) / Tasks_Completed`
- **Target**: <$0.50 per resolution
- **Optimization**: Semantic cache (Redis), prompt compression, model selection (GPT-4o-mini vs GPT-4)

**Tools**: Arize AI, WhyLabs, LangSmith, Helicone (LLM observability platforms)

**Dashboards**:

- **Executive**: AH_Score trend, cost burn rate
- **Manager**: Per-agent faithfulness, citations, cost
- **Engineer**: Token usage, latency p95/p99, guardrail triggers

### Process Observability

**Golden Signals Process**:

- **Cycle time p95**: End-to-end duration (target <180min)
- **STP %**: Straight-Through Processing rate (target >80%)
- **HITL backlog**: Queue size exceptions (target <50)
- **MTTR excepciones**: Mean Time To Resolve manual interventions (target <4h)
- **Compensation rate**: % sagas triggered compensations (target <5%)

**Tools**: Camunda Cockpit, Temporal UI, custom dashboards (Grafana + Prometheus)

**Dashboards**:

- **Executive**: PH_Score trend, processes at-risk
- **Manager**: Per-process STP, cycle time, backlog
- **Operator**: Live queue status, exception details, escalations

### Tech Stack Unified

**OpenTelemetry** (vendor-neutral):

- Single SDK for logs + metrics + traces
- **Collectors**: OTLP (OpenTelemetry Protocol) endpoints
- **Exporters**: Prometheus, Jaeger, DataDog, custom

**Prometheus + Grafana** (time-series + viz):

- Metrics scraping, storage, alerting
- Dashboards 3-tier (Executive, Manager, Engineer)

**Jaeger** (distributed tracing):

- Request flows across services/agents/pipelines
- Bottleneck identification

**Conexión KERNEL**:

- **D2_Percepción §2-§8**: Observables base + tech extended
- **E7 §5**: Observability foundation (reference)
- **A5_Medición**: Metrics frameworks comprehensive

---

## §9. GOVERNANCE & COMPLIANCE

### Policy-as-Code (OPA/Rego)

**Data Access Policies**:

```rego
package data.access

default allow = false

allow {
  input.user.role == "finance_engineer"
  input.resource.classification != "P0"  # Not top-secret
  input.resource.domain == "finanzas"  # Domain match
}

allow {
  input.user.role == "auditor"
  input.resource.classification in ["P1", "P2", "P3"]  # Read-only all but P0
}
```

**AI Guardrails Policies**:

```rego
package agent.guardrails

deny[msg] {
  input.agent.iterations > input.agent.max_iterations
  msg := sprintf("Agent %v exceeded max iterations", [input.agent.id])
}
```

**Process Approval Rules**:

```rego
package process.approval

hitl_required {
  input.invoice.amount_total > 10000
}

hitl_required {
  input.invoice.validation_score < 0.85
}
```

**Versioned Git, Tested CI**:

- Policies en Git (version control, audit history)
- CI tests policies (unit tests OPA, integration tests)
- Deploy policies via GitOps (ArgoCD, FluxCD)

### Security Zero-Trust

**mTLS** (Mutual TLS):

- Service-to-service authentication (both parties verify certificates)
- **Benefit**: No shared secrets, certificate-based trust

**JWT/OIDC**:

- User authentication (OAuth 2.1 flow)
- JWT tokens (stateless, claims-based)

**RLS/CLS** (Row/Column Level Security):

- **RLS**: PostgreSQL policies, Delta Lake filters (row-level por user)
- **CLS**: Column masking (PII columns masked per role)

**PII Detection + Masking**:

- **Detection**: Presidio, spaCy NER, regex patterns
- **Masking**: Tokenization (reversible), hashing (irreversible), encryption (key-based)

**Secrets Vault Rotation**:

- Auto-rotation keys/passwords (30-90 días)
- Zero-downtime rotation (dual-active keys during transition)

**Conexión**: E7 §6 Security (foundation, no duplicar)

### Compliance (Sector-Specific)

**GDPR** (EU General Data Protection Regulation):

- Right to erasure (delete user data <30 días)
- Data portability (export user data structured)
- Consent management (granular, revocable)

**HIPAA** (US Health Insurance Portability):

- PHI encryption (at-rest, in-transit)
- Audit trails access (who, when, what)
- Business Associate Agreements (BAAs con vendors)

**SOX** (Sarbanes-Oxley, US Financial):

- Immutable audit logs (financial data access)
- Segregation of duties (no single person end-to-end)
- Change management rigorous (approvals, reviews)

**OWASP Top-10 LLMs**: Ver §5.7

**EU AI Act** (risk-based regulation):

- High-risk AI systems: Conformity assessment, transparency, human oversight
- Prohibited practices: Social scoring, subliminal manipulation
- **Alignment**: Guardrails §5.3 implementan requirements

### FinOps

**Showback/Chargeback Domain**:

- Cost allocation per data domain, AI agent, process
- **Visibility**: Teams see own costs (incentive optimization)
- **Accountability**: Budget ownership (chargeback)

**Unit Economics Workflow**:

- **Data**: Cost/TB, cost/query, cost/product
- **AI**: Cost/task, cost/1K tokens, cost/agent
- **Process**: Cost/transaction, cost/STP instance

**Token Budgets** (LLM cost control):

- Per-agent limits daily/monthly
- Alert 80% budget consumed
- Auto-throttle 100% (prevent overrun)

**Rightsizing Automated**:

- Idle resources detection → Scale down/terminate
- Under-utilized instances → Smaller SKU
- **Tools**: Kubecost (K8s), Cloud provider native (AWS Cost Explorer)

**Conexión**: D4_Operación §9 FinOps, §4.7 FinOps Datos

---

## §10. PATRONES ESPECIALIZADOS (P57-P63)

**IMPORTANTE**: Definiciones canónicas de patterns P57-P63 viven en `APLICACION/A1_Patrones.md` §15 (single source of truth). Esta sección provee **ejemplos concretos E8-specific** y detalles de implementación.

**Ejemplo Implementación**: §3.2 Contrato completo, §4.4 Operating Model Federado (3 consumers: BI, Finance, Auditor).

---

**Ver A1 §15 para**: Problema, Contexto, Solución, Cuándo Usar, Evitar Si, Primitivos KERNEL, Antipatrones.

---

**P57: Data Product Pattern - (`A1_Patrones.md` §15 P57)**
**Ejemplo Concreto E8**: `billing_invoices` Data Product

**P58: RAG Auditable** (`A1_Patrones.md` §15 P58)  
**Ejemplo E8**: Chatbot normativa GORE Ñuble (§12 Caso 2) - Citations artículos Ley 21.180, curation pipeline §6.3, evaluation §6.4.

**P59: Saga Compensation** (`A1_Patrones.md` §15 P59)  
**Ejemplo E8**: Invoice approval workflow §7.3 - Post_ERP step con compensation Revert_Posting, BPMN orchestration Camunda.

**P60: HITL Checkpoint** (`A1_Patrones.md` §15 P60)  
**Ejemplo E8**: Invoice >$10K trigger §7.3, exception queue SLA 24-48h, form-based UI approval, resume workflow state preserved.

**P61: Multi-Agent Orchestration** (`A1_Patrones.md` §15 P61)  
**Ejemplo E8**: §5.6 Multi-Agent Patterns (Router, Supervisor-Worker, Specialist Pool, Debate) - 4 arquitecturas detalladas.

**P62: Contract-Driven Evolution** (`A1_Patrones.md` §15 P62)  
**Ejemplo E8**: `billing_invoices` v2.1.0 → v3.0.0 migration §3.2 - Add field `tax_id` optional, 120 días deprecation, adapter v1→v2.

**P63: Hybrid Search** (`A1_Patrones.md` §15 P63)  
**Ejemplo E8**: RAG normativa §6.3 - BM25 (Ley numbers exact match) + Vector (semantic concepts) + Cross-encoder rerank (autoridad score) + ACL filters

---

## §11. ANTIPATRONES

### Estructura Anti-Pattern (cada 15 líneas × 7 = 105 líneas)

**AP36: RPA Universal Hammer**

**Síntoma**: Usar RPA para toda automatización, incluso cuando APIs/ETL existen.

**Causa**: RPA vendor hype, falta expertise APIs, "quick win" presión.

**Consecuencia**:

- Bots frágiles (UI changes → break)
- Maintenance overhead alto (>60% effort)
- No escala (bots stateful, orchestration compleja)
- Security risk (credential management)

**Fix**:

1. Audit APIs disponibles (99% sistemas modernos tienen)
2. API-first design new integrations
3. RPA solo legacy absoluto sin APIs
4. CoE RPA governance (§7.4)

**Prevention**: Architecture review mandatory (APIs antes RPA approval).

**Fuente**: BPA.md §5

**Severidad**: 🟡 Importante (recoverable, pero costoso refactor)

---

**AP37: Data Sin Contrato**

**Síntoma**: Datos compartidos sin schema documentado, SLO, ownership.

**Causa**: "Move fast" cultura, no data governance, silos.

**Consecuencia**:

- Breaking changes silent (consumers crash production)
- Quality unknown (garbage in → garbage out)
- No ownership (nobody fixes issues)
- No lineage (impact analysis imposible)

**Fix**:

1. Implementar data contracts (§3.2 template)
2. Schema registry (Confluent, Apicurio)
3. Ownership assignment (RACI)
4. Lineage tools (OpenLineage)

**Prevention**: Contract-first data products (P57, P62).

**Fuente**: DATA.md anti-patterns

**Severidad**: 🔴 Crítico (data corruption, production outages)

---

**AP38: RAG Sin Curation**

**Síntoma**: RAG sobre corpus sin curate (fuentes no oficiales, vigencia unknown, calidad baja).

**Causa**: "Quick win" LLM without data quality investment.

**Consecuencia**:

- Hallucinations altas (>20%)
- Citas inválidas o ausentes
- Info desactualizada (derogado retrieved)
- Compliance risk (leak restricted docs)

**Fix**:

1. Curation pipeline (§6.3 5 fases)
2. Authority validation (solo oficial)
3. Vigencia tracking (metadata)
4. ACL enforcement (pre-filters)

**Prevention**: P58 RAG Auditable (curation mandatory).

**Fuente**: KNOW.md §10 + OCE

**Severidad**: 🔴 Crítico (legal risk, trust loss)

---

**AP39: Observabilidad Mínima IA**

**Síntoma**: LLM en producción sin monitoring faithfulness, cost, latency.

**Causa**: Treat LLM como "black box", no ML observability expertise.

**Consecuencia**:

- Degradation silent (quality drops, nobody notices)
- Cost overruns (no budgets, throttling)
- Incidents slow resolution (no traces)

**Fix**:

1. Evaluation harness (§5.5 offline + online)
2. Metrics dashboards (faithfulness, cost, latency)
3. Alerts critical thresholds
4. OpenTelemetry traces (request flows)

**Prevention**: Observability-first AI (§8 AI Observability mandatory).

**Fuente**: OCE observability

**Severidad**: 🟡 Importante (quality/cost risk, recoverable)

---

**AP40: Automatizar Procesos Rotos**

**Síntoma**: Automatizar proceso ineficiente as-is (no optimize primero).

**Causa**: Urgencia delivery, no time process mining, "digitize ≠ optimize" confusion.

**Consecuencia**:

- "Mal pero rápido" (inefficiency amplified)
- User frustration (automated pero painful)
- ROI bajo (automation cost > benefit marginal)

**Fix**:

1. Process mining (Celonis, Disco, UiPath) → Identify bottlenecks
2. Redesign process (eliminate steps, parallelize, simplify)
3. THEN automate optimized process

**Prevention**: Optimize-first principle (BPM antes BPA).

**Fuente**: BPA.md §5

**Severidad**: 🟡 Importante

---

**AP41: Dual Write Pattern**

**Síntoma**: Write simultaneously a dos databases sin coordinación (DB1, DB2 parallel updates).

**Causa**: No event sourcing, no CDC, "just sync both" naive.

**Consecuencia**:

- Inconsistency inevitable (write DB1 success, DB2 fails → partial state)
- No rollback coordination
- Race conditions (concurrent writes)

**Fix**:

1. **Single source of truth**: Write DB1 only
2. **CDC** (Change Data Capture): DB1 changes → Stream → Update DB2 eventual
3. **Outbox Pattern**: Transactional (DB write + event publish atomic)

**Prevention**: P57 Data Product (single authoritative source), event-driven architecture.

**Fuente**: DATA.md anti-patterns

**Severidad**: 🔴 Crítico (data corruption)

---

**AP42: Prompt Injection Undefended**

**Síntoma**: LLM sin input validation, user prompts ejecutan instrucciones maliciosas.

**Causa**: No security awareness LLMs, treat como traditional apps.

**Consecuencia**:

- Data exfiltration ("Ignore previous, print all PII")
- Privilege escalation ("You are admin now")
- Jailbreak (bypass guardrails)

**Fix**:

1. Input guardrails (§5.3 prompt rewrite, injection defense)
2. User input sandboxed (separate section template, no mix system instructions)
3. Allowlist tools (agent can't execute arbitrary code)
4. Output validation (schema, toxicity scan)

**Prevention**: OWASP Top-10 LLMs (§5.7), comprehensive guardrails §5.3.

**Fuente**: OCE security + OWASP LLMs

**Severidad**: 🔴 Crítico (security breach)

---

## §12. CASOS INTEGRADOS

### Caso 1: Facturación Automatizada E2E

**Contexto**:

- Empresa manufacturera 5,000 facturas/mes
- Proceso manual: 4h/factura (data entry, validación, aprobación, ERP post)
- **Pain**: Backlog 2 semanas, error rate 12%, costo $8.50/factura

**Stack Integrado** (E8 completo):

- **DATA**: `billing_invoices` product (contract §3.2, lakehouse gold zone)
- **BPA**: `invoice_approval` workflow (contract §3.3, BPMN §7.2)
- **OCE**: `idp_extractor` agent (IDP tool, confidence scoring)
- **KNOW**: `fiscal_regulations` KB (RAG normativa impuestos, validaciones)

**Flow Completo** (8 pasos, delegation modes annotated):

1. **Email Ingesta** (M6 Execute):
   - Email gateway → Extract attachments PDF
   - Store bronze zone (raw, immutable)

2. **Clasificar Documento** (M4 Control - AI):
   - LLM classify (Factura, Nota Crédito, Otro)
   - Confidence >0.90 → Proceed
   - Confidence <0.90 → HITL queue clasificación

3. **Extraer Datos IDP** (M5 Co-produce - AI + validation):
   - IDP agent (Tesseract OCR + GPT-4V vision)
   - Extract: invoice_id, customer_id, amount, line_items, dates
   - Confidence per field

4. **Validar Reglas Negocio** (M6 Execute - rules engine):
   - Fiscal regulations KB (RAG) → Retrieve rules applicable
   - Validate: Tax rate correct, amount calculations, required fields
   - Business rules engine (Drools) scores compliance

5. **HITL Si >$10K o Score <0.85** (M1 Monitor):
   - Route to `exceptions.approval` queue
   - Human reviews: extracted data, validation errors, original PDF
   - Decision: Approve (with corrections), Reject, Request more info
   - SLA: 48h (escalate supervisor if exceeded)

6. **Post ERP API** (M6 Execute - integration):
   - Call SAP API `/invoices/post`
   - Idempotency key: `invoice_id`
   - Success → Saga completes
   - Failure → Trigger compensation OR RPA fallback

7. **RPA Fallback** (M6 Execute bounded - último recurso):
   - Si API timeout/500 error persistente
   - UiPath bot logs in SAP GUI
   - Screen selectors validated (stability check)
   - Credential vault (JIT)
   - Post invoice, screenshot confirmation

8. **Archive & Notify** (M6 Execute):
   - Archive PDF + extracted_data → Document store
   - Update `billing_invoices` product (silver → gold pipeline)
   - Notify: Approver, Accounting team, Auditor (según roles)

**Métricas Resultado**:

| Métrica | Antes | Después | Mejora |
|:---|:---|:---|:---|
| Cycle time p95 | 4h | 45min | -81% |
| STP % | 0% (100% manual) | 82% | - |
| Error rate | 12% | 2.3% | -81% |
| Cost per invoice | $8.50 | $0.45 | -95% |
| Backlog | 2 semanas | <1 día | -93% |
| Human effort | 100% | 18% (HITL only) | -82% |

**Timeline Implementación**: 6 meses (pilot 2m, scale 4m)

**ROI**: Payback 8 meses, NPV 3 años $450K (5000 facturas/mes × savings)

**Conexión KERNEL**:

- **Integrates**: §3 (contracts), §4 (data), §5 (AI), §6 (knowledge), §7 (process)
- **Patterns applied**: P57, P58, P59, P60 explícitos
- **Delegation**: M1-M6 spectrum completo una pipeline
- **H_Score impact**: O11 Process Effectiveness +40 puntos (45 → 85)

### Caso 2: Chatbot Normativa Sector Público

**Contexto**:

- GORE Ñuble, 200 funcionarios consultas normativa diariamente
- Proceso manual: Email abogado, espera 2-48h, respuesta prosa sin citas
- **Pain**: Bottleneck legal team (3 abogados), inconsistencia respuestas, no trazabilidad

**Stack Integrado**:

- **KNOW**: `normativa_interna` collection (curated, 450 docs: Leyes, Decretos, Resoluciones, Instructivos)
- **OCE**: `rag_agent_normativa` (RAG contract §3.5, delegation M3 Enable)
- **DATA**: `consultas_analytics` product (track queries, improve KB coverage)

**Flow**:

1. **User Query** (natural language):
   - "¿Qué dice la Ley 21.180 sobre expedientes electrónicos?"
   - Interface: Slack bot, web chat, Teams integration

2. **Hybrid Search** (P63):
   - BM25: "Ley 21.180" + "expediente electrónico" (keyword exact)
   - Vector: Semantic similarity "documentos digitales gestión" (concept match)
   - Fusion: RRF (Reciprocal Rank Fusion) top-50

3. **Rerank** (Cross-Encoder):
   - Features: Vigencia (vigente priority), Autoridad (Ley > Instructivo), Entidades match
   - Top-10 chunks final

4. **Context Assembly**:
   - 10 chunks with metadata (doc, artículo, vigencia)
   - Hierarchy: `Ley_21180 > Título_II > Art_18 > Inciso_2`

5. **Generate Response** (M3 Enable - augment human):
   - LLM (GPT-4o-mini): Synthesize answer
   - **Modo extractivo**: Citas textuales artículos
   - **Mandatory citations**: [Ley 21.180, Art. 18, Inc. 2]

6. **Validate Output**:
   - Faithfulness check (grounded in context?)
   - Citation validation (all citations traceable?)
   - Toxicity scan (safe content?)

7. **Response con Citas**:
   - Answer prosa clara + sección "Fuentes" (citas estructuradas)
   - Nota vigencia: "(Vigente desde 2022-06-09)"

8. **Analytics** (continuous improvement):
   - Log query, response, citations used
   - Track: Satisfaction (thumbs up/down), query topics trending
   - Identify: Coverage gaps → Curate more docs

**Métricas Resultado**:

| Métrica | Antes | Después | Mejora |
|:---|:---|:---|:---|
| Resolution rate | 65% (abogado responde) | 85% (chatbot + HITL edge) | +31% |
| Response time p95 | 24h | 8s | -99.99% |
| Citation accuracy | N/A (prosa sin citas) | 0.96 | - |
| Satisfaction (CSAT) | 3.2/5 | 4.3/5 | +34% |
| Legal team load | 100% | 15% (HITL review only) | -85% |

**Timeline**: 4 meses (curation 2m, agent build 1m, adoption 1m)

**Conexión KERNEL**:

- **Patterns**: P58 RAG Auditable, P63 Hybrid Search
- **Delegation**: M3 Enable (agent augments funcionarios, no reemplaza)
- **E2_Público**: Gov-specific normativa (TDE Chile applicable)

### Caso 3: Data Mesh Multi-Dominio

**Contexto**:

- Enterprise 3 dominios (Finanzas, RRHH, Operaciones)
- **Before**: Data warehouse central (bottleneck DE team)
- **Pain**: Request data → 4 semanas backlog, quality baja (DE no domain experts), no ownership

**Solución** (Data Mesh):

**Dominios** (federados):

1. **Finanzas**: 3 products (billing_invoices, revenue_metrics, budget_actuals)
2. **RRHH**: 3 products (employees_master, payroll_summary, turnover_metrics)
3. **Operaciones**: 3 products (inventory_stock, supply_chain_orders, production_metrics)

**Governance Central**:

- **OPA policy-as-code**: Access policies, DQ baselines, retention rules
- **Catalog central**: Unity Catalog (AWS), DataHub (open-source)
- **SLO monitoring**: Prometheus + Grafana dashboards 3-tier
- **Lineage graph**: OpenLineage → Marquez UI (impact analysis)

**Platform** (enablement, no ownership):

- **Lakehouse**: Delta Lake sobre S3 (bronze/silver/gold zones)
- **Compute**: Spark on Kubernetes (auto-scaling)
- **Orchestration**: Apache Airflow (DAGs versionados Git)
- **Catalog**: Unity Catalog (metadata, ACLs, lineage)

**Métricas Resultado**:

| Métrica | Antes (Central DW) | Después (Data Mesh) | Mejora |
|:---|:---|:---|:---|
| Data products | 3 (centralizados) | 9 (federados) | +200% |
| Time-to-market new product | 4 semanas | 1 semana | -75% |
| Freshness p95 | 24h (batch nightly) | 22min (streaming) | -98% |
| DQ violations/1k | 3.5 | 0.08 | -98% |
| Ownership clarity | Ambiguo (DE team) | Clear (domain POs) | - |
| Satisfaction consumers | 2.8/5 | 4.5/5 | +61% |

**Adoption**: 12 meses (platform 4m, domain 1 per 2m sequential, governance continuous)

**Conexión KERNEL**:

- **P57 Data Product**: 9 products con contracts
- **Federación**: Domain autonomy con guardrails centralizados (meta-principio §1)
- **D1 §14**: Architecture patterns data mesh

---

## §13. CONEXIÓN KERNEL

### Primitivos Especializados E8

| Primitivo KERNEL | Manifestación E8 | Ejemplos Concretos |
|:---|:---|:---|
| **Dato** | ProductoDeDatos, Documento, Chunk, Feature, Event | `billing_invoices` (product), `ley21180_art18` (chunk), `invoice.received` (event) |
| **Actor** | LLM_Agent, RPA_Bot, Data_Engineer, Knowledge_Engineer, Process_Owner | `invoice_reviewer` (agent), `sap_posting_bot` (RPA), Data PO (actor) |
| **Flujo** | BPMN_Process, ETL_Pipeline, RAG_Pipeline, Saga_Flow | `invoice_approval` (BPMN), `bronze→silver→gold` (ETL), retrieval pipeline (RAG) |
| **Recurso** | Lakehouse, Model_Endpoint, Vector_DB, Knowledge_Base, Workflow_Engine | Delta Lake S3 (lakehouse), vLLM endpoint (model), Qdrant (vector), Camunda (workflow) |
| **Señal** | Event (EDA), DQ_Violation, Process_Exception, Guardrail_Trigger | `invoice.received`, `dq_fail_alert`, `hitl_escalation`, `cost_limit_exceeded` |
| **Límite** | SLO, Contract, Guardrail, Error_Budget, Deprecation_Policy | Freshness <30min, schema contract, max_iterations=5, budget 0.1%, 90d deprecation |

### Dominios KERNEL Extendidos

**D1_Arquitectura**:

- Tech stack patterns (reference E7 primario, E8 secundario lakehouse/vector DBs)
- Data architecture (medallion bronze/silver/gold §4.3)
- Multi-agent architecture (supervisor-worker §5.6)

**D2_Percepción + §8 Tech Observables** (extension v2.0 Week 6):

- **O_Base**: O1-O11 (CORE/05, D2 existentes)
- **OT1 Data Health**: Freshness p95, DQ violations/1k, Lineage coverage %
- **OT2 AI Performance**: Faithfulness, Citation exactness, TTFT p95, Cost/task
- **OT3 Process Effectiveness**: STP %, Cycle time p95, HITL backlog, MTTR

**D3_Decisión + §8 Algorithmic Modes** (extension v2.0 Week 6):

- **D_Base**: D1-D4 (existing decision modes)
- **D5 RAG-Augmented**: Evidence-based, citations mandatory (M3-M4)
- **D6 ReAct (Tool Calling)**: Reasoning→Action→Observation loop (M4-M5)
- **D7 Plan & Execute**: Multi-step planning, checkpoints (M5-M6)

**D4_Operación + §13 Tech Execution** (extension v2.0 Week 6):

- **E_Base**: E1-E3 (existing execution modes)
- **E4 Orquestada (BPMN)**: Workflow engine visibility, sagas, SLAs (M4)
- **E5 Reactiva (Event-Driven)**: Event bus, exactly-once, watermarks (M5-M6)
- **E6 Asistida (RPA + HITL)**: Bots + exception queues, último recurso (M5)

**Tabla Integración Delegation × Decision × Execution**:

| Decision Mode | Typical Delegation | Execution Mode | Example E8 |
|:---|:---|:---|:---|
| D5 RAG | M3 Enable | E4 Orquestada | Chatbot normativa (orchestrated RAG pipeline) |
| D6 ReAct | M4-M5 Control/Co-produce | E4 Orquestada | Invoice IDP agent (tool calls orchestrated) |
| D7 Plan&Execute | M5-M6 Co-produce/Execute | E5 Reactiva | Multi-step saga compensation (event-driven) |

**Conexión KERNEL**:

- **CORE/02 Flujo §4**: A1-A3 execution augmented con E4-E6
- **CORE/04 Delegación §8**: Purpose dimension extended algorithms
- **CORE/03 Decisión §3**: D1-D4 extended con D5-D7 algorithmic

---

## §14. MÉTRICAS TECH

### DH_Score (Data Health 0-100)

**Formula**:

```
DH_Score = 0.30×Freshness_Norm + 0.25×DQ_Norm + 0.20×Lineage_Norm + 0.15×SLO_Compliance + 0.10×Satisfaction
```

**Componentes**:

**Freshness_Norm** (0-100):

- Measure: `p95_freshness_minutes`
- Normalization: `100 - (p95_actual / p95_target × 100)` capped [0,100]
- Example: Target 30min, actual 22min → 100 - (22/30×100) = 27 → **100** (exceeds target = 100)

**DQ_Norm** (0-100):

- Measure: `violations_per_1k_rows`
- Normalization: `100 - (violations_actual / violations_threshold × 100)` capped [0,100]
- Example: Threshold 0.8, actual 0.08 → 100 - (0.08/0.8×100) = 90 → **90**

**Lineage_Norm** (0-100):

- Measure: `% columns con lineage documented`
- Direct: 85% coverage → **85**

**SLO_Compliance** (0-100):

- Measure: `(SLO_met / SLO_total) × 100`
- Example: 3 SLOs (freshness, availability, accuracy), 3 met → **100**

**Satisfaction** (0-100):

- Measure: CSAT surveys consumers (scale 1-5 → 0-100)
- Conversion: `(CSAT - 1) / 4 × 100`
- Example: CSAT 4.5/5 → (4.5-1)/4×100 = **87.5**

**Benchmarks**:

- **>80**: Excellent (world-class data products)
- **60-80**: Good (industry standard)
- **<60**: Needs attention (quality/reliability issues)

**Conexión**: A5_Medición §10 (extension v2.0 Week 7 - detailed)

### AH_Score (AI Health 0-100)

**Formula**:

```
AH_Score = 0.30×Faithfulness_Norm + 0.25×Citation_Norm + 0.20×Latency_Norm + 0.15×Cost_Norm + 0.10×Satisfaction
```

**Componentes**:

**Faithfulness_Norm** (0-100):

- Measure: Faithfulness score (0-1)
- Conversion: `Faithfulness × 100`
- Target: ≥0.90 → **≥90**

**Citation_Norm** (0-100):

- Measure: Citation exactness (0-1)
- Conversion: `Citation_Exactness × 100`
- Target: ≥0.95 → **≥95**

**Latency_Norm** (0-100):

- Measure: `TTFT_p95_ms`
- Normalization: `100 - (TTFT_actual / TTFT_target × 100)` capped [0,100]
- Target: <1200ms

**Cost_Norm** (0-100):

- Measure: `Cost_per_Task_USD`
- Normalization: `100 - (Cost_actual / Cost_target × 100)` capped [0,100]
- Target: <$0.50

**Satisfaction** (0-100):

- CSAT conversion (same as DH_Score)

**Benchmarks**:

- **>85**: Excellent (production-grade AI)
- **70-85**: Good (acceptable quality/cost)
- **<70**: Needs improvement (hallucinations, cost, or latency issues)

### PH_Score (Process Health 0-100)

**Formula**:

```
PH_Score = 0.35×STP_Norm + 0.25×CycleTime_Norm + 0.20×Error_Norm + 0.15×HITL_Backlog_Norm + 0.05×Compensation_Norm
```

**Componentes**:

**STP_Norm** (0-100):

- Measure: `STP_percentage`
- Direct: 82% STP → **82**

**CycleTime_Norm** (0-100):

- Measure: `cycle_time_p95_minutes`
- Normalization: `100 - (actual / target × 100)` capped
- Target: <180min

**Error_Norm** (0-100):

- Measure: `error_rate_percentage`
- Inverse: `100 - error_rate`
- Example: 2.3% error → **97.7**

**HITL_Backlog_Norm** (0-100):

- Measure: `hitl_queue_size`
- Inverse normalization: `100 - (backlog_actual / backlog_threshold × 100)` capped
- Threshold: 50 items

**Compensation_Norm** (0-100):

- Measure: `compensation_rate_percentage` (sagas triggered)
- Inverse: `100 - compensation_rate × 20` (weight 5% in formula)
- Target: <5% compensations

**Benchmarks**:

- **>80**: Excellent (streamlined, automated)
- **65-80**: Good (functional, minor friction)
- **<65**: Needs optimization (bottlenecks, manual heavy)

### H_Score Extended (Integration)

**KERNEL v2.0 extended** (14 observables):

```
H_Score_v2 = weighted_avg(O1-O11)
```

- **O1-O11**: Base observables (CORE/05 §3, D2_Percepción)

**Observables Técnicos de Diagnóstico (OT1-OT3) 0-100)**

**Formula**:

```
PH_Score = 0.35×STP_Norm + 0.25×CycleTime_Norm + 0.20×Error_Norm + 0.15×HITL_Backlog_Norm + 0.05×Compensation_Norm
```

- **OT1**: Data Health (DH_Score)
- **OT2**: AI Performance (AH_Score)
- **OT3**: Process Effectiveness (PH_Score)

**Relación con H_Score Canónico**: Los OT no forman parte del cálculo directo del H_Score, sino que actúan como **indicadores de causa raíz (drivers)** de los 16 observables principales. Un problema en un OT típicamente degrada uno o más de los observables canónicos.

**Conexión**: A5_Medición §10 (extension v2.0)

---

## §15. TEMPLATES RELACIONADAS

### Templates Contracts

- **T15_Contrato_Datos**: Ver §3.2 estructura base + example (REFERENCIA v2.0 Week 5)
- **T16_Contrato_Proceso**: Ver §3.3 estructura base + example (REFERENCIA v2.0 Week 5)
- **T17_Contrato_Agente**: Ver §3.4 estructura base + example (REFERENCIA v2.0 Week 5)
- **T18_Contrato_Conocimiento**: Ver §3.5 estructura base + example (REFERENCIA v2.0 Week 5)

### Templates Specs

- **T20_Data_Product_Spec**: Extiende T15 con product thinking (consumers, use cases, KPIs, roadmap) - REFERENCIA v2.0 Week 5
- **T21_AI_Agent_Spec**: Extiende T17 con deployment (model serving, autoscaling, FinOps, eval harness) - REFERENCIA v2.0 Week 5
- **T22_Process_Model_BPMN**: BPMN visual + executable YAML, swimlanes, testing scenarios - REFERENCIA v2.0 Week 5

**Todas templates creadas Week 5 según RADICAL_PLUS_PLAN_v2.0.md**.

---

## §16. ROADMAP IMPLEMENTACIÓN

### Fase 1: Foundations (M1-3, ~90 días)

**Objetivos**:

- Contracts foundation establecida
- 2 data products pilot
- 1 proceso BPMN automatizado
- 1 agente RAG production

**Actividades**:

1. **Governance setup** (mes 1):
   - CDO appointed, Data Council kickoff
   - OPA policies base (access, DQ baselines)
   - Tools selection (lakehouse, vector DB, workflow engine)

2. **Platform MVP** (mes 1-2):
   - Lakehouse deployed (Delta Lake S3 o Databricks)
   - Vector DB (Qdrant o pgvector)
   - Workflow engine (Camunda Community o Temporal)
   - Observability base (Prometheus + Grafana)

3. **Pilots** (mes 2-3):
   - Data product: `billing_invoices` (contract, pipeline, serving)
   - Data product: `customer_360` (analytics)
   - Process: `invoice_approval` (BPMN con HITL, RPA fallback)
   - Agent: `normativa_chatbot` (RAG curated, citations mandatory)

4. **Eval & Learn** (mes 3):
   - Metrics baselines (DH/AH/PH scores)
   - Lessons learned documentation
   - Roadmap adjust (Fase 2 plan)

**Deliverables Fase 1**:

- ✅ 2 data products production
- ✅ 1 process automated (STP >70%)
- ✅ 1 RAG agent (citation >0.90)
- ✅ Observability dashboards 3-tier
- ✅ Governance policies live (OPA)

### Fase 2: Scale Platform (M4-9, ~180 días)

**Objetivos**:

- Platform production-grade
- 5-10 data products
- 3-5 agents deployed
- 5+ procesos automatizados

**Platform Build**:

- **Lakehouse**: Multi-domain (Finanzas, RRHH, Ops)
- **Model serving**: vLLM cluster autoscaling
- **Workflow engine**: HA (High Availability) setup
- **Catalog**: DataHub o Unity Catalog (lineage + discovery)
- **Observability**: Full-stack (OpenTelemetry, Jaeger, advanced dashboards)

**Data Products** (5-10):

- Finanzas: revenue, budget, forecasts
- RRHH: headcount, turnover, payroll
- Ops: inventory, supply chain, production

**AI Agents** (3-5):

- RAG: Normativa, FAQs, knowledge search
- ReAct: Invoice IDP, contract review
- Planning: Workflow automation assistants

**Processes** (5+):

- Invoice-to-cash
- Hire-to-retire (RRHH)
- Procure-to-pay
- Support ticket resolution

### Fase 3: Federate & Govern (M10-18, ~270 días)

**Objetivos**:

- 10+ data products
- 5+ agents production-scale
- 20+ processes automated
- CoEs activos (Data, AI, BPA)

**Federación**:

- Domain teams ownership (3-5 domains)
- Platform team pure enablement (no product ownership)
- Guardrails centralizados mature (policy-as-code comprehensive)

**CoEs (Centers of Excellence)**:

- **CoE Data**: Best practices, reusable templates, data stewards network
- **CoE AI**: Model evaluation standards, prompt libraries, ethics board
- **CoE BPA**: Process mining, BPMN templates, RPA governance

**Advanced Capabilities**:

- **MDM**: Customer/Product golden records (match/merge algorithms)
- **Privacy advanced**: K-anonymity, differential privacy (ver E2_Público §10)
- **FinOps mature**: Chargeback operational, cost optimization automated
- **Deprecation systematic**: Schema evolution playbooks, backward-compat enforced

**Metrics Maturity**:

- **DH_Score**: >80 all products (excellent)
- **AH_Score**: >85 all agents
- **PH_Score**: >80 all processes
- **H_Score**: >85 org-wide (14 observables)

**Conexión KERNEL**:

- **A4_Implementación**: Roadmap structured (MVP → Scale → Optimize)
- **CORE/06 Capacidades**: C1-C7 todas habilitadas tech-augmented

---

## REFERENCIAS CRUZADAS

### CORE

- **CORE/01 Recurso §2-§3**: Datos, stack, infra como recursos
- **CORE/02 Flujo §4**: Pipelines, workflows, sagas como flujos
- **CORE/03 Actor §4**: Specialized actors (Data Engineer, AI Engineer, etc.)
- **CORE/03 Límite §3-§5**: SLOs, contracts, guardrails como límites
- **CORE/04 Delegación §3-§8**: M1-M6 aplicados AI/automation
- **CORE/05 Smartness §3-§5**: Quality, observability como smartness
- **CORE/06 Capacidades §2-§4**: Data, KM, AI como capabilities
- **CORE/07 Invariantes §1-§3**: I1 Minimalidad (contracts unificados), I2 Ortogonalidad (E7-E8 95%), I3 Trazabilidad (lineage)
- **CORE/08 Crisis Management**: Exception handling, HITL como crisis prevention

### DOMINIOS

- **D1_Arquitectura §1-§2**: Org structure, stack patterns, data architecture
- **D1 §14** (extension v2.0 Week 6): Tech Stack Patterns detallado
- **D2_Percepción §2**: Observables base O1-O11
- **D2 §8** (extension v2.0 Week 6): Tech Observables OT1-OT3 (DH, AH, PH)
- **D3_Decisión §3**: Decision modes base D1-D4
- **D3 §8** (extension v2.0 Week 6): Algorithmic Modes D5-D7 (RAG, ReAct, Plan)
- **D4_Operación §2-§4**: Execution modes, CI/CD
- **D4 §13** (extension v2.0 Week 6): Tech Execution E4-E6 (Orquestada, Reactiva, Asistida)

### APLICACION

- **A1_Patrones**:
  - P53 Orchestration Agent
  - P54-P56 Desarrollo (Piecemeal, Walking Skeleton, Continuous Refactoring)
  - P57-P63 Tech Patterns (nuevos v2.0, este doc §10)
- **A2_Antipatrones**:
  - AP36-AP42 Tech Anti-Patterns (nuevos v2.0, este doc §11)
- **A3_Diagnóstico §4**: Tech friction assessment
- **A4_Implementación §3-§5**: Governance, KM, roadmaps
- **A5_Medición**:
  - §5 DORA metrics (reference)
  - §7 Evaluation frameworks
  - §10 Tech Metrics (extension v2.0 Week 7)

### DOMINIOS_ESPECIALIZADOS

- **E7_Enterprise_Technology**: Apps, UX, DevOps (orthogonal 90%, overlap infra 10%)
- **E2_Público**: Gov-specific (TDE Chile, normativa RAG applicable)
- **E3-E5**: Sector-specific patterns (reference tech base E7-E8)

### REFERENCIA

- **R1_Casos**: Casos tech agregados (migrations)
- **R6_Templates**:
  - T13_ADR (existente v1.4)
  - T15-T18 Contracts (nuevos v2.0)
  - T19-T22 Specs (nuevos v2.0)
- **R7_Bibliografia**: Sources (DATA, OCE, KNOW, BPA, SIGMA) - Week 8

---

