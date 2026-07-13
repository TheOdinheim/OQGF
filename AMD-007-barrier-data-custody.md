# OQGF-1.0 — NORMATIVE AMENDMENT 007
## The Barrier Requirement: Selective Boundary Control and Data Custody Across Trust Compartments

**Amendment ID:** OQGF-AMD-2026-007
**Amends:** OQGF-1.0, Part A, Section A.2 (Organ 2 — OQGF-I, Inflammation). Introduces the **Barrier Layer** as a named sub-function of Organ 2 and adds requirements **OQGF-I-8 through OQGF-I-15**. Does **not** modify OQGF-I-1 through OQGF-I-7; it extends the organ that already owns the boundary.
**Author:** Jeremy Rose, CEO — Odin's LLC, Wasilla, Alaska
**Date:** 10 July 2026
**Status:** Public draft for NIST, sector regulators, and the Odin's engineering team
**Normative dependencies:** OQGF-I (Organ 2, boundary + sentinels), OQGF-G (Organ 1, for the custody-record-as-bill-of-materials sibling and the AIBOM privileged-context link, OQGF-G-2), OQGF-M (Organ 3, the actor side of a crossing, OQGF-M-1), OQGF-A (Organ 5, recording); OQGF-P-2 (deterministic/heuristic boundary, AMD-002), OQGF-P-3 and OQGF-P-4 (central and peripheral tolerance, AMD-002), OQGF-P-7 (coordinated signaling, AMD-004), OQGF-P-8 (resolution, AMD-005), OQGF-P-9 (accountable risk acceptance, AMD-006); interacts with AMD-001 (costimulation / architectural anergy).

---

## AMD.0 Front matter

### AMD.0.1 Purpose of this amendment

OQGF-1.0 governs, at a trust boundary, **who** crosses (Organ 3, MHC attestation), **what artifact** is built and shipped (Organ 1, the Genetic Layer's CBOM and AIBOM), **what cryptographic exposure** the channel carries (Organ 2's HNDL sentinels), and, with AMD-001, **what an actor intends** when it acts. Each of these is a distinct object, well governed.

One object at the boundary is not yet governed: **the data content itself, crossing in either direction.** An actor may hold a perfect identity, present a valid attestation, carry a faithful intent chain, and move over a fully post-quantum channel — and still carry sensitive data out of a governed compartment into an ungoverned one, or bring data of unknown origin into a context where it will be treated as authoritative. Identity governs the mover. Intent governs the action. Neither governs the substance that crosses.

This is the governance object underneath the data-spillage and shadow-AI problem. An employee who pastes proprietary data into an unsanctioned external tool has committed no attestation failure, no artifact-provenance failure, no classical-TLS exposure, and — if authorized and acting in good faith — no intent-provenance failure. What has failed is **data custody**: sensitive data left a compartment the organization controls for one it does not, and nothing at the boundary was tasked with governing the crossing. The mirror direction fails the same way: data of unknown provenance enters and is silently admitted into a training corpus or a model registry, and the model inherits whatever that data carried.

This amendment makes data custody at the boundary a first-class, cryptographically accountable control. It introduces the Barrier Layer: a selective control on what data may cross a controlled trust boundary, in both directions, distinct from the identity, artifact, cryptographic, and intent controls that already operate there.

### AMD.0.2 Why this extends Organ 2 rather than forming a new organ

The framework distinguishes **organs** (anatomical structures — what a thing is and does) from the **Physiology Layer** (OQGF-P, systemic emergent behaviors — how the whole system acts). Data custody at the boundary is a structure, not a systemic behavior; it belongs with the organs.

Among the organs, its home is Organ 2. OQGF-I already owns every trust boundary: OQGF-I-1 deploys a sentinel network "at every network boundary that carries data classified above Public." The barrier is the **enforcement counterpart to the sentinel's detection** — the sentinel observes what crosses; the barrier decides whether it may. In immunology these are two halves of one interface: the microfold cell samples what is in the lumen, and the epithelial tight junction controls what passes. Housing them in one organ keeps a single trust boundary whole. Splitting boundary detection (Organ 2) from boundary enforcement (a separate organ) would fragment one boundary across two organs — the anti-pattern this framework avoids.

