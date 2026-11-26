# Motion majorities and denominator choices

[All decision profiles](../README.md) · [Clerk procedure](../../../handbook/governance/motions-and-weights.md)

Each electorate has a certified quorum. These cases concern the motion threshold after quorum was established. The same numerical poll can have different outcomes under distinct charter editions. Test the exact denominator and the smallest passing affirmative count.

## Reproduce the cases

1. Compute decisive weight as yes plus no; cast weight also includes abstentions. Eligible rights also include absences. Reconcile all categories to seats.
2. For an inclusive fraction p/q use the smallest integer y such that y × q ≥ p × denominator. For strict majority require y × 2 > denominator.
3. Independently sum the five attendance/choice quantities according to the profile, test the integer cross-product, and compare the arithmetic yes/no tie flag. Equality of affirmative and negative votes can differ from the decision threshold.

## Profile pages

| Profile | Cases | Case ranges |
| --- | ---: | --- |
| Strict majority of decisive votes | 840 | [1–325](simple-01.md), [326–650](simple-02.md), [651–840](simple-03.md) |
| Two-thirds of decisive votes | 840 | [1–325](super-01.md), [326–650](super-02.md), [651–840](super-03.md) |
| Three-fifths including abstentions | 840 | [1–325](cast-01.md), [326–650](cast-02.md), [651–840](cast-03.md) |
| Three-quarters of eligible rights | 840 | [1–325](eligible-01.md), [326–650](eligible-02.md), [651–840](eligible-03.md) |
| All abstain or no cast ballots, with two sole-decisive controls | 8 | [1–8](zero-denominators.md) |
