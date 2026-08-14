# OQGF-1.0 — NORMATIVE AMENDMENT 013
## The Recursive Inferential Privacy Requirement: Governing Knowledge Created by Authorized Disclosure

**Amendment ID:** OQGF-AMD-2026-013
**Amends:** OQGF-1.0, Section A.P (Physiology Layer). Adds a new requirement, OQGF-P-14.
Does **not** modify AMD-009 (OQGF-P-11, Personal Data), AMD-007 (OQGF-I-8 through I-15, Barrier
and Data Custody), or any prior amendment; it adds the inferential-consequence property that
those amendments presume but do not specify, per the OQGF annotation convention.
**Author:** Jeremy Rose, CEO — Odin's LLC, Wasilla, Alaska
**Date:** 14 August 2026
**Status:** Public draft for NIST, sector regulators, and the Odin's engineering team
**Normative dependencies:** OQGF-I-8 through OQGF-I-15 (AMD-007, Barrier/Data Custody — the
egress gate this amendment sits beside, conjunctively); OQGF-P-11 (AMD-009, Personal Data —
lifecycle obligations this amendment does not replace); OQGF-P-10 (AMD-008, Risk Surveillance —
a material inferential exposure enters the Register); OQGF-P-13 (AMD-012, Recursive Risk
Propagation — a material exposure may enter the RRPG; the Privacy Inferability Hypergraph is NOT
the RRPG); OQGF-P-2 (AMD-002, deterministic/heuristic boundary); OQGF-P-9 (AMD-006, accountable
risk acceptance — bounded, not waiver-grade); OQGF-M-8 through OQGF-M-14 (AMD-001, intent
provenance); OQGF-P-12 (AMD-011, Capability-Triggered Assurance — recipient capability is one
input); OQGF-A-1, OQGF-A-5 (Organ 5 recording and the Designated Accountable Party).
**Method posture:** Method-neutral. Classical, quantum, hybrid, probabilistic, causal, or other
estimators may satisfy the analytical requirements if they meet the declared assurance criteria.
This amendment does not require a quantum estimator.

---

## AMD.0 Front matter

### AMD.0.1 Purpose of this amendment

OQGF already governs whether information is personal (AMD-009), why it is processed (purpose
limitation), how long it is retained (retention bound), where it may cross a boundary (AMD-007
Barrier), what capabilities a system possesses (AMD-011), and how material risk propagates
(AMD-012). Those properties remain necessary but are not sufficient for AI-mediated privacy.

A system may release several individually permitted facts while enabling a recipient — a person,
an AI model, or a downstream system — to derive a protected proposition that was never directly
released.

> **An authorized datum is not necessarily an authorized inference.**

Three facts illustrate the shape:

```text
fact A — individually permitted
fact B — individually permitted
fact C — individually permitted
recipient prior knowledge K — external
──────────────────────────────────────
protected proposition S becomes inferable
```

Every existing gate passes. The data is correctly classified. The crossings are authorized. The
purpose is declared. The recipient is authenticated. The egress channel is governed. And the
recipient, combining A, B, C with what they already knew, can now derive a fact the organization
was supposed to protect — a medical condition, a corporate strategy, a mission state, a trade
secret, a future location, or a non-personal but rights-affecting conclusion.

This is the compositional inference failure, and no current OQGF requirement governs it. The gap
was verified against every document in the corpus: zero normative requirements govern what
knowledge a disclosure enables, what a recipient can derive, or what inferential consequence a
release carries.

This amendment closes it by making **inferential consequence before disclosure** a governed
object. It adds a prospective requirement to assess and govern the new knowledge enabled by
disclosure — direct inferability, recursive multi-hop inferability, cumulative inferability,
many-to-one mosaic inferability, recipient-specific inferability, and uncertainty in recipient
knowledge and capability — before the release crosses the boundary.

### AMD.0.2 Why this is a Physiology-Layer requirement and not an extension to AMD-009

AMD-009 correctly treats Personal Data as a governed classification with lifecycle obligations:
minimization, purpose limitation, retention, crypto-shredding erasure, and subject rights.
Inferential privacy is a different failure mode. The compositional inference attack does not
require any individual datum to be misclassified, mishandled, or improperly released. It requires
only that the *combination* of individually proper releases enables an inference the organization
is supposed to prevent.

And the protected proposition need not be Personal Data. Corporate strategy, mission state, trade
secrets, operational relationships, future location, collective or family information, and
non-personal but rights-affecting facts can all be exposed by combining individually permitted
disclosures. Confining inferential privacy to AMD-009 would incorrectly imply that only data
already tagged Personal is subject to compositional inference — and would leave corporate,
mission, and operational secrets unprotected against exactly the same attack.

