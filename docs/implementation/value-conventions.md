# Value conventions and conformance fixtures

A representation-level pass establishes only that a candidate can be interpreted. A record-level decision also requires authority, compatible relationships, the correct lifecycle state and the owning domain’s invariants. The examples are synthetic. Currency examples use a two-decimal fixture. Regulated or locally configurable rules use the church’s approved edition.

An empty field in a partial edit means no supplied replacement. An explicit request to clear a value is a distinct action. Evaluate both against the record’s rules and state. A system-assigned identifier, a projected field, and a conditional completion field are not prompts to collect additional information from a member. Relative fixture identifiers such as Person·A01 name an existing test target in organization A. The separate B01 target belongs to another independent church.

[Department index](README.md)

## alias

Projection of an authoritative field. Rebuild the projection from its authorized source revision.

| Case | Expected interpretation |
| --- | --- |
| value returned by the owner | Rebuild the projection from its authorized source revision. |
| independent write to the projected value | Route the correction to the owning record. |
| Owner revokes or corrects the source | Invalidate the prior projection at the defined effective point. |
| Rebuild after missed update | Use authoritative revision and reconcile lag. |
| User lacks access to the source field | Projection does not reveal the value. |

## bool

Explicit logical choice. Preserve the supplied value; do not promote an unanswered choice to consent.

| Case | Expected interpretation |
| --- | --- |
| true or false | Preserve the supplied value; do not promote an unanswered choice to consent. |
| ambiguous imported text | Map only declared true/false representations. |
| False versus blank | Retain the distinction if absence is allowed. |
| Historic default changes | Issued records keep the value used at decision time. |
| User has no authority to set the flag | Reject the attempted change even when the value is well formed. |

## clock

Local wall-clock time. Preserve local clock time and associate the relevant zone and civil date when scheduling.

| Case | Expected interpretation |
| --- | --- |
| 09:30 | Preserve local clock time and associate the relevant zone and civil date when scheduling. |
| 25:10 | Reject invalid clock hour. |
| Scheduled time in a skipped local hour | Use the recurrence owner’s stated gap rule. |
| Repeated local hour | Resolve the occurrence explicitly before issuing reminders. |
| Midnight crossing | Associate the correct service date and end date. |

## coordinates

Geographic coordinate or location value. Confirm the coordinate convention and permitted disclosure precision.

| Case | Expected interpretation |
| --- | --- |
| coordinate with datum, axis and allowed precision | Confirm the coordinate convention and permitted disclosure precision. |
| outside the declared axis range | Reject or request a verified map correction. |
| Two coordinate axes exchanged | Check expected bounds and locality before publication. |
| Sensitive location is generalized | Publish only the authorized precision. |
| Campus relocates | Preserve historic location evidence on already issued material. |

## currency

Monetary unit code. Resolve the code and its precision as of the transaction.

| Case | Expected interpretation |
| --- | --- |
| an enabled currency code, such as NAD | Resolve the code and its precision as of the transaction. |
| currency symbol shared by multiple currencies | Request the unambiguous currency. |
| Two amounts have different currencies | Report separate totals or translate using recorded rates. |
| Catalog changes after document issue | The stored document keeps its currency. |
| Unrecognized imported code | Hold the row for currency mapping before an amount-dependent approval or exchange. |

## date

Civil calendar date. Keep the date without converting it into a time or shifting it across zones.

| Case | Expected interpretation |
| --- | --- |
| 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | Reject instead of advancing into May. |
| Midnight in a different time zone | A civil date remains the entered date. |
| Date lies on an effective-period boundary | Apply the owning record’s explicit endpoint convention. |

## day

Day of the month. Validate against the known month and year, respecting precision.

| Case | Expected interpretation |
| --- | --- |
| 29 | Validate against the known month and year, respecting precision. |
| 32 | Reject impossible day. |
| 29 February, year unknown | Preserve a possible month/day without claiming a particular year. |
| 31 April | Reject as an impossible date. |
| Month unknown | Preserve declared precision; no invented January. |

## decimal

Exact decimal measure. Retain decimal magnitude, unit and precision required by the record.

| Case | Expected interpretation |
| --- | --- |
| 2.50 in its declared unit | Retain decimal magnitude, unit and precision required by the record. |
| unlabelled mixed units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | Use an effective conversion; preserve earlier observations. |

