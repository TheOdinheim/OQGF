# OQGF-1.0 — NORMATIVE AMENDMENT 012
## The Recursive Risk-Propagation Requirement: Governing Residual, Induced, and Downstream Risk in Machine-Speed AI Systems

**Amendment ID:** OQGF-AMD-2026-012
**Amends:** OQGF-1.0, Section A.P (Physiology Layer). Adds a new requirement, OQGF-P-13.
Does **not** modify OQGF-P-10 (AMD-008), OQGF-P-12 (AMD-011), or any prior amendment; it governs
the cross-cutting causal, temporal, and topological relationships among the risks those amendments
surface, per the OQGF annotation convention.
**Author:** Jeremy Rose, CEO — Odin's LLC, Wasilla, Alaska
**Date:** 14 August 2026
**Status:** Public draft for NIST, sector regulators, and the Odin's engineering team
**Normative dependencies:** OQGF-P-10 (AMD-008, Risk Surveillance — the authoritative Risk
Register this amendment indexes into, never duplicates); OQGF-P-12 (AMD-011,
Capability-Triggered Assurance — Capability Envelope, Trajectory Record, independent
termination); OQGF-M-8 through OQGF-M-14 (AMD-001, intent provenance and monotonic attenuation);
OQGF-P-2 (AMD-002, deterministic/heuristic boundary); OQGF-P-5 (AMD-002, response-storm
detection and host-harm bound); OQGF-P-7 (AMD-004, coordinated signaling and cascade bounds);
OQGF-P-8 (AMD-005, resolution and de-escalation); OQGF-P-9 (AMD-006, accountable risk
acceptance); OQGF-I-6 (graded response); OQGF-A-1 and OQGF-A-5 (decision records and the
Designated Accountable Party); A.6.1 (incident response); A.6.3 (human oversight).

---

## AMD.0 Front matter

### AMD.0.1 Purpose of this amendment

AMD-008 establishes the load-bearing premise. Its terminology defines Residual Risk as the risk
remaining after a Reduce or Transfer disposition, "itself re-assessed and re-dispositioned." Its
OQGF-P-10.5 states that a mitigation cannot close a risk without assessing what remains. Its
reference type makes the recursion explicit:

```rust
Reduce   { plan: TreatmentPlan, residual: Box<RiskEntry> }
Transfer { mechanism: TransferMechanism, residual: Box<RiskEntry> }
```

That type is correct but structurally limited. `Box<RiskEntry>` is a linked list — one parent,
one child. Real-world risk propagation is not a list. It is a graph:

- **One risk branches into several.** A compromised credential exposes the systems it
  authenticates to, the data those systems hold, and the supply chain they feed. That is three
  downstream risks from one event, not one residual.
- **Several risks converge into one.** A compound failure — a model trained on biased data,
  deployed with overbroad authority, in a system with no independent termination — is not caused
  by any single predecessor. It is caused by the convergence of several.
- **A control reduces one risk while inducing another.** An automated emergency shutdown protects
  integrity but threatens availability. Immunosuppression treats autoimmunity but opens the door
  to opportunistic infection. The treatment is not free of risk; it shifts risk from one node
  to another.
- **A descendant is shared by several causal paths.** Two independent failures may each
  independently lead to the same downstream consequence. Deduplicating one path hides the
  second.
- **A feedback loop returns to an earlier state.** A response can amplify the condition that
  triggered it. AMD-004's cascade bounds govern the signal loop; nothing governs the *risk
  topology* of the loop.
- **Propagation can outrun human response.** Knight Capital lost $460 million in 45 minutes. The
  July 2026 agent incidents ran for days before detection. When the time to an irreversible
  consequence is shorter than the time a human needs to detect, decide, and act, human oversight
  is not a real-time control — it is after-the-fact accountability. That distinction must be
  governed.

AMD-001 governs authority and intent across hops. AMD-004 governs authenticated defensive-signal
cascades and bounds their loops. AMD-011 governs capability, containment, sub-agent attenuation,
independent termination, and trajectory reconstruction. No current OQGF requirement makes the
**risk-propagation topology itself** a first-class governed object that links all of those
mechanisms through one auditable causal and temporal model.

This amendment supplies the missing systemic behavior. It does not replace the Risk Register, the
Capability Envelope, the Intent Provenance Chain, the Signal Cascade, the Trajectory Record, or
accountable acceptance. It links them through one governed graph and adds the temporal governance
that determines whether human intervention can be credited as a real-time control.

### AMD.0.2 Why this is a Physiology-Layer requirement and not an extension to AMD-008 or AMD-011

Three alternative placements were analyzed.

**Embedding in AMD-008** would place graph topology, temporal containment, capability
reconciliation, and machine-speed control semantics inside a requirement whose present purpose is
risk registration and disposition. AMD-008 catalogs and dispositions risks; this amendment governs
how risk *moves, changes, branches, combines, and feeds back* across the system AMD-008 describes.
Making AMD-008 carry both would overload a register requirement with systemic temporal-control
semantics and blur the clean separation between "what are the risks" and "how do they propagate."

**Embedding in AMD-011** would confine the principle to autonomous agent systems. The same
propagation topology exists in algorithmic trading, cyber-physical control, supply chains,
identity systems, automated incident response, and tightly coupled digital infrastructure. An
agent-specific home would wrongly narrow a general risk property.

**Splitting across AMD-008 and AMD-011** would fragment one safety property across two amendment
lifecycles and create room for partial implementation to be mistaken for full graph governance.

No single organ owns recursive risk propagation. A root risk may originate in Organ 1, be
detected by Organ 2, cross an identity boundary in Organ 3, require containment by Organ 4, and
be reconstructed from Organ 5. Its downstream consequences may be created by a control, an agent,
a dependency, a person, or an external system. The propagation topology is a property of the whole
governed system. That is the Physiology-Layer test, and it is the same test that placed risk
surveillance (P-10), personal data (P-11), and capability-triggered assurance (P-12) in this
namespace.

