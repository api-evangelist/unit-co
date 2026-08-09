---
name: Originate an ACH payment
description: Create a counterparty and originate an ACH credit or debit payment from a Unit deposit account, safely retried with an idempotency key.
api: openapi/unit-payments-openapi.json
operations: [counterparties, getInstitution, getAndCreatePayments, getAndUpdatePayment, cancelPayment]
---

# Originate an ACH payment

Use an **Org API token** or a **Customer token** carrying `counterparties-write` and `ach-payments-write` (a sensitive, fund-movement scope — requires 2FA within the prior 24h; a Customer token handles the OTP for you).

## Steps

1. **(Optional) Validate routing** — `GET /institutions/{routingNumber}` (`getInstitution`) to confirm the destination bank.
2. **Create the counterparty** — `POST /counterparties` (`counterparties`) with the external account/routing number and name. Reuse existing counterparties where possible.
3. **Originate the payment** — `POST /payments` (`getAndCreatePayments`) with an `achPayment` resource: `relationships.account` (the source deposit account), `relationships.counterparty`, `amount`, `direction` (`Credit`/`Debit`), and `description`.
4. **Track status** — `GET /payments/{paymentId}` (`getAndUpdatePayment`), or subscribe to `payment.created` → `payment.clearing` → `payment.sent`/`payment.returned` webhooks. Cancel a pending payment with `POST /payments/{paymentId}/cancel` (`cancelPayment`).

## Rules
- **Idempotency (critical)**: always send an idempotency key on `POST /payments`; on a network failure retry with the **same** key so the payment occurs at most once (48h retention).
- **Retries**: retry only 408/429/5xx with exponential backoff + jitter.
- **Returns**: a returned ACH fires `payment.returned` and posts an offsetting transaction; reason codes R01–R85 are catalogued in `errors/unit-ach-return-codes.yml`.
- **Errors**: `insufficient_funds`, `limits_exceeded`, `payment_invalid` (`errors/unit-problem-types.yml`).
