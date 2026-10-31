# Australian Energy Regulator

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

**Areas:** Energy · Australia · Utilities · Electricity · Gas · Energy Markets · Consumer Data Right · Retail Energy · Regulations · Government · Open Data · Smart Metering

## Australian Energy Regulator on APIs.io

Everything profiled for Australian Energy Regulator is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/aer/](https://apis.io/providers/aer/)** — or go straight to one of the APIs or properties below.

### APIs (9)

- [Australian Energy Regulator Data Holder Customers API](https://apis.io/apis/aer/aer-data-holder-customers-api/) — Data Holder Customer endpoints
- [Australian Energy Regulator Data Holder Operations API](https://apis.io/apis/aer/aer-data-holder-operations-api/) — Data Holder Operations endpoints
- [Australian Energy Regulator Distributed Energy Resources API](https://apis.io/apis/aer/aer-distributed-energy-resources-api/) — Distributed Energy Resource endpoints
- [Australian Energy Regulator Electricity Service Points API](https://apis.io/apis/aer/aer-electricity-service-points-api/) — Electricity Service Point endpoints
- [Australian Energy Regulator Electricity Usage API](https://apis.io/apis/aer/aer-electricity-usage-api/) — Electricity Usage endpoints
- [Australian Energy Regulator Energy Account Balances API](https://apis.io/apis/aer/aer-energy-account-balances-api/) — Energy Account Balance endpoints
- [Australian Energy Regulator Energy Account Billing API](https://apis.io/apis/aer/aer-energy-account-billing-api/) — Energy Account Billing endpoints
- [Australian Energy Regulator Energy Accounts API](https://apis.io/apis/aer/aer-energy-accounts-api/) — Energy Account endpoints
- [Australian Energy Regulator Energy Plans API](https://apis.io/apis/aer/aer-energy-plans-api/) — Energy Plan endpoints

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [aer-energy-prd](https://apis.io/servers/aer/aer-energy-prd/)

#### Collections (2)

Postman and Open Collection request collections.

- [CDR Energy API](https://apis.io/collections/aer/open-cdr-energy-api/)
- [CDR Common API](https://apis.io/collections/aer/open-cds-common-api/)

#### Overlays (2)

OpenAPI overlays, including conversational phrasing for each operation.

- [Aer Cdr Energy Api Overlay](https://apis.io/overlays/aer/aer-cdr-energy-api-overlay/)
- [Aer Cds Common Api Overlay](https://apis.io/overlays/aer/aer-cds-common-api-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Aer Authentication](https://apis.io/security/aer/aer-authentication/)
- [Aer Domain Security](https://apis.io/security/aer/aer-domain-security/)
- [Aer Vulnerability Disclosure](https://apis.io/security/aer/aer-vulnerability-disclosure/)

#### Rate limits (1)

Published request limits.

- [Aer Rate Limits](https://apis.io/rate-limits/aer/aer-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.aer.gov.au/)
- [Documentation](https://www.aer.gov.au/energy-product-reference-data)
- [Getting started](https://www.aer.gov.au/documents/fact-sheet-accessing-energy-product-reference-data)
- [API reference](https://consumerdatastandardsaustralia.github.io/standards/)
- [Support](https://www.aer.gov.au/about/contact-us)
- [Blog](https://www.aer.gov.au/news)
- [Security](https://www.aer.gov.au/.well-known/security.txt)
- [Terms of service](https://www.aer.gov.au/about/policies/disclaimer-copyright)
- [Privacy policy](https://www.aer.gov.au/about/policies/privacy)
- [Status](https://cdr.energymadeeasy.gov.au/agl/cds-au/v1/discovery/status)

## API Evangelist rating

**Kin Score 40.8** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 66.1 |
| Contract quality | 44.7 |
| Contract governance | 18.2 |
| Operational transparency | 68.4 |
| Developer ergonomics | 35.1 |
| Access clarity | 18.4 |

**Agent readiness 23.4** — agent-aware

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | — |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | distinct |

**Regulatory alignment 26.2** — Energy & Utilities

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/aer/](https://apis.io/providers/aer/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Australian Energy Regulator: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/aer/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
