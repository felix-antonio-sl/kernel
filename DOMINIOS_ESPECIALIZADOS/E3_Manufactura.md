# E3_Sector_Manufactura (Industry 4.0)

**Versión:** 2.0.0  
**Estado:** Production  
**Audiencia:** Directores Operaciones, Ingenieros Industriales, Jefes Planta, Arquitectos MES/SCADA  
**Dependencias**: CORE/01-08, DOMINIOS/D1-D4, APLICACION/A1-A5, E7-E8

---

## §0. QUICK START MVM (Minimum Viable Manufacturing 4.0)

### Checklist MVM (6 meses - Digital Twin Básico + Predictive Maintenance)

**1. Sensórica Básica** (Mes 1-2):

- ✅ Instrumentar 3-5 máquinas críticas (sensores vibración, temperatura, corriente)
- ✅ IoT gateway (MQTT broker, edge computing)
- ✅ Conectividad cloud (AWS IoT, Azure IoT Hub, Google Cloud IoT)

**2. Data Pipeline** (Mes 2-3):

- ✅ Ingesta streaming (Kafka, Azure Event Hubs)
- ✅ Storage time-series (InfluxDB, TimescaleDB)
- ✅ Dashboards real-time (Grafana, PowerBI)

**3. Analytics Básico** (Mes 3-4):

- ✅ OEE cálculo automático (disponibilidad × rendimiento × calidad)
- ✅ Alertas anomalías (thresholds vibración, temperatura)
- ✅ Digital twin básico (gemelo 3D estado máquina, Unity3D o Siemens Plant Simulation)

**4. Predictive Maintenance Pilot** (Mes 4-6):

- ✅ ML model vibración → Predict falla (LSTM, Random Forest)
- ✅ RUL (Remaining Useful Life) estimation
- ✅ Maintenance scheduling automated (integration CMMS)

**Resultado MVM**:

- **OEE**: +5-10 puntos (baseline → instrumented)
- **MTBF** (Mean Time Between Failures): +15%
- **Unplanned downtime**: -20%
- **ROI**: 12-18 meses

**Conexión KERNEL**: D4_Operación §3 MVA/MVP, CORE/06 Capacidades C4 Technology

---

## §1. OVERVIEW SECTOR + REGULACIÓN

### Manufactura Chile (Contexto)

**Sectores Clave**:

- **Minería**: Cobre, litio (40% exportaciones chilenas)
- **Alimentos**: Vino, salmón, frutas (agroindustria)
- **Forestal**: Celulosa, madera
- **Metalmecánica**: Autopartes, maquinaria industrial
- **Química**: Fertilizantes, plásticos

**Desafíos Industria 4.0 Chile**:

- Brecha productividad vs países OCDE (40% gap)
- Adopción tecnología heterogénea (grandes empresas avanzadas, pymes rezagadas)
- Talento especializado escaso (data scientists industriales, ingenieros IoT)
- Inversión I+D baja (0.36% PIB vs 2.4% OCDE promedio)

**Oportunidad**:

- Industry 4.0 puede cerrar brecha productividad (McKinsey: +25-45% output manufacturing)
- Smart manufacturing como diferenciador competitivo (calidad, customization, sostenibilidad)

### Regulación y Standards

**ISO 9001** (Sistemas Gestión Calidad):

- Requisitos SGC (enfoque procesos, mejora continua, satisfacción cliente)
- Certificación (auditoría tercera parte, renovación anual)
- **Aplicable**: Todos sectores manufactura

**Six Sigma** (Metodología Calidad):

- DMAIC (Define, Measure, Analyze, Improve, Control)
- Métricas: DPMO (Defects Per Million Opportunities), Sigma level (6σ = 3.4 DPMO)
- **Conexión KERNEL**: CORE/05 Smartness (Six Sigma operationaliza quality systematic)

**Safety Standards**:

