# BIP: Miner Template Control Signaling

**BIP:** ?  
**Title:** Miner Template Control Signaling  
**Author:** Christian  
**Status:** Draft  
**Type:** Informational  
**Assigned:** ?  
**License:** BSD-2-Clause

## Abstract

This document proposes a standardized signaling and commitment mechanism through which Bitcoin miners can publicly express their preference for **Miner Template Control (MTC)**.

MTC means that an individual miner retains the ability to construct and control the block template used for its own mining work, including transaction selection and transaction ordering, rather than being required to mine exclusively on a block template constructed by a mining pool.

The proposal does not introduce a Bitcoin consensus rule and does not require Bitcoin nodes to recognize or enforce MTC.

Instead, it establishes a voluntary coordination mechanism intended to improve communication between miners and mining pools and to create transparent economic incentives for pools to provide miner-controlled block templates.

A miner can use the mechanism to communicate its demand for MTC **before leaving its current pool**. A pool can therefore observe measurable demand for MTC and respond to that demand before hashpower necessarily migrates elsewhere.

If a pool does not provide the requested functionality, miners can subsequently direct their committed hashpower toward infrastructure that does.

Stratum V2 with Job Declaration is one possible technical implementation of MTC, but this proposal is protocol-independent.

---

## Motivation

Bitcoin mining involves several distinct forms of control.

Hashpower may be distributed among a large number of independently owned mining devices while the construction of the blocks being mined remains controlled by a comparatively small number of pool operators.

A mining pool may aggregate hashpower from many independent miners while retaining centralized control over:

- transaction selection;
- transaction ordering;
- block-template construction; and
- consequently, the set of transactions its participating miners are attempting to include in blocks.

The distribution of physical mining hardware and the distribution of block-template construction authority are therefore separate properties.

Technical mechanisms for miner-controlled block construction already exist.

For example, Stratum V2 Job Declaration allows miners to declare custom mining jobs containing transactions selected by the miner rather than having work unilaterally imposed by the pool. A Template Provider can provide custom block templates, and this role can be fulfilled by a Bitcoin Core full node or another node implementation.

However, technical availability does not necessarily produce economic adoption.

A miner may prefer MTC while having no standardized way to communicate that preference to its current pool.

Without such a mechanism, the miner may effectively have only two choices:

1. accept the pool's current architecture; or
2. leave the pool.

This proposal introduces a third option:

**the miner can publicly communicate its preference before leaving.**

---

## 1. Miner Template Control

For the purposes of this proposal, mining infrastructure provides **Miner Template Control** if an individual miner is able to:

1. independently construct a candidate block template;
2. select transactions for that template;
3. determine the ordering of those transactions;
4. submit mining work based on that template;
5. receive valid mining shares and the applicable rewards through the infrastructure; and
6. mine without being required by the infrastructure to replace its template with one constructed by the pool.

The precise protocol used to provide these properties is outside the scope of this proposal.

Stratum V2 Job Declaration is one possible implementation.

MTC therefore describes a **functional property**, not a particular mining protocol.

---

## 2. Miner Signaling

A miner may publicly signal support for MTC.

The signal indicates that the miner considers miner-controlled block-template construction a desired property of its mining infrastructure.

The primary purpose of the signal is communication.

A miner should be able to communicate:

> I want my mining infrastructure to provide Miner Template Control.

without being required to immediately leave its existing pool.

The signal SHOULD be:

- publicly observable;
- independently countable;
- attributable to the signaling miner or to identifiable mining hashpower where technically possible;
- distinguishable from Bitcoin consensus signaling; and
- resistant to accidental or ambiguous interpretation.

The signaling mechanism MUST NOT change Bitcoin consensus rules.

This proposal does not prescribe a specific signaling mechanism.

---

## 3. Preference and Commitment

The proposal distinguishes between **expressing a preference** and **making an economic commitment**.

### Preference

A miner publicly signals its preference for MTC.

This signal does not require the miner to immediately change pools.

Its purpose is to communicate demand.

### Commitment

A miner may additionally commit a specified amount of hashpower for a defined period to mining infrastructure that satisfies the MTC requirement.

The commitment gives the signal economic credibility.

A suggested commitment period is 2016 blocks, although this value is not normative and should be evaluated during review.

The distinction is important because communication should precede enforcement.

The intended sequence is:

**preference → communication → opportunity for the pool to respond → commitment → migration if necessary.**

---

## 4. Communication Between Miners and Pools

A central purpose of the proposal is to improve communication between miners and pools.

A pool may otherwise discover that its miners value MTC only when those miners actually leave.

This is an inefficient feedback mechanism.

Under this proposal, miners can communicate their preference while continuing to use their existing infrastructure.

For example:

1. A miner currently contributes hashpower to Pool A.
2. The miner signals support for MTC.
3. Pool A can observe that a measurable amount of its participating hashpower has expressed this preference.
4. Pool A can choose to implement MTC or provide compatible infrastructure.
5. If Pool A responds successfully, the miner has no reason to migrate its hashpower merely to obtain MTC.
6. If Pool A does not respond, the miner can direct its committed hashpower toward another pool or infrastructure that provides MTC.

