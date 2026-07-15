# OQGF-1.0 — NORMATIVE AMENDMENT 008
## The Risk Surveillance Requirement: Continuous Identification, Assessment, and Disposition of Risk

**Amendment ID:** OQGF-AMD-2026-008
**Amends:** OQGF-1.0, Section A.P (Physiology Layer). Adds a new requirement, OQGF-P-10.
Does **not** modify OQGF-P-9; it defines the risk-identification and disposition front-half
of which OQGF-P-9 (AMD-006) is the accept-branch back-half, per the OQGF annotation
convention.
**Author:** Jeremy Rose, CEO — Odin's LLC, Wasilla, Alaska
**Date:** 15 July 2026
**Status:** Public draft for NIST, sector regulators, and the Odin's engineering team
**Normative dependencies:** OQGF-A (Organ 5, Memory, for the register of record and the
accountable DAP, OQGF-A-5); OQGF-P-1 (host-harm bound, AMD-002), OQGF-P-5 (autoimmunity /
storm detection as a risk source, AMD-002), OQGF-P-9 (accountable risk acceptance, AMD-006);
OQGF-G-4 and OQGF-M-1 (the two Deterministic Gates, as one risk source among several);
OQGF-M-13 (documented risk requiring DAP acceptance, AMD-001, now given a register of record);
consistent with the per-crate `THREAT_MODEL.md` obligation of Part C.

---

## AMD.0 Front matter

### AMD.0.1 Purpose of this amendment

OQGF-P-9 (AMD-006) governs one moment in the life of one kind of risk: the deliberate,
accountable decision to **proceed past a finding a Deterministic Gate has already caught** —
a quantum-vulnerable component at the Genetic Layer gate (OQGF-G-4) or an unattested actor
at the MHC gate (OQGF-M-1). It does this well: the acceptance is scoped, named to a DAP,
expiring, signed, recorded, and reportable. But it is the *back half* of the *accept branch*
of the risk process, and it presupposes two things the framework does not yet require.

**First, it presupposes the risk was found.** A Deterministic Gate finds exactly two
conserved patterns: a disallowed cryptographic algorithm, and an unattested actor. It finds
nothing else. Model risk — bias, drift, hallucination, degraded accuracy on a shifting
population — is invisible to it. Operational risk, supply-chain risk beyond cryptography,
key-management risk, business and contractual risk, and any risk surfaced by a threat model
rather than a scanner: none of these trips a gate, and the framework provides no required
place to write them down. A risk that is never recorded is never owned, never dispositioned,
and never reviewed.

**Second, it presupposes the only disposition is acceptance.** The standard risk-response
set has four members — **avoid, reduce, transfer, accept** (NIST SP 800-37; ISO/IEC 27005).
OQGF-P-9 specifies the fourth in full and is silent on the other three. An organization that
decides to *remove* a risk source (avoid), *lower* its likelihood or impact (reduce), or
*shift* it to a third party (transfer) has no normative obligation to record that decision,
assign it an owner, or track it to completion.

This amendment supplies the front half. It requires a **Risk Register** — a continuously
maintained catalog of identified risks, each assessed, each owned by a named accountable
party, each carrying exactly one of the four dispositions. Where the disposition is *accept*,
this amendment does not invent a second acceptance mechanism: it routes to OQGF-P-9. The two
requirements compose cleanly — OQGF-P-10 finds, assesses, and decides; OQGF-P-9 is the
accountable form of the one decision to carry a risk that cannot yet be removed.

Two boundaries are stated at the outset, because they define what this amendment is and is
not. The Risk Register is **not a Deterministic Gate**: it does not block builds, and it does
not change the fail-closed behavior of OQGF-G-4 or OQGF-M-1, which stand exactly as
specified. And the Register does not *prevent* risk; it makes risk **visible, owned, and
tracked**. Its assurance is accountability, not enforcement. This is a deliberate choice,
defended in AMD.0.5.

### AMD.0.2 Why this is a Physiology-Layer requirement and not an organ extension