This mirrors the precedent of AMD-001, which housed intent binding — a genuinely distinct object — as an extension of the identity organ (OQGF-M) because intent is adjacent to identity. Data custody is adjacent to boundary detection, so it extends Organ 2. Two further points confirm the placement: a new top-level organ letter **B** would collide with the OQGF-B Baseline conformance designation; and the epithelial barrier is anatomically part of innate immunity, immediately adjacent to the inflammatory response that Organ 2 models. The Barrier Layer is therefore a named sub-function of Organ 2, with its own dedicated requirements (OQGF-I-8 through OQGF-I-15), not a distortion of the existing seven.

### AMD.0.3 The biological basis

The body is a set of **compartments** separated by **epithelial barriers**: the skin, the respiratory tract, the blood-brain barrier, and — the largest immune interface in the body — the gut mucosa. These barriers are the biological control surfaces for what crosses between compartments.

An epithelial barrier is not a passive wall. It is **selective and bidirectional**. Nutrients and water are actively transported inward; waste is moved outward; pathogens, toxins, and foreign antigens are excluded or sampled under control. Its structure has four elements that map directly onto data custody:

- **Tight junctions** between epithelial cells control what passes *between* them (the paracellular route), and regulated transporters control what passes *through* them (the transcellular route). The barrier's selectivity is a property of the boundary itself — not of the identity of any single actor. This is the **enforcement gate**.
- **Secretory IgA (sIgA)** in the overlying mucus binds and *tags* foreign material, marking what it is. This is the **custody record** — a mark that travels with the material and states something verifiable about it.
- **Microfold (M) cells** sample the luminal contents and present them to the immune system for inspection. This is the **content sentinel** — probabilistic sampling of what is trying to cross.
- **Barrier integrity** is load-bearing. When the epithelium is breached — "leaky gut" — luminal contents, including bacterial LPS, translocate into the bloodstream and trigger systemic inflammation. A breached barrier is not a quiet failure; it is an incident, because the compartment separation on which everything downstream depends has been lost.

A crucial detail governs the strictness of the barrier: **different compartments warrant different barriers.** The blood-brain barrier enforces a far stricter policy on what may enter the central nervous system than the gut mucosa enforces on the lumen. The strictness is a property of the compartment's value. This is the biological analog of **classification-dependent destination policy** and of the framework's conformance levels.

The translation is exact. An organization is a set of trust compartments separated by boundaries. The barrier at each boundary governs what data crosses — not by the identity of the mover (that is Organ 3), but by **what the data is** (its classification) and **where it is going** (destination policy), carried in a signed custody record that tags the data as sIgA tags an antigen, sampled by a content sentinel as M cells sample the lumen. Data routed around the barrier is the leaky-gut failure, and it is an incident in its own right.

### AMD.0.4 Terminology additions

- **Controlled Boundary** — a trust boundary the organization operates and can enforce at, between a governed compartment and a less-governed or ungoverned one (e.g., the egress point from a managed network, the interface between an internal data lake and an external service). The compartment interface.
- **Barrier** — the selective control at a Controlled Boundary that governs the crossing of data content in both directions. The epithelial tight-junction analog.
- **Boundary Custody Record (BCR)** — a signed statement of what a piece of data is and where it is authorized to go, carried with or matched to data crossing a Controlled Boundary. A bill of materials for data in transit, sibling to the CBOM (OQGF-G-1) and AIBOM (OQGF-G-2). The sIgA-tag analog.
- **Data Classification** — the declared sensitivity tier of a piece of data (e.g., Public, CUI, Secret), determining which destinations are authorized.
- **Destination Policy** — the declared set of destinations authorized to receive data of a given classification.
- **Privileged Context** — a context in which ingress data is treated as authoritative or is incorporated into artifacts from which models are built: a training corpus, evaluation dataset, fine-tuning corpus, model registry, or any AIBOM-governed artifact (OQGF-G-2).
- **Uncontrolled Channel** — a path through which governed data could leave outside barrier enforcement, because the organization does not operate or cannot enforce at that path (e.g., a personal device on a home network).
- **Barrier Bypass** — data crossing a Controlled Boundary outside the barrier's enforcement path. The breached-epithelium ("leaky gut") analog.

### AMD.0.5 Scope and relationship to AEGIS

The AMD-002 boundary (AMD.0.4 of that amendment) is reaffirmed. OQGF requires selective boundary control on data as a property of a conforming system. It does not mandate any particular data-loss-prevention product, cloud access security broker, or content-inspection engine. An operator MAY use such tooling to satisfy the heuristic-sentinel requirements and the enforcement requirements here, but OQGF neither requires nor depends on any product, and conformance is assessed against the requirements in this document. Where the amendment resembles a runtime data-security product, it does so to illustrate satisfiability, never to mandate a vendor.

