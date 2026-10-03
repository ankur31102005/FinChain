# FinChain — AI-Enhanced Blockchain Financial Services Platform

> **Secure, Transparent and Intelligent Financial Services using Blockchain, DeFi and AI**
>
> B.Tech AI & Machine Learning capstone project · Academic simulation only

---

## Abstract

FinChain is a simulated blockchain-based financial services platform that demonstrates how modern
fintech combines **blockchain architecture, decentralized finance (DeFi), central bank digital
currency (CBDC), regulatory compliance (KYC/AML) and artificial intelligence** in one working
system. Users open wallets, send transactions that are recorded on a real SHA-256 hash-linked
blockchain, borrow and lend through DeFi smart-contract simulations, trade tokenized real-world
assets, and are continuously monitored by a **Random Forest fraud-detection model** and a rule
based AML engine. The project is built in pure Python (FastAPI + SQLAlchemy + scikit-learn) with
a professional Bootstrap 5 dashboard.

## Problem Statement

Traditional financial systems suffer from (a) opaque, siloed ledgers, (b) slow multi-intermediary
settlement, (c) slow and manual compliance checks, and (d) rising digital fraud. Students and
engineers therefore need hands-on understanding of how blockchain, DeFi, CBDC and AI jointly
address these pain points — without touching real money or real banking rails.

## Objectives

1. Implement a working educational blockchain (blocks, SHA-256 hashing, hash links, validators).
2. Demonstrate immutability live: tamper a sealed block → integrity breaks → restore.
3. Simulate financial services: wallets, transfers, deposits, loans, DeFi pools.
4. Tokenize real-world assets with fractional ownership.
5. Simulate CBDC issuance and cross-border blockchain settlement.
6. Detect fraud with a trained Random Forest classifier and explainable AML rules.
7. Compare consensus mechanisms (PoW / PoS / PoA) and benchmark scalability.

## Features

| Area | What you can demo |
|---|---|
| Authentication | JWT login, bcrypt password hashing, 3 roles (customer / admin / central bank) |
| Wallet | FC-prefixed demo addresses, balance, deposit, send, receive |
| Transactions | 9 types (transfer, deposit, withdrawal, loan, DeFi, token, CBDC, cross-border, insurance) — every tx is fraud-scored, AML-scanned and mined into a block |
| Blockchain Explorer | Block cards with hashes, validator, tx list; click to inspect |
| Tampering demo | Modify a sealed tx → ❌ INTEGRITY COMPROMISED → restore → ✓ VALID |
| Consensus | PoW mining playground, PoS weighted demo, PoA (used by the chain), comparison table |
| DeFi | Liquidity pool, 8% APY deposits, 60% LTV borrowing, repay, utilization chart |
| Loans | Collateral-backed loans, auto-approval rules, repayment, collateral release, liquidation demo |
| Tokenization | Real estate / gold / bonds / invoices, fractional buy & sell, ownership % |
| Smart contracts | Lending, Tokenization, Insurance, CBDC contracts with rules + execution logs |
| Insurance | Parametric travel policy: buy ₹500 → claim FLIGHT_CANCELLED → instant ₹50,000 payout |
| KYC | Demo-data submission, admin approve/reject workflow |
| AML | HIGH_VALUE / REVIEW / RAPID_FIRE / STRUCTURING rules, alert queue, resolve |
| AI Fraud | Random Forest (trained on 4,000 synthetic txs, joblib-persisted), what-if analyzer with probability meter and reasons |
| CBDC | Central bank issues e₹, user transfers, circulation stats |
| Cross-border | India→USA corridor: traditional vs blockchain fee/speed comparison |
| Analytics | 7 live Chart.js charts + scalability benchmark (TPS) |
| Security Lab | SHA-256 avalanche demo, digital signature demo, JWT inspector |

## Architecture

```
                 Web Browser (Bootstrap 5 + Chart.js)
                              │
                          FastAPI
                              │
        ┌─────────────────────┼─────────────────────┐
        ▼                     ▼                     ▼
  Financial Services    Blockchain Engine      AI/ML Engine
  (tx, loans, DeFi,     (Block, Chain,         (Random Forest,
   assets, CBDC,         Wallet, PoA            fraud_model.py,
   KYC, AML)             consensus)             joblib)
        └─────────────────────┼─────────────────────┘
                              ▼
                        SQLAlchemy ORM
                              ▼
                    SQLite (PostgreSQL-ready)
```

