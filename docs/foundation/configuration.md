# Applying church policy to forms and approvals

Churches decide what qualifies for membership, which offices exist, how they certify a roll, which communications are optional, what counts as a quorum and when an expenditure needs a second signature. Preserve each choice with its owner, scope, version and effective time. Translated labels such as fellowship, assembly and parish may describe the same underlying concept. An old report must still be interpretable in the language and rules used when it was certified.

## Where each fact belongs

| Question | Authoritative record | Church-specific interpretation |
| --- | --- | --- |
| Who defines the type and permissible values of this choice? | SettingDefinition, with effective values held by SettingEdition | One owner defines fallback, units and whether a narrower scope may override. No conflicting effective value at the same scope and instant. |
| How is an option translated or retired? | VocabularyTerm and the published language edition | Display a translation for the reader or indicate the fallback. Keep a stable term code for historical use. A changed meaning requires a different code. |
| What questions did the person actually answer? | FormEdition and FormSubmission | A submitted form is pinned to its exact edition, privacy notice, language and review history. Later configuration edits leave it readable. |
| Who owns the follow-up? | WorkflowEdition, WorkflowInstance and WorkItem | A published workflow freezes the start conditions, ordering, stop conditions, task owner and failure route. A care referral may expose only “contact assigned coordinator”. |
| Who approved this exact proposal? | ApprovalRequest and ApprovalDecision | A response binds to the target revision. A material edit invalidates the earlier approval. Several roles held by one person never satisfy two independent signatures. |
| Which church instrument controls a board vote? | CharterEdition and ProcedureRule | The governance clerk identifies the operative rule for the meeting class and date. Changing an ordinary preference cannot override an adopted charter. |

## Question, answer and route details

These are the logical children of the corresponding platform records. A conforming implementation may keep ordered children inside an immutable edition.

| Child | Fields | Invariants |
| --- | --- | --- |
| FormQuestion | id; form_edition_id → FormEdition; stable_key: code; input_kind: text, option, integer, amount, date, reference, file or acknowledgement; labels: localized text; constraints, allowed_options, show_when: typed definition; required_when_shown: boolean; sensitivity, retention_class: codes; display_order: integer | Rule dependencies cannot form cycles. Hidden questions are cleared from pending submissions and never block completion. Files require type and size validation. |
| FormAnswer | submission_id → FormSubmission; question_id → FormQuestion; ordinal: integer; value: typed; classification: code; source_language: optional tag | Enforce the question's type and cardinality. The question belongs to the submitted edition. Corrections have an amendment, reason and actor. |
| ApprovalStage | id; workflow_edition_id → WorkflowEdition; step_key: code; sequence: integer; eligible_role: ref; threshold: integer; route: all, any or count; substitute_rule: optional policy; deadline_rule: optional duration/calendar | Each stage instantiates an ApprovalRequest. Later stages open after the required predecessor outcome. A substitute must independently possess authority. A single response cannot count on different sides of a separation-of-duties rule. |

## Worked example and checks

A new-member form asks which congregation the guest attends. Choosing baptism preparation opens an additional question and a voluntary follow-up request. A secretary can return an incomplete form. Acceptance creates one membership application linked to its source. A volunteer who can distribute the form cannot approve admission or read a protected answer.

Two conflicting active quorum policies at the same scope cannot publish. A new translation has no effect on an earlier vote. A reviewer who also submitted a restricted payment request is routed to another authorized reviewer. A voluntary checkbox initially appears unselected. A person withdrawing a form stops pending reminders and triggers the applicable retention workflow. A policy changed after submission is shown alongside the original effective policy if a reviewer must resolve a transitional case.

Continue to [shared configuration and documents](../platform/configuration-content.md), [work queues and approvals](../platform/workflow-approvals.md) or [governing authority](../governance/README.md) for the complete record and transition definitions.