### AMD.0.6 Design assumptions requiring confirmation

This amendment makes the following design calls. Each is the fail-safe default; flag any you wish to change.

1. **Egress enforcement of a declared classification is a Deterministic Gate; content inference is Heuristic.** Enforcing "data declared Secret may not go to an unauthorized destination" fires on a conserved danger pattern and is non-suppressible (OQGF-P-2). Guessing whether *unlabeled* data is sensitive is probabilistic and belongs on the trained, tolerable layer (OQGF-P-3, OQGF-P-4). Assumed because a known classification crossing to a forbidden destination is not a false positive to be tolerated, while content inference produces false positives that must be.
2. **Knowingly proceeding past the egress gate is Accountable Risk Acceptance, not suppression.** A deliberate, bounded decision to send classified data past the barrier for a legitimate reason is handled under OQGF-P-9 (AMD-006): recorded, scoped, expiring, DAP-signed, and visibly distinct from an unrestricted crossing. Assumed because the egress gate is a Deterministic Gate, and the only honest way past a Deterministic Gate is a visible, accountable acceptance that never hides the finding.
3. **Unprovenanced ingress is quarantined, not denied.** Data arriving without provenance is marked untrusted and barred from Privileged Contexts, but MAY be used in non-privileged contexts. Assumed because legitimately provenanceless data (public data) is useful and should not be discarded; only its promotion into model-building artifacts is gated.
4. **Enforcement is at controlled boundaries only, and uncontrolled channels are a named, managed obligation.** The barrier does not claim to enforce on what the organization does not control; it requires that uncontrolled channels be enumerated and their reliance reduced. Assumed because the framework states what it can enforce and refuses to overclaim what it cannot.

---

## AMD.1 Normative requirements

These requirements establish the Barrier Layer as a sub-function of Organ 2.

**OQGF-I-8 (Barrier at Controlled Boundaries).** A conforming system SHALL identify its Controlled Boundaries and SHALL deploy a Barrier at each that governs the crossing of data content in both directions. The Barrier is the enforcement counterpart to the OQGF-I-1 sentinel: the sentinel observes what crosses; the Barrier decides whether it may. A Controlled Boundary with no Barrier does not satisfy this requirement.

**OQGF-I-9 (Boundary Custody Record).** Data authorized to cross a Controlled Boundary above the Public classification SHALL carry, or be matched at the Barrier to, a signed Boundary Custody Record stating at minimum the data's classification, its origin, and the destinations authorized for that classification. The BCR is a bill of materials for data in transit — sibling to the CBOM (OQGF-G-1) and AIBOM (OQGF-G-2) — and SHALL be signed under a signature algorithm approved at the system's conformance level. A BCR that is unsigned, malformed, or expired SHALL NOT authorize a crossing.

**OQGF-I-10 (Egress Control — Deterministic, Fail-Closed).** Data of a declared classification above Public SHALL NOT cross a Controlled Boundary to a destination not authorized for that classification. Absent a valid BCR authorizing the crossing, the Barrier SHALL deny it. Enforcement of a declared classification against an unauthorized destination is a **Deterministic Gate** under OQGF-P-2 (AMD-002): it is fail-closed and non-suppressible, and no tolerance mechanism, exception, or operator action SHALL open it. A deliberate, bounded decision to send classified data past the Barrier for a legitimate reason that cannot yet be otherwise satisfied SHALL be handled as **Accountable Risk Acceptance** under OQGF-P-9 (AMD-006) — recorded, scoped, expiring, DAP-signed, its finding kept visible and its verdict visibly distinct from an unrestricted crossing — and SHALL NOT be expressed as suppression.

**OQGF-I-11 (Ingress Provenance).** Data entering across a Controlled Boundary without established provenance SHALL be marked untrusted and SHALL NOT enter a Privileged Context — a training corpus, evaluation dataset, fine-tuning corpus, model registry, or any AIBOM-governed artifact (OQGF-G-2) — until its provenance is established and recorded. Unprovenanced ingress data MAY be used in non-privileged contexts; it SHALL NOT be treated as authoritative, nor admitted to the artifacts from which models are built, on the strength of its mere arrival.

