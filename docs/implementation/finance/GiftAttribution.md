# GiftAttribution

Credit for a person or organization associated with a gift, separate from the payer and giver.

A recognition credit carries no monetary claim or entitlement to correspondence about another giver. Revocation removes future publication and preserves history of authorized releases.

Organization scope, revision and audit information follow the [shared record conventions](../../foundation/record-conventions.md).

## Fields

| Field | Declaration | Use |
| --- | --- | --- |
| `gift_id` | `ref Gift` | Original contribution. [Gift](Gift.md). |
| `credited_party_ref` | `protected_ref` | Person, organization or permitted memorial identity. |
| `role` | `code` | Memorial, tribute, adviser, referrer or sponsor recognition. |
| `publicity_scope` | `code` | Authorized audience. |
| `label` | `text?` | Approved wording for that audience. |
| `instruction_ref` | `protected_ref` | Evidence and duration of permission. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [DevelopmentCreditInstruction](../development/DevelopmentCreditInstruction.md).`finance_attribution_id` | GiftAttribution identity | Reconcile the reference in the source record and preserve its correction history. |
| [TributeInstruction](../development/TributeInstruction.md).`gift_attribution_id` | GiftAttribution identity | Reconcile the reference in the source record and preserve its correction history. |

## Acceptance decision

A memorial offering has a legal donor, an honoree and a family notice recipient. Only the donor receives their giving statement. The family notice uses its separate instruction.

[Offerings, gifts and donor correspondence](../../finance/giving.md) · [Giving record index](README.md)
