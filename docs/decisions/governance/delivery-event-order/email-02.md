# Email bounce and unsubscribe evidence · 2 of 2

[Decision profiles](../README.md) · [Method and other cases](README.md) · [Clerk procedure](../../../handbook/governance/delivery-incident-desk.md)

**Given.** Five observations arrive consecutively at 09:00, 09:01, 09:02, 09:03 and 09:04 UTC for one already submitted route. B is a final non-delivery bounce from this adapter. U is a verified unsubscribe for future optional traffic. D is verified final delivery to the same endpoint; a contradictory bounce needs review. X is a wrong-sender callback. T records the local timeout. K is a reconciliation lookup with no new delivery information. A is provider acceptance (for channel, confirmed publication).

Use the row inputs with this profile. Compare every expected output at the indicated cutoff. Case numbers are local to this profile.

| Case | Arrival order | Trace | Duplicate observations | Quarantined | Future route | Final status | Post views observed | Confirmed people |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| EMAIL-0326 | B → A → D → T → U | f f r r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0327 | B → A → D → U → T | f f r r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0328 | B → A → D → X → U | f f r Q r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0329 | B → A → D → K → U | f f r r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0330 | B → A → U → T → K | f f f f f | 0 | 0 | future optional suppressed | failed | — | 0 |
| EMAIL-0331 | B → A → U → D → K | f f f r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0332 | B → A → U → K → T | f f f f f | 0 | 0 | future optional suppressed | failed | — | 0 |
| EMAIL-0333 | B → A → X → T → D | f f Q f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0334 | B → A → X → D → U | f f Q r r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0335 | B → A → X → U → K | f f Q f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0336 | B → A → X → K → U | f f Q f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0337 | B → A → K → D → T | f f f r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0338 | B → A → K → U → T | f f f f f | 0 | 0 | future optional suppressed | failed | — | 0 |
| EMAIL-0339 | B → A → K → X → D | f f f Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0340 | B → D → T → A → X | f r r r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0341 | B → D → T → U → K | f r r r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0342 | B → D → T → X → K | f r r Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0343 | B → D → A → T → U | f r r r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0344 | B → D → A → U → T | f r r r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0345 | B → D → A → X → U | f r r Q r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0346 | B → D → A → K → X | f r r r Q | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0347 | B → D → U → T → K | f r r r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0348 | B → D → U → X → T | f r r Q r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0349 | B → D → U → K → T | f r r r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0350 | B → D → X → T → U | f r Q r r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0351 | B → D → X → A → U | f r Q r r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0352 | B → D → X → U → K | f r Q r r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0353 | B → D → X → K → U | f r Q r r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0354 | B → D → K → A → T | f r r r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0355 | B → D → K → U → T | f r r r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0356 | B → D → K → X → A | f r r Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0357 | B → U → T → A → K | f f f f f | 0 | 0 | future optional suppressed | failed | — | 0 |
| EMAIL-0358 | B → U → T → D → K | f f f r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0359 | B → U → T → K → A | f f f f f | 0 | 0 | future optional suppressed | failed | — | 0 |
| EMAIL-0360 | B → U → A → T → D | f f f f r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0361 | B → U → A → D → X | f f f r Q | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0362 | B → U → A → X → D | f f f Q r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0363 | B → U → A → K → X | f f f f Q | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0364 | B → U → D → T → K | f f r r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0365 | B → U → D → X → T | f f r Q r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0366 | B → U → D → K → T | f f r r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0367 | B → U → X → T → D | f f Q f r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0368 | B → U → X → A → K | f f Q f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0369 | B → U → X → D → K | f f Q r r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0370 | B → U → K → T → A | f f f f f | 0 | 0 | future optional suppressed | failed | — | 0 |
| EMAIL-0371 | B → U → K → A → T | f f f f f | 0 | 0 | future optional suppressed | failed | — | 0 |
| EMAIL-0372 | B → U → K → D → A | f f f r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0373 | B → U → K → X → A | f f f Q f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0374 | B → X → T → A → K | f Q f f f | 0 | 1 | as previously permitted | failed | — | 0 |
| EMAIL-0375 | B → X → T → D → K | f Q f r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0376 | B → X → T → K → A | f Q f f f | 0 | 1 | as previously permitted | failed | — | 0 |
| EMAIL-0377 | B → X → A → T → D | f Q f f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0378 | B → X → A → D → U | f Q f r r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0379 | B → X → A → U → K | f Q f f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0380 | B → X → A → K → U | f Q f f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0381 | B → X → D → A → T | f Q r r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0382 | B → X → D → U → T | f Q r r r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0383 | B → X → D → K → A | f Q r r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0384 | B → X → U → T → D | f Q f f r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0385 | B → X → U → A → K | f Q f f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0386 | B → X → U → D → K | f Q f r r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0387 | B → X → K → T → A | f Q f f f | 0 | 1 | as previously permitted | failed | — | 0 |
| EMAIL-0388 | B → X → K → A → T | f Q f f f | 0 | 1 | as previously permitted | failed | — | 0 |
| EMAIL-0389 | B → X → K → D → A | f Q f r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0390 | B → X → K → U → D | f Q f f r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0391 | B → K → T → A → X | f f f f Q | 0 | 1 | as previously permitted | failed | — | 0 |
| EMAIL-0392 | B → K → T → U → A | f f f f f | 0 | 0 | future optional suppressed | failed | — | 0 |
| EMAIL-0393 | B → K → T → X → A | f f f Q f | 0 | 1 | as previously permitted | failed | — | 0 |
| EMAIL-0394 | B → K → A → T → U | f f f f f | 0 | 0 | future optional suppressed | failed | — | 0 |
| EMAIL-0395 | B → K → A → D → U | f f f r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0396 | B → K → A → U → X | f f f f Q | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0397 | B → K → A → X → U | f f f Q f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0398 | B → K → D → A → T | f f r r r | 0 | 0 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0399 | B → K → D → U → T | f f r r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0400 | B → K → D → X → A | f f r Q r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0401 | B → K → U → T → X | f f f f Q | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0402 | B → K → U → A → X | f f f f Q | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0403 | B → K → U → X → T | f f f Q f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0404 | B → K → X → T → A | f f Q f f | 0 | 1 | as previously permitted | failed | — | 0 |
| EMAIL-0405 | B → K → X → A → D | f f Q f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0406 | B → K → X → D → A | f f Q r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0407 | B → K → X → U → D | f f Q f r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0408 | U → T → A → D → K | p u a d d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0409 | U → T → A → X → D | p u a Q d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0410 | U → T → A → K → D | p u a a d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0411 | U → T → D → A → X | p u d d Q | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0412 | U → T → D → B → K | p u d r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0413 | U → T → D → X → K | p u d Q d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0414 | U → T → B → A → D | p u f f r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0415 | U → T → B → D → A | p u f r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0416 | U → T → B → X → D | p u f Q r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0417 | U → T → B → K → D | p u f f r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0418 | U → T → X → A → K | p u Q a a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0419 | U → T → X → D → K | p u Q d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0420 | U → T → X → K → A | p u Q u a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0421 | U → T → K → A → D | p u u a d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0422 | U → T → K → D → B | p u u d r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0423 | U → T → K → B → X | p u u f Q | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0424 | U → T → K → X → B | p u u Q f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0425 | U → A → T → B → D | p a a f r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0426 | U → A → T → X → D | p a a Q d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0427 | U → A → T → K → B | p a a a f | 0 | 0 | future optional suppressed | failed | — | 0 |
| EMAIL-0428 | U → A → D → T → X | p a d d Q | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0429 | U → A → D → B → K | p a d r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0430 | U → A → D → X → K | p a d Q d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0431 | U → A → B → T → D | p a f f r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0432 | U → A → B → D → T | p a f r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0433 | U → A → B → X → D | p a f Q r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0434 | U → A → B → K → X | p a f f Q | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0435 | U → A → X → T → K | p a Q a a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0436 | U → A → X → B → T | p a Q f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0437 | U → A → X → K → T | p a Q a a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0438 | U → A → K → T → B | p a a a f | 0 | 0 | future optional suppressed | failed | — | 0 |
| EMAIL-0439 | U → A → K → D → B | p a a d r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0440 | U → A → K → B → X | p a a f Q | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0441 | U → A → K → X → B | p a a Q f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0442 | U → D → T → B → A | p d d r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0443 | U → D → T → X → A | p d d Q d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0444 | U → D → T → K → B | p d d d r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0445 | U → D → A → T → K | p d d d d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0446 | U → D → A → B → K | p d d r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0447 | U → D → A → K → T | p d d d d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0448 | U → D → B → T → A | p d r r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0449 | U → D → B → A → X | p d r r Q | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0450 | U → D → B → X → A | p d r Q r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0451 | U → D → B → K → X | p d r r Q | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0452 | U → D → X → T → K | p d Q d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0453 | U → D → X → B → T | p d Q r r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0454 | U → D → X → K → T | p d Q d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0455 | U → D → K → T → B | p d d d r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0456 | U → D → K → A → X | p d d d Q | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0457 | U → D → K → B → X | p d d r Q | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0458 | U → B → T → A → D | p f f f r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0459 | U → B → T → D → A | p f f r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0460 | U → B → T → X → D | p f f Q r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0461 | U → B → T → K → D | p f f f r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0462 | U → B → A → T → K | p f f f f | 0 | 0 | future optional suppressed | failed | — | 0 |
| EMAIL-0463 | U → B → A → D → K | p f f r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0464 | U → B → A → K → T | p f f f f | 0 | 0 | future optional suppressed | failed | — | 0 |
| EMAIL-0465 | U → B → D → T → A | p f r r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0466 | U → B → D → A → X | p f r r Q | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0467 | U → B → D → X → K | p f r Q r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0468 | U → B → D → K → X | p f r r Q | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0469 | U → B → X → A → T | p f Q f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0470 | U → B → X → D → T | p f Q r r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0471 | U → B → X → K → A | p f Q f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0472 | U → B → K → T → D | p f f f r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0473 | U → B → K → A → X | p f f f Q | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0474 | U → B → K → D → X | p f f r Q | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0475 | U → X → T → A → D | p Q u a d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0476 | U → X → T → D → A | p Q u d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0477 | U → X → T → B → D | p Q u f r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0478 | U → X → T → K → B | p Q u u f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0479 | U → X → A → T → K | p Q a a a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0480 | U → X → A → B → T | p Q a f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0481 | U → X → A → K → T | p Q a a a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0482 | U → X → D → T → B | p Q d d r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0483 | U → X → D → A → B | p Q d d r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0484 | U → X → D → B → K | p Q d r r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0485 | U → X → D → K → B | p Q d d r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0486 | U → X → B → A → T | p Q f f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0487 | U → X → B → D → T | p Q f r r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0488 | U → X → B → K → A | p Q f f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0489 | U → X → K → T → B | p Q p u f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0490 | U → X → K → A → B | p Q p a f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0491 | U → X → K → B → T | p Q p f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0492 | U → K → T → A → D | p p u a d | 0 | 0 | future optional suppressed | delivered | — | 1 |
| EMAIL-0493 | U → K → T → D → B | p p u d r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0494 | U → K → T → B → D | p p u f r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0495 | U → K → T → X → B | p p u Q f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0496 | U → K → A → T → X | p p a a Q | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0497 | U → K → A → B → T | p p a f f | 0 | 0 | future optional suppressed | failed | — | 0 |
| EMAIL-0498 | U → K → A → X → T | p p a Q a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0499 | U → K → D → T → B | p p d d r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0500 | U → K → D → A → X | p p d d Q | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0501 | U → K → D → B → X | p p d r Q | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0502 | U → K → B → T → A | p p f f f | 0 | 0 | future optional suppressed | failed | — | 0 |
| EMAIL-0503 | U → K → B → A → T | p p f f f | 0 | 0 | future optional suppressed | failed | — | 0 |
| EMAIL-0504 | U → K → B → D → A | p p f r r | 0 | 0 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0505 | U → K → B → X → A | p p f Q f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0506 | U → K → X → T → B | p p Q u f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0507 | U → K → X → A → B | p p Q a f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0508 | U → K → X → B → T | p p Q f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0509 | X → T → A → D → B | Q u a d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0510 | X → T → A → B → U | Q u a f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0511 | X → T → A → U → K | Q u a a a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0512 | X → T → A → K → U | Q u a a a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0513 | X → T → D → B → A | Q u d r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0514 | X → T → D → U → A | Q u d d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0515 | X → T → D → K → B | Q u d d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0516 | X → T → B → A → U | Q u f f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0517 | X → T → B → D → K | Q u f r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0518 | X → T → B → U → K | Q u f f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0519 | X → T → U → A → D | Q u u a d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0520 | X → T → U → D → A | Q u u d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0521 | X → T → U → B → D | Q u u f r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0522 | X → T → U → K → B | Q u u u f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0523 | X → T → K → A → U | Q u u a a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0524 | X → T → K → B → A | Q u u f f | 0 | 1 | as previously permitted | failed | — | 0 |
| EMAIL-0525 | X → T → K → U → A | Q u u u a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0526 | X → A → T → D → U | Q a a d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0527 | X → A → T → B → U | Q a a f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0528 | X → A → T → U → K | Q a a a a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0529 | X → A → T → K → U | Q a a a a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0530 | X → A → D → B → T | Q a d r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0531 | X → A → D → U → T | Q a d d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0532 | X → A → D → K → B | Q a d d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0533 | X → A → B → T → K | Q a f f f | 0 | 1 | as previously permitted | failed | — | 0 |
| EMAIL-0534 | X → A → B → D → K | Q a f r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0535 | X → A → B → K → T | Q a f f f | 0 | 1 | as previously permitted | failed | — | 0 |
| EMAIL-0536 | X → A → U → T → D | Q a a a d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0537 | X → A → U → D → B | Q a a d r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0538 | X → A → U → B → D | Q a a f r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0539 | X → A → U → K → B | Q a a a f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0540 | X → A → K → T → U | Q a a a a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0541 | X → A → K → B → T | Q a a f f | 0 | 1 | as previously permitted | failed | — | 0 |
| EMAIL-0542 | X → A → K → U → T | Q a a a a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0543 | X → D → T → A → U | Q d d d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0544 | X → D → T → B → K | Q d d r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0545 | X → D → T → U → K | Q d d d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0546 | X → D → A → T → B | Q d d d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0547 | X → D → A → B → T | Q d d r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0548 | X → D → A → U → B | Q d d d r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0549 | X → D → A → K → B | Q d d d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0550 | X → D → B → T → K | Q d r r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0551 | X → D → B → A → K | Q d r r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0552 | X → D → B → K → T | Q d r r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0553 | X → D → U → T → A | Q d d d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0554 | X → D → U → A → B | Q d d d r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0555 | X → D → U → B → K | Q d d r r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0556 | X → D → U → K → B | Q d d d r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0557 | X → D → K → A → T | Q d d d d | 0 | 1 | as previously permitted | delivered | — | 1 |
| EMAIL-0558 | X → D → K → B → T | Q d d r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0559 | X → D → K → U → A | Q d d d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0560 | X → B → T → A → U | Q f f f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0561 | X → B → T → D → K | Q f f r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0562 | X → B → T → U → K | Q f f f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0563 | X → B → A → T → D | Q f f f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0564 | X → B → A → D → T | Q f f r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0565 | X → B → A → U → D | Q f f f r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0566 | X → B → A → K → U | Q f f f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0567 | X → B → D → T → K | Q f r r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0568 | X → B → D → U → T | Q f r r r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0569 | X → B → D → K → T | Q f r r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0570 | X → B → U → T → D | Q f f f r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0571 | X → B → U → A → D | Q f f f r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0572 | X → B → U → D → K | Q f f r r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0573 | X → B → U → K → D | Q f f f r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0574 | X → B → K → A → T | Q f f f f | 0 | 1 | as previously permitted | failed | — | 0 |
| EMAIL-0575 | X → B → K → D → T | Q f f r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0576 | X → B → K → U → A | Q f f f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0577 | X → U → T → A → K | Q p u a a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0578 | X → U → T → D → K | Q p u d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0579 | X → U → T → K → A | Q p u u a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0580 | X → U → A → T → D | Q p a a d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0581 | X → U → A → D → B | Q p a d r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0582 | X → U → A → B → D | Q p a f r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0583 | X → U → A → K → B | Q p a a f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0584 | X → U → D → T → K | Q p d d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0585 | X → U → D → B → T | Q p d r r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0586 | X → U → D → K → T | Q p d d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0587 | X → U → B → T → D | Q p f f r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0588 | X → U → B → A → K | Q p f f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0589 | X → U → B → D → K | Q p f r r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0590 | X → U → K → T → A | Q p p u a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0591 | X → U → K → A → T | Q p p a a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0592 | X → U → K → D → A | Q p p d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0593 | X → U → K → B → A | Q p p f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0594 | X → K → T → A → U | Q p u a a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0595 | X → K → T → D → U | Q p u d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0596 | X → K → T → U → A | Q p u u a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0597 | X → K → A → T → D | Q p a a d | 0 | 1 | as previously permitted | delivered | — | 1 |
| EMAIL-0598 | X → K → A → D → B | Q p a d r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0599 | X → K → A → B → U | Q p a f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0600 | X → K → A → U → B | Q p a a f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0601 | X → K → D → A → T | Q p d d d | 0 | 1 | as previously permitted | delivered | — | 1 |
| EMAIL-0602 | X → K → D → B → T | Q p d r r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0603 | X → K → D → U → A | Q p d d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0604 | X → K → B → T → D | Q p f f r | 0 | 1 | as previously permitted | review contradictory evidence | — | 0 |
| EMAIL-0605 | X → K → B → A → U | Q p f f f | 0 | 1 | future optional suppressed | failed | — | 0 |
| EMAIL-0606 | X → K → B → D → U | Q p f r r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
| EMAIL-0607 | X → K → U → T → A | Q p p u a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0608 | X → K → U → A → T | Q p p a a | 0 | 1 | future optional suppressed | accepted only | — | 0 |
| EMAIL-0609 | X → K → U → D → A | Q p p d d | 0 | 1 | future optional suppressed | delivered | — | 1 |
| EMAIL-0610 | X → K → U → B → D | Q p p f r | 0 | 1 | future optional suppressed | review contradictory evidence | — | 0 |
