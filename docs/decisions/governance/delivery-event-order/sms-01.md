# SMS delivery and unknown handoff reconciliation · 1 of 2

[Decision profiles](../README.md) · [Method and other cases](README.md) · [Clerk procedure](../../../handbook/governance/delivery-incident-desk.md)

**Given.** Five observations arrive consecutively at 09:00, 09:01, 09:02, 09:03 and 09:04 UTC for one already submitted route. D and D2 repeat the same verified delivery event. F is a definitive failure incompatible with a delivered event for this same destination. X is a wrong-sender callback. T records the local timeout. K is a reconciliation lookup with no new delivery information. A is provider acceptance (for channel, confirmed publication).

Use the row inputs with this profile. Compare every expected output at the indicated cutoff. Case numbers are local to this profile.

| Case | Arrival order | Trace | Duplicate observations | Quarantined | Future route | Final status | Post views observed | Confirmed people |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| SMS-0001 | T → A → D → D2 → F | u a d d r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0002 | T → A → D → F → D2 | u a d r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0003 | T → A → D → X → F | u a d Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0004 | T → A → D → K → F | u a d d r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0005 | T → A → D2 → D → K | u a d d d | 1 | 0 | as previously permitted | delivered | — | 1 |
| SMS-0006 | T → A → D2 → F → K | u a d r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0007 | T → A → D2 → K → D | u a d d d | 1 | 0 | as previously permitted | delivered | — | 1 |
| SMS-0008 | T → A → F → D → D2 | u a f r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0009 | T → A → F → D2 → X | u a f r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0010 | T → A → F → X → D2 | u a f Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0011 | T → A → F → K → X | u a f f Q | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0012 | T → A → X → D → K | u a Q d d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0013 | T → A → X → F → D | u a Q f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0014 | T → A → X → K → D2 | u a Q a d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0015 | T → A → K → D → F | u a a d r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0016 | T → A → K → D2 → X | u a a d Q | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0017 | T → A → K → F → X | u a a f Q | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0018 | T → D → A → D2 → F | u d d d r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0019 | T → D → A → F → D2 | u d d r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0020 | T → D → A → X → F | u d d Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0021 | T → D → A → K → F | u d d d r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0022 | T → D → D2 → A → K | u d d d d | 1 | 0 | as previously permitted | delivered | — | 1 |
| SMS-0023 | T → D → D2 → F → K | u d d r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0024 | T → D → D2 → K → A | u d d d d | 1 | 0 | as previously permitted | delivered | — | 1 |
| SMS-0025 | T → D → F → A → X | u d r r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0026 | T → D → F → D2 → X | u d r r Q | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0027 | T → D → F → X → K | u d r Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0028 | T → D → F → K → X | u d r r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0029 | T → D → X → D2 → A | u d Q d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0030 | T → D → X → F → A | u d Q r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0031 | T → D → X → K → D2 | u d Q d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0032 | T → D → K → A → F | u d d d r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0033 | T → D → K → D2 → X | u d d d Q | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0034 | T → D → K → F → X | u d d r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0035 | T → D2 → A → D → F | u d d d r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0036 | T → D2 → A → F → X | u d d r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0037 | T → D2 → A → X → F | u d d Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0038 | T → D2 → A → K → X | u d d d Q | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0039 | T → D2 → D → A → K | u d d d d | 1 | 0 | as previously permitted | delivered | — | 1 |
| SMS-0040 | T → D2 → D → X → A | u d d Q d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0041 | T → D2 → D → K → A | u d d d d | 1 | 0 | as previously permitted | delivered | — | 1 |
| SMS-0042 | T → D2 → F → A → X | u d r r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0043 | T → D2 → F → D → X | u d r r Q | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0044 | T → D2 → F → X → K | u d r Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0045 | T → D2 → F → K → X | u d r r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0046 | T → D2 → X → D → A | u d Q d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0047 | T → D2 → X → F → D | u d Q r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0048 | T → D2 → X → K → D | u d Q d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0049 | T → D2 → K → A → X | u d d d Q | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0050 | T → D2 → K → D → X | u d d d Q | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0051 | T → D2 → K → X → A | u d d Q d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0052 | T → F → A → D → D2 | u f f r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0053 | T → F → A → D2 → X | u f f r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0054 | T → F → A → X → D2 | u f f Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0055 | T → F → A → K → X | u f f f Q | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0056 | T → F → D → A → K | u f r r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0057 | T → F → D → X → A | u f r Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0058 | T → F → D → K → D2 | u f r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0059 | T → F → D2 → A → X | u f r r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0060 | T → F → D2 → D → K | u f r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0061 | T → F → D2 → X → K | u f r Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0062 | T → F → X → A → D | u f Q f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0063 | T → F → X → D → A | u f Q r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0064 | T → F → X → D2 → D | u f Q r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0065 | T → F → X → K → D | u f Q f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0066 | T → F → K → A → X | u f f f Q | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0067 | T → F → K → D → X | u f f r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0068 | T → F → K → X → A | u f f Q f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0069 | T → X → A → D → F | u Q a d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0070 | T → X → A → D2 → F | u Q a d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0071 | T → X → A → F → K | u Q a f f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0072 | T → X → A → K → F | u Q a a f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0073 | T → X → D → D2 → A | u Q d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0074 | T → X → D → F → A | u Q d r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0075 | T → X → D → K → D2 | u Q d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0076 | T → X → D2 → A → F | u Q d d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0077 | T → X → D2 → D → K | u Q d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0078 | T → X → D2 → F → K | u Q d r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0079 | T → X → F → A → D | u Q f f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0080 | T → X → F → D → D2 | u Q f r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0081 | T → X → F → D2 → D | u Q f r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0082 | T → X → F → K → D2 | u Q f f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0083 | T → X → K → A → F | u Q u a f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0084 | T → X → K → D2 → A | u Q u d d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0085 | T → X → K → F → A | u Q u f f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0086 | T → K → A → D → F | u u a d r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0087 | T → K → A → D2 → F | u u a d r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0088 | T → K → A → F → X | u u a f Q | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0089 | T → K → A → X → F | u u a Q f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0090 | T → K → D → D2 → A | u u d d d | 1 | 0 | as previously permitted | delivered | — | 1 |
| SMS-0091 | T → K → D → F → D2 | u u d r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0092 | T → K → D → X → D2 | u u d Q d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0093 | T → K → D2 → A → X | u u d d Q | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0094 | T → K → D2 → D → X | u u d d Q | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0095 | T → K → D2 → X → A | u u d Q d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0096 | T → K → F → A → D | u u f f r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0097 | T → K → F → D → D2 | u u f r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0098 | T → K → F → D2 → D | u u f r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0099 | T → K → F → X → D2 | u u f Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0100 | T → K → X → A → F | u u Q a f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0101 | T → K → X → D2 → A | u u Q d d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0102 | T → K → X → F → D | u u Q f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0103 | A → T → D → D2 → X | a a d d Q | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0104 | A → T → D → F → K | a a d r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0105 | A → T → D → X → K | a a d Q d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0106 | A → T → D2 → D → F | a a d d r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0107 | A → T → D2 → F → D | a a d r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0108 | A → T → D2 → X → F | a a d Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0109 | A → T → D2 → K → F | a a d d r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0110 | A → T → F → D → K | a a f r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0111 | A → T → F → D2 → K | a a f r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0112 | A → T → F → K → D | a a f f r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0113 | A → T → X → D → F | a a Q d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0114 | A → T → X → D2 → F | a a Q d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0115 | A → T → X → F → K | a a Q f f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0116 | A → T → X → K → F | a a Q a f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0117 | A → T → K → D2 → D | a a a d d | 1 | 0 | as previously permitted | delivered | — | 1 |
| SMS-0118 | A → T → K → F → D | a a a f r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0119 | A → T → K → X → D2 | a a a Q d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0120 | A → D → T → D2 → X | a d d d Q | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0121 | A → D → T → F → K | a d d r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0122 | A → D → T → X → K | a d d Q d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0123 | A → D → D2 → T → F | a d d d r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0124 | A → D → D2 → F → X | a d d r Q | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0125 | A → D → D2 → X → F | a d d Q r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0126 | A → D → D2 → K → X | a d d d Q | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0127 | A → D → F → T → K | a d r r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0128 | A → D → F → X → T | a d r Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0129 | A → D → F → K → T | a d r r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0130 | A → D → X → T → F | a d Q d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0131 | A → D → X → D2 → F | a d Q d r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0132 | A → D → X → F → K | a d Q r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0133 | A → D → X → K → F | a d Q d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0134 | A → D → K → D2 → T | a d d d d | 1 | 0 | as previously permitted | delivered | — | 1 |
| SMS-0135 | A → D → K → F → D2 | a d d r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0136 | A → D → K → X → D2 | a d d Q d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0137 | A → D2 → T → D → K | a d d d d | 1 | 0 | as previously permitted | delivered | — | 1 |
| SMS-0138 | A → D2 → T → F → K | a d d r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0139 | A → D2 → T → K → D | a d d d d | 1 | 0 | as previously permitted | delivered | — | 1 |
| SMS-0140 | A → D2 → D → T → F | a d d d r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0141 | A → D2 → D → F → X | a d d r Q | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0142 | A → D2 → D → X → F | a d d Q r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0143 | A → D2 → D → K → X | a d d d Q | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0144 | A → D2 → F → T → K | a d r r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0145 | A → D2 → F → X → T | a d r Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0146 | A → D2 → F → K → D | a d r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0147 | A → D2 → X → T → F | a d Q d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0148 | A → D2 → X → D → K | a d Q d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0149 | A → D2 → X → F → K | a d Q r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0150 | A → D2 → K → T → D | a d d d d | 1 | 0 | as previously permitted | delivered | — | 1 |
| SMS-0151 | A → D2 → K → D → T | a d d d d | 1 | 0 | as previously permitted | delivered | — | 1 |
| SMS-0152 | A → D2 → K → F → D | a d d r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0153 | A → D2 → K → X → D | a d d Q d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0154 | A → F → T → D → K | a f f r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0155 | A → F → T → D2 → K | a f f r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0156 | A → F → T → K → D | a f f f r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0157 | A → F → D → T → X | a f r r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0158 | A → F → D → D2 → X | a f r r Q | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0159 | A → F → D → X → K | a f r Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0160 | A → F → D → K → X | a f r r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0161 | A → F → D2 → D → T | a f r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0162 | A → F → D2 → X → T | a f r Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0163 | A → F → D2 → K → D | a f r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0164 | A → F → X → T → D2 | a f Q f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0165 | A → F → X → D → K | a f Q r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0166 | A → F → X → D2 → K | a f Q r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0167 | A → F → K → T → D | a f f f r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0168 | A → F → K → D → D2 | a f f r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0169 | A → F → K → D2 → D | a f f r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0170 | A → F → K → X → D2 | a f f Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0171 | A → X → T → D → K | a Q a d d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0172 | A → X → T → F → D | a Q a f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0173 | A → X → T → K → D | a Q a a d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0174 | A → X → D → T → F | a Q d d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0175 | A → X → D → D2 → F | a Q d d r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0176 | A → X → D → F → K | a Q d r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0177 | A → X → D → K → F | a Q d d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0178 | A → X → D2 → D → T | a Q d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0179 | A → X → D2 → F → D | a Q d r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0180 | A → X → D2 → K → D | a Q d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0181 | A → X → F → T → K | a Q f f f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0182 | A → X → F → D → K | a Q f r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0183 | A → X → F → K → T | a Q f f f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0184 | A → X → K → T → D | a Q a a d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0185 | A → X → K → D → D2 | a Q a d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0186 | A → X → K → D2 → D | a Q a d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0187 | A → X → K → F → D2 | a Q a f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0188 | A → K → T → D → X | a a a d Q | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0189 | A → K → T → F → D | a a a f r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0190 | A → K → T → X → D2 | a a a Q d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0191 | A → K → D → T → F | a a d d r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0192 | A → K → D → D2 → X | a a d d Q | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0193 | A → K → D → F → X | a a d r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0194 | A → K → D2 → T → D | a a d d d | 1 | 0 | as previously permitted | delivered | — | 1 |
| SMS-0195 | A → K → D2 → D → T | a a d d d | 1 | 0 | as previously permitted | delivered | — | 1 |
| SMS-0196 | A → K → D2 → F → D | a a d r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0197 | A → K → D2 → X → D | a a d Q d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0198 | A → K → F → T → X | a a f f Q | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0199 | A → K → F → D → X | a a f r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0200 | A → K → F → X → T | a a f Q f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0201 | A → K → X → T → D2 | a a Q a d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0202 | A → K → X → D → D2 | a a Q d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0203 | A → K → X → D2 → F | a a Q d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0204 | A → K → X → F → D2 | a a Q f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0205 | D → T → A → F → D2 | d d d r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0206 | D → T → A → X → D2 | d d d Q d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0207 | D → T → A → K → F | d d d d r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0208 | D → T → D2 → A → X | d d d d Q | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0209 | D → T → D2 → F → K | d d d r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0210 | D → T → D2 → X → K | d d d Q d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0211 | D → T → F → A → D2 | d d r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0212 | D → T → F → D2 → X | d d r r Q | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0213 | D → T → F → X → D2 | d d r Q r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0214 | D → T → F → K → X | d d r r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0215 | D → T → X → A → K | d d Q d d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0216 | D → T → X → F → A | d d Q r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0217 | D → T → X → K → A | d d Q d d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0218 | D → T → K → A → F | d d d d r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0219 | D → T → K → D2 → F | d d d d r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0220 | D → T → K → F → X | d d d r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0221 | D → T → K → X → F | d d d Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0222 | D → A → T → F → D2 | d d d r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0223 | D → A → T → X → F | d d d Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0224 | D → A → T → K → F | d d d d r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0225 | D → A → D2 → T → K | d d d d d | 1 | 0 | as previously permitted | delivered | — | 1 |
| SMS-0226 | D → A → D2 → F → K | d d d r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0227 | D → A → D2 → K → T | d d d d d | 1 | 0 | as previously permitted | delivered | — | 1 |
| SMS-0228 | D → A → F → T → D2 | d d r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0229 | D → A → F → D2 → X | d d r r Q | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0230 | D → A → F → X → D2 | d d r Q r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0231 | D → A → F → K → X | d d r r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0232 | D → A → X → T → K | d d Q d d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0233 | D → A → X → F → T | d d Q r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0234 | D → A → X → K → D2 | d d Q d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0235 | D → A → K → T → F | d d d d r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0236 | D → A → K → D2 → X | d d d d Q | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0237 | D → A → K → F → X | d d d r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0238 | D → D2 → T → A → F | d d d d r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0239 | D → D2 → T → F → A | d d d r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0240 | D → D2 → T → X → F | d d d Q r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0241 | D → D2 → T → K → F | d d d d r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0242 | D → D2 → A → T → K | d d d d d | 1 | 0 | as previously permitted | delivered | — | 1 |
| SMS-0243 | D → D2 → A → F → K | d d d r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0244 | D → D2 → A → K → T | d d d d d | 1 | 0 | as previously permitted | delivered | — | 1 |
| SMS-0245 | D → D2 → F → T → X | d d r r Q | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0246 | D → D2 → F → A → X | d d r r Q | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0247 | D → D2 → F → X → K | d d r Q r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0248 | D → D2 → F → K → X | d d r r Q | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0249 | D → D2 → X → A → T | d d Q d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0250 | D → D2 → X → F → T | d d Q r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0251 | D → D2 → X → K → A | d d Q d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0252 | D → D2 → K → T → F | d d d d r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0253 | D → D2 → K → A → X | d d d d Q | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0254 | D → D2 → K → F → X | d d d r Q | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0255 | D → F → T → A → D2 | d r r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0256 | D → F → T → D2 → X | d r r r Q | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0257 | D → F → T → X → D2 | d r r Q r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0258 | D → F → T → K → X | d r r r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0259 | D → F → A → T → K | d r r r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0260 | D → F → A → X → T | d r r Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0261 | D → F → A → K → T | d r r r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0262 | D → F → D2 → T → X | d r r r Q | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0263 | D → F → D2 → A → X | d r r r Q | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0264 | D → F → D2 → X → K | d r r Q r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0265 | D → F → D2 → K → X | d r r r Q | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0266 | D → F → X → A → T | d r Q r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0267 | D → F → X → D2 → A | d r Q r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0268 | D → F → X → K → A | d r Q r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0269 | D → F → K → T → X | d r r r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0270 | D → F → K → A → X | d r r r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0271 | D → F → K → X → T | d r r Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0272 | D → X → T → A → D2 | d Q d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0273 | D → X → T → D2 → F | d Q d d r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0274 | D → X → T → F → D2 | d Q d r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0275 | D → X → T → K → F | d Q d d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0276 | D → X → A → T → K | d Q d d d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0277 | D → X → A → F → T | d Q d r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0278 | D → X → A → K → D2 | d Q d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0279 | D → X → D2 → T → F | d Q d d r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0280 | D → X → D2 → A → K | d Q d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0281 | D → X → D2 → F → K | d Q d r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0282 | D → X → F → T → A | d Q r r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0283 | D → X → F → A → T | d Q r r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0284 | D → X → F → D2 → A | d Q r r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0285 | D → X → F → K → A | d Q r r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0286 | D → X → K → T → F | d Q d d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0287 | D → X → K → A → F | d Q d d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0288 | D → X → K → F → T | d Q d r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0289 | D → K → T → A → F | d d d d r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0290 | D → K → T → D2 → F | d d d d r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0291 | D → K → T → F → X | d d d r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0292 | D → K → T → X → F | d d d Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0293 | D → K → A → D2 → T | d d d d d | 1 | 0 | as previously permitted | delivered | — | 1 |
| SMS-0294 | D → K → A → F → T | d d d r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0295 | D → K → A → X → D2 | d d d Q d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0296 | D → K → D2 → T → F | d d d d r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0297 | D → K → D2 → A → X | d d d d Q | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0298 | D → K → D2 → F → X | d d d r Q | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0299 | D → K → F → T → A | d d r r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0300 | D → K → F → A → D2 | d d r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0301 | D → K → F → D2 → A | d d r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0302 | D → K → F → X → D2 | d d r Q r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0303 | D → K → X → T → F | d d Q d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0304 | D → K → X → D2 → T | d d Q d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0305 | D → K → X → F → T | d d Q r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0306 | D2 → T → A → D → X | d d d d Q | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0307 | D2 → T → A → F → X | d d d r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0308 | D2 → T → A → X → K | d d d Q d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0309 | D2 → T → A → K → X | d d d d Q | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0310 | D2 → T → D → F → A | d d d r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0311 | D2 → T → D → X → A | d d d Q d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0312 | D2 → T → D → K → F | d d d d r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0313 | D2 → T → F → A → K | d d r r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0314 | D2 → T → F → D → K | d d r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0315 | D2 → T → F → K → A | d d r r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0316 | D2 → T → X → A → D | d d Q d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0317 | D2 → T → X → D → F | d d Q d r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0318 | D2 → T → X → F → D | d d Q r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0319 | D2 → T → X → K → F | d d Q d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0320 | D2 → T → K → A → X | d d d d Q | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0321 | D2 → T → K → F → A | d d d r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0322 | D2 → T → K → X → A | d d d Q d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0323 | D2 → A → T → D → X | d d d d Q | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0324 | D2 → A → T → F → K | d d d r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0325 | D2 → A → T → X → K | d d d Q d | 0 | 1 | as previously permitted | delivered | — | 1 |
