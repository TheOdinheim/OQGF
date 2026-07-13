# OQGF-1.0 — NORMATIVE AMENDMENT 002

The Self-Tolerance Requirement: The Physiology Layer and the Bound on Host Harm Amendment ID: OQGF-AMD-2026-002 Amends: OQGF-1.0, Part A — adds a new cross-cutting section, A.P (Systemic Properties / Physiology Layer). This amendment does not modify a single organ; it states properties that all five organs SHALL collectively exhibit and individually conform to. Author: Jeremy Rose, CEO — Odin’s LLC, Wasilla, Alaska Date: 8 June 2026 Status: Public draft for NIST, sector regulators, and the Odin’s engineering team Normative dependencies: all five organs — OQGF-G (Organ 1), OQGF-I (Organ 2), OQGF-M (Organ 3), OQGF-R (Organ 4), OQGF-A (Organ 5); interacts with AMD-001.

## AMD.0 Front matter

### AMD.0.1 Purpose of this amendment

OQGF-1.0 specifies five organs. The five organs are the framework’s anatomy — the
parts and what each part does. They do not yet state the framework’s physiology — the
system-wide behaviors that distinguish a living immune system from a list of organs.
The immune system’s defining achievement is not any single organ. It is a set of
emergent properties: it learns from exposure, it coordinates without a central controller,
it stands down after a fight, and — most importantly — it attacks non-self without
destroying the body it protects. A defense that has no bound on the harm it does to
its own host is not an immune system. It is an autoimmune disease.
This amendment introduces the Physiology Layer (Section A.P) and fully specifies its
first and most consequential property: self-tolerance — the bound on the harm OQGF’s
own defenses may inflict on legitimate operations. It establishes three further properties
— adaptation, coordinated signaling, and resolution — as binding obligations to be
specified in full in a later revision.
OQGF-1.0 is built on assumed breach (Organ 2) and zero trust (Organ 3). A framework
built on suspicion needs an explicit, cryptographically accountable limit on that
suspicion. Without one, the framework’s own success criteria push it toward the failure
mode it can least afford to name: a defense so aggressive it blocks the work it exists to
protect. This amendment names that failure mode and bounds it.

### AMD.0.2 The biological basis

The adaptive immune system must attack any non-self molecule without attacking the
body itself. The mechanism that achieves this is tolerance, and it operates in two
stages.
Central tolerance occurs at the site where lymphocytes are made — the thymus for T-cells, the bone marrow for B-cells. Developing cells whose receptors bind too strongly
to self- peptides are deleted or edited before they are ever released. A cell that would
attack the host never enters circulation.
Peripheral tolerance governs cells that have already been released. Regulatory T-cells
(Tregs) actively suppress self-reactive lymphocytes that escaped central screening, and
cells that recognize an antigen without proper costimulation are driven into anergy —
the same mechanism AMD-001 invokes for identity-without-intent. Tolerance, in other
words, is the machinery that makes appropriate suspicion safe.
When tolerance fails, the result is autoimmune disease — multiple sclerosis, type 1
diabetes, rheumatoid arthritis, lupus, Hashimoto’s thyroiditis — the immune system
attacking the body it was built to defend. A second, distinct self-harm failure mode is
the cytokine storm: not a failure of target discrimination, but a failure of proportion — a
response correct in its target yet so large it threatens the host through its sheer
magnitude (severe sepsis, CAR-T cytokine release syndrome). Autoimmunity is the
defense hitting the wrong target. The storm is the defense hitting the right target far too
hard.
One structural point governs everything that follows. Tolerance is primarily a
property of the learned, adaptive layer. Lymphocytes are screened and suppressed
because they are trained. The innate layer — complement, pattern-recognition
receptors, phagocytes — fires on conserved danger patterns (PAMPs) and is not subject
to learned suppression. You do not “train tolerance” into the response to a conserved
pathogen signature; that response fires regardless. This maps directly onto OQGF: the
deterministic gates fire on a conserved danger pattern (a quantum-vulnerable
algorithm) and must remain non-suppressible, while the heuristic detectors are the
trained layer to which tolerance applies.

### AMD.0.3 Terminology additions

