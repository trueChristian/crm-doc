# Sensitive appointment, private route required · 1 of 2

[Decision profiles](../README.md) · [Method and other cases](README.md) · [Clerk procedure](../../../handbook/governance/contact-routing.md)

**Given.** Preference order private Telegram → EMAIL → SMS. An approved generic alert may use an individually verified, nonshared channel. A shared address/number must be excluded. A representative must hold purpose-specific authority at handoff. All cases concern one intended person and pass the sender authorization check.

Use the row inputs with this profile. Compare every expected output at the indicated cutoff. Case numbers are local to this profile.

| Case | Email | SMS | Telegram | Post | Capacity | At freeze | Before handoff | At release | Operation |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PRIVATE-0001 | ready | ready | linked | n/a | direct | Telegram direct | unchanged | Telegram direct | preserve disposition |
| PRIVATE-0002 | ready | ready | linked | n/a | representative with authority | Telegram direct | unchanged | Telegram direct | preserve disposition |
| PRIVATE-0003 | ready | ready | linked | n/a | direct | Telegram direct | email unsafe | Telegram direct | preserve disposition |
| PRIVATE-0004 | ready | ready | linked | n/a | representative with authority | Telegram direct | email unsafe | Telegram direct | preserve disposition |
| PRIVATE-0005 | ready | ready | linked | n/a | direct | Telegram direct | SMS opt-out | Telegram direct | preserve disposition |
| PRIVATE-0006 | ready | ready | linked | n/a | representative with authority | Telegram direct | SMS opt-out | Telegram direct | preserve disposition |
| PRIVATE-0007 | ready | ready | linked | n/a | direct | Telegram direct | chat blocked | email | reselect before handoff |
| PRIVATE-0008 | ready | ready | linked | n/a | representative with authority | Telegram direct | chat blocked | email | reselect before handoff |
| PRIVATE-0009 | ready | ready | linked | n/a | direct | Telegram direct | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0010 | ready | ready | linked | n/a | representative with authority | Telegram direct | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0011 | ready | ready | channel member | n/a | direct | email | unchanged | email | preserve disposition |
| PRIVATE-0012 | ready | ready | channel member | n/a | representative with authority | email | unchanged | email | preserve disposition |
| PRIVATE-0013 | ready | ready | channel member | n/a | direct | email | email unsafe | sms | reselect before handoff |
| PRIVATE-0014 | ready | ready | channel member | n/a | representative with authority | email | email unsafe | sms | reselect before handoff |
| PRIVATE-0015 | ready | ready | channel member | n/a | direct | email | SMS opt-out | email | preserve disposition |
| PRIVATE-0016 | ready | ready | channel member | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| PRIVATE-0017 | ready | ready | channel member | n/a | direct | email | chat blocked | email | preserve disposition |
| PRIVATE-0018 | ready | ready | channel member | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| PRIVATE-0019 | ready | ready | channel member | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0020 | ready | ready | channel member | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0021 | ready | ready | unlinked | n/a | direct | email | unchanged | email | preserve disposition |
| PRIVATE-0022 | ready | ready | unlinked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| PRIVATE-0023 | ready | ready | unlinked | n/a | direct | email | email unsafe | sms | reselect before handoff |
| PRIVATE-0024 | ready | ready | unlinked | n/a | representative with authority | email | email unsafe | sms | reselect before handoff |
| PRIVATE-0025 | ready | ready | unlinked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| PRIVATE-0026 | ready | ready | unlinked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| PRIVATE-0027 | ready | ready | unlinked | n/a | direct | email | chat blocked | email | preserve disposition |
| PRIVATE-0028 | ready | ready | unlinked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| PRIVATE-0029 | ready | ready | unlinked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0030 | ready | ready | unlinked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0031 | ready | ready | blocked | n/a | direct | email | unchanged | email | preserve disposition |
| PRIVATE-0032 | ready | ready | blocked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| PRIVATE-0033 | ready | ready | blocked | n/a | direct | email | email unsafe | sms | reselect before handoff |
| PRIVATE-0034 | ready | ready | blocked | n/a | representative with authority | email | email unsafe | sms | reselect before handoff |
| PRIVATE-0035 | ready | ready | blocked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| PRIVATE-0036 | ready | ready | blocked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| PRIVATE-0037 | ready | ready | blocked | n/a | direct | email | chat blocked | email | preserve disposition |
| PRIVATE-0038 | ready | ready | blocked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| PRIVATE-0039 | ready | ready | blocked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0040 | ready | ready | blocked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0041 | ready | shared | linked | n/a | direct | Telegram direct | unchanged | Telegram direct | preserve disposition |
| PRIVATE-0042 | ready | shared | linked | n/a | representative with authority | Telegram direct | unchanged | Telegram direct | preserve disposition |
| PRIVATE-0043 | ready | shared | linked | n/a | direct | Telegram direct | email unsafe | Telegram direct | preserve disposition |
| PRIVATE-0044 | ready | shared | linked | n/a | representative with authority | Telegram direct | email unsafe | Telegram direct | preserve disposition |
| PRIVATE-0045 | ready | shared | linked | n/a | direct | Telegram direct | SMS opt-out | Telegram direct | preserve disposition |
| PRIVATE-0046 | ready | shared | linked | n/a | representative with authority | Telegram direct | SMS opt-out | Telegram direct | preserve disposition |
| PRIVATE-0047 | ready | shared | linked | n/a | direct | Telegram direct | chat blocked | email | reselect before handoff |
| PRIVATE-0048 | ready | shared | linked | n/a | representative with authority | Telegram direct | chat blocked | email | reselect before handoff |
| PRIVATE-0049 | ready | shared | linked | n/a | direct | Telegram direct | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0050 | ready | shared | linked | n/a | representative with authority | Telegram direct | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0051 | ready | shared | channel member | n/a | direct | email | unchanged | email | preserve disposition |
| PRIVATE-0052 | ready | shared | channel member | n/a | representative with authority | email | unchanged | email | preserve disposition |
| PRIVATE-0053 | ready | shared | channel member | n/a | direct | email | email unsafe | no permitted route | hold for resolution |
| PRIVATE-0054 | ready | shared | channel member | n/a | representative with authority | email | email unsafe | no permitted route | hold for resolution |
| PRIVATE-0055 | ready | shared | channel member | n/a | direct | email | SMS opt-out | email | preserve disposition |
| PRIVATE-0056 | ready | shared | channel member | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| PRIVATE-0057 | ready | shared | channel member | n/a | direct | email | chat blocked | email | preserve disposition |
| PRIVATE-0058 | ready | shared | channel member | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| PRIVATE-0059 | ready | shared | channel member | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0060 | ready | shared | channel member | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0061 | ready | shared | unlinked | n/a | direct | email | unchanged | email | preserve disposition |
| PRIVATE-0062 | ready | shared | unlinked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| PRIVATE-0063 | ready | shared | unlinked | n/a | direct | email | email unsafe | no permitted route | hold for resolution |
| PRIVATE-0064 | ready | shared | unlinked | n/a | representative with authority | email | email unsafe | no permitted route | hold for resolution |
| PRIVATE-0065 | ready | shared | unlinked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| PRIVATE-0066 | ready | shared | unlinked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| PRIVATE-0067 | ready | shared | unlinked | n/a | direct | email | chat blocked | email | preserve disposition |
| PRIVATE-0068 | ready | shared | unlinked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| PRIVATE-0069 | ready | shared | unlinked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0070 | ready | shared | unlinked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0071 | ready | shared | blocked | n/a | direct | email | unchanged | email | preserve disposition |
| PRIVATE-0072 | ready | shared | blocked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| PRIVATE-0073 | ready | shared | blocked | n/a | direct | email | email unsafe | no permitted route | hold for resolution |
| PRIVATE-0074 | ready | shared | blocked | n/a | representative with authority | email | email unsafe | no permitted route | hold for resolution |
| PRIVATE-0075 | ready | shared | blocked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| PRIVATE-0076 | ready | shared | blocked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| PRIVATE-0077 | ready | shared | blocked | n/a | direct | email | chat blocked | email | preserve disposition |
| PRIVATE-0078 | ready | shared | blocked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| PRIVATE-0079 | ready | shared | blocked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0080 | ready | shared | blocked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0081 | ready | verified declined | linked | n/a | direct | Telegram direct | unchanged | Telegram direct | preserve disposition |
| PRIVATE-0082 | ready | verified declined | linked | n/a | representative with authority | Telegram direct | unchanged | Telegram direct | preserve disposition |
| PRIVATE-0083 | ready | verified declined | linked | n/a | direct | Telegram direct | email unsafe | Telegram direct | preserve disposition |
| PRIVATE-0084 | ready | verified declined | linked | n/a | representative with authority | Telegram direct | email unsafe | Telegram direct | preserve disposition |
| PRIVATE-0085 | ready | verified declined | linked | n/a | direct | Telegram direct | SMS opt-out | Telegram direct | preserve disposition |
| PRIVATE-0086 | ready | verified declined | linked | n/a | representative with authority | Telegram direct | SMS opt-out | Telegram direct | preserve disposition |
| PRIVATE-0087 | ready | verified declined | linked | n/a | direct | Telegram direct | chat blocked | email | reselect before handoff |
| PRIVATE-0088 | ready | verified declined | linked | n/a | representative with authority | Telegram direct | chat blocked | email | reselect before handoff |
| PRIVATE-0089 | ready | verified declined | linked | n/a | direct | Telegram direct | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0090 | ready | verified declined | linked | n/a | representative with authority | Telegram direct | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0091 | ready | verified declined | channel member | n/a | direct | email | unchanged | email | preserve disposition |
| PRIVATE-0092 | ready | verified declined | channel member | n/a | representative with authority | email | unchanged | email | preserve disposition |
| PRIVATE-0093 | ready | verified declined | channel member | n/a | direct | email | email unsafe | no permitted route | hold for resolution |
| PRIVATE-0094 | ready | verified declined | channel member | n/a | representative with authority | email | email unsafe | no permitted route | hold for resolution |
| PRIVATE-0095 | ready | verified declined | channel member | n/a | direct | email | SMS opt-out | email | preserve disposition |
| PRIVATE-0096 | ready | verified declined | channel member | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| PRIVATE-0097 | ready | verified declined | channel member | n/a | direct | email | chat blocked | email | preserve disposition |
| PRIVATE-0098 | ready | verified declined | channel member | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| PRIVATE-0099 | ready | verified declined | channel member | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0100 | ready | verified declined | channel member | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0101 | ready | verified declined | unlinked | n/a | direct | email | unchanged | email | preserve disposition |
| PRIVATE-0102 | ready | verified declined | unlinked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| PRIVATE-0103 | ready | verified declined | unlinked | n/a | direct | email | email unsafe | no permitted route | hold for resolution |
| PRIVATE-0104 | ready | verified declined | unlinked | n/a | representative with authority | email | email unsafe | no permitted route | hold for resolution |
| PRIVATE-0105 | ready | verified declined | unlinked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| PRIVATE-0106 | ready | verified declined | unlinked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| PRIVATE-0107 | ready | verified declined | unlinked | n/a | direct | email | chat blocked | email | preserve disposition |
| PRIVATE-0108 | ready | verified declined | unlinked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| PRIVATE-0109 | ready | verified declined | unlinked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0110 | ready | verified declined | unlinked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0111 | ready | verified declined | blocked | n/a | direct | email | unchanged | email | preserve disposition |
| PRIVATE-0112 | ready | verified declined | blocked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| PRIVATE-0113 | ready | verified declined | blocked | n/a | direct | email | email unsafe | no permitted route | hold for resolution |
| PRIVATE-0114 | ready | verified declined | blocked | n/a | representative with authority | email | email unsafe | no permitted route | hold for resolution |
| PRIVATE-0115 | ready | verified declined | blocked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| PRIVATE-0116 | ready | verified declined | blocked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| PRIVATE-0117 | ready | verified declined | blocked | n/a | direct | email | chat blocked | email | preserve disposition |
| PRIVATE-0118 | ready | verified declined | blocked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| PRIVATE-0119 | ready | verified declined | blocked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0120 | ready | verified declined | blocked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0121 | ready | unverified | linked | n/a | direct | Telegram direct | unchanged | Telegram direct | preserve disposition |
| PRIVATE-0122 | ready | unverified | linked | n/a | representative with authority | Telegram direct | unchanged | Telegram direct | preserve disposition |
| PRIVATE-0123 | ready | unverified | linked | n/a | direct | Telegram direct | email unsafe | Telegram direct | preserve disposition |
| PRIVATE-0124 | ready | unverified | linked | n/a | representative with authority | Telegram direct | email unsafe | Telegram direct | preserve disposition |
| PRIVATE-0125 | ready | unverified | linked | n/a | direct | Telegram direct | SMS opt-out | Telegram direct | preserve disposition |
| PRIVATE-0126 | ready | unverified | linked | n/a | representative with authority | Telegram direct | SMS opt-out | Telegram direct | preserve disposition |
| PRIVATE-0127 | ready | unverified | linked | n/a | direct | Telegram direct | chat blocked | email | reselect before handoff |
| PRIVATE-0128 | ready | unverified | linked | n/a | representative with authority | Telegram direct | chat blocked | email | reselect before handoff |
| PRIVATE-0129 | ready | unverified | linked | n/a | direct | Telegram direct | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0130 | ready | unverified | linked | n/a | representative with authority | Telegram direct | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0131 | ready | unverified | channel member | n/a | direct | email | unchanged | email | preserve disposition |
| PRIVATE-0132 | ready | unverified | channel member | n/a | representative with authority | email | unchanged | email | preserve disposition |
| PRIVATE-0133 | ready | unverified | channel member | n/a | direct | email | email unsafe | no permitted route | hold for resolution |
| PRIVATE-0134 | ready | unverified | channel member | n/a | representative with authority | email | email unsafe | no permitted route | hold for resolution |
| PRIVATE-0135 | ready | unverified | channel member | n/a | direct | email | SMS opt-out | email | preserve disposition |
| PRIVATE-0136 | ready | unverified | channel member | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| PRIVATE-0137 | ready | unverified | channel member | n/a | direct | email | chat blocked | email | preserve disposition |
| PRIVATE-0138 | ready | unverified | channel member | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| PRIVATE-0139 | ready | unverified | channel member | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0140 | ready | unverified | channel member | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0141 | ready | unverified | unlinked | n/a | direct | email | unchanged | email | preserve disposition |
| PRIVATE-0142 | ready | unverified | unlinked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| PRIVATE-0143 | ready | unverified | unlinked | n/a | direct | email | email unsafe | no permitted route | hold for resolution |
| PRIVATE-0144 | ready | unverified | unlinked | n/a | representative with authority | email | email unsafe | no permitted route | hold for resolution |
| PRIVATE-0145 | ready | unverified | unlinked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| PRIVATE-0146 | ready | unverified | unlinked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| PRIVATE-0147 | ready | unverified | unlinked | n/a | direct | email | chat blocked | email | preserve disposition |
| PRIVATE-0148 | ready | unverified | unlinked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| PRIVATE-0149 | ready | unverified | unlinked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0150 | ready | unverified | unlinked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0151 | ready | unverified | blocked | n/a | direct | email | unchanged | email | preserve disposition |
| PRIVATE-0152 | ready | unverified | blocked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| PRIVATE-0153 | ready | unverified | blocked | n/a | direct | email | email unsafe | no permitted route | hold for resolution |
| PRIVATE-0154 | ready | unverified | blocked | n/a | representative with authority | email | email unsafe | no permitted route | hold for resolution |
| PRIVATE-0155 | ready | unverified | blocked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| PRIVATE-0156 | ready | unverified | blocked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| PRIVATE-0157 | ready | unverified | blocked | n/a | direct | email | chat blocked | email | preserve disposition |
| PRIVATE-0158 | ready | unverified | blocked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| PRIVATE-0159 | ready | unverified | blocked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0160 | ready | unverified | blocked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0161 | ready | none | linked | n/a | direct | Telegram direct | unchanged | Telegram direct | preserve disposition |
| PRIVATE-0162 | ready | none | linked | n/a | representative with authority | Telegram direct | unchanged | Telegram direct | preserve disposition |
| PRIVATE-0163 | ready | none | linked | n/a | direct | Telegram direct | email unsafe | Telegram direct | preserve disposition |
| PRIVATE-0164 | ready | none | linked | n/a | representative with authority | Telegram direct | email unsafe | Telegram direct | preserve disposition |
| PRIVATE-0165 | ready | none | linked | n/a | direct | Telegram direct | SMS opt-out | Telegram direct | preserve disposition |
| PRIVATE-0166 | ready | none | linked | n/a | representative with authority | Telegram direct | SMS opt-out | Telegram direct | preserve disposition |
| PRIVATE-0167 | ready | none | linked | n/a | direct | Telegram direct | chat blocked | email | reselect before handoff |
| PRIVATE-0168 | ready | none | linked | n/a | representative with authority | Telegram direct | chat blocked | email | reselect before handoff |
| PRIVATE-0169 | ready | none | linked | n/a | direct | Telegram direct | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0170 | ready | none | linked | n/a | representative with authority | Telegram direct | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0171 | ready | none | channel member | n/a | direct | email | unchanged | email | preserve disposition |
| PRIVATE-0172 | ready | none | channel member | n/a | representative with authority | email | unchanged | email | preserve disposition |
| PRIVATE-0173 | ready | none | channel member | n/a | direct | email | email unsafe | no permitted route | hold for resolution |
| PRIVATE-0174 | ready | none | channel member | n/a | representative with authority | email | email unsafe | no permitted route | hold for resolution |
| PRIVATE-0175 | ready | none | channel member | n/a | direct | email | SMS opt-out | email | preserve disposition |
| PRIVATE-0176 | ready | none | channel member | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| PRIVATE-0177 | ready | none | channel member | n/a | direct | email | chat blocked | email | preserve disposition |
| PRIVATE-0178 | ready | none | channel member | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| PRIVATE-0179 | ready | none | channel member | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0180 | ready | none | channel member | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0181 | ready | none | unlinked | n/a | direct | email | unchanged | email | preserve disposition |
| PRIVATE-0182 | ready | none | unlinked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| PRIVATE-0183 | ready | none | unlinked | n/a | direct | email | email unsafe | no permitted route | hold for resolution |
| PRIVATE-0184 | ready | none | unlinked | n/a | representative with authority | email | email unsafe | no permitted route | hold for resolution |
| PRIVATE-0185 | ready | none | unlinked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| PRIVATE-0186 | ready | none | unlinked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| PRIVATE-0187 | ready | none | unlinked | n/a | direct | email | chat blocked | email | preserve disposition |
| PRIVATE-0188 | ready | none | unlinked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| PRIVATE-0189 | ready | none | unlinked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0190 | ready | none | unlinked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0191 | ready | none | blocked | n/a | direct | email | unchanged | email | preserve disposition |
| PRIVATE-0192 | ready | none | blocked | n/a | representative with authority | email | unchanged | email | preserve disposition |
| PRIVATE-0193 | ready | none | blocked | n/a | direct | email | email unsafe | no permitted route | hold for resolution |
| PRIVATE-0194 | ready | none | blocked | n/a | representative with authority | email | email unsafe | no permitted route | hold for resolution |
| PRIVATE-0195 | ready | none | blocked | n/a | direct | email | SMS opt-out | email | preserve disposition |
| PRIVATE-0196 | ready | none | blocked | n/a | representative with authority | email | SMS opt-out | email | preserve disposition |
| PRIVATE-0197 | ready | none | blocked | n/a | direct | email | chat blocked | email | preserve disposition |
| PRIVATE-0198 | ready | none | blocked | n/a | representative with authority | email | chat blocked | email | preserve disposition |
| PRIVATE-0199 | ready | none | blocked | n/a | direct | email | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0200 | ready | none | blocked | n/a | representative with authority | email | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0201 | shared | ready | linked | n/a | direct | Telegram direct | unchanged | Telegram direct | preserve disposition |
| PRIVATE-0202 | shared | ready | linked | n/a | representative with authority | Telegram direct | unchanged | Telegram direct | preserve disposition |
| PRIVATE-0203 | shared | ready | linked | n/a | direct | Telegram direct | email unsafe | Telegram direct | preserve disposition |
| PRIVATE-0204 | shared | ready | linked | n/a | representative with authority | Telegram direct | email unsafe | Telegram direct | preserve disposition |
| PRIVATE-0205 | shared | ready | linked | n/a | direct | Telegram direct | SMS opt-out | Telegram direct | preserve disposition |
| PRIVATE-0206 | shared | ready | linked | n/a | representative with authority | Telegram direct | SMS opt-out | Telegram direct | preserve disposition |
| PRIVATE-0207 | shared | ready | linked | n/a | direct | Telegram direct | chat blocked | sms | reselect before handoff |
| PRIVATE-0208 | shared | ready | linked | n/a | representative with authority | Telegram direct | chat blocked | sms | reselect before handoff |
| PRIVATE-0209 | shared | ready | linked | n/a | direct | Telegram direct | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0210 | shared | ready | linked | n/a | representative with authority | Telegram direct | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0211 | shared | ready | channel member | n/a | direct | sms | unchanged | sms | preserve disposition |
| PRIVATE-0212 | shared | ready | channel member | n/a | representative with authority | sms | unchanged | sms | preserve disposition |
| PRIVATE-0213 | shared | ready | channel member | n/a | direct | sms | email unsafe | sms | preserve disposition |
| PRIVATE-0214 | shared | ready | channel member | n/a | representative with authority | sms | email unsafe | sms | preserve disposition |
| PRIVATE-0215 | shared | ready | channel member | n/a | direct | sms | SMS opt-out | no permitted route | hold for resolution |
| PRIVATE-0216 | shared | ready | channel member | n/a | representative with authority | sms | SMS opt-out | no permitted route | hold for resolution |
| PRIVATE-0217 | shared | ready | channel member | n/a | direct | sms | chat blocked | sms | preserve disposition |
| PRIVATE-0218 | shared | ready | channel member | n/a | representative with authority | sms | chat blocked | sms | preserve disposition |
| PRIVATE-0219 | shared | ready | channel member | n/a | direct | sms | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0220 | shared | ready | channel member | n/a | representative with authority | sms | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0221 | shared | ready | unlinked | n/a | direct | sms | unchanged | sms | preserve disposition |
| PRIVATE-0222 | shared | ready | unlinked | n/a | representative with authority | sms | unchanged | sms | preserve disposition |
| PRIVATE-0223 | shared | ready | unlinked | n/a | direct | sms | email unsafe | sms | preserve disposition |
| PRIVATE-0224 | shared | ready | unlinked | n/a | representative with authority | sms | email unsafe | sms | preserve disposition |
| PRIVATE-0225 | shared | ready | unlinked | n/a | direct | sms | SMS opt-out | no permitted route | hold for resolution |
| PRIVATE-0226 | shared | ready | unlinked | n/a | representative with authority | sms | SMS opt-out | no permitted route | hold for resolution |
| PRIVATE-0227 | shared | ready | unlinked | n/a | direct | sms | chat blocked | sms | preserve disposition |
| PRIVATE-0228 | shared | ready | unlinked | n/a | representative with authority | sms | chat blocked | sms | preserve disposition |
| PRIVATE-0229 | shared | ready | unlinked | n/a | direct | sms | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0230 | shared | ready | unlinked | n/a | representative with authority | sms | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0231 | shared | ready | blocked | n/a | direct | sms | unchanged | sms | preserve disposition |
| PRIVATE-0232 | shared | ready | blocked | n/a | representative with authority | sms | unchanged | sms | preserve disposition |
| PRIVATE-0233 | shared | ready | blocked | n/a | direct | sms | email unsafe | sms | preserve disposition |
| PRIVATE-0234 | shared | ready | blocked | n/a | representative with authority | sms | email unsafe | sms | preserve disposition |
| PRIVATE-0235 | shared | ready | blocked | n/a | direct | sms | SMS opt-out | no permitted route | hold for resolution |
| PRIVATE-0236 | shared | ready | blocked | n/a | representative with authority | sms | SMS opt-out | no permitted route | hold for resolution |
| PRIVATE-0237 | shared | ready | blocked | n/a | direct | sms | chat blocked | sms | preserve disposition |
| PRIVATE-0238 | shared | ready | blocked | n/a | representative with authority | sms | chat blocked | sms | preserve disposition |
| PRIVATE-0239 | shared | ready | blocked | n/a | direct | sms | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0240 | shared | ready | blocked | n/a | representative with authority | sms | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0241 | shared | shared | linked | n/a | direct | Telegram direct | unchanged | Telegram direct | preserve disposition |
| PRIVATE-0242 | shared | shared | linked | n/a | representative with authority | Telegram direct | unchanged | Telegram direct | preserve disposition |
| PRIVATE-0243 | shared | shared | linked | n/a | direct | Telegram direct | email unsafe | Telegram direct | preserve disposition |
| PRIVATE-0244 | shared | shared | linked | n/a | representative with authority | Telegram direct | email unsafe | Telegram direct | preserve disposition |
| PRIVATE-0245 | shared | shared | linked | n/a | direct | Telegram direct | SMS opt-out | Telegram direct | preserve disposition |
| PRIVATE-0246 | shared | shared | linked | n/a | representative with authority | Telegram direct | SMS opt-out | Telegram direct | preserve disposition |
| PRIVATE-0247 | shared | shared | linked | n/a | direct | Telegram direct | chat blocked | no permitted route | hold for resolution |
| PRIVATE-0248 | shared | shared | linked | n/a | representative with authority | Telegram direct | chat blocked | no permitted route | hold for resolution |
| PRIVATE-0249 | shared | shared | linked | n/a | direct | Telegram direct | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0250 | shared | shared | linked | n/a | representative with authority | Telegram direct | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0251 | shared | shared | channel member | n/a | direct | no permitted route | unchanged | no permitted route | preserve disposition |
| PRIVATE-0252 | shared | shared | channel member | n/a | representative with authority | no permitted route | unchanged | no permitted route | preserve disposition |
| PRIVATE-0253 | shared | shared | unlinked | n/a | direct | no permitted route | unchanged | no permitted route | preserve disposition |
| PRIVATE-0254 | shared | shared | unlinked | n/a | representative with authority | no permitted route | unchanged | no permitted route | preserve disposition |
| PRIVATE-0255 | shared | shared | blocked | n/a | direct | no permitted route | unchanged | no permitted route | preserve disposition |
| PRIVATE-0256 | shared | shared | blocked | n/a | representative with authority | no permitted route | unchanged | no permitted route | preserve disposition |
| PRIVATE-0257 | shared | verified declined | linked | n/a | direct | Telegram direct | unchanged | Telegram direct | preserve disposition |
| PRIVATE-0258 | shared | verified declined | linked | n/a | representative with authority | Telegram direct | unchanged | Telegram direct | preserve disposition |
| PRIVATE-0259 | shared | verified declined | linked | n/a | direct | Telegram direct | email unsafe | Telegram direct | preserve disposition |
| PRIVATE-0260 | shared | verified declined | linked | n/a | representative with authority | Telegram direct | email unsafe | Telegram direct | preserve disposition |
| PRIVATE-0261 | shared | verified declined | linked | n/a | direct | Telegram direct | SMS opt-out | Telegram direct | preserve disposition |
| PRIVATE-0262 | shared | verified declined | linked | n/a | representative with authority | Telegram direct | SMS opt-out | Telegram direct | preserve disposition |
| PRIVATE-0263 | shared | verified declined | linked | n/a | direct | Telegram direct | chat blocked | no permitted route | hold for resolution |
| PRIVATE-0264 | shared | verified declined | linked | n/a | representative with authority | Telegram direct | chat blocked | no permitted route | hold for resolution |
| PRIVATE-0265 | shared | verified declined | linked | n/a | direct | Telegram direct | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0266 | shared | verified declined | linked | n/a | representative with authority | Telegram direct | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0267 | shared | verified declined | channel member | n/a | direct | no permitted route | unchanged | no permitted route | preserve disposition |
| PRIVATE-0268 | shared | verified declined | channel member | n/a | representative with authority | no permitted route | unchanged | no permitted route | preserve disposition |
| PRIVATE-0269 | shared | verified declined | unlinked | n/a | direct | no permitted route | unchanged | no permitted route | preserve disposition |
| PRIVATE-0270 | shared | verified declined | unlinked | n/a | representative with authority | no permitted route | unchanged | no permitted route | preserve disposition |
| PRIVATE-0271 | shared | verified declined | blocked | n/a | direct | no permitted route | unchanged | no permitted route | preserve disposition |
| PRIVATE-0272 | shared | verified declined | blocked | n/a | representative with authority | no permitted route | unchanged | no permitted route | preserve disposition |
| PRIVATE-0273 | shared | unverified | linked | n/a | direct | Telegram direct | unchanged | Telegram direct | preserve disposition |
| PRIVATE-0274 | shared | unverified | linked | n/a | representative with authority | Telegram direct | unchanged | Telegram direct | preserve disposition |
| PRIVATE-0275 | shared | unverified | linked | n/a | direct | Telegram direct | email unsafe | Telegram direct | preserve disposition |
| PRIVATE-0276 | shared | unverified | linked | n/a | representative with authority | Telegram direct | email unsafe | Telegram direct | preserve disposition |
| PRIVATE-0277 | shared | unverified | linked | n/a | direct | Telegram direct | SMS opt-out | Telegram direct | preserve disposition |
| PRIVATE-0278 | shared | unverified | linked | n/a | representative with authority | Telegram direct | SMS opt-out | Telegram direct | preserve disposition |
| PRIVATE-0279 | shared | unverified | linked | n/a | direct | Telegram direct | chat blocked | no permitted route | hold for resolution |
| PRIVATE-0280 | shared | unverified | linked | n/a | representative with authority | Telegram direct | chat blocked | no permitted route | hold for resolution |
| PRIVATE-0281 | shared | unverified | linked | n/a | direct | Telegram direct | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0282 | shared | unverified | linked | n/a | representative with authority | Telegram direct | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0283 | shared | unverified | channel member | n/a | direct | no permitted route | unchanged | no permitted route | preserve disposition |
| PRIVATE-0284 | shared | unverified | channel member | n/a | representative with authority | no permitted route | unchanged | no permitted route | preserve disposition |
| PRIVATE-0285 | shared | unverified | unlinked | n/a | direct | no permitted route | unchanged | no permitted route | preserve disposition |
| PRIVATE-0286 | shared | unverified | unlinked | n/a | representative with authority | no permitted route | unchanged | no permitted route | preserve disposition |
| PRIVATE-0287 | shared | unverified | blocked | n/a | direct | no permitted route | unchanged | no permitted route | preserve disposition |
| PRIVATE-0288 | shared | unverified | blocked | n/a | representative with authority | no permitted route | unchanged | no permitted route | preserve disposition |
| PRIVATE-0289 | shared | none | linked | n/a | direct | Telegram direct | unchanged | Telegram direct | preserve disposition |
| PRIVATE-0290 | shared | none | linked | n/a | representative with authority | Telegram direct | unchanged | Telegram direct | preserve disposition |
| PRIVATE-0291 | shared | none | linked | n/a | direct | Telegram direct | email unsafe | Telegram direct | preserve disposition |
| PRIVATE-0292 | shared | none | linked | n/a | representative with authority | Telegram direct | email unsafe | Telegram direct | preserve disposition |
| PRIVATE-0293 | shared | none | linked | n/a | direct | Telegram direct | SMS opt-out | Telegram direct | preserve disposition |
| PRIVATE-0294 | shared | none | linked | n/a | representative with authority | Telegram direct | SMS opt-out | Telegram direct | preserve disposition |
| PRIVATE-0295 | shared | none | linked | n/a | direct | Telegram direct | chat blocked | no permitted route | hold for resolution |
| PRIVATE-0296 | shared | none | linked | n/a | representative with authority | Telegram direct | chat blocked | no permitted route | hold for resolution |
| PRIVATE-0297 | shared | none | linked | n/a | direct | Telegram direct | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0298 | shared | none | linked | n/a | representative with authority | Telegram direct | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0299 | shared | none | channel member | n/a | direct | no permitted route | unchanged | no permitted route | preserve disposition |
| PRIVATE-0300 | shared | none | channel member | n/a | representative with authority | no permitted route | unchanged | no permitted route | preserve disposition |
| PRIVATE-0301 | shared | none | unlinked | n/a | direct | no permitted route | unchanged | no permitted route | preserve disposition |
| PRIVATE-0302 | shared | none | unlinked | n/a | representative with authority | no permitted route | unchanged | no permitted route | preserve disposition |
| PRIVATE-0303 | shared | none | blocked | n/a | direct | no permitted route | unchanged | no permitted route | preserve disposition |
| PRIVATE-0304 | shared | none | blocked | n/a | representative with authority | no permitted route | unchanged | no permitted route | preserve disposition |
| PRIVATE-0305 | verified declined | ready | linked | n/a | direct | Telegram direct | unchanged | Telegram direct | preserve disposition |
| PRIVATE-0306 | verified declined | ready | linked | n/a | representative with authority | Telegram direct | unchanged | Telegram direct | preserve disposition |
| PRIVATE-0307 | verified declined | ready | linked | n/a | direct | Telegram direct | email unsafe | Telegram direct | preserve disposition |
| PRIVATE-0308 | verified declined | ready | linked | n/a | representative with authority | Telegram direct | email unsafe | Telegram direct | preserve disposition |
| PRIVATE-0309 | verified declined | ready | linked | n/a | direct | Telegram direct | SMS opt-out | Telegram direct | preserve disposition |
| PRIVATE-0310 | verified declined | ready | linked | n/a | representative with authority | Telegram direct | SMS opt-out | Telegram direct | preserve disposition |
| PRIVATE-0311 | verified declined | ready | linked | n/a | direct | Telegram direct | chat blocked | sms | reselect before handoff |
| PRIVATE-0312 | verified declined | ready | linked | n/a | representative with authority | Telegram direct | chat blocked | sms | reselect before handoff |
| PRIVATE-0313 | verified declined | ready | linked | n/a | direct | Telegram direct | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0314 | verified declined | ready | linked | n/a | representative with authority | Telegram direct | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0315 | verified declined | ready | channel member | n/a | direct | sms | unchanged | sms | preserve disposition |
| PRIVATE-0316 | verified declined | ready | channel member | n/a | representative with authority | sms | unchanged | sms | preserve disposition |
| PRIVATE-0317 | verified declined | ready | channel member | n/a | direct | sms | email unsafe | sms | preserve disposition |
| PRIVATE-0318 | verified declined | ready | channel member | n/a | representative with authority | sms | email unsafe | sms | preserve disposition |
| PRIVATE-0319 | verified declined | ready | channel member | n/a | direct | sms | SMS opt-out | no permitted route | hold for resolution |
| PRIVATE-0320 | verified declined | ready | channel member | n/a | representative with authority | sms | SMS opt-out | no permitted route | hold for resolution |
| PRIVATE-0321 | verified declined | ready | channel member | n/a | direct | sms | chat blocked | sms | preserve disposition |
| PRIVATE-0322 | verified declined | ready | channel member | n/a | representative with authority | sms | chat blocked | sms | preserve disposition |
| PRIVATE-0323 | verified declined | ready | channel member | n/a | direct | sms | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0324 | verified declined | ready | channel member | n/a | representative with authority | sms | recipient out of scope | exclude · authority | suppress |
| PRIVATE-0325 | verified declined | ready | unlinked | n/a | direct | sms | unchanged | sms | preserve disposition |
