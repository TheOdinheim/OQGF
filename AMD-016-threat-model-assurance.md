# OQGF-1.0 — NORMATIVE AMENDMENT 016
## The Threat-Model Assurance Requirement: Provenance, Freshness, Coverage, and Continuous Adversarial Reconciliation

**Amendment ID:** OQGF-AMD-2026-016
**Amends:** OQGF-1.0, Section A.P (Physiology Layer). Adds a new requirement, OQGF-P-17.
Does **not** modify AMD-008 (OQGF-P-10, Risk Surveillance), AMD-012 (OQGF-P-13, Recursive Risk
Propagation), or any prior amendment; it governs the quality and lifecycle of the threat-model
artifact that those amendments consume as a risk source, per the OQGF annotation convention.
**Author:** Jeremy Rose, CEO — Odin's LLC, Wasilla, Alaska
**Date:** 21 August 2026
**Status:** Public draft for NIST, sector regulators, and the Odin's engineering team
**Implementation posture:** Implementation-neutral. A conforming organization MAY satisfy these
requirements with human-maintained threat models, conventional attack graphs, commercial threat-
modeling platforms, neuro-symbolic engines, or any combination. This amendment governs the
property the threat model must carry, not the product that produces it.
**Normative dependencies:** OQGF-P-10 (AMD-008, Risk Surveillance — the Risk Register that
receives threat-model findings as a risk source, OQGF-P-10.2); OQGF-P-13 (AMD-012, Recursive
Risk Propagation — the RRPG that may carry downstream consequences of threat-model findings);
OQGF-P-15 (AMD-014, Adaptive Containment — threat-model findings may signal containment but
SHALL NOT directly mutate the ECE); OQGF-P-16 (AMD-015, Cognitive Integrity — threat-model
output is evidence and proposal, not instruction authority); OQGF-P-12 (AMD-011,
Capability-Triggered Assurance — the attested Capability Envelope and Trajectory Record against
which the threat model is reconciled); OQGF-P-6 (AMD-003, Adaptation — confirmed threat-model
failures may seed detector refinement); OQGF-P-7 (AMD-004, Coordinated Signaling); OQGF-P-2
(AMD-002, deterministic/heuristic boundary); OQGF-A-1/OQGF-A-5 (Organ 5 recording and the DAP);
Part C per-crate `THREAT_MODEL.md` obligation (the document this amendment makes governed).

---

## AMD.0 Front matter

### AMD.0.1 Purpose of this amendment

OQGF-P-10.2 (AMD-008) lists "threat models maintained per trust boundary" as one of the named
risk sources from which the Risk Register SHALL be continuously fed. The per-crate
`THREAT_MODEL.md` obligation in Part C requires that each crate ship a threat model covering
trust boundaries, assets, threats, and mitigations. AMD-012 governs how risk propagates once it
enters the register. AMD-014 governs runtime containment. AMD-015 governs semantic authority.

None of them governs the **threat model itself**.

The framework consumes the threat model as input. It never asks whether the input is honest,
fresh, complete, or reconciled against the system it claims to describe.

A threat model that silently drops a known attack path is consumed without objection. A threat
model whose claims were accurate six months ago but describe a system that has since changed is
consumed without reconciliation. A threat model in which a machine-learning hypothesis is
presented indistinguishably from a verified observation is consumed without epistemic challenge.
An observed adversary path that appears nowhere in the threat model disappears into the gap
between what was modeled and what was real, with no requirement to make that gap visible.

This amendment closes those four failures by governing the quality and lifecycle of the
threat-model artifact: provenance on every claim, epistemic distinction between verified and
hypothesized, versioning and freshness, declared reconciliation against the deployed system,
and explicit coverage failures when observed adversary behavior falls outside the model.

### AMD.0.2 What this amendment governs and what it does not

This amendment governs the **properties** a threat model must carry to serve as a governed OQGF
risk source. It does not mandate a particular threat-modeling product, algorithm, ML architecture,
knowledge base, graph structure, or vendor. A human-maintained threat model that satisfies these
properties conforms. An automated engine that satisfies them conforms. A system that produces
impressive-looking threat analysis but cannot version its claims, distinguish hypothesis from
observation, or reconcile against reality does not conform, regardless of how advanced its
technology is.

