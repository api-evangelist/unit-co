---
name: Issue and manage a debit card
description: Issue a debit card for a customer account, set per-card limits, and handle freeze / report-lost / replace lifecycle actions on Unit.
api: openapi/unit-cards-openapi.json
operations: [cards, card, cardLimits, freezeCard, unfreezeCard, reportLostCard, reportStolenCard, replaceCard, closeCard]
---

# Issue and manage a debit card

Use an **Org API token** or **Customer token** with `cards-write`. PCI-sensitive actions (reveal PAN/CVV, set PIN) require a **Customer token** with `cards-sensitive-write` and prior 2FA.

## Steps

1. **Issue the card** — `POST /cards` (`cards`) with an `individualDebitCard` (or virtual/business variant) whose `relationships.account` and `relationships.customer` point at the target account/customer.
2. **Set spending limits** — `PATCH /cards/{cardId}/limits` (`cardLimits`) to configure daily/monthly purchase and withdrawal limits.
3. **Lifecycle actions**:
   - Freeze / unfreeze: `POST /cards/{cardId}/freeze` (`freezeCard`) / `POST /cards/{cardId}/unfreeze` (`unfreezeCard`).
   - Report lost / stolen: `POST /cards/{cardId}/report-lost` (`reportLostCard`) / `POST /cards/{cardId}/report-stolen` (`reportStolenCard`).
   - Replace: `POST /cards/{cardId}/replace` (`replaceCard`); close: `POST /cards/{cardId}/close` (`closeCard`).
4. **Inspect** — `GET /cards/{cardId}` (`card`), optionally `?include=customer,account`.

## Rules
- **Idempotency**: physical and virtual debit-card creation **share** the idempotency key — sending the same key across both is intentional (see `conventions/unit-conventions.yml`).
- **Errors**: `not_supported_for_card_status`, `not_supported_for_card_type`, `forbidden` (missing scope / wrong token type) — `errors/unit-problem-types.yml`.
- For real-time authorization decisioning on this card, see the Authorization Requests API (`openapi/unit-authorizations-openapi.json`).
