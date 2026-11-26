# IntegrationSubscription

[Integrations, exports and event delivery](../../platform/exchange-events.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Filter only approved event fields. Endpoints cannot subscribe beyond the principal's permissions.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `connection_id` | Ref(ConnectionProfile) | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `contract_id` | Ref(InterfaceEdition) | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `event_filter` | structured rule | Required when the record reaches its applicable state | [rule](../value-conventions.md#rule) |
| `delivery_mode` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `last_checkpoint` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `enabled_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `suspended_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### connection_id

The target is [ConnectionProfile](ConnectionProfile.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ConnectionProfile·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | ConnectionProfile·MISSING | Queue the missing ConnectionProfile mapping or reject the command before linking. |
| Wrong scope | ConnectionProfile·B01 | Do not attach another church’s ConnectionProfile without a supported exchange and local authority. |
| Target rename | Rename ConnectionProfile·A01 after linking | The existing connection_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No connection_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### contract_id

The target is [InterfaceEdition](InterfaceEdition.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | InterfaceEdition·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | InterfaceEdition·MISSING | Queue the missing InterfaceEdition mapping or reject the command before linking. |
| Wrong scope | InterfaceEdition·B01 | Do not attach another church’s InterfaceEdition without a supported exchange and local authority. |
| Target rename | Rename InterfaceEdition·A01 after linking | The existing contract_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No contract_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### event_filter

Use versioned structured decision or expression for `IntegrationSubscription.event_filter`. Check types, dependencies, owner, version and scope before activation.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | approved clause for event_filter | Check types, dependencies, owner, version and scope before activation. |
| Malformed or unmapped | cyclic or unbound condition in event_filter | Reject activation; retain last accepted edition. |
| Two rules at the same scope conflict | two matching clauses of equal priority | Use documented precedence or block publication for review. |
| Rule changes after a decision | rule version 2 proposed after version 1 approved the event | Keep the prior decision bound to its evaluated edition. |
| Preview a rule on an eligible sample | dry-run edition on locally approved test inputs | Explain matched conditions; produce no live effect. |
| Incomplete record | No event_filter at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### delivery_mode

Use versioned classification or status code for `IntegrationSubscription.delivery_mode`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active delivery_mode code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped delivery_mode code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No delivery_mode at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### last_checkpoint

Use human-readable text for `IntegrationSubscription.last_checkpoint`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered last_checkpoint in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No last_checkpoint provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### enabled_at

Use unambiguous point in time for `IntegrationSubscription.enabled_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No enabled_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### suspended_at

Use unambiguous point in time for `IntegrationSubscription.suspended_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No suspended_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [IntegrationDeliveryAttempt](IntegrationDeliveryAttempt.md).`subscription_id` | IntegrationSubscription identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
