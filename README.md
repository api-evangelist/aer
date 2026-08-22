# Australian Energy Regulator (aer)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

The Australian Energy Regulator (AER) is the independent national economic regulator of Australia's energy markets, established under the Competition and Consumer Act 2010 and operating alongside the ACCC. It sets network revenues and prices, enforces the National Electricity, Gas and Energy Retail Rules, monitors wholesale and retail market conduct, sets the Default Market Offer, keeps the public registers of authorised retailers and exemptions, and operates Energy Made Easy, the government price-comparison service. Its API posture is the strongest found among Australian energy regulators and it is genuinely implemented rather than merely mandated. The AER is a designated data holder under the Competition and Consumer (Consumer Data Right) Rules 2020 and it serves the Consumer Data Standards energy Product Reference Data endpoints — Get Generic Plans and Get Generic Plan Detail — anonymously, with no accreditation, no API key and no signup, returning live retail plan, tariff, fee, discount and eligibility data for the six jurisdictions that adopted the National Energy Customer Framework. Verified on 2026-07-27, 79 of the 84 energy data-holder brands in the ACCC CDR Register point their productBaseUri at the AER's own host, cdr.energymadeeasy.gov.au, which makes the regulator the actual operator of the product-data API layer for nearly the whole Australian retail energy industry. The split matters: the AER's open surface is product and tariff data only. It holds and exposes no individual consumer usage or billing data — the CDR consumer endpoints 404 on its host — because those flow from retailers as primary data holders and AEMO as the secondary data holder gateway, behind ACCC accreditation, OAuth2/OIDC and mTLS. The AER's own market statistics, wholesale performance reporting and public registers are published as web pages, charts and document downloads, not as an API, and no developer., developers., api., docs. or data. subdomain resolves.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/aer/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/aer/refs/heads/main/apis.yml)

## Tags

- Energy
- Australia
- Utilities
- Electricity
- Gas
- Energy Markets
- Consumer Data Right
- Retail Energy
- Regulation
- Government
- Open Data
- Smart Metering

## Timestamps

- **Created:** 2026-07-27
- **Modified:** 2026-07-27

## APIs

### AER Energy Product Reference Data - Get Generic Plans

Anonymous, unaccredited Consumer Data Right energy Product Reference Data endpoint operated by the AER. Returns a paged summary of all current, generally available retail energy plans for one retailer brand, covering plan name, fuel type, brand, distributor and postcode geography, plan type and effective dates. The retailer brand is a path segment taken from the AER's published list of CDR energy base URIs — for example `https://cdr.energymadeeasy.gov.au/agl/cds-au/v1/energy/plans?type=ALL`, which returned HTTP 200 with 1,343 AGL plans on 2026-07-27. Requires the `x-v` request header; only version 1 is supported and any other value returns 406. Default page size is 25, maximum 1000. There is no Australia-wide call — one request per retailer brand.