The relationship to the existing stack is precise:

| This amendment governs | These amendments govern what happens next |
| --- | --- |
| Is the threat model versioned? | AMD-008 receives threat-model findings as risk entries |
| Are its claims provenance-bound? | AMD-012 models how the risk propagates |
| Are hypotheses distinguishable from facts? | AMD-014 may contract capabilities on threat findings |
| Is it reconciled against the deployed system? | AMD-015 ensures the threat modeler's output is evidence, not authority |
| Are coverage failures explicit? | AMD-003 refines detectors from confirmed misses |

The upstream quality of the threat model determines the downstream integrity of everything that
consumes it. A risk register built on an unversioned, stale, un-reconciled threat model is an
accountability record of risks someone imagined six months ago, not a record of risks the system
actually faces.

### AMD.0.3 Why this is a Physiology-Layer requirement

A threat model spans every organ. The assets it describes live in Organ 1. The boundaries it
maps live in Organ 2. The identities and attestation it depends on live in Organ 3. The
redundancy and independent control it assumes live in Organ 4. The evidence it produces and the
history it maintains live in Organ 5. The reconciliation of the threat model against the deployed
system requires the Capability Envelope (AMD-011), the Trajectory Record (AMD-011), the Risk
Register (AMD-008), and the RRPG (AMD-012). No single organ owns the quality of a threat model.
It is a systemic property — Physiology, at P-17.

### AMD.0.4 The biological basis

The immune system does not maintain a static threat catalog consulted once at deployment.

**Dendritic cells** are sentinel cells that continuously sample the tissue environment for
foreign material. When a dendritic cell encounters a pathogen, it processes the antigen and
migrates to a lymph node, where it presents the evidence to the adaptive immune system — T cells
and B cells — which then mount a targeted response. Critically, the presentation includes
context: the dendritic cell presents not just the antigen but the conditions under which it was
encountered, the tissue of origin, and the danger signals that accompanied it. The adaptive
system's response is conditioned on that contextual evidence, not on the antigen alone.

After exposure, the immune system maintains **immune memory** — long-lived memory T and B cells
that enable a faster, stronger response to a previously encountered pathogen. But immune memory
is not static: it is continuously updated by re-exposure, cross-reactive encounters, and
environmental signals. A memory cell that has not been restimulated eventually wanes. The immune
system's threat model is living, evidence-based, context-conditioned, and continuously
reconciled against what it actually encounters.

The translation is exact in the properties it shares and honestly bounded in the properties it
does not:

Continuous sampling → continuous reconciliation of the threat model against the deployed system.
Evidence presentation with context → provenance-bound, evidence-carrying claims. Adaptive
response conditioned on evidence → risk findings that carry their epistemic state. Immune memory
updated by re-exposure → threat-model versioning with freshness. Waning memory → stale claims
that must be reconciled or retired.

Biology does **not** maintain a formal attack hypergraph, a Datalog reachability engine, or a
graph neural network proposing missing transitions. Those are engineering constructions. The
biological alignment is to the **lifecycle properties** — continuous, evidence-based, contextual,
updatable, reconcilable — not to the implementation mechanism.

### AMD.0.5 Terminology additions

- **Threat-Model Artifact** — the versioned, provenance-bound representation of adversarial
  threats, attack paths, prerequisites, controls, and residuals maintained as a governed OQGF
  risk source. May be a document, a graph, a database, a formal model, or any combination.
- **Threat-Model Claim** — a material assertion within the artifact: the existence of a threat,
  the feasibility of a path, the effectiveness of a control, the absence of a vulnerability, or
  the satisfaction of a prerequisite.
- **Claim Provenance** — the origin, evidence, method, and confidence supporting a Threat-Model
  Claim.
- **Epistemic State (Threat-Model)** — the classification of a claim's evidential basis:
  Observed (directly witnessed in the deployed system or confirmed incident), Verified (tested
  or independently confirmed), Modeled (derived from analysis or simulation), Hypothesized
  (proposed by a learned system, analyst judgment, or external intelligence without independent
  verification), or Refuted (contradicted by evidence, with superseding reference).