The framework distinguishes **organs** (anatomical structures — what a thing is and does)
from the **Physiology Layer** (OQGF-P, systemic emergent behaviors — how the whole system
acts). Risk identification and disposition is not the function of any one organ. Its inputs
arrive from Organ 1 (a gate finding), Organ 2 (an incident, an autoimmunity signal), Organ 5
(the recorded history the register lives in), and from threat models and external
intelligence that belong to no organ at all. Its output — a disposition — governs how the
whole system carries or sheds a risk. A property whose inputs span every organ and whose
behavior is systemic belongs in OQGF-P, not in a single organ.

This is the same placement, for the same reason, as its sibling OQGF-P-9, which lives in the
cross-cutting namespace precisely because "the same accountability need exists wherever a
fail-closed gate exists" (AMD-006, AMD.0.5). Risk surveillance sits one level above that: the
same identification-and-disposition need exists wherever a risk exists, gate-caught or not.
The requirement therefore takes the next number in the Physiology namespace, OQGF-P-10,
adjacent to the accept-branch requirement it feeds.

### AMD.0.3 The biological basis

The immune system does not wait at its gates. Before any pathogen reaches complement or a
pattern-recognition receptor, the system runs **continuous surveillance**. Dendritic cells
patrol every tissue, sampling antigens and carrying them to the lymph nodes for cataloging.
Natural killer cells inspect every cell they meet against two independent tests — "missing
self" (the absence of the MHC-I an honest cell should display) and "induced self" (the stress
ligands a damaged or infected cell puts up). The system maintains, in effect, a running
catalog of what it has encountered and what state the body is in.

Surveillance is not the same as the gate, and it is not the same as the response. It is the
**finding and the triage** that precede both. And crucially, what surveillance finds is not
met with a single reflex. It is **triaged into a disposition**: ignore it (it is harmless or
self), tolerate it under active regulation (the maternal–fetal and commensal accommodations
of AMD-006), hand it to the adaptive system to be neutralized (reduce), or mark it for
immediate elimination (avoid the threat by destroying its source). The immune system's power
comes as much from *finding and correctly triaging* threats as from the gates that fire on
the two or three patterns it can recognize without thinking.

The translation is exact. The Deterministic Gates (OQGF-G-4, OQGF-M-1) are the reflexive,
conserved-pattern back-end — they fire on the crypto pattern and the attestation pattern and
nothing else, exactly as complement fixes on a foreign surface and asks no further questions.
Risk surveillance is the dendritic-cell-and-NK-cell front-end: it finds the risks the gates
were never watching for, catalogs them, assesses each one, and assigns each a disposition —
avoid, reduce, transfer, or accept — exactly as the immune system triages what its patrols
bring back. A defense that has only gates and no surveillance can see only what its gates are
shaped for; it is blind to everything else moving through the tissue.

### AMD.0.4 Terminology additions

- **Risk** — a condition that could adversely affect the confidentiality, integrity,
  availability, safety, fairness, or accountability of a system in scope, or the organization
  operating it. Broader than a Deterministic-Gate finding: a gate finding is one kind of risk,
  not the definition of the set.
- **Risk Register** — the continuously maintained catalog of identified risks, each recording
  its description and context, an assessment of likelihood and impact, a named Designated
  Accountable Party owner, and exactly one disposition. Recorded in Organ 5 (OQGF-A). The
  surveillance catalog / immune-memory analog.
