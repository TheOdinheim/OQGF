# OQGF-1.0 — NORMATIVE AMENDMENT 003

The Adaptation Requirement: Affinity Maturation for Incident-Driven Detection Amendment ID: OQGF-AMD-2026-003 Amends: OQGF-1.0, Section A.P (Physiology Layer). Supersedes the deferred OQGF-P-6 obligation introduced as a stub in AMD-002 with full normative content (OQGF-P-6.1 through OQGF-P-6.6). The AMD-002 P-6 stub SHALL be annotated as superseded by this amendment. Author: Jeremy Rose, CEO — Odin’s LLC, Wasilla, Alaska Date: 8 June 2026 Status: Public draft for NIST, sector regulators, and the Odin’s engineering team Normative dependencies: OQGF-A (Organ 5, Memory), OQGF-I (Organ 2, Inflammation), OQGF-P-1 and OQGF-P-3 (AMD-002, self-tolerance); interacts with AMD-001.

## AMD.0 Front matter

### AMD.0.1 Purpose of this amendment

AMD-002 introduced the Physiology Layer and named adaptation (OQGF-P-6) as a
binding obligation, deferring its detail. This amendment supplies that detail.
Organ 5 (Memory) records what happened. Adaptation governs what the system learns
from that record. Without it, every recurrence of a known attack is met with the same
response as the first encounter, and the framework accumulates no defensive
advantage from its own history. The biological immune system does not work that way: a
second exposure is met faster, harder, and with more specificity than the first, because
the system improved between exposures. This amendment makes that improvement a
governed, accountable, tolerance-bounded capability — never an ungoverned self-modification.

### AMD.0.2 The biological basis

After a primary response, B-cells in the germinal center undergo affinity maturation.
Two processes run together. Somatic hypermutation randomly mutates the antibody
gene, producing variant antibodies. Clonal selection then keeps only the variants that
bind the antigen better and lets them proliferate (clonal expansion). Over successive
rounds, binding affinity rises by orders of magnitude. The output is a faster, stronger,
more specific secondary response — and durable memory cells.
The safety-critical detail is this: somatic hypermutation is random, so it can produce a
variant that binds self. The germinal center therefore subjects every matured B-cell to a
tolerance checkpoint — self-reactive variants are culled before release. Improvement
is gated by tolerance. Affinity maturation that produced autoimmunity would be a
catastrophic failure, so biology does not permit it: a better antibody that attacks the
host is discarded, no matter how good its binding.
This maps directly onto OQGF. A refined detector born from an incident is a
hypermutated variant. It is selected by proving it detects the attack class better. And it
SHALL pass the self-tolerance screen (OQGF-P-3) before it is allowed to act —
improvement that increased host harm is discarded, exactly as the germinal center
discards a self-reactive clone.

### AMD.0.3 Terminology additions

Refined Detector — a candidate heuristic detector (tighter pattern, adjusted
threshold, new signature) derived from a confirmed incident to detect that incident’s
attack class faster or more specifically. The hypermutated-variant analog.
Seeding Incident — a DAP-confirmed true positive, recorded in Organ 5, that
authorizes the generation of a Refined Detector.
Evaluation Corpus — an independent set of attack and known-good samples
(distinct from the seeding sample) against which a Refined Detector is selected. The
clonal-selection arena.
Detector Provenance — the signed lineage of a Refined Detector: its seeding
incident, the evaluation corpus version, its self-tolerance screening result, and the
approving DAP.
Maturation Pipeline — the governed process from seeding incident to selected,
screened, approved, activated Refined Detector.

### AMD.0.4 Design assumptions requiring confirmation

This amendment makes the following design calls. Each is the fail-safe default; flag any
you wish to change.
1. Human-gated activation. Autonomous generation of Refined Detectors is
permitted; autonomous activation above Baseline is prohibited and requires DAP
approval (OQGF-P-6.6). Assumed because ungoverned self-modification of a
security control is itself a risk.
2. Independent selection corpus. A Refined Detector is selected against an
Evaluation Corpus separate from the seeding sample, not the seeding sample alone
(OQGF-P-6.2). Assumed to prevent overfitting and single-sample poisoning.
3. Mandatory reversibility. Every activated Refined Detector is versioned and
reversible, and a rollback is itself a recorded event (OQGF-P-6.5). Assumed so a bad
lesson can be undone.

## AMD.1 Normative requirements