### AMD.0.3 The biological basis

The immune system does not encounter a threat, apply one response, and declare the matter closed.

A primary disturbance produces downstream signaling, recruitment, inflammation, tissue damage,
compensatory regulation, and further signals. The response can attenuate the threat, but the
response can also become a source of host harm. OQGF already encodes parts of this biology:
OQGF-P-5 treats self-harm and response storms as governable failures; OQGF-P-7.5 requires signal
cascades to be rate-limited and loop-bounded; OQGF-P-8 governs resolution rather than assuming
that escalation ends itself.

What the framework does not yet encode is the **topology of the cascade as a governed object**.
The complement cascade is a directed graph with amplification loops: C3 convertase cleaves C3 into
C3a and C3b; C3b feeds back to form more C3 convertase (positive feedback); regulatory proteins
(Factor H, Factor I, C1-inhibitor) are embedded checkpoints at every amplification node, not
afterthoughts bolted on at the end. The coagulation cascade is the same shape: thrombin activates
more prothrombin (positive feedback), while antithrombin and protein C provide structurally
embedded negative feedback. In both systems, the *topology* — which nodes amplify, which
attenuate, where feedback returns, and how fast each transition fires — is the thing the body
governs, not just the individual molecules.

And critically, the body governs the **time** of the cascade. The complement system activates in
seconds, far faster than the adaptive immune system can mount a response. The body does not
pretend that adaptive immunity (which takes days) is a real-time control for complement (which
takes seconds). It places **innate, pre-positioned, fast-acting controls** at the amplification
nodes — properdin, Factor H, C4b-binding protein — that act at the speed of the cascade, not at
the speed of deliberation. The adaptive system provides the intelligent, targeted, retrospective
response; the innate controls provide the *in-time* containment.

The translation is exact. A risk propagation graph in an AI system has amplification loops
(a response that worsens the condition), attenuation points (controls that reduce risk),
convergence (compound failures from multiple causes), and feedback (a downstream state that
re-creates an upstream condition). The topology must be governed as a structure, not flattened
into a list. And when propagation can reach an irreversible consequence faster than a human can
detect, decide, and act, **pre-authorized deterministic controls** — the innate complement
regulators — must be positioned at the amplification nodes. Human oversight is the adaptive
immune system: intelligent, accountable, retrospective. It is not a real-time control when the
cascade moves faster than deliberation.

