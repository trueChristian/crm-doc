# Bringing records in and keeping them trustworthy

A new church can move from paper registers, spreadsheets and earlier software in stages. The migration lead owns a signed scope stating which years, congregations, kinds of evidence, attachments, restrictions, outstanding handoffs and historic gift records transfer. The applicable departmental custodian signs the reconciliation. Preserve a human-readable record of omissions and the reason for each.

## Logical records

| Entity | Fields | Relationship and constraint |
|---|---|---|
| DataSource | source_key code, label text, owner_id Ref(UserAccount), source_timezone zone, default_language tag, sensitivity code, state code | One source provides many batches and crosswalks. Store its stable key through later replacements. |
| MappingEdition | source_id Ref(DataSource), target_entity code, edition integer, rules list(structured mapping), required_fields set(code), dictionary_revision text, approved_by Ref(UserAccount)?, approved_at instant? | Each rule maps a named column to a field with type, null policy, transform, vocabulary map and loss policy. Lock published editions. |
| ImportBatch | source_id Ref(DataSource), mapping_id Ref(MappingEdition), mode code, file_manifest_ref ResourceRef, input_digest text, as_of instant?, submitted_by Ref(UserAccount), state code, cutoff_at instant?, summary structured counts | Many staged rows. Idempotency key combines source, digest, mapping and intended run scope. |
| ImportRow | batch_id Ref(ImportBatch), source_row_key text, source_object_key text?, original_digest text, staged_value_ref ResourceRef, normalized_value_ref ResourceRef?, result code, issue_keys set(code), target_ref ResourceRef?, target_revision integer? | Unique row key per batch. Bulk access to staged personal data is restricted and expires. |
| ExternalKey | source_id Ref(DataSource), source_type code, external_key text, target_ref ResourceRef, first_seen_at instant, last_seen_at instant | Unique source/type/external key. Protect leading zeros and case when meaningful. Many historical keys can point to a canonical target. |
| QualityIssue | issue_kind code, affected_ref ResourceRef, field_keys set(code), severity code, evidence_ref ResourceRef?, state code, assigned_to Ref(UserAccount)?, decision text?, reviewed_at instant? | Group similar issues for reporting. Resolving requires the corrected value or an accepted exception and review date. |
| DuplicateCandidate | left_ref ResourceRef, right_ref ResourceRef, match_signals set(code), confidence_band code, state code, reviewed_by Ref(UserAccount)?, reason text? | Ordered pair unique per active comparison. Match within the authorized isolation boundary. Never expose hidden candidate fields to an unauthorized operator. |
| MergeDecision | survivor_ref ResourceRef, losing_ref ResourceRef, decided_by Ref(UserAccount), approved_by Ref(UserAccount)?, field_choices structured map, dependency_plan_ref ResourceRef, before_ref ResourceRef, applied_at instant?, reversed_by_ref Ref(MergeDecision)? | A merge retains a redirect and prior values according to policy. Lock both records during application. |
| ReconciliationCheck | batch_id Ref(ImportBatch), check_type code, dimension_key text, source_value exact value, target_value exact value, tolerance exact value, variance_reason text?, signed_by Ref(UserAccount)?, signed_at instant? | Monetary controls require currency, precision, fund and period. Differences outside tolerance block acceptance. |

## Import lifecycle and cutover

1. Inventory source authority and field ownership. Identify duplicates, multi-value cells, lost leading zeros, impossible dates, delayed transfers and missing photos. Distinguish zero from empty and explicitly cleared from absent. Keep partial birth dates at their actual precision. A report of suspect ages does not fill in birth dates.
2. Start a dry run in a scoped staging area. Recognize encoding, delimiter, dates, decimal separators, phone format, time zone and translated codes. Validate references and relationship types before applying writes. Present counts for insert, update, skip, reject and ambiguous match; a custodian can sample before/after changes.
3. Load parent records before dependent joins or defer unresolved references to a queue. Apply a declared unit atomically, for example one household and its household memberships, or one verified gift and all its designation allocations. A batch may contain both committed units and review items. Record the disposition of every input row.
4. Map stable IDs, source provenance and rights first. Consent requires evidence appropriate to purpose. Unknown consent remains unknown. Do not trigger welcome emails, customer payments or published notices while replaying history. Activate downstream automation only at a specified and signed cutover.
5. Check opening and closing totals per fund and currency, headcount by status and date, attachment counts or digests and orphan relationships. Reconcile skipped rows to source totals. Run a final delta against the agreed cutoff and preserve a read-only source snapshot for the approved duration. Give stewards a discrepancy queue.
6. Restart from the last committed unit after interruption. Repeating a batch with the same changes returns previous operations. Conflicting changes since staging enter review. Undo before external delivery by compensating only rows owned by that batch. Where an external recipient has accepted a financial handoff or a church custodian has approved a change, require a named compensating process and retain the chain.

## Duplicate decisions

Match deterministically on trusted source identifiers first. Similar names, an address, shared phone numbers, ambiguous transliterations and matching birth dates raise a candidate. They never prove a match unaided. Review the field provenance side by side, work from the least sensitive evidence needed, and choose the winner separately for each conflicting value. Include directed kinship, donation attribution, attendance, account links, active access grants, restrictions, effective dates and media consent in the impact preview.

The keeper inherits valid references and the stricter active disclosure restrictions until reviewed. Merge participation links only where identifiers and domain keys agree. Consolidate alternate spellings as approved aliases. Preserve donor evidence, external handoff references and approved-minute references to their original subject through an alias. Two active personal accounts or contradictory safeguarding restrictions require escalation. Unmerging must distinguish pre-merge assignments from subsequent events and queue ambiguous links, with a record of how each was reallocated.

## Acceptance

- The source includes household codes 0014 and 14, two identical names, five people sharing one contact number and no birth dates. The preview preserves both codes and five records, and the operator can decline the duplicate proposals.
- An import of 100 rows commits 84, rejects 10 invalid rows and defers six for missing parents. Counts reconcile to 100. A restart can apply the six after parent creation without duplicating any of the 84.
- A dry run maps two currencies to one currency without conversion. Finance reconciliation blocks the cutover, names the currencies and reports the variance.
- Merging a visitor and their later member profile preserves their original attendance and effective membership date. A previous directory exclusion survives the merge and appears in the review.
- Correcting a mistaken merge restores attributable pre-merge links and flags a post-merge payment for finance review. Reversal records the operator and reason.