## Technology Stack

- **Python 3.11+** (tested on 3.13/3.14)
- **FastAPI + Uvicorn** — REST API + Jinja2 server-rendered pages
- **SQLAlchemy 2** — ORM, SQLite file DB (swap `FINCHAIN_DATABASE_URL` for PostgreSQL)
- **Passlib/bcrypt + python-jose** — password hashing and JWT
- **hashlib (SHA-256)** — pure-Python blockchain, no external chain
- **scikit-learn, pandas, NumPy, joblib** — fraud model
- **Bootstrap 5, Chart.js, Bootstrap Icons** — frontend

## Installation (3 commands)

```bash
python -m venv venv
venv\Scripts\activate          # Windows   (Linux/Mac: source venv/bin/activate)
pip install -r requirements.txt
```

## Database setup

None! Tables are created automatically and demo data seeds itself on first run
(or run `python seed_data.py` to force a fresh dataset).

## How to run

```bash
python run.py
# or: uvicorn app.main:app --reload
```

Open **http://127.0.0.1:8000** — interactive API docs at `/docs`.

## Demo credentials

| Role | Login | Password |
|---|---|---|
| Customer | `customer@finchain.demo` | `Demo@123` |
| Admin / Compliance | `admin@finchain.demo` | `Admin@123` |
| Central Bank | `centralbank@finchain.demo` | `CBDC@123` |

## API documentation

Full interactive Swagger UI: **http://127.0.0.1:8000/docs**

Key endpoints:

```
POST /api/auth/register        POST /api/auth/login          GET  /api/dashboard
POST /api/transactions         POST /api/transactions/deposit
GET  /api/blockchain           POST /api/blockchain/validate
POST /api/blockchain/tamper    POST /api/blockchain/restore  GET  /api/blockchain/consensus
POST /api/defi/deposit         POST /api/defi/borrow         POST /api/defi/repay
POST /api/loans                POST /api/loans/{id}/repay
GET  /api/assets               POST /api/assets/tokenize     POST /api/assets/{id}/buy
POST /api/kyc                  PUT  /api/kyc/{id}            GET  /api/aml/alerts
POST /api/fraud/analyze        POST /api/cbdc/issue          POST /api/cbdc/transfer
POST /api/cbdc/crossborder/send                              GET  /api/analytics/overview
```

## Screenshots

Run the app and capture: ① login page ② dashboard ③ blockchain explorer with the
integrity banner ④ tamper modal + compromised state ⑤ AI fraud analyzer ⑥ analytics.

## Limitations

- Single-node simulation; no peer-to-peer network.
- PoA validator rotation is round-robin, not Byzantine-fault-tolerant.
- Digital signatures are hash-based demos, not ECDSA.
- FX rates and interest maths are simplified for clarity.
- SQLite is used for zero-config setup; not for production concurrency.

## Future scope

- ECDSA (secp256k1) signatures via the `ecdsa`/`coincurve` libraries
- Multi-node chain gossip and real BFT consensus
- PostgreSQL + Alembic migrations
- Hyperledger Fabric or Ethereum testnet integration layer
- Live fraud model retraining pipeline and SHAP explainability
- UPI/NEFT-style rail simulations and ISO 20022 message formats

## Academic disclaimer

This platform is built **solely for educational assessment**. It uses fake data, fake wallets,
fake KYC documents and simulated currency. It is **not** connected to RBI, SWIFT, banks,
payment gateways or any cryptocurrency network, and must not be used for real financial activity.

## Testing

```bash
venv\Scripts\python -m pytest tests/ -q
# 48 passed
```

Covers: auth, RBAC, transactions, insufficient balance, AML triggers, blockchain validation,
tampering, restore, wallets, DeFi LTV rules, loans, KYC workflow, fraud model behaviour,
CBDC role restrictions, tokenization, insurance claims, consensus info.
"# FinChain" 
