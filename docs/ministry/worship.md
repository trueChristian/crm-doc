# Worship and music

A planner prepares a service from a reusable order, selects readings and music, confirms people, distributes an approved plan and records what actually happened. A small church can use a one-page printed order. A larger church can run parallel plans in two languages with different musicians and technical cues.

## Records

| Logical record | Fields | Cardinality and rules |
| --- | --- | --- |
| WorshipTemplate | `name text`, `season_code code?`, `language code`, `group_id → MinistryGroup?`, `version count`, `state code` | Templates define reusable ordered sections. Applying a template makes a version-specific copy so later changes leave published services intact. |
| ServicePlan | `occurrence_id → EventOccurrence`, `template_id → WorshipTemplate?`, `title text`, `language code`, `planner_id → Person`, `state code`, `revision count`, `approved_by → UserAccount?`, `approved_at instant?` | One occurrence may have several tracks, for example different venues or languages. One approved active revision per track. Cross-track dependencies are explicit. |
| ServicePlanItem | `plan_id → ServicePlan`, `parent_id → ServicePlanItem?`, `sequence count`, `kind code`, `title text`, `duration_minutes count?`, `fixed_local_start time?`, `lead_person_id → Person?`, `visibility code`, `content_ref id?` | Acyclic sections contain items and subitems. Kinds include welcome, prayer, reading, music, sermon, offering, communion, testimony, announcements and dismissal. Permit silence or an untimed item. A fixed start can expose a timing conflict. |
| ServiceCue | `item_id → ServicePlanItem`, `team_code code`, `sequence count`, `trigger text`, `instruction text`, `responsible_assignment_id → VolunteerAssignment?`, `attachment_ref id?` | Technical or accessibility cue such as microphone change, interpretation handoff, visual announcement or caption start. Public orders exclude private cues. |
| ServiceRunEntry | `item_id → ServicePlanItem`, `status code`, `actual_start instant?`, `actual_end instant?`, `operator_id → UserAccount`, `reason text?` | Capture performed, skipped, substituted or interrupted. Timing reports distinguish projected and actual lengths. Preserve approved plan. |
| MusicWork | `title text`, `alternate_title text?`, `language code`, `composer_credit text?`, `writer_credit text?`, `catalogue_key text?`, `owner_label text?`, `themes code_set?`, `status code` | Multiple works may share a title. Catalogue keys and credited names aid disambiguation. Lyrics, scores and recording assets require their own access and rights checks. |
| MusicArrangement | `work_id → MusicWork`, `title text`, `language code`, `key_code code?`, `tempo_per_minute count?`, `time_signature text?`, `instrumentation text?`, `duration_seconds count?`, `revision count`, `asset_ref id?` | A work can have several keys, languages or arrangements. A service selection identifies the exact version issued to each participant. |
| MusicPermission | `work_id → MusicWork`, `arrangement_id → MusicArrangement?`, `use_code code`, `territory_scope text`, `valid_from date`, `valid_until date?`, `reviewed_by → UserAccount`, `decision code`, `evidence_ref id?` | Separate decisions for in-room performance, printing, projection, rehearsal downloads, live transmission and archival access. Venue or online terms can differ. Unknown or expired permission requires review for the affected use. |
| MusicUse | `item_id → ServicePlanItem`, `arrangement_id → MusicArrangement`, `sequence count`, `selected_key code?`, `planned_use code_set`, `actual_use code_set?`, `reported_at instant?` | A medley has multiple uses in order. Record actual performance and scope for usage reporting, including substitutes on the day. |
| RehearsalCall | `plan_id → ServicePlan`, `occurrence_id → EventOccurrence`, `team_id → MinistryGroup?`, `instructions text?`, `published_at instant?` | Distinct rehearsal occurrence with its own reservations and availability checks. Schedules reference published material and its authorized audience. |

## Planning, access and handoff

1. Choose the service date and track, copy the seasonal order, set the service's expected finish and position the fixed-time elements. Catch overlaps and missing owners before approval. Assign staffing via duty shifts so the same volunteer cannot unknowingly be assigned to the children's room and a music item at once.
2. Link each sermon slot to a speaker or guest and any planned teaching series. The church publication reviewer approves the recording, transcript, permitted audience and access window. A separately authorized provider can report an applicable external entitlement. A scheduled speaker or public service time alone cannot authorize publication. An archive editor sees outstanding recording and rights decisions before releasing the service.
3. Select the arrangement and intended uses. The approved public bulletin can list titles and credits under the configured policy. Private arrangements or rehearsal references are visible only to authorized participants and only while the relevant permission remains effective. Allow a planner to publish the order with the unapproved asset suppressed.
4. Issue a dated revision to musicians, floor teams, operators, interpreters and the congregation using distinct views. Performers may receive their calls, keys and charts. Operators receive cue sheets. Members can obtain a large-print, accessible or translated order. Keep drafts, prayer confidences and private telephone numbers off public copies.
5. A live operator can mark an item complete, skip a cue or add an unscheduled item. After the service the planner reviews actual times, work use and outstanding follow-up. A substitution in a published music set requires a fresh permission check for recording or distribution.

## Verification

| Scenario | Required result |
| --- | --- |
| Two simultaneous services share a speaker | The planner sees the overlap and travel issue before confirming both. |
| A song is approved for in-room use and its recording decision is pending | In-room teams receive permitted materials. The publishing editor sees an unresolved archive use and can omit or hold that segment. |
| The choir receives revision four after making notes on revision three | Both issue records remain; each view identifies the current revision and changed cues. |
| A communion item takes eight minutes longer than planned | Actual run sheet captures the overrun and projected downstream times change. Approved source timings remain historically reproducible. |
| A deaf member opens the published service order | The member can find interpretation availability, accessible service details and text alternatives for public instructions. |
| A musician withdraws before rehearsal | The coverage dashboard exposes the vacancy, while past music use and the identity of the previous performer remain traceable. |

See [volunteers](volunteers.md) and [calendars](calendar.md).
