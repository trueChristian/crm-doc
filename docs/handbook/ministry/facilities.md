# Reserve rooms and equipment that really exist

A building booking promises space in a specific layout over a time interval. Equipment promises a serial-numbered unit or quantity at a location. A single request can require all of them. The facilities steward decides whether a partial fulfilment is acceptable before making independent commitments. The [facilities dictionary](../../ministry/resources.md) defines the records involved.

## Expand space and time requirements

Represent exclusive use at the smallest independently allocatable space. A whole hall consisting of East and West consumes both leaves. A meeting in East consumes East only. Shared routes or sound restrictions can impose additional explicit exclusions. Avoid transitive overblocking: if East conflicts with the whole hall and West conflicts with the whole hall, East and West can still be used together unless their own layouts are incompatible.

For a booking from S to E, reserve from S less setup to E plus reset. Use a half-open interval. Two occupied intervals conflict when each begins before the other's end. Check facility closures, operational holds, externally hired slots and active approved commitments using the same expanded footprint. Do not count a reservation upgraded from hold to confirmed twice. A capacity decision considers the selected layout's usable capacity, accessible circulation, steward's approved limit and current closure restrictions.

For pooled equipment, the expected quantity can change inside the requested interval. At each boundary apply all returns or hold expiries effective at that instant before demands beginning then, unless inspection or transport still blocks reissue. For each resulting nonempty segment, compute owned and usable stock less overlapping claims, unreturned loans outside those claims, maintenance quarantine and already promised transfers. A partially issued reservation still counts once across reserved and custody states. Guaranteed quantity for the interval is the lowest free quantity across the segments.

## Worked partition and equipment conflict

| Resource | Existing commitment | Effective result |
| --- | --- | --- |
| East partition | Service from 10:00 to 11:00, setup 15 min, reset 20 min | East occupied 09:45 to 11:20 exclusive. |
| West partition | Class from 10:40 to 11:10, setup 10 min, reset 10 min | West occupied 10:30 to 11:20 exclusive. |
| Whole hall | Requested from 11:30 to 12:30, setup 20 min | Needs East and West from 11:10. Both conflict for ten minutes. |
| Forty chairs | Four quarantined. Existing claim of 20 until 11:15; another claim of 10 begins 11:00 and ends 11:45. | 16 free before 11:00, 6 free until 11:15, 26 free until 11:45, 36 thereafter. |

The requester needs 14 chairs for setup and the whole session. At 11:10 both space and equipment fail. A new public start at 11:40 with setup from 11:20 satisfies both: the partitions are released, and the lowest free quantity after 11:20 is 26. Reserve both leaves and 14 chairs together. From 11:20 to 11:45, free chair quantity becomes 12. An alternative request requiring 30 chairs over the same interval still fails. Keeping the revised room while claiming the original chairs elsewhere would double promise the chairs.

Two separate bookings on the two partitions may both succeed at 09:15 provided setup and reset leave them free by their respective occupied intervals. If a service request can accept an alternative layout, show its alternate capacity and setup alongside the time difference before confirmation. A recurring booking that is blocked only on its third week should expose one exception and nine valid weeks, preserving the requester’s stated all-or-nothing or separated-date preference.

## Loan, return and damage

A steward scanning an identified projector checks its custody status, due time, condition and any qualification required of the borrower. For a pooled class whose request is ten stands, record actual issue of eight and whether two remain committed for later collection or have been released. On return of six usable and one damaged, keep one outstanding, move one to quarantine and make six available after inspection. The issue should reconcile as 8 = 6 usable returns + 1 damaged return + 1 outstanding. Do not count the quarantined stand as available merely because it is back in the building.

A lost item opens a follow-up, a maintenance defect opens a work order, and damage charge proposals go to finance with evidence. The facilities record cannot recognize a financial charge or release a deposit. Closing a work order authorizes reinspection; return to service requires the designated steward's decision. Incoming replacement equipment remains unavailable until physically received, inspected and located.

## Changes after promises were made

A water leak closes East until an unknown end. Flag all future claims whose footprint intersects East, including whole-hall services. The room steward sees affected booking identifiers, start times, required capacities and accessible features. Keep occupants, childcare authority and private meeting description restricted. The calendar editor considers alternate rooms, postponement, reduction of future sales or cancellation. A paid retreat retains all admissions and monetary history until those owners apply their decisions.

A tentative simulation proposes alternatives without notifying the church or editing live inventory. On approval re-evaluate every interval using current versions. If a competing tenant just booked the proposed room, record a stale proposal, leave the existing booking intact until the church decides, and show the new conflict. A replay of a successful relocation moves the same booking once and leaves one practical notice per affected eligible recipient.

**Reconciliation at shift change.** Compare occupied rooms with approved bookings, named custodians with issued equipment, degraded stock with open work orders, access items with return dates, and charged or refunded deposits with their linked authorized finance states. A caretaker can resolve a room inspection while accounting still shows a pending deposit refund. Each owner sees which work is theirs.

[Manual index](README.md) · [Calendar changes](recurrence.md) · [Equipment and fleet records](../../ministry/resources.md)