- **Disposition** — the decided treatment of a risk, exactly one of **Avoid** (eliminate the
  risk source), **Reduce** (lower its likelihood or impact by a mitigation), **Transfer**
  (shift it to a third party by contract or insurance), or **Accept** (deliberately carry it,
  per OQGF-P-9's accountability properties).
- **Residual Risk** — the risk that remains after a Reduce or Transfer disposition is
  executed; itself re-assessed and re-dispositioned.
- **Risk Source** — an origin from which risks enter the Register: a confirmed incident
  (Organ 5 / OQGF-P-5), a threat model, a Deterministic-Gate finding, a supply-chain or
  dependency change, or external intelligence.

### AMD.0.5 Scope, and the relationship to OQGF-P-9 (Accountable Risk Acceptance)

OQGF-P-10 and OQGF-P-9 are the two halves of the risk process, and they must not be
duplicated into two competing mechanisms:

| | OQGF-P-10 — Risk Register | OQGF-P-9 — Risk-Acceptance Entry |
| --- | --- | --- |
| Governs | identification, assessment, and disposition of **all** risk | the **accept** disposition of a Deterministic-Gate finding |
| Scope of risk | any risk (model, operational, supply-chain, business, gate finding) | a specific, still-visible Deterministic-Gate finding |
| Dispositions | all four (avoid, reduce, transfer, accept) | accept only |
| Is a gate? | **No** — a catalog; does not block | operates **at** a Deterministic Gate; keeps the finding visible |
| Relationship | **produces** an accept disposition | **is** the accountable form of that accept, at the gate |

The composition rule is precise. When a risk in the Register is dispositioned **accept**, that
acceptance SHALL carry the accountability properties of an OQGF-P-9 Risk-Acceptance Entry — a
named DAP, a specific scope, an expiry, a PQC signature, an Organ-5 record. Where the accepted
risk **is** a Deterministic-Gate finding, the acceptance SHALL be realized *as* an OQGF-P-9
Risk-Acceptance Entry at that gate (AMD-006), so the gate itself reflects the decision and
keeps the finding visible. Where the accepted risk is **not** a gate finding — a tolerated
model-drift risk, say, that no gate watches — there is no gate to attach to, but the Register
entry SHALL carry the identical accountability structure. OQGF-P-10 therefore *consumes*
OQGF-P-9 for the gate-finding case and reuses its accountability shape for the rest; it does
not introduce a second acceptance mechanism, and it does not modify AMD-006.

### AMD.0.6 Design assumptions requiring confirmation

This amendment makes the following design calls. Each is the fail-safe default; flag any you
wish to change.

1. **The Register is a catalog, not a gate.** OQGF-P-10 does not block builds and does not
   alter the fail-closed behavior of the Deterministic Gates, which stand exactly as
   specified. The safety-critical risks — quantum-vulnerable cryptography, unattested actors
   — are already gated by OQGF-G-4 and OQGF-M-1; the Register covers the far broader risk
   universe those gates were never shaped to catch. Assumed because turning the Register into
   a hard build gate would either paralyze delivery on risks with no coherent block semantics
   (how does a build "fail" on a contractual risk?) or pressure teams to under-report to keep
   the pipeline green — and under-reporting is the one failure a risk register must never
   incentivize. The Register's assurance is completeness, ownership, and tracking, not
   prevention.
2. **Exactly four dispositions, and accept reuses OQGF-P-9.** Every registered risk carries
   exactly one of avoid, reduce, transfer, accept — the canonical, regulator-recognized set
   (NIST SP 800-37, ISO/IEC 27005). Accept reuses the OQGF-P-9 accountability structure.
   Assumed because inventing a fifth disposition or a parallel acceptance mechanism would
   break the mapping to established practice and fragment accountability across two records of
   the same decision.
3. **Identification is continuous, not a point-in-time snapshot.** New risks continuously
   enter the Register from confirmed incidents, threat models, gate findings, dependency
   changes, and external intelligence. Assumed because a register updated only at audit time
   is theater — immune surveillance is a standing function, not an annual inspection.
4. **Every entry is owned by a named DAP.** An unowned risk is an unmanaged risk. Assumed
   because ownership is the property that turns a catalog into accountability, consistent with
   every prior amendment's insistence on a named natural person.

---

## AMD.1 Normative requirements

These requirements add OQGF-P-10 to Section A.P. They do not modify OQGF-P-9; they define the
identification-and-disposition process that feeds it.

**OQGF-P-10.1 (Risk Register).** A conforming system SHALL maintain a Risk Register recording,
for every identified risk in scope: a description and its context; an assessment of its
likelihood and its impact; a named Designated Accountable Party owner (DAP, OQGF-A-5); and
exactly one disposition (OQGF-P-10.3). The Register SHALL be recorded in Organ 5 (OQGF-A). A
risk that is not recorded, not assessed, not owned, or not dispositioned does not satisfy this
requirement.

**OQGF-P-10.2 (Continuous Identification).** Risk identification SHALL be a continuous
function, not a point-in-time exercise, drawing at minimum from: confirmed incidents recorded
in Organ 5, including autoimmunity and storm events (OQGF-P-5); the threat models maintained
per trust boundary (the per-crate `THREAT_MODEL.md` obligation); Deterministic-Gate findings
(OQGF-G-4, OQGF-M-1); supply-chain and dependency changes (OQGF-G-6.2 supply-chain
re-evaluation); and material changes to the system or its operating environment. A Register
that is refreshed only at assessment time does not satisfy this requirement.

**OQGF-P-10.3 (Disposition).** Every registered risk SHALL carry exactly one disposition from
the set {Avoid, Reduce, Transfer, Accept}. Avoid, Reduce, and Transfer SHALL each carry a
tracked treatment plan with an owner and a target date (OQGF-P-10.5). Accept SHALL be expressed
with the accountability properties of OQGF-P-10.4. A risk carrying no disposition, or more than
one, does not satisfy this requirement.

**OQGF-P-10.4 (Accountable Acceptance).** An Accept disposition SHALL carry the accountability
properties of an OQGF-P-9 Risk-Acceptance Entry: a named DAP, a scope specific to the risk (never
a blanket acceptance of a class of risk), an expiry, a PQC signature binding the acceptance to
the issuing DAP (dual-family at High-Assurance per OQGF-M-2), and an Organ-5 record with its
justification. Where the accepted risk is a finding of a Deterministic Gate (OQGF-G-4 or
OQGF-M-1), the acceptance SHALL be realized as an OQGF-P-9 Risk-Acceptance Entry at that gate,
so the gate reflects the decision and the finding remains visible per OQGF-P-9.1. This
requirement introduces no second acceptance mechanism for gate findings and does not modify
AMD-006.

**OQGF-P-10.5 (Tracking to Closure).** Avoid, Reduce, and Transfer dispositions SHALL be
tracked to completion. A treatment plan that is decided but not executed SHALL remain visible in
the Register as an open item until it is completed. On completion of a Reduce or Transfer
disposition, the Residual Risk SHALL be re-assessed and re-dispositioned; a mitigation SHALL NOT
close a risk without an assessment of what remains after it.

**OQGF-P-10.6 (Review, Reporting, and Non-Deletion).** The Register SHALL be reviewed
periodically and SHALL be reportable on demand as a standing inventory of the organization's
identified risks and their dispositions — generalizing the OQGF-P-9.5 accepted-risk inventory to
the full risk set. A risk that is closed, superseded, or re-dispositioned SHALL be annotated and
retained, never deleted, consistent with the OQGF-A append-only discipline: the Register records
not only the risks currently carried but the history of how each was decided.

---

## AMD.2 Conformance criteria per level

**Baseline (OQGF-B):** A Risk Register exists and records description, context, likelihood,
impact, a named DAP owner, and exactly one disposition per risk (OQGF-P-10.1, OQGF-P-10.3); the
Accept disposition carries OQGF-P-9 accountability and, for gate findings, is realized as an
OQGF-P-9 entry (OQGF-P-10.4); the Register is recorded in Organ 5. Single-PQC-family acceptance
signatures acceptable.

**Enhanced (OQGF-E):** All Baseline criteria, plus continuous identification from the named risk
sources (OQGF-P-10.2); Avoid/Reduce/Transfer plans tracked to closure with visible open items
and residual-risk re-assessment (OQGF-P-10.5); a reportable standing inventory of all identified
risks and dispositions subject to periodic review (OQGF-P-10.6).

**High-Assurance (OQGF-H):** All Enhanced criteria, plus dual-PQC-family signatures on every
Accept disposition (ML-DSA + SLH-DSA, consistent with OQGF-M-2); second-DAP review of any Accept
disposition on a high-impact risk; a declared maximum acceptance duration after which
re-acceptance requires fresh justification (consistent with OQGF-P-9 High-Assurance); and
periodic re-assessment of residual risk after every executed mitigation.

---

## AMD.3 Assessment procedures

An auditor SHALL:

1. Request the Risk Register and confirm every entry records description, context, likelihood,
   impact, a named DAP owner, and exactly one disposition (OQGF-P-10.1, OQGF-P-10.3).
   **This is the load-bearing test of this amendment.**
2. Introduce a new risk through a confirmed incident and, separately, through a threat-model
   finding, and confirm both reach the Register without a point-in-time refresh (OQGF-P-10.2).
3. Take an Accept disposition on a genuine Deterministic-Gate finding and confirm it is realized
   as an OQGF-P-9 Risk-Acceptance Entry visible at the gate with the finding still present; take
   an Accept disposition on a non-gate risk and confirm it carries the identical accountability
   structure (OQGF-P-10.4).
4. Take a Reduce disposition, confirm the mitigation is tracked as an open item until executed,
   and confirm the residual risk is re-assessed and re-dispositioned on completion
   (OQGF-P-10.5).
5. Request the standing inventory and confirm it enumerates all identified risks and their
   dispositions (OQGF-P-10.6).
6. Attempt to delete a closed or superseded risk and confirm it is annotated and retained, not
   removed (OQGF-P-10.6).

---

## AMD.4 Control mappings

- **NIST AI RMF:** MAP-1.1, MAP-2.2, MAP-5.1 (context, risk identification, and impact);
  MEASURE-1.1, MEASURE-2.6; MANAGE-1.2, MANAGE-1.3 (risk treatment and documented response),
  MANAGE-2.1; GOVERN-1.2, GOVERN-4.1 (accountable risk governance).
- **NIST SP 800-53 Rev. 5:** RA-3 (risk assessment), RA-7 (risk response — the full
  accept/avoid/mitigate/transfer set), PM-9 (risk management strategy), PM-28 (risk framing),
  CA-5 (plan of action and milestones, for tracked Reduce/Avoid items), AU-2 and AU-10
  (recording and non-repudiation of disposition decisions), CM-3 (recorded change/exception
  control).
- **NIST SP 800-37 (RMF):** the risk-response dispositions — accept, avoid, mitigate, transfer —
  made explicit, owned, tracked, and reviewable. OQGF-P-9 specified *accept*; OQGF-P-10 adds the
  other three and the identification-and-assessment front-half.
- **NIST SP 800-30:** the risk-assessment methodology (likelihood × impact) underlying
  OQGF-P-10.1.
- **ISO/IEC 42001:** Clause 6 (risk assessment and treatment), Clause 8, Clause 9 (review);
  Annex A.5, A.6.
- **ISO/IEC 27005 / ISO 31000 lineage:** the established risk-management cycle — identify,
  assess, treat, monitor, review — of which this requirement is the OQGF expression.
- **CNSA 2.0:** ML-DSA-87 for acceptance-entry signatures; dual-family at High-Assurance per
  OQGF-M-2.
- **Lineage:** consistent with enterprise risk-register practice (identified, assessed, owned,
  dispositioned, tracked, reviewed) and with the object-capability principle that a disposition
  is itself an attributable, signed act.

---

## AMD.5 Technical architecture (implementation hooks)

The Risk Register is a core type (`oqgf-core`), persisted in `oqgf-memory` (Organ 5). Its Accept
disposition reuses the AMD-006 `RiskAcceptance` type unchanged for gate findings, and an
identically-shaped accountable record for non-gate risks; no second DAP type is introduced, the
existing `DesignatedAccountableParty` is reused, and the Deterministic Gates are untouched.

### AMD.5.1 Core types

```rust
/// The continuously maintained catalog of identified risks (OQGF-P-10.1).
/// Persisted in oqgf-memory (Organ 5), append-only: closed and superseded
/// entries are annotated and retained, never deleted (OQGF-P-10.6).
pub trait RiskRegister: Send + Sync {
    /// Record a newly identified risk. Identification is continuous; sources
    /// include incidents (OQGF-P-5), threat models, gate findings, and
    /// dependency changes (OQGF-P-10.2).
    fn record(&self, risk: RiskEntry) -> RiskId;

    /// The standing inventory of all identified risks and their dispositions
    /// (OQGF-P-10.6). Generalizes AMD-006 `RiskAcceptanceRegistry::active`
    /// from the accept subset to the full risk set.
    fn inventory(&self) -> Vec<RiskEntry>;
}

/// One risk in the Register. Assessed, owned, and dispositioned (OQGF-P-10.1).
pub struct RiskEntry {
    pub id: RiskId,
    pub description: String,
    pub context: String,
    pub likelihood: Likelihood,           // OQGF-P-10.1 assessment
    pub impact: Impact,                   // OQGF-P-10.1 assessment
    pub owner: DesignatedAccountableParty,// reuse existing type (OQGF-A-5)
    pub source: RiskSource,               // OQGF-P-10.2 provenance
    pub disposition: Disposition,         // exactly one (OQGF-P-10.3)
}

/// Exactly one of the four canonical risk responses (OQGF-P-10.3).
/// Avoid/Reduce/Transfer carry a tracked plan (OQGF-P-10.5). Accept reuses the
/// AMD-006 accountability structure (OQGF-P-10.4).
pub enum Disposition {
    Avoid   { plan: TreatmentPlan },
    Reduce  { plan: TreatmentPlan, residual: Box<RiskEntry> },
    Transfer{ mechanism: TransferMechanism, residual: Box<RiskEntry> },
    /// For a Deterministic-Gate finding, this Accept SHALL be realized as an
    /// AMD-006 RiskAcceptance at the gate (OQGF-P-10.4), so the gate reflects it
    /// and the finding stays visible (OQGF-P-9.1). For a non-gate risk, the same
    /// accountability shape applies with no gate to attach to.
    Accept  { acceptance: RiskAcceptance },   // AMD-006 type, reused unchanged
}

/// A tracked treatment plan for an Avoid/Reduce/Transfer disposition. Remains an
/// open item in the Register until executed (OQGF-P-10.5).
pub struct TreatmentPlan {
    pub owner: DesignatedAccountableParty,
    pub target: SystemTime,
    pub status: TreatmentStatus,          // Open | Executed
}
```

The composition with AMD-006 is a type-level fact, not a new mechanism: the `Accept` variant
*holds* a `RiskAcceptance`, so an accepted gate finding is the same object the OQGF-P-9 gate
already consumes. The Register adds the front half — identification, assessment, and the other
three dispositions — without duplicating the accept machinery or touching the gates.

### AMD.5.2 What this closes, and what it does not

This amendment **closes** the following:

- **Risks with no place to be recorded.** Every risk in scope — not only the two conserved
  patterns the gates catch — now has a required home, an owner, an assessment, and a disposition
  (OQGF-P-10.1).
- **The missing three dispositions.** Avoid, Reduce, and Transfer now have normative existence,
  tracked plans, and residual-risk re-assessment (OQGF-P-10.3, OQGF-P-10.5); OQGF-P-9 no longer
  stands alone as the only recorded risk decision.
- **Point-in-time risk theater.** Identification is a continuous function fed by named sources,
  not an annual snapshot (OQGF-P-10.2).
- **Orphaned accepted risks.** The AMD-001 OQGF-M-13 "documented risk requiring DAP acceptance"
  and every OQGF-P-9 acceptance now sit in one enumerable Register of record (OQGF-P-10.4,
  OQGF-P-10.6).
- **Silent mitigation drift.** A decided-but-unexecuted mitigation stays visible as an open item
  rather than disappearing into good intentions (OQGF-P-10.5).

This amendment **does not** fully close, and states so honestly:

- **The Register catalogs risks that were identified; it cannot catalog risks no one thought
  of.** Unknown-unknowns remain. Surveillance widens the aperture — incidents, threat models,
  external intelligence — but no register can enumerate what was never seen. This is the same
  shape as the residuals of every prior amendment: the framework reduces the surface and names
  what remains rather than claiming completeness.
- **Disposition quality is a governance judgment the framework cannot certify.** A wrong Accept,
  an under-scoped Reduce, an ill-advised Transfer: each is now named, owned, tracked, and
  reviewable — never silent or anonymous — but whether a given disposition was *correct* is a
  judgment, not a property the framework verifies. This is the same shape as the OQGF-P-9
  residual.
- **The Register is not a gate; it does not prevent.** Its assurance is visibility, ownership,
  and tracking. A DAP who ignores a tracked mitigation, or accepts a risk that should have been
  avoided, is made visible by the Register but is not stopped by it. That is a governance
  failure the framework surfaces for review rather than one it structurally prevents — a
  deliberate boundary (AMD.0.5, AMD.0.6 assumption 1), not an oversight. The Deterministic Gates
  remain the only structural prevention, and they are untouched.

---

## AMD.6 Traceability

| Requirement | Implementation hook |
| --- | --- |
| OQGF-P-10.1 | `oqgf-core::RiskRegister` + `RiskEntry` (assessed, owned, dispositioned); persisted append-only in `oqgf-memory`; reuses `bom::DesignatedAccountableParty` |
| OQGF-P-10.2 | `RiskRegister::record` fed from `oqgf-memory` incidents (OQGF-P-5), `THREAT_MODEL.md` review, gate findings (`CiGate`, `oqgf-mhc`), and supply-chain re-evaluation |
| OQGF-P-10.3 | `Disposition` enum — exactly one of `Avoid` / `Reduce` / `Transfer` / `Accept`; Avoid/Reduce/Transfer carry `TreatmentPlan` |
| OQGF-P-10.4 | `Disposition::Accept` holds the AMD-006 `RiskAcceptance` type unchanged; for a gate finding, realized as an OQGF-P-9 entry via `RiskAcceptanceRegistry::apply` |
| OQGF-P-10.5 | `TreatmentPlan.status` (`Open` until `Executed`); `Reduce`/`Transfer` carry a `residual: RiskEntry` re-assessed on completion |
| OQGF-P-10.6 | `RiskRegister::inventory` standing report; append-only annotation of closed/superseded entries in `oqgf-memory`; periodic-review record |

---

## AMD.7 Change log

v1.0 — Initial public draft, 15 July 2026. Adds OQGF-P-10 (Risk Surveillance) to the Physiology
Layer: a continuously maintained Risk Register that identifies, assesses, owns, and dispositions
all risk in scope — not only the two conserved patterns the Deterministic Gates catch.
Establishes the four canonical dispositions (avoid, reduce, transfer, accept), tracked plans and
residual-risk re-assessment for the first three, and, for accept, reuse of the AMD-006 OQGF-P-9
Risk-Acceptance Entry — realized at the gate for a gate finding, and with identical accountability
for a non-gate risk. Defines OQGF-P-10 as the identification-and-disposition front half of which
OQGF-P-9 is the accept-branch back half; the two compose and OQGF-P-9 is not modified. The
Register is a catalog, not a gate: it makes risk visible, owned, and tracked, and it does not
alter the fail-closed behavior of OQGF-G-4 or OQGF-M-1, which stand exactly as specified. Gives
the AMD-001 OQGF-M-13 documented-risk and every OQGF-P-9 acceptance a single enumerable register
of record, consistent with the OQGF-A append-only discipline. Three residuals are named rather
than claimed eliminated — unknown-unknowns, disposition-quality judgment, and the fact that a
catalog does not prevent — each mapped to the shape of a prior amendment's residual.

— End of OQGF Amendment 008.
