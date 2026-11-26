# CommunicationPurpose

[Recipients and channel policy](../../communications/recipients-and-channels.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Stable organization/code. Distinguish worship announcements, volunteer duties, governance notices, receipts, giving appeals and pastoral contact. Changing a purpose creates a reviewed edition.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `data_purpose_id` | DataPurpose ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `organization_id` | Organization ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `code` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `label` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `description` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `class` | operational/optional/emergency | Optional under owner conditions | [enum](../value-conventions.md#enum) |
| `permitted_content` | enum set | Required when the record reaches its applicable state | [list](../value-conventions.md#list) |
| `default_sensitivity` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `default_eligibility` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `policy_edition` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `active_from` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `retired_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### data_purpose_id

The target is [DataPurpose](../platform/DataPurpose.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DataPurpose·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | DataPurpose·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | DataPurpose·MISSING | Queue the missing DataPurpose mapping or reject the command before linking. |
| Wrong scope | DataPurpose·B01 | Do not attach another church’s DataPurpose without a supported exchange and local authority. |
| Target rename | Rename DataPurpose·A01 after linking | The existing data_purpose_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No data_purpose_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

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

### code

Use human-readable text for `CommunicationPurpose.code`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered code in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### label

Use human-readable text for `CommunicationPurpose.label`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered label in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No label at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### description

Use human-readable text for `CommunicationPurpose.description`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered description in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No description at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### class

Declared alternatives in owner order: `operational`, `optional`, `emergency`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | operational | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_class | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Absent in intake | No class provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### permitted_content

Use ordered collection or mathematical set for `CommunicationPurpose.permitted_content`. Preserve ordering when meaningful; enforce uniqueness when the declaration is a set.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted members A and B | Preserve ordering when meaningful; enforce uniqueness when the declaration is a set. |
| Malformed or unmapped | an element outside the declared domain | Reject the affected collection or stage its invalid item under the import policy. |
| Same element appears twice | A, A, B | Apply declared sequence/set multiplicity without doubling financial or voting effects. |
| Empty collection versus unknown collection | empty collection and missing collection | Preserve the distinction where the rule requires evidence. |
| One element later becomes restricted | authorization for member B withdrawn before export | Recompute permitted projection before export or display. |
| Incomplete record | No permitted_content at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### default_sensitivity

Use versioned classification or status code for `CommunicationPurpose.default_sensitivity`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active default_sensitivity code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped default_sensitivity code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No default_sensitivity at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### default_eligibility

Use versioned classification or status code for `CommunicationPurpose.default_eligibility`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active default_eligibility code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped default_eligibility code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No default_eligibility at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### policy_edition

Use human-readable text for `CommunicationPurpose.policy_edition`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered policy_edition in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No policy_edition at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### active_from

Use civil calendar date for `CommunicationPurpose.active_from`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No active_from at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### retired_on

Use civil calendar date for `CommunicationPurpose.retired_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No retired_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [Campaign](Campaign.md).`purpose_id` | CommunicationPurpose identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ContactDecision](ContactDecision.md).`purpose_id` | CommunicationPurpose identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ContactRestriction](ContactRestriction.md).`purpose_id` | CommunicationPurpose identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ContactSubscription](ContactSubscription.md).`purpose_id` | CommunicationPurpose identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ContactTree](ContactTree.md).`purpose_id` | CommunicationPurpose identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ContactWindow](ContactWindow.md).`purpose_id` | CommunicationPurpose identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DigestEdition](DigestEdition.md).`purpose_id` | CommunicationPurpose identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DispatchRequest](DispatchRequest.md).`purpose_id` | CommunicationPurpose identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MessageTemplate](MessageTemplate.md).`purpose_id` | CommunicationPurpose identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReminderRule](ReminderRule.md).`purpose_id` | CommunicationPurpose identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReplyThread](ReplyThread.md).`purpose_id` | CommunicationPurpose identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
