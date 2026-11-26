# LegacyNotice

[Donor service and gift acceptance](../../development/donor-service.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Allow a confidential intention with no value and withdrawal without solicitation. Restrict estate and family contact details. Verification of an executor and grant of authority precedes action or disclosure.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `giving_party_id` | ref GivingParty? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `adviser_contact_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `assessment_id` | ref GiftOfferAssessment? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `stage` | enquiry/intent_recorded/notification/administration/distributed/withdrawn | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `disclosure_scope` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `asset_description` | protected_text? | Optional under owner conditions | [protected](../value-conventions.md#protected) |
| `estimated_amount` | money? | Optional under owner conditions | [money](../value-conventions.md#money) |
| `currency` | code? | Optional under owner conditions | [currency](../value-conventions.md#currency) |
| `terms_evidence_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `administrator_contact_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `next_review` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `received_gift_id` | ref Gift? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### giving_party_id

The target is [GivingParty](../finance/GivingParty.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GivingParty·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | GivingParty·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | GivingParty·MISSING | Queue the missing GivingParty mapping or reject the command before linking. |
| Wrong scope | GivingParty·B01 | Do not attach another church’s GivingParty without a supported exchange and local authority. |
| Target rename | Rename GivingParty·A01 after linking | The existing giving_party_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No giving_party_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### adviser_contact_ref

Use scoped or external reference for `LegacyNotice.adviser_contact_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified adviser_contact_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped adviser_contact_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No adviser_contact_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### assessment_id

The target is [GiftOfferAssessment](GiftOfferAssessment.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GiftOfferAssessment·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | GiftOfferAssessment·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | GiftOfferAssessment·MISSING | Queue the missing GiftOfferAssessment mapping or reject the command before linking. |
| Wrong scope | GiftOfferAssessment·B01 | Do not attach another church’s GiftOfferAssessment without a supported exchange and local authority. |
| Target rename | Rename GiftOfferAssessment·A01 after linking | The existing assessment_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No assessment_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### stage

Declared alternatives in owner order: `enquiry`, `intent_recorded`, `notification`, `administration`, `distributed`, `withdrawn`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | enquiry | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_stage | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No stage at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### disclosure_scope

Use versioned classification or status code for `LegacyNotice.disclosure_scope`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active disclosure_scope code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped disclosure_scope code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No disclosure_scope at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### asset_description

Use restricted value or protected content reference for `LegacyNotice.asset_description`. Keep value and purpose together; apply field-level authority to projections.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted asset_description supplied in a restricted context | Keep value and purpose together; apply field-level authority to projections. |
| Malformed or unmapped | public disclosure without authority | Withhold publication unless the specific disclosure rule permits it. |
| Search snippet or autocomplete | restricted fact returned in type-ahead search | Filter before returning any protected content or revealing its existence. |
| Authorized report excludes this field | otherwise permitted export excludes the restricted field | Omit it from hidden metadata and attachments as well. |
| Approval withdrawn after a preview | draft was previewed before authority was withdrawn | Recheck at release; keep only permitted audit evidence. |
| Absent in intake | No asset_description provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### estimated_amount

Use exact monetary amount with currency for `LegacyNotice.estimated_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Absent in intake | No estimated_amount provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### currency

Use monetary unit code for `LegacyNotice.currency`. Resolve the code and its precision as of the transaction.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD | Resolve the code and its precision as of the transaction. |
| Malformed or unmapped | ambiguous $ | Request the unambiguous currency. |
| Two amounts have different currencies | 24.50 NAD and 24.50 USD | Report separate totals or translate using recorded rates. |
| Catalog changes after document issue | document issued before currency-profile revision | The stored document keeps its currency. |
| Unrecognized imported code | unmapped monetary unit in staged transaction | Stage unmapped currency; block financial posting. |
| Absent in intake | No currency provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### terms_evidence_ref

Use scoped or external reference for `LegacyNotice.terms_evidence_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified terms_evidence_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped terms_evidence_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No terms_evidence_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### administrator_contact_ref

Use scoped or external reference for `LegacyNotice.administrator_contact_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified administrator_contact_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped administrator_contact_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No administrator_contact_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### next_review

Use civil calendar date for `LegacyNotice.next_review`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No next_review provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### received_gift_id

The target is [Gift](../finance/Gift.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Gift·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Gift·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Gift·MISSING | Queue the missing Gift mapping or reject the command before linking. |
| Wrong scope | Gift·B01 | Do not attach another church’s Gift without a supported exchange and local authority. |
| Target rename | Rename Gift·A01 after linking | The existing received_gift_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No received_gift_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