Physiology Layer (A.P) — the cross-cutting set of system-wide properties every
organ SHALL collectively exhibit, distinct from any single organ’s function.
Host Harm — the application of a defensive response (denial, quarantine, key
rotation, throttling, or escalation) to a legitimate operation: one that is authorized
and conformant with declared policy. Host harm is the governance analog of self-attack.
Self Set — the declared, versioned corpus of known-good operations and baselines
that represents “self.” Detectors are screened against it before deployment.
Deterministic Gate (Non-Suppressible) — a fail-closed safety control that fires on
a conserved danger pattern: the Genetic Layer crypto/SBOM gate (OQGF-G-4) and
MHC attestation verification (OQGF-M-1). The innate-layer analog. Tolerance SHALL
NOT apply to it.
Heuristic Response (Tolerable) — a graded, behavioral, or statistical detection
(Organ 2 sentinels, cross-hop behavioral reconciliation, anomaly scoring). The
adaptive-layer analog. Tolerance MAY apply to it.
Tolerance Grant — a signed, narrowly scoped, expiring suppression of a confirmed
false positive, issued by a Designated Accountable Party. The Treg analog.
Central Tolerance (governance) — pre-deployment screening of a detector
against the Self Set; the thymic negative-selection analog.
Peripheral Tolerance (governance) — runtime suppression of confirmed false
positives by accountable, recorded, expiring Tolerance Grants.
Autoimmunity (governance) — a sustained rise in host-harm rate; the framework
increasingly blocking legitimate work.
Response Storm (governance) — a graded response whose magnitude itself
threatens host availability (e.g., mass key rotation, broad quarantine); the cytokine-storm analog.

### AMD.0.4 Scope and relationship to AEGIS

OQGF is a normative governance specification: it states what a conforming system
SHALL be. AEGIS is a separate commercial product that implements immune-style
defense at runtime. The distinction is load-bearing for this amendment.
This amendment defines properties a conforming system must exhibit. An operator MAY
use AEGIS, or any other tooling, to satisfy the heuristic-layer properties (for example,
AEGIS-style tolerance training to satisfy peripheral tolerance). But OQGF neither
requires nor depends on AEGIS, and conformance is assessed against the requirements
in this document, not against any product. OQGF remains vendor-neutral by design.
Where this amendment borrows an implementation pattern that resembles a runtime
product, it does so to illustrate satisfiability, never to mandate a vendor.

## AMD.1 Normative requirements

