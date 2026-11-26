# AppealGoal

[Appeals and attribution](../../development/appeals.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Each goal declares eligibility, refund treatment, as-of policy and unit. Cash and goods can have separate goals. Amendments preserve earlier public targets.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `appeal_id` | ref FundraisingAppeal | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `measure` | settled_cash/confirmed_pledges/eligible_goods/participants/fulfilled_match | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `target_quantity` | decimal | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `unit` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `currency` | code? | Optional under owner conditions | [currency](../value-conventions.md#currency) |
| `due_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `reporting_basis` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `revision` | integer | Required when the record reaches its applicable state | [version](../value-conventions.md#version) |
| `approved_by` | ref UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### appeal_id

The target is [FundraisingAppeal](FundraisingAppeal.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FundraisingAppeal·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | FundraisingAppeal·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | FundraisingAppeal·MISSING | Queue the missing FundraisingAppeal mapping or reject the command before linking. |
| Wrong scope | FundraisingAppeal·B01 | Do not attach another church’s FundraisingAppeal without a supported exchange and local authority. |
| Target rename | Rename FundraisingAppeal·A01 after linking | The existing appeal_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No appeal_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### measure

Declared alternatives in owner order: `settled_cash`, `confirmed_pledges`, `eligible_goods`, `participants`, `fulfilled_match`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | settled_cash | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_measure | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No measure at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### target_quantity

Use exact decimal measure for `AppealGoal.target_quantity`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No target_quantity at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### unit

Use versioned classification or status code for `AppealGoal.unit`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active unit code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped unit code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No unit at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### currency

Use monetary unit code for `AppealGoal.currency`. Resolve the code and its precision as of the transaction.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD | Resolve the code and its precision as of the transaction. |
| Malformed or unmapped | ambiguous $ | Request the unambiguous currency. |
| Two amounts have different currencies | 24.50 NAD and 24.50 USD | Report separate totals or translate using recorded rates. |
| Catalog changes after document issue | document issued before currency-profile revision | The stored document keeps its currency. |
| Unrecognized imported code | unmapped monetary unit in staged transaction | Stage unmapped currency; block financial posting. |
| Absent in intake | No currency provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### due_on

Use civil calendar date for `AppealGoal.due_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No due_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### reporting_basis

Use human-readable text for `AppealGoal.reporting_basis`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered reporting_basis in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No reporting_basis at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### revision

Use revision number or opaque revision token for `AppealGoal.revision`. Compare under the declared revision scheme. Require the expected version for conflicting work.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | the current revision returned by the owner | Compare under the declared revision scheme. Require the expected version for conflicting work. |
| Malformed or unmapped | superseded version presented for a new approval | Reject or reopen review against the current contents. |
| Two operators begin at revision seven | two edits both cite baseline 7 | Commit the first change once and re-evaluate the second; never overwrite an unreviewed difference. |
| Re-read an already approved revision | re-open issued revision 4 after revision 6 | Return the frozen value and evidence for that edition. |
| Replay of an earlier result | same business operation observed at two revisions | Correlate by the business operation identity; a newer version does not create a second effect. |
| Incomplete record | No revision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

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

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AppealSnapshot](AppealSnapshot.md).`goal_id` | AppealGoal identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ImpactEvidenceLine](ImpactEvidenceLine.md).`goal_id` | AppealGoal identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
