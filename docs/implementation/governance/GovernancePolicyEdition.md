# GovernancePolicyEdition

[Annual assemblies, policies and review](../../governance/annual-cycle-and-policy.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Prevent overlapping effective editions for the same population and policy. Acknowledgement does not grant system access or substitute for evidence of required training.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `policy_id` | GovernancePolicy ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `edition` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `text_version_ref` | text | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `digest` | text | Required when the record reaches its applicable state | [digest](../value-conventions.md#digest) |
| `authorizing_resolution_id` | Resolution ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `effective_from` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `effective_until` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `review_due_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `disposition` | adopt/amend/retire | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `acknowledgment_class` | none/read/affirm | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `predecessor_id` | GovernancePolicyEdition ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### policy_id

The target is [GovernancePolicy](GovernancePolicy.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GovernancePolicy·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | GovernancePolicy·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | GovernancePolicy·MISSING | Queue the missing GovernancePolicy mapping or reject the command before linking. |
| Wrong scope | GovernancePolicy·B01 | Do not attach another church’s GovernancePolicy without a supported exchange and local authority. |
| Target rename | Rename GovernancePolicy·A01 after linking | The existing policy_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No policy_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### edition

Use human-readable text for `GovernancePolicyEdition.edition`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered edition in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No edition at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### text_version_ref

Use scoped or external reference for `GovernancePolicyEdition.text_version_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified text_version_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped text_version_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No text_version_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### digest

Use integrity fingerprint or opaque verifier for `GovernancePolicyEdition.digest`. Bind the algorithm or verifier scheme and object revision to the evidence.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified fingerprint of edition A | Bind the algorithm or verifier scheme and object revision to the evidence. |
| Malformed or unmapped | different fingerprint for the same purported bytes | Quarantine the mismatch or deny the claim. |
| An identical copy is rechecked | compare original bytes with verified copy | Equality confirms the checked bytes or verifier under the same scheme only. |
| New revision has changed content | different bytes under a new edition | Compute new evidence; preserve the prior verified revision. |
| A user knows a digest | unprivileged user presents a publicly observed fingerprint | Knowledge alone grants no additional access outside the documented token protocol. |
| Incomplete record | No digest at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### authorizing_resolution_id

The target is [Resolution](Resolution.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Resolution·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Resolution·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Resolution·MISSING | Queue the missing Resolution mapping or reject the command before linking. |
| Wrong scope | Resolution·B01 | Do not attach another church’s Resolution without a supported exchange and local authority. |
| Target rename | Rename Resolution·A01 after linking | The existing authorizing_resolution_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No authorizing_resolution_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### effective_from

Use civil calendar date for `GovernancePolicyEdition.effective_from`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No effective_from at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### effective_until

Use civil calendar date for `GovernancePolicyEdition.effective_until`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No effective_until provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### review_due_on

Use civil calendar date for `GovernancePolicyEdition.review_due_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No review_due_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### disposition

Declared alternatives in owner order: `adopt`, `amend`, `retire`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | adopt | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_disposition | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No disposition at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### acknowledgment_class

Declared alternatives in owner order: `none`, `read`, `affirm`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | none | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_acknowledgment_class | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No acknowledgment_class at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### predecessor_id

The target is [GovernancePolicyEdition](GovernancePolicyEdition.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GovernancePolicyEdition·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | GovernancePolicyEdition·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | GovernancePolicyEdition·MISSING | Queue the missing GovernancePolicyEdition mapping or reject the command before linking. |
| Wrong scope | GovernancePolicyEdition·B01 | Do not attach another church’s GovernancePolicyEdition without a supported exchange and local authority. |
| Target rename | Rename GovernancePolicyEdition·A01 after linking | The existing predecessor_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No predecessor_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [GovernancePolicyEdition](GovernancePolicyEdition.md).`predecessor_id` | GovernancePolicyEdition identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PolicyAcknowledgement](PolicyAcknowledgement.md).`edition_id` | GovernancePolicyEdition identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
