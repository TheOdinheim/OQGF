# OQGF-1.0 — NORMATIVE AMENDMENT 004

The Coordinated Signaling Requirement: Cytokine-Style Posture Coupling Without Central Command Amendment ID: OQGF-AMD-2026-004 Amends: OQGF-1.0, Section A.P (Physiology Layer). Supersedes the deferred OQGF-P-7 obligation introduced as a stub in AMD-002 with full normative content (OQGF-P-7.1 through OQGF-P-7.6). The AMD-002 P-7 stub SHALL be annotated as superseded by this amendment. Author: Jeremy Rose, CEO — Odin’s LLC, Wasilla, Alaska Date: 8 June 2026 Status: Public draft for NIST, sector regulators, and the Odin’s engineering team Normative dependencies: all five organs; OQGF-R (Organ 4, redundancy), OQGF-A (Organ 5); OQGF-P-5 (AMD-002, storm detection); OQGF-P-8 (AMD-005, resolution); interacts with AMD-001.

## AMD.0 Front matter

### AMD.0.1 Purpose of this amendment

AMD-002 named coordinated signaling (OQGF-P-7) as a binding obligation and
deferred its detail. This amendment supplies it.
OQGF’s five organs detect different things. Without coordination, a detection in one
organ stays in that organ: Inflammation can see a harvest-now-decrypt-later pattern
and never tell the MHC layer to tighten attestation, or the Genetic Layer to shorten re-emission cadence. The immune system does not silo its information. A signal from one
cell changes the behavior of others, and it does so without a central brain — there is
no coordinator whose failure stops the response. This amendment makes inter-organ
signaling a normative property: detection in one organ can raise the posture of others,
the signals are authenticated, the coordination is decentralized, and a forged signal can
never stand the system down.

### AMD.0.2 The biological basis

Immune cells coordinate chiefly through cytokines — secreted signaling molecules that
change the behavior of the cells that receive them. There is no central controller.
Coordination is local (paracrine and autocrine diffusion) and through cell-to-cell
contact, and it scales out to systemic effects only when local signaling crosses
thresholds.
Three properties matter here. First, posture coupling: a signal from one cell changes
what another cell does — interferons, for example, put neighboring cells into an antiviral
state before those cells are infected, priming the defense ahead of the threat. Second,
decentralization and redundancy: there are many cytokines with overlapping
functions and no single signaling pathway whose loss silences the response —
pleiotropy and redundancy are designed in. Third, the failure mode is the runaway
loop: a cytokine storm is signaling feedback that escalates out of proportion and
harms the host through its own magnitude.
The translation: OQGF organs emit authenticated signals that raise each other’s
posture, with no single coordinator to lose, and with the signaling cascade itself
bounded so it cannot become a storm.

### AMD.0.3 Terminology additions

Signal — an authenticated, scoped, expiring message emitted by an organ on
detection or material state change, intended to affect the posture of one or more
other organs. The cytokine analog.
Posture Coupling — a declared relationship in which a Signal of sufficient severity
from one organ changes the defensive posture of a different organ.
Raise-Only Autonomy — the rule that an autonomous Signal may only increase
defensive posture; decreasing posture is governed by Resolution (OQGF-P-8) and
never by a raw Signal.
Signal Cascade — a chain of Signals triggered by one another. A cascade that
threatens host availability is a Response Storm under OQGF-P-5.

### AMD.0.4 Scope and relationship to AEGIS

This is the amendment most likely to resemble a runtime product, so the AMD-002
boundary (AMD.0.4) is reaffirmed in the strongest terms. OQGF requires coordinated
signaling as a property of any conforming system. It does not mandate any particular
event bus, message broker, or signaling product. AEGIS implements a runtime event bus
in which detection at one layer strengthens others; an operator MAY use AEGIS or
comparable tooling to satisfy these requirements, but OQGF neither requires nor
depends on it, and conformance is assessed against the requirements here. The
requirements below specify properties of the signaling, not a product that signals.

### AMD.0.5 Design assumptions requiring confirmation

This amendment makes the following design calls. Each is the fail-safe default; flag any
you wish to change.
1. Signed envelope plus canonical classes, not a fixed catalog. A general signed
Signal envelope is mandated, along with a small set of canonical Signal classes; the
full per-organ Signal catalog is left to implementation (OQGF-P-7.1). Assumed to
give teeth without over-specifying.
2. At-least-once, per-source-ordered, idempotent delivery. Signals are delivered
at least once, ordered per source, with idempotent handlers; no global ordering is
required. Assumed to match decentralized biology and survive partition.
3. Raise-only autonomy. Autonomous Signals may only raise posture; de-escalation
is resolution-gated (OQGF-P-7.4, with OQGF-P-8). Assumed because it makes a
forged or replayed Signal incapable of standing the system down — the fail-safe
choice.

