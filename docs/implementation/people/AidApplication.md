# AidApplication

[Benevolence and community aid](../../people/benevolence-and-community-aid.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One designated beneficiary kind; a private identifier may substitute for a missing named applicant. Quantities require a unit and amounts a currency. A group distribution records aggregate counts where individual identification is unnecessary.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | ID | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `program_id` | → AidProgram | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `person_id` | → Person? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `household_id` | → Household? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `private_applicant_label` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `beneficiary_kind` | enum(person, household, organization, anonymous_distribution) | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `external_party_ref` | ID? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `received_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `requested_support_code` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `requested_amount` | decimal? | Optional under owner conditions | [decimal](../value-conventions.md#decimal) |
| `currency` | code? | Optional under owner conditions | [currency](../value-conventions.md#currency) |
| `quantity` | decimal? | Optional under owner conditions | [decimal](../value-conventions.md#decimal) |
| `unit` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `requested_by_ref` | ID? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `unsafe_contact_note` | restricted text? | Optional under owner conditions | [protected](../value-conventions.md#protected) |
| `status` | enum(received, assessing, awaiting_information, approved, partly_approved, declined, withdrawn, closed) | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `AidApplication.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AidApplication·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### program_id

The target is [AidProgram](AidProgram.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AidProgram·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | AidProgram·MISSING | Queue the missing AidProgram mapping or reject the command before linking. |
| Wrong scope | AidProgram·B01 | Do not attach another church’s AidProgram without a supported exchange and local authority. |
| Target rename | Rename AidProgram·A01 after linking | The existing program_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No program_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### person_id

The target is [Person](Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing person_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No person_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### household_id

The target is [Household](Household.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Household·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Household·MISSING | Queue the missing Household mapping or reject the command before linking. |
| Wrong scope | Household·B01 | Do not attach another church’s Household without a supported exchange and local authority. |
| Target rename | Rename Household·A01 after linking | The existing household_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No household_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### private_applicant_label

Use human-readable text for `AidApplication.private_applicant_label`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered private_applicant_label in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No private_applicant_label provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### beneficiary_kind

Declared alternatives in owner order: `person`, `household`, `organization`, `anonymous_distribution`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | person | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_beneficiary_kind | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No beneficiary_kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### external_party_ref

Use scoped or external reference for `AidApplication.external_party_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified external_party_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped external_party_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No external_party_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### received_at

Use unambiguous point in time for `AidApplication.received_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No received_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### requested_support_code

Use versioned classification or status code for `AidApplication.requested_support_code`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active requested_support_code code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped requested_support_code code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No requested_support_code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### requested_amount

Use exact decimal measure for `AidApplication.requested_amount`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Absent in intake | No requested_amount provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### currency

Use monetary unit code for `AidApplication.currency`. Resolve the code and its precision as of the transaction.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD | Resolve the code and its precision as of the transaction. |
| Malformed or unmapped | ambiguous $ | Request the unambiguous currency. |
| Two amounts have different currencies | 24.50 NAD and 24.50 USD | Report separate totals or translate using recorded rates. |
| Catalog changes after document issue | document issued before currency-profile revision | The stored document keeps its currency. |
| Unrecognized imported code | unmapped monetary unit in staged transaction | Stage unmapped currency; block financial posting. |
| Absent in intake | No currency provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### quantity

Use exact decimal measure for `AidApplication.quantity`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Absent in intake | No quantity provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### unit

Use versioned classification or status code for `AidApplication.unit`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active unit code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped unit code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No unit provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### requested_by_ref

Use scoped or external reference for `AidApplication.requested_by_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified requested_by_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped requested_by_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No requested_by_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### unsafe_contact_note

Use restricted value or protected content reference for `AidApplication.unsafe_contact_note`. Keep value and purpose together; apply field-level authority to projections.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted unsafe_contact_note supplied in a restricted context | Keep value and purpose together; apply field-level authority to projections. |
| Malformed or unmapped | public disclosure without authority | Withhold publication unless the specific disclosure rule permits it. |
| Search snippet or autocomplete | restricted fact returned in type-ahead search | Filter before returning any protected content or revealing its existence. |
| Authorized report excludes this field | otherwise permitted export excludes the restricted field | Omit it from hidden metadata and attachments as well. |
| Approval withdrawn after a preview | draft was previewed before authority was withdrawn | Recheck at release; keep only permitted audit evidence. |
| Absent in intake | No unsafe_contact_note provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### status

Declared alternatives in owner order: `received`, `assessing`, `awaiting_information`, `approved`, `partly_approved`, `declined`, `withdrawn`, `closed`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | received | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_status | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No status at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AidAssessment](AidAssessment.md).`application_id` | AidApplication identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AidAward](AidAward.md).`application_id` | AidApplication identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AidReview](AidReview.md).`application_id` | AidApplication identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RoundPlacement](../administration/RoundPlacement.md).`application_id` | AidApplication identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Use the minimum evidence allowed by the selected anonymous, pseudonymous or identified mode. A permitted operator may be accountable for receiving or reviewing work without collecting the identity of a protected subject. Keep safe-channel, identity and case evidence apart from releasable totals and narratives; apply the original permissions to the verification evidence.
