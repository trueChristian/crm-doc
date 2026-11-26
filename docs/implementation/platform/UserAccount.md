# UserAccount

[Accounts, representation and authorization](../../platform/identity-access.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Zero or one current person per human account, at most one active personal account per person per organization. Supports invited users awaiting a link. Give integrations their own principal.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `person_id` | Ref(Person)? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `display_name` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `sign_in_state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `verified_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `last_sign_in_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `disabled_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `access_revision` | integer | Required when the record reaches its applicable state | [version](../value-conventions.md#version) |
| `version` | integer | Required when the record reaches its applicable state | [version](../value-conventions.md#version) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### person_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing person_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No person_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### display_name

Use human-readable text for `UserAccount.display_name`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered display_name in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No display_name at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### sign_in_state

Use versioned classification or status code for `UserAccount.sign_in_state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active sign_in_state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped sign_in_state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No sign_in_state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### verified_at

Use unambiguous point in time for `UserAccount.verified_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No verified_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### last_sign_in_at

Use unambiguous point in time for `UserAccount.last_sign_in_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No last_sign_in_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### disabled_at

Use unambiguous point in time for `UserAccount.disabled_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No disabled_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### access_revision

Use revision number or opaque revision token for `UserAccount.access_revision`. Compare under the declared revision scheme. Require the expected version for conflicting work.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | the current revision returned by the owner | Compare under the declared revision scheme. Require the expected version for conflicting work. |
| Malformed or unmapped | superseded version presented for a new approval | Reject or reopen review against the current contents. |
| Two operators begin at revision seven | two edits both cite baseline 7 | Commit the first change once and re-evaluate the second; never overwrite an unreviewed difference. |
| Re-read an already approved revision | re-open issued revision 4 after revision 6 | Return the frozen value and evidence for that edition. |
| Replay of an earlier result | same business operation observed at two revisions | Correlate by the business operation identity; a newer version does not create a second effect. |
| Incomplete record | No access_revision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### version

Use revision number or opaque revision token for `UserAccount.version`. Compare under the declared revision scheme. Require the expected version for conflicting work.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | the current revision returned by the owner | Compare under the declared revision scheme. Require the expected version for conflicting work. |
| Malformed or unmapped | superseded version presented for a new approval | Reject or reopen review against the current contents. |
| Two operators begin at revision seven | two edits both cite baseline 7 | Commit the first change once and re-evaluate the second; never overwrite an unreviewed difference. |
| Re-read an already approved revision | re-open issued revision 4 after revision 6 | Return the frozen value and evidence for that edition. |
| Replay of an earlier result | same business operation observed at two revisions | Correlate by the business operation identity; a newer version does not create a second effect. |
| Incomplete record | No version at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AccessException](../commerce/AccessException.md).`assigned_to` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AccessGrant](../commerce/AccessGrant.md).`beneficiary_account_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AccessItemIssue](../ministry/AccessItemIssue.md).`issued_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AccessRole](AccessRole.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AccountInvitation](AccountInvitation.md).`issued_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AccountabilityCohort](../assurance/AccountabilityCohort.md).`supervisor_account_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AccountabilityEntry](../assurance/AccountabilityEntry.md).`verified_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AccountabilityTransfer](../assurance/AccountabilityTransfer.md).`acknowledged_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AccountabilityTransfer](../assurance/AccountabilityTransfer.md).`dispatched_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AgreementReview](../development/AgreementReview.md).`reviewer_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AidAdjustment](../people/AidAdjustment.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AidAssessment](../people/AidAssessment.md).`assessor_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AidAward](../people/AidAward.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AidAward](../people/AidAward.md).`second_approver_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AidReview](../people/AidReview.md).`assigned_to` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AppealAllocationCredit](../development/AppealAllocationCredit.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AppealGoal](../development/AppealGoal.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AppealProspect](../development/AppealProspect.md).`steward_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AppealResponse](../development/AppealResponse.md).`next_owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AppealSnapshot](../development/AppealSnapshot.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ApprovalDecision](ApprovalDecision.md).`voter_ref` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AssistanceFeedback](AssistanceFeedback.md).`submitted_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AssistanceIssue](../ministry/AssistanceIssue.md).`issued_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AssistanceReview](AssistanceReview.md).`reviewer_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AssistanceRun](AssistanceRun.md).`actor_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AssistantEdition](AssistantEdition.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AssistedService](AssistedService.md).`session_owner` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AssuranceFinding](../assurance/AssuranceFinding.md).`responsible_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AttendanceCount](../ministry/AttendanceCount.md).`recorded_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AttendanceRecord](../ministry/AttendanceRecord.md).`recorded_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AudienceDefinition](../communications/AudienceDefinition.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AudienceSnapshot](../communications/AudienceSnapshot.md).`built_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Authenticator](Authenticator.md).`account_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AuthorityReview](../people/AuthorityReview.md).`reviewer_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AwardDecisionReview](../development/AwardDecisionReview.md).`authorized_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [BankPayoutMatch](../commerce/BankPayoutMatch.md).`matched_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [BenefitDelivery](../development/BenefitDelivery.md).`reviewer_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [BulletinEdition](../communications/BulletinEdition.md).`editor_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [BulletinItem](../communications/BulletinItem.md).`proofed_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CalendarSubscription](../ministry/CalendarSubscription.md).`account_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Campaign](../communications/Campaign.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CapabilityEnrollment](CapabilityEnrollment.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CareAssignment](../people/CareAssignment.md).`assigned_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CareAssignment](../people/CareAssignment.md).`user_account_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CareCase](../people/CareCase.md).`coordinating_account_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CareContact](../people/CareContact.md).`assigned_to` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CareDisclosure](../people/CareDisclosure.md).`authorized_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CareNote](../people/CareNote.md).`author_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CarePlanAction](../people/CarePlanAction.md).`assigned_to` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CareRequest](../people/CareRequest.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Cart](../commerce/Cart.md).`account_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CaseAppeal](../assurance/CaseAppeal.md).`independent_reviewer_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CashCount](../commerce/CashCount.md).`counted_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CashMovement](../commerce/CashMovement.md).`cashier_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CashShift](../commerce/CashShift.md).`closed_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CashShift](../commerce/CashShift.md).`opened_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CashShift](../commerce/CashShift.md).`reviewed_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CertificateIssue](../people/CertificateIssue.md).`issued_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ChangeProposal](ChangeProposal.md).`requested_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ChangeProposal](ChangeProposal.md).`reviewer_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ChannelBindingChallenge](../communications/ChannelBindingChallenge.md).`issued_to_account_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ChildCheckIn](../ministry/ChildCheckIn.md).`recorded_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Collection](../commerce/Collection.md).`verifier_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CollectionAttempt](../ministry/CollectionAttempt.md).`operator_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CollectionAttempt](../ministry/CollectionAttempt.md).`second_reviewer_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CollectionBatch](../finance/CollectionBatch.md).`custodian_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CollectionCount](../finance/CollectionCount.md).`counted_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CollectionCount](../finance/CollectionCount.md).`witnessed_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CongregationParticipation](../people/CongregationParticipation.md).`recorded_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ContactTree](../communications/ContactTree.md).`steward_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ContinuityDuty](../assurance/ContinuityDuty.md).`deputy_account_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ContinuityDuty](../assurance/ContinuityDuty.md).`primary_account_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ContinuityExercise](../assurance/ContinuityExercise.md).`authorized_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ContinuityExercise](../assurance/ContinuityExercise.md).`coordinator_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ContinuityPlan](../assurance/ContinuityPlan.md).`coordinator_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ControlTest](../assurance/ControlTest.md).`reviewer_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ControlTest](../assurance/ControlTest.md).`tester_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CountSession](../commerce/CountSession.md).`counter_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CountSession](../commerce/CountSession.md).`reviewer_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Coupon](../commerce/Coupon.md).`issued_to_account_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CreditMovement](../commerce/CreditMovement.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CustomFieldValue](CustomFieldValue.md).`recorded_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Dashboard](Dashboard.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DataPurpose](DataPurpose.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DataSource](DataSource.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DeliveryEndpoint](../communications/DeliveryEndpoint.md).`owner_account_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DeliveryException](../communications/DeliveryException.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DirectoryDisclosure](../people/DirectoryDisclosure.md).`decided_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DirectoryDisclosure](../people/DirectoryDisclosure.md).`recorded_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DirectoryExport](../people/DirectoryExport.md).`created_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DisclosurePackage](DisclosurePackage.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DisclosurePackage](DisclosurePackage.md).`prepared_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DispatchRequest](../communications/DispatchRequest.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DisposalDecision](DisposalDecision.md).`reviewed_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DisputeEvidence](../commerce/DisputeEvidence.md).`reviewed_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DocumentRevision](DocumentRevision.md).`uploaded_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DonorServiceCase](../development/DonorServiceCase.md).`assigned_to` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DuplicateCandidate](DuplicateCandidate.md).`reviewed_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DuplicateReview](../people/DuplicateReview.md).`reviewed_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [EditorialReview](../commerce/EditorialReview.md).`reviewer_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [EmergencyAccess](EmergencyAccess.md).`requester_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [EmergencyAccess](EmergencyAccess.md).`reviewer_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [EquipmentHandoff](../ministry/EquipmentHandoff.md).`recorded_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [EvaluationResult](EvaluationResult.md).`reviewer_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [EventPublication](../ministry/EventPublication.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [EvidenceCustody](../people/EvidenceCustody.md).`custodian_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [EvidenceCustody](../people/EvidenceCustody.md).`next_custodian_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ExemptionEvidence](../commerce/ExemptionEvidence.md).`verified_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ExerciseReview](../assurance/ExerciseReview.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ExerciseReview](../assurance/ExerciseReview.md).`facilitator_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ExitManifestItem](ExitManifestItem.md).`verified_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ExitPlan](ExitPlan.md).`authorized_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ExitPlan](ExitPlan.md).`requested_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ExportJob](ExportJob.md).`requested_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FacilityClosure](../ministry/FacilityClosure.md).`created_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FollowUpAction](../people/FollowUpAction.md).`assigned_to` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FollowUpAction](../people/FollowUpAction.md).`handoff_recipient_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FollowUpEnrollment](../people/FollowUpEnrollment.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FulfilmentException](../commerce/FulfilmentException.md).`assigned_to` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FundRestriction](../finance/FundRestriction.md).`reviewer_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FundingOpportunity](../development/FundingOpportunity.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FundraisingAppeal](../development/FundraisingAppeal.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GiftClaim](../commerce/GiftClaim.md).`purchaser_account_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GiftClaim](../commerce/GiftClaim.md).`redeemed_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GiftOfferAssessment](../development/GiftOfferAssessment.md).`reviewer_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GivingDocument](../finance/GivingDocument.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GrantAction](../commerce/GrantAction.md).`decision_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GrantApplication](../development/GrantApplication.md).`coordinator_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GrantApplication](../development/GrantApplication.md).`signatory_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GroupInvitation](../ministry/GroupInvitation.md).`invited_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GroupParticipation](../ministry/GroupParticipation.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GroupRolePeriod](../ministry/GroupRolePeriod.md).`appointed_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GroupRosterSnapshot](../ministry/GroupRosterSnapshot.md).`produced_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [HandlingRestriction](HandlingRestriction.md).`issuing_actor` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [HandoverCredential](../ministry/HandoverCredential.md).`reissued_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [HospitalityAllocation](../ministry/HospitalityAllocation.md).`reviewer_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [IdentityReview](IdentityReview.md).`requested_account_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [IdentityReview](IdentityReview.md).`reviewer_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ImpactPublication](../development/ImpactPublication.md).`reviewed_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ImportBatch](ImportBatch.md).`submitted_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [IncidentBulletin](../communications/IncidentBulletin.md).`authorized_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [IncidentCase](IncidentCase.md).`coordinator_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [IncidentEvidence](../assurance/IncidentEvidence.md).`submitted_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [IncidentOccurrence](../assurance/IncidentOccurrence.md).`review_owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [IncidentOccurrenceLink](../assurance/IncidentOccurrenceLink.md).`linked_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [IncidentResolution](../assurance/IncidentResolution.md).`closing_reviewer_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [IncidentReview](../assurance/IncidentReview.md).`lead_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [IncidentTriage](../assurance/IncidentTriage.md).`assigned_owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [IncidentTriage](../assurance/IncidentTriage.md).`reviewer_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [IncidentUpdate](../ministry/IncidentUpdate.md).`actor_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [InsuranceClaim](../assurance/InsuranceClaim.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [InsurancePolicy](../assurance/InsurancePolicy.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [IntegrationPrincipal](IntegrationPrincipal.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [InterfaceEdition](InterfaceEdition.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [JournalEntry](../finance/JournalEntry.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [JournalEntry](../finance/JournalEntry.md).`created_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [LanguageEdition](LanguageEdition.md).`review_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [LearningAward](../ministry/LearningAward.md).`issuer_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [LearningEnrolment](../ministry/LearningEnrolment.md).`submitted_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [LearningEvidence](../ministry/LearningEvidence.md).`attested_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [LiveSession](../commerce/LiveSession.md).`producer_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [LocalChange](LocalChange.md).`actor_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MappingEdition](MappingEdition.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MediaRelease](../commerce/MediaRelease.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MediaRights](../commerce/MediaRights.md).`reviewer_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MediaWithdrawal](../commerce/MediaWithdrawal.md).`initiated_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MembershipApplication](../people/MembershipApplication.md).`owner_account_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MembershipDecision](../people/MembershipDecision.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MembershipDecision](../people/MembershipDecision.md).`recorded_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MergeDecision](MergeDecision.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MergeDecision](MergeDecision.md).`decided_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MessageTemplate](../communications/MessageTemplate.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MetricDefinition](MetricDefinition.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MusicPermission](../ministry/MusicPermission.md).`reviewed_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OccurrenceOverride](../ministry/OccurrenceOverride.md).`changed_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OfflinePack](OfflinePack.md).`prepared_for` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OperationalAction](../ministry/OperationalAction.md).`verified_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OperationalAlert](OperationalAlert.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OperationalBriefing](../ministry/OperationalBriefing.md).`decided_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OperationalReview](../ministry/OperationalReview.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OperationsIncident](../ministry/OperationsIncident.md).`reported_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Order](../commerce/Order.md).`buyer_account_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OrderAmendment](../commerce/OrderAmendment.md).`decision_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OrderContact](../commerce/OrderContact.md).`changed_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PartnerPromise](../development/PartnerPromise.md).`accountable_owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PartnershipAgreement](../development/PartnershipAgreement.md).`authorized_signatory_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PartnershipAgreement](../development/PartnershipAgreement.md).`church_owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PartnershipDelivery](../development/PartnershipDelivery.md).`verified_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PathStepResult](../ministry/PathStepResult.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PersonMerge](../people/PersonMerge.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PersonMilestone](../people/PersonMilestone.md).`verified_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PersonRelationship](../people/PersonRelationship.md).`recorded_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PlaybackSession](../commerce/PlaybackSession.md).`beneficiary_account_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PolicyEndorsement](../assurance/PolicyEndorsement.md).`recorded_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PostingRuleVersion](../finance/PostingRuleVersion.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PresentationPreference](PresentationPreference.md).`account_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PreservationHold](PreservationHold.md).`authorized_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PreservationHold](PreservationHold.md).`release_authority` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PrintBatch](../communications/PrintBatch.md).`prepared_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProfileChangeRequest](../people/ProfileChangeRequest.md).`requested_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProfileChangeRequest](../people/ProfileChangeRequest.md).`reviewed_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProfileInvitation](../people/ProfileInvitation.md).`issued_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProjectOutcome](../ministry/ProjectOutcome.md).`reviewer_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProposalEdition](../development/ProposalEdition.md).`approval_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProposalEdition](../development/ProposalEdition.md).`submitted_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProposalRequirement](../development/ProposalRequirement.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProtectionAccess](../people/ProtectionAccess.md).`granted_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProtectionAccess](../people/ProtectionAccess.md).`user_account_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProtectionCase](../people/ProtectionCase.md).`assigned_lead` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProtectionCase](../people/ProtectionCase.md).`fallback_owner` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProtectionEntry](../people/ProtectionEntry.md).`recorded_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProtectionReferral](../people/ProtectionReferral.md).`authorized_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProtectiveMeasure](../people/ProtectiveMeasure.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PublicationApproval](../communications/PublicationApproval.md).`reviewer_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [QualityIssue](QualityIssue.md).`assigned_to` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReadinessCheck](../ministry/ReadinessCheck.md).`reviewed_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReadinessPlan](../ministry/ReadinessPlan.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReconciliationCheck](ReconciliationCheck.md).`signed_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RecoveryCheck](RecoveryCheck.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RecurringJournal](../finance/RecurringJournal.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Refund](../commerce/Refund.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RegisterBook](../people/RegisterBook.md).`custodian_account_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RegisterEntry](../people/RegisterEntry.md).`entered_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RegisteredDevice](RegisteredDevice.md).`assigned_to` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RegistrationAnswer](../ministry/RegistrationAnswer.md).`captured_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReleaseRecord](ReleaseRecord.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RemedyVerification](../assurance/RemedyVerification.md).`verifier_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReminderRule](../communications/ReminderRule.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReplyThread](../communications/ReplyThread.md).`assigned_to` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReportDefinition](ReportDefinition.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReportRun](ReportRun.md).`requested_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReportSchedule](ReportSchedule.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReportSubmissionEdition](../development/ReportSubmissionEdition.md).`reviewer_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReportSubmissionEdition](../development/ReportSubmissionEdition.md).`submitted_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RepresentationAuthority](../people/RepresentationAuthority.md).`verified_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ResponsibilityCover](ResponsibilityCover.md).`absent_account_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ResponsibilityCover](ResponsibilityCover.md).`alternate_account_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ResponsibilityCover](ResponsibilityCover.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RestoreExercise](RestoreExercise.md).`coordinator` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RetentionRule](RetentionRule.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReturnRequest](../commerce/ReturnRequest.md).`decision_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReturnRequest](../commerce/ReturnRequest.md).`requester_account_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReunificationDecision](../assurance/ReunificationDecision.md).`checked_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReunificationDecision](../assurance/ReunificationDecision.md).`handover_operator_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReunificationDecision](../assurance/ReunificationDecision.md).`reviewer_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReviewConflict](../assurance/ReviewConflict.md).`alternate_account_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReviewConflict](../assurance/ReviewConflict.md).`determined_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReviewDecision](../assurance/ReviewDecision.md).`decided_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReviewDocket](../assurance/ReviewDocket.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RiskAcceptance](../assurance/RiskAcceptance.md).`accepted_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RiskAssessment](../assurance/RiskAssessment.md).`assessed_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RiskAssessment](../assurance/RiskAssessment.md).`reviewed_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RiskControl](../assurance/RiskControl.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RiskEntry](../assurance/RiskEntry.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RiskMethod](../assurance/RiskMethod.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RiskTreatment](../assurance/RiskTreatment.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RiskTreatment](../assurance/RiskTreatment.md).`verified_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RiteRecord](../people/RiteRecord.md).`recorded_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RiteRecord](../people/RiteRecord.md).`verified_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RoleGrant](RoleGrant.md).`account_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RoleGrant](RoleGrant.md).`granted_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RollSnapshot](../people/RollSnapshot.md).`certified_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RoomBooking](../ministry/RoomBooking.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RoomStay](../ministry/RoomStay.md).`received_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RoomStay](../ministry/RoomStay.md).`sent_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SalesTaxSelection](../commerce/SalesTaxSelection.md).`reviewed_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SavedView](SavedView.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ScheduledJob](ScheduledJob.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SeatAssignment](../commerce/SeatAssignment.md).`assigned_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SeatAssignment](../commerce/SeatAssignment.md).`beneficiary_account_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Sermon](../commerce/Sermon.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SermonSeries](../commerce/SermonSeries.md).`curator_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ServiceObjective](ServiceObjective.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ServicePlan](../ministry/ServicePlan.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ServiceRunEntry](../ministry/ServiceRunEntry.md).`operator_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ServiceTimeEntry](../ministry/ServiceTimeEntry.md).`reviewed_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SessionCareInstruction](../ministry/SessionCareInstruction.md).`reviewer_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SessionReconciliation](../ministry/SessionReconciliation.md).`counted_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SessionReconciliation](../ministry/SessionReconciliation.md).`resolved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SettingDefinition](SettingDefinition.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SettingEdition](SettingEdition.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SharingRelease](../communications/SharingRelease.md).`editor_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SharingRelease](../communications/SharingRelease.md).`released_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ShiftExchange](../ministry/ShiftExchange.md).`reviewed_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SignInIdentity](SignInIdentity.md).`account_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SponsorReport](../development/SponsorReport.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StewardshipAction](../development/StewardshipAction.md).`assigned_to` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StewardshipPlan](../development/StewardshipPlan.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StockMovement](../commerce/StockMovement.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StockRecall](../commerce/StockRecall.md).`issued_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StockReceipt](../commerce/StockReceipt.md).`received_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StockTransfer](../commerce/StockTransfer.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StockTransfer](../commerce/StockTransfer.md).`requested_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StoreCredit](../commerce/StoreCredit.md).`owner_account_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SubjectRequest](SubjectRequest.md).`assigned_to` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Subscription](../commerce/Subscription.md).`subscriber_account_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SupervisionMovement](../ministry/SupervisionMovement.md).`accepted_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SupervisionMovement](../ministry/SupervisionMovement.md).`requested_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SupporterInstruction](../development/SupporterInstruction.md).`communicated_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SuppressionPeriod](../communications/SuppressionPeriod.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SyncConflict](SyncConflict.md).`assigned_to` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [TemplateEdition](../communications/TemplateEdition.md).`approved_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [TripParticipant](../ministry/TripParticipant.md).`reviewed_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [UserSession](UserSession.md).`account_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [VisitorEncounter](../people/VisitorEncounter.md).`captured_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [VolunteerApplication](../ministry/VolunteerApplication.md).`reviewer_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [VolunteerAssignment](../ministry/VolunteerAssignment.md).`assigned_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [VolunteerCredential](../ministry/VolunteerCredential.md).`verified_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [VolunteerSkill](../ministry/VolunteerSkill.md).`assessed_by` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [WorkflowEdition](WorkflowEdition.md).`owner_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [WorkspaceProfile](WorkspaceProfile.md).`administrator_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [WorkspaceProfile](WorkspaceProfile.md).`alternate_id` | UserAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
