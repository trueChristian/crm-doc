# Reading the logical data model

A named entity represents a set of records with a single owner. It can be implemented as a table, document collection or another equivalent representation. A field described as derived must yield the stated answer even if the implementation caches it. Identifiers are opaque. A person's name, email, household, username, mobile number and giving number can all change or be shared.

## Reading the dictionaries

| Notation | Meaning and test |
| --- | --- |
| id, ref, A → B | A durable identifier or a reference to exactly one B unless marked optional. It must resolve under the correct organization and access rules. |
| optional, nullable, ?, 0..1 | The value can be absent. Unknown, withheld, inapplicable and a known zero are distinct if a decision depends on the difference. |
| 1..n, 0..n, unique together | One or more, zero or more, and a combination that must occur at most once. A many-to-many relationship with dates, type or evidence has its own record. |
| text, rich text, code, enum, boolean | Text preserves the entered script. Render rich content safely for its audience. A code has stable meaning and a separate translated display label. A boolean has two defined states. |
| date, instant, local time, zone, duration | Date-only facts stay on that civil date. An instant is unambiguous in time. Recurrences retain the intended wall clock and named time zone, with an explicit rule for missing or repeated times. |
| interval, effective_from, effective_until | Unless a page specifies otherwise, the start is inclusive, the end exclusive. An absent end is open. For example membership ending on 1 July is absent from the 1 July roll. |
| integer, quantity, decimal, rate | State unit, permitted sign, range, precision and rounding. Preserve the rate and conversion used on an issued document. Never compute money from an approximate binary fraction. |
| money, currency | Exact amount plus a currency code, stored together or bound by a required parent currency. Totals combine like currencies or show a named translation basis. |
| snapshot, version, revision | Preserve exactly what someone approved, paid, signed, received or reported. A correction links to its predecessor. Re-running a historic report has an explicit choice of the original or restated view. |
| file reference, evidence, attachment | Managed object with media type, size, integrity digest, version, audience and retention. Downloads, previews, print and search inherit the record restrictions. |
| structured values, list | Validate against a named definition and its version. If items have different owners, times, permissions or states, use child records with their own identities. |

## Common envelope

The owning scope is explicit or inherited through one required parent. Document either route. Operations crossing church boundaries require a recorded exchange of data; a known identifier alone grants no access. These fields describe the minimum information recoverable for mutable business records, including when parts are provided by a common audit service.

| Field | Logical type and requirement |
| --- | --- |
| id | Stable required identifier, unique in its entity namespace. |
| organization_id | Required Organization reference or deterministic parent path for scoped records. Globally shared code definitions must be explicitly designated. |
| created_at, created_by | Required instant and accountable actor. A scheduled job, import and anonymous submission have identifiable actor kinds. |
| updated_at, updated_by, revision | Last accepted change, actor and monotonically increasing revision or equivalent version token. Reject conflicting writes with a recoverable comparison. |
| effective_from, effective_until | Include on dated relationships and policy versions. A recording date can differ from the date the fact took effect. |
| status | One state from the owning page. State changes carry reason and actor when withdrawing, correcting or making an exception. |
| source_reference | Optional provenance, unique in an agreed namespace for imported or externally originated transactions. It cannot expose private external identifiers in member-facing outputs. |

## Invariants across departments

1. A church role, family tie, user login, ministry assignment, financial authority and publication permission are different facts. Only an explicit grant confers a privileged action.
2. Historic records retain identity through renaming, moves, household splits, closures and account deactivation. Corrections to an identity resolve through a reviewed merge or reversal. Preserve the original identity on signed records.
3. Every retryable submission or background transfer has a scoped operation key and a recorded outcome. Same key and equivalent material inputs returns the first result. Same key with changed material inputs is a conflict.
4. Historical decisions keep the applicable policy version. Retention, holds, anonymization and authorized disclosure apply to copies, derived search entries and exports as well as the primary record.
5. Readers of an approved result can distinguish empty, unavailable, suppressed for privacy, and incomplete data. Membership totals, voting eligibility, a headcount and unique people are separate measures.
6. Money, stock, attendance, delivery, consent and access each have one owning ledger or register. Downstream records link to that source, maintain their own lifecycle and reconcile against it.

**Acceptance.** Two people sharing an email can have separate person records. Repeating an import of a posted receipt leaves one business event. A correction effective last quarter changes a restated roll while the original certified report remains available to its permitted readers. An unauthorized search gives no indication that a restricted record exists.
