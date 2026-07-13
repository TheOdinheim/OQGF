# Odin's Quantum AI/ML Governance Framework (OQGF-1.0)

**Integrated Deliverable: Formal Specification, Thought-Leadership Whitepaper, and Technical Architecture**

*Author: Jeremy Rose, CEO — Odin's LLC, Wasilla, Alaska*
*Document Set ID: OQGF-INTEGRATED-2026-001*
*Date: 20 May 2026*
*Status: Public draft for NIST, sector regulators, and the Odin's engineering team*

---

# PART A — FORMAL NORMATIVE GOVERNANCE FRAMEWORK SPECIFICATION

## A.0 Front matter

### A.0.1 Title
**Odin's Quantum AI/ML Governance Framework**, OQGF-1.0.

### A.0.2 Document scope
This publication specifies a normative governance framework for organizations that build, deploy, or rely on artificial intelligence and machine learning systems in an environment where (a) cryptographically relevant quantum computers (CRQCs) are anticipated within the operational lifetime of those systems, and (b) AI systems are themselves subject to safety, fairness, accountability, and explainability obligations. OQGF-1.0 organizes requirements into five "organs," each modeled on a function of the human adaptive immune system. The document defines requirements, conformance levels, assessment procedures, and mappings to existing federal and international controls.

### A.0.3 Applicability statement
OQGF-1.0 applies to:
- Federal agencies and their contractors operating AI/ML systems on federal information systems or National Security Systems (NSS).
- Operators of any of the sixteen critical infrastructure sectors designated in NSM-22.
- Commercial entities that voluntarily adopt OQGF to demonstrate quantum-safe and AI-governance maturity.
- Vendors supplying AI/ML, cryptographic, or quantum computing components into the above environments.

OQGF-1.0 is voluntary in its civilian form and mandatory only where adopted by reference by a contracting authority, sector risk management agency (SRMA), or regulator.

### A.0.4 Normative references
The following documents are incorporated by reference. Where a reference is undated, the latest edition applies.
- **NIST FIPS 203** — Module-Lattice-Based Key-Encapsulation Mechanism Standard (ML-KEM).
- **NIST FIPS 204** — Module-Lattice-Based Digital Signature Standard (ML-DSA).
- **NIST FIPS 205** — Stateless Hash-Based Digital Signature Standard (SLH-DSA).
- **NIST SP 800-208** — Recommendation for Stateful Hash-Based Signature Schemes (LMS, XMSS).
- **NIST IR 8547 (Initial Public Draft, Nov 12 2024)** — Transition to Post-Quantum Cryptography Standards.
- **NIST AI RMF 1.0** (NIST AI 100-1, Jan 26 2023) and the Generative AI Profile NIST AI 600-1.
- **ISO/IEC 42001:2023** — Artificial intelligence management system.
- **CNSA 2.0** — NSA Commercial National Security Algorithm Suite 2.0 (CSA, May 30 2025 republication).
- **NIST SP 800-53 Rev. 5** — Security and Privacy Controls for Information Systems and Organizations.
- **NIST SP 800-171** Rev. 3 — Protecting CUI in Nonfederal Systems.
- **NIST SP 1800-38 A/B/C** — Migration to Post-Quantum Cryptography (NCCoE preliminary drafts).
- **NIST SP 800-90A/B/C** — Random bit generation, entropy sources, and RBG construction.
- **NIST SP 800-218** — Secure Software Development Framework (SSDF).
- **NIST FIPS 199 / FIPS 200** — Security categorization and minimum requirements.
- **DoW CIO memorandum "Preparing for Migration to Post Quantum Cryptography,"** signed 18 Nov 2025 (cleared 20 Nov 2025).
- **NSM-22** (Apr 30 2024) — National Security Memorandum on Critical Infrastructure Security and Resilience.

### A.0.5 Terminology
- **AIBOM (AI Bill of Materials)** — a machine-readable inventory of an AI/ML system's models, training and evaluation datasets, prompts, fine-tuning artifacts, frameworks, weights provenance, and licensing.
- **CBOM (Cryptographic Bill of Materials)** — a machine-readable inventory of every cryptographic primitive, parameter set, key, certificate, library, and protocol used by a system, including the algorithm identifier, library version, FIPS validation reference, and the location of each use.
- **CRQC (Cryptographically Relevant Quantum Computer)** — a quantum computer of sufficient logical-qubit count and fidelity to break currently deployed public-key cryptography (RSA, ECDH/ECDSA, DH) in a tactically meaningful time.
- **HNDL (Harvest Now, Decrypt Later)** — the adversary practice of recording quantum-vulnerable ciphertext today for decryption once a CRQC is available.
- **Organ** — a coherent set of governance functions in OQGF, modeled on a biological subsystem; each organ has a purpose, normative requirements, and assessment procedures.
- **Sentinel** — a software component that observes traffic, behavior, or telemetry at a defined boundary and emits structured signals to other organs.
- **Attestation** — a cryptographically signed claim about the identity, configuration, or measured state of a hardware or software component.
- **Statistical reproducibility** — for a quantum computation, the property that the sampled output distribution from a stated circuit on a stated device matches a declared noise model within a stated statistical test (e.g., Kolmogorov-Smirnov, χ²) at a stated confidence level.
- **Mosca's inequality (X + Y > Z)** — if data must remain confidential for X years, the migration to PQC takes Y years, and a CRQC is anticipated in Z years, then migration must already be in progress.
- **Re-signing** — replacing or augmenting an existing signature with a signature under a newer cryptographic generation, preserving the chain of provenance.
- **Designated Accountable Party (DAP)** — a named natural person bearing legal and reputational responsibility for a specific AI/ML system's outcomes.

### A.0.6 Conformance levels
OQGF-1.0 defines three levels, aligned to FIPS 199 impact:
- **Baseline (OQGF-B)** — Low impact systems; minimum quantum-safe hygiene and AI accountability.
- **Enhanced (OQGF-E)** — Moderate impact; full five-organ coverage with continuous monitoring.
- **High-Assurance (OQGF-H)** — High impact and NSS-adjacent; CNSA 2.0 algorithms, dual-PQC-family signing, multi-jurisdictional replication, third-party continuous attestation.

A system shall not claim a conformance level higher than the lowest-level organ it implements.

### A.0.7 Normative verb conventions
SHALL / SHALL NOT denote absolute requirements. SHOULD / SHOULD NOT denote strong recommendations whose deviation requires documented justification. MAY denotes permitted choices.

---

## A.1 Organ 1 — OQGF-G (Genetic Layer / Compliance as Code)

### A.1.1 Purpose
The Genetic Layer encodes the system's identity at birth: what it is made of, how it was built, what cryptography protects it, and which policies govern it. Like DNA, this information must travel with every cell of the system and must be verifiable at any point in the lifecycle.

### A.1.2 Architectural rationale
In biology, every cell carries the same genome; compliance, likewise, must be intrinsic to every artifact rather than bolted on at deployment. By compiling cryptographic and AI bills of material at first commit and binding them to signed artifacts, OQGF-G ensures that quantum-vulnerable code cannot enter production without raising a visible alarm, and that any AI system can be reconstructed and audited from its declared genome.

### A.1.3 Normative requirements
- **OQGF-G-1** The organization SHALL maintain a current CBOM for every system in scope, conformant to CycloneDX 1.6 or later (or SPDX equivalent), listing every cryptographic primitive, library, parameter set, certificate, key reference, and protocol with its FIPS validation reference where applicable.
- **OQGF-G-2** The organization SHALL maintain a current AIBOM for every AI/ML system in scope, listing models, weights provenance, training data sources, evaluation datasets, fine-tuning corpora, prompts, system messages, frameworks, and licenses.
- **OQGF-G-3** Every release artifact (binary, container image, model weights file, or signed manifest) SHALL be cryptographically signed using a signature algorithm approved at the system's conformance level (see A.1.4) and SHALL embed or reference its CBOM and AIBOM digests.
- **OQGF-G-4** The build pipeline SHALL enforce, as a non-bypassable gate, that no artifact may be promoted to a regulated environment unless its CBOM and AIBOM are present, signed, and free of disallowed algorithms.
- **OQGF-G-5** Cryptographic agility SHALL be designed in from first commit: no algorithm identifier may be hard-coded; all algorithms SHALL be selected through a negotiation layer that supports at minimum one classical and one PQC alternative per primitive class.
- **OQGF-G-6** All cryptographic modules in scope SHALL be FIPS 140-3 validated by 21 September 2026; FIPS 140-2 modules SHALL NOT be included in new procurements after that date.
- **OQGF-G-7** Key lifetime SHALL be set to satisfy Mosca's inequality: for confidentiality keys protecting data that must remain secret for X years, with anticipated migration duration Y, the key SHALL be replaced with a PQC-protected key not later than (Z − X − Y) years before the anticipated CRQC date Z, with Z defaulting to 2030 unless a documented sector-specific value applies.
- **OQGF-G-8** Policy SHALL be expressed as code, version-controlled, signed, and evaluated automatically against every build; policy changes SHALL require dual review.
- **OQGF-G-9** The CBOM and AIBOM SHALL be regenerated and re-signed on every release and SHALL be retained for the retention period mandated by the applicable sector overlay (default seven years).

