# ReportSubmissionEdition

[Grant applications and reporting](../../development/grant-applications.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Freeze submission and retain sponsor response. Corrections link the earlier edition, record changed figures and require fresh approval.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `report_id` | ref SponsorReport | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `revision` | integer | Required when the record reaches its applicable state | [version](../value-conventions.md#version) |
| `evidence_bundle_ref` | opaque_ref | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `source_fingerprints` | text | Required when the record reaches its applicable state | [digest](../value-conventions.md#digest) |
| `reviewer_id` | ref UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `approved_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `submitted_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `submitted_by` | ref UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `receipt_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `response_due` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `response_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### report_id

The target is [SponsorReport](SponsorReport.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | SponsorReport·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | SponsorReport·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | SponsorReport·MISSING | Queue the missing SponsorReport mapping or reject the command before linking. |
| Wrong scope | SponsorReport·B01 | Do not attach another church’s SponsorReport without a supported exchange and local authority. |
| Target rename | Rename SponsorReport·A01 after linking | The existing report_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No report_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### revision

Use revision number or opaque revision token for `ReportSubmissionEdition.revision`. Compare under the declared revision scheme. Require the expected version for conflicting work.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | the current revision returned by the owner | Compare under the declared revision scheme. Require the expected version for conflicting work. |
| Malformed or unmapped | superseded version presented for a new approval | Reject or reopen review against the current contents. |
| Two operators begin at revision seven | two edits both cite baseline 7 | Commit the first change once and re-evaluate the second; never overwrite an unreviewed difference. |
| Re-read an already approved revision | re-open issued revision 4 after revision 6 | Return the frozen value and evidence for that edition. |
| Replay of an earlier result | same business operation observed at two revisions | Correlate by the business operation identity; a newer version does not create a second effect. |
| Incomplete record | No revision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### evidence_bundle_ref

Use scoped or external reference for `ReportSubmissionEdition.evidence_bundle_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified evidence_bundle_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped evidence_bundle_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No evidence_bundle_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### source_fingerprints

Use integrity fingerprint or opaque verifier for `ReportSubmissionEdition.source_fingerprints`. Bind the algorithm or verifier scheme and object revision to the evidence.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified fingerprint of edition A | Bind the algorithm or verifier scheme and object revision to the evidence. |
| Malformed or unmapped | different fingerprint for the same purported bytes | Quarantine the mismatch or deny the claim. |
| An identical copy is rechecked | compare original bytes with verified copy | Equality confirms the checked bytes or verifier under the same scheme only. |
| New revision has changed content | different bytes under a new edition | Compute new evidence; preserve the prior verified revision. |
| A user knows a digest | unprivileged user presents a publicly observed fingerprint | Knowledge alone grants no additional access outside the documented token protocol. |
| Incomplete record | No source_fingerprints at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### reviewer_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing reviewer_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No reviewer_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### approved_at

Use unambiguous point in time for `ReportSubmissionEdition.approved_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No approved_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### submitted_at

Use unambiguous point in time for `ReportSubmissionEdition.submitted_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

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

### receipt_ref

Use scoped or external reference for `ReportSubmissionEdition.receipt_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified receipt_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped receipt_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No receipt_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### response_due

Use civil calendar date for `ReportSubmissionEdition.response_due`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No response_due provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### response_ref

Use scoped or external reference for `ReportSubmissionEdition.response_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified response_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped response_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No response_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
