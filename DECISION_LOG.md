# AI Access Privacy Decision Log

**Status:** Foundational Draft — Proposed for Ratification  
**Version:** 0.1.0  
**Canonical Repository:** `Sohadot/AIAccessPrivacy`  
**Governance Authority:** Repository Owner  
**Record Model:** Append-only, owner-ratified, evidence-linked

---

## 1. Purpose

This document is the official governance memory of AI Access Privacy.

It is **not** a changelog and **not** a task list.

A changelog records what changed in files. This log records **why** a decision was made, **who** had the authority to make it, and **under what conditions** it may be reviewed or reversed.

Its function is to preserve, for every material decision:

- the decision that was taken;
- the authority who took it;
- the date of the decision;
- its status;
- the context and problem;
- the alternatives that were considered;
- the rationale;
- the constraints and consequences;
- the evidence or related artifacts;
- the review or revocation conditions;
- which decisions it amends or supersedes.

The official state of the project must be reconstructable from this log together with the Git history. If the two ever disagree, that disagreement is itself a matter to be recorded and resolved here, not hidden.

---

## 2. Record Rules

These rules are normative for this log.

1. **Append-only.** Prior decisions are never deleted and never re-edited to conceal history. New entries are added; old entries remain.

   The append-only requirement applies to accepted decision entries after this log enters `main`. Draft review changes made before the first merge may revise the proposed structure and entries, provided the PR history remains available. After entry into `main`, corrections to accepted decisions must proceed forward through amendments or later decisions.

2. **Errors are corrected forward.** A mistake is corrected by a later decision or an Amendment that links back to the original record. The original record is not rewritten.

3. **Permitted statuses.** Every decision carries exactly one of:
   - `Proposed`
   - `Accepted`
   - `Deferred`
   - `Rejected`
   - `Superseded`
   - `Revoked`

4. **Acceptance is explicit and owner-only.** A decision becomes `Accepted` only by an explicit decision of the Repository Owner. No other actor, process, or automation can confer `Accepted` status.

5. **Merge is not acceptance.** Merging a file or a pull request does not, by itself, accept a decision unless that acceptance is stated explicitly. Merging this log makes it a working governance record; it does not accept any `Proposed` decision within it.

6. **Required fields.** Every material decision must include:
   - Decision ID
   - Title
   - Date
   - Status
   - Authority
   - Context
   - Decision
   - Rationale
   - Alternatives considered
   - Consequences
   - Evidence / related artifacts
   - Review triggers
   - Supersedes / superseded by

7. **No retroactive authority.** A decision is not granted authority merely because it was recorded. Recording establishes provenance, not ratification.

8. **Uncertainty stays visible.** Open questions, disputes, and unresolved disagreements are recorded rather than smoothed over. A decision may be `Accepted` while still naming what remains unsettled.

### 2.1 On recorded vs. new decisions

This log distinguishes two different acts:

- **Recording a prior decision** — entering, with provenance, a decision the Repository Owner has already made outside this log. The record documents an existing fact; it does not create new authority.
- **Issuing a new decision** — proposing something not yet decided. Such an entry begins as `Proposed` and becomes `Accepted` only by a later explicit owner decision under Rule 4.

An entry must make clear which of the two it is. Recorded prior decisions state the date and authority of the original act; newly proposed decisions remain `Proposed` until separately accepted.

---

## 3. Status Definitions

- **Proposed** — put forward for consideration; not yet accepted; confers no authority.
- **Accepted** — explicitly adopted by the Repository Owner; in force until superseded or revoked.
- **Deferred** — consideration postponed; no decision in force.
- **Rejected** — considered and declined; retained for the record.
- **Superseded** — replaced by a later accepted decision, which is named in the entry.
- **Revoked** — withdrawn by a later explicit decision; the withdrawing decision is named.

---

## 4. Decisions

> `DEC-001`–`DEC-005`, marked `Accepted`, **record prior explicit decisions of the Repository Owner** (see §2.1). `DEC-000` is a **new** governance decision; it was issued as `Proposed` and then explicitly accepted by the Repository Owner during the review of PR #2 — its acceptance was not conferred by merge or by AI review.

