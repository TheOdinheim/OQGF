# OQGF-1.0 — NORMATIVE AMENDMENT 017
## The Model Lifecycle Assurance Requirement: Training Provenance, Alignment Integrity, and Weight-to-Serving Attestation

**Amendment ID:** OQGF-AMD-2026-017
**Amends:** OQGF-1.0, Section A.P (Physiology Layer). Adds a new requirement, OQGF-P-18.
Does **not** modify OQGF-G-2 (AIBOM) or OQGF-G-3 (artifact signing); it extends the lifecycle
governance of the model artifact those requirements inventory and sign, per the OQGF annotation
convention. OQGF-G-2 inventories what a model IS; this amendment governs how it BECAME that, and
whether what is serving is what was governed.
**Author:** Jeremy Rose, CEO — Odin's LLC, Wasilla, Alaska
**Date:** 21 August 2026
**Status:** Public draft for NIST, sector regulators, and the Odin's engineering team
**Implementation posture:** Implementation-neutral. A conforming organization MAY use any
training framework, alignment technique, fine-tuning method, serving infrastructure, or model
family. This amendment governs the lifecycle properties, not the tools.
**Normative dependencies:** OQGF-G-2 (AIBOM — the inventory this amendment extends with
lifecycle provenance); OQGF-G-3 (artifact signing — the cryptographic foundation this amendment
builds on for weight integrity); OQGF-G-4 (Deterministic Gate — the non-bypassable build gate);
OQGF-I-11 (AMD-007, ingress provenance — training data as Privileged Context ingress);
OQGF-P-10 (AMD-008, Risk Surveillance — safety-capability tradeoffs and training incidents as
risk); OQGF-P-12 (AMD-011, Capability-Triggered Assurance — the deployed Capability Envelope);
OQGF-P-16 (AMD-015, Cognitive Integrity — alignment as the origin of the model's semantic-
authority behavior); OQGF-P-2 (AMD-002, deterministic/heuristic boundary); OQGF-A-1/OQGF-A-5
(Organ 5 recording and the DAP); OQGF-M-2 (dual-PQC-family signatures); CNSA 2.0.

---

## AMD.0 Front matter

### AMD.0.1 Purpose of this amendment

OQGF governs what a model does — its intent (AMD-001), data crossings (AMD-007), capabilities
(AMD-011), containment (AMD-014), semantic authority (AMD-015), risk propagation (AMD-012),
inferential privacy (AMD-013), threat-model quality (AMD-016), and explanation validity
(AMD-010). OQGF-G-2 inventories what a model is — its components, datasets, frameworks, and
licenses. OQGF-G-3 signs the resulting artifact.

What remains ungoverned is the **lifecycle between raw materials and deployed model** — the
process by which training data, alignment procedures, fine-tuning decisions, and weight
integrity assurance produce the model that will be governed by everything else.

This matters because the model's training is the origin of its behavior. A model fine-tuned on
cybersecurity data measurably degrades in safety alignment (documented in CyberLLMInstruct
research: cyber fine-tuning erodes safety benchmarks). A model whose weights are silently
substituted between signing and serving may behave entirely differently from the model that was
evaluated. A fine-tuned variant produced from a governed base model without its own provenance
is an ungoverned derivative wearing a governed parent's credentials. A model whose alignment
procedure used an undocumented reward model has an unauditable behavioral origin.

The AIBOM lists training data sources. It does not require those sources to carry per-dataset
provenance, epistemic classification, license verification, or contamination assessment. It
does not require the alignment process to be documented as a governed lifecycle event. It does
not require that fine-tuning produce a new governed artifact with its own safety evaluation.
It does not require that the model serving inference be cryptographically verified against the
model that passed governance at the point of serving, not just at the point of signing.

This amendment closes those gaps by governing the model's lifecycle from training data through
alignment through fine-tuning through deployment attestation — the full provenance chain from
raw materials to served weights.

### AMD.0.2 Why this is not an extension of OQGF-G-2

