# ProposalBudgetLine

[Grant applications and reporting](../../development/grant-applications.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Explain differences between quantity times unit cost and sponsor request. A promised match is distinct from a verified available match, including grants prohibited from counting as matching funds.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `application_id` | ref GrantApplication | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `project_id` | ref MissionProject | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `finance_budget_line_id` | ref BudgetLine? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `category` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `quantity` | decimal | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `unit_cost` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `requested_amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `church_match` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `third_party_match` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `match_evidence_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `currency` | code | Required when the record reaches its applicable state | [currency](../value-conventions.md#currency) |
| `indirect_basis` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |

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

### project_id

The target is [MissionProject](../ministry/MissionProject.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MissionProject·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | MissionProject·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | MissionProject·MISSING | Queue the missing MissionProject mapping or reject the command before linking. |
| Wrong scope | MissionProject·B01 | Do not attach another church’s MissionProject without a supported exchange and local authority. |
| Target rename | Rename MissionProject·A01 after linking | The existing project_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No project_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### finance_budget_line_id

The target is [BudgetLine](../finance/BudgetLine.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | BudgetLine·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | BudgetLine·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | BudgetLine·MISSING | Queue the missing BudgetLine mapping or reject the command before linking. |
| Wrong scope | BudgetLine·B01 | Do not attach another church’s BudgetLine without a supported exchange and local authority. |
| Target rename | Rename BudgetLine·A01 after linking | The existing finance_budget_line_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No finance_budget_line_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### category

Use versioned classification or status code for `ProposalBudgetLine.category`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active category code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped category code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No category at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### quantity

Use exact decimal measure for `ProposalBudgetLine.quantity`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No quantity at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### unit_cost

Use exact monetary amount with currency for `ProposalBudgetLine.unit_cost`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No unit_cost at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### requested_amount

Use exact monetary amount with currency for `ProposalBudgetLine.requested_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No requested_amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### church_match

Use exact monetary amount with currency for `ProposalBudgetLine.church_match`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No church_match at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### third_party_match

Use exact monetary amount with currency for `ProposalBudgetLine.third_party_match`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No third_party_match at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### match_evidence_ref

Use scoped or external reference for `ProposalBudgetLine.match_evidence_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified match_evidence_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped match_evidence_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No match_evidence_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### currency

Use monetary unit code for `ProposalBudgetLine.currency`. Resolve the code and its precision as of the transaction.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD | Resolve the code and its precision as of the transaction. |
| Malformed or unmapped | ambiguous $ | Request the unambiguous currency. |
| Two amounts have different currencies | 24.50 NAD and 24.50 USD | Report separate totals or translate using recorded rates. |
| Catalog changes after document issue | document issued before currency-profile revision | The stored document keeps its currency. |
| Unrecognized imported code | unmapped monetary unit in staged transaction | Stage unmapped currency; block financial posting. |
| Incomplete record | No currency at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### indirect_basis

Use human-readable text for `ProposalBudgetLine.indirect_basis`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered indirect_basis in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No indirect_basis provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