No single organ owns inferential privacy. A proposed disclosure can originate from an
Organ-1-classified asset, be semantically assessed by Organ 2, be authorized under Organ-3
identity and intent, cross the Organ-2 Barrier, depend on Organ-4 redundancy, and require
Organ-5 recording and reconstruction. The inferential consequence is an emergent property of the
composition of authorized facts with recipient knowledge and capabilities — a systemic behavior
across the governed system. That is the Physiology-Layer test, the same test that placed every
cross-cutting requirement from P-1 through P-13 in this namespace.

### AMD.0.3 The biological basis

The immune system faces the compositional-exposure problem directly, and two biological
mechanisms translate this amendment's core requirements.

The first is **epitope spreading** in autoimmune disease. The immune system initially attacks one
self-antigen — call it antigen A. The inflammation from that attack physically damages tissue,
exposing additional self-antigens (B, C) that were previously hidden inside intact cells. The
immune system then mounts new responses against B and C — antigens it was never directly exposed
to but can now "infer" from the consequences of its own initial authorized response. This is
recursive inferential exposure: the first authorized interaction enables discovery of additional
protected information through a cascading, compositional process. Each tissue-damage event
(individual disclosure) is a consequence of the immune system's own legitimate action — but the
resulting exposure of B and C was never intended and progressively widens the attack surface.

The translation is exact. A governed system releases fact A (authorized, individually
permitted). The release causes no harm by itself. But the recipient, combining A with their
existing knowledge, can now infer protected proposition B. And from B, they can infer C. Each
step was enabled by an authorized disclosure; the cascading inference was never authorized. P-14.4
(Recursive Inferability) is the governance of epitope spreading: analysis does not stop at the
first inference; it follows the reachable inference path until a governed termination condition or
an uncertainty frontier is reached.

The second mechanism is **conformational epitopes**. An antigenic surface recognized by an
antibody can be formed by multiple discontinuous peptide segments that fold together spatially.
Each segment individually is non-immunogenic — the immune system does not recognize it. Together
they form a three-dimensional surface that antibodies bind with high affinity. The immune system
responds to the *composition*, not the components.

This is the mosaic inference attack. Three individually non-revealing facts — a department, a
salary band, a performance rating — are each non-identifying and individually permitted. Combined,
they identify one person. The protected proposition (identity) is formed by the spatial folding
of non-revealing components, exactly as the conformational epitope is formed by the spatial
folding of non-immunogenic segments. P-14.5 (Non-Additive and Mosaic Exposure) is the governance
of conformational recognition: the system must assess the combination, not only the components.

A body that governed antigen exposure only by checking whether each individual peptide segment
was immunogenic — and never checked whether the combination formed a conformational epitope —
would miss every antibody-mediated autoimmune attack driven by molecular mimicry and
conformational recognition. A governance framework that checks whether each individual datum is
classified and authorized — and never checks whether the combination enables a protected
inference — misses every compositional privacy attack. The immune system learned to check both.
This amendment requires the governance framework to do the same.

### AMD.0.4 Terminology additions

- **Protected Proposition** — a fact, attribute, relationship, state, event, prediction, or
  conclusion whose inferability is governed for one or more Privacy Principals. The protected
  antigen analog.
- **Privacy Principal** — a person, organization, group, mission, or other rights/authority
  holder whose protected proposition is governed.
- **Recipient Knowledge State** — a bounded representation or uncertainty model of facts
  plausibly available to a recipient before a proposed release.
- **Recipient Capability Profile** — a bounded representation of a recipient's plausible
  analytical capabilities, including models, databases, tools, public-web access, organizational
  access, and compute.
- **Privacy Inferability Hypergraph (PIH)** — a directed attributed hypergraph in which tail
  propositions may jointly enable inference of a head proposition, with recipient-, purpose-,
  time-, and capability-conditioned inferability parameters. Distinct from and SHALL NOT be
  silently treated as the AMD-012 Recursive Risk-Propagation Graph.
- **Inferential Exposure Delta** — the nonnegative counterfactual increase in inferability of a
  Protected Proposition caused by a candidate release: Δ_j(a) = [P(s_j | K_r ⊕ a) − P(s_j |
  K_r)]₊ or a documented equivalent estimator.
- **Recursive Inferential Privacy Loss** — a governed loss measure aggregating newly attributable
  inferential exposure over one or more inference depths and protected propositions.
- **Interaction Exposure** — inferential exposure created by a combination of facts beyond that
  attributed to the facts independently. The conformational-epitope analog.
- **Candidate Release** — an exact, redacted, generalized, tokenized, perturbed, derived,
  proof-based, local-compute, encrypted-compute, or denied form considered before disclosure.
- **Inferential Privacy Gate** — the deterministic reference-monitor function that authorizes the
  final release form after required policy, utility, inferability, uncertainty, and principal
  checks. External to and unmodifiable by the model.

### AMD.0.5 Scope, and the relationship to AMD-007, AMD-009, AMD-011, and AMD-012

