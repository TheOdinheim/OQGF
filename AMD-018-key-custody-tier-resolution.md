# AMD-018 — Key Custody Tier Resolution

**Amendment ID:** AMD-018
**Amends:** OQGF-1.0 §A.4.3 (OQGF-R-6), §A.4.4 (Organ 4 conformance criteria), §A.4.5 (assessment procedures)
**Status:** Normative amendment to OQGF-1.0
**Author:** Jeremy Rose, CEO — Odin's LLC, Wasilla, Alaska
**Date:** 7 September 2026
**Designated Accountable Party:** Jeremy Rose

---

## AMD.0 Why this amendment exists

OQGF-1.0 states OQGF-R-6 two ways, and they do not agree.

**§A.4.3 (normative requirement):**

> **OQGF-R-6** Long-lived secrets (root signing keys, audit-signing keys) SHALL be sharded using Shamir's Secret Sharing or threshold cryptography with a quorum of at least 3-of-5.

An unqualified SHALL. It binds at every conformance level, including Baseline.

**§A.4.4 (conformance criteria per level):**

> - **Baseline:** Single PQC family acceptable; one cloud; one entropy source plus DRBG.
> - **Enhanced:** Dual PQC families for audit signatures; multi-cloud capable; two entropy sources.
> - **High-Assurance:** Dual or triple PQC families for all evidentiary signatures; multi-cloud live; cross-jurisdictional audit replication; **3-of-5 threshold custody**.

Threshold custody appears at High-Assurance only. Baseline and Enhanced do not name it.

**A framework cannot require something unconditionally in one section and gate it to one tier in another.** An implementer reading §A.4.3 concludes they are non-conformant at every level without Shamir. An implementer reading §A.4.4 concludes threshold custody is a High-Assurance obligation and their Enhanced posture is fine. Both readings are supportable from the text, which means the requirement is unenforceable as written: any auditor finding can be answered by pointing at the other section.

This surfaced in production. The BROKKR architecture (BROKKR-ARCH-2026-001, Rev 1.18 §1.4, §6.11, §13) recorded OQGF-R-6 as **PARTIAL with the gap named**, explicitly declining to resolve the contradiction in its own favor:

> "This architecture does not resolve that contradiction; it is a framework ambiguity referred upward. … BROKKR does not claim OQGF-R-6 satisfied at Enhanced. It is recorded PARTIAL with the gap named. Naming an unmet requirement is conformant. Quietly reading it down to a tier where it vanishes is not — and reading it down would have been the disposition that unblocked the build, which is precisely why it was not chosen."

That is the correct behavior for an implementation and the wrong outcome for a framework. An implementation that refuses to read a requirement down is doing its job; a framework that forces that choice is not doing its own. **This amendment resolves the ambiguity at the level that owns it.**

---

## AMD.1 Disposition

**The §A.4.4 tiered reading governs.** Threshold custody is a High-Assurance obligation. Enhanced requires hardware-backed key custody with dual-control issuance and declared custody model. §A.4.3's unqualified SHALL is replaced with tiered normative text that says the same thing the conformance table already said.

This resolution is not chosen because it is easier. It is chosen for two reasons, stated so a future reader can weigh them.

### AMD.1.1 Reason one — the requirement matches the tier's threat model

Every other High-Assurance obligation in OQGF-1.0 shares a shape: **it requires organizational scale, not merely better engineering.**

| High-Assurance obligation | What it requires beyond Enhanced |
|---|---|
| OQGF-R-5 — cross-jurisdictional audit replication | Legal presence in two or more jurisdictions |
| OQGF-M-2 — dual-family signed attestations | An attestation issuer capable of dual-family signing |
| OQGF-M-3 — reconciliation on *every* quantum job | Continuous statistical infrastructure, not sampled |
| OQGF-M-6 — vendor trust score **gating procurement** | A procurement function the score can gate |
| OQGF-I — continuous monitoring of every session | A staffed monitoring capability |

3-of-5 threshold custody is that same shape. It requires **five distinct key holders with genuine separation of duty** — five people (or five organizational roles) who can be assembled for a key ceremony and who do not collude. That is an organizational property, not a cryptographic one.

For an organization that cannot staff five separated holders, "3-of-5" produces one of two outcomes, both bad:

1. **Theater** — one person holds five shares in five folders, or two people hold shares in a way that reconstructs on either's authority. The mechanism is present and the property it exists to provide is absent.
2. **A false claim** — the requirement is checked off because Shamir code exists, without the custody separation that makes Shamir meaningful.

**A requirement placed at a tier where its implementers cannot honestly satisfy it does not raise the floor. It teaches implementers to read requirements down**, and once that habit exists it does not stay confined to the requirement that taught it. This is the same failure mode OQGF-P-2 forbids for deterministic gates and the same one the framework's own assessment procedures are designed to catch.

