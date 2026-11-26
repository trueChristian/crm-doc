# AccessGrant

[Subscriptions, grants and playback](../../commerce/access.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Each grant identifies one verifiable beneficiary or pending claim, permissible scope, quantity and an originating purchase, term or authorized free grant. Unique source action and beneficiary seat. A claim and an account can coexist only after verified redemption links them.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `plan_id` | ref AccessPlan | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `beneficiary_account_id` | ref UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `beneficiary_person_id` | ref Person? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `claim_id` | ref GiftClaim? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `order_line_id` | ref OrderLine? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `subscription_term_id` | ref SubscriptionTerm? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `approval_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `starts_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `ends_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `activation_deadline` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `activated_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `granted_units` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `state` | awaiting_claim/pending_start/active/suspended/expired/revoked | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `reason` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `source_action_key` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### plan_id

The target is [AccessPlan](AccessPlan.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AccessPlan·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | AccessPlan·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | AccessPlan·MISSING | Queue the missing AccessPlan mapping or reject the command before linking. |
| Wrong scope | AccessPlan·B01 | Do not attach another church’s AccessPlan without a supported exchange and local authority. |
| Target rename | Rename AccessPlan·A01 after linking | The existing plan_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No plan_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### beneficiary_account_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing beneficiary_account_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No beneficiary_account_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### beneficiary_person_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing beneficiary_person_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No beneficiary_person_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### claim_id

The target is [GiftClaim](GiftClaim.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GiftClaim·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | GiftClaim·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | GiftClaim·MISSING | Queue the missing GiftClaim mapping or reject the command before linking. |
| Wrong scope | GiftClaim·B01 | Do not attach another church’s GiftClaim without a supported exchange and local authority. |
| Target rename | Rename GiftClaim·A01 after linking | The existing claim_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No claim_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### order_line_id

The target is [OrderLine](OrderLine.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | OrderLine·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | OrderLine·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | OrderLine·MISSING | Queue the missing OrderLine mapping or reject the command before linking. |
| Wrong scope | OrderLine·B01 | Do not attach another church’s OrderLine without a supported exchange and local authority. |
| Target rename | Rename OrderLine·A01 after linking | The existing order_line_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No order_line_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### subscription_term_id

The target is [SubscriptionTerm](SubscriptionTerm.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | SubscriptionTerm·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | SubscriptionTerm·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | SubscriptionTerm·MISSING | Queue the missing SubscriptionTerm mapping or reject the command before linking. |
| Wrong scope | SubscriptionTerm·B01 | Do not attach another church’s SubscriptionTerm without a supported exchange and local authority. |
| Target rename | Rename SubscriptionTerm·A01 after linking | The existing subscription_term_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No subscription_term_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### approval_ref

Use scoped or external reference for `AccessGrant.approval_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified approval_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped approval_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No approval_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### starts_at

Use unambiguous point in time for `AccessGrant.starts_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No starts_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### ends_at

Use unambiguous point in time for `AccessGrant.ends_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No ends_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### activation_deadline

Use unambiguous point in time for `AccessGrant.activation_deadline`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No activation_deadline provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### activated_at

Use unambiguous point in time for `AccessGrant.activated_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No activated_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### granted_units

Use whole-number measure for `AccessGrant.granted_units`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No granted_units at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### state

Declared alternatives in owner order: `awaiting_claim`, `pending_start`, `active`, `suspended`, `expired`, `revoked`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | awaiting_claim | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### reason

Use versioned classification or status code for `AccessGrant.reason`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active reason code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped reason code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No reason provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### source_action_key

Use human-readable text for `AccessGrant.source_action_key`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered source_action_key in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No source_action_key at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AccessDecision](AccessDecision.md).`grant_id` | AccessGrant identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AccessException](AccessException.md).`grant_id` | AccessGrant identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FulfilmentLine](FulfilmentLine.md).`access_grant_id` | AccessGrant identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GrantAction](GrantAction.md).`grant_id` | AccessGrant identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PlaybackSession](PlaybackSession.md).`grant_id` | AccessGrant identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SeatAssignment](SeatAssignment.md).`grant_id` | AccessGrant identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