| Existing requirement | What it governs | What this amendment adds |
| --- | --- | --- |
| OQGF-I-10 / AMD-007 | Whether data of a declared classification may cross to an unauthorized destination | Whether the *inferential consequence* of a release crosses a privacy boundary, even when each datum individually passes |
| OQGF-P-11 / AMD-009 | Personal-data lifecycle: minimization, purpose, retention, erasure, subject rights | The compositional inference attack across individually permitted releases, beyond Personal Data, before disclosure |
| OQGF-P-12 / AMD-011 | What the composed system can do, reach, and cause | Recipient capability as an input to inferability assessment |
| OQGF-P-13 / AMD-012 | How risk states propagate, branch, converge, and feed back | A material inferential exposure MAY enter the P-10 Risk Register and therefore the P-13 graph; the PIH is NOT the RRPG |

For a governed outbound crossing, P-14 is an **additional conjunct**, not a substitute:

```text
ALLOW only if
    identity/authorization passes
AND AMD-007 data-classification crossing passes
AND AMD-009 personal-data obligations pass (when applicable)
AND AMD-011 capability/destination constraints pass (when applicable)
AND AMD-013 inferential-privacy decision passes
```

A release blocked by any mandatory conjunct SHALL NOT be made by claiming that another passed.

### AMD.0.6 Design assumptions requiring confirmation

This amendment makes the following design calls. Each is the fail-safe default. All were ratified
by the DAP on 14 August 2026 and are recorded here as decided.

1. **Standalone placement at OQGF-P-14.** *(Ratified.)* The requirement applies beyond Personal
   Data, introduces recipient-conditioned inferability, has recursive and mosaic semantics not
   present in lifecycle governance, requires a pre-disclosure analytical and enforcement loop,
   and spans multiple organs.
2. **The Inferential Privacy Gate is a Deterministic Gate under OQGF-P-2.** *(Ratified.)* Neural
   components propose; the deterministic path decides. Same pattern as OQGF-G-4, OQGF-I-10,
   OQGF-P-12.4, and OQGF-P-13.9.
3. **Recipient knowledge unknown ≠ recipient knowledge zero.** *(Ratified.)* An unknown recipient
   knowledge state SHALL NOT be interpreted as an empty one. For high-impact propositions,
   uncertainty triggers conservative controls, not optimistic release.
4. **Method-neutral.** *(Ratified.)* The amendment requires the property (prospective,
   recipient-conditioned, recursive inferability assessment) without mandating how.
5. **The PIH is NOT the RRPG.** *(Ratified.)* P-13 models risk-state propagation; P-14 models
   knowledge-state inferability. One-way data flow, not a feedback loop.
6. **Risk acceptance does not waive non-waivable rights.** *(Ratified.)* OQGF-P-9 does not
   authorize a DAP to waive a legal prohibition, a non-waivable right, another principal's
   policy, or a deterministic P-14 prohibition that defines no acceptance path. Bounded
   exceptions are explicit, signed, purpose-bound, recipient-bound, time-bound, recorded, and
   incapable of silently propagating.
7. **Disclosure history is not automatically reset.** *(Ratified.)* Session boundaries, agent
   restarts, model changes, or protocol changes do not reset inferential privacy state when the
   recipient can plausibly retain prior information.
8. **Denial text does not reveal the protected inference.** *(Ratified.)* A denial that reveals
   what was being protected defeats the protection.

---

## AMD.1 Normative requirements

These requirements add OQGF-P-14 to Section A.P. They do not modify AMD-009, AMD-007, or any
prior amendment; they add the inferential-consequence property those amendments presume.

**OQGF-P-14.1 (Protected-Proposition Governance).** A conforming system SHALL identify Protected
Propositions material to its declared privacy policy and SHALL bind each proposition to one or
more Privacy Principals, a governing policy, and an accountable source of authority (OQGF-A-5).
Protected Propositions MAY be discovered or proposed by learned systems, but their authoritative
adoption, removal, or material weakening SHALL require the deterministic governance path
(OQGF-P-14.8). The absence of a direct data field containing the proposition SHALL NOT be treated
as evidence that the proposition cannot be exposed. A system that governs only explicitly stored
data and never assesses what can be inferred from it does not satisfy this requirement.

**OQGF-P-14.2 (Recipient-Conditioned Privacy State).** Before a material outbound disclosure, a
conforming system SHALL assess inferential privacy relative to the intended recipient or a
defensible recipient threat class. The assessment SHALL include, where material: estimated prior
knowledge (Recipient Knowledge State); recipient role and relationship; declared purpose;
available tools, models, and data sources (Recipient Capability Profile); relevant prior
disclosure history; and uncertainty in those estimates. Unknown recipient knowledge SHALL NOT be
interpreted as zero knowledge.

**OQGF-P-14.3 (Prospective Counterfactual Evaluation).** For each material Candidate Release, the
system SHALL compare the protected-proposition inferability state before and after hypothetical
release. For protected proposition s_j and candidate release a: the Inferential Exposure Delta
Δ_j(a) = [P(s_j | K_r ⊕ a) − P(s_j | K_r)]₊ , or a documented equivalent estimator. The
requirement is prospective: evaluation SHALL occur before release when the crossing is
controllable.

