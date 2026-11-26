# Risk ownership, control testing and prevention

The board needs to know which risks it has accepted, which controls actually operated and which actions are overdue. A risk is a possible harmful event. An incident is an occurrence; a control is a specific preventive, detective or corrective measure; a treatment is an agreed change. Keep an accountable person and an independent review path for each material decision.

## Logical records

| Record | Fields | Rules and relationships |
|---|---|---|
| RiskMethod | id ID, organization_id → Organization, version integer, title text, scope_ref ID?, likelihood_levels ordered codes, impact_levels ordered codes, rating_matrix pairs → rating, time_horizon duration, appetite_by_category code map, valid_from date, valid_until date?, approved_by → UserAccount | Validate that each likelihood/impact pair resolves exactly once; distinguish qualitative labels from numerical estimates. Freeze the version used in a decision and state the period the rating covers. |
| RiskEntry | id ID, organization_id → Organization, congregation_id → Congregation?, campus_id → Campus?, category code, cause text, event text, consequence text, owner_id → UserAccount, opened_on date, next_review_on date, visibility code, state enum(proposed, active, under_review, accepted, retired), predecessor_id → RiskEntry? | One scope and purpose per risk; link a scoped risk to an organization-wide parent where useful. Preserve localized ownership. Acquiring insurance may transfer an exposure but does not prove a control works. |
| RiskAssessment | id ID, risk_id → RiskEntry, method_id → RiskMethod, assessed_on date, horizon_end date, inherent_likelihood code, inherent_impact code, residual_likelihood code?, residual_impact code?, confidence code, assumptions text, evidence_ref ID?, assessed_by → UserAccount, reviewed_by → UserAccount?, review_due_on date | Inherent assessment precedes controls. Residual assessment takes only evidenced controls into account. Unknown residual impact remains unknown; it cannot become a green rating. Store separate impact dimensions when the method requires them. |
| RiskControl | id ID, organization_id → Organization, name text, intended_effect text, kind enum(prevent, detect, correct), owner_id → UserAccount, operating_frequency code, test_frequency code, evidence_requirement text, active_from date, valid_until date? | A control may address several risks; an owner may delegate execution. Operational tasks such as an inspection remain with facilities or finance, with an evidence reference returned. |
| RiskControlLink | id ID, risk_id → RiskEntry, control_id → RiskControl, rationale text, from_date date, until_date date? | Many-to-many dated relationship; prevent overlapping duplicate links. |
| ControlTest | id ID, control_id → RiskControl, method text, period_from date, period_until date, sample_basis text, tester_id → UserAccount, tested_at instant?, finding enum(planned, effective, partial, failed, insufficient_evidence), exception_evidence_ref ID?, next_due_on date, reviewer_id → UserAccount? | Distinguish a completed test from a passed test. Material or conflicted controls require a reviewer independent of their operation. |
| RiskTreatment | id ID, risk_id → RiskEntry, strategy enum(reduce, avoid, transfer, accept), proposed_change text, owner_id → UserAccount, due_on date, funding_ref ID?, status enum(proposed, approved, in_progress, evidence_due, verified, declined), completion_ref ID?, verified_by → UserAccount? | Completion must have evidence and an outcome. A verified treatment may trigger reassessment; it must never rewrite the original assessment. |
| RiskAcceptance | id ID, assessment_id → RiskAssessment, approving_body_ref ID, decision_ref ID, rationale text, constraints text?, effective_from date, effective_until date, earlier_review_trigger text?, accepted_by → UserAccount | Time-bound acceptance under delegated authority, including above-appetite exceptions if permitted. Require an escalation when risk exceeds the decision maker's authority. |
| AssuranceFinding | id ID, organization_id → Organization, source_kind enum(control_test, audit, inspection, case_review, exercise), source_ref ID, safe_summary text, severity code, responsible_id → UserAccount, target_on date, status enum(open, remediation, verification, closed, reopened), verification_ref ID? | A preventive action can be reported in aggregate without exposing a protected case or whistleblower. Each affected owner receives only the action and safe context. |

## Cadence, escalation and evidence

At intake, name a cause, event and consequence, scope, owner, assessment interval and decision authority. Facilities hazards, financial errors, continuity, staffing shortages, pastoral confidentiality and supplier interruption can use one common method with suitable categories. A central board may see aggregate material items while operational files remain locally restricted.

After assessment, compare the derived rating with the applicable appetite. Assign treatments and control tests where warranted. Overdue tests show “assurance overdue” even if the prior result was effective. Notify the owner and alternate on review dates, failed tests, expired acceptance, material incidents or changes in scope. An owner cannot accept risk outside their delegation or approve their own undisclosed conflict. Preserve dated appointment and departure handoffs.

Board packs can show inherent/residual ratings, evidence dates, material movements, overdue owners, decisions coming due and unresolved verified actions. Publish only the approved edition. Recalculate comparable trends under the same method or clearly separate periods with different matrices. Low incident counts can reflect reporting patterns; avoid ranking congregations by alleged misconduct or using counts to judge an individual's suitability.

## Acceptance

| Case | Expected result |
|---|---|
| A boiler's maintenance check is overdue while an insurance policy remains in force | Facilities supplies the overdue fact. The control lacks current evidence. Insurance status remains separate. |
| An elder proposes acceptance beyond their financial delegation | Approval routes to the authorized body. The proposal cannot close the risk. |
| A drill discovers that accessible notices are unavailable | A finding names an owner and due date. Closure requires evidence and a reviewer can reopen the finding after a failed retest. |
| A risk matrix changes halfway through a year | Original quarterly reports retain their prior method and rating. A comparison using the new method is labelled as restated. |