## digest

Integrity fingerprint or opaque verifier. Bind the algorithm or verifier scheme and object revision to the evidence.

| Case | Expected interpretation |
| --- | --- |
| digest created for the verified content or issued secret | Bind the algorithm or verifier scheme and object revision to the evidence. |
| fingerprint that differs from verified content | Quarantine the mismatch or deny the claim. |
| An identical copy is rechecked | Equality confirms the checked bytes or verifier under the same scheme only. |
| New revision has changed content | Compute new evidence; preserve the prior verified revision. |
| A user knows a digest | Knowledge alone grants no additional access outside the documented token protocol. |

## duration

Elapsed interval or named calendar duration. Preserve unit and distinguish elapsed minutes from a calendar day or working day.

| Case | Expected interpretation |
| --- | --- |
| 30 minutes if elapsed units are configured | Preserve unit and distinguish elapsed minutes from a calendar day or working day. |
| 30 with no resolvable unit | Request an interval unit. |
| A working-day deadline crosses a closure | Use the named work-calendar edition. |
| A civil day crosses an offset change | Do not assume 24 elapsed hours. |
| Zero-length interval | Apply the owner’s validity or immediate-trigger rule. |

## email

Electronic mail address. Preserve the supplied mailbox and its verification status separately.

| Case | Expected interpretation |
| --- | --- |
| a verified contact endpoint supplied by the addressee | Preserve the supplied mailbox and its verification status separately. |
| address with no routable mailbox/domain structure | Mark the endpoint invalid; retain restricted evidence for correction. |
| Shared household mailbox | Permit separate people to share a reachable endpoint; independently evaluate identity and contact purpose. |
| Delivery failure after earlier verification | Record failure by route and purpose; do not remove membership or erase the historic send. |
| Imported address is reachable but consent unknown | Withhold optional communication until eligibility is established. |

## enum

Enumerated stable choice. Preserve the stable code and resolve its localized label separately.

| Case | Expected interpretation |
| --- | --- |
| one declared choice | Preserve the stable code and resolve its localized label separately. |
| choice outside the declared vocabulary | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | Require the underlying code. |
| Display label changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | Retain raw staging evidence; never silently choose the first option. |

## filesize

Nonnegative whole byte count. Compare against the inspected payload, configured size limit and verified content reference.

| Case | Expected interpretation |
| --- | --- |
| 512 measured bytes | Compare against the inspected payload, configured size limit and verified content reference. |
| negative or fractional byte count | Reject impossible measurement. |
| Empty file | Record zero bytes and apply permitted file-type/content rules. |
| Reported length differs from stored bytes | Withhold release and require reinspection. |
| Maximum permitted size | Check equality and the one-byte-over case at intake. |

## instant

Unambiguous point in time. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Case | Expected interpretation |
| --- | --- |
| 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| ambiguous repeated local clock time with no disambiguation | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | Apply the documented validity interval at the decision point. |

## integer

Whole-number measure. Preserve integer precision and enforce the specific field bounds.

| Case | Expected interpretation |
| --- | --- |
| 2 where the field range admits it | Preserve integer precision and enforce the specific field bounds. |
| 2.5 presented as a count | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | Keep absence distinct from an observed zero. |

## key

Opaque identity or token. Compare the opaque value under its issuer rules; preserve leading characters.

| Case | Expected interpretation |
| --- | --- |
| assigned stable key in the owning namespace | Compare the opaque value under its issuer rules; preserve leading characters. |
| display name supplied in place of an identity | Request a verified lookup or an explicit mapping. |
| Renamed display label | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | Use the owning creation outcome and return the established identity. |

## language

Language or locale identifier. Resolve the published language or locale without inferring a person’s nationality.

| Case | Expected interpretation |
| --- | --- |
| an enabled language such as en | Resolve the published language or locale without inferring a person’s nationality. |
| unknown label in an unmapped language list | Keep the source value for review. |
| Specific translation unavailable | Apply the declared fallback and identify which language is being displayed. |
| User changes preferred language | Future communications use the effective preference; issued wording is preserved. |
| Two regional variants exist | Apply the requested locale/version where available. |

## list

Ordered collection or mathematical set. Preserve ordering when meaningful; enforce uniqueness when the declaration is a set.

