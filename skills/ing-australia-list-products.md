---
name: List ING Australia banking products (public CDR PRD)
description: Retrieve ING Australia's publicly offered banking products and their full detail through the unauthenticated Consumer Data Right Product Reference Data endpoints. No credentials required.
api: openapi/ing-australia-cds-banking-products-openapi.yml
operations: [listBankingProducts, getBankingProductDetail]
auth: none
---

# List ING Australia banking products

ING's Product Reference Data (PRD) endpoints are **public and unauthenticated** —
part of Australia's Consumer Data Right. Base URL:
`https://id.ob.ing.com.au/cds-au/v1`.

## Rules
- Send the mandatory `x-v` header set to the endpoint version you want (start with
  `x-v: 5` for `listBankingProducts`, `x-v: 7` for `getBankingProductDetail`).
  Optionally send `x-min-v`. If the version is unsupported you get `406`
  (`urn:au-cds:error:cds-all:Header/UnsupportedVersion`).
- Do **not** send the `x-fapi-*` headers — those are for authenticated calls only.
- Pagination is offset-based: `page` (default 1) and `page-size` (default 25); read
  `links` and `meta.totalPages` from the response.

## Steps
1. **List products** — `GET /banking/products` (`listBankingProducts`).
   - Optional filters: `effective` (CURRENT/FUTURE/ALL), `updated-since`
     (DateTimeString), `brand`, `product-category`.
   - Results are ordered by `lastUpdated` descending; page through via `page`.
2. **Pick a productId** from `data.products[].productId`.
3. **Get product detail** — `GET /banking/products/{productId}`
   (`getBankingProductDetail`) with `x-v: 7` to retrieve fees, rates, eligibility,
   features and constraints.

## Errors
See `errors/ing-australia-problem-types.yml`. Common: `400 Field/Invalid`,
`404 Resource/Invalid` (bad productId), `406 Header/UnsupportedVersion`.