### A.1.4 Conformance criteria per level
- **Baseline:** CBOM and AIBOM present, signed with ML-DSA-65 or SLH-DSA-128s; CI gate present for disallowed algorithms; FIPS 140-3 modules by 21 Sep 2026.
- **Enhanced:** All of the above plus full cryptographic agility layer; key lifetime calculation documented per primitive; policy-as-code under signed control.
- **High-Assurance:** All of the above plus CNSA 2.0 algorithms (ML-KEM-1024, ML-DSA-87, LMS/XMSS for code signing, AES-256, SHA-384/512); HSM-backed signing keys; dual-control key issuance; build pipeline itself signed and attested.

### A.1.5 Assessment procedures
An auditor SHALL: (1) request the CBOM and AIBOM for a randomly selected release; (2) verify each signature using only the public roots of trust declared by the organization; (3) attempt to push a build containing a banned algorithm and confirm the CI gate rejects it; (4) inspect HSM logs for key issuance events; (5) replay the Mosca calculation for at least one long-lived confidentiality key.

### A.1.6 Control mappings
- **NIST AI RMF:** GOVERN-1.1, GOVERN-4.2, MAP-4.1.
- **NIST SP 800-53 Rev. 5:** CM-2, CM-8, SR-3, SR-4, SR-11, SI-7, SA-8, SA-10, SA-11, SA-15.
- **ISO/IEC 42001 Annex A:** A.6 (resources for AI systems), A.7 (data for AI systems), A.10 (third-party and customer relationships).
- **CNSA 2.0:** ML-KEM-1024, ML-DSA-87, LMS/XMSS per SP 800-208.

---

## A.2 Organ 2 — OQGF-I (Inflammation Organ / Assumed Breach)

### A.2.1 Purpose
The Inflammation Organ assumes the adversary is already inside. It deploys sentinels that watch for harvest-now-decrypt-later activity, classical-TLS exposure, and abnormal access to AI/quantum infrastructure, and it mounts a graded response.

### A.2.2 Architectural rationale
Inflammation is the body's first-response signal: heat, redness, and swelling that recruit defenders and localize damage. OQGF-I does the analogous work for cryptographic and AI infrastructure, raising risk scores, rotating keys, and isolating compromised paths before the harvested ciphertext can be exploited.

### A.2.3 Normative requirements
- **OQGF-I-1** A sentinel network SHALL be deployed at every network boundary that carries data classified above Public, capable of identifying classical key exchange (RSA, ECDH without ML-KEM hybrid) and emitting an HNDL risk event.
- **OQGF-I-2** After 31 December 2030, classical-only TLS for data above Public SHALL be treated as a reportable incident; before that date, it SHALL be treated as a graded risk event according to the HNDL risk score in A.2.5.
- **OQGF-I-3** The organization SHALL maintain a documented trust model for every quantum cloud provider in use (IBM Quantum, AWS Braket, Azure Quantum, IonQ Cloud, Quantinuum, others) including data-handling, multi-tenant isolation, attestation availability, and jurisdictional considerations.
- **OQGF-I-4** Authentication to AI training pipelines, model registries, and quantum cloud endpoints SHALL be layered: at minimum a PQC-signed device attestation (see Organ 3) plus a short-lived user credential plus a workload identity, with all three required for any privileged action.
- **OQGF-I-5** The HNDL risk score SHALL be computed per session and per asset using at least: the cryptographic strength of the channel, the confidentiality lifetime of the data, the exposure surface, and threat-intelligence signals; the score and its inputs SHALL be retained.
- **OQGF-I-6** A graded response engine SHALL be in place: low risk triggers logging; medium risk triggers rate limiting and alerting; high risk triggers automated key rotation, session termination, and incident response handoff.
- **OQGF-I-7** Resolution and de-escalation SHALL be governed by signed policy; an inflammatory response SHALL NOT be terminated without a recorded resolution event including who, what, when, and why.

### A.2.4 Conformance criteria per level
- **Baseline:** Sentinels at the perimeter; HNDL risk scoring on inbound TLS; weekly review of high-score events.
- **Enhanced:** Sentinels at all internal trust boundaries; layered authentication enforced; automated graded response.
- **High-Assurance:** Continuous monitoring of every quantum cloud session; real-time threat-intel fusion; CNSA 2.0 channel preference enforced; classical-TLS treated as incident immediately for NSS data.

### A.2.5 Assessment procedures
An auditor SHALL: (1) attempt a classical-only TLS connection to a sentinel-protected endpoint and verify the risk event; (2) trigger a synthetic HNDL pattern and verify the graded response; (3) inspect quantum cloud session logs for layered authentication evidence; (4) confirm that resolution events include named approvers.

### A.2.6 Control mappings
- **NIST AI RMF:** MEASURE-2.6, MEASURE-2.7, MANAGE-2.1, MANAGE-4.1.
- **NIST SP 800-53 Rev. 5:** AC-2, AC-3, AC-17, AU-6, AU-12, IR-4, IR-5, IR-6, SC-7, SC-8, SC-12, SI-4.
- **ISO/IEC 42001 Annex A:** A.8 (information for interested parties), A.9 (use of AI systems).
- **CNSA 2.0:** mandated key establishment via ML-KEM-1024 for NSS sessions.

---

## A.3 Organ 3 — OQGF-M (MHC Layer / Zero Trust)

### A.3.1 Purpose
The MHC Layer is the framework's identity organ. As major histocompatibility complex molecules display fragments of every protein a cell makes so the immune system can verify "self," OQGF-M continuously displays the identity and measured state of every device, workload, model, and quantum job for cryptographic verification.

### A.3.2 Architectural rationale
Static credentials and perimeter trust collapse under quantum and AI threats. The MHC analog requires that every actor present, on demand, a fresh, PQC-signed claim about what it is, what state it is in, and what it intends to do. For quantum workloads the claim extends to the circuit, the calibration data, and the empirical output distribution.

### A.3.3 Normative requirements
- **OQGF-M-1** Every device and workload acting on data above Public SHALL present a PQC-signed attestation rooted in a hardware root of trust (TPM 2.0, AMD SEV-SNP, Intel TDX/SGX, or NVIDIA H100 CC) before being granted any privilege.
- **OQGF-M-2** Attestations SHALL be dual-signed under two PQC families (lattice and either hash or code) for High-Assurance systems.
- **OQGF-M-3** Quantum hardware attestation SHALL include three reconciled elements: the executed circuit, the device calibration data at execution time, and the empirical sampling distribution; these SHALL be statistically tested against the declared noise model.
- **OQGF-M-4** Credentials SHALL be short-lived: workload credentials SHALL expire within 24 hours, user privileged sessions within 8 hours, and quantum-job tokens within 1 hour.
- **OQGF-M-5** Mutual authentication SHALL be required for every connection; one-sided TLS SHALL NOT satisfy this requirement.
- **OQGF-M-6** A vendor trust score SHALL be computed per supplier based on declared attestation capability, FIPS validation, breach history, jurisdictional exposure, and statistical reconciliation pass rate; the score SHALL be reviewed quarterly.
- **OQGF-M-7** Continuous attestation SHALL be performed at intervals not exceeding the credential lifetime divided by four.

### A.3.4 Conformance criteria per level
- **Baseline:** TPM 2.0 attestation; classical or PQC-signed; short-lived credentials.
- **Enhanced:** PQC-signed attestations; statistical reconciliation on at least one quantum provider; documented vendor trust scores.
- **High-Assurance:** Dual-family signed attestations; statistical reconciliation on every quantum job; vendor trust score gating procurement.

