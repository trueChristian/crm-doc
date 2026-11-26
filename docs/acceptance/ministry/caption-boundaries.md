# Evaluate caption timing at every edit boundary

This fixture checks the 60-second recording in [the archive handover](archive-handover.md). It supplies expected values for every ordered, nonempty pair of the 16 boundary probes. An implementation can run all 120 intervals with synthetic cue text. The values are milliseconds. Treat each interval as inclusive at its start and exclusive at its end.

The source retains [0,12000), [18000,30000) and [40000,60000). Insert no silence between kept portions. Output starts for those portions are 0, 12000 and 24000 respectively. For each nonempty intersection with a kept portion, add its offsets from that portion’s start to the corresponding output start. Preserve the separate source-fragment identities even when fragments touch on the output timeline.

| Review class | What the editor must be able to determine |
| --- | --- |
| Keep timing | The whole cue survived in one unchanged source interval. Normal editorial review and audience restrictions still apply. |
| Review trim | Only one fragment survived but some original cue duration was removed. Listen to the surviving audio and approve wording and attribution. |
| Review split | Two or three noncontiguous source fragments survived. Preserve each fragment separately for editorial review. Identical text copied onto both can disclose the cut. |
| Omit | The cue has zero surviving duration. Exclude its time, wording and speaker metadata from the edited public rendition. |

