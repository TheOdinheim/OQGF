# OQGF-1.0 — Odins Quantum AI/ML Governance Framework

OQGF is an AI security and governance framework modeled on the human immune system, written for federal and critical-infrastructure environments preparing for the post-quantum transition. It is built around five organs — Genetic (compliance-as-code), Inflammation (assumed breach), MHC (zero trust), Redundant Defense, and Memory (360-degree accountability) — plus a cross-cutting Physiology Layer that states properties all five organs must collectively exhibit.

Start with [OQGF-1_0.md](OQGF-1_0.md). It contains the five organs, the shared Physiology Layer, and the integrated requirements, tier criteria, and assessments from all eighteen amendment documents and the Organ 5 evidence-capture patch. The separate amendment files remain in place for their rationale, research, source assumptions, and change history. You do not need to apply them separately to reconstruct the current normative reading.

The framework remains a public draft. The **8 October 2026 consistency revision** resolves the identified wording conflicts across requirements, tiers, assessments, amendments, and architecture notes. The [resolution record](OQGF-1_0.md#synchronization-review) explains 24 issue groups and their effect; the [common rules](OQGF-1_0.md#a09-common-interpretation-signature-profiles-and-assessment-limits) define precedence, signature roles, retention, and assessment limits. No implementation conformance is claimed. [The integration map](OQGF-1_0.md#integration-map) records the revisions used, including AMD-011.1, 012.1, 014.1, 017.1, AMD-006 v2, and AMD-002 editorial v1.1.

## Read by organ

| Section | Current requirements |
|---|---|
| [Organ 1](OQGF-1_0.md#organ-1) | Genetic Layer / compliance as code, with shared lifecycle and governance connections |
| [Organ 2](OQGF-1_0.md#organ-2) | Inflammation / assumed breach, including the Barrier Layer |
| [Organ 3](OQGF-1_0.md#organ-3) | Identity, attestation, and intent provenance |
| [Organ 4](OQGF-1_0.md#organ-4) | Redundant defense and tiered key custody |
| [Organ 5](OQGF-1_0.md#organ-5) | Evidence, explanation validity, and independent capture |
| [Shared physiology](OQGF-1_0.md#physiology) | Requirements that govern multiple organs together |

For each future amendment, update its source file and the corresponding framework requirements, tiers, assessments, dependencies, and architecture notes in the same change. Preserve requirement identifiers and record the update in the framework change log.

## Documents

| File | Title |
|---|---|
| [OQGF-1_0.md](OQGF-1_0.md) | Odins Quantum AI/ML Governance Framework (OQGF-1.0) — Formal Specification, Whitepaper, and Technical Architecture |
| [AMD-001-intent-binding.md](AMD-001-intent-binding.md) | The Costimulation Requirement: Intent Provenance Binding for Multi-Hop Agentic Systems |
| [AMD-002-self-tolerance.md](AMD-002-self-tolerance.md) | The Self-Tolerance Requirement: The Physiology Layer and the Bound on Host Harm |
| [AMD-003-adaptation.md](AMD-003-adaptation.md) | The Adaptation Requirement: Affinity Maturation for Incident-Driven Detection |
| [AMD-004-coordinated-signaling.md](AMD-004-coordinated-signaling.md) | The Coordinated Signaling Requirement: Cytokine-Style Posture Coupling Without Central Command |
| [AMD-005-resolution-homeostasis.md](AMD-005-resolution-homeostasis.md) | The Resolution Requirement: Active Return to Baseline and the Bound on Chronic Escalation |
| [AMD-006-accountable-risk-acceptance.md](AMD-006-accountable-risk-acceptance.md) | The Accountable Risk Acceptance Requirement: Recorded, Non-Suppressing Acceptance of a Deterministic-Gate Finding |
| [AMD-007-barrier-data-custody.md](AMD-007-barrier-data-custody.md) | The Barrier Requirement: Selective Boundary Control and Data Custody Across Trust Compartments |
| [AMD-008-risk-surveillance.md](AMD-008-risk-surveillance.md) | The Risk Surveillance Requirement: Continuous Identification, Assessment, and Disposition of Risk |
| [AMD-009-personal-data-lifecycle.md](AMD-009-personal-data-lifecycle.md) | The Personal Data Requirement: Lifecycle Obligations for Personal Data as a Governed Classification |
| [AMD-010-explanation-validity.md](AMD-010-explanation-validity.md) | The Explanation Validity Requirement: Bounded Scope, Null Explanations, and Channel Attestation for Quantum-Appropriate Explainability at Scale |
| [AMD-011-capability-triggered-assurance.md](AMD-011-capability-triggered-assurance.md) | The Capability-Triggered Assurance Requirement: Dual-Axis Determination and Containment Governance for Autonomous Agent Systems |
| [AMD-012-recursive-risk-propagation.md](AMD-012-recursive-risk-propagation.md) | The Recursive Risk-Propagation Requirement: Governing Residual, Induced, and Downstream Risk in Machine-Speed AI Systems |
| [AMD-013-recursive-inferential-privacy.md](AMD-013-recursive-inferential-privacy.md) | The Recursive Inferential Privacy Requirement: Governing Knowledge Created by Authorized Disclosure |
| [AMD-014-adaptive-containment.md](AMD-014-adaptive-containment.md) | The Adaptive Containment Requirement: Monotonic Capability Contraction for Autonomous Systems Under Boundary Pressure |
| [AMD-015-cognitive-integrity.md](AMD-015-cognitive-integrity.md) | The Cognitive Integrity Requirement: Provenance-Bound Semantic Authority and Instruction/Data Separation |
| [AMD-016-threat-model-assurance.md](AMD-016-threat-model-assurance.md) | The Threat-Model Assurance Requirement: Provenance, Freshness, Coverage, and Continuous Adversarial Reconciliation |
| [AMD-017-model-lifecycle-assurance.md](AMD-017-model-lifecycle-assurance.md) | The Model Lifecycle Assurance Requirement: Training Provenance, Alignment Integrity, and Weight-to-Serving Attestation |
| [OQGF-organ5-evidence-capture-hardening-patch.md](OQGF-organ5-evidence-capture-hardening-patch.md) | Patch — OQGF Organ 5 Evidence-Capture Hardening |
| [AMD-018-key-custody-tier-resolution.md](AMD-018-key-custody-tier-resolution.md) | Key Custody Tier Resolution: Resolving the OQGF-R-6 Contradiction Between Unconditional and Tiered Threshold Custody |

## Design principles

**Fail-safe asymmetry.** Deterministic gates retain findings and fail closed without valid evidence and authorization. P-9 permits only scoped, policy-eligible accepted-risk outcomes; these are not clean conformance results. Raw autonomous Signals only raise posture. Resolution follows P-8; P-15 containment restoration requires DAP authorization wherever it applies.

**The model is never in the trust path.** For any blocking, licensing, or posture-changing decision, the machine-learning component is advisory only. A deterministic spine makes the binding calls.

**The governor is itself governed.** Privileged actions of the governance system are subject to the same costimulation requirements it enforces. There is no god mode.

## Status

Public draft for NIST, sector regulators, and practitioners. Amendments retain their IDs and dated history and carry the current maintenance date. This repository contains 21 documentation files, not the proposed Rust/Python implementation, assessor accreditation, or deployment certifications. CNSA mappings do not authorize the civilian dual-family profile for National Security Systems; the explicit compatibility boundary is in A.0.9. No new amendment number is introduced by this consistency revision.

## Author

Jeremy Rose, CEO — Odins LLC, Wasilla, Alaska

© 2026 Odins LLC. All rights reserved.
