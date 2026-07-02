# Unit (unit-co)

Unit is a Banking-as-a-Service (BaaS) platform that lets companies embed deposit accounts, cards, payments, and lending into their own products without becoming a bank. A single REST API, built on the JSON:API specification (media type `application/vnd.api+json`) and secured with Bearer/JWT tokens, covers onboarding (Applications), Customers, Deposit and Credit Accounts, Debit and Credit Cards, real-time card Authorizations, Payments (Book, ACH, Wire, Recurring, Cash Deposits), Counterparties, Checks, Transactions, Statements, Tax Forms, Fees, Rewards, Credit and Repayments, and Events delivered as signed HTTP webhooks. Unit publishes an official OpenAPI 3.0.2 specification (github.com/unit-finance/openapi-unit-sdk) plus generated Node.js, Python, Ruby, and Java SDKs. Sandbox runs at `api.s.unit.sh`; production access is provisioned per signed BaaS agreement with Unit's partner banks.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/unit-co/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/unit-co/refs/heads/main/apis.yml)

## About JSON:API

Every Unit request and response uses the JSON:API convention: the primary resource is wrapped in a top-level `data` object with `type`, `id`, `attributes`, and `relationships`, list endpoints return `data` as an array plus a `meta.pagination` block, and the media type on both request and response is `application/vnd.api+json` rather than plain `application/json`. See [About JSON:API](https://www.unit.co/docs/api/about-jsonapi/).

## Tags

- FinTech
- BaaS
- Banking
- Payments
- Card Issuing
- ACH
- Lending
- JSON:API

## Timestamps

- **Created:** 2026-07-02
- **Modified:** 2026-07-02

## APIs

### Unit Applications API

Individual and business application onboarding - create, get, update, list, and cancel applications; manage application forms, uploaded KYC/KYB documents (front/back, verify, download), business beneficial owners, and surface an application's missing fields. An approved application creates a Customer resource.

- **Human URL:** [https://www.unit.co/docs/api/applications/](https://www.unit.co/docs/api/applications/)
- **Base URL:** `https://api.s.unit.sh`

#### Properties

- [Documentation](https://www.unit.co/docs/api/)
- [API Reference](https://www.unit.co/docs/api/applications/)
- [OpenAPI](openapi/unit-co-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/unit-co.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/unit-co.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Unit Customers API

Manage individual and business Customer resources created from approved applications - get, update, list, and archive customers, and add or remove authorized users who can transact on a customer's accounts and cards.

- **Human URL:** [https://www.unit.co/docs/api/customers/](https://www.unit.co/docs/api/customers/)
- **Base URL:** `https://api.s.unit.sh`

#### Properties

- [Documentation](https://www.unit.co/docs/api/customers/)
- [OpenAPI](openapi/unit-co-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/unit-co.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/unit-co.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Unit Accounts API

Create, get, update, list, freeze/unfreeze, close, and reopen deposit and credit accounts; manage Deposit Account Control Agreements (enter/activate/deactivate DACA); retrieve account limits, deposit products, end-of-day balance history, credit repayment information, and add or remove joint customers on an account.

- **Human URL:** [https://www.unit.co/docs/api/accounts/deposit-accounts/overview/](https://www.unit.co/docs/api/accounts/deposit-accounts/overview/)
- **Base URL:** `https://api.s.unit.sh`

#### Properties

- [Documentation](https://www.unit.co/docs/api/accounts/deposit-accounts/overview/)
- [API Reference](https://www.unit.co/docs/api/accounts/)
- [OpenAPI](openapi/unit-co-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/unit-co.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/unit-co.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Unit Cards API

Issue and manage individual and business debit and credit cards - create, get, update, list, freeze/unfreeze, close, replace, and check PIN status; report a card lost or stolen; retrieve card spending limits; and look up nearby surcharge-free ATM locations.

- **Human URL:** [https://www.unit.co/docs/api/cards/](https://www.unit.co/docs/api/cards/)
- **Base URL:** `https://api.s.unit.sh`

#### Properties

- [Documentation](https://www.unit.co/docs/api/cards/)
- [OpenAPI](openapi/unit-co-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/unit-co.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/unit-co.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Unit Card Authorizations API

List and retrieve completed card Authorization resources, and handle real-time Authorization Requests - Unit calls a configured webhook for every attempt to use a card so you can approve or decline it inline (with reasons such as InsufficientFunds, DoNotHonor, or RestrictedCard) before the transaction is authorized.

- **Human URL:** [https://docs.unit.co/cards-authorization-requests/](https://docs.unit.co/cards-authorization-requests/)
- **Base URL:** `https://api.s.unit.sh`

#### Properties

- [Documentation](https://docs.unit.co/cards-authorization-requests/)
- [API Reference](https://www.unit.co/docs/api/cards-authorizations/)
- [OpenAPI](openapi/unit-co-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/unit-co.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/unit-co.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Unit Payments API

Move money with Book Payments (instant internal transfers), ACH (originating debit/credit) and Wire payments, one-time and Recurring Payments, and retail Cash Deposits (barcode-based). Also manage incoming Received Payments - advance, reprocess, or return an ACH transaction - and cancel pending payments.

- **Human URL:** [https://www.unit.co/docs/api/payments/book/](https://www.unit.co/docs/api/payments/book/)
- **Base URL:** `https://api.s.unit.sh`

#### Properties

- [Documentation](https://docs.unit.co/payments/)
- [API Reference](https://www.unit.co/docs/api/payments/book/)
- [OpenAPI](openapi/unit-co-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/unit-co.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/unit-co.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Unit Counterparties API

Create, get, update, list, and delete Counterparty resources - external bank accounts (often verified via a Plaid processor token) that can send or receive ACH payments - and check a Plaid-verified counterparty's balance. Includes routing-number Institution lookups used to validate counterparties.

- **Human URL:** [https://www.unit.co/docs/api/counterparties/overview/](https://www.unit.co/docs/api/counterparties/overview/)
- **Base URL:** `https://api.s.unit.sh`

#### Properties

- [Documentation](https://www.unit.co/docs/api/counterparties/overview/)
- [API Reference](https://www.unit.co/docs/api/payments-counterparties/)
- [OpenAPI](openapi/unit-co-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/unit-co.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/unit-co.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Unit Checks API

Mobile Check Deposits - create, get, update, list, confirm, and retrieve front/back images of a deposited check - and outbound Check Payments (print-and-mail) - create, approve, cancel, return, and retrieve front/back images.

- **Human URL:** [https://docs.unit.co/check-deposits/](https://docs.unit.co/check-deposits/)
- **Base URL:** `https://api.s.unit.sh`

#### Properties

- [Documentation](https://docs.unit.co/check-deposits/)
- [API Reference](https://www.unit.co/docs/api/checks/)
- [OpenAPI](openapi/unit-co-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/unit-co.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/unit-co.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Unit Transactions API

Read-only ledger of confirmed, posted financial movements on an account - list transactions with filtering and paging, get a single transaction by account and transaction id, and update transaction tags. Transactions are final and are never created directly through the API.

- **Human URL:** [https://www.unit.co/docs/api/transactions/overview/](https://www.unit.co/docs/api/transactions/overview/)
- **Base URL:** `https://api.s.unit.sh`

#### Properties

- [Documentation](https://www.unit.co/docs/api/transactions/overview/)
- [API Reference](https://www.unit.co/docs/api/transactions/)
- [OpenAPI](openapi/unit-co-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/unit-co.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/unit-co.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Unit Statements and Tax Forms API

Retrieve auto-generated monthly account statements as HTML or PDF, plus bank-verification PDFs, for deposit and credit accounts; list and retrieve annual Tax Forms and their PDFs, with webhook events on creation and updates for electronic delivery consent workflows.

- **Human URL:** [https://docs.unit.co/statements/](https://docs.unit.co/statements/)
- **Base URL:** `https://api.s.unit.sh`

#### Properties

- [Documentation](https://docs.unit.co/statements/)
- [API Reference](https://www.unit.co/docs/api/statements/)
- [OpenAPI](openapi/unit-co-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/unit-co.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/unit-co.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Unit Events and Webhooks API

List and retrieve Event resources (resource.event-named, e.g. application.created, account.frozen, card.authorization) going back up to 90 days, and manage Webhook subscriptions - create, get, update, list, enable, and disable - that deliver those events as HMAC-signed HTTP POST callbacks to your endpoint.

- **Human URL:** [https://docs.unit.co/webhooks/](https://docs.unit.co/webhooks/)
- **Base URL:** `https://api.s.unit.sh`

#### Properties

- [Documentation](https://docs.unit.co/webhooks/)
- [API Reference](https://www.unit.co/docs/api/events/)
- [OpenAPI](openapi/unit-co-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/unit-co.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/unit-co.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Unit Risk and Fraud Prevention API

Create, list, get, and disable ACH/check Stop Payments; list and retrieve card transaction Disputes; and, through the dashboard-driven white-label Card Fraud Outreach flow, notify customers of suspected fraud and act on their response. Positive Pay check-matching rules are also configured under this surface.

- **Human URL:** [https://www.unit.co/docs/api/stop-payments/apis/](https://www.unit.co/docs/api/stop-payments/apis/)
- **Base URL:** `https://api.s.unit.sh`

#### Properties

- [Documentation](https://www.unit.co/docs/api/stop-payments/apis/)
- [API Reference](https://www.unit.co/docs/api/disputes/)
- [OpenAPI](openapi/unit-co-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/unit-co.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/unit-co.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Unit Credit and Repayments API

Manage repayments on Unit credit accounts and receivables - create, get, and list one-time Repayments; create, get, list, enable, and disable Recurring Repayments. Works alongside Credit Accounts (a deposit-account type) and Credit Applications for line-of-credit and charge card programs.

- **Human URL:** [https://docs.unit.co/repayments/](https://docs.unit.co/repayments/)
- **Base URL:** `https://api.s.unit.sh`

#### Properties

- [Documentation](https://docs.unit.co/repayments/)
- [API Reference](https://docs.unit.co/credit-accounts/)
- [OpenAPI](openapi/unit-co-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/unit-co.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/unit-co.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Unit Fees and Rewards API

Create and reverse one-off Fees against a customer's account for activities not covered by Unit's native fee schedule, and create and list Rewards (cashback-style credits) paid into a customer's account.

- **Human URL:** [https://www.unit.co/docs/api/fees/overview/](https://www.unit.co/docs/api/fees/overview/)
- **Base URL:** `https://api.s.unit.sh`

#### Properties

- [Documentation](https://www.unit.co/docs/api/fees/overview/)
- [API Reference](https://www.unit.co/docs/api/fees/)
- [OpenAPI](openapi/unit-co-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/unit-co.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/unit-co.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Unit API Tokens API

Issue and revoke org-level API tokens scoped to a Unit user, and create short-lived Customer API Tokens (plus SMS/email verification challenges) that let end users authenticate directly against Unit from a client application with reduced scope.

- **Human URL:** [https://www.unit.co/docs/tokens/](https://www.unit.co/docs/tokens/)
- **Base URL:** `https://api.s.unit.sh`

#### Properties

- [Documentation](https://www.unit.co/docs/tokens/)
- [API Reference](https://www.unit.co/docs/api/org-api-tokens/)
- [OpenAPI](openapi/unit-co-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/unit-co.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/unit-co.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [GitHub Organization](https://github.com/unit-finance)
- [LinkedIn](https://www.linkedin.com/company/unit-finance)
- [Website](https://www.unit.co/)
- [Documentation](https://www.unit.co/docs/api/)
- [Plans](plans/unit-co-plans-pricing.yml)
- [Rate Limits](rate-limits/unit-co-rate-limits.yml)
- [Fin Ops](finops/unit-co-finops.yml)

## Review

[review.yml](review.yml) answers a standing catalog question - does Unit expose a documented public WebSocket API? - **No.** Unit's own API is JSON:API-flavored REST over HTTPS; its realtime behavior (Events, real-time card Authorization Requests) is delivered as HMAC-signed HTTP POST callbacks to a subscriber-configured Webhook URL, not a persistent WebSocket connection. See review.yml for the full transport breakdown and the confirmed endpoint list.

## A Note on the OpenAPI Source

Unit officially publishes and maintains a real OpenAPI 3.0.2 specification at [github.com/unit-finance/openapi-unit-sdk](https://github.com/unit-finance/openapi-unit-sdk), used to generate its own [Node.js](https://github.com/unit-finance/unit-node-sdk), [Python](https://github.com/unit-finance/unit-python-sdk), Ruby, and Java SDKs. [openapi/unit-co-openapi.yml](openapi/unit-co-openapi.yml) in this repository was built from that upstream spec - all 117 paths were fetched and confirmed directly, then re-typed into a condensed JSON:API resource envelope for readability rather than reproduced schema-for-schema.

## A Note on This Network's Prior `unit` Entry

A thinner, earlier catalog entry for this same company already exists in this network under aid `unit` (two broad API groupings: a general REST API and Webhooks). This `unit-co` entry supersedes it in depth - 15 resource-scoped APIs backed by Unit's officially published OpenAPI spec - but the two have not been merged or deduplicated; both currently coexist in the catalog.

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