---

### DEC-000 — Decision Governance and Append-Only Record

- **Decision ID:** DEC-000
- **Title:** Decision Governance and Append-Only Record
- **Date:** 2026-07-28
- **Status:** Accepted
- **Authority:** Repository Owner
- **Decision date:** 2026-07-28

**Context**

The project has begun making foundational governance decisions but has had no durable, rule-bound mechanism to preserve them. Without a governance memory, declared governance has no record of how it came to be, and the project's official state cannot be reconstructed or audited.

**Decision**

Establish this log as the governance memory of the project, governed by the Record Rules in §2, and specifically resolve that:

- the Repository Owner is the final ratifying authority;
- AI review is advisory only and confers no ratification or acceptance;
- accepted decisions are never erased;
- amendment or revocation is done by a new decision, not by editing the past;
- the official state of the project must be reconstructable from this decision log together with the Git history.

**Rationale**

Governance that is declared but not remembered is unaccountable. An append-only, owner-ratified record separates the authority to decide from the act of recording, and prevents implicit or retroactive ratification.

**Alternatives considered**

- *No formal log (rely on Git history and PR discussion).* Rejected: history of files is not a record of reasoning, authority, or status.
- *A changelog or task list.* Rejected: neither preserves rationale, authority, alternatives, or review conditions.
- *An editable living document.* Rejected: editing to "clean up" the past destroys the audit trail this record exists to protect.

**Consequences**

- All future material decisions are recorded here under the required fields.
- Acceptance requires an explicit owner act; nothing is accepted by merge alone.
- The project gains an auditable, reconstructable governance state.

**Evidence / related artifacts**

- This file (`DECISION_LOG.md`).
- `CATEGORY_DEVELOPMENT_MODEL.md` §10 (Amendment and Ratification), which requires this log for ratification.

**Review triggers**

- Any change to the Governance Authority.
- Any proposal to alter the append-only or acceptance rules.

**Supersedes / superseded by**

- Supersedes: none.
- Superseded by: none.

> DEC-000 was explicitly accepted by the Repository Owner during the review of PR #2. Its acceptance was not conferred by merge, automation, or AI review.

---

### DEC-001 — Canonical Source and Publication Architecture

- **Decision ID:** DEC-001
- **Title:** Canonical Source and Publication Architecture
- **Date:** 2026-07-28
- **Status:** Accepted
- **Authority:** Repository Owner
- **Decision date:** 2026-07-28

**Context**

The project needs an unambiguous source of legal truth and a durable publication posture, so that authority does not depend on any closed, mutable platform.

**Decision (recorded prior owner decision)**

- GitHub is the legal source of truth.
- IPFS is the content-addressed publication layer for appropriate released versions. Release persistence requires maintained pinning and must not be assumed solely from the existence of a CID.
- `aiaccess.privacy` is the official decentralized identity.
- No closed website builder is a legal source for any foundational artifact.

**Rationale**

Reference authority requires a source that is traceable, versioned, and not controllable by a third-party vendor. Separating the versioned source of truth, content-addressed publication, and decentralized identity keeps their functions independently reviewable.

**Alternatives considered**

- *A hosted website builder as the primary source.* Rejected: closed, mutable, not independently verifiable.
- *A single platform for source, publication, and identity.* Rejected: couples functions that should be independently auditable.

**Consequences**

- Foundational artifacts must live in the repository, not in a closed builder.
- Released versions may be pinned to IPFS; content is immutable under its CID, but continued availability depends on maintained pinning.

**Constraints (explicit scope limit)**

- This decision does **not** yet mandate the final technical publication method.
- It does **not** establish or confirm custom records or unverified subdomains.

**Evidence / related artifacts**

- `CATEGORY_DEVELOPMENT_MODEL.md` header (`Canonical Repository`, `Primary Asset`).

**Review triggers**

- Any proposal to treat a non-repository source as canonical.
- Selection of a final publication method.