- **Threat-Model Coverage** — the set of adversary paths, techniques, prerequisites, and
  conditions the artifact claims to represent.
- **Coverage Failure** — material observed adversary behavior that falls outside the
  Threat-Model Coverage: an attack path, technique, prerequisite exploitation, or effect that
  occurred and was not represented in the model. An explicit gap, not a silent omission.
- **Reconciliation Cadence** — the declared interval or trigger-based schedule at which the
  threat model is reconciled against the attested deployed system state. Declared by the
  operator, not fixed by the specification.

### AMD.0.6 Design assumptions requiring confirmation

All were ratified by the DAP on 21 August 2026 and are recorded here as decided.

1. **Standalone placement at OQGF-P-17.** *(Ratified.)* The threat-model artifact's quality is
   upstream of AMD-008, AMD-012, AMD-014, and AMD-015 — it governs the input those amendments
   consume.
2. **Implementation-neutral.** *(Ratified.)* Human-maintained, automated, neuro-symbolic, or
   any other implementation may conform if the properties are satisfied.
3. **Reconciliation cadence is declared, not fixed.** *(Ratified.)* A fixed cadence would be
   simultaneously too frequent for slow-changing systems and too infrequent for fast-changing
   ones. The operator declares the cadence; the framework requires the declaration and the
   reconciliation. Same pattern as AMD-010 (declared scope bound), AMD-011 (declared capability
   properties), and AMD-014 (declared containment scope).
4. **Epistemic distinction at all tiers.** *(Ratified.)* A machine-generated hypothesis
   presented indistinguishably from a verified observation is a false-assurance failure
   regardless of conformance level. A Baseline system must still distinguish "we observed this"
   from "a model proposed this." Depth and sophistication scale with tier; the distinction
   itself does not.
5. **Learned components may propose; they may not authorize.** *(Ratified.)* Same P-2 pattern.
   An ML system may propose a new threat, a missing path, a stale claim, or a coverage gap. It
   SHALL NOT autonomously convert that proposal into authoritative risk, containment, semantic
   authority, or risk-acceptance state.
6. **Coverage failures are explicit, not silent.** *(Ratified.)* An observed adversary path not
   in the threat model is a model-coverage failure, not a non-event. The failure enters governed
   reconciliation.
7. **Threat-model history is append-only.** *(Ratified.)* Superseded claims are annotated and
   retained. The history of what was believed, when, and on what evidence is itself governed
   evidence. Consistent with the OQGF-A and OQGF-P-10.6 append-only discipline.
8. **The amendment does not sell a product through the standard.** *(Ratified.)* No specific
   threat-modeling engine, knowledge base, ML architecture, or vendor is required for
   conformance.

---

## AMD.1 Normative requirements

These requirements add OQGF-P-17 to Section A.P. They do not modify AMD-008, AMD-012, or any
prior amendment; they govern the quality and lifecycle of the threat-model artifact those
amendments consume.

**OQGF-P-17.1 (Threat-Model Assurance).** A threat model used as an OQGF Risk Source under
OQGF-P-10.2 (AMD-008) SHALL be versioned, provenance-bound, and uncertainty-preserving. Each
material version SHALL carry a version identifier, a timestamp, a responsible DAP (OQGF-A-5),
and a declaration of the system scope and adversary scope it claims to cover. A threat model
that is unversioned, undated, unowned, or scope-undeclared does not satisfy this requirement.

**OQGF-P-17.2 (Claim Provenance and Evidence).** Every material Threat-Model Claim SHALL carry
Claim Provenance: the origin of the claim (observation, test, analysis, simulation, learned
proposal, external intelligence, or analyst judgment); the evidence supporting it; the evidence
contradicting it where known; and its confidence or uncertainty. A claim without provenance SHALL
be treated as Hypothesized rather than verified. A claim whose provenance is fabricated,
misattributed, or whose supporting evidence is no longer available SHALL be flagged for
reconciliation.

