# AudienceEntry

[Campaigns, audiences and content](../../communications/campaigns-and-content.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Has one intended recipient unit under the chosen scope. Deduplicate intersecting groups before route selection. Record exclusions minimally and only where retention permits.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `snapshot_id` | AudienceSnapshot ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `person_id` | Person ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `household_id` | Household ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `representation_id` | RepresentationAuthority ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `membership_reason` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `language` | locale? | Optional under owner conditions | [language](../value-conventions.md#language) |
| `included` | boolean | Required when the record reaches its applicable state | [bool](../value-conventions.md#bool) |
| `exclusion_reason` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `source_revision` | text | Required when the record reaches its applicable state | [version](../value-conventions.md#version) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### snapshot_id

The target is [AudienceSnapshot](AudienceSnapshot.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AudienceSnapshot·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | AudienceSnapshot·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | AudienceSnapshot·MISSING | Queue the missing AudienceSnapshot mapping or reject the command before linking. |
| Wrong scope | AudienceSnapshot·B01 | Do not attach another church’s AudienceSnapshot without a supported exchange and local authority. |
| Target rename | Rename AudienceSnapshot·A01 after linking | The existing snapshot_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No snapshot_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### person_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing person_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No person_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### household_id

The target is [Household](../people/Household.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Household·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Household·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Household·MISSING | Queue the missing Household mapping or reject the command before linking. |
| Wrong scope | Household·B01 | Do not attach another church’s Household without a supported exchange and local authority. |
| Target rename | Rename Household·A01 after linking | The existing household_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No household_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### representation_id

The target is [RepresentationAuthority](../people/RepresentationAuthority.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | RepresentationAuthority·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | RepresentationAuthority·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | RepresentationAuthority·MISSING | Queue the missing RepresentationAuthority mapping or reject the command before linking. |
| Wrong scope | RepresentationAuthority·B01 | Do not attach another church’s RepresentationAuthority without a supported exchange and local authority. |
| Target rename | Rename RepresentationAuthority·A01 after linking | The existing representation_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No representation_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### membership_reason

Use versioned classification or status code for `AudienceEntry.membership_reason`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active membership_reason code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped membership_reason code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No membership_reason at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### language

Use language or locale identifier for `AudienceEntry.language`. Resolve the published language or locale without inferring a person’s nationality.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | en | Resolve the published language or locale without inferring a person’s nationality. |
| Malformed or unmapped | unmapped locale display label | Keep the source value for review. |
| Specific translation unavailable | specific translation missing at delivery time | Apply the declared fallback and identify which language is being displayed. |
| User changes preferred language | approved letter after preferred-language change | Future communications use the effective preference; issued wording is preserved. |
| Two regional variants exist | two permitted regional variants in catalogue | Apply the requested locale/version where available. |
| Absent in intake | No language provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### included

Use explicit logical choice for `AudienceEntry.included`. Preserve the supplied value; do not promote an unanswered choice to consent.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | true | Preserve the supplied value; do not promote an unanswered choice to consent. |
| Malformed or unmapped | unmapped input “perhaps” | Map only declared true/false representations. |
| False versus blank | false and absent | Retain the distinction if absence is allowed. |
| Historic default changes | historical edition had false as its default | Issued records keep the value used at decision time. |
| User has no authority to set the flag | valid true submitted outside authorized role | Reject the attempted change even when the value is well formed. |
| Incomplete record | No included at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### exclusion_reason

Use versioned classification or status code for `AudienceEntry.exclusion_reason`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active exclusion_reason code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped exclusion_reason code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No exclusion_reason provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### source_revision

Use revision number or opaque revision token for `AudienceEntry.source_revision`. Compare under the declared revision scheme. Require the expected version for conflicting work.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | the current revision returned by the owner | Compare under the declared revision scheme. Require the expected version for conflicting work. |
| Malformed or unmapped | superseded version presented for a new approval | Reject or reopen review against the current contents. |
| Two operators begin at revision seven | two edits both cite baseline 7 | Commit the first change once and re-evaluate the second; never overwrite an unreviewed difference. |
| Re-read an already approved revision | re-open issued revision 4 after revision 6 | Return the frozen value and evidence for that edition. |
| Replay of an earlier result | same business operation observed at two revisions | Correlate by the business operation identity; a newer version does not create a second effect. |
| Incomplete record | No source_revision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [DispatchRecipient](DispatchRecipient.md).`entry_id` | AudienceEntry identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