These requirements establish Section A.P. They use a new cross-cutting namespace,
OQGF-P-*, because they belong to no single organ. Requirements OQGF-P-1 through
OQGF-P-5 specify self-tolerance in full. Requirements OQGF-P-6 through OQGF-P-8
establish three further physiology properties as binding obligations whose detailed
normative content is deferred to a future revision; the obligation itself is in force now.
Editorial note (v1.1, 8 June 2026). The “future revision” referenced above has
been issued. OQGF-P-6, P-7, and P-8 are now fully specified in Amendments 003
(Adaptation), 004 (Coordinated Signaling), and 005 (Resolution) respectively. The
deferred stubs below are retained, struck through, and cross-referenced per the
OQGF annotation convention; the operative normative content for these three
properties is the respective amendment.
OQGF-P-1 (Host-Harm Bound / Non-Maleficence). A conforming system SHALL
define host harm per AMD.0.3, SHALL continuously measure its host-harm rate, and
SHALL keep that rate within a declared, documented bound. Disruption of a legitimate
operation is a governance failure of equal standing to a missed threat; it SHALL be
tracked, reported, and reviewed with the same rigor applied to a false negative. A
system that measures only what it blocks, and not what it wrongly blocks, does not
satisfy this requirement.
OQGF-P-2 (Tolerance Scope — the innate/adaptive boundary). Self-tolerance
SHALL apply only to Heuristic Responses. It SHALL NOT apply to Deterministic Gates.
No tolerance mechanism, suppression, exception, or operator action defined anywhere
in OQGF SHALL cause a quantum- vulnerable artifact to pass the Genetic Layer gate
(OQGF-G-4), nor an unattested actor to be admitted past MHC verification (OQGF-M-1).
Deterministic Gates SHALL remain fail-closed and non-suppressible. Tolerance reduces
false alarms on the trained layer; it never opens a confirmed hole on the conserved-pattern layer. This requirement is the safety constraint on which every other
requirement in this amendment depends, and it SHALL be enforced structurally — a
request to suppress a Deterministic Gate SHALL be refused, not honored silently.
OQGF-P-3 (Central Tolerance — pre-deployment self-screening). Before
activation, every Heuristic Response detector SHALL be screened against the declared
Self Set and SHALL NOT be deployed if its host-harm rate against that baseline exceeds
the declared bound (OQGF-P-1). The Self Set version, the screening result, and the
deployment decision SHALL be recorded in Organ 5 (OQGF-A). A detector that fires on
known-good operations is rejected before it ever acts, exactly as a strongly self-reactive
lymphocyte is deleted before it leaves the thymus.
OQGF-P-4 (Peripheral Tolerance — accountable runtime suppression). A
confirmed false positive on a Heuristic Response MAY be suppressed at runtime only by
a Designated Accountable Party (DAP, OQGF-A-5) issuing a Tolerance Grant. Each
Tolerance Grant SHALL be narrowly scoped (to a specific detector and signal or pattern,
never blanket), SHALL carry an expiry, SHALL be PQC-signed binding it to the issuing
DAP, and SHALL be recorded in Organ 5 and subject to periodic review. A Tolerance
Grant SHALL NOT, under any construction, attach to a Deterministic Gate (OQGF-P-2).
Expired or out-of-scope grants SHALL have no effect.
OQGF-P-5 (Autoimmunity and Storm Detection). A conforming system SHALL
monitor for two self-harm failure modes and treat the detection of either as a security
incident in its own right: (a) autoimmunity — a sustained rise in host-harm rate above
the declared bound; and (b) response storm — any single graded response whose
magnitude exceeds a declared host- availability threshold (for example, a key-rotation
or quarantine action above a configured blast radius). On detection of either, the system
SHALL raise it through the Organ 2 (OQGF-I) graded-response path and record it in
Organ 5, on the principle that the defense harming the host is itself an incident, not a
side effect to be tolerated.
⚠ SUPERSEDED IN PART by AMD-003 (8 June 2026). Retained for the record per
the OQGF annotation convention. The OQGF-P-6 obligation remains binding; its full
normative content (OQGF-P-6.1–6.6) now lives in Amendment 003 — Adaptation.
The struck text below is no longer the operative specification.
OQGF-P-6 (Adaptation — affinity maturation) [obligation; full specification
deferred]. A conforming system SHALL be capable of improving detection specificity
from confirmed incidents: a confirmed true positive SHALL be able to produce a refined
detector or threshold that is regression-tested and version-recorded before activation.
This property is distinct from Organ 5, which records what happened; this property
governs learning from the record. Any detector produced by adaptation SHALL itself
pass central-tolerance screening (OQGF-P-3) before activation, so that learning cannot
bypass the host-harm bound. Detailed normative content is deferred; the obligation is in
force.
⚠ SUPERSEDED IN PART by AMD-004 (8 June 2026). Retained for the record per
the OQGF annotation convention. The OQGF-P-7 obligation remains binding; its full
normative content (OQGF-P-7.1–7.6) now lives in Amendment 004 — Coordinated
Signaling. The struck text below is no longer the operative specification.
OQGF-P-7 (Coordinated Signaling — no central command) [obligation; full
specification deferred]. Detection or material state change in any organ SHALL be
capable of propagating a signed signal that adjusts the posture of other organs, without
reliance on a single central controller whose failure would silence coordination. This
generalizes AMD-001’s point-to-point emission (architectural anergy raised to Organ 2
and recorded in Organ 5) into a system-wide property. Detailed normative content — the
signal taxonomy and propagation guarantees — is deferred; the obligation is in force.
⚠ SUPERSEDED IN PART by AMD-005 (8 June 2026). Retained for the record per
the OQGF annotation convention. The OQGF-P-8 obligation remains binding; its full
normative content (OQGF-P-8.1–8.7) now lives in Amendment 005 — Resolution.
The struck text below is no longer the operative specification.
OQGF-P-8 (Resolution — homeostasis / return to baseline) [obligation; full
specification deferred]. Every escalation — a Threat Level raise, a quarantine, a
tightened threshold — SHALL have a defined, recorded de-escalation path and SHALL
return to the declared baseline posture once the triggering condition resolves. A system
that escalates but cannot de-escalate exhibits chronic inflammation, which is itself a
host-harm failure mode under OQGF-P-1. Detailed normative content — resolution
criteria and proof of return-to-baseline — is deferred; the obligation is in force.

