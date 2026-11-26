# Collection

[Counter sales and fulfilment](../../commerce/fulfilment.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Claim token is scoped, single-use and replaceable. Verify the named collector or authorized substitute. Expiry routes to supervised release/refund under accepted terms.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `group_id` | ref FulfilmentGroup | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `pickup_location_id` | ref StockLocation | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `contact_version_id` | ref OrderContact | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `claim_token_fingerprint` | text | Required when the record reaches its applicable state | [digest](../value-conventions.md#digest) |
| `ready_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `expires_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `collected_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `verifier_id` | ref UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `proof_kind` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `state` | awaiting/ready/collected/expired/recalled | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### group_id

The target is [FulfilmentGroup](FulfilmentGroup.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FulfilmentGroup·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | FulfilmentGroup·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | FulfilmentGroup·MISSING | Queue the missing FulfilmentGroup mapping or reject the command before linking. |
| Wrong scope | FulfilmentGroup·B01 | Do not attach another church’s FulfilmentGroup without a supported exchange and local authority. |
| Target rename | Rename FulfilmentGroup·A01 after linking | The existing group_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No group_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### pickup_location_id

The target is [StockLocation](StockLocation.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | StockLocation·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | StockLocation·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | StockLocation·MISSING | Queue the missing StockLocation mapping or reject the command before linking. |
| Wrong scope | StockLocation·B01 | Do not attach another church’s StockLocation without a supported exchange and local authority. |
| Target rename | Rename StockLocation·A01 after linking | The existing pickup_location_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No pickup_location_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### contact_version_id

The target is [OrderContact](OrderContact.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | OrderContact·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | OrderContact·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | OrderContact·MISSING | Queue the missing OrderContact mapping or reject the command before linking. |
| Wrong scope | OrderContact·B01 | Do not attach another church’s OrderContact without a supported exchange and local authority. |
| Target rename | Rename OrderContact·A01 after linking | The existing contact_version_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No contact_version_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### claim_token_fingerprint

Use integrity fingerprint or opaque verifier for `Collection.claim_token_fingerprint`. Bind the algorithm or verifier scheme and object revision to the evidence.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified fingerprint of edition A | Bind the algorithm or verifier scheme and object revision to the evidence. |
| Malformed or unmapped | different fingerprint for the same purported bytes | Quarantine the mismatch or deny the claim. |
| An identical copy is rechecked | compare original bytes with verified copy | Equality confirms the checked bytes or verifier under the same scheme only. |
| New revision has changed content | different bytes under a new edition | Compute new evidence; preserve the prior verified revision. |
| A user knows a digest | unprivileged user presents a publicly observed fingerprint | Knowledge alone grants no additional access outside the documented token protocol. |
| Incomplete record | No claim_token_fingerprint at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### ready_at

Use unambiguous point in time for `Collection.ready_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No ready_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### expires_at

Use unambiguous point in time for `Collection.expires_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No expires_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### collected_at

Use unambiguous point in time for `Collection.collected_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No collected_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### verifier_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing verifier_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No verifier_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### proof_kind

Use versioned classification or status code for `Collection.proof_kind`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active proof_kind code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped proof_kind code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No proof_kind provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Declared alternatives in owner order: `awaiting`, `ready`, `collected`, `expired`, `recalled`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | awaiting | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