**OQGF-P-14.4 (Recursive Inferability).** Where a newly inferable proposition can materially
enable another Protected Proposition, analysis SHALL continue across the reachable inference path
to the depth required by declared policy or until a governed uncertainty frontier is reached. The
system SHALL NOT assume that the immediate inference is the terminus. Fixed implementation limits
MAY exist, but a limit that truncates a still-material plausible path SHALL produce an explicit
unresolved inferability state, not an implied safe result. This is the epitope-spreading
governance: the cascade of inference is followed, not assumed to stop at the first step.

**OQGF-P-14.5 (Non-Additive and Mosaic Exposure).** The system SHALL support representation of
many-to-one inference in which a combination of propositions enables a Protected Proposition not
materially inferable from the components independently. Where material, candidate evaluation
SHALL compare combination exposure against independent exposure and SHALL treat positive
synergistic exposure as governed privacy state. A system that scores every datum independently
but cannot represent a material known combination does not satisfy this requirement for that use
case. This is the conformational-epitope governance: the composition creates the recognizable
surface, not the components.

**OQGF-P-14.6 (Longitudinal Disclosure State).** A conforming system SHALL maintain sufficient
disclosure history to evaluate cumulative and interaction exposure across relevant prior
releases. Session boundaries, agent restarts, model changes, or protocol changes SHALL NOT
automatically reset inferential privacy state when the recipient can plausibly retain prior
information. History may be attenuated or retired only under a declared, auditable relevance
policy. A system that forgets what it already told a recipient and re-evaluates each release in
isolation does not satisfy this requirement when the cumulative effect is material.

**OQGF-P-14.7 (Minimum-Loss Task-Sufficient Release).** Where more than one Candidate Release can
satisfy the authorized task, the system SHALL select a policy-permitted candidate that minimizes
governed inferential privacy loss subject to declared task-utility requirements. Candidate classes
SHOULD include, where applicable: exact release; redaction; generalization;
tokenization/pseudonymization; differential-privacy mechanism; derived answer; cryptographic or
attested proof; local computation; encrypted computation; and denial. This requirement does not
prescribe one optimization algorithm; it requires that the system consider alternatives rather
than defaulting to full disclosure when a less-exposing form satisfies the task.

**OQGF-P-14.8 (Deterministic Inferential Privacy Gate).** The final release authorization SHALL
be made by a deterministic control path external to and unmodifiable by the model or estimator.
Learned components MAY propose Protected Propositions, propose hyperedges, estimate inferability,
estimate utility, and propose transformations. They SHALL NOT authorize release, suppress a
Protected Proposition, lower a privacy threshold, declare uncertainty resolved, erase disclosure
history, convert Deny or Abstain into Allow, broaden Purpose, or waive another principal's
rights. A prompt, model instruction, heuristic tolerance, or model confidence statement SHALL NOT
satisfy this requirement. This is the OQGF-P-2 Deterministic Gate applied to inferential privacy:
neural proposes; deterministic decides.

**OQGF-P-14.9 (Uncertainty and Conservative Failure).** Inferability estimates SHALL carry a
declared uncertainty, calibration, or assurance state commensurate with the method used. For a
high-impact Protected Proposition, insufficient assurance SHALL result in stronger
transformation, local execution, consent or review, abstention, or denial according to policy.
The system SHALL NOT present an uncalibrated or out-of-domain score as a precise privacy
probability. Where the Recipient Knowledge State is materially uncertain, the system SHALL use a
conservative estimate consistent with the declared threat class, not an optimistic one.

**OQGF-P-14.10 (Multiple Privacy Principals).** Where a disclosure materially affects more than
one Privacy Principal, the system SHALL evaluate the applicable policy for each affected
principal. One principal's authorization SHALL NOT automatically waive another principal's
protected interest. The aggregation or conflict-resolution rule SHALL be declared, deterministic
at enforcement, and auditable.

**OQGF-P-14.11 (Privacy-Model Protection and Safe Explanation).** The system SHALL protect its
inferability model, subject-specific graph state, Protected Proposition set, and detailed
inference pathways as sensitive governance assets. Recipient-facing denials SHALL NOT be required
to reveal the Protected Proposition or the exact inferential path that triggered the control.
Full path explanations SHALL be restricted to authorized principals, auditors, DAPs, or other
governed roles. A denial that reveals the protected inference defeats the protection it was
supposed to enforce.

**OQGF-P-14.12 (Estimator Neutrality and Quantum Evidence).** This amendment SHALL NOT require a
quantum estimator. A quantum or hybrid quantum estimator MAY satisfy the analytical requirements
only if it meets the same calibration, provenance, assurance, and audit requirements as a
classical estimator. A claim that quantum processing itself supplies privacy SHALL NOT satisfy
this amendment. Where a QML estimator is chosen in preference to a classical estimator for
operational reasons, the operator SHALL maintain evidence supporting the claimed operational
advantage within the declared use domain.

