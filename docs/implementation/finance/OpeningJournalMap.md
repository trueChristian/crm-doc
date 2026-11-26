# OpeningJournalMap

[Financial onboarding, cutover and handover](../../finance/cutover.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Choose one posting path. Open documents attach as subledger evidence to openings or create controlled posting lines that are excluded from a separate opening import.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `item_id` | → OpeningItem | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `journal_line_ref` | → JournalLine | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `role` | {posting,subledger_evidence} | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `identifier` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### item_id

The target is [OpeningItem](OpeningItem.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | OpeningItem·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | OpeningItem·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | OpeningItem·MISSING | Queue the missing OpeningItem mapping or reject the command before linking. |
| Wrong scope | OpeningItem·B01 | Do not attach another church’s OpeningItem without a supported exchange and local authority. |
| Target rename | Rename OpeningItem·A01 after linking | The existing item_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No item_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### journal_line_ref

The target is [JournalLine](JournalLine.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | JournalLine·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | JournalLine·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | JournalLine·MISSING | Queue the missing JournalLine mapping or reject the command before linking. |
| Wrong scope | JournalLine·B01 | Do not attach another church’s JournalLine without a supported exchange and local authority. |
| Target rename | Rename JournalLine·A01 after linking | The existing journal_line_ref keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No journal_line_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### amount

Use exact monetary amount with currency for `OpeningJournalMap.amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### role

Declared alternatives in owner order: `posting`, `subledger_evidence`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | posting | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_role | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No role at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### identifier

Use human-readable text for `OpeningJournalMap.identifier`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered identifier in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No identifier at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