The signal therefore acts as an **early-warning mechanism** for pools.

It gives the pool an opportunity to respond to miner demand before the pool actually loses the associated hashpower.

For miners, it provides a way to communicate a meaningful preference before taking the economically more disruptive step of changing pools.

This communication function is an independent benefit of the proposal, even before any hashpower migration takes place.

---

## 5. Economic Mechanism

The intended economic mechanism is:

**signaling → public visibility → pool awareness → opportunity to respond → miner choice → hashpower migration if necessary → economic pressure → adoption.**

The proposal does not assume that pools will adopt MTC merely because miners signal it.

Instead, signaling makes previously difficult-to-observe demand visible.

Pools can then compete for miners by providing the functionality those miners value.

If a pool ignores sufficiently large and credible demand for MTC, participating miners have an economically meaningful alternative: directing their hashpower toward infrastructure that satisfies the requirement.

The market therefore provides the principal enforcement mechanism.

No Bitcoin consensus enforcement is required.

---

## 6. Miner Choice and Voting With Hashpower

The proposal relies on voluntary miner choice.

A miner that makes an MTC commitment should be able to direct the committed hashpower only toward infrastructure satisfying the stated MTC requirement.

If the current pool does not provide MTC, the miner may move to another pool.

This creates a form of economic signaling analogous to voting with one's purchasing power.

The important distinction is that the signaling mechanism allows the preference to become visible **before** the actual migration takes place.

Consequently, the pool has an opportunity to respond before losing the miner.

---

## 7. Public Measurement

Independent observers SHOULD be able to distinguish at least three different states:

1. **Signaling**  
   Hashpower expressing a preference for MTC.

2. **Claimed compatibility**  
   Mining infrastructure publicly claiming to provide MTC.

3. **Demonstrable use**  
   Hashpower for which there is independent evidence that MTC is actually being used.

These categories MUST NOT be conflated.

A pool claiming compatibility should not automatically be counted as receiving MTC-signaling hashpower.

Likewise, signaling should not automatically be interpreted as proof that a miner is currently using MTC.

Public statistics should make these distinctions explicit.

---

## 8. Pool Transparency

Mining pools that support MTC SHOULD publicly document:

- the protocol or mechanism used;
- whether miners can construct their own block templates;
- whether miners can independently select transactions;
- whether miners can independently order transactions;
- whether the pool can override a miner-created template;
- how shares based on miner-created templates are handled; and
- how failover operates.

This allows miners to make informed choices and enables independent comparison of mining infrastructure.

---

## 9. Signaling Mechanism

The exact mechanism for publicly signaling an MTC preference is intentionally left open.

Possible approaches include, but are not limited to:

- a mining-protocol-level signal;
- a separate public commitment mechanism;
- a mechanism associated with mining identities or payout infrastructure;
- or a block-level signal, provided that it can be implemented without ambiguity or interference with Bitcoin consensus signaling.

The proposal does **not** currently assign a bit in the Bitcoin block version field.

In particular, BIP 9 defines version-bit signaling primarily in the context of soft-fork deployments, while current BIP 323 reserves bits 5 through 28 of `nVersion` for general-purpose mining nonce space and removes those bits from soft-fork signaling. Any use of `nVersion` for MTC signaling would therefore require careful coordination with existing and future Bitcoin protocol conventions and should not be assumed by this proposal.

The final signaling mechanism should satisfy the following properties:

1. it must not modify Bitcoin consensus rules;
2. it should be publicly observable;
3. it should be independently measurable;
4. it should minimize ambiguity regarding what is being signaled;
5. it should allow a meaningful association between the signal and the committed hashpower where practical; and
6. it should not interfere with existing or future Bitcoin protocol signaling mechanisms.

Determining the best mechanism is an explicit subject for further discussion.

---

## 10. Commitment Representation

A commitment should, where technically practical, identify:

- the amount of hashpower covered by the commitment;
- the beginning of the commitment period;
- the duration or end height;
- and the MTC requirement to which the commitment applies.

The commitment should be publicly verifiable to the greatest extent practical.

The exact method for binding a commitment to specific mining hashpower remains an open technical question.

The proposal does not require miners to reveal their real-world identities.

---

## 11. No Consensus Enforcement

This proposal intentionally does not make MTC a Bitcoin consensus requirement.

Bitcoin nodes MUST NOT reject a block merely because:

- the miner did not signal MTC;
- the miner used a pool-controlled template;
- the pool does not support MTC; or
- the block does not contain an MTC signal.

MTC is an economic and organizational property of mining infrastructure, not a consensus property of Bitcoin.

The proposal therefore introduces no consensus rule.

---

## 12. Relationship to Stratum V2

Stratum V2 Job Declaration provides a concrete technical mechanism for miners to create and declare custom mining jobs. Its specification explicitly describes custom jobs as jobs containing transactions selected by the miner rather than unilaterally imposed by the pool.

However, this proposal does not require Stratum V2.

The desired property is MTC.

Any mining protocol capable of providing the specified functionality could satisfy the requirement.

