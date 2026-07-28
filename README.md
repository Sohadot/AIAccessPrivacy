# AIAccessPrivacy

A vendor-neutral reference category for **governed AI access** — defining,
declaring, verifying, observing, and revoking the conditions under which AI
systems may access data, identities, tools, services, and execution
capabilities.

## Documents

| File | Purpose |
|------|---------|
| [`CATEGORY_THESIS.md`](CATEGORY_THESIS.md) | Why the category exists, its definition, scope, and mission. |
| [`CATEGORY_BOUNDARY.md`](CATEGORY_BOUNDARY.md) | What the category is and is not; its relationship to adjacent disciplines. |
| [`SPEC.md`](SPEC.md) | **AI Access Declaration** — the machine-readable specification (v0.1). |
| [`schema/ai-access.schema.json`](schema/ai-access.schema.json) | JSON Schema for validating declarations. |
| [`examples/ai-access.json`](examples/ai-access.json) | A complete example declaration. |

## The AI Access Declaration

The core artifact of this category is a portable, machine-readable file —
`ai-access.json`, published at `/.well-known/ai-access.json` — that declares the
governed conditions of AI access to a set of resources. It makes existing
controls (OAuth, IAM, Zero Trust) *observable* as part of AI access, without
replacing them.

See [`SPEC.md`](SPEC.md) to get started.