OQGF-G-2 is a component inventory requirement in Organ 1 (the Genetic Layer). It answers:
*what is this model made of?* This amendment answers a different question: *how did those
materials become this model, was the process governed, and is the model serving inference the
model that was governed?*

The lifecycle spans multiple organs. Training data provenance involves Organ 2 (ingress via
AMD-007 I-11). Alignment governance involves Organ 5 (the recorded decisions and tradeoffs).
Weight integrity involves Organ 3 (attestation that the served model matches the signed
artifact). Fine-tuning governance involves Organ 1 (new AIBOM), Organ 5 (recorded event), and
Organ 3 (new attestation). Safety-capability tradeoff governance involves AMD-008 (risk
register). No single organ owns the model lifecycle. It is a systemic property — Physiology,
at P-18.

### AMD.0.3 The biological basis

The immune system's recognition capability is not arbitrary. It is produced through a governed
developmental process with quality control at every stage.

**V(D)J recombination** in the bone marrow and thymus generates the diversity of T-cell and
B-cell receptors — the raw recognition capability. This is the training phase: raw materials
(gene segments) are assembled into a functional receptor (the model). The process is stochastic
and produces enormous diversity, but it is not ungoverned — recombination-activating genes (RAG1,
RAG2) control the process, and the resulting receptors are subject to checkpoints.

**Thymic selection** is the alignment phase. Developing T cells undergo positive selection (can
you recognize self-MHC? — functional competence) and negative selection (do you react too
strongly to self-antigens? — safety). Cells that fail positive selection die by neglect — they
are non-functional. Cells that fail negative selection die by apoptosis — they are dangerous.
Only cells that pass both checkpoints are released to the periphery. The alignment process is
itself governed: the thymic epithelial cells that present self-antigens are a dedicated quality-
control infrastructure, not the developing T cells checking themselves.

**Peripheral tolerance** is the post-deployment safety layer. Even after thymic selection, some
self-reactive cells escape. Regulatory T cells, anergy, and activation-induced cell death
provide ongoing safety enforcement in the periphery — the inference-time guardrails.

The translation:

Training data → gene segments (raw materials). Training process → V(D)J recombination
(assembly). Alignment (RLHF/DPO) → thymic selection (positive: is it competent? negative: is it
dangerous?). Safety benchmarking → the checkpoint between selection and release. Weight signing
→ the "release to periphery" attestation that the cell that enters circulation is the cell that
passed selection. Deployment attestation → peripheral immune surveillance confirming the cells
in circulation are the right ones. Fine-tuning → somatic hypermutation (further specialization
of an already-selected cell, producing new diversity that must itself be re-selected). Model
retirement → senescence/apoptosis of cells that are no longer needed or have become dangerous.

The immune system does not release a T cell to the periphery and then trust that it will forever
be the same cell that passed selection. Peripheral tolerance mechanisms continuously verify. The
governance framework must not sign a model's weights once and then trust that the same weights
are serving six months later without re-verification.

### AMD.0.4 Terminology additions

- **Training Provenance Record** — a governed record of the datasets, preprocessing, and
  conditions under which a model was trained, extending the AIBOM from a component list to a
  lifecycle record.
- **Dataset Provenance** — per-dataset metadata: source, collection method, license, hash,
  size, date range, preprocessing, known biases, contamination assessment, and epistemic
  classification (curated/crawled/synthetic/augmented/unknown).
- **Alignment Record** — a governed record of the alignment process: technique (RLHF, DPO,
  constitutional, instruction tuning), reward model provenance, preference dataset provenance,
  safety benchmarks before and after, and the safety-capability tradeoff assessment.
- **Safety-Capability Tradeoff** — the documented change in safety alignment caused by domain
  specialization. A model fine-tuned for cybersecurity may gain capability while losing safety;
  the tradeoff is measured, recorded, and governed.
- **Fine-Tuning Event** — a governed lifecycle event producing a new model variant from a base,
  with its own provenance, AIBOM extension, safety re-evaluation, and weight signature.
