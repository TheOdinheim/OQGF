# OQGF-1.0 — NORMATIVE AMENDMENT 010
## The Explanation Validity Requirement: Bounded Scope, Null Explanations, and Channel Attestation for Quantum-Appropriate Explainability at Scale

**Amendment ID:** OQGF-AMD-2026-010
**Amends:** OQGF-1.0, Section A.5 (Organ 5 — OQGF-A, Memory / 360-Degree Accountability). Adds
new requirements, OQGF-A-8 through OQGF-A-12. Does **not** modify OQGF-A-1 through OQGF-A-7; it
extends the organ that already owns explanation artifacts, per the OQGF annotation convention.
It gives OQGF-A-4 the scope, validity, and channel-integrity properties that requirement
presumes but does not specify.
**Author:** Jeremy Rose, CEO — Odin's LLC, Wasilla, Alaska
**Date:** 25 July 2026
**Status:** Public draft for NIST, sector regulators, and the Odin's engineering team
**Normative dependencies:** OQGF-A-4 (quantum-appropriate explanation artifacts — the requirement
this amendment makes well-defined at scale); OQGF-A-1 (the decision record the artifact
accompanies), OQGF-A-2 (the recorded circuit, calibration snapshot, full empirical sampling
distribution, and reconciliation test result), OQGF-A-5 (the DAP), OQGF-A-6 (re-signing);
OQGF-M-3 (three-way quantum hardware attestation and statistical reconciliation against a
declared noise model — the pattern this amendment reuses); OQGF-R-1 (dual PQC signature families
for evidentiary signatures); A.6.1 (incident response, statistical-reconciliation-failure
trigger); OQGF-P-10 (AMD-008, the Risk Register that receives an unexplained decision);
OQGF-P-9 (AMD-006, accountable acceptance where such a risk is carried).


