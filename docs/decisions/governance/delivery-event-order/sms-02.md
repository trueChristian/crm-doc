# SMS delivery and unknown handoff reconciliation · 2 of 2

[Decision profiles](../README.md) · [Method and other cases](README.md) · [Clerk procedure](../../../handbook/governance/delivery-incident-desk.md)

**Given.** Five observations arrive consecutively at 09:00, 09:01, 09:02, 09:03 and 09:04 UTC for one already submitted route. D and D2 repeat the same verified delivery event. F is a definitive failure incompatible with a delivered event for this same destination. X is a wrong-sender callback. T records the local timeout. K is a reconciliation lookup with no new delivery information. A is provider acceptance (for channel, confirmed publication).

Use the row inputs with this profile. Compare every expected output at the indicated cutoff. Case numbers are local to this profile.

| Case | Arrival order | Trace | Duplicate observations | Quarantined | Future route | Final status | Post views observed | Confirmed people |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| SMS-0326 | D2 → A → D → T → F | d d d d r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0327 | D2 → A → D → F → T | d d d r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0328 | D2 → A → D → X → F | d d d Q r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0329 | D2 → A → D → K → F | d d d d r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0330 | D2 → A → F → T → K | d d r r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0331 | D2 → A → F → D → K | d d r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0332 | D2 → A → F → K → T | d d r r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0333 | D2 → A → X → T → D | d d Q d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0334 | D2 → A → X → D → F | d d Q d r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0335 | D2 → A → X → F → K | d d Q r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0336 | D2 → A → X → K → F | d d Q d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0337 | D2 → A → K → D → T | d d d d d | 1 | 0 | as previously permitted | delivered | — | 1 |
| SMS-0338 | D2 → A → K → F → T | d d d r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0339 | D2 → A → K → X → D | d d d Q d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0340 | D2 → D → T → A → X | d d d d Q | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0341 | D2 → D → T → F → K | d d d r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0342 | D2 → D → T → X → K | d d d Q d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0343 | D2 → D → A → T → F | d d d d r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0344 | D2 → D → A → F → T | d d d r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0345 | D2 → D → A → X → F | d d d Q r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0346 | D2 → D → A → K → X | d d d d Q | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0347 | D2 → D → F → T → K | d d r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0348 | D2 → D → F → X → T | d d r Q r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0349 | D2 → D → F → K → T | d d r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0350 | D2 → D → X → T → F | d d Q d r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0351 | D2 → D → X → A → F | d d Q d r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0352 | D2 → D → X → F → K | d d Q r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0353 | D2 → D → X → K → F | d d Q d r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0354 | D2 → D → K → A → T | d d d d d | 1 | 0 | as previously permitted | delivered | — | 1 |
| SMS-0355 | D2 → D → K → F → T | d d d r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0356 | D2 → D → K → X → A | d d d Q d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0357 | D2 → F → T → A → K | d r r r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0358 | D2 → F → T → D → K | d r r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0359 | D2 → F → T → K → A | d r r r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0360 | D2 → F → A → T → D | d r r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0361 | D2 → F → A → D → X | d r r r Q | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0362 | D2 → F → A → X → D | d r r Q r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0363 | D2 → F → A → K → X | d r r r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0364 | D2 → F → D → T → K | d r r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0365 | D2 → F → D → X → T | d r r Q r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0366 | D2 → F → D → K → T | d r r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0367 | D2 → F → X → T → D | d r Q r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0368 | D2 → F → X → A → K | d r Q r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0369 | D2 → F → X → D → K | d r Q r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0370 | D2 → F → K → T → A | d r r r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0371 | D2 → F → K → A → T | d r r r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0372 | D2 → F → K → D → A | d r r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0373 | D2 → F → K → X → A | d r r Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0374 | D2 → X → T → A → K | d Q d d d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0375 | D2 → X → T → D → K | d Q d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0376 | D2 → X → T → K → A | d Q d d d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0377 | D2 → X → A → T → D | d Q d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0378 | D2 → X → A → D → F | d Q d d r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0379 | D2 → X → A → F → K | d Q d r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0380 | D2 → X → A → K → F | d Q d d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0381 | D2 → X → D → A → T | d Q d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0382 | D2 → X → D → F → T | d Q d r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0383 | D2 → X → D → K → A | d Q d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0384 | D2 → X → F → T → D | d Q r r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0385 | D2 → X → F → A → K | d Q r r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0386 | D2 → X → F → D → K | d Q r r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0387 | D2 → X → K → T → A | d Q d d d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0388 | D2 → X → K → A → T | d Q d d d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0389 | D2 → X → K → D → A | d Q d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0390 | D2 → X → K → F → D | d Q d r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0391 | D2 → K → T → A → X | d d d d Q | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0392 | D2 → K → T → F → A | d d d r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0393 | D2 → K → T → X → A | d d d Q d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0394 | D2 → K → A → T → F | d d d d r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0395 | D2 → K → A → D → F | d d d d r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0396 | D2 → K → A → F → X | d d d r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0397 | D2 → K → A → X → F | d d d Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0398 | D2 → K → D → A → T | d d d d d | 1 | 0 | as previously permitted | delivered | — | 1 |
| SMS-0399 | D2 → K → D → F → T | d d d r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0400 | D2 → K → D → X → A | d d d Q d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0401 | D2 → K → F → T → X | d d r r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0402 | D2 → K → F → A → X | d d r r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0403 | D2 → K → F → X → T | d d r Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0404 | D2 → K → X → T → A | d d Q d d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0405 | D2 → K → X → A → D | d d Q d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0406 | D2 → K → X → D → A | d d Q d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0407 | D2 → K → X → F → D | d d Q r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0408 | F → T → A → D → K | f f f r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0409 | F → T → A → X → D | f f f Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0410 | F → T → A → K → D | f f f f r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0411 | F → T → D → A → X | f f r r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0412 | F → T → D → D2 → K | f f r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0413 | F → T → D → X → K | f f r Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0414 | F → T → D2 → A → D | f f r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0415 | F → T → D2 → D → A | f f r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0416 | F → T → D2 → X → D | f f r Q r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0417 | F → T → D2 → K → D | f f r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0418 | F → T → X → A → K | f f Q f f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0419 | F → T → X → D → K | f f Q r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0420 | F → T → X → K → A | f f Q f f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0421 | F → T → K → A → D | f f f f r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0422 | F → T → K → D → D2 | f f f r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0423 | F → T → K → D2 → X | f f f r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0424 | F → T → K → X → D2 | f f f Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0425 | F → A → T → D2 → D | f f f r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0426 | F → A → T → X → D | f f f Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0427 | F → A → T → K → D2 | f f f f r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0428 | F → A → D → T → X | f f r r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0429 | F → A → D → D2 → K | f f r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0430 | F → A → D → X → K | f f r Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0431 | F → A → D2 → T → D | f f r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0432 | F → A → D2 → D → T | f f r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0433 | F → A → D2 → X → D | f f r Q r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0434 | F → A → D2 → K → X | f f r r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0435 | F → A → X → T → K | f f Q f f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0436 | F → A → X → D2 → T | f f Q r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0437 | F → A → X → K → T | f f Q f f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0438 | F → A → K → T → D2 | f f f f r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0439 | F → A → K → D → D2 | f f f r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0440 | F → A → K → D2 → X | f f f r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0441 | F → A → K → X → D2 | f f f Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0442 | F → D → T → D2 → A | f r r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0443 | F → D → T → X → A | f r r Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0444 | F → D → T → K → D2 | f r r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0445 | F → D → A → T → K | f r r r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0446 | F → D → A → D2 → K | f r r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0447 | F → D → A → K → T | f r r r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0448 | F → D → D2 → T → A | f r r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0449 | F → D → D2 → A → X | f r r r Q | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0450 | F → D → D2 → X → A | f r r Q r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0451 | F → D → D2 → K → X | f r r r Q | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0452 | F → D → X → T → K | f r Q r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0453 | F → D → X → D2 → T | f r Q r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0454 | F → D → X → K → T | f r Q r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0455 | F → D → K → T → D2 | f r r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0456 | F → D → K → A → X | f r r r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0457 | F → D → K → D2 → X | f r r r Q | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0458 | F → D2 → T → A → D | f r r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0459 | F → D2 → T → D → A | f r r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0460 | F → D2 → T → X → D | f r r Q r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0461 | F → D2 → T → K → D | f r r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0462 | F → D2 → A → T → K | f r r r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0463 | F → D2 → A → D → K | f r r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0464 | F → D2 → A → K → T | f r r r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0465 | F → D2 → D → T → A | f r r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0466 | F → D2 → D → A → X | f r r r Q | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0467 | F → D2 → D → X → K | f r r Q r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0468 | F → D2 → D → K → X | f r r r Q | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0469 | F → D2 → X → A → T | f r Q r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0470 | F → D2 → X → D → T | f r Q r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0471 | F → D2 → X → K → A | f r Q r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0472 | F → D2 → K → T → D | f r r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0473 | F → D2 → K → A → X | f r r r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0474 | F → D2 → K → D → X | f r r r Q | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0475 | F → X → T → A → D | f Q f f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0476 | F → X → T → D → A | f Q f r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0477 | F → X → T → D2 → D | f Q f r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0478 | F → X → T → K → D2 | f Q f f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0479 | F → X → A → T → K | f Q f f f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0480 | F → X → A → D2 → T | f Q f r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0481 | F → X → A → K → T | f Q f f f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0482 | F → X → D → T → D2 | f Q r r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0483 | F → X → D → A → D2 | f Q r r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0484 | F → X → D → D2 → K | f Q r r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0485 | F → X → D → K → D2 | f Q r r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0486 | F → X → D2 → A → T | f Q r r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0487 | F → X → D2 → D → T | f Q r r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0488 | F → X → D2 → K → A | f Q r r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0489 | F → X → K → T → D2 | f Q f f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0490 | F → X → K → A → D2 | f Q f f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0491 | F → X → K → D2 → T | f Q f r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0492 | F → K → T → A → D | f f f f r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0493 | F → K → T → D → D2 | f f f r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0494 | F → K → T → D2 → D | f f f r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0495 | F → K → T → X → D2 | f f f Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0496 | F → K → A → T → X | f f f f Q | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0497 | F → K → A → D2 → T | f f f r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0498 | F → K → A → X → T | f f f Q f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0499 | F → K → D → T → D2 | f f r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0500 | F → K → D → A → X | f f r r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0501 | F → K → D → D2 → X | f f r r Q | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0502 | F → K → D2 → T → A | f f r r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0503 | F → K → D2 → A → T | f f r r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0504 | F → K → D2 → D → A | f f r r r | 1 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0505 | F → K → D2 → X → A | f f r Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0506 | F → K → X → T → D2 | f f Q f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0507 | F → K → X → A → D2 | f f Q f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0508 | F → K → X → D2 → T | f f Q r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0509 | X → T → A → D → D2 | Q u a d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0510 | X → T → A → D2 → F | Q u a d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0511 | X → T → A → F → K | Q u a f f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0512 | X → T → A → K → F | Q u a a f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0513 | X → T → D → D2 → A | Q u d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0514 | X → T → D → F → A | Q u d r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0515 | X → T → D → K → D2 | Q u d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0516 | X → T → D2 → A → F | Q u d d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0517 | X → T → D2 → D → K | Q u d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0518 | X → T → D2 → F → K | Q u d r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0519 | X → T → F → A → D | Q u f f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0520 | X → T → F → D → A | Q u f r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0521 | X → T → F → D2 → D | Q u f r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0522 | X → T → F → K → D2 | Q u f f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0523 | X → T → K → A → F | Q u u a f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0524 | X → T → K → D2 → A | Q u u d d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0525 | X → T → K → F → A | Q u u f f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0526 | X → A → T → D → F | Q a a d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0527 | X → A → T → D2 → F | Q a a d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0528 | X → A → T → F → K | Q a a f f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0529 | X → A → T → K → F | Q a a a f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0530 | X → A → D → D2 → T | Q a d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0531 | X → A → D → F → T | Q a d r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0532 | X → A → D → K → D2 | Q a d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0533 | X → A → D2 → T → K | Q a d d d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0534 | X → A → D2 → D → K | Q a d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0535 | X → A → D2 → K → T | Q a d d d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0536 | X → A → F → T → D | Q a f f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0537 | X → A → F → D → D2 | Q a f r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0538 | X → A → F → D2 → D | Q a f r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0539 | X → A → F → K → D2 | Q a f f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0540 | X → A → K → T → F | Q a a a f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0541 | X → A → K → D2 → T | Q a a d d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0542 | X → A → K → F → T | Q a a f f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0543 | X → D → T → A → F | Q d d d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0544 | X → D → T → D2 → K | Q d d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0545 | X → D → T → F → K | Q d d r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0546 | X → D → A → T → D2 | Q d d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0547 | X → D → A → D2 → T | Q d d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0548 | X → D → A → F → D2 | Q d d r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0549 | X → D → A → K → D2 | Q d d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0550 | X → D → D2 → T → K | Q d d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0551 | X → D → D2 → A → K | Q d d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0552 | X → D → D2 → K → T | Q d d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0553 | X → D → F → T → A | Q d r r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0554 | X → D → F → A → D2 | Q d r r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0555 | X → D → F → D2 → K | Q d r r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0556 | X → D → F → K → D2 | Q d r r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0557 | X → D → K → A → T | Q d d d d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0558 | X → D → K → D2 → T | Q d d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0559 | X → D → K → F → A | Q d d r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0560 | X → D2 → T → A → F | Q d d d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0561 | X → D2 → T → D → K | Q d d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0562 | X → D2 → T → F → K | Q d d r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0563 | X → D2 → A → T → D | Q d d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0564 | X → D2 → A → D → T | Q d d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0565 | X → D2 → A → F → D | Q d d r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0566 | X → D2 → A → K → F | Q d d d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0567 | X → D2 → D → T → K | Q d d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0568 | X → D2 → D → F → T | Q d d r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0569 | X → D2 → D → K → T | Q d d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0570 | X → D2 → F → T → D | Q d r r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0571 | X → D2 → F → A → D | Q d r r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0572 | X → D2 → F → D → K | Q d r r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0573 | X → D2 → F → K → D | Q d r r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0574 | X → D2 → K → A → T | Q d d d d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0575 | X → D2 → K → D → T | Q d d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0576 | X → D2 → K → F → A | Q d d r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0577 | X → F → T → A → K | Q f f f f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0578 | X → F → T → D → K | Q f f r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0579 | X → F → T → K → A | Q f f f f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0580 | X → F → A → T → D | Q f f f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0581 | X → F → A → D → D2 | Q f f r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0582 | X → F → A → D2 → D | Q f f r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0583 | X → F → A → K → D2 | Q f f f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0584 | X → F → D → T → K | Q f r r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0585 | X → F → D → D2 → T | Q f r r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0586 | X → F → D → K → T | Q f r r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0587 | X → F → D2 → T → D | Q f r r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0588 | X → F → D2 → A → K | Q f r r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0589 | X → F → D2 → D → K | Q f r r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0590 | X → F → K → T → A | Q f f f f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0591 | X → F → K → A → T | Q f f f f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0592 | X → F → K → D → A | Q f f r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0593 | X → F → K → D2 → A | Q f f r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0594 | X → K → T → A → F | Q p u a f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0595 | X → K → T → D → F | Q p u d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0596 | X → K → T → F → A | Q p u f f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0597 | X → K → A → T → D | Q p a a d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0598 | X → K → A → D → D2 | Q p a d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0599 | X → K → A → D2 → F | Q p a d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0600 | X → K → A → F → D2 | Q p a f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0601 | X → K → D → A → T | Q p d d d | 0 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0602 | X → K → D → D2 → T | Q p d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0603 | X → K → D → F → A | Q p d r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0604 | X → K → D2 → T → D | Q p d d d | 1 | 1 | as previously permitted | delivered | — | 1 |
| SMS-0605 | X → K → D2 → A → F | Q p d d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0606 | X → K → D2 → D → F | Q p d d r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0607 | X → K → F → T → A | Q p f f f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0608 | X → K → F → A → T | Q p f f f | 0 | 1 | as previously permitted | failed | — | 0 |
| SMS-0609 | X → K → F → D → A | Q p f r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| SMS-0610 | X → K → F → D2 → D | Q p f r r | 1 | 1 | as previously permitted | review contradictory evidence | — | 0 |
