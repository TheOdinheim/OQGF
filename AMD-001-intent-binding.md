# OQGF-1.0 — NORMATIVE AMENDMENT 001
## The Costimulation Requirement: Intent Provenance Binding for Multi-Hop Agentic Systems

**Amendment ID:** OQGF-AMD-2026-001
**Amends:** OQGF-1.0, Part A, Section A.3 (Organ 3 — OQGF-M / MHC Layer)
**Author:** Jeremy Rose, CEO — Odin's LLC, Wasilla, Alaska
**Date:** 31 May 2026
**Status:** Public draft for NIST, sector regulators, and the Odin's engineering team
**Normative dependencies:** OQGF-M (Organ 3), OQGF-I (Organ 2), OQGF-A (Organ 5)

---

## AMD.0 Front matter

### AMD.0.1 Purpose of this amendment

OQGF-1.0 Organ 3 (MHC Layer) establishes cryptographic identity for every device,
workload, model, and quantum job through PQC-signed attestation. Attestation answers
the question *who is this actor and what does it claim to intend*.

This amendment addresses a gap that cryptographic identity alone does not close: in
multi-agent and multi-hop agentic systems, **intent is reframed as it propagates across
hops**, and a valid signature on a reframed intent does not prove that the reframed
intent is a faithful derivation of the originally authorized intent.

An agent can hold a cryptographically perfect identity, present a valid attestation, and
still execute an action that no one authorized — because the intent it received at hop N
was silently broadened, redirected, or reframed somewhere between hop 1 and hop N.
Signing the intent at each hop proves authorship of the reframing. It does not prevent
the reframing.

This amendment makes intent provenance a first-class, cryptographically enforced
security primitive.

### AMD.0.2 The biological basis

The human adaptive immune system solved this exact problem with the **two-signal model
of lymphocyte activation**.

A naive T-cell that recognizes an antigen presented on an MHC molecule receives
**Signal 1** — identity recognition. But Signal 1 alone does **not** activate the T-cell.
The T-cell requires **Signal 2** — costimulation — a second, independent confirmatory
signal from the antigen-presenting cell verifying that the context is legitimate.

A T-cell that receives Signal 1 without Signal 2 does not simply stand down. It is driven
into **anergy** — a state of lasting functional unresponsiveness. Identity recognition in
the absence of costimulation actively disables the cell rather than leaving it neutral.
This is the immune system's defense against autoimmunity: recognition alone is never
sufficient authority to act.

The adaptive immune system reinforces this with **linked recognition**. For a B-cell to
mount an antibody response, it must receive help from a helper T-cell that recognizes an
epitope physically linked to the same antigen. Neither cell can unilaterally authorize a
full response. The decision to act must be corroborated across a chain, and each link in
the chain must verify a connected piece of the same original threat.

OQGF-M already implements Signal 1: PQC-signed identity attestation. This amendment
implements **Signal 2** for agentic systems — a verifiable, cryptographically attenuated
intent provenance chain that must accompany identity before any privileged action is
permitted. Identity without verified intent provenance induces **architectural anergy**:
the action is denied, not executed.

### AMD.0.3 Terminology additions

- **Intent Provenance Chain (IPC)** — a cryptographically signed, hash-linked record of
  every intent derivation from the root authorization to the current hop, such that any
  verifier can reconstruct the full lineage of an intent and confirm each derivation.
- **Root Intent (RI)** — the original authorized intent issued by a Designated Accountable
  Party (DAP, see OQGF-A-5) or an authenticated principal, scoped to least privilege, and
  carrying its invariant set.
- **Intent Caveat** — an append-only restriction added to an intent at a hop. Caveats may
  only narrow authority. The cryptographic construction prevents removal or broadening.
- **Monotonic Intent Attenuation (MIA)** — the property that the authority granted by an
  intent can only decrease, never increase, as the intent propagates across hops.
- **Intent Invariant** — a hard constraint declared in the Root Intent that SHALL hold at
  every hop regardless of any permitted reframing (for example: "no external API calls",
  "read-only on production", "no PII egress").
- **Architectural Anergy** — the mandated default state in which an actor presenting valid
  identity but unverifiable or violated intent provenance is denied all privileged action.

---

## AMD.1 Normative requirements