- **ISO 45001**: Sistemas Gestión Seguridad y Salud Ocupacional
- **OHSAS 18001** (predecessor ISO 45001, aún vigente transición)
- **Req Chile**: Ley 16.744 (Seguro Accidentes Trabajo), DS 594 (Condiciones Sanitarias Básicas)

**Ambiental**:

- **ISO 14001**: Sistemas Gestión Ambiental
- **Req Chile**: SEIA (Sistema Evaluación Impacto Ambiental), emisiones (DS 138/2005)

**Industry-Specific**:

- **Alimentos**: HACCP, ISO 22000 (seguridad alimentaria)
- **Automotriz**: IATF 16949 (calidad automotriz)
- **Farmacéutica**: GMP (Good Manufacturing Practices), ISO 13485 (medical devices)

**Conexión KERNEL**: Límite L3 (regulatory compliance como límite operación)

---

## §2. MAPEO PRIMITIVOS KERNEL

| Primitivo | Manifestación Manufactura | Ejemplo Planta Automotriz |
|:---|:---|:---|
| **Recurso** | Máquinas, líneas producción, materias primas, WIP, finished goods, personal, energía | Línea ensamble robots (R3 Capacity), Inventario chassis (R2 Material), Operadores turno (R4 Human) |
| **Flujo** | Procesos producción, supply chain, quality control, maintenance workflows | Estampado → Soldadura → Pintura → Ensamble (F3 Complex), Kanban pull (F2 Automated) |
| **Actor** | Operadores, supervisores, ingenieros proceso, técnicos mantenimiento, planificadores | Operador CNC (A2 Organizational), Ingeniero proceso (A3 Specialized), AGV robot (A5 Automated) |
| **Señal** | Alarmas máquina, quality defects, cambios demanda, eventos supply chain | Vibración >threshold (S2 Digital), defecto visual (S1 Natural), orden producción (S2 Digital) |
| **Dato** | Telemetría sensores, parámetros proceso, métricas calidad, órdenes producción | Temperatura motor 85°C (D1 Signal), defectos/1M 340 (D2 Structured), orden #12345 (D2) |
| **Límite** | SLAs clientes, capacity constraints, quality specs, safety regulations, presupuesto | Lead time <15 días (L1 Performance), Capacidad 10K unidades/mes (L1), Defects <500 DPMO (L2 Quality) |

**Conexión**: CORE/01-03 Primitivos (E3 especializa manufactura)

---

## §3. STACK TECNOLÓGICO VERTICAL

### MES (Manufacturing Execution Systems)

**Función**: Bridge ERP ↔ Shop Floor (gestionar producción tiempo real).

**Vendors Líderes**:

- **Siemens Opcenter** (ex-Camstar): Suite completa, integración Siemens automation
- **Rockwell FactoryTalk**: Integrated con Allen-Bradley PLCs
- **SAP ME** (Manufacturing Execution): Integración nativa SAP ERP
- **Dassault Systèmes DELMIA**: MES + digital twin (3DEXPERIENCE platform)

**Capacidades MES**:

1. **Production Scheduling**: Órdenes → Secuencia optimizada (constraints capacity, materiales)
2. **Quality Management**: Inspecciones, SPC (Statistical Process Control), NCRs (Non-Conformance Reports)
3. **Maintenance Management**: Work orders, preventive/predictive schedules
4. **Genealogy/Traceability**: Batch/serial tracking (compliance, recalls)
5. **Performance Analysis**: OEE real-time, downtimes root cause

**Conexión KERNEL**: Recurso R3 (MES como capacity platform)

### SCADA & IoT

**SCADA** (Supervisory Control and Data Acquisition):

- **Función**: Monitorear y controlar procesos industriales (PLCs, RTUs, HMIs)
- **Vendors**: Siemens WinCC, Rockwell RSView, Wonderware InTouch, Ignition (Inductive Automation)

**IoT Industrial** (IIoT):

