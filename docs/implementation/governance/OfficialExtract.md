# OfficialExtract

[Minutes, resolutions and the archive](../../governance/minutes-and-resolutions.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Copy reviewed text into the issued extract. A recipient should be able to verify which edition it came from. Removing access ends future retrieval, while the issue register records copies already released.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `issued_document_id` | DocumentIssue ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `edition_id` | MinuteEdition ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `item_id` | MinuteItem ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `recipient_scope` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `disclosure_basis` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `excerpt_text` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `attachment_manifest` | identifiers | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `issued_by` | Person ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `issued_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `digest` | text | Required when the record reaches its applicable state | [digest](../value-conventions.md#digest) |
| `withdrawn_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `replacement_id` | OfficialExtract ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### issued_document_id

The target is [DocumentIssue](../administration/DocumentIssue.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DocumentIssue·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | DocumentIssue·MISSING | Queue the missing DocumentIssue mapping or reject the command before linking. |
| Wrong scope | DocumentIssue·B01 | Do not attach another church’s DocumentIssue without a supported exchange and local authority. |
| Target rename | Rename DocumentIssue·A01 after linking | The existing issued_document_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No issued_document_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### edition_id

The target is [MinuteEdition](MinuteEdition.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MinuteEdition·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | MinuteEdition·MISSING | Queue the missing MinuteEdition mapping or reject the command before linking. |
| Wrong scope | MinuteEdition·B01 | Do not attach another church’s MinuteEdition without a supported exchange and local authority. |
| Target rename | Rename MinuteEdition·A01 after linking | The existing edition_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No edition_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### item_id

The target is [MinuteItem](MinuteItem.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MinuteItem·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | MinuteItem·MISSING | Queue the missing MinuteItem mapping or reject the command before linking. |
| Wrong scope | MinuteItem·B01 | Do not attach another church’s MinuteItem without a supported exchange and local authority. |
| Target rename | Rename MinuteItem·A01 after linking | The existing item_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No item_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### recipient_scope

Use human-readable text for `OfficialExtract.recipient_scope`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered recipient_scope in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No recipient_scope at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### disclosure_basis

Use human-readable text for `OfficialExtract.disclosure_basis`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered disclosure_basis in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No disclosure_basis at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### excerpt_text

Use human-readable text for `OfficialExtract.excerpt_text`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered excerpt_text in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No excerpt_text at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### attachment_manifest

Use scoped or external reference for `OfficialExtract.attachment_manifest`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified attachment_manifest in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped attachment_manifest | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No attachment_manifest at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### issued_by

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing issued_by keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No issued_by at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### issued_at

Use unambiguous point in time for `OfficialExtract.issued_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No issued_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### digest

Use integrity fingerprint or opaque verifier for `OfficialExtract.digest`. Bind the algorithm or verifier scheme and object revision to the evidence.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified fingerprint of edition A | Bind the algorithm or verifier scheme and object revision to the evidence. |
| Malformed or unmapped | different fingerprint for the same purported bytes | Quarantine the mismatch or deny the claim. |
| An identical copy is rechecked | compare original bytes with verified copy | Equality confirms the checked bytes or verifier under the same scheme only. |
| New revision has changed content | different bytes under a new edition | Compute new evidence; preserve the prior verified revision. |
| A user knows a digest | unprivileged user presents a publicly observed fingerprint | Knowledge alone grants no additional access outside the documented token protocol. |
| Incomplete record | No digest at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### withdrawn_at

Use unambiguous point in time for `OfficialExtract.withdrawn_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No withdrawn_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### replacement_id

The target is [OfficialExtract](OfficialExtract.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | OfficialExtract·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | OfficialExtract·MISSING | Queue the missing OfficialExtract mapping or reject the command before linking. |
| Wrong scope | OfficialExtract·B01 | Do not attach another church’s OfficialExtract without a supported exchange and local authority. |
| Target rename | Rename OfficialExtract·A01 after linking | The existing replacement_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No replacement_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [GovernanceReview](GovernanceReview.md).`released_extract_id` | OfficialExtract identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OfficialExtract](OfficialExtract.md).`replacement_id` | OfficialExtract identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
