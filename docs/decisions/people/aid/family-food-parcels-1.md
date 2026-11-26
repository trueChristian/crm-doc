# Family food parcels — part 1 of 2

[Policy and other cases](README.md)

One approved award of 24 parcels; all inputs use parcels at 0 decimal places. One original settled fulfillment, when present, may be partially returned. An outstanding payment or stock issue is reserved against authority. Historical issued and returned amounts are kept even when the net amount is zero. Reviewers can reconstruct this case using the supplied opening facts.

| Case | Opening gross | Opening returns | Opening reserved | Requested event and value | Decision | New net delivered | New reserved | New free authority |
|---|---|---|---|---|---|---|---|---|
| AID-01981 | 0 | 0 | 0 | Request new 8 | Reserve once | 0 | 8 | 16 |
| AID-01982 | 0 | 0 | 0 | Request new 23 | Reserve once | 0 | 23 | 1 |
| AID-01983 | 0 | 0 | 0 | Request new 24 | Reserve once | 0 | 24 | 0 |
| AID-01984 | 0 | 0 | 0 | Request new 25 | Exceeds remaining authority | 0 | 0 | 24 |
| AID-01985 | 0 | 0 | 10 | Request new 8 | Reserve once | 0 | 18 | 6 |
| AID-01986 | 0 | 0 | 10 | Request new 13 | Reserve once | 0 | 23 | 1 |
| AID-01987 | 0 | 0 | 10 | Request new 14 | Reserve once | 0 | 24 | 0 |
| AID-01988 | 0 | 0 | 10 | Request new 15 | Exceeds remaining authority | 0 | 10 | 14 |
| AID-01989 | 0 | 0 | 10 | Confirm pending 10 | Settle original once | 10 | 0 | 14 |
| AID-01990 | 0 | 0 | 10 | Fail pending 10 | Release pending reservation | 0 | 0 | 24 |
| AID-01991 | 0 | 0 | 24 | Request new 1 | Exceeds remaining authority | 0 | 24 | 0 |
| AID-01992 | 0 | 0 | 24 | Request new 8 | Exceeds remaining authority | 0 | 24 | 0 |
| AID-01993 | 0 | 0 | 24 | Confirm pending 24 | Settle original once | 24 | 0 | 0 |
| AID-01994 | 0 | 0 | 24 | Fail pending 24 | Release pending reservation | 0 | 0 | 24 |
| AID-01995 | 5 | 0 | 0 | Request new 8 | Reserve once | 5 | 8 | 11 |
| AID-01996 | 5 | 0 | 0 | Request new 18 | Reserve once | 5 | 18 | 1 |
| AID-01997 | 5 | 0 | 0 | Request new 19 | Reserve once | 5 | 19 | 0 |
| AID-01998 | 5 | 0 | 0 | Request new 20 | Exceeds remaining authority | 5 | 0 | 19 |
| AID-01999 | 5 | 0 | 0 | Replay settled 5 | Original receipt; no new effect | 5 | 0 | 19 |
| AID-02000 | 5 | 0 | 0 | Record return 1 | Apply linked return once | 4 | 0 | 20 |
| AID-02001 | 5 | 0 | 0 | Record return 3 | Apply linked return once | 2 | 0 | 22 |
| AID-02002 | 5 | 0 | 0 | Record return 5 | Apply linked return once | 0 | 0 | 24 |
| AID-02003 | 5 | 0 | 0 | Record return 6 | Return exceeds net fulfillment | 5 | 0 | 19 |
| AID-02004 | 5 | 0 | 8 | Request new 8 | Reserve once | 5 | 16 | 3 |
| AID-02005 | 5 | 0 | 8 | Request new 10 | Reserve once | 5 | 18 | 1 |
| AID-02006 | 5 | 0 | 8 | Request new 11 | Reserve once | 5 | 19 | 0 |
| AID-02007 | 5 | 0 | 8 | Request new 12 | Exceeds remaining authority | 5 | 8 | 11 |
| AID-02008 | 5 | 0 | 8 | Confirm pending 8 | Settle original once | 13 | 0 | 11 |
| AID-02009 | 5 | 0 | 8 | Fail pending 8 | Release pending reservation | 5 | 0 | 19 |
| AID-02010 | 5 | 0 | 8 | Replay settled 5 | Original receipt; no new effect | 5 | 8 | 11 |
| AID-02011 | 5 | 0 | 8 | Record return 1 | Apply linked return once | 4 | 8 | 12 |
| AID-02012 | 5 | 0 | 8 | Record return 3 | Apply linked return once | 2 | 8 | 14 |
| AID-02013 | 5 | 0 | 8 | Record return 5 | Apply linked return once | 0 | 8 | 16 |
| AID-02014 | 5 | 0 | 8 | Record return 6 | Return exceeds net fulfillment | 5 | 8 | 11 |
| AID-02015 | 5 | 0 | 19 | Request new 1 | Exceeds remaining authority | 5 | 19 | 0 |
| AID-02016 | 5 | 0 | 19 | Request new 8 | Exceeds remaining authority | 5 | 19 | 0 |
| AID-02017 | 5 | 0 | 19 | Confirm pending 19 | Settle original once | 24 | 0 | 0 |
| AID-02018 | 5 | 0 | 19 | Fail pending 19 | Release pending reservation | 5 | 0 | 19 |
| AID-02019 | 5 | 0 | 19 | Replay settled 5 | Original receipt; no new effect | 5 | 19 | 0 |
| AID-02020 | 5 | 0 | 19 | Record return 1 | Apply linked return once | 4 | 19 | 1 |
| AID-02021 | 5 | 0 | 19 | Record return 3 | Apply linked return once | 2 | 19 | 3 |
| AID-02022 | 5 | 0 | 19 | Record return 5 | Apply linked return once | 0 | 19 | 5 |
| AID-02023 | 5 | 0 | 19 | Record return 6 | Return exceeds net fulfillment | 5 | 19 | 0 |
| AID-02024 | 5 | 1 | 0 | Request new 8 | Reserve once | 4 | 8 | 12 |
| AID-02025 | 5 | 1 | 0 | Request new 19 | Reserve once | 4 | 19 | 1 |
| AID-02026 | 5 | 1 | 0 | Request new 20 | Reserve once | 4 | 20 | 0 |
| AID-02027 | 5 | 1 | 0 | Request new 21 | Exceeds remaining authority | 4 | 0 | 20 |
| AID-02028 | 5 | 1 | 0 | Replay settled 5 | Original receipt; no new effect | 4 | 0 | 20 |
| AID-02029 | 5 | 1 | 0 | Record return 1 | Apply linked return once | 3 | 0 | 21 |
| AID-02030 | 5 | 1 | 0 | Record return 2 | Apply linked return once | 2 | 0 | 22 |
| AID-02031 | 5 | 1 | 0 | Record return 4 | Apply linked return once | 0 | 0 | 24 |
| AID-02032 | 5 | 1 | 0 | Record return 5 | Return exceeds net fulfillment | 4 | 0 | 20 |
| AID-02033 | 5 | 1 | 8 | Request new 8 | Reserve once | 4 | 16 | 4 |
| AID-02034 | 5 | 1 | 8 | Request new 11 | Reserve once | 4 | 19 | 1 |
| AID-02035 | 5 | 1 | 8 | Request new 12 | Reserve once | 4 | 20 | 0 |
| AID-02036 | 5 | 1 | 8 | Request new 13 | Exceeds remaining authority | 4 | 8 | 12 |
| AID-02037 | 5 | 1 | 8 | Confirm pending 8 | Settle original once | 12 | 0 | 12 |
| AID-02038 | 5 | 1 | 8 | Fail pending 8 | Release pending reservation | 4 | 0 | 20 |
| AID-02039 | 5 | 1 | 8 | Replay settled 5 | Original receipt; no new effect | 4 | 8 | 12 |
| AID-02040 | 5 | 1 | 8 | Record return 1 | Apply linked return once | 3 | 8 | 13 |
| AID-02041 | 5 | 1 | 8 | Record return 2 | Apply linked return once | 2 | 8 | 14 |
| AID-02042 | 5 | 1 | 8 | Record return 4 | Apply linked return once | 0 | 8 | 16 |
| AID-02043 | 5 | 1 | 8 | Record return 5 | Return exceeds net fulfillment | 4 | 8 | 12 |
| AID-02044 | 5 | 1 | 20 | Request new 1 | Exceeds remaining authority | 4 | 20 | 0 |
| AID-02045 | 5 | 1 | 20 | Request new 8 | Exceeds remaining authority | 4 | 20 | 0 |
| AID-02046 | 5 | 1 | 20 | Confirm pending 20 | Settle original once | 24 | 0 | 0 |
| AID-02047 | 5 | 1 | 20 | Fail pending 20 | Release pending reservation | 4 | 0 | 20 |
| AID-02048 | 5 | 1 | 20 | Replay settled 5 | Original receipt; no new effect | 4 | 20 | 0 |
| AID-02049 | 5 | 1 | 20 | Record return 1 | Apply linked return once | 3 | 20 | 1 |
| AID-02050 | 5 | 1 | 20 | Record return 2 | Apply linked return once | 2 | 20 | 2 |
| AID-02051 | 5 | 1 | 20 | Record return 4 | Apply linked return once | 0 | 20 | 4 |
| AID-02052 | 5 | 1 | 20 | Record return 5 | Return exceeds net fulfillment | 4 | 20 | 0 |
| AID-02053 | 5 | 5 | 0 | Request new 8 | Reserve once | 0 | 8 | 16 |
| AID-02054 | 5 | 5 | 0 | Request new 23 | Reserve once | 0 | 23 | 1 |
| AID-02055 | 5 | 5 | 0 | Request new 24 | Reserve once | 0 | 24 | 0 |
| AID-02056 | 5 | 5 | 0 | Request new 25 | Exceeds remaining authority | 0 | 0 | 24 |
| AID-02057 | 5 | 5 | 0 | Replay settled 5 | Original receipt; no new effect | 0 | 0 | 24 |
| AID-02058 | 5 | 5 | 10 | Request new 8 | Reserve once | 0 | 18 | 6 |
| AID-02059 | 5 | 5 | 10 | Request new 13 | Reserve once | 0 | 23 | 1 |
| AID-02060 | 5 | 5 | 10 | Request new 14 | Reserve once | 0 | 24 | 0 |
| AID-02061 | 5 | 5 | 10 | Request new 15 | Exceeds remaining authority | 0 | 10 | 14 |
| AID-02062 | 5 | 5 | 10 | Confirm pending 10 | Settle original once | 10 | 0 | 14 |
| AID-02063 | 5 | 5 | 10 | Fail pending 10 | Release pending reservation | 0 | 0 | 24 |
| AID-02064 | 5 | 5 | 10 | Replay settled 5 | Original receipt; no new effect | 0 | 10 | 14 |
| AID-02065 | 5 | 5 | 24 | Request new 1 | Exceeds remaining authority | 0 | 24 | 0 |
| AID-02066 | 5 | 5 | 24 | Request new 8 | Exceeds remaining authority | 0 | 24 | 0 |
| AID-02067 | 5 | 5 | 24 | Confirm pending 24 | Settle original once | 24 | 0 | 0 |
| AID-02068 | 5 | 5 | 24 | Fail pending 24 | Release pending reservation | 0 | 0 | 24 |
| AID-02069 | 5 | 5 | 24 | Replay settled 5 | Original receipt; no new effect | 0 | 24 | 0 |
| AID-02070 | 12 | 0 | 0 | Request new 8 | Reserve once | 12 | 8 | 4 |
| AID-02071 | 12 | 0 | 0 | Request new 11 | Reserve once | 12 | 11 | 1 |
| AID-02072 | 12 | 0 | 0 | Request new 12 | Reserve once | 12 | 12 | 0 |
| AID-02073 | 12 | 0 | 0 | Request new 13 | Exceeds remaining authority | 12 | 0 | 12 |
| AID-02074 | 12 | 0 | 0 | Replay settled 12 | Original receipt; no new effect | 12 | 0 | 12 |
| AID-02075 | 12 | 0 | 0 | Record return 1 | Apply linked return once | 11 | 0 | 13 |
| AID-02076 | 12 | 0 | 0 | Record return 6 | Apply linked return once | 6 | 0 | 18 |
| AID-02077 | 12 | 0 | 0 | Record return 12 | Apply linked return once | 0 | 0 | 24 |
| AID-02078 | 12 | 0 | 0 | Record return 13 | Return exceeds net fulfillment | 12 | 0 | 12 |
| AID-02079 | 12 | 0 | 5 | Request new 6 | Reserve once | 12 | 11 | 1 |
| AID-02080 | 12 | 0 | 5 | Request new 7 | Reserve once | 12 | 12 | 0 |
| AID-02081 | 12 | 0 | 5 | Request new 8 | Exceeds remaining authority | 12 | 5 | 7 |
| AID-02082 | 12 | 0 | 5 | Confirm pending 5 | Settle original once | 17 | 0 | 7 |
| AID-02083 | 12 | 0 | 5 | Fail pending 5 | Release pending reservation | 12 | 0 | 12 |
| AID-02084 | 12 | 0 | 5 | Replay settled 12 | Original receipt; no new effect | 12 | 5 | 7 |
| AID-02085 | 12 | 0 | 5 | Record return 1 | Apply linked return once | 11 | 5 | 8 |
| AID-02086 | 12 | 0 | 5 | Record return 6 | Apply linked return once | 6 | 5 | 13 |
| AID-02087 | 12 | 0 | 5 | Record return 12 | Apply linked return once | 0 | 5 | 19 |
| AID-02088 | 12 | 0 | 5 | Record return 13 | Return exceeds net fulfillment | 12 | 5 | 7 |
| AID-02089 | 12 | 0 | 12 | Request new 1 | Exceeds remaining authority | 12 | 12 | 0 |
| AID-02090 | 12 | 0 | 12 | Request new 8 | Exceeds remaining authority | 12 | 12 | 0 |
| AID-02091 | 12 | 0 | 12 | Confirm pending 12 | Settle original once | 24 | 0 | 0 |
| AID-02092 | 12 | 0 | 12 | Fail pending 12 | Release pending reservation | 12 | 0 | 12 |
| AID-02093 | 12 | 0 | 12 | Replay settled 12 | Original receipt; no new effect | 12 | 12 | 0 |
| AID-02094 | 12 | 0 | 12 | Record return 1 | Apply linked return once | 11 | 12 | 1 |
| AID-02095 | 12 | 0 | 12 | Record return 6 | Apply linked return once | 6 | 12 | 6 |
| AID-02096 | 12 | 0 | 12 | Record return 12 | Apply linked return once | 0 | 12 | 12 |
| AID-02097 | 12 | 0 | 12 | Record return 13 | Return exceeds net fulfillment | 12 | 12 | 0 |
| AID-02098 | 12 | 1 | 0 | Request new 8 | Reserve once | 11 | 8 | 5 |
| AID-02099 | 12 | 1 | 0 | Request new 12 | Reserve once | 11 | 12 | 1 |
| AID-02100 | 12 | 1 | 0 | Request new 13 | Reserve once | 11 | 13 | 0 |
| AID-02101 | 12 | 1 | 0 | Request new 14 | Exceeds remaining authority | 11 | 0 | 13 |
| AID-02102 | 12 | 1 | 0 | Replay settled 12 | Original receipt; no new effect | 11 | 0 | 13 |
| AID-02103 | 12 | 1 | 0 | Record return 1 | Apply linked return once | 10 | 0 | 14 |
| AID-02104 | 12 | 1 | 0 | Record return 6 | Apply linked return once | 5 | 0 | 19 |
| AID-02105 | 12 | 1 | 0 | Record return 11 | Apply linked return once | 0 | 0 | 24 |
| AID-02106 | 12 | 1 | 0 | Record return 12 | Return exceeds net fulfillment | 11 | 0 | 13 |
| AID-02107 | 12 | 1 | 5 | Request new 7 | Reserve once | 11 | 12 | 1 |
| AID-02108 | 12 | 1 | 5 | Request new 8 | Reserve once | 11 | 13 | 0 |
| AID-02109 | 12 | 1 | 5 | Request new 9 | Exceeds remaining authority | 11 | 5 | 8 |
| AID-02110 | 12 | 1 | 5 | Confirm pending 5 | Settle original once | 16 | 0 | 8 |
| AID-02111 | 12 | 1 | 5 | Fail pending 5 | Release pending reservation | 11 | 0 | 13 |
| AID-02112 | 12 | 1 | 5 | Replay settled 12 | Original receipt; no new effect | 11 | 5 | 8 |
| AID-02113 | 12 | 1 | 5 | Record return 1 | Apply linked return once | 10 | 5 | 9 |
| AID-02114 | 12 | 1 | 5 | Record return 6 | Apply linked return once | 5 | 5 | 14 |
| AID-02115 | 12 | 1 | 5 | Record return 11 | Apply linked return once | 0 | 5 | 19 |
| AID-02116 | 12 | 1 | 5 | Record return 12 | Return exceeds net fulfillment | 11 | 5 | 8 |
| AID-02117 | 12 | 1 | 13 | Request new 1 | Exceeds remaining authority | 11 | 13 | 0 |
| AID-02118 | 12 | 1 | 13 | Request new 8 | Exceeds remaining authority | 11 | 13 | 0 |
| AID-02119 | 12 | 1 | 13 | Confirm pending 13 | Settle original once | 24 | 0 | 0 |
| AID-02120 | 12 | 1 | 13 | Fail pending 13 | Release pending reservation | 11 | 0 | 13 |
| AID-02121 | 12 | 1 | 13 | Replay settled 12 | Original receipt; no new effect | 11 | 13 | 0 |
| AID-02122 | 12 | 1 | 13 | Record return 1 | Apply linked return once | 10 | 13 | 1 |
| AID-02123 | 12 | 1 | 13 | Record return 6 | Apply linked return once | 5 | 13 | 6 |
| AID-02124 | 12 | 1 | 13 | Record return 11 | Apply linked return once | 0 | 13 | 11 |
| AID-02125 | 12 | 1 | 13 | Record return 12 | Return exceeds net fulfillment | 11 | 13 | 0 |
| AID-02126 | 12 | 3 | 0 | Request new 8 | Reserve once | 9 | 8 | 7 |
| AID-02127 | 12 | 3 | 0 | Request new 14 | Reserve once | 9 | 14 | 1 |
| AID-02128 | 12 | 3 | 0 | Request new 15 | Reserve once | 9 | 15 | 0 |
| AID-02129 | 12 | 3 | 0 | Request new 16 | Exceeds remaining authority | 9 | 0 | 15 |
| AID-02130 | 12 | 3 | 0 | Replay settled 12 | Original receipt; no new effect | 9 | 0 | 15 |
| AID-02131 | 12 | 3 | 0 | Record return 1 | Apply linked return once | 8 | 0 | 16 |
| AID-02132 | 12 | 3 | 0 | Record return 5 | Apply linked return once | 4 | 0 | 20 |
| AID-02133 | 12 | 3 | 0 | Record return 9 | Apply linked return once | 0 | 0 | 24 |
| AID-02134 | 12 | 3 | 0 | Record return 10 | Return exceeds net fulfillment | 9 | 0 | 15 |
| AID-02135 | 12 | 3 | 6 | Request new 8 | Reserve once | 9 | 14 | 1 |
| AID-02136 | 12 | 3 | 6 | Request new 9 | Reserve once | 9 | 15 | 0 |
| AID-02137 | 12 | 3 | 6 | Request new 10 | Exceeds remaining authority | 9 | 6 | 9 |
| AID-02138 | 12 | 3 | 6 | Confirm pending 6 | Settle original once | 15 | 0 | 9 |
| AID-02139 | 12 | 3 | 6 | Fail pending 6 | Release pending reservation | 9 | 0 | 15 |
| AID-02140 | 12 | 3 | 6 | Replay settled 12 | Original receipt; no new effect | 9 | 6 | 9 |
| AID-02141 | 12 | 3 | 6 | Record return 1 | Apply linked return once | 8 | 6 | 10 |
| AID-02142 | 12 | 3 | 6 | Record return 5 | Apply linked return once | 4 | 6 | 14 |
| AID-02143 | 12 | 3 | 6 | Record return 9 | Apply linked return once | 0 | 6 | 18 |
| AID-02144 | 12 | 3 | 6 | Record return 10 | Return exceeds net fulfillment | 9 | 6 | 9 |
| AID-02145 | 12 | 3 | 15 | Request new 1 | Exceeds remaining authority | 9 | 15 | 0 |
| AID-02146 | 12 | 3 | 15 | Request new 8 | Exceeds remaining authority | 9 | 15 | 0 |
| AID-02147 | 12 | 3 | 15 | Confirm pending 15 | Settle original once | 24 | 0 | 0 |
| AID-02148 | 12 | 3 | 15 | Fail pending 15 | Release pending reservation | 9 | 0 | 15 |
| AID-02149 | 12 | 3 | 15 | Replay settled 12 | Original receipt; no new effect | 9 | 15 | 0 |
| AID-02150 | 12 | 3 | 15 | Record return 1 | Apply linked return once | 8 | 15 | 1 |
| AID-02151 | 12 | 3 | 15 | Record return 5 | Apply linked return once | 4 | 15 | 5 |
| AID-02152 | 12 | 3 | 15 | Record return 9 | Apply linked return once | 0 | 15 | 9 |
| AID-02153 | 12 | 3 | 15 | Record return 10 | Return exceeds net fulfillment | 9 | 15 | 0 |
| AID-02154 | 12 | 12 | 0 | Request new 8 | Reserve once | 0 | 8 | 16 |
| AID-02155 | 12 | 12 | 0 | Request new 23 | Reserve once | 0 | 23 | 1 |
| AID-02156 | 12 | 12 | 0 | Request new 24 | Reserve once | 0 | 24 | 0 |
| AID-02157 | 12 | 12 | 0 | Request new 25 | Exceeds remaining authority | 0 | 0 | 24 |
| AID-02158 | 12 | 12 | 0 | Replay settled 12 | Original receipt; no new effect | 0 | 0 | 24 |
| AID-02159 | 12 | 12 | 10 | Request new 8 | Reserve once | 0 | 18 | 6 |
| AID-02160 | 12 | 12 | 10 | Request new 13 | Reserve once | 0 | 23 | 1 |
| AID-02161 | 12 | 12 | 10 | Request new 14 | Reserve once | 0 | 24 | 0 |
| AID-02162 | 12 | 12 | 10 | Request new 15 | Exceeds remaining authority | 0 | 10 | 14 |
| AID-02163 | 12 | 12 | 10 | Confirm pending 10 | Settle original once | 10 | 0 | 14 |
| AID-02164 | 12 | 12 | 10 | Fail pending 10 | Release pending reservation | 0 | 0 | 24 |
| AID-02165 | 12 | 12 | 10 | Replay settled 12 | Original receipt; no new effect | 0 | 10 | 14 |
| AID-02166 | 12 | 12 | 24 | Request new 1 | Exceeds remaining authority | 0 | 24 | 0 |
| AID-02167 | 12 | 12 | 24 | Request new 8 | Exceeds remaining authority | 0 | 24 | 0 |
| AID-02168 | 12 | 12 | 24 | Confirm pending 24 | Settle original once | 24 | 0 | 0 |
| AID-02169 | 12 | 12 | 24 | Fail pending 24 | Release pending reservation | 0 | 0 | 24 |
| AID-02170 | 12 | 12 | 24 | Replay settled 12 | Original receipt; no new effect | 0 | 24 | 0 |
| AID-02171 | 19 | 0 | 0 | Request new 4 | Reserve once | 19 | 4 | 1 |
| AID-02172 | 19 | 0 | 0 | Request new 5 | Reserve once | 19 | 5 | 0 |
| AID-02173 | 19 | 0 | 0 | Request new 6 | Exceeds remaining authority | 19 | 0 | 5 |
| AID-02174 | 19 | 0 | 0 | Request new 8 | Exceeds remaining authority | 19 | 0 | 5 |
| AID-02175 | 19 | 0 | 0 | Replay settled 19 | Original receipt; no new effect | 19 | 0 | 5 |
| AID-02176 | 19 | 0 | 0 | Record return 1 | Apply linked return once | 18 | 0 | 6 |
| AID-02177 | 19 | 0 | 0 | Record return 10 | Apply linked return once | 9 | 0 | 15 |
| AID-02178 | 19 | 0 | 0 | Record return 19 | Apply linked return once | 0 | 0 | 24 |
| AID-02179 | 19 | 0 | 0 | Record return 20 | Return exceeds net fulfillment | 19 | 0 | 5 |
| AID-02180 | 19 | 0 | 2 | Request new 2 | Reserve once | 19 | 4 | 1 |
| AID-02181 | 19 | 0 | 2 | Request new 3 | Reserve once | 19 | 5 | 0 |
| AID-02182 | 19 | 0 | 2 | Request new 4 | Exceeds remaining authority | 19 | 2 | 3 |
| AID-02183 | 19 | 0 | 2 | Request new 8 | Exceeds remaining authority | 19 | 2 | 3 |
| AID-02184 | 19 | 0 | 2 | Confirm pending 2 | Settle original once | 21 | 0 | 3 |
| AID-02185 | 19 | 0 | 2 | Fail pending 2 | Release pending reservation | 19 | 0 | 5 |
| AID-02186 | 19 | 0 | 2 | Replay settled 19 | Original receipt; no new effect | 19 | 2 | 3 |
| AID-02187 | 19 | 0 | 2 | Record return 1 | Apply linked return once | 18 | 2 | 4 |
| AID-02188 | 19 | 0 | 2 | Record return 10 | Apply linked return once | 9 | 2 | 13 |
| AID-02189 | 19 | 0 | 2 | Record return 19 | Apply linked return once | 0 | 2 | 22 |
| AID-02190 | 19 | 0 | 2 | Record return 20 | Return exceeds net fulfillment | 19 | 2 | 3 |
| AID-02191 | 19 | 0 | 5 | Request new 1 | Exceeds remaining authority | 19 | 5 | 0 |
| AID-02192 | 19 | 0 | 5 | Request new 8 | Exceeds remaining authority | 19 | 5 | 0 |
| AID-02193 | 19 | 0 | 5 | Confirm pending 5 | Settle original once | 24 | 0 | 0 |
| AID-02194 | 19 | 0 | 5 | Fail pending 5 | Release pending reservation | 19 | 0 | 5 |
| AID-02195 | 19 | 0 | 5 | Replay settled 19 | Original receipt; no new effect | 19 | 5 | 0 |
| AID-02196 | 19 | 0 | 5 | Record return 1 | Apply linked return once | 18 | 5 | 1 |
| AID-02197 | 19 | 0 | 5 | Record return 10 | Apply linked return once | 9 | 5 | 10 |
| AID-02198 | 19 | 0 | 5 | Record return 19 | Apply linked return once | 0 | 5 | 19 |
| AID-02199 | 19 | 0 | 5 | Record return 20 | Return exceeds net fulfillment | 19 | 5 | 0 |
| AID-02200 | 19 | 1 | 0 | Request new 5 | Reserve once | 18 | 5 | 1 |
| AID-02201 | 19 | 1 | 0 | Request new 6 | Reserve once | 18 | 6 | 0 |
| AID-02202 | 19 | 1 | 0 | Request new 7 | Exceeds remaining authority | 18 | 0 | 6 |
| AID-02203 | 19 | 1 | 0 | Request new 8 | Exceeds remaining authority | 18 | 0 | 6 |
| AID-02204 | 19 | 1 | 0 | Replay settled 19 | Original receipt; no new effect | 18 | 0 | 6 |
| AID-02205 | 19 | 1 | 0 | Record return 1 | Apply linked return once | 17 | 0 | 7 |
| AID-02206 | 19 | 1 | 0 | Record return 9 | Apply linked return once | 9 | 0 | 15 |
| AID-02207 | 19 | 1 | 0 | Record return 18 | Apply linked return once | 0 | 0 | 24 |
| AID-02208 | 19 | 1 | 0 | Record return 19 | Return exceeds net fulfillment | 18 | 0 | 6 |
| AID-02209 | 19 | 1 | 2 | Request new 3 | Reserve once | 18 | 5 | 1 |
| AID-02210 | 19 | 1 | 2 | Request new 4 | Reserve once | 18 | 6 | 0 |
| AID-02211 | 19 | 1 | 2 | Request new 5 | Exceeds remaining authority | 18 | 2 | 4 |
| AID-02212 | 19 | 1 | 2 | Request new 8 | Exceeds remaining authority | 18 | 2 | 4 |
| AID-02213 | 19 | 1 | 2 | Confirm pending 2 | Settle original once | 20 | 0 | 4 |
| AID-02214 | 19 | 1 | 2 | Fail pending 2 | Release pending reservation | 18 | 0 | 6 |
| AID-02215 | 19 | 1 | 2 | Replay settled 19 | Original receipt; no new effect | 18 | 2 | 4 |
| AID-02216 | 19 | 1 | 2 | Record return 1 | Apply linked return once | 17 | 2 | 5 |
| AID-02217 | 19 | 1 | 2 | Record return 9 | Apply linked return once | 9 | 2 | 13 |
| AID-02218 | 19 | 1 | 2 | Record return 18 | Apply linked return once | 0 | 2 | 22 |
| AID-02219 | 19 | 1 | 2 | Record return 19 | Return exceeds net fulfillment | 18 | 2 | 4 |
| AID-02220 | 19 | 1 | 6 | Request new 1 | Exceeds remaining authority | 18 | 6 | 0 |
| AID-02221 | 19 | 1 | 6 | Request new 8 | Exceeds remaining authority | 18 | 6 | 0 |
| AID-02222 | 19 | 1 | 6 | Confirm pending 6 | Settle original once | 24 | 0 | 0 |
| AID-02223 | 19 | 1 | 6 | Fail pending 6 | Release pending reservation | 18 | 0 | 6 |
| AID-02224 | 19 | 1 | 6 | Replay settled 19 | Original receipt; no new effect | 18 | 6 | 0 |
| AID-02225 | 19 | 1 | 6 | Record return 1 | Apply linked return once | 17 | 6 | 1 |
| AID-02226 | 19 | 1 | 6 | Record return 9 | Apply linked return once | 9 | 6 | 9 |
| AID-02227 | 19 | 1 | 6 | Record return 18 | Apply linked return once | 0 | 6 | 18 |
| AID-02228 | 19 | 1 | 6 | Record return 19 | Return exceeds net fulfillment | 18 | 6 | 0 |
| AID-02229 | 19 | 5 | 0 | Request new 8 | Reserve once | 14 | 8 | 2 |
| AID-02230 | 19 | 5 | 0 | Request new 9 | Reserve once | 14 | 9 | 1 |
| AID-02231 | 19 | 5 | 0 | Request new 10 | Reserve once | 14 | 10 | 0 |
| AID-02232 | 19 | 5 | 0 | Request new 11 | Exceeds remaining authority | 14 | 0 | 10 |
| AID-02233 | 19 | 5 | 0 | Replay settled 19 | Original receipt; no new effect | 14 | 0 | 10 |
| AID-02234 | 19 | 5 | 0 | Record return 1 | Apply linked return once | 13 | 0 | 11 |
| AID-02235 | 19 | 5 | 0 | Record return 7 | Apply linked return once | 7 | 0 | 17 |
| AID-02236 | 19 | 5 | 0 | Record return 14 | Apply linked return once | 0 | 0 | 24 |
| AID-02237 | 19 | 5 | 0 | Record return 15 | Return exceeds net fulfillment | 14 | 0 | 10 |
| AID-02238 | 19 | 5 | 4 | Request new 5 | Reserve once | 14 | 9 | 1 |
| AID-02239 | 19 | 5 | 4 | Request new 6 | Reserve once | 14 | 10 | 0 |
| AID-02240 | 19 | 5 | 4 | Request new 7 | Exceeds remaining authority | 14 | 4 | 6 |
| AID-02241 | 19 | 5 | 4 | Request new 8 | Exceeds remaining authority | 14 | 4 | 6 |
| AID-02242 | 19 | 5 | 4 | Confirm pending 4 | Settle original once | 18 | 0 | 6 |
| AID-02243 | 19 | 5 | 4 | Fail pending 4 | Release pending reservation | 14 | 0 | 10 |
| AID-02244 | 19 | 5 | 4 | Replay settled 19 | Original receipt; no new effect | 14 | 4 | 6 |
| AID-02245 | 19 | 5 | 4 | Record return 1 | Apply linked return once | 13 | 4 | 7 |
| AID-02246 | 19 | 5 | 4 | Record return 7 | Apply linked return once | 7 | 4 | 13 |
| AID-02247 | 19 | 5 | 4 | Record return 14 | Apply linked return once | 0 | 4 | 20 |
| AID-02248 | 19 | 5 | 4 | Record return 15 | Return exceeds net fulfillment | 14 | 4 | 6 |
| AID-02249 | 19 | 5 | 10 | Request new 1 | Exceeds remaining authority | 14 | 10 | 0 |
| AID-02250 | 19 | 5 | 10 | Request new 8 | Exceeds remaining authority | 14 | 10 | 0 |
| AID-02251 | 19 | 5 | 10 | Confirm pending 10 | Settle original once | 24 | 0 | 0 |
| AID-02252 | 19 | 5 | 10 | Fail pending 10 | Release pending reservation | 14 | 0 | 10 |
| AID-02253 | 19 | 5 | 10 | Replay settled 19 | Original receipt; no new effect | 14 | 10 | 0 |
| AID-02254 | 19 | 5 | 10 | Record return 1 | Apply linked return once | 13 | 10 | 1 |
| AID-02255 | 19 | 5 | 10 | Record return 7 | Apply linked return once | 7 | 10 | 7 |
| AID-02256 | 19 | 5 | 10 | Record return 14 | Apply linked return once | 0 | 10 | 14 |
| AID-02257 | 19 | 5 | 10 | Record return 15 | Return exceeds net fulfillment | 14 | 10 | 0 |
| AID-02258 | 19 | 19 | 0 | Request new 8 | Reserve once | 0 | 8 | 16 |
| AID-02259 | 19 | 19 | 0 | Request new 23 | Reserve once | 0 | 23 | 1 |
| AID-02260 | 19 | 19 | 0 | Request new 24 | Reserve once | 0 | 24 | 0 |
| AID-02261 | 19 | 19 | 0 | Request new 25 | Exceeds remaining authority | 0 | 0 | 24 |
| AID-02262 | 19 | 19 | 0 | Replay settled 19 | Original receipt; no new effect | 0 | 0 | 24 |
| AID-02263 | 19 | 19 | 10 | Request new 8 | Reserve once | 0 | 18 | 6 |
| AID-02264 | 19 | 19 | 10 | Request new 13 | Reserve once | 0 | 23 | 1 |
| AID-02265 | 19 | 19 | 10 | Request new 14 | Reserve once | 0 | 24 | 0 |
| AID-02266 | 19 | 19 | 10 | Request new 15 | Exceeds remaining authority | 0 | 10 | 14 |
| AID-02267 | 19 | 19 | 10 | Confirm pending 10 | Settle original once | 10 | 0 | 14 |
| AID-02268 | 19 | 19 | 10 | Fail pending 10 | Release pending reservation | 0 | 0 | 24 |
| AID-02269 | 19 | 19 | 10 | Replay settled 19 | Original receipt; no new effect | 0 | 10 | 14 |
| AID-02270 | 19 | 19 | 24 | Request new 1 | Exceeds remaining authority | 0 | 24 | 0 |
| AID-02271 | 19 | 19 | 24 | Request new 8 | Exceeds remaining authority | 0 | 24 | 0 |
| AID-02272 | 19 | 19 | 24 | Confirm pending 24 | Settle original once | 24 | 0 | 0 |
| AID-02273 | 19 | 19 | 24 | Fail pending 24 | Release pending reservation | 0 | 0 | 24 |
| AID-02274 | 19 | 19 | 24 | Replay settled 19 | Original receipt; no new effect | 0 | 24 | 0 |
| AID-02275 | 24 | 0 | 0 | Request new 1 | Exceeds remaining authority | 24 | 0 | 0 |
| AID-02276 | 24 | 0 | 0 | Request new 8 | Exceeds remaining authority | 24 | 0 | 0 |
| AID-02277 | 24 | 0 | 0 | Replay settled 24 | Original receipt; no new effect | 24 | 0 | 0 |
| AID-02278 | 24 | 0 | 0 | Record return 1 | Apply linked return once | 23 | 0 | 1 |
| AID-02279 | 24 | 0 | 0 | Record return 12 | Apply linked return once | 12 | 0 | 12 |
| AID-02280 | 24 | 0 | 0 | Record return 24 | Apply linked return once | 0 | 0 | 24 |
| AID-02281 | 24 | 0 | 0 | Record return 25 | Return exceeds net fulfillment | 24 | 0 | 0 |
| AID-02282 | 24 | 1 | 0 | Request new 1 | Reserve once | 23 | 1 | 0 |
| AID-02283 | 24 | 1 | 0 | Request new 2 | Exceeds remaining authority | 23 | 0 | 1 |
| AID-02284 | 24 | 1 | 0 | Request new 8 | Exceeds remaining authority | 23 | 0 | 1 |
| AID-02285 | 24 | 1 | 0 | Replay settled 24 | Original receipt; no new effect | 23 | 0 | 1 |
| AID-02286 | 24 | 1 | 0 | Record return 1 | Apply linked return once | 22 | 0 | 2 |
| AID-02287 | 24 | 1 | 0 | Record return 12 | Apply linked return once | 11 | 0 | 13 |
| AID-02288 | 24 | 1 | 0 | Record return 23 | Apply linked return once | 0 | 0 | 24 |
| AID-02289 | 24 | 1 | 0 | Record return 24 | Return exceeds net fulfillment | 23 | 0 | 1 |
| AID-02290 | 24 | 1 | 1 | Request new 1 | Exceeds remaining authority | 23 | 1 | 0 |
| AID-02291 | 24 | 1 | 1 | Request new 8 | Exceeds remaining authority | 23 | 1 | 0 |
| AID-02292 | 24 | 1 | 1 | Confirm pending 1 | Settle original once | 24 | 0 | 0 |
| AID-02293 | 24 | 1 | 1 | Fail pending 1 | Release pending reservation | 23 | 0 | 1 |
| AID-02294 | 24 | 1 | 1 | Replay settled 24 | Original receipt; no new effect | 23 | 1 | 0 |
| AID-02295 | 24 | 1 | 1 | Record return 1 | Apply linked return once | 22 | 1 | 1 |
| AID-02296 | 24 | 1 | 1 | Record return 12 | Apply linked return once | 11 | 1 | 12 |
| AID-02297 | 24 | 1 | 1 | Record return 23 | Apply linked return once | 0 | 1 | 23 |
| AID-02298 | 24 | 1 | 1 | Record return 24 | Return exceeds net fulfillment | 23 | 1 | 0 |
| AID-02299 | 24 | 6 | 0 | Request new 5 | Reserve once | 18 | 5 | 1 |
| AID-02300 | 24 | 6 | 0 | Request new 6 | Reserve once | 18 | 6 | 0 |