- **Cloud Platforms**:
  - **AWS IoT Core**: MQTT broker, rules engine, shadows (device state)
  - **Azure IoT Hub**: D2C/C2D messaging, Azure Digital Twins integration
  - **Siemens MindSphere**: Industrial IoT SaaS (analytics, apps pre-built)
  - **GE Predix** (sunset 2021, migrated): Early IIoT, lessons learned (cloud-agnostic now preferred)
- **Edge Computing**: AWS Greengrass, Azure IoT Edge (local processing, latency-sensitive, offline resilience)

**Protocolos**:

- **OPC UA** (Open Platform Communications Unified Architecture): Industrial standard interoperability (vendor-neutral)
- **MQTT**: Lightweight pub/sub (IoT devices resource-constrained)
- **Modbus**: Legacy industrial (serial, TCP/IP)

**Conexión**: E7 §3 Stack (cloud platforms), E8 §4 Data (streaming ingestion)

### Digital Twin & Simulation

**Digital Twin** (gemelo digital):

- **Definición**: Réplica virtual asset físico (máquina, línea, planta) con sync bidireccional real-time
- **Componentes**:
  - **Physical Asset**: Máquina real (sensores, actuadores)
  - **Virtual Model**: CAD 3D + physics simulation + behavior models
  - **Data Connection**: Bidireccional (physical → virtual telemetry, virtual → physical control commands)
  - **Analytics**: ML models sobre twin (predict, optimize, scenario testing)

**Vendors/Tools**:

- **Siemens NX + Plant Simulation**: Diseño + simulación discreta
- **Dassault 3DEXPERIENCE**: PLM + digital twin unified
- **ANSYS Twin Builder**: Physics-based simulation (thermal, mechanical, electrical)
- **Unity3D / Unreal Engine**: Visualization immersive (VR/AR factory tours, training)

**Uso Cases**:

- **Design**: Test designs virtual antes build físico (reduce prototypes)
- **Commissioning**: Virtual commissioning línea producción (reduce downtime setup)
- **Operation**: Monitor real-time, predict failures, optimize parámetros
- **Training**: Operators entrenados en twin (safe, cost-effective)

**Conexión KERNEL**: Recurso R3 (twin como capacity virtual)

---

## §4-§9. PATRONES MANUFACTURA (8 Patterns, 240 líneas total)

### P_MFG1: Digital Twin Pattern

**Problema**: Optimización producción trial-and-error en planta real → Costoso, riesgoso, lento.

**Contexto**: Líneas producción complejas, parámetros múltiples (velocidad, temperatura, presión), optimización requiere experimentación.

**Solución**: Crear digital twin → Simulate escenarios → Optimize virtual → Apply físico.

**Implementación**:

1. **Model Física**: CAD 3D máquina/línea (geometría, kinematics)
2. **Instrumentar**: Sensores real-time (telemetry feed twin)
3. **Calibrate**: Model parameters vs datos reales (physics simulation accurate)
4. **Optimize**: Simular escenarios (what-if), algoritmos optimization (gradient descent, genetic algorithms)
5. **Apply**: Mejores parámetros → Physical asset (PLC commands)
6. **Monitor**: Resultados reales → Update model (continuous learning)

**Conexión KERNEL**:

- **Dato D1**: Telemetry streaming (signals)
- **Recurso R3**: Twin como capacity virtual
- **Flujo F2**: Optimization loop automated

**Cuándo Usar**: High-value assets, optimization ROI alto, safety-critical (test virtual primero).

**Ejemplo**: Planta química optimiza reactor temperature/pressure (twin simula 1000 combinaciones → Identifica óptimo → Yield +8%).

### P_MFG2: Predictive Maintenance Pattern

**Problema**: Reactive maintenance (fix cuando falla) → Downtime no planeado, costos altos. Preventive calendar-based → Over-maintenance (cambiar partes vida útil restante).

**Contexto**: Máquinas críticas (CNC, robots, hornos), fallos cuestan $10K-$100K/hora downtime.

**Solución**: ML models predict fallas → Mantener justo antes fallo (condition-based).

**Implementación**:

