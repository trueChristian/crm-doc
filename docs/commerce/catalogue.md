# Catalogue and offers

A product describes what people recognize. A variant identifies a sellable unit. An offer specifies where and to whom a variant may be supplied. This distinction lets one book description support physical and digital editions, collection at the church office and a gift of free access. [Inventory](inventory.md), [pricing](pricing.md) and [access](access.md) use stable identifiers even when a title changes.

## Logical records

| Table | Fields | Relationships and rules |
| --- | --- | --- |
| Product | organization_id ref Organization, catalogue_code code, kind physical/digital/service/bundle, title text, summary text?, description text?, owner_campus_id ref Campus?, state draft/in_review/published/withdrawn, published_at instant?, archived_at instant? | Catalogue code unique per organization. Withdrawal preserves historical sales. Search visibility requires an eligible active offer. |
| ProductTranslation | product_id ref Product, locale code, title text, description text?, accessibility_text text?, approval_state draft/approved | One approved translation per product and locale. Fall back to the published base description only where the audience can view it. |
| ProductVariant | product_id ref Product, sku code, unit_code code, format code?, mass quantity?, mass_unit code?, depth quantity?, width quantity?, height quantity?, length_unit code?, inventory_policy tracked/untracked/made_to_order, fulfilment_kind ship/collect/digital/service, tax_class code, state active/retired | Each sellable line references one variant. All measures positive when set. SKU unique per organization. Shipping requires enough dimensions for the chosen rate method. |
| VariantOption | product_id ref Product, key code, display_name text, position integer | Option key unique within product, e.g. language, cut or binding. |
| VariantOptionValue | variant_id ref ProductVariant, option_id ref VariantOption, value_code code, label text | Unique pair. Option and variant share product. Exact option combinations unique for active variants. |
| ProductIdentifier | variant_id ref ProductVariant, scheme code, issuer text, value text | Enforce unique organization/issuer/scheme/value for active scan identifiers. Unknown barcodes require explicit lookup and confirmation. |
| Category | organization_id ref Organization, parent_id ref Category?, code code, name text, order_index integer | Acyclic hierarchy. A variant may appear in multiple browse categories through its product. |
| ProductCategory | product_id ref Product, category_id ref Category, display_order integer | Unique pair. Category membership never widens visibility. |
| ProductAsset | product_id ref Product, variant_id ref ProductVariant?, media_ref opaque_ref, role cover/gallery/sample/instructions, alt_text text?, position integer, clearance_state pending/approved/withdrawn | Only cleared assets reach an eligible offer. Public samples require independently cleared rights. |
| BundlePart | bundle_variant_id ref ProductVariant, component_variant_id ref ProductVariant, units quantity, price_weight rate, fulfilment_rule included/optional_choice, choice_group code? | Reject self-reference and cycles across bundles. For chosen components, freeze quantities and allocated amounts at checkout. |
| ShopChannel | organization_id ref Organization, campus_id ref Campus?, code code, name text, kind storefront/counter/internal, currency code, locale code, time_zone text, active boolean | A channel belongs to one organization and can serve several congregations by configuration. |
| Offer | variant_id ref ProductVariant, channel_id ref ShopChannel, audience_policy_ref opaque_ref, availability_from instant, availability_until instant?, min_units quantity, max_units quantity?, supply_policy in_stock/preorder/backorder/unlimited, terms_version text, access_plan_id ref AccessPlan?, state draft/approved/paused/retired | A variant can have many offers. Digital delivery must define the grant or access policy. Active windows are half-open. Approved terms include cancellation, refund, renewal and delivery rules as applicable. |
| OfferLimit | offer_id ref Offer, unit_limit quantity, period once/day/week/event, subject account/verified_customer/order, event_ref opaque_ref? | Identify enforced scope and how guest orders qualify before publishing. Avoid collecting extra identifying data solely to enforce a weak limit. |

## Publication and ordering rules

An editor drafts the description, variants, translations and offers. A reviewer checks price availability, required tax classification, rights, stock policy and delivery methods. A preview displays what a guest, approved participant and staff member can see at each channel. Publication records the reviewed revision. A restricted offer must remain absent from public search, feeds, recommendations, metadata, images and purchase history lookups by unrelated users. Scheduled withdrawal closes new ordering at the boundary. Existing orders use their snapshots and retain agreed delivery or enter an explicit exception workflow.

Purchasable bundles declare whether parts ship together, fulfil independently or depend on a choice. Fixed component prices allocated for refunds and accounting must sum to the charged bundle amount. A scarce physical component limits the bundle. A duplicate digital component follows the [grant rules](access.md). Digital items provide a format summary, accessibility details and access duration before purchase. No entitlement to an unpublished or expired recording can be offered unless a preorder states its release condition and cancellation remedy.

## Acceptance examples

1. A staff member retires a large blue shirt and introduces a new supplier's equivalent. The replacement has a new SKU. A return against the old order still identifies the retired variant and its original selling price.
2. The last physical workbook is held in a bundle for one purchaser. A second basket sees the digital-only option or an explicit backorder according to offer terms. It cannot claim immediate delivery of the workbook.
3. A public shop visitor cannot discover a members-only retreat recording by searching the speaker, browsing its category, guessing its offer identifier or requesting a cover image. A permitted purchaser can find the approved version.
4. A channel's product is visible in two languages. An editor updates its title while an order is being placed. The confirmed order records exactly the title, terms and currency shown in the accepted quote.
