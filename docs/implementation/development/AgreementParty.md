# AgreementParty

[Partnerships, sponsorships and impact](../../development/partnerships.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Identify one represented party per row. Many parties may share an agreement. Official signatory and routine point of contact can differ. Contacts require usable permissions.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `agreement_id` | ref PartnershipAgreement | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `partner_id` | ref MinistryPartner? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `internal_organization_id` | ref Organization? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `project_role_id` | ref ProjectPartnerRole? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `designation` | lead/funder/host/delivery_partner/sponsor/beneficiary | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `authority_evidence_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `signed_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `assigned_contact_id` | ref Person? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

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

### partner_id

The target is [MinistryPartner](../ministry/MinistryPartner.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MinistryPartner·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | MinistryPartner·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | MinistryPartner·MISSING | Queue the missing MinistryPartner mapping or reject the command before linking. |
| Wrong scope | MinistryPartner·B01 | Do not attach another church’s MinistryPartner without a supported exchange and local authority. |
| Target rename | Rename MinistryPartner·A01 after linking | The existing partner_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No partner_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### internal_organization_id

The target is [Organization](../foundation/Organization.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Organization·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Organization·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Organization·MISSING | Queue the missing Organization mapping or reject the command before linking. |
| Wrong scope | Organization·B01 | Do not attach another church’s Organization without a supported exchange and local authority. |
| Target rename | Rename Organization·A01 after linking | The existing internal_organization_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No internal_organization_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### project_role_id

The target is [ProjectPartnerRole](../ministry/ProjectPartnerRole.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ProjectPartnerRole·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ProjectPartnerRole·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ProjectPartnerRole·MISSING | Queue the missing ProjectPartnerRole mapping or reject the command before linking. |
| Wrong scope | ProjectPartnerRole·B01 | Do not attach another church’s ProjectPartnerRole without a supported exchange and local authority. |
| Target rename | Rename ProjectPartnerRole·A01 after linking | The existing project_role_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No project_role_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### designation

Declared alternatives in owner order: `lead`, `funder`, `host`, `delivery_partner`, `sponsor`, `beneficiary`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | lead | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_designation | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No designation at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### authority_evidence_ref

Use scoped or external reference for `AgreementParty.authority_evidence_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified authority_evidence_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped authority_evidence_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No authority_evidence_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### signed_at

Use unambiguous point in time for `AgreementParty.signed_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No signed_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### assigned_contact_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing assigned_contact_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No assigned_contact_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [PartnerPromise](PartnerPromise.md).`party_id` | AgreementParty identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SponsorshipBenefit](SponsorshipBenefit.md).`delivering_party_id` | AgreementParty identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SponsorshipBenefit](SponsorshipBenefit.md).`receiving_party_id` | AgreementParty identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
