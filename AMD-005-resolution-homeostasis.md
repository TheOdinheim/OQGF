# OQGF-1.0 — NORMATIVE AMENDMENT 005

The Resolution Requirement: Active Return to Baseline and the Bound on Chronic Escalation Amendment ID: OQGF-AMD-2026-005 Amends: OQGF-1.0, Section A.P (Physiology Layer). Supersedes the deferred OQGF-P-8 obligation introduced as a stub in AMD-002 with full normative content (OQGF-P-8.1 through OQGF-P-8.7). The AMD-002 P-8 stub SHALL be annotated as superseded by this amendment. Author: Jeremy Rose, CEO — Odin’s LLC, Wasilla, Alaska Date: 8 June 2026 Status: Public draft for NIST, sector regulators, and the Odin’s engineering team Normative dependencies: OQGF-I (Organ 2), OQGF-A (Organ 5); OQGF-P-1 (AMD-002, host harm); OQGF-P-7.4 (AMD-004, raise-only autonomy); OQGF-P-6 (AMD-003, learned-detector preservation).

## AMD.0 Front matter

### AMD.0.1 Purpose of this amendment

AMD-002 named resolution (OQGF-P-8) as a binding obligation and deferred its detail.
This amendment supplies it, and in doing so closes the loop opened by AMD-004:
signaling can raise posture autonomously, so something must govern bringing posture
back down.
OQGF can escalate — raise a Threat Level, quarantine a workload, tighten a threshold,
shift to an emergency key-rotation posture. AMD-002 already names the failure of a
system that escalates but never returns: chronic high-alert is itself host harm. This
amendment requires that every escalation has a defined, accountable way down, that
the way down is deliberate rather than an implicit timeout, that it does not flap, that it
preserves what the system learned, and that an escalation which never resolves is itself
flagged.

### AMD.0.2 The biological basis

Inflammation must resolve, and resolution is an active process, not the mere absence
of a stimulus. Specialized pro-resolving mediators actively switch inflammation off,
macrophages clear apoptotic debris, and tissue is restored to its homeostatic set point
— body temperature is brought back to 37 °C, not left elevated.
The adaptive response stands down deliberately too. After an infection clears, the great
majority of expanded effector T-cells die by apoptosis in the contraction phase,
leaving a small, stable memory population. The system disbands most of the army on
purpose — but it keeps the intelligence. Memory cells persist. You stand down the
response; you retain the lesson.
The failure mode is chronic inflammation — a failure to resolve — which drives tissue
damage and disease. An immune response that never switches off is not vigilance; it is
pathology. The governance translation is exact: an escalation that never de-escalates is
not security posture; it is a self-harm condition that must be detected and corrected.

### AMD.0.3 Terminology additions

Escalation — any defensive posture change that raises restriction above the
declared baseline (Threat Level raise, quarantine, threshold tightening, emergency
rotation posture).
Resolution Path — the declared criteria for when an Escalation’s triggering
condition is considered cleared, together with the target baseline posture to return
to.
Baseline Posture — the declared steady-state (“homeostatic set point”) an
Escalation returns to on resolution.
Dwell and Hold — the minimum time spent escalated (dwell) and the window over
which the clear condition must persist (hold) before de-escalation, preventing
oscillation. The graded- contraction analog.
Chronic Escalation — an Escalation persisting beyond its declared maximum
duration without resolving or being explicitly re-justified. The chronic-inflammation
analog.

### AMD.0.4 Design assumptions requiring confirmation

This amendment makes the following design calls. Each is the fail-safe default; flag any
you wish to change.
1. DAP-confirmed de-escalation above Baseline. Resolution criteria are evaluated
automatically, but actual de-escalation above Baseline requires DAP confirmation;
the system errs toward staying escalated (OQGF-P-8.5). Assumed because
premature stand-down re-exposes the host, and standing down should be a
deliberate, accountable act.
2. Mandatory hysteresis. Every Escalation type declares a minimum dwell and a
clear-condition hold window; the values are deployment policy, but their presence is
mandatory (OQGF-P-8.3). Assumed to prevent flapping.
3. Declared maximum duration. Every Escalation type declares a maximum duration;
exceeding it without resolution or re-justification raises a Chronic Escalation
condition (OQGF-P-8.6). Assumed so no high-alert state can quietly become
permanent.

## AMD.1 Normative requirements

