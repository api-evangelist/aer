---
name: Sweep the national retail energy plan catalogue
description: >-
  Build a complete, refreshable national picture of Australian retail energy plans by
  enumerating every energy data-holder brand from the ACCC CDR Register and paging the
  AER's product-data endpoint for each one — including the operational checks that keep
  a sweep honest.
api: openapi/cdr-energy-api-openapi.json
base_url: https://cdr.energymadeeasy.gov.au/{brand}/cds-au/v1
operations:
- listEnergyPlans
- getEnergyPlanDetail
- getStatus
- getOutages
method: generated
generated: '2026-07-27'
---

# Sweep the national retail energy plan catalogue

There is no Australia-wide query. The AER says so in its own FAQ, and says the
per-retailer restriction is under review. Until it changes, "national" means a loop.

## Step 1 — enumerate the brands

The AER publishes its base-URI list as a **document**, and its FAQ confirms a JSON
retailer list does not exist yet ("Currently no, but we are working on providing this in
JSON format"). So enumerate from the ACCC's register instead — anonymous, machine
readable, and the authoritative source of `productBaseUri`:

```
GET https://api.cdr.gov.au/cdr-register/v1/energy/data-holders/brands/summary
x-v: 1
```

As of 2026-07-27 it returned 84 energy brands. **79 carry a `productBaseUri` on
`https://cdr.energymadeeasy.gov.au`** — those are the AER-hosted ones. One brand
self-hosts (Cooperative Power) and four carry no `productBaseUri` at all. Do not
hard-code the split; re-read the register each run, and treat the host in
`productBaseUri` as authoritative rather than assuming the AER.

## Step 2 — check the surface is up (`getStatus`, `getOutages`)

```
GET https://cdr.energymadeeasy.gov.au/{brand}/cds-au/v1/discovery/status     # x-v: 1
GET https://cdr.energymadeeasy.gov.au/{brand}/cds-au/v1/discovery/outages    # x-v: 1
```

`status` returns `data.status` (`OK` and friends) with an `updateTime`; `outages`
returns `data.outages[]`. This is the AER's status page — there is no HTML one. Both
endpoints are brand-scoped: the unbranded `/cds-au/v1/discovery/status` returns 404.
Known quirk: the outages response `links.self` has been observed echoing a different
brand path than the one requested, so do not parse `links.self` for identity.

## Step 3 — page every brand (`listEnergyPlans`)

```
GET https://cdr.energymadeeasy.gov.au/{brand}/cds-au/v1/energy/plans?type=ALL&fuelType=ALL&page-size=1000&page=N
x-v: 1
```

- `page-size` maximum is 1000; 1001 is a `400`
  (`urn:au-cds:error:cds-all:Field/InvalidPageSize`). Use 1000 to minimise calls.
- Stop on `meta.totalPages`, or follow `links.next` until it is absent.
- Volumes are uneven and that is normal: AGL returned 1,343 plans, Energy Locals 308,
  Ergon 36 on the same day.
- **`meta.totalRecords: 0` with HTTP 200 is the failure mode to guard.** Unknown brand
  segments return an empty set rather than a 404, so a typo looks like a retailer with
  no plans. Cross-check any zero against the register before publishing it.
- Coverage is NECF jurisdictions only — TAS, VIC, SA, ACT, NSW, QLD. WA and NT plans do
  not exist in this dataset; refer to the state regulator instead of reporting a gap.

## Step 4 — refresh incrementally

Re-sweeping everything daily is wasteful. Use `updated-since` (a CDS DateTimeString) on
`listEnergyPlans` to pull only what changed, and re-fetch detail (`getEnergyPlanDetail`,
`x-v: 3`) only for plans whose `lastUpdated` moved. Plan values are permanently fixed —
a change means a new `planId` or an incremented trailing digit — so `planId` +
`lastUpdated` is a safe cache key.

## Operating rules

- Public traffic across all callers is bounded by the CDS Non-Functional Requirements at
  300 TPS; `Retry-After` is CORS-exposed. Serialise or lightly parallelise per brand
  rather than fanning out 79 concurrent sweeps.
- The performance obligation on the AER is 95% of calls per hour within 1500ms and
  99.5% monthly availability — those are the numbers to alert against.
- Log `x-fapi-interaction-id` per call. It is the only thing `cdr-support@aer.gov.au`
  can trace.
- Everything is read-only `GET`. A sweep can be retried freely; there is nothing to make
  idempotent.
- Do not attempt `/energy/accounts*` or `/energy/electricity/servicepoints*` on this
  host — they are consumer data held by retailers and AEMO, and return 404 here.
