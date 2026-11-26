# ConsolidationGroup

[Financial statements, close and consolidation](../../finance/reporting.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Explicit group boundary with documented inclusion/exclusion, effective dates and approved consolidation method. A shared church name is insufficient.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `reporting_organization_id` | → Organization | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `title` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `reporting_currency` | code | Required when the record reaches its applicable state | [currency](../value-conventions.md#currency) |
| `basis` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `fiscal_calendar` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `boundary_policy_version` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### reporting_organization_id

The target is [Organization](../foundation/Organization.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Organization·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Organization·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Organization·MISSING | Queue the missing Organization mapping or reject the command before linking. |
| Wrong scope | Organization·B01 | Do not attach another church’s Organization without a supported exchange and local authority. |
| Target rename | Rename Organization·A01 after linking | The existing reporting_organization_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No reporting_organization_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### title

Use human-readable text for `ConsolidationGroup.title`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered title in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No title at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### reporting_currency

Use monetary unit code for `ConsolidationGroup.reporting_currency`. Resolve the code and its precision as of the transaction.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD | Resolve the code and its precision as of the transaction. |
| Malformed or unmapped | ambiguous $ | Request the unambiguous currency. |
| Two amounts have different currencies | 24.50 NAD and 24.50 USD | Report separate totals or translate using recorded rates. |
| Catalog changes after document issue | document issued before currency-profile revision | The stored document keeps its currency. |
| Unrecognized imported code | unmapped monetary unit in staged transaction | Stage unmapped currency; block financial posting. |
| Incomplete record | No reporting_currency at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### basis

Use versioned classification or status code for `ConsolidationGroup.basis`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active basis code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped basis code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No basis at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### fiscal_calendar

Use human-readable text for `ConsolidationGroup.fiscal_calendar`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered fiscal_calendar in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No fiscal_calendar at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### boundary_policy_version

Use human-readable text for `ConsolidationGroup.boundary_policy_version`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered boundary_policy_version in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No boundary_policy_version at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [ConsolidationMember](ConsolidationMember.md).`group_id` | ConsolidationGroup identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ConsolidationRun](ConsolidationRun.md).`group_id` | ConsolidationGroup identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