**OQGF-P-17.3 (Epistemic Distinction).** Every material Threat-Model Claim SHALL carry an
Epistemic State distinguishing at minimum: Observed, Verified, Modeled, Hypothesized, and
Refuted. Machine-generated hypotheses — including claims proposed by ML systems, graph neural
networks, language models, or any learned component — SHALL be distinguishable from verified or
observed facts at all conformance tiers. A system that presents a learned hypothesis
indistinguishably from a confirmed observation does not satisfy this requirement, because
indistinguishable presentation is false assurance. This distinction is required at Baseline, not
only at Enhanced or High-Assurance.

**OQGF-P-17.4 (Continuous Reconciliation).** The threat model SHALL be reconciled against the
attested deployed system state at a declared Reconciliation Cadence appropriate to the system's
rate of change. Reconciliation SHALL verify at minimum: that the system described in the threat
model matches the system actually deployed (architecture, components, dependencies, network,
credentials, capabilities, and trust boundaries); that controls claimed as mitigations are
actually present and functioning; that prerequisites claimed as absent are actually absent; and
that the adversary scope remains appropriate. A threat model reconciled only at initial
deployment or annual audit does not satisfy this requirement for a system that changes
materially between reconciliation points.

**OQGF-P-17.5 (Coverage Failure).** Material observed adversary behavior — an attack path,
technique application, prerequisite exploitation, or external effect — that falls outside the
current Threat-Model Coverage SHALL create an explicit Coverage Failure. A Coverage Failure
SHALL be recorded in Organ 5, entered into the OQGF-P-10 Risk Register (AMD-008) as a risk
source, and subjected to governed reconciliation. An observed adversary path that is not in the
threat model SHALL NOT silently disappear during summarization, model update, or version
transition. Coverage Failures are model-coverage debt: the threat model claimed to represent the
adversary landscape, and reality proved it incomplete.

**OQGF-P-17.6 (Deterministic Authority Over Threat-Model State).** Learned components MAY
propose new threats, missing paths, stale claims, coverage gaps, prerequisite changes, control
failures, and attacker-capability updates. They SHALL NOT autonomously convert those proposals
into authoritative OQGF-P-10 risk state, OQGF-P-13 propagation state, OQGF-P-15 containment
state, OQGF-P-16 semantic-authority state, or OQGF-P-9 risk-acceptance state. Promotion from
proposal to authoritative state SHALL require the deterministic governance path, which validates
provenance, evidence, epistemic state, and DAP authorization. This preserves the OQGF-P-2
invariant: learned components discover; deterministic governance authorizes.

**OQGF-P-17.7 (Attacker Conditioning).** Threat-model claims SHALL be conditioned on explicit
adversary profiles — attacker capability, knowledge, access, tools, objectives, and resources —
rather than an implicit universal adversary. A claim that a path is "feasible" without stating
for which attacker, under what access, with what capability, does not satisfy this requirement.
Attacker profiles MAY be abstract classes (opportunistic external, credentialed insider,
supply-chain, advanced persistent, autonomous AI) but SHALL be declared rather than assumed.

**OQGF-P-17.8 (Reconciliation Against Trajectory and Capability).** For systems governed by
OQGF-P-12 (AMD-011), the threat model SHALL be reconciled against the attested Capability
Envelope (OQGF-P-12.2, OQGF-P-12.3) and the observed Trajectory Record (OQGF-P-12.8).
Capabilities present in the deployed environment but absent from the threat model's system
description are threat-model coverage gaps. Observed actions or effects not predicted by any
modeled path are reconciliation triggers. This reconciliation reuses OQGF-P-13.10 (AMD-012,
Capability–Intent–Trajectory–Risk reconciliation) rather than creating a competing mechanism.

**OQGF-P-17.9 (Versioning and Non-Deletion).** Threat-model versions SHALL be retained in
Organ 5. Superseded claims SHALL be annotated with the superseding version and evidence, not
deleted. The history of what was believed, when, on what evidence, and why it changed is itself
governed evidence — it enables post-incident reconstruction of what the threat model covered at
the time of an incident. Consistent with the OQGF-A and OQGF-P-10.6 append-only discipline.