1. **Instrumentar**: Sensores vibración, temperatura, corriente, acústica
2. **Data Collection**: Time-series histórico (fallos pasados labeled)
3. **Feature Engineering**: RMS vibración, FFT spectrum, temperature trends, duty cycles
4. **Model Training**: LSTM (sequence prediction), Random Forest (classification falla/no-falla), survival analysis (RUL estimation)
5. **Deployment**: Model scoring real-time stream (Spark Streaming, Flink)
6. **Alert**: RUL <7 días → Maintenance work order automático (CMMS integration)
7. **Feedback Loop**: Fallos reales → Retrain model (continuous improvement)

**Métricas**:

- **MTBF** (Mean Time Between Failures): +30-50%
- **Maintenance cost**: -20-30% (no over-maintenance)
- **Unplanned downtime**: -40-60%

**Conexión KERNEL**:

- **P58 RAG Pattern** (análogo): Data (historical failures) → Retrieve (similar patterns) → Predict (ML inference)
- **Delegación M4-M5**: ML model predice (M4 Control), técnico decide ejecutar (M5 Co-produce)

**Ejemplo**: Compresor industrial (predict bearing failure 10 días advance, evita downtime $45K, reemplaza bearing $2K planificado).

### P_MFG3: Adaptive Supply Chain Management

**Problema**: Supply chain stático (forecast-driven) → Exceso inventario o stockouts cuando demanda volátil.

**Contexto**: Productos customizados, demand variability alta, lead times proveedores largos.

**Solución**: Supply chain adaptativa (demand sensing real-time, dynamic replenishment).

**Implementación**:

1. **Demand Sensing**: POS data, social media, weather (external signals) → ML forecast short-term (7-30 días)
2. **Inventory Optimization**: Safety stock dinámico (service level targets vs holding cost)
3. **Supplier Collaboration**: EDI/APIs real-time (proveedores ven forecast, adjust capacity)
4. **Dynamic Routing**: Logistics optimization (minimize cost, meet SLAs)

**Métricas**:

- **Inventory turns**: +20-40% (less capital tied)
- **Stockout rate**: -50% (better availability)
- **Forecast accuracy** (MAPE): 35% → 18% (ML vs statistical)

**Conexión KERNEL**:

- **Flujo F3**: Supply chain como flujo complejo multi-actor
- **E8 §5 AI**: ML forecasting (demand prediction)

**Ejemplo**: Fabricante electrónica (smartphones) - Demand sensing identifica spike (nuevo competidor falla) → Increase producción 20% proactivo → Captura market share +$15M.

### P_MFG4: Computer Vision Quality Control

**Problema**: Inspección visual manual → Subjetivo, lento, fatiga humana (defects missed).

**Contexto**: High-volume production (>100 unidades/hora), defectos visuales críticos (scratches, dents, color mismatch).

**Solución**: Computer vision automated inspection (cameras + ML).

**Implementación**:

1. **Imaging**: Cameras high-res (8MP+), iluminación controlada (túnel visión), múltiples ángulos
2. **Model**: CNN (Convolutional Neural Network) trained defects (classification, segmentation, detection)
3. **Integration**: En línea producción (real-time, <500ms latency per inspección)
4. **Action**: Defect detected → Reject automático (pneumatic ejector) o alert operator (borderline cases)
5. **Feedback**: False positives/negatives → Retrain model (active learning)

**Métricas**:

- **Defect detection rate**: 85% (human fatigue) → 99.5% (CV)
- **Inspection time**: 30s/unit → 2s/unit
- **False reject rate**: <1% (tuning threshold)

**Conexión KERNEL**:

- **Delegación M5-M6**: CV clasifica (M5 Co-produce), humano valida edge cases (M5), auto-reject clear defects (M6 Execute)
- **E8 §5 AI**: Computer vision como AI capability

**Ejemplo**: Planta automotriz pintura - CV detecta micro-scratches (human miss), rework antes ensamble final → Warranty claims -40%.

