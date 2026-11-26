# Meal credits — part 2 of 2

[Policy and other cases](README.md)

One approved award of 60 credits; all inputs use credits at 0 decimal places. One original settled fulfillment, when present, may be partially returned. An outstanding payment or stock issue is reserved against authority. Historical issued and returned amounts are kept even when the net amount is zero. Reviewers can reconstruct this case using the supplied opening facts.

| Case | Opening gross | Opening returns | Opening reserved | Requested event and value | Decision | New net delivered | New reserved | New free authority |
|---|---|---|---|---|---|---|---|---|
| AID-03849 | 48 | 48 | 60 | Request new 1 | Exceeds remaining authority | 0 | 60 | 0 |
| AID-03850 | 48 | 48 | 60 | Request new 20 | Exceeds remaining authority | 0 | 60 | 0 |
| AID-03851 | 48 | 48 | 60 | Confirm pending 60 | Settle original once | 60 | 0 | 0 |
| AID-03852 | 48 | 48 | 60 | Fail pending 60 | Release pending reservation | 0 | 0 | 60 |
| AID-03853 | 48 | 48 | 60 | Replay settled 48 | Original receipt; no new effect | 0 | 60 | 0 |
| AID-03854 | 60 | 0 | 0 | Request new 1 | Exceeds remaining authority | 60 | 0 | 0 |
| AID-03855 | 60 | 0 | 0 | Request new 20 | Exceeds remaining authority | 60 | 0 | 0 |
| AID-03856 | 60 | 0 | 0 | Replay settled 60 | Original receipt; no new effect | 60 | 0 | 0 |
| AID-03857 | 60 | 0 | 0 | Record return 1 | Apply linked return once | 59 | 0 | 1 |
| AID-03858 | 60 | 0 | 0 | Record return 30 | Apply linked return once | 30 | 0 | 30 |
| AID-03859 | 60 | 0 | 0 | Record return 60 | Apply linked return once | 0 | 0 | 60 |
| AID-03860 | 60 | 0 | 0 | Record return 61 | Return exceeds net fulfillment | 60 | 0 | 0 |
| AID-03861 | 60 | 1 | 0 | Request new 1 | Reserve once | 59 | 1 | 0 |
| AID-03862 | 60 | 1 | 0 | Request new 2 | Exceeds remaining authority | 59 | 0 | 1 |
| AID-03863 | 60 | 1 | 0 | Request new 20 | Exceeds remaining authority | 59 | 0 | 1 |
| AID-03864 | 60 | 1 | 0 | Replay settled 60 | Original receipt; no new effect | 59 | 0 | 1 |
| AID-03865 | 60 | 1 | 0 | Record return 1 | Apply linked return once | 58 | 0 | 2 |
| AID-03866 | 60 | 1 | 0 | Record return 30 | Apply linked return once | 29 | 0 | 31 |
| AID-03867 | 60 | 1 | 0 | Record return 59 | Apply linked return once | 0 | 0 | 60 |
| AID-03868 | 60 | 1 | 0 | Record return 60 | Return exceeds net fulfillment | 59 | 0 | 1 |
| AID-03869 | 60 | 1 | 1 | Request new 1 | Exceeds remaining authority | 59 | 1 | 0 |
| AID-03870 | 60 | 1 | 1 | Request new 20 | Exceeds remaining authority | 59 | 1 | 0 |
| AID-03871 | 60 | 1 | 1 | Confirm pending 1 | Settle original once | 60 | 0 | 0 |
| AID-03872 | 60 | 1 | 1 | Fail pending 1 | Release pending reservation | 59 | 0 | 1 |
| AID-03873 | 60 | 1 | 1 | Replay settled 60 | Original receipt; no new effect | 59 | 1 | 0 |
| AID-03874 | 60 | 1 | 1 | Record return 1 | Apply linked return once | 58 | 1 | 1 |
| AID-03875 | 60 | 1 | 1 | Record return 30 | Apply linked return once | 29 | 1 | 30 |
| AID-03876 | 60 | 1 | 1 | Record return 59 | Apply linked return once | 0 | 1 | 59 |
| AID-03877 | 60 | 1 | 1 | Record return 60 | Return exceeds net fulfillment | 59 | 1 | 0 |
| AID-03878 | 60 | 15 | 0 | Request new 14 | Reserve once | 45 | 14 | 1 |
| AID-03879 | 60 | 15 | 0 | Request new 15 | Reserve once | 45 | 15 | 0 |
| AID-03880 | 60 | 15 | 0 | Request new 16 | Exceeds remaining authority | 45 | 0 | 15 |
| AID-03881 | 60 | 15 | 0 | Request new 20 | Exceeds remaining authority | 45 | 0 | 15 |
| AID-03882 | 60 | 15 | 0 | Replay settled 60 | Original receipt; no new effect | 45 | 0 | 15 |
| AID-03883 | 60 | 15 | 0 | Record return 1 | Apply linked return once | 44 | 0 | 16 |
| AID-03884 | 60 | 15 | 0 | Record return 23 | Apply linked return once | 22 | 0 | 38 |
| AID-03885 | 60 | 15 | 0 | Record return 45 | Apply linked return once | 0 | 0 | 60 |
| AID-03886 | 60 | 15 | 0 | Record return 46 | Return exceeds net fulfillment | 45 | 0 | 15 |
| AID-03887 | 60 | 15 | 6 | Request new 8 | Reserve once | 45 | 14 | 1 |
| AID-03888 | 60 | 15 | 6 | Request new 9 | Reserve once | 45 | 15 | 0 |
| AID-03889 | 60 | 15 | 6 | Request new 10 | Exceeds remaining authority | 45 | 6 | 9 |
| AID-03890 | 60 | 15 | 6 | Request new 20 | Exceeds remaining authority | 45 | 6 | 9 |
| AID-03891 | 60 | 15 | 6 | Confirm pending 6 | Settle original once | 51 | 0 | 9 |
| AID-03892 | 60 | 15 | 6 | Fail pending 6 | Release pending reservation | 45 | 0 | 15 |
| AID-03893 | 60 | 15 | 6 | Replay settled 60 | Original receipt; no new effect | 45 | 6 | 9 |
| AID-03894 | 60 | 15 | 6 | Record return 1 | Apply linked return once | 44 | 6 | 10 |
| AID-03895 | 60 | 15 | 6 | Record return 23 | Apply linked return once | 22 | 6 | 32 |
| AID-03896 | 60 | 15 | 6 | Record return 45 | Apply linked return once | 0 | 6 | 54 |
| AID-03897 | 60 | 15 | 6 | Record return 46 | Return exceeds net fulfillment | 45 | 6 | 9 |
| AID-03898 | 60 | 15 | 15 | Request new 1 | Exceeds remaining authority | 45 | 15 | 0 |
| AID-03899 | 60 | 15 | 15 | Request new 20 | Exceeds remaining authority | 45 | 15 | 0 |
| AID-03900 | 60 | 15 | 15 | Confirm pending 15 | Settle original once | 60 | 0 | 0 |
| AID-03901 | 60 | 15 | 15 | Fail pending 15 | Release pending reservation | 45 | 0 | 15 |
| AID-03902 | 60 | 15 | 15 | Replay settled 60 | Original receipt; no new effect | 45 | 15 | 0 |
| AID-03903 | 60 | 15 | 15 | Record return 1 | Apply linked return once | 44 | 15 | 1 |
| AID-03904 | 60 | 15 | 15 | Record return 23 | Apply linked return once | 22 | 15 | 23 |
| AID-03905 | 60 | 15 | 15 | Record return 45 | Apply linked return once | 0 | 15 | 45 |
| AID-03906 | 60 | 15 | 15 | Record return 46 | Return exceeds net fulfillment | 45 | 15 | 0 |
| AID-03907 | 60 | 60 | 0 | Request new 20 | Reserve once | 0 | 20 | 40 |
| AID-03908 | 60 | 60 | 0 | Request new 59 | Reserve once | 0 | 59 | 1 |
| AID-03909 | 60 | 60 | 0 | Request new 60 | Reserve once | 0 | 60 | 0 |
| AID-03910 | 60 | 60 | 0 | Request new 61 | Exceeds remaining authority | 0 | 0 | 60 |
| AID-03911 | 60 | 60 | 0 | Replay settled 60 | Original receipt; no new effect | 0 | 0 | 60 |
| AID-03912 | 60 | 60 | 24 | Request new 20 | Reserve once | 0 | 44 | 16 |
| AID-03913 | 60 | 60 | 24 | Request new 35 | Reserve once | 0 | 59 | 1 |
| AID-03914 | 60 | 60 | 24 | Request new 36 | Reserve once | 0 | 60 | 0 |
| AID-03915 | 60 | 60 | 24 | Request new 37 | Exceeds remaining authority | 0 | 24 | 36 |
| AID-03916 | 60 | 60 | 24 | Confirm pending 24 | Settle original once | 24 | 0 | 36 |
| AID-03917 | 60 | 60 | 24 | Fail pending 24 | Release pending reservation | 0 | 0 | 60 |
| AID-03918 | 60 | 60 | 24 | Replay settled 60 | Original receipt; no new effect | 0 | 24 | 36 |
| AID-03919 | 60 | 60 | 60 | Request new 1 | Exceeds remaining authority | 0 | 60 | 0 |
| AID-03920 | 60 | 60 | 60 | Request new 20 | Exceeds remaining authority | 0 | 60 | 0 |
| AID-03921 | 60 | 60 | 60 | Confirm pending 60 | Settle original once | 60 | 0 | 0 |
| AID-03922 | 60 | 60 | 60 | Fail pending 60 | Release pending reservation | 0 | 0 | 60 |
| AID-03923 | 60 | 60 | 60 | Replay settled 60 | Original receipt; no new effect | 0 | 60 | 0 |
