# Organization provisioning, shared work and exit

A congregation is a ministry community. A campus denotes a site or service location. An organization controls the policy, accounts and data entrusted to it. An organization can operate several congregations and campuses. Independently governed churches can cooperate without sharing all their data. The organization's structural records and effective dates are owned by the organizational directory; the records below govern service availability and authorized exchange.

## Logical records

| Entity | Fields | Relationship and constraint |
|---|---|---|
| WorkspaceProfile | organization_ref Ref(Organization), state code, administrator_id Ref(UserAccount), alternate_id Ref(UserAccount)?, activated_at instant?, suspended_at instant?, closed_at instant?, configuration_edition text | Exactly one service profile per organization. Resolve onboarding appointments before activation; maintain a recovery authority when the last administrator leaves. |
| CapabilityEnrollment | capability_key code, state code, scope_ref ResourceRef, policy_edition text, owner_id Ref(UserAccount), starts_at instant, ends_at instant?, trial_data_policy code | Explicitly enable optional features such as storefronts, paid media and assistance. Validate dependencies before activation and plan data access after disabling. |
| OnboardingStep | profile_id Ref(WorkspaceProfile), step_key code, order_no integer, responsible_ref ResourceRef, required boolean, state code, completed_at instant?, evidence_ref ResourceRef? | Unique step per workspace and onboarding edition. Flag unresolved requirements before public launch. |
| SharingAgreement | sending_organization_id Ref(Organization), receiving_organization_id Ref(Organization), purpose_key code, permitted_classes set(code), allowed_fields set(code), recipient_role code, starts_at instant, expires_at instant, approval_sender_ref ResourceRef, approval_receiver_ref ResourceRef, state code | Explicit cross-organization relationship. Each side sees its own authorized agreement details. No automatic federation by network membership. |
| SharedDelivery | agreement_id Ref(SharingAgreement), sender_subject_ref ResourceRef, exported_fields set(code), sent_at instant?, payload_digest text, receiver_reference opaque?, accepted_at instant?, recall_state code, state code | One explicitly scoped transfer. Recipient uses its own local identity keys. Maintain evidence for correction and agreed deletion notices. |
| ExitPlan | profile_id Ref(WorkspaceProfile), requested_by Ref(UserAccount), authorized_by Ref(UserAccount)?, export_scope set(code), planned_stop_at instant, successor_contact_ref ResourceRef?, retention_decision_ref ResourceRef, state code | Requires independent organization authority before final shutdown. A custodian may remain for legally or pastorally retained records. |
| ExitManifestItem | plan_id Ref(ExitPlan), class_key code, format_key code, count integer, checksum text?, artifact_ref ResourceRef?, verification_state code, verified_by Ref(UserAccount)? | Include attachments, joins, stable keys, permissions, restrictions, account attribution, balances, receipt evidence and known exclusions. |

## Opening and operation

1. Verify the authority of the person setting up the church. Establish organization boundaries, named primary and recovery contacts, language, time zone, currency and fiscal year. Create a first privileged account through an independently verified appointment. Store no real personal data in a sample workspace.
2. Decide which features the church uses, what it calls membership and ministries, who approves sensitive actions, whether visitors appear in directories and which tasks require data consent. Give newcomers a minimal role. Show each ministry owner the impact of enabling optional features.
3. Prepare test records and simulate registration, invitation, giving, check-in, minutes approval and a failed notification as applicable. Confirm account recovery, accessible member entry, restrictions and opening balances. Record custodian acceptance and clear test data before live activation.
4. For a campus move, group closure, church split or merger, record effective dates, responsibilities, access changes and historic reporting. Moving an operational scope inside a church retains history under its original context. Transfer between independent organizations requires different authority, a deliberate record set, recipient acceptance and reconciliation. Membership never automatically creates a personal record in every affiliated church.
5. Suspend a compromised connection, active account or whole workspace at the narrowest appropriate boundary. Preserve evidence and access for authorized incident custodians. Publish a generic availability notice without disclosing personal data. Recovery follows an approved reopening decision.

## Shared work and offboarding

For a joint camp, define the hosting church, the responsible church for emergencies and the minimum event roster the host may see. The sending church confirms it may share each field for the event purpose. A host can acknowledge receipt without seeing the wider directory. Communicate corrections and withdrawals under the agreement, identify offline copies and expire the host's access after the event. An invitation to register directly with the host is an alternative where policy requires direct collection.

For network reports, authorize each participating organization independently, agree metric definitions and aggregation limits, then send permitted aggregates. A network officer has no default power to search across congregations, inspect donor-level details, read care notes or administer local accounts. Joint workspaces have named owners and an exit route.

For closure, stop new public sales and subscriptions on the agreed date, settle outstanding orders and donations, supply refunds and statutory/organizational records under designated ownership, notify active members through approved channels and revoke integrations. Produce the export package and have the receiving custodian verify it by restoring a sample person, household, approved minutes and balanced financial period. Store retained materials and holds under an assigned custodian. Remove public listings, scheduled messages and active credentials. Dispose of expired replicas and document backup expiry dates. Closing a workspace never reassigns church funds or automatically joins directories.

## Acceptance

- Two independent churches both use an external contact key of 1001, the same volunteer email and the same campus name. Each user and report sees only its own domain unless an explicit valid sharing agreement is exercised.
- At a joint camp, the host receives the approved attendance roster with emergency instructions; regular donors, unrestricted household addresses and unrelated siblings never appear. The host's access expires at the agreed cutoff.
- When a congregation becomes independent, past attendance and journals remain attributable to their former organization; only the agreed records and current rights transfer to the successor.
- An organization can verify and take delivery of a complete portable export before closure. Active payment obligations, holds, undelivered receipts and missing acceptances are visible and individually assigned before shutdown.