### P_MFG5: OEE Real-Time Monitoring

**OEE** (Overall Equipment Effectiveness):

```
OEE = Availability × Performance × Quality

Availability = (Operating_Time / Planned_Production_Time)
Performance = (Ideal_Cycle_Time × Total_Count / Operating_Time)
Quality = (Good_Count / Total_Count)
```

**Pattern**: Instrumentar → Calcular automático → Dashboard → Continuous improvement.

**Implementación**:

1. **Data Capture**: Downtimes (PLC signals), cycle times (counters), defects (quality system)
2. **Calculation Real-Time**: Stream processing (Spark, Flink) → OEE por máquina, línea, turno
3. **Pareto Analysis**: Top loss categories (setup time, micro-stops, speed loss, defects)
4. **Dashboards**: Andon boards (factory floor), executive dashboards (Grafana, PowerBI)
5. **PDCA**: Plan-Do-Check-Act cycles (target OEE +5 puntos/quarter)

**World-Class OEE**: >85% (availability >90%, performance >95%, quality >99%)

**Conexión KERNEL**:

- **D2_Percepción O4**: OEE como observable velocity operacional
- **A5_Medición §2**: Metrics frameworks (OEE standard manufacturing)

### P_MFG6: AGV Orchestration (Autonomous Guided Vehicles)

**Problema**: Material handling manual → Labor-intensive, errores picking, bottlenecks logística interna.

**Contexto**: Warehouses grandes, producción JIT (Just-In-Time), múltiples líneas paralelas.

**Solución**: AGVs/AMRs (Autonomous Mobile Robots) orquestados software.

**Implementación**:

1. **Fleet**: 10-50 AGVs (laser-guided, vision-guided, magnetic-guided según layout)
2. **Orchestration Software**: Fleet manager (optimiza rutas, balancea carga, evita colisiones)
3. **Integration MES**: Órdenes producción → AGV tasks automático (entregar materias primas, recoger WIP, transport finished goods)
4. **Charging**: Auto-docking estaciones carga (battery <20% → Return charge)

**Métricas**:

- **Material handling cost**: -60% (AGVs vs forklifts + operators)
- **Picking accuracy**: 99.8% (vs 97% manual)
- **Throughput**: +25% (24/7 operation, no breaks)

**Conexión KERNEL**:

- **Actor A5**: AGV como actor automated
- **Flujo F2**: Orchestration como flujo automated
- **P61 Multi-Agent**: AGV fleet coordination (análogo multi-agent)

### P_MFG7: Energy Optimization

**Problema**: Energía ~20-40% costo operacional manufactura, consumo ineficiente (máquinas idle, peaks demand).

**Contexto**: Plantas energy-intensive (fundición, química, papel), tarifas eléctricas time-of-use.

**Solución**: Monitoreo consumo real-time + optimization scheduling + demand response.

**Implementación**:

1. **Submetering**: Medidores por máquina/línea (kWh real-time)
2. **Baseline**: Energy consumption profiles (idle, normal, peak)
3. **Scheduling Optimization**: Shift cargas high-energy a off-peak hours (tarifas bajas)
4. **Demand Response**: Curtail loads en peaks (utility signals, avoid demand charges)
5. **ML Optimization**: Predict energy optimal settings (temperatura, RPM, presión) → Minimize kWh per unit produced

**Métricas**:

- **Energy cost**: -15-25% (scheduling + efficiency)
- **Carbon footprint**: -20% (renewable integration, efficiency)
- **kWh/unit**: -10% (process optimization)

**Conexión KERNEL**: Recurso R2 (energía como financial resource optimizable)

### P_MFG8: Supply Chain Visibility (Blockchain/IoT)

**Problema**: Supply chain opaco (proveedores tier-2/3 unknown), trazabilidad limitada (recalls costosos), counterfeits.

**Contexto**: Regulación estricta (farmacéutica, alimentos, automotriz), recalls ($10M-$100M costo), brand protection.