**OQGF-P-17.10 (Risk and Propagation Linkage).** Material threat-model findings SHALL enter
the OQGF-P-10 Risk Register (AMD-008) as risk sources. Where applicable, downstream
consequences SHALL be represented in the OQGF-P-13 RRPG (AMD-012). Material Coverage Failures
SHALL additionally be assessed for the risk created by the gap itself — the risk that an
unmodeled adversary path was exploitable during the period the model failed to cover it.
Threat-model findings MAY emit OQGF-P-7 Signals (AMD-004) and MAY trigger OQGF-P-15 (AMD-014)
containment through the existing Signal-to-Cap pathway. No second risk register, propagation
graph, signal bus, or containment engine SHALL be created.

---

## AMD.2 Conformance criteria per level

**Baseline (OQGF-B):** Threat models versioned, dated, DAP-owned, and scope-declared
(OQGF-P-17.1); material claims carry provenance (OQGF-P-17.2); machine-generated hypotheses
distinguishable from verified facts (OQGF-P-17.3); a declared Reconciliation Cadence exists
(OQGF-P-17.4); Coverage Failures recorded in Organ 5 and entered into the Risk Register
(OQGF-P-17.5); learned proposals not autonomously authoritative (OQGF-P-17.6); threat-model
history retained (OQGF-P-17.9). Single-PQC-family signatures on threat-model versions acceptable.

**Enhanced (OQGF-E):** All Baseline criteria, plus reconciliation against the attested deployed
system at the declared cadence (OQGF-P-17.4); attacker-conditioned claims (OQGF-P-17.7);
reconciliation against Capability Envelope and Trajectory Record for AMD-011 systems
(OQGF-P-17.8); risk and propagation linkage (OQGF-P-17.10); adversarial testing of at least
one stale claim and one unmodeled path; event-driven reconciliation on material system change.

**High-Assurance (OQGF-H):** All Enhanced criteria, plus dual-PQC-family signatures on
threat-model versions and material claim records per OQGF-R-1; independent verification of
reconciliation completeness; second-DAP review of material Coverage Failure dispositions;
adversarial testing of epistemic-state corruption (hypothesis presented as verified),
provenance fabrication, stale-claim persistence, and silent coverage-gap closure; continuous or
near-real-time reconciliation commensurate with the system's rate of change; periodic replay of
threat-model evidence against Organ 5 records.

---

## AMD.3 Assessment procedures

An auditor SHALL:

1. Request a threat-model version and confirm it carries a version identifier, timestamp,
   responsible DAP, system scope, and adversary scope (OQGF-P-17.1). **This is the
   load-bearing test of this amendment**: it proves the threat model is a governed artifact,
   not an ungoverned document.
2. Select a material claim and confirm it carries provenance, supporting evidence, and epistemic
   state (OQGF-P-17.2, OQGF-P-17.3). Confirm a machine-generated hypothesis is visually and
   structurally distinguishable from a verified observation.
3. Introduce a material system change (add a component, change a network path, add a credential)
   and confirm the threat model is reconciled within the declared cadence (OQGF-P-17.4). Confirm
   the reconciliation verifies that the threat model's system description matches the deployed
   system.
4. Simulate an observed adversary path not present in the threat model and confirm an explicit
   Coverage Failure is created, recorded in Organ 5, and entered into the Risk Register
   (OQGF-P-17.5). Confirm the failure does not silently disappear during a model update.
5. Ask a learned component to promote a hypothesis to verified status and confirm the
   deterministic governance path prevents autonomous promotion (OQGF-P-17.6).
6. Request a claim asserted as "feasible" and confirm it specifies which adversary profile,
   under what access and capability (OQGF-P-17.7).
7. Add a capability to the deployed system that is absent from the threat model and confirm
   the gap is detected as a coverage issue (OQGF-P-17.8).
8. Supersede a threat-model claim and confirm the prior version is annotated and retained,
   not deleted (OQGF-P-17.9).
9. Confirm a material threat-model finding enters the P-10 Risk Register and, where applicable,
   links into the P-13 RRPG (OQGF-P-17.10).
10. At High-Assurance, corrupt a claim's epistemic state (present a hypothesis as verified) and
    confirm the system detects or prevents the corruption.

---

## AMD.4 Control mappings

