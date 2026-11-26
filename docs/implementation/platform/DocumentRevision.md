# DocumentRevision

[Configuration, reusable forms and document custody](../../platform/configuration-content.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Positive revision, nonnegative length. Immutable content within a revision. A quarantined upload stays unavailable.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `document_id` | Ref(DocumentRecord) | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `revision` | integer | Required when the record reaches its applicable state | [version](../value-conventions.md#version) |
| `file_ref` | protected content | Required when the record reaches its applicable state | [protected](../value-conventions.md#protected) |
| `display_filename` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `declared_format` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `verified_format` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `size_bytes` | integer | Required when the record reaches its applicable state | [filesize](../value-conventions.md#filesize) |
| `content_digest` | text | Required when the record reaches its applicable state | [digest](../value-conventions.md#digest) |
| `inspection_state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `uploaded_by` | Ref(UserAccount) | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `uploaded_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `approved_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### document_id

The target is [DocumentRecord](DocumentRecord.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DocumentRecord·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | DocumentRecord·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | DocumentRecord·MISSING | Queue the missing DocumentRecord mapping or reject the command before linking. |
| Wrong scope | DocumentRecord·B01 | Do not attach another church’s DocumentRecord without a supported exchange and local authority. |
| Target rename | Rename DocumentRecord·A01 after linking | The existing document_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No document_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### revision

Use revision number or opaque revision token for `DocumentRevision.revision`. Compare under the declared revision scheme. Require the expected version for conflicting work.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | the current revision returned by the owner | Compare under the declared revision scheme. Require the expected version for conflicting work. |
| Malformed or unmapped | superseded version presented for a new approval | Reject or reopen review against the current contents. |
| Two operators begin at revision seven | two edits both cite baseline 7 | Commit the first change once and re-evaluate the second; never overwrite an unreviewed difference. |
| Re-read an already approved revision | re-open issued revision 4 after revision 6 | Return the frozen value and evidence for that edition. |
| Replay of an earlier result | same business operation observed at two revisions | Correlate by the business operation identity; a newer version does not create a second effect. |
| Incomplete record | No revision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### file_ref

Use restricted value or protected content reference for `DocumentRevision.file_ref`. Keep value and purpose together; apply field-level authority to projections.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted file_ref supplied in a restricted context | Keep value and purpose together; apply field-level authority to projections. |
| Malformed or unmapped | public disclosure without authority | Withhold publication unless the specific disclosure rule permits it. |
| Search snippet or autocomplete | restricted fact returned in type-ahead search | Filter before returning any protected content or revealing its existence. |
| Authorized report excludes this field | otherwise permitted export excludes the restricted field | Omit it from hidden metadata and attachments as well. |
| Approval withdrawn after a preview | draft was previewed before authority was withdrawn | Recheck at release; keep only permitted audit evidence. |
| Incomplete record | No file_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### display_filename

Use human-readable text for `DocumentRevision.display_filename`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered display_filename in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No display_filename at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### declared_format

Use versioned classification or status code for `DocumentRevision.declared_format`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active declared_format code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped declared_format code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No declared_format at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### verified_format

Use versioned classification or status code for `DocumentRevision.verified_format`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active verified_format code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped verified_format code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No verified_format provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### size_bytes

Use nonnegative whole byte count for `DocumentRevision.size_bytes`. Compare against the inspected payload, configured size limit and verified content reference.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 512 measured bytes | Compare against the inspected payload, configured size limit and verified content reference. |
| Malformed or unmapped | negative or fractional byte count | Reject impossible measurement. |
| Empty file | 0 bytes measured | Record zero bytes and apply permitted file-type/content rules. |
| Reported length differs from stored bytes | 512 reported and 509 measured | Withhold release and require reinspection. |
| Maximum permitted size | limit L bytes and measured length L + 1 | Check equality and the one-byte-over case at intake. |
| Incomplete record | No size_bytes at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### content_digest

Use integrity fingerprint or opaque verifier for `DocumentRevision.content_digest`. Bind the algorithm or verifier scheme and object revision to the evidence.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified fingerprint of edition A | Bind the algorithm or verifier scheme and object revision to the evidence. |
| Malformed or unmapped | different fingerprint for the same purported bytes | Quarantine the mismatch or deny the claim. |
| An identical copy is rechecked | compare original bytes with verified copy | Equality confirms the checked bytes or verifier under the same scheme only. |
| New revision has changed content | different bytes under a new edition | Compute new evidence; preserve the prior verified revision. |
| A user knows a digest | unprivileged user presents a publicly observed fingerprint | Knowledge alone grants no additional access outside the documented token protocol. |
| Incomplete record | No content_digest at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### inspection_state

Use versioned classification or status code for `DocumentRevision.inspection_state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active inspection_state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped inspection_state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No inspection_state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### uploaded_by

The target is [UserAccount](UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing uploaded_by keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No uploaded_by at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### uploaded_at

Use unambiguous point in time for `DocumentRevision.uploaded_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No uploaded_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### approved_at

Use unambiguous point in time for `DocumentRevision.approved_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No approved_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [DocumentRecord](DocumentRecord.md).`current_revision_id` | DocumentRevision identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
