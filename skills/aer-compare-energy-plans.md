---
name: Compare Australian retail energy plans
description: >-
  Pull current retail electricity and gas plans for one or more Australian retailer
  brands from the AER's Consumer Data Right product-data API and compare their tariffs,
  fees, discounts and eligibility. Anonymous — no key, no accreditation, no signup.
api: openapi/cdr-energy-api-openapi.json
base_url: https://cdr.energymadeeasy.gov.au/{brand}/cds-au/v1
operations:
- listEnergyPlans
- getEnergyPlanDetail
method: generated
generated: '2026-07-27'
---

# Compare Australian retail energy plans

The Australian Energy Regulator hosts the product-data layer for nearly the whole
Australian retail energy market: 79 of the 84 energy brands in the ACCC CDR Register
point their `productBaseUri` at `https://cdr.energymadeeasy.gov.au`. Everything below
is anonymous and read-only.

## Before you start

- **Resolve the brand.** The `{brand}` path segment is not optional and not guessable.
  Get it from the ACCC CDR Register, which is also anonymous:
  `GET https://api.cdr.gov.au/cdr-register/v1/energy/data-holders/brands/summary`
  with header `x-v: 1`, then read `productBaseUri` for the brand you want. An
  unrecognised brand does **not** 404 — it returns `200` with `meta.totalRecords: 0`,
  so a guess fails silently.
- **Send the version header.** `x-v` is mandatory. Omitting it is a `400`
  (`urn:au-cds:error:cds-all:Header/Missing`); a wrong value is a `406`
  (`urn:au-cds:error:cds-all:Header/UnsupportedVersion`).
- **There is no Australia-wide query.** One paged sweep per brand. Coverage is the six
  NECF jurisdictions only: TAS, VIC, SA, ACT, NSW, QLD. WA and NT are out of scope.

## Step 1 — list the plans for a brand (`listEnergyPlans`)

```
GET https://cdr.energymadeeasy.gov.au/{brand}/cds-au/v1/energy/plans?type=ALL&fuelType=ALL&page-size=1000
x-v: 1
```

- `type`: `STANDING` | `MARKET` | `REGULATED` | `ALL`
- `fuelType`: `ELECTRICITY` | `GAS` | `DUAL` | `ALL`
- `effective`: current plans only are served, whatever you pass — the AER does not
  expose future or historical plans.
- `updated-since`: use this for incremental refreshes instead of re-pulling everything.
- Paging: `page` (1-based) and `page-size` (default 25, **maximum 1000** — 1001 is a
  hard `400` `urn:au-cds:error:cds-all:Field/InvalidPageSize`). Read
  `meta.totalRecords` / `meta.totalPages` and follow `links.next`.

Each item gives you `planId`, `brand`, `brandName`, `fuelType`, `type`, `displayName`,
`customerType`, `effectiveFrom`, `lastUpdated` and `geography` (`distributors`,
`includedPostcodes`, optionally `excludedPostcodes`). Filter to the customer's
postcode with `geography.includedPostcodes` before fetching detail — that is what keeps
the next step from being thousands of calls.

## Step 2 — fetch the contract for each shortlisted plan (`getEnergyPlanDetail`)

```
GET https://cdr.energymadeeasy.gov.au/{brand}/cds-au/v1/energy/plans/{planId}
x-v: 3
```

**Version 3 is the only supported version** — version 2 was retired on 3 March 2025.
If you must tolerate future changes, send `x-v: 3` plus `x-min-v: 1` and read the `x-v`
response header to see what you were actually served.

The response body sits under `data` and carries `electricityContract` and/or
`gasContract` (mandatory for the matching `fuelType`), plus `meteringCharges`. Inside
the contract you get `tariffPeriod[]`, `controlledLoad[]`, `solarFeedInTariff[]`,
`discounts[]`, `incentives[]`, `fees[]`, `eligibility[]`, `greenPowerCharges[]`,
`pricingModel`, `isFixed`, `termType`, `billFrequency` and `coolingOffDays`.

## Step 3 — compare honestly

- Read `tariffPeriod[].rateBlockUType` first (`singleRate`, `timeOfUseRates`,
  `demandCharges`) — it tells you which rate object is populated. Do not assume a
  single rate.
- `dailySupplyCharge` applies to every plan; `dailySupplyChargeType: BAND` (with
  `bandedDailySupplyCharges`) shows up on selected Queensland plans.
- Absent optional fields mean **not offered**, not missing data. Controlled load is
  electricity-only and only applies where one is installed. Demand charges only apply
  to electricity customers with smart meters. Discounts and incentives are retailer
  discretion, with no rules governing how a discount is calculated.
- `discounts` are dollar or percentage amounts; `incentives` are things the customer
  receives. Do not add them together.
- Check `eligibility[]` before presenting a plan as available.

## Rules and etiquette

- Everything is `GET`. There is no write surface, no idempotency key and nothing to
  roll back.
- Throughput is governed by the CDS Non-Functional Requirements — 300 TPS total across
  all callers for public traffic, and `Retry-After` is CORS-exposed if you are
  throttled. Sweep politely; use `updated-since`.
- Keep the `x-fapi-interaction-id` response header for every call. It is the only
  correlation handle, and it is what to quote when mailing `cdr-support@aer.gov.au`.
- Before blaming your code for empty or failing responses, poll
  `GET /{brand}/cds-au/v1/discovery/status` with `x-v: 1`.
- Plan values are permanently fixed; a changed plan appears as a new `planId` or an
  incremented trailing digit. Cache by `planId` + `lastUpdated`.