- **Human URL:** [https://www.aer.gov.au/energy-product-reference-data](https://www.aer.gov.au/energy-product-reference-data)
- **Base URL:** `https://cdr.energymadeeasy.gov.au/agl/cds-au/v1`

#### Tags

- Energy
- Consumer Data Right
- Product Reference Data
- Electricity
- Gas
- Tariffs

#### Properties

- [Documentation](https://www.aer.gov.au/energy-product-reference-data)
- [API Reference](https://consumerdatastandardsaustralia.github.io/standards/index.html#get-generic-plans)
- [OpenAPI](openapi/cdr-energy-api-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Specification](https://consumerdatastandardsaustralia.github.io/standards/)
- [Documentation](https://www.aer.gov.au/documents/consumer-data-right-energy-retailer-base-uris-and-cdr-brands)
- [Documentation](https://www.aer.gov.au/documents/fact-sheet-accessing-energy-product-reference-data)
- [Registry](https://api.cdr.gov.au/cdr-register/v1/energy/data-holders/brands/summary)

### AER Energy Product Reference Data - Get Generic Plan Detail

Anonymous, unaccredited Consumer Data Right energy Product Reference Data endpoint operated by the AER. Returns the full detail of a single current, generally available retail energy plan by plan identifier — tariff structures, metering charges, contract terms, incentives, discounts, fees, solar feed-in and eligibility. Version 3 is the supported version; version 2 was retired on 3 March 2025 and requests with `x-v` other than 3 return 406. Verified 2026-07-27 with `GET https://cdr.energymadeeasy.gov.au/agl/cds-au/v1/energy/plans/AGL1067320MRE2@EME` and header `x-v: 3`, HTTP 200.

- **Human URL:** [https://www.aer.gov.au/energy-product-reference-data](https://www.aer.gov.au/energy-product-reference-data)
- **Base URL:** `https://cdr.energymadeeasy.gov.au/agl/cds-au/v1`

#### Tags

- Energy
- Consumer Data Right
- Product Reference Data
- Tariffs
- Electricity
- Gas

#### Properties

- [Documentation](https://www.aer.gov.au/energy-product-reference-data)
- [API Reference](https://consumerdatastandardsaustralia.github.io/standards/#cdr-energy-api_get-generic-plan-detail)
- [OpenAPI](openapi/cdr-energy-api-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Specification](https://consumerdatastandardsaustralia.github.io/standards/)
- [Documentation](https://www.aer.gov.au/documents/consumer-data-right-energy-retailer-base-uris-and-cdr-brands)

## Common Properties

- [Website](https://www.aer.gov.au/)
- [About](https://www.aer.gov.au/about)
- [Contact](https://www.aer.gov.au/about/contact-us)
- [Documentation](https://www.aer.gov.au/energy-product-reference-data)
- [API Reference](https://consumerdatastandardsaustralia.github.io/standards/)
- [Registers](https://www.aer.gov.au/industry/registers)
- [Registers](https://www.aer.gov.au/industry/registers/authorisations)
- [Data Portal](https://www.aer.gov.au/industry/registers/charts)
- [Reports](https://www.aer.gov.au/industry/wholesale/performance)
- [Website](https://www.energymadeeasy.gov.au/)
- [Blog](https://www.aer.gov.au/news)
- [RSS](https://www.aer.gov.au/rss.xml)
- [Regulation](https://www.cdr.gov.au/)

## Maintainers

- **Kin Lane** — kin@apievangelist.com

## Artifacts

Enrichment round 2026-07-27 (search → generate → derive; every claim probed live or cited):

- `openapi/` — CDR Energy API 1.36.0 and CDR Common API 1.36.0 (both DSB-authored, harvested verbatim)
- `overlays/` — what is true of the **AER's deployment** of those two specs (which operations are served, at which versions, on which real host)
- `authentication/` — the anonymous model plus the mandatory `x-v` / optional `x-min-v` header contract
- `conventions/` — base-URI shape, version negotiation, paging, envelope, tracing, CORS (no idempotency: the surface is read-only)
- `errors/` — the CDS `urn:au-cds:error:` catalogue, captured from live 400/404/406 responses
- `lifecycle/` — endpoint version schedule with real deprecation and retirement dates, CDS SLA, and the machine-readable status endpoint
- `rate-limits/` — the CDS Non-Functional Requirements the AER's own FAQ adopts (300 TPS public traffic, 1500ms/95%, 99.5% availability)
- `conformance/` — what the AER conforms to and, just as usefully, what it does not (no OAuth, no RFC 9457, no Green Button/IEEE 2030.5/CIM)
- `data-model/` — the plan entity graph derived from the specification's `$ref` tree
- `changelog/` — AER version notices plus DSB standards releases
- `well-known/` + `security/` — RFC 9116 `security.txt` (contact only, no policy), TLS/DNS posture
- `mcp/` — a **candidate** tool surface and its crosswalk to real `operationId`s (the AER publishes no MCP server)
- `skills/`, `llms/` — generated agent operating instructions and an `llms.txt` (the AER publishes neither)

## Notes

The specifications in `openapi/` are the Data Standards Body's **CDR Energy API 1.36.0** and **CDR Common API 1.36.0**, harvested verbatim from the Consumer Data Standards repository on 2026-07-27. It is the contract the AER serves, not a specification the AER publishes — the AER publishes none. The AER implements only the two `/energy/plans` operations from the energy spec, plus the two anonymous `/discovery/status` and `/discovery/outages` operations from the common spec — verified live on 2026-07-27, and the closest thing the AER has to a status page. The account, billing, service point, usage and distributed-energy-resource paths belong to retailers and AEMO and return 404 on the AER's host. See `review.yml` for the full mandate, access-gate and provenance record.