- **Weight Integrity Attestation** — cryptographic verification at serving time that the model
  weights loaded into inference are the weights that were signed after governance. PQC-signed
  (ML-DSA-87; dual-family at High-Assurance per OQGF-M-2).
- **Base-Model License Compliance** — documented compliance with the base model's acceptable-use
  policy and license terms, recorded as a governance obligation rather than an afterthought.
- **Model Retirement** — governed withdrawal of a model version from service: superseded,
  found unsafe, training data compromised, or alignment invalidated.

### AMD.0.5 Design assumptions requiring confirmation

All were ratified by the DAP on 21 August 2026 and are recorded here as decided.

1. **Standalone placement at OQGF-P-18.** *(Ratified.)* The model lifecycle spans Organs 1, 2,
   3, and 5 plus AMD-008 risk governance. No single organ owns it.
2. **Implementation-neutral.** *(Ratified.)* Any training framework, alignment technique, or
   serving infrastructure may conform if the lifecycle properties are satisfied.
3. **Per-dataset provenance is required, not just per-AIBOM.** *(Ratified.)* An AIBOM that
   lists "Common Crawl" without recording the snapshot date, hash, preprocessing, or known
   contamination is an inventory, not provenance.
4. **Alignment is a governed lifecycle event, not an implementation detail.** *(Ratified.)* The
   alignment process (reward model, preference data, technique, safety benchmarks) is recorded
   and auditable.
5. **Fine-tuning produces a new governed artifact.** *(Ratified.)* A fine-tuned variant inherits
   the base model's governance and extends it with its own provenance, safety re-evaluation, and
   weight signature. It does not silently ride the base model's credentials.
6. **Weight integrity is verified at serving time, not only at signing time.** *(Ratified.)* A
   model signed six months ago and never re-verified may not be the model currently serving.
7. **Safety-capability tradeoffs are measured and recorded.** *(Ratified.)* Domain fine-tuning
   that degrades safety alignment is not prohibited — it is governed. The tradeoff is measured,
   recorded, entered into the risk register, and accepted or remediated.
8. **Base-model license compliance is a governance obligation.** *(Ratified.)* Where the base
   model carries use restrictions (Meta AUP, export controls), compliance is documented in the
   lifecycle record.

---

## AMD.1 Normative requirements

These requirements add OQGF-P-18 to Section A.P. They do not modify OQGF-G-2 or OQGF-G-3;
they extend the lifecycle governance of the model artifact those requirements inventory and sign.

**OQGF-P-18.1 (Training Provenance Record).** A model used in a governed AI/ML system SHALL
have a Training Provenance Record extending the OQGF-G-2 AIBOM with lifecycle provenance: the
datasets used, the training configuration, the training infrastructure, the responsible DAP,
and the date. The Training Provenance Record is a governed extension of the AIBOM, not a
replacement; the AIBOM continues to serve its existing inventory function.

**OQGF-P-18.2 (Dataset Provenance).** Each material training dataset referenced in the Training
Provenance Record SHALL carry Dataset Provenance: source and collection method; license and
terms; cryptographic hash (SHA-256 or SHA-3); size and date range; preprocessing applied; known
biases or limitations; contamination assessment (benchmark leakage, PII, copyrighted material,
adversarial content); and epistemic classification (curated, crawled, synthetic, augmented,
unknown). Unknown provenance SHALL be recorded as unknown, not silently omitted. A dataset whose
provenance cannot be established SHALL be treated as unprovenanced ingress under OQGF-I-11
(AMD-007) for the purpose of determining whether it may enter a training corpus.

**OQGF-P-18.3 (Alignment Governance).** The alignment process — RLHF, DPO, constitutional AI,
instruction tuning, safety training, or any technique that shapes the model's behavioral
properties — SHALL be recorded as a governed lifecycle event. The Alignment Record SHALL
include: the technique and its parameters; the reward model or preference dataset (with its own
provenance); safety benchmarks evaluated before and after alignment; the responsible DAP; and
the version. A model whose alignment process is undocumented — whose behavioral origin is an
unauditable black box — does not satisfy this requirement.

