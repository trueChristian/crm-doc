# Allocate a promotion and compute the quoted tax

One basket has two separately taxable goods A and B, one tax component and one coupon shared in proportion to their pre-discount prices. Exact half cents in the discount allocation go to A. Both goods are eligible, with equal priority. All figures below are minor currency units. Set the rounding level before accepting the quote. In document mode, round the combined tax and then assign any residual by largest fractional remainder, ties to A.

Check discount conservation and the identity gross = A + B − coupon + tax A + tax B. The allocation oracle computes floors and residuals, and independently rounds the exact first share. Document tax is independently checked against the combined base multiplied by the rate.

For A 101 and B 99 with a coupon of 25, the exact shares are 12.625 and 12.375. Deduct 13 from A and 12 from B before calculating any tax. Returning A uses its frozen tax row.

[Worked manual](../../../handbook/commerce/quote-calculation.md) · [All decision suites](../README.md)

| Range | First input record | Last input record |
| --- | --- | --- |
| [1–240](cases-0001-0240.md) | 17 / 19 / 1 / 5 | 17 / 1062 / 25 / 10 |
| [241–480](cases-0241-0480.md) | 35 / 19 / 1 / 5 | 35 / 1062 / 25 / 10 |
| [481–720](cases-0481-0720.md) | 51 / 19 / 1 / 5 | 51 / 1062 / 25 / 10 |
| [721–960](cases-0721-0960.md) | 67 / 19 / 1 / 5 | 67 / 1062 / 25 / 10 |
| [961–1200](cases-0961-1200.md) | 99 / 19 / 1 / 5 | 99 / 1062 / 25 / 10 |
| [1201–1440](cases-1201-1440.md) | 101 / 19 / 1 / 5 | 101 / 1062 / 25 / 10 |
| [1441–1680](cases-1441-1680.md) | 149 / 19 / 1 / 5 | 149 / 1062 / 25 / 10 |
| [1681–1920](cases-1681-1920.md) | 199 / 19 / 1 / 5 | 199 / 1062 / 25 / 10 |
| [1921–2160](cases-1921-2160.md) | 251 / 19 / 1 / 5 | 251 / 1062 / 25 / 10 |
| [2161–2400](cases-2161-2400.md) | 499 / 19 / 1 / 5 | 499 / 1062 / 25 / 10 |
| [2401–2640](cases-2401-2640.md) | 1001 / 19 / 1 / 5 | 1001 / 1062 / 25 / 10 |
| [2641–2880](cases-2641-2880.md) | 2643 / 19 / 1 / 5 | 2643 / 1062 / 25 / 10 |
