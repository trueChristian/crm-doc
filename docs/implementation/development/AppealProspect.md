# AppealProspect

[Appeals and attribution](../../development/appeals.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique active assignment per appeal and party. Store only voluntarily offered or approved information relevant to the invitation. Reassignment includes current contact limitations.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `appeal_id` | ref FundraisingAppeal | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `giving_party_id` | ref GivingParty | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `steward_id` | ref UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `origin` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `eligible_purpose` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `assigned_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `review_by` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `stage` | identified/permitted/in_discussion/asked/closed | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `decline_reason` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `restricted_note_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### appeal_id

The target is [FundraisingAppeal](FundraisingAppeal.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FundraisingAppeal·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | FundraisingAppeal·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | FundraisingAppeal·MISSING | Queue the missing FundraisingAppeal mapping or reject the command before linking. |
| Wrong scope | FundraisingAppeal·B01 | Do not attach another church’s FundraisingAppeal without a supported exchange and local authority. |
| Target rename | Rename FundraisingAppeal·A01 after linking | The existing appeal_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No appeal_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### giving_party_id

The target is [GivingParty](../finance/GivingParty.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GivingParty·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | GivingParty·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | GivingParty·MISSING | Queue the missing GivingParty mapping or reject the command before linking. |
| Wrong scope | GivingParty·B01 | Do not attach another church’s GivingParty without a supported exchange and local authority. |
| Target rename | Rename GivingParty·A01 after linking | The existing giving_party_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No giving_party_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### steward_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing steward_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No steward_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### origin

Use versioned classification or status code for `AppealProspect.origin`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active origin code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped origin code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No origin at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### eligible_purpose

Use versioned classification or status code for `AppealProspect.eligible_purpose`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active eligible_purpose code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped eligible_purpose code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No eligible_purpose at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### assigned_on

Use civil calendar date for `AppealProspect.assigned_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No assigned_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### review_by

Use civil calendar date for `AppealProspect.review_by`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No review_by at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### stage

Declared alternatives in owner order: `identified`, `permitted`, `in_discussion`, `asked`, `closed`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | identified | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_stage | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No stage at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### decline_reason

Use versioned classification or status code for `AppealProspect.decline_reason`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active decline_reason code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped decline_reason code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No decline_reason provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### restricted_note_ref

Use scoped or external reference for `AppealProspect.restricted_note_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified restricted_note_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped restricted_note_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No restricted_note_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AppealAsk](AppealAsk.md).`prospect_id` | AppealProspect identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
