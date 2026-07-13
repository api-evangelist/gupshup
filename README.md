# Gupshup (gupshup)

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
