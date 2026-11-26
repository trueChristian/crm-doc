# LanguageEdition

[Inclusive workflows and international presentation](../../platform/experience-accessibility.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique resource, edition and language. Store approval separately for each translation, and mark stale when its source changes.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `content_ref` | ResourceRef | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `source_revision` | integer | Required when the record reaches its applicable state | [version](../value-conventions.md#version) |
| `locale` | tag | Required when the record reaches its applicable state | [language](../value-conventions.md#language) |
| `direction` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `status` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `title` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `body_ref` | ResourceRef | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `translator_ref` | ResourceRef? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `review_by` | Ref(UserAccount)? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `published_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### content_ref

Use scoped or external reference for `LanguageEdition.content_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified content_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped content_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No content_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### source_revision

Use revision number or opaque revision token for `LanguageEdition.source_revision`. Compare under the declared revision scheme. Require the expected version for conflicting work.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | the current revision returned by the owner | Compare under the declared revision scheme. Require the expected version for conflicting work. |
| Malformed or unmapped | superseded version presented for a new approval | Reject or reopen review against the current contents. |
| Two operators begin at revision seven | two edits both cite baseline 7 | Commit the first change once and re-evaluate the second; never overwrite an unreviewed difference. |
| Re-read an already approved revision | re-open issued revision 4 after revision 6 | Return the frozen value and evidence for that edition. |
| Replay of an earlier result | same business operation observed at two revisions | Correlate by the business operation identity; a newer version does not create a second effect. |
| Incomplete record | No source_revision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### locale

Use language or locale identifier for `LanguageEdition.locale`. Resolve the published language or locale without inferring a person’s nationality.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | en | Resolve the published language or locale without inferring a person’s nationality. |
| Malformed or unmapped | unmapped locale display label | Keep the source value for review. |
| Specific translation unavailable | specific translation missing at delivery time | Apply the declared fallback and identify which language is being displayed. |
| User changes preferred language | approved letter after preferred-language change | Future communications use the effective preference; issued wording is preserved. |
| Two regional variants exist | two permitted regional variants in catalogue | Apply the requested locale/version where available. |
| Incomplete record | No locale at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### direction

Use versioned classification or status code for `LanguageEdition.direction`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active direction code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped direction code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No direction at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### status

Use versioned classification or status code for `LanguageEdition.status`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active status code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped status code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No status at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### title

Use human-readable text for `LanguageEdition.title`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered title in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No title provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### body_ref

Use scoped or external reference for `LanguageEdition.body_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified body_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped body_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No body_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### translator_ref

Use scoped or external reference for `LanguageEdition.translator_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified translator_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped translator_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No translator_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### review_by

The target is [UserAccount](UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing review_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No review_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### published_at

Use unambiguous point in time for `LanguageEdition.published_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No published_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
