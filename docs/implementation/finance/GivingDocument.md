# GivingDocument

[Offerings, gifts and donor service](../../finance/giving.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Issuance fixes entity details, dates, address, contributions, currency and template version. Require controlled cancellation and reissue; prevent duplicate official numbering.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `giving_party_id` | → GivingParty | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `kind` | {acknowledgement,receipt,statement,correction} | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `number` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `period_start` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `period_end` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `generated_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `approved_by` | → UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `delivery_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `snapshot` | evidence | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `replaces_id` | → GivingDocument? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### giving_party_id

The target is [GivingParty](GivingParty.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GivingParty·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | GivingParty·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | GivingParty·MISSING | Queue the missing GivingParty mapping or reject the command before linking. |
| Wrong scope | GivingParty·B01 | Do not attach another church’s GivingParty without a supported exchange and local authority. |
| Target rename | Rename GivingParty·A01 after linking | The existing giving_party_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No giving_party_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### kind

Declared alternatives in owner order: `acknowledgement`, `receipt`, `statement`, `correction`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | acknowledgement | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_kind | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### number

Use human-readable text for `GivingDocument.number`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered number in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No number at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### period_start

Use civil calendar date for `GivingDocument.period_start`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No period_start at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### period_end

Use civil calendar date for `GivingDocument.period_end`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No period_end at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### generated_at

Use unambiguous point in time for `GivingDocument.generated_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No generated_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### approved_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing approved_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No approved_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### delivery_ref

Use scoped or external reference for `GivingDocument.delivery_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified delivery_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped delivery_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No delivery_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### snapshot

Use scoped or external reference for `GivingDocument.snapshot`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified snapshot in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped snapshot | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No snapshot at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### replaces_id

The target is [GivingDocument](GivingDocument.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GivingDocument·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | GivingDocument·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | GivingDocument·MISSING | Queue the missing GivingDocument mapping or reject the command before linking. |
| Wrong scope | GivingDocument·B01 | Do not attach another church’s GivingDocument without a supported exchange and local authority. |
| Target rename | Rename GivingDocument·A01 after linking | The existing replaces_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No replaces_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [GivingDocument](GivingDocument.md).`replaces_id` | GivingDocument identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GivingDocumentItem](GivingDocumentItem.md).`document_id` | GivingDocument identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StewardshipAction](../development/StewardshipAction.md).`related_document_id` | GivingDocument identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