**OQGF-I-12 (Data-Content Sentinel — Heuristic).** The sentinel network (OQGF-I-1) SHALL include, at each Controlled Boundary, a data-content sentinel capable of identifying (a) classified or sensitive data attempting egress without a matching BCR, and (b) unprovenanced data attempting ingress into a Privileged Context, and of emitting a boundary-custody Signal per OQGF-P-7 (AMD-004). Content inference — judging whether *unlabeled* data is sensitive — is a **Heuristic Response** under OQGF-P-2: tolerance (OQGF-P-4) MAY apply to its false positives, and it SHALL be screened against the Self Set before deployment (OQGF-P-3). The heuristic sentinel is a backstop to, never a replacement for, the deterministic enforcement of declared classification (OQGF-I-10).

**OQGF-I-13 (Custody Decisions in Memory).** Every Barrier decision — a crossing allowed, denied, or quarantined, in either direction — SHALL be recorded in Organ 5 (OQGF-A) with the BCR digest or a record of its absence, the classification, the destination or origin, the deciding policy, and, where applicable, the accountable DAP. Boundary custody SHALL be reconstructable after the fact.

**OQGF-I-14 (The Uncontrolled-Channel Obligation).** The Barrier enforces only at boundaries the organization controls. A conforming system SHALL enumerate the Uncontrolled Channels through which governed data could leave outside Barrier enforcement, SHALL record that enumeration, and SHALL treat the reduction of reliance on those channels as a standing governance obligation — including by making the governed path the path of least resistance, so the incentive to use an Uncontrolled Channel is reduced rather than merely forbidden. The framework does not claim to enforce on what it does not control; it requires that what it does not control be named and managed, not ignored. A conforming system SHALL NOT represent Barrier enforcement as covering Uncontrolled Channels.

**OQGF-I-15 (Barrier-Bypass Detection).** A conforming system SHALL detect data crossing a Controlled Boundary outside the Barrier's enforcement path — a Barrier Bypass — and SHALL raise it through the OQGF-I graded-response engine (OQGF-I-6) and record it in Organ 5. A breached Barrier is an incident in its own right, on the principle that a Barrier's value depends on its being the only path across the boundary it governs.

---

## AMD.2 Conformance criteria per level

**Baseline (OQGF-B):** Barrier deployed at identified Controlled Boundaries (OQGF-I-8); signed BCR required for egress above Public (OQGF-I-9); deterministic, fail-closed egress control with knowingly-proceed routed through Accountable Risk Acceptance, never suppression (OQGF-I-10); Barrier decisions recorded in Organ 5 (OQGF-I-13); Uncontrolled Channels enumerated and recorded (OQGF-I-14). Single-PQC-family BCR signatures acceptable.

**Enhanced (OQGF-E):** All Baseline criteria, plus ingress-provenance gating into Privileged Contexts (OQGF-I-11); a data-content sentinel with central-tolerance screening and tolerable false positives (OQGF-I-12); Barrier-Bypass detection feeding the graded-response engine (OQGF-I-15); a documented reduction plan for the enumerated Uncontrolled Channels (OQGF-I-14).

**High-Assurance (OQGF-H):** All Enhanced criteria, plus dual-PQC-family BCR signatures (ML-DSA + SLH-DSA, consistent with OQGF-M-2); DAP-reviewed Destination Policy; full BCR retention in Organ 5 for the sector retention period; and periodic re-screening of the content sentinel against the evolving Self Set as the baseline changes (consistent with OQGF-P-6 High-Assurance).

---

## AMD.3 Assessment procedures

An auditor SHALL:

1. Attempt to egress data of a declared classification above Public to a destination not authorized for that classification, and confirm the Barrier denies it fail-closed; confirm no tolerance mechanism, exception, or operator action can open it (OQGF-I-10). **This is the load-bearing test of this amendment.**
2. Attempt to send classified data past the Barrier and confirm the only permitted path is an Accountable Risk Acceptance under OQGF-P-9 that keeps the finding visible and produces a verdict distinct from an unrestricted crossing — not a suppression (OQGF-I-10 / AMD-006).
3. Present data with an expired or malformed BCR and confirm the crossing is denied (OQGF-I-9, OQGF-I-10).
4. Introduce unprovenanced data at ingress and confirm it cannot enter a training corpus, evaluation set, fine-tuning corpus, or model registry until provenance is established and recorded, while confirming it remains usable in a non-privileged context (OQGF-I-11).
5. Inject sensitive data without a classification label and confirm the content sentinel flags it and emits a Signal, and confirm its false positives are tolerable and screened rather than fail-closed (OQGF-I-12).
6. Route data around the Barrier and confirm the Bypass is detected, raised through the graded-response engine, and recorded (OQGF-I-15).
7. Inspect Organ 5 and confirm crossings — allowed, denied, and quarantined — are recorded with BCR digest (or its absence), classification, destination or origin, and deciding policy (OQGF-I-13).
8. Inspect the enumerated Uncontrolled-Channel register and its reduction plan, and confirm no material represents Barrier enforcement as covering those channels (OQGF-I-14).

