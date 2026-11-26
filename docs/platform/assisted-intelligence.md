# Optional assistance with retrieval, drafting and translation

A secretary asks, “Which approved council decisions about the hall roof still have open actions?” The assistant returns each resolution, its meeting date, current action owner and a link to the permitted record edition. If two councils used the same hall name, it asks which council. If the minutes are still in draft or contain no answer, it says exactly what it found. Staff can reach the same records using ordinary search.

## Suitable capabilities and authority

| Capability | Allowed inputs and output | Decision owner and limits |
|---|---|---|
| Find an approved decision, procedure, sermon or event | Accessible, current, permitted records; a concise answer with edition-specific internal evidence. | Viewer can open the cited context. Hidden records never determine suggestions or count as a reason given to the viewer. |
| Draft minutes or extract action candidates | Explicitly authorized meeting material and agenda; proposed decisions, owners, due dates and uncertainty. | Clerk edits and compares proposals with the meeting evidence. The chair or authorized body follows its normal confirmation process. |
| Prepare a notice or translation | Approved event facts, audience class, language and approved terminology; a labeled draft with source date. | Communications owner verifies time, venue, meaning and audience. Sending remains a separate authorized operation. |
| Improve sermon accessibility | Authorized source recording or text; provisional transcript, speaker labels, chapters and captions with time ranges. | Media editor verifies names, sensitive testimonies, usage rights and publication permission before release. |
| Explain aggregate figures | Permitted, sufficiently aggregated report values and approved metric definitions; explanation with report period and edition. | Treasurer checks conclusions. Deterministic reports supply all figures. AI cannot post entries or supply a missing balance. |
| Help navigate church services | Published service descriptions in the member's selected language and accessible format. | Present human contact and ordinary search. Avoid spiritual or medical determinations or evaluation of individual beliefs. |

The organization enables each capability separately. People can use equivalent ordinary workflows and decline optional processing within the relevant purpose. Exclude restricted care, known safety cases, donor-level data, children’s records and sensitive meeting material from default retrieval and model training. Model output must never decide release of a child, eligibility for assistance, discipline, membership admission, volunteer safeguarding clearance or a financial approval. Do not rank people by generosity, spirituality, vulnerability or predicted departure. Staff can create reviewed aggregate trends without assigning such labels to individuals.

## Logical records

| Entity | Fields | Relationship and constraint |
|---|---|---|
| AssistancePolicy | capability_key code, scope_ref ResourceRef, enabled boolean, purpose_id Ref(DataPurpose), permitted_classes set(code), allowed_operations set(code), processing_boundary code, retention_class code, reviewer_role_ref Ref(AccessRole), edition integer | A denied purpose or class blocks processing before retrieval or transfer. A disabled capability leaves ordinary screens usable. |
| AssistantEdition | capability_key code, model_family text, revision text, instruction_edition text, evaluation_ref ResourceRef, approved_by Ref(UserAccount)?, approved_at instant?, state code | Pin the edition used for each result. Changes to retrieval, prompts, vocabulary or model require evaluation. |
| AssistanceRun | policy_id Ref(AssistancePolicy), edition_id Ref(AssistantEdition), actor_id Ref(UserAccount), scope_ref ResourceRef, request_digest text?, started_at instant, state code, completed_at instant?, output_class code?, fallback_reason code? | Recheck current rights and purposes on retrieval, review, opening and final action. Store raw personal prompts only if explicitly allowed. |
| EvidencePin | run_id Ref(AssistanceRun), source_ref ResourceRef, source_revision integer, excerpt_locator text, selected_fields set(code), checked_at instant | References are internal, versioned and individually access-checked. Never reveal the label or existence of a now-inaccessible source. |
| AssistedDraft | run_id Ref(AssistanceRun), target_kind code, draft_ref ResourceRef, language tag, uncertainty_flags set(code), state code, supersedes_ref Ref(AssistedDraft)? | A draft may have successive edited versions. Applying it to a domain record requires independent normal validation. |
| AssistanceReview | draft_id Ref(AssistedDraft), reviewer_id Ref(UserAccount), decision code, changed_fields set(code), reason text?, decision_at instant, domain_result_ref ResourceRef? | Can approve, request edit, reject or withdraw. Publication, sending and posting require separate domain actions. |
| EvaluationCase | capability_key code, scenario_key code, language tag, fixture_ref ResourceRef, expected_behavior code, prohibited_fields set(code), scoring_rule structured test | Use synthetic or expressly authorized evaluation data. Include unfamiliar names, limited data, failed access and stale permissions. |
| EvaluationResult | edition_id Ref(AssistantEdition), case_id Ref(EvaluationCase), run_at instant, actual_result code, evidence_ref ResourceRef?, reviewer_id Ref(UserAccount)?, outcome code | Release gate records exact results and repeatability. Restrict output artifacts to evaluation users. |
| AssistanceFeedback | run_id Ref(AssistanceRun), submitted_by Ref(UserAccount), issue_kind code, submitted_at instant, state code, response_at instant?, corrective_action_ref ResourceRef? | Route factual errors, rights leaks, poor translations and accessibility issues to their owners. |

## Execution, cost and expiry

Filter candidates using current authority, permitted classes and effective consent before assembling input. Apply equivalent controls to extracted text, embeddings or other derived representations. Treat words inside imported documents as source content. They carry no authority to change instructions, fetch unrelated records or contact anyone. A processing agreement defines service location, permitted data, retention, operator access, learning use and disposal confirmation. An unapproved processor or unknown agreement blocks the feature.

Show the viewer when a passage is paraphrased, which internal records support it and which details need checking. For numerical or eligibility queries use the authoritative domain calculation and cite its edition. If evidence conflicts, show the discrepancy and route to the custodian; when evidence is absent, provide the ordinary search or staff contact. A generated suggestion conveys no permission to access its source. Accessibility features include keyboard review, text alternatives and original/translated passages side by side.

Recheck pins and material permissions when a draft is reviewed or reused. A changed source edition marks affected drafts stale; re-open or regenerate after review. Revocation of a source invalidates cached answers, snippets and derived indexes. If an already-approved public item was based on a later-withdrawn source, notify its owner and use the normal correction, takedown or republication process. Keep the record of actions actually taken and minimize retained prompt content.

Set per-organization quotas and timeouts, show an estimate for long media work and expose cancel, fallback and cost totals without private prompts. Before rollout, compare with a trusted human-authored sample in the church's languages. Fail the gate for any unauthorized disclosure, unreviewed external action, fabricated internal reference or unsafe protected decision in the acceptance set. Specify minimum acceptable transcription and translation quality with the publishing team. Run a limited opt-in trial and repeat after each edition change. Disable a malfunctioning capability immediately; keep ordinary church operations available.

## Acceptance

- A secretary can open each cited resolution around the hall roof. A private pastoral discussion mentioning the same roof contributes neither a result nor a visible hint.
- Removing access after an answer was cached prevents the viewer from reopening a protected answer or excerpt. A published correction creates a visible review task for the owner of an earlier draft.
- Minutes containing text instructing an assistant to send a roster yield no outbound operation. Only a proposed summary reaches the authorized reviewer.
- A translation changes the meaning of an event deadline. The reviewer corrects it before publication and logs the language issue against that edition.
- A question about an individual's predicted giving produces no ranking; an authorized treasurer can separately retrieve the approved aggregate financial report.
- A cancelled transcription sends no publication request. During a processor outage the editor can upload an approved caption file and complete the same publication workflow.
