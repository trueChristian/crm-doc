# Facilities, equipment and fleet

A room can be offered to several ministries at different times, partitioned into smaller rooms, shared with another tenant or hired to an outside organization. A volunteer can borrow one identified projector or reserve twelve folding chairs. A vehicle reservation promises the vehicle. A passenger allocation promises a seat on a particular leg. The steward can trace each promise from request to return and identify the person responsible at each handoff.

## Facilities and time commitments

| Logical record | Fields | Cardinality and rules |
| --- | --- | --- |
| FacilitySpace | `campus_id → Campus`, `parent_id → FacilitySpace?`, `name text`, `space_code code`, `space_type code`, `capacity count`, `access_features code_set?`, `zone zone`, `steward_id → Person`, `status code` | Hierarchy of building, floor, hall and child rooms. Unique campus code. Capacity, accessible entry, induction loop and amenities support discovery. Sensitive key or entry instructions stay restricted. |
| SpaceConflict | `space_id → FacilitySpace`, `other_space_id → FacilitySpace`, `conflict_kind code`, `reason text` | Undirected exclusion or shared-layout rule. Reserve a hall and prevent concurrent use of its partitioned halves, while independent halves can be reserved together. Canonicalize pair order, reject self-reference. |
| SpaceLayout | `space_id → FacilitySpace`, `label text`, `usable_capacity count`, `setup_minutes count`, `reset_minutes count`, `layout_ref id?` | Space can have banquet, lecture or classroom layouts. Usable capacity cannot exceed its approved space limit. |
| RoomBooking | `space_id → FacilitySpace`, `layout_id → SpaceLayout?`, `occurrence_id → EventOccurrence?`, `requester_id → Person`, `external_party_ref id?`, `purpose text`, `starts_at instant`, `ends_at instant`, `setup_minutes count`, `reset_minutes count`, `expected_people count?`, `hold_until instant?`, `state code`, `approved_by → UserAccount?` | Evaluate conflicts using the half-open occupied interval including setup and reset. States requested, held, approved, occupied, released, cancelled, declined. External hire can exist without a church event. |
| FacilityRental | `booking_id → RoomBooking`, `agreement_ref id`, `payer_ref id`, `billing_order_ref id?`, `deposit_ref id?`, `insurance_review code?`, `inspection_outcome code?`, `settlement_state code` | Finance owns deposit liability, invoicing, forfeiture approval and refunds. No facility operator can create cash or settle an invoice by completing a room inspection. |
| FacilityClosure | `space_id → FacilitySpace`, `starts_at instant`, `ends_at instant?`, `reason_code code`, `created_by → UserAccount`, `public_label text?`, `work_order_id → ResourceWorkOrder?` | Planned maintenance and urgent closures affect future proposals and trigger a review for existing reservations. Unrelated private incident details remain hidden. |

## Equipment and stewardship

| Logical record | Fields | Cardinality and rules |
| --- | --- | --- |
| EquipmentClass | `code code`, `title text`, `tracking_kind code`, `unit code`, `qualification_required code?` | Track individually identified equipment or pooled quantities. Consumable stock leaves inventory on issue and follows stock movement rules. |
| EquipmentItem | `class_id → EquipmentClass`, `tag text`, `serial text?`, `home_space_id → FacilitySpace?`, `asset_ref id?`, `condition code`, `state code`, `inspection_due_on date?` | One physical unit with an organization-unique tag. Asset reference ties equipment to the financial fixed-asset record where applicable. |
| EquipmentPool | `class_id → EquipmentClass`, `space_id → FacilitySpace`, `owned_qty decimal`, `unusable_qty decimal`, `last_counted_at instant?` | One pool per class, location and unit. Available quantity at a time accounts for outages, losses and overlapping reservations. |
| EquipmentReservation | `item_id → EquipmentItem?`, `pool_id → EquipmentPool?`, `occurrence_id → EventOccurrence?`, `booking_id → RoomBooking?`, `custodian_id → Person`, `starts_at instant`, `due_at instant`, `quantity decimal`, `state code` | Exactly one item or pool, with quantity one for an identified item. Booked, issued, partly returned, returned, overdue, lost and cancelled. Prevent double allocation. |
| EquipmentHandoff | `reservation_id → EquipmentReservation`, `action code`, `quantity decimal`, `occurred_at instant`, `giver_id → Person?`, `receiver_id → Person?`, `condition code`, `note text?`, `recorded_by → UserAccount` | Preserve each issue, partial return, transfer or loss report. Returned quantity cannot exceed outstanding quantity. Disputed damage requires review. |
| ResourceWorkOrder | `space_id → FacilitySpace?`, `item_id → EquipmentItem?`, `vehicle_id → MinistryVehicle?`, `reported_at instant`, `priority code`, `description text`, `assigned_to → Person?`, `due_on date?`, `state code`, `cost_ref id?`, `reopened_from_id → ResourceWorkOrder?` | One primary asset or space per order. Link related orders for multi-asset work. Log triage, assignment, completion evidence, independent acceptance where needed and next inspection. |
| AccessItemIssue | `space_id → FacilitySpace`, `item_reference text`, `recipient_id → Person`, `issued_at instant`, `due_at instant?`, `returned_at instant?`, `issued_by → UserAccount`, `state code` | Manage assigned keys, cards and temporary access under restricted visibility. Loss opens a steward action, with identifying access details excluded from broad notifications. |

