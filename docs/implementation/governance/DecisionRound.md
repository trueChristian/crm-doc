# DecisionRound

[Deliberation and voting](../../governance/deliberation-and-voting.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Exactly one motion or election. Persist tie handling, eligible totals and rule revision. Opening freezes the text and round rules. Written or asynchronous decisions require explicit authority, a fixed closing instant and a recorded quorum basis.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `motion_id` | Motion ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `election_id` | ElectionContest ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `roll_id` | MeetingRoll ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `quorum_id` | QuorumCheck ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `round_number` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `proposal_snapshot` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `method` | consensus/show_of_hands/named/secret/written | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `threshold_rule` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `denominator_basis` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `secrecy_class` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `opened_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `closed_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `state` | prepared/open/frozen/certified/void | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

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

### election_id

The target is [ElectionContest](ElectionContest.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ElectionContest·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ElectionContest·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ElectionContest·MISSING | Queue the missing ElectionContest mapping or reject the command before linking. |
| Wrong scope | ElectionContest·B01 | Do not attach another church’s ElectionContest without a supported exchange and local authority. |
| Target rename | Rename ElectionContest·A01 after linking | The existing election_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No election_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### roll_id

The target is [MeetingRoll](MeetingRoll.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MeetingRoll·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | MeetingRoll·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | MeetingRoll·MISSING | Queue the missing MeetingRoll mapping or reject the command before linking. |
| Wrong scope | MeetingRoll·B01 | Do not attach another church’s MeetingRoll without a supported exchange and local authority. |
| Target rename | Rename MeetingRoll·A01 after linking | The existing roll_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No roll_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### quorum_id

The target is [QuorumCheck](QuorumCheck.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | QuorumCheck·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | QuorumCheck·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | QuorumCheck·MISSING | Queue the missing QuorumCheck mapping or reject the command before linking. |
| Wrong scope | QuorumCheck·B01 | Do not attach another church’s QuorumCheck without a supported exchange and local authority. |
| Target rename | Rename QuorumCheck·A01 after linking | The existing quorum_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No quorum_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### round_number

Use whole-number measure for `DecisionRound.round_number`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No round_number at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### proposal_snapshot

Use human-readable text for `DecisionRound.proposal_snapshot`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered proposal_snapshot in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No proposal_snapshot at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### method

Declared alternatives in owner order: `consensus`, `show_of_hands`, `named`, `secret`, `written`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | consensus | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_method | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No method at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### threshold_rule

Use versioned classification or status code for `DecisionRound.threshold_rule`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active threshold_rule code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped threshold_rule code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No threshold_rule at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### denominator_basis

Use versioned classification or status code for `DecisionRound.denominator_basis`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active denominator_basis code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped denominator_basis code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No denominator_basis at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### secrecy_class

Use versioned classification or status code for `DecisionRound.secrecy_class`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active secrecy_class code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped secrecy_class code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No secrecy_class at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### opened_at

Use unambiguous point in time for `DecisionRound.opened_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No opened_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### closed_at

Use unambiguous point in time for `DecisionRound.closed_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No closed_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Declared alternatives in owner order: `prepared`, `open`, `frozen`, `certified`, `void`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | prepared | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AnonymousBallot](AnonymousBallot.md).`round_id` | DecisionRound identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DecisionRuling](DecisionRuling.md).`replacement_round_id` | DecisionRound identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DecisionRuling](DecisionRuling.md).`round_id` | DecisionRound identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MinuteItem](MinuteItem.md).`decision_round_id` | DecisionRound identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ResultCount](ResultCount.md).`round_id` | DecisionRound identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [VotingEntitlement](VotingEntitlement.md).`round_id` | DecisionRound identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