**Solución**: End-to-end visibility (IoT tracking + blockchain immutability).

**Implementación**:

1. **IoT Tracking**: RFID tags, GPS trackers, temperature sensors (cold chain)
2. **Blockchain Ledger**: Hyperledger Fabric, Ethereum private (immutable events: origin, custody transfers, inspections)
3. **Integration**: ERP, WMS, TMS (transport mgmt) write events blockchain
4. **Consumer Transparency**: QR codes productos → Scan → Ver provenance completo (origen materias primas, manufacturing steps, inspections, transport)

**Ejemplo**: Salmón chileno exportación - IoT sensors temperatura toda cold chain + blockchain eventos → Consumer app muestra: "Capturado 15-OCT, Procesado Planta X 16-OCT, Temp. -2°C mantenida, Shipped 18-OCT, Arrived EU 25-OCT" (trust, premium pricing).

**Conexión KERNEL**:

- **I3 Trazabilidad**: Blockchain operationaliza trazabilidad inmutable
- **E8 §4.5 Lineage**: Supply chain lineage (materials → products)

---

## §10. ANTIPATRONES MANUFACTURA

### AP_MFG1: Data Silos (Equipment → No Integration)

**Síntoma**: Cada máquina/sistema propio dashboard, no integración (MES, SCADA, ERP, quality isolated).

**Consecuencia**: No visibilidad holística, decisiones sub-óptimas (local optimization, global sub-optimization), manual data consolidation (Excel).

**Fix**: Unified data lake (§3), OEE dashboards consolidados, integration MES ↔ ERP ↔ SCADA (OPC UA, APIs).

**Severidad**: 🟡 Importante

### AP_MFG2: Over-Automation Premature

**Síntoma**: Automatizar proceso inestable (high variability, no standardized) → Robots/AGVs subutilizados.

**Consecuencia**: ROI bajo, flexibility loss (automation lock-in), change costly.

**Fix**: **Stabilize process first** (Lean, Six Sigma reduce variability) → THEN automate stable process.

**Severidad**: 🟡 Importante

**Conexión**: AP_TECH1 Premature Microservices (analogía)

### AP_MFG3: Ignoring Plant Floor Knowledge

**Síntoma**: Decisiones tech/process sin input operadores, tech stack desconectado realidad planta.

**Causa Raíz**: Engineers/management no escuchar front-line workers, "ivory tower" decision-making.

**Consecuencia**: 
- Resistance adoption nuevos sistemas ("no funciona en realidad")
- Workarounds manuales proliferan (sistema bypassed)
- Deployment failures (10-20% rollouts fail por usability)
- Knowledge operadores no capturado (bus factor alto)

**Fix**:
1. **Involve operators design**: Workshops co-design UX sistemas
2. **Usability testing planta**: Pilots con operadores reales antes full rollout
3. **Continuous feedback**: Canales feedback operadores → Tech team (mensual)
4. **Operator training**: Capacitación hands-on, no solo slides
5. **Incentivos adoption**: Bonos linked successful deployment

**Severidad**: 🟢 Moderado

**Conexión**: AP05 Conway Inverse Fallacy (cambiar sin entender ground truth)

---

### AP_MFG4: Vendor Lock-In OT

**Síntoma**: Single vendor ecosistema completo (PLC + SCADA + MES propietario), no interoperabilidad.

**Causa Raíz**: 
- Convenience short-term ("todo funciona junto out-of-box")
- Evitar integración complexity upfront
- Salesperson convincente (bundle deals, descuentos)

**Consecuencia**:
- **Cost switching prohibitivo**: $500K-$5M migration cost (reemplazar todo)
- **Innovation slow**: Vendor roadmap dicta innovación (no tu roadmap)
- **Pricing power vendor**: Annual maintenance +10-15% (captive customer)
- **Best-of-breed impossible**: Stuck suboptimal tools (no puedes cambiar piece)

