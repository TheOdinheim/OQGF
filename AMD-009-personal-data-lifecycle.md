# OQGF-1.0 — NORMATIVE AMENDMENT 009
## The Personal Data Requirement: Lifecycle Obligations for Personal Data as a Governed Classification

**Amendment ID:** OQGF-AMD-2026-009
**Amends:** OQGF-1.0, Section A.P (Physiology Layer). Adds a new requirement, OQGF-P-11.
Does **not** modify AMD-007 or OQGF-A; it references the AMD-007 Data Classification vocabulary
and the OQGF-A append-only store, adding personal-data lifecycle obligations across them, per
the OQGF annotation convention. It converts the "privacy-preserving derivative" hook already
present in OQGF-A-1 into a specified obligation with a mechanism.
**Author:** Jeremy Rose, CEO — Odin's LLC, Wasilla, Alaska
**Date:** 15 July 2026
**Status:** Public draft for NIST, sector regulators, and the Odin's engineering team
**Normative dependencies:** OQGF-A (Organ 5, Memory — the append-only store, the DAP, OQGF-A-1,
OQGF-A-5, OQGF-A-6 re-signing, and OQGF-A-7 the regulator query interface); OQGF-I-9 (Boundary
Custody Record) and OQGF-I-11 (ingress into a Privileged Context) and the AMD-007 Data
Classification vocabulary; OQGF-G-2 (AIBOM) and OQGF-G-7 (Mosca's inequality, key lifetime);
OQGF-R-6 (threshold key custody); OQGF-P-9 and OQGF-P-10 (a personal-data risk is a risk, dispositioned
in the Register); CNSA 2.0 for the quantum-safe encryption on which erasure durability rests.

---

## AMD.0 Front matter

### AMD.0.1 Purpose of this amendment

OQGF-1.0 governs *sensitive* data generically. AMD-007's Barrier gates the crossing of
classified data (OQGF-I-10) and quarantines unprovenanced ingress (OQGF-I-11); Organ 5 records a
"privacy-preserving derivative" of a decision's input (OQGF-A-1). Nowhere does the framework say
what obligations attach when the sensitive data is specifically **personal data** — data relating
to an identifiable natural person. Personal data carries duties that generic sensitive data does
not: it must be **minimized** (collect and keep only what a declared purpose needs), **purpose-
limited** (used only for the purpose it was collected for, never silently repurposed), **retention-
bounded** (kept only as long as the purpose requires), **erasable** (removed on a lawful request or
at end of purpose), and its subject must be able to **exercise rights** over it (access,
rectification, erasure). These are the substance of every privacy regime, and the framework is
currently silent on all of them.

Naming them is not the hard part. The hard part is a genuine, load-bearing contradiction with the
framework's own foundations. **The right to erasure says: delete the person's data on request.
The OQGF-A accountability principle says: never delete anything — corrections are annotations,
the historical record is append-only and preserved.** Taken naively, an accountability framework
and a privacy regime cannot both be satisfied: one demands deletion, the other forbids it.

This amendment resolves the contradiction rather than choosing a side, and the resolution is the
core of the amendment: **erasure by crypto-shredding.** Personal data at rest is encrypted under a
per-subject key; erasure is performed by destroying the *key*, not the *record*. The ciphertext
and its audit skeleton — that a record existed, when, under what classification, and on whose
authority it was erased — remain in the append-only store, so accountability and integrity are
preserved. The content is cryptographically irrecoverable, so erasure is satisfied. The append-only
chain is never broken; a signed tombstone records that erasure occurred. Nothing is deleted; the
content is made unreadable. That is how the erasure obligation and the never-delete principle
coexist.

One further point makes this amendment native to a *quantum* governance framework and not a
generic privacy annex bolted onto it. **Crypto-shredding is only durable erasure if the encryption
is quantum-safe.** If personal data were encrypted under a quantum-vulnerable algorithm, a future
cryptographically relevant quantum computer would recover the "erased" content by breaking the
cipher — the harvest-now-decrypt-later adversary applies to erased ciphertext exactly as to any
other ciphertext (OQGF-G-7, Mosca's inequality). Erasure that a future machine can undo is not
erasure. This amendment therefore requires that the key protecting erasable personal data be
quantum-safe (CNSA 2.0). In a post-quantum world, the right to be forgotten is a cryptographic
guarantee only if the cryptography is post-quantum — which is the framework's entire reason for
existing, now applied to privacy.

### AMD.0.2 Why this is a Physiology-Layer requirement and not an organ or Barrier extension

Personal-data obligations are lifecycle-wide, and no single organ owns the lifecycle.
**Minimization** constrains what enters the AIBOM (Organ 1, OQGF-G-2) and what crosses the Barrier
(Organ 2, OQGF-I-11). **Purpose limitation** governs every use, across every organ. **Retention and
erasure** operate in the append-only store (Organ 5, OQGF-A). **Subject rights** are served through
Organ 5's regulator interface (OQGF-A-7). A property whose obligations span Organs 1, 2, and 5 is,
by the framework's own test, a systemic behavior — Physiology, not an organ.

This is the same reasoning that placed OQGF-P-9 and OQGF-P-10 in the cross-cutting namespace: the
obligation is not the function of one anatomical structure but a behavior of the whole system. It
would be a mistake to house personal-data lifecycle inside AMD-007's Barrier merely because the
Barrier already carries a classification vocabulary. The Barrier governs *crossings*; retention and
erasure are not crossings, minimization is not only a crossing, and purpose limitation is not only a
crossing. Forcing the lifecycle into Organ 2 would fragment it across the wrong organ — the exact
anti-pattern AMD-007 itself warns against. This requirement therefore *references* the AMD-007 Data
Classification vocabulary — adding "Personal Data" as a recognized classification the Barrier
already knows how to gate — while *living* at OQGF-P-11, adjacent to the risk requirements it
composes with.

### AMD.0.3 The biological basis

Two biological mechanisms translate this requirement, and together they cover its whole span.

The first is **immune privilege.** Certain compartments — the eye, the brain, the testis, the
maternal–fetal interface — are immune-privileged sites, where material is handled under special,
protective rules: access is restricted, the ordinary responses are modulated, and the compartment
is treated with heightened care precisely because what it holds is consequential. Personal data is
the framework's immune-privileged material: a category that warrants restricted access, declared
purpose, and heightened, lifecycle-long handling beyond what ordinary sensitive data receives. And
critically, immune privilege is a property *orthogonal* to threat level — a privileged site is not
simply "more dangerous," it is *specially governed*. So too personal data: a datum can be personal
and public (a published name), or personal and secret, and the privilege attaches either way.

The second is **apoptosis and clearance.** A cell that has served its purpose does not persist
indefinitely and does not die by rupturing into the tissue. It undergoes **programmed cell death** —
an orderly, regulated dismantling — and is cleanly cleared by macrophages **without triggering
inflammation**. The purpose ends; the cell is removed; the removal is clean and leaves no debris
that provokes autoimmunity. This is the exact shape of retention-limited erasure done right:
personal data collected for a declared purpose is removed when the purpose ends, and the removal is
*clean* — it does not tear a hole in the surrounding record. Crypto-shredding is the apoptotic
mechanism: the content is dismantled (made cryptographically irrecoverable) while the structural
skeleton (that a record existed, its timestamp, its authority) is preserved and the append-only
chain — the tissue — is left intact. Necrosis, a cell bursting and spilling its contents, would be
the naive "delete the record" approach: it satisfies removal but ruptures the integrity of
everything around it. Apoptosis is why the body can shed cells by the billion without ever losing
the coherence of the tissue, and crypto-shredding is why the framework can erase personal data
without ever breaking the append-only record.

### AMD.0.4 Terminology additions

- **Personal Data** — data relating to an identifiable natural person, whether directly (a name, an
  identifier) or indirectly (data that, combined with other held data, identifies a person).
- **Personal-Data Tag** — a Data Classification *dimension* (AMD-007) marking a datum as Personal.
  It **composes with, and is orthogonal to, the sensitivity tier** (Public / CUI / Secret …): a
  datum may be Personal and Public, or Personal and Secret. The tag triggers the lifecycle
  obligations of this requirement regardless of sensitivity tier.
- **Purpose** — the declared reason personal data was collected, recorded in its custody record
  (BCR, OQGF-I-9) or AIBOM (OQGF-G-2). Personal data may be used only for its declared Purpose
  (OQGF-P-11.3).
- **Retention Period** — the declared span, tied to the Purpose, for which personal data may be
  held before erasure (OQGF-P-11.4).
- **Crypto-Shredding (Cryptographic Erasure)** — erasure performed by destroying the quantum-safe
  key under which personal data is encrypted at rest, rendering the ciphertext irrecoverable while
  the record itself is preserved in the append-only store (OQGF-P-11.5). The apoptosis analog.
- **Erasure Tombstone** — the signed, append-only record that an erasure occurred: the record
  reference, the classification, the time, and the acting DAP. The audit skeleton that survives
  clearance.
- **Subject Right** — a data subject's ability to obtain what personal data relating to them is
  held, its purpose and retention, and to require its erasure (OQGF-P-11.6).

### AMD.0.5 Scope and relationship to AMD-007 and OQGF-A

The AMD-007 boundary is reaffirmed: OQGF requires personal-data lifecycle governance as a property
of a conforming system. It does not mandate any particular privacy-management product, consent
platform, or data-subject-request tool; an operator MAY use such tooling to satisfy these
requirements, and conformance is assessed against the requirements here. This amendment does not
weaken OQGF-A: the append-only store is never made deletable. It adds a mechanism — crypto-shredding
— by which the *content* of a personal-data record can be made irrecoverable while the *record*
remains, so the erasure obligation is met without the store ever deleting anything. Where privacy
law and the accountability record are in genuine tension, this amendment resolves that tension
explicitly (AMD.0.6 assumption 1 and its stated residual) rather than leaving it implicit.

This amendment does not claim conformance with any specific privacy statute. Where it cites GDPR,
CCPA/CPRA, or other regimes, it does so as **lineage** — the requirements are consistent with the
established principles of those regimes — not as a certification of compliance, which depends on
jurisdiction-specific facts the framework cannot assess.

### AMD.0.6 Design assumptions requiring confirmation

This amendment makes the following design calls. Each is the fail-safe default; flag any you wish
to change. Assumption 1 is load-bearing and should be ratified explicitly.

1. **Erasure is by crypto-shredding, not record deletion.** Personal data whose erasure may be
   required SHALL be encrypted at rest under a quantum-safe key; erasure destroys the key; the
   append-only record and its audit skeleton are preserved; a signed tombstone records the erasure.
   Assumed because it is the only construction that satisfies both the erasure obligation and the
   OQGF-A append-only / never-delete principle at once. The alternative — deleting the record —
   would break the append-only chain and the accountability guarantee that the whole framework
   rests on, to satisfy an obligation that key destruction already satisfies. **This is the
   decision that reconciles privacy with accountability, and it is yours to ratify.**
2. **Crypto-shredding requires quantum-safe encryption.** The key protecting erasable personal data
   SHALL be quantum-safe (CNSA 2.0). Assumed because a quantum-vulnerable cipher makes "erased"
   ciphertext recoverable by a future CRQC — harvest-now-decrypt-later applies to erased data
   exactly as to any other data (OQGF-G-7). Erasure that a future machine can undo is not erasure;
   in a post-quantum framework, only post-quantum crypto-shredding is durable.
3. **Personal-ness is a classification dimension, orthogonal to sensitivity tier.** A datum can be
   Personal and Public, or Personal and Secret; the Personal-Data Tag triggers lifecycle
   obligations regardless of tier. Assumed because privacy duties attach to personal data even when
   it is not "secret" — a published home address is public and still personal — and conflating
   personal-ness with the Public→Secret scale would leave low-sensitivity personal data ungoverned.
4. **Purpose is declared and binding; repurposing is a fresh, accountable decision.** Personal data
   carries a declared Purpose; using it for a materially different purpose requires a new
   DAP-accountable decision recorded in Organ 5, not a silent reuse. Assumed because purpose
   limitation is the core of every privacy regime, and silent repurposing — support-ticket personal
   data quietly admitted to a training corpus — is exactly the shadow-AI ingress failure AMD-007
   half-addresses; this closes the personal-data half.
5. **Subject rights reuse the OQGF-A-7 regulator interface.** Access and erasure requests are served
   through the existing Organ 5 query interface, extended to authenticated data subjects, within its
   declared response window. Assumed to reuse the accountability surface the framework already has
   rather than mint a second query subsystem.

---

## AMD.1 Normative requirements

These requirements add OQGF-P-11 to Section A.P. They do not modify AMD-007 or OQGF-A; they add
personal-data lifecycle obligations that reference the AMD-007 classification vocabulary and operate
over the OQGF-A append-only store.

**OQGF-P-11.1 (Personal Data as a Governed Classification).** A conforming system SHALL identify
Personal Data — data relating to an identifiable natural person — in scope, and SHALL mark it with a
Personal-Data Tag: a Data Classification dimension (AMD-007) that composes with, and is orthogonal
to, the sensitivity tier. The Personal-Data Tag SHALL trigger the lifecycle obligations of this
requirement (OQGF-P-11.2 through OQGF-P-11.7) regardless of the datum's sensitivity tier, including
where that tier is Public. A system that governs personal data only when it is also highly sensitive
does not satisfy this requirement.

**OQGF-P-11.2 (Minimization).** A conforming system SHALL collect and retain Personal Data only to
the extent necessary for a declared Purpose. Personal Data admitted to a Privileged Context — a
training corpus, evaluation dataset, fine-tuning corpus, model registry, or any AIBOM-governed
artifact (OQGF-I-11, OQGF-G-2) — SHALL be minimized to what the declared Purpose requires. Bulk
admission of Personal Data beyond the declared Purpose, or "collect everything in case it is useful,"
SHALL NOT satisfy this requirement.

**OQGF-P-11.3 (Purpose Limitation).** Personal Data SHALL carry a declared Purpose recorded in its
Boundary Custody Record (OQGF-I-9) or its AIBOM entry (OQGF-G-2). Personal Data SHALL be used only
for its declared Purpose. Use for a materially different purpose SHALL require a fresh decision by a
Designated Accountable Party (OQGF-A-5), recorded in Organ 5; silent repurposing SHALL NOT occur. A
change of purpose is a decision, not a default.

**OQGF-P-11.4 (Retention Bound).** Personal Data SHALL carry a declared Retention Period tied to its
Purpose, and SHALL be erased (OQGF-P-11.5) when the Retention Period elapses or the Purpose is
fulfilled, whichever is earlier. An indefinite-retention default SHALL NOT satisfy this requirement.
The Retention Period is subject to any overriding legal-hold or sector-retention obligation, which,
where it applies, SHALL itself be recorded as the basis for continued retention.

**OQGF-P-11.5 (Erasure by Crypto-Shredding).** Erasure of Personal Data SHALL be performed by
destroying the quantum-safe key under which it is encrypted at rest, and SHALL NOT be performed by
deleting the record from the append-only store (Organ 5, OQGF-A). On erasure: the ciphertext and the
audit skeleton — that a record existed, its timestamp, its classification, and the authority for
erasure — SHALL be preserved; and a signed Erasure Tombstone SHALL be appended recording the erasure
event, its time, and the acting DAP (dual-family signature at High-Assurance per OQGF-M-2). The key
protecting erasable Personal Data SHALL be quantum-safe (CNSA 2.0: ML-KEM key establishment and/or
AES-256), because erasure by key destruction is durable only if the cipher is not quantum-vulnerable
(OQGF-G-7). This requirement reconciles the erasure obligation with the OQGF-A append-only and
never-delete principles: the record is never deleted; its content is made cryptographically
irrecoverable, and the fact and authority of erasure are themselves recorded.

**OQGF-P-11.6 (Subject Rights).** A conforming system SHALL be able to answer, for an authenticated
data subject: what Personal Data relating to them is held, its declared Purpose, and its Retention
Period; and SHALL be able to execute erasure (OQGF-P-11.5) on a lawful request. These SHALL be served
through the Organ 5 regulator query interface (OQGF-A-7), extended to authenticated data subjects,
within that interface's declared response window. A subject's own personal data SHALL be
reconstructable for disclosure and erasable on request through the same accountable interface that
serves a lawful regulatory query.

**OQGF-P-11.7 (Personal Data in the Accountability Record).** Where Organ 5 records a regulated
decision (OQGF-A-1), any Personal Data in the recorded input SHALL be stored either as a
privacy-preserving derivative or under the crypto-shredding regime of OQGF-P-11.5, so that the
accountability obligation (OQGF-A) and the erasure obligation (OQGF-P-11.5) do not conflict. This
converts the "privacy-preserving derivative" hook already present in OQGF-A-1 into a specified
obligation: the accountability record SHALL NOT become a store of un-erasable Personal Data, and the
re-signing of audit records over time (OQGF-A-6) SHALL preserve the crypto-shredding property — a
re-signed record of erased Personal Data SHALL remain irrecoverable.

---

## AMD.2 Conformance criteria per level

**Baseline (OQGF-B):** Personal Data identified and tagged across sensitivity tiers, the tag
triggering lifecycle obligations even when the tier is Public (OQGF-P-11.1); a declared Purpose and
Retention Period per datum (OQGF-P-11.3, OQGF-P-11.4); erasure by crypto-shredding under a
quantum-safe key with the append-only record preserved and a signed tombstone (OQGF-P-11.5);
personal data in the accountability record stored as a derivative or under crypto-shredding
(OQGF-P-11.7). Single-PQC-family tombstone signatures acceptable; at-rest encryption quantum-safe
per CNSA 2.0.

**Enhanced (OQGF-E):** All Baseline criteria, plus minimization into Privileged Contexts
(OQGF-P-11.2); purpose-limitation enforcement with a fresh DAP decision required on any material
repurposing (OQGF-P-11.3); subject access answered through the Organ 5 interface (OQGF-P-11.6).

**High-Assurance (OQGF-H):** All Enhanced criteria, plus subject erasure executed within the
OQGF-A-7 response window (OQGF-P-11.6); dual-PQC-family signatures on Erasure Tombstones (ML-DSA +
SLH-DSA per OQGF-M-2); DAP-reviewed Purpose declarations; **per-subject key granularity** so that
erasure is subject-precise rather than purpose-coarse; threshold custody of erasable-data keys
consistent with OQGF-R-6; and periodic minimization audits of Privileged Contexts.

---

## AMD.3 Assessment procedures

An auditor SHALL:

1. Identify a datum relating to an identifiable person whose sensitivity tier is Public, and confirm
   it is tagged Personal and that the tag triggers the lifecycle obligations despite the Public tier
   (OQGF-P-11.1).
2. Request erasure of a Personal datum and confirm: the quantum-safe key is destroyed; the ciphertext
   and audit skeleton remain in the append-only store; a signed Erasure Tombstone records the event,
   its time, and the acting DAP; and the record is **not** deleted (OQGF-P-11.5). Then confirm the
   at-rest key was quantum-safe (CNSA 2.0) such that the erased content is not recoverable by breaking
   the cipher (OQGF-P-11.5, OQGF-G-7). **This is the load-bearing test of this amendment** — it proves
   erasure and the append-only record coexist.
3. Confirm Personal Data carries a declared Purpose and Retention Period, then attempt to use it for a
   materially different purpose and confirm a fresh DAP decision is required and recorded, not a silent
   reuse (OQGF-P-11.3).
4. Elapse a Retention Period (absent a recorded legal hold) and confirm erasure fires
   (OQGF-P-11.4 → OQGF-P-11.5).
5. Attempt to admit Personal Data beyond the declared Purpose into a training corpus and confirm
   minimization bars the excess (OQGF-P-11.2, via OQGF-I-11).
6. As an authenticated subject, request what Personal Data is held and confirm the Organ 5 interface
   answers within its window; request erasure and confirm it executes per OQGF-P-11.5 (OQGF-P-11.6).
7. Inspect an Organ 5 accountability record containing Personal Data and confirm it is a
   privacy-preserving derivative or under crypto-shredding, and that a re-signed record of erased data
   remains irrecoverable (OQGF-P-11.7, OQGF-A-6).

---

## AMD.4 Control mappings

- **NIST Privacy Framework (NIST PF):** the data-processing and minimization functions — CONTROL-P
  (management of data processing consistent with purpose), COMMUNICATE-P (transparency to
  individuals), and the CT.DM data-management category (retention, disposal, and individual access).
  This is the primary mapping; OQGF-P-11 is the OQGF expression of the Privacy Framework's
  data-lifecycle outcomes.
- **NIST SP 800-53 Rev. 5 — the PT (PII Processing and Transparency) family**, invoked here for the
  first time in the framework: PT-2 (authority and purpose), PT-3 (purpose specification — the direct
  OQGF-P-11.3 mapping), PT-4/PT-5 (consent and privacy notice), PT-6 (system of records), PT-7
  (specific categories of PII); plus SI-12 and AU-11 (information handling and retention, OQGF-P-11.4),
  SI-18 (PII quality), AC-21 (information sharing), and MP-6 (media sanitization, the OQGF-P-11.5
  analog). The framework maps to a document titled *Security and Privacy Controls*; this amendment is
  where the privacy families are finally used.
- **NIST SP 800-88 Rev. 1:** media sanitization, which explicitly recognizes **cryptographic erase**
  as a sanitization technique — the standards basis for OQGF-P-11.5.
- **ISO/IEC 42001 Annex A.7** (data for AI systems, including provenance and quality) for
  minimization into Privileged Contexts; **ISO/IEC 27701** (privacy information management) and
  **ISO/IEC 29100** (privacy framework) lineage for the lifecycle obligations.
- **EU AI Act:** Article 10 (data governance) for minimization and provenance into training data.
- **CNSA 2.0:** ML-KEM-1024 and/or AES-256 for at-rest encryption of erasable Personal Data (the
  durability basis of crypto-shredding); ML-DSA-87 (+ SLH-DSA at High-Assurance per OQGF-M-2) for
  Erasure Tombstones.
- **Privacy-regime lineage (consistency, not certification):** GDPR Art. 5 (minimization, purpose
  limitation, storage limitation), Art. 15 (access), Art. 17 (erasure); CCPA/CPRA (notice, purpose,
  deletion). Cited as the established principles these requirements are consistent with, not as a
  compliance claim.

---

## AMD.5 Technical architecture (implementation hooks)

The Personal-Data Tag is a classification *dimension* composing with the AMD-007 `DataClassification`,
carried on the data descriptor and the Boundary Custody Record. Erasure reuses the existing key
infrastructure — the HSM / PKCS#11 pool in which per-tenant KEKs are already first-class entries — by
adding a per-subject key whose destruction is the erasure act. Tombstones are written to `oqgf-memory`
(Organ 5). No second DAP type is introduced; the existing `DesignatedAccountableParty` is reused, and
the AMD-007 classification machinery is referenced, not duplicated.

### AMD.5.1 Core types

```rust
/// A classification DIMENSION marking a datum as relating to an identifiable
/// person (OQGF-P-11.1). Orthogonal to the AMD-007 sensitivity tier: a datum
/// may be Personal AND Public, or Personal AND Secret. Carried alongside the
/// existing DataClassification, not as a variant of it.
pub struct PersonalDataTag {
    pub subject: SubjectRef,          // the identifiable person (OQGF-P-11.6)
    pub purpose: Purpose,             // declared, binding (OQGF-P-11.3)
    pub retention: RetentionPolicy,   // tied to purpose (OQGF-P-11.4)
    pub key: SubjectKeyRef,           // quantum-safe at-rest key (OQGF-P-11.5)
}

/// The lifecycle governor for personal data. Enforces minimization, purpose
/// limitation, retention, and erasure across Organs 1, 2, and 5 — which is why
/// this is a Physiology-Layer requirement, not an organ extension.
pub trait PersonalDataLifecycle: Send + Sync {
    /// Admit personal data to a Privileged Context only to the extent the
    /// declared Purpose requires (OQGF-P-11.2; gated with OQGF-I-11).
    fn admit_minimized(&self, data: &PersonalDatum, ctx: &PrivilegedContext) -> AdmitResult;

    /// A material change of purpose requires a fresh DAP decision, recorded in
    /// Organ 5 — never a silent reuse (OQGF-P-11.3).
    fn repurpose(&self, datum: &PersonalDatum, new: Purpose, dap: &DesignatedAccountableParty)
        -> Result<(), NeedsFreshDecision>;

    /// Erase by destroying the quantum-safe key, NOT by deleting the record.
    /// The record and audit skeleton persist; a signed tombstone is appended
    /// (OQGF-P-11.5). Returns the tombstone written to Organ 5.
    fn crypto_shred(&self, datum: &PersonalDatum, dap: &DesignatedAccountableParty)
        -> ErasureTombstone;
}

/// The audit skeleton that survives erasure (OQGF-P-11.5). Appended to
/// oqgf-memory; the record is preserved, the content is not recoverable.
pub struct ErasureTombstone {
    pub record_ref: RecordRef,        // the record that remains, now unreadable
    pub classification: DataClassification,
    pub erased_at: SystemTime,
    pub dap: DesignatedAccountableParty,  // reuse existing type (OQGF-A-5)
    pub signature: DualSignature,     // ML-DSA (+ SLH-DSA at High-Assurance)
}
```

The safety property is a key-management fact, not a store-deletion path: the append-only store has
no delete operation, and `crypto_shred` never calls one — it destroys a `SubjectKeyRef` and appends a
tombstone. Because the at-rest key is quantum-safe (CNSA 2.0), the ciphertext that remains is
irrecoverable even against a future CRQC, so the erasure is durable in exactly the threat model the
whole framework is built for. Erasure and append-only integrity are not traded off against each
other; they are made compatible by moving the deletion from the record to the key.

### AMD.5.2 What this closes, and what it does not

This amendment **closes** the following:

- **The absence of personal-data governance.** Personal data now has a classification dimension and a
  full lifecycle — minimization, purpose limitation, retention, erasure, and subject rights — where
  the framework previously governed only generic sensitive data (OQGF-P-11.1 through OQGF-P-11.6).
- **The erasure-versus-append-only contradiction.** Crypto-shredding under a quantum-safe key
  satisfies the right to erasure while the append-only store deletes nothing; the record and the
  authority for its erasure both survive (OQGF-P-11.5).
- **The quantum durability gap in erasure.** Requiring the at-rest key to be quantum-safe closes the
  hole in which "erased" data could be recovered by a future CRQC — the framework's own core threat
  model, applied to erasure (OQGF-P-11.5, OQGF-G-7).
- **Silent repurposing of personal data.** A material change of purpose is now a recorded,
  DAP-accountable decision, closing the personal-data half of the shadow-AI ingress problem AMD-007
  began (OQGF-P-11.3).
- **The un-erasable accountability record.** The OQGF-A-1 "privacy-preserving derivative" hook is now
  a specified obligation, so the accountability store does not become a permanent store of un-erasable
  personal data, and re-signing preserves the erasure (OQGF-P-11.7, OQGF-A-6).

This amendment **does not** fully close, and states so honestly:

- **Erasure durability rests on key destruction being complete.** If a copy of the subject key
  survives — an unpurged backup, an exported HSM blob — the ciphertext becomes recoverable and the
  erasure is illusory. The framework requires quantum-safe encryption and key destruction but cannot
  by itself guarantee no key copy persists anywhere; that is key-management hygiene, a governance and
  operational problem. This is the same shape as prior residuals, bounded by threshold custody
  (OQGF-R-6) and DAP accountability, and named rather than eliminated.
- **Crypto-shredding erases content, not the fact of the record.** The append-only skeleton
  necessarily preserves that a record existed, when, and under what classification. For most privacy
  regimes this is acceptable and is often itself required by the audit obligation; but a regime that
  demanded erasure of the *existence* of a record could not be satisfied without breaking append-only
  integrity. The framework states this tension honestly and resolves it in favor of preserving the
  audit skeleton, because an accountability framework that could erase the fact of its own records
  could erase its own accountability. This is a deliberate boundary, not an oversight.
- **Identifiability is a judgment.** Whether a datum "relates to an identifiable person" — especially
  after pseudonymization or aggregation — is a governance judgment; mislabeling personal data as
  non-personal opens a hole in OQGF-P-11.1. This is the same shape as the AMD-007 classification-
  accuracy residual, mitigated by the content sentinel (OQGF-I-12) and DAP-owned classification
  governance.
- **The declaration can be over-broad.** An over-broad declared Purpose defeats purpose limitation
  from the inside, exactly as an over-broad Root Intent defeats intent binding in AMD-001. Named,
  bounded by DAP accountability and review, not eliminated.

---

## AMD.6 Traceability

| Requirement | Implementation hook |
| --- | --- |
| OQGF-P-11.1 | `oqgf-core::PersonalDataTag` as a dimension composing with AMD-007 `DataClassification`; carried on the data descriptor and `BoundaryCustodyRecord` |
| OQGF-P-11.2 | `PersonalDataLifecycle::admit_minimized`; gated with OQGF-I-11 ingress into a Privileged Context; ties to `bom::Aibom` (OQGF-G-2) |
| OQGF-P-11.3 | `Purpose` on the `PersonalDataTag` / BCR / AIBOM; `PersonalDataLifecycle::repurpose` returns `NeedsFreshDecision`; decision recorded in `oqgf-memory` |
| OQGF-P-11.4 | `RetentionPolicy` tied to `Purpose`; scheduled retention sweep triggering `crypto_shred`; legal-hold override recorded |
| OQGF-P-11.5 | `PersonalDataLifecycle::crypto_shred` destroys a quantum-safe `SubjectKeyRef` (CNSA 2.0, `oqgf-crypto`); no store-delete path; `ErasureTombstone` appended to `oqgf-memory` |
| OQGF-P-11.6 | subject-authenticated path on the OQGF-A-7 regulator interface in `oqgf-memory`; access reconstructs, erasure invokes `crypto_shred` |
| OQGF-P-11.7 | Organ 5 `AuditEvent` stores personal input as a privacy-preserving derivative or under crypto-shredding; `ReSigner` (OQGF-A-6) preserves irrecoverability |

---

## AMD.7 Change log

v1.0 — Initial public draft, 15 July 2026. Adds OQGF-P-11 (Personal Data) to the Physiology Layer:
personal data becomes a governed classification dimension (orthogonal to the AMD-007 sensitivity
tier) carrying lifecycle obligations — minimization into Privileged Contexts, declared and binding
purpose with accountable repurposing, retention bounds, erasure, and subject rights. The load-bearing
contribution is the reconciliation of the right to erasure with the OQGF-A append-only / never-delete
principle: erasure is performed by crypto-shredding — destroying the quantum-safe at-rest key — so the
record and its audit skeleton are preserved while the content is made cryptographically irrecoverable,
and a signed Erasure Tombstone records the erasure. Because a quantum-vulnerable cipher would let a
future CRQC recover "erased" data (OQGF-G-7), the at-rest key SHALL be quantum-safe (CNSA 2.0): in a
post-quantum framework, only post-quantum crypto-shredding is durable erasure. Converts the OQGF-A-1
"privacy-preserving derivative" hook into a specified obligation and requires re-signing (OQGF-A-6) to
preserve irrecoverability. References the AMD-007 classification vocabulary and the OQGF-A store
without modifying either; invokes the NIST SP 800-53 PT family for the first time in the framework.
Four residuals are named rather than claimed eliminated — key-destruction completeness, erasure of the
fact versus the content, identifiability judgment, and over-broad purpose declaration — each mapped to
the shape of a prior amendment's residual.

— End of OQGF Amendment 009.
