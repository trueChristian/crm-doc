# Quiet windows, elapsed reminders and discontinuous local clocks

[All decision profiles](../README.md) · [Clerk procedure](../../../handbook/governance/emergency-and-reminders.md)

These cases model a minute-resolution scheduler. The member's local quiet window repeats each local day. A wall-clock hour can be skipped or repeated while elapsed reminder offsets remain absolute.

## Reproduce the cases

1. Compute planned instant as service instant minus lead minutes. Deadline is service instant minus minimum useful lead. A planned instant after the deadline expires immediately.
2. Convert each candidate instant to local time under its effective offset. A crossing-midnight window is quiet if local minutes are at or after its start OR before its end; a same-day window uses AND.
3. Inspect the actual minute sequence from planned through deadline inclusively. Select the earliest permitted instant or expire. This avoids manufacturing nonexistent local instants and handles a repeated local hour under its actual UTC offset.

## Profile pages

| Profile | Cases | Case ranges |
| --- | ---: | --- |
| Overnight quiet period in fixed UTC+02 | 875 | [1–325](overnight-01.md), [326–650](overnight-02.md), [651–875](overnight-03.md) |
| Daytime quiet window for shift workers | 875 | [1–325](nightshift-01.md), [326–650](nightshift-02.md), [651–875](nightshift-03.md) |
| Forward clock change in variable-offset zone | 875 | [1–325](spring-01.md), [326–650](spring-02.md), [651–875](spring-03.md) |
| Repeated hour in variable-offset zone | 875 | [1–325](autumn-01.md), [326–650](autumn-02.md), [651–875](autumn-03.md) |