**Fix**:
1. **Open standards adoption**: OPC UA (interoperability PLCs), MQTT (IoT)
2. **Multi-vendor strategy**: Mix vendors por capability (PLC Siemens, SCADA Ignition, MES custom)
3. **API-first architecture**: Integration layer abstract vendors
4. **Exit clauses contracts**: Data portability guarantees, no lock-in clauses
5. **Vendor evaluation**: Score vendor lock-in risk (criteria: standards support, APIs, data export)

**Severidad**: 🟡 Alto

**Conexión**: P74 Supply Chain Visibility (open standards blockchain interop)

---

### AP_MFG5: Reactive Quality Control

**Síntoma**: Inspect product final stage, scrap/rework post-facto ($10K-$100K/día waste).

**Causa Raíz**: 
- Quality as afterthought ("we’ll inspect at end")
- No process control (parameters drift unnoticed)
- Cost-cutting inspection inline (false economy)

**Consecuencia**:
- **Scrap rate 3-5%**: Producto ya fabricado, costo hundido
- **Rework cost +20% COGS**: Labor rework expensive
- **Customer complaints**: Defects escapan inspección final (1-2% slip through)
- **Root cause unknown**: No data qué step introdujo defect

**Fix**:
1. **SPC (Statistical Process Control)**: Monitor parameters real-time (control charts)
2. **In-line inspection**: Inspect cada etapa crítica (no solo final)
3. **P_MFG4 Computer Vision**: Automated inspection 100% unidades
4. **Root cause prevention**: Pareto analysis defects → Fix upstream causes
5. **Poka-yoke**: Error-proofing design (impossible fabricar incorrecto)

**Métricas Fix**:
- Scrap rate: 3-5% → <1%
- Rework cost: 20% COGS → 5% COGS
- Customer complaints: -70%

**Severidad**: 🟡 Alto

**Conexión**: P_MFG4 Computer Vision QC (mitigation pattern)

---

### AP_MFG6: Calendar-Based Maintenance Only

**Síntoma**: Cambiar partes fixed schedule (cada 6 meses), ignore condición actual asset.

**Causa Raíz**: 
- Legacy practice ("siempre lo hemos hecho así")
- No telemetry instrumentation (no visibility condition)
- Risk-averse culture ("mejor safe than sorry")

**Consecuencia**:
- **Over-maintenance +30% cost**: Cambiar bearings 60% vida útil restante
- **Under-maintenance failures**: Assets fallan antes schedule (unplanned downtime)
- **Waste partes**: Partes descartadas vida útil ($50K-$200K/yr)
- **Opportunity cost**: Maintenance windows unnecessary (producción stopped)

**Fix**:
1. **P_MFG2 Predictive Maintenance**: ML models predict RUL (Remaining Useful Life)
2. **Condition-based triggers**: Maintain when condition threshold (vibration >X, temp >Y)
3. **Telemetry sensors**: Instrumentar assets críticos (vibration, temp, oil analysis)
4. **Hybrid approach**: Calendar as backup (si telemetry fails), condition-based primary
5. **CMMS integration**: Work orders triggered condition alerts auto

**Métricas Fix**:
- Maintenance cost: -20-30%
- Unplanned downtime: -40%
- Parts waste: -60%

**Severidad**: 🟢 Moderado

**Conexión**: P_MFG2 Predictive Maintenance (direct mitigation)

---

### AP_MFG7: No Digital Twin Optimization

**Síntoma**: Trial-and-error optimization planta real → Costly ($10K-$100K/experiment), slow (semanas), riesgoso (fallas equipo).

**Causa Raíz**:
- No leverage simulation tech ("too expensive", "too complex")
- Risk-averse culture ("no tocar lo que funciona")
- Lack expertise digital twin (skill gap)

**Consecuencia**:
- **Optimization experiments limited**: Solo 2-3 tests/yr (fear disruption)
- **Yield sub-óptimo -5-10%**: Never find óptimo (parameter space unexplored)
- **Innovation slow**: Competitors digital twin optimize faster
- **Safety risk**: Experiments planta real risk equipment damage