These requirements extend OQGF-M. They are numbered to continue the Organ 3 sequence
(existing requirements are OQGF-M-1 through OQGF-M-7).

**OQGF-M-8 (Intent Provenance Chain).** Every privileged action in a multi-hop agentic
system SHALL be accompanied by an Intent Provenance Chain that records, for each hop from
the Root Intent forward: the hop identity (per OQGF-M-1 attestation), the intent received,
the intent emitted, the digest of the prior chain entry, and a PQC signature over the
entry. A verifier SHALL be able to reconstruct the complete chain back to the Root Intent
using only declared public roots of trust.

**OQGF-M-9 (Monotonic Intent Attenuation).** The authority expressed by an intent SHALL
only narrow as it propagates. Each hop MAY add intent caveats; no hop SHALL be able to
broaden the authority it received. The cryptographic construction SHALL make broadening
computationally infeasible, not merely detectable. Where an actor at hop N requires
authority broader than it received, it SHALL request a new Root Intent from an authorized
principal rather than self-broadening.

**OQGF-M-10 (Intent Invariant Enforcement).** The Root Intent SHALL carry an invariant
set. Every hop SHALL evaluate the current action against the invariant set before acting,
independent of any reframing that has occurred upstream. Invariants are themselves
subject to monotonic attenuation: a hop MAY add invariants but SHALL NOT remove or weaken
an invariant present in the chain.

**OQGF-M-11 (Costimulation Gate).** No actor SHALL be granted privileged action on the
basis of identity attestation (Signal 1) alone. A privileged action SHALL require both a
valid identity attestation per OQGF-M-1 and a valid Intent Provenance Chain per OQGF-M-8
(Signal 2). An actor presenting valid identity with absent, malformed, or invariant-
violating intent provenance SHALL be placed in architectural anergy: all privileged
action denied, with the denial emitted as a signed event to Organ 2 (OQGF-I) and recorded
in Organ 5 (OQGF-A).

**OQGF-M-12 (Cross-Hop Behavioral Reconciliation).** The action actually executed at each
hop SHALL be reconciled against both the intent declared at that hop and the Root Intent.
Deviation between declared intent and executed action, or between executed action and the
Root Intent invariant set, SHALL trigger the OQGF-I graded response engine. This
requirement links Organ 3 (identity-intent binding) to Organ 2 (assumed breach) and is
assessed jointly.

**OQGF-M-13 (Least-Privilege Root Scoping).** The Root Intent SHALL be scoped to the
minimum authority required for the authorized task at the time of issuance. Broad,
long-lived, or open-ended Root Intents SHALL be documented as a risk requiring DAP
acceptance, because monotonic attenuation cannot constrain authority that was over-granted
at the root. The narrowest defensible Root Intent is the primary control against
in-scope reframing.

**OQGF-M-14 (Intent Chain Freshness).** Intent Provenance Chains SHALL carry a freshness
nonce and an expiry. A chain whose expiry has passed SHALL NOT authorize action and SHALL
require re-issuance from an authorized principal. Chain expiry SHALL NOT exceed the
credential lifetime of the actor at the current hop (per OQGF-M-4).

---

## AMD.2 Conformance criteria per level

**Baseline (OQGF-B):** Intent Provenance Chain present and signed (OQGF-M-8); Costimulation
Gate enforced for identity-plus-intent (OQGF-M-11); architectural anergy as default deny.
Single-PQC-family chain signatures acceptable.

**Enhanced (OQGF-E):** All Baseline criteria, plus Monotonic Intent Attenuation
cryptographically enforced (OQGF-M-9); Intent Invariant Enforcement at every hop
(OQGF-M-10); Cross-Hop Behavioral Reconciliation feeding the graded response engine
(OQGF-M-12); documented least-privilege Root Intent scoping (OQGF-M-13).

**High-Assurance (OQGF-H):** All Enhanced criteria, plus dual-PQC-family signatures on
every chain entry (lattice and hash-based, consistent with OQGF-M-2); chain freshness
bound to per-hop credential lifetime (OQGF-M-14); invariant sets reviewed and signed by a
DAP; full Intent Provenance Chains retained in Organ 5 for the sector retention period.

---

## AMD.3 Assessment procedures

An auditor SHALL:

