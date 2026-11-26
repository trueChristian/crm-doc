# Birthday without year

[Policy and other cases](README.md)

Test Month and day only in the declared view only. The audience, field, current authority and publication surface all matter. An unrelated field stays at its own decision; other household members do not automatically inherit the change.

| Case | Audience | Basis required | Change at evaluation | Surface | Before | Current | Expected display or delivery |
|---|---|---|---|---|---|---|---|
| DIR-00100 | Self | Own verified record | Shared record becomes protected | Live card | Visible | Hidden | Omit field and navigation hint |
| DIR-00101 | Self | Own verified record | Shared record becomes protected | Printed edition | Visible | Hidden | Omit in new print; track existing copies |
| DIR-00102 | Self | Own verified record | Shared record becomes protected | Expiring download | Visible | Hidden | Deny new retrieval; expire link |
| DIR-00103 | Self | Own verified record | Account suspended | Live card | Visible | Hidden | Omit field and navigation hint |
| DIR-00104 | Self | Own verified record | Account suspended | Printed edition | Visible | Hidden | Omit in new print; track existing copies |
| DIR-00105 | Self | Own verified record | Account suspended | Expiring download | Visible | Hidden | Deny new retrieval; expire link |
| DIR-00106 | Self | Own verified record | Account restored | Live card | Hidden | Visible | Render approved field |
| DIR-00107 | Self | Own verified record | Account restored | Printed edition | Hidden | Visible | Include in new edition; older edition unchanged |
| DIR-00108 | Self | Own verified record | Account restored | Expiring download | Hidden | Visible | Permit fresh retrieval |
| DIR-00109 | Self | Own verified record | Field correction accepted | Live card | Visible | Visible | Render approved field; corrected value only |
| DIR-00110 | Self | Own verified record | Field correction accepted | Printed edition | Visible | Visible | Include in new edition; corrected value only |
| DIR-00111 | Self | Own verified record | Field correction accepted | Expiring download | Visible | Visible | Permit fresh retrieval; corrected value only |
| DIR-00112 | Verified representative | Current field-scoped delegated access | Grant expires | Live card | Visible | Hidden | Omit field and navigation hint |
| DIR-00113 | Verified representative | Current field-scoped delegated access | Grant expires | Printed edition | Visible | Hidden | Omit in new print; track existing copies |
| DIR-00114 | Verified representative | Current field-scoped delegated access | Grant expires | Expiring download | Visible | Hidden | Deny new retrieval; expire link |
| DIR-00115 | Verified representative | Current field-scoped delegated access | Scope renewed | Live card | Hidden | Visible | Render approved field |
| DIR-00116 | Verified representative | Current field-scoped delegated access | Scope renewed | Printed edition | Hidden | Visible | Include in new edition; older edition unchanged |
| DIR-00117 | Verified representative | Current field-scoped delegated access | Scope renewed | Expiring download | Hidden | Visible | Permit fresh retrieval |
| DIR-00118 | Verified representative | Current field-scoped delegated access | Authority contested | Live card | Visible | Hidden | Omit field and navigation hint |
| DIR-00119 | Verified representative | Current field-scoped delegated access | Authority contested | Printed edition | Visible | Hidden | Omit in new print; track existing copies |
| DIR-00120 | Verified representative | Current field-scoped delegated access | Authority contested | Expiring download | Visible | Hidden | Deny new retrieval; expire link |
| DIR-00121 | Verified representative | Current field-scoped delegated access | Shared record becomes protected | Live card | Visible | Hidden | Omit field and navigation hint |
| DIR-00122 | Verified representative | Current field-scoped delegated access | Shared record becomes protected | Printed edition | Visible | Hidden | Omit in new print; track existing copies |
| DIR-00123 | Verified representative | Current field-scoped delegated access | Shared record becomes protected | Expiring download | Visible | Hidden | Deny new retrieval; expire link |
| DIR-00124 | Verified representative | Current field-scoped delegated access | Field correction accepted | Live card | Visible | Visible | Render approved field; corrected value only |
| DIR-00125 | Verified representative | Current field-scoped delegated access | Field correction accepted | Printed edition | Visible | Visible | Include in new edition; corrected value only |
| DIR-00126 | Verified representative | Current field-scoped delegated access | Field correction accepted | Expiring download | Visible | Visible | Permit fresh retrieval; corrected value only |
| DIR-00127 | Church directory | Eligible person and field-specific audience opt-in | Audience opt-in withdrawn | Live card | Visible | Hidden | Omit field and navigation hint |
| DIR-00128 | Church directory | Eligible person and field-specific audience opt-in | Audience opt-in withdrawn | Search hint | Visible | Hidden | Exclude value, match and count hint |
| DIR-00129 | Church directory | Eligible person and field-specific audience opt-in | Audience opt-in withdrawn | Printed edition | Visible | Hidden | Omit in new print; track existing copies |
| DIR-00130 | Church directory | Eligible person and field-specific audience opt-in | Audience opt-in withdrawn | Expiring download | Visible | Hidden | Deny new retrieval; expire link |
| DIR-00131 | Church directory | Eligible person and field-specific audience opt-in | Membership eligibility ends | Live card | Visible | Hidden | Omit field and navigation hint |
| DIR-00132 | Church directory | Eligible person and field-specific audience opt-in | Membership eligibility ends | Search hint | Visible | Hidden | Exclude value, match and count hint |
| DIR-00133 | Church directory | Eligible person and field-specific audience opt-in | Membership eligibility ends | Printed edition | Visible | Hidden | Omit in new print; track existing copies |
| DIR-00134 | Church directory | Eligible person and field-specific audience opt-in | Membership eligibility ends | Expiring download | Visible | Hidden | Deny new retrieval; expire link |
| DIR-00135 | Church directory | Eligible person and field-specific audience opt-in | Audience changes | Live card | Visible | Hidden | Omit field and navigation hint |
| DIR-00136 | Church directory | Eligible person and field-specific audience opt-in | Audience changes | Search hint | Visible | Hidden | Exclude value, match and count hint |
| DIR-00137 | Church directory | Eligible person and field-specific audience opt-in | Audience changes | Printed edition | Visible | Hidden | Omit in new print; track existing copies |
| DIR-00138 | Church directory | Eligible person and field-specific audience opt-in | Audience changes | Expiring download | Visible | Hidden | Deny new retrieval; expire link |
| DIR-00139 | Church directory | Eligible person and field-specific audience opt-in | Protection removed after review | Live card | Hidden | Visible | Render approved field |
| DIR-00140 | Church directory | Eligible person and field-specific audience opt-in | Protection removed after review | Search hint | Hidden | Visible | Match via permitted field only |
| DIR-00141 | Church directory | Eligible person and field-specific audience opt-in | Protection removed after review | Printed edition | Hidden | Visible | Include in new edition; older edition unchanged |
| DIR-00142 | Church directory | Eligible person and field-specific audience opt-in | Protection removed after review | Expiring download | Hidden | Visible | Permit fresh retrieval |
| DIR-00143 | Church directory | Eligible person and field-specific audience opt-in | Field correction accepted | Live card | Visible | Visible | Render approved field; corrected value only |
| DIR-00144 | Church directory | Eligible person and field-specific audience opt-in | Field correction accepted | Search hint | Visible | Visible | Match via permitted field only; corrected value only |
| DIR-00145 | Church directory | Eligible person and field-specific audience opt-in | Field correction accepted | Printed edition | Visible | Visible | Include in new edition; corrected value only |
| DIR-00146 | Church directory | Eligible person and field-specific audience opt-in | Field correction accepted | Expiring download | Visible | Visible | Permit fresh retrieval; corrected value only |
| DIR-00147 | Public listing | Eligible person and field-specific audience opt-in | Audience opt-in withdrawn | Live card | Visible | Hidden | Omit field and navigation hint |
| DIR-00148 | Public listing | Eligible person and field-specific audience opt-in | Audience opt-in withdrawn | Search hint | Visible | Hidden | Exclude value, match and count hint |
| DIR-00149 | Public listing | Eligible person and field-specific audience opt-in | Audience opt-in withdrawn | Printed edition | Visible | Hidden | Omit in new print; track existing copies |
| DIR-00150 | Public listing | Eligible person and field-specific audience opt-in | Audience opt-in withdrawn | Expiring download | Visible | Hidden | Deny new retrieval; expire link |
| DIR-00151 | Public listing | Eligible person and field-specific audience opt-in | Membership eligibility ends | Live card | Visible | Hidden | Omit field and navigation hint |
| DIR-00152 | Public listing | Eligible person and field-specific audience opt-in | Membership eligibility ends | Search hint | Visible | Hidden | Exclude value, match and count hint |
| DIR-00153 | Public listing | Eligible person and field-specific audience opt-in | Membership eligibility ends | Printed edition | Visible | Hidden | Omit in new print; track existing copies |
| DIR-00154 | Public listing | Eligible person and field-specific audience opt-in | Membership eligibility ends | Expiring download | Visible | Hidden | Deny new retrieval; expire link |
| DIR-00155 | Public listing | Eligible person and field-specific audience opt-in | Audience changes | Live card | Visible | Hidden | Omit field and navigation hint |
| DIR-00156 | Public listing | Eligible person and field-specific audience opt-in | Audience changes | Search hint | Visible | Hidden | Exclude value, match and count hint |
| DIR-00157 | Public listing | Eligible person and field-specific audience opt-in | Audience changes | Printed edition | Visible | Hidden | Omit in new print; track existing copies |
| DIR-00158 | Public listing | Eligible person and field-specific audience opt-in | Audience changes | Expiring download | Visible | Hidden | Deny new retrieval; expire link |
| DIR-00159 | Public listing | Eligible person and field-specific audience opt-in | Protection removed after review | Live card | Hidden | Visible | Render approved field |
| DIR-00160 | Public listing | Eligible person and field-specific audience opt-in | Protection removed after review | Search hint | Hidden | Visible | Match via permitted field only |
| DIR-00161 | Public listing | Eligible person and field-specific audience opt-in | Protection removed after review | Printed edition | Hidden | Visible | Include in new edition; older edition unchanged |
| DIR-00162 | Public listing | Eligible person and field-specific audience opt-in | Protection removed after review | Expiring download | Hidden | Visible | Permit fresh retrieval |
| DIR-00163 | Public listing | Eligible person and field-specific audience opt-in | Field correction accepted | Live card | Visible | Visible | Render approved field; corrected value only |
| DIR-00164 | Public listing | Eligible person and field-specific audience opt-in | Field correction accepted | Search hint | Visible | Visible | Match via permitted field only; corrected value only |
| DIR-00165 | Public listing | Eligible person and field-specific audience opt-in | Field correction accepted | Printed edition | Visible | Visible | Include in new edition; corrected value only |
| DIR-00166 | Public listing | Eligible person and field-specific audience opt-in | Field correction accepted | Expiring download | Visible | Visible | Permit fresh retrieval; corrected value only |
| DIR-00167 | Assignment roster | Active assignment and need for field | Assignment ends | Live card | Visible | Hidden | Omit field and navigation hint |
| DIR-00168 | Assignment roster | Active assignment and need for field | Assignment ends | Search hint | Visible | Hidden | Exclude value, match and count hint |
| DIR-00169 | Assignment roster | Active assignment and need for field | Assignment ends | Printed edition | Visible | Hidden | Omit in new print; track existing copies |
| DIR-00170 | Assignment roster | Active assignment and need for field | Assignment ends | Expiring download | Visible | Hidden | Deny new retrieval; expire link |
| DIR-00171 | Assignment roster | Active assignment and need for field | Duty narrowed | Live card | Visible | Hidden | Omit field and navigation hint |
| DIR-00172 | Assignment roster | Active assignment and need for field | Duty narrowed | Search hint | Visible | Hidden | Exclude value, match and count hint |
| DIR-00173 | Assignment roster | Active assignment and need for field | Duty narrowed | Printed edition | Visible | Hidden | Omit in new print; track existing copies |
| DIR-00174 | Assignment roster | Active assignment and need for field | Duty narrowed | Expiring download | Visible | Hidden | Deny new retrieval; expire link |
| DIR-00175 | Assignment roster | Active assignment and need for field | New duty confirmed | Live card | Hidden | Visible | Render approved field |
| DIR-00176 | Assignment roster | Active assignment and need for field | New duty confirmed | Search hint | Hidden | Visible | Match via permitted field only |
| DIR-00177 | Assignment roster | Active assignment and need for field | New duty confirmed | Printed edition | Hidden | Visible | Include in new edition; older edition unchanged |
| DIR-00178 | Assignment roster | Active assignment and need for field | New duty confirmed | Expiring download | Hidden | Visible | Permit fresh retrieval |
| DIR-00179 | Assignment roster | Active assignment and need for field | Shared record becomes protected | Live card | Visible | Hidden | Omit field and navigation hint |
| DIR-00180 | Assignment roster | Active assignment and need for field | Shared record becomes protected | Search hint | Visible | Hidden | Exclude value, match and count hint |
| DIR-00181 | Assignment roster | Active assignment and need for field | Shared record becomes protected | Printed edition | Visible | Hidden | Omit in new print; track existing copies |
| DIR-00182 | Assignment roster | Active assignment and need for field | Shared record becomes protected | Expiring download | Visible | Hidden | Deny new retrieval; expire link |
| DIR-00183 | Household member | Individually approved household field | Separate household formed | Live card | Visible | Hidden | Omit field and navigation hint |
| DIR-00184 | Household member | Individually approved household field | Separate household formed | Search hint | Visible | Hidden | Exclude value, match and count hint |
| DIR-00185 | Household member | Individually approved household field | Separate household formed | Printed edition | Visible | Hidden | Omit in new print; track existing copies |
| DIR-00186 | Household member | Individually approved household field | Separate household formed | Expiring download | Visible | Hidden | Deny new retrieval; expire link |
| DIR-00187 | Household member | Individually approved household field | Household consent withdrawn | Live card | Visible | Hidden | Omit field and navigation hint |
| DIR-00188 | Household member | Individually approved household field | Household consent withdrawn | Search hint | Visible | Hidden | Exclude value, match and count hint |
| DIR-00189 | Household member | Individually approved household field | Household consent withdrawn | Printed edition | Visible | Hidden | Omit in new print; track existing copies |
| DIR-00190 | Household member | Individually approved household field | Household consent withdrawn | Expiring download | Visible | Hidden | Deny new retrieval; expire link |
| DIR-00191 | Household member | Individually approved household field | Household consent granted | Live card | Hidden | Visible | Render approved field |
| DIR-00192 | Household member | Individually approved household field | Household consent granted | Search hint | Hidden | Visible | Match via permitted field only |
| DIR-00193 | Household member | Individually approved household field | Household consent granted | Printed edition | Hidden | Visible | Include in new edition; older edition unchanged |
| DIR-00194 | Household member | Individually approved household field | Household consent granted | Expiring download | Hidden | Visible | Permit fresh retrieval |
| DIR-00195 | Household member | Individually approved household field | Shared record becomes protected | Live card | Visible | Hidden | Omit field and navigation hint |
| DIR-00196 | Household member | Individually approved household field | Shared record becomes protected | Search hint | Visible | Hidden | Exclude value, match and count hint |
| DIR-00197 | Household member | Individually approved household field | Shared record becomes protected | Printed edition | Visible | Hidden | Omit in new print; track existing copies |
| DIR-00198 | Household member | Individually approved household field | Shared record becomes protected | Expiring download | Visible | Hidden | Deny new retrieval; expire link |
