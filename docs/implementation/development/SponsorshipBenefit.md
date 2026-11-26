# SponsorshipBenefit

[Partnerships, sponsorships and impact](../../development/partnerships.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Define the tangible benefit, permitted placement, territory, time and brand use. Finance reviews exchange value, eligible contribution amount, invoice and receipt treatment.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `agreement_id` | ref PartnershipAgreement | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `delivering_party_id` | ref AgreementParty | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `receiving_party_id` | ref AgreementParty | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `kind` | logo_space/tickets/advertising/venue/printing/other | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `description` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `committed_quantity` | decimal | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `unit` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `estimated_exchange_value` | money? | Optional under owner conditions | [money](../value-conventions.md#money) |
| `currency` | code? | Optional under owner conditions | [currency](../value-conventions.md#currency) |
| `valuation_evidence_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `approval_scope_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### agreement_id

The target is [PartnershipAgreement](PartnershipAgreement.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | PartnershipAgreement·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | PartnershipAgreement·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | PartnershipAgreement·MISSING | Queue the missing PartnershipAgreement mapping or reject the command before linking. |
| Wrong scope | PartnershipAgreement·B01 | Do not attach another church’s PartnershipAgreement without a supported exchange and local authority. |
| Target rename | Rename PartnershipAgreement·A01 after linking | The existing agreement_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No agreement_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### delivering_party_id

The target is [AgreementParty](AgreementParty.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AgreementParty·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | AgreementParty·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | AgreementParty·MISSING | Queue the missing AgreementParty mapping or reject the command before linking. |
| Wrong scope | AgreementParty·B01 | Do not attach another church’s AgreementParty without a supported exchange and local authority. |
| Target rename | Rename AgreementParty·A01 after linking | The existing delivering_party_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No delivering_party_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### receiving_party_id

The target is [AgreementParty](AgreementParty.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AgreementParty·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | AgreementParty·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | AgreementParty·MISSING | Queue the missing AgreementParty mapping or reject the command before linking. |
| Wrong scope | AgreementParty·B01 | Do not attach another church’s AgreementParty without a supported exchange and local authority. |
| Target rename | Rename AgreementParty·A01 after linking | The existing receiving_party_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No receiving_party_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### kind

Declared alternatives in owner order: `logo_space`, `tickets`, `advertising`, `venue`, `printing`, `other`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | logo_space | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_kind | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### description

Use human-readable text for `SponsorshipBenefit.description`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered description in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No description at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### committed_quantity

Use exact decimal measure for `SponsorshipBenefit.committed_quantity`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No committed_quantity at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### unit

Use versioned classification or status code for `SponsorshipBenefit.unit`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active unit code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped unit code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No unit at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### estimated_exchange_value

Use exact monetary amount with currency for `SponsorshipBenefit.estimated_exchange_value`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Absent in intake | No estimated_exchange_value provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### currency

Use monetary unit code for `SponsorshipBenefit.currency`. Resolve the code and its precision as of the transaction.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD | Resolve the code and its precision as of the transaction. |
| Malformed or unmapped | ambiguous $ | Request the unambiguous currency. |
| Two amounts have different currencies | 24.50 NAD and 24.50 USD | Report separate totals or translate using recorded rates. |
| Catalog changes after document issue | document issued before currency-profile revision | The stored document keeps its currency. |
| Unrecognized imported code | unmapped monetary unit in staged transaction | Stage unmapped currency; block financial posting. |
| Absent in intake | No currency provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### valuation_evidence_ref

Use scoped or external reference for `SponsorshipBenefit.valuation_evidence_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified valuation_evidence_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped valuation_evidence_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No valuation_evidence_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### approval_scope_ref

Use scoped or external reference for `SponsorshipBenefit.approval_scope_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified approval_scope_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped approval_scope_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No approval_scope_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [BenefitDelivery](BenefitDelivery.md).`benefit_id` | SponsorshipBenefit identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
