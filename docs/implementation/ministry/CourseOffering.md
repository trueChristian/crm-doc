# CourseOffering

[Learning and formation](../../ministry/learning.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Many offerings of one version. Named approval required to substitute materials or an instructor. Use the event waitlist when places are limited.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `curriculum_id` | → Curriculum | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `term_id` | → GroupTerm? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `instructor_id` | → Person | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `campus_id` | → Campus? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `start_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `end_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `language` | code | Required when the record reaches its applicable state | [language](../value-conventions.md#language) |
| `capacity` | count? | Optional under owner conditions | [integer](../value-conventions.md#integer) |
| `enrol_policy` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### curriculum_id

The target is [Curriculum](Curriculum.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Curriculum·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Curriculum·MISSING | Queue the missing Curriculum mapping or reject the command before linking. |
| Wrong scope | Curriculum·B01 | Do not attach another church’s Curriculum without a supported exchange and local authority. |
| Target rename | Rename Curriculum·A01 after linking | The existing curriculum_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No curriculum_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### term_id

The target is [GroupTerm](GroupTerm.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GroupTerm·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | GroupTerm·MISSING | Queue the missing GroupTerm mapping or reject the command before linking. |
| Wrong scope | GroupTerm·B01 | Do not attach another church’s GroupTerm without a supported exchange and local authority. |
| Target rename | Rename GroupTerm·A01 after linking | The existing term_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No term_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### instructor_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing instructor_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No instructor_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### campus_id

The target is [Campus](../foundation/Campus.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Campus·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Campus·MISSING | Queue the missing Campus mapping or reject the command before linking. |
| Wrong scope | Campus·B01 | Do not attach another church’s Campus without a supported exchange and local authority. |
| Target rename | Rename Campus·A01 after linking | The existing campus_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No campus_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### start_on

Use civil calendar date for `CourseOffering.start_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No start_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### end_on

Use civil calendar date for `CourseOffering.end_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No end_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### language

Use language or locale identifier for `CourseOffering.language`. Resolve the published language or locale without inferring a person’s nationality.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | en | Resolve the published language or locale without inferring a person’s nationality. |
| Malformed or unmapped | unmapped locale display label | Keep the source value for review. |
| Specific translation unavailable | specific translation missing at delivery time | Apply the declared fallback and identify which language is being displayed. |
| User changes preferred language | approved letter after preferred-language change | Future communications use the effective preference; issued wording is preserved. |
| Two regional variants exist | two permitted regional variants in catalogue | Apply the requested locale/version where available. |
| Incomplete record | No language at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### capacity

Use whole-number measure for `CourseOffering.capacity`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Absent in intake | No capacity provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### enrol_policy

Use versioned classification or status code for `CourseOffering.enrol_policy`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active enrol_policy code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped enrol_policy code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No enrol_policy at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### state

Use versioned classification or status code for `CourseOffering.state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [CourseSession](CourseSession.md).`offering_id` | CourseOffering identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [LearningEnrolment](LearningEnrolment.md).`offering_id` | CourseOffering identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
