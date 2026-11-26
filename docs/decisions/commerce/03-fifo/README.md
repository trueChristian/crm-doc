# Issue, return and revalue original FIFO cost layers

Two sellable, church-owned receipts at the same location form FIFO layers A (oldest) and B. All prices are minor units per book. Issue only after sufficient stock is present. Returned copies can be identified and follow reverse issue order back to their original cost layers. All returned copies pass inspection. No fees or revaluation. A shortage declines the entire issue and preserves inventory unchanged.

The operations calculation consumes layers by exhaustion. An independent oracle expands a physical sequence of unit costs, slices the exact issue, restores the tail and compares total issued, returned and ending asset value. Quantity and cost must conserve across the same movement identity.

With 2 A at 80, 4 B at 110, an issue of 3 costs 270. Returning the last unit restores 110 to B. Closing inventory is four B worth 440. A second return of that same unit must be rejected.

[Worked manual](../../../handbook/commerce/inventory-custody.md) · [All decision suites](../README.md)

| Range | First input record | Last input record |
| --- | --- | --- |
| [1–240](cases-0001-0240.md) | 1 / 2 / 31/45 / 1 | 1 / 4 / 145/145 / 4 |
| [241–480](cases-0241-0480.md) | 1 / 4 / 145/145 / 5 | 2 / 2 / 80/110 / 4 |
| [481–720](cases-0481-0720.md) | 2 / 2 / 80/110 / 4 | 2 / 4 / 110/80 / 5 |
| [721–960](cases-0721-0960.md) | 2 / 4 / 110/80 / 5 | 2 / 10 / 110/80 / 11 |
| [961–1200](cases-0961-1200.md) | 2 / 10 / 110/80 / 11 | 3 / 3 / 80/110 / 6 |
| [1201–1440](cases-1201-1440.md) | 3 / 3 / 80/110 / 6 | 3 / 7 / 31/45 / 4 |
| [1441–1680](cases-1441-1680.md) | 3 / 7 / 31/45 / 4 | 3 / 10 / 99/101 / 1 |
| [1681–1920](cases-1681-1920.md) | 3 / 10 / 99/101 / 2 | 5 / 3 / 45/31 / 8 |
| [1921–2160](cases-1921-2160.md) | 5 / 3 / 45/31 / 8 | 5 / 4 / 99/101 / 6 |
| [2161–2400](cases-2161-2400.md) | 5 / 4 / 99/101 / 6 | 5 / 10 / 45/31 / 1 |
| [2401–2640](cases-2401-2640.md) | 5 / 10 / 45/31 / 4 | 8 / 2 / 99/101 / 8 |
| [2641–2880](cases-2641-2880.md) | 8 / 2 / 99/101 / 8 | 8 / 4 / 45/31 / 8 |
| [2881–3120](cases-2881-3120.md) | 8 / 4 / 45/31 / 8 | 8 / 7 / 110/80 / 15 |
| [3121–3360](cases-3121-3360.md) | 8 / 7 / 110/80 / 15 | 13 / 2 / 31/45 / 13 |
| [3361–3600](cases-3361-3600.md) | 13 / 2 / 31/45 / 14 | 13 / 3 / 99/101 / 1 |
| [3601–3840](cases-3601-3840.md) | 13 / 3 / 99/101 / 12 | 13 / 7 / 31/45 / 19 |
| [3841–4080](cases-3841-4080.md) | 13 / 7 / 31/45 / 19 | 13 / 10 / 110/80 / 12 |
| [4081–4158](cases-4081-4158.md) | 13 / 10 / 110/80 / 12 | 13 / 10 / 145/145 / 24 |
