# AssistanceRound

[Agreements, service rounds and relief distribution](../../administration/community-programs.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One round can accept many applications. Opening, closing intake and completing reconciliation are independent transitions.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | Owner-scoped business value; see the record rule | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `terms_id` | → ProgramServiceTerms | Required at applicable lifecycle step | [relation](../value-conventions.md#relation) |
| `intake_opens_at` | instants | Required at applicable lifecycle step | [instant](../value-conventions.md#instant) |
| `intake_closes_at` | instants | Required at applicable lifecycle step | [instant](../value-conventions.md#instant) |
| `service_date` | date | Required at applicable lifecycle step | [date](../value-conventions.md#date) |
| `distribution_id` | → CommunityDistribution optional | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `unit_kind` | parcel, voucher, visit, scholarship or service | Required at applicable lifecycle step | [enum](../value-conventions.md#enum) |
| `capacity` | count | Required at applicable lifecycle step | [integer](../value-conventions.md#integer) |
| `coordinator` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [resource](../value-conventions.md#resource) |
| `state` | draft, open, paused, closed, reconciled | Required at applicable lifecycle step | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `AssistanceRound.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AssistanceRound·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### terms_id

The target is [ProgramServiceTerms](ProgramServiceTerms.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ProgramServiceTerms·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | ProgramServiceTerms·MISSING | Queue the missing ProgramServiceTerms mapping or reject the command before linking. |
| Wrong scope | ProgramServiceTerms·B01 | Do not attach another church’s ProgramServiceTerms without a supported exchange and local authority. |
| Target rename | Rename ProgramServiceTerms·A01 after linking | The existing terms_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No terms_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### intake_opens_at

Use unambiguous point in time for `AssistanceRound.intake_opens_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No intake_opens_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### intake_closes_at

Use unambiguous point in time for `AssistanceRound.intake_closes_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No intake_closes_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### service_date

Use civil calendar date for `AssistanceRound.service_date`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No service_date at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### distribution_id

The target is [CommunityDistribution](../ministry/CommunityDistribution.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CommunityDistribution·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | CommunityDistribution·MISSING | Queue the missing CommunityDistribution mapping or reject the command before linking. |
| Wrong scope | CommunityDistribution·B01 | Do not attach another church’s CommunityDistribution without a supported exchange and local authority. |
| Target rename | Rename CommunityDistribution·A01 after linking | The existing distribution_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No distribution_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### unit_kind

Declared alternatives in owner order: `parcel`, `voucher`, `visit`, `scholarship`, `service`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | parcel | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_unit_kind | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No unit_kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### capacity

Use whole-number measure for `AssistanceRound.capacity`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No capacity at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### coordinator

Use scoped or external reference for `AssistanceRound.coordinator`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified coordinator in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped coordinator | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No coordinator at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### state

Declared alternatives in owner order: `draft`, `open`, `paused`, `closed`, `reconciled`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | draft | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [RoundPlacement](RoundPlacement.md).`round_id` | AssistanceRound identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
