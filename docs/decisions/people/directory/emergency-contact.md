# Emergency contact

[Policy and other cases](README.md)

Test Purpose-limited emergency endpoint in the declared view only. The audience, field, current authority and publication surface all matter. An unrelated field stays at its own decision; other household members do not automatically inherit the change.

| Case | Audience | Basis required | Change at evaluation | Surface | Before | Current | Expected display or delivery |
|---|---|---|---|---|---|---|---|
| DIR-00575 | Self | Own verified record | Shared record becomes protected | Live card | Visible | Hidden | Omit field and navigation hint |
| DIR-00576 | Self | Own verified record | Shared record becomes protected | Expiring download | Visible | Hidden | Deny new retrieval; expire link |
| DIR-00577 | Self | Own verified record | Account suspended | Live card | Visible | Hidden | Omit field and navigation hint |
| DIR-00578 | Self | Own verified record | Account suspended | Expiring download | Visible | Hidden | Deny new retrieval; expire link |
| DIR-00579 | Self | Own verified record | Account restored | Live card | Hidden | Visible | Render approved field |
| DIR-00580 | Self | Own verified record | Account restored | Expiring download | Hidden | Visible | Permit fresh retrieval |
| DIR-00581 | Self | Own verified record | Field correction accepted | Live card | Visible | Visible | Render approved field; corrected value only |
| DIR-00582 | Self | Own verified record | Field correction accepted | Expiring download | Visible | Visible | Permit fresh retrieval; corrected value only |
| DIR-00583 | Verified representative | Current field-scoped delegated access | Grant expires | Live card | Visible | Hidden | Omit field and navigation hint |
| DIR-00584 | Verified representative | Current field-scoped delegated access | Grant expires | Expiring download | Visible | Hidden | Deny new retrieval; expire link |
| DIR-00585 | Verified representative | Current field-scoped delegated access | Scope renewed | Live card | Hidden | Visible | Render approved field |
| DIR-00586 | Verified representative | Current field-scoped delegated access | Scope renewed | Expiring download | Hidden | Visible | Permit fresh retrieval |
| DIR-00587 | Verified representative | Current field-scoped delegated access | Authority contested | Live card | Visible | Hidden | Omit field and navigation hint |
| DIR-00588 | Verified representative | Current field-scoped delegated access | Authority contested | Expiring download | Visible | Hidden | Deny new retrieval; expire link |
| DIR-00589 | Verified representative | Current field-scoped delegated access | Shared record becomes protected | Live card | Visible | Hidden | Omit field and navigation hint |
| DIR-00590 | Verified representative | Current field-scoped delegated access | Shared record becomes protected | Expiring download | Visible | Hidden | Deny new retrieval; expire link |
| DIR-00591 | Verified representative | Current field-scoped delegated access | Field correction accepted | Live card | Visible | Visible | Render approved field; corrected value only |
| DIR-00592 | Verified representative | Current field-scoped delegated access | Field correction accepted | Expiring download | Visible | Visible | Permit fresh retrieval; corrected value only |
| DIR-00593 | Assignment roster | Active assignment and need for field | Assignment ends | Live card | Visible | Hidden | Omit field and navigation hint |
| DIR-00594 | Assignment roster | Active assignment and need for field | Assignment ends | Search hint | Visible | Hidden | Exclude value, match and count hint |
| DIR-00595 | Assignment roster | Active assignment and need for field | Assignment ends | Printed edition | Visible | Hidden | Omit in new print; track existing copies |
| DIR-00596 | Assignment roster | Active assignment and need for field | Assignment ends | Expiring download | Visible | Hidden | Deny new retrieval; expire link |
| DIR-00597 | Assignment roster | Active assignment and need for field | Duty narrowed | Live card | Visible | Hidden | Omit field and navigation hint |
| DIR-00598 | Assignment roster | Active assignment and need for field | Duty narrowed | Search hint | Visible | Hidden | Exclude value, match and count hint |
| DIR-00599 | Assignment roster | Active assignment and need for field | Duty narrowed | Printed edition | Visible | Hidden | Omit in new print; track existing copies |
| DIR-00600 | Assignment roster | Active assignment and need for field | Duty narrowed | Expiring download | Visible | Hidden | Deny new retrieval; expire link |
| DIR-00601 | Assignment roster | Active assignment and need for field | New duty confirmed | Live card | Hidden | Visible | Render approved field |
| DIR-00602 | Assignment roster | Active assignment and need for field | New duty confirmed | Search hint | Hidden | Visible | Match via permitted field only |
| DIR-00603 | Assignment roster | Active assignment and need for field | New duty confirmed | Printed edition | Hidden | Visible | Include in new edition; older edition unchanged |
| DIR-00604 | Assignment roster | Active assignment and need for field | New duty confirmed | Expiring download | Hidden | Visible | Permit fresh retrieval |
| DIR-00605 | Assignment roster | Active assignment and need for field | Shared record becomes protected | Live card | Visible | Hidden | Omit field and navigation hint |
| DIR-00606 | Assignment roster | Active assignment and need for field | Shared record becomes protected | Search hint | Visible | Hidden | Exclude value, match and count hint |
| DIR-00607 | Assignment roster | Active assignment and need for field | Shared record becomes protected | Printed edition | Visible | Hidden | Omit in new print; track existing copies |
| DIR-00608 | Assignment roster | Active assignment and need for field | Shared record becomes protected | Expiring download | Visible | Hidden | Deny new retrieval; expire link |