**Supersedes / superseded by**

- Supersedes: none.
- Superseded by: none.

---

### DEC-002 — Permanent Sovereign Operating Asset

- **Decision ID:** DEC-002
- **Title:** Permanent Sovereign Operating Asset
- **Date:** 2026-07-28
- **Status:** Accepted
- **Authority:** Repository Owner
- **Decision date:** 2026-07-28

**Context**

The project's posture toward its primary asset must be settled so that development, quality, and governance expectations follow from it.

**Decision (recorded prior owner decision)**

- `aiaccess.privacy` is a permanent sovereign operating asset, not an asset built for sale.
- Value is maximized through reference authority, operational infrastructure, historical data, trust, adoption, and recurring revenue.
- Not being for sale does not relax requirements of quality, transparency, or governance.

**Rationale**

An operating asset held for long-term reference authority is governed differently from an asset built to be sold. Fixing this posture prevents short-term product or exit pressures from eroding neutrality and evidence standards.

**Alternatives considered**

- *Build-to-sell posture.* Rejected: would subordinate reference integrity to exit value.
- *Leave posture unstated.* Rejected: leaves quality and governance expectations undefined.

**Consequences**

- Quality, transparency, and governance obligations apply regardless of commercial interest.
- Revenue is a means to sustain independence, not an exit objective.

**Evidence / related artifacts**

- `CATEGORY_DEVELOPMENT_MODEL.md` header (`Asset Posture`) and §2 (Governing Objective).

**Review triggers**

- Any proposal that would treat the asset as for sale or relax governance for commercial reasons.

**Supersedes / superseded by**

- Supersedes: none.
- Superseded by: none.

---

### DEC-003 — Category Before Product; Operationalizability Required

- **Decision ID:** DEC-003
- **Title:** Category Before Product; Operationalizability Required
- **Date:** 2026-07-28
- **Status:** Accepted
- **Authority:** Repository Owner
- **Decision date:** 2026-07-28

**Context**

The order of development must be fixed so that no product retroactively defines the category, and so that conceptual work is disciplined by operational and commercial reality.

**Decision (recorded prior owner decision)**

- The category is defined before the product.
- Ontology precedes standardization.
- The category is not complete until it is operationalizable and can become a product.
- Every foundational artifact must achieve:
  - conceptual correctness;
  - operational applicability;
  - commercial viability without compromising reference integrity.

**Rationale**

Defining the category first protects it from being narrowed to whatever a single product happens to do. Requiring operationalizability prevents concepts that cannot be applied from being presented as mature primitives.

**Alternatives considered**

- *Product-first development.* Rejected: would let a product define the category retroactively.
- *Pure conceptual work without an operationalizability test.* Rejected: risks unusable abstractions.

**Consequences**

- Foundational artifacts are held to the three-part test above.
- Standardization work waits on sufficient ontological understanding.

**Evidence / related artifacts**

- `CATEGORY_DEVELOPMENT_MODEL.md` §3.1–§3.3 and the Layer 0 completion gate.

**Review triggers**

- Any proposal to standardize an object not yet ontologically defined.
- Any artifact that fails the three-part test.

**Supersedes / superseded by**

- Supersedes: none.
- Superseded by: none.

---

### DEC-004 — Governed Isolation of Exploratory Work

- **Decision ID:** DEC-004
- **Title:** Governed Isolation of Exploratory Work
- **Date:** 2026-07-28
- **Status:** Accepted
- **Authority:** Repository Owner
- **Decision date:** 2026-07-28

**Context**

Experiments on future-layer capabilities are useful before those layers are formally entered, but they must not be mistaken for delivered capability, maturity, or conformance.

**Decision (recorded prior owner decision)**

- Experiments on future layers may be built before those layers are formally entered.
- Such experiments must be non-normative, isolated, and clearly labeled.
- They are never counted as layer progress, conformance, or standard.
- `EXP-001` is preserved as an exploratory research record and is not merged as a foundation before Layer 0 is complete and it has been re-reviewed.

**Rationale**