## AMD.2 Conformance criteria per level

Baseline (OQGF-B): Host harm defined and measured (OQGF-P-1). Tolerance scope
enforced — Deterministic Gates demonstrably non-suppressible (OQGF-P-2). Peripheral
tolerance via signed, scoped, expiring Tolerance Grants recorded in Organ 5 (OQGF-P-4). Single-PQC-family grant signatures acceptable.
Enhanced (OQGF-E): All Baseline criteria, plus central-tolerance pre-deployment
screening of every heuristic detector against the Self Set (OQGF-P-3); autoimmunity
and storm detection feeding the graded-response path (OQGF-P-5); a defined and
recorded de-escalation path for every escalation (OQGF-P-8).
High-Assurance (OQGF-H): All Enhanced criteria, plus a formally declared and
audited host-harm bound with trend reporting (OQGF-P-1, OQGF-P-5); the adaptation
loop with regression-tested, screened detector updates (OQGF-P-6); coordinated
cross-organ signaling with no single point of coordination failure (OQGF-P-7); Tolerance
Grants dual-PQC-family signed (lattice and hash-based, consistent with OQGF-M-2)
and reviewed by a second DAP.

## AMD.3 Assessment procedures

An auditor SHALL:
1. Inspect the declared host-harm definition and bound, and confirm the system
measures host-harm rate as a first-class metric alongside false-negative rate
(OQGF-P-1).
2. Attempt to issue a Tolerance Grant against a Deterministic Gate — the crypto/SBOM
gate (OQGF-G-4) or MHC attestation (OQGF-M-1) — and confirm the operation is
refused, not silently accepted, and that no path exists to suppress a fail-closed gate
(OQGF-P-2). This is the load-bearing negative test of this amendment.
3. Select a deployed heuristic detector at random and inspect its central-tolerance
screening record in Organ 5: the Self Set version used, the measured host-harm rate
against it, and the deployment decision (OQGF-P-3).
4. Select an active Tolerance Grant and confirm it is narrowly scoped, carries an expiry,
is PQC-signed and bound to a DAP, and is recorded in Organ 5; then replay an
expired grant and confirm it has no effect (OQGF-P-4).
5. Induce a host-harm rate above the declared bound (or simulate a response above
the storm threshold) and confirm the system raises it as an incident through the
Organ 2 graded- response path and records it in Organ 5 (OQGF-P-5).
6. Confirm that a sample escalation has a defined, recorded de-escalation path and
returns to the declared baseline once its trigger clears (OQGF-P-8).

## AMD.4 Control mappings

NIST AI RMF: MEASURE-2.5 (valid and reliable), MEASURE-2.6 (safe), MEASURE-2.11 (managing harmful outcomes), MANAGE-2.1, MANAGE-4.1; GOVERN-1.3 and
GOVERN-4.1 (human oversight and accountable decision-making over
suppressions).
NIST SP 800-53 Rev. 5: SI-4 (system monitoring), SI-10 (information input
validation), CA-7 (continuous monitoring), AU-6 (audit review and analysis), AU-10
(non-repudiation, for signed Tolerance Grants), AC-6 (least privilege, on who may
suppress), SC-5 (denial-of- service protection, with the response storm understood
as self-induced DoS), CP-2 (contingency planning, for availability under self-harm
conditions).
ISO/IEC 42001 Annex A: A.6, A.9; operational monitoring under Clauses 8–9.
CNSA 2.0: ML-DSA-87 for Tolerance Grant signatures; dual-family (ML-DSA + SLH-DSA) at High-Assurance per OQGF-M-2.
Cross-discipline lineage: consistent with detection-theory operating-point
selection (the false-positive / false-negative trade is a chosen point on an ROC
curve, not an accident) and with site-reliability error-budget practice (the host-harm
bound is, in effect, an error budget for false positives, governed and reported rather
than left implicit).

## AMD.5 Technical architecture (implementation hooks)

This section maps the amendment to the OQGF reference implementation (Part C). The
Physiology Layer is cross-cutting, so its core types live in oqgf-core , with enforcement
surfaces in oqgf-inflammation (Organ 2) and records in oqgf-memory (Organ 5).

### AMD.5.1 The structural invariant

