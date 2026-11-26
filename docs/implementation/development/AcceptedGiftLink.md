# AcceptedGiftLink

[Donor service and gift acceptance](../../development/donor-service.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique source/target handoff. Link only records compatible with accepted terms. An intention can link a pledge when formally authorized; a posting requires the finance receipt or recognition decision.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `assessment_id` | ref GiftOfferAssessment | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `pledge_id` | ref Pledge? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `gift_id` | ref Gift? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `in_kind_gift_id` | ref InKindGift? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `fund_restriction_id` | ref FundRestriction? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `handoff_key` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `accepted_version` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `acknowledged_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### assessment_id

The target is [GiftOfferAssessment](GiftOfferAssessment.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GiftOfferAssessment·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | GiftOfferAssessment·MISSING | Queue the missing GiftOfferAssessment mapping or reject the command before linking. |
| Wrong scope | GiftOfferAssessment·B01 | Do not attach another church’s GiftOfferAssessment without a supported exchange and local authority. |
| Target rename | Rename GiftOfferAssessment·A01 after linking | The existing assessment_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No assessment_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### pledge_id

The target is [Pledge](../finance/Pledge.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Pledge·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Pledge·MISSING | Queue the missing Pledge mapping or reject the command before linking. |
| Wrong scope | Pledge·B01 | Do not attach another church’s Pledge without a supported exchange and local authority. |
| Target rename | Rename Pledge·A01 after linking | The existing pledge_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No pledge_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### gift_id

The target is [Gift](../finance/Gift.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Gift·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Gift·MISSING | Queue the missing Gift mapping or reject the command before linking. |
| Wrong scope | Gift·B01 | Do not attach another church’s Gift without a supported exchange and local authority. |
| Target rename | Rename Gift·A01 after linking | The existing gift_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No gift_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### in_kind_gift_id

The target is [InKindGift](../finance/InKindGift.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | InKindGift·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | InKindGift·MISSING | Queue the missing InKindGift mapping or reject the command before linking. |
| Wrong scope | InKindGift·B01 | Do not attach another church’s InKindGift without a supported exchange and local authority. |
| Target rename | Rename InKindGift·A01 after linking | The existing in_kind_gift_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No in_kind_gift_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### fund_restriction_id

The target is [FundRestriction](../finance/FundRestriction.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FundRestriction·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | FundRestriction·MISSING | Queue the missing FundRestriction mapping or reject the command before linking. |
| Wrong scope | FundRestriction·B01 | Do not attach another church’s FundRestriction without a supported exchange and local authority. |
| Target rename | Rename FundRestriction·A01 after linking | The existing fund_restriction_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No fund_restriction_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### handoff_key

Use human-readable text for `AcceptedGiftLink.handoff_key`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered handoff_key in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No handoff_key at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### accepted_version

Use whole-number measure for `AcceptedGiftLink.accepted_version`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No accepted_version at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### acknowledged_at

Use unambiguous point in time for `AcceptedGiftLink.acknowledged_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No acknowledged_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
