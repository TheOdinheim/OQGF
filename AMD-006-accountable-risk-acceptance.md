# OQGF-1.0 — NORMATIVE AMENDMENT 006
## The Accountable Risk Acceptance Requirement: Recorded, Non-Suppressing Acceptance of a Deterministic-Gate Finding

**Amendment ID:** OQGF-AMD-2026-006
**Amends:** OQGF-1.0, Section A.P (Physiology Layer). Adds a new requirement, OQGF-P-9.
The 8 October 2026 consistency revision synchronizes the acceptance boundary with
OQGF-P-2, G-4, M-1, I-10, and P-12.4. OQGF-P-4 remains the separate heuristic-tolerance mechanism.
**Author:** Jeremy Rose, CEO — Odin's LLC, Wasilla, Alaska
**Date:** 10 June 2026 (v2, reconciled against the Genetic Layer reference implementation
as built through hardening round R6)
**Status:** Public draft for NIST, sector regulators, and the Odin's engineering team
**Normative dependencies:** OQGF-G (Organ 1, Genetic Layer), OQGF-M (Organ 3, MHC),
OQGF-A (Organ 5); OQGF-P-1 (host-harm bound, AMD-002), OQGF-P-2 (tolerance scope /
non-suppressible gate, AMD-002), OQGF-P-4 (peripheral tolerance, AMD-002);
OQGF-M-13 (least-privilege root scoping / documented risk requiring DAP acceptance,
AMD-001).


