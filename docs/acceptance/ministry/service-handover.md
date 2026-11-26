# Change a service after the teams have acknowledged it

A duty lead changes the running order after rehearsal and then reconciles the hours of two people who shared a role. This test binds the public service, the published plan, the technical cue, the staffing brief and actual service observations to the same occurrence. Start each branch from the indicated checkpoint. All local times in this fixture have the same known offset.

## Approved plan and people

| Identity | Authorized scope and seeded fact |
| --- | --- |
| Plan P | One service occurrence at 10:00, one speech track with approved ServicePlan revision 4. Teaching starts 10:10, ends 10:30, and a fixed external handoff starts 10:35. The five-minute interval is an interpretation handover. |
| Position I | One required interpreter from 09:45 to 10:45. Cleared interpreter Arun accepted the required slot, Bea accepted standby and Cy declined. An accepted standby may replace a required slot only after the coordinator approves the handover. |
| Position S | Sound operator Dee has a separate accepted assignment. A private ServiceCue contains a producer communication route. Its instruction is scoped to the sound team. |
| Readiness | The operational briefing uses ReadinessPlan version 2. The technical team has acknowledged version 2. An approved change to live safety or privacy cues requires a fresh acknowledgement under this fixture policy. |
| Scope of assistance | An adviser may suggest an available interpreter from eligible workers. Only the coordinator authorizes an invitation or replacement, and only the duty lead certifies present coverage. |

## Revise the issued package

| Step | Command or concurrent change | Observable outcome |
| --- | --- | --- |
| S01 | Add four minutes to the teaching while retaining the full handover in a draft | Projected handoff moves from 10:35 to 10:39, overlapping the fixed start by four minutes. Published revision 4 stays active while the planner resolves the conflict. |
| S02 | Agree to start teaching four minutes earlier and retain the 24-minute duration | The revised interval is 10:06–10:30 and the handover still ends at 10:35. Confirm the preceding item can end at 10:06, or obtain its owner's approval to revise it. |
| S03 | Another editor issues a change to revision 4 before the first planner saves | Detect the stale base. Show both proposed changes against the issued revision. The planner must recheck timing, cues and recipients before issuing a successor. Preserve exactly one current approved revision for this track. |
| S04 | A producer now requires an earlier switch to private output and a fresh acknowledgement | Issue the authorized cue revision to the technical team. If the operational briefing instruction also changes, issue the new briefing against its applicable plan version and acknowledge that briefing. A ServicePlan revision number does not automatically become DutyAcknowledgement.plan_version. |
| S05 | Dee opens the issued cue and acknowledges the revised briefing | Record the specific briefing, assignment, plan version, time and method. A repeat submit resolves the original acknowledgment. The earlier affirmative reply remains historical. |
| S06 | The musician, the visiting speaker and a public visitor retrieve packets | Each gets the permitted order and times. Only the authorized technical team receives the producer communication route and private cue. A guest must not discover the route through a calendar feed or an obsolete attachment link. |
| S07 | The duty lead receives no acknowledgment by the agreed cutoff | Show an outstanding instruction with named follow-up. The lead applies the configured alternative or holds the affected output. Reading a bulletin, receiving a delivery receipt or appearing on the printed team list cannot certify the instruction. |

## Handover under a live assignment

Seed an additional assignment for the same interpreter at another campus from 11:05, and require 20 minutes between campuses. Arun can leave the first campus at 10:45 and meet the second start exactly. At 10:12 an organizer proposes extending the first commitment to 10:55. Model a partial replacement with dated shift segments under the same occurrence and position. Upon approval, the original shift covers 09:45–10:20 and the relief shift covers 10:20–10:45. Retire the earlier whole-interval staffing projection while retaining its history. An assignment inherits its interval from its shift.

| Step | Operational decision | Expected owner and counts |
| --- | --- | --- |
| S08 | The organizer previews extending Arun to 10:55 | Estimated arrival is 11:15, ten minutes late. Preserve both current accepted intervals and show the conflict to the coordinator. |
| S09 | Arun requests an exchange effective at 10:20. Bea has not confirmed replacement | For [10:12,10:20) there is still one required assignment. Bea is a standby only. If Arun cannot continue, display an actual coverage gap for the affected interval. |
| S10 | Bea accepts at 10:15, but the coordinator discovers that her current clearance ends before the proposed replacement period | Under the fixture rule requiring clearance for the full assigned interval, do not activate the replacement. Give the coordinator a safe eligibility outcome. Other volunteers receive no private reason. |
| S11 | A qualified reserve Cai is offered the 10:20–10:45 relief, accepts, and receives coordinator approval | Record the original, proposed candidate, reviewing account and accepted replacement in the exchange history. The duty lead observes physical handover at 10:22. Preserve the two-minute difference between scheduled and observed facts. |
| S12 | After the accepted exchange a delayed acceptance for Bea arrives | Record the superseded offer outcome. Cai remains the designated relief. Only one effective replacement for the original assignment is allowed. |
| S13 | Two time reports arrive from paper and from the returning operator | Match each observation to its assignment and distinguish observation time from entry time. Competing raw facts produce one assigned review and preserve both accounts. No duplicate approved service minutes. |

The approved time values below assume Arun actually worked 09:45–10:22 continuously and Cai 10:22–10:45 continuously. Those intervals meet at their half-open boundary. The role received 60 minutes of actual coverage, with 37 attributed to Arun and 23 to Cai. Two people served, while the required concurrent position count stayed one. The next-campus requirement remains individually attached to Arun.

For the gap branch only, set Arun's actual departure to 10:20 and keep Cai's arrival at 10:22. The coverage report now has 58 observed person-minutes and a two-minute uncovered interval. An approved correction to Arun's time references the preceding entry through ServiceTimeEntry.correction_of_id and identifies its reviewer. A previously printed 60-minute rota continues to describe the scheduled requirement.

## Reconcile plan, observed activity and reports

| Observation | Acceptable reporting result |
| --- | --- |
| The service ended at 10:43, but the team was assigned through 10:45 for closing work | Keep service end and volunteer departure independent. Report the 60-minute position interval only when its observed activities support it. |
| An operator marked a reading skipped at 10:14; later evidence establishes it was performed at 10:16 | Authorized review corrects the effective observation with change history. The approved order stays reconstructible. Recalculate actual durations and music-use statistics only where the correction applies. |
| An interpreter had an account in two congregations | The source church sees its assignments and approved minutes. A cross-church training recognition can be shared under its own authority. Neither congregation receives the other's shift list by default. |
| A coordinator repeats the approval of Cai after a timeout | The team sees one effective replacement, one resulting change notice per intended recipient, and the pre-existing acceptance outcome. Reconciliation can trace all delivery attempts to that change. |
| The church requests volunteer hours for payroll | Transfer no wage order from this fixture. The hours register reports approved volunteer minutes. A separately authorized payroll record or expense claim must carry its own evidence. |

[Worship records](../../ministry/worship.md) · [Operational briefings](../../ministry/readiness.md) · [Shift exchange fields](../../implementation/ministry/ShiftExchange.md) · [Service time fields](../../implementation/ministry/ServiceTimeEntry.md)
