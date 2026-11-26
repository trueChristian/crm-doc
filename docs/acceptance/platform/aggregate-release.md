# Release a volunteer report whose totals can disclose a suppressed campus

A network coordinator publishes counts of distinct volunteers who completed an approved training unit. Two separately appointed custodians can inspect authorized local source records. The public reporting role can read only approved aggregate views. Build the following synthetic counts from qualifying people, each assigned to exactly one campus at the cutoff. No person overlaps campuses in this fixture.

| Campus | People at cutoff 1 | Late corrections for the same period | Corrected people at cutoff 2 |
| --- | ---: | ---: | ---: |
| North | 12 | 0 | 12 |
| Central | 5 | 0 | 5 |
| South | 1 | +1 | 2 |
| East | 0 | 0 | 0 |
| Total | 18 | +1 | 19 |

The local public-release profile suppresses counts 1–4. Zero is publishable only when it cannot resolve a protected count. It permits the campus breakdown or organization total in the stated approved releases, disallows person-level drill-through, and treats combinations of earlier and later publications as available to the reader. Document the period, watermark, distinct counting grain and late-correction basis for both runs.

## Test the first release

| Request or output | Expected result and check |
| --- | --- |
| Unprotected operator reconciliation | An authorized custodian with rights over all four counts sees 12, 5, 1 and 0, which reconcile to 18. A local-only custodian cannot inspect the other campuses. |
| Candidate public output: all cells apart from South, plus total | Reject. Anyone can compute 18 − 12 − 5 − 0 = 1. Hiding the chart label alone does not change the result. |
| Approved first publication for this exercise | Show North = 12, East = 0 and total = 18. Withhold both Central and South. Use an identical display for the two withheld cells. The user can infer only their sum, 6, from these three numbers. |
| Rebuild with charts and accessible alternatives | Text summary, accessible data table, downloaded values, annotations, tooltips and chart axes display the same release. No full row data, hidden series, drill-down or machine-readable exact count is attached. |
| Search or assistant asks “how many in South?” under this public role | Use the published presentation and omit the restricted values. No inferred count, person names, source titles or direct link to a restricted extract. |
| Public reader requests Central alone, or all campuses except South | Withhold a new exact result which would identify South when combined with the public release. A fresh session, language, report export or shared saved view does not change this rule. |
| Scheduled report goes to a former custodian | At execution, re-evaluate the recipient and report authority. No restricted attachment or working private result link is sent to this recipient. |

The fixture's masking rule chooses Central as the complementary cell and uses the same “withheld” state for both cells. It does not expose which is primary or classify one cell as definitely above the threshold. A different release policy may publish a coarser organization-only report, but must provide the same disclosure test across every supported view.

## Restate without identifying the late addition

The first issue remains publicly available. A proposed footnote names South as the sole campus corrected; a proposed updated issue also publishes total 19. Together with the earlier issue these disclose that exactly one South volunteer was added. This fixture's profile protects small changes in a named campus as well as small totals.

1. Preserve both internal snapshots with their data watermarks and definition edition, and the reason in restricted custody. The first issue must still reproduce from its original source cutoff. Rerunning after the correction does not rewrite what was published.
2. For the revised public release, keep the two complementary cells suppressed, omit the identifying footnote, and publish the approved aggregate wording “period figures were restated following reconciliation.” The approved publication in this test gives North 12, East 0 and organization total 19. The change is known to be in the combined withheld pair, without locating it to a campus from either public view.
3. Attempt a second report that documents that Central was unchanged. Reject that disclosure because the two reports would assign the difference to South. Apply the test to companion reports, explanatory text and previously published releases in the fixture's disclosure inventory.
4. Revoke a custodian's detail permission while their saved results are open. Following a row link, exporting the old output or loading the private cache requires current authority. The signed public report remains available in its authorized presentation.
5. Compare the member with staff and public routes before sign-off. Reconcile distinct people = 19, public campus numerics = 2, withheld campus entries = 2, public totals = 1. A zero from East cannot replace a withheld value. Changing the language changes labels only.

For an independent negative test, add a person with two qualifying attendance events under the same campus and period. The event count grows by two; the count of distinct qualifying people grows by one if this person was previously absent, and zero if already included. A canceled event contributes zero qualifying completions under this fixture's definition.

Use [MetricDefinition](../../implementation/platform/MetricDefinition.md), [MetricSnapshot](../../implementation/platform/MetricSnapshot.md), [ReportDefinition](../../implementation/platform/ReportDefinition.md), [ReportRun](../../implementation/platform/ReportRun.md), [ReportSchedule](../../implementation/platform/ReportSchedule.md) and [SavedView](../../implementation/platform/SavedView.md).
