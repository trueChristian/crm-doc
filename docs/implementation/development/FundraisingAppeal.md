# FundraisingAppeal

[Appeals and attribution](../../development/appeals.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique organization/code, no parent cycles. Approval records objective, handling of shortfall, excess or cancellation and authority to accept a restriction before publication.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `organization_id` | ref Organization | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `congregation_id` | ref Congregation? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `parent_appeal_id` | ref FundraisingAppeal? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `project_id` | ref MissionProject? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `code` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `title` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `purpose` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `finance_fund_id` | ref Fund? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `owner_id` | ref UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `currency` | code | Required when the record reaches its applicable state | [currency](../value-conventions.md#currency) |
| `opens_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `closes_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `fallback_terms` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `public_summary` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `approval_state` | draft/review/approved/open/paused/closed/withdrawn | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### organization_id

The target is [Organization](../foundation/Organization.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Organization·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Organization·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Organization·MISSING | Queue the missing Organization mapping or reject the command before linking. |
| Wrong scope | Organization·B01 | Do not attach another church’s Organization without a supported exchange and local authority. |
| Target rename | Rename Organization·A01 after linking | The existing organization_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No organization_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### congregation_id

The target is [Congregation](../foundation/Congregation.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Congregation·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Congregation·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Congregation·MISSING | Queue the missing Congregation mapping or reject the command before linking. |
| Wrong scope | Congregation·B01 | Do not attach another church’s Congregation without a supported exchange and local authority. |
| Target rename | Rename Congregation·A01 after linking | The existing congregation_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No congregation_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### parent_appeal_id

The target is [FundraisingAppeal](FundraisingAppeal.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FundraisingAppeal·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | FundraisingAppeal·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | FundraisingAppeal·MISSING | Queue the missing FundraisingAppeal mapping or reject the command before linking. |
| Wrong scope | FundraisingAppeal·B01 | Do not attach another church’s FundraisingAppeal without a supported exchange and local authority. |
| Target rename | Rename FundraisingAppeal·A01 after linking | The existing parent_appeal_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No parent_appeal_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### project_id

The target is [MissionProject](../ministry/MissionProject.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MissionProject·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | MissionProject·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | MissionProject·MISSING | Queue the missing MissionProject mapping or reject the command before linking. |
| Wrong scope | MissionProject·B01 | Do not attach another church’s MissionProject without a supported exchange and local authority. |
| Target rename | Rename MissionProject·A01 after linking | The existing project_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No project_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### code

Use versioned classification or status code for `FundraisingAppeal.code`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active code code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped code code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### title

Use human-readable text for `FundraisingAppeal.title`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered title in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No title at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### purpose

Use human-readable text for `FundraisingAppeal.purpose`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered purpose in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No purpose at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### finance_fund_id

The target is [Fund](../finance/Fund.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Fund·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Fund·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Fund·MISSING | Queue the missing Fund mapping or reject the command before linking. |
| Wrong scope | Fund·B01 | Do not attach another church’s Fund without a supported exchange and local authority. |
| Target rename | Rename Fund·A01 after linking | The existing finance_fund_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No finance_fund_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### owner_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing owner_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No owner_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### currency

Use monetary unit code for `FundraisingAppeal.currency`. Resolve the code and its precision as of the transaction.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD | Resolve the code and its precision as of the transaction. |
| Malformed or unmapped | ambiguous $ | Request the unambiguous currency. |
| Two amounts have different currencies | 24.50 NAD and 24.50 USD | Report separate totals or translate using recorded rates. |
| Catalog changes after document issue | document issued before currency-profile revision | The stored document keeps its currency. |
| Unrecognized imported code | unmapped monetary unit in staged transaction | Stage unmapped currency; block financial posting. |
| Incomplete record | No currency at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### opens_at

Use unambiguous point in time for `FundraisingAppeal.opens_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No opens_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### closes_at

Use unambiguous point in time for `FundraisingAppeal.closes_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No closes_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### fallback_terms

Use human-readable text for `FundraisingAppeal.fallback_terms`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered fallback_terms in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No fallback_terms provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### public_summary

Use human-readable text for `FundraisingAppeal.public_summary`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered public_summary in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No public_summary provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### approval_state

Declared alternatives in owner order: `draft`, `review`, `approved`, `open`, `paused`, `closed`, `withdrawn`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | draft | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_approval_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No approval_state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AppealAllocationCredit](AppealAllocationCredit.md).`appeal_id` | FundraisingAppeal identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AppealChannel](AppealChannel.md).`appeal_id` | FundraisingAppeal identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AppealGoal](AppealGoal.md).`appeal_id` | FundraisingAppeal identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AppealProspect](AppealProspect.md).`appeal_id` | FundraisingAppeal identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AppealSnapshot](AppealSnapshot.md).`appeal_id` | FundraisingAppeal identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FundraisingAppeal](FundraisingAppeal.md).`parent_appeal_id` | FundraisingAppeal identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GiftOfferAssessment](GiftOfferAssessment.md).`appeal_id` | FundraisingAppeal identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ImpactPublication](ImpactPublication.md).`appeal_id` | FundraisingAppeal identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MatchOffer](MatchOffer.md).`appeal_id` | FundraisingAppeal identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StewardshipPlan](StewardshipPlan.md).`appeal_id` | FundraisingAppeal identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
