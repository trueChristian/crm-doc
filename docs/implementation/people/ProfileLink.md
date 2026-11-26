# ProfileLink

[Directory publication and member self-service](../../people/directory-and-self-service.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Project the church-person linkage maintained by UserAccount. Derive pending assertions from IdentityReview and verified status from the canonical identity decision. One ID and state transition govern all views. Delegates sign in separately.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | = UserAccount.id | Assigned or projected by owner | [alias](../value-conventions.md#alias) |
| `person_id` | → Person? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `link_status` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `access_revision` | integer | Required when the record reaches its applicable state | [version](../value-conventions.md#version) |
| `verified_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `identity_review_ref` | → IdentityReview? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Authoritative source: `UserAccount.id`. Record one change at that owner and re-evaluate derived access.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount.id | Rebuild the projection from its authorized source revision. |
| Malformed or unmapped | independent local value | Route the correction to the owning record. |
| Owner revokes or corrects the source | owner changes revision 7 to 8 | Invalidate the prior projection at the defined effective point. |
| Rebuild after missed update | projection is at revision 6, owner is at 8 | Use authoritative revision and reconcile lag. |
| User lacks access to the source field | grant for the original source expires | Projection does not reveal the value. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### person_id

The target is [Person](Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing person_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No person_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### link_status

Use versioned classification or status code for `ProfileLink.link_status`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active link_status code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped link_status code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No link_status at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### access_revision

Use revision number or opaque revision token for `ProfileLink.access_revision`. Compare under the declared revision scheme. Require the expected version for conflicting work.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | the current revision returned by the owner | Compare under the declared revision scheme. Require the expected version for conflicting work. |
| Malformed or unmapped | superseded version presented for a new approval | Reject or reopen review against the current contents. |
| Two operators begin at revision seven | two edits both cite baseline 7 | Commit the first change once and re-evaluate the second; never overwrite an unreviewed difference. |
| Re-read an already approved revision | re-open issued revision 4 after revision 6 | Return the frozen value and evidence for that edition. |
| Replay of an earlier result | same business operation observed at two revisions | Correlate by the business operation identity; a newer version does not create a second effect. |
| Incomplete record | No access_revision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### verified_at

Use unambiguous point in time for `ProfileLink.verified_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No verified_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### identity_review_ref

The target is [IdentityReview](../platform/IdentityReview.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | IdentityReview·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | IdentityReview·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | IdentityReview·MISSING | Queue the missing IdentityReview mapping or reject the command before linking. |
| Wrong scope | IdentityReview·B01 | Do not attach another church’s IdentityReview without a supported exchange and local authority. |
| Target rename | Rename IdentityReview·A01 after linking | The existing identity_review_ref keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No identity_review_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
