# Reconciling out-of-order callbacks, duplicate events and publication counts

[All decision profiles](../README.md) · [Clerk procedure](../../../handbook/governance/delivery-incident-desk.md)

The event tokens encode different evidence about the same submitted route. Reconciliation returns factual delivery and future-route permission as separate results. These cases assume a documented adapter with the exact meanings on its page; transport acceptance alone is never identity-level delivery.

## Reproduce the cases

1. Read five events at minute intervals in the listed arrival order. Repeated provider event identity contributes to duplicate count only. A wrong-sender observation goes into quarantine (Q), leaving the effective delivery state unchanged.
2. After each other event show p pending, u unknown, a accepted, d delivered, f failed, r conflicting final evidence, or s posted. A late timeout cannot override provider evidence. A subsequent unsubscribe or lost post permission updates future routing independently.
3. On a person route count one only for an uncontradicted final delivered observation in this fixture. On the publication route count zero individual receipts even if a view aggregate exists. A permission failure affecting future posts does not undo an earlier confirmed publication.

## Profile pages

| Profile | Cases | Case ranges |
| --- | ---: | --- |
| SMS delivery and unknown handoff reconciliation | 610 | [1–325](sms-01.md), [326–610](sms-02.md) |
| Email bounce and unsubscribe evidence | 610 | [1–325](email-01.md), [326–610](email-02.md) |
| Telegram channel acceptance and permission changes | 610 | [1–325](channel-01.md), [326–610](channel-02.md) |