- **NIST AI RMF:** MAP-1.1, MAP-2.2, MAP-5.1 (context, risk identification, and impact — the
  threat model as a governed MAP input); MEASURE-1.1, MEASURE-2.6 (validity, reliability, and
  the conditions under which the threat model's claims hold); MANAGE-1.2, MANAGE-4.1 (risk
  treatment and post-deployment monitoring — continuous reconciliation); GOVERN-1.2, GOVERN-4.1
  (accountable governance of the threat-model artifact).
- **NIST SP 800-53 Rev. 5:** RA-3 (risk assessment — the threat model as a governed risk
  assessment artifact), RA-5 (vulnerability monitoring — reconciliation against actual
  vulnerabilities), RA-7 (risk response — Coverage Failures as risk inputs), PM-9 and PM-28
  (risk management strategy and risk framing), CA-7 (continuous monitoring — reconciliation
  cadence), SI-4 (system monitoring — observed adversary behavior as reconciliation input),
  SA-11 (developer testing and evaluation — threat-model accuracy), AU-2, AU-3, AU-12 (audit
  content and generation — threat-model evidence and versioning).
- **NIST SP 800-30:** risk assessment methodology — the threat model as a governed artifact
  within the NIST risk-assessment lifecycle.
- **NIST AI 100-2e2025:** adversarial-ML threat classification by lifecycle stage, attacker
  goals, capabilities, and knowledge — the basis for attacker-conditioned claims (OQGF-P-17.7).
- **EU AI Act:** Article 9 (risk management system — threat-model quality as a risk-management
  input); Article 12 (record-keeping — versioned threat-model history); Article 15 (accuracy,
  robustness, and cybersecurity — reconciliation against deployed reality).
- **ISO/IEC 42001:** Clause 6 (risk assessment), Clause 8 (operational controls), Clause 9
  (performance evaluation — reconciliation as performance evidence); Annex A.5, A.6.
- **MITRE ATT&CK / ATLAS lineage:** ATT&CK v19.2 as the established enterprise adversary
  knowledge base; ATLAS as the AI-system extension. The amendment does not require ATT&CK or
  ATLAS but recognizes them as authoritative structured sources that may support conformance.
- **CNSA 2.0:** ML-DSA-87 for threat-model version signatures; dual-family at High-Assurance
  per OQGF-R-1.

---

## AMD.5 Technical architecture (implementation hooks)

AMD-016 introduces no new organ, no new risk register, no new propagation graph, no new signal
bus, no new containment engine, and no new semantic-authority mechanism. It extends `oqgf-core`
with threat-model assurance types and persists evidence in `oqgf-memory` (Organ 5).

### AMD.5.1 Core types