1. Select a privileged action at random from a multi-hop chain and request its full Intent
   Provenance Chain. Verify every signature back to the Root Intent using only declared
   public roots of trust.
2. Attempt to broaden authority at an intermediate hop (inject a caveat removal or scope
   expansion) and confirm that verification fails — that broadening is computationally
   prevented, not merely flagged (OQGF-M-9).
3. Construct an action that satisfies the declared intent at the final hop but violates a
   Root Intent invariant, and confirm the Costimulation Gate denies it and the actor enters
   architectural anergy (OQGF-M-10, OQGF-M-11).
4. Present a valid identity attestation with an absent Intent Provenance Chain and confirm
   default deny (OQGF-M-11).
5. Inspect Organ 5 records to confirm denial events and behavioral-reconciliation deviations
   are captured with the DAP and the full chain (OQGF-M-12).
6. Replay an expired Intent Provenance Chain and confirm it does not authorize action
   (OQGF-M-14).

---

## AMD.4 Control mappings

- **NIST AI RMF:** GOVERN-1.4, MAP-3.2, MEASURE-2.5, MANAGE-2.1.
- **NIST SP 800-53 Rev. 5:** AC-3 (access enforcement), AC-4 (information flow enforcement),
  AC-6 (least privilege), IA-9 (service identification and authentication), CM-5 (access
  restrictions for change), AU-10 (non-repudiation).
- **ISO/IEC 42001 Annex A:** A.5, A.6, A.9.
- **CNSA 2.0:** ML-DSA-87 for chain entry signatures; dual-family (ML-DSA + SLH-DSA) at
  High-Assurance per OQGF-M-2.
- **Object-capability lineage:** consistent with the principle of attenuation in SPKI/SDSI
  and capability-based delegation models.

---

## AMD.5 Technical architecture (implementation hooks)

This section maps the amendment to the OQGF reference implementation (Part C), extending
the `oqgf-mhc` crate.

### AMD.5.1 Cryptographic construction

The Intent Provenance Chain is constructed as a **PQC-signed, attenuating credential chain**
combining two primitives, each chosen for a specific property:

**Attenuation integrity — keyed hash chaining (post-quantum safe).** Each intent caveat is
bound to the chain via an HMAC construction keyed on the prior chain state, in the manner of
macaroons. Symmetric primitives are quantum-resistant: Grover's algorithm yields only a
quadratic speedup, so HMAC-SHA-384 retains 192-bit security against a quantum adversary.
The append-only construction makes caveat removal or reordering computationally infeasible —
an attacker cannot recompute the chain HMAC without the per-hop keys. This delivers
Monotonic Intent Attenuation (OQGF-M-9): authority can only narrow.

**Non-repudiation — PQC signatures.** Keyed hashing proves the chain was not tampered with,
but does not prove *who* authored each derivation. Each chain entry is therefore additionally
signed under ML-DSA (dual-family with SLH-DSA at High-Assurance), binding the hop's attested
identity (OQGF-M-1) to the intent derivation it produced. This delivers the per-hop
non-repudiation required for Organ 5 forensic reconstruction and for AU-10.

**Lineage — hash-linked entries.** Each entry references the digest of the prior entry,
producing a tamper-evident chain back to the Root Intent. Any verifier can walk the chain
and confirm each link.

### AMD.5.2 Core types (extending oqgf-mhc)

```rust
/// The original authorized intent, issued by a DAP or authenticated principal.
pub struct RootIntent {
    pub principal: SubjectId,          // who authorized this
    pub dap: Dap,                      // accountable natural person (OQGF-A-5)
    pub scope: IntentScope,            // least-privilege authority (OQGF-M-13)
    pub invariants: InvariantSet,      // hard constraints (OQGF-M-10)
    pub nonce: Nonce,                  // freshness (OQGF-M-14)
    pub expiry: SystemTime,
    pub signature: DualSignature,      // ML-DSA (+ SLH-DSA at High-Assurance)
}

/// A single hop's derivation of intent from the prior chain state.
pub struct IntentChainEntry {
    pub hop_identity: Attestation,     // Signal 1 (OQGF-M-1)
    pub received_digest: Digest,       // digest of prior entry (lineage)
    pub emitted_intent: IntentScope,   // MUST be subset of received (OQGF-M-9)
    pub added_caveats: Vec<Caveat>,    // append-only restrictions
    pub added_invariants: InvariantSet,// MAY add, SHALL NOT remove (OQGF-M-10)
    pub chain_hmac: Hmac,              // attenuation integrity (post-quantum)
    pub signature: DualSignature,      // non-repudiation (Signal 2 authorship)
}

pub struct IntentProvenanceChain {
    pub root: RootIntent,
    pub entries: Vec<IntentChainEntry>,
}

pub trait CostimulationGate: Send + Sync {
    /// Grant privileged action only if BOTH identity (Signal 1) and a valid
    /// Intent Provenance Chain (Signal 2) verify. Otherwise return Anergy.
    fn authorize(
        &self,
        identity: &Attestation,
        chain: &IntentProvenanceChain,
        action: &Action,
    ) -> AuthorizationDecision; // Granted | Anergy { reason, signed_event }
}
```

