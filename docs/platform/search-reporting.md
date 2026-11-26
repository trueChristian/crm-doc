# Finding records and reporting

A secretary searches for a member remembered by an earlier surname, a minister checks outstanding follow-ups, a treasurer compares restricted fund balances and a member finds last month's approved minutes. Every result must explain what it represents and which date or period it covers. Each department owns business definitions and exclusions for its measures; this chapter owns their reuse and publication.

## Logical records

| Entity | Fields | Relationship and constraint |
|---|---|---|
| SearchProjection | source_ref ResourceRef, source_revision integer, locale tag, searchable_fields set(code), visible_scopes set(ResourceRef), classification code, indexed_at instant, stale_after instant? | Derived representation per record/locale. Private aliases and highlights have field permissions. Exclude restricted bodies from broad indexing. |
| SavedView | owner_id Ref(UserAccount), resource_type code, title text, filter_tree structured rule, sort_keys list(code), column_keys list(code), visibility code, shared_scope_ref ResourceRef?, revision integer | A shared definition confers no access to the result. Validate requested fields for each viewer. |
| MetricDefinition | metric_key code, title text, owner_id Ref(UserAccount), revision integer, grain code, numerator_rule structured rule, denominator_rule structured rule?, date_basis code, dimensions set(code), suppression_rule structured rule, effective_at date | Document counting unit, inclusion, deduplication, timezone, null and correction behavior. An effective revision is immutable. |
| ReportDefinition | report_key code, title text, owner_id Ref(UserAccount), metric_refs set(Ref(MetricDefinition)), parameter_schema structured rule, allowed_views set(code), revision integer, classification code | Each published edition retains metric editions. Include labels, totals and drill-through permissions. |
| ReportRun | definition_id Ref(ReportDefinition), requested_by Ref(UserAccount), as_of instant, period_start date?, period_end date?, scope_ref ResourceRef, parameters structured values, data_watermark instant, state code, output_ref ResourceRef?, generated_at instant? | Reproducibility requires definition edition, population rules, source cutoff and adjustments edition. |
| Dashboard | title text, owner_id Ref(UserAccount), audience_scope ResourceRef, refresh_interval duration, layout list(ordered widget), default_period code | Each widget points to a published report or saved view. Widgets inherit the viewer's access at run time. |
| ReportSchedule | definition_id Ref(ReportDefinition), scope_ref ResourceRef, recipient_rule structured rule, frequency_rule structured recurrence, zone zone, expires_at instant?, owner_id Ref(UserAccount), active boolean | Verify current recipients and authority at execution. Prefer a new permission-checked report link for sensitive output. |
| MetricSnapshot | metric_id Ref(MetricDefinition), scope_ref ResourceRef, period_start date, period_end date, revision integer, value exact number?, unit code, population_count integer?, suppression_state code, source_run_id Ref(ReportRun) | A restatement points to its prior revision; distinguish provisional and formally issued figures. |

## Search behavior

Search permitted names, aliases, words, codes and configured filters. Support spelling variations and local scripts without rewriting the authoritative name. Exact identifiers take priority and every result includes record kind and enough nonsensitive context to distinguish namesakes. Authorized operators can filter active, historic, transferred and archived records. Suggestions, recent items, result counts, summaries, facets, keyboard navigation and downloads observe the same scope. Revoked content is removed from all live views immediately by checking the source authority even while an index rebuilds.

Return “no matching accessible records” consistently for missing and protected targets. Never fill surname or transliteration from another person's fields. Preserve original-script names and sort choices. A member may disable personal recent searches; do not retain private case queries in suggestions or operational logs. Link resolvers evaluate attachment access at open time.

## Report vocabulary and custody

| Measure | Population and time rule | Required companion information |
|---|---|---|
| Members as of a date | Distinct people whose qualifying membership spell covers the date in the selected congregation. Report home congregation and affiliate memberships separately. | Count status rules, explicit cutoff, handling of transfers, unknown dates and cross-campus duplicates. |
| Guests returning | Distinct qualifying first-time guests in a cohort with a later eligible attendance within a defined window. | Cohort dates, follow-up window, denominator and exclusions for anonymous headcounts. |
| Attendance | Named unique people per occurrence and anonymous headcount reported separately with the counter's declared counting method. | Whether headcount includes named attendees, no combined total if overlap is unknown, cancelled occurrences excluded. |
| Volunteer coverage | Filled eligible required slots divided by required slots on active rosters. | State whether invited or confirmed assignments qualify; identify overlapping slots and unmet requirements. |
| Giving and budget | Financial definition approved by the treasurer, tied to posting status, report basis, currency, restriction and fiscal period. | Distinguish cash gifts, pledges and revenue; fund balance equals opening balance plus movement under the accounting policy. |
| Meeting actions | Open or overdue actions assigned from approved decisions as of the report cutoff. | Distinguish pending minutes, waived tasks and revised due dates. |

Support period comparisons using equivalent date windows, and show the effect of partial periods, late entries and corrected facts. A missing value is distinct from zero. Totals use authoritative underlying facts and appropriate precision, particularly for money and ratios. Cross-campus totals deduplicate people if the definition counts people. Require explicit treatment of campus transfers. Record a note against an issued report explaining a material restatement.

Small groups can expose identities through charts, totals, leaderboards or subtraction. Suppress small cells under the organization's disclosure policy and apply complementary suppression where needed. Restrict exports and repeated queries that could defeat suppression. The report owner can see suppressed values only under separately granted permission. Provide an accessible data table and an understandable narrative alongside charts. Personnel, pastoral risk and spirituality rankings are excluded from general dashboards.

## Acceptance

- A person associated with two campuses counts once in an organization-wide person metric and appears according to the documented campus attribution rule. The total explains any difference from the sum of campus rows.
- An anonymous service count of 78 includes 30 named check-ins. Display 78 overall and 30 identified; prevent an overall value of 108.
- A hidden case is absent from autocomplete, counts, report totals, scheduled delivery, search previews and drill-through even while the search projection is rebuilding.
- A board member leaves the council before a report schedule runs. They receive no protected data. Live links from older messages recheck permission.
- Re-running a historical report with unchanged source facts and editions reproduces its totals. A backdated correction yields a labeled restatement with the earlier report retained.
