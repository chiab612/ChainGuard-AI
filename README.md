# ChainGuard-AI
AI-powered DeFi security scanner — detect rug pulls, flag suspicious wallets, and generate audit-trail reports stored on AWS.

# ⛨ ChainGuard AI

> AI-powered DeFi security scanner — detect rug pulls, flag suspicious wallets, and generate audit-trail reports stored on AWS.

![Risk Score](https://img.shields.io/badge/Risk%20Scanner-Live-red?style=flat-square)
![AWS](https://img.shields.io/badge/AWS-Bedrock%20%7C%20DynamoDB%20%7C%20Lambda-orange?style=flat-square&logo=amazon-aws)
![Hackathon](https://img.shields.io/badge/H0%3A%20Hack%20the%20Zero%20Stack-2026-blue?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)

---

## What is ChainGuard AI?

ChainGuard AI lets anyone scan a smart contract or wallet address and get an instant AI-generated risk report — no coding knowledge required. In 3 seconds you know:

- Whether a contract has rug pull vectors (unlocked liquidity, unrestricted mint)
- Whether a wallet has been linked to known scam addresses
- A full audit trail stored permanently on AWS DynamoDB

Built for the **H0: Hack the Zero Stack** hackathon using Vercel v0 (frontend) + AWS (backend).

---

## Demo

![ChainGuard AI Dashboard](./assets/demo-screenshot.png)

---

## Architecture

```
User Input (contract / wallet address)
        │
        ▼
 Vercel v0 Frontend
 (Dashboard UI)
        │
        ▼
 AWS API Gateway → Lambda
        │
        ├──────────────────────┐
        ▼                      ▼
Amazon Bedrock          Blockchain APIs
(AI Risk Analysis)    (Etherscan / Sui)
        │                      │
        └──────────┬───────────┘
                   ▼
           AWS DynamoDB
       (Risk report + audit trail)
```

---

## Features

| Feature | Description |
|---|---|
| **Contract risk scan** | Detects rug pull patterns, mint abuse, unlocked liquidity, proxy upgrade risks |
| **Wallet analysis** | Tracks transaction history, flags links to known scam addresses |
| **AI-generated report** | Amazon Bedrock (Claude / Nova) produces a plain-language risk summary |
| **Permanent audit trail** | Every scan is stored in AWS DynamoDB — tamper-proof record |
| **PDF export** | Download a shareable report for any contract or wallet |

---

## Tech Stack

### Frontend
- **Vercel v0** — AI-generated dashboard UI
- HTML / CSS / JavaScript

### Backend (AWS)
| Service | Role |
|---|---|
| **Amazon Bedrock** | LLM risk analysis engine (Claude / Nova model) |
| **AWS Lambda** | Serverless orchestration — coordinates API calls |
| **AWS DynamoDB** | NoSQL storage for scan results and audit logs |
| **AWS S3** | PDF report storage |
| **AWS API Gateway** | Frontend ↔ Lambda bridge |

### Blockchain Data
- **Etherscan API** — Ethereum on-chain data
- **Sui Explorer API** — Sui Network transactions

---

## Getting Started

### Prerequisites

- AWS account (Free Tier works — [sign up here](https://aws.amazon.com/free/))
- Node.js 18+
- Vercel account (free)

### Installation

```bash
# Clone the repo
git clone https://github.com/YOUR_USERNAME/chainguard-ai.git
cd chainguard-ai

# Install dependencies
npm install

# Configure AWS credentials
aws configure

# Set environment variables
cp .env.example .env
# Edit .env with your API keys
```

### Environment Variables

```env
AWS_REGION=ap-northeast-1
DYNAMODB_TABLE=chainguard-scans
BEDROCK_MODEL_ID=anthropic.claude-3-5-sonnet-20241022-v2:0
ETHERSCAN_API_KEY=your_key_here
```

### Deploy

```bash
# Deploy Lambda functions
npm run deploy:lambda

# Deploy frontend to Vercel
vercel deploy
```

---

## API Usage

```bash
# Scan a contract address
POST /api/scan
{
  "address": "0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045",
  "chain": "ethereum"
}

# Response
{
  "riskScore": 73,
  "level": "HIGH",
  "findings": [...],
  "reportId": "uuid",
  "auditTrailUrl": "dynamodb://..."
}
```

---

## Roadmap

- [x] MVP: contract risk scan + DynamoDB audit trail
- [x] Wallet transaction analysis
- [x] AI-generated PDF reports
- [ ] Sui blockchain support
- [ ] Real-time alert webhooks
- [ ] Multi-chain dashboard (EVM + Sui)
- [ ] Telegram bot integration for Taiwan DeFi community

---

## Hackathon Context

Built for **[H0: Hack the Zero Stack](https://h01.devpost.com)** (AWS × Vercel, June 2026).

This project is part of a multi-hackathon strategy — the same codebase will be extended for:
- **AWS AI Agent Global Hackathon** (Q3 2026) — upgraded with Bedrock AgentCore
- **DIGITIMES × AWS Taiwan Hackathon** — localized for Taiwan crypto fraud patterns

---

## License

MIT © 2026 ChainGuard AI
