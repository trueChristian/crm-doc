# ProgramServiceTerms

[Agreements, service rounds and relief distribution](../../administration/community-programs.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Add operational terms to a specific agreement. A budget is a ceiling. It never authorizes an individual payment.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | Owner-scoped business value; see the record rule | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `agreement_id` | → PartnershipAgreement | Required at applicable lifecycle step | [relation](../value-conventions.md#relation) |
| `project_id` | → MissionProject | Required at applicable lifecycle step | [relation](../value-conventions.md#relation) |
| `aid_program_id` | → AidProgram | Required at applicable lifecycle step | [relation](../value-conventions.md#relation) |
| `service_area` | text | Required at applicable lifecycle step | [text](../value-conventions.md#text) |
| `valid_from` | dates | Required at applicable lifecycle step | [date](../value-conventions.md#date) |
| `valid_until` | dates | Required at applicable lifecycle step | [date](../value-conventions.md#date) |
| `eligibility_policy_ref` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [resource](../value-conventions.md#resource) |
| `approved_budget_ref` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [resource](../value-conventions.md#resource) |
| `report_due_rule` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [rule](../value-conventions.md#rule) |
| `disclosure_limits` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [structured](../value-conventions.md#structured) |
| `signatories` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [list](../value-conventions.md#list) |
| `evidence_ref` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `ProgramServiceTerms.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ProgramServiceTerms·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### agreement_id

The target is [PartnershipAgreement](../development/PartnershipAgreement.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | PartnershipAgreement·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | PartnershipAgreement·MISSING | Queue the missing PartnershipAgreement mapping or reject the command before linking. |
| Wrong scope | PartnershipAgreement·B01 | Do not attach another church’s PartnershipAgreement without a supported exchange and local authority. |
| Target rename | Rename PartnershipAgreement·A01 after linking | The existing agreement_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No agreement_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### project_id

The target is [MissionProject](../ministry/MissionProject.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MissionProject·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | MissionProject·MISSING | Queue the missing MissionProject mapping or reject the command before linking. |
| Wrong scope | MissionProject·B01 | Do not attach another church’s MissionProject without a supported exchange and local authority. |
| Target rename | Rename MissionProject·A01 after linking | The existing project_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No project_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### aid_program_id

The target is [AidProgram](../people/AidProgram.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AidProgram·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | AidProgram·MISSING | Queue the missing AidProgram mapping or reject the command before linking. |
| Wrong scope | AidProgram·B01 | Do not attach another church’s AidProgram without a supported exchange and local authority. |
| Target rename | Rename AidProgram·A01 after linking | The existing aid_program_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No aid_program_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### service_area

Use human-readable text for `ProgramServiceTerms.service_area`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered service_area in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No service_area at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### valid_from

Use civil calendar date for `ProgramServiceTerms.valid_from`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No valid_from at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### valid_until

Use civil calendar date for `ProgramServiceTerms.valid_until`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No valid_until at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### eligibility_policy_ref

Use scoped or external reference for `ProgramServiceTerms.eligibility_policy_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified eligibility_policy_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped eligibility_policy_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No eligibility_policy_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### approved_budget_ref

Use scoped or external reference for `ProgramServiceTerms.approved_budget_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified approved_budget_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped approved_budget_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No approved_budget_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### report_due_rule

Use versioned structured decision or expression for `ProgramServiceTerms.report_due_rule`. Check types, dependencies, owner, version and scope before activation.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | approved clause for report_due_rule | Check types, dependencies, owner, version and scope before activation. |
| Malformed or unmapped | cyclic or unbound condition in report_due_rule | Reject activation; retain last accepted edition. |
| Two rules at the same scope conflict | two matching clauses of equal priority | Use documented precedence or block publication for review. |
| Rule changes after a decision | rule version 2 proposed after version 1 approved the event | Keep the prior decision bound to its evaluated edition. |
| Preview a rule on an eligible sample | dry-run edition on locally approved test inputs | Explain matched conditions; produce no live effect. |
| Incomplete record | No report_due_rule at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### disclosure_limits

Use typed value or bounded compound record for `ProgramServiceTerms.disclosure_limits`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of disclosure_limits matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for disclosure_limits | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Incomplete record | No disclosure_limits at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### signatories

Use ordered collection or mathematical set for `ProgramServiceTerms.signatories`. Preserve ordering when meaningful; enforce uniqueness when the declaration is a set.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted members A and B | Preserve ordering when meaningful; enforce uniqueness when the declaration is a set. |
| Malformed or unmapped | an element outside the declared domain | Reject the affected collection or stage its invalid item under the import policy. |
| Same element appears twice | A, A, B | Apply declared sequence/set multiplicity without doubling financial or voting effects. |
| Empty collection versus unknown collection | empty collection and missing collection | Preserve the distinction where the rule requires evidence. |
| One element later becomes restricted | authorization for member B withdrawn before export | Recompute permitted projection before export or display. |
| Incomplete record | No signatories at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### evidence_ref

Use scoped or external reference for `ProgramServiceTerms.evidence_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified evidence_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped evidence_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No evidence_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AssistanceRound](AssistanceRound.md).`terms_id` | ProgramServiceTerms identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProgramFeedback](ProgramFeedback.md).`terms_id` | ProgramServiceTerms identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProgramIndicator](ProgramIndicator.md).`terms_id` | ProgramServiceTerms identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
