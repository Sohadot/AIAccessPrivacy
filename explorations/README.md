# Explorations

This directory holds **exploratory prototypes**.

An exploration is an attempt to express some part of the AI Access Privacy
category in a concrete form — a data model, an artifact, a tool sketch — in
order to learn something about the category.

## Status of everything in this directory

Explorations are **non-normative**. They do not define the category, do not
constrain it, and carry no authority over it.

Specifically, nothing in this directory:

- defines AI Access Privacy or any part of it
- is a standard, specification, or proposed standard
- is stable, versioned for adoption, or intended for implementation
- should be cited as a reference for the category

The foundational documents are [`../CATEGORY_THESIS.md`](../CATEGORY_THESIS.md)
and [`../CATEGORY_BOUNDARY.md`](../CATEGORY_BOUNDARY.md). Those govern. These do not.

## Why explorations exist

A category can be defined abstractly and still be unbuildable. Explorations
test the opposite direction: given the category as currently stated, can a
concrete artifact be produced from it, and what breaks when you try?

The output of an exploration is **not the artifact**. The output is what the
attempt revealed — the distinctions that turned out to be unstable, the
questions the category has not yet answered, the boundaries that leaked.

Those findings are inputs to the conceptual and ontological work. The artifact
itself is a by-product, and may be discarded entirely.

## Direction of authority

```
CATEGORY_THESIS.md / CATEGORY_BOUNDARY.md   →   ontology   →   explorations
                    (foundation)                              (evidence, disposable)
```

Authority flows down. Findings flow back up as questions, never as commitments.

An exploration is never promoted to a foundational document by being useful.
If a model here turns out to be right, it earns that status through the
conceptual work — not by having been built first.

## Register

| ID | Exploration | Question it was testing | Status |
|---|---|---|---|
| **EXP-001** | [`ai-access-declaration/`](ai-access-declaration/) | Can the category's scope elements be expressed as a single machine-readable artifact? | Exploratory, non-normative, pre-ontology prototype. Reviewed; not merged as foundation. Findings recorded. |

## Gate

No exploration is merged as a foundational document, and no product,
service, conformance program, or certification is derived from one, before the
Layer 0 documents listed in the [root README](../README.md#layer-0--foundation)
are ratified.

The reason is specific: conformance, evidence, and independence are undefined at
this stage, so any assurance claim built on an exploration would be
unsupportable — and a first draft that ships early tends to become the standard
by default rather than by merit.
