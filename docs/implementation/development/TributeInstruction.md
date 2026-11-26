# TributeInstruction

[Donor service and gift acceptance](../../development/donor-service.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Honor an independent decision about informing the family, making a public dedication and displaying the amount. Never assume either honoree or family agreed to publicity.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `giving_party_id` | ref GivingParty | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `gift_attribution_id` | ref GiftAttribution? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `kind` | memorial/honour | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `public_name` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `notify_contact_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `message` | protected_text? | Optional under owner conditions | [protected](../value-conventions.md#protected) |
| `amount_visibility` | hidden/permitted | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `notice_authority_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `current_state` | pending/approved/notified/withdrawn | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### giving_party_id

The target is [GivingParty](../finance/GivingParty.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GivingParty·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | GivingParty·MISSING | Queue the missing GivingParty mapping or reject the command before linking. |
| Wrong scope | GivingParty·B01 | Do not attach another church’s GivingParty without a supported exchange and local authority. |
| Target rename | Rename GivingParty·A01 after linking | The existing giving_party_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No giving_party_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### gift_attribution_id

The target is [GiftAttribution](../finance/GiftAttribution.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GiftAttribution·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | GiftAttribution·MISSING | Queue the missing GiftAttribution mapping or reject the command before linking. |
| Wrong scope | GiftAttribution·B01 | Do not attach another church’s GiftAttribution without a supported exchange and local authority. |
| Target rename | Rename GiftAttribution·A01 after linking | The existing gift_attribution_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No gift_attribution_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### kind

Declared alternatives in owner order: `memorial`, `honour`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | memorial | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_kind | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### public_name

Use human-readable text for `TributeInstruction.public_name`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered public_name in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No public_name provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### notify_contact_ref

Use scoped or external reference for `TributeInstruction.notify_contact_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified notify_contact_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped notify_contact_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No notify_contact_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### message

Use restricted value or protected content reference for `TributeInstruction.message`. Keep value and purpose together; apply field-level authority to projections.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted message supplied in a restricted context | Keep value and purpose together; apply field-level authority to projections. |
| Malformed or unmapped | public disclosure without authority | Withhold publication unless the specific disclosure rule permits it. |
| Search snippet or autocomplete | restricted fact returned in type-ahead search | Filter before returning any protected content or revealing its existence. |
| Authorized report excludes this field | otherwise permitted export excludes the restricted field | Omit it from hidden metadata and attachments as well. |
| Approval withdrawn after a preview | draft was previewed before authority was withdrawn | Recheck at release; keep only permitted audit evidence. |
| Absent in intake | No message provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### amount_visibility

Declared alternatives in owner order: `hidden`, `permitted`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | hidden | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_amount_visibility | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No amount_visibility at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### notice_authority_ref

Use scoped or external reference for `TributeInstruction.notice_authority_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified notice_authority_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped notice_authority_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No notice_authority_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### current_state

Declared alternatives in owner order: `pending`, `approved`, `notified`, `withdrawn`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | pending | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_current_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No current_state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
