# Suntegrity ☀️🔗

**Universal Golden Record for Residential Solar Assets**  
• Live performance dashboards (Enphase)  
• Compliance & document vault (OCR)  
• kWh-token minting (ERC-1155 on Base) linked to RECs  
• Stripe-verified payment gating  
• Modular API layer for utilities, IRS, monitoring, and more

![build](https://github.com/<ORG_OR_USER>/suntegrity/actions/workflows/ci.yml/badge.svg)

---

## ✨ Features
| Module | Highlights |
|--------|------------|
| **Dashboards** | Real-time kWh vs PPA curve, PR, availability; critical Enphase alarms |
| **Repositories** | Versioned Compliance & Project Folders with OCR, expiry reminders |
| **Tokenization** | Stripe webhook → mint ERC-1155 kWh tokens on Base (includes `REC_serial`) |
| **RBAC** | Admin • Operator/Owner • Customer (plus Installer / Investor / Auditor placeholders) |
| **Notifications** | Email + SMS (Twilio) – Info • Warning • Critical |
| **Branding** | Chainlink Blue · Solar Yellow · Signal Orange · Navy Background |

---

## 🏗 Architecture

```mermaid
flowchart LR
  subgraph Frontend (React)
    A1[Admin UI] --- A2[Operator/Owner UI] --- A3[Customer Portal]
  end
  subgraph Backend (Node/TS)
    B1[REST API] --> B2[GraphQL Gateway]
    B2 --> DB[(PostgreSQL)]
    B2 --> IPFS[(IPFS / S3 Docs)]
    B2 --> Enphase[Enphase API]
    B2 --> Stripe[Stripe Webhooks]
    B2 --> Base[Base L2 | ERC-1155]
    B2 --> Twilio[Twilio SMS]
  end
  A1 ~~> B1
  A2 ~~> B1
  A3 ~~> B1