The whole amendment rests on OQGF-P-2: tolerance applies to the trained layer, never
to the conserved-pattern layer. The reference implementation SHALL encode this in the
type system, so that suppressing a Deterministic Gate is a refused operation, not a
policy that could be misconfigured. Every defensive response is classified at
construction; a Tolerance Grant can only be constructed against a Heuristic response,
and the controller refuses any grant whose target is Deterministic . This makes the
safety property structural — in the spirit of AMD-001, prevented rather than merely
detected.

### AMD.5.2 Core types (extending oqgf-core)

```rust
/// Classifies every defensive response by whether self-tolerance may apply.
/// This enum is the structural encoding of OQGF-P-2.
pub enum ResponseClass {
    /// Fail-closed safety gate firing on a conserved danger pattern.
    /// Non-suppressible. (OQGF-G-4 crypto/SBOM gate, OQGF-M-1 attestation)
    Deterministic,
    /// Graded / behavioral / statistical detection on the trained layer.
    /// Tolerance Grants may apply. (OQGF-I sentinels, cross-hop reconciliation)
    Heuristic,
}

/// The declared known-good baseline ("self"). Heuristic detectors are screened
/// against it before deployment — central tolerance (OQGF-P-3).
pub struct SelfSet {
    pub version: SelfSetVersion,
    pub corpus_digest: Digest,   // what "self" is, pinned
    pub owner: Dap,              // accountable for the baseline
}

/// A signed, scoped, expiring suppression of a confirmed false positive.
/// The peripheral-tolerance / Treg analog (OQGF-P-4).
pub struct ToleranceGrant {
    pub target: DetectorId,       // a specific Heuristic detector
    pub scope: SuppressionScope,  // narrow: signal / pattern / tenant
    pub dap: Dap,                 // accountable party (OQGF-A-5)
    pub issued: SystemTime,
    pub expiry: SystemTime,       // SHALL expire (OQGF-P-4)
    pub signature: DualSignature, // ML-DSA (+ SLH-DSA at High-Assurance)
}

/// Host-harm measurement vs the declared bound (OQGF-P-1, OQGF-P-5).
pub struct HostHarmReport {
    pub rate: f64,                 // legitimate ops harmed / legitimate ops
    pub bound: f64,                // declared ceiling (OQGF-P-1)
    pub autoimmunity: bool,        // sustained breach of bound (OQGF-P-5a)
    pub storm: Option<StormEvent>, // response exceeding blast radius (OQGF-P-5b)
}

pub trait ToleranceController: Send + Sync {
    /// Attach a Tolerance Grant. SHALL refuse if the target response is
    /// Deterministic (OQGF-P-2) — returns Err, never a silent no-op.
    fn grant(
        &self,
        grant: ToleranceGrant,
        class: ResponseClass,
    ) -> Result<GrantId, ToleranceError>; // Err(NonSuppressibleGate) if Deterministic
    /// Screen a heuristic detector against the Self Set before deployment.
    /// Refuses deployment if host-harm against baseline exceeds bound (OQGF-P-3).
    fn screen(
        &self,
        detector: &DetectorSpec,
        self_set: &SelfSet,
    ) -> Result<ScreenPass, ToleranceError>; // Err(FailsCentralTolerance)
    /// Current host-harm posture (OQGF-P-1, OQGF-P-5).
    fn host_harm(&self) -> HostHarmReport;
}
```

### AMD.5.3 Enforcement algorithm

On any attempt to suppress a detection, the Tolerance Controller SHALL:

1. Confirm the target response is Heuristic. If it is Deterministic, refuse with `NonSuppressibleGate` and emit a signed event to Organ 2 (OQGF-P-2).
2. Confirm the grant is narrowly scoped and carries an expiry; reject blanket or non-expiring grants (OQGF-P-4).
3. Verify the DAP's PQC signature on the grant (OQGF-P-4).
4. Record the grant in Organ 5 (OQGF-A).
5. On each subsequent detection, apply only unexpired, in-scope grants.

Independently and continuously, the host-harm monitor SHALL compute the host-harm rate; on a sustained breach of the bound (autoimmunity) or a single response above the storm threshold, it SHALL raise an incident through the Organ 2 graded-response path and record it in Organ 5 (OQGF-P-5).

### AMD.5.4 What this closes, and what it does not

This amendment closes the following:

