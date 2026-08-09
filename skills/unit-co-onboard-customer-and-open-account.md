---
name: Onboard a customer and open a deposit account
description: Create an application, collect KYC/KYB documents, and open a deposit account for the approved customer on Unit.
api: openapi/unit-applications-openapi.json
operations: [applications, application, documents, uploadApplicationDocumentFile, listCustomers, customer, accounts, account]
---

# Onboard a customer and open a deposit account

Use an **Org API token** with `applications-write`, `customers`, and `accounts-write` scopes. All requests use the JSON:API media type `application/vnd.api+json` and `Authorization: Bearer <token>`.

## Steps

1. **Create the application** — `POST /applications` (`applications`). Send an `individualApplication` or `businessApplication` resource with the applicant's attributes. The customer's phone must be verified via OTP before submission (2FA); if you use Unit's application form component it handles this for you.
2. **Handle required documents** — if the application returns status `awaitingDocuments`, list requirements with `GET /applications/{applicationId}/documents` (`documents`) and upload each side with `POST /applications/{applicationId}/documents/{documentId}/multipart` (`uploadApplicationDocumentFile`).
3. **Poll for approval** — `GET /applications/{applicationId}` (`application`) until status is `Approved` (or subscribe to the `application.approved` webhook). Approval produces a Customer.
4. **Find the customer** — `GET /customers` (`listCustomers`) filtered by the application, or `GET /customers/{customerId}` (`customer`).
5. **Open the deposit account** — `POST /accounts` (`accounts`) with a `depositAccount` resource whose `relationships.customer` points at the customer and a valid `depositProduct`. Retrieve it with `GET /accounts/{accountId}` (`account`).

## Rules
- **Idempotency**: send an idempotency key (≤255 chars, UUID v4) on `POST /applications` and `POST /accounts`; keys are retained 48h. See `conventions/unit-conventions.yml`.
- **Errors**: JSON:API `errors[]` with `code`/`detail`/`meta.supportId`; watch for `invalid_value`, `already_exists`, `limits_exceeded` (`errors/unit-problem-types.yml`).
- Test the whole flow in Sandbox (`https://api.s.unit.sh`) and drive approve/deny outcomes via the application simulation endpoints.
