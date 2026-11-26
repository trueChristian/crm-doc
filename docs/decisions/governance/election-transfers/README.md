# Auditable preferential ballot transfers and unresolved final seats

[All decision profiles](../README.md) · [Clerk procedure](../../../handbook/governance/election-control.md)

The rows test two explicit single-seat procedures from an already reconciled first count. An exhausted paper in the frozen-denominator profile can prevent election even when one remaining candidate leads.

## Reproduce the cases

1. Verify the initial three totals, that C is uniquely lowest and that no candidate reached the initial majority. Transfer every C paper exactly once.
2. Calculate final A and B; add the exhausted papers and check exact equality to the original total. Select the denominator named in the profile.
3. Find the smallest whole count strictly above half; test each finalist against it before checking a tie or other unfilled seat. Never use display rounding to break the tie.

## Profile pages

| Profile | Cases | Case ranges |
| --- | ---: | --- |
| Ranked runoff on continuing votes | 815 | [1–325](continuing-01.md), [326–650](continuing-02.md), [651–815](continuing-03.md) |
| Ranked runoff on original valid papers | 815 | [1–325](original-01.md), [326–650](original-02.md), [651–815](original-03.md) |
