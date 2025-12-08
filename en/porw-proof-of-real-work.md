# PoRW (Proof of Real Work)

**Verifiable Work Execution Standard — Version 1.0**



***

## **1.Overview**

PoRW (Proof of Real Work) is NodeX’s verifiable execution mechanism designed for globally distributed devices. It proves that a device **actually executed real tasks**, and converts this into measurable contribution units used for:

* Node contribution scoring
* Scheduling priority
* Reward distribution
* Machine reputation (MID)
* AI Body Layer's trusted execution

**PoRW has one clear mission:** **Make every real piece of work provable. Make every contribution fairly rewarded.**&#x50;oRW addresses long-standing problems in Web3, DePIN, and AI agent economies:

* Hard to verify whether a device actually performed a task
* Hard to distinguish real nodes from Sybil/fake nodes
* Black-box outputs are difficult to validate
* Task execution is not auditable
* Reward systems cannot form a trusted economic loop

***

## **2.Core Concept — Tri-Dimensional Verification**

Traditional systems rely on single verification methods (results only, uptime only, declared compute only). PoRW replaces this with **a multidimensional, heterogeneous, complementary verification model**, based on:

* NodeX’s ability to run scripts on devices
* Distributed task dispatch
* Market-driven incentives and penalties

PoRW’s verification system consists of three dimensions:

***

### **2.1 Correlation (Physical–Logical Collision)**

**Best for:** Mining, black-box systems, third-party workloadsCross-checking between:

* **Local script reports:** logs, processes, CPU/GPU patterns
* **External API/on-chain data:** shares, rewards, block height

Detects:

* Fake logs
* Running tasks outside the platform
* “Fake work, real rewards” fraud patterns

***

### **2.2 Probabilistic Redundancy (Distributed Consensus)**

**Best for:** AI inference, compute tasksMechanism:

* Same task dispatched to multiple homogeneous devices
* Compare results (Hash, pHash, CLIP Score)
* Majority rule (Byzantine-style consensus)

Prevents:

* Outsourcing compute
* Skipping execution
* Faking outputs
* Randomness manipulation

Enhancement: reverse image inference to validate whether an output could realistically come from the given task.

***

### **2.3 Social Arbitration (Market-Driven Verification)**

**Best for:** C2C compute renting, SLA-based deliveryMechanism:

* Reputation staking
* SLA monitoring
* User-side reporting + system logs
* Automated dispute resolution

Detects:

* Fake online status
* Overstated performance
* Delivery manipulation

***

## **3.PoRW Architecture**

PoRW sits between NodeX’s **Coordinator Layer** and **Settlement Layer**, converting all workloads into unified **UoC (Unit of Compute)** contribution values.

```
   Coordinator Layer
           ↓
        PoRW Engine
           ↓
   Settlement Layer
```

***

### **3.1 Role Definitions**

| Role       | Description                                           |
| ---------- | ----------------------------------------------------- |
| Worker     | Device executing tasks + generating PoRW data         |
| Dispatcher | Sends tasks/scripts to Workers                        |
| Verifier   | Performs result comparison, correlation, log analysis |
| Reporter   | SLA reporter/user in C2C marketplace                  |

***

## **4.Modular Verification Models**

NodeX’s workload types fall into four categories. Each has a dedicated PoRW validation model.

***

### **Module A — Traffic-Based Verification (RPC / API / Network)**

**Mechanism:** Canary requests + traffic mirroring

* Random test requests hidden inside real traffic
* Workers cannot distinguish test vs. real
* Failure → entire window invalidated

**Score formula**

```
Score = (Requests × Success_Rate) − (Penalty × Latency_Factor)
```

***

### **Module B — Result-Based Verification (Mining / CDN / Black-box)**

**Mechanism:** Internal logs + external oracle cross-checkInternal:

* Logs, PID, CPU/GPU usage
* Script health checks

External:

* On-chain or API data (rewards, shares, blocks)

**Mismatch → invalid work** Detects fake logs, off-platform execution, or fabricated shares.

***

### **Module C — Compute-Based Verification (AI / Rendering / Math)**

**Mechanism:** Probabilistic redundancy consensus

* Same task → 3 devices
* Compare output hash / semantic score
* Majority = truth
* Deviant node punished: score reduction + reputation decrease

Enhanced validation:

* Reverse image/prompt inference to ensure authenticity

***

### **Module D — SLA-Based Verification (C2C Marketplace)**

**Mechanism:** Social arbitrationIncludes:

* Reputation staking
* Automatic SLA monitoring
* User-submitted evidence
* Script log replay during disputes

Penalties:

* Slashed stake
* Reputation reduction
* Loss of marketplace privileges

***

## **5.Unified Settlement Model**

All PoRW outputs are converted into unified contribution values:

```
PoRW_Final = Base_Work × Quality_Index × Reputation_Factor
```

#### **Base\_Work**

* Requests
* Compute cycles
* Execution time
* Task complexity

#### **Quality\_Index (0.8–1.2)**

* Success rate
* Latency
* Performance deviation

#### **Reputation\_Factor (0.0–1.5)**

* Based on MID
* Good actors get multipliers
* Cheaters earn drastically less

***

## **6.Anti-Cheat System**

PoRW uses a multilayer defense stack:

1. **Random challenges** (anti pre-computation)
2. **Multi-point redundancy** (anti result forgery)
3. **Time + performance curves** (anti outsourcing “shadow compute”)
4. **Environment fingerprinting** (anti device emulation)
5. **Reputation decay** (reduces long-term incentives for cheaters)

***

## **7.Complementarity with ZKP / TEE / Oracles / MPC**

PoRW does _not_ replace other cryptographic/verification technologies. It complements them.

***

#### **7.1 With ZKP (Zero-Knowledge Proofs)**

ZKP proves correctness of **deterministic computation**. PoRW proves correctness of **real-world execution**.

* ZKP = result correctness
* PoRW = process correctness

They work best together.

***

#### **7.2 With TEE (Trusted Execution Environments)**

TEE protects execution **inside trusted hardware**. PoRW validates execution **on untrusted devices**.

* TEE = trusted environment
* PoRW = trusted behavior

***

#### **7.3 With Oracles**

Oracles provide **external truth**. PoRW provides **internal truth**.Together:

* Logs ↔ On-chain reward
* Input ↔ Output mappings
* Cross-verification for fraud detection

***

#### **7.4 With MPC / Secure Computation**

MPC protects data privacy.PoRW validates execution integrity.

***

## **8.Why PoRW Matters**

PoRW transforms NodeX into:

* A verifiable execution platform
* A trusted device network
* The execution layer of the AI Body
* The foundation of the Machine Economy

**In one sentence:** **Without PoRW, AI cannot trust devices. Without PoRW, devices cannot earn trustable rewards.**

***

## **9.PoRW Public Roadmap**

#### **Phase 1 — Foundational Verification (Current)**

* Script dispatch & log collection
* Device fingerprint & reputation database

#### **Phase 2 — Access-Layer Verification**

* Full rollout of Traffic-Based + Result-Based modules
* Miner-node correlation checks

#### **Phase 3 — Compute Consensus Layer**

* Large-scale deployment of compute redundancy
* Distributed result comparison engine

#### **Phase 4 — Automated Settlement Layer**

* Final PoRW scoring model
* On-chain or TEE-based settlement

***

## **10.End State**

PoRW enables a new era of machine collaboration:

* Devices become sustainable income-generating assets
* AI agents operate with real-world execution guarantees
* All contributions are transparent, auditable, and unfakeable
* NodeX becomes the world’s largest **Trusted Machine Execution Network**

<br>