## AMD.1 Normative requirements

These requirements supersede and fully specify OQGF-P-7.
OQGF-P-7.1 (Signed Signal Envelope). Inter-organ Signals SHALL use a common
signed envelope carrying: the source organ, the Signal class, a severity, the intended
posture effect, a scope, a freshness nonce, and an expiry — signed under ML-DSA
(dual-family at High-Assurance per OQGF-M-2). A Signal that is unsigned, malformed,
or expired SHALL be ignored. An attacker SHALL NOT be able to drive organ posture by
forging a Signal.
OQGF-P-7.2 (Posture Coupling). A Signal of sufficient severity SHALL be able to
change the posture of an organ other than the one that emitted it — for example, an
Organ 2 (Inflammation) HNDL detection raising Organ 3 (MHC) attestation frequency
and shortening Organ 1 (Genetic Layer) re-emission cadence. The set of cross-organ
couplings (which Signal classes affect which organs, and how) SHALL be declared and
recorded in Organ 5.
OQGF-P-7.3 (Decentralization / No Coordination Single Point of Failure). Inter-organ signaling SHALL NOT depend on a single coordination component whose failure
silences it. Loss of any one organ or transport path SHALL degrade coordination
gracefully, not halt it. This requirement is assessed jointly with Organ 4 (OQGF-R) and is
the “no central command” guarantee.
OQGF-P-7.4 (Raise-Only Autonomy). An autonomous Signal MAY only raise defensive
posture. Lowering posture (de-escalation) SHALL NOT be performed in response to a
raw Signal and SHALL be governed by Resolution (OQGF-P-8). Consequently a forged,
replayed, or misleading Signal cannot stand the system down; at worst it can over-tighten, which is bounded by self-tolerance (OQGF-P-1, OQGF-P-5). This mirrors the
monotonic, fail-safe spirit of AMD-001.
OQGF-P-7.5 (Cascade Bound). Signal propagation SHALL be rate-limited and loop-bounded so that a Signal Cascade cannot itself threaten host availability. A cascade
exceeding its declared bound SHALL be detected and raised as a Response Storm under
OQGF-P-5. This is the cytokine-storm prevention, and it is the binding link to AMD-002.
OQGF-P-7.6 (Signal Provenance in Memory). Material Signals and the posture
changes they caused SHALL be recorded in Organ 5 (OQGF-A) for forensic
reconstruction: what was signaled, by which organ, with what effect, and when.
Coordination SHALL be auditable after the fact.

## AMD.2 Conformance criteria per level

Baseline (OQGF-B): Signed Signal envelope with expiry, forged/expired Signals ignored
(OQGF-P-7.1); at least one declared, recorded cross-organ Posture Coupling (OQGF-P-7.2); raise-only autonomy (OQGF-P-7.4). Single-PQC-family Signal signatures
acceptable.
Enhanced (OQGF-E): All Baseline criteria, plus demonstrated decentralization —
coordination survives loss of any one transport path (OQGF-P-7.3); cascade bounding
with storm escalation (OQGF-P-7.5); Signal provenance recorded in Organ 5 (OQGF-P-7.6).
High-Assurance (OQGF-H): All Enhanced criteria, plus dual-PQC-family Signal
signatures (ML-DSA + SLH-DSA); demonstrated graceful degradation under loss of any
one organ; and a declared, reviewed full coupling matrix across all five organs.

## AMD.3 Assessment procedures

An auditor SHALL:
1. Inject a forged or expired Signal and confirm it is ignored — that organ posture
cannot be driven by an unauthenticated message (OQGF-P-7.1).
2. Trigger a high-severity detection in one organ and confirm the declared posture
change actually occurs in the coupled organ, and that the coupling is recorded
(OQGF-P-7.2).
3. Disable a signaling transport path and confirm coordination degrades gracefully
rather than halting — no single coordinator silences the system (OQGF-P-7.3).
4. Replay a captured Signal that, if honored as a de-escalation, would stand the system
down, and confirm it cannot — autonomous Signals only raise posture (OQGF-P-7.4).
This is the load-bearing test of this amendment.
5. Induce a signal loop and confirm the cascade is bounded and escalated as a
Response Storm under OQGF-P-5 (OQGF-P-7.5).
6. Inspect Organ 5 and confirm material Signals and their posture effects are recorded
(OQGF-P-7.6).

## AMD.4 Control mappings

NIST AI RMF: MANAGE-2.1, MANAGE-4.1, MEASURE-2.6.
NIST SP 800-53 Rev. 5: SI-4 (system monitoring), IR-4 (incident handling
coordination), IR-5, AU-10 (Signal non-repudiation), SC-5 (cascade understood as
self-induced denial of service), CP-2 (availability under coordination failure).
ISO/IEC 42001 Annex A: A.6, A.9; Clause 10.
CNSA 2.0: ML-DSA-87 for Signal signatures; dual-family at High-Assurance per
OQGF-M-2.
Cross-discipline lineage: consistent with event-driven architecture,
gossip/epidemic propagation (decentralized, partition-tolerant), and the
immunological “danger model” (context, not mere foreignness, drives the response).

