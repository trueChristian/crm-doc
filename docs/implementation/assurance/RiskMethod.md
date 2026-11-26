# RiskMethod

[Risk ownership, control testing and prevention](../../assurance/risk-and-prevention.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Validate that each likelihood/impact pair resolves exactly once; distinguish qualitative labels from numerical estimates. Freeze the version used in a decision and state the period the rating covers.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | ID | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `organization_id` | → Organization | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `version` | integer | Required when the record reaches its applicable state | [version](../value-conventions.md#version) |
| `title` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `scope_ref` | ID? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `likelihood_levels` | ordered codes | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `impact_levels` | ordered codes | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `rating_matrix` | pairs → rating | Required when the record reaches its applicable state | [structured](../value-conventions.md#structured) |
| `time_horizon` | duration | Required when the record reaches its applicable state | [duration](../value-conventions.md#duration) |
| `appetite_by_category` | code map | Required when the record reaches its applicable state | [list](../value-conventions.md#list) |
| `valid_from` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `valid_until` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `approved_by` | → UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `RiskMethod.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | RiskMethod·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### organization_id

The target is [Organization](../foundation/Organization.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Organization·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Organization·MISSING | Queue the missing Organization mapping or reject the command before linking. |
| Wrong scope | Organization·B01 | Do not attach another church’s Organization without a supported exchange and local authority. |
| Target rename | Rename Organization·A01 after linking | The existing organization_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No organization_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### version

Use revision number or opaque revision token for `RiskMethod.version`. Compare under the declared revision scheme. Require the expected version for conflicting work.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | the current revision returned by the owner | Compare under the declared revision scheme. Require the expected version for conflicting work. |
| Malformed or unmapped | superseded version presented for a new approval | Reject or reopen review against the current contents. |
| Two operators begin at revision seven | two edits both cite baseline 7 | Commit the first change once and re-evaluate the second; never overwrite an unreviewed difference. |
| Re-read an already approved revision | re-open issued revision 4 after revision 6 | Return the frozen value and evidence for that edition. |
| Replay of an earlier result | same business operation observed at two revisions | Correlate by the business operation identity; a newer version does not create a second effect. |
| Incomplete record | No version at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### title

Use human-readable text for `RiskMethod.title`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered title in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No title at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### scope_ref

Use scoped or external reference for `RiskMethod.scope_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified scope_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped scope_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No scope_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### likelihood_levels

Use versioned classification or status code for `RiskMethod.likelihood_levels`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active likelihood_levels code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped likelihood_levels code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No likelihood_levels at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### impact_levels

Use versioned classification or status code for `RiskMethod.impact_levels`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active impact_levels code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped impact_levels code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No impact_levels at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### rating_matrix

Use typed value or bounded compound record for `RiskMethod.rating_matrix`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of rating_matrix matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for rating_matrix | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Incomplete record | No rating_matrix at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### time_horizon

Use elapsed interval or named calendar duration for `RiskMethod.time_horizon`. Preserve unit and distinguish elapsed minutes from a calendar day or working day.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 30 minutes in elapsed-time profile | Preserve unit and distinguish elapsed minutes from a calendar day or working day. |
| Malformed or unmapped | duration without resolvable unit | Request an interval unit. |
| A working-day deadline crosses a closure | a one-workday deadline starting on Friday | Use the named work-calendar edition. |
| A civil day crosses an offset change | a local civil day covers 23 or 25 elapsed hours | Do not assume 24 elapsed hours. |
| Zero-length interval | duration of zero units | Apply the owner’s validity or immediate-trigger rule. |
| Incomplete record | No time_horizon at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### appetite_by_category

Use ordered collection or mathematical set for `RiskMethod.appetite_by_category`. Preserve ordering when meaningful; enforce uniqueness when the declaration is a set.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted members A and B | Preserve ordering when meaningful; enforce uniqueness when the declaration is a set. |
| Malformed or unmapped | an element outside the declared domain | Reject the affected collection or stage its invalid item under the import policy. |
| Same element appears twice | A, A, B | Apply declared sequence/set multiplicity without doubling financial or voting effects. |
| Empty collection versus unknown collection | empty collection and missing collection | Preserve the distinction where the rule requires evidence. |
| One element later becomes restricted | authorization for member B withdrawn before export | Recompute permitted projection before export or display. |
| Incomplete record | No appetite_by_category at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### valid_from

Use civil calendar date for `RiskMethod.valid_from`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No valid_from at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### valid_until

Use civil calendar date for `RiskMethod.valid_until`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No valid_until provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### approved_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing approved_by keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No approved_by at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [RiskAssessment](RiskAssessment.md).`method_id` | RiskMethod identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
