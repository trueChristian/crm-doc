# Registration, tickets and attendance

An invitation is an offer to respond. A registration requests places. A seat is a capacity claim. A ticket grants admission under stated conditions. Attendance records an observation. Keep those meanings distinct so guests who walk in, people who paid and did not attend, and anonymous headcounts are reported accurately.

## Records

| Logical record | Fields | Cardinality and validation |
| --- | --- | --- |
| AdmissionOption | `occurrence_id → EventOccurrence`, `label text`, `capacity count?`, `units_per_seat count`, `opens_at instant`, `closes_at instant`, `fee_product_ref id?`, `eligibility_rule code?`, `max_per_request count?`, `transfer_policy code`, `cancel_policy code` | Examples include general admission, a family table, transport or an accessible seat. Shared room or vehicle capacity applies across options. Option-specific pools require a documented release rule. |
| EventRegistration | `occurrence_id → EventOccurrence`, `booked_by_person_id → Person?`, `contact_ref id?`, `group_id → MinistryGroup?`, `submitted_at instant`, `state code`, `request_key text`, `order_ref id?`, `terms_revision text?` | One occurrence has many registrations. Require a responsible person or restricted guest contact. A repeat request with the same key and content returns the original result. |
| RegistrationPlace | `registration_id → EventRegistration`, `option_id → AdmissionOption`, `person_id → Person?`, `guest_label text?`, `quantity count`, `state code`, `hold_expires_at instant?`, `confirmed_at instant?`, `cancelled_at instant?` | For named attendance, one place per attendee. Unnamed group allocations require a responsible contact and a positive quantity. For child sessions obtain a verified person record before admission. |
| AdmissionSeat | `option_id → AdmissionOption`, `seat_label text`, `zone_label text?`, `accessible_features code_set?`, `place_id → RegistrationPlace?` | Optional allocated seating. One active allocation per seat and occurrence. Reserve accessible stock according to stated policy and protect accessibility requests. |
| WaitingEntry | `place_id → RegistrationPlace`, `priority_band code`, `queued_at instant`, `sequence count`, `split_allowed bool`, `offered_at instant?`, `offer_expires_at instant?`, `state code` | Sort by approved priority, queue time and sequence. Retain offer history. Tied times have deterministic ordering. An organizer records any exception and reason. |
| AdmissionTicket | `place_id → RegistrationPlace`, `version count`, `token_reference text`, `issued_at instant`, `state code`, `redeemed_at instant?`, `replaced_by_id → AdmissionTicket?` | One live single-admit ticket per named place or unit. A ticket's scannable value contains no name, date of birth or payment information. Transfer or reissue invalidates prior version. |
| AttendanceRecord | `occurrence_id → EventOccurrence`, `person_id → Person?`, `place_id → RegistrationPlace?`, `group_id → MinistryGroup?`, `state code`, `observed_at instant`, `recorded_by → UserAccount`, `source code`, `correction_reason text?` | Named or restricted guest observation. Unique counted presence per person and occurrence. Mark present, excused, absent, late or remote only where reliably known. Record room movements or multiple scans separately. |
| AttendanceCount | `occurrence_id → EventOccurrence`, `segment code`, `observed_at instant`, `count count`, `method code`, `relationship_to_named code`, `recorded_by → UserAccount` | Declare total headcount, additional anonymous count or estimate. Overlapping estimates cannot be added. Anonymous participants have no invented identities. |
| RegistrationAnswer | `place_id → RegistrationPlace`, `question_revision_ref id`, `answer typed_value`, `sensitivity code`, `captured_by → UserAccount?`, `captured_at instant`, `expires_on date?` | Only collect answers needed for this activity. Acknowledgement ties to exact terms version and signer, with independent records for guardians where required. |

## Admission and changes

1. A family selects three places. Check eligibility, consent where applicable, sales dates, per-person restrictions and all capacity pools together. A group stays together unless the booker explicitly allows a partial allocation. Unpaid reservations use an expiring hold whose time is shown to the booker.
2. For a paid place, commerce owns order and payment. Confirmation uses a verified settlement or authorized payment state selected by event policy. A fee waiver records its authorizer, purpose and fee amount. If a late payment arrives after expiry, try a fresh allocation. When capacity has filled, route the recorded payment for refund or authorized alternative. Do not displace the current holder.
3. A cancellation makes a confirmed place available, retires active tickets and requests a refund assessment under the accepted terms. Releasing capacity and paying a refund each have a separate status. Partial cancellations leave the rest of the family booking intact. Fees, discounts and tax are corrected in commerce and finance.
4. Offer released places to the waiting list. An offer holds exactly the offered units until expiry. On timeout, release them once, update the entry and offer the next eligible set according to the published policy. Staff can see households skipped because of the contiguous-seat requirement.
5. At entry the steward checks validity, version and prior redemption. A duplicate scan displays the original redemption time to authorized staff. Re-entry policy can record exit and re-entry without adding another attendee. A ticket transfer checks the new holder's eligibility and replaces the credential. Printed, low-connectivity and walk-in workflows share the same reconciliation rules.

An offline device records a unique observation and receipt time. Without a live seat authority it can admit only preallocated inventory under a written local decision. Duplicate redemption across offline devices is flagged for review on synchronization. Recorded actual attendance survives an admission dispute. A guest may remain anonymous where registration and safeguarding policies allow it. A visitor explicitly requesting follow-up may be linked to a person later with staff review and unchanged historical counts.

## Attendance reports and examples

Attendance rolls can show expected, checked in, absent and unmarked separately. Count adults, children, volunteers and online attenders under explicitly named measures. A streamed view device can represent several people. Show device views separately from individually confirmed participants. A leader gets their own event's roster, a ticket checker gets minimal admission details, and an analyst can receive totals with small groups suppressed.

| Acceptance case | Observable result |
| --- | --- |
| Capacity is 50. There are 46 confirmed and three held places | One place remains bookable. An expiring hold releases its three places once, even under retry. |
| A registration for three meets room capacity of two | It waits as a unit unless the booker previously allowed a split. A seat guaranteed to another family remains unavailable. |
| A cancelled ticket is scanned after transfer | Staff see that the credential is invalid. Only the replacement is eligible. Both versions remain traceable without disclosing the new holder to the old holder. |
| 60 named people attended and ushers counted 82 people in total | Display 60 named and 82 total. If counts are comparable the estimate of unnamed attendees is 22. Never report 142. |
| Two scanners observe the same named attendee | Both scan observations can be audited. The named attendee total increases by one. |
| A welcome visitor has no name or email and declines follow-up | An authorized anonymous counter increments. No fabricated person, communication recipient or formal membership is created. |
