# SolicitationAppeal

[Campaigns and specialized gifts](../../finance/special-giving.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Distinguish solicitation channel from gift channel. Keep outreach preferences and public anonymity intact.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `campaign_id` | → GivingCampaign | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `code` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `channel_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `audience_snapshot_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `issue_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `ask_amount` | money? | Optional under owner conditions | [money](../value-conventions.md#money) |
| `consent_scope` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `cost_source_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `response_window_days` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### campaign_id

The target is [GivingCampaign](GivingCampaign.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GivingCampaign·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | GivingCampaign·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | GivingCampaign·MISSING | Queue the missing GivingCampaign mapping or reject the command before linking. |
| Wrong scope | GivingCampaign·B01 | Do not attach another church’s GivingCampaign without a supported exchange and local authority. |
| Target rename | Rename GivingCampaign·A01 after linking | The existing campaign_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No campaign_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### code

Use human-readable text for `SolicitationAppeal.code`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered code in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### channel_ref

Use scoped or external reference for `SolicitationAppeal.channel_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified channel_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped channel_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No channel_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### audience_snapshot_ref

Use scoped or external reference for `SolicitationAppeal.audience_snapshot_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified audience_snapshot_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped audience_snapshot_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No audience_snapshot_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### issue_on

Use civil calendar date for `SolicitationAppeal.issue_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No issue_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### ask_amount

Use exact monetary amount with currency for `SolicitationAppeal.ask_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Absent in intake | No ask_amount provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### consent_scope

Use versioned classification or status code for `SolicitationAppeal.consent_scope`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active consent_scope code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped consent_scope code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No consent_scope at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### cost_source_ref

Use scoped or external reference for `SolicitationAppeal.cost_source_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified cost_source_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped cost_source_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No cost_source_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### response_window_days

Use whole-number measure for `SolicitationAppeal.response_window_days`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No response_window_days at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