**Consistency revision — 8 October 2026:** current requirements, tier summaries, and assessments are synchronized with the integrated framework. The [common conformance/signature/retention rules](OQGF-1_0.md#a09-common-interpretation-signature-profiles-and-assessment-limits) apply to this amendment. See the [resolution record](OQGF-1_0.md#synchronization-review). Original IDs and dated decisions are preserved; this is a public-draft maintenance revision, not a new AMD or an implementation pass.

---

## AMD.0 Front matter

### AMD.0.1 Purpose of this amendment

OQGF-A-4 requires quantum-appropriate explanation artifacts to accompany decisions made by
variational or kernel quantum models — dominant Pauli-string contributions for VQC outputs,
kernel attribution for QSVM outputs, or measurement-statistic attribution where applicable. The
requirement is correct, and at the scales at which quantum machine learning is deployed today it
is satisfiable. It nonetheless presumes three properties it does not specify, and each becomes
load-bearing exactly as QML scales into the regime the framework is meant to govern for the next
decade.

**First, it presumes the explanation has a knowable scope.** For an N-qubit system there are 4^N
Pauli strings. At ten qubits that is roughly a million; at fifty it exceeds any classical
enumeration. "Dominant Pauli-string contributions" is therefore a complete description of a
small system and a vanishing sample of a large one — and nothing in the framework requires an
artifact to say which it is. An explanation that covers all observables of weight two, presented
without stating that bound, implies a completeness it does not have. The remedy is not to forbid
partial explanations; the feasibility and coverage of an explanation depend on the model, observable family, and available sampling resources. The remedy
is to require that the bound be **declared and recorded**, so that a reader — an auditor, a
regulator, a DAP — knows exactly what the artifact does and does not cover.

**Second, it presumes the explanation signal exists.** Variational quantum circuits are subject to
**barren plateaus** in particular circuit, cost-function, initialization, and noise regimes: gradient variance may decay exponentially with size (McClean et al., 2018; Cerezo et al., 2021). This does not imply that every observable expectation or every large model vanishes. Explanation validity must be tested for the chosen observable, method, profile, and sampling budget.
The framework currently has no way to record that outcome as anything other than a successful
explanation. This is the most dangerous failure mode in this amendment's scope, because it is
silent: the audit chain would assert that a regulated decision was explained when in fact the
explanation carried no information. **False assurance is worse than acknowledged absence.**

**Third — and this is the sharpest problem — it presumes that a flat explanation means a flat
model.** A vanishing explanation signal has at least two very different causes: the model is in an
expected barren-plateau regime (physics), or the explanation channel has been tampered with,
miscalibrated, or is silently failing (adversarial or operational). Observationally the two are
identical. A framework that cannot distinguish them cannot tell an untrainable model from a
suppressed one, and an adversary who can flatten an explanation channel can render a model's
behavior permanently unexaminable while every record continues to read "explained."

This amendment supplies the three missing properties. It requires explanation artifacts to
**declare their scope bound** (OQGF-A-8); it defines the **Null Explanation** — the honest,
explicitly-marked record of an explanation that carried no information, which SHALL NOT be
recorded as valid, and on which a regulated decision SHALL NOT be acted until a named DAP signs
for it (OQGF-A-9, OQGF-A-10); it requires a **declared trainability profile** reconciled against
observation, reusing the OQGF-M-3 declare-then-test pattern to separate expected physics from
anomaly (OQGF-A-11); and it requires a **Canary Probe** — an analytically known, non-flat control
circuit run through the same explanation pipeline — to attest that the explanation channel itself
is alive (OQGF-A-12).

### AMD.0.2 Why this extends Organ 5 and not the Physiology Layer

Explanation artifacts are Organ 5's property. OQGF-A-4 defines them, OQGF-A-1 records them beside
the decision they explain, OQGF-A-2 records the quantum evidence they are derived from, and
OQGF-A-6 re-signs them across cryptographic generations. The scope, validity, and channel
integrity of an explanation are properties *of that artifact*, produced and stored by the organ
that already owns it. This is the AMD-007 pattern — extend the organ that already owns the
territory — and it is deliberately not the AMD-008/AMD-009 pattern, which placed risk and
personal data in the Physiology Layer because their obligations spanned Organs 1, 2, and 5 with
no single owner. Here there is a single owner. The requirements therefore take the next free
numbers in the Organ 5 namespace, OQGF-A-8 through OQGF-A-12, immediately after the requirements
they qualify.

One consequence of that placement is stated plainly, because it determines the shape of
OQGF-A-10: **Organ 5 is the recorder, not a gate.** The framework's structural prevention lives in
the applicable Deterministic Gates (including G-4, M-1, I-10, and P-12.4). Organ 5's assurance is that the record is
complete, honest, and attributable. The Null Explanation is therefore fail-closed *in the sense
that matters for a recorder* — it refuses to record a non-explanation as an explanation — and its
consequence for action is enforced by the consuming authorization path, which must validate the DAP acknowledgment and current evidence state before action. Recording an acknowledgment alone does not enforce that rule.

### AMD.0.3 The biological basis

The immune system faces this amendment's central problem directly, and its answer is the source
of the mechanism in OQGF-A-12.

A clinician testing a patient's cell-mediated immunity confronts an ambiguity identical to the
one above. The patient is exposed to an antigen and nothing happens. Two very different
conclusions are available: the patient is **anergic** — the immune system is in a state of
expected unresponsiveness — or the patient's response is being **actively suppressed** by a
pathogen or a lesion. The observation is the same in both cases: no response.

The clinical resolution is the **anergy panel**. Alongside the antigen of interest, the clinician
administers **recall antigens** — common antigens (candida, tetanus toxoid, mumps) to which
essentially every immunocompetent person responds. If the recall antigens produce a normal
response, the immune system is demonstrably functional and the flat result on the test antigen is
a true negative — real biology, not machinery failure. If the recall antigens are *also* flat,
the problem is not the antigen at all: **the immune system itself is not responding**, and the
original test result carries no information whatsoever.

The translation is exact and is the novel contribution of this amendment. The **Canary Probe** is
the recall antigen: a small, shallow, analytically known circuit whose explanation is
non-degenerate by construction, run through the same explanation pipeline, on the same device, in
the same session as the job under governance. A correct canary explanation demonstrates that the
channel is alive, and a flat explanation from the real model is therefore a true observation about
the model — an expected trainability regime. A flat canary demonstrates that the **channel** is
not responding, and every explanation produced in that session carries no information and SHALL
NOT be recorded as valid, regardless of what the real model's artifact appears to show. Anergy is
distinguished from suppression by testing the responder, not the stimulus.

The second mechanism, OQGF-A-11, is the framework's own immunological logic reused: the system
declares what response it expects and then tests what it observes, exactly as OQGF-M-3 declares a
noise model and reconciles the empirical sampling distribution against it. A flat signal matching
the declared trainability profile is expected physiology. A flat signal deviating from it is an
anomaly, and anomalies are incidents.

*Novelty status: the proposed anergy-panel analogy and its QML use are not asserted here
to be novel or established prior art. A separate current literature review is required
before making such a claim. The cited classical-shadow and barren-plateau results are
method- and regime-dependent; they do not prove this framework's implementation.*

### AMD.0.4 Terminology additions

- **Explanation Scope Bound** — the declared limit of what an explanation artifact covers:
  the observable weight bound *k*, the estimation method, the sample count, and the confidence
  interval and its individual or simultaneous coverage meaning. The declared method may
  estimate a bounded observable set with stated uncertainty; it is not an exact complete
  description, and it makes no unsupported coverage claim about the remainder.
- **Null Explanation** — an artifact that does not supply an accepted explanation: its
  signal is statistically indistinguishable from zero under A-9, is invalidated by an
  A-11 reconciliation anomaly or A-12 channel failure, or lacks required validity evidence.
  Record Null with a supported cause or pending cause plus an Evidence Gap; never report
  it as Valid. Statistical non-detection does not prove that information is physically absent.
- **Trainability Profile** — the declared expected signal/gradient-variance behavior for a given
  model architecture, qubit count, and device, against which the observed explanation signal is
  statistically reconciled (the OQGF-M-3 declare-then-test pattern applied to explainability).
- **Expected Trainability Regime** — a flat explanation signal that reconciles with the declared
  Trainability Profile: real physics, not an anomaly. Still a Null Explanation.
- **Reconciliation Anomaly** — a flat or distorted explanation signal that deviates from the
  declared Trainability Profile: an incident trigger under A.6.1, not an expected regime.
- **Canary Probe** — an analytically known, shallow, non-degenerate control circuit executed
  through the same explanation pipeline, device, and session as a governed job, whose result provides bounded evidence about explanation-channel function for a declared scope. The recall-antigen analog.
- **Channel Failure** — the condition in which a Canary Probe fails to produce its known
  explanation, indicating that the declared channel check failed; the record SHALL distinguish a confirmed malfunction from an inconclusive or unavailable check. A failed check alone does not prove adversarial compromise or identify the root cause.

### AMD.0.5 Scope, and what this amendment does not require

The AMD-007 boundary is reaffirmed: OQGF requires the *properties* below as conditions of
conformance. It does not mandate a particular estimation library, QML framework, or explanation
product. **Classical shadows** (Huang, Kueng, and Preskill, 2020) are named throughout as the
best-understood method for producing bounded, sample-efficient estimates of low-weight
observables at scale, and are RECOMMENDED, but any method that yields a declared bound, a sample
count, and a stated confidence interval satisfies OQGF-A-8. The framework specifies the honesty of
the artifact, not the mathematics used to produce it.

This amendment does not weaken OQGF-A-4; every artifact that satisfied OQGF-A-4 before continues
to satisfy it, and now additionally declares what it covers and whether it carried information.
It does not convert Organ 5 into a Deterministic Gate (AMD.0.2). And it does not claim to make
large-scale QML explainable: it makes the *limits* of large-scale QML explainability explicit,
recorded, and accountable, which is a different and achievable thing.

### AMD.0.6 Design assumptions requiring confirmation

This amendment makes the following design calls. Each is the fail-safe default; flag any you wish
to change. Assumptions 1, 2, and 3 were ratified by the DAP on 25 July 2026 and are recorded here
as decided.

1. **A Null Explanation is never recorded as valid, and it gates action through DAP
   accountability.** *(Ratified.)* The failure this requirement exists to prevent is the silent
   recording of a meaningless artifact as a successful explanation — an audit chain that asserts a
   decision was explained when it was not. Recording Null is therefore the fail-closed behavior of
   a recorder. Additionally, and stricter than the recorder's minimum, a regulated decision
   carrying a Null Explanation SHALL NOT be acted upon until a named DAP signs an acknowledgment
   (OQGF-A-10). Assumed because an unexplained regulated decision is precisely the class of
   decision that must not proceed anonymously; the acknowledgment makes proceeding a named,
   signed, reviewable act rather than a default.
2. **The Canary Probe is REQUIRED at High-Assurance and RECOMMENDED below, at a declared
   granularity.** *(Ratified.)* The probe consumes shots and therefore money on every execution at
   which it is run. Requiring it at High-Assurance places the cost on the conformance tier already
   provisioning dual-family signatures, HSM-backed keys, and threshold custody. Granularity —
   per-job, per-session, or per-batch — is declared by the operator, because a channel failure is
   a property of a pipeline and a session rather than of an individual job, and session or batch
   granularity retains most of the assurance at a fraction of the cost.
3. **The Explanation Scope Bound is declared by the operator, not fixed by the specification.**
   *(Ratified.)* A fixed weight bound cannot be simultaneously correct for a five-qubit model and a
   hundred-qubit model, and would age out as hardware improves, forcing perpetual amendment. This
   reuses the OQGF-M-3 pattern, which declares a noise model rather than legislating one. The
   residual — an operator who declares a uselessly low bound and passes on a technicality — is
   named explicitly in AMD.5.2 and bounded by DAP accountability, exactly as an over-broad Root
   Intent is bounded in AMD-001 and an over-broad Purpose in AMD-009.
4. **Estimation method is not mandated; classical shadows are RECOMMENDED.** Assumed to keep the
   framework method-neutral and durable as estimation techniques improve, consistent with
   AMD.0.5.
5. **A Channel Failure invalidates the declared scope.** The binding scope is the job, session, or batch declared under A-12, with its pipeline, device, time range, and membership. A session-scoped probe covers the whole declared session; a narrower declared scope is not silently promoted to session scope. Scope SHALL NOT be narrowed after failure to preserve a favorable result; evidence of wider impact SHALL expand the invalidation with a recorded reason. This follows the ratified granularity decision in assumption 2.

---

## AMD.1 Normative requirements

These requirements add OQGF-A-8 through OQGF-A-12 to Section A.5. They do not modify OQGF-A-1
through OQGF-A-7; they specify the scope, validity, and channel-integrity properties that
OQGF-A-4 presumes.

**OQGF-A-8 (Bounded Explanation Scope).** Every quantum-appropriate explanation artifact recorded
under OQGF-A-4 SHALL declare its Explanation Scope Bound: the observable weight bound *k* (or the
equivalent structural limit of the method used), the estimation method, the number of samples, and
the confidence interval at which the estimates hold. An artifact that does not declare its bound
SHALL NOT satisfy OQGF-A-4. The record SHALL identify the covered observable set and whether confidence is
individual or simultaneous, including the declared treatment of multiple comparisons.
An artifact SHALL NOT be presented, formatted, or recorded in a manner
that implies coverage beyond its declared bound. Classical-shadow estimation (AMD.4) is RECOMMENDED
for systems at which direct enumeration of the observable space is intractable; any method
yielding a declared bound, sample count, and confidence interval satisfies this requirement.

**OQGF-A-9 (Null Explanation).** Where the explanation signal is statistically indistinguishable
from zero at the declared confidence level (OQGF-A-8), the artifact SHALL be recorded as a **Null
Explanation**, explicitly marked as such, with its cause recorded as one of: Expected Trainability
Regime (OQGF-A-11), Reconciliation Anomaly (OQGF-A-11), or Channel Failure (OQGF-A-12). A Null
Explanation SHALL NOT be recorded, reported, or exported as a valid explanation, and SHALL NOT be
suppressed or omitted from the Organ 5 record. A system that records an information-free artifact
as a successful explanation does not satisfy OQGF-A-4. If evidence cannot support one
of the three causes, the artifact SHALL remain Null with classification pending and an
explicit Evidence Gap; a missing profile or inconclusive test SHALL NOT be labeled
Expected Trainability Regime. Pending cause is an unresolved evidence state, not a fourth
cause or a valid explanation. A-10 action authorization SHALL remain blocked until the
required cause and acknowledgment evidence are available.

**OQGF-A-10 (Accountability for Unexplained Decisions).** A regulated AI/ML decision whose
explanation artifact is Null is an **unexplained regulated decision**. Such a decision SHALL NOT
be acted upon until a Designated Accountable Party (OQGF-A-5) has signed an acknowledgment
recording the decision reference, the Null cause, and the justification for proceeding; the
acknowledgment SHALL be PQC-signed (dual-family at High-Assurance per OQGF-R-1) and recorded in
Organ 5. The condition SHALL additionally be recorded in the Risk Register (OQGF-P-10, AMD-008);
where the resulting risk is carried rather than remediated, it SHALL be dispositioned Accept with
the accountability properties of OQGF-P-9 (AMD-006). This requirement introduces no new
Deterministic Gate and does not alter OQGF-G-4 or OQGF-M-1; it makes proceeding without an
explanation a named, signed, reviewable act rather than a silent default.

**OQGF-A-11 (Trainability Declaration and Reconciliation).** A conforming system SHALL declare a
**Trainability Profile** for each governed variational or kernel quantum model — the expected
explanation-signal behavior (e.g., gradient or expectation-value variance as a function of qubit
count, circuit depth, and device) — and SHALL statistically reconcile the observed explanation
signal against it, recording the test and its result alongside the artifact. A flat signal supported as consistent with the declared profile under a predeclared
test, uncertainty bound, and adequate sampling SHALL be recorded as an Expected
Trainability Regime. Failure to reject a mismatch with an underpowered test is not sufficient;
inconclusive reconciliation SHALL remain an Evidence Gap under A-9. A flat
or distorted signal that deviates from the declared profile SHALL be recorded as a Reconciliation
Anomaly, SHALL mark the affected artifact Null under A-9, and SHALL trigger the incident-response pathway for statistical reconciliation failure
under A.6.1. This requirement applies the OQGF-M-3 declare-then-test pattern to explainability;
it does not modify OQGF-M-3.

**OQGF-A-12 (Canary Probe / Explanation Channel Attestation).** A conforming system at
High-Assurance SHALL execute a **Canary Probe** — a shallow, analytically known control circuit
whose correct explanation is non-degenerate by construction — through the same explanation
pipeline, on the same device, within the same session as the governed job, at a declared
granularity (per-job, per-session, or per-batch). The scope membership and acceptance tolerance, sample budget, and decision rule SHALL be declared before the governed results are used. The probe's produced explanation SHALL be compared against its known analytic result under that rule. A passing result supplies bounded evidence for that scope and fault model; it does not prove that every job or every failure mode is correct. Where the probe fails to produce its known result,
a **Channel Failure** SHALL be recorded, every explanation artifact produced within that scope
SHALL be recorded as Null with cause Channel Failure (OQGF-A-9), and the incident-response pathway
under A.6.1 SHALL be triggered. The Canary Probe is RECOMMENDED at Baseline and Enhanced. The
probe circuit SHALL NOT be predictable to the point of permitting selective evasion; probe
selection SHALL be varied. A required probe that is missing or inconclusive SHALL leave
channel assurance unresolved and SHALL NOT support a valid-artifact claim. Invalidation
SHALL be appended with references to all affected artifacts; previously signed records
SHALL NOT be overwritten. Consumers and exports SHALL evaluate the latest validity state
and the required acknowledgment before use. A failure discovered after an action SHALL
trigger retrospective incident review and notification to affected governed consumers;
the framework SHALL NOT claim the late check prevented the earlier action.

---

## AMD.2 Conformance criteria per level

**Baseline (OQGF-B):** A-8–A-11 apply to governed quantum explanation artifacts at every tier: scope, method, samples and confidence; explicit Null status with supported cause or an unresolved evidence gap; DAP acknowledgment before action on a classified Null result; and Trainability Profiles with recorded reconciliation. Single-PQC-family acknowledgments are acceptable. A-12 canaries are RECOMMENDED at a declared scope.

**Enhanced (OQGF-E):** All Baseline criteria, with Enhanced audit-record signatures under A-3 and assessment under A.7. Trainability Profiles are already required at Baseline. A-12 canaries remain RECOMMENDED.

**High-Assurance (OQGF-H):** All Enhanced criteria, plus the Canary Probe REQUIRED at a declared
granularity with varied probe selection, Channel Failure invalidating every artifact in scope
(OQGF-A-12); dual-PQC-family signatures on DAP acknowledgments and explanation artifacts
(OQGF-R-1); second-DAP review of any acknowledgment permitting action on an unexplained
high-impact decision; and periodic review of declared Scope Bounds and Trainability Profiles for
continued adequacy.

---

## AMD.3 Assessment procedures

An auditor SHALL:

1. Select a recorded explanation artifact at random and confirm it declares its weight bound,
   estimation method, sample count, and confidence interval, and that its presentation does not
   imply coverage beyond that bound (OQGF-A-8).
2. Induce or select a case in which the explanation signal is statistically indistinguishable from
   zero, and confirm the artifact is recorded as Null with a cause, is not recorded or exported as
   valid, and is not omitted from the record (OQGF-A-9). **This is the load-bearing test of this
   amendment**: it checks, for the exercised case, that the system reports absence of explanation rather than manufacturing
   false assurance.
3. Confirm that a decision carrying a Null Explanation was not acted upon absent a signed DAP
   acknowledgment recording cause and justification, verify the PQC signature chain, and confirm
   the corresponding Risk Register entry exists (OQGF-A-10, OQGF-P-10).
4. Request the declared Trainability Profile for a governed model and the recorded reconciliation
   result; confirm a flat-and-matching signal was classified Expected Trainability Regime and a
   flat-and-deviating signal was classified Reconciliation Anomaly and raised as an incident
   (OQGF-A-11, A.6.1).
5. At High-Assurance, request Canary Probe records for a sampled session and confirm the probe
   produced its known analytic result; confirm the declared granularity; and confirm probe
   selection is varied (OQGF-A-12).
6. Where a canary is required or claimed, inject a deliberate explanation-channel fault (for example, a misconfigured estimator or a
   truncated sample path) and confirm the Canary Probe detects it, that a Channel Failure is
   recorded, that every artifact in scope is marked Null with cause Channel Failure, and that
   incident response is triggered (OQGF-A-12, OQGF-A-9).
7. Confirm that re-signing under OQGF-A-6 preserves the Null marking, its cause, and the declared
   Scope Bound.

---

## AMD.4 Control mappings and scientific basis

- **NIST AI RMF:** MEASURE-2.9 (the model is explained, validated, and documented), MEASURE-2.5
  and MEASURE-2.6 (validity, reliability, and the conditions under which measurement fails),
  MEASURE-3.1 (mechanisms for tracking identified risks over time), MANAGE-4.1 (post-deployment
  monitoring); GOVERN-1.2 and GOVERN-4.1 (accountable governance of a decision proceeding without
  explanation).
- **NIST SP 800-53 Rev. 5:** AU-2 and AU-3 (content of audit records — here, the honesty and
  completeness of the explanation record), AU-10 (non-repudiation of the DAP acknowledgment),
  SI-4 (system monitoring, for the channel-attestation and anomaly pathways), SI-7 (software,
  firmware, and information integrity, for the explanation pipeline itself), CA-7 (continuous
  monitoring), RA-3 and RA-7 (the unexplained-decision risk and its disposition, via AMD-008).
- **NIST AI 100-2 (Adversarial Machine Learning taxonomy):** the explanation channel treated as an
  attack surface in its own right, rather than as trusted instrumentation.
- **EU AI Act:** Article 12 (record-keeping), Article 13 (transparency and provision of
  information to deployers — an explanation whose bound is undeclared is not transparent),
  Article 14 (human oversight — the DAP acknowledgment pathway), Article 15 (accuracy, robustness,
  and cybersecurity, for channel integrity).
- **ISO/IEC 42001:** Clause 9 (monitoring, measurement, analysis, and evaluation); Annex A
  controls for AI system performance monitoring and documentation. **ISO/IEC 23894** for AI risk
  guidance on the unexplained-decision pathway.
- **CNSA 2.0:** ML-DSA-87 for operational signing of artifacts and acknowledgments; dual-family
  (ML-DSA + SLH-DSA) at High-Assurance per OQGF-R-1.
- **Scientific basis (established results, cited as prior art):**
  - *Barren plateaus:* McClean, Boixo, Smelyanskiy, Babbush, and Neven, "Barren plateaus in
    quantum neural network training landscapes," *Nature Communications* 9, 4812 (2018);
    Cerezo, Sone, Volkoff, Cincio, and Coles, "Cost function dependent barren plateaus in shallow
    parametrized quantum circuits," *Nature Communications* 12, 1791 (2021). The basis for
    OQGF-A-11's Expected Trainability Regime.
  - *Classical shadows:* Huang, Kueng, and Preskill, "Predicting many properties of a quantum
    system from very few measurements," *Nature Physics* 16, 1050–1057 (2020). The basis for the
    RECOMMENDED bounded-estimation method under OQGF-A-8.
  - *Anergy panels / recall-antigen testing:* established clinical immunology practice, the
    biological source of OQGF-A-12. Its application to QML explanation-channel attestation is
    an unverified design analogy, with no novelty or prior-art claim (AMD.0.3).

**Mapping boundary:** CNSA references do not make SLH-DSA an NSS-approved algorithm. The dual-family rule is an additional OQGF profile requirement; A.0.9 governs compatibility, algorithm parameters, and evidence roles. A mapping is not external certification.

---

## AMD.5 Technical architecture (implementation hooks)

**Implementation status:** the following interfaces and dependency names are design sketches. They are not compiled code delivered by this repository. Historical references to an external implementation report the source author's context, not a fresh verification of that implementation. Apply the current normative text and A.0.9; an omitted field, enum variant, verifier check, or backend is not a conformance exemption.

Explanation artifacts are produced and stored by `oqgf-memory` (Organ 5), with Pauli-string
decomposition and kernel evaluation computed Python-side through PennyLane/Qiskit and ingested via
PyO3 (Part C, C.3.5 and C.4). This amendment adds scope, validity, reconciliation, and canary
fields to the artifact; it introduces no new organ, no new gate, and no second DAP type — the
existing `DesignatedAccountableParty` is reused, and the OQGF-M-3 reconciliation machinery is
mirrored rather than duplicated.

### AMD.5.1 Core types

```rust
/// A quantum-appropriate explanation artifact (OQGF-A-4), now carrying its
/// declared bound, its validity, its trainability reconciliation, and its
/// channel attestation. Stored in oqgf-memory beside the decision record.
pub struct ExplanationArtifact {
    pub decision_ref: DecisionRef,          // the OQGF-A-1 record explained
    pub scope: ExplanationScope,            // OQGF-A-8 — declared, never implied
    pub validity: ExplanationValidity,      // OQGF-A-9 — Valid or Null
    pub trainability: TrainabilityReconciliation, // OQGF-A-11
    pub canary: Option<CanaryAttestation>,  // OQGF-A-12 (required at High-Assurance)
    pub signature: DualSignature,           // OQGF-R-1 at High-Assurance
}

/// The declared limit of what this artifact covers (OQGF-A-8). An artifact
/// without a scope does not satisfy OQGF-A-4.
pub struct ExplanationScope {
    pub method: EstimationMethod,      // ClassicalShadow | DirectExpectation | Kernel | Other
    pub weight_bound: u8,              // k — declared by the operator, not fixed by the spec
    pub samples: u64,
    pub confidence: ConfidenceInterval,
}

/// OQGF-A-9. A Null artifact is never recorded, reported, or exported as Valid,
/// and is never omitted. Absence of explanation is recorded as absence.
pub enum ExplanationValidity {
    Valid,
    Null {
        cause: Option<NullCause>, // None means pending cause plus a required Evidence Gap; no action
        evidence_gap: Option<EvidenceGapRef>, // must be present while cause is unresolved
        /// OQGF-A-10: the decision SHALL NOT be acted upon until this is present
        /// and signed. None => unexplained and unacknowledged => no action.
        acknowledgment: Option<DapAcknowledgment>,
        /// OQGF-A-10: the corresponding AMD-008 Risk Register entry.
        risk_ref: RiskId,
    },
}

pub enum NullCause {
    /// Flat AND reconciles with the declared Trainability Profile: real physics.
    ExpectedTrainabilityRegime,
    /// Flat or distorted AND deviates from the profile: incident under A.6.1.
    ReconciliationAnomaly,
    /// A declared canary check failed; cause investigation is still required.
    ChannelFailure,
}

/// OQGF-A-11 — the OQGF-M-3 declare-then-test pattern applied to explainability.
pub struct TrainabilityReconciliation {
    pub declared_profile: TrainabilityProfile,
    pub observed_signal: SignalStatistic,
    pub test: StatisticalTest,      // mirrors the M-3 K-S / chi-squared machinery
    pub outcome: TrainabilityOutcome, // Consistent | Deviates | Inconclusive
}

/// OQGF-A-12 — a known-answer circuit providing bounded evidence that the
/// explanation channel produced the expected result for the sampled fault model. Failure invalidates the whole scope, not one job.
pub struct CanaryAttestation {
    pub probe_id: ProbeId,             // varied selection; not predictable
    pub granularity: CanaryScope,      // PerJob | PerSession | PerBatch (declared)
    pub expected: KnownExplanation,    // analytic, non-degenerate by construction
    pub observed: ExplanationDigest,
    pub outcome: CanaryOutcome,        // Attested | ChannelFailure | Unresolved
}
```

The enum distinguishes represented validity states; it cannot stop a producer from falsely constructing `Valid`, and an optional acknowledgment field does not enforce authorization. A conforming consumer must check evidence, scope membership, current append-only invalidations, cause classification, and all required DAP signatures before acting. Producer/consumer validation and negative tests are required to establish that behavior. The sketch is not an implemented enforcement guarantee.

### AMD.5.2 What this closes, and what it does not

This amendment **closes** the following:

- **The undeclared-scope problem.** An explanation artifact now states what it covers — bound,
  method, samples, confidence — so a partial explanation can never imply completeness
  (OQGF-A-8).
- **Silent false assurance.** An information-free artifact is recorded as Null with a cause, never
  as a successful explanation. Validity checks and consumers must enforce that distinction;
  an enum alone cannot do so (OQGF-A-9).
- **The anonymous unexplained decision.** Proceeding on a decision that could not be explained is
  now a named, signed, justified, risk-registered act rather than a default (OQGF-A-10, via
  AMD-008 and AMD-006).
- **The physics-versus-attack ambiguity.** A flat signal is classified against a declared
  Trainability Profile: supported consistency permits the expected-regime classification,
  deviation triggers an incident, and inconclusive evidence remains unresolved (OQGF-A-11).
- **The unexamined explanation channel.** A declared canary supplies a bounded check for
  the exercised channel regime and fault model, with failure and missing evidence explicitly
  affecting artifact validity; it does not guarantee detection of every selective attack (A-12).

This amendment **does not** fully close, and states so honestly:

- **A declared Scope Bound can be set uselessly low.** An operator who declares *k* = 1 produces a
  technically conforming artifact of almost no explanatory value. This is the same residual shape
  as an over-broad Root Intent in AMD-001 and an over-broad Purpose in AMD-009: the declaration is
  honest and recorded, but its *adequacy* is a governance judgment the framework surfaces for
  DAP review and periodic re-examination (High-Assurance) rather than one it can certify. Naming
  the bound does not make the bound wise; it makes an unwise bound visible.
- **The Canary Probe attests the channel for the probe's regime, not universally.** An adaptive
  adversary who can distinguish probe circuits from governed circuits could suppress explanations
  selectively while passing the canary. Varied, non-predictable probe selection (OQGF-A-12) raises
  the cost of that attack; it does not eliminate it. Named, bounded, not solved.
- **Estimation cost depends on the measurement scheme and observable family.** A declared
  low-weight bound may be useful but is not a universal theorem that every higher-weight
  observable is unestimable. Sampling cost, accessible structure, uncertainty, and omitted
  observables must be stated for the actual method and job.
- **A valid explanation is not necessarily a good one.** An artifact may satisfy every requirement
  here — bounded, non-null, reconciled, channel-attested — and still be a poor explanation of the
  decision it accompanies. Explanation *quality* remains a governance and scientific judgment, the
  same residual shape carried by every prior amendment.
- **Trainability Profiles are declared and can be wrong.** A profile that overstates expected
  flatness would classify a genuine anomaly as expected physics. This is the OQGF-M-3 residual
  inherited: a declared model is only as good as its declaration, bounded by DAP accountability
  and periodic review.

---

## AMD.6 Traceability

| Requirement | Implementation hook |
| --- | --- |
| OQGF-A-8 | `oqgf-memory::ExplanationScope` on every artifact; classical-shadow estimator reached Python-side via `oqgf.qsdk` (PennyLane/Qiskit) and ingested through PyO3; bound recorded, never implied |
| OQGF-A-9 | `ExplanationValidity::Null { cause, evidence_gap, .. }` plus producer/consumer validation of the latest validity state; invalidations persist append-only |
| OQGF-A-10 | `DapAcknowledgment` (reuses `DesignatedAccountableParty`, OQGF-A-5) required before action; dual-signed via `oqgf-redundant` at High-Assurance; `risk_ref` into the AMD-008 `RiskRegister` |
| OQGF-A-11 | `TrainabilityReconciliation` mirroring the OQGF-M-3 K-S / χ² machinery in `oqgf-mhc`; `Deviates` routes to the A.6.1 incident pathway |
| OQGF-A-12 | `CanaryAttestation` executed through `oqgf-quantum-broker::{ibm,braket,azure,ionq,quantinuum}` in-session; `ChannelFailure` marks every artifact in the declared `CanaryScope` Null |
| Cross-cutting | `ReSigner` (OQGF-A-6) preserves Null marking, cause, and declared scope across cryptographic generations |

---

## AMD.7 Change log

v1.0 — Initial public draft, 25 July 2026. Adds OQGF-A-8 through OQGF-A-12 to Organ 5, specifying
the scope, validity, and channel-integrity properties that OQGF-A-4 presumes but does not define,
and which become load-bearing as quantum machine learning scales. Requires every explanation
artifact to declare its Explanation Scope Bound — weight bound, method, samples, confidence — so a
partial explanation can never imply completeness (OQGF-A-8). Defines the Null Explanation: an
information-free artifact is recorded explicitly as Null with its cause and is never recorded or
exported as valid, making silent false assurance unrepresentable rather than merely discouraged
(OQGF-A-9). Makes an unexplained regulated decision a named, signed, justified, risk-registered
act: such a decision SHALL NOT be acted upon until a DAP signs an acknowledgment, and the
condition is recorded in the AMD-008 Risk Register and, if carried, accepted under AMD-006
(OQGF-A-10). Separates expected physics from attack by declaring a Trainability Profile and
statistically reconciling the observed signal against it — reusing the OQGF-M-3 declare-then-test
pattern — with deviation routed to A.6.1 incident response (OQGF-A-11). Introduces the Canary
Probe, an analytically known non-degenerate control circuit run through the same explanation
pipeline, device, and session, attesting that the explanation channel itself is alive; a failed
probe marks every artifact in its declared scope Null with cause Channel Failure (OQGF-A-12). The
Canary Probe is the anergy-panel construction from clinical immunology — testing the responder
rather than the stimulus — and its application to QML explanation-channel attestation is believed
novel and is to be literature-verified before publication. Extends Organ 5 without modifying
OQGF-A-1 through OQGF-A-7 and introduces no new Deterministic Gate; OQGF-G-4 and OQGF-M-1 stand
exactly as specified. Five residuals are named rather than claimed eliminated — a uselessly low
declared bound, adaptive evasion of the canary, the physics limit on high-weight observables,
explanation quality as a judgment, and a wrong Trainability Profile — each mapped to the shape of
a prior amendment's residual.

— End of OQGF Amendment 010.

<!-- source-sync:navigation -->
**Integrated reading — 8 October 2026:** this amendment's operative requirements, tier criteria, and assessments are incorporated in [the current framework](OQGF-1_0.md#organ-5). Its identity and historical entries are retained; current text includes the dated consistency corrections. See the [integration map](OQGF-1_0.md#integration-map) and [resolution record](OQGF-1_0.md#synchronization-review). Future changes must update both views together.