**Fix**:
1. **P_MFG1 Digital Twin**: Build twin assets críticos (high-value, complex)
2. **Start simple**: 1 línea pilot (not entire plant), prove ROI
3. **Vendor partnerships**: Siemens Plant Simulation, ANSYS Twin Builder (managed service)
4. **Training team**: Upskill engineers simulation tools (certification programs)
5. **Simulation-driven optimization**: Test 100s scenarios virtual, apply best 3-5 real

**Métricas Fix**:
- Optimization experiments: 3/yr → 50+/yr (virtual)
- Yield improvement: +5-15% (find true optimum)
- Experiment cost: $50K/test → $500/simulation
- Time-to-optimize: 6 meses → 2 semanas

**Severidad**: 🟢 Moderado

**Conexión**: P_MFG1 Digital Twin (direct mitigation), P_MFG7 Energy Optimization (twin simulates energy)

---

## §11. MÉTRICAS MANUFACTURA

### OEE (Detailed)

**World-Class Benchmarks**:

- **OEE >85%**: Elite (automotive, pharma)
- **OEE 65-85%**: Good (majority industries)
- **OEE <65%**: Needs improvement

**Components Benchmarks**:

- **Availability >90%**: Downtime mínimo (planned + unplanned <10%)
- **Performance >95%**: Velocidad real ≈ ideal (micro-stops, speed loss <5%)
- **Quality >99%**: Defects <1% (scrap, rework minimal)

**Conexión**: A5_Medición §2 KPIs (OEE como KPI core)

### MTBF/MTTR

- **MTBF** (Mean Time Between Failures): Average time equipment operates sin falla (target >1000h)
- **MTTR** (Mean Time To Repair): Average time reparar falla (target <4h)
- **Reliability**: MTBF / (MTBF + MTTR)

**Conexión**: D2_Percepción O7 (reliability como observable)

### Cost per Unit

```
Cost_Unit = (Material_Cost + Labor_Cost + Overhead_Energy + Maintenance_Amortized) / Units_Produced
```

**Target**: Reduce 5-10% anual (efficiency gains, yield improvement, energy optimization).

---

## §12. CASO COMPLETO: Planta Automotriz Stamping

**Contexto** (15 líneas):

- Planta estampado metálico (chasis, puertas, capots)
- 8 líneas producción (presses 500-2500 ton)
- Output: 120K piezas/mes
- OEE inicial: 62% (benchmark 78% industria)

**Solución** (30 líneas):

1. **Digital Twin**: 8 líneas modeladas (Siemens Plant Simulation)
2. **Predictive Maintenance**: 24 presses instrumentadas
3. **Vision QC**: Inspección automated 100% piezas (defects visuales)
4. **Energy Optimization**: Scheduling shifts peak demand
5. **OEE Monitoring**: Real-time dashboards

**Métricas** (24 meses) (20 líneas):

- **OEE**: 62% → 83% (+34%)
- **Unplanned downtime**: 180h/mes → 45h/mes (-75%)
- **Defect rate**: 1.2% → 0.3% (- 75%)
- **Energy cost**: $2.1M/año → $1.6M/año (-24%)
- **Throughput**: 120K → 145K piezas/mes (+21%)

**H_Score**: 58 → 79 (+36%)

**ROI**: $4.5M inversión, payback 16 meses, NPV 3 años $12M.

**Conexión**: P_MFG1-8 applied, delegation M4-M6, observables O4/O7/O8.

---

## §13. COMPLIANCE & STANDARDS

- ISO 9001: SGC
- Six Sigma: DMAIC, DPMO
- ISO 45001: Safety
- ISO 14001: Ambiental

---

## §14. REFERENCIAS

- Siemens Opcenter, Rockwell FactoryTalk, AWS IoT Core, Azure IoT Hub, Siemens MindSphere (vendors)
- ISO 9001:2015, ISO 45001:2018, ISO 14001:2015 (standards)

---
