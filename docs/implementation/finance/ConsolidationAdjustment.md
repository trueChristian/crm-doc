# ConsolidationAdjustment

[Financial statements, close and consolidation](../../finance/reporting.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Each adjustment batch balances in reporting currency and belongs to the consolidation layer. Resolve unbalanced inter-entity items in a review queue.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `run_id` | → ConsolidationRun | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `kind` | {mapping,alignment,translation,elimination} | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `left_source` | ? | Optional under owner conditions | [structured](../value-conventions.md#structured) |
| `right_source` | ? | Optional under owner conditions | [structured](../value-conventions.md#structured) |
| `account_code` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `amount_signed` | signed_money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `reason` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `prepared_by_ref` | Owner-scoped business value; see the record rule | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `approved_by_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### run_id

The target is [ConsolidationRun](ConsolidationRun.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ConsolidationRun·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ConsolidationRun·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ConsolidationRun·MISSING | Queue the missing ConsolidationRun mapping or reject the command before linking. |
| Wrong scope | ConsolidationRun·B01 | Do not attach another church’s ConsolidationRun without a supported exchange and local authority. |
| Target rename | Rename ConsolidationRun·A01 after linking | The existing run_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No run_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### kind

Declared alternatives in owner order: `mapping`, `alignment`, `translation`, `elimination`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | mapping | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_kind | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### left_source

Use typed value or bounded compound record for `ConsolidationAdjustment.left_source`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of left_source matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for left_source | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Absent in intake | No left_source provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### right_source

Use typed value or bounded compound record for `ConsolidationAdjustment.right_source`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of right_source matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for right_source | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Absent in intake | No right_source provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### account_code

Use human-readable text for `ConsolidationAdjustment.account_code`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered account_code in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No account_code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### amount_signed

Use exact monetary amount with currency for `ConsolidationAdjustment.amount_signed`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No amount_signed at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### reason

Use human-readable text for `ConsolidationAdjustment.reason`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered reason in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No reason at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### prepared_by_ref

Use scoped or external reference for `ConsolidationAdjustment.prepared_by_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified prepared_by_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped prepared_by_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No prepared_by_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### approved_by_ref

Use scoped or external reference for `ConsolidationAdjustment.approved_by_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified approved_by_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped approved_by_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No approved_by_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