These requirements supersede and fully specify OQGF-P-8.
OQGF-P-8.1 (Declared Resolution Path). Every Escalation type SHALL declare,
before it may be used, its Resolution Path — the criteria marking the triggering condition
cleared, and the target Baseline Posture. An Escalation with no declared Resolution Path
SHALL NOT be permitted. There are no one-way ratchets.
OQGF-P-8.2 (Active, Recorded Resolution). Return to the Baseline Posture SHALL
be an explicit, recorded decision in Organ 5 (OQGF-A) — the cleared condition, the time,
and the accountable DAP — not an implicit or silent timeout. Resolution is an act the
system performs and records, not an absence it drifts into.
OQGF-P-8.3 (Hysteresis / Anti-Flap). A Resolution Path SHALL include a minimum
dwell time at the escalated posture and a hold window over which the clear condition
must persist before de-escalation. These SHALL be set to prevent rapid oscillation
between escalated and baseline states. The system contracts deliberately, not instantly.
OQGF-P-8.4 (Memory Preservation on Stand-Down). De-escalation SHALL NOT
erase the Organ 5 record of the incident, nor revert any tolerance-screened Refined
Detector produced under OQGF-P-6. The response stands down; the forensic record
and the learned defense are retained. Standing down the army does not discard the
intelligence.
OQGF-P-8.5 (Resolution Authority / Fail-Safe Asymmetry). Autonomous action
MAY raise posture (OQGF-P-7.4) but SHALL NOT autonomously de-escalate above
Baseline. De-escalation above Baseline SHALL require the Resolution Path criteria to be
met and DAP confirmation. Where the system is uncertain, it SHALL remain escalated.
Raising posture is cheap and reversible; lowering it prematurely re-exposes the host, so
lowering is the guarded direction.
OQGF-P-8.6 (Chronic-Escalation Detection). An Escalation persisting beyond its
declared maximum duration without resolving or being explicitly re-justified by a DAP
SHALL be flagged as a Chronic Escalation, raised through Organ 2 (OQGF-I), and
recorded in Organ 5. Chronic Escalation is treated as a host-harm condition under
OQGF-P-1, on the principle that a response that never switches off is pathology, not
vigilance.
OQGF-P-8.7 (Proof of Return — High-Assurance). At High-Assurance, the system
SHALL record a post-resolution baseline-conformance check demonstrating that the
declared Baseline Posture was actually restored. Return to baseline SHALL be
demonstrable, not merely asserted.

## AMD.2 Conformance criteria per level

Baseline (OQGF-B): Every Escalation type has a declared Resolution Path (OQGF-P-8.1); resolution is an explicit recorded decision, not a silent timeout (OQGF-P-8.2);
hysteresis present to prevent flapping (OQGF-P-8.3).
Enhanced (OQGF-E): All Baseline criteria, plus memory preservation on stand-down
(OQGF-P-8.4); fail-safe authority asymmetry with DAP-confirmed de-escalation above
Baseline (OQGF-P-8.5); Chronic-Escalation detection (OQGF-P-8.6).
High-Assurance (OQGF-H): All Enhanced criteria, plus recorded proof of return to
baseline (OQGF-P-8.7); dual-PQC-family signatures on resolution decisions (ML-DSA +
SLH-DSA per OQGF-M-2); and second-DAP review of any de-escalation from the
highest Escalation level.

## AMD.3 Assessment procedures

An auditor SHALL:
1. Attempt to register an Escalation type with no declared Resolution Path and confirm
it is refused (OQGF-P-8.1).
2. Resolve an active Escalation and confirm the de-escalation is an explicit recorded
decision in Organ 5 with the cleared condition and accountable DAP — not an
unrecorded timeout (OQGF-P-8.2).
3. Oscillate the clear condition rapidly and confirm the dwell/hold hysteresis prevents
the system from flapping between escalated and baseline (OQGF-P-8.3).
4. De-escalate an Escalation and confirm the Organ 5 incident record and any OQGF-P-6 Refined Detector survive the stand-down (OQGF-P-8.4).
5. Meet a Resolution Path’s criteria above Baseline and confirm the system does not
stand down without DAP confirmation — that it errs toward staying escalated
(OQGF-P-8.5). This is the load-bearing test of this amendment.
6. Hold an Escalation past its declared maximum duration and confirm a Chronic
Escalation is flagged, raised through Organ 2, and recorded (OQGF-P-8.6).

## AMD.4 Control mappings

NIST AI RMF: MANAGE-2.4 (response and recovery), MANAGE-4.1, MEASURE-2.6.
NIST SP 800-53 Rev. 5: IR-4 (incident handling, including recovery), CP-2, CP-10
(system recovery and reconstitution), SI-4 (monitoring for chronic conditions), AU-10 (non-repudiation of resolution decisions).
ISO/IEC 42001 Annex A: A.6, A.9; Clause 10.
CNSA 2.0: ML-DSA-87 for resolution-decision signatures; dual-family at High-Assurance per OQGF-M-2.
Cross-discipline lineage: consistent with the circuit-breaker recovery pattern
(Closed/Open/Half-Open with cooldown-probe recovery), the site-reliability incident
lifecycle (detect → mitigate → resolve → return to steady state), and control-theory
hysteresis for oscillation damping.

## AMD.5 Technical architecture (implementation hooks)

The resolution engine lives in oqgf-inflammation (Organ 2), drawing on oqgf-memory for
the incident record and learned-detector preservation, and is the governed counterpart
to the AMD-004 raise-only signaling path. The established analog is the circuit-breaker
recovery cycle — invoked as a governance requirement, not a mandated product.

