# Relief blankets — part 2 of 2

[Policy and other cases](README.md)

One approved award of 45 blankets; all inputs use blankets at 0 decimal places. One original settled fulfillment, when present, may be partially returned. An outstanding payment or stock issue is reserved against authority. Historical issued and returned amounts are kept even when the net amount is zero. Reviewers can reconstruct this case using the supplied opening facts.

| Case | Opening gross | Opening returns | Opening reserved | Requested event and value | Decision | New net delivered | New reserved | New free authority |
|---|---|---|---|---|---|---|---|---|
| AID-03058 | 36 | 36 | 45 | Request new 1 | Exceeds remaining authority | 0 | 45 | 0 |
| AID-03059 | 36 | 36 | 45 | Request new 15 | Exceeds remaining authority | 0 | 45 | 0 |
| AID-03060 | 36 | 36 | 45 | Confirm pending 45 | Settle original once | 45 | 0 | 0 |
| AID-03061 | 36 | 36 | 45 | Fail pending 45 | Release pending reservation | 0 | 0 | 45 |
| AID-03062 | 36 | 36 | 45 | Replay settled 36 | Original receipt; no new effect | 0 | 45 | 0 |
| AID-03063 | 45 | 0 | 0 | Request new 1 | Exceeds remaining authority | 45 | 0 | 0 |
| AID-03064 | 45 | 0 | 0 | Request new 15 | Exceeds remaining authority | 45 | 0 | 0 |
| AID-03065 | 45 | 0 | 0 | Replay settled 45 | Original receipt; no new effect | 45 | 0 | 0 |
| AID-03066 | 45 | 0 | 0 | Record return 1 | Apply linked return once | 44 | 0 | 1 |
| AID-03067 | 45 | 0 | 0 | Record return 23 | Apply linked return once | 22 | 0 | 23 |
| AID-03068 | 45 | 0 | 0 | Record return 45 | Apply linked return once | 0 | 0 | 45 |
| AID-03069 | 45 | 0 | 0 | Record return 46 | Return exceeds net fulfillment | 45 | 0 | 0 |
| AID-03070 | 45 | 1 | 0 | Request new 1 | Reserve once | 44 | 1 | 0 |
| AID-03071 | 45 | 1 | 0 | Request new 2 | Exceeds remaining authority | 44 | 0 | 1 |
| AID-03072 | 45 | 1 | 0 | Request new 15 | Exceeds remaining authority | 44 | 0 | 1 |
| AID-03073 | 45 | 1 | 0 | Replay settled 45 | Original receipt; no new effect | 44 | 0 | 1 |
| AID-03074 | 45 | 1 | 0 | Record return 1 | Apply linked return once | 43 | 0 | 2 |
| AID-03075 | 45 | 1 | 0 | Record return 22 | Apply linked return once | 22 | 0 | 23 |
| AID-03076 | 45 | 1 | 0 | Record return 44 | Apply linked return once | 0 | 0 | 45 |
| AID-03077 | 45 | 1 | 0 | Record return 45 | Return exceeds net fulfillment | 44 | 0 | 1 |
| AID-03078 | 45 | 1 | 1 | Request new 1 | Exceeds remaining authority | 44 | 1 | 0 |
| AID-03079 | 45 | 1 | 1 | Request new 15 | Exceeds remaining authority | 44 | 1 | 0 |
| AID-03080 | 45 | 1 | 1 | Confirm pending 1 | Settle original once | 45 | 0 | 0 |
| AID-03081 | 45 | 1 | 1 | Fail pending 1 | Release pending reservation | 44 | 0 | 1 |
| AID-03082 | 45 | 1 | 1 | Replay settled 45 | Original receipt; no new effect | 44 | 1 | 0 |
| AID-03083 | 45 | 1 | 1 | Record return 1 | Apply linked return once | 43 | 1 | 1 |
| AID-03084 | 45 | 1 | 1 | Record return 22 | Apply linked return once | 22 | 1 | 22 |
| AID-03085 | 45 | 1 | 1 | Record return 44 | Apply linked return once | 0 | 1 | 44 |
| AID-03086 | 45 | 1 | 1 | Record return 45 | Return exceeds net fulfillment | 44 | 1 | 0 |
| AID-03087 | 45 | 11 | 0 | Request new 10 | Reserve once | 34 | 10 | 1 |
| AID-03088 | 45 | 11 | 0 | Request new 11 | Reserve once | 34 | 11 | 0 |
| AID-03089 | 45 | 11 | 0 | Request new 12 | Exceeds remaining authority | 34 | 0 | 11 |
| AID-03090 | 45 | 11 | 0 | Request new 15 | Exceeds remaining authority | 34 | 0 | 11 |
| AID-03091 | 45 | 11 | 0 | Replay settled 45 | Original receipt; no new effect | 34 | 0 | 11 |
| AID-03092 | 45 | 11 | 0 | Record return 1 | Apply linked return once | 33 | 0 | 12 |
| AID-03093 | 45 | 11 | 0 | Record return 17 | Apply linked return once | 17 | 0 | 28 |
| AID-03094 | 45 | 11 | 0 | Record return 34 | Apply linked return once | 0 | 0 | 45 |
| AID-03095 | 45 | 11 | 0 | Record return 35 | Return exceeds net fulfillment | 34 | 0 | 11 |
| AID-03096 | 45 | 11 | 4 | Request new 6 | Reserve once | 34 | 10 | 1 |
| AID-03097 | 45 | 11 | 4 | Request new 7 | Reserve once | 34 | 11 | 0 |
| AID-03098 | 45 | 11 | 4 | Request new 8 | Exceeds remaining authority | 34 | 4 | 7 |
| AID-03099 | 45 | 11 | 4 | Request new 15 | Exceeds remaining authority | 34 | 4 | 7 |
| AID-03100 | 45 | 11 | 4 | Confirm pending 4 | Settle original once | 38 | 0 | 7 |
| AID-03101 | 45 | 11 | 4 | Fail pending 4 | Release pending reservation | 34 | 0 | 11 |
| AID-03102 | 45 | 11 | 4 | Replay settled 45 | Original receipt; no new effect | 34 | 4 | 7 |
| AID-03103 | 45 | 11 | 4 | Record return 1 | Apply linked return once | 33 | 4 | 8 |
| AID-03104 | 45 | 11 | 4 | Record return 17 | Apply linked return once | 17 | 4 | 24 |
| AID-03105 | 45 | 11 | 4 | Record return 34 | Apply linked return once | 0 | 4 | 41 |
| AID-03106 | 45 | 11 | 4 | Record return 35 | Return exceeds net fulfillment | 34 | 4 | 7 |
| AID-03107 | 45 | 11 | 11 | Request new 1 | Exceeds remaining authority | 34 | 11 | 0 |
| AID-03108 | 45 | 11 | 11 | Request new 15 | Exceeds remaining authority | 34 | 11 | 0 |
| AID-03109 | 45 | 11 | 11 | Confirm pending 11 | Settle original once | 45 | 0 | 0 |
| AID-03110 | 45 | 11 | 11 | Fail pending 11 | Release pending reservation | 34 | 0 | 11 |
| AID-03111 | 45 | 11 | 11 | Replay settled 45 | Original receipt; no new effect | 34 | 11 | 0 |
| AID-03112 | 45 | 11 | 11 | Record return 1 | Apply linked return once | 33 | 11 | 1 |
| AID-03113 | 45 | 11 | 11 | Record return 17 | Apply linked return once | 17 | 11 | 17 |
| AID-03114 | 45 | 11 | 11 | Record return 34 | Apply linked return once | 0 | 11 | 34 |
| AID-03115 | 45 | 11 | 11 | Record return 35 | Return exceeds net fulfillment | 34 | 11 | 0 |
| AID-03116 | 45 | 45 | 0 | Request new 15 | Reserve once | 0 | 15 | 30 |
| AID-03117 | 45 | 45 | 0 | Request new 44 | Reserve once | 0 | 44 | 1 |
| AID-03118 | 45 | 45 | 0 | Request new 45 | Reserve once | 0 | 45 | 0 |
| AID-03119 | 45 | 45 | 0 | Request new 46 | Exceeds remaining authority | 0 | 0 | 45 |
| AID-03120 | 45 | 45 | 0 | Replay settled 45 | Original receipt; no new effect | 0 | 0 | 45 |
| AID-03121 | 45 | 45 | 18 | Request new 15 | Reserve once | 0 | 33 | 12 |
| AID-03122 | 45 | 45 | 18 | Request new 26 | Reserve once | 0 | 44 | 1 |
| AID-03123 | 45 | 45 | 18 | Request new 27 | Reserve once | 0 | 45 | 0 |
| AID-03124 | 45 | 45 | 18 | Request new 28 | Exceeds remaining authority | 0 | 18 | 27 |
| AID-03125 | 45 | 45 | 18 | Confirm pending 18 | Settle original once | 18 | 0 | 27 |
| AID-03126 | 45 | 45 | 18 | Fail pending 18 | Release pending reservation | 0 | 0 | 45 |
| AID-03127 | 45 | 45 | 18 | Replay settled 45 | Original receipt; no new effect | 0 | 18 | 27 |
| AID-03128 | 45 | 45 | 45 | Request new 1 | Exceeds remaining authority | 0 | 45 | 0 |
| AID-03129 | 45 | 45 | 45 | Request new 15 | Exceeds remaining authority | 0 | 45 | 0 |
| AID-03130 | 45 | 45 | 45 | Confirm pending 45 | Settle original once | 45 | 0 | 0 |
| AID-03131 | 45 | 45 | 45 | Fail pending 45 | Release pending reservation | 0 | 0 | 45 |
| AID-03132 | 45 | 45 | 45 | Replay settled 45 | Original receipt; no new effect | 0 | 45 | 0 |
