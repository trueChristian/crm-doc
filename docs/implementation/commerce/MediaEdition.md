# MediaEdition

[Sermon library and publication](../../commerce/media.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Versioned edit lineage. Transcript and captions target the exact edition/timing under review. A public excerpt is its own cleared edition.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `delivery_id` | ref SermonDelivery | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `parent_edition_id` | ref MediaEdition? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `edition_kind` | audio/video/text/slides | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `revision` | integer | Required when the record reaches its applicable state | [version](../value-conventions.md#version) |
| `language` | code | Required when the record reaches its applicable state | [language](../value-conventions.md#language) |
| `duration_seconds` | integer? | Optional under owner conditions | [integer](../value-conventions.md#integer) |
| `source_asset_id` | ref MediaAsset? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `access_classification` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `editorial_state` | draft/review/approved/superseded/withdrawn | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

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

### parent_edition_id

The target is [MediaEdition](MediaEdition.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MediaEdition·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | MediaEdition·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | MediaEdition·MISSING | Queue the missing MediaEdition mapping or reject the command before linking. |
| Wrong scope | MediaEdition·B01 | Do not attach another church’s MediaEdition without a supported exchange and local authority. |
| Target rename | Rename MediaEdition·A01 after linking | The existing parent_edition_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No parent_edition_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### edition_kind

Declared alternatives in owner order: `audio`, `video`, `text`, `slides`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | audio | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_edition_kind | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No edition_kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### revision

Use revision number or opaque revision token for `MediaEdition.revision`. Compare under the declared revision scheme. Require the expected version for conflicting work.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | the current revision returned by the owner | Compare under the declared revision scheme. Require the expected version for conflicting work. |
| Malformed or unmapped | superseded version presented for a new approval | Reject or reopen review against the current contents. |
| Two operators begin at revision seven | two edits both cite baseline 7 | Commit the first change once and re-evaluate the second; never overwrite an unreviewed difference. |
| Re-read an already approved revision | re-open issued revision 4 after revision 6 | Return the frozen value and evidence for that edition. |
| Replay of an earlier result | same business operation observed at two revisions | Correlate by the business operation identity; a newer version does not create a second effect. |
| Incomplete record | No revision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### language

Use language or locale identifier for `MediaEdition.language`. Resolve the published language or locale without inferring a person’s nationality.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | en | Resolve the published language or locale without inferring a person’s nationality. |
| Malformed or unmapped | unmapped locale display label | Keep the source value for review. |
| Specific translation unavailable | specific translation missing at delivery time | Apply the declared fallback and identify which language is being displayed. |
| User changes preferred language | approved letter after preferred-language change | Future communications use the effective preference; issued wording is preserved. |
| Two regional variants exist | two permitted regional variants in catalogue | Apply the requested locale/version where available. |
| Incomplete record | No language at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### duration_seconds

Use whole-number measure for `MediaEdition.duration_seconds`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Absent in intake | No duration_seconds provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### source_asset_id

The target is [MediaAsset](MediaAsset.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MediaAsset·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | MediaAsset·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | MediaAsset·MISSING | Queue the missing MediaAsset mapping or reject the command before linking. |
| Wrong scope | MediaAsset·B01 | Do not attach another church’s MediaAsset without a supported exchange and local authority. |
| Target rename | Rename MediaAsset·A01 after linking | The existing source_asset_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No source_asset_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### access_classification

Use versioned classification or status code for `MediaEdition.access_classification`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active access_classification code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped access_classification code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No access_classification at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### editorial_state

Declared alternatives in owner order: `draft`, `review`, `approved`, `superseded`, `withdrawn`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | draft | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_editorial_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No editorial_state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [EditorialReview](EditorialReview.md).`edition_id` | MediaEdition identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MediaEdition](MediaEdition.md).`parent_edition_id` | MediaEdition identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MediaRelease](MediaRelease.md).`edition_id` | MediaEdition identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MediaRendition](MediaRendition.md).`edition_id` | MediaEdition identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MediaRights](MediaRights.md).`edition_id` | MediaEdition identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MediaWithdrawal](MediaWithdrawal.md).`edition_id` | MediaEdition identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [TranscriptSegment](TranscriptSegment.md).`edition_id` | MediaEdition identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
