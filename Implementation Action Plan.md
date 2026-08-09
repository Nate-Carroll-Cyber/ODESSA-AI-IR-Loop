# ODESSA — Implementation Action Plan
Companion to the ODESSA specification. Each bullet is an action; stage references point back to the full spec for requirements language, mappings, and rationale. Sequence: Prepare → Build → Operate → Respond.

---

## Phase 1 — Prepare (Stage 0, pre-deployment)

**Governance**
- [ ] Name agentic autonomy as a formal risk in enterprise risk management and compliance programs.
- [ ] Issue an interim agentic-security standard: accountable owners, pre-authorized shutdown authority, spending limits, restricted tool scopes.
- [ ] Document the information security incident management plan.
- [ ] Define incident declaration criteria (thresholds that elevate a runtime event to a declared incident).
- [ ] Prioritize security-automation investment by risk reduction and automation ROI; treat automation as a continuum, not a binary.
- [ ] Evaluate multiple model classes (frontier and open-weight) for defensive-tooling fit; re-evaluate selections as the threat landscape shifts.

**Provisioning**
- [ ] Size the STEP_UP rate budget to actual reviewer capacity.
- [ ] Define autonomy-tier criteria and promotion requirements.
- [ ] Assign kill-switch authorization roles (per-agent, per-cluster, global scopes).
- [ ] Establish the authenticated change-management path for the policy store.

**Response readiness**
- [ ] Stand up two response postures: firm-as-victim and firm's-agent-as-attacker.
- [ ] Pre-provision and test incident tooling, including AI-assisted telemetry correlation; validate fallback tooling availability under incident conditions.
- [ ] Open internal reporting pathways for personnel and an external intake channel for third-party adverse-impact reports.
- [ ] Run agentic-AI tabletop exercises: autonomous attack, persistent malicious agent, tooling unavailability during forensics.

**Gate:** no production deployment without a tested external intake channel and exercised plan.

---

## Phase 2 — Build (Stages 1, 4, 5 substrate)

**Identity & provenance (Stage 1)**
- [ ] Issue every agent a unique, immutable identifier with cryptographic credential binding.
- [ ] Record ownership chains from every sub-agent back to the Agent Owner.
- [ ] Log machine-readable capability declarations before execution; treat declared scope as the least-privilege ceiling.
- [ ] Implement structured, machine-parseable action logging tied to agent identity, session, and parent agent.

**Intent anchoring (Stage 1)**
- [ ] Capture the original user request at session start; store it immutably in the control plane, out-of-band from agent context.
- [ ] Re-supply clean intent to the evaluator on every action; inject it into every sub-agent payload.
- [ ] Build the out-of-band re-attestation path for legitimate mid-session goal changes; route in-context goal changes to STEP_UP.

**Validation (Stage 4)**
- [ ] Treat all input as untrusted: tool outputs, documents, inter-agent messages, memory.
- [ ] Normalize, sanitize, and mask sensitive patterns before downstream models see input.
- [ ] Validate every dynamically generated subtask before it touches external data or tools.
- [ ] Verify provenance of tools and MCP servers before runtime binding.

**Enforcement (Stage 5)**
- [ ] Deploy guardrails out-of-process: gateway at the tool/inter-agent egress boundary, sidecar/proxy at the inference boundary.
- [ ] Enforce least privilege at credential issuance; flag over-scoped credentials as findings pre-abuse.
- [ ] Enforce permission narrowing on every delegation hop; terminate orphaned sub-agents.
- [ ] Apply compositional (taint/egress) limits session-wide across all agents serving the same intent.
- [ ] Implement kill-switch and circuit-breaker states with authenticated, receipted, scoped invocation.
- [ ] Mandate HITL checkpoints for sensitive transactions, communications, and system changes.
- [ ] Enforce strict network and system segmentation so a compromised agent cannot move laterally, exploit misconfigured service accounts, or harvest cluster-wide vault credentials.

**Protecting the protector**
- [ ] Make receipts and decision records append-only and tamper-evident (hash-chained or WORM).
- [ ] Lock the policy store behind the authenticated change-management path; receipt every policy change.
- [ ] Access-control the decoy inventory in the control plane.

