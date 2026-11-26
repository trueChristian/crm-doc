# Inclusive workflows and international presentation

A member may use a screen reader, have limited literacy, share a device, read right-to-left, depend on a printed form or pay for mobile data. A service leader may be working in a noisy hall while holding a child. A secretary may enter hundreds of attendance rows by keyboard. These are supported ways of completing work. Each workflow has one named outcome, predictable navigation, a confirmation or receipt and an accessible route to correct mistakes.

## Logical records

| Entity | Fields | Relationship and constraint |
|---|---|---|
| PresentationPreference | account_id Ref(UserAccount), language_order list(tag), time_zone zone?, calendar_display code?, number_format code?, time_format code?, density code?, reduced_motion boolean?, preferred_medium code? | At most one current preference per account. A first-time visitor can use an ephemeral preference without an account. |
| LanguageEdition | content_ref ResourceRef, source_revision integer, locale tag, direction code, status code, title text?, body_ref ResourceRef, translator_ref ResourceRef?, review_by Ref(UserAccount)?, published_at instant? | Unique resource, edition and language. Store approval separately for each translation, and mark stale when its source changes. |
| LocalePolicy | scope_ref ResourceRef, default_language tag, fallback_languages list(tag), local_zone zone, display_rules structured values, date_order code | Scope precedence is explicit. Configure service times and fiscal timezones with their owning domains. |
| AssistedService | session_owner Ref(UserAccount), subject_id Ref(Person)?, task_kind code, representation_ref ResourceRef?, medium code, requested_at instant, state code, completed_at instant?, receipt_ref ResourceRef? | Record that assistance was provided, including who submitted and how the member reviewed it. Store accommodation details only where necessary. |
| FormDraft | owner_ref ResourceRef, form_ref ResourceRef, form_revision integer, current_step code, values_ref ResourceRef, saved_at instant, expires_at instant, state code | Resume only as the authorized owner or delegate. Do not retain sensitive fields beyond the shortest approved draft policy. |
| UsabilityTest | journey_key code, audience_profile code, language tag, input_mode code, device_class code, tested_revision text, result code, issue_ref ResourceRef?, retested_at instant? | Test actual tasks with representative users and document unresolved barriers, severity and alternative. |

## Interaction contract

- Every action and input has a stable text label, a programmatically associated name and a clear purpose. Keyboard order follows reading order; focused controls remain visible. Dialogs announce their purpose, keep focus inside while open and return it to the initiating control.
- People can complete sign-in, contact editing, invitations, registrations, check-in, document approval, refund review and reports using the keyboard alone. Charts, maps, drag-and-drop rosters, signature capture and verification challenges have equivalent text or assisted paths. A delegate still requires authority for the underlying act.
- Show errors next to the field and in a navigable summary. Retain valid entries, identify the action to take and announce success or failure. A timeout warns in advance when policy permits extension. Expiry never submits an unapproved draft. Dangerous or monetary actions display consequences, exact amount/currency, affected person and receipt after confirmation.
- Target at least 4.5 to 1 contrast for ordinary text and 3 to 1 for large text and essential control boundaries. Text and icons distinguish states as well as color. At 200 percent text enlargement, labels and actions remain reachable; at a narrow width equivalent to 320 layout pixels, ordinary pages reflow. Provide a readable alternate layout for wide financial grids.
- Lightweight views omit decorative downloads and optional media until requested. Show text alternatives for images, captions or transcripts for published spoken material where permitted, and labels for language, speakers and recording date. Provide text, print and large-type versions of worship orders, directions, notices and registration confirmations.
- Allow a member to save a draft on their own device, review it before final submission and obtain a reference number. Shared kiosks avoid personal autofill, recent queries and residual print previews. A secretary may enter a paper form using its original submission date and evidence; the audit identifies the actual entry operator.

## Language, dates and names

Store human names in the person's preferred form and support mononyms, aliases, diacritics, original scripts and differing family-name order. Ask how the person wishes to be addressed. Preserve non-Latin characters in search and exports. Phone and postal addresses allow region-specific formats, organizations without street addresses and contacts without a personal device.

Use language, script and regional choices explicitly. The fallback sequence is member selection, the activity's published alternatives, then the church default. Label the language actually displayed. If an approved notice or consent translation is unavailable, offer a suitable assisted path and record the edition actually accepted. Stale approval-critical translations require review before reuse. Plural forms, gendered terms where needed, currency symbols and number separators belong to the translation or formatter. Do not build translatable sentences by pasting isolated fragments together.

Present dates unambiguously in messages with mixed audiences. Recurring services use the venue's local wall time and zone; a traveler can also view personal time. Specify how ambiguous and nonexistent clock times resolve. Birth dates and festival dates remain civil dates; historical or approximate dates retain their precision. Percent, currency and distance displays include units. Numeric input accepts only a documented unambiguous local representation; ask the user when the interpretation is uncertain.

## Acceptance

- A keyboard-only user signs in, finds a service and registers two household members, corrects an invalid field, receives confirmation and exits without focus getting lost.
- A screen reader hears each required field, error summary and successful volunteer confirmation once. The visual “full” indicator has an equivalent announced state.
- In a right-to-left language, a mixed-script personal name and a financial amount remain legible and the correct record is edited. A missing translation is clearly labeled with its actual language.
- A guest using a slow connection sees usable service times and contact options before downloading a sermon image. Duplicate taps on submission create one registration.
- A secretary assists a member to review a printed summary; the register records the member as subject, secretary as operator and paper receipt as evidence. Private details are cleared on logout.
