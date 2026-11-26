# Travel passes — part 1 of 2

[Policy and other cases](README.md)

One approved award of 30 passes; all inputs use passes at 0 decimal places. One original settled fulfillment, when present, may be partially returned. An outstanding payment or stock issue is reserved against authority. Historical issued and returned amounts are kept even when the net amount is zero. Reviewers can reconstruct this case using the supplied opening facts.

| Case | Opening gross | Opening returns | Opening reserved | Requested event and value | Decision | New net delivered | New reserved | New free authority |
|---|---|---|---|---|---|---|---|---|
| AID-02345 | 0 | 0 | 0 | Request new 10 | Reserve once | 0 | 10 | 20 |
| AID-02346 | 0 | 0 | 0 | Request new 29 | Reserve once | 0 | 29 | 1 |
| AID-02347 | 0 | 0 | 0 | Request new 30 | Reserve once | 0 | 30 | 0 |
| AID-02348 | 0 | 0 | 0 | Request new 31 | Exceeds remaining authority | 0 | 0 | 30 |
| AID-02349 | 0 | 0 | 12 | Request new 10 | Reserve once | 0 | 22 | 8 |
| AID-02350 | 0 | 0 | 12 | Request new 17 | Reserve once | 0 | 29 | 1 |
| AID-02351 | 0 | 0 | 12 | Request new 18 | Reserve once | 0 | 30 | 0 |
| AID-02352 | 0 | 0 | 12 | Request new 19 | Exceeds remaining authority | 0 | 12 | 18 |
| AID-02353 | 0 | 0 | 12 | Confirm pending 12 | Settle original once | 12 | 0 | 18 |
| AID-02354 | 0 | 0 | 12 | Fail pending 12 | Release pending reservation | 0 | 0 | 30 |
| AID-02355 | 0 | 0 | 30 | Request new 1 | Exceeds remaining authority | 0 | 30 | 0 |
| AID-02356 | 0 | 0 | 30 | Request new 10 | Exceeds remaining authority | 0 | 30 | 0 |
| AID-02357 | 0 | 0 | 30 | Confirm pending 30 | Settle original once | 30 | 0 | 0 |
| AID-02358 | 0 | 0 | 30 | Fail pending 30 | Release pending reservation | 0 | 0 | 30 |
| AID-02359 | 6 | 0 | 0 | Request new 10 | Reserve once | 6 | 10 | 14 |
| AID-02360 | 6 | 0 | 0 | Request new 23 | Reserve once | 6 | 23 | 1 |
| AID-02361 | 6 | 0 | 0 | Request new 24 | Reserve once | 6 | 24 | 0 |
| AID-02362 | 6 | 0 | 0 | Request new 25 | Exceeds remaining authority | 6 | 0 | 24 |
| AID-02363 | 6 | 0 | 0 | Replay settled 6 | Original receipt; no new effect | 6 | 0 | 24 |
| AID-02364 | 6 | 0 | 0 | Record return 1 | Apply linked return once | 5 | 0 | 25 |
| AID-02365 | 6 | 0 | 0 | Record return 3 | Apply linked return once | 3 | 0 | 27 |
| AID-02366 | 6 | 0 | 0 | Record return 6 | Apply linked return once | 0 | 0 | 30 |
| AID-02367 | 6 | 0 | 0 | Record return 7 | Return exceeds net fulfillment | 6 | 0 | 24 |
| AID-02368 | 6 | 0 | 10 | Request new 10 | Reserve once | 6 | 20 | 4 |
| AID-02369 | 6 | 0 | 10 | Request new 13 | Reserve once | 6 | 23 | 1 |
| AID-02370 | 6 | 0 | 10 | Request new 14 | Reserve once | 6 | 24 | 0 |
| AID-02371 | 6 | 0 | 10 | Request new 15 | Exceeds remaining authority | 6 | 10 | 14 |
| AID-02372 | 6 | 0 | 10 | Confirm pending 10 | Settle original once | 16 | 0 | 14 |
| AID-02373 | 6 | 0 | 10 | Fail pending 10 | Release pending reservation | 6 | 0 | 24 |
| AID-02374 | 6 | 0 | 10 | Replay settled 6 | Original receipt; no new effect | 6 | 10 | 14 |
| AID-02375 | 6 | 0 | 10 | Record return 1 | Apply linked return once | 5 | 10 | 15 |
| AID-02376 | 6 | 0 | 10 | Record return 3 | Apply linked return once | 3 | 10 | 17 |
| AID-02377 | 6 | 0 | 10 | Record return 6 | Apply linked return once | 0 | 10 | 20 |
| AID-02378 | 6 | 0 | 10 | Record return 7 | Return exceeds net fulfillment | 6 | 10 | 14 |
| AID-02379 | 6 | 0 | 24 | Request new 1 | Exceeds remaining authority | 6 | 24 | 0 |
| AID-02380 | 6 | 0 | 24 | Request new 10 | Exceeds remaining authority | 6 | 24 | 0 |
| AID-02381 | 6 | 0 | 24 | Confirm pending 24 | Settle original once | 30 | 0 | 0 |
| AID-02382 | 6 | 0 | 24 | Fail pending 24 | Release pending reservation | 6 | 0 | 24 |
| AID-02383 | 6 | 0 | 24 | Replay settled 6 | Original receipt; no new effect | 6 | 24 | 0 |
| AID-02384 | 6 | 0 | 24 | Record return 1 | Apply linked return once | 5 | 24 | 1 |
| AID-02385 | 6 | 0 | 24 | Record return 3 | Apply linked return once | 3 | 24 | 3 |
| AID-02386 | 6 | 0 | 24 | Record return 6 | Apply linked return once | 0 | 24 | 6 |
| AID-02387 | 6 | 0 | 24 | Record return 7 | Return exceeds net fulfillment | 6 | 24 | 0 |
| AID-02388 | 6 | 1 | 0 | Request new 10 | Reserve once | 5 | 10 | 15 |
| AID-02389 | 6 | 1 | 0 | Request new 24 | Reserve once | 5 | 24 | 1 |
| AID-02390 | 6 | 1 | 0 | Request new 25 | Reserve once | 5 | 25 | 0 |
| AID-02391 | 6 | 1 | 0 | Request new 26 | Exceeds remaining authority | 5 | 0 | 25 |
| AID-02392 | 6 | 1 | 0 | Replay settled 6 | Original receipt; no new effect | 5 | 0 | 25 |
| AID-02393 | 6 | 1 | 0 | Record return 1 | Apply linked return once | 4 | 0 | 26 |
| AID-02394 | 6 | 1 | 0 | Record return 3 | Apply linked return once | 2 | 0 | 28 |
| AID-02395 | 6 | 1 | 0 | Record return 5 | Apply linked return once | 0 | 0 | 30 |
| AID-02396 | 6 | 1 | 0 | Record return 6 | Return exceeds net fulfillment | 5 | 0 | 25 |
| AID-02397 | 6 | 1 | 10 | Request new 10 | Reserve once | 5 | 20 | 5 |
| AID-02398 | 6 | 1 | 10 | Request new 14 | Reserve once | 5 | 24 | 1 |
| AID-02399 | 6 | 1 | 10 | Request new 15 | Reserve once | 5 | 25 | 0 |
| AID-02400 | 6 | 1 | 10 | Request new 16 | Exceeds remaining authority | 5 | 10 | 15 |
| AID-02401 | 6 | 1 | 10 | Confirm pending 10 | Settle original once | 15 | 0 | 15 |
| AID-02402 | 6 | 1 | 10 | Fail pending 10 | Release pending reservation | 5 | 0 | 25 |
| AID-02403 | 6 | 1 | 10 | Replay settled 6 | Original receipt; no new effect | 5 | 10 | 15 |
| AID-02404 | 6 | 1 | 10 | Record return 1 | Apply linked return once | 4 | 10 | 16 |
| AID-02405 | 6 | 1 | 10 | Record return 3 | Apply linked return once | 2 | 10 | 18 |
| AID-02406 | 6 | 1 | 10 | Record return 5 | Apply linked return once | 0 | 10 | 20 |
| AID-02407 | 6 | 1 | 10 | Record return 6 | Return exceeds net fulfillment | 5 | 10 | 15 |
| AID-02408 | 6 | 1 | 25 | Request new 1 | Exceeds remaining authority | 5 | 25 | 0 |
| AID-02409 | 6 | 1 | 25 | Request new 10 | Exceeds remaining authority | 5 | 25 | 0 |
| AID-02410 | 6 | 1 | 25 | Confirm pending 25 | Settle original once | 30 | 0 | 0 |
| AID-02411 | 6 | 1 | 25 | Fail pending 25 | Release pending reservation | 5 | 0 | 25 |
| AID-02412 | 6 | 1 | 25 | Replay settled 6 | Original receipt; no new effect | 5 | 25 | 0 |
| AID-02413 | 6 | 1 | 25 | Record return 1 | Apply linked return once | 4 | 25 | 1 |
| AID-02414 | 6 | 1 | 25 | Record return 3 | Apply linked return once | 2 | 25 | 3 |
| AID-02415 | 6 | 1 | 25 | Record return 5 | Apply linked return once | 0 | 25 | 5 |
| AID-02416 | 6 | 1 | 25 | Record return 6 | Return exceeds net fulfillment | 5 | 25 | 0 |
| AID-02417 | 6 | 2 | 0 | Request new 10 | Reserve once | 4 | 10 | 16 |
| AID-02418 | 6 | 2 | 0 | Request new 25 | Reserve once | 4 | 25 | 1 |
| AID-02419 | 6 | 2 | 0 | Request new 26 | Reserve once | 4 | 26 | 0 |
| AID-02420 | 6 | 2 | 0 | Request new 27 | Exceeds remaining authority | 4 | 0 | 26 |
| AID-02421 | 6 | 2 | 0 | Replay settled 6 | Original receipt; no new effect | 4 | 0 | 26 |
| AID-02422 | 6 | 2 | 0 | Record return 1 | Apply linked return once | 3 | 0 | 27 |
| AID-02423 | 6 | 2 | 0 | Record return 2 | Apply linked return once | 2 | 0 | 28 |
| AID-02424 | 6 | 2 | 0 | Record return 4 | Apply linked return once | 0 | 0 | 30 |
| AID-02425 | 6 | 2 | 0 | Record return 5 | Return exceeds net fulfillment | 4 | 0 | 26 |
| AID-02426 | 6 | 2 | 10 | Request new 10 | Reserve once | 4 | 20 | 6 |
| AID-02427 | 6 | 2 | 10 | Request new 15 | Reserve once | 4 | 25 | 1 |
| AID-02428 | 6 | 2 | 10 | Request new 16 | Reserve once | 4 | 26 | 0 |
| AID-02429 | 6 | 2 | 10 | Request new 17 | Exceeds remaining authority | 4 | 10 | 16 |
| AID-02430 | 6 | 2 | 10 | Confirm pending 10 | Settle original once | 14 | 0 | 16 |
| AID-02431 | 6 | 2 | 10 | Fail pending 10 | Release pending reservation | 4 | 0 | 26 |
| AID-02432 | 6 | 2 | 10 | Replay settled 6 | Original receipt; no new effect | 4 | 10 | 16 |
| AID-02433 | 6 | 2 | 10 | Record return 1 | Apply linked return once | 3 | 10 | 17 |
| AID-02434 | 6 | 2 | 10 | Record return 2 | Apply linked return once | 2 | 10 | 18 |
| AID-02435 | 6 | 2 | 10 | Record return 4 | Apply linked return once | 0 | 10 | 20 |
| AID-02436 | 6 | 2 | 10 | Record return 5 | Return exceeds net fulfillment | 4 | 10 | 16 |
| AID-02437 | 6 | 2 | 26 | Request new 1 | Exceeds remaining authority | 4 | 26 | 0 |
| AID-02438 | 6 | 2 | 26 | Request new 10 | Exceeds remaining authority | 4 | 26 | 0 |
| AID-02439 | 6 | 2 | 26 | Confirm pending 26 | Settle original once | 30 | 0 | 0 |
| AID-02440 | 6 | 2 | 26 | Fail pending 26 | Release pending reservation | 4 | 0 | 26 |
| AID-02441 | 6 | 2 | 26 | Replay settled 6 | Original receipt; no new effect | 4 | 26 | 0 |
| AID-02442 | 6 | 2 | 26 | Record return 1 | Apply linked return once | 3 | 26 | 1 |
| AID-02443 | 6 | 2 | 26 | Record return 2 | Apply linked return once | 2 | 26 | 2 |
| AID-02444 | 6 | 2 | 26 | Record return 4 | Apply linked return once | 0 | 26 | 4 |
| AID-02445 | 6 | 2 | 26 | Record return 5 | Return exceeds net fulfillment | 4 | 26 | 0 |
| AID-02446 | 6 | 6 | 0 | Request new 10 | Reserve once | 0 | 10 | 20 |
| AID-02447 | 6 | 6 | 0 | Request new 29 | Reserve once | 0 | 29 | 1 |
| AID-02448 | 6 | 6 | 0 | Request new 30 | Reserve once | 0 | 30 | 0 |
| AID-02449 | 6 | 6 | 0 | Request new 31 | Exceeds remaining authority | 0 | 0 | 30 |
| AID-02450 | 6 | 6 | 0 | Replay settled 6 | Original receipt; no new effect | 0 | 0 | 30 |
| AID-02451 | 6 | 6 | 12 | Request new 10 | Reserve once | 0 | 22 | 8 |
| AID-02452 | 6 | 6 | 12 | Request new 17 | Reserve once | 0 | 29 | 1 |
| AID-02453 | 6 | 6 | 12 | Request new 18 | Reserve once | 0 | 30 | 0 |
| AID-02454 | 6 | 6 | 12 | Request new 19 | Exceeds remaining authority | 0 | 12 | 18 |
| AID-02455 | 6 | 6 | 12 | Confirm pending 12 | Settle original once | 12 | 0 | 18 |
| AID-02456 | 6 | 6 | 12 | Fail pending 12 | Release pending reservation | 0 | 0 | 30 |
| AID-02457 | 6 | 6 | 12 | Replay settled 6 | Original receipt; no new effect | 0 | 12 | 18 |
| AID-02458 | 6 | 6 | 30 | Request new 1 | Exceeds remaining authority | 0 | 30 | 0 |
| AID-02459 | 6 | 6 | 30 | Request new 10 | Exceeds remaining authority | 0 | 30 | 0 |
| AID-02460 | 6 | 6 | 30 | Confirm pending 30 | Settle original once | 30 | 0 | 0 |
| AID-02461 | 6 | 6 | 30 | Fail pending 30 | Release pending reservation | 0 | 0 | 30 |
| AID-02462 | 6 | 6 | 30 | Replay settled 6 | Original receipt; no new effect | 0 | 30 | 0 |
| AID-02463 | 15 | 0 | 0 | Request new 10 | Reserve once | 15 | 10 | 5 |
| AID-02464 | 15 | 0 | 0 | Request new 14 | Reserve once | 15 | 14 | 1 |
| AID-02465 | 15 | 0 | 0 | Request new 15 | Reserve once | 15 | 15 | 0 |
| AID-02466 | 15 | 0 | 0 | Request new 16 | Exceeds remaining authority | 15 | 0 | 15 |
| AID-02467 | 15 | 0 | 0 | Replay settled 15 | Original receipt; no new effect | 15 | 0 | 15 |
| AID-02468 | 15 | 0 | 0 | Record return 1 | Apply linked return once | 14 | 0 | 16 |
| AID-02469 | 15 | 0 | 0 | Record return 8 | Apply linked return once | 7 | 0 | 23 |
| AID-02470 | 15 | 0 | 0 | Record return 15 | Apply linked return once | 0 | 0 | 30 |
| AID-02471 | 15 | 0 | 0 | Record return 16 | Return exceeds net fulfillment | 15 | 0 | 15 |
| AID-02472 | 15 | 0 | 6 | Request new 8 | Reserve once | 15 | 14 | 1 |
| AID-02473 | 15 | 0 | 6 | Request new 9 | Reserve once | 15 | 15 | 0 |
| AID-02474 | 15 | 0 | 6 | Request new 10 | Exceeds remaining authority | 15 | 6 | 9 |
| AID-02475 | 15 | 0 | 6 | Confirm pending 6 | Settle original once | 21 | 0 | 9 |
| AID-02476 | 15 | 0 | 6 | Fail pending 6 | Release pending reservation | 15 | 0 | 15 |
| AID-02477 | 15 | 0 | 6 | Replay settled 15 | Original receipt; no new effect | 15 | 6 | 9 |
| AID-02478 | 15 | 0 | 6 | Record return 1 | Apply linked return once | 14 | 6 | 10 |
| AID-02479 | 15 | 0 | 6 | Record return 8 | Apply linked return once | 7 | 6 | 17 |
| AID-02480 | 15 | 0 | 6 | Record return 15 | Apply linked return once | 0 | 6 | 24 |
| AID-02481 | 15 | 0 | 6 | Record return 16 | Return exceeds net fulfillment | 15 | 6 | 9 |
| AID-02482 | 15 | 0 | 15 | Request new 1 | Exceeds remaining authority | 15 | 15 | 0 |
| AID-02483 | 15 | 0 | 15 | Request new 10 | Exceeds remaining authority | 15 | 15 | 0 |
| AID-02484 | 15 | 0 | 15 | Confirm pending 15 | Settle original once | 30 | 0 | 0 |
| AID-02485 | 15 | 0 | 15 | Fail pending 15 | Release pending reservation | 15 | 0 | 15 |
| AID-02486 | 15 | 0 | 15 | Replay settled 15 | Original receipt; no new effect | 15 | 15 | 0 |
| AID-02487 | 15 | 0 | 15 | Record return 1 | Apply linked return once | 14 | 15 | 1 |
| AID-02488 | 15 | 0 | 15 | Record return 8 | Apply linked return once | 7 | 15 | 8 |
| AID-02489 | 15 | 0 | 15 | Record return 15 | Apply linked return once | 0 | 15 | 15 |
| AID-02490 | 15 | 0 | 15 | Record return 16 | Return exceeds net fulfillment | 15 | 15 | 0 |
| AID-02491 | 15 | 1 | 0 | Request new 10 | Reserve once | 14 | 10 | 6 |
| AID-02492 | 15 | 1 | 0 | Request new 15 | Reserve once | 14 | 15 | 1 |
| AID-02493 | 15 | 1 | 0 | Request new 16 | Reserve once | 14 | 16 | 0 |
| AID-02494 | 15 | 1 | 0 | Request new 17 | Exceeds remaining authority | 14 | 0 | 16 |
| AID-02495 | 15 | 1 | 0 | Replay settled 15 | Original receipt; no new effect | 14 | 0 | 16 |
| AID-02496 | 15 | 1 | 0 | Record return 1 | Apply linked return once | 13 | 0 | 17 |
| AID-02497 | 15 | 1 | 0 | Record return 7 | Apply linked return once | 7 | 0 | 23 |
| AID-02498 | 15 | 1 | 0 | Record return 14 | Apply linked return once | 0 | 0 | 30 |
| AID-02499 | 15 | 1 | 0 | Record return 15 | Return exceeds net fulfillment | 14 | 0 | 16 |
| AID-02500 | 15 | 1 | 6 | Request new 9 | Reserve once | 14 | 15 | 1 |
| AID-02501 | 15 | 1 | 6 | Request new 10 | Reserve once | 14 | 16 | 0 |
| AID-02502 | 15 | 1 | 6 | Request new 11 | Exceeds remaining authority | 14 | 6 | 10 |
| AID-02503 | 15 | 1 | 6 | Confirm pending 6 | Settle original once | 20 | 0 | 10 |
| AID-02504 | 15 | 1 | 6 | Fail pending 6 | Release pending reservation | 14 | 0 | 16 |
| AID-02505 | 15 | 1 | 6 | Replay settled 15 | Original receipt; no new effect | 14 | 6 | 10 |
| AID-02506 | 15 | 1 | 6 | Record return 1 | Apply linked return once | 13 | 6 | 11 |
| AID-02507 | 15 | 1 | 6 | Record return 7 | Apply linked return once | 7 | 6 | 17 |
| AID-02508 | 15 | 1 | 6 | Record return 14 | Apply linked return once | 0 | 6 | 24 |
| AID-02509 | 15 | 1 | 6 | Record return 15 | Return exceeds net fulfillment | 14 | 6 | 10 |
| AID-02510 | 15 | 1 | 16 | Request new 1 | Exceeds remaining authority | 14 | 16 | 0 |
| AID-02511 | 15 | 1 | 16 | Request new 10 | Exceeds remaining authority | 14 | 16 | 0 |
| AID-02512 | 15 | 1 | 16 | Confirm pending 16 | Settle original once | 30 | 0 | 0 |
| AID-02513 | 15 | 1 | 16 | Fail pending 16 | Release pending reservation | 14 | 0 | 16 |
| AID-02514 | 15 | 1 | 16 | Replay settled 15 | Original receipt; no new effect | 14 | 16 | 0 |
| AID-02515 | 15 | 1 | 16 | Record return 1 | Apply linked return once | 13 | 16 | 1 |
| AID-02516 | 15 | 1 | 16 | Record return 7 | Apply linked return once | 7 | 16 | 7 |
| AID-02517 | 15 | 1 | 16 | Record return 14 | Apply linked return once | 0 | 16 | 14 |
| AID-02518 | 15 | 1 | 16 | Record return 15 | Return exceeds net fulfillment | 14 | 16 | 0 |
| AID-02519 | 15 | 4 | 0 | Request new 10 | Reserve once | 11 | 10 | 9 |
| AID-02520 | 15 | 4 | 0 | Request new 18 | Reserve once | 11 | 18 | 1 |
| AID-02521 | 15 | 4 | 0 | Request new 19 | Reserve once | 11 | 19 | 0 |
| AID-02522 | 15 | 4 | 0 | Request new 20 | Exceeds remaining authority | 11 | 0 | 19 |
| AID-02523 | 15 | 4 | 0 | Replay settled 15 | Original receipt; no new effect | 11 | 0 | 19 |
| AID-02524 | 15 | 4 | 0 | Record return 1 | Apply linked return once | 10 | 0 | 20 |
| AID-02525 | 15 | 4 | 0 | Record return 6 | Apply linked return once | 5 | 0 | 25 |
| AID-02526 | 15 | 4 | 0 | Record return 11 | Apply linked return once | 0 | 0 | 30 |
| AID-02527 | 15 | 4 | 0 | Record return 12 | Return exceeds net fulfillment | 11 | 0 | 19 |
| AID-02528 | 15 | 4 | 8 | Request new 10 | Reserve once | 11 | 18 | 1 |
| AID-02529 | 15 | 4 | 8 | Request new 11 | Reserve once | 11 | 19 | 0 |
| AID-02530 | 15 | 4 | 8 | Request new 12 | Exceeds remaining authority | 11 | 8 | 11 |
| AID-02531 | 15 | 4 | 8 | Confirm pending 8 | Settle original once | 19 | 0 | 11 |
| AID-02532 | 15 | 4 | 8 | Fail pending 8 | Release pending reservation | 11 | 0 | 19 |
| AID-02533 | 15 | 4 | 8 | Replay settled 15 | Original receipt; no new effect | 11 | 8 | 11 |
| AID-02534 | 15 | 4 | 8 | Record return 1 | Apply linked return once | 10 | 8 | 12 |
| AID-02535 | 15 | 4 | 8 | Record return 6 | Apply linked return once | 5 | 8 | 17 |
| AID-02536 | 15 | 4 | 8 | Record return 11 | Apply linked return once | 0 | 8 | 22 |
| AID-02537 | 15 | 4 | 8 | Record return 12 | Return exceeds net fulfillment | 11 | 8 | 11 |
| AID-02538 | 15 | 4 | 19 | Request new 1 | Exceeds remaining authority | 11 | 19 | 0 |
| AID-02539 | 15 | 4 | 19 | Request new 10 | Exceeds remaining authority | 11 | 19 | 0 |
| AID-02540 | 15 | 4 | 19 | Confirm pending 19 | Settle original once | 30 | 0 | 0 |
| AID-02541 | 15 | 4 | 19 | Fail pending 19 | Release pending reservation | 11 | 0 | 19 |
| AID-02542 | 15 | 4 | 19 | Replay settled 15 | Original receipt; no new effect | 11 | 19 | 0 |
| AID-02543 | 15 | 4 | 19 | Record return 1 | Apply linked return once | 10 | 19 | 1 |
| AID-02544 | 15 | 4 | 19 | Record return 6 | Apply linked return once | 5 | 19 | 6 |
| AID-02545 | 15 | 4 | 19 | Record return 11 | Apply linked return once | 0 | 19 | 11 |
| AID-02546 | 15 | 4 | 19 | Record return 12 | Return exceeds net fulfillment | 11 | 19 | 0 |
| AID-02547 | 15 | 15 | 0 | Request new 10 | Reserve once | 0 | 10 | 20 |
| AID-02548 | 15 | 15 | 0 | Request new 29 | Reserve once | 0 | 29 | 1 |
| AID-02549 | 15 | 15 | 0 | Request new 30 | Reserve once | 0 | 30 | 0 |
| AID-02550 | 15 | 15 | 0 | Request new 31 | Exceeds remaining authority | 0 | 0 | 30 |
| AID-02551 | 15 | 15 | 0 | Replay settled 15 | Original receipt; no new effect | 0 | 0 | 30 |
| AID-02552 | 15 | 15 | 12 | Request new 10 | Reserve once | 0 | 22 | 8 |
| AID-02553 | 15 | 15 | 12 | Request new 17 | Reserve once | 0 | 29 | 1 |
| AID-02554 | 15 | 15 | 12 | Request new 18 | Reserve once | 0 | 30 | 0 |
| AID-02555 | 15 | 15 | 12 | Request new 19 | Exceeds remaining authority | 0 | 12 | 18 |
| AID-02556 | 15 | 15 | 12 | Confirm pending 12 | Settle original once | 12 | 0 | 18 |
| AID-02557 | 15 | 15 | 12 | Fail pending 12 | Release pending reservation | 0 | 0 | 30 |
| AID-02558 | 15 | 15 | 12 | Replay settled 15 | Original receipt; no new effect | 0 | 12 | 18 |
| AID-02559 | 15 | 15 | 30 | Request new 1 | Exceeds remaining authority | 0 | 30 | 0 |
| AID-02560 | 15 | 15 | 30 | Request new 10 | Exceeds remaining authority | 0 | 30 | 0 |
| AID-02561 | 15 | 15 | 30 | Confirm pending 30 | Settle original once | 30 | 0 | 0 |
| AID-02562 | 15 | 15 | 30 | Fail pending 30 | Release pending reservation | 0 | 0 | 30 |
| AID-02563 | 15 | 15 | 30 | Replay settled 15 | Original receipt; no new effect | 0 | 30 | 0 |
| AID-02564 | 24 | 0 | 0 | Request new 5 | Reserve once | 24 | 5 | 1 |
| AID-02565 | 24 | 0 | 0 | Request new 6 | Reserve once | 24 | 6 | 0 |
| AID-02566 | 24 | 0 | 0 | Request new 7 | Exceeds remaining authority | 24 | 0 | 6 |
| AID-02567 | 24 | 0 | 0 | Request new 10 | Exceeds remaining authority | 24 | 0 | 6 |
| AID-02568 | 24 | 0 | 0 | Replay settled 24 | Original receipt; no new effect | 24 | 0 | 6 |
| AID-02569 | 24 | 0 | 0 | Record return 1 | Apply linked return once | 23 | 0 | 7 |
| AID-02570 | 24 | 0 | 0 | Record return 12 | Apply linked return once | 12 | 0 | 18 |
| AID-02571 | 24 | 0 | 0 | Record return 24 | Apply linked return once | 0 | 0 | 30 |
| AID-02572 | 24 | 0 | 0 | Record return 25 | Return exceeds net fulfillment | 24 | 0 | 6 |
| AID-02573 | 24 | 0 | 2 | Request new 3 | Reserve once | 24 | 5 | 1 |
| AID-02574 | 24 | 0 | 2 | Request new 4 | Reserve once | 24 | 6 | 0 |
| AID-02575 | 24 | 0 | 2 | Request new 5 | Exceeds remaining authority | 24 | 2 | 4 |
| AID-02576 | 24 | 0 | 2 | Request new 10 | Exceeds remaining authority | 24 | 2 | 4 |
| AID-02577 | 24 | 0 | 2 | Confirm pending 2 | Settle original once | 26 | 0 | 4 |
| AID-02578 | 24 | 0 | 2 | Fail pending 2 | Release pending reservation | 24 | 0 | 6 |
| AID-02579 | 24 | 0 | 2 | Replay settled 24 | Original receipt; no new effect | 24 | 2 | 4 |
| AID-02580 | 24 | 0 | 2 | Record return 1 | Apply linked return once | 23 | 2 | 5 |
| AID-02581 | 24 | 0 | 2 | Record return 12 | Apply linked return once | 12 | 2 | 16 |
| AID-02582 | 24 | 0 | 2 | Record return 24 | Apply linked return once | 0 | 2 | 28 |
| AID-02583 | 24 | 0 | 2 | Record return 25 | Return exceeds net fulfillment | 24 | 2 | 4 |
| AID-02584 | 24 | 0 | 6 | Request new 1 | Exceeds remaining authority | 24 | 6 | 0 |
| AID-02585 | 24 | 0 | 6 | Request new 10 | Exceeds remaining authority | 24 | 6 | 0 |
| AID-02586 | 24 | 0 | 6 | Confirm pending 6 | Settle original once | 30 | 0 | 0 |
| AID-02587 | 24 | 0 | 6 | Fail pending 6 | Release pending reservation | 24 | 0 | 6 |
| AID-02588 | 24 | 0 | 6 | Replay settled 24 | Original receipt; no new effect | 24 | 6 | 0 |
| AID-02589 | 24 | 0 | 6 | Record return 1 | Apply linked return once | 23 | 6 | 1 |
| AID-02590 | 24 | 0 | 6 | Record return 12 | Apply linked return once | 12 | 6 | 12 |
| AID-02591 | 24 | 0 | 6 | Record return 24 | Apply linked return once | 0 | 6 | 24 |
| AID-02592 | 24 | 0 | 6 | Record return 25 | Return exceeds net fulfillment | 24 | 6 | 0 |
| AID-02593 | 24 | 1 | 0 | Request new 6 | Reserve once | 23 | 6 | 1 |
| AID-02594 | 24 | 1 | 0 | Request new 7 | Reserve once | 23 | 7 | 0 |
| AID-02595 | 24 | 1 | 0 | Request new 8 | Exceeds remaining authority | 23 | 0 | 7 |
| AID-02596 | 24 | 1 | 0 | Request new 10 | Exceeds remaining authority | 23 | 0 | 7 |
| AID-02597 | 24 | 1 | 0 | Replay settled 24 | Original receipt; no new effect | 23 | 0 | 7 |
| AID-02598 | 24 | 1 | 0 | Record return 1 | Apply linked return once | 22 | 0 | 8 |
| AID-02599 | 24 | 1 | 0 | Record return 12 | Apply linked return once | 11 | 0 | 19 |
| AID-02600 | 24 | 1 | 0 | Record return 23 | Apply linked return once | 0 | 0 | 30 |
| AID-02601 | 24 | 1 | 0 | Record return 24 | Return exceeds net fulfillment | 23 | 0 | 7 |
| AID-02602 | 24 | 1 | 3 | Request new 3 | Reserve once | 23 | 6 | 1 |
| AID-02603 | 24 | 1 | 3 | Request new 4 | Reserve once | 23 | 7 | 0 |
| AID-02604 | 24 | 1 | 3 | Request new 5 | Exceeds remaining authority | 23 | 3 | 4 |
| AID-02605 | 24 | 1 | 3 | Request new 10 | Exceeds remaining authority | 23 | 3 | 4 |
| AID-02606 | 24 | 1 | 3 | Confirm pending 3 | Settle original once | 26 | 0 | 4 |
| AID-02607 | 24 | 1 | 3 | Fail pending 3 | Release pending reservation | 23 | 0 | 7 |
| AID-02608 | 24 | 1 | 3 | Replay settled 24 | Original receipt; no new effect | 23 | 3 | 4 |
| AID-02609 | 24 | 1 | 3 | Record return 1 | Apply linked return once | 22 | 3 | 5 |
| AID-02610 | 24 | 1 | 3 | Record return 12 | Apply linked return once | 11 | 3 | 16 |
| AID-02611 | 24 | 1 | 3 | Record return 23 | Apply linked return once | 0 | 3 | 27 |
| AID-02612 | 24 | 1 | 3 | Record return 24 | Return exceeds net fulfillment | 23 | 3 | 4 |
| AID-02613 | 24 | 1 | 7 | Request new 1 | Exceeds remaining authority | 23 | 7 | 0 |
| AID-02614 | 24 | 1 | 7 | Request new 10 | Exceeds remaining authority | 23 | 7 | 0 |
| AID-02615 | 24 | 1 | 7 | Confirm pending 7 | Settle original once | 30 | 0 | 0 |
| AID-02616 | 24 | 1 | 7 | Fail pending 7 | Release pending reservation | 23 | 0 | 7 |
| AID-02617 | 24 | 1 | 7 | Replay settled 24 | Original receipt; no new effect | 23 | 7 | 0 |
| AID-02618 | 24 | 1 | 7 | Record return 1 | Apply linked return once | 22 | 7 | 1 |
| AID-02619 | 24 | 1 | 7 | Record return 12 | Apply linked return once | 11 | 7 | 12 |
| AID-02620 | 24 | 1 | 7 | Record return 23 | Apply linked return once | 0 | 7 | 23 |
| AID-02621 | 24 | 1 | 7 | Record return 24 | Return exceeds net fulfillment | 23 | 7 | 0 |
| AID-02622 | 24 | 6 | 0 | Request new 10 | Reserve once | 18 | 10 | 2 |
| AID-02623 | 24 | 6 | 0 | Request new 11 | Reserve once | 18 | 11 | 1 |
| AID-02624 | 24 | 6 | 0 | Request new 12 | Reserve once | 18 | 12 | 0 |
| AID-02625 | 24 | 6 | 0 | Request new 13 | Exceeds remaining authority | 18 | 0 | 12 |
| AID-02626 | 24 | 6 | 0 | Replay settled 24 | Original receipt; no new effect | 18 | 0 | 12 |
| AID-02627 | 24 | 6 | 0 | Record return 1 | Apply linked return once | 17 | 0 | 13 |
| AID-02628 | 24 | 6 | 0 | Record return 9 | Apply linked return once | 9 | 0 | 21 |
| AID-02629 | 24 | 6 | 0 | Record return 18 | Apply linked return once | 0 | 0 | 30 |
| AID-02630 | 24 | 6 | 0 | Record return 19 | Return exceeds net fulfillment | 18 | 0 | 12 |
| AID-02631 | 24 | 6 | 5 | Request new 6 | Reserve once | 18 | 11 | 1 |
| AID-02632 | 24 | 6 | 5 | Request new 7 | Reserve once | 18 | 12 | 0 |
| AID-02633 | 24 | 6 | 5 | Request new 8 | Exceeds remaining authority | 18 | 5 | 7 |
| AID-02634 | 24 | 6 | 5 | Request new 10 | Exceeds remaining authority | 18 | 5 | 7 |
| AID-02635 | 24 | 6 | 5 | Confirm pending 5 | Settle original once | 23 | 0 | 7 |
| AID-02636 | 24 | 6 | 5 | Fail pending 5 | Release pending reservation | 18 | 0 | 12 |
| AID-02637 | 24 | 6 | 5 | Replay settled 24 | Original receipt; no new effect | 18 | 5 | 7 |
| AID-02638 | 24 | 6 | 5 | Record return 1 | Apply linked return once | 17 | 5 | 8 |
| AID-02639 | 24 | 6 | 5 | Record return 9 | Apply linked return once | 9 | 5 | 16 |
| AID-02640 | 24 | 6 | 5 | Record return 18 | Apply linked return once | 0 | 5 | 25 |
| AID-02641 | 24 | 6 | 5 | Record return 19 | Return exceeds net fulfillment | 18 | 5 | 7 |
| AID-02642 | 24 | 6 | 12 | Request new 1 | Exceeds remaining authority | 18 | 12 | 0 |
| AID-02643 | 24 | 6 | 12 | Request new 10 | Exceeds remaining authority | 18 | 12 | 0 |
| AID-02644 | 24 | 6 | 12 | Confirm pending 12 | Settle original once | 30 | 0 | 0 |
| AID-02645 | 24 | 6 | 12 | Fail pending 12 | Release pending reservation | 18 | 0 | 12 |
| AID-02646 | 24 | 6 | 12 | Replay settled 24 | Original receipt; no new effect | 18 | 12 | 0 |
| AID-02647 | 24 | 6 | 12 | Record return 1 | Apply linked return once | 17 | 12 | 1 |
| AID-02648 | 24 | 6 | 12 | Record return 9 | Apply linked return once | 9 | 12 | 9 |
| AID-02649 | 24 | 6 | 12 | Record return 18 | Apply linked return once | 0 | 12 | 18 |
| AID-02650 | 24 | 6 | 12 | Record return 19 | Return exceeds net fulfillment | 18 | 12 | 0 |
| AID-02651 | 24 | 24 | 0 | Request new 10 | Reserve once | 0 | 10 | 20 |
| AID-02652 | 24 | 24 | 0 | Request new 29 | Reserve once | 0 | 29 | 1 |
| AID-02653 | 24 | 24 | 0 | Request new 30 | Reserve once | 0 | 30 | 0 |
| AID-02654 | 24 | 24 | 0 | Request new 31 | Exceeds remaining authority | 0 | 0 | 30 |
| AID-02655 | 24 | 24 | 0 | Replay settled 24 | Original receipt; no new effect | 0 | 0 | 30 |
| AID-02656 | 24 | 24 | 12 | Request new 10 | Reserve once | 0 | 22 | 8 |
| AID-02657 | 24 | 24 | 12 | Request new 17 | Reserve once | 0 | 29 | 1 |
| AID-02658 | 24 | 24 | 12 | Request new 18 | Reserve once | 0 | 30 | 0 |
| AID-02659 | 24 | 24 | 12 | Request new 19 | Exceeds remaining authority | 0 | 12 | 18 |
| AID-02660 | 24 | 24 | 12 | Confirm pending 12 | Settle original once | 12 | 0 | 18 |
| AID-02661 | 24 | 24 | 12 | Fail pending 12 | Release pending reservation | 0 | 0 | 30 |
| AID-02662 | 24 | 24 | 12 | Replay settled 24 | Original receipt; no new effect | 0 | 12 | 18 |
| AID-02663 | 24 | 24 | 30 | Request new 1 | Exceeds remaining authority | 0 | 30 | 0 |
| AID-02664 | 24 | 24 | 30 | Request new 10 | Exceeds remaining authority | 0 | 30 | 0 |