| Case | Expected interpretation |
| --- | --- |
| two permitted elements in the declared element type | Preserve ordering when meaningful; enforce uniqueness when the declaration is a set. |
| an element of an incompatible type | Reject the affected collection or stage its invalid item under the import policy. |
| Same element appears twice | Apply declared sequence/set multiplicity without doubling financial or voting effects. |
| Empty collection versus unknown collection | Preserve the distinction where the rule requires evidence. |
| One element later becomes restricted | Recompute permitted projection before export or display. |

## money

Exact monetary amount with currency. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Case | Expected interpretation |
| --- | --- |
| 24.50 in a configured two-decimal currency | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| two currencies combined without a rate/basis | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | Use the original component currency and owner’s sign/direction convention. |

## month

Civil month number. Accept month 1 through 12 and keep any unknown year separate.

| Case | Expected interpretation |
| --- | --- |
| 2 | Accept month 1 through 12 and keep any unknown year separate. |
| 13 | Reject out-of-range month. |
| 1 and 12 | Both are possible calendar months. |
| 0 or a fractional month | Reject. |
| Known month, unknown year | Do not manufacture a date of birth. |

## percentage

Percentage with declared scale. Carry the percent unit, denominator and reporting precision.

| Case | Expected interpretation |
| --- | --- |
| 12.5 percent under the stated convention | Carry the percent unit, denominator and reporting precision. |
| joining fractional and percentage scales without conversion | Require unambiguous scale and denominator. |
| 0.125 represented as a fraction | Interpret as 12.5 percent only under the explicit fraction convention. |
| Zero denominator | Represent rate as unavailable, never as an observed zero. |
| Aggregate across groups | Recompute from underlying eligible numerators and denominators when required. |

## protected

Restricted value or protected content reference. Keep value and purpose together; apply field-level authority to projections.

| Case | Expected interpretation |
| --- | --- |
| scoped representation approved for the specific purpose | Keep value and purpose together; apply field-level authority to projections. |
| sensitive value offered for a public listing | Withhold publication unless the specific disclosure rule permits it. |
| Search snippet or autocomplete | Filter before returning any protected content or revealing its existence. |
| Authorized report excludes this field | Omit it from hidden metadata and attachments as well. |
| Approval withdrawn after a preview | Recheck at release; keep only permitted audit evidence. |

## ratio

Exact ratio, rate or weighting. Carry the declared unit, direction and calculation precision.

| Case | Expected interpretation |
| --- | --- |
| 1.125 as an exact decimal where the unit permits | Carry the declared unit, direction and calculation precision. |
| ratio with an undefined denominator | Record an undefined result or reject calculation as the owning rule specifies. |
| 0.125 versus 12.5 percent | Require the unit before comparing or converting. |
| Inverse rate provided | Require explicit direction and an approved conversion. |
| Financial document already issued | Retain the original rate, effective date and rounding basis. |

## relation

Single typed record reference. Resolve stable identity in the permitted scope.

| Case | Expected interpretation |
| --- | --- |
| existing permitted target | Resolve stable identity in the permitted scope. |
| identifier for a different record type | Return a type mismatch without changing the link. |
| Target temporarily absent from an import | Stage a dependency; recheck when the owner maps the source key. |
| Target belongs to a second independent church | Require the explicitly authorized exchange and local mapping. A foreign key alone cannot authorize linking. |
| Authorized target changes its display name | The reference still resolves to its original identity. |

## resource

Scoped or external reference. Resolve against the permitted kind, owning namespace and purpose.

| Case | Expected interpretation |
| --- | --- |
| registered kind plus resolvable key | Resolve against the permitted kind, owning namespace and purpose. |
| unqualified key from a different namespace | Request clarification or quarantine the mapping. |
| Same visible code from two sources | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | Resolve the same destination record once. |

## rule

Versioned structured decision or expression. Check types, dependencies, owner, version and scope before activation.

| Case | Expected interpretation |
| --- | --- |
| validated definition in the permitted rule vocabulary | Check types, dependencies, owner, version and scope before activation. |
| cycle or undefined dependency | Reject activation; retain last accepted edition. |
| Two rules at the same scope conflict | Use documented precedence or block publication for review. |
| Rule changes after a decision | Keep the prior decision bound to its evaluated edition. |
| Preview a rule on an eligible sample | Explain matched conditions; produce no live effect. |

