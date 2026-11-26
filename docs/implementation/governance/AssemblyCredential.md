# AssemblyCredential

[Annual assemblies, policies and review](../../governance/annual-cycle-and-policy.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Respect the sending body's quota and replacements. Cross-organization assemblies receive an authorized minimum credential or certified extract only. A delegate's local contact list and membership record remain with the originating organization.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `meeting_id` | GovernanceMeeting ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `sending_body_id` | GoverningBody ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `delegate_person_id` | Person ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `substitute_for_id` | AssemblyCredential ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `appointment_evidence` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `class` | voting/observer/adviser | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `capacity_basis` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `certified_by` | Person ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `certified_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `withdrawn_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `roll_entry_id` | VotingRollEntry ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### meeting_id

The target is [GovernanceMeeting](GovernanceMeeting.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GovernanceMeeting·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | GovernanceMeeting·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | GovernanceMeeting·MISSING | Queue the missing GovernanceMeeting mapping or reject the command before linking. |
| Wrong scope | GovernanceMeeting·B01 | Do not attach another church’s GovernanceMeeting without a supported exchange and local authority. |
| Target rename | Rename GovernanceMeeting·A01 after linking | The existing meeting_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No meeting_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### sending_body_id

The target is [GoverningBody](GoverningBody.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GoverningBody·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | GoverningBody·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | GoverningBody·MISSING | Queue the missing GoverningBody mapping or reject the command before linking. |
| Wrong scope | GoverningBody·B01 | Do not attach another church’s GoverningBody without a supported exchange and local authority. |
| Target rename | Rename GoverningBody·A01 after linking | The existing sending_body_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No sending_body_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### delegate_person_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing delegate_person_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No delegate_person_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### substitute_for_id

The target is [AssemblyCredential](AssemblyCredential.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AssemblyCredential·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | AssemblyCredential·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | AssemblyCredential·MISSING | Queue the missing AssemblyCredential mapping or reject the command before linking. |
| Wrong scope | AssemblyCredential·B01 | Do not attach another church’s AssemblyCredential without a supported exchange and local authority. |
| Target rename | Rename AssemblyCredential·A01 after linking | The existing substitute_for_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No substitute_for_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### appointment_evidence

Use human-readable text for `AssemblyCredential.appointment_evidence`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered appointment_evidence in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No appointment_evidence at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### class

Declared alternatives in owner order: `voting`, `observer`, `adviser`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | voting | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_class | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No class at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### capacity_basis

Use human-readable text for `AssemblyCredential.capacity_basis`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered capacity_basis in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No capacity_basis at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### certified_by

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing certified_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No certified_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### certified_at

Use unambiguous point in time for `AssemblyCredential.certified_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No certified_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### withdrawn_at

Use unambiguous point in time for `AssemblyCredential.withdrawn_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No withdrawn_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### roll_entry_id

The target is [VotingRollEntry](VotingRollEntry.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | VotingRollEntry·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | VotingRollEntry·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | VotingRollEntry·MISSING | Queue the missing VotingRollEntry mapping or reject the command before linking. |
| Wrong scope | VotingRollEntry·B01 | Do not attach another church’s VotingRollEntry without a supported exchange and local authority. |
| Target rename | Rename VotingRollEntry·A01 after linking | The existing roll_entry_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No roll_entry_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AssemblyCredential](AssemblyCredential.md).`substitute_for_id` | AssemblyCredential identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
