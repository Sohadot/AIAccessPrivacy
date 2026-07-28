# AI Access Declaration — Specification v0.1

**Status:** Draft
**Category:** AI Access Privacy
**File name:** `ai-access.json`
**Discovery path:** `/.well-known/ai-access.json`

---

## 1. Purpose

The AI Access Declaration is a machine-readable document that describes the
governed conditions under which an artificial intelligence system may access a
set of resources.

It is the concrete, verifiable expression of the AI Access Privacy category.

Where the category thesis defines *what* must be governed, this specification
defines *how it is declared* — in a single, portable, machine-readable file that
any party can publish, fetch, parse, verify, and monitor.

The declaration does not grant access. It **describes** access: the boundaries,
permitted operations, conditions, exposure, identity context, verification
status, and revocation state of a relationship between an AI system and a
resource.

---

## 2. Design Principles

1. **Vendor-neutral.** No dependency on a specific model, cloud, or IAM product.
2. **Descriptive, not enforcing.** The file declares intent and boundaries; it
   does not replace OAuth, IAM, or Zero Trust — it makes them *observable*.
3. **Portable.** A single JSON document, resolvable over HTTPS or embedded.
4. **Verifiable.** Every declaration can carry evidence and a verification status.
5. **Revocable.** Every declaration has a lifecycle and an explicit revocation state.
6. **Human- and machine-readable.** Strict JSON, stable field names, documented here.

---

## 3. Discovery

A declaration SHOULD be published at:

```
https://<host>/.well-known/ai-access.json
```

A resource, dataset, tool, or API MAY reference its declaration via an HTTP
header:

```
AI-Access-Declaration: https://example.com/.well-known/ai-access.json
```

---

## 4. Document Structure

The top-level document is a JSON object with the following members.

| Field            | Type    | Required | Description                                             |
|------------------|---------|----------|---------------------------------------------------------|
| `spec_version`   | string  | yes      | Specification version. `"0.1"` for this document.       |
| `declaration_id` | string  | yes      | Globally unique identifier (UUID or URI).               |
| `issued_at`      | string  | yes      | RFC 3339 timestamp of issuance.                         |
| `expires_at`     | string  | no       | RFC 3339 timestamp after which the declaration is stale.|
| `issuer`         | object  | yes      | The party publishing the declaration. See §5.           |
| `ai_system`      | object  | yes      | The AI system the declaration concerns. See §6.         |
| `access_grants`  | array   | yes      | The declared access relationships. See §7.              |
| `prohibitions`   | array   | no       | Explicitly forbidden operations or resources. See §8.   |
| `verification`   | object  | no       | Verification status and evidence. See §9.               |
| `observation`    | object  | no       | Continuous observation / logging posture. See §10.      |
| `revocation`     | object  | yes      | Lifecycle and revocation state. See §11.                |

---

## 5. `issuer`

Identifies who is making the declaration.

| Field     | Type   | Required | Description                                   |
|-----------|--------|----------|-----------------------------------------------|
| `name`    | string | yes      | Legal or organizational name.                 |
| `uri`     | string | no       | Canonical URI for the issuer.                 |
| `contact` | string | yes      | Email or URI for governance questions.        |
| `role`    | string | yes      | One of `resource-owner`, `ai-operator`, `third-party-auditor`. |

---

## 6. `ai_system`

Identifies the AI system whose access is being governed.

| Field          | Type    | Required | Description                                              |
|----------------|---------|----------|----------------------------------------------------------|
| `name`         | string  | yes      | Name of the AI system or agent.                          |
| `operator`     | string  | yes      | Party operating the system.                              |
| `model_family` | string  | no       | e.g. `gpt`, `claude`, `gemini`, `internal`.              |
| `agentic`      | boolean | yes      | `true` if the system can invoke tools or act autonomously.|
| `identifier`   | string  | no       | Stable identifier for the system (URI, DID, or key id).  |

---

## 7. `access_grants`

An array of declared access relationships. Each element is an object.

| Field                  | Type   | Required | Description                                                        |
|------------------------|--------|----------|--------------------------------------------------------------------|
| `resource`             | object | yes      | The resource being accessed. `{ "type": ..., "identifier": ... }`. `type` is one of `data`, `identity`, `tool`, `service`, `execution`. |
| `permitted_operations` | array  | yes      | e.g. `["read"]`, `["read","write"]`, `["invoke"]`, `["execute"]`.  |
| `purpose`              | string | yes      | Declared purpose of the access (human-readable).                   |
| `conditions`           | array  | no       | Conditions that must hold, as strings or structured predicates.    |
| `data_exposure`        | object | no       | What data classes are exposed. See §7.1.                           |
| `identity_context`     | object | no       | On whose behalf access occurs. See §7.2.                           |
| `authorization`        | object | no       | Underlying authorization reference. See §7.3.                      |