**OQGF-P-18.4 (Safety-Capability Tradeoff).** Where domain-specific fine-tuning or continued
pretraining materially changes the model's safety alignment — measured by established safety
benchmarks — the change SHALL be recorded as a Safety-Capability Tradeoff, assessed, and
entered into the OQGF-P-10 Risk Register (AMD-008). A degradation in safety alignment is not
prohibited; it is governed. The tradeoff SHALL be measured (before and after), documented
(which benchmarks, what magnitude), owned (a named DAP), and either remediated (additional
safety training, guardrails, capability restrictions) or accountably accepted under OQGF-P-9
(AMD-006). A system that fine-tunes for domain capability without measuring the safety impact
does not satisfy this requirement.

**OQGF-P-18.5 (Weight Integrity Attestation).** The model weights loaded into inference SHALL be
cryptographically verified against the signed artifact produced after governance. Verification
SHALL occur at model load time, not only at the original signing event. The signature SHALL be
PQC (ML-DSA-87; dual-family ML-DSA + SLH-DSA at High-Assurance per OQGF-M-2). A model whose
weights are signed once and served for months without re-verification does not satisfy this
requirement — the served weights must be the governed weights, verified at the point of serving.
Discovery that served weights do not match the signed artifact SHALL constitute a weight-integrity
failure, triggering incident response under A.6.1.

**OQGF-P-18.6 (Fine-Tuning as a Governed Lifecycle Event).** Fine-tuning, continued pretraining,
adapter training (LoRA/QLoRA), distillation, quantization, and any process that produces a
derivative model SHALL be recorded as a governed Fine-Tuning Event. The event SHALL produce: a
new or extended Training Provenance Record; a new or extended AIBOM entry; a safety re-evaluation
(OQGF-P-18.4); a new weight signature (OQGF-P-18.5); and a responsible DAP. A derivative model
SHALL NOT silently inherit the base model's governance credentials without its own lifecycle
record. The base model's provenance is an input to the derivative's provenance, not a substitute
for it.

**OQGF-P-18.7 (Model Versioning and Lineage).** The relationship between base models, fine-tuned
variants, quantized versions, and deployed instances SHALL be versioned and traceable. Each
model version SHALL carry: a unique version identifier; its parent version (if a derivative); its
Training Provenance Record; its Alignment Record; its weight signature; and its deployment
status. Versioning SHALL be append-only consistent with OQGF-A; superseded versions are annotated
and retained, not deleted. Post-incident reconstruction SHALL be able to determine exactly which
model version was serving at a given time.

**OQGF-P-18.8 (Deployment Attestation).** Before a model enters service and periodically
thereafter, the deployed instance SHALL be attested against its governed specification: the
weights match the signed artifact (OQGF-P-18.5); the serving configuration matches the declared
deployment; inference-time guardrails (safety classifiers, output filters, tool-use gates) are
present and functioning; and the Capability Envelope (AMD-011) is correctly declared. A model
deployed without attestation, or whose attestation has expired beyond the declared interval,
SHALL NOT serve governed inference. This mirrors the AMD-011 environment attestation
(OQGF-P-12.3) and the AMD-014 post-contraction attestation (OQGF-P-15.8) — the same pattern
applied to the model itself.

**OQGF-P-18.9 (Base-Model License Compliance).** Where the base model carries license terms or
acceptable-use restrictions, compliance SHALL be documented in the lifecycle record and SHALL be
auditable. Material restrictions — prohibitions on specific use cases, naming requirements,
attribution obligations, geographic restrictions, derivative-work terms — SHALL be recorded as
governance obligations. A model deployed in violation of its base-model license is non-conforming
regardless of the quality of its other lifecycle governance.

