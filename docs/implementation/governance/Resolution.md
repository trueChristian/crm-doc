# Resolution

[Minutes, resolutions and the archive](../../governance/minutes-and-resolutions.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique body/number. Some decisions take effect when passed and others upon ratification. Preserve both adoption and effective dates and their authority. Link an amended or rescinded resolution to its predecessor.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `body_id` | GoverningBody ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `item_id` | MinuteItem ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `motion_id` | Motion ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `number` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `exact_text` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `disposition` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `decision_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `effective_from` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `expires_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `visibility` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `state` | pending_confirmation/effective/suspended/fulfilled/rescinded/expired | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `supersedes_id` | Resolution ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### body_id

The target is [GoverningBody](GoverningBody.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GoverningBody·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | GoverningBody·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | GoverningBody·MISSING | Queue the missing GoverningBody mapping or reject the command before linking. |
| Wrong scope | GoverningBody·B01 | Do not attach another church’s GoverningBody without a supported exchange and local authority. |
| Target rename | Rename GoverningBody·A01 after linking | The existing body_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No body_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### item_id

The target is [MinuteItem](MinuteItem.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MinuteItem·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | MinuteItem·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | MinuteItem·MISSING | Queue the missing MinuteItem mapping or reject the command before linking. |
| Wrong scope | MinuteItem·B01 | Do not attach another church’s MinuteItem without a supported exchange and local authority. |
| Target rename | Rename MinuteItem·A01 after linking | The existing item_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No item_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### motion_id

The target is [Motion](Motion.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Motion·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Motion·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Motion·MISSING | Queue the missing Motion mapping or reject the command before linking. |
| Wrong scope | Motion·B01 | Do not attach another church’s Motion without a supported exchange and local authority. |
| Target rename | Rename Motion·A01 after linking | The existing motion_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No motion_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### number

Use human-readable text for `Resolution.number`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered number in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No number at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### exact_text

Use human-readable text for `Resolution.exact_text`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered exact_text in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No exact_text at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### disposition

Use versioned classification or status code for `Resolution.disposition`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active disposition code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped disposition code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No disposition at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### decision_at

Use unambiguous point in time for `Resolution.decision_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No decision_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### effective_from

Use civil calendar date for `Resolution.effective_from`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No effective_from provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### expires_on

Use civil calendar date for `Resolution.expires_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No expires_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### visibility

Use versioned classification or status code for `Resolution.visibility`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active visibility code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped visibility code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No visibility at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### state

Declared alternatives in owner order: `pending_confirmation`, `effective`, `suspended`, `fulfilled`, `rescinded`, `expired`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | pending_confirmation | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### supersedes_id

The target is [Resolution](Resolution.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Resolution·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Resolution·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Resolution·MISSING | Queue the missing Resolution mapping or reject the command before linking. |
| Wrong scope | Resolution·B01 | Do not attach another church’s Resolution without a supported exchange and local authority. |
| Target rename | Rename Resolution·A01 after linking | The existing supersedes_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No supersedes_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [BudgetVersion](../finance/BudgetVersion.md).`meeting_resolution_ref` | Resolution identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GovernancePolicyEdition](GovernancePolicyEdition.md).`authorizing_resolution_id` | Resolution identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Resolution](Resolution.md).`supersedes_id` | Resolution identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ResolutionAction](ResolutionAction.md).`resolution_id` | Resolution identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
