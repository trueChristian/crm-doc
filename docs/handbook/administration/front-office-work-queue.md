# Front-office queue, assisted service and resource lending

A receptionist handles three distinct types of work. A public question such as a service time can be answered immediately. An enquiry that promises a return call needs a tracked owner and safe route. A confidential disclosure needs a restricted handoff. Staff should be able to do all three without accidentally enrolling someone, creating an account or publishing their details.

## Screen and queue behavior

| View | Initial columns | Filters and actions | Fields kept outside this view |
| --- | --- | --- | --- |
| Unassigned requests | Reference, received time, broad routing topic, time promised, campus, safe-channel indicator | Claim, refer, reprioritize with reason, find overdue work. Claim compares current assignment revision. | Private message body, child identity, care notes and donor detail. |
| My callbacks | Reference, agreed local window and zone, permitted communication route, next action | Open a permitted request, record attempt, reschedule or hand over. | Another worker's restricted request and unrelated family contact. |
| Team supervision | Waiting age, queue, owner, stage, reassignment reason and due time | Rebalance workload and accept returned referrals. | Sensitive narrative unless separately authorized. |
| Public enquiry | Current service location, schedule, language, accessible directions and validity | Answer, print approved directions or refer to a published contact. | Private premises details, attendance list and internal identifiers. |
| Lending counter | Inventory accession, article description, copy state, kit condition and due date | Issue, renew, return, reserve or report a damaged item. | Other borrowers' identities and their full household history. |

A claim changes a queue item to one accountable owner. If a team is only a candidate group, taking the work prevents simultaneous claims; reopening puts it back into a named queue. A returned referral shows the sending office that the receiver declined or could not accept. A successful send without acceptance remains outstanding. Closing a reception request never certifies that a care case, investigation, grant payment or booking finished.

## Worked shift

At 09:00 a guest asks about an accessible entrance. The receptionist gives the public directions. No named profile is needed. At 09:12 a person asks for a private call between 14:00 and 14:30 and excludes voicemail. Store the safe route privately. At 13:50 a staff member becomes unavailable. The supervisor redirects the task to an eligible colleague and records the receiving person's acceptance. At 14:08 the colleague gets no answer. Record one attempt, leave no voicemail, and follow the agreed retry route. The earlier receptionist can verify handoff status without opening the private narrative.

If the caller later asks for the directory, the enquiry reference alone cannot establish identity or membership. If the guest requests deletion of the call details, identify the subject, applicable purpose and any retention or hold first. A public report of ordinary office demand can count the request without including the callback number or the sensitive topic.

## Lending inventory and returns

Use a LoanTitle for the reusable catalogue entry and a LoanCopy for the physical item. A study kit containing six books can circulate as one individually checked kit. Record the list issued and the condition. The purchase value or depreciation belongs to financial or asset records. A second-hand donated book offered for sale must be received into the correct inventory disposition before it can also be represented in a lending pool.

| Transaction | Required checks | Accepted result | Reversal or exception |
| --- | --- | --- | --- |
| Place reservation | Eligible borrower or accepted guest identity, title/copy, pickup site and queue policy | Waiting position with tie-break input and notification preference | An expired offer advances once. A returned book triggers only one next offer. |
| Issue | Available actual copy, borrower, due date and time convention, expected contents, issuer | One open loan, copy unavailable and a receipt that states the original contents | A second check-out is rejected even if the catalogue view was cached. |
| Renew | Current borrower or authorized staff, renewal limit, holds waiting, applicable exception | New due date with change history and permitted notice | A waiting borrower's precedence cannot disappear through a backdated edit. |
| Return complete kit | Verified copy, actual date, recorder and condition | One return, next status determined from queue and condition | Duplicate check-in returns the existing receipt without new notices or charges. |
| Return with missing item | Received items and condition, missing piece, safe acknowledgement | Open condition case and route copy to inspection; issue evidence of partial return | Assessing a fee requires an authorized decision and an accounts receivable reference. |
| Declare lost and later recover | Last custody event, reviewed decision and later recovery evidence | Keep linked loss and recovery events; update loan and asset state under their owners | A cash refund of a previously settled fee follows its own approved finance workflow. |

A reservation and a loan have different effects. A lender may see the number waiting without seeing other borrowers. A notification worker rechecks loan status just before issuing an overdue reminder. A returned loan with a missing part may still have an investigation open; the reminder must describe only the authorized outstanding matter.

[Office and lending records](../../administration/office-services.md) · [Administration manuals](README.md)
