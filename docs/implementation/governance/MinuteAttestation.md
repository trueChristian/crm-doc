# MinuteAttestation

[Minutes, resolutions and the archive](../../governance/minutes-and-resolutions.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Each required attestor signs the same revision. Returning a draft records the reason. A changed draft invalidates previous approvals for the superseded digest.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `edition_id` | MinuteEdition ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `attestor_id` | Person ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `attesting_office_id` | OfficeTerm ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `role` | preparer/chair/confirmer/witness | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `decision` | approve/return/confirm | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `signed_digest` | text | Required when the record reaches its applicable state | [digest](../value-conventions.md#digest) |
| `signed_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `evidence_ref` | text? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `comment` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### edition_id

The target is [MinuteEdition](MinuteEdition.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MinuteEdition·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | MinuteEdition·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | MinuteEdition·MISSING | Queue the missing MinuteEdition mapping or reject the command before linking. |
| Wrong scope | MinuteEdition·B01 | Do not attach another church’s MinuteEdition without a supported exchange and local authority. |
| Target rename | Rename MinuteEdition·A01 after linking | The existing edition_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No edition_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### attestor_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing attestor_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No attestor_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### attesting_office_id

The target is [OfficeTerm](OfficeTerm.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | OfficeTerm·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | OfficeTerm·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | OfficeTerm·MISSING | Queue the missing OfficeTerm mapping or reject the command before linking. |
| Wrong scope | OfficeTerm·B01 | Do not attach another church’s OfficeTerm without a supported exchange and local authority. |
| Target rename | Rename OfficeTerm·A01 after linking | The existing attesting_office_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No attesting_office_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### role

Declared alternatives in owner order: `preparer`, `chair`, `confirmer`, `witness`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | preparer | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_role | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No role at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### decision

Declared alternatives in owner order: `approve`, `return`, `confirm`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | approve | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_decision | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No decision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### signed_digest

Use integrity fingerprint or opaque verifier for `MinuteAttestation.signed_digest`. Bind the algorithm or verifier scheme and object revision to the evidence.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified fingerprint of edition A | Bind the algorithm or verifier scheme and object revision to the evidence. |
| Malformed or unmapped | different fingerprint for the same purported bytes | Quarantine the mismatch or deny the claim. |
| An identical copy is rechecked | compare original bytes with verified copy | Equality confirms the checked bytes or verifier under the same scheme only. |
| New revision has changed content | different bytes under a new edition | Compute new evidence; preserve the prior verified revision. |
| A user knows a digest | unprivileged user presents a publicly observed fingerprint | Knowledge alone grants no additional access outside the documented token protocol. |
| Incomplete record | No signed_digest at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### signed_at

Use unambiguous point in time for `MinuteAttestation.signed_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No signed_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### evidence_ref

Use scoped or external reference for `MinuteAttestation.evidence_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified evidence_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped evidence_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No evidence_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### comment

Use human-readable text for `MinuteAttestation.comment`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered comment in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No comment provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
