# What's new in v2.6

Design System **v2.6.0**, 19 November 2026 (decision DS-10). This release adds rules only: one list of sign-in
methods, one contract for outside services and the full analytics list, the same for every product in the
organisation, web and native. No token, component, motion or asset changes.

## Added

- **Rule 15: sign-in and identity.** Every product with accounts supports password, Google, Apple, GitHub, any OIDC
  provider, SAML 2.0, passkeys and phone code by SMS. Everything except password is off until the operator switches
  it on. It also covers two-step sign-in with recovery codes, linking several methods to one person, sessions and
  "sign out everywhere", device checks for the phone apps (App Attest, Play Integrity), what happens without email,
  throttling and audit. Staff keep the authenticator rule 4 requires. Landing pages, product docs and this site
  have no accounts of their own. See [product rules §15](product-rules.md#15-sign-in-and-identity).
- **Rule 16: outside services.** One contract (off by default, secrets write-only, a test action, the outbox,
  honest "unavailable") and one provider list per kind: email (SMTP, Amazon SES, Resend, Postmark), SMS (Twilio,
  MSG91), push (FCM, APNs), chat (Slack, Discord, Mattermost, Telegram, signed webhook) and AI (Anthropic API).
  Storage, payments and analytics keep their own rules. See [§16](product-rules.md#16-outside-services).
- **Rule 8.4: shared event names.** One list of analytics event names for every product and client, starting with
  `page_view`; a new event is added to the list before any product sends it.
- **New-feature checklist** items 14 (sign-in) and 15 (outside services).

## Changed

- **Rule 8.2** now names every product (web apps, landing pages, product docs, Android and iOS) and lists Mixpanel,
  which, when set up, is the one page-analytics provider. Mixpanel joins the mobile SDK list.
- **Rule 8.3** (Mixpanel) applies to the native apps too, under the mobile rules in 8.2.
- The rules site has a new page, **Sign-in, identity and outside services**.

## For products

Each product adopts these rules in its own repository. Nothing in this release changes how the kit is installed
or consumed.