### A.3.5 Assessment procedures
An auditor SHALL: (1) request a fresh attestation from a randomly selected workload and verify the PQC signature chain; (2) request a sample of quantum job records and verify the Kolmogorov-Smirnov or χ² reconciliation result; (3) inspect vendor trust score history.

### A.3.6 Control mappings
- **NIST AI RMF:** GOVERN-1.4, MAP-3.2, MEASURE-2.5.
- **NIST SP 800-53 Rev. 5:** IA-2, IA-3, IA-5, IA-8, IA-9, AC-3, AC-6, SC-12, SC-23.
- **ISO/IEC 42001 Annex A:** A.5, A.6, A.10.
- **CNSA 2.0:** ML-DSA-87 device certificates; LMS/XMSS for firmware identity.

---

## A.4 Organ 4 — OQGF-R (Redundant Defense Organ / No SPOF)

### A.4.1 Purpose
Eliminate single points of cryptographic, computational, or jurisdictional failure. If one PQC family is broken, one cloud is compromised, or one entropy source is malicious, the organism survives.

### A.4.2 Architectural rationale
The immune system carries multiple, independently evolved defenses (innate, adaptive humoral, adaptive cellular). One can fail without organism death. OQGF-R imposes the same diversity on cryptographic families, infrastructure providers, entropy, and audit storage.

### A.4.3 Normative requirements
- **OQGF-R-1** High-Assurance systems SHALL employ at least two PQC signature families (one lattice — ML-DSA — and one hash-based — SLH-DSA — with code-based HQC added once standardized) in parallel for any signature relied on for legal evidence.
- **OQGF-R-2** Production deployments SHALL be capable of multi-cloud operation; vendor lock-in to a single cryptographic, quantum, or compute provider SHALL be documented as a risk requiring DAP acceptance.
- **OQGF-R-3** Where operationally permitted, a classical fallback (RSA-3072 or ECDSA P-384) SHALL be available in hybrid mode through 31 December 2030, after which classical fallback SHALL be removed except where explicit waiver applies.
- **OQGF-R-4** Entropy sources SHALL be diversified across at least two physically independent mechanisms, validated under NIST SP 800-90B with continuous Repetition Count and Adaptive Proportion tests. **Per the DoW CIO memorandum of 18 Nov 2025, non-local quantum randomness generation and non-FIPS RNGs SHALL NOT be used as the sole source of entropy for confidentiality, authenticity, or key establishment in any DoD/DoW-connected system; FIPS-validated local QRNGs MAY contribute as one of two or more sources.**
- **OQGF-R-5** Audit trails SHALL be replicated across at least two legal jurisdictions for High-Assurance systems, using CRDT- or hash-linked-log replication to preserve append-only integrity under partition.
- **OQGF-R-6** Long-lived secrets (root signing keys, audit-signing keys) SHALL be sharded using Shamir's Secret Sharing or threshold cryptography with a quorum of at least 3-of-5.
- **OQGF-R-7** The architecture SHALL include a placeholder integration point for future quantum-network key distribution, but SHALL NOT depend on it for current confidentiality.

### A.4.4 Conformance criteria per level
- **Baseline:** Single PQC family acceptable; one cloud; one entropy source plus DRBG.
- **Enhanced:** Dual PQC families for audit signatures; multi-cloud capable; two entropy sources.
- **High-Assurance:** Dual or triple PQC families for all evidentiary signatures; multi-cloud live; cross-jurisdictional audit replication; 3-of-5 threshold custody.

### A.4.5 Assessment procedures
An auditor SHALL: (1) verify a sample audit signature under each declared PQC family independently; (2) simulate the failure of one cloud provider and verify continuity; (3) inspect entropy health-test logs; (4) inspect Shamir share custody records and recovery rehearsal evidence.

### A.4.6 Control mappings
- **NIST AI RMF:** MANAGE-1.3, MANAGE-4.3.
- **NIST SP 800-53 Rev. 5:** CP-2, CP-6, CP-7, CP-9, SC-12, SC-13, SC-28, SI-13, SR-3.
- **ISO/IEC 42001 Annex A:** A.6, A.9.
- **CNSA 2.0:** ML-KEM-1024, ML-DSA-87, LMS/XMSS; AES-256; SHA-384/512.

---

## A.5 Organ 5 — OQGF-A (Memory Organ / 360-Degree Accountability)

### A.5.1 Purpose
Record everything that matters, in a form that will still be verifiable when today's cryptography is broken and today's people are gone.

### A.5.2 Architectural rationale
Immunological memory makes second exposures survivable. OQGF-A makes regulatory and forensic re-examination possible decades after the fact, including for quantum computations whose outputs are inherently probabilistic.

### A.5.3 Normative requirements
- **OQGF-A-1** For every regulated AI/ML decision the system SHALL record: the model identifier and version, the AIBOM digest, the input (or a privacy-preserving derivative thereof), the output, the explanation artifact, the timestamp, and the DAP.
- **OQGF-A-2** For every quantum computation the system SHALL record the circuit, the device identifier, the calibration snapshot, and the **full empirical sampling distribution** — not a summary statistic — together with the declared noise model and the reconciliation test result.
- **OQGF-A-3** Audit records SHALL be signed under at least two PQC families and timestamped via an RFC 3161-compliant authority that itself supports PQC signing.
- **OQGF-A-4** Quantum-appropriate explanation artifacts SHALL accompany decisions made by variational or kernel quantum models: e.g., dominant Pauli-string contributions for VQC outputs, kernel attribution for QSVM outputs, or measurement-statistic attribution where applicable.
- **OQGF-A-5** Every regulated AI/ML system SHALL have a named DAP recorded in the audit record; the DAP SHALL be a natural person, not an entity.
- **OQGF-A-6** Audit signatures SHALL be re-signed under the prevailing cryptographic generation at intervals not exceeding five years, preserving the original signatures and chain.
- **OQGF-A-7** A regulatory query interface SHALL be available within 72 hours of a lawful request, exposing the full audit chain in a read-only, signed export.

### A.5.4 Conformance criteria per level
- **Baseline:** Decision logging with classical or single-PQC signatures; manual export available.
- **Enhanced:** Dual-PQC signatures; quantum sampling distributions retained; explanation artifacts present.
- **High-Assurance:** All of the above plus periodic re-signing on an automated schedule; cross-jurisdictional replication; live regulator portal.

### A.5.5 Assessment procedures
An auditor SHALL: (1) select a regulated decision at random and request the full chain; (2) verify both PQC signatures; (3) re-run the statistical reconciliation on a sampled quantum record; (4) confirm DAP identity and acknowledgment; (5) inspect the re-signing log.

### A.5.6 Control mappings
- **NIST AI RMF:** MEASURE-2.8, MEASURE-2.9, MEASURE-2.10, MANAGE-2.2, MANAGE-3.1.
- **NIST SP 800-53 Rev. 5:** AU-2, AU-3, AU-9, AU-10, AU-11, AU-12, SI-12.
- **ISO/IEC 42001 Annex A:** A.8, A.9.
- **CNSA 2.0:** LMS/XMSS for long-term archival signing; ML-DSA-87 for operational signing.

---

## A.6 Cross-organ requirements

### A.6.1 Incident response
The organization SHALL maintain a quantum-and-AI-aware incident response plan that defines triggers (HNDL detection, attestation failure, statistical reconciliation failure, audit-chain break), roles, timelines, and cross-organ choreography. Tabletop exercises SHALL be conducted at least annually.

### A.6.2 Supply chain
SBOM, CBOM, and AIBOM SHALL be ingested for every third-party component. Vendors SHALL provide attestations of FIPS 140-3 validation status, PQC roadmap, and AI training data provenance. The supply-chain trust score (Organ 3) SHALL be re-evaluated upon every dependency update.

### A.6.3 Human oversight
Every High-Assurance AI/ML decision SHALL have a documented human-review pathway. The DAP SHALL be empowered to halt deployment.

### A.6.4 Third-party assessor accreditation
Third-party assessors performing OQGF conformance assessments SHALL hold credentials acceptable under the relevant federal or sector regime (e.g., FedRAMP 3PAO, CMMC C3PAO, ISO/IEC 17021-1 accreditation for ISO 42001) and SHALL complete OQGF-specific training maintained by the OQGF consortium.