**OQGF-P-18.10 (Model Retirement).** A governed model version SHALL have a retirement process:
conditions under which it is withdrawn from service (superseded, found unsafe, training data
compromised, alignment invalidated, license revoked), the responsible DAP, and the evidence
supporting retirement. Retirement SHALL be recorded in Organ 5. A retired model SHALL NOT be
re-deployed without a new governance lifecycle — retirement is not a pause.

---

## AMD.2 Conformance criteria per level

**Baseline (OQGF-B):** Training Provenance Record extending the AIBOM (OQGF-P-18.1); per-dataset
provenance for material datasets (OQGF-P-18.2); alignment process documented (OQGF-P-18.3);
weight integrity verified at model load (OQGF-P-18.5); fine-tuning recorded as a governed event
(OQGF-P-18.6); model versioning and lineage (OQGF-P-18.7); base-model license compliance
documented (OQGF-P-18.9); retirement process declared (OQGF-P-18.10). Single-PQC-family weight
signatures acceptable.

**Enhanced (OQGF-E):** All Baseline criteria, plus safety-capability tradeoff measured and
risk-registered for every material fine-tuning event (OQGF-P-18.4); deployment attestation
before service and at a declared interval (OQGF-P-18.8); contamination assessment for material
training datasets; reward-model provenance in alignment records; adversarial testing of weight-
integrity verification (substitute weights and confirm detection).

**High-Assurance (OQGF-H):** All Enhanced criteria, plus dual-PQC-family weight signatures
(ML-DSA + SLH-DSA per OQGF-M-2); continuous or near-real-time weight-integrity verification
during serving; independent verification of alignment records; second-DAP review of material
safety-capability tradeoff acceptances; adversarial testing of training-data poisoning,
fine-tuning-based safety degradation, weight substitution, and deployment-attestation bypass;
periodic replay of lifecycle evidence from Organ 5.

---

## AMD.3 Assessment procedures

An auditor SHALL:

1. Request a model's Training Provenance Record and confirm it extends the AIBOM with lifecycle
   provenance: datasets, configuration, infrastructure, DAP, and date (OQGF-P-18.1). **This is
   the load-bearing test of this amendment**: it proves the model's origin is governed, not
   just inventoried.
2. Select a material training dataset and confirm it carries per-dataset provenance: source,
   license, hash, preprocessing, and epistemic classification (OQGF-P-18.2). Confirm unknown
   provenance is recorded as unknown, not omitted.
3. Request the Alignment Record and confirm the alignment technique, reward model or preference
   data, and before/after safety benchmarks are documented (OQGF-P-18.3).
4. Identify a fine-tuning event and confirm safety benchmarks were measured before and after;
   confirm any material degradation is documented, risk-registered, and either remediated or
   accountably accepted (OQGF-P-18.4).
5. Corrupt or substitute the model weights and confirm the weight-integrity check detects the
   mismatch at model load time (OQGF-P-18.5).
6. Identify a fine-tuned derivative and confirm it has its own Training Provenance Record,
   AIBOM extension, safety re-evaluation, weight signature, and DAP — not just a pointer to
   the base model's credentials (OQGF-P-18.6).
7. Request the model lineage and confirm the chain from base model through fine-tuned variants
   to deployed instance is traceable (OQGF-P-18.7). Confirm post-incident reconstruction can
   identify which version was serving at a given time.
8. Confirm the deployed instance was attested before service: weights match, guardrails present,
   Capability Envelope declared (OQGF-P-18.8).
9. Request base-model license compliance documentation and confirm material restrictions are
   recorded (OQGF-P-18.9).
10. Retire a model version and confirm the retirement is recorded in Organ 5 and the model
    cannot be re-deployed without a new governance lifecycle (OQGF-P-18.10).

---

## AMD.4 Control mappings

- **NIST AI RMF:** MAP-1.1, MAP-2.3 (AI lifecycle, data governance, and provenance); MEASURE-2.3,
  MEASURE-2.6 (training-data quality, safety evaluation, and the conditions under which the
  model's properties hold); MANAGE-1.3, MANAGE-3.1 (model lifecycle management, deployment
  monitoring, and retirement); GOVERN-1.2, GOVERN-1.5 (accountability and documentation).
