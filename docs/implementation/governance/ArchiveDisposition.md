# ArchiveDisposition

[Minutes, resolutions and the archive](../../governance/minutes-and-resolutions.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Apply holds to originals, derivatives, search material and controlled copies. Destruction needs authorized approval and a disposition record. Preserve minimum non-content evidence when policy allows.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `disposal_decision_id` | DisposalDecision ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `custody_event_id` | CustodyEvent ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `book_id` | MinuteBook ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `record_locator` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `retention_rule` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `disposition_due` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `hold_reference` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `decision` | preserve/transfer/restrict/destroy | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `approved_by` | Person ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `performed_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `evidence` | text? | Optional under owner conditions | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### disposal_decision_id

The target is [DisposalDecision](../platform/DisposalDecision.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DisposalDecision·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | DisposalDecision·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | DisposalDecision·MISSING | Queue the missing DisposalDecision mapping or reject the command before linking. |
| Wrong scope | DisposalDecision·B01 | Do not attach another church’s DisposalDecision without a supported exchange and local authority. |
| Target rename | Rename DisposalDecision·A01 after linking | The existing disposal_decision_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No disposal_decision_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### custody_event_id

The target is [CustodyEvent](../administration/CustodyEvent.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CustodyEvent·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | CustodyEvent·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | CustodyEvent·MISSING | Queue the missing CustodyEvent mapping or reject the command before linking. |
| Wrong scope | CustodyEvent·B01 | Do not attach another church’s CustodyEvent without a supported exchange and local authority. |
| Target rename | Rename CustodyEvent·A01 after linking | The existing custody_event_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No custody_event_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### book_id

The target is [MinuteBook](MinuteBook.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MinuteBook·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | MinuteBook·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | MinuteBook·MISSING | Queue the missing MinuteBook mapping or reject the command before linking. |
| Wrong scope | MinuteBook·B01 | Do not attach another church’s MinuteBook without a supported exchange and local authority. |
| Target rename | Rename MinuteBook·A01 after linking | The existing book_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No book_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### record_locator

Use human-readable text for `ArchiveDisposition.record_locator`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered record_locator in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No record_locator at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### retention_rule

Use versioned classification or status code for `ArchiveDisposition.retention_rule`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active retention_rule code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped retention_rule code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No retention_rule at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### disposition_due

Use civil calendar date for `ArchiveDisposition.disposition_due`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No disposition_due provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### hold_reference

Use human-readable text for `ArchiveDisposition.hold_reference`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered hold_reference in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No hold_reference provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### decision

Declared alternatives in owner order: `preserve`, `transfer`, `restrict`, `destroy`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | preserve | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_decision | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No decision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### approved_by

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing approved_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No approved_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### performed_at

Use unambiguous point in time for `ArchiveDisposition.performed_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No performed_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### evidence

Use scoped or external reference for `ArchiveDisposition.evidence`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified evidence in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped evidence | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No evidence provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
