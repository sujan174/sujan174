# Sujan H

Infrastructure engineer. I build the plumbing that sits between AI agents and the systems they touch — gateways, policy engines, credential vaults, CLIs, MCP servers.

Rust · Go · TypeScript · Python — B.Tech IT, NITK Surathkal, graduating May 2027 — Bangalore, IST

**Open to internships, contract work, and founding-engineer roles (remote).**

[![Email](https://img.shields.io/badge/sjn.174%40gmail.com-D14836?style=flat-square&logo=gmail&logoColor=white)](mailto:sjn.174@gmail.com)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/sujan-h-358068378/)

---

## What I've shipped

### [TrueFlow](https://github.com/sujan174/TrueFlow) — an AI gateway in Rust

A proxy that sits between your agents and the model providers. Agents get a scoped, expiring, budget-capped virtual token; the real API key stays in an encrypted vault and never reaches the agent process. Two-line migration — change the base URL and the key, and every OpenAI-compatible client keeps working.

- **Policy engine** — rules against any request/response field, firing 15+ action types: `deny`, `redact`, `rate-limit`, `route`, `spend-cap`, `require-approval`, `tool-scope`, `shadow-log`
- **Credential vault** — AES-256-GCM envelope encryption, per-credential data keys wrapped by a master key that never touches the database
- **PII redaction** — 11 built-in patterns stripped before the request leaves your network, with optional Presidio sidecar (fail-open)
- **Spend caps that block**, not just alert — daily/monthly/lifetime budgets per token
- **Human-in-the-loop gates** — pause a request class for review, no application code changes
- **Routing** — 5 load-balancing strategies across 10 providers, exponential-backoff retries, per-endpoint circuit breakers

`Rust (Axum/Tower/Tokio) · PostgreSQL 16 · Redis 7 · Next.js 16 · Python + TypeScript SDKs · OpenTelemetry`

**<1 ms hot-path overhead. SSE streamed word-by-word with no buffering. 1,051 tests** across unit, integration, adversarial and E2E layers.

### [console.store](https://github.com/sujan174/console.store) — MCP server + multi-client installer, in Go

A terminal-native tool that provisions an MCP server into 7+ AI dev clients — Claude Desktop, Cursor, VS Code and others — reconciling JSON, TOML and YAML config formats. Idempotent: re-running never corrupts an existing config.

- OS keyring token storage rather than plaintext credentials on disk
- ed25519-signed binaries with a self-verifying auto-update path
- GoReleaser cross-compile matrix (linux/darwin/windows × amd64/arm64), 3 release channels, shipped through GitHub Actions
- 695 commits

`Go · MCP · GoReleaser · GitHub Actions · ed25519`

### [SafeKeys](https://github.com/sujan174/SafeKeys-github-Action) — secrets delivery for CI

A GitHub Action that pulls short-lived secrets from a vault at job runtime instead of storing them in repo settings. Three pieces: the [Action](https://github.com/sujan174/SafeKeys-github-Action) (TypeScript), a [vault server](https://github.com/sujan174/SafeKeys-Vault-Server), and a [Next.js console](https://github.com/sujan174/Safekeys-App).

`TypeScript · Next.js · GitHub Actions`

---

## Things I keep coming back to

**Latency budgets are a design constraint, not a benchmark.** TrueFlow's hot path is under a millisecond because every allocation on that path got argued with.

**Installers are where trust is won or lost.** Most of console.store is not the MCP server — it's the config reconciliation, the keyring handling, and the signing, because that is the part that breaks on someone else's machine.

**Secrets should be scoped and short-lived, everywhere.** Virtual tokens in TrueFlow, keyring storage in console.store, runtime injection in SafeKeys — same idea, three surfaces.

---

## Stack

**Systems** ![Rust](https://img.shields.io/badge/Rust-000000?style=flat-square&logo=rust&logoColor=white) ![Go](https://img.shields.io/badge/Go-00ADD8?style=flat-square&logo=go&logoColor=white) ![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white) ![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)

**Data** ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white) ![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)

**Infra** ![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white) ![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white) ![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white) ![OpenTelemetry](https://img.shields.io/badge/OpenTelemetry-000000?style=flat-square&logo=opentelemetry&logoColor=white)

**Interfaces** ![MCP](https://img.shields.io/badge/Model_Context_Protocol-1a1a1a?style=flat-square) ![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=next.js&logoColor=white)

---

<div align="center">

**Currently:** hardening TrueFlow's policy engine and extending console.store's client matrix.

If you're building agent infrastructure and want a second pair of hands — [email me](mailto:sjn.174@gmail.com).

</div>
