# School expenses — part 1 of 2

[Policy and other cases](README.md)

One approved award of 875.25 currency units; all inputs use currency units at 2 decimal places. One original settled fulfillment, when present, may be partially returned. An outstanding payment or stock issue is reserved against authority. Historical issued and returned amounts are kept even when the net amount is zero. Reviewers can reconstruct this case using the supplied opening facts.

| Case | Opening gross | Opening returns | Opening reserved | Requested event and value | Decision | New net delivered | New reserved | New free authority |
|---|---|---|---|---|---|---|---|---|
| AID-01189 | 0.00 | 0.00 | 0.00 | Request new 288.83 | Reserve once | 0.00 | 288.83 | 586.42 |
| AID-01190 | 0.00 | 0.00 | 0.00 | Request new 875.24 | Reserve once | 0.00 | 875.24 | 0.01 |
| AID-01191 | 0.00 | 0.00 | 0.00 | Request new 875.25 | Reserve once | 0.00 | 875.25 | 0.00 |
| AID-01192 | 0.00 | 0.00 | 0.00 | Request new 875.26 | Exceeds remaining authority | 0.00 | 0.00 | 875.25 |
| AID-01193 | 0.00 | 0.00 | 350.10 | Request new 288.83 | Reserve once | 0.00 | 638.93 | 236.32 |
| AID-01194 | 0.00 | 0.00 | 350.10 | Request new 525.14 | Reserve once | 0.00 | 875.24 | 0.01 |
| AID-01195 | 0.00 | 0.00 | 350.10 | Request new 525.15 | Reserve once | 0.00 | 875.25 | 0.00 |
| AID-01196 | 0.00 | 0.00 | 350.10 | Request new 525.16 | Exceeds remaining authority | 0.00 | 350.10 | 525.15 |
| AID-01197 | 0.00 | 0.00 | 350.10 | Confirm pending 350.10 | Settle original once | 350.10 | 0.00 | 525.15 |
| AID-01198 | 0.00 | 0.00 | 350.10 | Fail pending 350.10 | Release pending reservation | 0.00 | 0.00 | 875.25 |
| AID-01199 | 0.00 | 0.00 | 875.25 | Request new 0.01 | Exceeds remaining authority | 0.00 | 875.25 | 0.00 |
| AID-01200 | 0.00 | 0.00 | 875.25 | Request new 288.83 | Exceeds remaining authority | 0.00 | 875.25 | 0.00 |
| AID-01201 | 0.00 | 0.00 | 875.25 | Confirm pending 875.25 | Settle original once | 875.25 | 0.00 | 0.00 |
| AID-01202 | 0.00 | 0.00 | 875.25 | Fail pending 875.25 | Release pending reservation | 0.00 | 0.00 | 875.25 |
| AID-01203 | 175.05 | 0.00 | 0.00 | Request new 288.83 | Reserve once | 175.05 | 288.83 | 411.37 |
| AID-01204 | 175.05 | 0.00 | 0.00 | Request new 700.19 | Reserve once | 175.05 | 700.19 | 0.01 |
| AID-01205 | 175.05 | 0.00 | 0.00 | Request new 700.20 | Reserve once | 175.05 | 700.20 | 0.00 |
| AID-01206 | 175.05 | 0.00 | 0.00 | Request new 700.21 | Exceeds remaining authority | 175.05 | 0.00 | 700.20 |
| AID-01207 | 175.05 | 0.00 | 0.00 | Replay settled 175.05 | Original receipt; no new effect | 175.05 | 0.00 | 700.20 |
| AID-01208 | 175.05 | 0.00 | 0.00 | Record return 0.01 | Apply linked return once | 175.04 | 0.00 | 700.21 |
| AID-01209 | 175.05 | 0.00 | 0.00 | Record return 87.53 | Apply linked return once | 87.52 | 0.00 | 787.73 |
| AID-01210 | 175.05 | 0.00 | 0.00 | Record return 175.05 | Apply linked return once | 0.00 | 0.00 | 875.25 |
| AID-01211 | 175.05 | 0.00 | 0.00 | Record return 175.06 | Return exceeds net fulfillment | 175.05 | 0.00 | 700.20 |
| AID-01212 | 175.05 | 0.00 | 280.08 | Request new 288.83 | Reserve once | 175.05 | 568.91 | 131.29 |
| AID-01213 | 175.05 | 0.00 | 280.08 | Request new 420.11 | Reserve once | 175.05 | 700.19 | 0.01 |
| AID-01214 | 175.05 | 0.00 | 280.08 | Request new 420.12 | Reserve once | 175.05 | 700.20 | 0.00 |
| AID-01215 | 175.05 | 0.00 | 280.08 | Request new 420.13 | Exceeds remaining authority | 175.05 | 280.08 | 420.12 |
| AID-01216 | 175.05 | 0.00 | 280.08 | Confirm pending 280.08 | Settle original once | 455.13 | 0.00 | 420.12 |
| AID-01217 | 175.05 | 0.00 | 280.08 | Fail pending 280.08 | Release pending reservation | 175.05 | 0.00 | 700.20 |
| AID-01218 | 175.05 | 0.00 | 280.08 | Replay settled 175.05 | Original receipt; no new effect | 175.05 | 280.08 | 420.12 |
| AID-01219 | 175.05 | 0.00 | 280.08 | Record return 0.01 | Apply linked return once | 175.04 | 280.08 | 420.13 |
| AID-01220 | 175.05 | 0.00 | 280.08 | Record return 87.53 | Apply linked return once | 87.52 | 280.08 | 507.65 |
| AID-01221 | 175.05 | 0.00 | 280.08 | Record return 175.05 | Apply linked return once | 0.00 | 280.08 | 595.17 |
| AID-01222 | 175.05 | 0.00 | 280.08 | Record return 175.06 | Return exceeds net fulfillment | 175.05 | 280.08 | 420.12 |
| AID-01223 | 175.05 | 0.00 | 700.20 | Request new 0.01 | Exceeds remaining authority | 175.05 | 700.20 | 0.00 |
| AID-01224 | 175.05 | 0.00 | 700.20 | Request new 288.83 | Exceeds remaining authority | 175.05 | 700.20 | 0.00 |
| AID-01225 | 175.05 | 0.00 | 700.20 | Confirm pending 700.20 | Settle original once | 875.25 | 0.00 | 0.00 |
| AID-01226 | 175.05 | 0.00 | 700.20 | Fail pending 700.20 | Release pending reservation | 175.05 | 0.00 | 700.20 |
| AID-01227 | 175.05 | 0.00 | 700.20 | Replay settled 175.05 | Original receipt; no new effect | 175.05 | 700.20 | 0.00 |
| AID-01228 | 175.05 | 0.00 | 700.20 | Record return 0.01 | Apply linked return once | 175.04 | 700.20 | 0.01 |
| AID-01229 | 175.05 | 0.00 | 700.20 | Record return 87.53 | Apply linked return once | 87.52 | 700.20 | 87.53 |
| AID-01230 | 175.05 | 0.00 | 700.20 | Record return 175.05 | Apply linked return once | 0.00 | 700.20 | 175.05 |
| AID-01231 | 175.05 | 0.00 | 700.20 | Record return 175.06 | Return exceeds net fulfillment | 175.05 | 700.20 | 0.00 |
| AID-01232 | 175.05 | 0.01 | 0.00 | Request new 288.83 | Reserve once | 175.04 | 288.83 | 411.38 |
| AID-01233 | 175.05 | 0.01 | 0.00 | Request new 700.20 | Reserve once | 175.04 | 700.20 | 0.01 |
| AID-01234 | 175.05 | 0.01 | 0.00 | Request new 700.21 | Reserve once | 175.04 | 700.21 | 0.00 |
| AID-01235 | 175.05 | 0.01 | 0.00 | Request new 700.22 | Exceeds remaining authority | 175.04 | 0.00 | 700.21 |
| AID-01236 | 175.05 | 0.01 | 0.00 | Replay settled 175.05 | Original receipt; no new effect | 175.04 | 0.00 | 700.21 |
| AID-01237 | 175.05 | 0.01 | 0.00 | Record return 0.01 | Apply linked return once | 175.03 | 0.00 | 700.22 |
| AID-01238 | 175.05 | 0.01 | 0.00 | Record return 87.52 | Apply linked return once | 87.52 | 0.00 | 787.73 |
| AID-01239 | 175.05 | 0.01 | 0.00 | Record return 175.04 | Apply linked return once | 0.00 | 0.00 | 875.25 |
| AID-01240 | 175.05 | 0.01 | 0.00 | Record return 175.05 | Return exceeds net fulfillment | 175.04 | 0.00 | 700.21 |
| AID-01241 | 175.05 | 0.01 | 280.08 | Request new 288.83 | Reserve once | 175.04 | 568.91 | 131.30 |
| AID-01242 | 175.05 | 0.01 | 280.08 | Request new 420.12 | Reserve once | 175.04 | 700.20 | 0.01 |
| AID-01243 | 175.05 | 0.01 | 280.08 | Request new 420.13 | Reserve once | 175.04 | 700.21 | 0.00 |
| AID-01244 | 175.05 | 0.01 | 280.08 | Request new 420.14 | Exceeds remaining authority | 175.04 | 280.08 | 420.13 |
| AID-01245 | 175.05 | 0.01 | 280.08 | Confirm pending 280.08 | Settle original once | 455.12 | 0.00 | 420.13 |
| AID-01246 | 175.05 | 0.01 | 280.08 | Fail pending 280.08 | Release pending reservation | 175.04 | 0.00 | 700.21 |
| AID-01247 | 175.05 | 0.01 | 280.08 | Replay settled 175.05 | Original receipt; no new effect | 175.04 | 280.08 | 420.13 |
| AID-01248 | 175.05 | 0.01 | 280.08 | Record return 0.01 | Apply linked return once | 175.03 | 280.08 | 420.14 |
| AID-01249 | 175.05 | 0.01 | 280.08 | Record return 87.52 | Apply linked return once | 87.52 | 280.08 | 507.65 |
| AID-01250 | 175.05 | 0.01 | 280.08 | Record return 175.04 | Apply linked return once | 0.00 | 280.08 | 595.17 |
| AID-01251 | 175.05 | 0.01 | 280.08 | Record return 175.05 | Return exceeds net fulfillment | 175.04 | 280.08 | 420.13 |
| AID-01252 | 175.05 | 0.01 | 700.21 | Request new 0.01 | Exceeds remaining authority | 175.04 | 700.21 | 0.00 |
| AID-01253 | 175.05 | 0.01 | 700.21 | Request new 288.83 | Exceeds remaining authority | 175.04 | 700.21 | 0.00 |
| AID-01254 | 175.05 | 0.01 | 700.21 | Confirm pending 700.21 | Settle original once | 875.25 | 0.00 | 0.00 |
| AID-01255 | 175.05 | 0.01 | 700.21 | Fail pending 700.21 | Release pending reservation | 175.04 | 0.00 | 700.21 |
| AID-01256 | 175.05 | 0.01 | 700.21 | Replay settled 175.05 | Original receipt; no new effect | 175.04 | 700.21 | 0.00 |
| AID-01257 | 175.05 | 0.01 | 700.21 | Record return 0.01 | Apply linked return once | 175.03 | 700.21 | 0.01 |
| AID-01258 | 175.05 | 0.01 | 700.21 | Record return 87.52 | Apply linked return once | 87.52 | 700.21 | 87.52 |
| AID-01259 | 175.05 | 0.01 | 700.21 | Record return 175.04 | Apply linked return once | 0.00 | 700.21 | 175.04 |
| AID-01260 | 175.05 | 0.01 | 700.21 | Record return 175.05 | Return exceeds net fulfillment | 175.04 | 700.21 | 0.00 |
| AID-01261 | 175.05 | 43.76 | 0.00 | Request new 288.83 | Reserve once | 131.29 | 288.83 | 455.13 |
| AID-01262 | 175.05 | 43.76 | 0.00 | Request new 743.95 | Reserve once | 131.29 | 743.95 | 0.01 |
| AID-01263 | 175.05 | 43.76 | 0.00 | Request new 743.96 | Reserve once | 131.29 | 743.96 | 0.00 |
| AID-01264 | 175.05 | 43.76 | 0.00 | Request new 743.97 | Exceeds remaining authority | 131.29 | 0.00 | 743.96 |
| AID-01265 | 175.05 | 43.76 | 0.00 | Replay settled 175.05 | Original receipt; no new effect | 131.29 | 0.00 | 743.96 |
| AID-01266 | 175.05 | 43.76 | 0.00 | Record return 0.01 | Apply linked return once | 131.28 | 0.00 | 743.97 |
| AID-01267 | 175.05 | 43.76 | 0.00 | Record return 65.65 | Apply linked return once | 65.64 | 0.00 | 809.61 |
| AID-01268 | 175.05 | 43.76 | 0.00 | Record return 131.29 | Apply linked return once | 0.00 | 0.00 | 875.25 |
| AID-01269 | 175.05 | 43.76 | 0.00 | Record return 131.30 | Return exceeds net fulfillment | 131.29 | 0.00 | 743.96 |
| AID-01270 | 175.05 | 43.76 | 297.58 | Request new 288.83 | Reserve once | 131.29 | 586.41 | 157.55 |
| AID-01271 | 175.05 | 43.76 | 297.58 | Request new 446.37 | Reserve once | 131.29 | 743.95 | 0.01 |
| AID-01272 | 175.05 | 43.76 | 297.58 | Request new 446.38 | Reserve once | 131.29 | 743.96 | 0.00 |
| AID-01273 | 175.05 | 43.76 | 297.58 | Request new 446.39 | Exceeds remaining authority | 131.29 | 297.58 | 446.38 |
| AID-01274 | 175.05 | 43.76 | 297.58 | Confirm pending 297.58 | Settle original once | 428.87 | 0.00 | 446.38 |
| AID-01275 | 175.05 | 43.76 | 297.58 | Fail pending 297.58 | Release pending reservation | 131.29 | 0.00 | 743.96 |
| AID-01276 | 175.05 | 43.76 | 297.58 | Replay settled 175.05 | Original receipt; no new effect | 131.29 | 297.58 | 446.38 |
| AID-01277 | 175.05 | 43.76 | 297.58 | Record return 0.01 | Apply linked return once | 131.28 | 297.58 | 446.39 |
| AID-01278 | 175.05 | 43.76 | 297.58 | Record return 65.65 | Apply linked return once | 65.64 | 297.58 | 512.03 |
| AID-01279 | 175.05 | 43.76 | 297.58 | Record return 131.29 | Apply linked return once | 0.00 | 297.58 | 577.67 |
| AID-01280 | 175.05 | 43.76 | 297.58 | Record return 131.30 | Return exceeds net fulfillment | 131.29 | 297.58 | 446.38 |
| AID-01281 | 175.05 | 43.76 | 743.96 | Request new 0.01 | Exceeds remaining authority | 131.29 | 743.96 | 0.00 |
| AID-01282 | 175.05 | 43.76 | 743.96 | Request new 288.83 | Exceeds remaining authority | 131.29 | 743.96 | 0.00 |
| AID-01283 | 175.05 | 43.76 | 743.96 | Confirm pending 743.96 | Settle original once | 875.25 | 0.00 | 0.00 |
| AID-01284 | 175.05 | 43.76 | 743.96 | Fail pending 743.96 | Release pending reservation | 131.29 | 0.00 | 743.96 |
| AID-01285 | 175.05 | 43.76 | 743.96 | Replay settled 175.05 | Original receipt; no new effect | 131.29 | 743.96 | 0.00 |
| AID-01286 | 175.05 | 43.76 | 743.96 | Record return 0.01 | Apply linked return once | 131.28 | 743.96 | 0.01 |
| AID-01287 | 175.05 | 43.76 | 743.96 | Record return 65.65 | Apply linked return once | 65.64 | 743.96 | 65.65 |
| AID-01288 | 175.05 | 43.76 | 743.96 | Record return 131.29 | Apply linked return once | 0.00 | 743.96 | 131.29 |
| AID-01289 | 175.05 | 43.76 | 743.96 | Record return 131.30 | Return exceeds net fulfillment | 131.29 | 743.96 | 0.00 |
| AID-01290 | 175.05 | 175.05 | 0.00 | Request new 288.83 | Reserve once | 0.00 | 288.83 | 586.42 |
| AID-01291 | 175.05 | 175.05 | 0.00 | Request new 875.24 | Reserve once | 0.00 | 875.24 | 0.01 |
| AID-01292 | 175.05 | 175.05 | 0.00 | Request new 875.25 | Reserve once | 0.00 | 875.25 | 0.00 |
| AID-01293 | 175.05 | 175.05 | 0.00 | Request new 875.26 | Exceeds remaining authority | 0.00 | 0.00 | 875.25 |
| AID-01294 | 175.05 | 175.05 | 0.00 | Replay settled 175.05 | Original receipt; no new effect | 0.00 | 0.00 | 875.25 |
| AID-01295 | 175.05 | 175.05 | 350.10 | Request new 288.83 | Reserve once | 0.00 | 638.93 | 236.32 |
| AID-01296 | 175.05 | 175.05 | 350.10 | Request new 525.14 | Reserve once | 0.00 | 875.24 | 0.01 |
| AID-01297 | 175.05 | 175.05 | 350.10 | Request new 525.15 | Reserve once | 0.00 | 875.25 | 0.00 |
| AID-01298 | 175.05 | 175.05 | 350.10 | Request new 525.16 | Exceeds remaining authority | 0.00 | 350.10 | 525.15 |
| AID-01299 | 175.05 | 175.05 | 350.10 | Confirm pending 350.10 | Settle original once | 350.10 | 0.00 | 525.15 |
| AID-01300 | 175.05 | 175.05 | 350.10 | Fail pending 350.10 | Release pending reservation | 0.00 | 0.00 | 875.25 |
| AID-01301 | 175.05 | 175.05 | 350.10 | Replay settled 175.05 | Original receipt; no new effect | 0.00 | 350.10 | 525.15 |
| AID-01302 | 175.05 | 175.05 | 875.25 | Request new 0.01 | Exceeds remaining authority | 0.00 | 875.25 | 0.00 |
| AID-01303 | 175.05 | 175.05 | 875.25 | Request new 288.83 | Exceeds remaining authority | 0.00 | 875.25 | 0.00 |
| AID-01304 | 175.05 | 175.05 | 875.25 | Confirm pending 875.25 | Settle original once | 875.25 | 0.00 | 0.00 |
| AID-01305 | 175.05 | 175.05 | 875.25 | Fail pending 875.25 | Release pending reservation | 0.00 | 0.00 | 875.25 |
| AID-01306 | 175.05 | 175.05 | 875.25 | Replay settled 175.05 | Original receipt; no new effect | 0.00 | 875.25 | 0.00 |
| AID-01307 | 437.63 | 0.00 | 0.00 | Request new 288.83 | Reserve once | 437.63 | 288.83 | 148.79 |
| AID-01308 | 437.63 | 0.00 | 0.00 | Request new 437.61 | Reserve once | 437.63 | 437.61 | 0.01 |
| AID-01309 | 437.63 | 0.00 | 0.00 | Request new 437.62 | Reserve once | 437.63 | 437.62 | 0.00 |
| AID-01310 | 437.63 | 0.00 | 0.00 | Request new 437.63 | Exceeds remaining authority | 437.63 | 0.00 | 437.62 |
| AID-01311 | 437.63 | 0.00 | 0.00 | Replay settled 437.63 | Original receipt; no new effect | 437.63 | 0.00 | 437.62 |
| AID-01312 | 437.63 | 0.00 | 0.00 | Record return 0.01 | Apply linked return once | 437.62 | 0.00 | 437.63 |
| AID-01313 | 437.63 | 0.00 | 0.00 | Record return 218.82 | Apply linked return once | 218.81 | 0.00 | 656.44 |
| AID-01314 | 437.63 | 0.00 | 0.00 | Record return 437.63 | Apply linked return once | 0.00 | 0.00 | 875.25 |
| AID-01315 | 437.63 | 0.00 | 0.00 | Record return 437.64 | Return exceeds net fulfillment | 437.63 | 0.00 | 437.62 |
| AID-01316 | 437.63 | 0.00 | 175.05 | Request new 262.56 | Reserve once | 437.63 | 437.61 | 0.01 |
| AID-01317 | 437.63 | 0.00 | 175.05 | Request new 262.57 | Reserve once | 437.63 | 437.62 | 0.00 |
| AID-01318 | 437.63 | 0.00 | 175.05 | Request new 262.58 | Exceeds remaining authority | 437.63 | 175.05 | 262.57 |
| AID-01319 | 437.63 | 0.00 | 175.05 | Request new 288.83 | Exceeds remaining authority | 437.63 | 175.05 | 262.57 |
| AID-01320 | 437.63 | 0.00 | 175.05 | Confirm pending 175.05 | Settle original once | 612.68 | 0.00 | 262.57 |
| AID-01321 | 437.63 | 0.00 | 175.05 | Fail pending 175.05 | Release pending reservation | 437.63 | 0.00 | 437.62 |
| AID-01322 | 437.63 | 0.00 | 175.05 | Replay settled 437.63 | Original receipt; no new effect | 437.63 | 175.05 | 262.57 |
| AID-01323 | 437.63 | 0.00 | 175.05 | Record return 0.01 | Apply linked return once | 437.62 | 175.05 | 262.58 |
| AID-01324 | 437.63 | 0.00 | 175.05 | Record return 218.82 | Apply linked return once | 218.81 | 175.05 | 481.39 |
| AID-01325 | 437.63 | 0.00 | 175.05 | Record return 437.63 | Apply linked return once | 0.00 | 175.05 | 700.20 |
| AID-01326 | 437.63 | 0.00 | 175.05 | Record return 437.64 | Return exceeds net fulfillment | 437.63 | 175.05 | 262.57 |
| AID-01327 | 437.63 | 0.00 | 437.62 | Request new 0.01 | Exceeds remaining authority | 437.63 | 437.62 | 0.00 |
| AID-01328 | 437.63 | 0.00 | 437.62 | Request new 288.83 | Exceeds remaining authority | 437.63 | 437.62 | 0.00 |
| AID-01329 | 437.63 | 0.00 | 437.62 | Confirm pending 437.62 | Settle original once | 875.25 | 0.00 | 0.00 |
| AID-01330 | 437.63 | 0.00 | 437.62 | Fail pending 437.62 | Release pending reservation | 437.63 | 0.00 | 437.62 |
| AID-01331 | 437.63 | 0.00 | 437.62 | Replay settled 437.63 | Original receipt; no new effect | 437.63 | 437.62 | 0.00 |
| AID-01332 | 437.63 | 0.00 | 437.62 | Record return 0.01 | Apply linked return once | 437.62 | 437.62 | 0.01 |
| AID-01333 | 437.63 | 0.00 | 437.62 | Record return 218.82 | Apply linked return once | 218.81 | 437.62 | 218.82 |
| AID-01334 | 437.63 | 0.00 | 437.62 | Record return 437.63 | Apply linked return once | 0.00 | 437.62 | 437.63 |
| AID-01335 | 437.63 | 0.00 | 437.62 | Record return 437.64 | Return exceeds net fulfillment | 437.63 | 437.62 | 0.00 |
| AID-01336 | 437.63 | 0.01 | 0.00 | Request new 288.83 | Reserve once | 437.62 | 288.83 | 148.80 |
| AID-01337 | 437.63 | 0.01 | 0.00 | Request new 437.62 | Reserve once | 437.62 | 437.62 | 0.01 |
| AID-01338 | 437.63 | 0.01 | 0.00 | Request new 437.63 | Reserve once | 437.62 | 437.63 | 0.00 |
| AID-01339 | 437.63 | 0.01 | 0.00 | Request new 437.64 | Exceeds remaining authority | 437.62 | 0.00 | 437.63 |
| AID-01340 | 437.63 | 0.01 | 0.00 | Replay settled 437.63 | Original receipt; no new effect | 437.62 | 0.00 | 437.63 |
| AID-01341 | 437.63 | 0.01 | 0.00 | Record return 0.01 | Apply linked return once | 437.61 | 0.00 | 437.64 |
| AID-01342 | 437.63 | 0.01 | 0.00 | Record return 218.81 | Apply linked return once | 218.81 | 0.00 | 656.44 |
| AID-01343 | 437.63 | 0.01 | 0.00 | Record return 437.62 | Apply linked return once | 0.00 | 0.00 | 875.25 |
| AID-01344 | 437.63 | 0.01 | 0.00 | Record return 437.63 | Return exceeds net fulfillment | 437.62 | 0.00 | 437.63 |
| AID-01345 | 437.63 | 0.01 | 175.05 | Request new 262.57 | Reserve once | 437.62 | 437.62 | 0.01 |
| AID-01346 | 437.63 | 0.01 | 175.05 | Request new 262.58 | Reserve once | 437.62 | 437.63 | 0.00 |
| AID-01347 | 437.63 | 0.01 | 175.05 | Request new 262.59 | Exceeds remaining authority | 437.62 | 175.05 | 262.58 |
| AID-01348 | 437.63 | 0.01 | 175.05 | Request new 288.83 | Exceeds remaining authority | 437.62 | 175.05 | 262.58 |
| AID-01349 | 437.63 | 0.01 | 175.05 | Confirm pending 175.05 | Settle original once | 612.67 | 0.00 | 262.58 |
| AID-01350 | 437.63 | 0.01 | 175.05 | Fail pending 175.05 | Release pending reservation | 437.62 | 0.00 | 437.63 |
| AID-01351 | 437.63 | 0.01 | 175.05 | Replay settled 437.63 | Original receipt; no new effect | 437.62 | 175.05 | 262.58 |
| AID-01352 | 437.63 | 0.01 | 175.05 | Record return 0.01 | Apply linked return once | 437.61 | 175.05 | 262.59 |
| AID-01353 | 437.63 | 0.01 | 175.05 | Record return 218.81 | Apply linked return once | 218.81 | 175.05 | 481.39 |
| AID-01354 | 437.63 | 0.01 | 175.05 | Record return 437.62 | Apply linked return once | 0.00 | 175.05 | 700.20 |
| AID-01355 | 437.63 | 0.01 | 175.05 | Record return 437.63 | Return exceeds net fulfillment | 437.62 | 175.05 | 262.58 |
| AID-01356 | 437.63 | 0.01 | 437.63 | Request new 0.01 | Exceeds remaining authority | 437.62 | 437.63 | 0.00 |
| AID-01357 | 437.63 | 0.01 | 437.63 | Request new 288.83 | Exceeds remaining authority | 437.62 | 437.63 | 0.00 |
| AID-01358 | 437.63 | 0.01 | 437.63 | Confirm pending 437.63 | Settle original once | 875.25 | 0.00 | 0.00 |
| AID-01359 | 437.63 | 0.01 | 437.63 | Fail pending 437.63 | Release pending reservation | 437.62 | 0.00 | 437.63 |
| AID-01360 | 437.63 | 0.01 | 437.63 | Replay settled 437.63 | Original receipt; no new effect | 437.62 | 437.63 | 0.00 |
| AID-01361 | 437.63 | 0.01 | 437.63 | Record return 0.01 | Apply linked return once | 437.61 | 437.63 | 0.01 |
| AID-01362 | 437.63 | 0.01 | 437.63 | Record return 218.81 | Apply linked return once | 218.81 | 437.63 | 218.81 |
| AID-01363 | 437.63 | 0.01 | 437.63 | Record return 437.62 | Apply linked return once | 0.00 | 437.63 | 437.62 |
| AID-01364 | 437.63 | 0.01 | 437.63 | Record return 437.63 | Return exceeds net fulfillment | 437.62 | 437.63 | 0.00 |
| AID-01365 | 437.63 | 109.41 | 0.00 | Request new 288.83 | Reserve once | 328.22 | 288.83 | 258.20 |
| AID-01366 | 437.63 | 109.41 | 0.00 | Request new 547.02 | Reserve once | 328.22 | 547.02 | 0.01 |
| AID-01367 | 437.63 | 109.41 | 0.00 | Request new 547.03 | Reserve once | 328.22 | 547.03 | 0.00 |
| AID-01368 | 437.63 | 109.41 | 0.00 | Request new 547.04 | Exceeds remaining authority | 328.22 | 0.00 | 547.03 |
| AID-01369 | 437.63 | 109.41 | 0.00 | Replay settled 437.63 | Original receipt; no new effect | 328.22 | 0.00 | 547.03 |
| AID-01370 | 437.63 | 109.41 | 0.00 | Record return 0.01 | Apply linked return once | 328.21 | 0.00 | 547.04 |
| AID-01371 | 437.63 | 109.41 | 0.00 | Record return 164.11 | Apply linked return once | 164.11 | 0.00 | 711.14 |
| AID-01372 | 437.63 | 109.41 | 0.00 | Record return 328.22 | Apply linked return once | 0.00 | 0.00 | 875.25 |
| AID-01373 | 437.63 | 109.41 | 0.00 | Record return 328.23 | Return exceeds net fulfillment | 328.22 | 0.00 | 547.03 |
| AID-01374 | 437.63 | 109.41 | 218.81 | Request new 288.83 | Reserve once | 328.22 | 507.64 | 39.39 |
| AID-01375 | 437.63 | 109.41 | 218.81 | Request new 328.21 | Reserve once | 328.22 | 547.02 | 0.01 |
| AID-01376 | 437.63 | 109.41 | 218.81 | Request new 328.22 | Reserve once | 328.22 | 547.03 | 0.00 |
| AID-01377 | 437.63 | 109.41 | 218.81 | Request new 328.23 | Exceeds remaining authority | 328.22 | 218.81 | 328.22 |
| AID-01378 | 437.63 | 109.41 | 218.81 | Confirm pending 218.81 | Settle original once | 547.03 | 0.00 | 328.22 |
| AID-01379 | 437.63 | 109.41 | 218.81 | Fail pending 218.81 | Release pending reservation | 328.22 | 0.00 | 547.03 |
| AID-01380 | 437.63 | 109.41 | 218.81 | Replay settled 437.63 | Original receipt; no new effect | 328.22 | 218.81 | 328.22 |
| AID-01381 | 437.63 | 109.41 | 218.81 | Record return 0.01 | Apply linked return once | 328.21 | 218.81 | 328.23 |
| AID-01382 | 437.63 | 109.41 | 218.81 | Record return 164.11 | Apply linked return once | 164.11 | 218.81 | 492.33 |
| AID-01383 | 437.63 | 109.41 | 218.81 | Record return 328.22 | Apply linked return once | 0.00 | 218.81 | 656.44 |
| AID-01384 | 437.63 | 109.41 | 218.81 | Record return 328.23 | Return exceeds net fulfillment | 328.22 | 218.81 | 328.22 |
| AID-01385 | 437.63 | 109.41 | 547.03 | Request new 0.01 | Exceeds remaining authority | 328.22 | 547.03 | 0.00 |
| AID-01386 | 437.63 | 109.41 | 547.03 | Request new 288.83 | Exceeds remaining authority | 328.22 | 547.03 | 0.00 |
| AID-01387 | 437.63 | 109.41 | 547.03 | Confirm pending 547.03 | Settle original once | 875.25 | 0.00 | 0.00 |
| AID-01388 | 437.63 | 109.41 | 547.03 | Fail pending 547.03 | Release pending reservation | 328.22 | 0.00 | 547.03 |
| AID-01389 | 437.63 | 109.41 | 547.03 | Replay settled 437.63 | Original receipt; no new effect | 328.22 | 547.03 | 0.00 |
| AID-01390 | 437.63 | 109.41 | 547.03 | Record return 0.01 | Apply linked return once | 328.21 | 547.03 | 0.01 |
| AID-01391 | 437.63 | 109.41 | 547.03 | Record return 164.11 | Apply linked return once | 164.11 | 547.03 | 164.11 |
| AID-01392 | 437.63 | 109.41 | 547.03 | Record return 328.22 | Apply linked return once | 0.00 | 547.03 | 328.22 |
| AID-01393 | 437.63 | 109.41 | 547.03 | Record return 328.23 | Return exceeds net fulfillment | 328.22 | 547.03 | 0.00 |
| AID-01394 | 437.63 | 437.63 | 0.00 | Request new 288.83 | Reserve once | 0.00 | 288.83 | 586.42 |
| AID-01395 | 437.63 | 437.63 | 0.00 | Request new 875.24 | Reserve once | 0.00 | 875.24 | 0.01 |
| AID-01396 | 437.63 | 437.63 | 0.00 | Request new 875.25 | Reserve once | 0.00 | 875.25 | 0.00 |
| AID-01397 | 437.63 | 437.63 | 0.00 | Request new 875.26 | Exceeds remaining authority | 0.00 | 0.00 | 875.25 |
| AID-01398 | 437.63 | 437.63 | 0.00 | Replay settled 437.63 | Original receipt; no new effect | 0.00 | 0.00 | 875.25 |
| AID-01399 | 437.63 | 437.63 | 350.10 | Request new 288.83 | Reserve once | 0.00 | 638.93 | 236.32 |
| AID-01400 | 437.63 | 437.63 | 350.10 | Request new 525.14 | Reserve once | 0.00 | 875.24 | 0.01 |
| AID-01401 | 437.63 | 437.63 | 350.10 | Request new 525.15 | Reserve once | 0.00 | 875.25 | 0.00 |
| AID-01402 | 437.63 | 437.63 | 350.10 | Request new 525.16 | Exceeds remaining authority | 0.00 | 350.10 | 525.15 |
| AID-01403 | 437.63 | 437.63 | 350.10 | Confirm pending 350.10 | Settle original once | 350.10 | 0.00 | 525.15 |
| AID-01404 | 437.63 | 437.63 | 350.10 | Fail pending 350.10 | Release pending reservation | 0.00 | 0.00 | 875.25 |
| AID-01405 | 437.63 | 437.63 | 350.10 | Replay settled 437.63 | Original receipt; no new effect | 0.00 | 350.10 | 525.15 |
| AID-01406 | 437.63 | 437.63 | 875.25 | Request new 0.01 | Exceeds remaining authority | 0.00 | 875.25 | 0.00 |
| AID-01407 | 437.63 | 437.63 | 875.25 | Request new 288.83 | Exceeds remaining authority | 0.00 | 875.25 | 0.00 |
| AID-01408 | 437.63 | 437.63 | 875.25 | Confirm pending 875.25 | Settle original once | 875.25 | 0.00 | 0.00 |
| AID-01409 | 437.63 | 437.63 | 875.25 | Fail pending 875.25 | Release pending reservation | 0.00 | 0.00 | 875.25 |
| AID-01410 | 437.63 | 437.63 | 875.25 | Replay settled 437.63 | Original receipt; no new effect | 0.00 | 875.25 | 0.00 |
| AID-01411 | 700.20 | 0.00 | 0.00 | Request new 175.04 | Reserve once | 700.20 | 175.04 | 0.01 |
| AID-01412 | 700.20 | 0.00 | 0.00 | Request new 175.05 | Reserve once | 700.20 | 175.05 | 0.00 |
| AID-01413 | 700.20 | 0.00 | 0.00 | Request new 175.06 | Exceeds remaining authority | 700.20 | 0.00 | 175.05 |
| AID-01414 | 700.20 | 0.00 | 0.00 | Request new 288.83 | Exceeds remaining authority | 700.20 | 0.00 | 175.05 |
| AID-01415 | 700.20 | 0.00 | 0.00 | Replay settled 700.20 | Original receipt; no new effect | 700.20 | 0.00 | 175.05 |
| AID-01416 | 700.20 | 0.00 | 0.00 | Record return 0.01 | Apply linked return once | 700.19 | 0.00 | 175.06 |
| AID-01417 | 700.20 | 0.00 | 0.00 | Record return 350.10 | Apply linked return once | 350.10 | 0.00 | 525.15 |
| AID-01418 | 700.20 | 0.00 | 0.00 | Record return 700.20 | Apply linked return once | 0.00 | 0.00 | 875.25 |
| AID-01419 | 700.20 | 0.00 | 0.00 | Record return 700.21 | Return exceeds net fulfillment | 700.20 | 0.00 | 175.05 |
| AID-01420 | 700.20 | 0.00 | 70.02 | Request new 105.02 | Reserve once | 700.20 | 175.04 | 0.01 |
| AID-01421 | 700.20 | 0.00 | 70.02 | Request new 105.03 | Reserve once | 700.20 | 175.05 | 0.00 |
| AID-01422 | 700.20 | 0.00 | 70.02 | Request new 105.04 | Exceeds remaining authority | 700.20 | 70.02 | 105.03 |
| AID-01423 | 700.20 | 0.00 | 70.02 | Request new 288.83 | Exceeds remaining authority | 700.20 | 70.02 | 105.03 |
| AID-01424 | 700.20 | 0.00 | 70.02 | Confirm pending 70.02 | Settle original once | 770.22 | 0.00 | 105.03 |
| AID-01425 | 700.20 | 0.00 | 70.02 | Fail pending 70.02 | Release pending reservation | 700.20 | 0.00 | 175.05 |
| AID-01426 | 700.20 | 0.00 | 70.02 | Replay settled 700.20 | Original receipt; no new effect | 700.20 | 70.02 | 105.03 |
| AID-01427 | 700.20 | 0.00 | 70.02 | Record return 0.01 | Apply linked return once | 700.19 | 70.02 | 105.04 |
| AID-01428 | 700.20 | 0.00 | 70.02 | Record return 350.10 | Apply linked return once | 350.10 | 70.02 | 455.13 |
| AID-01429 | 700.20 | 0.00 | 70.02 | Record return 700.20 | Apply linked return once | 0.00 | 70.02 | 805.23 |
| AID-01430 | 700.20 | 0.00 | 70.02 | Record return 700.21 | Return exceeds net fulfillment | 700.20 | 70.02 | 105.03 |
| AID-01431 | 700.20 | 0.00 | 175.05 | Request new 0.01 | Exceeds remaining authority | 700.20 | 175.05 | 0.00 |
| AID-01432 | 700.20 | 0.00 | 175.05 | Request new 288.83 | Exceeds remaining authority | 700.20 | 175.05 | 0.00 |
| AID-01433 | 700.20 | 0.00 | 175.05 | Confirm pending 175.05 | Settle original once | 875.25 | 0.00 | 0.00 |
| AID-01434 | 700.20 | 0.00 | 175.05 | Fail pending 175.05 | Release pending reservation | 700.20 | 0.00 | 175.05 |
| AID-01435 | 700.20 | 0.00 | 175.05 | Replay settled 700.20 | Original receipt; no new effect | 700.20 | 175.05 | 0.00 |
| AID-01436 | 700.20 | 0.00 | 175.05 | Record return 0.01 | Apply linked return once | 700.19 | 175.05 | 0.01 |
| AID-01437 | 700.20 | 0.00 | 175.05 | Record return 350.10 | Apply linked return once | 350.10 | 175.05 | 350.10 |
| AID-01438 | 700.20 | 0.00 | 175.05 | Record return 700.20 | Apply linked return once | 0.00 | 175.05 | 700.20 |
| AID-01439 | 700.20 | 0.00 | 175.05 | Record return 700.21 | Return exceeds net fulfillment | 700.20 | 175.05 | 0.00 |
| AID-01440 | 700.20 | 0.01 | 0.00 | Request new 175.05 | Reserve once | 700.19 | 175.05 | 0.01 |
| AID-01441 | 700.20 | 0.01 | 0.00 | Request new 175.06 | Reserve once | 700.19 | 175.06 | 0.00 |
| AID-01442 | 700.20 | 0.01 | 0.00 | Request new 175.07 | Exceeds remaining authority | 700.19 | 0.00 | 175.06 |
| AID-01443 | 700.20 | 0.01 | 0.00 | Request new 288.83 | Exceeds remaining authority | 700.19 | 0.00 | 175.06 |
| AID-01444 | 700.20 | 0.01 | 0.00 | Replay settled 700.20 | Original receipt; no new effect | 700.19 | 0.00 | 175.06 |
| AID-01445 | 700.20 | 0.01 | 0.00 | Record return 0.01 | Apply linked return once | 700.18 | 0.00 | 175.07 |
| AID-01446 | 700.20 | 0.01 | 0.00 | Record return 350.10 | Apply linked return once | 350.09 | 0.00 | 525.16 |
| AID-01447 | 700.20 | 0.01 | 0.00 | Record return 700.19 | Apply linked return once | 0.00 | 0.00 | 875.25 |
| AID-01448 | 700.20 | 0.01 | 0.00 | Record return 700.20 | Return exceeds net fulfillment | 700.19 | 0.00 | 175.06 |
| AID-01449 | 700.20 | 0.01 | 70.02 | Request new 105.03 | Reserve once | 700.19 | 175.05 | 0.01 |
| AID-01450 | 700.20 | 0.01 | 70.02 | Request new 105.04 | Reserve once | 700.19 | 175.06 | 0.00 |
| AID-01451 | 700.20 | 0.01 | 70.02 | Request new 105.05 | Exceeds remaining authority | 700.19 | 70.02 | 105.04 |
| AID-01452 | 700.20 | 0.01 | 70.02 | Request new 288.83 | Exceeds remaining authority | 700.19 | 70.02 | 105.04 |
| AID-01453 | 700.20 | 0.01 | 70.02 | Confirm pending 70.02 | Settle original once | 770.21 | 0.00 | 105.04 |
| AID-01454 | 700.20 | 0.01 | 70.02 | Fail pending 70.02 | Release pending reservation | 700.19 | 0.00 | 175.06 |
| AID-01455 | 700.20 | 0.01 | 70.02 | Replay settled 700.20 | Original receipt; no new effect | 700.19 | 70.02 | 105.04 |
| AID-01456 | 700.20 | 0.01 | 70.02 | Record return 0.01 | Apply linked return once | 700.18 | 70.02 | 105.05 |
| AID-01457 | 700.20 | 0.01 | 70.02 | Record return 350.10 | Apply linked return once | 350.09 | 70.02 | 455.14 |
| AID-01458 | 700.20 | 0.01 | 70.02 | Record return 700.19 | Apply linked return once | 0.00 | 70.02 | 805.23 |
| AID-01459 | 700.20 | 0.01 | 70.02 | Record return 700.20 | Return exceeds net fulfillment | 700.19 | 70.02 | 105.04 |
| AID-01460 | 700.20 | 0.01 | 175.06 | Request new 0.01 | Exceeds remaining authority | 700.19 | 175.06 | 0.00 |
| AID-01461 | 700.20 | 0.01 | 175.06 | Request new 288.83 | Exceeds remaining authority | 700.19 | 175.06 | 0.00 |
| AID-01462 | 700.20 | 0.01 | 175.06 | Confirm pending 175.06 | Settle original once | 875.25 | 0.00 | 0.00 |
| AID-01463 | 700.20 | 0.01 | 175.06 | Fail pending 175.06 | Release pending reservation | 700.19 | 0.00 | 175.06 |
| AID-01464 | 700.20 | 0.01 | 175.06 | Replay settled 700.20 | Original receipt; no new effect | 700.19 | 175.06 | 0.00 |
| AID-01465 | 700.20 | 0.01 | 175.06 | Record return 0.01 | Apply linked return once | 700.18 | 175.06 | 0.01 |
| AID-01466 | 700.20 | 0.01 | 175.06 | Record return 350.10 | Apply linked return once | 350.09 | 175.06 | 350.10 |
| AID-01467 | 700.20 | 0.01 | 175.06 | Record return 700.19 | Apply linked return once | 0.00 | 175.06 | 700.19 |
| AID-01468 | 700.20 | 0.01 | 175.06 | Record return 700.20 | Return exceeds net fulfillment | 700.19 | 175.06 | 0.00 |
| AID-01469 | 700.20 | 175.05 | 0.00 | Request new 288.83 | Reserve once | 525.15 | 288.83 | 61.27 |
| AID-01470 | 700.20 | 175.05 | 0.00 | Request new 350.09 | Reserve once | 525.15 | 350.09 | 0.01 |
| AID-01471 | 700.20 | 175.05 | 0.00 | Request new 350.10 | Reserve once | 525.15 | 350.10 | 0.00 |
| AID-01472 | 700.20 | 175.05 | 0.00 | Request new 350.11 | Exceeds remaining authority | 525.15 | 0.00 | 350.10 |
| AID-01473 | 700.20 | 175.05 | 0.00 | Replay settled 700.20 | Original receipt; no new effect | 525.15 | 0.00 | 350.10 |
| AID-01474 | 700.20 | 175.05 | 0.00 | Record return 0.01 | Apply linked return once | 525.14 | 0.00 | 350.11 |
| AID-01475 | 700.20 | 175.05 | 0.00 | Record return 262.58 | Apply linked return once | 262.57 | 0.00 | 612.68 |
| AID-01476 | 700.20 | 175.05 | 0.00 | Record return 525.15 | Apply linked return once | 0.00 | 0.00 | 875.25 |
| AID-01477 | 700.20 | 175.05 | 0.00 | Record return 525.16 | Return exceeds net fulfillment | 525.15 | 0.00 | 350.10 |
| AID-01478 | 700.20 | 175.05 | 140.04 | Request new 210.05 | Reserve once | 525.15 | 350.09 | 0.01 |
| AID-01479 | 700.20 | 175.05 | 140.04 | Request new 210.06 | Reserve once | 525.15 | 350.10 | 0.00 |
| AID-01480 | 700.20 | 175.05 | 140.04 | Request new 210.07 | Exceeds remaining authority | 525.15 | 140.04 | 210.06 |
| AID-01481 | 700.20 | 175.05 | 140.04 | Request new 288.83 | Exceeds remaining authority | 525.15 | 140.04 | 210.06 |
| AID-01482 | 700.20 | 175.05 | 140.04 | Confirm pending 140.04 | Settle original once | 665.19 | 0.00 | 210.06 |
| AID-01483 | 700.20 | 175.05 | 140.04 | Fail pending 140.04 | Release pending reservation | 525.15 | 0.00 | 350.10 |
| AID-01484 | 700.20 | 175.05 | 140.04 | Replay settled 700.20 | Original receipt; no new effect | 525.15 | 140.04 | 210.06 |
| AID-01485 | 700.20 | 175.05 | 140.04 | Record return 0.01 | Apply linked return once | 525.14 | 140.04 | 210.07 |
| AID-01486 | 700.20 | 175.05 | 140.04 | Record return 262.58 | Apply linked return once | 262.57 | 140.04 | 472.64 |
| AID-01487 | 700.20 | 175.05 | 140.04 | Record return 525.15 | Apply linked return once | 0.00 | 140.04 | 735.21 |
| AID-01488 | 700.20 | 175.05 | 140.04 | Record return 525.16 | Return exceeds net fulfillment | 525.15 | 140.04 | 210.06 |
| AID-01489 | 700.20 | 175.05 | 350.10 | Request new 0.01 | Exceeds remaining authority | 525.15 | 350.10 | 0.00 |
| AID-01490 | 700.20 | 175.05 | 350.10 | Request new 288.83 | Exceeds remaining authority | 525.15 | 350.10 | 0.00 |
| AID-01491 | 700.20 | 175.05 | 350.10 | Confirm pending 350.10 | Settle original once | 875.25 | 0.00 | 0.00 |
| AID-01492 | 700.20 | 175.05 | 350.10 | Fail pending 350.10 | Release pending reservation | 525.15 | 0.00 | 350.10 |
| AID-01493 | 700.20 | 175.05 | 350.10 | Replay settled 700.20 | Original receipt; no new effect | 525.15 | 350.10 | 0.00 |
| AID-01494 | 700.20 | 175.05 | 350.10 | Record return 0.01 | Apply linked return once | 525.14 | 350.10 | 0.01 |
| AID-01495 | 700.20 | 175.05 | 350.10 | Record return 262.58 | Apply linked return once | 262.57 | 350.10 | 262.58 |
| AID-01496 | 700.20 | 175.05 | 350.10 | Record return 525.15 | Apply linked return once | 0.00 | 350.10 | 525.15 |
| AID-01497 | 700.20 | 175.05 | 350.10 | Record return 525.16 | Return exceeds net fulfillment | 525.15 | 350.10 | 0.00 |
| AID-01498 | 700.20 | 700.20 | 0.00 | Request new 288.83 | Reserve once | 0.00 | 288.83 | 586.42 |
| AID-01499 | 700.20 | 700.20 | 0.00 | Request new 875.24 | Reserve once | 0.00 | 875.24 | 0.01 |
| AID-01500 | 700.20 | 700.20 | 0.00 | Request new 875.25 | Reserve once | 0.00 | 875.25 | 0.00 |
| AID-01501 | 700.20 | 700.20 | 0.00 | Request new 875.26 | Exceeds remaining authority | 0.00 | 0.00 | 875.25 |
| AID-01502 | 700.20 | 700.20 | 0.00 | Replay settled 700.20 | Original receipt; no new effect | 0.00 | 0.00 | 875.25 |
| AID-01503 | 700.20 | 700.20 | 350.10 | Request new 288.83 | Reserve once | 0.00 | 638.93 | 236.32 |
| AID-01504 | 700.20 | 700.20 | 350.10 | Request new 525.14 | Reserve once | 0.00 | 875.24 | 0.01 |
| AID-01505 | 700.20 | 700.20 | 350.10 | Request new 525.15 | Reserve once | 0.00 | 875.25 | 0.00 |
| AID-01506 | 700.20 | 700.20 | 350.10 | Request new 525.16 | Exceeds remaining authority | 0.00 | 350.10 | 525.15 |
| AID-01507 | 700.20 | 700.20 | 350.10 | Confirm pending 350.10 | Settle original once | 350.10 | 0.00 | 525.15 |
| AID-01508 | 700.20 | 700.20 | 350.10 | Fail pending 350.10 | Release pending reservation | 0.00 | 0.00 | 875.25 |
