# Rites, milestones and register books

A church can keep baptism, dedication, profession of faith, confirmation, reception, marriage or blessing, ordination, commissioning, funeral and burial records using its own terminology and policy. An event may involve multiple principals, several witnesses and an officiant visiting from elsewhere. An account of a historical rite received from another congregation has a different provenance from an event performed locally.

## Logical records

| Record | Fields | Integrity and use |
|---|---|---|
| RiteDefinition | id ID, organization_id → Organization, code code, version integer, label text, effective_from date, until_date date?, required_roles code set, evidence_rule code, local_register_required boolean, repeat_rule enum(allow, review, once_by_policy), allowed_entry_kinds code set, certificate_template_ref ID? | Versioned local configuration. Define person roles, permitted external parties, required dates, entry numbering, certificate rules, protected fields and review authority before recording a rite. |
| RiteFieldDefinition | id ID, definition_id → RiteDefinition, field_key code, label text, value_type enum(text, date, year, code, boolean, number), allowed_values code set?, required_condition text?, visibility code, ordering integer | A structured extension for denomination- and location-specific details such as place of burial or book page. Unique key per definition version; evaluate conditions only against declared fields. |
| RegisterBook | id ID, congregation_id → Congregation, register_kind code, name text, series text, volume text, first_number integer, opened_on date, closed_on date?, custodian_account_id → UserAccount?, access_class code | Maintain independent numbering by series and volume. A closed book accepts dated amendments through an authorized correction process. |
| RiteRecord | id ID, definition_id → RiteDefinition, congregation_id → Congregation, entry_kind enum(performed_here, attested_elsewhere, historical_transcription), date_precision enum(day, month, year, unknown), occurred_on date?, occurred_month integer?, occurred_year year?, place_label text?, external_church_name text?, provenance text, evidence_ref ID?, state enum(draft, pending_review, entered, corrected, void), recorded_by → UserAccount, verified_by → UserAccount?, entered_at instant?, supersedes_id → RiteRecord? | Store known date components only; preserve source wording and provenance. Shared-event records may reference an event without exposing private fields. One ceremony can serve more than one principal. |
| RiteParticipant | id ID, rite_id → RiteRecord, role code, person_id → Person?, name_as_recorded text, sequence integer, relationship_as_recorded text?, external_affiliation text?, visibility code | At least the principals required by the rule. A witness or historic participant may have no local person record. Preserve names as originally recorded even after changes to the person register. |
| RiteFieldValue | id ID, rite_id → RiteRecord, field_definition_id → RiteFieldDefinition, value typed according to definition | One value per rite and field unless repetition is explicitly configured. The definition must belong to the rite's version. |
| RegisterEntry | id ID, book_id → RegisterBook, rite_id → RiteRecord, number integer, page_label text?, transcribed_reference text?, entered_at instant, entered_by → UserAccount, state enum(current, amended, void), amendment_ref ID? | Unique number per book. Allocate at entry; record a void or correction without reusing the number. Protect reserved numbers during simultaneous clerical entry. |
| CertificateIssue | id ID, rite_id → RiteRecord, recipient_person_id → Person?, recipient_label text, issue_number text, template_revision text, recorded_name_snapshot text, artifact_ref ID, status enum(issued, corrected, revoked), issued_at instant, issued_by → UserAccount, replaces_id → CertificateIssue?, disclosure_authority_ref ID | A rite can have several issues or extracts. Preserve exactly what was issued and its verification state. A certificate contains only the approved fields for its recipient and purpose. |

## Recording and retrieval

1. Select the ceremony and applicable definition. Where preparation is required, refer to a course, pastoral appointment or signed form and show only its completion status to the registrar.
2. Capture participants and roles, location, actual date or partial historical date and provenance. A marriage can have two principals; a baptism can record guardian or sponsor roles without granting them proxy rights.
3. Registrar reviews duplicate candidates, evidence and register scope. A possible duplicate with poor historical evidence enters a review queue. For a group service, validate each entry separately and report exact successes and failures. Enter successful records once.
4. An authorized approver confirms the entry, assigns its permanent reference, and permits an original certificate or later certified extract. A correction carries old and new wording, reviewer, reason, effective date and the earlier entry reference. Reprinting an unchanged issue is distinguishable from issuing a replacement.
5. Allow searches by name as recorded, register identifier, date range, place, participant role and permitted family link. Public inquiries receive only an authorized extract. Provide archivists a controlled export by volume including entry sequence, voids, amendments and custody manifest.
6. A rite may suggest membership follow-up under local policy. Admission still requires the authorized membership decision. Record an external baptism without claiming the church performed it. An imported burial date does not silently mark a living person as deceased; raise a verification task.

## Acceptance cases

| Case | Expected result |
|---|---|
| A year-only baptism is transcribed for someone who no longer attends | Historical year and provenance can be saved. No invented birthday, service day, account or active membership appears. |
| A spouse changes surname after a wedding | The original issue still prints the recorded names. A later extract displays only fields authorized under its template. |
| A registrar corrects a witness on an entered rite | Authorized users can reconstruct the previous version. Original book number remains reserved. An issued replacement links to the earlier issue. |
| Two clerks enter baptisms simultaneously and retry after a timeout | Each confirmed entry has one unique register number and one durable outcome. Gaps have an auditable void or reservation outcome. |
| An archivist reports local baptisms for the year | The report groups performed-here records separately from attestations and transcriptions; its definition explains whether counts are by ceremony or principal. |
