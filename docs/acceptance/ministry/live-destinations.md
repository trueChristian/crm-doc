# Run one service on several live destinations

The church operates its own viewing page. Its producer can select a church-operated origin, one or more hosted relays under church-controlled accounts, and an optional external audience channel. This fixture exercises two services running concurrently, a partial outage, and a withdrawal during transmission. The church can enable one destination without enrolling in any other. Local times below are UTC on the same date. The stated audiences and cutoffs are fixture policy.

## Prepare the records

| Fixture identity | Owner and starting evidence |
| --- | --- |
| Morning, east campus | The service has its own EventOccurrence, approved ServicePlan revision 3 and SermonDelivery E. The scheduled LiveSession E points to that delivery and its reviewed live rights. |
| Morning, west campus | A second occurrence uses the same Sermon but has a different SermonDelivery W and LiveSession W. Both services start at 09:00. W is restricted to members throughout. |
| Church web origin O | The viewing page uses this origin for E. A restricted viewing session for W evaluates W's audience on every new playback authorization. A waiting page has separate permission to show its title. |
| Optional relay R | A verified production ConnectionProfile serves a church account. The church has approved public live forwarding for E during its teaching item only. R does not accept a members-only audience. |
| Disabled relay D | A connection exists for a future destination. Its account and delivery subscription are inactive. Enabling R leaves D disabled. |
| East teaching item | The producer has reviewed record, church-web live and public relay use from 09:10 to 09:30. The following family testimony is in-room only. A separate, cleared holding slide is available for both active outputs. |
| West teaching item | The destination decision permits W on the members' church player. W has no approved public forwarding or recording use. |

Use the service, delivery and live-session identities to choose the stream. A common sermon title, room name, scheduled time or encoder nickname cannot distinguish these fixtures. Bind a destination to the connection, environment, external session identity, live session, approved audience and policy revision when enabling it. Keep the binding effective interval and prior revisions. A repeated external identity from a different church account belongs to that account's own mapping.

Store the routing policy version in scoped configuration. The protected endpoint belongs to ConnectionProfile, the credential reference to IntegrationPrincipal, and credential revision to the connection. The producer's ordinary view shows the connection label, last verified state, allowed uses and a safe reason for any hold. Public pages, status exports and ordinary operator histories omit provider keys and protected source addresses. Revoking one church's connection invalidates its outstanding operations against that connection.

## Connect and start

| Operator action | Durable outcome and viewer-visible proof |
| --- | --- |
| Publish E's waiting page at 08:40 while the source is silent | A public visitor sees the approved start information. Site discovery and play probes for W reveal only the audience-approved result. There is no live claim until content is available. |
| Start an input test at 08:45 with a private color slide | E becomes testing. A producer sees the preview. O and R continue to show only the approved pre-service state. Preview is never selected for public delivery as a side effect of a successful connection test. |
| Submit a start for W using E's external session reference | The receiver checks the binding and quarantines or rejects the mismatch. E and W retain their preceding states. A private reviewer can diagnose the two session references. |
| Open E on O at 09:00 for approved opening material, holding R until 09:10 | E is live on O. R has no audience-bound delivery of the opening. The producer sees the per-destination distinction. D receives no start request. |
| Start W on its church origin | An authorized member may play W. An anonymous visitor cannot get W's captions, stream or listening address by obtaining a copy of its page address. No recording begins. |
| Reach the east teaching cue at 09:10 | Recheck rights for E, this component, R, its audience and current time. One activation reaches R. Connect the player to an approved origin for its current audience. The web page keeps its church-owned location. |
| Send the same successful start receipt twice | The same receipt key and payload return the existing decision. The external route, chargeable start operation and session opening each have one business effect. Provider billing evidence, when available, can be reconciled to that one operation. |
| Attempt to attach R to W on the strength of E's public clearance | The authorization predicate fails for W. Preserve E's legitimate R session and W's active church member stream. |
| Give the route operator a new credential revision mid-service | Verify the new revision in its proper scope. Invalidate the old revision for future privileged operations after the approved cutover. Existing viewer grants follow their own authorization lifetimes. Require an explicit recovery action if the provider cannot rotate an active input. |

## Distinguish source loss, destination loss and a service ending

