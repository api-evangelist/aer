# Australian Energy Regulator (aer)

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

## Notes

The single specification in `openapi/` is the Data Standards Body's **CDR Energy API 1.36.0**, harvested verbatim from the Consumer Data Standards repository on 2026-07-27. It is the contract the AER serves, not a specification the AER publishes — the AER publishes none. The AER implements only the two `/energy/plans` operations from it; the account, billing, service point, usage and distributed-energy-resource paths belong to retailers and AEMO and return 404 on the AER's host. See `review.yml` for the full mandate, access-gate and provenance record.
