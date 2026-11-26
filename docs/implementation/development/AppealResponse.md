# AppealResponse

[Appeals and attribution](../../development/appeals.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

A response may remain anonymous. An enquiry or attendance at the supper does not authorize unrelated future contact. Forward opt-out promptly to communications and block queued solicitation.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `channel_id` | ref AppealChannel | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `giving_party_id` | ref GivingParty? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `received_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `kind` | enquiry/decline/interest/offer/referral/opt_out | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `next_owner_id` | ref UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `due_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `consent_basis_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `disposition` | open/assigned/resolved/withdrawn | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### channel_id

The target is [AppealChannel](AppealChannel.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AppealChannel·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | AppealChannel·MISSING | Queue the missing AppealChannel mapping or reject the command before linking. |
| Wrong scope | AppealChannel·B01 | Do not attach another church’s AppealChannel without a supported exchange and local authority. |
| Target rename | Rename AppealChannel·A01 after linking | The existing channel_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No channel_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### giving_party_id

The target is [GivingParty](../finance/GivingParty.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GivingParty·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | GivingParty·MISSING | Queue the missing GivingParty mapping or reject the command before linking. |
| Wrong scope | GivingParty·B01 | Do not attach another church’s GivingParty without a supported exchange and local authority. |
| Target rename | Rename GivingParty·A01 after linking | The existing giving_party_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No giving_party_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### received_at

Use unambiguous point in time for `AppealResponse.received_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No received_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### kind

Declared alternatives in owner order: `enquiry`, `decline`, `interest`, `offer`, `referral`, `opt_out`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | enquiry | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_kind | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### next_owner_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing next_owner_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No next_owner_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### due_on

Use civil calendar date for `AppealResponse.due_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No due_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### consent_basis_ref

Use scoped or external reference for `AppealResponse.consent_basis_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified consent_basis_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped consent_basis_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No consent_basis_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### disposition

Declared alternatives in owner order: `open`, `assigned`, `resolved`, `withdrawn`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | open | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_disposition | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No disposition at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Use the minimum evidence allowed by the selected anonymous, pseudonymous or identified mode. A permitted operator may be accountable for receiving or reviewing work without collecting the identity of a protected subject. Keep safe-channel, identity and case evidence apart from releasable totals and narratives; apply the original permissions to the verification evidence.
