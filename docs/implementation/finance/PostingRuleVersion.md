# PostingRuleVersion

[Books, dimensions and double entry](../../finance/ledger.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One applicable published version per event/date/policy. Preserve the rule used. New versions require sample posting checks and approval.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `book_id` | → FinanceBook | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `event_kind` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `version` | integer | Required when the record reaches its applicable state | [version](../value-conventions.md#version) |
| `valid_from` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `valid_until` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `debit_map` | configuration | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `credit_map` | configuration | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `dimension_rules` | configuration | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `approval_policy` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `approved_by` | → UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### book_id

The target is [FinanceBook](FinanceBook.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FinanceBook·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | FinanceBook·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | FinanceBook·MISSING | Queue the missing FinanceBook mapping or reject the command before linking. |
| Wrong scope | FinanceBook·B01 | Do not attach another church’s FinanceBook without a supported exchange and local authority. |
| Target rename | Rename FinanceBook·A01 after linking | The existing book_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No book_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### event_kind

Use versioned classification or status code for `PostingRuleVersion.event_kind`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active event_kind code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped event_kind code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No event_kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### version

Use revision number or opaque revision token for `PostingRuleVersion.version`. Compare under the declared revision scheme. Require the expected version for conflicting work.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | the current revision returned by the owner | Compare under the declared revision scheme. Require the expected version for conflicting work. |
| Malformed or unmapped | superseded version presented for a new approval | Reject or reopen review against the current contents. |
| Two operators begin at revision seven | two edits both cite baseline 7 | Commit the first change once and re-evaluate the second; never overwrite an unreviewed difference. |
| Re-read an already approved revision | re-open issued revision 4 after revision 6 | Return the frozen value and evidence for that edition. |
| Replay of an earlier result | same business operation observed at two revisions | Correlate by the business operation identity; a newer version does not create a second effect. |
| Incomplete record | No version at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### valid_from

Use civil calendar date for `PostingRuleVersion.valid_from`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No valid_from at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### valid_until

Use civil calendar date for `PostingRuleVersion.valid_until`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No valid_until provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### debit_map

Use exact decimal measure for `PostingRuleVersion.debit_map`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No debit_map at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### credit_map

Use exact decimal measure for `PostingRuleVersion.credit_map`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No credit_map at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### dimension_rules

Use exact decimal measure for `PostingRuleVersion.dimension_rules`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No dimension_rules at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### approval_policy

Use versioned classification or status code for `PostingRuleVersion.approval_policy`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active approval_policy code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped approval_policy code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No approval_policy at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### approved_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing approved_by keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No approved_by at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
