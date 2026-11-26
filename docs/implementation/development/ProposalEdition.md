# ProposalEdition

[Grant applications and reporting](../../development/grant-applications.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique application/revision. A submitted edition is immutable. For duplicate transport acknowledgements retain one logical submission; an amended sponsor request gets a new edition.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `application_id` | ref GrantApplication | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `revision` | integer | Required when the record reaches its applicable state | [version](../value-conventions.md#version) |
| `created_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `approval_by` | ref UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `approval_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `package_ref` | opaque_ref | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `package_fingerprint` | text | Required when the record reaches its applicable state | [digest](../value-conventions.md#digest) |
| `submitted_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `submitted_by` | ref UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `sponsor_ack_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `supersedes_id` | ref ProposalEdition? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### application_id

The target is [GrantApplication](GrantApplication.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GrantApplication·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | GrantApplication·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | GrantApplication·MISSING | Queue the missing GrantApplication mapping or reject the command before linking. |
| Wrong scope | GrantApplication·B01 | Do not attach another church’s GrantApplication without a supported exchange and local authority. |
| Target rename | Rename GrantApplication·A01 after linking | The existing application_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No application_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### revision

Use revision number or opaque revision token for `ProposalEdition.revision`. Compare under the declared revision scheme. Require the expected version for conflicting work.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | the current revision returned by the owner | Compare under the declared revision scheme. Require the expected version for conflicting work. |
| Malformed or unmapped | superseded version presented for a new approval | Reject or reopen review against the current contents. |
| Two operators begin at revision seven | two edits both cite baseline 7 | Commit the first change once and re-evaluate the second; never overwrite an unreviewed difference. |
| Re-read an already approved revision | re-open issued revision 4 after revision 6 | Return the frozen value and evidence for that edition. |
| Replay of an earlier result | same business operation observed at two revisions | Correlate by the business operation identity; a newer version does not create a second effect. |
| Incomplete record | No revision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### created_at

Use unambiguous point in time for `ProposalEdition.created_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No created_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### approval_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing approval_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No approval_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### approval_at

Use unambiguous point in time for `ProposalEdition.approval_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No approval_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### package_ref

Use scoped or external reference for `ProposalEdition.package_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified package_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped package_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No package_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### package_fingerprint

Use integrity fingerprint or opaque verifier for `ProposalEdition.package_fingerprint`. Bind the algorithm or verifier scheme and object revision to the evidence.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified fingerprint of edition A | Bind the algorithm or verifier scheme and object revision to the evidence. |
| Malformed or unmapped | different fingerprint for the same purported bytes | Quarantine the mismatch or deny the claim. |
| An identical copy is rechecked | compare original bytes with verified copy | Equality confirms the checked bytes or verifier under the same scheme only. |
| New revision has changed content | different bytes under a new edition | Compute new evidence; preserve the prior verified revision. |
| A user knows a digest | unprivileged user presents a publicly observed fingerprint | Knowledge alone grants no additional access outside the documented token protocol. |
| Incomplete record | No package_fingerprint at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### submitted_at

Use unambiguous point in time for `ProposalEdition.submitted_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No submitted_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### submitted_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing submitted_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No submitted_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### sponsor_ack_ref

Use scoped or external reference for `ProposalEdition.sponsor_ack_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified sponsor_ack_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped sponsor_ack_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No sponsor_ack_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### supersedes_id

The target is [ProposalEdition](ProposalEdition.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ProposalEdition·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ProposalEdition·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ProposalEdition·MISSING | Queue the missing ProposalEdition mapping or reject the command before linking. |
| Wrong scope | ProposalEdition·B01 | Do not attach another church’s ProposalEdition without a supported exchange and local authority. |
| Target rename | Rename ProposalEdition·A01 after linking | The existing supersedes_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No supersedes_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [ProposalEdition](ProposalEdition.md).`supersedes_id` | ProposalEdition identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
