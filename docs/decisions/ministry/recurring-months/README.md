# Which occurrences survive an exception or move?

M1, M2 and M3 are three generated candidate months from the displayed anchor month and interval. Numeric slot identities 1, 2, 3 persist across a move. E is an exceptional additional date. A fifth weekday can be absent.

Read 1 as first, 2 as second, 4 as fourth, 5 as fifth and −1 (shown as -1) as last matching weekday. A skip never invents an occurrence. An explicit addition matching an existing original key is deduplicated. A move onto another established date keeps both identities and opens a conflict review; it never merges attendees.

Original slots are checked twice: first using weekday arithmetic and then by listing all the dates in each month. The effective schedule is rebuilt by identity, so deleting a date cannot silently reappear on expansion. Times and zone are identical within these fixtures. Use the calendar manual for clock discontinuities.

[Ministry decisions](../README.md) · [Implementation manual](../../../handbook/ministry/recurrence.md)

| Open cases | Decision outcomes in this group | Cases |
| --- | --- | ---: |
| [Set 1](01.md) | collision review; retain both | 260 |
| [Set 2](02.md) | collision review; retain both | 260 |
| [Set 3](03.md) | collision review; retain both | 260 |
| [Set 4](04.md) | collision review; retain both | 260 |
| [Set 5](05.md) | collision review; retain both · keep exclusion and rebuild | 260 |
| [Set 6](06.md) | keep exclusion and rebuild | 260 |
| [Set 7](07.md) | keep exclusion and rebuild | 260 |
| [Set 8](08.md) | keep exclusion and rebuild | 260 |
| [Set 9](09.md) | keep exclusion and rebuild | 260 |
| [Set 10](10.md) | keep exclusion and rebuild · missing ordinal skipped | 260 |
| [Set 11](11.md) | missing ordinal skipped | 260 |
| [Set 12](12.md) | missing ordinal skipped | 260 |
| [Set 13](13.md) | missing ordinal skipped | 260 |
| [Set 14](14.md) | missing ordinal skipped · retain moved identity | 260 |
| [Set 15](15.md) | retain moved identity | 260 |
| [Set 16](16.md) | retain moved identity | 260 |
| [Set 17](17.md) | retain moved identity | 260 |
| [Set 18](18.md) | retain moved identity | 260 |
| [Set 19](19.md) | retain moved identity | 120 |