- **NIST SP 800-53 Rev. 5:** SA-10 (developer configuration management — training and alignment
  as governed configuration), SA-11 (developer testing — safety benchmarking), CM-2 and CM-3
  (baseline configuration and change control — model versioning), SI-7 (software/firmware/
  information integrity — weight-integrity attestation), AU-2/AU-3/AU-12 (audit content and
  generation — lifecycle evidence), RA-3 (risk assessment — safety-capability tradeoff).
- **EU AI Act:** Article 10 (data and data governance — training-data provenance, bias,
  contamination); Article 11 (technical documentation — lifecycle records); Article 15
  (accuracy, robustness, and cybersecurity — weight integrity); Annex IV (technical
  documentation requirements — AIBOM/Training Provenance Record alignment).
- **CycloneDX 1.7 ML-BOM (ECMA-424) / SPDX 3.0 AI Profile / OWASP AIBOM:** the emerging
  standard for machine-readable AI bill of materials. This amendment extends the inventory
  into lifecycle provenance.
- **ISO/IEC 42001:** Clause 6 (risk assessment), Clause 8 (operational controls for AI
  lifecycle), Clause 9 (monitoring and evaluation); **ISO/IEC 5338** (AI lifecycle processes).
- **CNSA 2.0:** ML-DSA-87 for weight signatures and lifecycle-record signing; dual-family at
  High-Assurance per OQGF-M-2. ML-KEM-1024 for protecting weights in transit (training
  pipeline to registry, registry to serving).

---

## AMD.5 Technical architecture (implementation hooks)

AMD-017 introduces no new organ. It extends `oqgf-core` with lifecycle types and persists
evidence in `oqgf-memory` (Organ 5). Weight-integrity verification uses the existing OQGF-G-3
signing infrastructure.

### AMD.5.1 Core types

```rust
/// The governed lifecycle record extending the AIBOM (OQGF-P-18.1).
/// From raw materials to served weights.
pub struct TrainingProvenanceRecord {
    pub model_ref: ModelVersionRef,
    pub aibom_ref: AibomRef,                   // extends, not replaces
    pub datasets: Vec<DatasetProvenance>,       // OQGF-P-18.2
    pub training_config: TrainingConfiguration,
    pub infrastructure: InfrastructureRef,
    pub alignment: AlignmentRecord,            // OQGF-P-18.3
    pub fine_tuning_events: Vec<FineTuningEvent>, // OQGF-P-18.6
    pub owner: DesignatedAccountableParty,
    pub created_at: SystemTime,
    pub signature: DualSignature,
}

/// Per-dataset provenance (OQGF-P-18.2). Unknown is a valid classification,
/// not a reason to omit the record.
pub struct DatasetProvenance {
    pub id: DatasetId,
    pub source: DataSource,
    pub collection_method: CollectionMethod,
    pub license: LicenseRef,
    pub hash: CryptoHash,                      // SHA-256 or SHA-3
    pub size: DatasetSize,
    pub date_range: DateRange,
    pub preprocessing: Vec<PreprocessingStep>,
    pub known_biases: Vec<BiasAssessment>,
    pub contamination: ContaminationAssessment, // benchmark leakage, PII, adversarial
    pub epistemic: DatasetEpistemicClass,       // Curated | Crawled | Synthetic | Augmented | Unknown
}

/// The alignment process as a governed lifecycle event (OQGF-P-18.3).
pub struct AlignmentRecord {
    pub technique: AlignmentTechnique,          // RLHF | DPO | Constitutional | InstructionTuning | Other
    pub reward_model: Option<RewardModelProvenance>,
    pub preference_data: Option<DatasetProvenance>,
    pub safety_before: SafetyBenchmarkResult,
    pub safety_after: SafetyBenchmarkResult,
    pub tradeoff: Option<SafetyCapabilityTradeoff>, // OQGF-P-18.4
    pub owner: DesignatedAccountableParty,
    pub version: AlignmentVersion,
}

/// The documented change in safety from domain specialization (OQGF-P-18.4).
/// Measured, recorded, and either remediated or accountably accepted.
pub struct SafetyCapabilityTradeoff {
    pub benchmarks: Vec<BenchmarkComparison>,   // before/after pairs
    pub magnitude: TradeoffMagnitude,
    pub risk_ref: RiskId,                       // AMD-008 Risk Register entry
    pub disposition: TradeoffDisposition,        // Remediated | Accepted(RiskAcceptance)
}

/// Cryptographic verification at serving time (OQGF-P-18.5).
/// The model in memory is the model that was governed.
pub struct WeightIntegrityAttestation {
    pub model_ref: ModelVersionRef,
    pub expected_hash: CryptoHash,
    pub observed_hash: CryptoHash,
    pub signature_verified: bool,
    pub attested_at: SystemTime,
    pub next_attestation: SystemTime,           // declared interval
}

/// Fine-tuning as a governed lifecycle event (OQGF-P-18.6).
/// Produces a new governed artifact, not a silent derivative.
pub struct FineTuningEvent {
    pub id: FineTuningEventId,
    pub base_model: ModelVersionRef,
    pub technique: FineTuningTechnique,         // FullFT | LoRA | QLoRA | DAP | Distillation | Quantization
    pub datasets: Vec<DatasetProvenance>,
    pub safety_reevaluation: SafetyCapabilityTradeoff,
    pub resulting_model: ModelVersionRef,
    pub weight_signature: DualSignature,        // new signature for the derivative
    pub owner: DesignatedAccountableParty,
    pub recorded_at: SystemTime,
}
```