## AMD.5 Technical architecture (implementation hooks)

The Signal envelope is a core type ( oqgf-core ); the transport is a trait ( oqgf-signal::SignalBus ) with decentralized, gossip-capable implementations — a trait, not a
mandated product, per AMD.0.4. Each organ implements an idempotent handler. The
AMD-001 anergy emission (anergy raised to Organ 2 and recorded in Organ 5) is the
reference instance of a Signal.

### AMD.5.1 Core types

```rust
/// Canonical Signal classes (the catalog is extensible per implementation).
pub enum SignalClass {
    ThreatDetected,        // an organ saw something
    PostureRaiseRequest,   // ask coupled organs to tighten (raise-only, OQGF-P-7.4)
    StateChangeNotice,     // material state change worth propagating
}

/// The signed cytokine envelope (OQGF-P-7.1).
pub struct Signal {
    pub source: OrganId,
    pub class: SignalClass,
    pub severity: Severity,
    pub effect: PostureEffect,    // SHALL be raise-only when autonomous (OQGF-P-7.4)
    pub scope: SignalScope,
    pub nonce: Nonce,             // freshness
    pub expiry: SystemTime,
    pub signature: DualSignature, // ML-DSA (+ SLH-DSA at High-Assurance)
}

pub trait SignalBus: Send + Sync {
    /// Emit a Signal. At-least-once, per-source-ordered delivery.
    fn emit(&self, signal: Signal) -> Result<(), SignalError>;
}

pub trait SignalHandler: Send + Sync {
    /// Idempotent. Verifies signature + freshness, then applies a raise-only
    /// posture change. A de-escalation effect on a raw Signal SHALL be refused
    /// and deferred to Resolution (OQGF-P-7.4 / OQGF-P-8).
    fn on_signal(&self, signal: &Signal) -> Result<PostureChange, SignalError>;
}
```

### AMD.5.2 What this closes, and what it does not

This amendment closes the following:

- **Siloed detection** — a detection in one organ can now raise the posture of others (OQGF-P-7.2).
- **Forged-signal control** — a Signal must be signed and fresh to have effect (OQGF-P-7.1); and even a valid Signal can only tighten, never stand the system down (OQGF-P-7.4).
- **Coordination single point of failure** — signaling is decentralized and degrades gracefully (OQGF-P-7.3), assessed with Organ 4.
- **Runaway coordination** — cascades are bounded and escalated as storms (OQGF-P-7.5), inherited from AMD-002.

This amendment does not fully close, and states so honestly:

- **Coordination amplifies detection; it does not create it.** Signaling makes a response faster and more coherent, but if no organ saw the threat, there is nothing to signal. Coverage is a detection problem, not a signaling one.
- **A compromised-but-attested organ can emit a valid, misleading Signal.** Because of raise-only autonomy (OQGF-P-7.4), the worst it can cause is over-tightening, which self-tolerance bounds and reports (OQGF-P-1, OQGF-P-5). The blast radius of a bad Signal is over-defense, never stand-down. This residual is named rather than claimed eliminated.

## AMD.6 Traceability

| Requirement | Implementation hook |
|---|---|
| OQGF-P-7.1 | `oqgf-core::Signal` signed envelope; handler rejects unsigned/expired |
| OQGF-P-7.2 | declared coupling matrix; `SignalHandler::on_signal` applies posture change |
| OQGF-P-7.3 | gossip-capable `SignalBus` impls; graceful degradation, assessed with `oqgf-redundant` |
| OQGF-P-7.4 | `PostureEffect` raise-only when autonomous; de-escalation refused, deferred to OQGF-P-8 |
| OQGF-P-7.5 | cascade rate-limit + loop bound; storm escalation via OQGF-P-5 |
| OQGF-P-7.6 | Signals + posture effects recorded in `oqgf-memory` |

## AMD.7 Change log

v1.0 — Initial public draft, 8 June 2026. Supersedes the AMD-002 OQGF-P-7 stub with
full normative content. Specifies authenticated, scoped, expiring inter-organ Signals;
cross-organ posture coupling; decentralization with no coordination single point of
failure; raise-only autonomy so a forged Signal cannot stand the system down; cascade
bounding tied to storm detection (OQGF-P-5); and Signal provenance in Organ 5.
Reaffirms the AEGIS boundary: OQGF requires coordinated signaling as a property, not a
product. Generalizes AMD-001’s point-to-point emission into a system-wide property.
— End of OQGF Amendment 004.