## structured

Typed value or bounded compound record. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Case | Expected interpretation |
| --- | --- |
| a value conforming to the field’s active definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| structure from an incompatible edition | Return a version or shape error. |
| One mandatory child missing | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | Isolate for mapping; do not discard data silently. |
| Historic re-render | Use the original definition and approved vocabulary. |

## telephone

Telephone endpoint or dialling address. Preserve the original and canonical dialling form. Check channel capability separately.

| Case | Expected interpretation |
| --- | --- |
| a normalized endpoint with a known country context | Preserve the original and canonical dialling form. Check channel capability separately. |
| local number with unresolved country/area context | Request the missing context before treating it as routable. |
| Several people share a number | Keep independent person and household records. |
| Reassigned or permanently failed number | Suppress affected sends and verify a new route. |
| SMS versus voice preference | A call permission is not sufficient to establish a separate messaging purpose. |

## text

Human-readable text. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Case | Expected interpretation |
| --- | --- |
| valid text in the source language | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| text supplied with an invalid encoding or disallowed control characters | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Preserve and display their original spelling. |
| Label changes after formal issue | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | Render in the field’s declared context and respect accessibility and disclosure rules. |

## version

Revision number or opaque revision token. Compare under the declared revision scheme. Require the expected version for conflicting work.

| Case | Expected interpretation |
| --- | --- |
| the current revision returned by the owner | Compare under the declared revision scheme. Require the expected version for conflicting work. |
| superseded version presented for a new approval | Reject or reopen review against the current contents. |
| Two operators begin at revision seven | Commit the first change once and re-evaluate the second; never overwrite an unreviewed difference. |
| Re-read an already approved revision | Return the frozen value and evidence for that edition. |
| Replay of an earlier result | Correlate by the business operation identity; a newer version does not create a second effect. |

## vocab

Versioned classification or status code. Check the relevant vocabulary and permitted transition before applying.

| Case | Expected interpretation |
| --- | --- |
| enabled code for this record and effective date | Check the relevant vocabulary and permitted transition before applying. |
| unmapped category | Request mapping to an authorized code. |
| Code retired before a new transaction | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | Run ordinary transition guards and approval checks. |

## year

Civil year. Preserve year precision separately from month/day.

| Case | Expected interpretation |
| --- | --- |
| 2024 | Preserve year precision separately from month/day. |
| 2024.5 | Reject a fractional calendar year. |
| Date reported only as a year | Do not store 1 January as the actual day. |
| Date used to determine age eligibility | Return a range or request verification if the answer depends on the day. |
| Cross-year comparison | Compare known intervals and disclose uncertainty. |

## zone

Time zone with civil-time rules. Preserve zone identity; use the applicable local rules for the date.

| Case | Expected interpretation |
| --- | --- |
| Africa/Windhoek | Preserve zone identity; use the applicable local rules for the date. |
| unqualified ambiguous abbreviation | Require a named zone or explicitly supported fixed offset. |
| Future recurring appointment | Recompute local-time occurrences using its stored zone and change policy. |
| Staff view from a second zone | Show the requested local display without moving the actual instant. |
| Zone changes for a campus | Re-evaluate future occurrences and retain historical issue evidence. |


## interval

Record the effective start and end together with the field's civil-date or instant basis. Use the [shared interval convention](../foundation/record-conventions.md). State whether a missing endpoint means open-ended or unknown. For an appointment valid from 1 June until 1 July, a 30 June duty is within the interval and a 1 July duty needs a new authority. Reject inverted intervals. A missing closing date on an application cannot by itself establish an active appointment.

## operation

Scope a retry key to the originating connection or actor, church and business action. Store the material input fingerprint and the original disposition. The same key and equivalent inputs returns the same record and status. Changed material inputs conflict. An interrupted submission whose receiver may have acted needs a lookup or reconciliation before a new external instruction. See [command outcomes](../handbook/business-commands.md).

## references

Where a field accepts a set of typed references, apply the [single-target relation rules](#relation) to every member and enforce the field's minimum, maximum and uniqueness rules. Reject an unauthorized or wrong-type member before applying the set. Two mentions of the same finding cannot count as two findings. An empty set, missing evidence and a set withheld from a particular reader have distinct reporting meanings.
