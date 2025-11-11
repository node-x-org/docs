# ProofX & PoRW

<p align="right"><a href="https://docs.node-x.xyz/proofx-and-porw">中文</a></p>

### **1.**&#x42;ackground and Vision

In an era where compute power becomes a global core resource, NodeX is dedicated to enabling every real device to securely on-chain and receive fair value rewards within a distributed network.

However, existing Web3 node networks generally suffer from two major issues:

* **Sybil attacks**: a single user fabricates hundreds of nodes by forging identities
* **Invalid compute rewards**: nodes cannot prove real task execution, leading to token economic inflation

To address this, we designed a dual framework of **ProofX (Real Identity Verification)** and **PoRW (Proof of Real Work)** to **rebuild a distributed trust layer** and provide a unified verification and incentive standard for the global compute market.

***

### 2.System Architecture Overview

**ProofX** and **PoRW** are not isolated modules but the underlying trust components within NodeX’s three-layer architecture (Device Layer, Coordination Layer, Trust Layer):

* **Device Layer**: Collects device fingerprints, performance benchmarks, and online behavior to generate a Machine Unique Identifier (MID)
* **Coordination Layer**: Schedules tasks and compute market activities
* **Trust Layer**: Verifies the authenticity of devices and tasks via ProofX & PoRW
* **Financialization**: Maps real contributions to points and token weights

***

### 3.ProofX: Real Identity Verification Mechanism

#### 3.1 Core Objective

**ProofX** is used to verify **the authenticity of node identities and compute power sources**, ensuring every participant represents an independent and verifiable real device.

#### 3.2 Verification Logic

* **MID Generation and Binding:**\
  Each device, at first registration, generates MID based on hardware hash, device fingerprint, and signing algorithm, serving as its unique network identity. Once established, the MID acts as an irreplaceable identity anchor in all subsequent task verification and settlement steps.
* **Random and Periodic Verification:**\
  The system issues Challenge tasks irregularly to ensure immediate device responses
* **Anti-fraud Mechanism:**\
  If a node submits anomalous results or features duplicate, automatic penalties are triggered (reputation decay, point reset, ban)

***

### 4.PoRW: Proof of Real Work Mechanism

#### 4.1 **Design Philosophy**

PoRW not only proves that the node is working, but also proves that the node completed valuable real work.\
The system tracks device task execution history based on MID, converting performance, online duration, stability, and success rate into a composite contribution value.

#### 4.2 Dynamic Points Calculation Model

* **EMA Reputation Points Algorithm:**&#x45;xponential Moving Average to resist short-term fluctuations
* **Quality Weighting Model**MIDs with long-term steady online presence and high-quality task execution receive higher PoRW weights
* **Fair Distribution：**&#x4C;ow-performance but stable nodes can still earn rewards matched to their contribution over the long term

***

### 5.Dual-Layer Collaboration: ProofX × PoRW

|                 |                                           |                                                  |                           |
| --------------- | ----------------------------------------- | ------------------------------------------------ | ------------------------- |
| Level           | ProofX Verification                       | PoRW Evaluation                                  | Joint Effect              |
| Identity Layer  | Ensure authenticity of accessing devices  | —                                                | Prevent Sybil attacks     |
| Execution Layer | Verify authenticity of devices performing | Measure task completion and efficiency           | Eliminate false tasks     |
| Incentive Layer | —                                         | Distribute rewards based on overall contribution | Achieve fair distribution |

Through the joint mechanism of **ProofX and PoRW**, NodeX lays **the foundation for a trusted compute network**. Only devices that pass ProofX verification, contribute via PoRW, and possess a unique MID are eligible for on-chain settlement points (AP / RP) and token mapping weights.

***

### 6.Security and Scalability

* **Tamper-proof Uploads:**&#x43;lients sign data based on MID, with on-chain notarization
* **Privacy Protection：**&#x4D;ID is fully separated from personal data, reflecting only device-layer identity
* **Modular Architecture:**&#x50;roofX and PoRW support independent upgrades and replacements
* **Cross-Chain Interoperability:**&#x41;dapts to cross-chain verification standards for both EVM and non-EVM environments

***

### 7.Summary

ProofX and PoRW jointly build a **verifiable, auditable, and sustainable** distributed trust system. It is not only the security backbone of NodeX but also the **Trust Anchor** for compute markets in the DePIN era.
