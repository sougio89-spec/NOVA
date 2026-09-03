<div align="center">

# NOVA

### Distributed Compute & Job Infrastructure

**OPUS → NEXUS → NOVA CORE / NOVA MINING → TOKENIA**

Experimental infrastructure for routing jobs, executing distributed compute and AI workloads, validating results, and settling Devnet rewards.

`DEVNET` · `OPEN-CORE` · `DISTRIBUTED COMPUTE` · `AI INFERENCE` · `SOLANA`

</div>

---


<div align="center">

<img src="assets/01_nova_overview.png" alt="NOVA decentralized compute network" width="100%">

</div>

---

## NOVA at a glance

<img src="assets/02_five_servers.png" alt="NOVA five servers ecosystem" width="100%">

### How a job moves through NOVA

<img src="assets/03_job_lifecycle.png" alt="NOVA job lifecycle" width="100%">

### Dual-token architecture

<img src="assets/04_dual_token_economy.png" alt="NOVA and NEXUS token economy" width="100%">

### Global network vision

<img src="assets/05_global_network.png" alt="NOVA global decentralized compute network" width="100%">

---

## What is NOVA?

NOVA is an experimental distributed infrastructure built around **five cooperating services**.

```text
                         ┌─────────────────────┐
                         │       CLIENTS       │
                         │ Companies / Builders│
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │        OPUS         │
                         │ Job Intake Gateway  │
                         └──────────┬──────────┘
                                    │
                                    ▼
                    ┌─────────────────────────────┐
                    │            NEXUS            │
                    │ Validate · Route · Orchestrate│
                    └───────────┬─────────┬───────┘
                                │         │
                    ┌───────────▼──┐   ┌──▼────────────┐
                    │  NOVA CORE   │   │ NOVA MINING   │
                    │ AI / Compute │   │ Worker Network │
                    └───────────┬──┘   └──┬────────────┘
                                │         │
                                └────┬────┘
                                     ▼
                          ┌─────────────────────┐
                          │      TOKENIA        │
                          │ Settlement / Ledger │
                          └──────────┬──────────┘
                                     │
                                     ▼
                          ┌─────────────────────┐
                          │   SOLANA DEVNET     │
                          │ NOVA-Test / NEXUS-Test│
                          └─────────────────────┘
```

The objective is simple: a job enters through OPUS, NEXUS validates and routes it, compute nodes execute it, the result is verified, and TOKENIA handles the corresponding test settlement.

> **Current status:** prototype / Devnet. NOVA does not currently claim to be a production network, a source of guaranteed revenue, or a mainnet financial product.

---

## The five services

| Service | Role | Current direction |
|---|---|---|
| **OPUS** | Job intake | Receives jobs from individuals, developers and companies |
| **NEXUS** | Network brain | Validation, routing, orchestration and node coordination |
| **NOVA CORE** | Compute layer | GPU compute and AI inference execution |
| **NOVA MINING** | Worker layer | Distributed workers and contribution accounting |
| **TOKENIA** | Economic layer | Reward ledger and Devnet token settlement |

---

## Devnet economy

NOVA currently uses two **test-only** Solana Devnet assets.

### NOVA-Test

```text
3TjaggzWLmy6c3PPFTUz63e5pr1RS2Hg25so5MRZRtRK
```

Designed for testing compute/mining rewards and the broader NOVA economy.

### NEXUS-Test

```text
F2GTysEXAtra3KGvnwfqpcuypz3Mb4pfok4L4b6SteHZ
```

Designed for testing NEXUS node, validation and orchestration rewards.

**Neither Devnet token has monetary value.**

---

## Job lifecycle

```text
01  SUBMIT
    OPUS receives a job
          ↓
02  VALIDATE
    NEXUS checks and classifies the request
          ↓
03  ROUTE
    NEXUS selects NOVA CORE or NOVA MINING capacity
          ↓
04  EXECUTE
    Worker performs the workload
          ↓
05  VERIFY
    Result / proof returns to NEXUS
          ↓
06  SETTLE
    TOKENIA records the reward
          ↓
07  DEVNET
    NOVA-Test or NEXUS-Test settlement
```

