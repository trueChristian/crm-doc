# Meal credits — part 1 of 2

[Policy and other cases](README.md)

One approved award of 60 credits; all inputs use credits at 0 decimal places. One original settled fulfillment, when present, may be partially returned. An outstanding payment or stock issue is reserved against authority. Historical issued and returned amounts are kept even when the net amount is zero. Reviewers can reconstruct this case using the supplied opening facts.

| Case | Opening gross | Opening returns | Opening reserved | Requested event and value | Decision | New net delivered | New reserved | New free authority |
|---|---|---|---|---|---|---|---|---|
| AID-03529 | 0 | 0 | 0 | Request new 20 | Reserve once | 0 | 20 | 40 |
| AID-03530 | 0 | 0 | 0 | Request new 59 | Reserve once | 0 | 59 | 1 |
| AID-03531 | 0 | 0 | 0 | Request new 60 | Reserve once | 0 | 60 | 0 |
| AID-03532 | 0 | 0 | 0 | Request new 61 | Exceeds remaining authority | 0 | 0 | 60 |
| AID-03533 | 0 | 0 | 24 | Request new 20 | Reserve once | 0 | 44 | 16 |
| AID-03534 | 0 | 0 | 24 | Request new 35 | Reserve once | 0 | 59 | 1 |
| AID-03535 | 0 | 0 | 24 | Request new 36 | Reserve once | 0 | 60 | 0 |
| AID-03536 | 0 | 0 | 24 | Request new 37 | Exceeds remaining authority | 0 | 24 | 36 |
| AID-03537 | 0 | 0 | 24 | Confirm pending 24 | Settle original once | 24 | 0 | 36 |
| AID-03538 | 0 | 0 | 24 | Fail pending 24 | Release pending reservation | 0 | 0 | 60 |
| AID-03539 | 0 | 0 | 60 | Request new 1 | Exceeds remaining authority | 0 | 60 | 0 |
| AID-03540 | 0 | 0 | 60 | Request new 20 | Exceeds remaining authority | 0 | 60 | 0 |
| AID-03541 | 0 | 0 | 60 | Confirm pending 60 | Settle original once | 60 | 0 | 0 |
| AID-03542 | 0 | 0 | 60 | Fail pending 60 | Release pending reservation | 0 | 0 | 60 |
| AID-03543 | 12 | 0 | 0 | Request new 20 | Reserve once | 12 | 20 | 28 |
| AID-03544 | 12 | 0 | 0 | Request new 47 | Reserve once | 12 | 47 | 1 |
| AID-03545 | 12 | 0 | 0 | Request new 48 | Reserve once | 12 | 48 | 0 |
| AID-03546 | 12 | 0 | 0 | Request new 49 | Exceeds remaining authority | 12 | 0 | 48 |
| AID-03547 | 12 | 0 | 0 | Replay settled 12 | Original receipt; no new effect | 12 | 0 | 48 |
| AID-03548 | 12 | 0 | 0 | Record return 1 | Apply linked return once | 11 | 0 | 49 |
| AID-03549 | 12 | 0 | 0 | Record return 6 | Apply linked return once | 6 | 0 | 54 |
| AID-03550 | 12 | 0 | 0 | Record return 12 | Apply linked return once | 0 | 0 | 60 |
| AID-03551 | 12 | 0 | 0 | Record return 13 | Return exceeds net fulfillment | 12 | 0 | 48 |
| AID-03552 | 12 | 0 | 19 | Request new 20 | Reserve once | 12 | 39 | 9 |
| AID-03553 | 12 | 0 | 19 | Request new 28 | Reserve once | 12 | 47 | 1 |
| AID-03554 | 12 | 0 | 19 | Request new 29 | Reserve once | 12 | 48 | 0 |
| AID-03555 | 12 | 0 | 19 | Request new 30 | Exceeds remaining authority | 12 | 19 | 29 |
| AID-03556 | 12 | 0 | 19 | Confirm pending 19 | Settle original once | 31 | 0 | 29 |
| AID-03557 | 12 | 0 | 19 | Fail pending 19 | Release pending reservation | 12 | 0 | 48 |
| AID-03558 | 12 | 0 | 19 | Replay settled 12 | Original receipt; no new effect | 12 | 19 | 29 |
| AID-03559 | 12 | 0 | 19 | Record return 1 | Apply linked return once | 11 | 19 | 30 |
| AID-03560 | 12 | 0 | 19 | Record return 6 | Apply linked return once | 6 | 19 | 35 |
| AID-03561 | 12 | 0 | 19 | Record return 12 | Apply linked return once | 0 | 19 | 41 |
| AID-03562 | 12 | 0 | 19 | Record return 13 | Return exceeds net fulfillment | 12 | 19 | 29 |
| AID-03563 | 12 | 0 | 48 | Request new 1 | Exceeds remaining authority | 12 | 48 | 0 |
| AID-03564 | 12 | 0 | 48 | Request new 20 | Exceeds remaining authority | 12 | 48 | 0 |
| AID-03565 | 12 | 0 | 48 | Confirm pending 48 | Settle original once | 60 | 0 | 0 |
| AID-03566 | 12 | 0 | 48 | Fail pending 48 | Release pending reservation | 12 | 0 | 48 |
| AID-03567 | 12 | 0 | 48 | Replay settled 12 | Original receipt; no new effect | 12 | 48 | 0 |
| AID-03568 | 12 | 0 | 48 | Record return 1 | Apply linked return once | 11 | 48 | 1 |
| AID-03569 | 12 | 0 | 48 | Record return 6 | Apply linked return once | 6 | 48 | 6 |
| AID-03570 | 12 | 0 | 48 | Record return 12 | Apply linked return once | 0 | 48 | 12 |
| AID-03571 | 12 | 0 | 48 | Record return 13 | Return exceeds net fulfillment | 12 | 48 | 0 |
| AID-03572 | 12 | 1 | 0 | Request new 20 | Reserve once | 11 | 20 | 29 |
| AID-03573 | 12 | 1 | 0 | Request new 48 | Reserve once | 11 | 48 | 1 |
| AID-03574 | 12 | 1 | 0 | Request new 49 | Reserve once | 11 | 49 | 0 |
| AID-03575 | 12 | 1 | 0 | Request new 50 | Exceeds remaining authority | 11 | 0 | 49 |
| AID-03576 | 12 | 1 | 0 | Replay settled 12 | Original receipt; no new effect | 11 | 0 | 49 |
| AID-03577 | 12 | 1 | 0 | Record return 1 | Apply linked return once | 10 | 0 | 50 |
| AID-03578 | 12 | 1 | 0 | Record return 6 | Apply linked return once | 5 | 0 | 55 |
| AID-03579 | 12 | 1 | 0 | Record return 11 | Apply linked return once | 0 | 0 | 60 |
| AID-03580 | 12 | 1 | 0 | Record return 12 | Return exceeds net fulfillment | 11 | 0 | 49 |
| AID-03581 | 12 | 1 | 20 | Request new 20 | Reserve once | 11 | 40 | 9 |
| AID-03582 | 12 | 1 | 20 | Request new 28 | Reserve once | 11 | 48 | 1 |
| AID-03583 | 12 | 1 | 20 | Request new 29 | Reserve once | 11 | 49 | 0 |
| AID-03584 | 12 | 1 | 20 | Request new 30 | Exceeds remaining authority | 11 | 20 | 29 |
| AID-03585 | 12 | 1 | 20 | Confirm pending 20 | Settle original once | 31 | 0 | 29 |
| AID-03586 | 12 | 1 | 20 | Fail pending 20 | Release pending reservation | 11 | 0 | 49 |
| AID-03587 | 12 | 1 | 20 | Replay settled 12 | Original receipt; no new effect | 11 | 20 | 29 |
| AID-03588 | 12 | 1 | 20 | Record return 1 | Apply linked return once | 10 | 20 | 30 |
| AID-03589 | 12 | 1 | 20 | Record return 6 | Apply linked return once | 5 | 20 | 35 |
| AID-03590 | 12 | 1 | 20 | Record return 11 | Apply linked return once | 0 | 20 | 40 |
| AID-03591 | 12 | 1 | 20 | Record return 12 | Return exceeds net fulfillment | 11 | 20 | 29 |
| AID-03592 | 12 | 1 | 49 | Request new 1 | Exceeds remaining authority | 11 | 49 | 0 |
| AID-03593 | 12 | 1 | 49 | Request new 20 | Exceeds remaining authority | 11 | 49 | 0 |
| AID-03594 | 12 | 1 | 49 | Confirm pending 49 | Settle original once | 60 | 0 | 0 |
| AID-03595 | 12 | 1 | 49 | Fail pending 49 | Release pending reservation | 11 | 0 | 49 |
| AID-03596 | 12 | 1 | 49 | Replay settled 12 | Original receipt; no new effect | 11 | 49 | 0 |
| AID-03597 | 12 | 1 | 49 | Record return 1 | Apply linked return once | 10 | 49 | 1 |
| AID-03598 | 12 | 1 | 49 | Record return 6 | Apply linked return once | 5 | 49 | 6 |
| AID-03599 | 12 | 1 | 49 | Record return 11 | Apply linked return once | 0 | 49 | 11 |
| AID-03600 | 12 | 1 | 49 | Record return 12 | Return exceeds net fulfillment | 11 | 49 | 0 |
| AID-03601 | 12 | 3 | 0 | Request new 20 | Reserve once | 9 | 20 | 31 |
| AID-03602 | 12 | 3 | 0 | Request new 50 | Reserve once | 9 | 50 | 1 |
| AID-03603 | 12 | 3 | 0 | Request new 51 | Reserve once | 9 | 51 | 0 |
| AID-03604 | 12 | 3 | 0 | Request new 52 | Exceeds remaining authority | 9 | 0 | 51 |
| AID-03605 | 12 | 3 | 0 | Replay settled 12 | Original receipt; no new effect | 9 | 0 | 51 |
| AID-03606 | 12 | 3 | 0 | Record return 1 | Apply linked return once | 8 | 0 | 52 |
| AID-03607 | 12 | 3 | 0 | Record return 5 | Apply linked return once | 4 | 0 | 56 |
| AID-03608 | 12 | 3 | 0 | Record return 9 | Apply linked return once | 0 | 0 | 60 |
| AID-03609 | 12 | 3 | 0 | Record return 10 | Return exceeds net fulfillment | 9 | 0 | 51 |
| AID-03610 | 12 | 3 | 20 | Request new 20 | Reserve once | 9 | 40 | 11 |
| AID-03611 | 12 | 3 | 20 | Request new 30 | Reserve once | 9 | 50 | 1 |
| AID-03612 | 12 | 3 | 20 | Request new 31 | Reserve once | 9 | 51 | 0 |
| AID-03613 | 12 | 3 | 20 | Request new 32 | Exceeds remaining authority | 9 | 20 | 31 |
| AID-03614 | 12 | 3 | 20 | Confirm pending 20 | Settle original once | 29 | 0 | 31 |
| AID-03615 | 12 | 3 | 20 | Fail pending 20 | Release pending reservation | 9 | 0 | 51 |
| AID-03616 | 12 | 3 | 20 | Replay settled 12 | Original receipt; no new effect | 9 | 20 | 31 |
| AID-03617 | 12 | 3 | 20 | Record return 1 | Apply linked return once | 8 | 20 | 32 |
| AID-03618 | 12 | 3 | 20 | Record return 5 | Apply linked return once | 4 | 20 | 36 |
| AID-03619 | 12 | 3 | 20 | Record return 9 | Apply linked return once | 0 | 20 | 40 |
| AID-03620 | 12 | 3 | 20 | Record return 10 | Return exceeds net fulfillment | 9 | 20 | 31 |
| AID-03621 | 12 | 3 | 51 | Request new 1 | Exceeds remaining authority | 9 | 51 | 0 |
| AID-03622 | 12 | 3 | 51 | Request new 20 | Exceeds remaining authority | 9 | 51 | 0 |
| AID-03623 | 12 | 3 | 51 | Confirm pending 51 | Settle original once | 60 | 0 | 0 |
| AID-03624 | 12 | 3 | 51 | Fail pending 51 | Release pending reservation | 9 | 0 | 51 |
| AID-03625 | 12 | 3 | 51 | Replay settled 12 | Original receipt; no new effect | 9 | 51 | 0 |
| AID-03626 | 12 | 3 | 51 | Record return 1 | Apply linked return once | 8 | 51 | 1 |
| AID-03627 | 12 | 3 | 51 | Record return 5 | Apply linked return once | 4 | 51 | 5 |
| AID-03628 | 12 | 3 | 51 | Record return 9 | Apply linked return once | 0 | 51 | 9 |
| AID-03629 | 12 | 3 | 51 | Record return 10 | Return exceeds net fulfillment | 9 | 51 | 0 |
| AID-03630 | 12 | 12 | 0 | Request new 20 | Reserve once | 0 | 20 | 40 |
| AID-03631 | 12 | 12 | 0 | Request new 59 | Reserve once | 0 | 59 | 1 |
| AID-03632 | 12 | 12 | 0 | Request new 60 | Reserve once | 0 | 60 | 0 |
| AID-03633 | 12 | 12 | 0 | Request new 61 | Exceeds remaining authority | 0 | 0 | 60 |
| AID-03634 | 12 | 12 | 0 | Replay settled 12 | Original receipt; no new effect | 0 | 0 | 60 |
| AID-03635 | 12 | 12 | 24 | Request new 20 | Reserve once | 0 | 44 | 16 |
| AID-03636 | 12 | 12 | 24 | Request new 35 | Reserve once | 0 | 59 | 1 |
| AID-03637 | 12 | 12 | 24 | Request new 36 | Reserve once | 0 | 60 | 0 |
| AID-03638 | 12 | 12 | 24 | Request new 37 | Exceeds remaining authority | 0 | 24 | 36 |
| AID-03639 | 12 | 12 | 24 | Confirm pending 24 | Settle original once | 24 | 0 | 36 |
| AID-03640 | 12 | 12 | 24 | Fail pending 24 | Release pending reservation | 0 | 0 | 60 |
| AID-03641 | 12 | 12 | 24 | Replay settled 12 | Original receipt; no new effect | 0 | 24 | 36 |
| AID-03642 | 12 | 12 | 60 | Request new 1 | Exceeds remaining authority | 0 | 60 | 0 |
| AID-03643 | 12 | 12 | 60 | Request new 20 | Exceeds remaining authority | 0 | 60 | 0 |
| AID-03644 | 12 | 12 | 60 | Confirm pending 60 | Settle original once | 60 | 0 | 0 |
| AID-03645 | 12 | 12 | 60 | Fail pending 60 | Release pending reservation | 0 | 0 | 60 |
| AID-03646 | 12 | 12 | 60 | Replay settled 12 | Original receipt; no new effect | 0 | 60 | 0 |
| AID-03647 | 30 | 0 | 0 | Request new 20 | Reserve once | 30 | 20 | 10 |
| AID-03648 | 30 | 0 | 0 | Request new 29 | Reserve once | 30 | 29 | 1 |
| AID-03649 | 30 | 0 | 0 | Request new 30 | Reserve once | 30 | 30 | 0 |
| AID-03650 | 30 | 0 | 0 | Request new 31 | Exceeds remaining authority | 30 | 0 | 30 |
| AID-03651 | 30 | 0 | 0 | Replay settled 30 | Original receipt; no new effect | 30 | 0 | 30 |
| AID-03652 | 30 | 0 | 0 | Record return 1 | Apply linked return once | 29 | 0 | 31 |
| AID-03653 | 30 | 0 | 0 | Record return 15 | Apply linked return once | 15 | 0 | 45 |
| AID-03654 | 30 | 0 | 0 | Record return 30 | Apply linked return once | 0 | 0 | 60 |
| AID-03655 | 30 | 0 | 0 | Record return 31 | Return exceeds net fulfillment | 30 | 0 | 30 |
| AID-03656 | 30 | 0 | 12 | Request new 17 | Reserve once | 30 | 29 | 1 |
| AID-03657 | 30 | 0 | 12 | Request new 18 | Reserve once | 30 | 30 | 0 |
| AID-03658 | 30 | 0 | 12 | Request new 19 | Exceeds remaining authority | 30 | 12 | 18 |
| AID-03659 | 30 | 0 | 12 | Request new 20 | Exceeds remaining authority | 30 | 12 | 18 |
| AID-03660 | 30 | 0 | 12 | Confirm pending 12 | Settle original once | 42 | 0 | 18 |
| AID-03661 | 30 | 0 | 12 | Fail pending 12 | Release pending reservation | 30 | 0 | 30 |
| AID-03662 | 30 | 0 | 12 | Replay settled 30 | Original receipt; no new effect | 30 | 12 | 18 |
| AID-03663 | 30 | 0 | 12 | Record return 1 | Apply linked return once | 29 | 12 | 19 |
| AID-03664 | 30 | 0 | 12 | Record return 15 | Apply linked return once | 15 | 12 | 33 |
| AID-03665 | 30 | 0 | 12 | Record return 30 | Apply linked return once | 0 | 12 | 48 |
| AID-03666 | 30 | 0 | 12 | Record return 31 | Return exceeds net fulfillment | 30 | 12 | 18 |
| AID-03667 | 30 | 0 | 30 | Request new 1 | Exceeds remaining authority | 30 | 30 | 0 |
| AID-03668 | 30 | 0 | 30 | Request new 20 | Exceeds remaining authority | 30 | 30 | 0 |
| AID-03669 | 30 | 0 | 30 | Confirm pending 30 | Settle original once | 60 | 0 | 0 |
| AID-03670 | 30 | 0 | 30 | Fail pending 30 | Release pending reservation | 30 | 0 | 30 |
| AID-03671 | 30 | 0 | 30 | Replay settled 30 | Original receipt; no new effect | 30 | 30 | 0 |
| AID-03672 | 30 | 0 | 30 | Record return 1 | Apply linked return once | 29 | 30 | 1 |
| AID-03673 | 30 | 0 | 30 | Record return 15 | Apply linked return once | 15 | 30 | 15 |
| AID-03674 | 30 | 0 | 30 | Record return 30 | Apply linked return once | 0 | 30 | 30 |
| AID-03675 | 30 | 0 | 30 | Record return 31 | Return exceeds net fulfillment | 30 | 30 | 0 |
| AID-03676 | 30 | 1 | 0 | Request new 20 | Reserve once | 29 | 20 | 11 |
| AID-03677 | 30 | 1 | 0 | Request new 30 | Reserve once | 29 | 30 | 1 |
| AID-03678 | 30 | 1 | 0 | Request new 31 | Reserve once | 29 | 31 | 0 |
| AID-03679 | 30 | 1 | 0 | Request new 32 | Exceeds remaining authority | 29 | 0 | 31 |
| AID-03680 | 30 | 1 | 0 | Replay settled 30 | Original receipt; no new effect | 29 | 0 | 31 |
| AID-03681 | 30 | 1 | 0 | Record return 1 | Apply linked return once | 28 | 0 | 32 |
| AID-03682 | 30 | 1 | 0 | Record return 15 | Apply linked return once | 14 | 0 | 46 |
| AID-03683 | 30 | 1 | 0 | Record return 29 | Apply linked return once | 0 | 0 | 60 |
| AID-03684 | 30 | 1 | 0 | Record return 30 | Return exceeds net fulfillment | 29 | 0 | 31 |
| AID-03685 | 30 | 1 | 12 | Request new 18 | Reserve once | 29 | 30 | 1 |
| AID-03686 | 30 | 1 | 12 | Request new 19 | Reserve once | 29 | 31 | 0 |
| AID-03687 | 30 | 1 | 12 | Request new 20 | Exceeds remaining authority | 29 | 12 | 19 |
| AID-03688 | 30 | 1 | 12 | Confirm pending 12 | Settle original once | 41 | 0 | 19 |
| AID-03689 | 30 | 1 | 12 | Fail pending 12 | Release pending reservation | 29 | 0 | 31 |
| AID-03690 | 30 | 1 | 12 | Replay settled 30 | Original receipt; no new effect | 29 | 12 | 19 |
| AID-03691 | 30 | 1 | 12 | Record return 1 | Apply linked return once | 28 | 12 | 20 |
| AID-03692 | 30 | 1 | 12 | Record return 15 | Apply linked return once | 14 | 12 | 34 |
| AID-03693 | 30 | 1 | 12 | Record return 29 | Apply linked return once | 0 | 12 | 48 |
| AID-03694 | 30 | 1 | 12 | Record return 30 | Return exceeds net fulfillment | 29 | 12 | 19 |
| AID-03695 | 30 | 1 | 31 | Request new 1 | Exceeds remaining authority | 29 | 31 | 0 |
| AID-03696 | 30 | 1 | 31 | Request new 20 | Exceeds remaining authority | 29 | 31 | 0 |
| AID-03697 | 30 | 1 | 31 | Confirm pending 31 | Settle original once | 60 | 0 | 0 |
| AID-03698 | 30 | 1 | 31 | Fail pending 31 | Release pending reservation | 29 | 0 | 31 |
| AID-03699 | 30 | 1 | 31 | Replay settled 30 | Original receipt; no new effect | 29 | 31 | 0 |
| AID-03700 | 30 | 1 | 31 | Record return 1 | Apply linked return once | 28 | 31 | 1 |
| AID-03701 | 30 | 1 | 31 | Record return 15 | Apply linked return once | 14 | 31 | 15 |
| AID-03702 | 30 | 1 | 31 | Record return 29 | Apply linked return once | 0 | 31 | 29 |
| AID-03703 | 30 | 1 | 31 | Record return 30 | Return exceeds net fulfillment | 29 | 31 | 0 |
| AID-03704 | 30 | 8 | 0 | Request new 20 | Reserve once | 22 | 20 | 18 |
| AID-03705 | 30 | 8 | 0 | Request new 37 | Reserve once | 22 | 37 | 1 |
| AID-03706 | 30 | 8 | 0 | Request new 38 | Reserve once | 22 | 38 | 0 |
| AID-03707 | 30 | 8 | 0 | Request new 39 | Exceeds remaining authority | 22 | 0 | 38 |
| AID-03708 | 30 | 8 | 0 | Replay settled 30 | Original receipt; no new effect | 22 | 0 | 38 |
| AID-03709 | 30 | 8 | 0 | Record return 1 | Apply linked return once | 21 | 0 | 39 |
| AID-03710 | 30 | 8 | 0 | Record return 11 | Apply linked return once | 11 | 0 | 49 |
| AID-03711 | 30 | 8 | 0 | Record return 22 | Apply linked return once | 0 | 0 | 60 |
| AID-03712 | 30 | 8 | 0 | Record return 23 | Return exceeds net fulfillment | 22 | 0 | 38 |
| AID-03713 | 30 | 8 | 15 | Request new 20 | Reserve once | 22 | 35 | 3 |
| AID-03714 | 30 | 8 | 15 | Request new 22 | Reserve once | 22 | 37 | 1 |
| AID-03715 | 30 | 8 | 15 | Request new 23 | Reserve once | 22 | 38 | 0 |
| AID-03716 | 30 | 8 | 15 | Request new 24 | Exceeds remaining authority | 22 | 15 | 23 |
| AID-03717 | 30 | 8 | 15 | Confirm pending 15 | Settle original once | 37 | 0 | 23 |
| AID-03718 | 30 | 8 | 15 | Fail pending 15 | Release pending reservation | 22 | 0 | 38 |
| AID-03719 | 30 | 8 | 15 | Replay settled 30 | Original receipt; no new effect | 22 | 15 | 23 |
| AID-03720 | 30 | 8 | 15 | Record return 1 | Apply linked return once | 21 | 15 | 24 |
| AID-03721 | 30 | 8 | 15 | Record return 11 | Apply linked return once | 11 | 15 | 34 |
| AID-03722 | 30 | 8 | 15 | Record return 22 | Apply linked return once | 0 | 15 | 45 |
| AID-03723 | 30 | 8 | 15 | Record return 23 | Return exceeds net fulfillment | 22 | 15 | 23 |
| AID-03724 | 30 | 8 | 38 | Request new 1 | Exceeds remaining authority | 22 | 38 | 0 |
| AID-03725 | 30 | 8 | 38 | Request new 20 | Exceeds remaining authority | 22 | 38 | 0 |
| AID-03726 | 30 | 8 | 38 | Confirm pending 38 | Settle original once | 60 | 0 | 0 |
| AID-03727 | 30 | 8 | 38 | Fail pending 38 | Release pending reservation | 22 | 0 | 38 |
| AID-03728 | 30 | 8 | 38 | Replay settled 30 | Original receipt; no new effect | 22 | 38 | 0 |
| AID-03729 | 30 | 8 | 38 | Record return 1 | Apply linked return once | 21 | 38 | 1 |
| AID-03730 | 30 | 8 | 38 | Record return 11 | Apply linked return once | 11 | 38 | 11 |
| AID-03731 | 30 | 8 | 38 | Record return 22 | Apply linked return once | 0 | 38 | 22 |
| AID-03732 | 30 | 8 | 38 | Record return 23 | Return exceeds net fulfillment | 22 | 38 | 0 |
| AID-03733 | 30 | 30 | 0 | Request new 20 | Reserve once | 0 | 20 | 40 |
| AID-03734 | 30 | 30 | 0 | Request new 59 | Reserve once | 0 | 59 | 1 |
| AID-03735 | 30 | 30 | 0 | Request new 60 | Reserve once | 0 | 60 | 0 |
| AID-03736 | 30 | 30 | 0 | Request new 61 | Exceeds remaining authority | 0 | 0 | 60 |
| AID-03737 | 30 | 30 | 0 | Replay settled 30 | Original receipt; no new effect | 0 | 0 | 60 |
| AID-03738 | 30 | 30 | 24 | Request new 20 | Reserve once | 0 | 44 | 16 |
| AID-03739 | 30 | 30 | 24 | Request new 35 | Reserve once | 0 | 59 | 1 |
| AID-03740 | 30 | 30 | 24 | Request new 36 | Reserve once | 0 | 60 | 0 |
| AID-03741 | 30 | 30 | 24 | Request new 37 | Exceeds remaining authority | 0 | 24 | 36 |
| AID-03742 | 30 | 30 | 24 | Confirm pending 24 | Settle original once | 24 | 0 | 36 |
| AID-03743 | 30 | 30 | 24 | Fail pending 24 | Release pending reservation | 0 | 0 | 60 |
| AID-03744 | 30 | 30 | 24 | Replay settled 30 | Original receipt; no new effect | 0 | 24 | 36 |
| AID-03745 | 30 | 30 | 60 | Request new 1 | Exceeds remaining authority | 0 | 60 | 0 |
| AID-03746 | 30 | 30 | 60 | Request new 20 | Exceeds remaining authority | 0 | 60 | 0 |
| AID-03747 | 30 | 30 | 60 | Confirm pending 60 | Settle original once | 60 | 0 | 0 |
| AID-03748 | 30 | 30 | 60 | Fail pending 60 | Release pending reservation | 0 | 0 | 60 |
| AID-03749 | 30 | 30 | 60 | Replay settled 30 | Original receipt; no new effect | 0 | 60 | 0 |
| AID-03750 | 48 | 0 | 0 | Request new 11 | Reserve once | 48 | 11 | 1 |
| AID-03751 | 48 | 0 | 0 | Request new 12 | Reserve once | 48 | 12 | 0 |
| AID-03752 | 48 | 0 | 0 | Request new 13 | Exceeds remaining authority | 48 | 0 | 12 |
| AID-03753 | 48 | 0 | 0 | Request new 20 | Exceeds remaining authority | 48 | 0 | 12 |
| AID-03754 | 48 | 0 | 0 | Replay settled 48 | Original receipt; no new effect | 48 | 0 | 12 |
| AID-03755 | 48 | 0 | 0 | Record return 1 | Apply linked return once | 47 | 0 | 13 |
| AID-03756 | 48 | 0 | 0 | Record return 24 | Apply linked return once | 24 | 0 | 36 |
| AID-03757 | 48 | 0 | 0 | Record return 48 | Apply linked return once | 0 | 0 | 60 |
| AID-03758 | 48 | 0 | 0 | Record return 49 | Return exceeds net fulfillment | 48 | 0 | 12 |
| AID-03759 | 48 | 0 | 5 | Request new 6 | Reserve once | 48 | 11 | 1 |
| AID-03760 | 48 | 0 | 5 | Request new 7 | Reserve once | 48 | 12 | 0 |
| AID-03761 | 48 | 0 | 5 | Request new 8 | Exceeds remaining authority | 48 | 5 | 7 |
| AID-03762 | 48 | 0 | 5 | Request new 20 | Exceeds remaining authority | 48 | 5 | 7 |
| AID-03763 | 48 | 0 | 5 | Confirm pending 5 | Settle original once | 53 | 0 | 7 |
| AID-03764 | 48 | 0 | 5 | Fail pending 5 | Release pending reservation | 48 | 0 | 12 |
| AID-03765 | 48 | 0 | 5 | Replay settled 48 | Original receipt; no new effect | 48 | 5 | 7 |
| AID-03766 | 48 | 0 | 5 | Record return 1 | Apply linked return once | 47 | 5 | 8 |
| AID-03767 | 48 | 0 | 5 | Record return 24 | Apply linked return once | 24 | 5 | 31 |
| AID-03768 | 48 | 0 | 5 | Record return 48 | Apply linked return once | 0 | 5 | 55 |
| AID-03769 | 48 | 0 | 5 | Record return 49 | Return exceeds net fulfillment | 48 | 5 | 7 |
| AID-03770 | 48 | 0 | 12 | Request new 1 | Exceeds remaining authority | 48 | 12 | 0 |
| AID-03771 | 48 | 0 | 12 | Request new 20 | Exceeds remaining authority | 48 | 12 | 0 |
| AID-03772 | 48 | 0 | 12 | Confirm pending 12 | Settle original once | 60 | 0 | 0 |
| AID-03773 | 48 | 0 | 12 | Fail pending 12 | Release pending reservation | 48 | 0 | 12 |
| AID-03774 | 48 | 0 | 12 | Replay settled 48 | Original receipt; no new effect | 48 | 12 | 0 |
| AID-03775 | 48 | 0 | 12 | Record return 1 | Apply linked return once | 47 | 12 | 1 |
| AID-03776 | 48 | 0 | 12 | Record return 24 | Apply linked return once | 24 | 12 | 24 |
| AID-03777 | 48 | 0 | 12 | Record return 48 | Apply linked return once | 0 | 12 | 48 |
| AID-03778 | 48 | 0 | 12 | Record return 49 | Return exceeds net fulfillment | 48 | 12 | 0 |
| AID-03779 | 48 | 1 | 0 | Request new 12 | Reserve once | 47 | 12 | 1 |
| AID-03780 | 48 | 1 | 0 | Request new 13 | Reserve once | 47 | 13 | 0 |
| AID-03781 | 48 | 1 | 0 | Request new 14 | Exceeds remaining authority | 47 | 0 | 13 |
| AID-03782 | 48 | 1 | 0 | Request new 20 | Exceeds remaining authority | 47 | 0 | 13 |
| AID-03783 | 48 | 1 | 0 | Replay settled 48 | Original receipt; no new effect | 47 | 0 | 13 |
| AID-03784 | 48 | 1 | 0 | Record return 1 | Apply linked return once | 46 | 0 | 14 |
| AID-03785 | 48 | 1 | 0 | Record return 24 | Apply linked return once | 23 | 0 | 37 |
| AID-03786 | 48 | 1 | 0 | Record return 47 | Apply linked return once | 0 | 0 | 60 |
| AID-03787 | 48 | 1 | 0 | Record return 48 | Return exceeds net fulfillment | 47 | 0 | 13 |
| AID-03788 | 48 | 1 | 5 | Request new 7 | Reserve once | 47 | 12 | 1 |
| AID-03789 | 48 | 1 | 5 | Request new 8 | Reserve once | 47 | 13 | 0 |
| AID-03790 | 48 | 1 | 5 | Request new 9 | Exceeds remaining authority | 47 | 5 | 8 |
| AID-03791 | 48 | 1 | 5 | Request new 20 | Exceeds remaining authority | 47 | 5 | 8 |
| AID-03792 | 48 | 1 | 5 | Confirm pending 5 | Settle original once | 52 | 0 | 8 |
| AID-03793 | 48 | 1 | 5 | Fail pending 5 | Release pending reservation | 47 | 0 | 13 |
| AID-03794 | 48 | 1 | 5 | Replay settled 48 | Original receipt; no new effect | 47 | 5 | 8 |
| AID-03795 | 48 | 1 | 5 | Record return 1 | Apply linked return once | 46 | 5 | 9 |
| AID-03796 | 48 | 1 | 5 | Record return 24 | Apply linked return once | 23 | 5 | 32 |
| AID-03797 | 48 | 1 | 5 | Record return 47 | Apply linked return once | 0 | 5 | 55 |
| AID-03798 | 48 | 1 | 5 | Record return 48 | Return exceeds net fulfillment | 47 | 5 | 8 |
| AID-03799 | 48 | 1 | 13 | Request new 1 | Exceeds remaining authority | 47 | 13 | 0 |
| AID-03800 | 48 | 1 | 13 | Request new 20 | Exceeds remaining authority | 47 | 13 | 0 |
| AID-03801 | 48 | 1 | 13 | Confirm pending 13 | Settle original once | 60 | 0 | 0 |
| AID-03802 | 48 | 1 | 13 | Fail pending 13 | Release pending reservation | 47 | 0 | 13 |
| AID-03803 | 48 | 1 | 13 | Replay settled 48 | Original receipt; no new effect | 47 | 13 | 0 |
| AID-03804 | 48 | 1 | 13 | Record return 1 | Apply linked return once | 46 | 13 | 1 |
| AID-03805 | 48 | 1 | 13 | Record return 24 | Apply linked return once | 23 | 13 | 24 |
| AID-03806 | 48 | 1 | 13 | Record return 47 | Apply linked return once | 0 | 13 | 47 |
| AID-03807 | 48 | 1 | 13 | Record return 48 | Return exceeds net fulfillment | 47 | 13 | 0 |
| AID-03808 | 48 | 12 | 0 | Request new 20 | Reserve once | 36 | 20 | 4 |
| AID-03809 | 48 | 12 | 0 | Request new 23 | Reserve once | 36 | 23 | 1 |
| AID-03810 | 48 | 12 | 0 | Request new 24 | Reserve once | 36 | 24 | 0 |
| AID-03811 | 48 | 12 | 0 | Request new 25 | Exceeds remaining authority | 36 | 0 | 24 |
| AID-03812 | 48 | 12 | 0 | Replay settled 48 | Original receipt; no new effect | 36 | 0 | 24 |
| AID-03813 | 48 | 12 | 0 | Record return 1 | Apply linked return once | 35 | 0 | 25 |
| AID-03814 | 48 | 12 | 0 | Record return 18 | Apply linked return once | 18 | 0 | 42 |
| AID-03815 | 48 | 12 | 0 | Record return 36 | Apply linked return once | 0 | 0 | 60 |
| AID-03816 | 48 | 12 | 0 | Record return 37 | Return exceeds net fulfillment | 36 | 0 | 24 |
| AID-03817 | 48 | 12 | 10 | Request new 13 | Reserve once | 36 | 23 | 1 |
| AID-03818 | 48 | 12 | 10 | Request new 14 | Reserve once | 36 | 24 | 0 |
| AID-03819 | 48 | 12 | 10 | Request new 15 | Exceeds remaining authority | 36 | 10 | 14 |
| AID-03820 | 48 | 12 | 10 | Request new 20 | Exceeds remaining authority | 36 | 10 | 14 |
| AID-03821 | 48 | 12 | 10 | Confirm pending 10 | Settle original once | 46 | 0 | 14 |
| AID-03822 | 48 | 12 | 10 | Fail pending 10 | Release pending reservation | 36 | 0 | 24 |
| AID-03823 | 48 | 12 | 10 | Replay settled 48 | Original receipt; no new effect | 36 | 10 | 14 |
| AID-03824 | 48 | 12 | 10 | Record return 1 | Apply linked return once | 35 | 10 | 15 |
| AID-03825 | 48 | 12 | 10 | Record return 18 | Apply linked return once | 18 | 10 | 32 |
| AID-03826 | 48 | 12 | 10 | Record return 36 | Apply linked return once | 0 | 10 | 50 |
| AID-03827 | 48 | 12 | 10 | Record return 37 | Return exceeds net fulfillment | 36 | 10 | 14 |
| AID-03828 | 48 | 12 | 24 | Request new 1 | Exceeds remaining authority | 36 | 24 | 0 |
| AID-03829 | 48 | 12 | 24 | Request new 20 | Exceeds remaining authority | 36 | 24 | 0 |
| AID-03830 | 48 | 12 | 24 | Confirm pending 24 | Settle original once | 60 | 0 | 0 |
| AID-03831 | 48 | 12 | 24 | Fail pending 24 | Release pending reservation | 36 | 0 | 24 |
| AID-03832 | 48 | 12 | 24 | Replay settled 48 | Original receipt; no new effect | 36 | 24 | 0 |
| AID-03833 | 48 | 12 | 24 | Record return 1 | Apply linked return once | 35 | 24 | 1 |
| AID-03834 | 48 | 12 | 24 | Record return 18 | Apply linked return once | 18 | 24 | 18 |
| AID-03835 | 48 | 12 | 24 | Record return 36 | Apply linked return once | 0 | 24 | 36 |
| AID-03836 | 48 | 12 | 24 | Record return 37 | Return exceeds net fulfillment | 36 | 24 | 0 |
| AID-03837 | 48 | 48 | 0 | Request new 20 | Reserve once | 0 | 20 | 40 |
| AID-03838 | 48 | 48 | 0 | Request new 59 | Reserve once | 0 | 59 | 1 |
| AID-03839 | 48 | 48 | 0 | Request new 60 | Reserve once | 0 | 60 | 0 |
| AID-03840 | 48 | 48 | 0 | Request new 61 | Exceeds remaining authority | 0 | 0 | 60 |
| AID-03841 | 48 | 48 | 0 | Replay settled 48 | Original receipt; no new effect | 0 | 0 | 60 |
| AID-03842 | 48 | 48 | 24 | Request new 20 | Reserve once | 0 | 44 | 16 |
| AID-03843 | 48 | 48 | 24 | Request new 35 | Reserve once | 0 | 59 | 1 |
| AID-03844 | 48 | 48 | 24 | Request new 36 | Reserve once | 0 | 60 | 0 |
| AID-03845 | 48 | 48 | 24 | Request new 37 | Exceeds remaining authority | 0 | 24 | 36 |
| AID-03846 | 48 | 48 | 24 | Confirm pending 24 | Settle original once | 24 | 0 | 36 |
| AID-03847 | 48 | 48 | 24 | Fail pending 24 | Release pending reservation | 0 | 0 | 60 |
| AID-03848 | 48 | 48 | 24 | Replay settled 48 | Original receipt; no new effect | 0 | 24 | 36 |