### AMD.1.2 Reason two — the two tiers defend against different threats, and both threats are real

Naming what each posture defends against makes the distinction principled rather than arbitrary.

**Enhanced — HSM-backed custody with dual control defends against:**
- **Key exfiltration.** The private key never exists in extractable form outside the hardware boundary. An attacker with full filesystem and memory access on the host does not obtain the key.
- **Unilateral issuance.** No single operator can sign, issue, or authorize a key operation alone. A compromised or malicious individual acting alone cannot produce a valid signature.
- **Undeclared custody.** The custody model is recorded in the CBOM, so the posture is auditable and a change to it is a visible change.

**High-Assurance — k-of-n threshold custody additionally defends against:**
- **Coerced or compromised operators exceeding the dual-control quorum.** Dual control fails when two operators collude, are coerced together, or are the same person under two credentials. A 3-of-5 threshold requires three of five separated holders, which raises the collusion bar and — critically — makes single-point coercion insufficient by construction rather than by policy.
- **HSM compromise as a single point of failure.** A threshold scheme can distribute shares across distinct hardware, distinct custodians, and distinct jurisdictions, so compromise of one HSM does not compromise the key. This is OQGF-R's own no-single-point-of-failure principle applied to custody, and it is why the requirement belongs at the tier that also mandates multi-jurisdictional replication (R-5).
- **Loss of a custodian.** Recovery from the loss of one or two holders without key loss is a property of k-of-n that dual control does not provide.

**Neither posture is weak.** Enhanced defends the threats an Enhanced-tier organization faces. High-Assurance defends the threats an organization operating across jurisdictions with adversarial nation-state exposure faces. The distinction is the threat model, and the tiers exist to say which threat model applies.

---

## AMD.2 Normative amendments

### AMD.2.1 OQGF-R-6 is replaced

**Strike** the current §A.4.3 OQGF-R-6 text:

> ~~**OQGF-R-6** Long-lived secrets (root signing keys, audit-signing keys) SHALL be sharded using Shamir's Secret Sharing or threshold cryptography with a quorum of at least 3-of-5.~~

**Replace with:**

> **OQGF-R-6** Long-lived secrets — root signing keys, audit-signing keys, and any key whose compromise would permit forgery of evidence relied upon as legal record — SHALL be held under a custody model appropriate to the declared conformance level, and that model SHALL be declared in the CBOM.
>
> - **OQGF-R-6.1 (Baseline)** Long-lived secrets SHALL be protected against extraction, and the protection mechanism SHALL be declared. Software-held keys are permitted at Baseline if the CBOM declares them as such.
>
> - **OQGF-R-6.2 (Enhanced)** Long-lived secrets SHALL be held in a hardware security module or equivalent hardware-backed key store from which the private key material cannot be extracted, and key issuance and rotation SHALL require dual control — no single individual or credential SHALL be sufficient to issue, rotate, or authorize use of a long-lived secret. The custody model, the hardware boundary, and the dual-control procedure SHALL be declared in the CBOM.
>
> - **OQGF-R-6.3 (High-Assurance)** In addition to R-6.2, long-lived secrets SHALL be held under k-of-n threshold custody using Shamir's Secret Sharing or threshold cryptography, with a quorum of at least 3-of-5. Shares SHALL be held by distinct custodians with documented separation of duty; a share-holding arrangement in which fewer than k independent parties can reconstruct the secret SHALL NOT satisfy this requirement. The organization SHALL maintain a documented key ceremony, a recovery procedure, and a rotation procedure, and SHALL rehearse recovery at least annually with the rehearsal recorded.
>
> **A declared custody model that overstates the separation actually achieved is a conformance failure, not a documentation defect.** Threshold cryptography implemented without custodial separation satisfies R-6.3 in mechanism and fails it in substance; assessment (§A.4.5) tests the separation, not the algorithm.

### AMD.2.2 §A.4.4 conformance criteria are amended

**Replace** the Organ 4 conformance criteria with:

> - **Baseline:** Single PQC family acceptable; one cloud; one entropy source plus DRBG; long-lived secrets extraction-protected with the mechanism declared (R-6.1).
> - **Enhanced:** Dual PQC families for audit signatures; multi-cloud capable; two entropy sources; **HSM-backed key custody with dual-control issuance and CBOM-declared custody model (R-6.2)**.
> - **High-Assurance:** Dual or triple PQC families for all evidentiary signatures; multi-cloud live; cross-jurisdictional audit replication; **3-of-5 threshold custody with documented ceremony, separated custodians, and annual recovery rehearsal (R-6.3)**.

### AMD.2.3 §A.4.5 assessment procedures are amended

**Replace** assessment item (4) with a tiered procedure:

