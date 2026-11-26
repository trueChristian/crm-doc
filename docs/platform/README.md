# Shared records and operating rules

Use these pages when a decision applies in several departments. A family is described in the people register, for example, while the right of a signed-in adult to act for a specific child is evaluated using the identity and privacy rules here. A church app can submit a registration or update through the API, and authorized staff can use MCP to discover and perform approved tasks. Every surface uses the same church rules.

## Find a task

| Task | Open | What the reader can decide |
|---|---|---|
| Open a church workspace, run a joint camp or leave the service | [Organization lifecycle](organization-lifecycle.md) | Isolation boundaries, independent federation, commissioning, controlled sharing and portable exit. |
| Invite someone, recover access, delegate a task or remove a leader | [Accounts and authorization](identity-access.md) | Account linkage, proof, session access, role scopes, delegated powers and emergency review. |
| Handle a photo refusal, privacy request, preservation hold or erasure | [Privacy and records](privacy-records.md) | Purpose-specific evidence, effective choice, restriction, redaction, retention and accountable disposal. |
| Translate the interface or support a shared device or paper form | [Inclusive experience](experience-accessibility.md) | Accessible actions, local language, dates, assisted entry, form recovery and measurable validation. |
| Add a custom register field, bilingual form or supporting document | [Configuration and documents](configuration-content.md) | Safe choices, typed fields, immutable editions, attachments, publication and rollback. |
| Route a form for review, chase a deadline or cover an absent approver | [Workflow and approvals](workflow-approvals.md) | Guarded transitions, claims, deadlines, evidence, separation of duties and compensation. |
| Migrate a spreadsheet, correct a duplicate or reconcile imported designations | [Migration and data quality](migration-data-quality.md) | Provenance, mapping, staged validation, stewardship, merges, cutover and reconciliation. |
| Build a church app, accept inbound updates or enable an assistant tool | [Church apps, the API and MCP](church-apps-and-integrations.md) | Which system owns the decision, what may cross the boundary and how can the church prove a complete workflow? |
| Exchange data, subscribe to a change or download a portable extract | [Exchange and events](exchange-events.md) | Credentials, contract editions, replay, idempotency, export rights and receipt handling. |
| Register arrivals at a temporary venue with unreliable connectivity | [Offline continuity](offline-continuity.md) | Minimal packs, expiry, conflicts, safe fallback, local evidence and synchronization. |
| Search a register or issue a reproducible annual report | [Search and reporting](search-reporting.md) | Metrics, eligibility, privacy, dashboards, snapshots and restatement. |
| Run service-day checks or recover after an outage | [Operations and recovery](operations-recovery.md) | Support ownership, monitoring, incidents, backup scope, rehearsals, verification and reopening. |
| Offer an assistant to find a decision, draft a notice or caption a sermon | [Assisted intelligence](assisted-intelligence.md) | Optional capabilities, permission boundaries, evidence, human review, quality gates and costs. |

## Reading the records

Logical records describe information and constraints independently of an implementation. The table notation is defined under [Accounts and authorization](identity-access.md). Foreign keys must target records in the same organization unless an explicitly authorized exchange names the recipient and permitted payload. When a field is a resource reference, validate the allowed resource type, scope and purpose at the point of use. Published editions are immutable. A subsequent correction creates a successor linked to the original event or edition.

Each page includes observable acceptance cases suitable for implementation, migration or a church commissioning exercise. Evaluate the ordinary workflow, refusal, overlap, expiry, concurrent action, revocation and recovery wherever the domain permits them. A policy choice belongs to its named custodian, with a particular scope, edition and effective date.

## Ownership handoffs

| Origin | Platform agreement | Return to department |
|---|---|---|
| People verifies an adult's authority over a child's named activities | RepresentationGrant evaluates that verified authority for a bounded account action. | Events and check-in revalidate the authoritative clearance at the point of use. |
| A person changes communication choices | ConsentDecision keeps purpose-specific evidence; the communications department resolves approved channel, subscription and endpoint. | Delivery rechecks eligibility, expiry and suppression before actual handoff. |
| An approved resolution, registration or gift correction produces a change | DomainEvent captures the committed source edition; subscribers maintain independent checkpoints. | The domain decides compensation, status and correction semantics. |
| A member requests a portable record | SubjectRequest protects identity evidence; DisclosurePackage limits fields, lifetime and audience. | Each custodian supplies permitted records and evaluates third-party redaction. |
| A supplier or staff member proposes a material change | ApprovalRequest binds authority to the exact proposed edition. | The owning department revalidates and commits the approved operation once. |
| A church publishes a report or generated summary | ReportRun binds the data cutoff and metric edition; EvidencePin links an assisted result to an accessible internal source. | The responsible secretary or treasurer reviews and issues the authoritative result. |