The safety properties are structural. `DatasetEpistemicClass::Unknown` is a valid variant, not
a missing value — unknown provenance is recorded, not silently omitted. `WeightIntegrityAttestation`
carries both `expected_hash` and `observed_hash`, so a mismatch is a type-level observable fact.
`FineTuningEvent` carries its own `weight_signature` and `safety_reevaluation` — a derivative
cannot exist without its own governance record.

### AMD.5.2 What this closes, and what it does not

This amendment **closes** the following:

- **The ungoverned training origin.** A model's training provenance is now a governed lifecycle
  record, not just a component list (OQGF-P-18.1, OQGF-P-18.2).
- **The unauditable alignment.** The alignment process is documented with reward-model provenance
  and before/after safety benchmarks (OQGF-P-18.3).
- **The unmeasured safety degradation.** Domain fine-tuning that degrades safety alignment is
  measured, risk-registered, and governed (OQGF-P-18.4).
- **The sign-once-serve-forever gap.** Weights are verified at serving time, not only at signing
  time (OQGF-P-18.5).
- **The ungoverned derivative.** Fine-tuned variants have their own lifecycle records and cannot
  silently inherit the base model's credentials (OQGF-P-18.6).
- **The untraceable lineage.** Base-to-derivative-to-deployment is versioned and reconstructable
  (OQGF-P-18.7).
- **The unattested deployment.** The deployed instance is verified against its governed
  specification before serving (OQGF-P-18.8).
- **The ignored license.** Base-model restrictions are governance obligations (OQGF-P-18.9).
- **The undead model.** Retired models stay retired (OQGF-P-18.10).

This amendment **does not** fully close, and states so honestly:

- **Training-data completeness.** Provenance is required for material datasets. An organization
  that deliberately omits a dataset from the record has falsified the provenance — a governance
  failure the framework surfaces through audit but cannot structurally prevent. Same shape as
  AMD-011's capability-envelope completeness.
- **Alignment quality.** A documented alignment process can still be a bad one. Safety benchmarks
  can be chosen to flatter the model. The framework requires the documentation; it cannot
  guarantee the quality of the underlying work. Same shape as AMD-016's claim-accuracy residual.
