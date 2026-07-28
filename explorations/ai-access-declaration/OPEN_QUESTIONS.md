# Open Questions Raised by EXP-001

> Non-normative. Questions for the Layer 0 conceptual and ontological work.
> None is answered here. The prototype's own answers carry no weight — they were
> arbitrary choices made to keep the artifact buildable.

Each item is a place where the modeling attempt was *forced* to decide something
the category has not decided. Items marked **[review]** were raised or sharpened
in review of the prototype.

---

## 1. Is an access relationship a list of grants? **[review]**

The category's object may be an **operational access relationship**. The
prototype reduced this directly to `access_grants`, which assumes every access
relationship is a *granted* one.

That assumption excludes at least:

- inherited or transitively acquired permission
- access that is discovered and undeclared
- actual access that **contradicts** the declared access
- access technically available but never exercised
- access delegated through a chain of intermediaries
- access conditional on runtime state

If any of these belong to the category, "grant" is the wrong primitive and the
schema shape is wrong beneath it. This must come out of the ontology before any
schema is fixed.

## 2. Which party is speaking, and with what authority? **[review]**

The prototype allows `issuer.role` to be `resource-owner`, `ai-operator`, or
`third-party-auditor` — with one document shape for all three. These parties do
not hold the same authority to issue a declaration. An auditor may *verify* a
declaration but should not issue an access declaration on the relationship
owner's behalf in the same form.

At minimum these appear to be distinct roles requiring separation:

- **declarant** — who makes the statement
- **subject** — the AI system the statement is about
- **resource controller** — who controls the accessed resource
- **operator** — who runs the system
- **verifier** — who checks the statement

One shape for all of them is a modeling error, and it lets a claim, a grant, and
an attestation become indistinguishable.

## 3. Claim states, and provenance per claim **[review]**

The prototype offers three document-level states: `unverified`, `self-attested`,
`third-party-verified`. The agreed distinction is finer:

**Declared · Observed · Verified · Enforced · Unknown**

More importantly, epistemic status attaches to **individual claims**, not to the
document. A single declaration may simultaneously hold:

- `retention` — self-declared
- tool list — automatically observed
- authorization mechanism — evidence-verified
- runtime enforcement — unknown

A document-level status therefore overstates the weakest claim and understates
the strongest. Claim-level provenance is likely required.

## 4. What makes observation evidentiary? **[review]**

`observation.logging: true` asserts that access is logged. It does not answer:

- what is logged
- who owns the log
- retention period
- whether the log is complete
- whether it is tamper-evident
- whether execution *results* are included
- whether a verifier can actually reach it

As written, the field conveys more assurance than its evidence supports. What
turns logging into evidence is undefined.

## 5. Conditions have no semantics

`conditions` is an array of strings such as `"human confirmation recorded"`.
This is prose wearing a data structure's clothing — no machine can evaluate it.

Free text is acceptable inside a prototype. It cannot serve as a basis for
monitoring or verification until there is a structured predicate model defining
what a condition ranges over, when it is evaluated, and who evaluates it. This
may be the largest gap the exercise exposed.

## 6. Are the five resource types a real partition?

`data | identity | tool | service | execution` came from the thesis's scope
sentence. As a partition it leaks immediately: invoking a tool that returns
records is a tool access *and* a data access; a service call that runs code is
both service and execution; an identity is also data.

Are these five *kinds* of resource, or five *aspects* any single access may
simultaneously have? The prototype assumed the former because JSON made it easy.

## 7. Is `purpose` governable?

`purpose` is unverifiable free text, yet it carries most of the privacy weight —
everything else describes mechanism; only purpose describes why. If purpose
cannot be verified, does declaring it accomplish anything the category should
count? If it can, what makes it verifiable?

## 8. Does revocation belong to the declaration or the grant?

The prototype attaches `revocation` to the declaration. But revoking a
*description* of access does not revoke *access*. If the underlying grant
survives, what has been revoked? This may indicate the declaration is the wrong
thing to carry a lifecycle.

## 9. No composition model

Agentic systems delegate: agent → subagent → tool → service. The prototype
describes one system against a flat resource list, with no way to express a
delegation chain or how access attenuates along it. If the category is about
agentic access, composition is likely central rather than an extension.

## 10. Possible boundary leak

`CATEGORY_BOUNDARY.md` states the category is not an authorization protocol and
does not replace OAuth or IAM — yet the prototype carries
`authorization.mechanism` and `authorization.reference`. Is referencing a
mechanism a legitimate observation of access posture, or the first step across
the category's own boundary? The boundary document does not settle this.

## 11. Is a single document the right unit?

One file per AI system, per resource set, per organization, per deployment? The
prototype implicitly chose "one per publisher" — a deployment convenience with
no grounding in the category.

## 12. Schema rigor is deliberately deferred **[review]**

The schema is permissive in ways that would produce false confidence if it were
treated as authoritative. Known and **intentionally unfixed** at prototype stage:

- `additionalProperties: true` at top level, and unset within objects — typos and
  unknown fields validate silently
- several URI-bearing fields carry no `format` constraint
- `contact` is unconstrained
- `declaration_id` is an unconstrained string
- no conditional requirement that `revoked_at` be present when status is `revoked`
- no constraint that `expires_at` follow `issued_at`
- `permitted_operations` is not bound to a controlled vocabulary
- no uniqueness constraints
- no claim-level provenance (see Q3)

These are not fixed now because tightening a schema whose underlying model is
unsettled would encode arbitrary choices more firmly, not less. Rigor follows
the ontology.

## 13. Discovery is unratified **[review]**

`/.well-known/ai-access.json` is a promising direction for machine
discoverability, but no well-known URI has been registered and claiming one is a
standards act. Discovery is open.

---

## Summary

The exercise showed the category is **tractable**. It also showed that a
plausible artifact can be built while at least thirteen load-bearing decisions
remain undetermined.

That combination is the finding: buildability does not indicate readiness. An
artifact produced this early encodes arbitrary choices as though they were
commitments — which is why EXP-001 is not being merged as a foundation.