### AMD.5.1 Core types

```rust
/// Declared before an Escalation type may be used (OQGF-P-8.1, 8.3, 8.6).
pub struct EscalationType {
    pub id: EscalationId,
    pub resolution_criteria: ClearCondition,  // when the trigger is "cleared"
    pub baseline: BaselinePosture,            // homeostatic set point to return to
    pub dwell_min: Duration,                  // minimum time escalated (OQGF-P-8.3)
    pub hold_window: Duration,                // clear must persist this long (OQGF-P-8.3)
    pub max_duration: Duration,               // chronic threshold (OQGF-P-8.6)
}

/// An explicit, recorded de-escalation decision (OQGF-P-8.2, 8.5).
pub struct ResolutionDecision {
    pub escalation: EscalationId,
    pub cleared_condition: ClearEvidence,
    pub dap: Dap,                 // confirmation above Baseline (OQGF-P-8.5)
    pub at: SystemTime,
    pub signature: DualSignature, // ML-DSA (+ SLH-DSA at High-Assurance)
}

pub trait ResolutionEngine: Send + Sync {
    /// Evaluate whether an Escalation MAY de-escalate: criteria met AND
    /// dwell/hold satisfied. Above Baseline, returns NeedsDapConfirmation.
    fn may_resolve(&self, e: &EscalationId) -> ResolutionVerdict;
    // Eligible { needs_dap } | NotYet { reason } | Chronic (OQGF-P-8.5, 8.6)
    /// Perform a confirmed de-escalation. SHALL preserve the Organ 5 record and
    /// any OQGF-P-6 Refined Detector (OQGF-P-8.4). Records the decision.
    fn resolve(&self, d: ResolutionDecision) -> Result<ReturnedToBaseline, ResolveError>;
    /// Watchdog: flag Escalations past max_duration as Chronic (OQGF-P-8.6).
    fn scan_chronic(&self) -> Vec<ChronicEscalation>;
}
```

### AMD.5.2 What this closes, and what it does not

This amendment closes the following:

- **One-way escalation ratchets** — every Escalation has a declared way down (OQGF-P-8.1).
- **Silent or accidental stand-down** — de-escalation is explicit, recorded, and (above Baseline) DAP-confirmed (OQGF-P-8.2, 8.5).
- **Flapping** — dwell/hold hysteresis damps oscillation (OQGF-P-8.3).
- **Losing the lesson on stand-down** — the incident record and learned detectors survive de-escalation (OQGF-P-8.4).
- **Permanent silent high-alert** — Chronic Escalation is detected and raised as host harm (OQGF-P-8.6), closing the chronic-inflammation failure AMD-002 named.

This amendment does not fully close, and states so honestly:

- **Resolution criteria are a judgment about whether a threat is "gone," and that judgment can be wrong.** A premature resolution re-exposes the host. The amendment biases toward staying escalated (OQGF-P-8.5) and damps with hysteresis (OQGF-P-8.3), but the quality of the clear condition is a governance problem — the same shape as the AMD-002 Self Set residual.
- **Resolution governs posture, not eradication.** Returning to baseline means the declared clear condition was met; it does not prove the adversary is gone. The framework states what it controls (posture) and does not claim what it cannot (certainty that a threat has been eliminated).

## AMD.6 Traceability

| Requirement | Implementation hook |
|---|---|
| OQGF-P-8.1 | `EscalationType::resolution_criteria` + `baseline`; registration refused without them |
| OQGF-P-8.2 | `ResolutionDecision` recorded in `oqgf-memory`; no silent timeout path |
| OQGF-P-8.3 | `dwell_min` + `hold_window` enforced in `ResolutionEngine::may_resolve` |
| OQGF-P-8.4 | `resolve` preserves Organ 5 record + OQGF-P-6 detector; reversion prohibited |
| OQGF-P-8.5 | `may_resolve` returns `needs_dap` above Baseline; bias to remain escalated |
| OQGF-P-8.6 | `ResolutionEngine::scan_chronic` watchdog → Organ 2 + Organ 5 |
| OQGF-P-8.7 | post-resolution `BaselineConformanceCheck` recorded at High-Assurance |

## AMD.7 Change log

v1.0 — Initial public draft, 8 June 2026. Supersedes the AMD-002 OQGF-P-8 stub with
full normative content. Specifies declared resolution paths (no one-way ratchets);
active, recorded de-escalation; dwell/hold hysteresis against flapping; memory and
learned-detector preservation on stand-down; fail-safe authority asymmetry
(autonomous raise, DAP-confirmed lower); Chronic- Escalation detection closing the
chronic-inflammation failure mode; and High-Assurance proof of return to baseline.
Completes the Physiology Layer (OQGF-P) begun in AMD-002, and is the governed
counterpart to AMD-004’s raise-only signaling.
— End of OQGF Amendment 005.