These requirements supersede and fully specify OQGF-P-6.
OQGF-P-6.1 (Incident-Seeded Refinement). A Refined Detector MAY be generated
only from a Seeding Incident — a DAP-confirmed true positive recorded in Organ 5.
Unconfirmed, auto-labeled, or heuristically-scored detections SHALL NOT seed
adaptation. This is the first poisoning gate: the system does not learn from events no
accountable party has confirmed are real.
OQGF-P-6.2 (Selection on Independent Evidence). A Refined Detector SHALL be
activated only if it demonstrates improved detection of the Seeding Incident’s attack
class against an Evaluation Corpus that is independent of the seeding sample. A
candidate that improves only on the single seeding sample, or that improves detection
at the cost of degraded coverage elsewhere in the corpus, SHALL be disqualified. This is
clonal selection, and it is the second poisoning gate.
OQGF-P-6.3 (Tolerance-Gated Activation). No Refined Detector SHALL activate until
it passes central-tolerance screening (OQGF-P-3) against the current Self Set. A
refinement that improves detection but raises host harm above the declared bound
SHALL be discarded regardless of its detection gains. Improvement SHALL NOT come at
the cost of self-tolerance. This is the germinal-center tolerance checkpoint and the
binding link to AMD-002.
OQGF-P-6.4 (Detector Provenance). Every Refined Detector SHALL carry signed
Detector Provenance — the Seeding Incident identifier, the Evaluation Corpus version,
the self-tolerance screening result, and the approving DAP — recorded in Organ 5
(OQGF-A). A detector whose provenance cannot be reconstructed SHALL NOT be
active.
OQGF-P-6.5 (Reversibility). Every activated Refined Detector SHALL be versioned
and reversible. A rollback SHALL be a recorded event in Organ 5 carrying its justification
and the acting DAP. The system SHALL be able to return to any prior detector
generation.
OQGF-P-6.6 (No Autonomous Activation above Baseline). At Enhanced assurance
and above, activation of a Refined Detector SHALL require DAP approval. Autonomous
generation and autonomous selection are permitted; autonomous activation is not. At
Baseline, autonomous activation is permitted only for detectors that have passed OQGF-P-6.2 and OQGF-P-6.3 and whose provenance is recorded per OQGF-P-6.4.

## AMD.2 Conformance criteria per level

Baseline (OQGF-B): Refinement seeded only by confirmed incidents (OQGF-P-6.1);
selection on an independent corpus (OQGF-P-6.2); tolerance-gated activation (OQGF-P-6.3); recorded provenance (OQGF-P-6.4). Autonomous activation permitted only
under those gates.
Enhanced (OQGF-E): All Baseline criteria, plus mandatory reversibility with recorded
rollback (OQGF-P-6.5); DAP-approved activation, no autonomous activation (OQGF-P-6.6).
High-Assurance (OQGF-H): All Enhanced criteria, plus dual-PQC-family signatures on
Detector Provenance (ML-DSA + SLH-DSA, consistent with OQGF-M-2); a second-DAP
review of every activated Refined Detector; and periodic re-screening of active learned
detectors against the current Self Set as the baseline evolves.

## AMD.3 Assessment procedures

An auditor SHALL:
1. Attempt to seed a Refined Detector from an unconfirmed detection and confirm the
system refuses it (OQGF-P-6.1).
2. Submit a candidate that improves only on its seeding sample (overfit) and confirm
the selection stage disqualifies it (OQGF-P-6.2).
3. Submit a candidate that improves detection but fails the Self Set screen and confirm
it is discarded, not activated (OQGF-P-6.3). This is the load-bearing test:
improvement never overrides self-tolerance.
4. Select an active Refined Detector and reconstruct its full provenance from Organ 5 —
seeding incident, corpus version, screening result, approving DAP (OQGF-P-6.4).
5. Roll back an active Refined Detector and confirm the prior generation is restored and
the rollback is recorded (OQGF-P-6.5).
6. At Enhanced and above, confirm no path exists to activate a Refined Detector
without DAP approval (OQGF-P-6.6).

## AMD.4 Control mappings

NIST AI RMF: MAP-2.3, MEASURE-2.7 (security and resilience), MANAGE-4.1 (post-incident improvement), MANAGE-2.2.
NIST SP 800-53 Rev. 5: SI-4(2), SI-4(4) (automated analysis), CM-3
(configuration change control, applied to detector updates), CA-7 (continuous
monitoring), RA-5 (vulnerability monitoring), AU-10 (provenance non-repudiation).
ISO/IEC 42001 Annex A: A.6, A.10; continual improvement under Clause 10.
CNSA 2.0: ML-DSA-87 for provenance signatures; dual-family at High-Assurance
per OQGF-M-2.
Cross-discipline lineage: consistent with MLOps model-registry and canary-promotion practice (a new detector is a model change, versioned and promoted
under gates) and with data-poisoning-resistant continual learning.

## AMD.5 Technical architecture (implementation hooks)

The Maturation Pipeline lives in a dedicated surface ( oqgf-adapt , or a module within
oqgf-inflammation ), drawing seeding incidents from oqgf-memory , screening through
the AMD-002 ToleranceController , and writing provenance back to oqgf-memory .

### AMD.5.1 Core types

