# Emergency food voucher — part 1 of 2

[Policy and other cases](README.md)

One approved award of 125.50 currency units; all inputs use currency units at 2 decimal places. One original settled fulfillment, when present, may be partially returned. An outstanding payment or stock issue is reserved against authority. Historical issued and returned amounts are kept even when the net amount is zero. Reviewers can reconstruct this case using the supplied opening facts.

| Case | Opening gross | Opening returns | Opening reserved | Requested event and value | Decision | New net delivered | New reserved | New free authority |
|---|---|---|---|---|---|---|---|---|
| AID-00397 | 0.00 | 0.00 | 0.00 | Request new 41.42 | Reserve once | 0.00 | 41.42 | 84.08 |
| AID-00398 | 0.00 | 0.00 | 0.00 | Request new 125.49 | Reserve once | 0.00 | 125.49 | 0.01 |
| AID-00399 | 0.00 | 0.00 | 0.00 | Request new 125.50 | Reserve once | 0.00 | 125.50 | 0.00 |
| AID-00400 | 0.00 | 0.00 | 0.00 | Request new 125.51 | Exceeds remaining authority | 0.00 | 0.00 | 125.50 |
| AID-00401 | 0.00 | 0.00 | 50.20 | Request new 41.42 | Reserve once | 0.00 | 91.62 | 33.88 |
| AID-00402 | 0.00 | 0.00 | 50.20 | Request new 75.29 | Reserve once | 0.00 | 125.49 | 0.01 |
| AID-00403 | 0.00 | 0.00 | 50.20 | Request new 75.30 | Reserve once | 0.00 | 125.50 | 0.00 |
| AID-00404 | 0.00 | 0.00 | 50.20 | Request new 75.31 | Exceeds remaining authority | 0.00 | 50.20 | 75.30 |
| AID-00405 | 0.00 | 0.00 | 50.20 | Confirm pending 50.20 | Settle original once | 50.20 | 0.00 | 75.30 |
| AID-00406 | 0.00 | 0.00 | 50.20 | Fail pending 50.20 | Release pending reservation | 0.00 | 0.00 | 125.50 |
| AID-00407 | 0.00 | 0.00 | 125.50 | Request new 0.01 | Exceeds remaining authority | 0.00 | 125.50 | 0.00 |
| AID-00408 | 0.00 | 0.00 | 125.50 | Request new 41.42 | Exceeds remaining authority | 0.00 | 125.50 | 0.00 |
| AID-00409 | 0.00 | 0.00 | 125.50 | Confirm pending 125.50 | Settle original once | 125.50 | 0.00 | 0.00 |
| AID-00410 | 0.00 | 0.00 | 125.50 | Fail pending 125.50 | Release pending reservation | 0.00 | 0.00 | 125.50 |
| AID-00411 | 25.10 | 0.00 | 0.00 | Request new 41.42 | Reserve once | 25.10 | 41.42 | 58.98 |
| AID-00412 | 25.10 | 0.00 | 0.00 | Request new 100.39 | Reserve once | 25.10 | 100.39 | 0.01 |
| AID-00413 | 25.10 | 0.00 | 0.00 | Request new 100.40 | Reserve once | 25.10 | 100.40 | 0.00 |
| AID-00414 | 25.10 | 0.00 | 0.00 | Request new 100.41 | Exceeds remaining authority | 25.10 | 0.00 | 100.40 |
| AID-00415 | 25.10 | 0.00 | 0.00 | Replay settled 25.10 | Original receipt; no new effect | 25.10 | 0.00 | 100.40 |
| AID-00416 | 25.10 | 0.00 | 0.00 | Record return 0.01 | Apply linked return once | 25.09 | 0.00 | 100.41 |
| AID-00417 | 25.10 | 0.00 | 0.00 | Record return 12.55 | Apply linked return once | 12.55 | 0.00 | 112.95 |
| AID-00418 | 25.10 | 0.00 | 0.00 | Record return 25.10 | Apply linked return once | 0.00 | 0.00 | 125.50 |
| AID-00419 | 25.10 | 0.00 | 0.00 | Record return 25.11 | Return exceeds net fulfillment | 25.10 | 0.00 | 100.40 |
| AID-00420 | 25.10 | 0.00 | 40.16 | Request new 41.42 | Reserve once | 25.10 | 81.58 | 18.82 |
| AID-00421 | 25.10 | 0.00 | 40.16 | Request new 60.23 | Reserve once | 25.10 | 100.39 | 0.01 |
| AID-00422 | 25.10 | 0.00 | 40.16 | Request new 60.24 | Reserve once | 25.10 | 100.40 | 0.00 |
| AID-00423 | 25.10 | 0.00 | 40.16 | Request new 60.25 | Exceeds remaining authority | 25.10 | 40.16 | 60.24 |
| AID-00424 | 25.10 | 0.00 | 40.16 | Confirm pending 40.16 | Settle original once | 65.26 | 0.00 | 60.24 |
| AID-00425 | 25.10 | 0.00 | 40.16 | Fail pending 40.16 | Release pending reservation | 25.10 | 0.00 | 100.40 |
| AID-00426 | 25.10 | 0.00 | 40.16 | Replay settled 25.10 | Original receipt; no new effect | 25.10 | 40.16 | 60.24 |
| AID-00427 | 25.10 | 0.00 | 40.16 | Record return 0.01 | Apply linked return once | 25.09 | 40.16 | 60.25 |
| AID-00428 | 25.10 | 0.00 | 40.16 | Record return 12.55 | Apply linked return once | 12.55 | 40.16 | 72.79 |
| AID-00429 | 25.10 | 0.00 | 40.16 | Record return 25.10 | Apply linked return once | 0.00 | 40.16 | 85.34 |
| AID-00430 | 25.10 | 0.00 | 40.16 | Record return 25.11 | Return exceeds net fulfillment | 25.10 | 40.16 | 60.24 |
| AID-00431 | 25.10 | 0.00 | 100.40 | Request new 0.01 | Exceeds remaining authority | 25.10 | 100.40 | 0.00 |
| AID-00432 | 25.10 | 0.00 | 100.40 | Request new 41.42 | Exceeds remaining authority | 25.10 | 100.40 | 0.00 |
| AID-00433 | 25.10 | 0.00 | 100.40 | Confirm pending 100.40 | Settle original once | 125.50 | 0.00 | 0.00 |
| AID-00434 | 25.10 | 0.00 | 100.40 | Fail pending 100.40 | Release pending reservation | 25.10 | 0.00 | 100.40 |
| AID-00435 | 25.10 | 0.00 | 100.40 | Replay settled 25.10 | Original receipt; no new effect | 25.10 | 100.40 | 0.00 |
| AID-00436 | 25.10 | 0.00 | 100.40 | Record return 0.01 | Apply linked return once | 25.09 | 100.40 | 0.01 |
| AID-00437 | 25.10 | 0.00 | 100.40 | Record return 12.55 | Apply linked return once | 12.55 | 100.40 | 12.55 |
| AID-00438 | 25.10 | 0.00 | 100.40 | Record return 25.10 | Apply linked return once | 0.00 | 100.40 | 25.10 |
| AID-00439 | 25.10 | 0.00 | 100.40 | Record return 25.11 | Return exceeds net fulfillment | 25.10 | 100.40 | 0.00 |
| AID-00440 | 25.10 | 0.01 | 0.00 | Request new 41.42 | Reserve once | 25.09 | 41.42 | 58.99 |
| AID-00441 | 25.10 | 0.01 | 0.00 | Request new 100.40 | Reserve once | 25.09 | 100.40 | 0.01 |
| AID-00442 | 25.10 | 0.01 | 0.00 | Request new 100.41 | Reserve once | 25.09 | 100.41 | 0.00 |
| AID-00443 | 25.10 | 0.01 | 0.00 | Request new 100.42 | Exceeds remaining authority | 25.09 | 0.00 | 100.41 |
| AID-00444 | 25.10 | 0.01 | 0.00 | Replay settled 25.10 | Original receipt; no new effect | 25.09 | 0.00 | 100.41 |
| AID-00445 | 25.10 | 0.01 | 0.00 | Record return 0.01 | Apply linked return once | 25.08 | 0.00 | 100.42 |
| AID-00446 | 25.10 | 0.01 | 0.00 | Record return 12.55 | Apply linked return once | 12.54 | 0.00 | 112.96 |
| AID-00447 | 25.10 | 0.01 | 0.00 | Record return 25.09 | Apply linked return once | 0.00 | 0.00 | 125.50 |
| AID-00448 | 25.10 | 0.01 | 0.00 | Record return 25.10 | Return exceeds net fulfillment | 25.09 | 0.00 | 100.41 |
| AID-00449 | 25.10 | 0.01 | 40.16 | Request new 41.42 | Reserve once | 25.09 | 81.58 | 18.83 |
| AID-00450 | 25.10 | 0.01 | 40.16 | Request new 60.24 | Reserve once | 25.09 | 100.40 | 0.01 |
| AID-00451 | 25.10 | 0.01 | 40.16 | Request new 60.25 | Reserve once | 25.09 | 100.41 | 0.00 |
| AID-00452 | 25.10 | 0.01 | 40.16 | Request new 60.26 | Exceeds remaining authority | 25.09 | 40.16 | 60.25 |
| AID-00453 | 25.10 | 0.01 | 40.16 | Confirm pending 40.16 | Settle original once | 65.25 | 0.00 | 60.25 |
| AID-00454 | 25.10 | 0.01 | 40.16 | Fail pending 40.16 | Release pending reservation | 25.09 | 0.00 | 100.41 |
| AID-00455 | 25.10 | 0.01 | 40.16 | Replay settled 25.10 | Original receipt; no new effect | 25.09 | 40.16 | 60.25 |
| AID-00456 | 25.10 | 0.01 | 40.16 | Record return 0.01 | Apply linked return once | 25.08 | 40.16 | 60.26 |
| AID-00457 | 25.10 | 0.01 | 40.16 | Record return 12.55 | Apply linked return once | 12.54 | 40.16 | 72.80 |
| AID-00458 | 25.10 | 0.01 | 40.16 | Record return 25.09 | Apply linked return once | 0.00 | 40.16 | 85.34 |
| AID-00459 | 25.10 | 0.01 | 40.16 | Record return 25.10 | Return exceeds net fulfillment | 25.09 | 40.16 | 60.25 |
| AID-00460 | 25.10 | 0.01 | 100.41 | Request new 0.01 | Exceeds remaining authority | 25.09 | 100.41 | 0.00 |
| AID-00461 | 25.10 | 0.01 | 100.41 | Request new 41.42 | Exceeds remaining authority | 25.09 | 100.41 | 0.00 |
| AID-00462 | 25.10 | 0.01 | 100.41 | Confirm pending 100.41 | Settle original once | 125.50 | 0.00 | 0.00 |
| AID-00463 | 25.10 | 0.01 | 100.41 | Fail pending 100.41 | Release pending reservation | 25.09 | 0.00 | 100.41 |
| AID-00464 | 25.10 | 0.01 | 100.41 | Replay settled 25.10 | Original receipt; no new effect | 25.09 | 100.41 | 0.00 |
| AID-00465 | 25.10 | 0.01 | 100.41 | Record return 0.01 | Apply linked return once | 25.08 | 100.41 | 0.01 |
| AID-00466 | 25.10 | 0.01 | 100.41 | Record return 12.55 | Apply linked return once | 12.54 | 100.41 | 12.55 |
| AID-00467 | 25.10 | 0.01 | 100.41 | Record return 25.09 | Apply linked return once | 0.00 | 100.41 | 25.09 |
| AID-00468 | 25.10 | 0.01 | 100.41 | Record return 25.10 | Return exceeds net fulfillment | 25.09 | 100.41 | 0.00 |
| AID-00469 | 25.10 | 6.28 | 0.00 | Request new 41.42 | Reserve once | 18.82 | 41.42 | 65.26 |
| AID-00470 | 25.10 | 6.28 | 0.00 | Request new 106.67 | Reserve once | 18.82 | 106.67 | 0.01 |
| AID-00471 | 25.10 | 6.28 | 0.00 | Request new 106.68 | Reserve once | 18.82 | 106.68 | 0.00 |
| AID-00472 | 25.10 | 6.28 | 0.00 | Request new 106.69 | Exceeds remaining authority | 18.82 | 0.00 | 106.68 |
| AID-00473 | 25.10 | 6.28 | 0.00 | Replay settled 25.10 | Original receipt; no new effect | 18.82 | 0.00 | 106.68 |
| AID-00474 | 25.10 | 6.28 | 0.00 | Record return 0.01 | Apply linked return once | 18.81 | 0.00 | 106.69 |
| AID-00475 | 25.10 | 6.28 | 0.00 | Record return 9.41 | Apply linked return once | 9.41 | 0.00 | 116.09 |
| AID-00476 | 25.10 | 6.28 | 0.00 | Record return 18.82 | Apply linked return once | 0.00 | 0.00 | 125.50 |
| AID-00477 | 25.10 | 6.28 | 0.00 | Record return 18.83 | Return exceeds net fulfillment | 18.82 | 0.00 | 106.68 |
| AID-00478 | 25.10 | 6.28 | 42.67 | Request new 41.42 | Reserve once | 18.82 | 84.09 | 22.59 |
| AID-00479 | 25.10 | 6.28 | 42.67 | Request new 64.00 | Reserve once | 18.82 | 106.67 | 0.01 |
| AID-00480 | 25.10 | 6.28 | 42.67 | Request new 64.01 | Reserve once | 18.82 | 106.68 | 0.00 |
| AID-00481 | 25.10 | 6.28 | 42.67 | Request new 64.02 | Exceeds remaining authority | 18.82 | 42.67 | 64.01 |
| AID-00482 | 25.10 | 6.28 | 42.67 | Confirm pending 42.67 | Settle original once | 61.49 | 0.00 | 64.01 |
| AID-00483 | 25.10 | 6.28 | 42.67 | Fail pending 42.67 | Release pending reservation | 18.82 | 0.00 | 106.68 |
| AID-00484 | 25.10 | 6.28 | 42.67 | Replay settled 25.10 | Original receipt; no new effect | 18.82 | 42.67 | 64.01 |
| AID-00485 | 25.10 | 6.28 | 42.67 | Record return 0.01 | Apply linked return once | 18.81 | 42.67 | 64.02 |
| AID-00486 | 25.10 | 6.28 | 42.67 | Record return 9.41 | Apply linked return once | 9.41 | 42.67 | 73.42 |
| AID-00487 | 25.10 | 6.28 | 42.67 | Record return 18.82 | Apply linked return once | 0.00 | 42.67 | 82.83 |
| AID-00488 | 25.10 | 6.28 | 42.67 | Record return 18.83 | Return exceeds net fulfillment | 18.82 | 42.67 | 64.01 |
| AID-00489 | 25.10 | 6.28 | 106.68 | Request new 0.01 | Exceeds remaining authority | 18.82 | 106.68 | 0.00 |
| AID-00490 | 25.10 | 6.28 | 106.68 | Request new 41.42 | Exceeds remaining authority | 18.82 | 106.68 | 0.00 |
| AID-00491 | 25.10 | 6.28 | 106.68 | Confirm pending 106.68 | Settle original once | 125.50 | 0.00 | 0.00 |
| AID-00492 | 25.10 | 6.28 | 106.68 | Fail pending 106.68 | Release pending reservation | 18.82 | 0.00 | 106.68 |
| AID-00493 | 25.10 | 6.28 | 106.68 | Replay settled 25.10 | Original receipt; no new effect | 18.82 | 106.68 | 0.00 |
| AID-00494 | 25.10 | 6.28 | 106.68 | Record return 0.01 | Apply linked return once | 18.81 | 106.68 | 0.01 |
| AID-00495 | 25.10 | 6.28 | 106.68 | Record return 9.41 | Apply linked return once | 9.41 | 106.68 | 9.41 |
| AID-00496 | 25.10 | 6.28 | 106.68 | Record return 18.82 | Apply linked return once | 0.00 | 106.68 | 18.82 |
| AID-00497 | 25.10 | 6.28 | 106.68 | Record return 18.83 | Return exceeds net fulfillment | 18.82 | 106.68 | 0.00 |
| AID-00498 | 25.10 | 25.10 | 0.00 | Request new 41.42 | Reserve once | 0.00 | 41.42 | 84.08 |
| AID-00499 | 25.10 | 25.10 | 0.00 | Request new 125.49 | Reserve once | 0.00 | 125.49 | 0.01 |
| AID-00500 | 25.10 | 25.10 | 0.00 | Request new 125.50 | Reserve once | 0.00 | 125.50 | 0.00 |
| AID-00501 | 25.10 | 25.10 | 0.00 | Request new 125.51 | Exceeds remaining authority | 0.00 | 0.00 | 125.50 |
| AID-00502 | 25.10 | 25.10 | 0.00 | Replay settled 25.10 | Original receipt; no new effect | 0.00 | 0.00 | 125.50 |
| AID-00503 | 25.10 | 25.10 | 50.20 | Request new 41.42 | Reserve once | 0.00 | 91.62 | 33.88 |
| AID-00504 | 25.10 | 25.10 | 50.20 | Request new 75.29 | Reserve once | 0.00 | 125.49 | 0.01 |
| AID-00505 | 25.10 | 25.10 | 50.20 | Request new 75.30 | Reserve once | 0.00 | 125.50 | 0.00 |
| AID-00506 | 25.10 | 25.10 | 50.20 | Request new 75.31 | Exceeds remaining authority | 0.00 | 50.20 | 75.30 |
| AID-00507 | 25.10 | 25.10 | 50.20 | Confirm pending 50.20 | Settle original once | 50.20 | 0.00 | 75.30 |
| AID-00508 | 25.10 | 25.10 | 50.20 | Fail pending 50.20 | Release pending reservation | 0.00 | 0.00 | 125.50 |
| AID-00509 | 25.10 | 25.10 | 50.20 | Replay settled 25.10 | Original receipt; no new effect | 0.00 | 50.20 | 75.30 |
| AID-00510 | 25.10 | 25.10 | 125.50 | Request new 0.01 | Exceeds remaining authority | 0.00 | 125.50 | 0.00 |
| AID-00511 | 25.10 | 25.10 | 125.50 | Request new 41.42 | Exceeds remaining authority | 0.00 | 125.50 | 0.00 |
| AID-00512 | 25.10 | 25.10 | 125.50 | Confirm pending 125.50 | Settle original once | 125.50 | 0.00 | 0.00 |
| AID-00513 | 25.10 | 25.10 | 125.50 | Fail pending 125.50 | Release pending reservation | 0.00 | 0.00 | 125.50 |
| AID-00514 | 25.10 | 25.10 | 125.50 | Replay settled 25.10 | Original receipt; no new effect | 0.00 | 125.50 | 0.00 |
| AID-00515 | 62.75 | 0.00 | 0.00 | Request new 41.42 | Reserve once | 62.75 | 41.42 | 21.33 |
| AID-00516 | 62.75 | 0.00 | 0.00 | Request new 62.74 | Reserve once | 62.75 | 62.74 | 0.01 |
| AID-00517 | 62.75 | 0.00 | 0.00 | Request new 62.75 | Reserve once | 62.75 | 62.75 | 0.00 |
| AID-00518 | 62.75 | 0.00 | 0.00 | Request new 62.76 | Exceeds remaining authority | 62.75 | 0.00 | 62.75 |
| AID-00519 | 62.75 | 0.00 | 0.00 | Replay settled 62.75 | Original receipt; no new effect | 62.75 | 0.00 | 62.75 |
| AID-00520 | 62.75 | 0.00 | 0.00 | Record return 0.01 | Apply linked return once | 62.74 | 0.00 | 62.76 |
| AID-00521 | 62.75 | 0.00 | 0.00 | Record return 31.38 | Apply linked return once | 31.37 | 0.00 | 94.13 |
| AID-00522 | 62.75 | 0.00 | 0.00 | Record return 62.75 | Apply linked return once | 0.00 | 0.00 | 125.50 |
| AID-00523 | 62.75 | 0.00 | 0.00 | Record return 62.76 | Return exceeds net fulfillment | 62.75 | 0.00 | 62.75 |
| AID-00524 | 62.75 | 0.00 | 25.10 | Request new 37.64 | Reserve once | 62.75 | 62.74 | 0.01 |
| AID-00525 | 62.75 | 0.00 | 25.10 | Request new 37.65 | Reserve once | 62.75 | 62.75 | 0.00 |
| AID-00526 | 62.75 | 0.00 | 25.10 | Request new 37.66 | Exceeds remaining authority | 62.75 | 25.10 | 37.65 |
| AID-00527 | 62.75 | 0.00 | 25.10 | Request new 41.42 | Exceeds remaining authority | 62.75 | 25.10 | 37.65 |
| AID-00528 | 62.75 | 0.00 | 25.10 | Confirm pending 25.10 | Settle original once | 87.85 | 0.00 | 37.65 |
| AID-00529 | 62.75 | 0.00 | 25.10 | Fail pending 25.10 | Release pending reservation | 62.75 | 0.00 | 62.75 |
| AID-00530 | 62.75 | 0.00 | 25.10 | Replay settled 62.75 | Original receipt; no new effect | 62.75 | 25.10 | 37.65 |
| AID-00531 | 62.75 | 0.00 | 25.10 | Record return 0.01 | Apply linked return once | 62.74 | 25.10 | 37.66 |
| AID-00532 | 62.75 | 0.00 | 25.10 | Record return 31.38 | Apply linked return once | 31.37 | 25.10 | 69.03 |
| AID-00533 | 62.75 | 0.00 | 25.10 | Record return 62.75 | Apply linked return once | 0.00 | 25.10 | 100.40 |
| AID-00534 | 62.75 | 0.00 | 25.10 | Record return 62.76 | Return exceeds net fulfillment | 62.75 | 25.10 | 37.65 |
| AID-00535 | 62.75 | 0.00 | 62.75 | Request new 0.01 | Exceeds remaining authority | 62.75 | 62.75 | 0.00 |
| AID-00536 | 62.75 | 0.00 | 62.75 | Request new 41.42 | Exceeds remaining authority | 62.75 | 62.75 | 0.00 |
| AID-00537 | 62.75 | 0.00 | 62.75 | Confirm pending 62.75 | Settle original once | 125.50 | 0.00 | 0.00 |
| AID-00538 | 62.75 | 0.00 | 62.75 | Fail pending 62.75 | Release pending reservation | 62.75 | 0.00 | 62.75 |
| AID-00539 | 62.75 | 0.00 | 62.75 | Replay settled 62.75 | Original receipt; no new effect | 62.75 | 62.75 | 0.00 |
| AID-00540 | 62.75 | 0.00 | 62.75 | Record return 0.01 | Apply linked return once | 62.74 | 62.75 | 0.01 |
| AID-00541 | 62.75 | 0.00 | 62.75 | Record return 31.38 | Apply linked return once | 31.37 | 62.75 | 31.38 |
| AID-00542 | 62.75 | 0.00 | 62.75 | Record return 62.75 | Apply linked return once | 0.00 | 62.75 | 62.75 |
| AID-00543 | 62.75 | 0.00 | 62.75 | Record return 62.76 | Return exceeds net fulfillment | 62.75 | 62.75 | 0.00 |
| AID-00544 | 62.75 | 0.01 | 0.00 | Request new 41.42 | Reserve once | 62.74 | 41.42 | 21.34 |
| AID-00545 | 62.75 | 0.01 | 0.00 | Request new 62.75 | Reserve once | 62.74 | 62.75 | 0.01 |
| AID-00546 | 62.75 | 0.01 | 0.00 | Request new 62.76 | Reserve once | 62.74 | 62.76 | 0.00 |
| AID-00547 | 62.75 | 0.01 | 0.00 | Request new 62.77 | Exceeds remaining authority | 62.74 | 0.00 | 62.76 |
| AID-00548 | 62.75 | 0.01 | 0.00 | Replay settled 62.75 | Original receipt; no new effect | 62.74 | 0.00 | 62.76 |
| AID-00549 | 62.75 | 0.01 | 0.00 | Record return 0.01 | Apply linked return once | 62.73 | 0.00 | 62.77 |
| AID-00550 | 62.75 | 0.01 | 0.00 | Record return 31.37 | Apply linked return once | 31.37 | 0.00 | 94.13 |
| AID-00551 | 62.75 | 0.01 | 0.00 | Record return 62.74 | Apply linked return once | 0.00 | 0.00 | 125.50 |
| AID-00552 | 62.75 | 0.01 | 0.00 | Record return 62.75 | Return exceeds net fulfillment | 62.74 | 0.00 | 62.76 |
| AID-00553 | 62.75 | 0.01 | 25.10 | Request new 37.65 | Reserve once | 62.74 | 62.75 | 0.01 |
| AID-00554 | 62.75 | 0.01 | 25.10 | Request new 37.66 | Reserve once | 62.74 | 62.76 | 0.00 |
| AID-00555 | 62.75 | 0.01 | 25.10 | Request new 37.67 | Exceeds remaining authority | 62.74 | 25.10 | 37.66 |
| AID-00556 | 62.75 | 0.01 | 25.10 | Request new 41.42 | Exceeds remaining authority | 62.74 | 25.10 | 37.66 |
| AID-00557 | 62.75 | 0.01 | 25.10 | Confirm pending 25.10 | Settle original once | 87.84 | 0.00 | 37.66 |
| AID-00558 | 62.75 | 0.01 | 25.10 | Fail pending 25.10 | Release pending reservation | 62.74 | 0.00 | 62.76 |
| AID-00559 | 62.75 | 0.01 | 25.10 | Replay settled 62.75 | Original receipt; no new effect | 62.74 | 25.10 | 37.66 |
| AID-00560 | 62.75 | 0.01 | 25.10 | Record return 0.01 | Apply linked return once | 62.73 | 25.10 | 37.67 |
| AID-00561 | 62.75 | 0.01 | 25.10 | Record return 31.37 | Apply linked return once | 31.37 | 25.10 | 69.03 |
| AID-00562 | 62.75 | 0.01 | 25.10 | Record return 62.74 | Apply linked return once | 0.00 | 25.10 | 100.40 |
| AID-00563 | 62.75 | 0.01 | 25.10 | Record return 62.75 | Return exceeds net fulfillment | 62.74 | 25.10 | 37.66 |
| AID-00564 | 62.75 | 0.01 | 62.76 | Request new 0.01 | Exceeds remaining authority | 62.74 | 62.76 | 0.00 |
| AID-00565 | 62.75 | 0.01 | 62.76 | Request new 41.42 | Exceeds remaining authority | 62.74 | 62.76 | 0.00 |
| AID-00566 | 62.75 | 0.01 | 62.76 | Confirm pending 62.76 | Settle original once | 125.50 | 0.00 | 0.00 |
| AID-00567 | 62.75 | 0.01 | 62.76 | Fail pending 62.76 | Release pending reservation | 62.74 | 0.00 | 62.76 |
| AID-00568 | 62.75 | 0.01 | 62.76 | Replay settled 62.75 | Original receipt; no new effect | 62.74 | 62.76 | 0.00 |
| AID-00569 | 62.75 | 0.01 | 62.76 | Record return 0.01 | Apply linked return once | 62.73 | 62.76 | 0.01 |
| AID-00570 | 62.75 | 0.01 | 62.76 | Record return 31.37 | Apply linked return once | 31.37 | 62.76 | 31.37 |
| AID-00571 | 62.75 | 0.01 | 62.76 | Record return 62.74 | Apply linked return once | 0.00 | 62.76 | 62.74 |
| AID-00572 | 62.75 | 0.01 | 62.76 | Record return 62.75 | Return exceeds net fulfillment | 62.74 | 62.76 | 0.00 |
| AID-00573 | 62.75 | 15.69 | 0.00 | Request new 41.42 | Reserve once | 47.06 | 41.42 | 37.02 |
| AID-00574 | 62.75 | 15.69 | 0.00 | Request new 78.43 | Reserve once | 47.06 | 78.43 | 0.01 |
| AID-00575 | 62.75 | 15.69 | 0.00 | Request new 78.44 | Reserve once | 47.06 | 78.44 | 0.00 |
| AID-00576 | 62.75 | 15.69 | 0.00 | Request new 78.45 | Exceeds remaining authority | 47.06 | 0.00 | 78.44 |
| AID-00577 | 62.75 | 15.69 | 0.00 | Replay settled 62.75 | Original receipt; no new effect | 47.06 | 0.00 | 78.44 |
| AID-00578 | 62.75 | 15.69 | 0.00 | Record return 0.01 | Apply linked return once | 47.05 | 0.00 | 78.45 |
| AID-00579 | 62.75 | 15.69 | 0.00 | Record return 23.53 | Apply linked return once | 23.53 | 0.00 | 101.97 |
| AID-00580 | 62.75 | 15.69 | 0.00 | Record return 47.06 | Apply linked return once | 0.00 | 0.00 | 125.50 |
| AID-00581 | 62.75 | 15.69 | 0.00 | Record return 47.07 | Return exceeds net fulfillment | 47.06 | 0.00 | 78.44 |
| AID-00582 | 62.75 | 15.69 | 31.38 | Request new 41.42 | Reserve once | 47.06 | 72.80 | 5.64 |
| AID-00583 | 62.75 | 15.69 | 31.38 | Request new 47.05 | Reserve once | 47.06 | 78.43 | 0.01 |
| AID-00584 | 62.75 | 15.69 | 31.38 | Request new 47.06 | Reserve once | 47.06 | 78.44 | 0.00 |
| AID-00585 | 62.75 | 15.69 | 31.38 | Request new 47.07 | Exceeds remaining authority | 47.06 | 31.38 | 47.06 |
| AID-00586 | 62.75 | 15.69 | 31.38 | Confirm pending 31.38 | Settle original once | 78.44 | 0.00 | 47.06 |
| AID-00587 | 62.75 | 15.69 | 31.38 | Fail pending 31.38 | Release pending reservation | 47.06 | 0.00 | 78.44 |
| AID-00588 | 62.75 | 15.69 | 31.38 | Replay settled 62.75 | Original receipt; no new effect | 47.06 | 31.38 | 47.06 |
| AID-00589 | 62.75 | 15.69 | 31.38 | Record return 0.01 | Apply linked return once | 47.05 | 31.38 | 47.07 |
| AID-00590 | 62.75 | 15.69 | 31.38 | Record return 23.53 | Apply linked return once | 23.53 | 31.38 | 70.59 |
| AID-00591 | 62.75 | 15.69 | 31.38 | Record return 47.06 | Apply linked return once | 0.00 | 31.38 | 94.12 |
| AID-00592 | 62.75 | 15.69 | 31.38 | Record return 47.07 | Return exceeds net fulfillment | 47.06 | 31.38 | 47.06 |
| AID-00593 | 62.75 | 15.69 | 78.44 | Request new 0.01 | Exceeds remaining authority | 47.06 | 78.44 | 0.00 |
| AID-00594 | 62.75 | 15.69 | 78.44 | Request new 41.42 | Exceeds remaining authority | 47.06 | 78.44 | 0.00 |
| AID-00595 | 62.75 | 15.69 | 78.44 | Confirm pending 78.44 | Settle original once | 125.50 | 0.00 | 0.00 |
| AID-00596 | 62.75 | 15.69 | 78.44 | Fail pending 78.44 | Release pending reservation | 47.06 | 0.00 | 78.44 |
| AID-00597 | 62.75 | 15.69 | 78.44 | Replay settled 62.75 | Original receipt; no new effect | 47.06 | 78.44 | 0.00 |
| AID-00598 | 62.75 | 15.69 | 78.44 | Record return 0.01 | Apply linked return once | 47.05 | 78.44 | 0.01 |
| AID-00599 | 62.75 | 15.69 | 78.44 | Record return 23.53 | Apply linked return once | 23.53 | 78.44 | 23.53 |
| AID-00600 | 62.75 | 15.69 | 78.44 | Record return 47.06 | Apply linked return once | 0.00 | 78.44 | 47.06 |
| AID-00601 | 62.75 | 15.69 | 78.44 | Record return 47.07 | Return exceeds net fulfillment | 47.06 | 78.44 | 0.00 |
| AID-00602 | 62.75 | 62.75 | 0.00 | Request new 41.42 | Reserve once | 0.00 | 41.42 | 84.08 |
| AID-00603 | 62.75 | 62.75 | 0.00 | Request new 125.49 | Reserve once | 0.00 | 125.49 | 0.01 |
| AID-00604 | 62.75 | 62.75 | 0.00 | Request new 125.50 | Reserve once | 0.00 | 125.50 | 0.00 |
| AID-00605 | 62.75 | 62.75 | 0.00 | Request new 125.51 | Exceeds remaining authority | 0.00 | 0.00 | 125.50 |
| AID-00606 | 62.75 | 62.75 | 0.00 | Replay settled 62.75 | Original receipt; no new effect | 0.00 | 0.00 | 125.50 |
| AID-00607 | 62.75 | 62.75 | 50.20 | Request new 41.42 | Reserve once | 0.00 | 91.62 | 33.88 |
| AID-00608 | 62.75 | 62.75 | 50.20 | Request new 75.29 | Reserve once | 0.00 | 125.49 | 0.01 |
| AID-00609 | 62.75 | 62.75 | 50.20 | Request new 75.30 | Reserve once | 0.00 | 125.50 | 0.00 |
| AID-00610 | 62.75 | 62.75 | 50.20 | Request new 75.31 | Exceeds remaining authority | 0.00 | 50.20 | 75.30 |
| AID-00611 | 62.75 | 62.75 | 50.20 | Confirm pending 50.20 | Settle original once | 50.20 | 0.00 | 75.30 |
| AID-00612 | 62.75 | 62.75 | 50.20 | Fail pending 50.20 | Release pending reservation | 0.00 | 0.00 | 125.50 |
| AID-00613 | 62.75 | 62.75 | 50.20 | Replay settled 62.75 | Original receipt; no new effect | 0.00 | 50.20 | 75.30 |
| AID-00614 | 62.75 | 62.75 | 125.50 | Request new 0.01 | Exceeds remaining authority | 0.00 | 125.50 | 0.00 |
| AID-00615 | 62.75 | 62.75 | 125.50 | Request new 41.42 | Exceeds remaining authority | 0.00 | 125.50 | 0.00 |
| AID-00616 | 62.75 | 62.75 | 125.50 | Confirm pending 125.50 | Settle original once | 125.50 | 0.00 | 0.00 |
| AID-00617 | 62.75 | 62.75 | 125.50 | Fail pending 125.50 | Release pending reservation | 0.00 | 0.00 | 125.50 |
| AID-00618 | 62.75 | 62.75 | 125.50 | Replay settled 62.75 | Original receipt; no new effect | 0.00 | 125.50 | 0.00 |
| AID-00619 | 100.40 | 0.00 | 0.00 | Request new 25.09 | Reserve once | 100.40 | 25.09 | 0.01 |
| AID-00620 | 100.40 | 0.00 | 0.00 | Request new 25.10 | Reserve once | 100.40 | 25.10 | 0.00 |
| AID-00621 | 100.40 | 0.00 | 0.00 | Request new 25.11 | Exceeds remaining authority | 100.40 | 0.00 | 25.10 |
| AID-00622 | 100.40 | 0.00 | 0.00 | Request new 41.42 | Exceeds remaining authority | 100.40 | 0.00 | 25.10 |
| AID-00623 | 100.40 | 0.00 | 0.00 | Replay settled 100.40 | Original receipt; no new effect | 100.40 | 0.00 | 25.10 |
| AID-00624 | 100.40 | 0.00 | 0.00 | Record return 0.01 | Apply linked return once | 100.39 | 0.00 | 25.11 |
| AID-00625 | 100.40 | 0.00 | 0.00 | Record return 50.20 | Apply linked return once | 50.20 | 0.00 | 75.30 |
| AID-00626 | 100.40 | 0.00 | 0.00 | Record return 100.40 | Apply linked return once | 0.00 | 0.00 | 125.50 |
| AID-00627 | 100.40 | 0.00 | 0.00 | Record return 100.41 | Return exceeds net fulfillment | 100.40 | 0.00 | 25.10 |
| AID-00628 | 100.40 | 0.00 | 10.04 | Request new 15.05 | Reserve once | 100.40 | 25.09 | 0.01 |
| AID-00629 | 100.40 | 0.00 | 10.04 | Request new 15.06 | Reserve once | 100.40 | 25.10 | 0.00 |
| AID-00630 | 100.40 | 0.00 | 10.04 | Request new 15.07 | Exceeds remaining authority | 100.40 | 10.04 | 15.06 |
| AID-00631 | 100.40 | 0.00 | 10.04 | Request new 41.42 | Exceeds remaining authority | 100.40 | 10.04 | 15.06 |
| AID-00632 | 100.40 | 0.00 | 10.04 | Confirm pending 10.04 | Settle original once | 110.44 | 0.00 | 15.06 |
| AID-00633 | 100.40 | 0.00 | 10.04 | Fail pending 10.04 | Release pending reservation | 100.40 | 0.00 | 25.10 |
| AID-00634 | 100.40 | 0.00 | 10.04 | Replay settled 100.40 | Original receipt; no new effect | 100.40 | 10.04 | 15.06 |
| AID-00635 | 100.40 | 0.00 | 10.04 | Record return 0.01 | Apply linked return once | 100.39 | 10.04 | 15.07 |
| AID-00636 | 100.40 | 0.00 | 10.04 | Record return 50.20 | Apply linked return once | 50.20 | 10.04 | 65.26 |
| AID-00637 | 100.40 | 0.00 | 10.04 | Record return 100.40 | Apply linked return once | 0.00 | 10.04 | 115.46 |
| AID-00638 | 100.40 | 0.00 | 10.04 | Record return 100.41 | Return exceeds net fulfillment | 100.40 | 10.04 | 15.06 |
| AID-00639 | 100.40 | 0.00 | 25.10 | Request new 0.01 | Exceeds remaining authority | 100.40 | 25.10 | 0.00 |
| AID-00640 | 100.40 | 0.00 | 25.10 | Request new 41.42 | Exceeds remaining authority | 100.40 | 25.10 | 0.00 |
| AID-00641 | 100.40 | 0.00 | 25.10 | Confirm pending 25.10 | Settle original once | 125.50 | 0.00 | 0.00 |
| AID-00642 | 100.40 | 0.00 | 25.10 | Fail pending 25.10 | Release pending reservation | 100.40 | 0.00 | 25.10 |
| AID-00643 | 100.40 | 0.00 | 25.10 | Replay settled 100.40 | Original receipt; no new effect | 100.40 | 25.10 | 0.00 |
| AID-00644 | 100.40 | 0.00 | 25.10 | Record return 0.01 | Apply linked return once | 100.39 | 25.10 | 0.01 |
| AID-00645 | 100.40 | 0.00 | 25.10 | Record return 50.20 | Apply linked return once | 50.20 | 25.10 | 50.20 |
| AID-00646 | 100.40 | 0.00 | 25.10 | Record return 100.40 | Apply linked return once | 0.00 | 25.10 | 100.40 |
| AID-00647 | 100.40 | 0.00 | 25.10 | Record return 100.41 | Return exceeds net fulfillment | 100.40 | 25.10 | 0.00 |
| AID-00648 | 100.40 | 0.01 | 0.00 | Request new 25.10 | Reserve once | 100.39 | 25.10 | 0.01 |
| AID-00649 | 100.40 | 0.01 | 0.00 | Request new 25.11 | Reserve once | 100.39 | 25.11 | 0.00 |
| AID-00650 | 100.40 | 0.01 | 0.00 | Request new 25.12 | Exceeds remaining authority | 100.39 | 0.00 | 25.11 |
| AID-00651 | 100.40 | 0.01 | 0.00 | Request new 41.42 | Exceeds remaining authority | 100.39 | 0.00 | 25.11 |
| AID-00652 | 100.40 | 0.01 | 0.00 | Replay settled 100.40 | Original receipt; no new effect | 100.39 | 0.00 | 25.11 |
| AID-00653 | 100.40 | 0.01 | 0.00 | Record return 0.01 | Apply linked return once | 100.38 | 0.00 | 25.12 |
| AID-00654 | 100.40 | 0.01 | 0.00 | Record return 50.20 | Apply linked return once | 50.19 | 0.00 | 75.31 |
| AID-00655 | 100.40 | 0.01 | 0.00 | Record return 100.39 | Apply linked return once | 0.00 | 0.00 | 125.50 |
| AID-00656 | 100.40 | 0.01 | 0.00 | Record return 100.40 | Return exceeds net fulfillment | 100.39 | 0.00 | 25.11 |
| AID-00657 | 100.40 | 0.01 | 10.04 | Request new 15.06 | Reserve once | 100.39 | 25.10 | 0.01 |
| AID-00658 | 100.40 | 0.01 | 10.04 | Request new 15.07 | Reserve once | 100.39 | 25.11 | 0.00 |
| AID-00659 | 100.40 | 0.01 | 10.04 | Request new 15.08 | Exceeds remaining authority | 100.39 | 10.04 | 15.07 |
| AID-00660 | 100.40 | 0.01 | 10.04 | Request new 41.42 | Exceeds remaining authority | 100.39 | 10.04 | 15.07 |
| AID-00661 | 100.40 | 0.01 | 10.04 | Confirm pending 10.04 | Settle original once | 110.43 | 0.00 | 15.07 |
| AID-00662 | 100.40 | 0.01 | 10.04 | Fail pending 10.04 | Release pending reservation | 100.39 | 0.00 | 25.11 |
| AID-00663 | 100.40 | 0.01 | 10.04 | Replay settled 100.40 | Original receipt; no new effect | 100.39 | 10.04 | 15.07 |
| AID-00664 | 100.40 | 0.01 | 10.04 | Record return 0.01 | Apply linked return once | 100.38 | 10.04 | 15.08 |
| AID-00665 | 100.40 | 0.01 | 10.04 | Record return 50.20 | Apply linked return once | 50.19 | 10.04 | 65.27 |
| AID-00666 | 100.40 | 0.01 | 10.04 | Record return 100.39 | Apply linked return once | 0.00 | 10.04 | 115.46 |
| AID-00667 | 100.40 | 0.01 | 10.04 | Record return 100.40 | Return exceeds net fulfillment | 100.39 | 10.04 | 15.07 |
| AID-00668 | 100.40 | 0.01 | 25.11 | Request new 0.01 | Exceeds remaining authority | 100.39 | 25.11 | 0.00 |
| AID-00669 | 100.40 | 0.01 | 25.11 | Request new 41.42 | Exceeds remaining authority | 100.39 | 25.11 | 0.00 |
| AID-00670 | 100.40 | 0.01 | 25.11 | Confirm pending 25.11 | Settle original once | 125.50 | 0.00 | 0.00 |
| AID-00671 | 100.40 | 0.01 | 25.11 | Fail pending 25.11 | Release pending reservation | 100.39 | 0.00 | 25.11 |
| AID-00672 | 100.40 | 0.01 | 25.11 | Replay settled 100.40 | Original receipt; no new effect | 100.39 | 25.11 | 0.00 |
| AID-00673 | 100.40 | 0.01 | 25.11 | Record return 0.01 | Apply linked return once | 100.38 | 25.11 | 0.01 |
| AID-00674 | 100.40 | 0.01 | 25.11 | Record return 50.20 | Apply linked return once | 50.19 | 25.11 | 50.20 |
| AID-00675 | 100.40 | 0.01 | 25.11 | Record return 100.39 | Apply linked return once | 0.00 | 25.11 | 100.39 |
| AID-00676 | 100.40 | 0.01 | 25.11 | Record return 100.40 | Return exceeds net fulfillment | 100.39 | 25.11 | 0.00 |
| AID-00677 | 100.40 | 25.10 | 0.00 | Request new 41.42 | Reserve once | 75.30 | 41.42 | 8.78 |
| AID-00678 | 100.40 | 25.10 | 0.00 | Request new 50.19 | Reserve once | 75.30 | 50.19 | 0.01 |
| AID-00679 | 100.40 | 25.10 | 0.00 | Request new 50.20 | Reserve once | 75.30 | 50.20 | 0.00 |
| AID-00680 | 100.40 | 25.10 | 0.00 | Request new 50.21 | Exceeds remaining authority | 75.30 | 0.00 | 50.20 |
| AID-00681 | 100.40 | 25.10 | 0.00 | Replay settled 100.40 | Original receipt; no new effect | 75.30 | 0.00 | 50.20 |
| AID-00682 | 100.40 | 25.10 | 0.00 | Record return 0.01 | Apply linked return once | 75.29 | 0.00 | 50.21 |
| AID-00683 | 100.40 | 25.10 | 0.00 | Record return 37.65 | Apply linked return once | 37.65 | 0.00 | 87.85 |
| AID-00684 | 100.40 | 25.10 | 0.00 | Record return 75.30 | Apply linked return once | 0.00 | 0.00 | 125.50 |
| AID-00685 | 100.40 | 25.10 | 0.00 | Record return 75.31 | Return exceeds net fulfillment | 75.30 | 0.00 | 50.20 |
| AID-00686 | 100.40 | 25.10 | 20.08 | Request new 30.11 | Reserve once | 75.30 | 50.19 | 0.01 |
| AID-00687 | 100.40 | 25.10 | 20.08 | Request new 30.12 | Reserve once | 75.30 | 50.20 | 0.00 |
| AID-00688 | 100.40 | 25.10 | 20.08 | Request new 30.13 | Exceeds remaining authority | 75.30 | 20.08 | 30.12 |
| AID-00689 | 100.40 | 25.10 | 20.08 | Request new 41.42 | Exceeds remaining authority | 75.30 | 20.08 | 30.12 |
| AID-00690 | 100.40 | 25.10 | 20.08 | Confirm pending 20.08 | Settle original once | 95.38 | 0.00 | 30.12 |
| AID-00691 | 100.40 | 25.10 | 20.08 | Fail pending 20.08 | Release pending reservation | 75.30 | 0.00 | 50.20 |
| AID-00692 | 100.40 | 25.10 | 20.08 | Replay settled 100.40 | Original receipt; no new effect | 75.30 | 20.08 | 30.12 |
| AID-00693 | 100.40 | 25.10 | 20.08 | Record return 0.01 | Apply linked return once | 75.29 | 20.08 | 30.13 |
| AID-00694 | 100.40 | 25.10 | 20.08 | Record return 37.65 | Apply linked return once | 37.65 | 20.08 | 67.77 |
| AID-00695 | 100.40 | 25.10 | 20.08 | Record return 75.30 | Apply linked return once | 0.00 | 20.08 | 105.42 |
| AID-00696 | 100.40 | 25.10 | 20.08 | Record return 75.31 | Return exceeds net fulfillment | 75.30 | 20.08 | 30.12 |
| AID-00697 | 100.40 | 25.10 | 50.20 | Request new 0.01 | Exceeds remaining authority | 75.30 | 50.20 | 0.00 |
| AID-00698 | 100.40 | 25.10 | 50.20 | Request new 41.42 | Exceeds remaining authority | 75.30 | 50.20 | 0.00 |
| AID-00699 | 100.40 | 25.10 | 50.20 | Confirm pending 50.20 | Settle original once | 125.50 | 0.00 | 0.00 |
| AID-00700 | 100.40 | 25.10 | 50.20 | Fail pending 50.20 | Release pending reservation | 75.30 | 0.00 | 50.20 |
| AID-00701 | 100.40 | 25.10 | 50.20 | Replay settled 100.40 | Original receipt; no new effect | 75.30 | 50.20 | 0.00 |
| AID-00702 | 100.40 | 25.10 | 50.20 | Record return 0.01 | Apply linked return once | 75.29 | 50.20 | 0.01 |
| AID-00703 | 100.40 | 25.10 | 50.20 | Record return 37.65 | Apply linked return once | 37.65 | 50.20 | 37.65 |
| AID-00704 | 100.40 | 25.10 | 50.20 | Record return 75.30 | Apply linked return once | 0.00 | 50.20 | 75.30 |
| AID-00705 | 100.40 | 25.10 | 50.20 | Record return 75.31 | Return exceeds net fulfillment | 75.30 | 50.20 | 0.00 |
| AID-00706 | 100.40 | 100.40 | 0.00 | Request new 41.42 | Reserve once | 0.00 | 41.42 | 84.08 |
| AID-00707 | 100.40 | 100.40 | 0.00 | Request new 125.49 | Reserve once | 0.00 | 125.49 | 0.01 |
| AID-00708 | 100.40 | 100.40 | 0.00 | Request new 125.50 | Reserve once | 0.00 | 125.50 | 0.00 |
| AID-00709 | 100.40 | 100.40 | 0.00 | Request new 125.51 | Exceeds remaining authority | 0.00 | 0.00 | 125.50 |
| AID-00710 | 100.40 | 100.40 | 0.00 | Replay settled 100.40 | Original receipt; no new effect | 0.00 | 0.00 | 125.50 |
| AID-00711 | 100.40 | 100.40 | 50.20 | Request new 41.42 | Reserve once | 0.00 | 91.62 | 33.88 |
| AID-00712 | 100.40 | 100.40 | 50.20 | Request new 75.29 | Reserve once | 0.00 | 125.49 | 0.01 |
| AID-00713 | 100.40 | 100.40 | 50.20 | Request new 75.30 | Reserve once | 0.00 | 125.50 | 0.00 |
| AID-00714 | 100.40 | 100.40 | 50.20 | Request new 75.31 | Exceeds remaining authority | 0.00 | 50.20 | 75.30 |
| AID-00715 | 100.40 | 100.40 | 50.20 | Confirm pending 50.20 | Settle original once | 50.20 | 0.00 | 75.30 |
| AID-00716 | 100.40 | 100.40 | 50.20 | Fail pending 50.20 | Release pending reservation | 0.00 | 0.00 | 125.50 |
