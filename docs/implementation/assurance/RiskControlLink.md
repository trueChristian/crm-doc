# RiskControlLink

[Risk ownership, control testing and prevention](../../assurance/risk-and-prevention.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Many-to-many dated relationship; prevent overlapping duplicate links.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | ID | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `risk_id` | → RiskEntry | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `control_id` | → RiskControl | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `rationale` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `from_date` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `until_date` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `RiskControlLink.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | RiskControlLink·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### risk_id

The target is [RiskEntry](RiskEntry.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | RiskEntry·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | RiskEntry·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | RiskEntry·MISSING | Queue the missing RiskEntry mapping or reject the command before linking. |
| Wrong scope | RiskEntry·B01 | Do not attach another church’s RiskEntry without a supported exchange and local authority. |
| Target rename | Rename RiskEntry·A01 after linking | The existing risk_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No risk_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### control_id

The target is [RiskControl](RiskControl.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | RiskControl·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | RiskControl·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | RiskControl·MISSING | Queue the missing RiskControl mapping or reject the command before linking. |
| Wrong scope | RiskControl·B01 | Do not attach another church’s RiskControl without a supported exchange and local authority. |
| Target rename | Rename RiskControl·A01 after linking | The existing control_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No control_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### rationale

Use human-readable text for `RiskControlLink.rationale`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered rationale in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No rationale at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### from_date

Use civil calendar date for `RiskControlLink.from_date`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No from_date at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### until_date

Use civil calendar date for `RiskControlLink.until_date`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No until_date provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
