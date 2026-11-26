# ProfileInvitation

[Directory publication and member self-service](../../people/directory-and-self-service.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Show only AccountInvitation records for profile-link purpose. Use the same verifier, expiry, attempts, cancellation, reissue and atomic redemption. No additional secret or independent invitation exists in this view.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | = AccountInvitation.id | Assigned or projected by owner | [alias](../value-conventions.md#alias) |
| `person_id` | = intended_person_id | Assigned or projected by owner | [alias](../value-conventions.md#alias) |
| `delivery_contact_ref` | ID | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `issued_by` | → UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `expires_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `consumed_at` | = accepted_at? | Assigned or projected by owner | [alias](../value-conventions.md#alias) |
| `revoked_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `derived_state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Authoritative source: `AccountInvitation.id`. Record one change at that owner and re-evaluate derived access.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AccountInvitation.id | Rebuild the projection from its authorized source revision. |
| Malformed or unmapped | independent local value | Route the correction to the owning record. |
| Owner revokes or corrects the source | owner changes revision 7 to 8 | Invalidate the prior projection at the defined effective point. |
| Rebuild after missed update | projection is at revision 6, owner is at 8 | Use authoritative revision and reconcile lag. |
| User lacks access to the source field | grant for the original source expires | Projection does not reveal the value. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### person_id

Authoritative source: `intended_person_id`. Record one change at that owner and re-evaluate derived access.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | intended_person_id | Rebuild the projection from its authorized source revision. |
| Malformed or unmapped | independent local value | Route the correction to the owning record. |
| Owner revokes or corrects the source | owner changes revision 7 to 8 | Invalidate the prior projection at the defined effective point. |
| Rebuild after missed update | projection is at revision 6, owner is at 8 | Use authoritative revision and reconcile lag. |
| User lacks access to the source field | grant for the original source expires | Projection does not reveal the value. |
| Independent overwrite | Attempt to replace person_id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### delivery_contact_ref

Use scoped or external reference for `ProfileInvitation.delivery_contact_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified delivery_contact_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped delivery_contact_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No delivery_contact_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

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

### expires_at

Use unambiguous point in time for `ProfileInvitation.expires_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No expires_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### consumed_at

Authoritative source: `accepted_at?`. Record one change at that owner and re-evaluate derived access.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | accepted_at | Rebuild the projection from its authorized source revision. |
| Malformed or unmapped | independent local value | Route the correction to the owning record. |
| Owner revokes or corrects the source | owner changes revision 7 to 8 | Invalidate the prior projection at the defined effective point. |
| Rebuild after missed update | projection is at revision 6, owner is at 8 | Use authoritative revision and reconcile lag. |
| User lacks access to the source field | grant for the original source expires | Projection does not reveal the value. |
| Absent in intake | No consumed_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### revoked_at

Use unambiguous point in time for `ProfileInvitation.revoked_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No revoked_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### derived_state

Use versioned classification or status code for `ProfileInvitation.derived_state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active derived_state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped derived_state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No derived_state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