---

## A.7 Conformance assessment methodology
- **Self-assessment** is permitted at Baseline. Results SHALL be signed by a corporate officer.
- **Third-party attestation** is required at Enhanced and High-Assurance, conducted at least every 24 months.
- **Continuous monitoring** is required at High-Assurance: machine-readable telemetry from each organ SHALL be exported to the assessor's read-only portal with no fewer than weekly attestation packages.

---

## A.8 Sector overlays (16 NSM-22 sectors)

| Sector | Key OQGF adjustment |
|---|---|
| Chemical | Organ 4 entropy: process-control isolation; Organ 5 retention 10 years. |
| Commercial Facilities | Baseline acceptable; Organ 2 sentinels at IoT boundaries. |
| Communications | High-Assurance default; CNSA 2.0 mandatory on backbone; P25 crossover guidance. |
| Critical Manufacturing | Organ 1 firmware-signing via LMS/XMSS; Organ 3 attestation for OT devices. |
| Dams | Organ 2 sentinels on SCADA; Organ 5 retention aligned with NRC/FERC. |
| Defense Industrial Base | DoW CIO memo controls dominant; Organ 4 QRNG prohibition strictly enforced. |
| Emergency Services | Organ 2 sentinels at LMR/P25 boundaries; low-latency response. |
| Energy | Organ 3 attestation for inverters and grid edge; Organ 5 cross-ISO replication. |
| Financial Services | Organ 5 dual-family signatures mandatory; cross-jurisdictional replication aligned with FFIEC. |
| Food and Agriculture | Baseline acceptable; AIBOM emphasis on supply tracing. |
| Government Facilities | FedRAMP-aligned; FIPS 140-3 absolute. |
| Healthcare and Public Health | Organ 5 explanation artifacts mandatory; HIPAA-aligned retention. |
| Information Technology | Full five-organ; reference implementer status preferred. |
| Nuclear Reactors, Materials, Waste | High-Assurance default; Organ 5 retention 50 years; Organ 4 triple-family. |
| Transportation Systems | Organ 3 attestation for vehicle-edge AI; FAA NAS overlay separately. |
| Water and Wastewater | Baseline acceptable; Organ 2 sentinels on PLC networks. |

Sector SRMAs MAY publish more restrictive overlays.

---

## A.9 Appendices

### A.9.1 Sample CBOM schema (CycloneDX 1.6 extract)
```json
{
  "bomFormat": "CycloneDX",
  "specVersion": "1.6",
  "components": [{
    "type": "cryptographic-asset",
    "name": "ML-KEM-1024",
    "bom-ref": "pkg:crypto/ml-kem-1024@2024",
    "cryptoProperties": {
      "assetType": "algorithm",
      "algorithmProperties": {
        "primitive": "kem",
        "parameterSetIdentifier": "ML-KEM-1024",
        "nistQuantumSecurityLevel": 5,
        "executionEnvironment": "software-encrypted-ram",
        "implementationPlatform": "x86_64",
        "certificationLevel": "FIPS140-3-L1",
        "mode": "encapsulation"
      }
    }
  }]
}
```

### A.9.2 Sample AIBOM schema (CycloneDX ML-BOM extract)
```json
{
  "bomFormat": "CycloneDX",
  "specVersion": "1.6",
  "components": [{
    "type": "machine-learning-model",
    "name": "odins-anomaly-classifier",
    "version": "1.4.2",
    "modelCard": {
      "modelParameters": {
        "task": "binary-classification",
        "architectureFamily": "transformer",
        "modelArchitecture": "distilbert-base"
      },
      "datasets": [{ "ref": "dataset:odin-hndl-2026-q1" }],
      "considerations": {
        "ethicalConsiderations": ["bias-tested-against-sectors"],
        "fairnessAssessments": [{"groupAtRisk":"sector-energy","balancedAccuracyDelta":0.018}]
      }
    },
    "properties": [
      {"name":"odin:dap","value":"jrose@odinsllc.io"},
      {"name":"odin:retentionYears","value":"7"}
    ]
  }]
}
```

### A.9.3 Assessment checklist (extract, per organ)
Each organ ships with a YAML checklist whose items map 1:1 to A.1–A.5 normative requirements; pass/fail/n.a. with evidence pointer.

### A.9.4 Change log
v1.0 — Initial public draft, 20 May 2026.

---

# PART B — THOUGHT-LEADERSHIP WHITEPAPER

## B.1 Executive summary

The world is bolting AI governance to quantum-safe cryptography after the fact, and the seams will fail. Three deadlines make this concrete: **CNSA 2.0 procurement gate on 1 January 2027**; **FIPS 140-2 sunset on 21 September 2026**; and **EU AI Act high-risk obligations on 2 August 2026**. Each deadline lands inside the next eighteen months; none of them speak to each other; and the agencies and vendors trying to comply are duplicating effort, missing overlaps, and creating new attack surface at the joints.

Odin's LLC proposes a different organizing principle. The human immune system already solves, in biology, the governance problems we are struggling to solve in software: identity verification at every cell boundary, layered redundancy, graded response to novel threats, durable memory across decades, and accountability rooted in the organism rather than the pathogen. We have re-expressed that biology as a five-organ governance framework — **OQGF-1.0** — covering Genetic (compliance as code), Inflammation (assumed breach and HNDL sentinels), MHC (zero-trust attestation), Redundant Defense (no single point of cryptographic or jurisdictional failure), and Memory (forensic accountability across cryptographic generations). The framework is fully mapped to NIST AI RMF, NIST SP 800-53 Rev. 5, ISO/IEC 42001, CNSA 2.0, and the November 2025 DoW CIO PQC directive.

The call to action is immediate. Organizations that begin Genetic-layer work (CBOM/AIBOM, cryptographic agility, FIPS 140-3 migration) by Q3 2026 will clear the September 2026 and January 2027 gates. Organizations that wait will not.

## B.2 The convergence: why quantum and AI governance must be solved together

Federal AI policy assumes the cryptography underneath it is sound. CNSA 2.0 and NIST PQC standards assume the workloads above them are unsurprising. They are both wrong. AI training pipelines now consume more network ciphertext than any other federal workload class; model weights are the most valuable static intellectual property most organizations possess; and quantum cloud providers are routing real circuits over classical TLS today. **The harvest-now-decrypt-later adversary does not care whether a packet is from a database backup or a foundation-model training run; they care whether it is encrypted with RSA-2048.** And the AI-risk adversary does not care whether your model is fair if its weights have been silently substituted by a supply-chain compromise the AI framework was never designed to detect.

Bolting AI and quantum governance together after the fact yields three failure modes. **First, double-counting:** the same control is implemented twice with subtly different evidence, doubling cost and halving auditability. **Second, gap-zones:** the boundary between an AI governance regime ending at the model card and a cryptographic regime beginning at the TLS handshake is a wide unguarded plain where attestation, audit, and key custody all evaporate. **Third, control collisions:** AI explainability requirements demand that decision inputs be retained, while quantum-safe data-minimization requirements want them shredded; without an organizing framework these collide at audit time.

Convergence must be designed in from the genome.

## B.3 The immune system insight

The immune system is the only proven, scalable, multi-decade governance architecture humans know of. It defends a body of trillions of cells against pathogens it has never seen, while maintaining tolerance for self and durable memory of past exposures. It runs without a central CPU, without an external regulator, and with graceful degradation across thousands of failure modes.

Current AI and cybersecurity frameworks lean on metaphors borrowed from castles (perimeters), factories (pipelines), or libraries (catalogs). None of those metaphors survive contact with an adversary that arrives inside the boundary, mutates faster than the defender, and persists across generations. The immune metaphor does, because biology had to solve exactly that problem.

OQGF takes five immune functions seriously. The genome encodes identity at birth. Inflammation localizes and signals damage. MHC display gives every cell a verifiable, current claim of "self." Redundant defense ensures no single failure is fatal. Memory makes second exposures survivable. Every one of those functions has a direct, testable analog in quantum AI/ML governance, and the five-organ structure of OQGF is the result.

We do not claim the metaphor is perfect. The immune system causes autoimmunity, allergy, and occasional catastrophic failures. We treat those failure modes as honestly as we treat its strengths.

## B.4 The five organs in narrative form

