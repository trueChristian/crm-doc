# GivingDocument

A donor-facing acknowledgement or statement edition, or a reference to one issued by an authorized external system.

The CRM may issue courtesy acknowledgements or giving history. When a separate receipt issuer is designated, hold official output until its authorized copy/reference arrives. Redelivery uses the existing edition and rechecks recipient authority. A correction preserves both versions.

Organization scope, revision and audit information follow the [shared record conventions](../../foundation/record-conventions.md).

## Fields

| Field | Declaration | Use |
| --- | --- | --- |
| `giving_party_id` | `ref GivingParty` | Authorized giving identity. [GivingParty](GivingParty.md). |
| `kind` | `acknowledgement/history/official_receipt/correction` | Type presented to the donor. |
| `issuer_ref` | `opaque_ref` | One designated issuer for the kind, church and covered transactions. |
| `issuer_key` | `text` | Unique document number or stable external edition. |
| `period_start` | `date` | First included local date. |
| `period_end` | `date` | Last included local date. |
| `snapshot_ref` | `protected_ref` | Fixed identity, language, covered lines, dates and meaning at issuance. |
| `replaces_id` | `ref GivingDocument?` | Original when corrected. [GivingDocument](GivingDocument.md). |
| `issued_at` | `instant?` | Actual issuance. |
| `state` | `prepared/issued/superseded/withdrawn` | Distinct from delivery outcome. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [GivingDocument](GivingDocument.md).`replaces_id` | GivingDocument identity | Reconcile the reference in the source record and preserve its correction history. |
| [GivingDocumentItem](GivingDocumentItem.md).`document_id` | GivingDocument identity | Reconcile the reference in the source record and preserve its correction history. |
| [StewardshipAction](../development/StewardshipAction.md).`related_document_id` | GivingDocument identity | Reconcile the reference in the source record and preserve its correction history. |

## Acceptance decision

A changed address after mailing does not silently change the issued document. A copy for the same permitted recipient uses its original identifier. The audit records redelivery separately.

[Offerings, gifts and donor correspondence](../../finance/giving.md) · [Giving record index](README.md)
