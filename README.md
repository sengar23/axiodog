# AxioDog — Safe, Human-Approved AI-Agent Transactions (Base-first)

**AxioDog** is an open-source **policy engine + approval console** that lets AI agents act on-chain **only within guardrails**:
_simulate → explain (plain English) → check policy → human approve → execute_.

> **Launch chain:** Base • **License:** MIT / Apache-2.0 (dual) • **Status:** Pre-MVP (actively building)

---

## Why AxioDog
AI agents can trigger blockchain transactions. Without a standard safety layer, teams risk:
- **Financial loss** (overspending, bad approvals)
- **Security issues** (malicious contracts, wrong recipients)
- **Compliance gaps** (no audit trail or human sign-off)

AxioDog makes agent transactions **safe, explainable, and controllable** before anything hits the chain.

---

## Core Features (MVP)
- **PolicyAccount (ERC-4337 smart account)**  
  Spend caps (per-tx/day), token/contract/recipient allow-lists, time windows, optional co-sign (EIP-1271), emergency lock.
- **Agent SDK (TypeScript)**  
  Safe primitives (`transfer`, `swap`, `approve`, `call`) that always run `simulate → explain → checkPolicy → queue`.
- **Review Console (Next.js + OnchainKit)**  
  Queue of pending requests, simulation diffs, policy checks, one-click Approve/Reject, activity timeline.
- **Gasless UX (Paymaster/Bundler)**  
  Sponsor first transactions to reduce friction for non-crypto users.
- **Audit trail (optional)**  
  Off-chain explanations/logs hashed and pinned (e.g., IPFS); CIDs surfaced in events.

---


## Tech Stack
- **On-chain:** Solidity, ERC-4337-compatible smart account, OpenZeppelin, Foundry/Hardhat for testing
- **Frontend:** Next.js, TypeScript, TailwindCSS, **OnchainKit**
- **Agents & Wallets:** **CDP AgentKit**, **CDP Wallet SDK**
- **Payments/Swaps:** **CDP Onramp API**, **CDP Swap API**
- **Gasless:** **CDP Paymaster/Bundler**
- **Backend:** Node.js, lightweight API, Postgres/Supabase (queue & audit index)
- **Infra:** Vercel, Base RPC, optional IPFS pinning

---

## Roadmap (9 weeks MVP)
- **M1 (Weeks 1–3) — Core rails**  
  `PolicyAccount`, `PolicyRegistry`, simulation + explanations, Console (queue + detail), Base Sepolia demo.
- **M2 (Weeks 4–6) — Gasless + logs**  
  Paymaster/Bundler, evented audit trail (+ optional IPFS CIDs), docs & quickstarts, example flows.
- **M3 (Weeks 7–9) — Merchant flows**  
  Subscriptions/recurring + retries, SDK polish, analytics hooks, demo dashboard.

> Post-MVP: risk oracles integration (e.g., slippage/depeg), attestation hooks, policy template marketplace.

## CDP Integrations (Base)
- **Wallet SDK** — connect/sign userOps from the console.
- **AgentKit** — bridge agent intents to AxioDog SDK.
- **Onramp API** — optional fiat → USDC flow embedded in onboarding.
- **Swap API** — quotes + execution bounded by policy (slippage cap, allow-lists).
- **Paymaster/Bundler** — sponsor first transactions; restrict sponsorship to approved userOps.


## Security Model

### Threats & Mitigations
- **Bypass policy:** all writes go through PolicyAccount; optional EIP-1271 co-sign; Paymaster only sponsors approved ops.
- **Phishing/malicious targets:** allow-lists + explorer/ENS labels; optional risk feeds post-MVP.
- **Abuse of caps:** per-token rolling caps; emergency lock.
- **Log tampering:** hash logs; IPFS pinning; include CID in on-chain events.

### Operational
- **Principle of least privilege** for API keys; rotate regularly.
- **CI checks** (lint, typecheck, tests, slither).

## Milestones & Acceptance

- **M1 — Core rails (3 wks)**  
  Contracts compiled & tested; Queue + Request Detail pages; Base Sepolia demo; >85% unit coverage for policy logic.
- **M2 — Gasless + logs (3 wks)**  
  Paymaster wired; two end-to-end flows (send USDC, swap with cap) pass; docs/quickstarts live.
- **M3 — Merchant flows (3 wks)**  
  Subscriptions + retries; CLI for policy updates; 3 external devs complete quickstart unaided.