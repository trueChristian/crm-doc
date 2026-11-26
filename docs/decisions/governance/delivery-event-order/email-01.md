# Email bounce and unsubscribe evidence · 1 of 2

[Decision profiles](../README.md) · [Method and other cases](README.md) · [Clerk procedure](../../../handbook/governance/delivery-incident-desk.md)

**Given.** Five observations arrive consecutively at 09:00, 09:01, 09:02, 09:03 and 09:04 UTC for one already submitted route. B is a final non-delivery bounce from this adapter. U is a verified unsubscribe for future optional traffic. D is verified final delivery to the same endpoint; a contradictory bounce needs review. X is a wrong-sender callback. T records the local timeout. K is a reconciliation lookup with no new delivery information. A is provider acceptance (for channel, confirmed publication).

Use the row inputs with this profile. Compare every expected output at the indicated cutoff. Case numbers are local to this profile.

| Case | Arrival order | Trace | Duplicate observations | Quarantined | Future route | Final status | Post views observed | Confirmed people |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| EMAIL-0001 | T → A → D → B → U | u a d r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0002 | T → A → D → U → B | u a d d r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0003 | T → A → D → X → U | u a d Q d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0004 | T → A → D → K → U | u a d d d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0005 | T → A → B → D → K | u a f r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0006 | T → A → B → U → K | u a f f f | 0 | 0 | future optional suppressed | failed | — | 0 |
| EMAIL-0007 | T → A → B → K → D | u a f f r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0008 | T → A → U → D → B | u a a d r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0009 | T → A → U → B → X | u a a f Q | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0010 | T → A → U → X → B | u a a Q f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0011 | T → A → U → K → X | u a a a Q | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0012 | T → A → X → D → K | u a Q d d | 0 | 1 | as previously permitted | delivered | — | 1 |
| EMAIL-0013 | T → A → X → U → D | u a Q a d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0014 | T → A → X → K → B | u a Q a f | 0 | 1 | as previously permitted | failed | — | 0 |
| EMAIL-0015 | T → A → K → D → U | u a a d d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0016 | T → A → K → B → X | u a a f Q | 0 | 1 | as previously permitted | failed | — | 0 |
| EMAIL-0017 | T → A → K → U → X | u a a a Q | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0018 | T → D → A → B → U | u d d r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0019 | T → D → A → U → B | u d d d r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0020 | T → D → A → X → U | u d d Q d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0021 | T → D → A → K → U | u d d d d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0022 | T → D → B → A → K | u d r r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0023 | T → D → B → U → K | u d r r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0024 | T → D → B → K → A | u d r r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0025 | T → D → U → A → X | u d d d Q | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0026 | T → D → U → B → X | u d d r Q | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0027 | T → D → U → X → K | u d d Q d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0028 | T → D → U → K → X | u d d d Q | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0029 | T → D → X → B → A | u d Q r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0030 | T → D → X → U → A | u d Q d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0031 | T → D → X → K → B | u d Q d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0032 | T → D → K → A → U | u d d d d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0033 | T → D → K → B → X | u d d r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0034 | T → D → K → U → X | u d d d Q | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0035 | T → B → A → D → U | u f f r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0036 | T → B → A → U → X | u f f f Q | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0037 | T → B → A → X → U | u f f Q f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0038 | T → B → A → K → X | u f f f Q | 0 | 1 | as previously permitted | failed | — | 0 |
| EMAIL-0039 | T → B → D → A → K | u f r r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0040 | T → B → D → X → A | u f r Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0041 | T → B → D → K → A | u f r r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0042 | T → B → U → A → X | u f f f Q | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0043 | T → B → U → D → X | u f f r Q | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0044 | T → B → U → X → K | u f f Q f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0045 | T → B → U → K → X | u f f f Q | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0046 | T → B → X → D → A | u f Q r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0047 | T → B → X → U → D | u f Q f r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0048 | T → B → X → K → D | u f Q f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0049 | T → B → K → A → X | u f f f Q | 0 | 1 | as previously permitted | failed | — | 0 |
| EMAIL-0050 | T → B → K → D → X | u f f r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0051 | T → B → K → X → A | u f f Q f | 0 | 1 | as previously permitted | failed | — | 0 |
| EMAIL-0052 | T → U → A → D → B | u u a d r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0053 | T → U → A → B → X | u u a f Q | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0054 | T → U → A → X → B | u u a Q f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0055 | T → U → A → K → X | u u a a Q | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0056 | T → U → D → A → K | u u d d d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0057 | T → U → D → X → A | u u d Q d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0058 | T → U → D → K → B | u u d d r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0059 | T → U → B → A → X | u u f f Q | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0060 | T → U → B → D → K | u u f r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0061 | T → U → B → X → K | u u f Q f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0062 | T → U → X → A → D | u u Q a d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0063 | T → U → X → D → A | u u Q d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0064 | T → U → X → B → D | u u Q f r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0065 | T → U → X → K → D | u u Q u d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0066 | T → U → K → A → X | u u u a Q | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0067 | T → U → K → D → X | u u u d Q | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0068 | T → U → K → X → A | u u u Q a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0069 | T → X → A → D → U | u Q a d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0070 | T → X → A → B → U | u Q a f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0071 | T → X → A → U → K | u Q a a a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0072 | T → X → A → K → U | u Q a a a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0073 | T → X → D → B → A | u Q d r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0074 | T → X → D → U → A | u Q d d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0075 | T → X → D → K → B | u Q d d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0076 | T → X → B → A → U | u Q f f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0077 | T → X → B → D → K | u Q f r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0078 | T → X → B → U → K | u Q f f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0079 | T → X → U → A → D | u Q u a d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0080 | T → X → U → D → B | u Q u d r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0081 | T → X → U → B → D | u Q u f r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0082 | T → X → U → K → B | u Q u u f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0083 | T → X → K → A → U | u Q u a a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0084 | T → X → K → B → A | u Q u f f | 0 | 1 | as previously permitted | failed | — | 0 |
| EMAIL-0085 | T → X → K → U → A | u Q u u a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0086 | T → K → A → D → U | u u a d d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0087 | T → K → A → B → U | u u a f f | 0 | 0 | future optional suppressed | failed | — | 0 |
| EMAIL-0088 | T → K → A → U → X | u u a a Q | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0089 | T → K → A → X → U | u u a Q a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0090 | T → K → D → B → A | u u d r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0091 | T → K → D → U → B | u u d d r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0092 | T → K → D → X → B | u u d Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0093 | T → K → B → A → X | u u f f Q | 0 | 1 | as previously permitted | failed | — | 0 |
| EMAIL-0094 | T → K → B → D → X | u u f r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0095 | T → K → B → X → A | u u f Q f | 0 | 1 | as previously permitted | failed | — | 0 |
| EMAIL-0096 | T → K → U → A → D | u u u a d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0097 | T → K → U → D → B | u u u d r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0098 | T → K → U → B → D | u u u f r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0099 | T → K → U → X → B | u u u Q f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0100 | T → K → X → A → U | u u Q a a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0101 | T → K → X → B → A | u u Q f f | 0 | 1 | as previously permitted | failed | — | 0 |
| EMAIL-0102 | T → K → X → U → D | u u Q u d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0103 | A → T → D → B → X | a a d r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0104 | A → T → D → U → K | a a d d d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0105 | A → T → D → X → K | a a d Q d | 0 | 1 | as previously permitted | delivered | — | 1 |
| EMAIL-0106 | A → T → B → D → U | a a f r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0107 | A → T → B → U → D | a a f f r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0108 | A → T → B → X → U | a a f Q f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0109 | A → T → B → K → U | a a f f f | 0 | 0 | future optional suppressed | failed | — | 0 |
| EMAIL-0110 | A → T → U → D → K | a a a d d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0111 | A → T → U → B → K | a a a f f | 0 | 0 | future optional suppressed | failed | — | 0 |
| EMAIL-0112 | A → T → U → K → D | a a a a d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0113 | A → T → X → D → U | a a Q d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0114 | A → T → X → B → U | a a Q f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0115 | A → T → X → U → K | a a Q a a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0116 | A → T → X → K → U | a a Q a a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0117 | A → T → K → B → D | a a a f r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0118 | A → T → K → U → D | a a a a d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0119 | A → T → K → X → B | a a a Q f | 0 | 1 | as previously permitted | failed | — | 0 |
| EMAIL-0120 | A → D → T → B → X | a d d r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0121 | A → D → T → U → K | a d d d d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0122 | A → D → T → X → K | a d d Q d | 0 | 1 | as previously permitted | delivered | — | 1 |
| EMAIL-0123 | A → D → B → T → U | a d r r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0124 | A → D → B → U → X | a d r r Q | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0125 | A → D → B → X → U | a d r Q r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0126 | A → D → B → K → X | a d r r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0127 | A → D → U → T → K | a d d d d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0128 | A → D → U → X → T | a d d Q d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0129 | A → D → U → K → T | a d d d d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0130 | A → D → X → T → U | a d Q d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0131 | A → D → X → B → U | a d Q r r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0132 | A → D → X → U → K | a d Q d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0133 | A → D → X → K → U | a d Q d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0134 | A → D → K → B → T | a d d r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0135 | A → D → K → U → B | a d d d r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0136 | A → D → K → X → B | a d d Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0137 | A → B → T → D → K | a f f r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0138 | A → B → T → U → K | a f f f f | 0 | 0 | future optional suppressed | failed | — | 0 |
| EMAIL-0139 | A → B → T → K → D | a f f f r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0140 | A → B → D → T → U | a f r r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0141 | A → B → D → U → X | a f r r Q | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0142 | A → B → D → X → U | a f r Q r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0143 | A → B → D → K → X | a f r r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0144 | A → B → U → T → K | a f f f f | 0 | 0 | future optional suppressed | failed | — | 0 |
| EMAIL-0145 | A → B → U → X → T | a f f Q f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0146 | A → B → U → K → D | a f f f r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0147 | A → B → X → T → U | a f Q f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0148 | A → B → X → D → K | a f Q r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0149 | A → B → X → U → K | a f Q f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0150 | A → B → K → T → D | a f f f r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0151 | A → B → K → D → T | a f f r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0152 | A → B → K → U → D | a f f f r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0153 | A → B → K → X → D | a f f Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0154 | A → U → T → D → K | a a a d d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0155 | A → U → T → B → K | a a a f f | 0 | 0 | future optional suppressed | failed | — | 0 |
| EMAIL-0156 | A → U → T → K → D | a a a a d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0157 | A → U → D → T → X | a a d d Q | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0158 | A → U → D → B → X | a a d r Q | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0159 | A → U → D → X → K | a a d Q d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0160 | A → U → D → K → X | a a d d Q | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0161 | A → U → B → D → T | a a f r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0162 | A → U → B → X → T | a a f Q f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0163 | A → U → B → K → D | a a f f r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0164 | A → U → X → T → B | a a Q a f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0165 | A → U → X → D → K | a a Q d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0166 | A → U → X → B → K | a a Q f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0167 | A → U → K → T → D | a a a a d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0168 | A → U → K → D → B | a a a d r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0169 | A → U → K → B → D | a a a f r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0170 | A → U → K → X → B | a a a Q f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0171 | A → X → T → D → K | a Q a d d | 0 | 1 | as previously permitted | delivered | — | 1 |
| EMAIL-0172 | A → X → T → U → D | a Q a a d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0173 | A → X → T → K → D | a Q a a d | 0 | 1 | as previously permitted | delivered | — | 1 |
| EMAIL-0174 | A → X → D → T → U | a Q d d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0175 | A → X → D → B → U | a Q d r r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0176 | A → X → D → U → K | a Q d d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0177 | A → X → D → K → U | a Q d d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0178 | A → X → B → D → T | a Q f r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0179 | A → X → B → U → D | a Q f f r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0180 | A → X → B → K → D | a Q f f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0181 | A → X → U → T → K | a Q a a a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0182 | A → X → U → D → K | a Q a d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0183 | A → X → U → K → T | a Q a a a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0184 | A → X → K → T → D | a Q a a d | 0 | 1 | as previously permitted | delivered | — | 1 |
| EMAIL-0185 | A → X → K → D → B | a Q a d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0186 | A → X → K → B → D | a Q a f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0187 | A → X → K → U → B | a Q a a f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0188 | A → K → T → D → X | a a a d Q | 0 | 1 | as previously permitted | delivered | — | 1 |
| EMAIL-0189 | A → K → T → U → D | a a a a d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0190 | A → K → T → X → B | a a a Q f | 0 | 1 | as previously permitted | failed | — | 0 |
| EMAIL-0191 | A → K → D → T → U | a a d d d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0192 | A → K → D → B → X | a a d r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0193 | A → K → D → U → X | a a d d Q | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0194 | A → K → B → T → D | a a f f r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0195 | A → K → B → D → T | a a f r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0196 | A → K → B → U → D | a a f f r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0197 | A → K → B → X → D | a a f Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0198 | A → K → U → T → X | a a a a Q | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0199 | A → K → U → D → X | a a a d Q | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0200 | A → K → U → X → T | a a a Q a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0201 | A → K → X → T → B | a a Q a f | 0 | 1 | as previously permitted | failed | — | 0 |
| EMAIL-0202 | A → K → X → D → B | a a Q d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0203 | A → K → X → B → U | a a Q f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0204 | A → K → X → U → B | a a Q a f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0205 | D → T → A → U → B | d d d d r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0206 | D → T → A → X → B | d d d Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0207 | D → T → A → K → U | d d d d d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0208 | D → T → B → A → X | d d r r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0209 | D → T → B → U → K | d d r r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0210 | D → T → B → X → K | d d r Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0211 | D → T → U → A → B | d d d d r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0212 | D → T → U → B → X | d d d r Q | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0213 | D → T → U → X → B | d d d Q r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0214 | D → T → U → K → X | d d d d Q | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0215 | D → T → X → A → K | d d Q d d | 0 | 1 | as previously permitted | delivered | — | 1 |
| EMAIL-0216 | D → T → X → U → A | d d Q d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0217 | D → T → X → K → A | d d Q d d | 0 | 1 | as previously permitted | delivered | — | 1 |
| EMAIL-0218 | D → T → K → A → U | d d d d d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0219 | D → T → K → B → U | d d d r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0220 | D → T → K → U → X | d d d d Q | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0221 | D → T → K → X → U | d d d Q d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0222 | D → A → T → U → B | d d d d r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0223 | D → A → T → X → U | d d d Q d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0224 | D → A → T → K → U | d d d d d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0225 | D → A → B → T → K | d d r r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0226 | D → A → B → U → K | d d r r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0227 | D → A → B → K → T | d d r r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0228 | D → A → U → T → B | d d d d r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0229 | D → A → U → B → X | d d d r Q | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0230 | D → A → U → X → B | d d d Q r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0231 | D → A → U → K → X | d d d d Q | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0232 | D → A → X → T → K | d d Q d d | 0 | 1 | as previously permitted | delivered | — | 1 |
| EMAIL-0233 | D → A → X → U → T | d d Q d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0234 | D → A → X → K → B | d d Q d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0235 | D → A → K → T → U | d d d d d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0236 | D → A → K → B → X | d d d r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0237 | D → A → K → U → X | d d d d Q | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0238 | D → B → T → A → U | d r r r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0239 | D → B → T → U → A | d r r r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0240 | D → B → T → X → U | d r r Q r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0241 | D → B → T → K → U | d r r r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0242 | D → B → A → T → K | d r r r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0243 | D → B → A → U → K | d r r r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0244 | D → B → A → K → T | d r r r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0245 | D → B → U → T → X | d r r r Q | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0246 | D → B → U → A → X | d r r r Q | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0247 | D → B → U → X → K | d r r Q r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0248 | D → B → U → K → X | d r r r Q | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0249 | D → B → X → A → T | d r Q r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0250 | D → B → X → U → T | d r Q r r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0251 | D → B → X → K → A | d r Q r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0252 | D → B → K → T → U | d r r r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0253 | D → B → K → A → X | d r r r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0254 | D → B → K → U → X | d r r r Q | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0255 | D → U → T → A → B | d d d d r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0256 | D → U → T → B → X | d d d r Q | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0257 | D → U → T → X → B | d d d Q r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0258 | D → U → T → K → X | d d d d Q | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0259 | D → U → A → T → K | d d d d d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0260 | D → U → A → X → T | d d d Q d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0261 | D → U → A → K → T | d d d d d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0262 | D → U → B → T → X | d d r r Q | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0263 | D → U → B → A → X | d d r r Q | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0264 | D → U → B → X → K | d d r Q r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0265 | D → U → B → K → X | d d r r Q | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0266 | D → U → X → A → T | d d Q d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0267 | D → U → X → B → A | d d Q r r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0268 | D → U → X → K → A | d d Q d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0269 | D → U → K → T → X | d d d d Q | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0270 | D → U → K → A → X | d d d d Q | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0271 | D → U → K → X → T | d d d Q d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0272 | D → X → T → A → B | d Q d d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0273 | D → X → T → B → U | d Q d r r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0274 | D → X → T → U → B | d Q d d r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0275 | D → X → T → K → U | d Q d d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0276 | D → X → A → T → K | d Q d d d | 0 | 1 | as previously permitted | delivered | — | 1 |
| EMAIL-0277 | D → X → A → U → T | d Q d d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0278 | D → X → A → K → B | d Q d d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0279 | D → X → B → T → U | d Q r r r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0280 | D → X → B → A → K | d Q r r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0281 | D → X → B → U → K | d Q r r r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0282 | D → X → U → T → A | d Q d d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0283 | D → X → U → A → T | d Q d d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0284 | D → X → U → B → A | d Q d r r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0285 | D → X → U → K → A | d Q d d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0286 | D → X → K → T → U | d Q d d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0287 | D → X → K → A → U | d Q d d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0288 | D → X → K → U → T | d Q d d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0289 | D → K → T → A → U | d d d d d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0290 | D → K → T → B → U | d d d r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0291 | D → K → T → U → X | d d d d Q | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0292 | D → K → T → X → U | d d d Q d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0293 | D → K → A → B → T | d d d r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0294 | D → K → A → U → T | d d d d d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0295 | D → K → A → X → B | d d d Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0296 | D → K → B → T → U | d d r r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0297 | D → K → B → A → X | d d r r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0298 | D → K → B → U → X | d d r r Q | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0299 | D → K → U → T → A | d d d d d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0300 | D → K → U → A → B | d d d d r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0301 | D → K → U → B → A | d d d r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0302 | D → K → U → X → B | d d d Q r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0303 | D → K → X → T → U | d d Q d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0304 | D → K → X → B → T | d d Q r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0305 | D → K → X → U → T | d d Q d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0306 | B → T → A → D → X | f f f r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0307 | B → T → A → U → X | f f f f Q | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0308 | B → T → A → X → K | f f f Q f | 0 | 1 | as previously permitted | failed | — | 0 |
| EMAIL-0309 | B → T → A → K → X | f f f f Q | 0 | 1 | as previously permitted | failed | — | 0 |
| EMAIL-0310 | B → T → D → U → A | f f r r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0311 | B → T → D → X → A | f f r Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0312 | B → T → D → K → U | f f r r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0313 | B → T → U → A → K | f f f f f | 0 | 0 | future optional suppressed | failed | — | 0 |
| EMAIL-0314 | B → T → U → D → K | f f f r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0315 | B → T → U → K → A | f f f f f | 0 | 0 | future optional suppressed | failed | — | 0 |
| EMAIL-0316 | B → T → X → A → D | f f Q f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0317 | B → T → X → D → U | f f Q r r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0318 | B → T → X → U → D | f f Q f r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0319 | B → T → X → K → U | f f Q f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0320 | B → T → K → A → X | f f f f Q | 0 | 1 | as previously permitted | failed | — | 0 |
| EMAIL-0321 | B → T → K → U → A | f f f f f | 0 | 0 | future optional suppressed | failed | — | 0 |
| EMAIL-0322 | B → T → K → X → A | f f f Q f | 0 | 1 | as previously permitted | failed | — | 0 |
| EMAIL-0323 | B → A → T → D → X | f f f r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0324 | B → A → T → U → K | f f f f f | 0 | 0 | future optional suppressed | failed | — | 0 |
| EMAIL-0325 | B → A → T → X → K | f f f Q f | 0 | 1 | as previously permitted | failed | — | 0 |