**Consistency revision — 8 October 2026:** current requirements, tier summaries, and assessments are synchronized with the integrated framework. The [common conformance/signature/retention rules](OQGF-1_0.md#a09-common-interpretation-signature-profiles-and-assessment-limits) apply to this amendment. See the [resolution record](OQGF-1_0.md#synchronization-review). Original IDs and dated decisions are preserved; this is a public-draft maintenance revision, not a new AMD or an implementation pass.

---

## AMD.0 Front matter

### AMD.0.1 Purpose of this amendment

OQGF-P-2 (AMD-002) requires non-suppression, valid evidence, and deterministic authorization. Its former absolute prohibition on proceeding despite any gate finding conflicted with this amendment's accepted-risk outcome. The 8 October 2026 revision resolves that conflict explicitly: eligible policy findings may be accepted under P-9, but missing identity, invalid evidence, absent intent authority, and binding external prohibitions may not be bypassed.

In operating a real deterministic gate, a second, legitimate need appears that OQGF-P-2
does not by itself address: an organization sometimes must **knowingly proceed past a
true, detected finding** — a dependency that is genuinely quantum-vulnerable but cannot
yet be removed, accepted deliberately for a bounded period by an accountable party. The
original 10 June source describes a Genetic Layer implementation doing this through an allow-list
(`oqgf.allow.toml`): entries that permit the build to proceed despite a still-detected
quantum-vulnerable component.

**Historical implementation context (10 June 2026; not re-verified here).** The source reported that the reference implementation preserved findings as follows. An accepted
component is **not** removed from the Cryptographic Bill of Materials; it remains present,
still flagged quantum-vulnerable, rerouted only from the blocking list into a separate
disclosure list, and recorded in the signed CBOM and the machine-readable policy result.
Detection is never suppressed. What the implementation does **not** yet do is *say so where
a human will see it*: an accepted-risk build prints the same `PASSED` banner, the same
`Violations: 0`, and the same exit code as a genuinely clean build. The carried risk is in
the artifacts but silent on the console. This amendment closes that gap and fixes the
behavior as normative.

This reconciles an apparent contradiction with OQGF-P-2 explicitly rather than leaving it
implicit. The resolution rests on a single distinction:

- **Suppression** removes or hides a finding. After suppression, the finding is absent
  from output, or the verdict is indistinguishable from one in which the finding never
  existed. OQGF-P-2 forbids this on a Deterministic Gate. OQGF-P-4 confines tolerance
  (which is suppression of a heuristic false positive) to the trained layer for the same
  reason.
- **Accountable Risk Acceptance** does not remove or hide anything. The finding remains
  fully visible in the Cryptographic Bill of Materials and in the gate's output; the
  verdict is visibly **not** a clean pass; and an accountable party has recorded a scoped,
  expiring, signed decision to proceed despite the visible finding.

Suppression makes the gate lie. Risk acceptance keeps the gate honest and attaches a name
to the decision to proceed anyway. The first is forbidden on a Deterministic Gate; the
second is permitted **only when it preserves the finding and has valid exception authority under P-9.2**. This amendment defines
the second mechanism, gives it the accountability properties of an OQGF-P-4 Tolerance
Grant without its suppression semantics, and states the bright line that keeps the two
from ever being confused.

### AMD.0.2 The biological basis

The innate immune system's recognition of conserved danger patterns is not subject to
tolerance the way self-antigens are. Complement fixes on a foreign surface; pattern
receptors fire on pathogen-associated molecular patterns. These are the biological
deterministic gates, and they do not negotiate.

Yet the body does, in specific and tightly governed circumstances, **proceed in the
continued presence of recognized non-self without erasing the recognition.** The
maternal–fetal interface is the clearest example. The fetus is semi-foreign and is
**recognized** as such — the antigens are present and seen; recognition is not deleted.
What the body mounts is not blindness but a **deliberately regulated, locally scoped,
time-bounded, actively maintained accommodation**: regulatory T-cells, HLA-G expression,
local immunomodulation. The accommodation is scoped to that tissue and that period; it
does not disable innate recognition anywhere else in the body; and it is reversible — when
the regulation lapses, defense resumes, with pre-eclampsia and fetal loss as the failure
modes. The commensal microbiome is governed the same way: trillions of recognized foreign
organisms are accommodated by active, bounded regulation (secretory IgA, the mucus
barrier, spatial segregation, regulatory T-cells), and the **same** organisms trigger full
inflammation the moment that barrier is breached. In neither case is foreignness erased.
The recognition stands; a scoped, conditional, reversible decision not to attack is layered
on top of it.

The analogy motivates the design below; it is not an engineering proof. Accountable Risk Acceptance is not suppression of detection — the
quantum-vulnerable finding is still recognized and still visible. It is a scoped,
time-bounded, accountable, reversible decision to proceed in its continued presence, which
does not disable the gate for anything else and which lapses on expiry back into blocking.

### AMD.0.3 Terminology additions

- **Deterministic Gate** — as defined in OQGF-P-2: a fail-closed, non-suppressible control.
  The set includes G-4, M-1, I-10, P-12.4, and other explicitly designated gates;
  each retains its own non-waivable evidence and authorization conditions.
- **Suppression** — any mechanism whose effect is that a finding is absent from the
  system's output, or that the verdict produced is indistinguishable from a verdict
  produced when the finding did not exist. Tolerance (OQGF-P-4) is suppression of a
  heuristic false positive.
- **Accountable Risk Acceptance** — a recorded decision, by a Designated Accountable Party,
  to proceed past a specific, still-visible Deterministic-Gate finding, under which the
  finding remains present in output and the verdict remains visibly distinct from a clean
  pass.
- **Risk-Acceptance Entry** — the signed, scoped, expiring record of one Accountable Risk
  Acceptance, bound to a named DAP and recorded in Organ 5. The concrete instance in the
  reference implementation is one accepted entry in `oqgf.allow.toml`, upgraded to carry the
  properties this amendment requires.
- **Accepted-Risk Verdict** — a gate verdict indicating the gate is proceeding while
  carrying one or more accepted risks, distinguishable by construction from a clean verdict.

### AMD.0.4 Scope and relationship to OQGF-P-4 (Tolerance)

OQGF-P-4 and OQGF-P-9 are siblings with one decisive difference, and they must never be
collapsed:

| | OQGF-P-4 — Tolerance Grant | OQGF-P-9 — Risk-Acceptance Entry |
| --- | --- | --- |
| Acts on | a **heuristic** response | a **deterministic** gate finding |
| Effect on the finding | **suppresses** it (false positive made to go away) | **does not suppress** — finding stays fully visible |
| Effect on the verdict | the alert no longer fires | verdict is visibly **not** a clean pass |
| May attach to a Deterministic Gate? | **No** (OQGF-P-2) | **Only to eligible policy findings with valid exception authority** (P-9.2) |
| Shared accountability properties | scoped, expiring, PQC-signed, DAP-issued, Organ-5-recorded | scoped, expiring, PQC-signed, DAP-issued, Organ-5-recorded |

The accountability properties are identical by design. The semantics are opposite: a
Tolerance Grant removes a false alarm; a Risk-Acceptance Entry preserves a true finding and
records who chose to proceed past it. This is the load-bearing distinction of this
amendment.

### AMD.0.5 Design assumptions requiring confirmation

This amendment makes the following design calls. Each is the fail-safe default; flag any you
wish to change.

1. **Distinguishable verdict, with a conditional promote code.** The human-readable and
   structured reports SHALL retain every finding and distinguish Clean, AcceptedRisk,
   and Blocked. Exit 0 is required for Clean or for AcceptedRisk only when every blocker
   has an eligible, current, authorized P-9 entry and every non-waivable prerequisite
   passes. Any remaining blocker requires the block exit status. A DAP signature alone
   is not sufficient authorization. The historical renderer example motivates visible
   disclosure; it is not evidence that the current gate satisfies this contract.

2. **Risk acceptance is its own register, reusing existing types.** A Risk-Acceptance Entry
   is neither a Tolerance Grant (OQGF-P-4) nor a Self Set member (OQGF-P-3). The allow-list
   maps to a distinct `RiskAcceptanceRegistry`. The accountable-party type already exists in
   the reference implementation (`DesignatedAccountableParty` in `oqgf-core::bom`) and SHALL
   be reused rather than duplicated. The implementation already carries an `accepted_risk`
   field on each component; this amendment enriches what that acceptance records, it does not
   invent the routing. Assumed because conflating acceptance with tolerance or self-set would
   blur the OQGF-P-2 / P-4 boundary the framework depends on, and because minting a second DAP
   type would fragment accountability.
3. **Applies to all Deterministic Gates.** OQGF-P-9 governs acceptance at both OQGF-G-4
   (crypto) and OQGF-M-1 (attestation), since both are Deterministic Gates under OQGF-P-2.
   This shared placement does not make every failure waivable. At M-1, only an
   otherwise authenticated actor's eligible policy finding may be accepted; absent,
   forged, expired, or unverifiable identity attestation remains blocking. The same
   eligibility rule applies to the other explicitly designated gates.
4. **Full P-4-equivalent accountability is mandatory, not optional.** Every entry SHALL
   carry a named DAP, a specific scope, an expiry, a PQC signature, and an Organ-5 record.
   The allow-list entries described in the historical source carried only a reason string; this amendment makes the
   other four properties mandatory. Assumed because an exception without an accountable
   party, an expiry, or a signature is an unaudited backdoor, not an accepted risk.

---

## AMD.1 Normative requirements

These requirements add OQGF-P-9 to Section A.P. The current text is synchronized with
P-2's exception boundary; P-4 remains a separate mechanism for heuristic false positives.

**OQGF-P-9.1 (Non-Suppression / Visibility Preserved).** A Risk-Acceptance Entry SHALL NOT
remove, mask, or hide the finding it accepts. The accepted finding SHALL remain present in
the relevant inventory or evidence record (the CBOM for cryptographic findings) and in the gate's output. The gate's **human-readable
report** SHALL distinguish a clean result from a result that is proceeding while carrying one
or more accepted risks, naming the accepted findings; it SHALL NOT present an accepted-risk
build as indistinguishable from a clean build. In the command-line promote/block contract,
if there are no blocking findings, or every blocking finding has a valid, eligible
acceptance, and all non-waivable prerequisites pass, the gate SHALL return the promote
code (0). Otherwise it SHALL return the block status; the required distinction is in the report
and the structured output, not the exit code. No Risk-Acceptance Entry SHALL, under any
construction, cause a quantum-vulnerable artifact to produce a *verdict* indistinguishable
from one in which no quantum-vulnerable artifact were present. This requirement is what
permits Accountable Risk Acceptance to attach to a Deterministic Gate without violating
OQGF-P-2, and the carrying-accepted-risk state SHALL be a distinct, named result, not a
clean pass with the risk recorded only where no operator will see it.

**OQGF-P-9.2 (Accountable Risk-Acceptance Entry).** A decision to proceed past a
Deterministic-Gate finding SHALL be expressed as a Risk-Acceptance Entry that is: scoped to
a specific finding by the exact affected object, action, resource, or component identity
and the precise finding identifier/advisory or reason (never a
blanket acceptance of a class such as "all quantum-vulnerable components"); bound to a named
Designated Accountable Party (DAP, OQGF-A-5); carrying an expiry; PQC-signed binding the
acceptance to the issuing DAP (dual-family at High-Assurance per OQGF-M-2); and recorded in
Organ 5 (OQGF-A) with its justification. An entry lacking any of these properties SHALL have
no effect. The signed entry SHALL identify the governing exception-policy version and
the issuing DAP's authority for the specific finding, action, target, and environment.
The gate SHALL verify that policy permits this class of exception before applying it.
Missing/invalid required signatures, identity, intent, or custody evidence; non-waivable
legal or contractual restrictions; and required containment Resolution SHALL NOT be
overridden. Acceptance does not confer conformance with an unmet requirement. It SHALL
be recorded against the relevant inventory or evidence object; CBOM references apply to
cryptographic findings, not indiscriminately to every kind of gate.

**OQGF-P-9.3 (Expiry and Reversion).** An expired or out-of-scope Risk-Acceptance Entry
SHALL have no effect, and on expiry the accepted finding SHALL revert to blocking exactly as
if no entry had existed. Acceptance is a bounded, renewable decision, never a permanent
waiver. Re-acceptance SHALL be a fresh, separately recorded decision, not an automatic
renewal.

**OQGF-P-9.4 (Boundary Against Tolerance).** A Risk-Acceptance Entry under OQGF-P-9 is not a
Tolerance Grant under OQGF-P-4 and SHALL NOT be construed, recorded, or implemented as one.
No mechanism SHALL permit a Risk-Acceptance Entry to be used to suppress (remove or hide) a
finding, and no mechanism SHALL permit a Tolerance Grant to attach to a Deterministic Gate
(reaffirming OQGF-P-2). The two registers SHALL be distinct, and a single decision SHALL NOT
be expressible as both.

**OQGF-P-9.5 (Review and Reporting).** Risk-Acceptance Entries SHALL be subject to periodic
review on the same footing as OQGF-P-4 Tolerance Grants, and the standing inventory of
currently active accepted risks SHALL be reportable on demand. This operationalizes the
OQGF-P-1 obligation that a host-affecting decision be tracked, reported, and reviewed: an
accepted quantum-vulnerable component is a carried risk, and a system that cannot enumerate
the risks it is currently carrying does not satisfy OQGF-P-1.

---

## AMD.2 Conformance criteria per level

**Baseline (OQGF-B):** P-9.1–P-9.5 apply: eligibility under declared exception policy; a distinct accepted-risk result; visible findings; scoped, DAP-bound, expiring PQC-signed entries; expiry reversion; separation from tolerance; and a periodically reviewed, reportable register. Single-PQC-family acceptance signatures are acceptable.

**Enhanced (OQGF-E):** All Baseline criteria, assessed under A.7. Register separation and review are already mandatory at Baseline.

**High-Assurance (OQGF-H):** All Enhanced criteria, plus dual-PQC-family signatures on every
Risk-Acceptance Entry (ML-DSA + SLH-DSA, consistent with OQGF-M-2); second-DAP review of any
acceptance of a quantum-vulnerable production-scope component; and a declared maximum
acceptance duration after which re-acceptance requires fresh justification.

---

## AMD.3 Assessment procedures

An auditor SHALL:

1. Place a genuinely quantum-vulnerable component in production scope with a valid
   policy-eligible Risk-Acceptance Entry, with all other prerequisites satisfied, and confirm the component is still present in the CBOM output, the
   human-readable report visibly names it as a carried accepted risk (not a clean pass), and
   the exit status is the promote code (0). Then place the same component with **no** valid
   entry and confirm it blocks. The two runs SHALL be distinguishable in the report
   (OQGF-P-9.1). *This is the load-bearing test of this amendment.*
2. Submit a Risk-Acceptance Entry missing a DAP, an expiry, or a signature, and confirm it
   has no effect and the finding still blocks (OQGF-P-9.2).
3. Expire an active Risk-Acceptance Entry and confirm the accepted finding reverts to
   blocking with no residual effect (OQGF-P-9.3).
4. Attempt to express a Risk-Acceptance Entry that removes a finding from output, and attempt
   to attach a Tolerance Grant to a Deterministic Gate, and confirm both are refused
   (OQGF-P-9.4, reaffirming OQGF-P-2).
5. Request the standing inventory of active accepted risks and confirm it enumerates every
   current acceptance with its DAP, scope, and expiry (OQGF-P-9.5).
6. Present a correctly signed acceptance for a non-waivable finding, missing identity,
   missing intent, or missing custody evidence; confirm denial. Present one accepted
   finding together with an unaccepted blocker and confirm a blocking exit status.

---

## AMD.4 Control mappings

- **NIST AI RMF:** GOVERN-1.2 (accountable risk decisions), GOVERN-4.1, MANAGE-1.3
  (documented risk acceptance), MEASURE-2.6.
- **NIST SP 800-53 Rev. 5:** CA-5 (plan of action and milestones / accepted weaknesses),
  RA-7 (risk response), PM-9 (risk management strategy), AU-10 (non-repudiation of the
  acceptance decision), CM-3 (recorded change/exception control).
- **NIST SP 800-37 (RMF):** the risk-response disposition of *accept*, made explicit,
  accountable, scoped, and time-bounded rather than implicit.
- **ISO/IEC 42001 Annex A:** A.5, A.6; Clause 6 (risk treatment and acceptance); Clause 9
  (review).
- **CNSA 2.0:** ML-DSA-87 for Risk-Acceptance Entry signatures; dual-family at
  High-Assurance per OQGF-M-2.
- **Lineage:** consistent with formal risk-acceptance / exception-management practice
  (documented, owned, expiring, reviewed) and with object-capability accountability — the
  decision to proceed is itself an attributable, signed act.

**Mapping boundary:** CNSA references do not make SLH-DSA an NSS-approved algorithm. The dual-family rule is an additional OQGF profile requirement; A.0.9 governs compatibility, algorithm parameters, and evidence roles. A mapping is not external certification.

---

## AMD.5 Technical architecture (implementation hooks)

**Implementation status:** the following interfaces and dependency names are design sketches. They are not compiled code delivered by this repository. Historical references to an external implementation report the source author's context, not a fresh verification of that implementation. Apply the current normative text and A.0.9; an omitted field, enum variant, verifier check, or backend is not a conformance exemption.

The Risk-Acceptance register is a core type (`oqgf-core`), consumed by the Genetic Layer
gate (Organ 1) and available to the MHC attestation gate (Organ 3). The concrete instance is
`oqgf.allow.toml`, with each entry upgraded from a bare `crate` + `reason` pair to the full
structure below.

The reference implementation already has the load-bearing routing: each `CryptoComponent`
carries an `accepted_risk: Option<String>` field, and two filters in `oqgf-core::bom`
(`quantum_vulnerable_components`, the blocking list, which requires `accepted_risk.is_none()`;
and `accepted_risk_components`, the disclosure list, which requires `accepted_risk.is_some()`)
route a component out of blocking and into disclosure *without removing it from the CBOM*.
This amendment does not replace that mechanism. It (a) enriches what an acceptance records
from a bare string to an accountable structure, and (b) requires the human-readable report to
surface the disclosure list, which it currently does not.

### AMD.5.1 Core types

```rust
/// An accountable, scoped, expiring, signed decision to proceed past a
/// still-visible Deterministic-Gate finding (OQGF-P-9). NOT a ToleranceGrant
/// (OQGF-P-4) and NOT a SelfSet member (OQGF-P-3).
///
/// Replaces the bare `reason: String` carried in `oqgf.allow.toml` today. The
/// `dap` field reuses the EXISTING `oqgf-core::bom::DesignatedAccountableParty`
/// type — no second DAP type is introduced.
pub struct RiskAcceptance {
    pub finding: FindingId,              // exact component identity + advisory/reason (OQGF-P-9.2)
    pub gate: DeterministicGateId,       // OQGF-G-4 (crypto) or OQGF-M-1 (attestation)
    pub dap: DesignatedAccountableParty, // reuse existing type (OQGF-A-5)
    pub justification: String,           // the prior `reason` string, retained (Organ 5)
    pub expiry: SystemTime,              // bounded, renewable only by fresh decision (OQGF-P-9.3)
    pub signature: DualSignature,        // ML-DSA (+ SLH-DSA at High-Assurance)
}

/// Distinct verdicts for reporting (OQGF-P-9.1). Callers and renderers must enforce
/// the distinction; this declaration alone is not a guarantee: `AcceptedRisk` is a
/// separate variant carrying the still-visible findings, not a `Clean` with a flag.
///
/// Exit-code mapping (OQGF-P-9.1): both `Clean` and `AcceptedRisk` map to the
/// promote exit code (0); `Blocked` maps to the block exit code (1). The report
/// text, NOT the exit code, carries the clean-vs-accepted-risk distinction.
pub enum GateVerdict {
    Clean,
    Blocked {
        findings: Vec<FindingId>,
    },
    AcceptedRisk {
        accepted: Vec<RiskAcceptance>,
        still_visible: Vec<FindingId>, // the accepted findings remain in the CBOM
    },
}

pub trait RiskAcceptanceRegistry: Send + Sync {
    /// Apply current acceptances to a finding set. A RiskAcceptance SHALL NOT remove
    /// a finding; it changes the verdict from `Blocked` to `AcceptedRisk` with the
    /// finding still present. Expired or out-of-scope entries are ignored and the
    /// finding remains `Blocked` (OQGF-P-9.3). Any other unaccepted blocker also
    /// keeps the overall verdict Blocked. Apply only P-9.2-eligible entries.
    /// This generalizes the existing
    /// `accepted_risk` routing in `oqgf-core::bom`.
    fn apply(&self, findings: &[Finding]) -> GateVerdict;

    /// The standing inventory of currently active accepted risks (OQGF-P-9.5).
    fn active(&self) -> Vec<RiskAcceptance>;
}
```

The enum represents the three outcomes; it cannot prove that a renderer or caller uses them correctly. The gate must validate P-9.2 eligibility and every remaining blocker, and both report formats must retain accepted findings. Only Clean or a fully authorized AcceptedRisk may map to exit 0; mixed accepted/unaccepted findings remain Blocked. These behaviors require implementation and negative-test evidence.

### AMD.5.2 What this closes, and what it does not

This amendment **closes** the following:

- **The apparent OQGF-P-2 contradiction, and the silent-console gap underneath it.** The
  reference gate already keeps an accepted finding in the CBOM and reroutes it from blocking
  to disclosure without suppression — so in the *data* the gate never silently greens a
  quantum-vulnerable artifact. The real gap was that the *human-readable report* printed an
  accepted-risk build identically to a clean one. OQGF-P-9.1 closes that by requiring the
  report to name carried risk, while keeping the promote exit code intact.
- **Unaccountable exceptions.** An accepted risk now requires a named DAP, a scope, an
  expiry, a signature, and an Organ-5 record (OQGF-P-9.2); the `crate` + `reason` pair the
  allow-list carries today no longer suffices.
- **Permanent silent waivers.** Acceptance expires and reverts to blocking; renewal is a
  fresh, recorded decision (OQGF-P-9.3).
- **Confusion of acceptance with tolerance.** The two registers are distinct and a decision
  cannot be expressed as both (OQGF-P-9.4), preserving the OQGF-P-2 / P-4 boundary.
- **Untracked carried risk.** The set of currently accepted risks is enumerable and reviewed
  (OQGF-P-9.5), satisfying the OQGF-P-1 reporting obligation.

This amendment **does not** fully close, and states so honestly:

- **The quality of the risk decision itself.** Accountable Risk Acceptance makes the decision
  to proceed scoped, time-bounded, visible, attributable, and reviewable. It does **not**
  make the decision *correct*. A DAP can accept a risk that should not have been accepted.
  The framework guarantees that a wrong acceptance is at least named, bounded, signed, and
  reviewable — never silent or anonymous — but whether a given quantum-vulnerable component
  should be tolerated for a given period is a governance judgment, not a property the
  framework can certify. This is the residual, and it is the same shape as the over-broad
  Root Intent residual of AMD-001 (OQGF-M-13) and the Self Set residual of AMD-002: the
  framework reduces the surface to exactly this judgment and names it rather than claiming
  elimination.

---

## AMD.6 Traceability

| Requirement | Implementation hook |
| --- | --- |
| OQGF-P-9.1 | `GateVerdict::AcceptedRisk` distinct variant; finding retained in CBOM via existing `bom::accepted_risk_components` disclosure filter; **`report.rs` PASS renderer extended to print carried accepted risks** (the current gap); exit 0 only for Clean or fully authorized AcceptedRisk; any remaining blocker returns block |
| OQGF-P-9.2 | `RiskAcceptance` fields all required, reusing `bom::DesignatedAccountableParty`; allow-list parser `scanner/rust.rs:~1489` extended beyond `crate`+`reason`; record in Organ 5 |
| OQGF-P-9.3 | `RiskAcceptanceRegistry::apply` ignores expired/out-of-scope entries; component falls back into `bom::quantum_vulnerable_components` blocking filter |
| OQGF-P-9.4 | Separate `RiskAcceptanceRegistry` and `ToleranceController`; no shared path; gate refuses a tolerance grant (OQGF-P-2) |
| OQGF-P-9.5 | `RiskAcceptanceRegistry::active` standing inventory; periodic review record in Organ 5 |

---

## AMD.7 Change log

v1.0 — Initial public draft, 10 June 2026. Adds OQGF-P-9 (Accountable Risk Acceptance on
Deterministic Gates) to the Physiology Layer. Defines the suppression/acceptance distinction
that reconciles the Genetic Layer allow-list with the OQGF-P-2 non-suppressible-gate
guarantee: an accepted quantum-vulnerable finding remains visible in the CBOM and produces a
verdict distinct from a clean pass, while a named DAP, a scope, an expiry, a PQC signature,
and an Organ-5 record make the decision accountable. Distinguishes Accountable Risk
Acceptance (permitted on a Deterministic Gate, because it does not suppress) from a Tolerance
Grant (OQGF-P-4, suppression of a heuristic false positive, never attached to a Deterministic
Gate per OQGF-P-2). Does not modify OQGF-P-2 or OQGF-P-4. Residual: the framework makes a risk
acceptance accountable, bounded, and visible, but cannot certify that the acceptance is
correct — a governance judgment, named rather than eliminated.

v2.0 — 10 June 2026. Reconciled against the Genetic Layer reference implementation as built
through hardening round R6. Three substantive refinements, no change to the requirement's
intent: (1) OQGF-P-9.1 now separates the *human-readable report* (which SHALL distinguish
clean from carrying-accepted-risk) from the *exit code* (which SHALL remain the promote code
0, because a signed acceptance is an authorization to promote and the exit code is the CI
contract). (2) The amendment now credits the implementation's existing non-suppression
behavior — the accepted component already stays in the CBOM and is rerouted from blocking to
disclosure — and identifies the real gap as the text PASS report not surfacing that
disclosure. (3) Core types reuse the existing `DesignatedAccountableParty` rather than
minting a second DAP type, and the hooks are mapped to real implementation sites
(`bom::accepted_risk_components`, the `report.rs` PASS renderer, the `scanner/rust.rs`
allow-list parser). Per the OQGF annotation convention, v1.0 is retained above; this entry
records what changed.

— End of OQGF Amendment 006.

<!-- source-sync:navigation -->
**Integrated reading — 8 October 2026:** this amendment's operative requirements, tier criteria, and assessments are incorporated in [the current framework](OQGF-1_0.md#oqgf-p-9). Its identity and historical entries are retained; current text includes the dated consistency corrections. See the [integration map](OQGF-1_0.md#integration-map) and [resolution record](OQGF-1_0.md#synchronization-review). Future changes must update both views together.