- **Weight integrity during inference.** Verification at model load time catches substitution.
  It does not catch in-memory corruption during inference (bit flips, side-channel attacks,
  adversarial runtime modification). Same shape as AMD-014's hardware-channel residual.
- **Upstream base-model governance.** When the base model is an open-weight release from a third
  party (Meta, Mistral, etc.), Odin's controls its own fine-tuning lifecycle but not the base
  model's training governance. The base model's provenance is recorded as received; the framework
  cannot retroactively govern Meta's training decisions. This is honest: the derivative is
  governed from the point it enters Odin's lifecycle.
- **Human governance.** Someone must decide which datasets are material, which safety benchmarks
  are appropriate, when a tradeoff is acceptable, and when a model should be retired.
  Determinism enforces the governance path; it does not replace judgment.

---

## AMD.6 Traceability

| Requirement | Implementation hook | Existing OQGF dependency |
| --- | --- | --- |
| OQGF-P-18.1 | `oqgf-core::TrainingProvenanceRecord` extending `Aibom` | G-2 AIBOM |
| OQGF-P-18.2 | `DatasetProvenance` with hash, license, epistemic classification | I-11 ingress provenance |
| OQGF-P-18.3 | `AlignmentRecord` with technique, reward model, benchmarks | A-1 decision record |
| OQGF-P-18.4 | `SafetyCapabilityTradeoff` → P-10 Risk Register | P-10, P-9 |
| OQGF-P-18.5 | `WeightIntegrityAttestation` at load time; PQC-signed | G-3 artifact signing, M-2, CNSA 2.0 |
| OQGF-P-18.6 | `FineTuningEvent` with own provenance and safety re-eval | G-2, P-18.1–P-18.5 |
| OQGF-P-18.7 | `ModelVersionRef` parent-child lineage; append-only | A append-only, P-10.6 |
| OQGF-P-18.8 | deployment attestation mirroring P-12.3 and P-15.8 | P-12.3, P-15.8 |
| OQGF-P-18.9 | `LicenseRef` as governance obligation in lifecycle record | G-2 license field |
| OQGF-P-18.10 | retirement event in Organ 5; re-deployment blocked | A-1, P-10 |

---

## AMD.7 Change log

v1.0 — Initial public draft, 21 August 2026. Adds OQGF-P-18 (Model Lifecycle Assurance) to the
Physiology Layer: governs the full lifecycle of the model artifact from training data through
alignment through fine-tuning through deployment attestation. Extends the OQGF-G-2 AIBOM from a
component inventory to a lifecycle provenance record with per-dataset provenance, alignment
governance, and fine-tuning as governed events. Requires safety-capability tradeoff measurement
and risk-register entry when domain specialization degrades safety alignment. Requires
PQC-signed weight-integrity attestation at serving time, not only at signing time. Requires
fine-tuned derivatives to have their own governance lifecycle rather than silently inheriting
the base model's credentials. Requires model versioning and lineage, deployment attestation,
base-model license compliance as a governance obligation, and governed model retirement.

Responds to documented research findings that cybersecurity domain fine-tuning measurably degrades
safety alignment (CyberLLMInstruct), that weight substitution between signing and serving is a
realistic supply-chain attack, and that derivative models produced without their own governance
create ungoverned behavioral origins wearing governed credentials. Biological alignment grounded
in V(D)J recombination (training diversity), thymic selection (alignment quality control), and
peripheral tolerance (inference-time safety) — the immune system governs the developmental
lifecycle that produces its recognition capability, not just the capability once deployed.

Does not modify OQGF-G-2 (AIBOM inventory), OQGF-G-3 (artifact signing), or any prior
amendment; extends the lifecycle governance those requirements provide. Implementation-neutral:
any training framework, alignment technique, fine-tuning method, or serving infrastructure may
conform. Five residuals named — training-data completeness, alignment quality, in-memory
integrity, upstream base-model governance, and human judgment — each mapped to a prior
amendment's residual shape.

— End of OQGF Amendment 017.
