# Programmes, hospitality and personal itineraries

A weekend retreat sells one admission, lets each attendee choose workshops, serves meals and reserves accessible transport. A conference runs several simultaneous tracks and must adapt a participant's itinerary if a session moves. A programme organizes these activities without creating duplicate people, attendance or financial records.

## Records and constraints

| Record | Typed fields | Interpretation |
| --- | --- | --- |
| MinistryProgramme | `title text`, `owner_group_id → MinistryGroup`, `lead_id → Person`, `starts_on date`, `ends_on date`, `zone zone`, `main_occurrence_id → EventOccurrence?`, `state code` | Group one or more occurrences under a retreat, conference, holiday club or multi-site gathering. The main occurrence can own general admission. |
| ProgrammeTrack | `programme_id → MinistryProgramme`, `name text`, `audience code`, `language code`, `sequence count`, `access_rule code?` | A programme can contain tracks by topic, language, age or format. Track visibility and admission permission are separately checked. |
| ProgrammeSession | `programme_id → MinistryProgramme`, `occurrence_id → EventOccurrence`, `track_id → ProgrammeTrack?`, `access_code code`, `choice_group code?`, `prerequisite_session_id → ProgrammeSession?` | Access can be open, require general admission, require separate reservation, or be an authorized staff-only activity. An occurrence belongs once per programme. Reject cross-programme cycles in prerequisites. |
| ProgrammeSelection | `session_id → ProgrammeSession`, `person_id → Person`, `general_place_id → RegistrationPlace?`, `session_place_id → RegistrationPlace?`, `state code`, `selected_at instant` | References distinct general and workshop capacity claims. A provisional selection is a preference; reserve only after capacity and eligibility checks. Use original seat and waitlist services. |
| HospitalityOffer | `programme_id → MinistryProgramme`, `session_id → ProgrammeSession?`, `kind code`, `label text`, `service_start instant`, `service_end instant`, `capacity count?`, `response_due instant?`, `steward_id → Person`, `product_ref id?` | Meal sitting, overnight accommodation, translation device loan, assisted transfer or host-family placement. Define the measurement unit, privacy and allocation constraints for each offering. |
| HospitalityAllocation | `offer_id → HospitalityOffer`, `person_id → Person`, `units count`, `state code`, `preference_ref id?`, `reviewer_id → UserAccount?`, `fulfilled_at instant?`, `stock_movement_ref id?` | One active request per person and offer unless policy allows multiple units. Use requested, approved, waitlisted, cancelled or fulfilled. A dietary or access need is a restricted operational instruction. |
| ItineraryNotice | `selection_id → ProgrammeSelection`, `change_code code`, `occurrence_revision count`, `action_by instant?`, `delivery_ref id?`, `resolved_at instant?` | One notice per change and recipient. Material changes requiring a choice remain unresolved until the attendee selects or staff complete an approved manual action. |

## Decision flow

A planner lays out tracks and publishes the applicable choices, session duration, accessible route information, seat limits and admission rules. A member, household representative or guest chooses workshops for a named attendee. Check eligibility individually. A group booker needs explicit authorization to see that person's access accommodations. Prevent duplicate or overlapping required sessions and show realistic movement time between buildings. A person can still maintain tentative alternatives in a private planning view.

When payment is required, commerce determines the order and refund state. A programme pass may include three workshops, two meals and a recorded sermon for thirty days. Link each admitted activity to the person's applicable qualification. Media access belongs to the entitlement owner; attending or missing a meal cannot activate or revoke a recording. A partial admission refund identifies which session, meal or access right is affected under the stated bundle policy.

Hospitality leads receive expected portions or beds and any verified instructions needed for delivery. They can request a private clarification without exposing a medical explanation to kitchen or room volunteers. Overnight allocations and host placements require consent and safeguarding review under the church's rules. A demand forecast shows counts by service and confidence based on confirmations, with upper and lower demand if waiting places are offered. Attendees may decline optional choices. A common itinerary presents times, room changes, meal reservations, shuttle legs and a printable accessible schedule. Staff can assist a visitor without requiring an account or smartphone.

## Acceptance

| Scenario | Observable result |
| --- | --- |
| A family holds four weekend passes but only two children attend a limited workshop | Four general places and two workshop places are consumed. Workshop attendance is reconciled separately. |
| A participant selects a new session overlapping an existing confirmed choice | Show the conflict and offer an atomic exchange only if the new place can be confirmed. The original place stays effective if the exchange fails. |
| A workshop moves to another building ten minutes before a passenger boards a shuttle | Flag the affected connections, record an owner and notify only affected attendees using permitted routes. An organizer can offer another session or assisted travel. |
| A meal steward requests a count of vegetarian portions | They receive fulfilled, confirmed and outstanding quantities by sitting. Dietary explanations and household details are excluded. |
| A room opens for ten more participants in an otherwise sold-out programme | Increase the workshop pool without admitting an eleventh general attendee beyond the programme's overall limit. |

See [calendars](calendar.md), [registrations](registration.md), [transport](resources.md) and [child check-in](child-check-in.md).