- **Silent over-blocking of legitimate work** — now a measured, bounded, reported metric of equal standing to false negatives (OQGF-P-1, OQGF-P-5).
- **The risk that "tolerance" weakens fail-safe** — structurally prevented: Deterministic Gates are non-suppressible by construction, and a request to suppress one is refused, not honored (OQGF-P-2).
- **Unaccountable suppressions** — eliminated: every suppression is a signed, scoped, expiring Tolerance Grant bound to a DAP and recorded in Organ 5 (OQGF-P-4).
- **Detectors that attack known-good operations** — rejected before deployment by central-tolerance screening (OQGF-P-3).

This amendment does not fully close, and states so honestly:

- **Defining "legitimate" is a policy judgment, not a cryptographic one.** Host-harm measurement depends on a correct Self Set. A mislabeled baseline — one that records a malicious operation as "self" — creates a tolerance hole. This is a labeling and governance problem, not a cryptographic one, and it has the same shape as AMD-001's residual: the framework reduces the attack surface to exactly this point and names it. It is mitigated by central-tolerance screening (OQGF-P-3), DAP accountability for the Self Set (AMD.5.2), and the hard guarantee that no mislabeling can ever reach a Deterministic Gate (OQGF-P-2). The worst a bad baseline can do is over-tolerate a heuristic alert; it can never open the crypto gate.
- **Adaptation can be poisoned.** OQGF-P-6 (obligation; deferred) lets the system learn from confirmed incidents. A falsely "confirmed" incident could teach a harmful detector. The obligation already requires every learned detector to pass central-tolerance screening (OQGF-P-3) before activation, but the full poisoning-resistance treatment is deferred to the revision that specifies OQGF-P-6 in detail. It is named here rather than left implicit.
- **OQGF-P-6, P-7, and P-8 are obligations, not yet full requirements.** Their detailed normative content, conformance tests, and implementation hooks are deferred. The obligation binds now; the specification follows.

## AMD.6 Traceability

| Requirement | Implementation hook |
|---|---|
| OQGF-P-1 | `oqgf-core::HostHarmReport`; `ToleranceController::host_harm` |
| OQGF-P-2 | `oqgf-core::ResponseClass`; `ToleranceController::grant` returning `NonSuppressibleGate` on Deterministic |
| OQGF-P-3 | `ToleranceController::screen` against `SelfSet`; screening record in `oqgf-memory` |
| OQGF-P-4 | `oqgf-core::ToleranceGrant` (scoped, expiring, dual-signed); grant record in `oqgf-memory` |
| OQGF-P-5 | host-harm monitor → `oqgf-inflammation` graded response; incident record in `oqgf-memory` |
| OQGF-P-6 | (deferred) adaptation pipeline; learned detectors re-enter screen (OQGF-P-3) |
| OQGF-P-7 | (deferred) generalizes AMD-001 signed-event emission across all organs |
| OQGF-P-8 | (deferred) de-escalation path + return-to-baseline proof in `oqgf-inflammation` |

## AMD.7 Change log

v1.0 — Initial public draft, 8 June 2026. Introduces the Physiology Layer (Section A.P)
and the OQGF-P-* namespace. Fully specifies self-tolerance (OQGF-P-1 through OQGF-P-5): the host-harm bound, the non-suppressible-gate boundary that confines
tolerance to the trained layer, central and peripheral tolerance, and autoimmunity/storm
detection. Establishes adaptation (OQGF-P-6), coordinated signaling (OQGF-P-7), and
resolution (OQGF-P-8) as binding obligations with detailed specification deferred. The
load-bearing safety constraint is OQGF-P-2: no tolerance mechanism may cause a
quantum-vulnerable artifact to pass the Genetic Layer gate or an unattested actor to
pass MHC verification. Complements AMD-001: where AMD-001 makes the system
appropriately suspicious (architectural anergy on unverified intent), AMD-002 bounds
that suspicion so it cannot metastasize into autoimmunity.
v1.1 — 8 June 2026. Annotated the three deferred obligations as superseded in part:
OQGF-P-6, P-7, and P-8 are now fully specified in Amendments 003 (Adaptation), 004
(Coordinated Signaling), and 005 (Resolution). Per the OQGF annotation convention, the
original stub text is retained, struck through, and cross-referenced rather than deleted
or rewritten. The self-tolerance core (OQGF-P-1 through P-5) is unchanged. No
normative requirement was removed.
— End of OQGF Amendment 002.