### 7.1 `data_exposure`

| Field           | Type   | Description                                             |
|-----------------|--------|---------------------------------------------------------|
| `classes`       | array  | e.g. `["public"]`, `["pii"]`, `["confidential"]`.       |
| `retention`     | string | e.g. `none`, `session`, `30d`, `indefinite`.            |
| `training_use`  | boolean| Whether accessed data may be used for model training.   |

### 7.2 `identity_context`

| Field         | Type   | Description                                                    |
|---------------|--------|----------------------------------------------------------------|
| `on_behalf_of`| string | `end-user`, `service-account`, `autonomous`.                   |
| `delegation`  | string | Reference to the delegation grant (e.g. OAuth token audience). |

### 7.3 `authorization`

| Field       | Type   | Description                                              |
|-------------|--------|----------------------------------------------------------|
| `mechanism` | string | e.g. `oauth2`, `api-key`, `mtls`, `iam-role`.            |
| `reference` | string | Opaque reference to the grant (never the secret itself). |

---

## 8. `prohibitions`

An array of explicitly forbidden operations. Each element:

| Field       | Type   | Required | Description                                     |
|-------------|--------|----------|-------------------------------------------------|
| `resource`  | object | no       | Resource the prohibition applies to (or omit for global). |
| `operation` | string | yes      | The forbidden operation.                        |
| `reason`    | string | no       | Human-readable rationale.                       |

---

## 9. `verification`

| Field          | Type   | Description                                                        |
|----------------|--------|--------------------------------------------------------------------|
| `status`       | string | `unverified`, `self-attested`, `third-party-verified`.             |
| `method`       | string | How verification was performed.                                    |
| `verified_by`  | string | Party who verified (URI or name).                                  |
| `evidence_uri` | string | Link to evidence (report, signature, attestation).                 |
| `verified_at`  | string | RFC 3339 timestamp.                                                 |

---

## 10. `observation`

| Field         | Type    | Description                                                     |
|---------------|---------|-----------------------------------------------------------------|
| `logging`     | boolean | Whether access under this declaration is logged.                |
| `endpoint`    | string  | URI where observation records or posture can be queried.        |
| `frequency`   | string  | e.g. `real-time`, `daily`, `on-access`.                         |

---

## 11. `revocation`

| Field        | Type   | Required | Description                                                |
|--------------|--------|----------|------------------------------------------------------------|
| `status`     | string | yes      | `active`, `suspended`, `revoked`.                          |
| `revoked_at` | string | no       | RFC 3339 timestamp if revoked.                             |
| `uri`        | string | no       | Endpoint to check live revocation status.                 |
| `contact`    | string | no       | Contact for revocation requests.                          |

---

## 12. Conformance

A document conforms to this specification if:

1. It is valid JSON.
2. All fields marked **Required** are present and correctly typed.
3. `spec_version` equals `"0.1"`.
4. Every `access_grants[].resource.type` is one of the enumerated values.
5. `revocation.status` is one of the enumerated values.

A consumer MUST treat a declaration as **not authoritative** when `expires_at`
is in the past or `revocation.status` is `revoked`.

---

## 13. Versioning

This specification uses `MAJOR.MINOR` versioning. Backward-incompatible changes
increment `MAJOR`. Additive, optional fields increment `MINOR`. Consumers MUST
ignore unknown fields to preserve forward compatibility.

---

## 14. Relationship to the Category

This specification implements the scope defined in `CATEGORY_THESIS.md`:

| Category scope element              | Declaration field(s)                    |
|-------------------------------------|-----------------------------------------|
| access boundaries                   | `access_grants`, `prohibitions`         |
| declared permissions                | `access_grants[].permitted_operations`  |
| execution capabilities              | `resource.type: execution`, `ai_system.agentic` |
| data exposure                       | `access_grants[].data_exposure`         |
| identity relationships              | `access_grants[].identity_context`      |
| authorization context               | `access_grants[].authorization`         |
| verification status                 | `verification`                          |
| evidence of declared behavior       | `verification.evidence_uri`             |
| continuous observation              | `observation`                           |
| revocation and lifecycle management | `revocation`, `expires_at`              |

The specification is intentionally minimal in v0.1. Future versions will add
signature envelopes, structured condition predicates, and a validation schema.
