# PreservationCheck

[Documents, archives, certificates and custody](../../administration/archives.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Do not replace a damaged master without preserving the evidence and decision. A redacted working copy is unsuitable as a preservation master.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | Owner-scoped business value; see the record rule | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `copy_id` | → ArchiveCopy | Required at applicable lifecycle step | [relation](../value-conventions.md#relation) |
| `due_on` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [date](../value-conventions.md#date) |
| `performed_at` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [instant](../value-conventions.md#instant) |
| `expected_digest` | optional | Optional under owner conditions | [digest](../value-conventions.md#digest) |
| `observed_digest` | optional | Optional under owner conditions | [digest](../value-conventions.md#digest) |
| `condition_grade` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [structured](../value-conventions.md#structured) |
| `result` | pass, repair, unreadable or mismatch | Required at applicable lifecycle step | [enum](../value-conventions.md#enum) |
| `replacement_copy_id` | → ArchiveCopy | Required at applicable lifecycle step | [relation](../value-conventions.md#relation) |
| `reported_by` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `PreservationCheck.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | PreservationCheck·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### copy_id

The target is [ArchiveCopy](ArchiveCopy.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ArchiveCopy·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ArchiveCopy·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ArchiveCopy·MISSING | Queue the missing ArchiveCopy mapping or reject the command before linking. |
| Wrong scope | ArchiveCopy·B01 | Do not attach another church’s ArchiveCopy without a supported exchange and local authority. |
| Target rename | Rename ArchiveCopy·A01 after linking | The existing copy_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No copy_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### due_on

Use civil calendar date for `PreservationCheck.due_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No due_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### performed_at

Use unambiguous point in time for `PreservationCheck.performed_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No performed_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### expected_digest

Use integrity fingerprint or opaque verifier for `PreservationCheck.expected_digest`. Bind the algorithm or verifier scheme and object revision to the evidence.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified fingerprint of edition A | Bind the algorithm or verifier scheme and object revision to the evidence. |
| Malformed or unmapped | different fingerprint for the same purported bytes | Quarantine the mismatch or deny the claim. |
| An identical copy is rechecked | compare original bytes with verified copy | Equality confirms the checked bytes or verifier under the same scheme only. |
| New revision has changed content | different bytes under a new edition | Compute new evidence; preserve the prior verified revision. |
| A user knows a digest | unprivileged user presents a publicly observed fingerprint | Knowledge alone grants no additional access outside the documented token protocol. |
| Absent in intake | No expected_digest provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### observed_digest

Use integrity fingerprint or opaque verifier for `PreservationCheck.observed_digest`. Bind the algorithm or verifier scheme and object revision to the evidence.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified fingerprint of edition A | Bind the algorithm or verifier scheme and object revision to the evidence. |
| Malformed or unmapped | different fingerprint for the same purported bytes | Quarantine the mismatch or deny the claim. |
| An identical copy is rechecked | compare original bytes with verified copy | Equality confirms the checked bytes or verifier under the same scheme only. |
| New revision has changed content | different bytes under a new edition | Compute new evidence; preserve the prior verified revision. |
| A user knows a digest | unprivileged user presents a publicly observed fingerprint | Knowledge alone grants no additional access outside the documented token protocol. |
| Absent in intake | No observed_digest provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### condition_grade

Use typed value or bounded compound record for `PreservationCheck.condition_grade`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of condition_grade matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for condition_grade | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Incomplete record | No condition_grade at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### result

Declared alternatives in owner order: `pass`, `repair`, `unreadable`, `mismatch`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | pass | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_result | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No result at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### replacement_copy_id

The target is [ArchiveCopy](ArchiveCopy.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ArchiveCopy·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ArchiveCopy·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ArchiveCopy·MISSING | Queue the missing ArchiveCopy mapping or reject the command before linking. |
| Wrong scope | ArchiveCopy·B01 | Do not attach another church’s ArchiveCopy without a supported exchange and local authority. |
| Target rename | Rename ArchiveCopy·A01 after linking | The existing replacement_copy_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No replacement_copy_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### reported_by

Use scoped or external reference for `PreservationCheck.reported_by`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified reported_by in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped reported_by | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No reported_by at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
