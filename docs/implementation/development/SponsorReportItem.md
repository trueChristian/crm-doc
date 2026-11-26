# SponsorReportItem

[Grant applications and reporting](../../development/grant-applications.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Cite an owned internal fact, approved evidence or explanatory narrative. Exclude identifiable beneficiary data by default. Record estimate vs observed measure, period and units.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `report_id` | ref SponsorReport | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `outcome_id` | ref ProjectOutcome? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `award_cost_id` | ref AwardCost? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `finance_snapshot_id` | ref ReportSnapshot? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `narrative_text` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `evidence_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `disclosure_authority_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `reporting_basis` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### report_id

The target is [SponsorReport](SponsorReport.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | SponsorReport·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | SponsorReport·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | SponsorReport·MISSING | Queue the missing SponsorReport mapping or reject the command before linking. |
| Wrong scope | SponsorReport·B01 | Do not attach another church’s SponsorReport without a supported exchange and local authority. |
| Target rename | Rename SponsorReport·A01 after linking | The existing report_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No report_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### outcome_id

The target is [ProjectOutcome](../ministry/ProjectOutcome.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ProjectOutcome·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ProjectOutcome·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ProjectOutcome·MISSING | Queue the missing ProjectOutcome mapping or reject the command before linking. |
| Wrong scope | ProjectOutcome·B01 | Do not attach another church’s ProjectOutcome without a supported exchange and local authority. |
| Target rename | Rename ProjectOutcome·A01 after linking | The existing outcome_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No outcome_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### award_cost_id

The target is [AwardCost](../finance/AwardCost.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AwardCost·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | AwardCost·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | AwardCost·MISSING | Queue the missing AwardCost mapping or reject the command before linking. |
| Wrong scope | AwardCost·B01 | Do not attach another church’s AwardCost without a supported exchange and local authority. |
| Target rename | Rename AwardCost·A01 after linking | The existing award_cost_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No award_cost_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### finance_snapshot_id

The target is [ReportSnapshot](../finance/ReportSnapshot.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ReportSnapshot·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ReportSnapshot·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ReportSnapshot·MISSING | Queue the missing ReportSnapshot mapping or reject the command before linking. |
| Wrong scope | ReportSnapshot·B01 | Do not attach another church’s ReportSnapshot without a supported exchange and local authority. |
| Target rename | Rename ReportSnapshot·A01 after linking | The existing finance_snapshot_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No finance_snapshot_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### narrative_text

Use human-readable text for `SponsorReportItem.narrative_text`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered narrative_text in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No narrative_text provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### evidence_ref

Use scoped or external reference for `SponsorReportItem.evidence_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified evidence_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped evidence_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No evidence_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### disclosure_authority_ref

Use scoped or external reference for `SponsorReportItem.disclosure_authority_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified disclosure_authority_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped disclosure_authority_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No disclosure_authority_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### reporting_basis

Use versioned classification or status code for `SponsorReportItem.reporting_basis`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active reporting_basis code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped reporting_basis code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No reporting_basis at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