**Organ 1 — Genetic Layer.** In biology, every cell carries the same DNA, verifiable end-to-end. In OQGF, every artifact carries its CBOM and AIBOM, signed at first commit, enforced at the build gate, and traceable through deployment. Failure looks like a quantum-vulnerable library shipped in a model-serving container that nobody noticed because the SBOM was a PDF.

**Organ 2 — Inflammation Organ.** Inflammation is the body's way of saying *something is wrong here, send help.* OQGF's sentinels watch for HNDL patterns, classical-TLS exposure on regulated data, and abnormal access to AI/quantum infrastructure, and they trigger graded responses up to and including automated key rotation. Failure looks like a quantum cloud session that ran for six months over classical TLS while quietly exfiltrating circuits.

**Organ 3 — MHC Layer.** MHC molecules are the body's way of letting every cell prove what it is, on demand, to any T cell that asks. OQGF demands the same of every device, workload, model, and quantum job: a fresh, PQC-signed attestation, and for quantum jobs a three-way reconciliation of circuit, calibration, and sampling distribution. Failure looks like a substituted GPU returning plausible but subtly malicious gradients to a federated learning aggregator.

**Organ 4 — Redundant Defense Organ.** Innate and adaptive immunity overlap on purpose. OQGF requires that no single cryptographic family, cloud, jurisdiction, or entropy source can bring down the organism. The November 2025 DoW CIO directive prohibiting non-local QRNG and non-FIPS RNG as confidentiality entropy is folded into Organ 4 directly. Failure looks like a single lattice break taking down every audit signature simultaneously.

**Organ 5 — Memory Organ.** Immunological memory persists for decades. OQGF retains every regulated decision, every quantum sampling distribution, dual-PQC-signed and periodically re-signed across cryptographic generations. Failure looks like a 2028 lawsuit asking for a 2026 decision whose signature is unverifiable because the algorithm has been deprecated and nobody re-signed.

## B.5 The whitespace: ten governance products that do not yet exist (ranked)

1. A CBOM-aware CI gate for AI/ML pipelines.
2. An HNDL risk-scoring sentinel for quantum cloud sessions.
3. A statistical-reconciliation broker that verifies sampling distributions across IBM, AWS, Azure, IonQ, and Quantinuum on demand.
4. A dual-PQC-family audit-signing service with automated re-signing across cryptographic generations.
5. A vendor trust-scoring system tied to attestation pass-rate rather than questionnaires.
6. A FIPS-aware entropy aggregator that enforces the DoW CIO November 2025 prohibitions.
7. A regulator-facing query portal for OQGF-1.0 audit chains.
8. A federated-learning aggregator with PQC-signed gradient attestations.
9. A quantum-appropriate explanation generator (Pauli-string and kernel-attribution).
10. A reference OQGF conformance assessor toolkit for 3PAOs.

## B.6 The path forward

Adoption begins with a CBOM/AIBOM inventory and the Organ 1 CI gate; that alone closes the September 2026 FIPS 140-2 sunset risk. Inflammation sentinels follow, then MHC attestation, then Redundant Defense, then Memory. A consortium of federal agencies, sector SRMAs, cloud providers, quantum providers, and AI labs administers conformance, with third-party assessors trained against the OQGF reference checklists. Odin's commits to opening the assessor checklists, the CBOM/AIBOM schemas, and reference test vectors under a permissive license; the implementation crates ship dual-license (Apache-2.0 + MIT) with a proprietary High-Assurance package for FedRAMP-aligned deployment.

## B.7 Author note

Jeremy Rose is the founder and CEO of Odin's LLC, headquartered in Wasilla, Alaska, focused on AI security and quantum-safe governance for federal critical communications. Odin's prior work in P25 crossover security and federated learning attestation informs the OQGF reference architecture in Part C. This whitepaper is the public face of OQGF-1.0; the normative framework (Part A) and the technical architecture (Part C) are its operating documents.

---

# PART C — COMPREHENSIVE TECHNICAL ARCHITECTURE

## C.1 Architectural principles

### C.1.1 Rust-first rationale
Rust is the default implementation language for every OQGF crate. The reasons are concrete and not stylistic.

First, **memory safety matters most where cryptography lives.** Buffer overruns and use-after-frees in C cryptography libraries have produced the worst CVEs of the last twenty years. Rust eliminates whole classes of these at compile time, without garbage collection.

Second, **performance matters in sentinel hot paths.** Organ 2 sentinels must inspect TLS at line rate on edge hardware; tokio-based async Rust delivers that with predictable latency and no GC pauses.

Third, **embedded and edge support.** OQGF must run on P25 radios, GPU farms, and air-gapped enclaves. Rust's `no_std` subset and tier-2 SGX target (`x86_64-fortanix-unknown-sgx`) cover all three.

Fourth, **the type system enforces correctness.** Cryptographic agility is a type problem: an algorithm identifier is not a string. We use Rust's enums and traits to make "wrong algorithm" a compile error wherever possible.

Fifth, **zero-cost abstractions** let us write generic, auditable code without runtime penalty. Traits compile away.

### C.1.2 Python use cases
Python is used **only** for ML pipelines and quantum SDK integration. Qiskit, PennyLane, and Cirq are Python-native; rewriting them is not an option. MLflow, Kubeflow, Flower, FATE, and most data-science tooling assume Python. Where Python is necessary, we expose Rust functionality through **PyO3 0.28** bindings published as the `oqgf-python` package via `maturin`.

### C.1.3 PyO3 binding strategy
Each Rust crate that needs a Python face exports a thin `pyo3` module re-exporting its public types. We follow these rules: (1) all heavy lifting stays in Rust; Python is a thin orchestration layer; (2) the GIL is held only across cheap boundary calls; long-running operations release it via `Python::detach`; (3) every Python-visible function has a `.pyi` type stub for IDE support; (4) we ship wheels for cp311–cp314, including the free-threaded `t` variant.

### C.1.4 no_std subset for embedded
The crates `oqgf-core` (types and traits) and `oqgf-edge-sentinel` (Organ 2 edge runtime) are buildable `no_std + alloc`. They depend only on `serde` (with `derive`), `heapless`, `subtle`, and the RustCrypto pure-Rust PQC stack (`ml-kem`, `ml-dsa`, `slh-dsa`).

---

## C.2 System topology

The OQGF reference implementation has a **control plane**, a **data plane**, and three distinct execution surfaces.

The **control plane** is a small set of central services: the policy server (Rego via `regorus`), the vendor trust-scoring service, the regulator portal, and the re-signing scheduler. It runs in containers in a FedRAMP-aligned cloud, replicated across at least two regions and (for High-Assurance) at least two jurisdictions.

The **data plane** is the field: sentinels at network boundaries, attestation agents on every workload host, audit emitters in every regulated AI/ML decision path. Data-plane components are written to be small, fast, and offline-tolerant.

The **central audit substrate** is a PostgreSQL deployment with crypto-agile columns (each signature column carries both an algorithm OID and the signature bytes), CRDT-replicated across jurisdictions for High-Assurance.