---

## AMD.4 Control mappings

- **NIST AI RMF:** MAP-4.1 (provenance and lineage), MEASURE-2.6, MANAGE-2.1, GOVERN-6.1 (data and third-party governance).
- **NIST SP 800-53 Rev. 5:** **AC-4 (Information Flow Enforcement)** — the central mapping, including enhancements on flow control by data classification and on preventing encrypted data from bypassing content-checking mechanisms; **SC-7 (Boundary Protection)**; AC-3 (access enforcement); AC-21 (information sharing); AC-23 (data mining protection); MP-6 (media handling, as the physical-media analog of a crossing); SI-4 (system monitoring, the content sentinel); AU-2, AU-10 (recording and non-repudiation of custody decisions); SC-8 (transmission confidentiality and integrity).
- **ISO/IEC 42001 Annex A:** A.7 (data for AI systems, including provenance), A.10 (third-party and customer relationships).
- **ISO/IEC 27001 lineage:** A.5.14 (information transfer), A.8.10 and A.8.12 (data leakage prevention and information deletion) as the established data-boundary controls this generalizes.
- **CNSA 2.0:** ML-DSA-87 for BCR signatures; dual-family (ML-DSA + SLH-DSA) at High-Assurance per OQGF-M-2.
- **EU AI Act:** Article 10 (data governance and training-data provenance) for the ingress path; Article 15 (cybersecurity) for the egress path.
- **Cross-discipline lineage:** consistent with data-loss-prevention (DLP) egress control, cloud access security broker (CASB) enforcement, data provenance and lineage systems, and zero-trust data security — in which the boundary and the data, not the network perimeter, are the control point.

---

## AMD.5 Technical architecture (implementation hooks)

The Barrier is an enforcement point at a Controlled Boundary; the Boundary Custody Record is a core type (`oqgf-core`), a sibling to `Cbom` and `Aibom`; the data-content sentinel extends the existing `oqgf-inflammation` sentinel network; and every decision is written to `oqgf-memory` (Organ 5). The deterministic egress gate reuses the AMD-002 `ResponseClass::Deterministic` discipline, and the knowingly-proceed path reuses the AMD-006 `RiskAcceptance` type unchanged. No second DAP type is introduced; the existing `DesignatedAccountableParty` is reused.

### AMD.5.1 Core types

