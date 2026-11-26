# Telegram channel acceptance and permission changes · 2 of 2

[Decision profiles](../README.md) · [Method and other cases](README.md) · [Clerk procedure](../../../handbook/governance/delivery-incident-desk.md)

**Given.** Five observations arrive consecutively at 09:00, 09:01, 09:02, 09:03 and 09:04 UTC for one already submitted route. A and A2 are duplicate confirmations of the same post. P withdraws posting permission for future sends. V records an aggregate 37 views of this post without identifying people. X is a wrong-sender callback. T records the local timeout. K is a reconciliation lookup with no new delivery information. A is provider acceptance (for channel, confirmed publication).

Use the row inputs with this profile. Compare every expected output at the indicated cutoff. Case numbers are local to this profile.

| Case | Arrival order | Trace | Duplicate observations | Quarantined | Future route | Final status | Post views observed | Confirmed people |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CHANNEL-0326 | P → A → A2 → T → V | p s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0327 | P → A → A2 → V → T | p s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0328 | P → A → A2 → X → V | p s s Q s | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0329 | P → A → A2 → K → V | p s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0330 | P → A → V → T → K | p s s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0331 | P → A → V → A2 → K | p s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0332 | P → A → V → K → T | p s s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0333 | P → A → X → T → A2 | p s Q s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0334 | P → A → X → A2 → V | p s Q s s | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0335 | P → A → X → V → K | p s Q s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0336 | P → A → X → K → V | p s Q s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0337 | P → A → K → A2 → T | p s s s s | 1 | 0 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0338 | P → A → K → V → T | p s s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0339 | P → A → K → X → A2 | p s s Q s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0340 | P → A2 → T → A → X | p s s s Q | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0341 | P → A2 → T → V → K | p s s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0342 | P → A2 → T → X → K | p s s Q s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0343 | P → A2 → A → T → V | p s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0344 | P → A2 → A → V → T | p s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0345 | P → A2 → A → X → V | p s s Q s | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0346 | P → A2 → A → K → X | p s s s Q | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0347 | P → A2 → V → T → K | p s s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0348 | P → A2 → V → X → T | p s s Q s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0349 | P → A2 → V → K → T | p s s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0350 | P → A2 → X → T → V | p s Q s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0351 | P → A2 → X → A → V | p s Q s s | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0352 | P → A2 → X → V → K | p s Q s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0353 | P → A2 → X → K → V | p s Q s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0354 | P → A2 → K → A → T | p s s s s | 1 | 0 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0355 | P → A2 → K → V → T | p s s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0356 | P → A2 → K → X → A | p s s Q s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0357 | P → V → T → A → K | p p u s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0358 | P → V → T → A2 → K | p p u s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0359 | P → V → T → K → A | p p u u s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0360 | P → V → A → T → A2 | p p s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0361 | P → V → A → A2 → X | p p s s Q | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0362 | P → V → A → X → A2 | p p s Q s | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0363 | P → V → A → K → X | p p s s Q | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0364 | P → V → A2 → T → K | p p s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0365 | P → V → A2 → X → T | p p s Q s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0366 | P → V → A2 → K → T | p p s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0367 | P → V → X → T → A2 | p p Q u s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0368 | P → V → X → A → K | p p Q s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0369 | P → V → X → A2 → K | p p Q s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0370 | P → V → K → T → A | p p p u s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0371 | P → V → K → A → T | p p p s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0372 | P → V → K → A2 → A | p p p s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0373 | P → V → K → X → A | p p p Q s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0374 | P → X → T → A → K | p Q u s s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0375 | P → X → T → A2 → K | p Q u s s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0376 | P → X → T → K → A | p Q u u s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0377 | P → X → A → T → A2 | p Q s s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0378 | P → X → A → A2 → V | p Q s s s | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0379 | P → X → A → V → K | p Q s s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0380 | P → X → A → K → V | p Q s s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0381 | P → X → A2 → A → T | p Q s s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0382 | P → X → A2 → V → T | p Q s s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0383 | P → X → A2 → K → A | p Q s s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0384 | P → X → V → T → A2 | p Q p u s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0385 | P → X → V → A → K | p Q p s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0386 | P → X → V → A2 → K | p Q p s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0387 | P → X → K → T → A | p Q p u s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0388 | P → X → K → A → T | p Q p s s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0389 | P → X → K → A2 → A | p Q p s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0390 | P → X → K → V → A2 | p Q p p s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0391 | P → K → T → A → X | p p u s Q | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0392 | P → K → T → V → A | p p u u s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0393 | P → K → T → X → A | p p u Q s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0394 | P → K → A → T → V | p p s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0395 | P → K → A → A2 → V | p p s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0396 | P → K → A → V → X | p p s s Q | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0397 | P → K → A → X → V | p p s Q s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0398 | P → K → A2 → A → T | p p s s s | 1 | 0 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0399 | P → K → A2 → V → T | p p s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0400 | P → K → A2 → X → A | p p s Q s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0401 | P → K → V → T → X | p p p u Q | 0 | 1 | posting suspended | await post confirmation | 37 | 0 |
| CHANNEL-0402 | P → K → V → A → X | p p p s Q | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0403 | P → K → V → X → T | p p p Q u | 0 | 1 | posting suspended | await post confirmation | 37 | 0 |
| CHANNEL-0404 | P → K → X → T → A | p p Q u s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0405 | P → K → X → A → A2 | p p Q s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0406 | P → K → X → A2 → A | p p Q s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0407 | P → K → X → V → A2 | p p Q p s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0408 | V → T → A → A2 → K | p u s s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0409 | V → T → A → X → A2 | p u s Q s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0410 | V → T → A → K → A2 | p u s s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0411 | V → T → A2 → A → X | p u s s Q | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0412 | V → T → A2 → P → K | p u s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0413 | V → T → A2 → X → K | p u s Q s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0414 | V → T → P → A → A2 | p u u s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0415 | V → T → P → A2 → A | p u u s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0416 | V → T → P → X → A2 | p u u Q s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0417 | V → T → P → K → A2 | p u u u s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0418 | V → T → X → A → K | p u Q s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0419 | V → T → X → A2 → K | p u Q s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0420 | V → T → X → K → A | p u Q u s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0421 | V → T → K → A → A2 | p u u s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0422 | V → T → K → A2 → P | p u u s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0423 | V → T → K → P → X | p u u u Q | 0 | 1 | posting suspended | await post confirmation | 37 | 0 |
| CHANNEL-0424 | V → T → K → X → P | p u u Q u | 0 | 1 | posting suspended | await post confirmation | 37 | 0 |
| CHANNEL-0425 | V → A → T → P → A2 | p s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0426 | V → A → T → X → A2 | p s s Q s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0427 | V → A → T → K → P | p s s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0428 | V → A → A2 → T → X | p s s s Q | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0429 | V → A → A2 → P → K | p s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0430 | V → A → A2 → X → K | p s s Q s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0431 | V → A → P → T → A2 | p s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0432 | V → A → P → A2 → T | p s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0433 | V → A → P → X → A2 | p s s Q s | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0434 | V → A → P → K → X | p s s s Q | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0435 | V → A → X → T → K | p s Q s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0436 | V → A → X → P → T | p s Q s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0437 | V → A → X → K → T | p s Q s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0438 | V → A → K → T → P | p s s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0439 | V → A → K → A2 → P | p s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0440 | V → A → K → P → X | p s s s Q | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0441 | V → A → K → X → P | p s s Q s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0442 | V → A2 → T → P → A | p s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0443 | V → A2 → T → X → A | p s s Q s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0444 | V → A2 → T → K → P | p s s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0445 | V → A2 → A → T → K | p s s s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0446 | V → A2 → A → P → K | p s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0447 | V → A2 → A → K → T | p s s s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0448 | V → A2 → P → T → A | p s s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0449 | V → A2 → P → A → X | p s s s Q | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0450 | V → A2 → P → X → A | p s s Q s | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0451 | V → A2 → P → K → X | p s s s Q | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0452 | V → A2 → X → T → K | p s Q s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0453 | V → A2 → X → P → T | p s Q s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0454 | V → A2 → X → K → T | p s Q s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0455 | V → A2 → K → T → P | p s s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0456 | V → A2 → K → A → X | p s s s Q | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0457 | V → A2 → K → P → X | p s s s Q | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0458 | V → P → T → A → A2 | p p u s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0459 | V → P → T → A2 → A | p p u s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0460 | V → P → T → X → A2 | p p u Q s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0461 | V → P → T → K → A2 | p p u u s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0462 | V → P → A → T → K | p p s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0463 | V → P → A → A2 → K | p p s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0464 | V → P → A → K → T | p p s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0465 | V → P → A2 → T → A | p p s s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0466 | V → P → A2 → A → X | p p s s Q | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0467 | V → P → A2 → X → K | p p s Q s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0468 | V → P → A2 → K → X | p p s s Q | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0469 | V → P → X → A → T | p p Q s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0470 | V → P → X → A2 → T | p p Q s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0471 | V → P → X → K → A | p p Q p s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0472 | V → P → K → T → A2 | p p p u s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0473 | V → P → K → A → X | p p p s Q | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0474 | V → P → K → A2 → X | p p p s Q | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0475 | V → X → T → A → A2 | p Q u s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0476 | V → X → T → A2 → A | p Q u s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0477 | V → X → T → P → A2 | p Q u u s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0478 | V → X → T → K → P | p Q u u u | 0 | 1 | posting suspended | await post confirmation | 37 | 0 |
| CHANNEL-0479 | V → X → A → T → K | p Q s s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0480 | V → X → A → P → T | p Q s s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0481 | V → X → A → K → T | p Q s s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0482 | V → X → A2 → T → P | p Q s s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0483 | V → X → A2 → A → P | p Q s s s | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0484 | V → X → A2 → P → K | p Q s s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0485 | V → X → A2 → K → P | p Q s s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0486 | V → X → P → A → T | p Q p s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0487 | V → X → P → A2 → T | p Q p s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0488 | V → X → P → K → A | p Q p p s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0489 | V → X → K → T → P | p Q p u u | 0 | 1 | posting suspended | await post confirmation | 37 | 0 |
| CHANNEL-0490 | V → X → K → A → P | p Q p s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0491 | V → X → K → P → T | p Q p p u | 0 | 1 | posting suspended | await post confirmation | 37 | 0 |
| CHANNEL-0492 | V → K → T → A → A2 | p p u s s | 1 | 0 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0493 | V → K → T → A2 → P | p p u s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0494 | V → K → T → P → A2 | p p u u s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0495 | V → K → T → X → P | p p u Q u | 0 | 1 | posting suspended | await post confirmation | 37 | 0 |
| CHANNEL-0496 | V → K → A → T → X | p p s s Q | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0497 | V → K → A → P → T | p p s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0498 | V → K → A → X → T | p p s Q s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0499 | V → K → A2 → T → P | p p s s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0500 | V → K → A2 → A → X | p p s s Q | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0501 | V → K → A2 → P → X | p p s s Q | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0502 | V → K → P → T → A | p p p u s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0503 | V → K → P → A → T | p p p s s | 0 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0504 | V → K → P → A2 → A | p p p s s | 1 | 0 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0505 | V → K → P → X → A | p p p Q s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0506 | V → K → X → T → P | p p Q u u | 0 | 1 | posting suspended | await post confirmation | 37 | 0 |
| CHANNEL-0507 | V → K → X → A → P | p p Q s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0508 | V → K → X → P → T | p p Q p u | 0 | 1 | posting suspended | await post confirmation | 37 | 0 |
| CHANNEL-0509 | X → T → A → A2 → P | Q u s s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0510 | X → T → A → P → V | Q u s s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0511 | X → T → A → V → K | Q u s s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0512 | X → T → A → K → V | Q u s s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0513 | X → T → A2 → P → A | Q u s s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0514 | X → T → A2 → V → A | Q u s s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0515 | X → T → A2 → K → P | Q u s s s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0516 | X → T → P → A → V | Q u u s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0517 | X → T → P → A2 → K | Q u u s s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0518 | X → T → P → V → K | Q u u u u | 0 | 1 | posting suspended | await post confirmation | 37 | 0 |
| CHANNEL-0519 | X → T → V → A → A2 | Q u u s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0520 | X → T → V → A2 → A | Q u u s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0521 | X → T → V → P → A2 | Q u u u s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0522 | X → T → V → K → P | Q u u u u | 0 | 1 | posting suspended | await post confirmation | 37 | 0 |
| CHANNEL-0523 | X → T → K → A → V | Q u u s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0524 | X → T → K → P → A | Q u u u s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0525 | X → T → K → V → A | Q u u u s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0526 | X → A → T → A2 → V | Q s s s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0527 | X → A → T → P → V | Q s s s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0528 | X → A → T → V → K | Q s s s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0529 | X → A → T → K → V | Q s s s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0530 | X → A → A2 → P → T | Q s s s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0531 | X → A → A2 → V → T | Q s s s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0532 | X → A → A2 → K → P | Q s s s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0533 | X → A → P → T → K | Q s s s s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0534 | X → A → P → A2 → K | Q s s s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0535 | X → A → P → K → T | Q s s s s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0536 | X → A → V → T → A2 | Q s s s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0537 | X → A → V → A2 → P | Q s s s s | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0538 | X → A → V → P → A2 | Q s s s s | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0539 | X → A → V → K → P | Q s s s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0540 | X → A → K → T → V | Q s s s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0541 | X → A → K → P → T | Q s s s s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0542 | X → A → K → V → T | Q s s s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0543 | X → A2 → T → A → V | Q s s s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0544 | X → A2 → T → P → K | Q s s s s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0545 | X → A2 → T → V → K | Q s s s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0546 | X → A2 → A → T → P | Q s s s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0547 | X → A2 → A → P → T | Q s s s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0548 | X → A2 → A → V → P | Q s s s s | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0549 | X → A2 → A → K → P | Q s s s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0550 | X → A2 → P → T → K | Q s s s s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0551 | X → A2 → P → A → K | Q s s s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0552 | X → A2 → P → K → T | Q s s s s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0553 | X → A2 → V → T → A | Q s s s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0554 | X → A2 → V → A → P | Q s s s s | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0555 | X → A2 → V → P → K | Q s s s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0556 | X → A2 → V → K → P | Q s s s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0557 | X → A2 → K → A → T | Q s s s s | 1 | 1 | as previously permitted | posted once | 0 | 0 |
| CHANNEL-0558 | X → A2 → K → P → T | Q s s s s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0559 | X → A2 → K → V → A | Q s s s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0560 | X → P → T → A → V | Q p u s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0561 | X → P → T → A2 → K | Q p u s s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0562 | X → P → T → V → K | Q p u u u | 0 | 1 | posting suspended | await post confirmation | 37 | 0 |
| CHANNEL-0563 | X → P → A → T → A2 | Q p s s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0564 | X → P → A → A2 → T | Q p s s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0565 | X → P → A → V → A2 | Q p s s s | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0566 | X → P → A → K → V | Q p s s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0567 | X → P → A2 → T → K | Q p s s s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0568 | X → P → A2 → V → T | Q p s s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0569 | X → P → A2 → K → T | Q p s s s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0570 | X → P → V → T → A2 | Q p p u s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0571 | X → P → V → A → A2 | Q p p s s | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0572 | X → P → V → A2 → K | Q p p s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0573 | X → P → V → K → A2 | Q p p p s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0574 | X → P → K → A → T | Q p p s s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0575 | X → P → K → A2 → T | Q p p s s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0576 | X → P → K → V → A | Q p p p s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0577 | X → V → T → A → K | Q p u s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0578 | X → V → T → A2 → K | Q p u s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0579 | X → V → T → K → A | Q p u u s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0580 | X → V → A → T → A2 | Q p s s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0581 | X → V → A → A2 → P | Q p s s s | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0582 | X → V → A → P → A2 | Q p s s s | 1 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0583 | X → V → A → K → P | Q p s s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0584 | X → V → A2 → T → K | Q p s s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0585 | X → V → A2 → P → T | Q p s s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0586 | X → V → A2 → K → T | Q p s s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0587 | X → V → P → T → A2 | Q p p u s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0588 | X → V → P → A → K | Q p p s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0589 | X → V → P → A2 → K | Q p p s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0590 | X → V → K → T → A | Q p p u s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0591 | X → V → K → A → T | Q p p s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0592 | X → V → K → A2 → A | Q p p s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0593 | X → V → K → P → A | Q p p p s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0594 | X → K → T → A → V | Q p u s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0595 | X → K → T → A2 → V | Q p u s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0596 | X → K → T → V → A | Q p u u s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0597 | X → K → A → T → A2 | Q p s s s | 1 | 1 | as previously permitted | posted once | 0 | 0 |
| CHANNEL-0598 | X → K → A → A2 → P | Q p s s s | 1 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0599 | X → K → A → P → V | Q p s s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0600 | X → K → A → V → P | Q p s s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0601 | X → K → A2 → A → T | Q p s s s | 1 | 1 | as previously permitted | posted once | 0 | 0 |
| CHANNEL-0602 | X → K → A2 → P → T | Q p s s s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0603 | X → K → A2 → V → A | Q p s s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0604 | X → K → P → T → A2 | Q p p u s | 0 | 1 | posting suspended | posted once | 0 | 0 |
| CHANNEL-0605 | X → K → P → A → V | Q p p s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0606 | X → K → P → A2 → V | Q p p s s | 0 | 1 | posting suspended | posted once | 37 | 0 |
| CHANNEL-0607 | X → K → V → T → A | Q p p u s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0608 | X → K → V → A → T | Q p p s s | 0 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0609 | X → K → V → A2 → A | Q p p s s | 1 | 1 | as previously permitted | posted once | 37 | 0 |
| CHANNEL-0610 | X → K → V → P → A2 | Q p p p s | 0 | 1 | posting suspended | posted once | 37 | 0 |