**OQGF-P-14.13 (Audit, Reconciliation, and Risk Linkage).** Organ 5 SHALL record sufficient
evidence to reconstruct each material inferential-privacy decision, including: recipient and
purpose; policy version; candidate set; selected transformation and verdict; protected
propositions evaluated; inferability assessment; uncertainty state; cumulative and interaction
assessment; estimator and version; and authorization, consent, or review where required. A
material privacy exposure discovered after release SHALL trigger reconciliation of the affected
Privacy Inferability Hypergraph. Where the exposure is a material organizational or system risk,
it SHALL create or update the OQGF-P-10 Risk Register entry (AMD-008) and link into OQGF-P-13
(AMD-012) where applicable.

---

## AMD.2 Conformance criteria per level

**Baseline (OQGF-B):** Protected Propositions maintained for material privacy concerns
(OQGF-P-14.1); intended recipient and purpose evaluated before material release (OQGF-P-14.2);
prospective counterfactual assessment within declared scope (OQGF-P-14.3); relevant disclosure
history preserved (OQGF-P-14.6); deterministic final release authority (OQGF-P-14.8); material
privacy verdict recorded in Organ 5 (OQGF-P-14.13); uncertainty treated explicitly with
conservative failure on high-impact propositions (OQGF-P-14.9). Single-PQC-family gate
signatures acceptable.

**Enhanced (OQGF-E):** All Baseline criteria, plus many-to-one mosaic representation
(OQGF-P-14.5); multi-hop recursive propagation (OQGF-P-14.4); candidate-transformation
comparison with minimum-loss selection (OQGF-P-14.7); calibrated inferability estimates;
event-driven update after material recipient-capability or disclosure-state change;
multi-principal handling with declared conflict-resolution (OQGF-P-14.10); adversarial tests for
cumulative and mosaic leakage.

**High-Assurance (OQGF-H):** All Enhanced criteria, plus robust or high-quantile treatment of
recipient uncertainty for high-impact propositions; independently reviewed Protected Proposition
policy; independent verification of deterministic gate logic; dual-PQC-family integrity
consistent with OQGF-R-1/OQGF-M-2; continuous or near-real-time disclosure-state reconciliation
commensurate with the fastest relevant release path; adversarial testing of estimator
underconfidence, graph poisoning, history truncation, model replacement, explanation leakage, and
recipient-capability drift; periodic replay of Organ-5 evidence against current P-14 policy.

Conformance level changes assurance depth and cadence. It SHALL NOT permit a known catastrophic or
rights-affecting inferential path to be silently ignored.

---

## AMD.3 Assessment procedures

An auditor SHALL:

1. Define a Protected Proposition not directly present in any outbound field; construct two or
   more individually permitted facts whose combination reveals that proposition; and confirm the
   system represents the combination and does not treat the facts only independently
   (OQGF-P-14.1, OQGF-P-14.5). **This is the load-bearing test of this amendment**: it proves
   the system governs compositional inference, not only individual data fields.
2. Show that a second disclosure changes the verdict because the first is retained in disclosure
   state, confirming cumulative assessment across prior releases (OQGF-P-14.6).
3. Construct a two-hop inference path and confirm downstream protected exposure is assessed, not
   assumed to terminate at the first inference (OQGF-P-14.4).
4. Remove recipient knowledge from the assessment and confirm uncertainty does not become an
   automatic allow; confirm conservative failure on a high-impact proposition (OQGF-P-14.9,
   OQGF-P-14.2).
5. Ask a model or estimator to authorize a denied release and confirm the deterministic gate
   refuses — no model instruction, prompt, or confidence statement overrides the gate
   (OQGF-P-14.8).
6. Confirm a lower-loss transformed response is selected when it satisfies utility requirements,
   rather than defaulting to full disclosure (OQGF-P-14.7).
7. Create a multi-principal conflict and verify the declared conflict-resolution policy is applied
   deterministically; confirm one principal's authorization does not automatically waive
   another's (OQGF-P-14.10).
8. Inspect recipient-facing denial text and verify it does not disclose the Protected Proposition
   or the exact inferential path that triggered the control (OQGF-P-14.11).
9. Replace the estimator and verify deterministic enforcement semantics remain unchanged — the
   gate is estimator-independent (OQGF-P-14.12, OQGF-P-14.8).
10. Replay a material privacy decision from Organ-5 records and confirm full reconstruction of
    recipient, purpose, candidates, verdict, protected propositions, inferability, uncertainty,
    and estimator version (OQGF-P-14.13).
11. Demonstrate linkage from a realized material inferential exposure into the P-10 Risk Register
    and, where applicable, the P-13 Recursive Risk-Propagation Graph (OQGF-P-14.13).

