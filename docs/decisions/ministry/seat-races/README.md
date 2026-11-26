# Which request owns the last available places?

H holds places and has one payment callback. A and B are independently bookable parties. X is the hold-expiry boundary; C is the verified capture. Letters run in the displayed committed order.

A/B take their whole request if sufficient unclaimed seats exist, otherwise they wait. C before X converts H’s original reservation. C after X reacquires sufficient free seats or records a paid, unfulfilled unit for remedy. X after a conversion has no effect. A repeated callback is keyed to the same H capture and returns the initial outcome.

The two ledgers used for checking are independent: one tracks quantities and one marks individually enumerated seats through the ordered commands. Final inventory and successful holder identities must agree. Waiting positions never count as held. No automatic payment refund is assumed.

[Ministry decisions](../README.md) · [Implementation manual](../../../handbook/ministry/admission.md)

| Open cases | Decision outcomes in this group | Cases |
| --- | --- | ---: |
| [Set 1](01.md) | converted hold; 0 bookings | 260 |
| [Set 2](02.md) | converted hold; 0 bookings · converted hold; 1 bookings | 260 |
| [Set 3](03.md) | converted hold; 1 bookings | 260 |
| [Set 4](04.md) | converted hold; 1 bookings · converted hold; 2 bookings | 260 |
| [Set 5](05.md) | converted hold; 2 bookings · paid; remedy due; 1 bookings | 260 |
| [Set 6](06.md) | paid; remedy due; 1 bookings · paid; remedy due; 2 bookings | 260 |
| [Set 7](07.md) | paid; remedy due; 2 bookings · reacquired; 0 bookings | 260 |
| [Set 8](08.md) | reacquired; 0 bookings | 260 |
| [Set 9](09.md) | reacquired; 0 bookings · reacquired; 1 bookings | 260 |
| [Set 10](10.md) | reacquired; 1 bookings · reacquired; 2 bookings | 260 |
| [Set 11](11.md) | reacquired; 2 bookings | 100 |
