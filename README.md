# ING Australia (ing-australia)

ING Australia is the retail banking division of ING Bank (Australia) Limited (ABN 24 000 893 292), a wholly owned subsidiary of the Dutch multinational ING Groep N.V. headquartered in Amsterdam. Launched in 1999 as ING Direct and rebranded to ING in 2017, it is a branchless, digital-first direct bank offering everyday transaction and savings accounts, home loans, superannuation, and insurance to Australian consumers. It is a foreign-owned Authorised Deposit-taking Institution (ADI) — not a customer-owned mutual — regulated by APRA and ASIC, and an accredited data holder under Australia's Consumer Data Right (CDR / Open Banking).

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/ing-australia/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/ing-australia/refs/heads/main/apis.yml)

## Tags

- Financial
- Banks
- Open Banking
- CDR
- Consumer Banking
- Australia
- Product Reference Data
- ADI

## Timestamps

- **Created:** 2026-07-20
- **Modified:** 2026-07-20

## APIs

### ING Australia CDR Product Reference Data API

Public, unauthenticated Product Reference Data (PRD) API mandated under Australia's Consumer Data Right. Exposes `GET /banking/products` (a paginated list of ING's publicly offered banking products) and `GET /banking/products/{productId}` (full product detail) under the Consumer Data Standards (CDS) path `/cds-au/v1`. Responses are versioned via the `x-v` request/response header. The base URI is ING Bank (Australia) Ltd's registered CDR `publicBaseUri` per the CDR Register.

- **Human URL:** [https://www.ing.com.au/](https://www.ing.com.au/)
- **Base URL:** `https://id.ob.ing.com.au/cds-au/v1`

#### Tags

- CDR
- Open Banking
- Product Reference Data
- Banking
- Consumer Data Standards

#### Properties

- [Documentation](https://www.ing.com.au/pdf/CDR-policy.pdf)
- [API Reference](https://consumerdatastandardsaustralia.github.io/standards/#product-reference-data-apis)
- [OpenAPI](openapi/ing-australia-cds-banking-products-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

## Common Properties

- [Website](https://www.ing.com.au/)
- [Documentation](https://www.ing.com.au/pdf/CDR-policy.pdf)
- [API Reference](https://consumerdatastandardsaustralia.github.io/standards/)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
