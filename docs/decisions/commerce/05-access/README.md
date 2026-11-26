# Evaluate rental and rights boundaries for a named viewer

Times below are integer hours from a fixture epoch, with half-open intervals. A claimed rental already began at first successful playback. A named viewer asks for a specific use. Both the rental interval and the matching licensed-use window must cover the request. A controlled withdrawal can end rights earlier. The test deliberately probes only effective boundaries, their neighbouring hours, and each component boundary where a different reason can apply. A denial exposes no private title to an outside viewer.

First evaluate publication and rights. The right opens at its start, closes at the earlier rights end/withdrawal and is checked before beneficiary grant timing. Then test grant start/end. An independent set-intersection oracle constructs the permitted integer hour set from both intervals. Confirm the status for each probe and the last permitted hour when one exists.

Rental [12,60), rights [0,72), withdrawal at 48 gives allowed hours 12 through 47. At 48 return rights-closed regardless of a valid remaining rental. A fresh rental starting at hour 60 cannot reopen these rights.

[Worked manual](../../../handbook/commerce/publication-and-withdrawal.md) · [All decision suites](../README.md)

| Range | First input record | Last input record |
| --- | --- | --- |
| [1–240](cases-0001-0240.md) | 0 / 6 / 0/24 / 12 | 0 / 24 / 0/48 / 24 |
| [241–480](cases-0241-0480.md) | 0 / 24 / 0/48 / 24 | 0 / 48 / 6/36 / 21 |
| [481–720](cases-0481-0720.md) | 0 / 48 / 6/36 / 21 | 6 / 12 / 0/48 / none |
| [721–960](cases-0721-0960.md) | 6 / 12 / 0/48 / none | 6 / 36 / 0/24 / none |
| [961–1200](cases-0961-1200.md) | 6 / 36 / 0/24 / none | 6 / 48 / 48/96 / 72 |
| [1201–1440](cases-1201-1440.md) | 6 / 48 / 48/96 / 72 | 12 / 12 / 24/72 / none |
| [1441–1680](cases-1441-1680.md) | 12 / 12 / 24/72 / none | 12 / 36 / 24/72 / 48 |
| [1681–1920](cases-1681-1920.md) | 12 / 36 / 24/72 / none | 18 / 6 / 12/60 / none |
| [1921–2160](cases-1921-2160.md) | 18 / 6 / 12/60 / none | 18 / 24 / 6/36 / 21 |
| [2161–2400](cases-2161-2400.md) | 18 / 24 / 6/36 / 21 | 18 / 48 / 0/24 / none |
| [2401–2640](cases-2401-2640.md) | 18 / 48 / 0/24 / none | 24 / 6 / 48/96 / 72 |
| [2641–2880](cases-2641-2880.md) | 24 / 6 / 48/96 / 72 | 24 / 24 / 48/96 / 72 |
| [2881–3120](cases-2881-3120.md) | 24 / 24 / 48/96 / 72 | 24 / 48 / 48/96 / 72 |
| [3121–3360](cases-3121-3360.md) | 24 / 48 / 48/96 / 72 | 36 / 12 / 24/72 / 48 |
| [3361–3600](cases-3361-3600.md) | 36 / 12 / 24/72 / 48 | 36 / 36 / 12/60 / 36 |
| [3601–3840](cases-3601-3840.md) | 36 / 36 / 12/60 / none | 48 / 6 / 6/36 / 21 |
| [3841–4080](cases-3841-4080.md) | 48 / 6 / 6/36 / 21 | 48 / 24 / 0/48 / none |
| [4081–4320](cases-4081-4320.md) | 48 / 24 / 0/48 / none | 48 / 48 / 0/48 / 24 |
| [4321–4416](cases-4321-4416.md) | 48 / 48 / 0/48 / 24 | 48 / 48 / 48/96 / none |