```rust
/// A signed statement of what a piece of data is and where it is authorized
/// to go, carried with or matched to data crossing a Controlled Boundary.
/// The secretory-IgA / molecular-tag analog. Structurally a bill of materials
/// for data-in-transit, sibling to Cbom (OQGF-G-1) and Aibom (OQGF-G-2).
pub struct BoundaryCustodyRecord {
    pub data_ref: DataRef,                    // content digest of the data covered
    pub classification: DataClassification,   // Public, CUI, Secret, ... (OQGF-I-9)
    pub origin: OriginId,                      // provenance root
    pub authorized_destinations: DestinationPolicy, // where it MAY go (OQGF-I-9)
    pub issued: SystemTime,
    pub expiry: SystemTime,                    // SHALL bound validity (OQGF-I-9)
    pub signature: DualSignature,              // ML-DSA (+ SLH-DSA at High-Assurance)
}

/// Direction of a boundary crossing.
pub enum CrossingDirection { Egress, Ingress }

/// The Barrier's verdict on a proposed crossing (OQGF-I-10, OQGF-I-11).
/// Fail-closed: absent valid custody for the destination, Deny.
pub enum BarrierVerdict {
    /// Crossing permitted; the matched custody record is carried for the record.
    Allow { record: BoundaryCustodyRecord },
    /// Egress of declared-classification data to an unauthorized destination,
    /// or a missing/expired/malformed BCR. Deterministic, non-suppressible
    /// (OQGF-I-10 / OQGF-P-2). A knowingly-proceed decision is expressed as an
    /// AMD-006 RiskAcceptance applied to this finding, NEVER as suppression.
    Deny { reason: DenyReason, finding: BoundaryFinding },
    /// Ingress without established provenance: untrusted holding. Usable in
    /// non-privileged contexts; barred from any Privileged Context (OQGF-I-11).
    Quarantine { reason: DenyReason },
}

pub trait Barrier: Send + Sync {
    /// Evaluate a proposed crossing. Egress of declared-classification data above
    /// Public requires a valid BCR authorizing the destination (OQGF-I-10);
    /// ingress without provenance yields Quarantine (OQGF-I-11). Records the
    /// decision in Organ 5 (OQGF-I-13). The egress deny is a Deterministic Gate:
    /// this method SHALL NOT expose a path that suppresses a Deny into an Allow;
    /// the only permitted override is an AMD-006 RiskAcceptance, applied upstream,
    /// which keeps the finding visible.
    fn evaluate(
        &self,
        data: &DataDescriptor,
        direction: CrossingDirection,
        boundary: &ControlledBoundary,
    ) -> BarrierVerdict;
}

/// A data-content sentinel: identifies classified data attempting egress without
/// a matching BCR, and unprovenanced data attempting ingress into a Privileged
/// Context, emitting a boundary-custody Signal (OQGF-P-7 / AMD-004). Extends the
/// OQGF-I-1 sentinel network. Content inference is a Heuristic Response
/// (OQGF-P-2): its false positives are tolerable (OQGF-P-4) and it is screened
/// against the Self Set before deployment (OQGF-P-3). (OQGF-I-12)
pub trait DataContentSentinel: Send + Sync {
    fn inspect(&self, flow: &BoundaryFlow) -> Option<BoundaryCustodyEvent>;
}

/// Detection of data crossing outside the Barrier's enforcement path (OQGF-I-15).
/// The breached-epithelium analog; raised through the OQGF-I-6 graded response.
pub trait BypassDetector: Send + Sync {
    fn scan(&self, boundary: &ControlledBoundary) -> Vec<BarrierBypass>;
}
```

The type system carries the safety property: `Deny` is a distinct variant of `BarrierVerdict`, and there is no method that turns a `Deny` into an `Allow`. The only sanctioned way past a deterministic egress `Deny` is an `AcceptedRisk` verdict produced by the AMD-006 `RiskAcceptanceRegistry` applied to the finding — which keeps the finding visible and the verdict distinct. OQGF-I-10's non-suppressibility is enforced structurally, in the spirit of OQGF-P-2.

### AMD.5.2 What this closes, and what it does not

This amendment **closes** the following:

- **Ungoverned data egress across controlled boundaries** — sensitive data leaving a governed compartment for an unauthorized destination is now gated, classified, and fail-closed (OQGF-I-8, OQGF-I-10).
- **Silent admission of unprovenanced data into model-building artifacts** — ingress data of unknown origin is quarantined and cannot enter a training corpus, evaluation set, fine-tuning corpus, or model registry until provenance is established (OQGF-I-11).
- **Crossings with no custody record** — a signed Boundary Custody Record is now required to authorize a crossing above Public (OQGF-I-9).
- **Untracked crossings** — every allowed, denied, and quarantined crossing is recorded in Organ 5 (OQGF-I-13).
- **Siloed boundary detection** — the data-content sentinel emits Signals that raise posture across organs via AMD-004 (OQGF-I-12).
- **Confusion of preventive control with detection** — the deterministic policy gate (declared classification to an unauthorized destination) and the heuristic content sentinel (inference over unlabeled data) are cleanly separated, honoring the AMD-002 innate/adaptive boundary (OQGF-I-10, OQGF-I-12).
- **The barrier being quietly routed around** — a Barrier Bypass is detected and raised as an incident (OQGF-I-15).

This amendment **does not** fully close, and states so honestly:

