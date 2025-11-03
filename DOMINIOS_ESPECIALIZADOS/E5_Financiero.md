# E5_Sector_Financiero (Fintech & Trading Systems)

**Versión:** 2.0.0  
**Estado:** Production  
**Audiencia:** CIOs Financieros, Arquitectos Core Banking, Quants, Risk Managers, Compliance Officers  
**Dependencias**: CORE/01-08, DOMINIOS/D1-D4, APLICACION/A1-A5, E7-E8

---

## §0. QUICK START MVF (Minimum Viable Fintech)

### Checklist MVF (Fintech Startup, 6 meses)

**1. Core Banking Básico** (Mes 1-3):

- ✅ Cuentas (savings, checking), transacciones (deposits, withdrawals, transfers)
- ✅ KYC/AML automated (identity verification, sanctions screening, PEP checks)
- ✅ Ledger double-entry (accounting reconciliation diaria)

**2. Compliance & Security** (Mes 2-4):

- ✅ SOX controls (segregation duties, audit trails immutable)
- ✅ Encryption: TLS 1.3 (in-transit), AES-256 (at-rest)
- ✅ PCI DSS (si pagos tarjeta): Tokenización, no store CVV

**3. Fraud Detection Real-Time** (Mes 4-6):

- ✅ Rules engine (velocity checks, geolocation anomalies, amount thresholds)
- ✅ ML model (behavioral scoring, transaction patterns)
- ✅ Case management (alertas investigador fraude, HITL decisiones)

**Resultado MVF**:

- **Fraud detection rate**: 75% (rules) → 92% (rules + ML)
- **False positives**: 8% → 3% (ML precision)
- **Compliance**: SOX/AML audit passed

**Conexión KERNEL**: P60 HITL (fraud cases high-stakes)

---

## §1. OVERVIEW SECTOR + REGULACIÓN

### Financiero Chile

**Sectores**:

- **Banca**: 18 bancos (Santander, BCI, Banco Chile líderes), activos $400B USD
- **Seguros**: Vida, generales, salud (ISAPREs)
- **AFPs**: Pensiones (capitalización individual)
- **Valores**: Bolsa Santiago, corredoras, AGFs (Administradoras Generales de Fondos)
- **Fintech**: Pagos digitales (Mercado Pago, Mach, Tenpo), lending (Cumplo, Becual), crypto (Buda, Orionx)

**Desafíos**:

- Legacy systems (COBOL mainframes 60-70% core banking)
- Open banking mandato (API abiertas, portabilidad clientes)
- Real-time payments (24/7, <10s settlement)
- AML/CFT compliance (lavado, financiamiento terrorismo) - costos altos

### Regulación Financiera

**Basilea III** (Capital Requirements):

- **Tier 1 Capital Ratio**: >6% (core equity)
- **Total Capital Ratio**: >10.5%
- **Leverage Ratio**: >3%
- **Liquidity Coverage Ratio (LCR)**: >100% (survive 30-day stress)

**SOX** (Sarbanes-Oxley, US):

- **Section 302**: CEO/CFO certify financial statements accuracy
- **Section 404**: Internal controls evaluation (COSO framework)
- **Section 802**: Audit trails immutable, retention 7 años
- **Aplicable**: Bancos chilenos listados NYSE, filiales US

**MiFID II** (EU Markets in Financial Instruments):

- Transparency, best execution, transaction reporting
- **Aplicable**: Banks operaciones EU

**Dodd-Frank** (US Financial Reform):

- Volcker Rule (proprietary trading restrictions), stress tests, living wills
- **Aplicable**: Subsidiaries US

**Chile-Specific**:

- **CMF** (Comisión Mercado Financiero): Supervisor bancos, seguros, valores
- **Ley General Bancos**: Capital mínimo, provisiones, límites exposición
- **SBIF** (ex-supervisor, absorbed por CMF 2019): Recopilación Información Financiera (RIF)

**Conexión KERNEL**: Límite L3 (regulatory más complejo, penalties severos $1M-$100M)

---

## §2. MAPEO PRIMITIVOS