---

## Phase 3 — Operate (Stages 2, 3, 6 runtime loop)

**Detection (Stage 2)**
- [ ] Establish behavioral baselines, including per-platform agentic cadence (loop rhythm, tool-call intervals, burst patterns).
- [ ] Deploy prompt-chain and trajectory-level observability across agents serving the same intent.
- [ ] Express compositional policy as deterministic taint rules enforceable at Stage 5.
- [ ] Deploy deception assets stack-wide: canary credentials, fake identities, decoy registries, honey datasets/APIs/clusters — indistinguishable from production.
- [ ] Route any decoy interaction directly to containment (decoy contact = ≥ L3, no downgrade).
- [ ] Maintain the decoy inventory to separate real impact from fabricated artifacts.
- [ ] Tag agent-generated noise at capture time to prevent forensic volume inflation.

**Triage (Stage 3)**
- [ ] Map detection summaries to L0–L3; escalate at ≥ L2.
- [ ] Enforce the STEP_UP budget; fail secure (deny/pause) when exceeded — never silently downgrade to allow.
- [ ] Run drift detection scope-primary (authorization-scope check), distance-secondary (cached intent embedding); never distance-only.
- [ ] Operate tiered autonomy: intern tier (read/summarize/draft-with-approval) until trust is earned.

**Assessment (Stage 6)**
- [ ] Log sanitized input, signals, risk level, action, outcome for every interception.
- [ ] Retain explainable rationale for every autonomous decision.
- [ ] Feed approved records to curated training sets; quarantine incident-window records until cleared.
- [ ] Continuously evaluate receipts against declaration criteria — declaration is automated, never dependent on human noticing.
- [ ] Run promotion gates on auditable behavior; track against the maturity model.
- [ ] Benchmark against AARM metrics (detection rate, FP rate, step-up calibration, escalation volume, receipt completeness, latency) — benchmark, don't just conformance-check.

**Continuous adversarial validation**
- [ ] Run continuous, autonomous red teaming against your own infrastructure — chain-and-discover, not just scripted scenario replay — and remediate what it finds before external actors do.
- [ ] Feed red-team findings back into Stage 2 detection signals and Stage 0 declaration criteria.
- [ ] Close the detect-to-remediate loop: on a discovered vulnerability, auto-propose a patch and deploy through a pipeline with automated rollback on availability impact — manual-only patching inundates engineers and negates automated discovery.
- [ ] Scope automated patch deployment as a pre-authorized, bounded, reversible action class with its own receipts — this is the sanctioned exception to the Stage 5 HITL-on-system-changes rule, not a contradiction of it; anything outside the bounded class still routes to HITL.

---

## Phase 4 — Respond (Downstream Workflow, post-declaration)

- [ ] Freeze and hash-verify original logs; analyze verified copies only.
- [ ] Execute the stakeholder communication plan.
- [ ] Eradicate: purge poisoned memory/knowledge stores, revoke incident-window credentials, quarantine incident-window training records.
- [ ] Validate magnitude environment-wide across non-agent systems.
- [ ] Conduct after-action review; feed lessons to Stage 0 (criteria/policy) and Stage 6 (learning).
- [ ] Treat any manual global kill-switch activation as a declarable event.
- [ ] Deploy defensive agents to parse, correlate, and triage incident-window telemetry at machine scale, so human responders can match the tempo of concurrent multi-agent attacks rather than drowning in forensically dense log volume.

---

## Standing constraints (never)

- Never deploy without external adverse-impact intake.
- Never let the agent hold the only copy of the intent anchor.
- Never accept goal changes through the agent's context as a new anchor.
- Never use semantic distance as the sole drift signal.
- Never silently downgrade an over-budget escalation stream to allow.
- Never let a sub-agent exceed its parent's permissions.
- Never bind to unverified tools, plugins, or MCP servers.
- Never alter original audit logs after forensic flagging.
- Never treat a passed evaluator check as proof of safety — assume a non-zero evade rate.
