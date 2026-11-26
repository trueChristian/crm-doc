# MembershipTransfer

[Membership, transfers and certified rolls](../../people/membership-and-rolls.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

An internal transfer references two distinct congregations. External side may be identified by a supplied name. Completion records the effective decision(s) according to policy. A letter alone is not proof of acceptance.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | ID | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `person_id` | → Person | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `source_congregation_id` | → Congregation? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `destination_congregation_id` | → Congregation? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `external_church_label` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `direction` | enum(incoming, outgoing, internal) | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `requested_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `issued_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `acknowledged_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `consent_or_authority_ref` | ID | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `evidence_ref` | ID? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `state` | enum(requested, prepared, issued, acknowledged, completed, cancelled, disputed) | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `exit_decision_id` | → MembershipDecision? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `entry_decision_id` | → MembershipDecision? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `MembershipTransfer.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MembershipTransfer·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### person_id

The target is [Person](Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing person_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No person_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### source_congregation_id

The target is [Congregation](../foundation/Congregation.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Congregation·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Congregation·MISSING | Queue the missing Congregation mapping or reject the command before linking. |
| Wrong scope | Congregation·B01 | Do not attach another church’s Congregation without a supported exchange and local authority. |
| Target rename | Rename Congregation·A01 after linking | The existing source_congregation_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No source_congregation_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### destination_congregation_id

The target is [Congregation](../foundation/Congregation.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Congregation·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Congregation·MISSING | Queue the missing Congregation mapping or reject the command before linking. |
| Wrong scope | Congregation·B01 | Do not attach another church’s Congregation without a supported exchange and local authority. |
| Target rename | Rename Congregation·A01 after linking | The existing destination_congregation_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No destination_congregation_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### external_church_label

Use human-readable text for `MembershipTransfer.external_church_label`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered external_church_label in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No external_church_label provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### direction

Declared alternatives in owner order: `incoming`, `outgoing`, `internal`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | incoming | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_direction | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No direction at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### requested_on

Use civil calendar date for `MembershipTransfer.requested_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No requested_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### issued_on

Use civil calendar date for `MembershipTransfer.issued_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No issued_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### acknowledged_on

Use civil calendar date for `MembershipTransfer.acknowledged_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No acknowledged_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### consent_or_authority_ref

Use scoped or external reference for `MembershipTransfer.consent_or_authority_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified consent_or_authority_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped consent_or_authority_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No consent_or_authority_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### evidence_ref

Use scoped or external reference for `MembershipTransfer.evidence_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified evidence_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped evidence_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No evidence_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Declared alternatives in owner order: `requested`, `prepared`, `issued`, `acknowledged`, `completed`, `cancelled`, `disputed`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | requested | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### exit_decision_id

The target is [MembershipDecision](MembershipDecision.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MembershipDecision·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | MembershipDecision·MISSING | Queue the missing MembershipDecision mapping or reject the command before linking. |
| Wrong scope | MembershipDecision·B01 | Do not attach another church’s MembershipDecision without a supported exchange and local authority. |
| Target rename | Rename MembershipDecision·A01 after linking | The existing exit_decision_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No exit_decision_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### entry_decision_id

The target is [MembershipDecision](MembershipDecision.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MembershipDecision·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | MembershipDecision·MISSING | Queue the missing MembershipDecision mapping or reject the command before linking. |
| Wrong scope | MembershipDecision·B01 | Do not attach another church’s MembershipDecision without a supported exchange and local authority. |
| Target rename | Rename MembershipDecision·A01 after linking | The existing entry_decision_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No entry_decision_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