Isolating exploratory work preserves the integrity of the layer model while still allowing early learning. Labeling and non-normativity prevent prototypes from being cited as evidence of maturity.

**Alternatives considered**

- *Forbid all forward experimentation.* Rejected: discards useful early learning.
- *Allow experiments to count toward layer progress.* Rejected: would let prototypes masquerade as delivered capability.

**Consequences**

- Exploratory branches remain isolated and clearly marked.
- `EXP-001` stays frozen as a research record pending Layer 0 completion and re-review.

**Evidence / related artifacts**

- `CATEGORY_DEVELOPMENT_MODEL.md` §6.2 (Exploratory prototypes).
- Exploratory branch `EXP-001`.

**Review triggers**

- Any proposal to merge exploratory work as foundational.
- Completion of Layer 0 (triggers re-review of `EXP-001`).

**Supersedes / superseded by**

- Supersedes: none.
- Superseded by: none.

---

### DEC-005 — Category Development Model Working-Draft Status

- **Decision ID:** DEC-005
- **Title:** Category Development Model Working-Draft Status
- **Date:** 2026-07-28
- **Status:** Accepted
- **Authority:** Repository Owner
- **Decision date:** 2026-07-28

**Context**

`CATEGORY_DEVELOPMENT_MODEL.md` v0.2.0 was merged into `main`. The legal status of that merge must be recorded so that merge is not mistaken for ratification.

**Decision (recorded prior owner decision)**

- `CATEGORY_DEVELOPMENT_MODEL.md` v0.2.0 was merged into `main` as: **Foundational Draft — Proposed for Ratification**.
- Merge does not equal ratification.
- The document becomes a **Ratified Foundational Governance Artifact** only by a later independent decision of the Repository Owner recorded in this log.
- This decision does **not** ratify the document's normative content; it fixes only its current legal status.

**Rationale**

Recording the merge status explicitly closes the gap between "merged" and "ratified" and prevents any implicit adoption of the document's normative content.

**Alternatives considered**

- *Treat merge as ratification.* Rejected: contradicts the corrected text of the document and the separation of merge from ratification.
- *Leave status unrecorded.* Rejected: leaves the document's legal status ambiguous.

**Consequences**

- `main` carries the document as a proposed draft, not a ratified artifact.
- Ratification requires a separate, later owner decision (see the critical constraint below).

**Evidence / related artifacts**

- Pull Request #1.
- Merge commit `7019769`.
- `CATEGORY_DEVELOPMENT_MODEL.md` v0.2.0 (§10, Amendment and Ratification).

**Review triggers**

- Any proposal to ratify the Category Development Model.
- Any substantive amendment to the document's normative content.

**Supersedes / superseded by**

- Supersedes: none.
- Superseded by: none.

---

## 5. Critical Constraint — No Implicit Ratification of the Category Development Model

No entry in this log currently ratifies `CATEGORY_DEVELOPMENT_MODEL.md`.

Ratification must be a **separate, later decision** — for example:

> **DEC-006 — Ratification of Category Development Model v0.2.0**

`DEC-006` shall not be written or accepted until:

1. this `DECISION_LOG.md` has been reviewed and merged, and
2. a new, explicit approval is issued by the Repository Owner.

Merging this log does not create `DEC-006`, does not accept any `Proposed` decision, and does not ratify the Category Development Model. (`DEC-000` was accepted by a separate, explicit owner decision — not by merge.)

---

## 6. Open Items

- `DEC-000` was explicitly accepted by the Repository Owner during the review of PR #2; the log's rules are therefore in force as a matter of owner decision, not of merge.
- Ratification of `CATEGORY_DEVELOPMENT_MODEL.md` (`DEC-006`) is not yet proposed and is intentionally deferred until this log is merged and reviewed.
- Remaining Layer 0 artifacts (`ACCESS_ONTOLOGY.md`, `FIRST_PRINCIPLES.md`, `CANONICAL_LANGUAGE.md`, `CLAIMS_AND_EVIDENCE_POLICY.md`) are not yet created.