## Fleet and assisted transport

| Logical record | Fields | Cardinality and rules |
| --- | --- | --- |
| MinistryVehicle | `campus_id → Campus`, `fleet_tag text`, `passenger_seats count`, `accessible_seats count`, `seat_layout_code code`, `registration_ref text?`, `asset_ref id?`, `inspection_due_on date?`, `insurance_due_on date?`, `state code` | Passenger capacity excludes driver. Alternative layouts explicitly define trade-offs between seat types. Compliance evidence and registration are restricted. |
| TransportJourney | `vehicle_id → MinistryVehicle`, `occurrence_id → EventOccurrence?`, `trip_leg_id → TripLeg?`, `driver_id → Person`, `departs_at instant`, `returns_at instant`, `route_label text`, `state code`, `opening_distance decimal?`, `closing_distance decimal?`, `distance_unit code?` | Recheck vehicle availability, capacity and driver clearance for entire journey. A paid driver or reimbursable mileage references finance separately. |
| TransportStop | `journey_id → TransportJourney`, `sequence count`, `public_label text`, `private_location_ref id?`, `scheduled_at instant`, `actual_at instant?` | One journey has ordered collection and drop-off stops. Drivers see only assigned riders and practical details during duty. |
| PassengerBooking | `journey_id → TransportJourney`, `person_id → Person`, `board_stop_id → TransportStop`, `leave_stop_id → TransportStop`, `seat_type code`, `assistance_ref id?`, `state code`, `boarded_at instant?`, `alighted_at instant?` | Both stops belong to the journey; leave follows board. Reserve capacity per segment and seat configuration. A child's authority for boarding or handover is checked separately. |

## Scheduling and exceptions

The steward can pencil in a tentative booking, set an expiry and assess conflicts before approval. Show maintenance, space layout, cleaning time, shared partition, equipment and travel overlap in a single decision. The same selected room and time requested simultaneously must produce a single confirmed allocation. Concurrency decisions apply across related partitions and pooled quantities. When a recurring reservation conflicts on two dates, indicate them individually and let the requester accept only the available dates or select alternatives. Moving a published service produces a capacity and accessibility recheck.

If a room becomes unusable after sales, keep existing admissions visible while the organizer approves a replacement, reduced capacity plan or cancellation. For equipment, issue the items actually collected and inspect returns before making damaged quantities available again. For transport, a late driver or missed pickup creates a coordinator action and a private notification; it does not mark a rider absent from worship. Keep route sheets limited to actual assigned riders and expire them after the journey.

## Acceptance

| Scenario | Observable result |
| --- | --- |
| Hall reservation ends at 13:00 with 30 minutes' reset; another begins at 13:20 | Conflict is visible through 13:30. A 13:30 start with zero setup can proceed. |
| East and west partitions are booked independently | A whole-hall booking conflicts with both. Returning one partition leaves the other unavailable. |
| Thirty chairs are held from a pool of forty and five are unusable | Five remain available in the overlap. Returning eight of ten issued chairs keeps two outstanding. |
| A driver loses clearance the day before a trip | Journey enters review, coverage alert goes to the coordinator, and private evidence stays restricted. |
| Five riders leave before four board at a later stop | Capacity checks reflect riders on each segment, while total distinct riders can exceed the vehicle's simultaneous passenger capacity. |
| An outside hirer reports a broken projector | Handoff and work order link to the item and rental; a proposed charge goes to finance for authorization and evidence. |