---

## AMD.4 Control mappings

- **NIST AI RMF:** MAP-1.5, MAP-2.2 (context and impact — inferential consequence as an impact
  input); MEASURE-2.6, MEASURE-2.11 (fairness, bias, and privacy risk from model outputs);
  MANAGE-2.1, MANAGE-2.4 (risk treatment and post-deployment monitoring — disclosure-state
  reconciliation); GOVERN-1.2, GOVERN-4.1 (accountable governance — DAP and deterministic gate).
- **NIST SP 800-53 Rev. 5:** PT-2 (authority and purpose — purpose-bound disclosure), PT-3
  (purpose specification — the conjunctive gate), SI-12 (information management and retention —
  disclosure-history governance), SI-18 (PII quality and accuracy — protected-proposition
  accuracy), AC-4 (information flow enforcement — the Inferential Privacy Gate as a flow-control
  mechanism), AU-2, AU-3, AU-12 (audit event content and generation — Organ 5 decision
  reconstruction), RA-3 (risk assessment — inferential exposure as a risk input), PM-9 (risk
  management strategy — privacy-risk governance).
- **NIST Privacy Framework:** CONTROL-P (management of data processing consistent with purpose);
  COMMUNICATE-P (transparency); CT.DM (data management — the prospective, pre-disclosure
  evaluation); CT.DP (data processing — recipient-conditioned, compositional assessment).
- **NIST SP 800-188 (De-Identification):** informative support for re-identification risk from
  combined data releases. The OQGF contribution is recipient-conditioned, recursive,
  pre-disclosure governance — extending de-identification from a static property of a dataset to
  a dynamic, recipient-aware, cumulative property of a disclosure sequence.
- **EU AI Act:** Article 10 (data governance — inferential consequence in training data);
  Article 12 (record-keeping — Organ 5 privacy decisions); Article 13 (transparency — safe
  explanation that does not reveal the protected inference).
- **GDPR lineage (consistency, not certification):** Article 5(1)(c) (data minimization — minimum-
  loss release); Article 25 (data protection by design and by default — prospective, pre-
  disclosure assessment); Recital 26 (likelihood of identification — the counterfactual
  evaluation).
- **ISO/IEC 42001:** Clause 6 (risk assessment), Annex A.7 (data for AI systems). **ISO/IEC
  27701 / ISO/IEC 29100 lineage** for privacy-lifecycle obligations. **ISO 31000** risk-cycle
  lineage through the P-10/P-13 linkage.
- **CNSA 2.0:** ML-DSA-87 for gate-decision signatures; dual-family (ML-DSA + SLH-DSA) at
  High-Assurance per OQGF-R-1.

---

## AMD.5 Technical architecture (implementation hooks)

The Privacy Inferability Hypergraph and the Inferential Privacy Gate are core types in
`oqgf-core`, persisted in `oqgf-memory` (Organ 5). The gate sits at the Controlled Boundary
alongside OQGF-I-10 (data-classification egress) and OQGF-P-12.4 (capability egress) as a
conjunctive enforcement layer. No existing type is modified; no existing gate is replaced.

### AMD.5.1 Core types