> (4) **Key custody, per declared level.**
> - **At Baseline:** inspect the CBOM's declared protection mechanism for long-lived secrets and verify the declaration matches the deployed mechanism.
> - **At Enhanced:** verify the private key material is non-extractable from the declared hardware boundary — request an export and confirm refusal — and inspect the dual-control procedure and its issuance records. **Attempt a single-operator issuance and confirm it is refused.**
> - **At High-Assurance:** additionally inspect Shamir share custody records, verify that shares are held by distinct custodians with documented separation of duty, inspect the key ceremony record, and inspect evidence of an annual recovery rehearsal. **Verify by inquiry that fewer than k independent parties cannot reconstruct the secret** — a threshold scheme whose shares are held by one party or one role does not satisfy R-6.3.

---

## AMD.3 What this amendment does not do

**It does not weaken key custody at any tier.** Enhanced previously had *no* named custody requirement in its conformance criteria while §A.4.3 demanded 3-of-5 unconditionally. After this amendment Enhanced has an explicit, testable custody requirement — hardware-backed, dual-control, CBOM-declared — where before it had a contradiction. **For an implementer who read §A.4.4 as governing, this is a strict increase in obligation.** For one who read §A.4.3 as governing, it is a relocation of one requirement to the tier whose threat model it addresses, with a substantive requirement put in its place.

**It does not remove threshold custody from the framework.** R-6.3 preserves the 3-of-5 quorum verbatim and adds what the original text lacked: custodial separation, a ceremony, a recovery procedure, and annual rehearsal. The original requirement could be satisfied by a Shamir implementation with all shares in one hand. **R-6.3 cannot.**

**It does not grant any implementation a pass.** An implementation claiming Enhanced must now demonstrate hardware-backed custody and dual control under §A.4.5, including a refused single-operator issuance. An implementation claiming High-Assurance must demonstrate everything Enhanced requires plus separated custodians and a rehearsed recovery.

**It does not disposition any specific implementation's conformance.** Whether a given system satisfies R-6.2 or R-6.3 is an assessment finding under §A.4.5, made against that system's evidence. This amendment states the requirement; it does not certify anyone against it.

---

## AMD.4 Effect on existing conformance claims

**Every conformance result recorded before this amendment is provisional with respect to OQGF-R-6.** A prior `partial` or `absent` verdict on R-6 was measured against a contradictory requirement and cannot be carried forward unexamined. The next conformance assessment of any affected system SHALL enumerate R-6.1, R-6.2, or R-6.3 as applicable to its declared level and record a verdict — `satisfied`, `partial`, `absent`, or `n.a. with justification` — with evidence.

**A verdict may move in either direction.** A system that recorded R-6 as `partial` because it lacked threshold custody at Enhanced may now record `satisfied` against R-6.2 *if and only if* it demonstrates hardware-backed custody and dual control. A system that recorded R-6 as `satisfied` on the strength of a Shamir implementation may now record `partial` against R-6.3 if its shares are not held by separated custodians. **The amendment does not automatically improve any verdict; it makes each verdict determinable.**

---

## AMD.5 Control mappings

The Organ 4 control mappings in §A.4.6 are extended:

- **NIST SP 800-53 Rev. 5:** SC-12 (cryptographic key establishment and management) and **SC-12(1) (availability)** and **SC-12(2)/(3) (symmetric and asymmetric key management)** apply at all levels; **SC-12(6) (physical control of keys)** maps to R-6.2's hardware boundary; **CP-9 (system backup)** and **SC-12(1)** map to R-6.3's recovery rehearsal.
- **NIST SP 800-57 Part 1 Rev. 5:** §6 (key management phases) and §8.1.5.2 (key recovery) inform R-6.3's ceremony and recovery obligations.
- **FIPS 140-3:** Level 2 or above satisfies R-6.2's hardware boundary where the module's key-storage service is used; the level SHALL be declared in the CBOM. **A FIPS validation is not by itself evidence of dual control** — R-6.2 requires both.
- **ISO/IEC 42001 Annex A:** A.6 (AI system lifecycle), A.9 (use of AI systems) unchanged.
- **CNSA 2.0:** unchanged.

---

## AMD.6 Rationale summary

The framework said two incompatible things about the same requirement, and an implementation caught it by refusing to choose the convenient reading. That refusal is what a governance framework is supposed to produce, and the framework owed it an answer.

The answer is that **key custody is tiered because the threats it defends against are tiered.** Hardware-backed custody with dual control defends the Enhanced threat model — key exfiltration and unilateral issuance — and it is testable, achievable, and now explicitly required where before it was absent. Threshold custody defends the High-Assurance threat model — custodian coercion, HSM single-point compromise, and custodian loss — and it belongs beside cross-jurisdictional replication, because both require the same thing: an organization distributed enough that no single point of trust remains.

**Placing each control at the tier that can implement it honestly is stronger framework design than placing every control at the tier that sounds strongest.** A requirement no one can meet is a requirement everyone learns to explain away.
