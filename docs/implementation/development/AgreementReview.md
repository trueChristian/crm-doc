# AgreementReview

[Partnerships, sponsorships and impact](../../development/partnerships.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Separate safeguarding cases, complaints and financial exceptions remain with the relevant domain. Record only the agreement's practical response and internal authority.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `agreement_id` | ref PartnershipAgreement | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `scheduled_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `reviewer_id` | ref UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `delivery_summary` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `exception_summary` | protected_text? | Optional under owner conditions | [protected](../value-conventions.md#protected) |
| `change_decision` | continue/remediate/suspend/terminate/renew | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `decision_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `next_review_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### agreement_id

The target is [PartnershipAgreement](PartnershipAgreement.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | PartnershipAgreement·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | PartnershipAgreement·MISSING | Queue the missing PartnershipAgreement mapping or reject the command before linking. |
| Wrong scope | PartnershipAgreement·B01 | Do not attach another church’s PartnershipAgreement without a supported exchange and local authority. |
| Target rename | Rename PartnershipAgreement·A01 after linking | The existing agreement_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No agreement_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### scheduled_on

Use civil calendar date for `AgreementReview.scheduled_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No scheduled_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### reviewer_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing reviewer_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No reviewer_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### delivery_summary

Use human-readable text for `AgreementReview.delivery_summary`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered delivery_summary in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No delivery_summary at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### exception_summary

Use restricted value or protected content reference for `AgreementReview.exception_summary`. Keep value and purpose together; apply field-level authority to projections.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted exception_summary supplied in a restricted context | Keep value and purpose together; apply field-level authority to projections. |
| Malformed or unmapped | public disclosure without authority | Withhold publication unless the specific disclosure rule permits it. |
| Search snippet or autocomplete | restricted fact returned in type-ahead search | Filter before returning any protected content or revealing its existence. |
| Authorized report excludes this field | otherwise permitted export excludes the restricted field | Omit it from hidden metadata and attachments as well. |
| Approval withdrawn after a preview | draft was previewed before authority was withdrawn | Recheck at release; keep only permitted audit evidence. |
| Absent in intake | No exception_summary provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### change_decision

Declared alternatives in owner order: `continue`, `remediate`, `suspend`, `terminate`, `renew`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | continue | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_change_decision | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No change_decision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### decision_ref

Use scoped or external reference for `AgreementReview.decision_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified decision_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped decision_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No decision_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### next_review_on

Use civil calendar date for `AgreementReview.next_review_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No next_review_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