### AMD.5.3 Verification algorithm

On every privileged action the Costimulation Gate SHALL:

1. Verify the identity attestation (Signal 1) per OQGF-M-1.
2. Verify the Root Intent signature and confirm the chain is not expired (OQGF-M-14).
3. Walk the chain from root to current hop. For each entry: verify the hash link to the
   prior entry, verify the chain HMAC, verify the PQC signature, and confirm
   `emitted_intent ⊆ received_intent` (monotonic attenuation, OQGF-M-9).
4. Confirm the proposed action lies within the current (most-attenuated) scope.
5. Evaluate the action against the accumulated invariant set (OQGF-M-10).
6. If all checks pass, grant. Otherwise return Anergy, emit a signed denial to Organ 2,
   and record it in Organ 5.

### AMD.5.4 What this closes, and what it does not

This amendment **closes** the following:

- Intent broadening across hops — cryptographically prevented by monotonic attenuation
  (OQGF-M-9), not merely detected.
- Intent reframing that violates a hard constraint — caught at every hop by invariant
  enforcement (OQGF-M-10), regardless of how the intent was reworded.
- Identity-only authorization — eliminated by the Costimulation Gate (OQGF-M-11);
  recognition without verified intent induces architectural anergy.
- Untraceable intent drift — eliminated by the full signed provenance chain (OQGF-M-8) and
  cross-hop behavioral reconciliation (OQGF-M-12).

This amendment **does not** fully close, and states so honestly:

- **Semantic reframing strictly within authorized scope.** If a Root Intent is scoped too
  broadly, an attacker can reframe within bounds to do something harmful that remains
  technically authorized. No cryptographic construction can fix authority that was
  over-granted at the root. The mitigation is OQGF-M-13 — the narrowest defensible Root
  Intent — and human-in-the-loop review (OQGF cross-organ A.6.3) for high-consequence
  actions. This is the residual gap, and it is a scoping and oversight problem, not a
  cryptographic one. The framework reduces the attack surface to exactly this residual and
  names it explicitly rather than claiming elimination.

---

## AMD.6 Traceability

| Requirement | Implementation hook |
| --- | --- |
| OQGF-M-8  | `oqgf-mhc::IntentProvenanceChain`, hash-linked signed entries |
| OQGF-M-9  | `IntentChainEntry` HMAC chaining + subset check on `emitted_intent` |
| OQGF-M-10 | `InvariantSet` evaluation at every hop in `CostimulationGate::authorize` |
| OQGF-M-11 | `CostimulationGate` returning `Anergy` on Signal-1-only or violation |
| OQGF-M-12 | Behavioral reconciliation feeding `oqgf-inflammation` graded response |
| OQGF-M-13 | `RootIntent::scope` least-privilege; DAP acceptance for broad scopes |
| OQGF-M-14 | `RootIntent::nonce` + `expiry`, bound to OQGF-M-4 credential lifetime |

---

## AMD.7 Change log

v1.0 — Initial public draft, 31 May 2026. Adds the Costimulation Requirement (OQGF-M-8
through OQGF-M-14) to Organ 3, closing the multi-hop intent-binding gap through verifiable
intent provenance, monotonic attenuation, invariant enforcement, and the two-signal
costimulation gate. Residual in-scope semantic reframing explicitly scoped to OQGF-M-13
and human oversight.

— End of OQGF Amendment 001.
