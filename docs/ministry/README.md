# Ministry operations

A secretary can start with a group, a date or a person's assignment. A ministry leader can start with the work due this week. Each route opens the same underlying records. Churches can activate individual areas independently.

| A person wants to… | Start here | Owner of the result |
| --- | --- | --- |
| Find a group, open a campus chapter, invite a guest, or hand a roster to a new leader | [Groups and participation](groups.md) | Group coordinator |
| Recruit helpers, renew clearance, fill a vacancy, swap a shift or count service hours | [Volunteers and rotas](volunteers.md) | Volunteer coordinator |
| Publish a local or online event, change a repeated date or display it across time zones | [Calendars and occurrences](calendar.md) | Calendar editor |
| Book several places, admit walk-ins, transfer a ticket or manage a waiting list | [Registration and attendance](registration.md) | Registration desk |
| Coordinate retreat workshops, meal sittings, guest accommodation and individual itineraries | [Programmes and hospitality](programmes.md) | Programme coordinator |
| Check a child into a room, coordinate a transfer or verify collection | [Children and handover](child-check-in.md) | Authorized room and release staff |
| Prepare a service order, music set, rehearsal, accessible worship or technical cue | [Worship and music](worship.md) | Service planner |
| Offer a class, assign a lesson, track progress or issue a completion record | [Learning and formation](learning.md) | Education coordinator |
| Arrange a mission trip, partner project, pantry distribution or community outcome report | [Missions and community service](missions.md) | Outreach coordinator |
| Reserve space and equipment, arrange transport or return an item for maintenance | [Facilities, equipment and fleet](resources.md) | Facilities or transport steward |
| Run an event briefing, handle an interruption or document an after-action review | [Operational readiness](readiness.md) | Duty lead |

[Rehearse one Sunday](service-rehearsal.md) to follow a visiting household, a staffing interruption, a music change, a waiting-list offer and a verified child handover across departments. The rehearsal also defines measurable limits for optional planning assistants.

## Shared reading rules

Each table row describes one logical record. Every record has an immutable `id`, an owning `organization_id` referencing Organization, its creation instant, its last change instant and its revision number. A reference has the identifier type of its target. References are required unless marked `?`. `date` is a local calendar date, `time` a local clock time, `instant` a point on the universal timeline, and `zone` a named time zone with change rules. `count` is a nonnegative integer. `quantity` is a decimal with an explicit unit. `code` is an enumerated or configured value and `text` is human-readable content. Money carries amount and currency together. A role name denotes a capability within its assigned organization, campus or group. Scope checks also apply to exports, searches and historical views.

**Ownership.** The register owns people, households, relationships, membership and authority to act for someone. An account identifies the person taking an action. Joining a choir, attending an event or teaching a class creates a ministry connection and leaves formal church membership unchanged. The communications area delivers notices from these records and applies contact preferences. The financial and commerce areas own money, orders and postings. Each ministry area retains the relevant reference and only the minimum information staff need.

**Use across departments.** An EventOccurrence is the common dated instance for rooms, reservations, shifts, service plans, registration, check-in and attendance. A child can hold one class enrolment, attend many sessions and be in one supervised room at a time. A booking reserves a physical resource for a time interval. A seat reservation allocates a person's place. A rota assigns work. These records can succeed or fail independently. When an event changes, the organizer sees the unresolved conflicts before publishing updated arrangements.

**History.** Changes to capacity, published times, eligibility, handover, assignment, permission and approval retain actor, time, reason, previous value and new value. Audiences receive a distinct, permission-filtered view. Emergency access has an expiry, a reason and later review. Identifiable operational exports have a recorded audience, purpose and expiry.

**Readiness.** An area is ready for use when its example, exception and acceptance cases can be demonstrated with fixtures containing guests, overlapping households, restricted information, partial dates, multiple campuses, cancellations and repeat submissions. Verify both the authorized experience and what a person outside the relevant scope can discover.
