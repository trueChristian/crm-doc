# MemorialTribute

[Weddings, funerals, memorials and cemetery administration](../../administration/life-events.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Approval of funeral details and publication of a photo, tribute or recording are independent decisions. Permit prompt withdrawal from public display.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | Owner-scoped business value; see the record rule | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `request_id` | → CeremonyRequest | Required at applicable lifecycle step | [relation](../value-conventions.md#relation) |
| `contributed_by` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [resource](../value-conventions.md#resource) |
| `content_ref` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [resource](../value-conventions.md#resource) |
| `publication_scope` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [structured](../value-conventions.md#structured) |
| `consent_ref` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [resource](../value-conventions.md#resource) |
| `review_state` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [vocab](../value-conventions.md#vocab) |
| `moderation_reason` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [text](../value-conventions.md#text) |
| `publish_from` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [structured](../value-conventions.md#structured) |
| `publish_until` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [structured](../value-conventions.md#structured) |
| `withdrawn_at` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [instant](../value-conventions.md#instant) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `MemorialTribute.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MemorialTribute·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### request_id

The target is [CeremonyRequest](CeremonyRequest.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CeremonyRequest·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | CeremonyRequest·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | CeremonyRequest·MISSING | Queue the missing CeremonyRequest mapping or reject the command before linking. |
| Wrong scope | CeremonyRequest·B01 | Do not attach another church’s CeremonyRequest without a supported exchange and local authority. |
| Target rename | Rename CeremonyRequest·A01 after linking | The existing request_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No request_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### contributed_by

Use scoped or external reference for `MemorialTribute.contributed_by`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified contributed_by in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped contributed_by | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No contributed_by at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### content_ref

Use scoped or external reference for `MemorialTribute.content_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified content_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped content_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No content_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### publication_scope

Use typed value or bounded compound record for `MemorialTribute.publication_scope`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of publication_scope matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for publication_scope | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Incomplete record | No publication_scope at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### consent_ref

Use scoped or external reference for `MemorialTribute.consent_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified consent_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped consent_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No consent_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### review_state

Use versioned classification or status code for `MemorialTribute.review_state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active review_state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped review_state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No review_state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### moderation_reason

Use human-readable text for `MemorialTribute.moderation_reason`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered moderation_reason in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No moderation_reason at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### publish_from

Use typed value or bounded compound record for `MemorialTribute.publish_from`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of publish_from matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for publish_from | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Incomplete record | No publish_from at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### publish_until

Use typed value or bounded compound record for `MemorialTribute.publish_until`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of publish_until matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for publish_until | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Incomplete record | No publish_until at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### withdrawn_at

Use unambiguous point in time for `MemorialTribute.withdrawn_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No withdrawn_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
