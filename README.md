# Gupshup (gupshup)

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

Gupshup is a conversational messaging and CPaaS platform (headquartered in India) that lets businesses send and receive messages across WhatsApp, SMS, RCS, and other channels, plus build chatbots and conversational AI journeys. The developer platform exposes REST APIs on `api.gupshup.io` - most prominently the WhatsApp Business API (send session and template messages, opt-in management, templates, media, and inbound webhooks) - authenticated with an `apikey` header and scoped to a registered app. Separate SMS, RCS, and Partner API surfaces are also documented.

**Access model:** Self-serve. Sign up, create an app, link a WhatsApp Business number, and get an account `apikey` from the dashboard. The `apikey` is sent as an HTTP header on every request and scopes calls to your account; operations reference the app by name (`src.name` field or the `appName` path segment). Messages are accepted asynchronously and return a `messageId`; delivery and inbound events are pushed to a callback URL / Subscription you host (inbound webhooks, not WebSocket). The Partner API (`partner.gupshup.io`) uses a partner token / app access token instead of the per-app `apikey`.

**Honesty note:** The send-message (`POST /wa/api/v1/msg`) and send-template (`POST /wa/api/v1/template/msg`) operations are confirmed against Gupshup's public API reference. The opt-in / opt-out, users, and template-list operations are documented in Gupshup's WhatsApp API guide (historically under the `/sm` path, now migrating to `/wa`); their request/response schemas are modeled from prose documentation. The SMS `/sm` surface is being retired (end-of-life announced), and RCS is served through the onboarding-gated Gupshup Enterprise gateway rather than the `apikey` REST surface — those are listed as documented channels but are not modeled in the OpenAPI.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/gupshup/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/gupshup/refs/heads/main/apis.yml)

## Tags

- Messaging
- WhatsApp
- Conversational AI
- CPaaS
- SMS
- RCS
- India
- Chatbots
- Business Messaging
- Communications

## Timestamps

- **Created:** 2026-07-12
- **Modified:** 2026-07-12

## APIs

### Gupshup WhatsApp Messaging API

Send session (user-initiated, 24-hour window) WhatsApp messages of many types - text, image, file, audio, video, sticker, location, contact, and interactive list / quick-reply - from a registered WhatsApp Business number via `POST /msg`, with delivery events returned to your webhook.

- **Human URL:** [https://docs.gupshup.io/reference/msg](https://docs.gupshup.io/reference/msg)
- **Base URL:** `https://api.gupshup.io/wa/api/v1`

#### Tags

- WhatsApp
- Messaging
- Business Messaging

#### Properties

- [Documentation](https://docs.gupshup.io/docs/whatsapp-api-introduction)
- [API Reference](https://docs.gupshup.io/reference/msg)
- [OpenAPI](openapi/gupshup-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/gupshup.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/gupshup.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Gupshup WhatsApp Template Messaging API

Send pre-approved WhatsApp template (HSM) messages to opted-in users outside the 24-hour session window via `POST /template/msg`, and list an app's templates and their approval status via `GET /template/list/{appName}`.

- **Human URL:** [https://docs.gupshup.io/docs/template-messages](https://docs.gupshup.io/docs/template-messages)
- **Base URL:** `https://api.gupshup.io/wa/api/v1`

#### Tags

- WhatsApp
- Templates
- Notifications

#### Properties

- [Documentation](https://docs.gupshup.io/docs/template-messages)
- [OpenAPI](openapi/gupshup-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/gupshup.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)

### Gupshup WhatsApp Opt-In Management API

Mark a user as opted-in or opted-out for an app and list the users who have interacted with your business number and their opt-in status. Required before template notifications can be delivered. Legacy opt-in/opt-out APIs are not supported for apps created after Aug 2025.

- **Human URL:** [https://docs.gupshup.io/docs/optin-message](https://docs.gupshup.io/docs/optin-message)
- **Base URL:** `https://api.gupshup.io/wa/api/v1`

#### Tags

- WhatsApp
- Opt-In
- Consent

#### Properties

- [Documentation](https://docs.gupshup.io/docs/optin-message)
- [OpenAPI](openapi/gupshup-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

### Gupshup SMS API

Broadcast SMS to a single number or many numbers programmatically via `POST /msg` on the `/sm` surface. Note - Gupshup has announced end-of-life for the `/sm` endpoints and recommends migrating SMS traffic to the `/wa` messaging surface.

- **Human URL:** [https://docs.gupshup.io/docs/sms-api-introduction](https://docs.gupshup.io/docs/sms-api-introduction)
- **Base URL:** `https://api.gupshup.io/sm/api/v1`

#### Tags

- SMS
- Messaging
- Notifications

#### Properties

- [Documentation](https://docs.gupshup.io/docs/sms-api-introduction)
- [Documentation](https://docs.gupshup.io/docs/send-message-to-single-number)

### Gupshup RCS API

Send RCS (Rich Communication Services) business messages - rich cards, carousels, suggested replies, and media. RCS is onboarding-gated (username / password issued by Gupshup) and served through the Gupshup Enterprise messaging gateway rather than the apikey-based `api.gupshup.io` REST surface.

- **Human URL:** [https://docs.gupshup.io/docs/rcs-api-introduction](https://docs.gupshup.io/docs/rcs-api-introduction)

#### Tags

- RCS
- Rich Messaging
- Business Messaging

#### Properties

- [Documentation](https://docs.gupshup.io/docs/rcs-api-introduction)
- [API Reference](https://docs.gupshup.io/docs/send-rcs-message)

### Gupshup Partner API

Token-authenticated Partner surface (`partner.gupshup.io`) for BSPs and resellers - manage apps, templates, subscriptions/callbacks, and send messages through Meta-format passthrough endpoints (e.g. `POST /partner/app/{appId}/v3/message`). Uses a partner token / app access token rather than the per-app `apikey` header.

- **Human URL:** [https://partner-docs.gupshup.io/docs/whatsapp-passthrough-apis-for-partners](https://partner-docs.gupshup.io/docs/whatsapp-passthrough-apis-for-partners)
- **Base URL:** `https://partner.gupshup.io/partner`

#### Tags

- Partner
- WhatsApp
- Passthrough

#### Properties

- [Documentation](https://partner-docs.gupshup.io/docs/whatsapp-passthrough-apis-for-partners)

## Common Properties

- [Authentication](authentication/gupshup-authentication.yml)
- [Domain Security](security/gupshup-domain-security.yml)
- [LinkedIn](https://www.linkedin.com/company/gupshup)
- [Website](https://www.gupshup.io)
- [Documentation](https://docs.gupshup.io)
- [Plans](plans/gupshup-plans-pricing.yml)
- [Rate Limits](rate-limits/gupshup-rate-limits.yml)
- [Fin Ops](finops/gupshup-finops.yml)
- [Blog](https://www.gupshup.io/resources/blog)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
