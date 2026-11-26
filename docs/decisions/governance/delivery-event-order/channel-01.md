# Telegram channel acceptance and permission changes · 1 of 2

[Decision profiles](../README.md) · [Method and other cases](README.md) · [Clerk procedure](../../../handbook/governance/delivery-incident-desk.md)

**Given.** Five observations arrive consecutively at 09:00, 09:01, 09:02, 09:03 and 09:04 UTC for one already submitted route. A and A2 are duplicate confirmations of the same post. P withdraws posting permission for future sends. V records an aggregate 37 views of this post without identifying people. X is a wrong-sender callback. T records the local timeout. K is a reconciliation lookup with no new delivery information. A is provider acceptance (for channel, confirmed publication).

Use the row inputs with this profile. Compare every expected output at the indicated cutoff. Case numbers are local to this profile.

| Case | Arrival order | Trace | Duplicate observations | Quarantined | Future route | Final status | Post views observed | Confirmed people |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CHANNEL-0001 | T → A → A2 → P → V | u s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0002 | T → A → A2 → V → P | u s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0003 | T → A → A2 → X → V | u s s Q s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0004 | T → A → A2 → K → V | u s s s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0005 | T → A → P → A2 → K | u s s s s | 1 | 0 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0006 | T → A → P → V → K | u s s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0007 | T → A → P → K → A2 | u s s s s | 1 | 0 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0008 | T → A → V → A2 → P | u s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0009 | T → A → V → P → X | u s s s Q | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0010 | T → A → V → X → P | u s s Q s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0011 | T → A → V → K → X | u s s s Q | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0012 | T → A → X → A2 → K | u s Q s s | 1 | 1 | as previously permitted | posted once | 0 | 0 |
| CHANNEL-0013 | T → A → X → V → A2 | u s Q s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0014 | T → A → X → K → P | u s Q s s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0015 | T → A → K → A2 → V | u s s s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0016 | T → A → K → P → X | u s s s Q | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0017 | T → A → K → V → X | u s s s Q | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0018 | T → A2 → A → P → V | u s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0019 | T → A2 → A → V → P | u s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0020 | T → A2 → A → X → V | u s s Q s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0021 | T → A2 → A → K → V | u s s s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0022 | T → A2 → P → A → K | u s s s s | 1 | 0 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0023 | T → A2 → P → V → K | u s s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0024 | T → A2 → P → K → A | u s s s s | 1 | 0 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0025 | T → A2 → V → A → X | u s s s Q | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0026 | T → A2 → V → P → X | u s s s Q | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0027 | T → A2 → V → X → K | u s s Q s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0028 | T → A2 → V → K → X | u s s s Q | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0029 | T → A2 → X → P → A | u s Q s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0030 | T → A2 → X → V → A | u s Q s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0031 | T → A2 → X → K → P | u s Q s s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0032 | T → A2 → K → A → V | u s s s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0033 | T → A2 → K → P → X | u s s s Q | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0034 | T → A2 → K → V → X | u s s s Q | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0035 | T → P → A → A2 → V | u u s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0036 | T → P → A → V → X | u u s s Q | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0037 | T → P → A → X → V | u u s Q s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0038 | T → P → A → K → X | u u s s Q | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0039 | T → P → A2 → A → K | u u s s s | 1 | 0 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0040 | T → P → A2 → X → A | u u s Q s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0041 | T → P → A2 → K → A | u u s s s | 1 | 0 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0042 | T → P → V → A → X | u u u s Q | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0043 | T → P → V → A2 → X | u u u s Q | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0044 | T → P → V → X → K | u u u Q u | 0 | 1 | posting suspended | await post confirmation | 37 | 0 |
| CHANNEL-0045 | T → P → V → K → X | u u u u Q | 0 | 1 | posting suspended | await post confirmation | 37 | 0 |
| CHANNEL-0046 | T → P → X → A2 → A | u u Q s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0047 | T → P → X → V → A2 | u u Q u s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0048 | T → P → X → K → A2 | u u Q u s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0049 | T → P → K → A → X | u u u s Q | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0050 | T → P → K → A2 → X | u u u s Q | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0051 | T → P → K → X → A | u u u Q s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0052 | T → V → A → A2 → P | u u s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0053 | T → V → A → P → X | u u s s Q | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0054 | T → V → A → X → P | u u s Q s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0055 | T → V → A → K → X | u u s s Q | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0056 | T → V → A2 → A → K | u u s s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0057 | T → V → A2 → X → A | u u s Q s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0058 | T → V → A2 → K → P | u u s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0059 | T → V → P → A → X | u u u s Q | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0060 | T → V → P → A2 → K | u u u s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0061 | T → V → P → X → K | u u u Q u | 0 | 1 | posting suspended | await post confirmation | 37 | 0 |
| CHANNEL-0062 | T → V → X → A → A2 | u u Q s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0063 | T → V → X → A2 → A | u u Q s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0064 | T → V → X → P → A2 | u u Q u s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0065 | T → V → X → K → A2 | u u Q u s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0066 | T → V → K → A → X | u u u s Q | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0067 | T → V → K → A2 → X | u u u s Q | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0068 | T → V → K → X → A | u u u Q s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0069 | T → X → A → A2 → V | u Q s s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0070 | T → X → A → P → V | u Q s s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0071 | T → X → A → V → K | u Q s s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0072 | T → X → A → K → V | u Q s s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0073 | T → X → A2 → P → A | u Q s s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0074 | T → X → A2 → V → A | u Q s s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0075 | T → X → A2 → K → P | u Q s s s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0076 | T → X → P → A → V | u Q u s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0077 | T → X → P → A2 → K | u Q u s s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0078 | T → X → P → V → K | u Q u u u | 0 | 1 | posting suspended | await post confirmation | 37 | 0 |
| CHANNEL-0079 | T → X → V → A → A2 | u Q u s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0080 | T → X → V → A2 → P | u Q u s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0081 | T → X → V → P → A2 | u Q u u s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0082 | T → X → V → K → P | u Q u u u | 0 | 1 | posting suspended | await post confirmation | 37 | 0 |
| CHANNEL-0083 | T → X → K → A → V | u Q u s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0084 | T → X → K → P → A | u Q u u s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0085 | T → X → K → V → A | u Q u u s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0086 | T → K → A → A2 → V | u u s s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0087 | T → K → A → P → V | u u s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0088 | T → K → A → V → X | u u s s Q | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0089 | T → K → A → X → V | u u s Q s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0090 | T → K → A2 → P → A | u u s s s | 1 | 0 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0091 | T → K → A2 → V → P | u u s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0092 | T → K → A2 → X → P | u u s Q s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0093 | T → K → P → A → X | u u u s Q | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0094 | T → K → P → A2 → X | u u u s Q | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0095 | T → K → P → X → A | u u u Q s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0096 | T → K → V → A → A2 | u u u s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0097 | T → K → V → A2 → P | u u u s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0098 | T → K → V → P → A2 | u u u u s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0099 | T → K → V → X → P | u u u Q u | 0 | 1 | posting suspended | await post confirmation | 37 | 0 |
| CHANNEL-0100 | T → K → X → A → V | u u Q s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0101 | T → K → X → P → A | u u Q u s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0102 | T → K → X → V → A2 | u u Q u s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0103 | A → T → A2 → P → X | s s s s Q | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0104 | A → T → A2 → V → K | s s s s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0105 | A → T → A2 → X → K | s s s Q s | 1 | 1 | as previously permitted | posted once | 0 | 0 |
| CHANNEL-0106 | A → T → P → A2 → V | s s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0107 | A → T → P → V → A2 | s s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0108 | A → T → P → X → V | s s s Q s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0109 | A → T → P → K → V | s s s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0110 | A → T → V → A2 → K | s s s s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0111 | A → T → V → P → K | s s s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0112 | A → T → V → K → A2 | s s s s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0113 | A → T → X → A2 → V | s s Q s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0114 | A → T → X → P → V | s s Q s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0115 | A → T → X → V → K | s s Q s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0116 | A → T → X → K → V | s s Q s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0117 | A → T → K → P → A2 | s s s s s | 1 | 0 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0118 | A → T → K → V → A2 | s s s s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0119 | A → T → K → X → P | s s s Q s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0120 | A → A2 → T → P → X | s s s s Q | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0121 | A → A2 → T → V → K | s s s s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0122 | A → A2 → T → X → K | s s s Q s | 1 | 1 | as previously permitted | posted once | 0 | 0 |
| CHANNEL-0123 | A → A2 → P → T → V | s s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0124 | A → A2 → P → V → X | s s s s Q | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0125 | A → A2 → P → X → V | s s s Q s | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0126 | A → A2 → P → K → X | s s s s Q | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0127 | A → A2 → V → T → K | s s s s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0128 | A → A2 → V → X → T | s s s Q s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0129 | A → A2 → V → K → T | s s s s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0130 | A → A2 → X → T → V | s s Q s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0131 | A → A2 → X → P → V | s s Q s s | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0132 | A → A2 → X → V → K | s s Q s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0133 | A → A2 → X → K → V | s s Q s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0134 | A → A2 → K → P → T | s s s s s | 1 | 0 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0135 | A → A2 → K → V → P | s s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0136 | A → A2 → K → X → P | s s s Q s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0137 | A → P → T → A2 → K | s s s s s | 1 | 0 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0138 | A → P → T → V → K | s s s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0139 | A → P → T → K → A2 | s s s s s | 1 | 0 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0140 | A → P → A2 → T → V | s s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0141 | A → P → A2 → V → X | s s s s Q | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0142 | A → P → A2 → X → V | s s s Q s | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0143 | A → P → A2 → K → X | s s s s Q | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0144 | A → P → V → T → K | s s s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0145 | A → P → V → X → T | s s s Q s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0146 | A → P → V → K → A2 | s s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0147 | A → P → X → T → V | s s Q s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0148 | A → P → X → A2 → K | s s Q s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0149 | A → P → X → V → K | s s Q s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0150 | A → P → K → T → A2 | s s s s s | 1 | 0 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0151 | A → P → K → A2 → T | s s s s s | 1 | 0 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0152 | A → P → K → V → A2 | s s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0153 | A → P → K → X → A2 | s s s Q s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0154 | A → V → T → A2 → K | s s s s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0155 | A → V → T → P → K | s s s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0156 | A → V → T → K → A2 | s s s s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0157 | A → V → A2 → T → X | s s s s Q | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0158 | A → V → A2 → P → X | s s s s Q | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0159 | A → V → A2 → X → K | s s s Q s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0160 | A → V → A2 → K → X | s s s s Q | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0161 | A → V → P → A2 → T | s s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0162 | A → V → P → X → T | s s s Q s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0163 | A → V → P → K → A2 | s s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0164 | A → V → X → T → P | s s Q s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0165 | A → V → X → A2 → K | s s Q s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0166 | A → V → X → P → K | s s Q s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0167 | A → V → K → T → A2 | s s s s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0168 | A → V → K → A2 → P | s s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0169 | A → V → K → P → A2 | s s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0170 | A → V → K → X → P | s s s Q s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0171 | A → X → T → A2 → K | s Q s s s | 1 | 1 | as previously permitted | posted once | 0 | 0 |
| CHANNEL-0172 | A → X → T → V → A2 | s Q s s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0173 | A → X → T → K → A2 | s Q s s s | 1 | 1 | as previously permitted | posted once | 0 | 0 |
| CHANNEL-0174 | A → X → A2 → T → V | s Q s s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0175 | A → X → A2 → P → V | s Q s s s | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0176 | A → X → A2 → V → K | s Q s s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0177 | A → X → A2 → K → V | s Q s s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0178 | A → X → P → A2 → T | s Q s s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0179 | A → X → P → V → A2 | s Q s s s | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0180 | A → X → P → K → A2 | s Q s s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0181 | A → X → V → T → K | s Q s s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0182 | A → X → V → A2 → K | s Q s s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0183 | A → X → V → K → T | s Q s s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0184 | A → X → K → T → A2 | s Q s s s | 1 | 1 | as previously permitted | posted once | 0 | 0 |
| CHANNEL-0185 | A → X → K → A2 → P | s Q s s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0186 | A → X → K → P → A2 | s Q s s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0187 | A → X → K → V → P | s Q s s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0188 | A → K → T → A2 → X | s s s s Q | 1 | 1 | as previously permitted | posted once | 0 | 0 |
| CHANNEL-0189 | A → K → T → V → A2 | s s s s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0190 | A → K → T → X → P | s s s Q s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0191 | A → K → A2 → T → V | s s s s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0192 | A → K → A2 → P → X | s s s s Q | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0193 | A → K → A2 → V → X | s s s s Q | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0194 | A → K → P → T → A2 | s s s s s | 1 | 0 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0195 | A → K → P → A2 → T | s s s s s | 1 | 0 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0196 | A → K → P → V → A2 | s s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0197 | A → K → P → X → A2 | s s s Q s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0198 | A → K → V → T → X | s s s s Q | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0199 | A → K → V → A2 → X | s s s s Q | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0200 | A → K → V → X → T | s s s Q s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0201 | A → K → X → T → P | s s Q s s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0202 | A → K → X → A2 → P | s s Q s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0203 | A → K → X → P → V | s s Q s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0204 | A → K → X → V → P | s s Q s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0205 | A2 → T → A → V → P | s s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0206 | A2 → T → A → X → P | s s s Q s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0207 | A2 → T → A → K → V | s s s s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0208 | A2 → T → P → A → X | s s s s Q | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0209 | A2 → T → P → V → K | s s s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0210 | A2 → T → P → X → K | s s s Q s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0211 | A2 → T → V → A → P | s s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0212 | A2 → T → V → P → X | s s s s Q | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0213 | A2 → T → V → X → P | s s s Q s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0214 | A2 → T → V → K → X | s s s s Q | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0215 | A2 → T → X → A → K | s s Q s s | 1 | 1 | as previously permitted | posted once | 0 | 0 |
| CHANNEL-0216 | A2 → T → X → V → A | s s Q s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0217 | A2 → T → X → K → A | s s Q s s | 1 | 1 | as previously permitted | posted once | 0 | 0 |
| CHANNEL-0218 | A2 → T → K → A → V | s s s s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0219 | A2 → T → K → P → V | s s s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0220 | A2 → T → K → V → X | s s s s Q | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0221 | A2 → T → K → X → V | s s s Q s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0222 | A2 → A → T → V → P | s s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0223 | A2 → A → T → X → V | s s s Q s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0224 | A2 → A → T → K → V | s s s s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0225 | A2 → A → P → T → K | s s s s s | 1 | 0 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0226 | A2 → A → P → V → K | s s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0227 | A2 → A → P → K → T | s s s s s | 1 | 0 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0228 | A2 → A → V → T → P | s s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0229 | A2 → A → V → P → X | s s s s Q | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0230 | A2 → A → V → X → P | s s s Q s | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0231 | A2 → A → V → K → X | s s s s Q | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0232 | A2 → A → X → T → K | s s Q s s | 1 | 1 | as previously permitted | posted once | 0 | 0 |
| CHANNEL-0233 | A2 → A → X → V → T | s s Q s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0234 | A2 → A → X → K → P | s s Q s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0235 | A2 → A → K → T → V | s s s s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0236 | A2 → A → K → P → X | s s s s Q | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0237 | A2 → A → K → V → X | s s s s Q | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0238 | A2 → P → T → A → V | s s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0239 | A2 → P → T → V → A | s s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0240 | A2 → P → T → X → V | s s s Q s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0241 | A2 → P → T → K → V | s s s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0242 | A2 → P → A → T → K | s s s s s | 1 | 0 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0243 | A2 → P → A → V → K | s s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0244 | A2 → P → A → K → T | s s s s s | 1 | 0 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0245 | A2 → P → V → T → X | s s s s Q | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0246 | A2 → P → V → A → X | s s s s Q | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0247 | A2 → P → V → X → K | s s s Q s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0248 | A2 → P → V → K → X | s s s s Q | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0249 | A2 → P → X → A → T | s s Q s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0250 | A2 → P → X → V → T | s s Q s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0251 | A2 → P → X → K → A | s s Q s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0252 | A2 → P → K → T → V | s s s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0253 | A2 → P → K → A → X | s s s s Q | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0254 | A2 → P → K → V → X | s s s s Q | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0255 | A2 → V → T → A → P | s s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0256 | A2 → V → T → P → X | s s s s Q | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0257 | A2 → V → T → X → P | s s s Q s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0258 | A2 → V → T → K → X | s s s s Q | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0259 | A2 → V → A → T → K | s s s s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0260 | A2 → V → A → X → T | s s s Q s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0261 | A2 → V → A → K → T | s s s s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0262 | A2 → V → P → T → X | s s s s Q | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0263 | A2 → V → P → A → X | s s s s Q | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0264 | A2 → V → P → X → K | s s s Q s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0265 | A2 → V → P → K → X | s s s s Q | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0266 | A2 → V → X → A → T | s s Q s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0267 | A2 → V → X → P → A | s s Q s s | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0268 | A2 → V → X → K → A | s s Q s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0269 | A2 → V → K → T → X | s s s s Q | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0270 | A2 → V → K → A → X | s s s s Q | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0271 | A2 → V → K → X → T | s s s Q s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0272 | A2 → X → T → A → P | s Q s s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0273 | A2 → X → T → P → V | s Q s s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0274 | A2 → X → T → V → P | s Q s s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0275 | A2 → X → T → K → V | s Q s s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0276 | A2 → X → A → T → K | s Q s s s | 1 | 1 | as previously permitted | posted once | 0 | 0 |
| CHANNEL-0277 | A2 → X → A → V → T | s Q s s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0278 | A2 → X → A → K → P | s Q s s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0279 | A2 → X → P → T → V | s Q s s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0280 | A2 → X → P → A → K | s Q s s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0281 | A2 → X → P → V → K | s Q s s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0282 | A2 → X → V → T → A | s Q s s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0283 | A2 → X → V → A → T | s Q s s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0284 | A2 → X → V → P → A | s Q s s s | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0285 | A2 → X → V → K → A | s Q s s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0286 | A2 → X → K → T → V | s Q s s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0287 | A2 → X → K → A → V | s Q s s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0288 | A2 → X → K → V → T | s Q s s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0289 | A2 → K → T → A → V | s s s s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0290 | A2 → K → T → P → V | s s s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0291 | A2 → K → T → V → X | s s s s Q | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0292 | A2 → K → T → X → V | s s s Q s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0293 | A2 → K → A → P → T | s s s s s | 1 | 0 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0294 | A2 → K → A → V → T | s s s s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0295 | A2 → K → A → X → P | s s s Q s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0296 | A2 → K → P → T → V | s s s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0297 | A2 → K → P → A → X | s s s s Q | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0298 | A2 → K → P → V → X | s s s s Q | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0299 | A2 → K → V → T → A | s s s s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0300 | A2 → K → V → A → P | s s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0301 | A2 → K → V → P → A | s s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0302 | A2 → K → V → X → P | s s s Q s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0303 | A2 → K → X → T → V | s s Q s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0304 | A2 → K → X → P → T | s s Q s s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0305 | A2 → K → X → V → T | s s Q s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0306 | P → T → A → A2 → X | p u s s Q | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0307 | P → T → A → V → X | p u s s Q | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0308 | P → T → A → X → K | p u s Q s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0309 | P → T → A → K → X | p u s s Q | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0310 | P → T → A2 → V → A | p u s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0311 | P → T → A2 → X → A | p u s Q s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0312 | P → T → A2 → K → V | p u s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0313 | P → T → V → A → K | p u u s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0314 | P → T → V → A2 → K | p u u s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0315 | P → T → V → K → A | p u u u s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0316 | P → T → X → A → A2 | p u Q s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0317 | P → T → X → A2 → V | p u Q s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0318 | P → T → X → V → A2 | p u Q u s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0319 | P → T → X → K → V | p u Q u u | 0 | 1 | posting suspended | await post confirmation | 37 | 0 |
| CHANNEL-0320 | P → T → K → A → X | p u u s Q | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0321 | P → T → K → V → A | p u u u s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0322 | P → T → K → X → A | p u u Q s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0323 | P → A → T → A2 → X | p s s s Q | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0324 | P → A → T → V → K | p s s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0325 | P → A → T → X → K | p s s Q s | 0 | 1 | posting suspended | posted once | 0 | 0 |