| Source start | Source end | Output fragments | Retained milliseconds | Review class |
| ---: | ---: | --- | ---: | --- |
| 0 | 1 | [0,1) | 1 | Keep timing |
| 0 | 11999 | [0,11999) | 11999 | Keep timing |
| 0 | 12000 | [0,12000) | 12000 | Keep timing |
| 0 | 12001 | [0,12000) | 12000 | Review trim |
| 0 | 17999 | [0,12000) | 12000 | Review trim |
| 0 | 18000 | [0,12000) | 12000 | Review trim |
| 0 | 18001 | [0,12000), [12000,12001) | 12001 | Review split |
| 0 | 29999 | [0,12000), [12000,23999) | 23999 | Review split |
| 0 | 30000 | [0,12000), [12000,24000) | 24000 | Review split |
| 0 | 30001 | [0,12000), [12000,24000) | 24000 | Review split |
| 0 | 39999 | [0,12000), [12000,24000) | 24000 | Review split |
| 0 | 40000 | [0,12000), [12000,24000) | 24000 | Review split |
| 0 | 40001 | [0,12000), [12000,24000), [24000,24001) | 24001 | Review split |
| 0 | 59999 | [0,12000), [12000,24000), [24000,43999) | 43999 | Review split |
| 0 | 60000 | [0,12000), [12000,24000), [24000,44000) | 44000 | Review split |
| 1 | 11999 | [1,11999) | 11998 | Keep timing |
| 1 | 12000 | [1,12000) | 11999 | Keep timing |
| 1 | 12001 | [1,12000) | 11999 | Review trim |
| 1 | 17999 | [1,12000) | 11999 | Review trim |
| 1 | 18000 | [1,12000) | 11999 | Review trim |
| 1 | 18001 | [1,12000), [12000,12001) | 12000 | Review split |
| 1 | 29999 | [1,12000), [12000,23999) | 23998 | Review split |
| 1 | 30000 | [1,12000), [12000,24000) | 23999 | Review split |
| 1 | 30001 | [1,12000), [12000,24000) | 23999 | Review split |
| 1 | 39999 | [1,12000), [12000,24000) | 23999 | Review split |
| 1 | 40000 | [1,12000), [12000,24000) | 23999 | Review split |
| 1 | 40001 | [1,12000), [12000,24000), [24000,24001) | 24000 | Review split |
| 1 | 59999 | [1,12000), [12000,24000), [24000,43999) | 43998 | Review split |
| 1 | 60000 | [1,12000), [12000,24000), [24000,44000) | 43999 | Review split |
| 11999 | 12000 | [11999,12000) | 1 | Keep timing |
| 11999 | 12001 | [11999,12000) | 1 | Review trim |
| 11999 | 17999 | [11999,12000) | 1 | Review trim |
| 11999 | 18000 | [11999,12000) | 1 | Review trim |
| 11999 | 18001 | [11999,12000), [12000,12001) | 2 | Review split |
| 11999 | 29999 | [11999,12000), [12000,23999) | 12000 | Review split |
| 11999 | 30000 | [11999,12000), [12000,24000) | 12001 | Review split |
| 11999 | 30001 | [11999,12000), [12000,24000) | 12001 | Review split |
| 11999 | 39999 | [11999,12000), [12000,24000) | 12001 | Review split |
| 11999 | 40000 | [11999,12000), [12000,24000) | 12001 | Review split |
| 11999 | 40001 | [11999,12000), [12000,24000), [24000,24001) | 12002 | Review split |
| 11999 | 59999 | [11999,12000), [12000,24000), [24000,43999) | 32000 | Review split |
| 11999 | 60000 | [11999,12000), [12000,24000), [24000,44000) | 32001 | Review split |
| 12000 | 12001 | None | 0 | Omit |
| 12000 | 17999 | None | 0 | Omit |
| 12000 | 18000 | None | 0 | Omit |
| 12000 | 18001 | [12000,12001) | 1 | Review trim |
| 12000 | 29999 | [12000,23999) | 11999 | Review trim |
| 12000 | 30000 | [12000,24000) | 12000 | Review trim |
| 12000 | 30001 | [12000,24000) | 12000 | Review trim |
| 12000 | 39999 | [12000,24000) | 12000 | Review trim |
| 12000 | 40000 | [12000,24000) | 12000 | Review trim |
| 12000 | 40001 | [12000,24000), [24000,24001) | 12001 | Review split |
| 12000 | 59999 | [12000,24000), [24000,43999) | 31999 | Review split |
| 12000 | 60000 | [12000,24000), [24000,44000) | 32000 | Review split |
| 12001 | 17999 | None | 0 | Omit |
| 12001 | 18000 | None | 0 | Omit |
| 12001 | 18001 | [12000,12001) | 1 | Review trim |
| 12001 | 29999 | [12000,23999) | 11999 | Review trim |
| 12001 | 30000 | [12000,24000) | 12000 | Review trim |
| 12001 | 30001 | [12000,24000) | 12000 | Review trim |
| 12001 | 39999 | [12000,24000) | 12000 | Review trim |
| 12001 | 40000 | [12000,24000) | 12000 | Review trim |
| 12001 | 40001 | [12000,24000), [24000,24001) | 12001 | Review split |
| 12001 | 59999 | [12000,24000), [24000,43999) | 31999 | Review split |
| 12001 | 60000 | [12000,24000), [24000,44000) | 32000 | Review split |
| 17999 | 18000 | None | 0 | Omit |
| 17999 | 18001 | [12000,12001) | 1 | Review trim |
| 17999 | 29999 | [12000,23999) | 11999 | Review trim |
| 17999 | 30000 | [12000,24000) | 12000 | Review trim |
| 17999 | 30001 | [12000,24000) | 12000 | Review trim |
| 17999 | 39999 | [12000,24000) | 12000 | Review trim |
| 17999 | 40000 | [12000,24000) | 12000 | Review trim |
| 17999 | 40001 | [12000,24000), [24000,24001) | 12001 | Review split |
| 17999 | 59999 | [12000,24000), [24000,43999) | 31999 | Review split |
| 17999 | 60000 | [12000,24000), [24000,44000) | 32000 | Review split |
| 18000 | 18001 | [12000,12001) | 1 | Keep timing |
| 18000 | 29999 | [12000,23999) | 11999 | Keep timing |
| 18000 | 30000 | [12000,24000) | 12000 | Keep timing |
| 18000 | 30001 | [12000,24000) | 12000 | Review trim |
| 18000 | 39999 | [12000,24000) | 12000 | Review trim |
| 18000 | 40000 | [12000,24000) | 12000 | Review trim |
| 18000 | 40001 | [12000,24000), [24000,24001) | 12001 | Review split |
| 18000 | 59999 | [12000,24000), [24000,43999) | 31999 | Review split |
| 18000 | 60000 | [12000,24000), [24000,44000) | 32000 | Review split |
| 18001 | 29999 | [12001,23999) | 11998 | Keep timing |
| 18001 | 30000 | [12001,24000) | 11999 | Keep timing |
| 18001 | 30001 | [12001,24000) | 11999 | Review trim |
| 18001 | 39999 | [12001,24000) | 11999 | Review trim |
| 18001 | 40000 | [12001,24000) | 11999 | Review trim |
| 18001 | 40001 | [12001,24000), [24000,24001) | 12000 | Review split |
| 18001 | 59999 | [12001,24000), [24000,43999) | 31998 | Review split |
| 18001 | 60000 | [12001,24000), [24000,44000) | 31999 | Review split |
| 29999 | 30000 | [23999,24000) | 1 | Keep timing |
| 29999 | 30001 | [23999,24000) | 1 | Review trim |
| 29999 | 39999 | [23999,24000) | 1 | Review trim |
| 29999 | 40000 | [23999,24000) | 1 | Review trim |
| 29999 | 40001 | [23999,24000), [24000,24001) | 2 | Review split |
| 29999 | 59999 | [23999,24000), [24000,43999) | 20000 | Review split |
| 29999 | 60000 | [23999,24000), [24000,44000) | 20001 | Review split |
| 30000 | 30001 | None | 0 | Omit |
| 30000 | 39999 | None | 0 | Omit |
| 30000 | 40000 | None | 0 | Omit |
| 30000 | 40001 | [24000,24001) | 1 | Review trim |
| 30000 | 59999 | [24000,43999) | 19999 | Review trim |
| 30000 | 60000 | [24000,44000) | 20000 | Review trim |
| 30001 | 39999 | None | 0 | Omit |
| 30001 | 40000 | None | 0 | Omit |
| 30001 | 40001 | [24000,24001) | 1 | Review trim |
| 30001 | 59999 | [24000,43999) | 19999 | Review trim |
| 30001 | 60000 | [24000,44000) | 20000 | Review trim |
| 39999 | 40000 | None | 0 | Omit |
| 39999 | 40001 | [24000,24001) | 1 | Review trim |
| 39999 | 59999 | [24000,43999) | 19999 | Review trim |
| 39999 | 60000 | [24000,44000) | 20000 | Review trim |
| 40000 | 40001 | [24000,24001) | 1 | Keep timing |
| 40000 | 59999 | [24000,43999) | 19999 | Keep timing |
| 40000 | 60000 | [24000,44000) | 20000 | Keep timing |
| 40001 | 59999 | [24001,43999) | 19998 | Keep timing |
| 40001 | 60000 | [24001,44000) | 19999 | Keep timing |
| 59999 | 60000 | [43999,44000) | 1 | Keep timing |

## Reconcile the fixture

The 120 source intervals produce 18 wholly retained cues, 45 single-fragment trims, 45 split cues, 12 omitted cues. Independently count retained milliseconds between each pair of source endpoints and verify the sum of all output-fragment lengths. A removed interval has zero length after mapping and contributes no caption row. Adjacent fragments from distinct source portions keep their separate provenance.

Reject a negative start, a start equal to or above the end, and an end beyond 60000 on this source. On the edited edition reject any cue extending above 44000. These bounds handle representational validity. An apparently valid cue can still require privacy, language or accessibility review before release.

[Transcript fields](../../implementation/commerce/TranscriptSegment.md) · [Editorial review fields](../../implementation/commerce/EditorialReview.md)
