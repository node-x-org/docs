---
description: >-
  AP + RP Dual Points Mechanism and ProofX Cold/Hot Reward Pool Adjustment
  System
---

# Points Program (AP+RP)

<p align="right"><a href="https://docs.node-x.xyz/chan-pin-shou-ce/nodehub/ji-fen-ji-hua-ap+rp">中文</a></p>

### 1.Design Intent

In the NodeX network, every device, every computing power unit, and every participant should receive **fair rewards** based on their **genuine contributions.**

Therefore, we have established a complete incentive system consisting of **ProofX + PoRW + AP/RP + cold/hot reward pool** adjustment,

ensuring a closed loop of "real devices → real computing power → real returns".

Core Philosophy:

**Incentivize genuine contributions and oppose false prosperity.**

***

### 2.ProofX: Trusted Device Verification Layer

ProofX is NodeX's **trusted computing verification protocol**, designed to ensure all nodes are real devices,preventing impersonation, device reuse, identity forgery, and other **Sybil attacks.**

**ProofX** verification includes:

| Verification Dimensions      | Description                                                                      |
| ---------------------------- | -------------------------------------------------------------------------------- |
| Device MID (Machine ID)      | Uniquely generated through hardware fingerprint, multi-signature, and encryption |
| Computing Power Authenticity | Verifies that CPU/GPU performance reports match actual benchmark scores          |
| Node Uniqueness              | Prevents the same device from registering multiple identities                    |
| Environment Trustworthiness  | Detects virtualization/proxy environments and verifies runtime isolation         |

Only verified devices are eligible to participate in RP/AP calculations and reward pool distribution.

***

### 3.Dual Scoring System: AP × RP

| Points Type          | Full Name       | Source                                          | Core Function                                       |
| -------------------- | --------------- | ----------------------------------------------- | --------------------------------------------------- |
| RP (Resource Points) | Resource Points | Real computing power verified by ProofX + PoRW  | Measures device computing power contribution        |
| AP (Action Points)   | Action Points   | Node task execution and community participation | Measures participation level and ecosystem activity |

RP represents computing power contribution, while AP represents ecosystem participation.

Together they constitute the participant's comprehensive contribution level in the system,and are ultimately mapped to token weights through smart contracts.

***

### 4.Reward Pool and Distribution Mechanism

The system daily releases a certain total amount of points based on overall network activity (initially 1,000,000 RP per day),and distributes them according to hardware dimensions:

| Dimension | Weight | Daily Cap (RP) |
| --------- | ------ | -------------- |
| CPU       | 25%    | 250000         |
| GPU       | 35%    | 350000         |
| RAM       | 12%    | 120000         |
| ROM       | 13%    | 130000         |
| NET       | 15%    | 150000         |

The reward pool adopts **a halving mechanism every six months (Halving),**&#x65;nsuring long-term inflation control and gradual scarcity of incentives.

***

### 5.Contribution Scoring Mechanism Driven by ProofX

The daily effective points calculation for each node is as follows:

```
Effective RP = PoRW Computing Power Weight × ProofX Reputation Coefficient × Reward Pool Distribution Ratio
```

The **ProofX** reputation coefficient dynamically changes based on device historical verification records, computing power authenticity, and stability.

The contribution score is composed of the following dimensions:

| Indicator                              | Description                                                       |
| -------------------------------------- | ----------------------------------------------------------------- |
| Performance Benchmark                  | Actual measured scores for CPU/GPU/IO/NET                         |
| Uptime                                 | Continuous online rate                                            |
| Stability                              | System operation fluctuation and failure rate                     |
| Completion Rate                        | Command execution/task success ratio                              |
| Verification Rate (R, from **ProofX**) | **ProofX** verification pass rate, used to determine authenticity |

All indicators are smoothed through EMA processing, and long-term stable nodes will receive higher reputation weights.

***

### 6.Dynamic Adjustment Mechanism of Cold Pool and Hot Pool

To maintain ecological balance and prevent computing power concentration, the system introduces **a cold/hot reward pool adjustment mechanism.**

#### 6.1 Classification Logic

* **Hot Pool:**\
  Actual computing power contribution rate ≥ expected weight (active competition), eligible for additional rewards.\
  Portion of undistributed rewards from the cold pool can be transferred to the hot pool, with a maximum overflow cap of 50% of the original pool.
* **Cold Pool:**\
  Actual computing power contribution rate < expected weight (insufficient participation),rewards are proportionally reduced, with the difference transferred to the hot pool.

#### 6.2 Participation Logic of ProofX

**ProofX** evaluates each node's authenticity score (R) in real-time,low R nodes (suspected false contributions) will be automatically assigned to the cold pool,high R nodes will receive priority rewards from the hot pool.

Therefore, the cold/hot pool mechanism not only bases on computing power contribution but also combines device trustworthiness to form a **dual-dimensional dynamic balance**.

#### 6.3 Results

* Rewards automatically adjust according to real activity levels, controlling inflation;
* Scarce and high-reputation computing power receives additional incentives;
* The network maintains a fair and robust computing power distribution overall.

### 7.Community Participation and AP Incentives

AP (Action Points) primarily rewards the following ecosystem behaviors:

* Node's initial connection and passing **ProofX** verification;
* Completing tasks and submitting commands;
* Inviting new nodes to join;
* Governance voting, staking, feedback, and other activities.

The system periodically calculates based on **AP × RP × ProofX reputation coefficient**,\
determining final token distribution weights, ensuring both computing power and active contributions are rewarded.

***

### 8.Points → Token Mapping Mechanism

Points themselves do not possess monetary attributes,but can be mapped to token weights periodically through on-chain smart contracts.

Mapping Principles:

* **Fairness:**&#x4D;apping ratio is proportional to comprehensive points;
* **Verification Priority:**&#x4E;odes that haven't passed ProofX / PoRW are ineligible for mapping;
* **Continuity:**&#x4C;ong-term active nodes receive decay protection;
* **Anti-cheating:**&#x50;oints of risk-flagged nodes will be frozen.

***

### 9.Summary

| Model                    | Function                                    | Incentive Source                                  |
| ------------------------ | ------------------------------------------- | ------------------------------------------------- |
| ProofX                   | Verify device authenticity                  | Prevent Sybil attacks, establish trusted identity |
| PoRW                     | Verify task authenticity and quality        | Dynamic points allocation                         |
| RP Resource Points       | Incentivizing Real Device Participation     | ProofX Verification Passed + PoRW Calculation     |
| AP Behavioral Model      | Incentivize genuine ecosystem participation | Node tasks, governance, interaction               |
| Cold/Hot Pool Adjustment | Dynamically balance resource incentives     | Scarce computing power incentive bonus            |
| Points→Token Mapping     | Build economic closed loop                  | Fair distribution of long-term contributions      |

Through **the ProofX + PoRW + AP + RP + Cold/Hot Reward Pool Adjustment Mechanism + Coin Mapping Mechanism,**&#x4E;odeX has achieved a complete trust closed loop from device verification to economic incentives:

> “Make Any Device On-Chain, Make Compute Social.”