This distinction is intentional.

The proposal seeks to create economic demand for miner-controlled templates rather than to mandate a particular mining protocol.

---

## 13. Incentive Structure

### For miners

The proposal provides:

- a mechanism to publicly express a preference for MTC;
- a means of communicating that preference without immediately changing pools;
- greater transparency concerning pool capabilities;
- the ability to coordinate with other miners;
- and an economically credible mechanism for changing infrastructure if the preference is not met.

### For pools

The proposal provides:

- early visibility into miner demand;
- an opportunity to retain miners by implementing requested functionality;
- an additional competitive feature with which to differentiate from other pools;
- and better information about why miners may otherwise leave.

### For the Bitcoin ecosystem

The proposal may provide:

- increased transparency concerning control over block construction;
- stronger economic incentives for decentralized template construction;
- greater separation between hashpower aggregation and block-template control; and
- potentially reduced concentration of transaction-selection authority.

---

## 14. Informational Thresholds

Public reporting MAY use thresholds such as:

- 1%;
- 5%;
- 10%;
- 20%;
- 30%; and
- 50%

of network hashpower signaling MTC.

These thresholds are informational only.

They do not activate consensus rules, invalidate blocks, or impose obligations on miners or pools.

Their purpose is to make changes in miner preference easier to observe and communicate.

---

## 15. Deployment

The proposal can be developed in several stages.

### Stage 1 — Discussion

Discuss the economic model and technical feasibility with miners, pool operators, protocol developers, and researchers.

### Stage 2 — Signaling Standard

Define a standardized, publicly interpretable signaling mechanism.

### Stage 3 — Software Support

Implement signaling, commitment, reporting, and optional enforcement mechanisms in mining software.

### Stage 4 — Statistical Infrastructure

Develop independent statistics capable of distinguishing signaling, claimed compatibility, and demonstrable MTC usage.

### Stage 5 — Miner Adoption

Miners voluntarily begin signaling their preference and, where desired, making commitments.

### Stage 6 — Market Coordination

Pools respond to observable demand and compete for MTC-supporting hashpower.

---

## 16. Security and Abuse Considerations

A signaling system may be subject to:

- false signaling;
- hashpower attribution errors;
- miners signaling without intending to follow through;
- pools falsely claiming MTC compatibility;
- temporary or strategic signaling;
- and attempts to manipulate public statistics.

These issues do not necessarily require consensus enforcement.

The principal defense is transparency and independent measurement.

Public statistics SHOULD distinguish between claims and demonstrable behavior.

Where practical, mining software SHOULD make it difficult for a miner to accidentally signal a commitment that its configured infrastructure cannot honor.

---

## 17. Open Questions

The following questions require further technical and economic discussion:

1. What is the most appropriate signaling mechanism?
2. Should signaling occur at the mining-protocol level, through a separate public commitment, or through another mechanism?
3. Is there a useful block-level signaling mechanism that does not conflict with existing Bitcoin conventions?
4. How can signaling avoid interference with consensus version bits and other uses of the block header?
5. Should signaling occur per block, per mining job, per share, or through a separate public commitment?
6. How can hashpower be attributed to individual miners without requiring disclosure of their identities?
7. How should a pool's MTC capability be independently verified?
8. What precisely constitutes sufficient miner control over a template?
9. How should failover behave when an MTC-compatible pool becomes unavailable?
10. What commitment duration provides useful economic credibility without unnecessarily restricting miners?
11. Should mining software provide automatic enforcement of a miner's MTC commitment?
12. What reference implementation and test suite would be useful?
13. Can existing Stratum V2 Job Declaration implementations serve as an initial interoperability reference?
14. Can the signaling mechanism provide sufficient public information to distinguish genuine miner preference from purely symbolic signaling?

---

## 18. Rationale

The proposal deliberately avoids attempting to solve mining centralization through Bitcoin consensus.

Instead, it targets an economic and communication problem.

Miners already possess the ultimate economic ability to choose where their hashpower is directed.

Pools already compete for that hashpower.

The missing mechanism is a standardized way for miners to communicate a specific architectural preference **before exercising that choice**.

MTC signaling attempts to provide that mechanism.

The intended result is not:

**miners threaten pools → pools are forced to comply**

but rather:

**miners express demand → pools receive information → pools can respond → miners choose → market incentives determine the outcome.**

This makes the proposal fundamentally voluntary and market-driven.

---

## 19. Conclusion

Miner Template Control can reduce the concentration of block-template construction without requiring changes to Bitcoin consensus.

Technical mechanisms for achieving MTC already exist, but economic adoption depends on miners having both a reason and a practical mechanism to demand the functionality.

A standardized public signaling mechanism can provide that missing coordination layer.

By allowing miners to communicate their preference before leaving a pool, the mechanism gives pools an opportunity to respond while giving miners a credible path to migrate their hashpower if their preference is not met.

The resulting process is:

**communication → coordination → transparency → competition → voluntary hashpower migration → economic adoption.**

This proposal therefore seeks to improve not only mining decentralization, but also the quality and timing of communication between miners and the pools competing for their hashpower.
