# PartnerPromise

[Partnerships, sponsorships and impact](../../development/partnerships.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Document who owes which action. Each promise can be fulfilled in portions and amendments preserve the prior commitment. Financial promises do not add to received totals.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `agreement_id` | ref PartnershipAgreement | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `party_id` | ref AgreementParty | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `project_milestone_id` | ref ProjectMilestone? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `kind` | cash/goods/volunteers/venue/report/equipment | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `description` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `promised_quantity` | decimal | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `unit` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `currency` | code? | Optional under owner conditions | [currency](../value-conventions.md#currency) |
| `due_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `accountable_owner_id` | ref UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `finance_pledge_id` | ref Pledge? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `finance_award_id` | ref GrantAward? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `state` | proposed/approved/in_progress/partial/met/waived/breached | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### agreement_id

The target is [PartnershipAgreement](PartnershipAgreement.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | PartnershipAgreement·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | PartnershipAgreement·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | PartnershipAgreement·MISSING | Queue the missing PartnershipAgreement mapping or reject the command before linking. |
| Wrong scope | PartnershipAgreement·B01 | Do not attach another church’s PartnershipAgreement without a supported exchange and local authority. |
| Target rename | Rename PartnershipAgreement·A01 after linking | The existing agreement_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No agreement_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### party_id

The target is [AgreementParty](AgreementParty.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AgreementParty·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | AgreementParty·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | AgreementParty·MISSING | Queue the missing AgreementParty mapping or reject the command before linking. |
| Wrong scope | AgreementParty·B01 | Do not attach another church’s AgreementParty without a supported exchange and local authority. |
| Target rename | Rename AgreementParty·A01 after linking | The existing party_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No party_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### project_milestone_id

The target is [ProjectMilestone](../ministry/ProjectMilestone.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ProjectMilestone·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ProjectMilestone·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ProjectMilestone·MISSING | Queue the missing ProjectMilestone mapping or reject the command before linking. |
| Wrong scope | ProjectMilestone·B01 | Do not attach another church’s ProjectMilestone without a supported exchange and local authority. |
| Target rename | Rename ProjectMilestone·A01 after linking | The existing project_milestone_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No project_milestone_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### kind

Declared alternatives in owner order: `cash`, `goods`, `volunteers`, `venue`, `report`, `equipment`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | cash | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_kind | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### description

Use human-readable text for `PartnerPromise.description`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered description in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No description at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### promised_quantity

Use exact decimal measure for `PartnerPromise.promised_quantity`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No promised_quantity at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### unit

Use versioned classification or status code for `PartnerPromise.unit`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active unit code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped unit code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No unit at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### currency

Use monetary unit code for `PartnerPromise.currency`. Resolve the code and its precision as of the transaction.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD | Resolve the code and its precision as of the transaction. |
| Malformed or unmapped | ambiguous $ | Request the unambiguous currency. |
| Two amounts have different currencies | 24.50 NAD and 24.50 USD | Report separate totals or translate using recorded rates. |
| Catalog changes after document issue | document issued before currency-profile revision | The stored document keeps its currency. |
| Unrecognized imported code | unmapped monetary unit in staged transaction | Stage unmapped currency; block financial posting. |
| Absent in intake | No currency provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### due_at

Use unambiguous point in time for `PartnerPromise.due_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No due_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### accountable_owner_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing accountable_owner_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No accountable_owner_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### finance_pledge_id

The target is [Pledge](../finance/Pledge.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Pledge·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Pledge·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Pledge·MISSING | Queue the missing Pledge mapping or reject the command before linking. |
| Wrong scope | Pledge·B01 | Do not attach another church’s Pledge without a supported exchange and local authority. |
| Target rename | Rename Pledge·A01 after linking | The existing finance_pledge_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No finance_pledge_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### finance_award_id

The target is [GrantAward](../finance/GrantAward.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GrantAward·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | GrantAward·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | GrantAward·MISSING | Queue the missing GrantAward mapping or reject the command before linking. |
| Wrong scope | GrantAward·B01 | Do not attach another church’s GrantAward without a supported exchange and local authority. |
| Target rename | Rename GrantAward·A01 after linking | The existing finance_award_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No finance_award_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Declared alternatives in owner order: `proposed`, `approved`, `in_progress`, `partial`, `met`, `waived`, `breached`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | proposed | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [PartnershipDelivery](PartnershipDelivery.md).`promise_id` | PartnerPromise identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