| Observation | Producer, viewer and reconciliation outcome |
| --- | --- |
| 09:13, R stops acknowledging delivery, but O still plays | Mark R degraded or its delivery pending as appropriate to the evidence. E remains live on O. A transport timeout is not proof that the remote audience stopped receiving content. |
| 09:14, retry an R activation after an acknowledgement was lost | Query the remote service for the bound external session where supported, or present one pending reconciliation to its owner. Retry with the original operation key where the contract supports it. Never start an uncorrelated second channel to clear the alert. |
| 09:16, both E outputs lose their common input | E is interrupted. The web page shows a connection interruption or the approved holding item. Record when loss was observed, which outputs were affected and the last verified media boundary. W continues independently. |
| 09:17, another relay offers to take over but can serve only public playback | Recheck the intended audience, destination grant, recording behavior, territory and component rights. A configured and cleared alternative may serve E. W remains held on its approved members' route if its existing source also fails. |
| 09:18, E's source is restored | Rejoin the same delivery/session and establish the first verified resumed media boundary. Record the gap in the private production report. The service does not gain another occurrence, sermon or named attendee. |
| R sends a delayed “offline” signal about 09:13 after recovery | Preserve the observation time and source. Compare the bound session, event revision and current observed state before updating the route. A historical outage can be recorded without making a recovered route unavailable again. |
| R rejects authorization and the connection owner suspends it | Stop further operations under that subscription. O can remain live for E. Restore only after the owner verifies scope and the authorized component is still in progress. |
| The operator selects pause on the church page | Verify the configured pause scope. A page-only pause has no effect on an independently active, external relay. Expose separate route status and a stop-all action for producers authorized to control all outgoing feeds. |

## Withhold a component and end the session

At 09:29:50 the east operator prepares the switch to the cleared slide. The intended cut is the boundary before the private testimony enters any unapproved output. A destination with buffering or delay must receive already-cleared material upstream of its buffer. A change to the text on the web page cannot protect a continuing outgoing feed.

1. Switch to the approved slide or silence before the disallowed source enters the encoder or outgoing route. Confirm the change from the monitored outgoing material on each selected route. Withhold the affected input if the cut cannot be verified. The in-room service can continue.
2. At 09:30 close R's teaching interval and stop forwarding E's raw service feed. Record the operation identity, local cutoff, remote acknowledgment and any unresolved delivery window. A provider that cannot apply this restriction cannot carry this service segment.
3. If the producer discovers that a private segment passed at 09:30:04, preserve a restricted review record with first and last known media offsets and affected destinations. Stop further exposure immediately on controlled outputs. Request removal of remote replay or clips, record confirmations separately and notify the responsible privacy and ministry roles through the appropriate restricted process. Do not claim that prior viewers' copies have been removed.
4. At 09:42 end E. A normal end on W at 09:46 must not alter E. Late start or live callbacks for either ended session retain their receipts and cannot restart transmission. A later rebroadcast needs its own scheduling and rights decision.
5. Open the church playback page as an anonymous visitor, authorized member, producer and expired member. Recheck the public discovery text, captions, direct playback and every alternative rendition. None may fall through to an unrestricted copy. Preserve end time, restricted operational evidence and any authorized private recording candidate.

## Acceptance measurements

| Surface | Expected observation at the end |
| --- | --- |
| Source service count | Two occurrences, two deliveries and two live sessions. The shared sermon work remains one. The east input recovery does not increment them. |
| Provider operations | R was selected only for E. D has no live operations. Each sent action names a permitted environment and a bound destination. Repeated receipts resolve to the existing result. |
| Church viewing policy | Four observer roles have tested the actual outgoing resource as well as the church page. Streaming devices may be counted in a separate measure. A stream view has created zero individual AttendanceRecord entries in this fixture. |
| Recovery | The east interruption has a start and observed recovery with affected routes. Unconfirmed remote cutoff remains open for its owner until independent evidence resolves it. |
| Recording | E has at most the authorized private recording candidate. W has zero recording candidates. Public replay count from these live events alone is zero. |

[Live session fields](../../implementation/commerce/LiveSession.md) · [Service cues](../../implementation/ministry/ServiceCue.md) · [Integration receipts and retry](../../platform/exchange-events.md) · [Archive acceptance](archive-handover.md)
