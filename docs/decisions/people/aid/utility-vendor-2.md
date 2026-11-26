# Utility vendor — part 2 of 2

[Policy and other cases](README.md)

One approved award of 350.00 currency units; all inputs use currency units at 2 decimal places. One original settled fulfillment, when present, may be partially returned. An outstanding payment or stock issue is reserved against authority. Historical issued and returned amounts are kept even when the net amount is zero. Reviewers can reconstruct this case using the supplied opening facts.

| Case | Opening gross | Opening returns | Opening reserved | Requested event and value | Decision | New net delivered | New reserved | New free authority |
|---|---|---|---|---|---|---|---|---|
| AID-00321 | 280.00 | 280.00 | 140.00 | Replay settled 280.00 | Original receipt; no new effect | 0.00 | 140.00 | 210.00 |
| AID-00322 | 280.00 | 280.00 | 350.00 | Request new 0.01 | Exceeds remaining authority | 0.00 | 350.00 | 0.00 |
| AID-00323 | 280.00 | 280.00 | 350.00 | Request new 115.50 | Exceeds remaining authority | 0.00 | 350.00 | 0.00 |
| AID-00324 | 280.00 | 280.00 | 350.00 | Confirm pending 350.00 | Settle original once | 350.00 | 0.00 | 0.00 |
| AID-00325 | 280.00 | 280.00 | 350.00 | Fail pending 350.00 | Release pending reservation | 0.00 | 0.00 | 350.00 |
| AID-00326 | 280.00 | 280.00 | 350.00 | Replay settled 280.00 | Original receipt; no new effect | 0.00 | 350.00 | 0.00 |
| AID-00327 | 350.00 | 0.00 | 0.00 | Request new 0.01 | Exceeds remaining authority | 350.00 | 0.00 | 0.00 |
| AID-00328 | 350.00 | 0.00 | 0.00 | Request new 115.50 | Exceeds remaining authority | 350.00 | 0.00 | 0.00 |
| AID-00329 | 350.00 | 0.00 | 0.00 | Replay settled 350.00 | Original receipt; no new effect | 350.00 | 0.00 | 0.00 |
| AID-00330 | 350.00 | 0.00 | 0.00 | Record return 0.01 | Apply linked return once | 349.99 | 0.00 | 0.01 |
| AID-00331 | 350.00 | 0.00 | 0.00 | Record return 175.00 | Apply linked return once | 175.00 | 0.00 | 175.00 |
| AID-00332 | 350.00 | 0.00 | 0.00 | Record return 350.00 | Apply linked return once | 0.00 | 0.00 | 350.00 |
| AID-00333 | 350.00 | 0.00 | 0.00 | Record return 350.01 | Return exceeds net fulfillment | 350.00 | 0.00 | 0.00 |
| AID-00334 | 350.00 | 0.01 | 0.00 | Request new 0.01 | Reserve once | 349.99 | 0.01 | 0.00 |
| AID-00335 | 350.00 | 0.01 | 0.00 | Request new 0.02 | Exceeds remaining authority | 349.99 | 0.00 | 0.01 |
| AID-00336 | 350.00 | 0.01 | 0.00 | Request new 115.50 | Exceeds remaining authority | 349.99 | 0.00 | 0.01 |
| AID-00337 | 350.00 | 0.01 | 0.00 | Replay settled 350.00 | Original receipt; no new effect | 349.99 | 0.00 | 0.01 |
| AID-00338 | 350.00 | 0.01 | 0.00 | Record return 0.01 | Apply linked return once | 349.98 | 0.00 | 0.02 |
| AID-00339 | 350.00 | 0.01 | 0.00 | Record return 175.00 | Apply linked return once | 174.99 | 0.00 | 175.01 |
| AID-00340 | 350.00 | 0.01 | 0.00 | Record return 349.99 | Apply linked return once | 0.00 | 0.00 | 350.00 |
| AID-00341 | 350.00 | 0.01 | 0.00 | Record return 350.00 | Return exceeds net fulfillment | 349.99 | 0.00 | 0.01 |
| AID-00342 | 350.00 | 0.01 | 0.01 | Request new 0.01 | Exceeds remaining authority | 349.99 | 0.01 | 0.00 |
| AID-00343 | 350.00 | 0.01 | 0.01 | Request new 115.50 | Exceeds remaining authority | 349.99 | 0.01 | 0.00 |
| AID-00344 | 350.00 | 0.01 | 0.01 | Confirm pending 0.01 | Settle original once | 350.00 | 0.00 | 0.00 |
| AID-00345 | 350.00 | 0.01 | 0.01 | Fail pending 0.01 | Release pending reservation | 349.99 | 0.00 | 0.01 |
| AID-00346 | 350.00 | 0.01 | 0.01 | Replay settled 350.00 | Original receipt; no new effect | 349.99 | 0.01 | 0.00 |
| AID-00347 | 350.00 | 0.01 | 0.01 | Record return 0.01 | Apply linked return once | 349.98 | 0.01 | 0.01 |
| AID-00348 | 350.00 | 0.01 | 0.01 | Record return 175.00 | Apply linked return once | 174.99 | 0.01 | 175.00 |
| AID-00349 | 350.00 | 0.01 | 0.01 | Record return 349.99 | Apply linked return once | 0.00 | 0.01 | 349.99 |
| AID-00350 | 350.00 | 0.01 | 0.01 | Record return 350.00 | Return exceeds net fulfillment | 349.99 | 0.01 | 0.00 |
| AID-00351 | 350.00 | 87.50 | 0.00 | Request new 87.49 | Reserve once | 262.50 | 87.49 | 0.01 |
| AID-00352 | 350.00 | 87.50 | 0.00 | Request new 87.50 | Reserve once | 262.50 | 87.50 | 0.00 |
| AID-00353 | 350.00 | 87.50 | 0.00 | Request new 87.51 | Exceeds remaining authority | 262.50 | 0.00 | 87.50 |
| AID-00354 | 350.00 | 87.50 | 0.00 | Request new 115.50 | Exceeds remaining authority | 262.50 | 0.00 | 87.50 |
| AID-00355 | 350.00 | 87.50 | 0.00 | Replay settled 350.00 | Original receipt; no new effect | 262.50 | 0.00 | 87.50 |
| AID-00356 | 350.00 | 87.50 | 0.00 | Record return 0.01 | Apply linked return once | 262.49 | 0.00 | 87.51 |
| AID-00357 | 350.00 | 87.50 | 0.00 | Record return 131.25 | Apply linked return once | 131.25 | 0.00 | 218.75 |
| AID-00358 | 350.00 | 87.50 | 0.00 | Record return 262.50 | Apply linked return once | 0.00 | 0.00 | 350.00 |
| AID-00359 | 350.00 | 87.50 | 0.00 | Record return 262.51 | Return exceeds net fulfillment | 262.50 | 0.00 | 87.50 |
| AID-00360 | 350.00 | 87.50 | 35.00 | Request new 52.49 | Reserve once | 262.50 | 87.49 | 0.01 |
| AID-00361 | 350.00 | 87.50 | 35.00 | Request new 52.50 | Reserve once | 262.50 | 87.50 | 0.00 |
| AID-00362 | 350.00 | 87.50 | 35.00 | Request new 52.51 | Exceeds remaining authority | 262.50 | 35.00 | 52.50 |
| AID-00363 | 350.00 | 87.50 | 35.00 | Request new 115.50 | Exceeds remaining authority | 262.50 | 35.00 | 52.50 |
| AID-00364 | 350.00 | 87.50 | 35.00 | Confirm pending 35.00 | Settle original once | 297.50 | 0.00 | 52.50 |
| AID-00365 | 350.00 | 87.50 | 35.00 | Fail pending 35.00 | Release pending reservation | 262.50 | 0.00 | 87.50 |
| AID-00366 | 350.00 | 87.50 | 35.00 | Replay settled 350.00 | Original receipt; no new effect | 262.50 | 35.00 | 52.50 |
| AID-00367 | 350.00 | 87.50 | 35.00 | Record return 0.01 | Apply linked return once | 262.49 | 35.00 | 52.51 |
| AID-00368 | 350.00 | 87.50 | 35.00 | Record return 131.25 | Apply linked return once | 131.25 | 35.00 | 183.75 |
| AID-00369 | 350.00 | 87.50 | 35.00 | Record return 262.50 | Apply linked return once | 0.00 | 35.00 | 315.00 |
| AID-00370 | 350.00 | 87.50 | 35.00 | Record return 262.51 | Return exceeds net fulfillment | 262.50 | 35.00 | 52.50 |
| AID-00371 | 350.00 | 87.50 | 87.50 | Request new 0.01 | Exceeds remaining authority | 262.50 | 87.50 | 0.00 |
| AID-00372 | 350.00 | 87.50 | 87.50 | Request new 115.50 | Exceeds remaining authority | 262.50 | 87.50 | 0.00 |
| AID-00373 | 350.00 | 87.50 | 87.50 | Confirm pending 87.50 | Settle original once | 350.00 | 0.00 | 0.00 |
| AID-00374 | 350.00 | 87.50 | 87.50 | Fail pending 87.50 | Release pending reservation | 262.50 | 0.00 | 87.50 |
| AID-00375 | 350.00 | 87.50 | 87.50 | Replay settled 350.00 | Original receipt; no new effect | 262.50 | 87.50 | 0.00 |
| AID-00376 | 350.00 | 87.50 | 87.50 | Record return 0.01 | Apply linked return once | 262.49 | 87.50 | 0.01 |
| AID-00377 | 350.00 | 87.50 | 87.50 | Record return 131.25 | Apply linked return once | 131.25 | 87.50 | 131.25 |
| AID-00378 | 350.00 | 87.50 | 87.50 | Record return 262.50 | Apply linked return once | 0.00 | 87.50 | 262.50 |
| AID-00379 | 350.00 | 87.50 | 87.50 | Record return 262.51 | Return exceeds net fulfillment | 262.50 | 87.50 | 0.00 |
| AID-00380 | 350.00 | 350.00 | 0.00 | Request new 115.50 | Reserve once | 0.00 | 115.50 | 234.50 |
| AID-00381 | 350.00 | 350.00 | 0.00 | Request new 349.99 | Reserve once | 0.00 | 349.99 | 0.01 |
| AID-00382 | 350.00 | 350.00 | 0.00 | Request new 350.00 | Reserve once | 0.00 | 350.00 | 0.00 |
| AID-00383 | 350.00 | 350.00 | 0.00 | Request new 350.01 | Exceeds remaining authority | 0.00 | 0.00 | 350.00 |
| AID-00384 | 350.00 | 350.00 | 0.00 | Replay settled 350.00 | Original receipt; no new effect | 0.00 | 0.00 | 350.00 |
| AID-00385 | 350.00 | 350.00 | 140.00 | Request new 115.50 | Reserve once | 0.00 | 255.50 | 94.50 |
| AID-00386 | 350.00 | 350.00 | 140.00 | Request new 209.99 | Reserve once | 0.00 | 349.99 | 0.01 |
| AID-00387 | 350.00 | 350.00 | 140.00 | Request new 210.00 | Reserve once | 0.00 | 350.00 | 0.00 |
| AID-00388 | 350.00 | 350.00 | 140.00 | Request new 210.01 | Exceeds remaining authority | 0.00 | 140.00 | 210.00 |
| AID-00389 | 350.00 | 350.00 | 140.00 | Confirm pending 140.00 | Settle original once | 140.00 | 0.00 | 210.00 |
| AID-00390 | 350.00 | 350.00 | 140.00 | Fail pending 140.00 | Release pending reservation | 0.00 | 0.00 | 350.00 |
| AID-00391 | 350.00 | 350.00 | 140.00 | Replay settled 350.00 | Original receipt; no new effect | 0.00 | 140.00 | 210.00 |
| AID-00392 | 350.00 | 350.00 | 350.00 | Request new 0.01 | Exceeds remaining authority | 0.00 | 350.00 | 0.00 |
| AID-00393 | 350.00 | 350.00 | 350.00 | Request new 115.50 | Exceeds remaining authority | 0.00 | 350.00 | 0.00 |
| AID-00394 | 350.00 | 350.00 | 350.00 | Confirm pending 350.00 | Settle original once | 350.00 | 0.00 | 0.00 |
| AID-00395 | 350.00 | 350.00 | 350.00 | Fail pending 350.00 | Release pending reservation | 0.00 | 0.00 | 350.00 |
| AID-00396 | 350.00 | 350.00 | 350.00 | Replay settled 350.00 | Original receipt; no new effect | 0.00 | 350.00 | 0.00 |
