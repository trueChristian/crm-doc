# Rota reminders, email then private chat · 1 of 2

[Decision profiles](../README.md) · [Method and other cases](README.md) · [Clerk procedure](../../../handbook/governance/contact-routing.md)

**Given.** Preference order EMAIL → private Telegram → SMS. Shared routes have express approval for this minimum-content message. Optional appeals have permission only where marked ready or approved shared. A representative must hold purpose-specific authority at handoff. All cases concern one intended person and pass the sender authorization check.

Use the row inputs with this profile. Compare every expected output at the indicated cutoff. Case numbers are local to this profile.

| Case | Email | SMS | Telegram | Post | Capacity | At freeze | Before handoff | At release | Operation |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| SERVICE-0001 | ready | ready | linked | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0002 | ready | ready | linked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0003 | ready | ready | linked | n/a | direct | email | email unsafe | Telegram direct | reselect before handoff |
| SERVICE-0004 | ready | ready | linked | n/a | representative with authority | email | email unsafe | Telegram direct | reselect before handoff |
| SERVICE-0005 | ready | ready | linked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0006 | ready | ready | linked | n/a | direct | email | chat blocked | email | preserve disposition |
| SERVICE-0007 | ready | ready | linked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0008 | ready | ready | linked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0009 | ready | ready | channel member | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0010 | ready | ready | channel member | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0011 | ready | ready | channel member | n/a | direct | email | email unsafe | sms | reselect before handoff |
| SERVICE-0012 | ready | ready | channel member | n/a | representative with authority | email | email unsafe | sms | reselect before handoff |
| SERVICE-0013 | ready | ready | channel member | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0014 | ready | ready | channel member | n/a | direct | email | chat blocked | email | preserve disposition |
| SERVICE-0015 | ready | ready | channel member | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0016 | ready | ready | channel member | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0017 | ready | ready | unlinked | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0018 | ready | ready | unlinked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0019 | ready | ready | unlinked | n/a | direct | email | email unsafe | sms | reselect before handoff |
| SERVICE-0020 | ready | ready | unlinked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0021 | ready | ready | unlinked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0022 | ready | ready | unlinked | n/a | direct | email | chat blocked | email | preserve disposition |
| SERVICE-0023 | ready | ready | unlinked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0024 | ready | ready | unlinked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0025 | ready | ready | blocked | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0026 | ready | ready | blocked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0027 | ready | ready | blocked | n/a | direct | email | email unsafe | sms | reselect before handoff |
| SERVICE-0028 | ready | ready | blocked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0029 | ready | ready | blocked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0030 | ready | ready | blocked | n/a | direct | email | chat blocked | email | preserve disposition |
| SERVICE-0031 | ready | ready | blocked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0032 | ready | ready | blocked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0033 | ready | shared | linked | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0034 | ready | shared | linked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0035 | ready | shared | linked | n/a | representative with authority | email | email unsafe | Telegram direct | reselect before handoff |
| SERVICE-0036 | ready | shared | linked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0037 | ready | shared | linked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0038 | ready | shared | linked | n/a | direct | email | chat blocked | email | preserve disposition |
| SERVICE-0039 | ready | shared | linked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0040 | ready | shared | linked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0041 | ready | shared | channel member | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0042 | ready | shared | channel member | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0043 | ready | shared | channel member | n/a | representative with authority | email | email unsafe | sms | reselect before handoff |
| SERVICE-0044 | ready | shared | channel member | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0045 | ready | shared | channel member | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0046 | ready | shared | channel member | n/a | direct | email | chat blocked | email | preserve disposition |
| SERVICE-0047 | ready | shared | channel member | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0048 | ready | shared | channel member | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0049 | ready | shared | unlinked | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0050 | ready | shared | unlinked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0051 | ready | shared | unlinked | n/a | representative with authority | email | email unsafe | sms | reselect before handoff |
| SERVICE-0052 | ready | shared | unlinked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0053 | ready | shared | unlinked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0054 | ready | shared | unlinked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0055 | ready | shared | unlinked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0056 | ready | shared | unlinked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0057 | ready | shared | blocked | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0058 | ready | shared | blocked | n/a | direct | email | email unsafe | sms | reselect before handoff |
| SERVICE-0059 | ready | shared | blocked | n/a | representative with authority | email | email unsafe | sms | reselect before handoff |
| SERVICE-0060 | ready | shared | blocked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0061 | ready | shared | blocked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0062 | ready | shared | blocked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0063 | ready | shared | blocked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0064 | ready | shared | blocked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0065 | ready | verified declined | linked | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0066 | ready | verified declined | linked | n/a | direct | email | email unsafe | Telegram direct | reselect before handoff |
| SERVICE-0067 | ready | verified declined | linked | n/a | representative with authority | email | email unsafe | Telegram direct | reselect before handoff |
| SERVICE-0068 | ready | verified declined | linked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0069 | ready | verified declined | linked | n/a | direct | email | chat blocked | email | preserve disposition |
| SERVICE-0070 | ready | verified declined | linked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0071 | ready | verified declined | linked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0072 | ready | verified declined | linked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0073 | ready | verified declined | channel member | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0074 | ready | verified declined | channel member | n/a | direct | email | email unsafe | no permitted route | hold for resolution |
| SERVICE-0075 | ready | verified declined | channel member | n/a | representative with authority | email | email unsafe | no permitted route | hold for resolution |
| SERVICE-0076 | ready | verified declined | channel member | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0077 | ready | verified declined | channel member | n/a | direct | email | chat blocked | email | preserve disposition |
| SERVICE-0078 | ready | verified declined | channel member | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0079 | ready | verified declined | channel member | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0080 | ready | verified declined | channel member | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0081 | ready | verified declined | unlinked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0082 | ready | verified declined | unlinked | n/a | direct | email | email unsafe | no permitted route | hold for resolution |
| SERVICE-0083 | ready | verified declined | unlinked | n/a | representative with authority | email | email unsafe | no permitted route | hold for resolution |
| SERVICE-0084 | ready | verified declined | unlinked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0085 | ready | verified declined | unlinked | n/a | direct | email | chat blocked | email | preserve disposition |
| SERVICE-0086 | ready | verified declined | unlinked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0087 | ready | verified declined | unlinked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0088 | ready | verified declined | blocked | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0089 | ready | verified declined | blocked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0090 | ready | verified declined | blocked | n/a | direct | email | email unsafe | no permitted route | hold for resolution |
| SERVICE-0091 | ready | verified declined | blocked | n/a | representative with authority | email | email unsafe | no permitted route | hold for resolution |
| SERVICE-0092 | ready | verified declined | blocked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0093 | ready | verified declined | blocked | n/a | direct | email | chat blocked | email | preserve disposition |
| SERVICE-0094 | ready | verified declined | blocked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0095 | ready | verified declined | blocked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0096 | ready | unverified | linked | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0097 | ready | unverified | linked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0098 | ready | unverified | linked | n/a | direct | email | email unsafe | Telegram direct | reselect before handoff |
| SERVICE-0099 | ready | unverified | linked | n/a | representative with authority | email | email unsafe | Telegram direct | reselect before handoff |
| SERVICE-0100 | ready | unverified | linked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0101 | ready | unverified | linked | n/a | direct | email | chat blocked | email | preserve disposition |
| SERVICE-0102 | ready | unverified | linked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0103 | ready | unverified | linked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0104 | ready | unverified | channel member | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0105 | ready | unverified | channel member | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0106 | ready | unverified | channel member | n/a | direct | email | email unsafe | no permitted route | hold for resolution |
| SERVICE-0107 | ready | unverified | channel member | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0108 | ready | unverified | channel member | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0109 | ready | unverified | channel member | n/a | direct | email | chat blocked | email | preserve disposition |
| SERVICE-0110 | ready | unverified | channel member | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0111 | ready | unverified | channel member | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0112 | ready | unverified | unlinked | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0113 | ready | unverified | unlinked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0114 | ready | unverified | unlinked | n/a | direct | email | email unsafe | no permitted route | hold for resolution |
| SERVICE-0115 | ready | unverified | unlinked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0116 | ready | unverified | unlinked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0117 | ready | unverified | unlinked | n/a | direct | email | chat blocked | email | preserve disposition |
| SERVICE-0118 | ready | unverified | unlinked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0119 | ready | unverified | unlinked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0120 | ready | unverified | blocked | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0121 | ready | unverified | blocked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0122 | ready | unverified | blocked | n/a | representative with authority | email | email unsafe | no permitted route | hold for resolution |
| SERVICE-0123 | ready | unverified | blocked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0124 | ready | unverified | blocked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0125 | ready | unverified | blocked | n/a | direct | email | chat blocked | email | preserve disposition |
| SERVICE-0126 | ready | unverified | blocked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0127 | ready | unverified | blocked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0128 | ready | none | linked | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0129 | ready | none | linked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0130 | ready | none | linked | n/a | representative with authority | email | email unsafe | Telegram direct | reselect before handoff |
| SERVICE-0131 | ready | none | linked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0132 | ready | none | linked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0133 | ready | none | linked | n/a | direct | email | chat blocked | email | preserve disposition |
| SERVICE-0134 | ready | none | linked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0135 | ready | none | linked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0136 | ready | none | channel member | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0137 | ready | none | channel member | n/a | direct | email | email unsafe | no permitted route | hold for resolution |
| SERVICE-0138 | ready | none | channel member | n/a | representative with authority | email | email unsafe | no permitted route | hold for resolution |
| SERVICE-0139 | ready | none | channel member | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0140 | ready | none | channel member | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0141 | ready | none | channel member | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0142 | ready | none | channel member | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0143 | ready | none | channel member | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0144 | ready | none | unlinked | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0145 | ready | none | unlinked | n/a | direct | email | email unsafe | no permitted route | hold for resolution |
| SERVICE-0146 | ready | none | unlinked | n/a | representative with authority | email | email unsafe | no permitted route | hold for resolution |
| SERVICE-0147 | ready | none | unlinked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0148 | ready | none | unlinked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0149 | ready | none | unlinked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0150 | ready | none | unlinked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0151 | ready | none | unlinked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0152 | ready | none | blocked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0153 | ready | none | blocked | n/a | direct | email | email unsafe | no permitted route | hold for resolution |
| SERVICE-0154 | ready | none | blocked | n/a | representative with authority | email | email unsafe | no permitted route | hold for resolution |
| SERVICE-0155 | ready | none | blocked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0156 | ready | none | blocked | n/a | direct | email | chat blocked | email | preserve disposition |
| SERVICE-0157 | ready | none | blocked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0158 | ready | none | blocked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0159 | ready | none | blocked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0160 | shared | ready | linked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0161 | shared | ready | linked | n/a | direct | email | email unsafe | Telegram direct | reselect before handoff |
| SERVICE-0162 | shared | ready | linked | n/a | representative with authority | email | email unsafe | Telegram direct | reselect before handoff |
| SERVICE-0163 | shared | ready | linked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0164 | shared | ready | linked | n/a | direct | email | chat blocked | email | preserve disposition |
| SERVICE-0165 | shared | ready | linked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0166 | shared | ready | linked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0167 | shared | ready | linked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0168 | shared | ready | channel member | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0169 | shared | ready | channel member | n/a | direct | email | email unsafe | sms | reselect before handoff |
| SERVICE-0170 | shared | ready | channel member | n/a | representative with authority | email | email unsafe | sms | reselect before handoff |
| SERVICE-0171 | shared | ready | channel member | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0172 | shared | ready | channel member | n/a | direct | email | chat blocked | email | preserve disposition |
| SERVICE-0173 | shared | ready | channel member | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0174 | shared | ready | channel member | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0175 | shared | ready | unlinked | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0176 | shared | ready | unlinked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0177 | shared | ready | unlinked | n/a | direct | email | email unsafe | sms | reselect before handoff |
| SERVICE-0178 | shared | ready | unlinked | n/a | representative with authority | email | email unsafe | sms | reselect before handoff |
| SERVICE-0179 | shared | ready | unlinked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0180 | shared | ready | unlinked | n/a | direct | email | chat blocked | email | preserve disposition |
| SERVICE-0181 | shared | ready | unlinked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0182 | shared | ready | unlinked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0183 | shared | ready | blocked | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0184 | shared | ready | blocked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0185 | shared | ready | blocked | n/a | direct | email | email unsafe | sms | reselect before handoff |
| SERVICE-0186 | shared | ready | blocked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0187 | shared | ready | blocked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0188 | shared | ready | blocked | n/a | direct | email | chat blocked | email | preserve disposition |
| SERVICE-0189 | shared | ready | blocked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0190 | shared | ready | blocked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0191 | shared | shared | linked | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0192 | shared | shared | linked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0193 | shared | shared | linked | n/a | direct | email | email unsafe | Telegram direct | reselect before handoff |
| SERVICE-0194 | shared | shared | linked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0195 | shared | shared | linked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0196 | shared | shared | linked | n/a | direct | email | chat blocked | email | preserve disposition |
| SERVICE-0197 | shared | shared | linked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0198 | shared | shared | linked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0199 | shared | shared | channel member | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0200 | shared | shared | channel member | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0201 | shared | shared | channel member | n/a | direct | email | email unsafe | sms | reselect before handoff |
| SERVICE-0202 | shared | shared | channel member | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0203 | shared | shared | channel member | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0204 | shared | shared | channel member | n/a | direct | email | chat blocked | email | preserve disposition |
| SERVICE-0205 | shared | shared | channel member | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0206 | shared | shared | channel member | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0207 | shared | shared | unlinked | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0208 | shared | shared | unlinked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0209 | shared | shared | unlinked | n/a | representative with authority | email | email unsafe | sms | reselect before handoff |
| SERVICE-0210 | shared | shared | unlinked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0211 | shared | shared | unlinked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0212 | shared | shared | unlinked | n/a | direct | email | chat blocked | email | preserve disposition |
| SERVICE-0213 | shared | shared | unlinked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0214 | shared | shared | unlinked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0215 | shared | shared | blocked | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0216 | shared | shared | blocked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0217 | shared | shared | blocked | n/a | representative with authority | email | email unsafe | sms | reselect before handoff |
| SERVICE-0218 | shared | shared | blocked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0219 | shared | shared | blocked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0220 | shared | shared | blocked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0221 | shared | shared | blocked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0222 | shared | shared | blocked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0223 | shared | verified declined | linked | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0224 | shared | verified declined | linked | n/a | direct | email | email unsafe | Telegram direct | reselect before handoff |
| SERVICE-0225 | shared | verified declined | linked | n/a | representative with authority | email | email unsafe | Telegram direct | reselect before handoff |
| SERVICE-0226 | shared | verified declined | linked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0227 | shared | verified declined | linked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0228 | shared | verified declined | linked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0229 | shared | verified declined | linked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0230 | shared | verified declined | linked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0231 | shared | verified declined | channel member | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0232 | shared | verified declined | channel member | n/a | direct | email | email unsafe | no permitted route | hold for resolution |
| SERVICE-0233 | shared | verified declined | channel member | n/a | representative with authority | email | email unsafe | no permitted route | hold for resolution |
| SERVICE-0234 | shared | verified declined | channel member | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0235 | shared | verified declined | channel member | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0236 | shared | verified declined | channel member | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0237 | shared | verified declined | channel member | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0238 | shared | verified declined | channel member | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0239 | shared | verified declined | unlinked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0240 | shared | verified declined | unlinked | n/a | direct | email | email unsafe | no permitted route | hold for resolution |
| SERVICE-0241 | shared | verified declined | unlinked | n/a | representative with authority | email | email unsafe | no permitted route | hold for resolution |
| SERVICE-0242 | shared | verified declined | unlinked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0243 | shared | verified declined | unlinked | n/a | direct | email | chat blocked | email | preserve disposition |
| SERVICE-0244 | shared | verified declined | unlinked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0245 | shared | verified declined | unlinked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0246 | shared | verified declined | unlinked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0247 | shared | verified declined | blocked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0248 | shared | verified declined | blocked | n/a | direct | email | email unsafe | no permitted route | hold for resolution |
| SERVICE-0249 | shared | verified declined | blocked | n/a | representative with authority | email | email unsafe | no permitted route | hold for resolution |
| SERVICE-0250 | shared | verified declined | blocked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0251 | shared | verified declined | blocked | n/a | direct | email | chat blocked | email | preserve disposition |
| SERVICE-0252 | shared | verified declined | blocked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0253 | shared | verified declined | blocked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0254 | shared | unverified | linked | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0255 | shared | unverified | linked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0256 | shared | unverified | linked | n/a | direct | email | email unsafe | Telegram direct | reselect before handoff |
| SERVICE-0257 | shared | unverified | linked | n/a | representative with authority | email | email unsafe | Telegram direct | reselect before handoff |
| SERVICE-0258 | shared | unverified | linked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0259 | shared | unverified | linked | n/a | direct | email | chat blocked | email | preserve disposition |
| SERVICE-0260 | shared | unverified | linked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0261 | shared | unverified | linked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0262 | shared | unverified | channel member | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0263 | shared | unverified | channel member | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0264 | shared | unverified | channel member | n/a | direct | email | email unsafe | no permitted route | hold for resolution |
| SERVICE-0265 | shared | unverified | channel member | n/a | representative with authority | email | email unsafe | no permitted route | hold for resolution |
| SERVICE-0266 | shared | unverified | channel member | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0267 | shared | unverified | channel member | n/a | direct | email | chat blocked | email | preserve disposition |
| SERVICE-0268 | shared | unverified | channel member | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0269 | shared | unverified | channel member | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0270 | shared | unverified | unlinked | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0271 | shared | unverified | unlinked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0272 | shared | unverified | unlinked | n/a | direct | email | email unsafe | no permitted route | hold for resolution |
| SERVICE-0273 | shared | unverified | unlinked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0274 | shared | unverified | unlinked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0275 | shared | unverified | unlinked | n/a | direct | email | chat blocked | email | preserve disposition |
| SERVICE-0276 | shared | unverified | unlinked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0277 | shared | unverified | unlinked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0278 | shared | unverified | blocked | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0279 | shared | unverified | blocked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0280 | shared | unverified | blocked | n/a | direct | email | email unsafe | no permitted route | hold for resolution |
| SERVICE-0281 | shared | unverified | blocked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0282 | shared | unverified | blocked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0283 | shared | unverified | blocked | n/a | direct | email | chat blocked | email | preserve disposition |
| SERVICE-0284 | shared | unverified | blocked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0285 | shared | unverified | blocked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0286 | shared | none | linked | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0287 | shared | none | linked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0288 | shared | none | linked | n/a | representative with authority | email | email unsafe | Telegram direct | reselect before handoff |
| SERVICE-0289 | shared | none | linked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0290 | shared | none | linked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0291 | shared | none | linked | n/a | direct | email | chat blocked | email | preserve disposition |
| SERVICE-0292 | shared | none | linked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0293 | shared | none | linked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0294 | shared | none | channel member | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0295 | shared | none | channel member | n/a | representative with authority | email | unchanged | email | preserve disposition |
| SERVICE-0296 | shared | none | channel member | n/a | representative with authority | email | email unsafe | no permitted route | hold for resolution |
| SERVICE-0297 | shared | none | channel member | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0298 | shared | none | channel member | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0299 | shared | none | channel member | n/a | direct | email | chat blocked | email | preserve disposition |
| SERVICE-0300 | shared | none | channel member | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0301 | shared | none | channel member | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0302 | shared | none | unlinked | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0303 | shared | none | unlinked | n/a | direct | email | email unsafe | no permitted route | hold for resolution |
| SERVICE-0304 | shared | none | unlinked | n/a | representative with authority | email | email unsafe | no permitted route | hold for resolution |
| SERVICE-0305 | shared | none | unlinked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0306 | shared | none | unlinked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0307 | shared | none | unlinked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0308 | shared | none | unlinked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0309 | shared | none | unlinked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0310 | shared | none | blocked | n/a | direct | email | unchanged | email | preserve disposition |
| SERVICE-0311 | shared | none | blocked | n/a | direct | email | email unsafe | no permitted route | hold for resolution |
| SERVICE-0312 | shared | none | blocked | n/a | representative with authority | email | email unsafe | no permitted route | hold for resolution |
| SERVICE-0313 | shared | none | blocked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| SERVICE-0314 | shared | none | blocked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| SERVICE-0315 | shared | none | blocked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| SERVICE-0316 | shared | none | blocked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0317 | shared | none | blocked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| SERVICE-0318 | verified declined | ready | linked | n/a | direct | Telegram direct | unchanged | Telegram direct | preserve disposition |
| SERVICE-0319 | verified declined | ready | linked | n/a | direct | Telegram direct | email unsafe | Telegram direct | preserve disposition |
| SERVICE-0320 | verified declined | ready | linked | n/a | representative with authority | Telegram direct | email unsafe | Telegram direct | preserve disposition |
| SERVICE-0321 | verified declined | ready | linked | n/a | direct | Telegram direct | SMS opt-out | Telegram direct | preserve disposition |
| SERVICE-0322 | verified declined | ready | linked | n/a | direct | Telegram direct | chat blocked | sms | reselect before handoff |
| SERVICE-0323 | verified declined | ready | linked | n/a | representative with authority | Telegram direct | chat blocked | sms | reselect before handoff |
| SERVICE-0324 | verified declined | ready | linked | n/a | direct | Telegram direct | recipient out of scope | exclude · authority | suppress |
| SERVICE-0325 | verified declined | ready | linked | n/a | representative with authority | Telegram direct | recipient out of scope | exclude · authority | suppress |
