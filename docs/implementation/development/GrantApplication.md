# GrantApplication

[Grant applications and reporting](../../development/grant-applications.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Each submitted revision links to the same application, with sponsor acknowledgement. A multi-project application adds scoped budget lines for each approved project. Partial award needs review against reduced scope.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `opportunity_id` | ref FundingOpportunity | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `project_id` | ref MissionProject | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `submission_reference` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `requested_amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `currency` | code | Required when the record reaches its applicable state | [currency](../value-conventions.md#currency) |
| `proposed_start` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `proposed_end` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `coordinator_id` | ref UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `signatory_id` | ref UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `status` | draft/review/approved/submitted/clarification/accepted/part_awarded/rejected/withdrawn | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `decision_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `award_id` | ref GrantAward? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### opportunity_id

The target is [FundingOpportunity](FundingOpportunity.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FundingOpportunity·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | FundingOpportunity·MISSING | Queue the missing FundingOpportunity mapping or reject the command before linking. |
| Wrong scope | FundingOpportunity·B01 | Do not attach another church’s FundingOpportunity without a supported exchange and local authority. |
| Target rename | Rename FundingOpportunity·A01 after linking | The existing opportunity_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No opportunity_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### project_id

The target is [MissionProject](../ministry/MissionProject.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MissionProject·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | MissionProject·MISSING | Queue the missing MissionProject mapping or reject the command before linking. |
| Wrong scope | MissionProject·B01 | Do not attach another church’s MissionProject without a supported exchange and local authority. |
| Target rename | Rename MissionProject·A01 after linking | The existing project_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No project_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### submission_reference

Use human-readable text for `GrantApplication.submission_reference`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered submission_reference in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No submission_reference provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### requested_amount

Use exact monetary amount with currency for `GrantApplication.requested_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No requested_amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### currency

Use monetary unit code for `GrantApplication.currency`. Resolve the code and its precision as of the transaction.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD | Resolve the code and its precision as of the transaction. |
| Malformed or unmapped | ambiguous $ | Request the unambiguous currency. |
| Two amounts have different currencies | 24.50 NAD and 24.50 USD | Report separate totals or translate using recorded rates. |
| Catalog changes after document issue | document issued before currency-profile revision | The stored document keeps its currency. |
| Unrecognized imported code | unmapped monetary unit in staged transaction | Hold the row for currency mapping before an amount-dependent approval or exchange. |
| Incomplete record | No currency at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### proposed_start

Use civil calendar date for `GrantApplication.proposed_start`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No proposed_start at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### proposed_end

Use civil calendar date for `GrantApplication.proposed_end`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No proposed_end at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### coordinator_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing coordinator_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No coordinator_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### signatory_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing signatory_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No signatory_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### status

Declared alternatives in owner order: `draft`, `review`, `approved`, `submitted`, `clarification`, `accepted`, `part_awarded`, `rejected`, `withdrawn`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | draft | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_status | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No status at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### decision_at

Use unambiguous point in time for `GrantApplication.decision_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No decision_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### award_id

The target is [GrantAward](../finance/GrantAward.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GrantAward·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | GrantAward·MISSING | Queue the missing GrantAward mapping or reject the command before linking. |
| Wrong scope | GrantAward·B01 | Do not attach another church’s GrantAward without a supported exchange and local authority. |
| Target rename | Rename GrantAward·A01 after linking | The existing award_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No award_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AwardDecisionReview](AwardDecisionReview.md).`application_id` | GrantApplication identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProposalBudgetLine](ProposalBudgetLine.md).`application_id` | GrantApplication identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProposalEdition](ProposalEdition.md).`application_id` | GrantApplication identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProposalRequirement](ProposalRequirement.md).`application_id` | GrantApplication identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
