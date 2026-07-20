---
name: Read ING Australia account data via CDR consumer data sharing
description: As an Accredited Data Recipient, read an ING customer's accounts, balances and transactions through the authenticated Consumer Data Right (Open Banking) endpoints under the FAPI 1.0 Advanced security profile.
api: openapi/ing-australia-cds-banking-products-openapi.yml
operations: [listBankingAccounts, getBankingAccountDetail, getBankingBalance, listBankingTransactions, getBankingTransactionDetail]
auth: cdr-oauth2
---

# Read ING Australia account data (CDR consumer data sharing)

These endpoints are **authenticated** and only callable inside the CDR ecosystem as
an **Accredited Data Recipient (ADR)** with the customer's consent. You cannot call
them with a simple API key.

## Auth (see authentication/ and scopes/)
- Profile: **FAPI 1.0 Advanced (AU CDR)**. Discover endpoints at
  `https://id.ob.ing.com.au/.well-known/openid-configuration`.
- Flow: `authorization_code` with **PAR required** (`/par`), **PKCE S256**,
  request objects signed **PS256**, client auth **private_key_jwt**, and
  **certificate-bound access tokens over mTLS** (RFC 8705).
- Request the scopes you need (see `scopes/ing-australia-scopes.yml`), e.g.
  `bank:accounts.basic:read`, `bank:transactions:read`.
- On every resource call send `x-v` (endpoint version) plus the FAPI headers
  `x-fapi-auth-date`, `x-fapi-interaction-id` (RFC 4122 UUID), and, when the
  customer is present, `x-fapi-customer-ip-address` + `x-cds-client-headers`.

## Steps
1. **List accounts** — `GET /banking/accounts` (`listBankingAccounts`,
   scope `bank:accounts.basic:read`). Filter with `product-category`,
   `open-status`, `is-owned`; page with `page`/`page-size`.
2. **(Optional) account detail** — `GET /banking/accounts/{accountId}`
   (`getBankingAccountDetail`, scope `bank:accounts.detail:read`).
3. **Balance** — `GET /banking/accounts/{accountId}/balance` (`getBankingBalance`).
4. **Transactions** — `GET /banking/accounts/{accountId}/transactions`
   (`listBankingTransactions`, scope `bank:transactions:read`). Filter with
   `oldest-time`/`newest-time` (defaults to newest-time minus 90 days),
   `min-amount`/`max-amount`, `text`.
5. **Transaction detail** — `GET /banking/accounts/{accountId}/transactions/{transactionId}`
   (`getBankingTransactionDetail`).

## Conventions & errors
Pagination, versioning and the error envelope are documented in
`conventions/ing-australia-conventions.yml` and
`errors/ing-australia-problem-types.yml`. Authorisation failures surface as
`404`/`422 Authorisation/UnavailableBankingAccount` or `.../InvalidBankingAccount`.
