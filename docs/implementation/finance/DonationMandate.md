# DonationMandate

Evidence of the donor’s permission for scheduled collections by an external payment service.

Credentials, bank details and card numbers remain with the provider. One operation key per mandate and due occurrence. Record external capture before verifying a monetary gift. A revocation stops new requests and routes in-flight captures for review.

Organization scope, revision and audit information follow the [shared record conventions](../../foundation/record-conventions.md).

## Fields

| Field | Declaration | Use |
| --- | --- | --- |
| `giving_party_id` | `ref GivingParty` | Donor authorizing collections. [GivingParty](GivingParty.md). |
| `provider_ref` | `opaque_ref` | Account and tokenized mandate reference. |
| `currency` | `code` | Currency approved by the donor. |
| `amount` | `money` | Authorized amount per occurrence. |
| `schedule` | `rule` | Frequency, anchor, start and optional end date. |
| `allocation_plan` | `protected_ref` | Agreed designations. |
| `consent_ref` | `protected_ref` | Terms, version and time of consent. |
| `state` | `pending/active/paused/revoked/expired` | Latest confirmed mandate state. |

## Acceptance decision

A provider times out on a scheduled request. The operator looks up the occurrence using its original key. A successful later callback yields one gift. A failed attempt adds no received money.

[Offerings, gifts and donor correspondence](../../finance/giving.md) · [Giving record index](README.md)
