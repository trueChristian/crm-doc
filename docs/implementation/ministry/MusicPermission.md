# MusicPermission

[Worship and music](../../ministry/worship.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Separate decisions for in-room performance, printing, projection, rehearsal downloads, live transmission and archival access. Venue or online terms can differ. Unknown or expired permission requires review for the affected use.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `work_id` | → MusicWork | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `arrangement_id` | → MusicArrangement? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `use_code` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `territory_scope` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `valid_from` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `valid_until` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `reviewed_by` | → UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `decision` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `evidence_ref` | id? | Optional under owner conditions | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### work_id

The target is [MusicWork](MusicWork.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MusicWork·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | MusicWork·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | MusicWork·MISSING | Queue the missing MusicWork mapping or reject the command before linking. |
| Wrong scope | MusicWork·B01 | Do not attach another church’s MusicWork without a supported exchange and local authority. |
| Target rename | Rename MusicWork·A01 after linking | The existing work_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No work_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### arrangement_id

The target is [MusicArrangement](MusicArrangement.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MusicArrangement·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | MusicArrangement·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | MusicArrangement·MISSING | Queue the missing MusicArrangement mapping or reject the command before linking. |
| Wrong scope | MusicArrangement·B01 | Do not attach another church’s MusicArrangement without a supported exchange and local authority. |
| Target rename | Rename MusicArrangement·A01 after linking | The existing arrangement_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No arrangement_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### use_code

Use versioned classification or status code for `MusicPermission.use_code`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active use_code code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped use_code code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No use_code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### territory_scope

Use human-readable text for `MusicPermission.territory_scope`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered territory_scope in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No territory_scope at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### valid_from

Use civil calendar date for `MusicPermission.valid_from`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No valid_from at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### valid_until

Use civil calendar date for `MusicPermission.valid_until`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No valid_until provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### reviewed_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing reviewed_by keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No reviewed_by at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### decision

Use versioned classification or status code for `MusicPermission.decision`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active decision code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped decision code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No decision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### evidence_ref

Use scoped or external reference for `MusicPermission.evidence_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified evidence_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped evidence_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No evidence_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
