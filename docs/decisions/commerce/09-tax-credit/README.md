# Credit multi-component tax by returned unit

Identical units are taxed with two components rounded half up at the line level. Component B is either independent on net or compounded on net plus the rounded A amount. Both components are apportioned across individual units separately: equal bases get equal shares with residual minor units assigned to ascending unit ordinal. Return the first named count of units. Each component can credit at most its original allocation. Shipping and gifts are absent.

Allocate component tax using quotient and remainder by unit. An independent exact rational oracle builds per-unit floor/remainder shares and sums the selected units, then checks credited and remaining totals, including full return. Historical component allocations are immutable even if current rates change.

Three units at 5 with A at 10% create A of 2. The first two units carry one A cent each and the third zero. Crediting the third alone means zero A; the fixture returns the first units. Which ordinal was returned matters.

[Worked manual](../../../handbook/commerce/quote-calculation.md) · [All decision suites](../README.md)

| Range | First input record | Last input record |
| --- | --- | --- |
| [1–240](cases-0001-0240.md) | 5 / 2 / 5/5 / net | 9 / 5 / 20/7 / net+A |
| [241–480](cases-0241-0480.md) | 9 / 7 / 5/5 / net | 33 / 4 / 20/7 / net+A |
| [481–720](cases-0481-0720.md) | 33 / 5 / 5/5 / net | 99 / 3 / 20/7 / net+A |
| [721–960](cases-0721-0960.md) | 99 / 4 / 5/5 / net | 129 / 2 / 10/5 / net+A |
| [961–1200](cases-0961-1200.md) | 129 / 2 / 15/3 / net | 251 / 7 / 5/5 / net+A |
| [1201–1440](cases-1201-1440.md) | 251 / 7 / 10/5 / net | 1001 / 5 / 5/5 / net+A |
| [1441–1496](cases-1441-1496.md) | 1001 / 5 / 10/5 / net | 1001 / 7 / 20/7 / net+A |
