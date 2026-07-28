# AIAccessPrivacy

A vendor-neutral reference category for **governed AI access** — defining,
declaring, verifying, observing, and revoking the conditions under which AI
systems may access data, identities, tools, services, and execution
capabilities.

The category is under active development. Nothing in this repository is a
ratified standard.

---

## Layer 0 — Foundation

The category is defined here. These documents govern everything else.

| Document | Purpose | Status |
|---|---|---|
| [`CATEGORY_THESIS.md`](CATEGORY_THESIS.md) | Why the category exists, its definition, scope, mission | Drafted |
| `CATEGORY_DEVELOPMENT_MODEL.md` | How the category is developed and ratified | Not started |
| `ACCESS_ONTOLOGY.md` | What access *is*; the relationship, grant, declaration, observation, verification distinctions | Not started |
| [`CATEGORY_BOUNDARY.md`](CATEGORY_BOUNDARY.md) | What the category is and is not | Partial — revision pending |
| `FIRST_PRINCIPLES.md` | The commitments the category rests on | Not started |
| `CANONICAL_LANGUAGE.md` | Controlled vocabulary | Not started |
| `CLAIMS_AND_EVIDENCE_POLICY.md` | What may be claimed, and what evidence supports each claim | Not started |

## Layer 1+ — Explorations

Concrete artifacts built to test the category. **Non-normative and disposable.**
They inform the foundation; they do not constrain it.

| ID | Exploration | Status |
|---|---|---|
| EXP-001 | [`explorations/ai-access-declaration/`](explorations/ai-access-declaration/) | Exploratory prototype — not merged as foundation |

See [`explorations/README.md`](explorations/README.md) for how explorations are
treated.

---

## Sequencing

Layer 0 is completed and ratified before any artifact is promoted, any
conformance model is defined, or any service, program, or certification is
derived from this work.

EXP-001 established that the category is *tractable* — its scope elements can be
given concrete machine-readable form. It also established that a plausible
artifact can be built while the foundational questions remain open, which is
exactly why it is retained as evidence rather than adopted as a specification.
Its findings are recorded in
[`explorations/ai-access-declaration/OPEN_QUESTIONS.md`](explorations/ai-access-declaration/OPEN_QUESTIONS.md).
