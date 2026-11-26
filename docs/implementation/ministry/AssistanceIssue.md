# AssistanceIssue

[Missions and community service](../../ministry/missions.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One recipient basis per issue, with policy permitting anonymous collection. Count and unit must be positive. Unique operation key prevents a repeated handover from decrementing stock twice.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `distribution_id` | → CommunityDistribution | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `supply_id` | → ProjectSupply | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `recipient_person_id` | → Person? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `recipient_household_id` | → Household? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `anonymous_case_ref` | text? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `issued_quantity` | decimal | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `unit` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `issued_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `issued_by` | → UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `stock_movement_ref` | → StockMovement? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `request_key` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### distribution_id

The target is [CommunityDistribution](CommunityDistribution.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CommunityDistribution·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | CommunityDistribution·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | CommunityDistribution·MISSING | Queue the missing CommunityDistribution mapping or reject the command before linking. |
| Wrong scope | CommunityDistribution·B01 | Do not attach another church’s CommunityDistribution without a supported exchange and local authority. |
| Target rename | Rename CommunityDistribution·A01 after linking | The existing distribution_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No distribution_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### supply_id

The target is [ProjectSupply](ProjectSupply.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ProjectSupply·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ProjectSupply·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ProjectSupply·MISSING | Queue the missing ProjectSupply mapping or reject the command before linking. |
| Wrong scope | ProjectSupply·B01 | Do not attach another church’s ProjectSupply without a supported exchange and local authority. |
| Target rename | Rename ProjectSupply·A01 after linking | The existing supply_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No supply_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### recipient_person_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing recipient_person_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No recipient_person_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### recipient_household_id

The target is [Household](../people/Household.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Household·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Household·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Household·MISSING | Queue the missing Household mapping or reject the command before linking. |
| Wrong scope | Household·B01 | Do not attach another church’s Household without a supported exchange and local authority. |
| Target rename | Rename Household·A01 after linking | The existing recipient_household_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No recipient_household_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### anonymous_case_ref

Use scoped or external reference for `AssistanceIssue.anonymous_case_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified anonymous_case_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped anonymous_case_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No anonymous_case_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### issued_quantity

Use exact decimal measure for `AssistanceIssue.issued_quantity`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No issued_quantity at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### unit

Use versioned classification or status code for `AssistanceIssue.unit`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active unit code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped unit code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No unit at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### issued_at

Use unambiguous point in time for `AssistanceIssue.issued_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No issued_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### issued_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing issued_by keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No issued_by at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### stock_movement_ref

The target is [StockMovement](../commerce/StockMovement.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | StockMovement·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | StockMovement·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | StockMovement·MISSING | Queue the missing StockMovement mapping or reject the command before linking. |
| Wrong scope | StockMovement·B01 | Do not attach another church’s StockMovement without a supported exchange and local authority. |
| Target rename | Rename StockMovement·A01 after linking | The existing stock_movement_ref keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No stock_movement_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### request_key

Use human-readable text for `AssistanceIssue.request_key`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered request_key in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No request_key at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [CollectionAcknowledgement](../administration/CollectionAcknowledgement.md).`issue_id` | AssistanceIssue identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
