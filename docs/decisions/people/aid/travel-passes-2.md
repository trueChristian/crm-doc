# Travel passes — part 2 of 2

[Policy and other cases](README.md)

One approved award of 30 passes; all inputs use passes at 0 decimal places. One original settled fulfillment, when present, may be partially returned. An outstanding payment or stock issue is reserved against authority. Historical issued and returned amounts are kept even when the net amount is zero. Reviewers can reconstruct this case using the supplied opening facts.

| Case | Opening gross | Opening returns | Opening reserved | Requested event and value | Decision | New net delivered | New reserved | New free authority |
|---|---|---|---|---|---|---|---|---|
| AID-02665 | 24 | 24 | 30 | Confirm pending 30 | Settle original once | 30 | 0 | 0 |
| AID-02666 | 24 | 24 | 30 | Fail pending 30 | Release pending reservation | 0 | 0 | 30 |
| AID-02667 | 24 | 24 | 30 | Replay settled 24 | Original receipt; no new effect | 0 | 30 | 0 |
| AID-02668 | 30 | 0 | 0 | Request new 1 | Exceeds remaining authority | 30 | 0 | 0 |
| AID-02669 | 30 | 0 | 0 | Request new 10 | Exceeds remaining authority | 30 | 0 | 0 |
| AID-02670 | 30 | 0 | 0 | Replay settled 30 | Original receipt; no new effect | 30 | 0 | 0 |
| AID-02671 | 30 | 0 | 0 | Record return 1 | Apply linked return once | 29 | 0 | 1 |
| AID-02672 | 30 | 0 | 0 | Record return 15 | Apply linked return once | 15 | 0 | 15 |
| AID-02673 | 30 | 0 | 0 | Record return 30 | Apply linked return once | 0 | 0 | 30 |
| AID-02674 | 30 | 0 | 0 | Record return 31 | Return exceeds net fulfillment | 30 | 0 | 0 |
| AID-02675 | 30 | 1 | 0 | Request new 1 | Reserve once | 29 | 1 | 0 |
| AID-02676 | 30 | 1 | 0 | Request new 2 | Exceeds remaining authority | 29 | 0 | 1 |
| AID-02677 | 30 | 1 | 0 | Request new 10 | Exceeds remaining authority | 29 | 0 | 1 |
| AID-02678 | 30 | 1 | 0 | Replay settled 30 | Original receipt; no new effect | 29 | 0 | 1 |
| AID-02679 | 30 | 1 | 0 | Record return 1 | Apply linked return once | 28 | 0 | 2 |
| AID-02680 | 30 | 1 | 0 | Record return 15 | Apply linked return once | 14 | 0 | 16 |
| AID-02681 | 30 | 1 | 0 | Record return 29 | Apply linked return once | 0 | 0 | 30 |
| AID-02682 | 30 | 1 | 0 | Record return 30 | Return exceeds net fulfillment | 29 | 0 | 1 |
| AID-02683 | 30 | 1 | 1 | Request new 1 | Exceeds remaining authority | 29 | 1 | 0 |
| AID-02684 | 30 | 1 | 1 | Request new 10 | Exceeds remaining authority | 29 | 1 | 0 |
| AID-02685 | 30 | 1 | 1 | Confirm pending 1 | Settle original once | 30 | 0 | 0 |
| AID-02686 | 30 | 1 | 1 | Fail pending 1 | Release pending reservation | 29 | 0 | 1 |
| AID-02687 | 30 | 1 | 1 | Replay settled 30 | Original receipt; no new effect | 29 | 1 | 0 |
| AID-02688 | 30 | 1 | 1 | Record return 1 | Apply linked return once | 28 | 1 | 1 |
| AID-02689 | 30 | 1 | 1 | Record return 15 | Apply linked return once | 14 | 1 | 15 |
| AID-02690 | 30 | 1 | 1 | Record return 29 | Apply linked return once | 0 | 1 | 29 |
| AID-02691 | 30 | 1 | 1 | Record return 30 | Return exceeds net fulfillment | 29 | 1 | 0 |
| AID-02692 | 30 | 8 | 0 | Request new 7 | Reserve once | 22 | 7 | 1 |
| AID-02693 | 30 | 8 | 0 | Request new 8 | Reserve once | 22 | 8 | 0 |
| AID-02694 | 30 | 8 | 0 | Request new 9 | Exceeds remaining authority | 22 | 0 | 8 |
| AID-02695 | 30 | 8 | 0 | Request new 10 | Exceeds remaining authority | 22 | 0 | 8 |
| AID-02696 | 30 | 8 | 0 | Replay settled 30 | Original receipt; no new effect | 22 | 0 | 8 |
| AID-02697 | 30 | 8 | 0 | Record return 1 | Apply linked return once | 21 | 0 | 9 |
| AID-02698 | 30 | 8 | 0 | Record return 11 | Apply linked return once | 11 | 0 | 19 |
| AID-02699 | 30 | 8 | 0 | Record return 22 | Apply linked return once | 0 | 0 | 30 |
| AID-02700 | 30 | 8 | 0 | Record return 23 | Return exceeds net fulfillment | 22 | 0 | 8 |
| AID-02701 | 30 | 8 | 3 | Request new 4 | Reserve once | 22 | 7 | 1 |
| AID-02702 | 30 | 8 | 3 | Request new 5 | Reserve once | 22 | 8 | 0 |
| AID-02703 | 30 | 8 | 3 | Request new 6 | Exceeds remaining authority | 22 | 3 | 5 |
| AID-02704 | 30 | 8 | 3 | Request new 10 | Exceeds remaining authority | 22 | 3 | 5 |
| AID-02705 | 30 | 8 | 3 | Confirm pending 3 | Settle original once | 25 | 0 | 5 |
| AID-02706 | 30 | 8 | 3 | Fail pending 3 | Release pending reservation | 22 | 0 | 8 |
| AID-02707 | 30 | 8 | 3 | Replay settled 30 | Original receipt; no new effect | 22 | 3 | 5 |
| AID-02708 | 30 | 8 | 3 | Record return 1 | Apply linked return once | 21 | 3 | 6 |
| AID-02709 | 30 | 8 | 3 | Record return 11 | Apply linked return once | 11 | 3 | 16 |
| AID-02710 | 30 | 8 | 3 | Record return 22 | Apply linked return once | 0 | 3 | 27 |
| AID-02711 | 30 | 8 | 3 | Record return 23 | Return exceeds net fulfillment | 22 | 3 | 5 |
| AID-02712 | 30 | 8 | 8 | Request new 1 | Exceeds remaining authority | 22 | 8 | 0 |
| AID-02713 | 30 | 8 | 8 | Request new 10 | Exceeds remaining authority | 22 | 8 | 0 |
| AID-02714 | 30 | 8 | 8 | Confirm pending 8 | Settle original once | 30 | 0 | 0 |
| AID-02715 | 30 | 8 | 8 | Fail pending 8 | Release pending reservation | 22 | 0 | 8 |
| AID-02716 | 30 | 8 | 8 | Replay settled 30 | Original receipt; no new effect | 22 | 8 | 0 |
| AID-02717 | 30 | 8 | 8 | Record return 1 | Apply linked return once | 21 | 8 | 1 |
| AID-02718 | 30 | 8 | 8 | Record return 11 | Apply linked return once | 11 | 8 | 11 |
| AID-02719 | 30 | 8 | 8 | Record return 22 | Apply linked return once | 0 | 8 | 22 |
| AID-02720 | 30 | 8 | 8 | Record return 23 | Return exceeds net fulfillment | 22 | 8 | 0 |
| AID-02721 | 30 | 30 | 0 | Request new 10 | Reserve once | 0 | 10 | 20 |
| AID-02722 | 30 | 30 | 0 | Request new 29 | Reserve once | 0 | 29 | 1 |
| AID-02723 | 30 | 30 | 0 | Request new 30 | Reserve once | 0 | 30 | 0 |
| AID-02724 | 30 | 30 | 0 | Request new 31 | Exceeds remaining authority | 0 | 0 | 30 |
| AID-02725 | 30 | 30 | 0 | Replay settled 30 | Original receipt; no new effect | 0 | 0 | 30 |
| AID-02726 | 30 | 30 | 12 | Request new 10 | Reserve once | 0 | 22 | 8 |
| AID-02727 | 30 | 30 | 12 | Request new 17 | Reserve once | 0 | 29 | 1 |
| AID-02728 | 30 | 30 | 12 | Request new 18 | Reserve once | 0 | 30 | 0 |
| AID-02729 | 30 | 30 | 12 | Request new 19 | Exceeds remaining authority | 0 | 12 | 18 |
| AID-02730 | 30 | 30 | 12 | Confirm pending 12 | Settle original once | 12 | 0 | 18 |
| AID-02731 | 30 | 30 | 12 | Fail pending 12 | Release pending reservation | 0 | 0 | 30 |
| AID-02732 | 30 | 30 | 12 | Replay settled 30 | Original receipt; no new effect | 0 | 12 | 18 |
| AID-02733 | 30 | 30 | 30 | Request new 1 | Exceeds remaining authority | 0 | 30 | 0 |
| AID-02734 | 30 | 30 | 30 | Request new 10 | Exceeds remaining authority | 0 | 30 | 0 |
| AID-02735 | 30 | 30 | 30 | Confirm pending 30 | Settle original once | 30 | 0 | 0 |
| AID-02736 | 30 | 30 | 30 | Fail pending 30 | Release pending reservation | 0 | 0 | 30 |
| AID-02737 | 30 | 30 | 30 | Replay settled 30 | Original receipt; no new effect | 0 | 30 | 0 |
