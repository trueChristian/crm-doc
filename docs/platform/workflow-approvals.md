# Work queues, workflow editions and approvals

A church secretary may need to chase a transfer certificate, an event organizer may wait for a guardian's permission and a treasurer may be waiting for an invoice approver. A personal work queue brings these assigned actions together while each domain remains the authority on what the business decision means. A task can be completed without changing a journal or confirming a meeting unless the owning domain explicitly accepts that command.

## Logical records

| Entity | Fields | Relationship and constraint |
|---|---|---|
| WorkflowEdition | workflow_key code, revision integer, purpose_id Ref(DataPurpose), owner_id Ref(UserAccount), trigger_kind code, trigger_contract_ref ResourceRef?, states set(code), transition_rules structured list, effective_at instant?, state code | Immutable published design. Each transition names source and destination, allowed role, guards, obligations and failure route. |
| WorkflowInstance | edition_id Ref(WorkflowEdition), subject_ref ResourceRef, trigger_key text, current_state code, business_calendar_ref Ref(WorkCalendar)?, started_at instant, closed_at instant?, correlation_key text, revision integer | Unique edition/subject/trigger. Existing work remains pinned unless a reviewed migration maps its state. |
| WorkItem | instance_id Ref(WorkflowInstance), step_key code, title text, assignee_ref ResourceRef?, candidate_scope_ref ResourceRef?, priority code, sensitivity code, available_at instant, due_at instant?, state code, outcome code?, claimed_at instant?, completed_at instant?, revision integer | Assign to one accountable owner or a queue that can be claimed once. Tasks can depend on named predecessors. Personal task labels must not disclose private case information. |
| WorkDependency | predecessor_id Ref(WorkItem), successor_id Ref(WorkItem), completion_rule code | No self-links or cycles. Completion rule specifies allowed outcomes for releasing the successor. |
| ApprovalRequest | instance_id Ref(WorkflowInstance), target_ref ResourceRef, target_revision integer, rule_key code, minimum_count integer, approver_scope ResourceRef, maker_ref ResourceRef, expires_at instant?, state code | Binds decisions to the exact proposed record edition and amount/terms where relevant. Independent approval applies when configured. |
| ApprovalDecision | request_id Ref(ApprovalRequest), voter_ref Ref(UserAccount), decision code, reason_ref ResourceRef?, acted_at instant, on_behalf_ref ResourceRef? | One effective decision per verified approving person and request edition. Multiple roles held by one person never multiply approval weight. |
| WorkflowStepResult | instance_id Ref(WorkflowInstance), operation_key text, attempt_no integer, input_revision integer, result_code code, result_ref ResourceRef?, occurred_at instant, error_key code? | Uniquely track each action and attempt. Business effects must have a separately deduplicated operation key. |
| WorkCalendar | label text, zone zone, weekly_open_intervals structured list, exception_dates structured list, effective_at date, version integer | Resolve local workdays and holidays when deadlines are created. Preserve deadline origin and communicate recalculation rules. |
| ResponsibilityCover | absent_account_id Ref(UserAccount), alternate_account_id Ref(UserAccount), scope_ref ResourceRef, starts_at instant, ends_at instant, permitted_task_kinds set(code), approved_by Ref(UserAccount) | Eligible cover may receive a task, but cannot gain domain authority from this record or bypass independence rules. |

## Execution and exceptions

Draft a workflow by describing the trigger, allowed states, actions, proof, deadlines and recipient of overdue tasks. Test successful, refused, incomplete, timed-out and duplicated triggers using sample records. Detect an unbounded cycle or runaway reminder before publishing. Each step has an execution ceiling, a cancellation route and a human owner. A recurring reminder inherits consent, local calendar and quiet-hour checks from communications. Pausing a workflow with pending notifications marks those obligations as paused or obsolete as defined by the owner.

A worker claims a task under their current role and scope. Validate current record edition and effective restrictions at claim, review and commit time. Independently approved requests progress only when all threshold and ordering rules hold. A proposer serving as chair and treasurer remains one individual and must not approve their own expense under a two-person policy. If eligible staff are unavailable, route to the designated independent authority. Out-of-office cover removes waiting time without changing the original approval requirements.

A business record changing materially after approval returns to review. Compare the approved proposal with its current version and show the reviewer the difference. A timed-out approval cannot be counted later without a fresh request. Store rejected, returned, delegated, expired, waived and withdrawn outcomes distinctly. Any waiver names its legal/organizational authority, reason and expiry. The worker may see ownership and deadline of a restricted task without seeing the contents of a private case.

If an external action is partial or uncertain, keep the step pending and reconcile with a stable external reference before retry. Persistent failure creates an incident or steward task. Cancelling a workflow stops outstanding work, preserves evidence and identifies completed effects requiring a domain-specific reversal. Migration to a newer workflow edition lists instances, their state mappings and remaining approvals; run a preview and retain prior editions.

## Acceptance

- A duplicate notice that a family applied for membership opens one review instance, while a new application after a prior closure receives its own trigger key.
- Two staff members claim the same follow-up simultaneously. Exactly one active assignment is created, with a clear “already claimed” result for the other.
- Editing the amount of an approved expense invalidates the prior financial approval. A duplicated approve action cannot release two payments or add an extra voter.
- A chair's alternate receives the overdue task during an absence but cannot view or approve it outside the alternate's independently granted scope.
- Pausing a rule after its reminder is queued prevents stale delivery. Reopening the process recalculates outstanding work using its approved deadline policy.