---

## Build a NOVA Node

The public repository is being prepared so external developers can eventually run test workers without receiving access to NOVA's private production internals.

### Target worker interface

A worker needs to be able to:

```text
REGISTER
   ↓
ADVERTISE CAPABILITIES
   ↓
RECEIVE JOB
   ↓
EXECUTE
   ↓
RETURN RESULT + PROOF
   ↓
RECEIVE VERIFIED REWARD
```

A minimal public protocol sample is available in:

```text
sdk/nova_protocol.py
examples/job.json
```

### Example reward object

```python
from decimal import Decimal
from sdk.nova_protocol import Reward, mint_for

reward = Reward(
    asset="NOVA_TEST",
    amount=Decimal("12.5"),
)

print(mint_for(reward.asset))
```

This public SDK is intentionally small today. The next milestone is a reproducible external worker client.

---

## Roadmap

### Phase 1 — Architecture
- [x] Five-service architecture
- [x] OPUS / NEXUS / CORE / MINING / TOKENIA separation
- [x] Dual-token Devnet model
- [x] Public open-core repository

### Phase 2 — Devnet
- [x] NOVA-Test mint
- [x] NEXUS-Test mint
- [ ] Reproducible five-service local environment
- [ ] End-to-end Devnet settlement demo
- [ ] Public transaction examples

### Phase 3 — External Nodes
- [ ] Public worker client
- [ ] Node registration protocol
- [ ] Capability discovery
- [ ] AI inference adapter
- [ ] GPU benchmark suite
- [ ] Public node telemetry

### Phase 4 — Public Testnet
- [ ] External test nodes
- [ ] Job marketplace test
- [ ] Public network metrics
- [ ] Failure / retry testing
- [ ] Security review

### Phase 5 — Production Research
- [ ] Economic simulations
- [ ] Anti-fraud validation research
- [ ] Treasury architecture review
- [ ] Independent security audit
- [ ] Mainnet decision only after validation

---

## We are looking for contributors

NOVA is early. That is exactly why contributions can have a large impact.

Areas where help is useful:

- **Distributed systems**
- **Python backend engineering**
- **GPU scheduling**
- **AI inference**
- **Solana development**
- **Cryptography / security**
- **Observability**
- **Benchmarking**
- **Developer tooling**
- **Technical documentation**

If you want to contribute, read [`CONTRIBUTING.md`](CONTRIBUTING.md) and start with an issue or a small pull request.

---

## Open-core model

This repository intentionally exposes the **public integration surface**, documentation, Devnet identifiers, protocol examples and contribution tooling.

The following categories are intentionally not published in the public edition:

- production treasury secrets
- private keys / seed phrases
- production infrastructure credentials
- proprietary anti-fraud internals
- sensitive orchestration policies
- production signing infrastructure

This allows developers to understand and integrate with NOVA without turning the public repository into a dump of sensitive production code.

---

## Repository structure

```text
.
├── README.md
├── CONTRIBUTING.md
├── SECURITY.md
├── LICENSE
├── .env.example
├── docs/
│   └── PUBLIC_ARCHITECTURE.md
├── examples/
│   └── job.json
├── sdk/
│   └── nova_protocol.py
└── .github/
    ├── ISSUE_TEMPLATE/
    └── PULL_REQUEST_TEMPLATE.md
```

---

## Security

NOVA is currently a **Devnet prototype**.

Never commit:

```text
seed phrases
private keys
treasury keypair JSON files
API secrets
JWT signing keys
database passwords
production credentials
```

See [`SECURITY.md`](SECURITY.md).

---

## License

The public repository is distributed under the **Apache License 2.0**.

Private NOVA components not included in this repository are not automatically covered by the public source distribution.

---

<div align="center">

### NOVA // BUILD THE COMPUTE NETWORK

**Devnet first. Measure everything. Scale only what works.**

</div>
