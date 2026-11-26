# Organization

[Churches, congregations, campuses and governing networks](../../foundation/organization.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One organization owns many congregations, campuses, configuration versions and staff assignments. Civil registration and ownership of a financial ledger are independently verified.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | Owner-scoped business value; see the record rule | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `code` | unique text | Required at applicable lifecycle step | [text](../value-conventions.md#text) |
| `display_name` | text | Required at applicable lifecycle step | [text](../value-conventions.md#text) |
| `legal_name` | optional text | Optional under owner conditions | [text](../value-conventions.md#text) |
| `organization_kind` | local_church, network or service_body | Required at applicable lifecycle step | [enum](../value-conventions.md#enum) |
| `default_locale` | language tag | Required at applicable lifecycle step | [language](../value-conventions.md#language) |
| `default_zone` | zone | Required at applicable lifecycle step | [zone](../value-conventions.md#zone) |
| `status` | onboarding, active, suspended or archived | Required at applicable lifecycle step | [enum](../value-conventions.md#enum) |
| `established_on` | optional dates | Optional under owner conditions | [date](../value-conventions.md#date) |
| `closed_on` | optional dates | Optional under owner conditions | [date](../value-conventions.md#date) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `Organization.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Organization·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### code

Use human-readable text for `Organization.code`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered code in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### display_name

Use human-readable text for `Organization.display_name`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered display_name in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No display_name at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### legal_name

Use human-readable text for `Organization.legal_name`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered legal_name in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No legal_name provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### organization_kind

Declared alternatives in owner order: `local_church`, `network`, `service_body`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | local_church | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_organization_kind | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No organization_kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### default_locale

Use language or locale identifier for `Organization.default_locale`. Resolve the published language or locale without inferring a person’s nationality.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | en | Resolve the published language or locale without inferring a person’s nationality. |
| Malformed or unmapped | unmapped locale display label | Keep the source value for review. |
| Specific translation unavailable | specific translation missing at delivery time | Apply the declared fallback and identify which language is being displayed. |
| User changes preferred language | approved letter after preferred-language change | Future communications use the effective preference; issued wording is preserved. |
| Two regional variants exist | two permitted regional variants in catalogue | Apply the requested locale/version where available. |
| Incomplete record | No default_locale at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### default_zone

Use time zone with civil-time rules for `Organization.default_zone`. Preserve zone identity; use the applicable local rules for the date.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Africa/Windhoek | Preserve zone identity; use the applicable local rules for the date. |
| Malformed or unmapped | ambiguous zone abbreviation | Require a named zone or explicitly supported fixed offset. |
| Future recurring appointment | fixed local Sunday service across offset change | Recompute local-time occurrences using its stored zone and change policy. |
| Staff view from a second zone | remote attendee opens the schedule abroad | Show the requested local display without moving the actual instant. |
| Zone changes for a campus | campus adopts a new effective zone | Re-evaluate future occurrences and retain historical issue evidence. |
| Incomplete record | No default_zone at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### status

Declared alternatives in owner order: `onboarding`, `active`, `suspended`, `archived`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | onboarding | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_status | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No status at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### established_on

Use civil calendar date for `Organization.established_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No established_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### closed_on

Use civil calendar date for `Organization.closed_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No closed_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AccessDecision](../commerce/AccessDecision.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AccessPlan](../commerce/AccessPlan.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AgreementParty](../development/AgreementParty.md).`internal_organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AidProgram](../people/AidProgram.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ArchiveCollection](../administration/ArchiveCollection.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AssuranceFinding](../assurance/AssuranceFinding.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AudienceDefinition](../communications/AudienceDefinition.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [BulletinEdition](../communications/BulletinEdition.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [BurialGround](../administration/BurialGround.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Campaign](../communications/Campaign.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Campus](Campus.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CapabilityTrial](../verification/CapabilityTrial.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Cart](../commerce/Cart.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Category](../commerce/Category.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CeremonyRequest](../administration/CeremonyRequest.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ChannelPublicationTarget](../communications/ChannelPublicationTarget.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ChurchAffiliation](ChurchAffiliation.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ChurchAffiliation](ChurchAffiliation.md).`related_organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CommunicationPurpose](../communications/CommunicationPurpose.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ConcernSubmission](../assurance/ConcernSubmission.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Congregation](Congregation.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ConsolidationGroup](../finance/ConsolidationGroup.md).`reporting_organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ContactTree](../communications/ContactTree.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ContinuityPlan](../assurance/ContinuityPlan.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DeliveryEndpoint](../communications/DeliveryEndpoint.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DispatchRequest](../communications/DispatchRequest.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [EmploymentEngagement](../administration/EmploymentEngagement.md).`legal_employer_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ExemptionEvidence](../commerce/ExemptionEvidence.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FinanceBook](../finance/FinanceBook.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FollowUpPath](../people/FollowUpPath.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FundingOpportunity](../development/FundingOpportunity.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FundraisingAppeal](../development/FundraisingAppeal.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GiftOfferAssessment](../development/GiftOfferAssessment.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GivingParty](../finance/GivingParty.md).`party_organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GoverningBody](../governance/GoverningBody.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Household](../people/Household.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [IncidentBulletin](../communications/IncidentBulletin.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [IncidentOccurrence](../assurance/IncidentOccurrence.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [IncidentReport](../assurance/IncidentReport.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [InsuranceClaim](../assurance/InsuranceClaim.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [InsurancePolicy](../assurance/InsurancePolicy.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [LoanTitle](../administration/LoanTitle.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MediaAsset](../commerce/MediaAsset.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MediaContributor](../commerce/MediaContributor.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MediaRights](../commerce/MediaRights.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MembershipPolicy](../people/MembershipPolicy.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MessageTemplate](../communications/MessageTemplate.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MilestoneDefinition](../people/MilestoneDefinition.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OfficeRequest](../administration/OfficeRequest.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Order](../commerce/Order.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OutreachReferral](../people/OutreachReferral.md).`referring_organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ParticipationCategory](../people/ParticipationCategory.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PartnershipAgreement](../development/PartnershipAgreement.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Person](../people/Person.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PriceList](../commerce/PriceList.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProcessorPayout](../commerce/ProcessorPayout.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Product](../commerce/Product.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Promotion](../commerce/Promotion.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProtectionPolicy](../people/ProtectionPolicy.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PublicPage](../administration/PublicPage.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RelationshipType](../people/RelationshipType.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReminderRule](../communications/ReminderRule.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReplyThread](../communications/ReplyThread.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReturnDefinition](../administration/ReturnDefinition.md).`authority_org_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReturnInstance](../administration/ReturnInstance.md).`reporting_org_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReturnPeriod](../administration/ReturnPeriod.md).`receiving_org_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RiskControl](../assurance/RiskControl.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RiskEntry](../assurance/RiskEntry.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RiskMethod](../assurance/RiskMethod.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RiteDefinition](../people/RiteDefinition.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SenderIdentity](../communications/SenderIdentity.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Sermon](../commerce/Sermon.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SermonSeries](../commerce/SermonSeries.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SharingAgreement](../platform/SharingAgreement.md).`receiving_organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SharingAgreement](../platform/SharingAgreement.md).`sending_organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SharingRequest](../communications/SharingRequest.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ShopChannel](../commerce/ShopChannel.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StaffPosition](../administration/StaffPosition.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StockLocation](../commerce/StockLocation.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StoreCredit](../commerce/StoreCredit.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Subscription](../commerce/Subscription.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SuppressionPeriod](../communications/SuppressionPeriod.md).`organization_id` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [WorkspaceProfile](../platform/WorkspaceProfile.md).`organization_ref` | Organization identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
