# Emergency food voucher — part 2 of 2

[Policy and other cases](README.md)

One approved award of 125.50 currency units; all inputs use currency units at 2 decimal places. One original settled fulfillment, when present, may be partially returned. An outstanding payment or stock issue is reserved against authority. Historical issued and returned amounts are kept even when the net amount is zero. Reviewers can reconstruct this case using the supplied opening facts.

| Case | Opening gross | Opening returns | Opening reserved | Requested event and value | Decision | New net delivered | New reserved | New free authority |
|---|---|---|---|---|---|---|---|---|
| AID-00717 | 100.40 | 100.40 | 50.20 | Replay settled 100.40 | Original receipt; no new effect | 0.00 | 50.20 | 75.30 |
| AID-00718 | 100.40 | 100.40 | 125.50 | Request new 0.01 | Exceeds remaining authority | 0.00 | 125.50 | 0.00 |
| AID-00719 | 100.40 | 100.40 | 125.50 | Request new 41.42 | Exceeds remaining authority | 0.00 | 125.50 | 0.00 |
| AID-00720 | 100.40 | 100.40 | 125.50 | Confirm pending 125.50 | Settle original once | 125.50 | 0.00 | 0.00 |
| AID-00721 | 100.40 | 100.40 | 125.50 | Fail pending 125.50 | Release pending reservation | 0.00 | 0.00 | 125.50 |
| AID-00722 | 100.40 | 100.40 | 125.50 | Replay settled 100.40 | Original receipt; no new effect | 0.00 | 125.50 | 0.00 |
| AID-00723 | 125.50 | 0.00 | 0.00 | Request new 0.01 | Exceeds remaining authority | 125.50 | 0.00 | 0.00 |
| AID-00724 | 125.50 | 0.00 | 0.00 | Request new 41.42 | Exceeds remaining authority | 125.50 | 0.00 | 0.00 |
| AID-00725 | 125.50 | 0.00 | 0.00 | Replay settled 125.50 | Original receipt; no new effect | 125.50 | 0.00 | 0.00 |
| AID-00726 | 125.50 | 0.00 | 0.00 | Record return 0.01 | Apply linked return once | 125.49 | 0.00 | 0.01 |
| AID-00727 | 125.50 | 0.00 | 0.00 | Record return 62.75 | Apply linked return once | 62.75 | 0.00 | 62.75 |
| AID-00728 | 125.50 | 0.00 | 0.00 | Record return 125.50 | Apply linked return once | 0.00 | 0.00 | 125.50 |
| AID-00729 | 125.50 | 0.00 | 0.00 | Record return 125.51 | Return exceeds net fulfillment | 125.50 | 0.00 | 0.00 |
| AID-00730 | 125.50 | 0.01 | 0.00 | Request new 0.01 | Reserve once | 125.49 | 0.01 | 0.00 |
| AID-00731 | 125.50 | 0.01 | 0.00 | Request new 0.02 | Exceeds remaining authority | 125.49 | 0.00 | 0.01 |
| AID-00732 | 125.50 | 0.01 | 0.00 | Request new 41.42 | Exceeds remaining authority | 125.49 | 0.00 | 0.01 |
| AID-00733 | 125.50 | 0.01 | 0.00 | Replay settled 125.50 | Original receipt; no new effect | 125.49 | 0.00 | 0.01 |
| AID-00734 | 125.50 | 0.01 | 0.00 | Record return 0.01 | Apply linked return once | 125.48 | 0.00 | 0.02 |
| AID-00735 | 125.50 | 0.01 | 0.00 | Record return 62.75 | Apply linked return once | 62.74 | 0.00 | 62.76 |
| AID-00736 | 125.50 | 0.01 | 0.00 | Record return 125.49 | Apply linked return once | 0.00 | 0.00 | 125.50 |
| AID-00737 | 125.50 | 0.01 | 0.00 | Record return 125.50 | Return exceeds net fulfillment | 125.49 | 0.00 | 0.01 |
| AID-00738 | 125.50 | 0.01 | 0.01 | Request new 0.01 | Exceeds remaining authority | 125.49 | 0.01 | 0.00 |
| AID-00739 | 125.50 | 0.01 | 0.01 | Request new 41.42 | Exceeds remaining authority | 125.49 | 0.01 | 0.00 |
| AID-00740 | 125.50 | 0.01 | 0.01 | Confirm pending 0.01 | Settle original once | 125.50 | 0.00 | 0.00 |
| AID-00741 | 125.50 | 0.01 | 0.01 | Fail pending 0.01 | Release pending reservation | 125.49 | 0.00 | 0.01 |
| AID-00742 | 125.50 | 0.01 | 0.01 | Replay settled 125.50 | Original receipt; no new effect | 125.49 | 0.01 | 0.00 |
| AID-00743 | 125.50 | 0.01 | 0.01 | Record return 0.01 | Apply linked return once | 125.48 | 0.01 | 0.01 |
| AID-00744 | 125.50 | 0.01 | 0.01 | Record return 62.75 | Apply linked return once | 62.74 | 0.01 | 62.75 |
| AID-00745 | 125.50 | 0.01 | 0.01 | Record return 125.49 | Apply linked return once | 0.00 | 0.01 | 125.49 |
| AID-00746 | 125.50 | 0.01 | 0.01 | Record return 125.50 | Return exceeds net fulfillment | 125.49 | 0.01 | 0.00 |
| AID-00747 | 125.50 | 31.38 | 0.00 | Request new 31.37 | Reserve once | 94.12 | 31.37 | 0.01 |
| AID-00748 | 125.50 | 31.38 | 0.00 | Request new 31.38 | Reserve once | 94.12 | 31.38 | 0.00 |
| AID-00749 | 125.50 | 31.38 | 0.00 | Request new 31.39 | Exceeds remaining authority | 94.12 | 0.00 | 31.38 |
| AID-00750 | 125.50 | 31.38 | 0.00 | Request new 41.42 | Exceeds remaining authority | 94.12 | 0.00 | 31.38 |
| AID-00751 | 125.50 | 31.38 | 0.00 | Replay settled 125.50 | Original receipt; no new effect | 94.12 | 0.00 | 31.38 |
| AID-00752 | 125.50 | 31.38 | 0.00 | Record return 0.01 | Apply linked return once | 94.11 | 0.00 | 31.39 |
| AID-00753 | 125.50 | 31.38 | 0.00 | Record return 47.06 | Apply linked return once | 47.06 | 0.00 | 78.44 |
| AID-00754 | 125.50 | 31.38 | 0.00 | Record return 94.12 | Apply linked return once | 0.00 | 0.00 | 125.50 |
| AID-00755 | 125.50 | 31.38 | 0.00 | Record return 94.13 | Return exceeds net fulfillment | 94.12 | 0.00 | 31.38 |
| AID-00756 | 125.50 | 31.38 | 12.55 | Request new 18.82 | Reserve once | 94.12 | 31.37 | 0.01 |
| AID-00757 | 125.50 | 31.38 | 12.55 | Request new 18.83 | Reserve once | 94.12 | 31.38 | 0.00 |
| AID-00758 | 125.50 | 31.38 | 12.55 | Request new 18.84 | Exceeds remaining authority | 94.12 | 12.55 | 18.83 |
| AID-00759 | 125.50 | 31.38 | 12.55 | Request new 41.42 | Exceeds remaining authority | 94.12 | 12.55 | 18.83 |
| AID-00760 | 125.50 | 31.38 | 12.55 | Confirm pending 12.55 | Settle original once | 106.67 | 0.00 | 18.83 |
| AID-00761 | 125.50 | 31.38 | 12.55 | Fail pending 12.55 | Release pending reservation | 94.12 | 0.00 | 31.38 |
| AID-00762 | 125.50 | 31.38 | 12.55 | Replay settled 125.50 | Original receipt; no new effect | 94.12 | 12.55 | 18.83 |
| AID-00763 | 125.50 | 31.38 | 12.55 | Record return 0.01 | Apply linked return once | 94.11 | 12.55 | 18.84 |
| AID-00764 | 125.50 | 31.38 | 12.55 | Record return 47.06 | Apply linked return once | 47.06 | 12.55 | 65.89 |
| AID-00765 | 125.50 | 31.38 | 12.55 | Record return 94.12 | Apply linked return once | 0.00 | 12.55 | 112.95 |
| AID-00766 | 125.50 | 31.38 | 12.55 | Record return 94.13 | Return exceeds net fulfillment | 94.12 | 12.55 | 18.83 |
| AID-00767 | 125.50 | 31.38 | 31.38 | Request new 0.01 | Exceeds remaining authority | 94.12 | 31.38 | 0.00 |
| AID-00768 | 125.50 | 31.38 | 31.38 | Request new 41.42 | Exceeds remaining authority | 94.12 | 31.38 | 0.00 |
| AID-00769 | 125.50 | 31.38 | 31.38 | Confirm pending 31.38 | Settle original once | 125.50 | 0.00 | 0.00 |
| AID-00770 | 125.50 | 31.38 | 31.38 | Fail pending 31.38 | Release pending reservation | 94.12 | 0.00 | 31.38 |
| AID-00771 | 125.50 | 31.38 | 31.38 | Replay settled 125.50 | Original receipt; no new effect | 94.12 | 31.38 | 0.00 |
| AID-00772 | 125.50 | 31.38 | 31.38 | Record return 0.01 | Apply linked return once | 94.11 | 31.38 | 0.01 |
| AID-00773 | 125.50 | 31.38 | 31.38 | Record return 47.06 | Apply linked return once | 47.06 | 31.38 | 47.06 |
| AID-00774 | 125.50 | 31.38 | 31.38 | Record return 94.12 | Apply linked return once | 0.00 | 31.38 | 94.12 |
| AID-00775 | 125.50 | 31.38 | 31.38 | Record return 94.13 | Return exceeds net fulfillment | 94.12 | 31.38 | 0.00 |
| AID-00776 | 125.50 | 125.50 | 0.00 | Request new 41.42 | Reserve once | 0.00 | 41.42 | 84.08 |
| AID-00777 | 125.50 | 125.50 | 0.00 | Request new 125.49 | Reserve once | 0.00 | 125.49 | 0.01 |
| AID-00778 | 125.50 | 125.50 | 0.00 | Request new 125.50 | Reserve once | 0.00 | 125.50 | 0.00 |
| AID-00779 | 125.50 | 125.50 | 0.00 | Request new 125.51 | Exceeds remaining authority | 0.00 | 0.00 | 125.50 |
| AID-00780 | 125.50 | 125.50 | 0.00 | Replay settled 125.50 | Original receipt; no new effect | 0.00 | 0.00 | 125.50 |
| AID-00781 | 125.50 | 125.50 | 50.20 | Request new 41.42 | Reserve once | 0.00 | 91.62 | 33.88 |
| AID-00782 | 125.50 | 125.50 | 50.20 | Request new 75.29 | Reserve once | 0.00 | 125.49 | 0.01 |
| AID-00783 | 125.50 | 125.50 | 50.20 | Request new 75.30 | Reserve once | 0.00 | 125.50 | 0.00 |
| AID-00784 | 125.50 | 125.50 | 50.20 | Request new 75.31 | Exceeds remaining authority | 0.00 | 50.20 | 75.30 |
| AID-00785 | 125.50 | 125.50 | 50.20 | Confirm pending 50.20 | Settle original once | 50.20 | 0.00 | 75.30 |
| AID-00786 | 125.50 | 125.50 | 50.20 | Fail pending 50.20 | Release pending reservation | 0.00 | 0.00 | 125.50 |
| AID-00787 | 125.50 | 125.50 | 50.20 | Replay settled 125.50 | Original receipt; no new effect | 0.00 | 50.20 | 75.30 |
| AID-00788 | 125.50 | 125.50 | 125.50 | Request new 0.01 | Exceeds remaining authority | 0.00 | 125.50 | 0.00 |
| AID-00789 | 125.50 | 125.50 | 125.50 | Request new 41.42 | Exceeds remaining authority | 0.00 | 125.50 | 0.00 |
| AID-00790 | 125.50 | 125.50 | 125.50 | Confirm pending 125.50 | Settle original once | 125.50 | 0.00 | 0.00 |
| AID-00791 | 125.50 | 125.50 | 125.50 | Fail pending 125.50 | Release pending reservation | 0.00 | 0.00 | 125.50 |
| AID-00792 | 125.50 | 125.50 | 125.50 | Replay settled 125.50 | Original receipt; no new effect | 0.00 | 125.50 | 0.00 |
