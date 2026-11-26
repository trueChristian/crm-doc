# GivingDocumentItem

A fixed, reproducible inclusion in a reviewed donor document.

Select one primary source per item. When adjustment is selected, reach its original allocation through its parent. Preserve original-currency grouping and issuer evidence. Document totals are reconstructed from the fixed edition.

Organization scope, revision and audit information follow the [shared record conventions](../../foundation/record-conventions.md).

## Fields

| Field | Declaration | Use |
| --- | --- | --- |
| `document_id` | `ref GivingDocument` | Issued or prepared edition. [GivingDocument](GivingDocument.md). |
| `line_key` | `text` | Unique line within the document. |
| `allocation_id` | `ref GiftAllocation?` | Monetary gift portion. [GiftAllocation](GiftAllocation.md). |
| `adjustment_id` | `ref GiftAdjustment?` | Confirmed correction affecting the portion. [GiftAdjustment](GiftAdjustment.md). |
| `in_kind_gift_id` | `ref InKindGift?` | Accepted goods acknowledged descriptively. [InKindGift](InKindGift.md). |
| `display_value` | `text` | Issued amount with currency or item description. |
| `basis_ref` | `protected_ref?` | Issuer eligibility determination where applicable. |

## Acceptance decision

A statement displays 100 given, followed by a 20 return in its covered interval. The net is 80. A public recognition credit and a custody count never produce statement lines.

[Offerings, gifts and donor correspondence](../../finance/giving.md) · [Giving record index](README.md)