The **cryptographic root of trust** is HSM-backed (PKCS#11 via `cryptoki`), with Shamir 3-of-5 sharding for the root signing keys.

The **quantum cloud integration broker** is a Rust service per provider (IBM, AWS Braket, Azure Quantum, IonQ, Quantinuum) speaking each provider's native API and emitting a normalized circuit-calibration-distribution attestation upstream.

The **federated learning aggregator** is a Rust service exposing both gRPC and HTTP APIs to Flower clients, with PQC-signed gradient attestation.

Edge sentinels are minimal Rust binaries; central services are containerized; air-gapped sites run the same binaries with manual policy and audit sync.

---

## C.3 Per-organ module architecture

The implementation lives in a single Cargo workspace with the following layout:

```
oqgf/
├── Cargo.toml                 # workspace
├── crates/
│   ├── oqgf-core/             # shared types, traits, no_std
│   ├── oqgf-crypto/           # crypto facade, algorithm negotiation
│   ├── oqgf-genetic/          # Organ 1
│   ├── oqgf-inflammation/     # Organ 2
│   ├── oqgf-mhc/              # Organ 3
│   ├── oqgf-redundant/        # Organ 4
│   ├── oqgf-memory/           # Organ 5
│   ├── oqgf-policy/           # regorus integration
│   ├── oqgf-attest/           # TPM, SEV-SNP, TDX, SGX, H100
│   ├── oqgf-quantum-broker/   # provider abstraction
│   ├── oqgf-fl/               # federated learning
│   ├── oqgf-edge-sentinel/    # no_std edge build
│   ├── oqgf-python/           # PyO3 bindings
│   └── oqgf-cli/              # operator CLI
└── deny.toml, .cargo/audit.toml, cyclonedx.toml
```

### C.3.1 Organ 1 — Genetic Layer (`oqgf-genetic`)

**Crate layout.** `oqgf-genetic` depends on `oqgf-core`, `oqgf-crypto`, `cyclonedx-bom` (for CBOM/AIBOM construction), `cargo-cyclonedx` (used as a build-time helper), `cryptoki` (HSM signing), and `regorus` (policy).

**Core types.**
```rust
/// A bill of materials (cryptographic or AI). Generic over the kind.
pub trait Bom: Sized + Send + Sync {
    type Kind: BomKind;
    fn digest(&self) -> Digest;
    fn to_cyclonedx(&self) -> serde_json::Value;
    fn sign(self, signer: &dyn Signer) -> Result<SignedBom<Self>, BomError>;
}

pub struct Cbom { /* CycloneDX 1.6 cryptographic-asset components */ }
pub struct Aibom { /* CycloneDX ML-BOM model + dataset components */ }
impl Bom for Cbom { type Kind = CryptographicAssets; /* ... */ }
impl Bom for Aibom { type Kind = MachineLearningArtifacts; /* ... */ }

/// Cryptographic-agility facade. Algorithm identifiers are typed.
pub enum SignatureAlg {
    MlDsa44, MlDsa65, MlDsa87,
    SlhDsaShake128s, SlhDsaShake192s, SlhDsaShake256s,
    LmsSha256N32H10, XmssSha256H10,
    EcdsaP256, EcdsaP384,                // classical fallback, deprecated 2030
}

pub trait Signer: Send + Sync {
    fn algorithm(&self) -> SignatureAlg;
    fn sign(&self, msg: &[u8]) -> Result<Signature, CryptoError>;
    fn fips_certificate(&self) -> Option<FipsCertRef>;
}

pub trait Verifier: Send + Sync {
    fn algorithm(&self) -> SignatureAlg;
    fn verify(&self, msg: &[u8], sig: &Signature) -> Result<(), CryptoError>;
}

pub struct CiGate { policy: PolicyBundle, signer: Arc<dyn Signer> }

impl CiGate {
    /// Block on a build promotion. Returns Ok only if CBOM, AIBOM, signatures,
    /// and policy all pass. This is the function CI calls.
    pub async fn evaluate(&self, artifact: &Artifact)
        -> Result<Promotion, CiGateError> { /* ... */ }
}
```

**Cryptographic primitive choices.** For ML-KEM and ML-DSA in FIPS-required paths we use **`aws-lc-rs` with the `fips` feature** (AWS-LC-FIPS v3.0 includes validated ML-KEM). For SLH-DSA we use **RustCrypto's `slh-dsa` crate**, since `liboqs-rust` does not yet expose FIPS 205 (only the legacy SPHINCS+). For LMS/XMSS firmware signing we use **`hbs-lms`** (RustCrypto). For classical fallback we use `aws-lc-rs`. The choice is dictated by FIPS validation, not preference: AWS-LC-FIPS v3.0 is the first 140-3 module in the world to include ML-KEM, and that fact lands us inside the September 2026 sunset.

**CI/CD plugins.** GitHub Actions, GitLab CI, and Jenkins integrations are thin shells that invoke the `oqgf-cli evaluate-build` subcommand and surface its exit status.

**Policy engine.** **`regorus` (Microsoft, pure-Rust, no_std-friendly, OPA v1 compliant)** is used for Rego evaluation. We chose `regorus` over CGO-wrapped OPA because we refuse to add a Go runtime to a Rust security boundary.

**HSM integration.** `cryptoki` against any PKCS#11 v3.0 HSM (CloudHSM, Entrust nShield, YubiHSM, Thales Luna). Sessions are pooled via `r2d2-cryptoki`. Root signing keys are non-exportable and Shamir-3-of-5 protected at the M-of-N HSM admin layer.

**Data schema.** CycloneDX 1.6 JSON for CBOM and AIBOM (see A.9.1, A.9.2). Internal storage uses `serde_json::Value` for forward compatibility with CycloneDX 1.7 (which adds richer ML-BOM).

**State.** `sled` is used for embedded build hosts; PostgreSQL 16 is the central store, with cryptographic columns typed as `(alg_oid TEXT, sig BYTEA)` pairs.

**Concurrency.** tokio 1.51 LTS, `mpsc` channels between the CI gate and the policy engine; actor pattern for the signing service.

**Error handling.** `thiserror` everywhere in the library; the binary wrappers use `anyhow`; no `unwrap`/`expect` on any code path that runs after process start.

**Testing.** `proptest 1.9` for CBOM serialization round-trips; `cargo-fuzz` against the CycloneDX parser; `testcontainers` to spin up a PostgreSQL + SoftHSM2 stack for integration tests.

**Deployment.** Container image (`distroless/cc-debian12`) plus a static-musl edge binary. FedRAMP Moderate target initially.

**Performance.** CI gate evaluation budget is 5 s p95 for repos up to 10k packages.

### C.3.2 Organ 2 — Inflammation Organ (`oqgf-inflammation`)

**Crate layout.** Depends on `oqgf-core`, `oqgf-crypto`, `rustls 0.23` (with `aws-lc-rs` provider and `prefer-post-quantum` feature), `tokio 1.51`, `tracing`, `opentelemetry`, plus optional `regorus` for the response engine.

**Core types.**
```rust
pub struct Sentinel<S: SentinelSource> { src: S, sink: SignalSink }

pub trait SentinelSource: Send + Sync {
    type Event: Send;
    async fn next(&mut self) -> Option<Self::Event>;
}

pub struct TlsObservation {
    pub peer: SocketAddr,
    pub negotiated_group: NamedGroup,    // includes X25519MLKEM768
    pub negotiated_sigalg: SignatureScheme,
    pub sni: Option<String>,
    pub ts: SystemTime,
}

pub struct HndlRiskScore { value: u8, factors: SmallVec<[RiskFactor; 8]> }

pub trait HndlScorer: Send + Sync {
    fn score(&self, o: &TlsObservation, ctx: &AssetContext) -> HndlRiskScore;
}

pub enum ResponseAction {
    Log, RateLimit { rps: u32 }, RotateKey { key_id: KeyId },
    Terminate { reason: String }, Escalate { ir_ref: IncidentRef },
}

pub trait ResponseEngine: Send + Sync {
    async fn react(&self, score: HndlRiskScore, asset: &AssetContext)
        -> Result<Vec<ResponseAction>, InflammationError>;
}
```

**TLS interception.** `rustls 0.23.27+` with `prefer-post-quantum` on by default; X25519MLKEM768 is negotiated where the peer supports it; classical-only connections produce a structured event. For inspection of third-party TLS we use rustls in **peer-as-MITM mode** only with documented consent; otherwise we observe at the metadata layer.

**HNDL detection.** Two-stage: a deterministic rule layer (banned cipher suites, banned groups, classification-of-data lookup) and a learned classifier consumed via ONNX Runtime through `ort` (or, where allowable, a Python-side scikit-learn classifier reached over PyO3). Statistical anomaly detection uses online Welford variance and Mann-Kendall trend tests in pure Rust.

**Threat intelligence.** STIX 2.1 ingest via `stix-rs` (or a thin in-house parser); MISP via REST.

**Graded response engine.** Implemented as a small actor running on tokio, taking `HndlRiskScore` inputs, consulting `regorus`-evaluated policy, and emitting `ResponseAction`s. Rate-limiting uses `governor`. Key rotation calls into `oqgf-genetic`'s signer pool.

**Resolution.** Every action emits a signed event into `oqgf-memory`; resolution requires a DAP-signed acknowledgment.

**Edge.** `oqgf-edge-sentinel` is a no_std + alloc build for ARMv8 and RISC-V targets, suitable for P25 inline deployment. It uses `embassy` for async on bare-metal where tokio is unavailable.

**Performance.** 100k TLS observations/sec/sentinel on a 4-core x86_64; <1 ms p99 to enqueue a scored event.

### C.3.3 Organ 3 — MHC Layer (`oqgf-mhc`)

**Crate layout.** Depends on `oqgf-core`, `oqgf-crypto`, `oqgf-attest`, `tss-esapi 7.6` (TPM), `sev` (AMD SEV-SNP via VirTEE), `tdx` (Intel TDX via VirTEE), Fortanix EDP for SGX targets, `spiffe 0.15` + `spiffe-rustls`, `tokio`.

**Core types.**
```rust
pub trait Attester: Send + Sync {
    type Evidence: Serialize;
    async fn collect(&self) -> Result<Self::Evidence, AttestError>;
}

pub trait Verifier: Send + Sync {
    type Evidence: DeserializeOwned;
    async fn verify(&self, e: &Self::Evidence) -> Result<Attestation, AttestError>;
}

pub enum HardwareRoT {
    Tpm2(TpmEvidence), SevSnp(SnpReport),
    TdxQuote(TdxQuote), Sgx(SgxQuote), H100Cc(H100Evidence),
}

pub struct Attestation {
    pub subject: SubjectId,
    pub measurements: Measurements,
    pub freshness: Nonce,
    pub signatures: DualSignature,       // ML-DSA + SLH-DSA at High-Assurance
}

pub struct QuantumJobAttestation {
    pub circuit_qasm: String,
    pub circuit_digest: Digest,
    pub provider: ProviderId,
    pub device_id: DeviceId,
    pub calibration: CalibrationSnapshot,
    pub samples: SamplingDistribution,
    pub declared_noise_model: NoiseModelRef,
    pub reconciliation: StatTestResult,  // KS or chi-squared
}

pub trait StatReconciler: Send + Sync {
    fn reconcile(&self, samples: &SamplingDistribution, model: &NoiseModel)
        -> StatTestResult;
}
```

**PQC certificate authority.** ML-DSA + SLH-DSA dual-signed X.509 certificates; CA backed by HSM. We follow the `composite-signatures` IETF draft conventions while it stabilizes.

**Quantum hardware broker.** A per-provider adapter (`oqgf-quantum-broker::ibm`, `::braket`, `::azure`, `::ionq`, `::quantinuum`) speaking each provider's REST/gRPC API, normalizing into `QuantumJobAttestation`.

**Statistical reconciliation.** Kolmogorov-Smirnov via `statrs`; χ² via `statrs`. For low-shot counts we use exact tests via `rust-fisher` where available; otherwise the test is marked inconclusive in the attestation.

**Short-lived tokens.** SPIFFE-compatible workload IDs via `spiffe 0.15`; PQC-signed JWTs minted via the dual-family CA. We document explicitly that upstream SPIFFE/SPIRE PQC support is community-driven (as of May 2026) and that our integration uses SPIRE's plugin architecture to inject ML-DSA signing.

**Continuous attestation loop.** A tokio task per workload with a jitter-scheduled re-attestation every `lifetime / 4`. Failures trigger `oqgf-inflammation` responses.

### C.3.4 Organ 4 — Redundant Defense (`oqgf-redundant`)

**Crate layout.** Depends on `oqgf-core`, `oqgf-crypto`, `vsss-rs` (Shamir + Feldman VSS), `automerge` (CRDT audit replication), `aws-lc-rs` (FIPS DRBG), `cryptoki` (HSM-backed RNG).

**Core types.**
```rust
pub struct MultiFamilySigner {
    primary: Arc<dyn Signer>,    // ML-DSA
    secondary: Arc<dyn Signer>,  // SLH-DSA
    tertiary: Option<Arc<dyn Signer>>,  // HQC-based when standardized
}

impl Signer for MultiFamilySigner {
    fn sign(&self, msg: &[u8]) -> Result<Signature, CryptoError> {
        // Sign in parallel; aggregate as DualSignature or TripleSignature.
    }
}

pub trait CloudOrchestrator: Send + Sync {
    async fn place(&self, w: Workload) -> Result<Placement, OrchError>;
    async fn failover(&self, p: &Placement) -> Result<Placement, OrchError>;
}

pub struct EntropyPool {
    sources: Vec<Box<dyn EntropySource>>, // at least two, FIPS-validated
    health: Sp80090BHealthMonitor,
}

pub trait EntropySource: Send + Sync {
    fn read(&mut self, buf: &mut [u8]) -> Result<(), EntropyError>;
    fn descriptor(&self) -> EntropySourceDescriptor; // type, FIPS cert ref
}

pub struct ShamirCustody { shares: Vec<ShareHolder>, threshold: u8 } // 3-of-5
```

**Multi-PQC-family signing facade.** Parallel ML-DSA-87 + SLH-DSA-Shake-192s; HQC will be added once FIPS standardization completes in 2027. Verification accepts any quorum defined by policy (default: both must verify for High-Assurance evidence).

**Multi-cloud.** Provider-agnostic placement via a trait abstraction; concrete implementations for AWS (FedRAMP High), Azure Government, GCP Assured Workloads, and Oracle Government Cloud. Automatic failover is event-driven, not poll-driven, and respects data-sovereignty policy expressed in Rego.

**Entropy.** Two FIPS-validated sources by default: CPU RDSEED (Intel CPU jitter) and an HSM-backed DRBG. **A local FIPS-validated QRNG MAY be added as a third source, but per the DoW CIO memo of 18 Nov 2025 SHALL NOT be the sole source for confidentiality, authenticity, or key establishment.** Continuous Repetition Count and Adaptive Proportion tests per SP 800-90B; min-entropy estimation maintained per source; failed source declared unavailable and replaced.

**Audit trail replication.** `automerge 3` CRDTs over a gossip layer (`libp2p`); append-only hash-linked log inside each CRDT entry for tamper-evidence. Replication targets are configured per jurisdiction.

**Secret sharing.** `vsss-rs` Shamir 3-of-5 for root signing material; Feldman VSS for verifiable shares.

**Quantum entanglement hooks.** A `QuantumNetworkProvider` trait whose default implementation returns `Unsupported`; reserved for future integration but explicitly never relied upon for confidentiality in this version.

### C.3.5 Organ 5 — Memory Organ (`oqgf-memory`)

**Crate layout.** Depends on `oqgf-core`, `oqgf-crypto`, `oqgf-redundant` (for dual-signing), PostgreSQL via `sqlx`, `zstd` for sampling-distribution compression, `rfc3161-client` for timestamping.

**Core types.**
```rust
pub struct AuditEvent {
    pub kind: AuditEventKind,            // Decision, QuantumJob, AttestFail, ...
    pub subject: SubjectId,
    pub dap: Dap,                        // Designated Accountable Party
    pub ts: SystemTime,
    pub payload: AuditPayload,
    pub explanation: Option<Explanation>,
    pub signatures: DualSignature,
    pub tsa_token: Rfc3161Token,
}

pub enum Explanation {
    Tabular { feature_attributions: Vec<(FeatureName, f64)> },
    QuantumPauli { dominant: Vec<(PauliString, f64)> },
    QuantumKernel { kernel_attributions: Vec<(SampleId, f64)> },
    Text { rationale: String, model_ref: ModelRef },
}

pub trait ReSigner: Send + Sync {
    async fn resign(&self, event_id: EventId, new_alg: SignatureAlg)
        -> Result<(), ReSignError>;
}
```

**Forensic event capture.** Every regulated AI/ML decision passes through `oqgf-memory::record()`. For quantum jobs the full sampling distribution is stored zstd-compressed (typical compression ~4–10× for sparse distributions).

**Dual-family audit signatures.** Via `MultiFamilySigner` from Organ 4.

**Re-signing engine.** A scheduled tokio task walks the audit store and re-signs any event whose signatures are older than the configured maximum (default 5 years) under the prevailing algorithm. Originals are preserved; the chain links forward.

**Quantum-appropriate explanations.** Pauli-string dominance via measurement-statistic decomposition (computed Python-side through PennyLane/Qiskit and ingested via PyO3); kernel attribution for QSVM via the closed-form kernel evaluation.

**Long-term retention.** PostgreSQL with table partitioning by year; cross-jurisdictional replication via `oqgf-redundant`.

**Regulator query interface.** Read-only REST API plus OAuth-secured portal; cryptographically signed export bundles include the full chain and the public roots of trust at the time of signing.

**Time-stamping.** RFC 3161 against a PQC-capable TSA; we ship a reference TSA (`oqgf-tsa`) as a separate small crate.

---

## C.4 Python integration layer (`oqgf-python`)

A single `maturin`-built wheel exposing:
- `oqgf.crypto` — `Signer`, `Verifier`, algorithm enums.
- `oqgf.bom` — CBOM, AIBOM construction and signing.
- `oqgf.attest` — quantum job attestation submission and reconciliation.
- `oqgf.memory` — decision recording from Python.
- `oqgf.qsdk` — adapters for **Qiskit ≥ 1.4**, **PennyLane ≥ 0.42**, **Cirq ≥ 1.5**, normalizing circuit + calibration + samples into `QuantumJobAttestation`.
- `oqgf.fl` — **Flower** Strategy subclasses with PQC-signed gradient attestation; **FATE** plugin shims.
- `oqgf.ml` — **MLflow**, **Kubeflow**, **SageMaker** hooks for AIBOM emission at training time and decision logging at inference time.
- `oqgf.notebook` — Jupyter magics for the analyst workflow.

Type stubs are shipped under `oqgf-stubs/`.

---

## C.5 Cross-cutting concerns

**Logging and observability.** `tracing` everywhere; `tracing-opentelemetry 0.31` bridges to OTLP; structured logs that pertain to audit are themselves signed under PQC before export.

**Configuration.** `figment` with layered sources (file → environment → policy-as-code overlay). Schema is `serde`-typed; a malformed config refuses to start.

**Error handling.** `thiserror` in libraries; `anyhow` in binaries; **no `panic!`, `unwrap`, or `expect` in production code paths** — enforced via `clippy::unwrap_used` and `clippy::expect_used` lints set to `deny` in CI.

**Threat modeling per crate.** Each crate ships a `THREAT_MODEL.md` covering trust boundaries, assets, threats (STRIDE-typed), and mitigations.

**Supply chain.** `cargo-audit` against RustSec DB on every CI run; `cargo-deny` for license, banned-crate, and duplicate-version enforcement; `cargo-cyclonedx` produces the per-crate SBOM; `cargo-vet` for peer-audit imports of high-risk dependencies. Reproducible builds inside a pinned container with `--locked`, `--remap-path-prefix`, and a `rust-toolchain.toml`. Compliance with **NIST SP 800-218 SSDF** is mapped per practice in `SSDF.md`.

**Documentation.** `rustdoc` for API docs; `mdbook` for user docs; `utoipa` for OpenAPI emission on REST endpoints; protobuf for gRPC.

---

## C.6 Deployment topology

**Edge.** Minimal Rust binaries (`oqgf-edge-sentinel`, `oqgf-attest-agent`) cross-compiled to ARMv8/RISC-V/x86_64-musl. Static binaries, no dynamic linkage, signed under ML-DSA + LMS. Suitable for P25 inline deployment, GPU farms, and edge AI inference appliances.

**Cloud.** Containerized services in FedRAMP-aligned environments. **Target Moderate baseline initially; High for NSS-adjacent.** Each container ships with an embedded SBOM (`cargo-auditable`) and is signed under dual-family PQC.

**Air-gapped.** Same binaries as edge; policy and audit synchronized via signed export packages on removable media.

**Hybrid quantum-classical.** Integration broker pattern: the broker holds provider credentials inside an HSM-backed secret store; circuits and samples flow through the broker so attestation is uniform.

**Multi-tenant.** Tenant isolation at the database layer (row-level security plus per-tenant signing keys); BYOK supported by treating tenant KEKs as first-class entries in the HSM/PKCS#11 pool.

---

## C.7 Roadmap and phased delivery

**Phase 1 (2026):** Organ 1 (Genetic) plus a P25 PQC crossover MVP. Targets a DOE SBIR award. Deliverables: CBOM/AIBOM toolchain, CI gate, FIPS 140-3 migration helper, edge sentinel reference.

**Phase 2 (2026–2027):** Organs 2 (Inflammation) and 3 (MHC). Targets a FAA NAS PQC pilot. Deliverables: production sentinels, attestation broker, dual-family CA.

**Phase 3 (2027–2028):** Full five-organ implementation aligned to the NIST AI RMF Critical Infrastructure Profile when published. Deliverables: redundant defense (multi-cloud, CRDT audit), memory organ (forensic capture + re-signing), regulator portal.

**Phase 4 (2028+):** Quantum cloud integration broker generalized across providers; FTQC (fault-tolerant quantum computing) governance preview; HQC integrated once FIPS standardization completes.

---

## C.8 Reference implementation milestones

The OQGF reference implementation ships in two tiers.

**Open source (Apache-2.0 + MIT dual license):** `oqgf-core`, `oqgf-crypto`, `oqgf-genetic`, `oqgf-inflammation`, `oqgf-mhc`, `oqgf-redundant` (basic), `oqgf-memory` (basic), `oqgf-python`. CBOM/AIBOM schemas and assessor checklists are CC-BY-4.0.

**Proprietary (Odin's commercial license):** the High-Assurance packaging — multi-cloud orchestration with FedRAMP High controls baked in, cross-jurisdictional CRDT replication, the regulator portal, and 24/7 support — and the OQGF Conformance Toolkit for accredited 3PAOs.

Contribution policy: Apache CLA, signed commits required, all PRs must pass `cargo audit`, `cargo deny`, `cargo cyclonedx`, and the threat-model review for any new trust boundary. The FedRAMP path begins with the cloud-control plane Phase 2; we follow the OSCAL automation pattern for control evidence.

---

## C.9 Traceability — every SHALL in Part A has a hook in Part C

| Requirement | Implementation hook |
|---|---|
| OQGF-G-1, G-2, G-9 | `oqgf-genetic::Cbom`, `Aibom`, scheduled re-emission task |
| OQGF-G-3 | `oqgf-genetic::SignedBom` + `MultiFamilySigner` |
| OQGF-G-4 | `oqgf-genetic::CiGate::evaluate` |
| OQGF-G-5 | `oqgf-crypto::Signer/Verifier` traits, algorithm enums |
| OQGF-G-6 | `aws-lc-rs` FIPS feature; CMVP cert refs surfaced in `Signer::fips_certificate` |
| OQGF-G-7 | `oqgf-genetic::MoscaCalculator` + key-lifetime policy in Rego |
| OQGF-G-8 | `oqgf-policy::regorus` integration, signed bundles |
| OQGF-I-1, I-2 | `oqgf-inflammation::Sentinel` with rustls TLS observation |
| OQGF-I-3 | `oqgf-quantum-broker::TrustModel` records per provider |
| OQGF-I-4 | `oqgf-mhc` layered token + SPIFFE workload + user OAuth |
| OQGF-I-5, I-6, I-7 | `HndlScorer`, `ResponseEngine`, signed resolution events |
| OQGF-M-1..M-7 | `oqgf-mhc`, `oqgf-attest`, `StatReconciler`, continuous-attestation tokio loop |
| OQGF-R-1 | `MultiFamilySigner` |
| OQGF-R-2 | `CloudOrchestrator` |
| OQGF-R-3 | classical fallback in `SignatureAlg`, sunset flag |
| OQGF-R-4 | `EntropyPool` + SP 800-90B health monitor + DoW QRNG policy gate |
| OQGF-R-5 | `automerge` CRDT replication |
| OQGF-R-6 | `vsss-rs` Shamir 3-of-5 |
| OQGF-R-7 | `QuantumNetworkProvider` trait, default `Unsupported` |
| OQGF-A-1..A-7 | `oqgf-memory::AuditEvent`, `Explanation`, `ReSigner`, RFC 3161 TSA, regulator portal |

---

## Closing note

The five-organ structure is not a metaphor we have decorated with engineering. It is engineering whose shape is, by deliberate choice, the shape of a living defense system. We do not believe the AI/quantum governance problem can be solved by adding requirements to a regime that was never designed for an adversary inside the perimeter. The organism is the right unit of analysis, the immune system is the right reference design, and the next eighteen months are the migration window. Build it now, while the deadlines are still ahead of us.

*"There is therefore now no condemnation to them which are in Christ Jesus, who walk not after the flesh, but after the Spirit. For the law of the Spirit of life in Christ Jesus hath made me free from the law of sin and death."* — Romans 8:1–2 (KJV). The framework above is, in its small technical way, an attempt at the same pattern: a law that gives life by enabling truthful self-verification rather than a law that condemns by external audit alone.

— *End of OQGF-1.0 integrated deliverable.*