```rust
/// A versioned, provenance-bound, uncertainty-preserving threat-model artifact
/// (OQGF-P-17.1). Governed as an OQGF risk source under P-10.2.
pub struct ThreatModelArtifact {
    pub id: ThreatModelId,
    pub version: ThreatModelVersion,
    pub system_scope: SystemScope,
    pub adversary_scope: Vec<AdversaryProfile>,     // OQGF-P-17.7
    pub claims: Vec<ThreatModelClaim>,
    pub reconciliation_cadence: ReconciliationCadence, // declared (OQGF-P-17.4)
    pub last_reconciled: SystemTime,
    pub owner: DesignatedAccountableParty,           // reuses existing type (OQGF-A-5)
    pub signature: DualSignature,
}

/// A material assertion within the artifact (OQGF-P-17.2, OQGF-P-17.3).
/// Every claim carries provenance and epistemic state.
pub struct ThreatModelClaim {
    pub id: ClaimId,
    pub assertion: ClaimAssertion,
    pub attacker: AdversaryProfileRef,               // conditioned (OQGF-P-17.7)
    pub provenance: ClaimProvenance,                  // OQGF-P-17.2
    pub epistemic_state: ThreatEpistemicState,        // OQGF-P-17.3
    pub confidence: ConfidenceAssessment,
    pub supporting_evidence: Vec<EvidenceRef>,
    pub contradicting_evidence: Vec<EvidenceRef>,
    pub status: ClaimStatus,                          // Active | Superseded | Refuted
}

/// Epistemic classification (OQGF-P-17.3). Distinguishable at ALL tiers.
/// A hypothesis presented as Observed is a conformance failure.
pub enum ThreatEpistemicState {
    /// Directly witnessed in the deployed system or confirmed incident.
    Observed { incident_ref: Option<IncidentRef> },
    /// Tested or independently confirmed.
    Verified { verification_ref: EvidenceRef },
    /// Derived from analysis, simulation, or formal reasoning.
    Modeled { method: AnalysisMethod },
    /// Proposed by a learned system, analyst judgment, or external intelligence
    /// without independent verification. SHALL be distinguishable from Observed
    /// and Verified at all tiers (OQGF-P-17.3).
    Hypothesized { source: ProposalSource },
    /// Contradicted by evidence. Superseding evidence recorded.
    Refuted { superseding: EvidenceRef },
}

/// An observed adversary path not in the threat model (OQGF-P-17.5).
/// Model-coverage debt. Enters Organ 5, the Risk Register, and
/// governed reconciliation. Does not silently disappear.
pub struct CoverageFailure {
    pub id: CoverageFailureId,
    pub observed_path: ObservedPathRef,
    pub threat_model_version: ThreatModelVersion,
    pub gap_description: String,
    pub risk_ref: RiskId,                             // AMD-008 Risk Register entry
    pub recorded_at: SystemTime,
    pub disposition: CoverageFailureDisposition,      // Open | Incorporated | Accepted
}

/// Attacker profile (OQGF-P-17.7). Claims are conditioned on explicit
/// adversary characteristics, not an implicit universal adversary.
pub struct AdversaryProfile {
    pub id: AdversaryProfileId,
    pub name: String,
    pub capability: AdversaryCapability,
    pub knowledge: AdversaryKnowledge,
    pub access: AdversaryAccess,
    pub objectives: Vec<AdversaryObjective>,
    pub resources: ResourceLevel,
}
```

The safety properties are structural. `ThreatEpistemicState` makes the distinction between
`Observed`, `Verified`, `Modeled`, and `Hypothesized` a type-level fact — there is no variant
that blurs the boundary. `CoverageFailure` is a first-class type persisted in Organ 5 — a
coverage gap cannot be silently swallowed by setting a boolean or omitting a log entry. The
`Hypothesized` variant carries a `ProposalSource` identifying the learned system that generated
it — provenance is structural, not a metadata field that can be quietly dropped.

### AMD.5.2 What this closes, and what it does not

This amendment **closes** the following:

- **The ungoverned risk source.** A threat model consumed by AMD-008 must now carry version,
  provenance, ownership, scope, and reconciliation (OQGF-P-17.1).
- **The undistinguished hypothesis.** A machine-generated claim is structurally distinguishable
  from a verified observation at all tiers (OQGF-P-17.3).
- **The stale threat model.** Reconciliation against the deployed system is required at a
  declared cadence; a threat model that describes a system that no longer exists is detected
  (OQGF-P-17.4).
- **The silent coverage gap.** An observed adversary path outside the model creates an explicit
  Coverage Failure that enters the Risk Register and cannot silently disappear (OQGF-P-17.5).
- **The self-authorizing ML proposer.** A learned system can propose threats but cannot promote
  them to authoritative risk state (OQGF-P-17.6).
- **The universal-adversary assumption.** Claims must state which adversary they apply to
  (OQGF-P-17.7).
- **The un-reconstructable threat history.** Superseded claims are retained, enabling post-
  incident reconstruction of what the model covered at the time (OQGF-P-17.9).

This amendment **does not** fully close, and states so honestly:

- **Threat-model completeness.** No requirement can guarantee that a threat model covers every
  possible attack. Coverage Failures make known gaps explicit; they cannot make unknown gaps
  visible. This is the same unknown-unknowns residual as AMD-008, AMD-011, and AMD-012.
- **Claim accuracy.** A claim can carry provenance and epistemic state and still be wrong. A
  "Verified" claim whose verification was flawed is a false positive the framework surfaces for
  review but cannot structurally prevent. Same shape as AMD-010's trainability-profile residual
  and AMD-012's causal-inference residual.
- **Reconciliation completeness.** Reconciliation verifies that the model matches the system
  within the declared scope. Aspects of the system outside the scope — undiscovered services,
  shadow IT, supply-chain depth beyond the SBOM — are not verified. Same shape as AMD-014's
  incomplete-mediation residual.
