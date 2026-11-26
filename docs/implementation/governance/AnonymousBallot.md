# AnonymousBallot

[Deliberation and voting](../../governance/deliberation-and-voting.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

No person, entitlement, device, entry sequence, fine-grained casting time, signature or delivery trace. Only use weight classes when they preserve secrecy; otherwise choose another rule-approved process.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `round_id` | DecisionRound ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `batch_code` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `selections` | limited choice list | Required when the record reaches its applicable state | [list](../value-conventions.md#list) |
| `weight_class` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `validity` | valid/blank/spoilt/challenged | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### round_id

The target is [DecisionRound](DecisionRound.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DecisionRound·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | DecisionRound·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | DecisionRound·MISSING | Queue the missing DecisionRound mapping or reject the command before linking. |
| Wrong scope | DecisionRound·B01 | Do not attach another church’s DecisionRound without a supported exchange and local authority. |
| Target rename | Rename DecisionRound·A01 after linking | The existing round_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No round_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### batch_code

Use human-readable text for `AnonymousBallot.batch_code`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered batch_code in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No batch_code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### selections

Use ordered collection or mathematical set for `AnonymousBallot.selections`. Preserve ordering when meaningful; enforce uniqueness when the declaration is a set.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted members A and B | Preserve ordering when meaningful; enforce uniqueness when the declaration is a set. |
| Malformed or unmapped | an element outside the declared domain | Reject the affected collection or stage its invalid item under the import policy. |
| Same element appears twice | A, A, B | Apply declared sequence/set multiplicity without doubling financial or voting effects. |
| Empty collection versus unknown collection | empty collection and missing collection | Preserve the distinction where the rule requires evidence. |
| One element later becomes restricted | authorization for member B withdrawn before export | Recompute permitted projection before export or display. |
| Incomplete record | No selections at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### weight_class

Use versioned classification or status code for `AnonymousBallot.weight_class`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active weight_class code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped weight_class code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No weight_class provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### validity

Declared alternatives in owner order: `valid`, `blank`, `spoilt`, `challenged`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | valid | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_validity | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No validity at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
