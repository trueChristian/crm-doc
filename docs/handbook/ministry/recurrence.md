# Expand a calendar and change an issued occurrence

A secretary must be able to answer both “Which service takes place next Sunday?” and “Which notice did the family receive before we moved it?” Keep the recurrence instruction, dated occurrence, publication revision and delivery record separately. Use the [calendar dictionary](../../ministry/calendar.md) for their identities.

## Input contract

Take the series identity and revision, named zone, first local date, clock time or all-day designation, duration rule, interval, applicable weekdays or month dates, week start, optional ordinal, end rule, included and excluded slots and the requested viewing window. Validate before expansion. Reject an interval of zero, negative duration, incompatible end rules and an invalid month number. A first occurrence that conflicts with the pattern requires an explicit organizer correction. A yearly calendar may add an extraordinary date independently. Preview exactly which local dates the organizer is approving.

All-day dates have no clock offset. For timed events, distinguish a fixed elapsed duration from an occurrence that promises to end at a stated local clock time. If a retreat promises a local finish that spans an offset change, derive both endpoint instants using the recorded zone rules. A reader in another zone may view both their local time and the host time. An imported time with no known location is a floating local time until its owner assigns the intended zone; block timed reminders and resource commitments that require an instant.

## Expansion procedure

1. Generate candidate local slots from the original anchor inside the bounded planning horizon, starting early enough to include items that overlap the display window. For an interval of two weeks, count weeks from the week containing the anchor according to the chosen week start. A view opened in a different week cannot change which weeks qualify.
2. For a monthly ordinal, list eligible weekdays inside that month in calendar order and select the ordinal from the beginning or the end. A fifth weekday in a month that has only four yields no match. For a requested day 31, explicitly choose skip or last available day under church policy. For a skipped invalid date, the default counting policy in this fixture does not consume an occurrence.
3. For each generated local slot, apply the configured gap and repeated-hour policy. A nonexistent time may be skipped, referred for review, or moved by the published adjustment. A repeated hour needs the earlier or later offset. Store the original local key, chosen offset and resolved instant so the same slot can be found after a change.
4. Apply the series limit to the generated sequence before adding explicit dates. Combine included dates with generated slots and collapse identical original keys. Apply exclusions last. A deleted recurring date receives an exclusion marker; otherwise an expansion will resurrect it. An independently added date does not extend the count-limited sequence.
5. Upsert by series and original slot. Preserve the occurrence identifier and original key through a reschedule. Apply approved per-date time, venue, capacity and cancellation overrides. Select results by overlap with the requested window using the effective dates. Also retrieve moved exceptions that originated outside the requested window. A moved date and an ordinary date now landing in the same room still have distinct identities and require collision review.
6. A second expansion with the same inputs and horizon returns the same rows and identifiers. A later civil offset-rule revision recalculates affected future instants and creates a review for published events that changed. Historical issued instants remain as recorded.

## Exercise A. Count, exclusion and move

Choose Wednesday 6 January 2027 at 18:00 as the first slot. Repeat weekly for four generated dates, exclude 20 January and explicitly add 29 January. Move the 13 January meeting to 14 January at 19:00.

| Original slot | Effective slot | Expected handling |
| --- | --- | --- |
| 6 Jan, 18:00 | 6 Jan, 18:00 | Ordinary occurrence. |
| 13 Jan, 18:00 | 14 Jan, 19:00 | Same identity as the issued 13 January meeting. Preserve its registrations. |
| 20 Jan, 18:00 | No public meeting | Retain the excluded slot for reconciliation. |
| 27 Jan, 18:00 | 27 Jan, 18:00 | Fourth generated occurrence. |
| 29 Jan, 18:00 | 29 Jan, 18:00 | Extra occurrence. Repeated addition of this key creates no duplicate. |

The working list has four visible meetings. A day view for 14 January includes the moved meeting even when its request starts after the original date. Removing the 29 January addition leaves three visible meetings. Starting another four-week set on 13 January would incorrectly issue 3 February.

## Exercise B. Local-time discontinuity

Use a test zone whose clock jumps from 01:59 to 03:00 on 28 March and repeats the hour 02:00–02:59 on 31 October. At an offset of +01:00 before the jump and +02:00 afterward, the spring service at 02:30 does not exist. Under the “advance by size of gap” policy its published time is 03:30, equivalent to 01:30 universal time. For 31 October, 02:30 with +02:00 is 00:30 universal time; 02:30 with +01:00 is 01:30 universal time. The selected fold creates one occurrence. A Friday-to-Sunday all-day retreat stores Friday and the following Monday as its exclusive boundary. Traveling to another zone does not turn it into a Thursday event.

## Scope of change and recovery

On “this date,” create an override and show affected duties, seats, bookings and notification revisions. On “this and later,” create a successor rule from the chosen original slot. Match explicitly retained future occurrences by stable identity. List unmatched already-booked dates separately for review before cancellation or reassignment. For “whole series,” preview both the future impact and any proposed correction to the historic display. A recorded attendance or issued notice is immutable evidence of what actually happened.

Publish the revised plan only after resolving mandatory room and availability conflicts. Queue a change notice per eligible recipient and publication revision. An obsolete reminder scheduled before the move is suppressed. If delivery fails, retry the same notice identity while preserving the revised service date. A moderator can withdraw a private joining instruction from the current view immediately; history of who received a prior notice remains restricted.

**Operator reconciliation.** Compare visible dates, original-slot identifiers, excludes, moves, seats still held, prior and current notice revisions, resolved instants and unacknowledged changes. A recurring listing that renders correctly but loses a family's registration after moving one date fails this exercise.

[Manual index](README.md) · [Calendar records](../../ministry/calendar.md)
