# Integrations, exports and event delivery

Every interface publishes a human-readable contract specifying the authoritative producer, record scope, required capabilities, allowed purposes, validation, success receipt, retry behavior, correction and reconciliation. A congregation can change a messaging, accounting or payment provider without changing the historic meaning of records. Only stable business identifiers cross domains. Integration data is subject to the same organization and field permissions as a staff request.

## Logical records

| Entity | Fields | Relationship and constraint |
|---|---|---|
| IntegrationPrincipal | name text, purpose_id Ref(DataPurpose), owner_id Ref(UserAccount), allowed_actions set(code), scope_ref ResourceRef, credential_ref secret reference, expires_at instant?, state code, last_used_at instant? | One dedicated non-human identity per connection and environment. Expiry and revocation invalidate pending work. |
| ConnectionProfile | principal_id Ref(IntegrationPrincipal), provider_kind code, destination_ref protected address, environment code, outbound_fields set(code), credential_revision integer, enabled_at instant?, egress_policy_ref ResourceRef | Allow only approved endpoints and require a verified test connection before activation. Credentials are replaceable without changing the identity. |
| InterfaceEdition | contract_key code, edition integer, owner_id Ref(UserAccount), required_fields set(code), optional_fields set(code), payload_rules structured schema, supported_since date, retire_after date? | Breaking changes create a new edition. Define units, codes, timestamp semantics, nullability, pagination, ordering and error meanings. |
| DomainEvent | event_key opaque, contract_id Ref(InterfaceEdition), aggregate_ref ResourceRef, aggregate_revision integer, event_kind code, occurred_at instant, recorded_at instant, actor_ref ResourceRef?, correlation_key text, cause_key text?, payload_ref ResourceRef | Created durably with the committed business change. Unique event key per organization. Payload is minimized and classified. |
| IntegrationSubscription | connection_id Ref(ConnectionProfile), contract_id Ref(InterfaceEdition), event_filter structured rule, delivery_mode code, last_checkpoint text?, enabled_at instant?, suspended_at instant? | Filter only approved event fields. Endpoints cannot subscribe beyond the principal's permissions. |
| IntegrationDeliveryAttempt | subscription_id Ref(IntegrationSubscription), event_id Ref(DomainEvent), attempt_no integer, started_at instant, completed_at instant?, outcome code, response_class code?, next_retry_at instant?, receipt_ref ResourceRef? | Unique subscription/event/attempt. Track success per subscriber, independently from business commit. |
| InboundReceipt | connection_id Ref(ConnectionProfile), sender_message_key text, contract_id Ref(InterfaceEdition), payload_digest text, arrived_at instant, authenticity_state code, business_state code, result_ref ResourceRef?, failure_key code? | Unique connection and sender message key. An existing key with a different payload enters quarantine. |
| ExchangeRequest | principal_ref ResourceRef, operation_key code, idempotency_key text, normalized_digest text, decision code, completed_at instant?, result_ref ResourceRef? | A repeated mutation with the same key and content returns the original outcome. A changed request under the same key conflicts. |
| ExportJob | requested_by Ref(UserAccount), contract_id Ref(InterfaceEdition), scope_ref ResourceRef, filter_snapshot structured rule, fields set(code), purpose_id Ref(DataPurpose), as_of instant, state code, row_count integer?, artifact_ref ResourceRef?, expires_at instant | One artifact per successful revision. Immutable job parameters bind the output to the request and user. |

## Contract behavior

Support list, detail and changes-since access where applicable. Use an opaque continuation tied to a stable sort key, snapshot, authorization and organization. A stale or expired cursor requests a fresh snapshot; an incremental feed includes deletion markers and a replay floor. Treat timestamps alone as insufficient tie breakers. Reject unknown required codes with field-level errors. Preserve supported optional fields through round trips. Include schema edition and character encoding in downloadable data. Provide a portable package with entity files, relationship keys, attachment manifest and a data dictionary.

Classify responses as accepted, committed, conflict, temporarily unavailable, permanent rejection or awaiting human review. Supply correlation and safe field-level reason without including private payloads. A receipt that acknowledges transport leaves the business operation pending until an explicit outcome arrives. Authenticate a callback, bind it to a connection and recipient, and validate freshness and prior receipts before it can change domain state. Out-of-order or missing aggregate revisions wait, reconcile against the authoritative current state or open a discrepancy. Payment notifications require the finance or commerce reconciliation specified by the owner.

Retry transient failures with bounded attempts, increasing delays and a ceiling. Pause on persistent recipient failure and alert the connection owner; record unprocessed events without blocking other subscribers. An operator can inspect redacted reasons, repair configuration and replay a stated interval. Replays must not duplicate gifts, stock depletion, receipts, notices or access grants. A manual acknowledgement references independent evidence. Record delivery and processing separately.

## Export workflow

A data steward selects a permitted purpose, scope and data dictionary edition, previews columns and submits. An approver attests if the record class, volume or recipient requires it. Recheck authority and restrictions at generation and at retrieval. If they changed, recompute or invalidate the artifact. Escape spreadsheet-active text in spreadsheet-oriented outputs while preserving original archival values in a documented safe representation. Include currency and offset/time zone fields as needed; keep dates with limited precision unchanged. Encrypt delivery and expire the artifact and access grant. Track downloads; a share link never expands authority.

## Acceptance

- Sending the same provider settlement receipt three times generates one application outcome and three delivery observations. A reused message key with a different total raises a discrepancy without posting.
- Two people updated in the same instant appear once each during snapshot pagination. Resuming after a deleted record uses the stable continuation.
- Expiring an integration credential pauses processing under that principal. Updating the credential and resuming drains the backlog once; another congregation's subscription proceeds throughout.
- An applicant is absent from an integration principal's scope. A direct request, bulk file and event subscription all omit the applicant and their attachments.
- A data steward exports ledger entries with localized labels. A different system can still reconstruct stable account keys, exact amounts, original currencies, entry-line joins and period dates.