- **Adversary evolution.** An attacker who develops genuinely novel capabilities between
  reconciliation points may exceed the declared adversary profiles. The framework requires
  declared profiles and reconciliation; it cannot predict what an adversary will invent.
- **Human governance.** Someone must decide what claims matter, what evidence is sufficient,
  what adversary profiles are appropriate, and when a Coverage Failure has been adequately
  addressed. Determinism enforces the governance path; it does not replace judgment.

---

## AMD.6 Traceability

| Requirement | Implementation hook | Existing OQGF dependency |
| --- | --- | --- |
| OQGF-P-17.1 | `oqgf-core::ThreatModelArtifact` (versioned, signed, scoped, DAP-owned) | P-10.2, A-1/A-5, Part C `THREAT_MODEL.md` |
| OQGF-P-17.2 | `ThreatModelClaim::provenance` and `evidence` fields | P-13.3 evidence pattern |
| OQGF-P-17.3 | `ThreatEpistemicState` enum; all-tier distinction | P-13.3 epistemic-state pattern |
| OQGF-P-17.4 | `ReconciliationCadence` (declared); reconciliation against deployed state | P-12.3 attestation; P-13.8 reconciliation triggers |
| OQGF-P-17.5 | `CoverageFailure` type; persisted in Organ 5; enters P-10 Risk Register | P-10.2 risk source; A-1 |
| OQGF-P-17.6 | deterministic governance path for proposal → authoritative state | P-2; P-13.9; P-15.5; P-16.14 |
| OQGF-P-17.7 | `AdversaryProfile` with capability/knowledge/access/objectives | NIST AI 100-2e2025 lineage |
| OQGF-P-17.8 | reconciliation against `CapabilityEnvelope` and `TrajectoryRecord` | P-12.2, P-12.8, P-13.10 |
| OQGF-P-17.9 | append-only `ThreatModelVersion` history in Organ 5 | P-10.6, A append-only |
| OQGF-P-17.10 | findings → P-10 Risk Register → P-13 RRPG; Signals → P-7 → P-15 | P-10, P-13, P-7, P-15 |

---

## AMD.7 Change log

v1.0 — Initial public draft, 21 August 2026. Adds OQGF-P-17 (Threat-Model Assurance) to the
Physiology Layer: governs the quality and lifecycle of the threat-model artifact consumed as an
OQGF Risk Source under AMD-008. Requires versioning, provenance-bound claims, epistemic
distinction between verified facts and machine-generated hypotheses at all conformance tiers,
continuous reconciliation against the attested deployed system at a declared cadence, explicit
Coverage Failures when observed adversary behavior falls outside the model, attacker-conditioned
claims, reconciliation against the AMD-011 Capability Envelope and Trajectory Record,
append-only version history, and risk/propagation linkage through existing AMD-008/AMD-012
mechanisms.

Establishes that learned components may propose threat-model changes but shall not autonomously
convert proposals into authoritative risk, containment, semantic authority, or risk-acceptance
state — the P-2 invariant applied to threat-model governance. Implementation-neutral: a
conforming organization may use human-maintained threat models, conventional attack graphs,
commercial platforms, neuro-symbolic engines, or any combination. The amendment governs the
property the threat-model artifact must carry, not the product that produces it.

Biological alignment grounded in dendritic-cell continuous sampling and immune-memory lifecycle:
the immune system's threat model is living, evidence-based, context-conditioned, and continuously
reconciled against what it encounters. Honestly bounded: biology does not maintain a formal
attack hypergraph; the predictive adversary graph is the engineering construction.

Does not modify AMD-008 (which remains the authoritative Risk Register), AMD-012 (which remains
the authoritative RRPG), AMD-014 (which remains the authoritative containment mechanism),
AMD-015 (which remains the authoritative semantic-authority mechanism), or any prior amendment.
Five residuals named rather than claimed eliminated — threat-model completeness, claim accuracy,
reconciliation completeness, adversary evolution, and human governance — each mapped to the shape
of a prior amendment's residual.

— End of OQGF Amendment 016.
