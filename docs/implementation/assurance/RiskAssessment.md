# RiskAssessment

[Risk ownership, control testing and prevention](../../assurance/risk-and-prevention.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Inherent assessment precedes controls. Residual assessment takes only evidenced controls into account. Unknown residual impact remains unknown; it cannot become a green rating. Store separate impact dimensions when the method requires them.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | ID | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `risk_id` | → RiskEntry | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `method_id` | → RiskMethod | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `assessed_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `horizon_end` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `inherent_likelihood` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `inherent_impact` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `residual_likelihood` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `residual_impact` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `confidence` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `assumptions` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `evidence_ref` | ID? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `assessed_by` | → UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `reviewed_by` | → UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `review_due_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `RiskAssessment.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | RiskAssessment·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
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

### method_id

The target is [RiskMethod](RiskMethod.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | RiskMethod·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | RiskMethod·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | RiskMethod·MISSING | Queue the missing RiskMethod mapping or reject the command before linking. |
| Wrong scope | RiskMethod·B01 | Do not attach another church’s RiskMethod without a supported exchange and local authority. |
| Target rename | Rename RiskMethod·A01 after linking | The existing method_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No method_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### assessed_on

Use civil calendar date for `RiskAssessment.assessed_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No assessed_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### horizon_end

Use civil calendar date for `RiskAssessment.horizon_end`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No horizon_end at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### inherent_likelihood

Use versioned classification or status code for `RiskAssessment.inherent_likelihood`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active inherent_likelihood code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped inherent_likelihood code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No inherent_likelihood at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### inherent_impact

Use versioned classification or status code for `RiskAssessment.inherent_impact`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active inherent_impact code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped inherent_impact code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No inherent_impact at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### residual_likelihood

Use versioned classification or status code for `RiskAssessment.residual_likelihood`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active residual_likelihood code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped residual_likelihood code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No residual_likelihood provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### residual_impact

Use versioned classification or status code for `RiskAssessment.residual_impact`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active residual_impact code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped residual_impact code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No residual_impact provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### confidence

Use versioned classification or status code for `RiskAssessment.confidence`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active confidence code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped confidence code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No confidence at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### assumptions

Use human-readable text for `RiskAssessment.assumptions`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered assumptions in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No assumptions at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### evidence_ref

Use scoped or external reference for `RiskAssessment.evidence_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified evidence_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped evidence_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No evidence_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### assessed_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing assessed_by keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No assessed_by at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### reviewed_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing reviewed_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No reviewed_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### review_due_on

Use civil calendar date for `RiskAssessment.review_due_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No review_due_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [RiskAcceptance](RiskAcceptance.md).`assessment_id` | RiskAssessment identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
