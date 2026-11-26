# Children and supervised handover

A child's attendance answers whether they were present. A custody trail answers who was responsible for them at each point. A child may attend with a neighbor, have guardians in two households or have restrictions that change during a service. Use the register's current verified authority to determine who can consent, drop off, receive notifications or collect. Each action has its own scope, dates and any restriction. Family names, household membership and possession of a label cannot establish those permissions.

## Records

| Logical record | Fields | Cardinality and constraints |
| --- | --- | --- |
| SupervisedSession | `occurrence_id → EventOccurrence`, `room_booking_id → RoomBooking`, `group_id → MinistryGroup?`, `capacity count`, `ratio_policy_key code`, `age_band_key code?`, `duty_lead_id → Person`, `open_at instant`, `close_at instant?`, `state code` | A single occurrence may have several rooms. Open only after staff, capacity, access arrangements and readiness are confirmed. Session is open, paused, closing or reconciled. |
| ChildCheckIn | `occurrence_id → EventOccurrence`, `child_id → Person`, `place_id → RegistrationPlace?`, `dropped_by_person_id → Person?`, `arrival_adult_ref id?`, `recorded_by → UserAccount`, `arrived_at instant`, `state code`, `released_at instant?` | One open supervision record per child across overlapping supervised occurrences. Require a verified arrival adult or approved exceptional process. State is admitted, supervised, transfer pending, collection pending, released or escalated. |
| RoomStay | `check_in_id → ChildCheckIn`, `session_id → SupervisedSession`, `entered_at instant`, `received_by → UserAccount`, `left_at instant?`, `sent_by → UserAccount?`, `movement_reason code` | One check-in has many stays. At most one active room and one designated responsible staff team per child. Preserve prior rooms. |
| HandoverCredential | `check_in_id → ChildCheckIn`, `reference text`, `version count`, `issued_at instant`, `expires_at instant`, `state code`, `reissued_by → UserAccount?` | Human-readable match or machine-readable private reference. Time and session limited. Replacement invalidates previous versions. Labels use a display name and operational code, with no address, birthday, diagnosis or family restriction. |
| SessionCareInstruction | `check_in_id → ChildCheckIn`, `source_ref id`, `category code`, `instruction text`, `verified_at instant`, `expires_at instant`, `reviewer_id → UserAccount` | Scoped practical instruction such as which adult to contact, an approved food precaution or accessibility adjustment. Only the staff caring for this child and the duty lead may view it during the authorized window. |
| CollectionAttempt | `check_in_id → ChildCheckIn`, `claimant_person_id → Person?`, `verification_method code`, `authority_ref id?`, `checked_at instant`, `operator_id → UserAccount`, `second_reviewer_id → UserAccount?`, `result code`, `reason_code code?` | Many attempts, one successful final handover. Check current active authority and restrictions at collection. Record refusal or escalation privately. Evidence copies are restricted and retained only under configured policy. |
| SupervisionMovement | `check_in_id → ChildCheckIn`, `from_session_id → SupervisedSession`, `to_session_id → SupervisedSession`, `requested_at instant`, `requested_by → UserAccount`, `accepted_at instant?`, `accepted_by → UserAccount?`, `state code` | The sending team remains responsible until receipt is acknowledged. Competing moves, closed destination and excess capacity block acceptance. |
| SessionReconciliation | `session_id → SupervisedSession`, `expected_present count`, `physically_counted count`, `counted_at instant`, `counted_by → UserAccount`, `difference_reason text?`, `resolved_by → UserAccount?` | Record counts at opening, transfers, collection and evacuation according to site policy. Discrepancies remain visible until investigated. |

## From arrival to release

At reception find the person or create a controlled guest record. Confirm the present adult, eligibility, current consent, accessible arrangements and emergency contact. Assign a suitable room with available capacity and qualified supervision. Where required instructions or authority cannot be verified, refer to the designated lead. A sign-in screen in a public foyer must conceal other families' names and all restriction details. Completing admission writes one active custody record, opens the room stay and contributes one attendance observation.

At a room change, staff agree a receiving room, confirm capacity and acknowledge the actual handover. Room occupancy changes once, on acknowledgement. If receipt is overdue, the duty lead sees the sending room, intended destination and elapsed time. A child with a pending move appears in the reconciliation and remains the sending team's responsibility.

At collection, check the claimant and the live permission and restriction decision. Use the session's matching credential and any prescribed second-person approval. When authority has been withdrawn, conflicting instructions exist or collection evidence is incomplete, retain supervision and contact the designated decision maker through an approved private route. Staff handling the queue see only the action they need. A lost label requires a documented alternate identity and authorization check, a reviewer and an audit trail. A personal relationship, verbal claim or emergency contact entry alone is insufficient for release.

Successful collection atomically closes custody, ends the room stay, records collector and staff decision, and invalidates the handover credential. Two staff trying to release the same child receive one confirmed release. If nobody collects, retain an open case, escalate through the designated procedure, and record contact attempts and the eventual handover. The session cannot be marked reconciled with unresolved custody. An evacuation roster is available to designated staff with collection permissions and safe assembly information scoped to the incident.

## Operational controls and acceptance

The church sets age bands, effective date for age, required credentials, supervision ratios, consent and escalation procedures. A ratio check uses eligible staff physically present and counts active children. It re-evaluates when a volunteer departs or a room receives a child. A desk may use a controlled offline roster only with an explicit alternate method for checking current authority and synchronizing changes. If authority cannot be established, retain supervision and contact the lead. A printed sheet is numbered, returned and retired under local policy.

| Acceptance case | Observable result |
| --- | --- |
| A parent authorized for collection on arrival becomes restricted before pickup | A new check refuses release, shows minimal operator guidance and sends the exception to a designated reviewer. |
| Two parents share custody and live at different addresses | Each permission is evaluated for that child, action and date. Household contact preferences cannot grant or withdraw pickup by themselves. |
| A household receives three labels for three children | One successful collection releases only the specified child. The other two remain assigned to their rooms. |
| A child is moved during a network interruption | Staff follow the controlled handover procedure. Reconciliation records sender, receiver, times and any conflict without duplicating custody or attendance. |
| A child never arrived, although registered | The registration remains unfulfilled, the custody register has no entry, and the evacuation roster excludes the child. |
| An operations analyst requests room usage | Counts are available at the agreed aggregation level. Individual restrictions, medication details and unsuccessful claimants are excluded. |

See [registration and attendance](registration.md), [volunteers and rotas](volunteers.md) and [operational readiness](readiness.md).