- **Uncontrolled channels.** Data that leaves through a channel the organization does not operate — a personal device on a home network — is outside Barrier enforcement, and no Barrier can reach it. This is the same shape as the residuals of AMD-001 (over-broad Root Intent), AMD-002 (the Self Set), and AMD-006 (the risk decision): the framework reduces the surface to exactly this case and **names it** rather than claiming elimination. OQGF-I-14 makes the naming and the reduction of reliance a normative obligation, but the residual mitigation is governance and usability — making the governed path frictionless so the incentive to use an Uncontrolled Channel collapses — not a cryptographic guarantee. The framework does not claim what it cannot enforce.
- **Classification accuracy.** The deterministic gate enforces on data whose classification is correctly assigned. Data whose sensitivity is mislabeled — sensitive content marked Public — creates a hole in the deterministic gate. This is the same shape as the AMD-002 Self Set residual. It is mitigated by the heuristic content sentinel (OQGF-I-12), which may catch mislabeled data by inspecting content, and by classification governance with DAP accountability — but content inference has its own limits, stated next.
- **Covert-channel and semantic exfiltration.** A determined insider can encode sensitive data to evade content inspection — steganography, paraphrase, or drip exfiltration in fragments each below a detection threshold. Content-based detection reduces this but cannot eliminate it; it is a fundamental limit of inspecting content rather than proving custody. This is the data-exfiltration analog of the AMD-001 in-scope-semantic-reframing residual: the deterministically closable part is closed, and what remains is the semantic residual, named rather than claimed solved.
- **Upstream provenance truth.** The Barrier verifies a BCR's signature but cannot verify the truth of what an upstream source attested about a datum's origin. A compromised-but-valid upstream signer can emit false-but-well-formed provenance. This is the same shape as the AMD-001 upstream-signer residual: signature verification proves who attested, not that the attestation is true.

---

## AMD.6 Traceability

| Requirement | Implementation hook |
| --- | --- |
| OQGF-I-8 | `oqgf-inflammation::Barrier` deployed per `ControlledBoundary`; paired with the OQGF-I-1 sentinel network |
| OQGF-I-9 | `oqgf-core::BoundaryCustodyRecord` (signed, classified, expiring); sibling to `bom::Cbom` / `bom::Aibom` |
| OQGF-I-10 | `Barrier::evaluate` returning `Deny` (Deterministic, `ResponseClass::Deterministic`); knowingly-proceed via AMD-006 `RiskAcceptanceRegistry::apply` → `AcceptedRisk`, never suppression |
| OQGF-I-11 | `Barrier::evaluate` returning `Quarantine`; Privileged-Context admission gated on recorded provenance; ties to `bom::Aibom` (OQGF-G-2) |
| OQGF-I-12 | `oqgf-inflammation::DataContentSentinel`; emits `Signal` (AMD-004); screened via AMD-002 `ToleranceController::screen` (OQGF-P-3); false positives via `ToleranceGrant` (OQGF-P-4) |
| OQGF-I-13 | Barrier decisions recorded in `oqgf-memory`; dual-signed at High-Assurance |
| OQGF-I-14 | Uncontrolled-Channel register + reduction plan recorded in `oqgf-memory`; no path represents enforcement over uncontrolled channels |
| OQGF-I-15 | `oqgf-inflammation::BypassDetector::scan` → OQGF-I-6 graded response; incident recorded in `oqgf-memory` |

---

## AMD.7 Change log

v1.0 — Initial public draft, 10 July 2026. Introduces the Barrier Layer as a named sub-function of Organ 2 (OQGF-I) and adds OQGF-I-8 through OQGF-I-15, closing the data-custody-at-the-boundary gap: selective control on what data crosses a Controlled Boundary in both directions. Specifies the Boundary Custody Record (a signed bill of materials for data in transit, sibling to CBOM and AIBOM); deterministic, fail-closed egress control of declared classification against unauthorized destinations; ingress-provenance gating that quarantines unprovenanced data from Privileged Contexts; a heuristic data-content sentinel screened under self-tolerance; recording of every crossing in Organ 5; the normative obligation to enumerate and reduce reliance on Uncontrolled Channels; and Barrier-Bypass detection. The load-bearing safety inheritance is OQGF-P-2: the egress classification gate is a Deterministic Gate, non-suppressible, and the only sanctioned way past it is an AMD-006 Accountable Risk Acceptance that keeps the finding visible — never suppression. Content inference is confined to the heuristic, tolerable layer (OQGF-P-3, OQGF-P-4), preserving the AMD-002 innate/adaptive boundary. Complements AMD-001 (which governs the mover and the action) by governing the substance that crosses. Four residuals are named rather than claimed eliminated — uncontrolled channels, classification accuracy, covert-channel exfiltration, and upstream provenance truth — each mapped to the shape of a prior amendment's residual.

— End of OQGF Amendment 007.