```rust
/// A governed proposition whose inferability is controlled (OQGF-P-14.1).
/// Bound to one or more Privacy Principals, a governing policy, and a DAP.
/// The protected antigen.
pub struct ProtectedProposition {
    pub id: PropositionId,
    pub description: String,
    pub principals: Vec<PrivacyPrincipal>,
    pub policy_ref: PolicyRef,
    pub authority: DesignatedAccountableParty,   // reuses existing type (OQGF-A-5)
}

/// A person, organization, group, mission, or rights holder (OQGF-P-14.10).
pub struct PrivacyPrincipal {
    pub id: PrincipalId,
    pub kind: PrincipalKind,   // Person | Organization | Group | Mission | Other
}

/// What the recipient plausibly knows and can do (OQGF-P-14.2).
/// Unknown ≠ zero (OQGF-P-14.9).
pub struct RecipientState {
    pub knowledge: KnowledgeModel,           // bounded, not assumed empty
    pub capability: CapabilityProfile,        // tools, models, data sources, compute
    pub disclosure_history: DisclosureLog,    // cumulative (OQGF-P-14.6)
    pub uncertainty: UncertaintyAssessment,
}

/// The pre-disclosure assessment for one candidate release (OQGF-P-14.3).
pub struct InferabilityAssessment {
    pub candidate: CandidateRelease,
    pub recipient: RecipientState,
    pub exposures: Vec<ExposureDelta>,        // per protected proposition
    pub recursive_depth: u8,                   // hops followed (OQGF-P-14.4)
    pub interaction_effects: Vec<InteractionExposure>, // mosaic (OQGF-P-14.5)
    pub estimator: EstimatorRef,               // provenance (OQGF-P-14.12)
    pub confidence: ConfidenceAssessment,
}

/// The nonnegative counterfactual increase in inferability (OQGF-P-14.3).
/// delta is NonNegative — claims that disclosure REDUCES inferability are
/// structurally unrepresentable.
pub struct ExposureDelta {
    pub proposition: PropositionId,
    pub prior: InferabilityScore,             // P(s_j | K_r)
    pub posterior: InferabilityScore,          // P(s_j | K_r ⊕ a)
    pub delta: NonNegative,                   // [posterior - prior]₊
    pub epistemic: EpistemicState,            // Observed | Modeled | Hypothesized
}

/// The Deterministic Gate for inferential privacy (OQGF-P-14.8).
/// External to and unmodifiable by the model. Neural proposes; this decides.
pub trait InferentialPrivacyGate: Send + Sync {
    fn evaluate(
        &self,
        assessment: &InferabilityAssessment,
        policy: &PrivacyPolicy,
    ) -> PrivacyVerdict;
}

/// The gate's decision (OQGF-P-14.8). No path from Deny/Abstain to Allow
/// exists through the model — only through the deterministic gate
/// re-evaluating with a different candidate (OQGF-P-14.7 minimum-loss).
pub enum PrivacyVerdict {
    Allow { transformation: TransformationType, justification: String },
    Deny { reason_code: ReasonCode },   // does NOT reveal the proposition (P-14.11)
    Abstain { uncertainty: UncertaintyAssessment },
}

/// Candidate release forms (OQGF-P-14.7). The system considers alternatives
/// rather than defaulting to full disclosure.
pub enum TransformationType {
    Exact,
    Redacted,
    Generalized,
    Tokenized,
    DifferentiallyPrivate { epsilon: f64 },
    DerivedAnswer,
    CryptographicProof,
    LocalComputation,
    EncryptedComputation,
    Denied,
}
```

The safety properties are structural. `PrivacyVerdict` has no variant and no method that converts
`Deny` or `Abstain` into `Allow` without passing through `InferentialPrivacyGate::evaluate` with
a different candidate — the model cannot override a denial. `ExposureDelta.delta` is
`NonNegative`, making negative deltas (claims that disclosure *reduces* inferability)
unrepresentable. `RecipientState.knowledge` has no "empty" default, so treating unknown knowledge
as zero requires an explicit, auditable choice rather than a silent default.

### AMD.5.2 What this closes, and what it does not

This amendment **closes** the following:

- **The compositional inference gap.** A system conforming to AMD-007, AMD-009, and AMD-011 can
  no longer release individually permitted facts whose combination enables a protected inference
  without prospective assessment (OQGF-P-14.1, OQGF-P-14.3, OQGF-P-14.5).
- **The memoryless disclosure problem.** A system that forgets what it already told a recipient
  and evaluates each release in isolation is non-conforming when cumulative exposure is material
  (OQGF-P-14.6).
- **The one-hop assumption.** Inferential analysis must follow the reachable path, not stop at
  the first step (OQGF-P-14.4).
- **The full-disclosure default.** Where a less-exposing form satisfies the task, the system
  considers it (OQGF-P-14.7).
- **The model-as-privacy-gate illusion.** No model instruction, prompt, or confidence statement
  authorizes release; the deterministic gate decides (OQGF-P-14.8).
- **The leaky denial.** A denial that reveals the protected inference defeats the protection
  (OQGF-P-14.11).
- **The quantum-privacy overclaim.** Quantum processing is not inherently privacy-preserving; a
  QML estimator must meet the same assurance standards as a classical one (OQGF-P-14.12).

This amendment **does not** fully close, and states so honestly:

- **Recipient knowledge is estimated, not known.** The system models what a recipient plausibly
  knows; the actual recipient may know more or less. P-14.2 requires that unknown knowledge not
  be treated as zero, and P-14.9 requires conservative failure on high-impact propositions, but
  the estimate can still be wrong. Same residual shape as AMD-010's trainability profile and
  AMD-012's causal inference: a declared model is only as good as its declaration.
- **Computational intractability at scale.** The counterfactual evaluation is computationally hard
  in the general case. The amendment is method-neutral and allows bounded and uncertainty models,
  but a system with millions of possible compositions faces real computational limits. Truncation
  produces an uncertainty frontier, not a safe verdict — but the frontier may be large.
  Materiality policy bounds the scope; the bound is itself a governance judgment. Same residual
  shape as AMD-012's graph-scale adversarial.
- **Semantic reframing.** A model instructed not to reveal X may answer a differently worded
  question that narrows X almost as much. Semantic reframing that evades literal pattern matching
  is a known privacy-research problem. The deterministic gate catches what the estimator flags;
  it does not catch what the estimator misses. Same residual shape as AMD-001's over-broad root
  intent: named, bounded by DAP accountability and estimator improvement, not eliminated.