A treatment that creates harm is the clinical concept of **iatrogenic injury**: the therapy
itself becomes a source of disease. CAR-T cytokine release syndrome (the engineered immune
therapy triggers a cytokine storm that threatens the patient's life) and
immunosuppression-induced opportunistic infection (suppressing autoimmunity opens the door to
pathogens the immune system would normally clear) are the canonical examples. The governance
translation is P-13.6: every material control must be assessed for the risk it creates,
displaces, concentrates, delays, or amplifies. A control is not credited solely on the reduction
it produces at one node when its downstream effect increases total risk elsewhere beyond
tolerance.

### AMD.0.4 Terminology additions

- **Recursive Risk-Propagation Graph (RRPG)** — a directed, attributed, temporal multigraph in
  which Risk Nodes represent governed risk states and Causal Edges represent evidenced mechanisms
  by which one risk's materialization, treatment, transfer, acceptance, or surrounding condition
  may create, expose, attenuate, amplify, or accelerate another risk. It is a multigraph because
  two nodes may be connected by more than one mechanism. It may contain cycles and therefore
  SHALL NOT be treated as a directed acyclic graph by assumption. The RRPG is a relationship
  layer over the authoritative AMD-008 Risk Register; it does not duplicate risk records.
- **Risk Node** — an addressable risk state mapped to one authoritative AMD-008 `RiskEntry`,
  with a stable identifier, owner, assessment, disposition, evidence, and current status.
- **Root Risk Node** — a Risk Node selected as the starting point for a particular analysis.
  A node may be a root in one analysis and a downstream node in another; "root" is a viewpoint,
  not an assertion that no prior cause exists.
- **Residual Risk Node** — the Risk Node representing what remains after a Reduce or Transfer
  treatment. A successor in the graph, subject to the same identification, assessment, ownership,
  disposition, and propagation requirements as any other Risk Node.
- **Induced Risk Node** — a risk created or materially increased by a treatment, safeguard,
  governance decision, recovery action, or other attempted control. The iatrogenic-injury analog.
- **Propagated Risk Node** — a downstream risk exposed or created through a causal mechanism
  across a technical, organizational, agent, market, social, or physical boundary.
- **Compound Risk Node** — a risk whose materialization depends on, or is materially worsened by,
  the convergence of two or more predecessor paths. A compound node preserves all material
  incoming lineage rather than selecting one convenient cause.
- **Systemic Risk Node** — a downstream risk whose scope extends beyond the originating component
  or organization because of common dependencies, correlated behavior, interconnected systems,
  or repeated use of a common model or control.
- **Causal Edge** — a directed, evidenced relationship between two Risk Nodes recording the
  mechanism, triggering condition, estimated latency, direction of effect, confidence, evidence
  provenance, and any boundary crossed.
- **Propagation Path** — an ordered sequence of Risk Nodes and Causal Edges through which risk
  may move or transform.
- **Feedback Component** — a set of Risk Nodes connected by a directed cycle, such that a
  downstream state can reinforce, recreate, or accelerate an earlier state.
- **Unresolved Risk Frontier** — the set of reachable points at which analysis stops without a
  valid termination condition because of missing evidence, unknown behavior, model limits,
  organizational boundaries, tooling limits, or a declared cutoff. A frontier is an open risk
  condition, not evidence of safety.
- **Propagation Latency** — the elapsed time, or defensible range, between the triggering
  condition on an edge and materialization of its downstream Risk Node.
- **Response Budget** — the combined time required to detect a material transition, make the
  authorized decision, and activate the effective control.
- **Time to Irreversibility** — the estimated time until a consequence cannot be reliably
  prevented, recalled, or restored within declared tolerances.
- **Intervention Margin** — `Time to Irreversibility − Response Budget`. A zero, negative, or
  materially uncertain margin means an ordinary human-only response cannot be credited as the
  primary real-time prevention control.
- **Graph Termination Condition** — an evidenced condition under which traversal of a particular
  path may stop without concealing a plausible material successor. Termination is path-specific.

### AMD.0.5 Scope, and the relationship to AMD-008 and AMD-011

| Existing requirement | Existing function | Addition in this amendment |
| --- | --- | --- |
| OQGF-P-10 / AMD-008 | Identifies, assesses, owns, dispositions, tracks, and retains each risk | Makes each material risk an addressable node and governs causal, temporal, branching, converging, and cyclic relationships among nodes |
| OQGF-P-10.5 | Re-assesses and re-dispositions residual risk | Prohibits treating that residual as the endpoint; maps its material outgoing edges and induced risks |
| OQGF-P-12.2 / AMD-011 | Declares what the composed system can do | Uses the Capability Envelope to identify plausible effect channels and graph-change triggers |
| OQGF-P-12.6 | Attenuates sub-agent capability and authority | Maps sub-agent creation and interaction to downstream nodes and cross-agent edges |
| OQGF-P-12.8 | Reconstructs the complete action trajectory | Reconciles observed actions and effects against predicted nodes and edges |
| OQGF-M-8–M-14 / AMD-001 | Binds and attenuates intent across hops | Compares authorized intent lineage with actual risk propagation |
| OQGF-P-7 / AMD-004 | Coordinates defensive posture and bounds signal cascades | Treats a harmful or amplifying response cascade as graph content |

The RRPG is an index and relationship layer over authoritative OQGF records. It SHALL NOT create
a competing copy of the Risk Register. Every Risk Node refers to exactly one authoritative
`RiskEntry`; the graph supplies lineage, topology, time, and evidence.

### AMD.0.6 Design assumptions requiring confirmation

This amendment makes the following design calls. Each is the fail-safe default. All were ratified
by the DAP on 14 August 2026 and are recorded here as decided.

1. **Standalone placement at OQGF-P-13.** *(Ratified.)* The requirement spans every organ and
   applies beyond agent systems — algorithmic trading, cyber-physical control, supply chains,
   tightly coupled digital infrastructure. Embedding in AMD-008 or AMD-011 would either overload
   a register requirement or wrongly narrow the principle to agents.
2. **The graph is a directed temporal multigraph, not a tree.** *(Ratified.)* The existing
   AMD-008 recursive field remains a valid simple-case representation, but the normative record
   must preserve branching, convergence, shared descendants, and cycles when they exist.
3. **Depth is condition-based, not fixed.** *(Ratified.)* No universal layer count is asserted.
   A configured cutoff is permitted only when the resulting Unresolved Risk Frontier is recorded,
   owned, assessed, and dispositioned. This matches the declared-not-fixed pattern of AMD-010
   (Scope Bound) and AMD-011 (Capability Properties).
4. **Materiality thresholds are declared governance policy.** *(Ratified.)* Approved by a DAP,
   recorded, and unavailable to the governed model for unilateral change. Low probability SHALL
   NOT by itself exclude catastrophic, rights-affecting, safety-critical, or systemic impact.
5. **AI may propose; it may not authorize.** *(Ratified.)* A neural system may discover candidate
   nodes, edges, treatments, or evidence. Only the deterministic governance path may adopt a graph
   mutation, close a path, reduce severity, remove an edge, or treat a frontier as resolved.
   This preserves the OQGF-P-2 invariant: neural components are heuristic proposers; the
   deterministic path is the gate.
6. **Timing is relative to the governed system.** *(Ratified.)* "Machine-speed" is not assigned
   one universal threshold. It is present when the credible Response Budget is greater than or
   too close to the Time to Irreversibility for the path being governed. Ranges and qualitative
   bands are acceptable where point estimates would create false precision.
7. **Transfer does not terminate causal responsibility.** *(Ratified.)* Contractual or financial
   transfer may alter accountability or loss allocation, but it does not establish that technical,
   societal, third-party, or systemic consequences cease.
8. **An acceptance does not silently flow downstream.** *(Ratified.)* Each material descendant is
   separately assessed and dispositioned. A broad acceptance of unknown descendants is prohibited,
   consistent with AMD-006's prohibition on blanket acceptance of a class of risk.
9. **Unknowns tighten rather than relax machine-speed controls.** *(Ratified.)* An unresolved
   high-impact path cannot be used to justify de-escalation. Resolution and de-escalation remain
   governed by OQGF-P-8 (AMD-005).
10. **Graph history is append-only.** *(Ratified.)* Corrections supersede prior assertions with
    provenance; they do not erase what was known, assumed, or decided at the time. Consistent
    with the OQGF-A and OQGF-P-10.6 append-only discipline.

---

## AMD.1 Normative requirements

These requirements add OQGF-P-13 to Section A.P. They do not modify OQGF-P-10 (AMD-008),
OQGF-P-12 (AMD-011), or any prior amendment; they govern the causal, temporal, and topological
relationships among the risks those amendments surface.

**OQGF-P-13.1 (Recursive Risk-Propagation Graph of Record).** A conforming system SHALL maintain
a Recursive Risk-Propagation Graph for every identified risk whose materialization, treatment,
transfer, acceptance, or surrounding conditions may plausibly create, expose, attenuate, amplify,
accelerate, or combine with another material risk. Every Risk Node SHALL reference exactly one
authoritative OQGF-P-10 Risk Register entry. The RRPG SHALL be recorded in Organ 5 and SHALL
preserve stable node and edge identifiers, provenance, time, owner, disposition, and status. A
list of risks with no governed relationships does not satisfy this requirement when material
relationships are known or reasonably discoverable.

**OQGF-P-13.2 (Residual Risk Is a Successor Node).** On execution of a Reduce or Transfer
disposition, every material Residual Risk SHALL be created or updated as an independently
addressable successor Risk Node, re-assessed, assigned a named DAP, and re-dispositioned under
OQGF-P-10 (AMD-008). The predecessor SHALL remain in the append-only record. Completion of the
treatment plan SHALL NOT close the propagation path merely because a residual node was recorded;
the residual node is subject to OQGF-P-13.3 through OQGF-P-13.11 in full. This requirement
converts the AMD-008 `Box<RiskEntry>` from a terminal field into a first-class governed
successor.

**OQGF-P-13.3 (Causal Edge Evidence and Boundary Crossing).** Every material Causal Edge SHALL
record: source and destination node identifiers; the asserted mechanism and triggering condition;
the direction of effect (creates, exposes, attenuates, amplifies, accelerates, delays); the
estimated Propagation Latency or range; confidence and uncertainty; supporting and contradicting
evidence; the technical, organizational, agent, market, social, or physical boundary crossed;
and the accountable approver of the assertion. Observed causation, modeled causation, and
hypothesis SHALL be distinguishable epistemic states. Correlation alone SHALL NOT be labeled
causation; where a shared cause is suspected, that uncertainty SHALL be represented explicitly.
An edge MAY be uncertain; uncertainty SHALL be recorded and SHALL NOT be converted into false
certainty.

**OQGF-P-13.4 (Branch, Convergence, and Feedback Governance).** The RRPG SHALL preserve all
material outgoing branches, all material incoming paths to Compound Risk Nodes, and all detected
Feedback Components. A representation that duplicates or discards a shared descendant, selects
only one cause for a compound risk, or silently breaks a cycle does not satisfy this requirement.
Feedback Components SHALL carry a declared amplification or attenuation assessment, a loop bound
where one can be enforced, and a linked OQGF-P-5 response-storm condition when the feedback may
threaten host or ecosystem availability. This requirement links the risk topology to the existing
cascade-bound machinery of AMD-004 (OQGF-P-7.5) and the storm detection of AMD-002 (OQGF-P-5)
without introducing a competing cascade mechanism.

**OQGF-P-13.5 (Traversal and Valid Termination).** Analysis SHALL continue along every material
reachable path until one of the following is evidenced for that path:

1. the risk source is Avoided or the path is Contained, and verification shows no material
   outgoing successor within the declared system scope and operating horizon;
2. a terminal consequence has been reached and all resulting continuing risks are separately
   represented;
3. a risk and its explicitly enumerated propagation scope are Accountably Accepted under
   OQGF-P-9 (AMD-006), with expiry and no implicit acceptance of unenumerated descendants; or
4. analysis cannot defensibly continue, in which case the path SHALL remain open at an
   Unresolved Risk Frontier governed under OQGF-P-13.11.

A Transfer disposition alone is not a termination condition. A Reduce disposition alone is not a
termination condition. A tooling depth limit is not a termination condition. The absence of
evidence for another edge is not evidence of absence unless the search scope, method, and
confidence are recorded and are commensurate with the governing tier.

**OQGF-P-13.6 (Control-Induced and Shifted Risk).** Every material treatment, safeguard,
containment action, recovery action, and governance decision SHALL be assessed for risk that it
creates, displaces, concentrates, delays, or amplifies. A material control-induced risk SHALL be
recorded as an Induced Risk Node and linked both to the controlled node and to the control or
decision that produced it. A control SHALL NOT be credited solely on the reduction it produces at
one node when its downstream effect increases total risk elsewhere beyond tolerance. This is the
iatrogenic-injury principle: the treatment itself is a risk source, and ignoring it is not
honesty.

**OQGF-P-13.7 (Temporal Governance and Intervention Margin).** Every path capable of abrupt,
irreversible, safety-critical, rights-affecting, externally consequential, or systemic effect
SHALL carry a defensible estimate or range for Propagation Latency, Response Budget, Time to
Irreversibility, and Intervention Margin. Where the Intervention Margin is zero, negative, or too
uncertain to establish timely human action, the system SHALL use pre-authorized deterministic
controls external to the model to prevent, rate-limit, isolate, pause, or terminate the relevant
effect. Independent termination SHALL reuse OQGF-P-12.5 (AMD-011) where applicable. Human
approval SHALL NOT be credited as the primary real-time control when the timing record shows a
human cannot reliably intervene before irreversibility. Human oversight remains the accountable
governance authority; this requirement governs whether it is also the *in-time* prevention
authority, and when it is not, positions the innate controls at the amplification nodes where the
cascade moves faster than deliberation.

**OQGF-P-13.8 (Continuous Graph Reconciliation).** The RRPG SHALL be continuously reconciled
against material change. Triggers SHALL include, at minimum: confirmed incidents; treatment
completion or failure; Deterministic-Gate findings; dependency or supply-chain change;
environment change; model or data drift; Capability Envelope change (OQGF-P-12.2); new tool,
credential, network, persistence, identity, or external-effect capability; sub-agent creation
(OQGF-P-12.6); material trajectory deviation (OQGF-P-12.8); cross-organ Signals (OQGF-P-7);
and relevant external intelligence. Reconciliation MAY update only the affected subgraph, but
periodic system-wide review SHALL test for missed cross-boundary, convergence, and feedback
relationships.

**OQGF-P-13.9 (Deterministic Graph Authority).** Neural components MAY propose Risk Nodes,
Causal Edges, assessments, treatments, and evidence links. They SHALL NOT unilaterally authorize
their adoption as the graph of record; delete or close a node; remove or weaken an edge; lower
an assessment; expand a materiality exclusion; resolve an Unresolved Risk Frontier; accept a
risk; or relax a control. Those state changes SHALL pass through a deterministic policy path
external to the model that validates schema, signatures, authorization, required evidence,
temporal bounds, and DAP approval. This preserves the OQGF-P-2 invariant: neural components are
heuristic proposers; the deterministic path is the gate. Deterministic validation certifies that
the governance conditions were met; it SHALL NOT be represented as proof that a causal hypothesis
is true.

**OQGF-P-13.10 (Capability–Intent–Trajectory–Risk Reconciliation).** For systems governed by
OQGF-P-12 (AMD-011), the RRPG SHALL be reconciled against: the declared and attested Capability
Envelope (OQGF-P-12.2, OQGF-P-12.3); the authorized Intent Provenance Chain (OQGF-M-8 through
OQGF-M-14, AMD-001); and the observed Trajectory Record (OQGF-P-12.8). A capability absent from
the graph but present in the deployed environment is a graph-coverage failure. An action outside
authorized intent is an authorization event under AMD-001 whether or not harm occurred. An
observed material effect with no predicted node or edge SHALL create a new Risk Source under
OQGF-P-10.2 (AMD-008), amend the RRPG with provenance, and trigger reassessment of the affected
subgraph. Authorization does not erase consequence; consequence does not retroactively authorize.

**OQGF-P-13.11 (Uncertainty, Frontier Governance, and Non-Deletion).** Every Unresolved Risk
Frontier SHALL record: why analysis stopped; what evidence is missing; what system or
organizational boundary blocks resolution; the plausible consequence range; the named DAP owner;
the governing disposition; the next review trigger; and the controls applied while uncertainty
remains. A high-impact frontier SHALL NOT justify autonomous de-escalation; resolution and
de-escalation remain governed by OQGF-P-8 (AMD-005). Closed, refuted, superseded, or
reclassified nodes and edges SHALL be annotated and retained, never deleted, consistent with
OQGF-A and OQGF-P-10.6. The RRPG SHALL distinguish "not yet observed," "searched and not found,"
"modeled unlikely," and "demonstrated absent within a declared scope"; those states are not
interchangeable.

---

## AMD.2 Conformance criteria per level

**Baseline (OQGF-B):** Each material Risk Register entry has an RRPG node; known material
relationships are represented as evidenced edges; residual risks are independently addressable
successor nodes; treatments are assessed for induced risk; each path is carried to a valid
termination condition or an owned Unresolved Risk Frontier; and graph history is retained in
Organ 5 (OQGF-P-13.1, OQGF-P-13.2, OQGF-P-13.5, OQGF-P-13.6, OQGF-P-13.11). Candidate content
generated by a model is visibly distinguished from the graph of record (OQGF-P-13.9).
Single-PQC-family graph-checkpoint signatures acceptable.

**Enhanced (OQGF-E):** All Baseline criteria, plus event-driven reconciliation from the triggers
in OQGF-P-13.8; explicit branch, convergence, shared-descendant, and feedback analysis
(OQGF-P-13.4); temporal estimates for consequential paths with deterministic containment when
the Intervention Margin is not reliably positive (OQGF-P-13.7); declared and DAP-approved
materiality policy; and Capability–Intent–Trajectory–Risk reconciliation for systems under
OQGF-P-12 (OQGF-P-13.10).

**High-Assurance (OQGF-H):** All Enhanced criteria, plus continuous or near-real-time
affected-subgraph reconciliation commensurate with the fastest material path; independent
verification of graph mutation policy; dual-PQC-family signatures on graph checkpoints per
OQGF-M-2/OQGF-R-1; second-DAP review before closing any catastrophic, systemic, or
safety-critical path; adversarial and fault-injection testing of branching, convergence,
feedback, frontier, and negative-Intervention-Margin cases; and periodic replay that reconciles
the Organ-5 trajectory with the graph of record.

Conformance level changes assurance depth and update cadence, not permission to hide a known
catastrophic path. A Baseline system with a known material path must still represent and
disposition it; the system's Capability-Triggered Tier (OQGF-P-12) may independently raise the
Governing Tier.

---

## AMD.3 Assessment procedures

An auditor SHALL:

1. Select a Reduce disposition and confirm that its Residual Risk has a stable Risk Node ID, an
   authoritative OQGF-P-10 entry, its own assessment and disposition, a causal edge from the
   predecessor, and continued downstream analysis (OQGF-P-13.2, OQGF-P-13.3). **This is the
   load-bearing test of this amendment**: it proves residual risk is a governed successor, not
   an endpoint.
2. Select a Transfer disposition and confirm the transfer did not automatically close the path;
   verify that remaining operational, third-party, contractual, concentration, and systemic risk
   were considered and that material successors are separately dispositioned (OQGF-P-13.5).
3. Introduce a mitigation that lowers one risk but creates another — for example, a rapid
   automated shutdown that protects integrity but threatens availability — and confirm an Induced
   Risk Node is created and linked both to the original node and to the control (OQGF-P-13.6).
4. Construct one branch, one convergence, one shared descendant, and one directed loop, and
   confirm the graph preserves each topology without duplication or silent truncation, and
   confirm the loop is bounded or governed as an OQGF-P-5 response-storm risk (OQGF-P-13.4).
5. Configure the analysis tool to stop at a shallow depth while a plausible material successor
   remains, and confirm it creates an owned Unresolved Risk Frontier rather than marking the
   branch safe or closed (OQGF-P-13.11).
6. Simulate a path whose credible propagation reaches an irreversible external effect before the
   ordinary human Response Budget expires, and confirm a pre-authorized deterministic control
   prevents, rate-limits, isolates, pauses, or terminates the effect without model cooperation
   (OQGF-P-13.7).
7. Ask a model to remove an edge, lower a risk, accept a descendant, and close a frontier, and
   confirm none becomes authoritative without the deterministic policy checks and required DAP
   approval (OQGF-P-13.9).
8. Add a Capability Property, create a sub-agent, or expose a previously undeclared network
   path, and confirm the affected graph is reconciled and that any unexplained capability or
   effect becomes a new OQGF-P-10 Risk Source (OQGF-P-13.10, OQGF-P-13.8).
9. Replay a sampled OQGF-P-12.8 Trajectory Record and verify that material tool calls,
   credential uses, network connections, state transitions, sub-agent actions, and external
   effects map to predicted nodes and edges or create traceable amendments (OQGF-P-13.10).
10. Attempt to delete a refuted or closed node or edge and confirm it is superseded with
    provenance and retained in Organ 5 rather than erased (OQGF-P-13.11).

---

## AMD.4 Control mappings

- **NIST AI RMF 1.0 / NIST AI 600-1:** GOVERN-1 and GOVERN-4 (accountable risk policy);
  MAP-1, MAP-2, MAP-3, MAP-5 (context, dependencies, actors, impacts — this amendment adds
  propagation topology as a MAP input); MEASURE-2.6 (residual negative risk, safe failure,
  real-time monitoring, and response time — directly mapped to OQGF-P-13.7); MANAGE-1, MANAGE-2,
  MANAGE-4 (prioritization, treatment, monitoring, and incident learning).
- **NIST SP 800-53 Rev. 5:** RA-3 (risk assessment — extended to graph topology), RA-7 (risk
  response — the four dispositions, now with propagation governance), PM-9 and PM-28 (risk
  management strategy and framing), CA-7 (continuous monitoring — graph reconciliation), SI-4
  (system monitoring), IR-4 and IR-5 (incident handling and monitoring), CP-2 (contingency
  planning — temporal governance), SA-8 (security and privacy engineering principles —
  deterministic graph authority), AU-2, AU-3, AU-12 (audit event content and generation —
  trajectory-graph reconciliation).
- **NIST SP 800-37 and SP 800-30:** the identify–assess–respond–monitor cycle and the likelihood,
  impact, uncertainty, and risk-response foundation already used by AMD-008. This amendment adds
  recursive topology and temporal machine-speed controls to the OQGF expression of that cycle.
- **NIST SP 800-221:** informative support for enterprise roll-up, interconnected risk, emergent
  effects, and risk created by responses. Cited as lineage, not as a mandate for the RRPG.
- **NIST SP 800-231:** informative support for causal chains, convergence, and chaining in its
  cybersecurity scope. This amendment generalizes the topology to risk governance.
- **ISO/IEC 42001:** Clause 6 (AI risk assessment and treatment), Clause 8 (operational control),
  Clause 9 (performance evaluation), Annex A.5 and A.6. **ISO 31000 / ISO/IEC 27005 lineage:**
  the continual risk cycle with recursive topology and temporal controls added.
- **CNSA 2.0:** dual-PQC-family signatures on graph checkpoints at High-Assurance per
  OQGF-M-2/OQGF-R-1; all graph-mutation authorization signatures under the existing
  tier-appropriate PQC requirements.
- **Factual basis (established findings, cited as lineage):**
  - Knight Capital (SEC, 16 October 2013): >$460M loss in ~45 minutes from automated order
    propagation — establishes that consequential propagation can exhaust human intervention time.
  - Flash Crash (joint CFTC–SEC, 30 September 2010): rapid interaction among automated execution
    and market liquidity — establishes convergence and feedback in automated systems.
  - NIST AI 600-1 (July 2024): multi-scope risk, correlated-failure exposure from algorithmic
    monocultures, abrupt time scales — supports temporal and correlation-aware governance.
  - International AI Safety Report 2026 (February 2026): autonomous agents reduce human
    intervention opportunities; multi-agent interactions introduce propagation and amplification.
  - These are cited as the evidentiary basis for the amendment's temporal-governance and
    propagation requirements, not as mandates for the RRPG structure.

---

## AMD.5 Technical architecture (implementation hooks)

The RRPG is a relationship layer over `oqgf-core::RiskEntry` (AMD-008), persisted in
`oqgf-memory` (Organ 5). It does not duplicate the Risk Register, the Capability Envelope, the
Intent Provenance Chain, or the Trajectory Record. Node references preserve the Risk Register as
the source of truth; edge and frontier events supply topology and evidence.

### AMD.5.1 Core types

```rust
use std::collections::{BTreeMap, BTreeSet};
use std::time::SystemTime;

/// Relationship layer over the AMD-008 Risk Register (OQGF-P-13.1).
/// Mutations are event-sourced and append-only in Organ 5.
pub struct RecursiveRiskPropagationGraph {
    pub id: GraphId,
    pub roots: BTreeSet<RiskId>,               // viewpoint-selected starting nodes
    pub nodes: BTreeMap<RiskId, RiskNode>,      // each references one RiskEntry
    pub edges: BTreeMap<EdgeId, CausalEdge>,    // directed, attributed, temporal
    pub frontier: BTreeMap<FrontierId, FrontierRecord>,
    pub governing_tier: ConformanceLevel,       // inherits from system (P-12.1)
    pub checkpoint: GraphCheckpoint,            // signed, append-only
}

/// One governed risk state (OQGF-P-13.1). Refers to, never duplicates, an
/// AMD-008 RiskEntry. The RiskEntry is the record; the RiskNode is the
/// graph position.
pub struct RiskNode {
    pub risk_ref: RiskId,                       // authoritative AMD-008 entry
    pub kind: RiskNodeKind,
    pub status: NodeStatus,                     // Active | Closed | Superseded
    pub owner: DesignatedAccountableParty,      // reuses existing type (OQGF-A-5)
    pub last_assessed_at: SystemTime,
    pub evidence: Vec<EvidenceRef>,
}

/// The structural kind of a node in the graph. Each variant carries the
/// provenance that distinguishes it (OQGF-P-13.2, P-13.6, P-13.4).
pub enum RiskNodeKind {
    Root,
    Residual   { treatment_ref: TreatmentRef },   // P-13.2 successor
    Induced    { control_ref: ControlRef },        // P-13.6 iatrogenic
    Propagated { boundary: BoundaryRef },          // cross-boundary downstream
    Compound   { predecessors: BTreeSet<RiskId> }, // P-13.4 convergence
    Systemic   { scope: SystemicScope },           // beyond originating component
}

/// A directed, evidenced relationship between two Risk Nodes (OQGF-P-13.3).
/// Multiple edges may connect the same pair through different mechanisms
/// (multigraph property).
pub struct CausalEdge {
    pub id: EdgeId,
    pub from: RiskId,
    pub to: RiskId,
    pub mechanism: CausalMechanism,
    pub condition: TriggerCondition,
    pub effect: PropagationEffect,              // Creates | Exposes | Attenuates | ...
    pub latency: EstimateRange,                 // Propagation Latency (P-13.7)
    pub confidence: ConfidenceAssessment,
    pub epistemic_state: EpistemicState,         // Observed | Modeled | Hypothesized | Refuted
    pub boundary_crossed: Option<BoundaryRef>,
    pub supporting_evidence: Vec<EvidenceRef>,
    pub contradicting_evidence: Vec<EvidenceRef>,
    pub approved_by: DesignatedAccountableParty, // DAP-accountable assertion
}

pub enum PropagationEffect {
    Creates, Exposes, Attenuates, Amplifies, Accelerates, Delays, Unknown,
}

pub enum EpistemicState {
    Observed,
    ExperimentallySupported,
    Modeled,
    Hypothesized,
    Refuted { superseding_evidence: EvidenceRef },
}

/// Temporal governance for a consequential path (OQGF-P-13.7).
/// A negative or uncertain margin requires pre-authorized deterministic controls.
pub struct TemporalEnvelope {
    pub propagation_latency: EstimateRange,
    pub detection_time: EstimateRange,
    pub decision_time: EstimateRange,
    pub control_activation_time: EstimateRange,
    pub time_to_irreversibility: EstimateRange,
}

impl TemporalEnvelope {
    /// Conservative margin: slow response, fast harm.
    pub fn conservative_intervention_margin(&self) -> DurationRange {
        self.time_to_irreversibility
            - (self.detection_time + self.decision_time + self.control_activation_time)
    }
}

/// Where analysis stopped without a valid termination condition (OQGF-P-13.11).
/// An open risk condition, not evidence of safety.
pub struct FrontierRecord {
    pub id: FrontierId,
    pub at_node: RiskId,
    pub reason: FrontierReason,
    pub missing_evidence: Vec<EvidenceNeed>,
    pub plausible_consequence: ImpactRange,
    pub owner: DesignatedAccountableParty,
    pub disposition_ref: DispositionRef,
    pub next_review: ReviewTrigger,
    pub interim_controls: Vec<ControlRef>,
}

pub enum FrontierReason {
    UnknownBehavior, MissingEvidence, OrganizationalBoundary,
    ToolingLimit, DeclaredCutoff, ModelLimit,
}

/// A neural component can submit this candidate. It cannot mutate the graph
/// (OQGF-P-13.9). The deterministic path validates and authorizes.
pub struct GraphMutationProposal {
    pub proposed_by: ActorRef,
    pub mutation: ProposedMutation,
    pub evidence: Vec<EvidenceRef>,
    pub created_at: SystemTime,
}

/// Deterministic policy path for graph state changes (OQGF-P-13.9).
/// Validates schema, signatures, authorization, evidence, temporal bounds,
/// and DAP approval. Does not certify causal truth — certifies that the
/// governance conditions were met.
pub trait GraphAuthority: Send + Sync {
    fn evaluate(
        &self,
        proposal: &GraphMutationProposal,
        policy: &GraphMutationPolicy,
    ) -> Result<AuthorizedGraphEvent, GraphPolicyError>;
}
```

The safety properties are structural. `GraphAuthority::evaluate` is the only path from proposal
to graph-of-record; there is no method that bypasses it. `EpistemicState` distinguishes observed
from hypothesized; there is no variant that permits false certainty. `FrontierRecord` is a
first-class type, not a boolean; an unresolved frontier cannot be silently hidden by setting a
flag. `TemporalEnvelope::conservative_intervention_margin` uses the slow end of response and the
fast end of harm, so the fail-safe direction is to trigger deterministic controls, not to
optimistically assume human-speed intervention will suffice.

### AMD.5.2 What this closes, and what it does not

This amendment **closes** the following:

- **Residual-as-endpoint ambiguity.** Residual risk is explicitly a governed successor node, not
  a terminal field (OQGF-P-13.2).
- **Tree-only lineage.** Branches, shared descendants, convergence, and feedback become normative
  (OQGF-P-13.4). The linked-list `Box<RiskEntry>` is valid for simple cases; the graph handles
  the rest.
- **Mitigation tunnel vision.** Control-induced and shifted risk must be assessed; a control is
  not credited solely on its beneficial effect at one node when it increases risk elsewhere
  (OQGF-P-13.6).
- **Depth-cap concealment.** Unresolved reachability becomes a visible frontier rather than an
  implied clean bill of health (OQGF-P-13.11).
- **Human-speed fiction.** Timing evidence determines whether human intervention can count as a
  real-time control, and positions pre-authorized deterministic controls where it cannot
  (OQGF-P-13.7).
- **Model self-governance.** A model can propose graph content but cannot authorize its own
  closure, acceptance, or control relaxation (OQGF-P-13.9).
- **Disconnected governance records.** Capability, intent, trajectory, register, and consequence
  are reconciled through stable references (OQGF-P-13.10).

This amendment **does not** fully close, and states so honestly:

- **Unknown unknowns remain.** No graph can include a risk for which there is no observation,
  hypothesis, signal, or evidence. Continuous reconciliation expands coverage; it does not prove
  completeness. This is the same residual shape as AMD-008's (OQGF-P-10) and AMD-011's
  (OQGF-P-12.2): the inventory covers what is known and declared; it cannot cover what was never
  seen.
- **Causal inference can be wrong.** A signed edge proves attribution and process, not causation.
  Competing evidence and epistemic state remain visible so the graph can be corrected without
  rewriting history. This is the same shape as AMD-010's trainability-profile residual: a
  declared model is only as good as its declaration.
- **Estimates can create false precision.** Latency, likelihood, impact, and irreversibility may
  be ranges or qualitative bands. Unsupported point estimates are discouraged; uncertainty is a
  governed fact, not a formatting defect.
- **Graph scale can be adversarial.** A system may create more candidate relationships than can
  be examined in real time. Materiality, prioritization, rate limits, and affected-subgraph
  analysis bound resource use; unexamined material paths remain frontier risk.
- **Controls can conflict.** A deterministic halt may protect integrity while harming availability
  or safety. OQGF-P-13.6 requires that induced risk be modeled; it cannot guarantee one control
  satisfies every objective.
- **Organizational boundaries obstruct evidence.** Third parties may not disclose enough data to
  resolve a path. Transfer contracts and assurance evidence can reduce uncertainty, but the
  frontier remains named while evidence is absent.
- **Human governance remains necessary.** Materiality, evidence quality, causal judgment, and
  acceptance require accountable people. Determinism enforces the decision path; it does not
  replace judgment. This is the standing residual of every amendment in the set.

---

## AMD.6 Traceability

| Requirement | Implementation hook | Existing OQGF dependency |
| --- | --- | --- |
| OQGF-P-13.1 | `RecursiveRiskPropagationGraph`, stable `RiskId`/`EdgeId`, Organ-5 event store | P-10.1, P-10.6, A-1 |
| OQGF-P-13.2 | `RiskNodeKind::Residual`, edge from predecessor, independent `RiskEntry` | P-10.5 |
| OQGF-P-13.3 | `CausalEdge`, `EpistemicState`, evidence references, boundary metadata | P-10.1, A-1 |
| OQGF-P-13.4 | branch/convergence in `BTreeMap`; loop/SCC detection; storm linkage | P-5, P-7.5 |
| OQGF-P-13.5 | path traversal, termination validator, `FrontierRecord` | P-8, P-9, P-10.3–P-10.6 |
| OQGF-P-13.6 | `RiskNodeKind::Induced`, control-to-risk lineage | P-10.2, P-10.5 |
| OQGF-P-13.7 | `TemporalEnvelope`, intervention-margin policy, independent control path | I-6, P-12.4, P-12.5 |
| OQGF-P-13.8 | change-trigger adapters and affected-subgraph reconciliation | P-7, P-10.2, P-12.2–P-12.8 |
| OQGF-P-13.9 | `GraphMutationProposal`, deterministic `GraphAuthority` trait | P-2, P-9, A-5 |
| OQGF-P-13.10 | references to `CapabilityEnvelope`, `IntentProvenanceChain`, `TrajectoryRecord` | M-8–M-14, P-12.2, P-12.6, P-12.8 |
| OQGF-P-13.11 | `FrontierRecord`, epistemic state, supersession events, checkpoint integrity | P-8, P-10.6, A-1 |

---

## AMD.7 Change log

v1.0 — Initial public draft, 14 August 2026. Adds OQGF-P-13 (Recursive Risk-Propagation) to the
Physiology Layer: converts AMD-008's nested residual-risk field from a terminal value into a
governed successor node in a directed, attributed, temporal multigraph — the Recursive
Risk-Propagation Graph — that preserves branching, convergence, shared descendants, and feedback
when they exist in the risk topology. Requires every material causal relationship to be evidenced,
boundary-aware, and epistemically classified (observed, modeled, hypothesized, or refuted).
Requires every material treatment, safeguard, and governance decision to be assessed for
control-induced risk — the iatrogenic-injury principle. Requires every propagation path to be
carried to a valid termination condition (avoided, terminal, accountably accepted with enumerated
scope, or explicitly open at an Unresolved Risk Frontier); Transfer and Reduce alone do not
terminate.

Introduces temporal governance: every consequential path carries defensible timing estimates
(Propagation Latency, Response Budget, Time to Irreversibility, Intervention Margin); where the
Intervention Margin is zero, negative, or materially uncertain, pre-authorized deterministic
controls external to the model are required, because human oversight is the accountable
governance authority but not necessarily the in-time prevention authority — the complement
regulators positioned at the amplification nodes where the cascade moves faster than
deliberation. Establishes deterministic graph authority: neural components may propose graph
content (nodes, edges, assessments, treatments, evidence) but may not unilaterally authorize
adoption, closure, severity reduction, edge removal, acceptance, or frontier resolution — those
state changes pass through a deterministic policy path preserving the OQGF-P-2 invariant. For
systems governed by OQGF-P-12 (AMD-011), reconciles the graph against the declared Capability
Envelope, the authorized Intent Provenance Chain, and the observed Trajectory Record — linking
capability, intent, action, and consequence through one auditable structure.

Governs the graph as append-only, cycle-aware, materiality-bounded, and continuously reconciled,
with graph history annotated and retained (never deleted) consistent with the OQGF-A and
OQGF-P-10.6 append-only discipline. Does not modify AMD-008 (which remains the authoritative
Risk Register), AMD-011 (which remains the capability, containment, and trajectory mechanism), or
any prior amendment; every node refers to exactly one authoritative `RiskEntry`, and the graph
supplies lineage, topology, time, and evidence over the existing record. Seven residuals are
named rather than claimed eliminated — unknown unknowns, causal-inference error, estimation false
precision, adversarial graph scale, conflicting controls, organizational-boundary obstruction,
and the necessity of human governance — each mapped to the shape of a prior amendment's residual.

— End of OQGF Amendment 012.