```rust
/// A confirmed true positive that authorizes refinement (OQGF-P-6.1).
pub struct SeedingIncident {
    pub incident_id: IncidentId,   // recorded in Organ 5
    pub confirmed_by: Dap,         // accountable confirmation
    pub attack_class: AttackClass,
}

/// A candidate refined detector — the hypermutated variant.
pub struct RefinedDetector {
    pub base: DetectorSpec,        // the heuristic being refined
    pub change: DetectorDelta,     // tighter pattern / threshold / signature
    pub generation: u64,           // versioning for reversibility (OQGF-P-6.5)
}

/// Signed lineage required before activation (OQGF-P-6.4).
pub struct DetectorProvenance {
    pub seeding: IncidentId,
    pub corpus_version: CorpusVersion,  // independent evaluation set (OQGF-P-6.2)
    pub screen_result: ScreenPass,      // self-tolerance pass (OQGF-P-6.3 / OQGF-P-3)
    pub approver: Dap,                  // DAP approval (OQGF-P-6.6)
    pub signature: DualSignature,       // ML-DSA (+ SLH-DSA at High-Assurance)
}

pub trait MaturationPipeline: Send + Sync {
    /// Generate a candidate from a confirmed incident. Refuses unconfirmed seeds.
    fn generate(&self, seed: &SeedingIncident) -> Result<RefinedDetector, AdaptError>;
    /// Select against an independent corpus; disqualify overfit / coverage regressions.
    fn select(&self, cand: &RefinedDetector, corpus: &EvaluationCorpus)
        -> Result<SelectionPass, AdaptError>;   // Err(Overfit | CoverageRegression)
    /// Activate ONLY after selection + self-tolerance screen + (above Baseline) DAP approval.
    /// Returns the prior generation handle so activation is reversible (OQGF-P-6.5).
    fn activate(&self, cand: RefinedDetector, prov: DetectorProvenance)
        -> Result<PriorGeneration, AdaptError>; // Err(FailsTolerance | NeedsApproval)
}
```

### AMD.5.2 What this closes, and what it does not

This amendment closes the following:

- **Stagnant response to recurring attacks** — the system now improves detection of confirmed attack classes (OQGF-P-6.1–6.3).
- **Ungoverned self-modification** — every learned detector is selected, tolerance-screened, provenance-recorded, and (above Baseline) DAP-approved before it acts (OQGF-P-6.4, 6.6).
- **Irreversible bad lessons** — every activation is versioned and reversible (OQGF-P-6.5).
- **Learning that breaks self-tolerance** — structurally prevented by the tolerance gate (OQGF-P-6.3), inherited from AMD-002.

This amendment does not fully close, and states so honestly:

- **Adaptation sharpens known classes; it does not invent defense against the genuinely novel.** Detecting an unseen attack class remains the job of the slow/behavioral path, not adaptation. The two are complementary; adaptation makes the known cheaper to catch, not the unknown visible.
- **Tolerance-aware poisoning is reduced, not eliminated.** An adversary who can engineer a falsely-confirmed incident and survive both independent-corpus selection and the self-tolerance screen could in principle teach a subtly harmful detector. The residual is the quality of incident confirmation and the Evaluation Corpus — a governance and data problem, the same shape as the AMD-002 Self Set residual. Its blast radius is bounded by reversibility (OQGF-P-6.5) and the fact that no learned detector can ever touch a Deterministic Gate (AMD-002 OQGF-P-2).

## AMD.6 Traceability

| Requirement | Implementation hook |
|---|---|
| OQGF-P-6.1 | `SeedingIncident` drawn from `oqgf-memory`; `MaturationPipeline::generate` refuses unconfirmed seeds |
| OQGF-P-6.2 | `MaturationPipeline::select` against `EvaluationCorpus`; `Err(Overfit \| CoverageRegression)` |
| OQGF-P-6.3 | `activate` calls AMD-002 `ToleranceController::screen`; `Err(FailsTolerance)` |
| OQGF-P-6.4 | `DetectorProvenance` recorded in `oqgf-memory`; dual-signed at High-Assurance |
| OQGF-P-6.5 | `RefinedDetector::generation` + `PriorGeneration` handle; recorded rollback |
| OQGF-P-6.6 | `activate` returns `Err(NeedsApproval)` above Baseline without DAP sign-off |

## AMD.7 Change log

v1.0 — Initial public draft, 8 June 2026. Supersedes the AMD-002 OQGF-P-6 stub with
full normative content. Specifies incident-seeded, independently-selected, tolerance-gated, provenance-recorded, reversible, human-approved detection refinement (affinity
maturation). Binding safety inheritance: a Refined Detector that fails self-tolerance
(OQGF-P-3) is discarded regardless of detection gains, and no learned detector can act
on a Deterministic Gate (OQGF-P-2). Complements AMD-001 (which gates authority) by
gating learning.
— End of OQGF Amendment 003.
