# DeliveryCredit

[Sermon library and publication](../../commerce/media.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One delivery can have multiple speakers and translators with distinct permissions.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `delivery_id` | ref SermonDelivery | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `contributor_id` | ref MediaContributor | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `role` | preacher/interpreter/reader/artist/editor/other | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `billing_order` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `public_credit` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `public_display` | boolean | Required when the record reaches its applicable state | [bool](../value-conventions.md#bool) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### delivery_id

The target is [SermonDelivery](SermonDelivery.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | SermonDelivery·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | SermonDelivery·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | SermonDelivery·MISSING | Queue the missing SermonDelivery mapping or reject the command before linking. |
| Wrong scope | SermonDelivery·B01 | Do not attach another church’s SermonDelivery without a supported exchange and local authority. |
| Target rename | Rename SermonDelivery·A01 after linking | The existing delivery_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No delivery_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### contributor_id

The target is [MediaContributor](MediaContributor.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MediaContributor·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | MediaContributor·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | MediaContributor·MISSING | Queue the missing MediaContributor mapping or reject the command before linking. |
| Wrong scope | MediaContributor·B01 | Do not attach another church’s MediaContributor without a supported exchange and local authority. |
| Target rename | Rename MediaContributor·A01 after linking | The existing contributor_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No contributor_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### role

Declared alternatives in owner order: `preacher`, `interpreter`, `reader`, `artist`, `editor`, `other`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | preacher | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_role | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No role at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### billing_order

Use whole-number measure for `DeliveryCredit.billing_order`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No billing_order at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### public_credit

Use human-readable text for `DeliveryCredit.public_credit`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered public_credit in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No public_credit provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### public_display

Use explicit logical choice for `DeliveryCredit.public_display`. Preserve the supplied value; do not promote an unanswered choice to consent.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | true | Preserve the supplied value; do not promote an unanswered choice to consent. |
| Malformed or unmapped | unmapped input “perhaps” | Map only declared true/false representations. |
| False versus blank | false and absent | Retain the distinction if absence is allowed. |
| Historic default changes | historical edition had false as its default | Issued records keep the value used at decision time. |
| User has no authority to set the flag | valid true submitted outside authorized role | Reject the attempted change even when the value is well formed. |
| Incomplete record | No public_display at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