- **Upstream truth.** Information that reaches the recipient through channels the system does not
  control changes the recipient's knowledge state without the system's awareness. P-14.6 handles
  known disclosure history; it cannot track unknown disclosures. Same residual shape as AMD-007's
  uncontrolled-channel residual.
- **Protected-proposition completeness.** The system governs propositions it has identified. A
  protected proposition that no one thought to declare is ungoverned — the same unknown-unknowns
  residual as AMD-008, AMD-011, and AMD-012.

---

## AMD.6 Traceability

| Requirement | Implementation hook | Existing OQGF dependency |
| --- | --- | --- |
| OQGF-P-14.1 | `oqgf-core::ProtectedProposition`, `PrivacyPrincipal`; adoption via deterministic path | P-11.1, P-10, A-1/A-5 |
| OQGF-P-14.2 | `RecipientState` (knowledge + capability + history); unknown ≠ zero | M-8–M-14, P-12 capability pattern |
| OQGF-P-14.3 | `InferabilityAssessment`, `ExposureDelta`; prospective, before release | P-2 deterministic/heuristic |
| OQGF-P-14.4 | `recursive_depth` on assessment; unresolved inferability state on truncation | P-13 conceptual sibling; distinct graph |
| OQGF-P-14.5 | `InteractionExposure`; combination ≠ sum of components | P-5/P-7 compositional precedent |
| OQGF-P-14.6 | `DisclosureLog` on `RecipientState`; no automatic reset | A-1, P-12.8 trajectory precedent |
| OQGF-P-14.7 | `TransformationType` enum; minimum-loss selection over candidates | I-10 Barrier; P-11 Purpose |
| OQGF-P-14.8 | `InferentialPrivacyGate` trait; `PrivacyVerdict` with no Deny→Allow bypass | P-2; I-10; P-12.4; P-13.9 |
| OQGF-P-14.9 | `UncertaintyAssessment`; conservative failure on high-impact | P-10/P-13 uncertainty pattern |
| OQGF-P-14.10 | multi-`PrivacyPrincipal` on `ProtectedProposition`; declared conflict rule | P-11 subject rights + A-5 |
| OQGF-P-14.11 | `PrivacyVerdict::Deny` carries `ReasonCode`, not proposition or path | G/R integrity + Organ 5 |
| OQGF-P-14.12 | `EstimatorRef` provenance; QML claims require evidence; quantum ≠ private | A-8–A-12 assurance pattern |
| OQGF-P-14.13 | full decision record in `oqgf-memory`; exposure → P-10 → P-13 | A-1, P-10, P-13 |

---

## AMD.7 Change log

v1.0 — Initial public draft, 14 August 2026. Adds OQGF-P-14 (Recursive Inferential Privacy) to
the Physiology Layer: makes inferential consequence before disclosure a governed object. Requires
every material outbound disclosure to be prospectively assessed against the protected propositions
it can enable a recipient to derive — not only the data it directly contains — through recipient-
conditioned, recursive, cumulative, and compositional analysis. Introduces the Privacy
Inferability Hypergraph as the structural representation of how tail propositions jointly enable
head propositions, distinct from and not to be silently treated as the AMD-012 Recursive
Risk-Propagation Graph. Requires a Deterministic Inferential Privacy Gate under OQGF-P-2: neural
components propose protected propositions, estimate inferability, and suggest transformations;
only the deterministic path authorizes release, and no model instruction, prompt, or confidence
statement may override a denial.

Extends the OQGF privacy thesis from "govern the data" to "govern the data, the disclosure, and
the protected knowledge the disclosure can enable." Applies beyond Personal Data to corporate
strategy, mission state, trade secrets, operational relationships, and any rights-affecting
proposition. Requires longitudinal disclosure-state tracking so cumulative exposure is assessed,
not forgotten. Requires minimum-loss task-sufficient release: where a less-exposing form satisfies
the task, the system considers it rather than defaulting to full disclosure. Requires that denial
text not reveal the protected inference. Requires estimator neutrality: a quantum estimator must
meet the same assurance standards as a classical one, and a claim that quantum processing itself
supplies privacy does not satisfy the amendment. Requires risk linkage: a material inferential
exposure enters the P-10 Risk Register and, where applicable, the P-13 graph.

Does not modify AMD-009 (Personal Data lifecycle), AMD-007 (Barrier and data custody), AMD-012
(recursive risk propagation), or any prior amendment; sits alongside them as an additional
conjunctive gate at the Controlled Boundary. Five residuals are named rather than claimed
eliminated — recipient-knowledge estimation, computational intractability at scale, semantic
reframing, upstream truth, and protected-proposition completeness — each mapped to the shape of a
prior amendment's residual.

The biological basis is epitope spreading (recursive inferential exposure: the first authorized
interaction enables discovery of additional protected information through a cascading process)
and conformational epitopes (mosaic inference: individually non-immunogenic segments that fold
together into a recognizable surface). The governance framework, like the immune system, must
govern both the individual components and the composition.

— End of OQGF Amendment 013.