| Primitivo | Manifestación Financiera | Ejemplo Trading Desk |
|:---|:---|:---|
| **Recurso** | Capital, liquidez, colateral, sistemas trading, datos market | Capital trading $50M (R2 Financial), Bloomberg Terminal (R3 Platform), Market data feeds (R1 Information) |
| **Flujo** | Trade lifecycle (order → execute → settle → clear), payment flows, loan origination | FX trade: Order → Match → Confirm → Settle T+2 (F2 Automated), Wire transfer (F1 Manual approval >$1M) |
| **Actor** | Traders, risk managers, compliance officers, clients, counterparties, exchanges | Trader (A3 Specialized), Risk Manager (A3), Algorithmic trading bot (A5 Automated) |
| **Señal** | Market data (prices, volumes), credit events, regulatory filings, alerts fraud | EUR/USD tick 1.0850 (S2 Digital real-time), Credit downgrade (S1 Natural event), Fraud alert score >0.95 (S2 Digital) |
| **Dato** | Transacciones, posiciones, P&L, market data, customer data (KYC), risk metrics | Transaction ID #789 (D2 Structured), VaR $2.5M (D2 Calculated), Trade tape ITCH 5.0 (D1 Signal binary) |
| **Límite** | Capital ratios, risk limits (VaR, stress loss), position limits, compliance (AML), SLAs clients | VaR daily <$5M (L1 Performance), Tier 1 >8% (L3 Regulatory), Trade execution <50ms p95 (L1 Performance) |

---

## §3. STACK TECNOLÓGICO FINANCIERO

### Core Banking & Payments

**Core Banking**: Temenos (T24/Transact), FIS (Profile, Horizon), Oracle FLEXCUBE  
**Payments**: FIS (PayNet), ACI Worldwide, SWIFT network (cross-border)  
**Cards**: First Data, TSYS (card issuing/processing)

**Chile**: Transbank (acquirer líder), Redcompra (ATM network), TEF (Transferencia Electrónica Fondos)

### Trading Systems

**Execution Platforms**:

