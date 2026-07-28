# AI Access Declaration — Exploratory Prototype 0.1

**Exploration ID:** EXP-001
**Status:** Exploratory, non-normative, pre-ontology prototype

> This document is non-normative and exploratory. It does not constitute the AI
> Access Privacy Standard. Its data model remains subject to revision after the
> Access Ontology, Category Boundary, First Principles, and Claims and Evidence
> Policy are ratified.

Do not implement it. Do not cite it as a reference for the category. Do not
publish artifacts derived from it as though they were conformant to anything.

---

## 1. What this was

An attempt to answer one question:

> Can the scope elements listed in `CATEGORY_THESIS.md` be expressed as a single,
> concrete, machine-readable artifact?

The attempt produced a JSON document shape describing the conditions under which
an AI system accesses a resource, together with a validation schema and a worked
example.

## 2. What it demonstrated

The scope elements *can* be given concrete form. Every element named in the
category thesis was expressible as a field, and a worked example validated
against the resulting schema.

Reviewed strengths worth carrying forward as candidate ideas — not as decisions:

- **Description is separated from granting.** The document describes access; it
  does not confer it. This separation held up under modeling.
- **Machine discoverability is achievable.** A fetchable JSON document at a
  predictable location makes access posture inspectable by third parties.
- **A schema plus a worked example** is the right shape for an operational test,
  because it forces the model to survive contact with a concrete case.
- **Issuer / AI system / access relationships / revocation** is a plausible
  first decomposition — plausible, not settled.

This is a positive result about **tractability**. It shows the category is not
purely abstract and can produce operational artifacts.

It is **not** a result about correctness. Expressibility is a weak test: many
mutually incompatible models would also have passed it.

## 3. What it does not establish

The prototype names itself the "concrete, verifiable expression" of the category
and defines how access is declared in a single file. That framing outran the
foundation. The category has not yet settled:

- what access **is**, ontologically
- the precise difference between a *declaration*, a *grant*, a *relationship*,
  an *observation*, and a *verification*

Until those are settled, this document establishes none of the following:

- that these are the right fields, or the right number of them
- that the five resource types are a real partition of the category
- that a single document is the right unit at all
- that an access relationship is adequately modeled as a list of grants
- any boundary, commitment, or vocabulary for AI Access Privacy

The distinctions below were the first that came to mind while modeling. They
were not derived from the ontology, because the ontology does not exist yet.
Several are probably wrong; see [`OPEN_QUESTIONS.md`](OPEN_QUESTIONS.md).

---

## 4. The model that was built

Recorded for reference. Descriptive throughout — no requirement language is
intended, and no conformance is defined.

| Field | Modeled as | Element it was reaching for |
|---|---|---|
| `prototype_version` | string | — |
| `declaration_id` | unique identifier | — |
| `issued_at` / `expires_at` | timestamps | lifecycle |
| `issuer` | party publishing the document | — |
| `ai_system` | the AI system being described | identity relationships |
| `access_grants` | array of access relationships | access boundaries, declared permissions |
| `prohibitions` | explicit negative statements | access boundaries |
| `verification` | status + evidence pointer | verification status, evidence |
| `observation` | logging/monitoring posture | continuous observation |
| `revocation` | lifecycle state | revocation and lifecycle |

Within each `access_grants` entry:

- `resource` — typed as one of `data`, `identity`, `tool`, `service`, `execution`
- `permitted_operations` — free-form operation strings
- `purpose` — free text
- `conditions` — free-text strings
- `data_exposure` — data classes, retention, training use
- `identity_context` — on whose behalf access occurs
- `authorization` — a reference to the underlying mechanism

Files:

- [`schema.json`](schema.json) — validation schema for the shape above
- [`example-declaration.json`](example-declaration.json) — a **synthetic**
  example that validates against it

### Discovery

The prototype assumed publication at a `/.well-known/ai-access.json` path with
an accompanying HTTP header. Machine discoverability is a genuine strength of
the approach and is retained as a **candidate** direction.

It is not a decision. No well-known URI has been registered, and claiming one is
a standards act this project is not yet positioned to make. Discovery remains an
open question.

---

## 5. Findings

The modeling exercise, and the review that followed it, surfaced a set of places
where the category has not yet decided something the artifact was forced to
decide arbitrarily.

Those are recorded in [`OPEN_QUESTIONS.md`](OPEN_QUESTIONS.md), and are the
actual output of this exploration.

---

## 6. Disposition

Retained as EXP-001 pending completion of the Layer 0 foundation:

- `CATEGORY_DEVELOPMENT_MODEL.md`
- `ACCESS_ONTOLOGY.md`
- `CATEGORY_BOUNDARY.md`
- `FIRST_PRINCIPLES.md`
- `CANONICAL_LANGUAGE.md`
- `CLAIMS_AND_EVIDENCE_POLICY.md`

To be re-reviewed afterward — at which point the correct outcome may be to
revise it, replace it, or delete it. None of those outcomes is privileged by the
fact that this was built first.

No validator service, conformance program, or certification is to be derived
from this prototype. Conformance, evidence, and independence are undefined, and
a certification claim without them would be unsupportable.