- **FIX Protocol** (Financial Information eXchange): Industry standard order routing (low-latency binary)
- **Bloomberg Terminal**: Market data + analytics + trading ($24K/user/año)
- **MetaTrader 4/5**: Retail forex/CFD trading
- **NinjaTrader**: Futures trading (C# automation)

**Order Management** (OMS):

- **Charles River** (State Street): Multi-asset OMS
- **Bloomberg AIM**: Asset/Investment Manager

**Risk Engines**:

- **Numerix**: Derivatives pricing, risk analytics (Monte Carlo, Greeks)
- **Murex**: Cross-asset trading + risk platform

**Low-Latency** (HFT - High-Frequency Trading):

- **Latency targets**: <1ms exchange co-location, <10μs FPGA-based
- **Tech**: C++, FPGA (field-programmable gate arrays), kernel bypass networking (DPDK)

---

## §4-§9. PATRONES FINANCIEROS (8 Patterns)

### P_FIN1: Fraud Detection Real-Time

**Problema**: Fraud post-facto detection → Losses $500K-$5M/año, customer trust loss.

**Solución**: Real-time scoring (rules + ML) → Block suspicious, alert investigator.

**Implementación**:

1. **Rules Engine**: Velocity (>5 transactions 10min), geolocation (IP Russia, card Chile), amount (>3× baseline)
2. **ML Model**: Behavioral features (time-of-day, merchant category, spend patterns) → XGBoost binary classification fraud/legit
3. **Scoring Real-Time**: Transaction stream (Kafka) → Score <100ms → Decision (approve, decline, HITL review)
4. **Case Management**: Alerts score >0.95 → Investigador review (call customer, freeze card)
5. **Feedback**: Confirmed frauds → Retrain model weekly

**Métricas**: Detection rate 92%, False positive 3%, Fraud losses -70%.

**Conexión**: P60 HITL (high-value HITL investigator), E8 §5 ML (real-time scoring)

### P_FIN2: Rigorous Backtesting (Trading Strategies)

**Problema**: Strategies optimized in-sample → Overfit, fail out-sample (production losses).

**Solución**: Backtest riguroso (walk-forward, out-of-sample validation, realistic slippage/commissions).

**Implementación**:

1. **Data Clean**: Historical prices, dividends, splits adjusted
2. **Walk-Forward**: Train window (2 años) → Test window (6 meses) → Slide → Repeat (no look-ahead bias)
3. **Realistic Costs**: Slippage (2-5 bps), commissions, market impact (large orders)
4. **Risk Metrics**: Sharpe Ratio, Max Drawdown, Calmar Ratio, Win Rate
5. **Stress Test**: 2008 crisis, flash crashes (strategy survives extremes?)
6. **Paper Trading**: Live market data, simulated execution (3-6 meses validate)
7. **Production**: Gradual capital allocation ($100K → $1M → $10M si metrics hold)

**Métricas**: Sharpe >1.5 (backtest) → 1.2 (production) acceptable degradation <20%.

**Conexión KERNEL**: A5_Medición §6 Backtesting (validation rigorous)

### P_FIN3: Algo Trading Adaptive

**Problema**: Static algo trading strategies → Regime changes (volatility spikes, correlations break) → Losses $500K-$5M drawdowns.

**Contexto**: Market regimes shift (bull, bear, high-vol, low-vol), strategies perform differently per regime, need adaptability real-time.

**Solución**: Regime detection + adaptive parameters.

**Implementación**:
1. **Regime Detection**: HMM (Hidden Markov Models), clustering (vol/correlation) → Classify regime (bull-low-vol, bear-high-vol, sideways)
2. **Strategy Bank**: Multiple strategies tuned per regime (mean-reversion low-vol, trend-following high-vol)
3. **Dynamic Allocation**: Regime detected → Allocate capital strategies optimal regime, reduce exposure sub-optimal
4. **Risk Controls**: Per-regime stop-loss, position limits adaptive

**Métricas**: Sharpe 1.2 (static) → 1.8 (adaptive), Max drawdown 18% → 12%, Crisis 2020 outperform benchmark +15%.

**Conexión**: E8 §5 AI (regime detection ML), P_FIN2 Backtesting (validate per regime)

---

### P_FIN4: Compliance Automation

**Problema**: Compliance manual (SOX, MiFID, Dodd-Frank) → Cost $500K-$5M/yr, errors audit findings, regulatory penalties $1M-$100M.

**Contexto**: Regulated financial (banks, brokers, asset managers), multiple jurisdictions, audit trails mandatory, reporting deadlines strict.

**Solución**: Automated compliance checks + reporting.

**Implementación**:
1. **Audit Trail Immutable**: Blockchain/append-only log (tamper-proof, retention 7 yr)
2. **Automated Checks**: Trade surveillance (wash trades, insider trading patterns → Alert compliance)
3. **Reporting Automated**: Regulatory filings (MiFID II transaction reporting → Generate+submit auto)
4. **Policy Enforcement**: Pre-trade checks (position limits, restricted securities → Block violating trades)
5. **Continuous Monitoring**: KPIs compliance (audit findings, policy violations → Dashboard executive)

**Métricas**: Compliance cost -40% ($3M→$1.8M/yr), Audit findings 12→2, Reporting time 80h→12h/mo, Penalties $0.

**Conexión**: P_SEC03 Security as Code (compliance as code), AP_FIN4 Compliance Reactive (antipattern)

---

### P_FIN5: KYC/AML Automation

**Problema**: KYC/AML manual → Onboarding 5-10 días, cost $50-$100/cliente, errors false positives/negatives, regulatory fines $1M-$100M.

**Contexto**: Regulated financial, customer onboarding high-volume, AML/CFT compliance mandatory (FATF, FinCEN), sanctions screening required.

**Solución**: Automated identity verification + risk scoring.

**Implementación**:
1. **Identity Verification**: OCR document scan (passport/ID), liveness detection (selfie video), database cross-check (government registries)
2. **Sanctions Screening**: Check OFAC, UN, EU sanctions lists real-time
3. **PEP Check**: Politically Exposed Persons databases
4. **Risk Scoring**: ML model (behavioral + demographic features → Risk 0-1: low/medium/high)
5. **Enhanced Due Diligence**: High-risk → Manual review KYC analyst
6. **Continuous Monitoring**: Transaction monitoring (patterns suspicious → Alert AML officer)

**Métricas**: Onboarding time 10d→15min, Cost $80→$5/cliente, False positives 15%→3%, AML fines $0, Customer satisfaction +45%.

**Conexión**: P_FIN1 Fraud Detection (similar ML scoring), Vendors: Onfido, Jumio, Trulioo

---

### P_FIN6: Portfolio Optimization

**Problema**: Manual portfolio construction → Suboptimal risk/return, rebalancing infrequent (quarterly), no constraint handling (ESG, sector limits).

**Contexto**: Asset management (mutual funds, ETFs, wealth mgmt), multiple assets (50-500), constraints complex (risk budgets, ESG scores, sector exposure), need rebalancing dynamic.

**Solución**: Quantitative optimization + constraints.

**Implementación**:
1. **Mean-Variance Optimization**: Markowitz efficient frontier, maximize Sharpe given risk tolerance
2. **Constraints**: Sector limits, ESG minimum scores, turnover limits reduce transaction costs
3. **Black-Litterman**: Combine market equilibrium + manager views
4. **Risk Parity**: Allocate per risk contribution, not capital
5. **Rebalancing Dynamic**: Threshold-based (drift >5% → Rebalance) or calendar-based monthly
6. **Backtesting**: Validate optimization historical data, stress test

**Métricas**: Sharpe 0.8 (manual) → 1.2 (optimized), Rebalancing cost -40%, ESG compliance 100%, Client retention +25%.

**Conexión**: P_FIN2 Backtesting (validate optimization), Libraries: cvxpy (Python convex optimization)

---

### P_FIN7: Market Making

**Problema**: Illiquid markets → Wide bid-ask spreads (5-10%), low volumes, price discovery poor.

**Contexto**: Market maker (broker-dealer, exchange), obligation provide liquidity, inventory risk (hold positions), adverse selection risk (informed traders).

**Solución**: Automated market making (AMM) algorithmic.

**Implementación**:
1. **Quote Management**: Post bid/ask quotes continuously, spread optimal (wide enough profit, narrow enough competitive)
2. **Inventory Management**: Target inventory neutral, skew quotes reduce inventory (long → Lower ask, higher bid)
3. **Risk Controls**: Max position limits, stop-loss inventory extremes
4. **Adverse Selection Mitigation**: Detect informed flow → Widen spreads or pause quoting
5. **Order Flow Internalization**: Match client orders internally, reduce exchange fees

**Métricas**: Bid-ask spread 10%→2%, Daily volume +300%, Inventory turnover 5x/day, P&L volatility -40%.

**Conexión**: P_FIN8 HFT (AMM requiere low-latency), FIX Protocol order management

---

### P_FIN8: High-Frequency Trading (HFT)

**Problema**: Latency >10ms → Miss arbitrage opportunities ($10K-$100K/day), adverse selection (frontrun by faster HFTs).

**Contexto**: HFT strategies (statistical arbitrage, latency arbitrage, market making), microsecond competition, co-location exchange, capital >$10M.

**Solución**: Ultra-low-latency tech stack.

**Implementación**:
1. **Co-location**: Servers exchange datacenter (latency <500μs exchange)
2. **Kernel Bypass Networking**: DPDK, Solarflare OpenOnload (avoid OS overhead)
3. **FPGA**: Field-programmable gate arrays (logic hardware <10μs)
4. **C++ Optimized**: Cache-friendly, lock-free data structures, profiling ns-level
5. **Direct Market Access**: FIX binary FIX/FAST (no broker intermediation)
6. **Timestamp Precision**: Nanosecond clocks, sync PTP Precision Time Protocol

**Métricas**: Latency 10ms→100μs (-99%), Arb opportunities captured +400%, Daily P&L $50K→$200K, Sharpe 3.5 (vs 1.8 pre-HFT).

**Conexión**: P_FIN7 Market Making (HFT tech apply), E7 §3 Stack (low-latency infrastructure), FPGA vendors: Xilinx, Intel

---

## §10. ANTIPATRONES

### AP_FIN1: Overfitting Backtest

**Síntoma**: Strategy Sharpe 2.5 backtest → 0.3 production (collapse), in-sample perfect, out-of-sample disaster.

**Causa Raíz**: 
- In-sample optimization sin out-of-sample validation (optimize parameters hasta perfection backtest data)
- Look-ahead bias (use future data train model)
- Survivorship bias (only stocks survived, ignore delisted)

**Consecuencia**:
- **Losses $100K-$10M**: Strategy fail production (capital lost)
- **Strategy abandoned**: 6-12 meses development waste
- **Reputation damage**: Investors lose trust ("you tested this?")
- **Regulatory scrutiny**: SEC questions risk management

**Fix**:
1. **P_FIN2 Rigorous Backtesting**: Walk-forward (train → test → slide → repeat)
2. **Out-of-sample validation**: Reserve 30% data never touch training
3. **Cross-validation**: K-fold cross-validation (k=5 typical)
4. **Realistic costs**: Model slippage 2-5 bps, commissions, market impact
5. **Paper trading**: 3-6 meses live market data, simulated execution (validate before capital)
6. **Simplicity bias**: Fewer parameters better (Occam's razor, avoid 20-parameter strategies)

**Métricas Fix**:
- Backtest-to-production degradation: <30% (Sharpe, Drawdown)
- Overfitting avoided: Out-of-sample validation mandatory
- Production losses: <backtest worst-case

**Severidad**: 🔴 Crítico

**Conexión**: P_FIN2 Rigorous Backtesting (direct mitigation), A5_Medición §6 Validation

---

### AP_FIN2: Ignoring Slippage

**Síntoma**: Backtest assume fills at mid-price, reality slippage 5-10 bps → Profitability illusion.

**Causa Raíz**: 
- Simplified assumptions ("assume instant fills mid-price")
- No market impact modeling (large orders move price)
- Ignore bid-ask spread (1-5 bps typical, 10-50 bps illiquid)

**Consecuencia**:
- **Backtest Sharpe 2.0 → Production 0.5**: Profitability disappears transaction costs
- **Strategy unprofitable**: Gross alpha 10 bps, net alpha -5 bps (after slippage)
- **Capital wasted**: Deploy $10M strategy, lose $500K/yr slippage
- **Over-trading**: High-frequency strategy not viable (slippage kills)

**Fix**:
1. **Model slippage realistic**: 2-5 bps typical, 5-10 bps large orders, 10-50 bps illiquid
2. **Market impact**: Square-root model (impact ∝ √(order_size / ADV))
3. **Bid-ask spread**: Model spread explicit (1 bps liquid, 5-10 bps normal, 50+ bps illiquid)
4. **Commissions**: Include exchange fees, broker commissions ($0.001-$0.005/share)
5. **P_FIN2 Backtesting**: Realistic costs mandatory (not optional)

**Métricas Fix**:
- Backtest includes slippage: 100% strategies (mandatory)
- Production vs backtest Sharpe: <30% degradation (acceptable)
- Slippage tracking: Monitor actual vs modeled (continuous improvement)

**Severidad**: 🟡 Alto

**Conexión**: P_FIN2 Rigorous Backtesting (model costs), AP_FIN1 Overfitting (related)

---

### AP_FIN3: No Risk Limits

**Síntoma**: Trader rogue positions unlimited, concentration risk 100% portfolio single asset → Catastrophic losses.

**Causa Raíz**: 
- Trust-based risk management ("trader X is experienced, no need limits")
- No automated controls (manual monitoring insufficient)
- Culture "make money, don't ask how" (incentives misaligned)

**Consecuencia**:
- **Catastrophic losses $1B-$5B**: Société Générale 2008 ($4.9B), UBS 2011 ($2.3B), Barings 1995 (bankruptcy)
- **Reputation destruction**: Firm name synonymous fraud/incompetence
- **Regulatory penalties**: $100M-$1B fines, licenses revoked
- **Systemic risk**: Large losses destabilize markets (flash crash risk)

**Fix**:
1. **Automated pre-trade checks**: Position limits ($10M max single position), sector concentration (<20% portfolio), VaR daily (<$1M 95% confidence)
2. **Stop-loss mandatory**: Max loss per position ($50K-$500K), per day ($1M-$10M), per month
3. **Real-time monitoring**: Alerts breaches (email, SMS, dashboard red), escalation CEO >$5M loss
4. **Segregation duties**: Trader execute, risk manager approve large positions, compliance audit trails
5. **Circuit breakers**: Auto-liquidate positions breach limits (no override without 2-person approval)

**Métricas Fix**:
- Risk limit breaches: 0 (automated controls)
- Max daily loss: <$1M (vs $100M+ rogue trader)
- VaR monitoring: Real-time (not end-of-day)
- Compliance violations: 0

**Severidad**: 🔴 Crítico

**Conexión**: P_FIN1 Fraud Detection (real-time monitoring), Regulatory mandates (Basel III, Dodd-Frank)

---

### AP_FIN4: Compliance Reactive

**Síntoma**: Audit findings → Scramble fix post-facto, penalties frequent, manual processes error-prone.

**Causa Raíz**: 
- Compliance afterthought ("deal with it when auditor comes")
- Manual processes (Excel spreadsheets, email trails, no automation)
- Siloed compliance (no integration trading systems)

**Consecuencia**:
- **Regulatory fines $1M-$100M**: SEC, FINRA, MiFID II violations (insider trading missed, wash trades not detected)
- **Audit findings 10-20/yr**: Repeated findings same issues (no systematic fix)
- **Reputation damage**: Regulatory actions public (media coverage, client trust loss)
- **Competitive disadvantage**: Compliance cost 2-3× competitors (manual vs automated)

**Fix**:
1. **P_FIN4 Compliance Automation**: Automated checks (trade surveillance, wash trades, insider patterns), immutable audit trails (blockchain/append-only)
2. **Proactive monitoring**: Real-time alerts (suspicious patterns detected, not quarterly review)
3. **Integration trading systems**: Compliance checks embedded workflow (pre-trade blocks, not post-trade cleanup)
4. **Continuous testing**: Compliance KPIs dashboard (audit findings, policy violations, training completion)
5. **Regulatory technology (RegTech)**: Vendors Actimize, NICE Actimize (trade surveillance), ComplyAdvantage (sanctions screening)

**Métricas Fix**:
- Compliance cost: -30-50% (automation reduces manual labor)
- Audit findings: 10-20/yr → 0-2/yr
- Regulatory penalties: $10M/yr → $0
- Time-to-report: 80h/mo → 12h/mo (automated)

**Severidad**: 🟡 Alto

**Conexión**: P_FIN4 Compliance Automation (direct mitigation), P_SEC03 Security as Code (analogous)

---

### AP_FIN5: Legacy No Modernize

**Síntoma**: COBOL mainframes 60-70% core banking, innovation impossible, talent scarce (avg age 55+), cost maintenance escalating.

**Causa Raíz**: 
- "If it works, don't touch it" mentality (fear break production)
- Migration fear (risk downtime, data loss, cost $50M-$500M)
- Technical debt accumulated 30-40 years (no documentation, spaghetti code)

**Consecuencia**:
- **Innovation slow**: Competitors fintech launch features 10x faster (mobile banking, APIs, real-time payments)
- **Talent attraction impossible**: Millennials/Gen-Z refuse learn COBOL ("career dead-end")
- **Cost maintenance escalating**: COBOL developers $150-$300/hr (scarcity premium), offshore impossible (knowledge tribal)
- **Regulatory risk**: Cannot comply new regulations (real-time reporting, API mandates)
- **Systemic fragility**: Single points failure (1-2 people understand critical systems)

**Fix**:
1. **P21 Strangler Fig**: Incremental migration (not big-bang), new features modern stack, legacy wrapped APIs
2. **API layer wrap legacy**: REST APIs abstract COBOL (isolate complexity, enable innovation)
3. **Gradual replacement**: Replace module-by-module (payments → accounts → loans), 3-5 years roadmap
4. **Dual-run period**: New + legacy parallel 6-12 meses (validate correctness, rollback safety)
5. **Knowledge capture**: Document tribal knowledge (before experts retire), train new team
6. **Cloud migration**: Lift-and-shift legacy cloud (AWS Mainframe Modernization, Azure Mainframe), THEN modernize

**Métricas Fix**:
- Time-to-market features: 12 meses → 2 meses
- Talent attraction: CV applications +300% (modern stack)
- Maintenance cost: Stable (not escalating 10%/yr)
- Innovation velocity: Feature releases 4/yr → 24/yr
- Technical debt: Decrease 10%/yr (vs increase 15%/yr)

**Severidad**: 🟡 Alto

**Conexión**: P21 Strangler Fig (direct mitigation), AP15 Big Bang Rewrite (avoid), E7 §10 Legacy Modernization

---

## §11. MÉTRICAS FINANCIERAS

- **Sharpe Ratio**: (Return - RiskFree) / StdDev (target >1.0, excellent >2.0)
- **Order-to-Trade Latency**: p95 <50ms (retail), <1ms (institutional HFT)
- **False Positive Rate** (fraud): <5% (user friction vs security)
- **VaR** (Value at Risk): 95% confidence, 1-day (typical $1M-$10M trading desk)
- **Compliance Cost**: $500K-$5M/año (AML, SOX, reporting), automation reduce 30-50%

---

## §12. CASO: Robo-Advising Platform

**Contexto**: Startup robo-advisor (inversión automatizada, low-fee).

**Solución**: ML portfolio construction + compliance automated + self-service UX.

**Métricas** (24 meses):

- **AUM** (Assets Under Mgmt): $0 → $50M
- **Cost gestión**: 1.2% tradicional → 0.25% robo (-80%)
- **Client base**: 0 → 5,000 (+500%)

**H_Score**: N/A (startup) → 74 (good)

**ROI**: Break-even M18.

---

## §13-§14. COMPLIANCE & REFERENCIAS

**Regulación**: Basilea III, SOX, MiFID II, Dodd-Frank, CMF Chile.  
**Tech**: FIX, Bloomberg, Numerix, Murex, Kafka (streaming), TimescaleDB (time-series).

---
