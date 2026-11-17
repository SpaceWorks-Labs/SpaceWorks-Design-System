# Recapture list for `screenshots/ux/`

All 49 shots were taken in the older Space Works **Events** app palette (lime-green sidebar, teal buttons).
They are recaptured from SpaceWorks 0.12.0 on the dev stack (`./scripts/dev.sh up --build`, web at
`http://localhost:5000`) with the current palette (`tokens/tokens.json`), keeping the **same file names**.

Viewports: **desktop** = 1280x800, **phone** = 390x844. Themes: **light** and **dark**; phone shots are light only.
Naming: `<screen>-<desktop|phone>-<light|dark>.webp`. Capture dark by adding the `dark` class to `<html>`
(or the theme toggle). The route column is the best-known match from the 0.12.0 router
(`frontend/src/`); the owner of the live pass should confirm each one when capturing.

| # | File stem | Screen shown in the old shot | SpaceWorks 0.12.0 route to recapture from | Variants |
|---|---|---|---|---|
| 1 | `account-profile` | Account profile: avatar, display name, tabs (Profile, Registrations, Your IDs, Organisations, Security) | `/m/<slug>/member/account` (signed-in member) | desktop light, desktop dark |
| 2 | `auth-reset-password` | Reset password card: email field, "Send reset link" | `/reset-password` | desktop light, desktop dark |
| 3 | `auth-sign-in` | Welcome back sign-in: Sign in / Create account switch, email + password, brand panel on the right | the sign-in page (`/login`, or any protected route while signed out) | desktop light, desktop dark, phone light |
| 4 | `detail-overview` | Event detail, Overview tab: date tile, stat cards, "Almost ready" checklist | `/m/<slug>/admin/events/<id>` (staff console, event overview) | desktop light, desktop dark, phone light |
| 5 | `flow-check-in` | Check-in desk: QR scanner, search attendees, override toggles | `/m/<slug>/admin/events/<id>` Check-in tab (staff scan flow) | desktop light, desktop dark, phone light |
| 6 | `form-new-organisation` | Create an organisation form: name, web address, description, logo | `/organizations/new` (new organisation form) | desktop light, desktop dark |
| 7 | `list-guests` | Event Guests tab: status filter chips, guest rows with Approve / Decline | `/m/<slug>/admin/events/<id>` Guests tab | desktop light, desktop dark, phone light |
| 8 | `list-member-ids` | Member IDs list: programme, tabs, table with ID number / status / valid until | `/m/<slug>/admin/members` Member IDs view (membership module) | desktop light, desktop dark, phone light |
| 9 | `public-event` | Public event page: title, venue map, "Join this event" register card | `/m/<slug>/events/<publicToken>` | desktop light, desktop dark, phone light |
| 10 | `public-organisation` | Public organisation page: header, upcoming/past tabs, event rows | `/o/<organizationSlug>` | desktop light, desktop dark, phone light |
| 11 | `public-ticket` | Ticket confirmation "You're in": event card and QR code | registration confirmation / ticket view after registering on `/m/<slug>/events/<publicToken>` | desktop light, desktop dark, phone light |
| 12 | `public-verify-card` | Public "Valid card" verification result for a member ID | public member-ID verify page (`/verify/<token>`) | desktop light, desktop dark, phone light |
| 13 | `public-verify-not-found` | Verification "Card not found" state | same verify page with an unknown token | desktop light, desktop dark, phone light |
| 14 | `settings-organisation` | Organisation Settings: logo, name, description, live public-page preview | `/organizations/<organizationSlug>/settings` | desktop light, desktop dark, phone light |
| 15 | `table-team` | Members / team table: stat cards, invite link, role selector, "what each role can do" | `/organizations/<organizationSlug>/members` (or `/m/<slug>/admin/staff`) | desktop light, desktop dark |
| 16 | `workspace-dashboard` | Workspace dashboard: greeting, next-up event card, stat tiles, activity | `/m/<slug>/admin` (staff console home) | desktop light, desktop dark, phone light |
| 17 | `workspace-empty-state` | Brand-new organisation: "ready" checklist with setup steps, no events yet | `/m/<slug>/admin` for a freshly created makerspace | desktop light, desktop dark |
| 18 | `workspace-organisations` | Organisation overview: banner, name, Settings / New series / New event actions, pending-approval notice, event + calendar | `/organizations/<organizationSlug>` | desktop light, desktop dark |

Total: **49 files** (18 screens: 18 desktop light, 18 desktop dark, 13 phone light).

Notes for the live pass:

- Use the seeded demo data so the shots stay consistent (Space Works Kochi, Demo Organiser, "Kochi Maker Night").
- The old shots show the Events product chrome ("space works / Events"); the new shots show whatever 0.12.0
  chrome the route renders. If a screen no longer exists in 0.12.0, keep the old file and list it in the pass report.
- Re-encode as WebP (quality ~80) at the sizes above; keep each file small.

## Recapture pass 2026-11-13 (SpaceWorks 0.12.0, dev stack)

Captured with Playwright (Chromium) on the dev stack, seeded showcase space `tinkerspace` ("Tinkerspace"), fictional
accounts only. Desktop 1280x800 light and dark, phone 390x844 light, WebP quality 80, same file names. The seeded
data in this repo is the showcase space, not "Space Works Kochi / Kochi Maker Night"; screens show that data.

Recaptured (36 of the 48 files on disk):

| File stem | Route used | Signed in as |
|---|---|---|
| `account-profile` (desktop light, dark) | `/m/tinkerspace/member/account` | member (Asha Menon) |
| `auth-reset-password` (desktop light, dark) | `/reset-password` | none |
| `auth-sign-in` (desktop light, dark, phone light) | `/sign-in` | none |
| `detail-overview` | `/m/tinkerspace/admin/events?event=5` (Overview tab) | Space Manager |
| `flow-check-in` | `/m/tinkerspace/admin/events?event=5&eventTab=checkin` | Space Manager |
| `list-guests` | `/m/tinkerspace/admin/events?event=5&eventTab=registrations` (the Guests tab is now "Registrations") | Space Manager |
| `list-member-ids` | `/m/tinkerspace/admin/member-cards` (Cards tab) | Space Manager |
| `public-event` | `/m/tinkerspace/events/<publicToken>` | none |
| `public-organisation` | `/o/tinkerspace-collective` (public profile switched on for the org first) | none |
| `public-verify-card` | `/verify/c/<token>` (public check switched on in member card settings, token minted for card TNK-0001) | none |
| `public-verify-not-found` | `/verify/c/<43-character unknown token>` | none |
| `table-team` (desktop only) | `/m/tinkerspace/admin/users` (Staff & roles) | Space Manager |
| `workspace-dashboard` | `/m/tinkerspace/admin/dashboard` | Space Manager |

Not recaptured (old files kept, in the old palette):

- `form-new-organisation`, `settings-organisation`, `workspace-organisations`: 0.12.0 has no `/organizations/new`,
  `/organizations/<slug>/settings` or `/organizations/<slug>` route (the router only has `/organizations`, the public
  directory, and `/o/<slug>`, the public page). Organisation creation lives in the member account page and is off by
  default (`ORGANIZATION_SELF_CREATION_ENABLED`), and the owner-side workspace is not a standalone screen.
- `public-ticket`: needs a registration confirmation for a signed-in member; the showcase registrations are guest rows
  with no account, so no ticket screen could be opened from seed data.
- `workspace-empty-state`: needs a brand-new makerspace with no data; no empty space was seeded in this pass.

Notes:

- `auth-sign-in` shows the brand panel of the sign-in page, which carries a staff ID-card illustration with a real
  person's name and photo (a design asset in the app, not seed data). Check it before these files are published.
- The phone shots of `list-guests` show the Status and Ticket selects reaching the right edge of the screen (no right
  gutter); this is how 0.12.0 renders today, not a capture error.


- 2026-11-13: auth-sign-in-desktop-light/-dark and auth-sign-in-phone-light retaken from the real signed-out sign-in page (the staff console route /m/tinkerspace/admin, with its Sign in / Create account form and brand panel; /sign-in is not a route). table-team-desktop-light/-dark retaken on /m/tinkerspace/admin/users after completing the "Confirm your identity" step-up, so the Staff & roles table, role selector and Invitations tab are visible. Seed data only.

## README pairs still missing (2026-11-17, README "Product screens by area")

Shown today (light and dark pair each, both in the current palette): sign-in and auth, tables, lists, detail pages,
flows, dashboard, public pages (all `screenshots/ux/`), and motion, logo, overlays (`screenshots/site/`).

Missing, for the dev-stack capture pass (desktop 1280x800, light and dark, seeded showcase space `tinkerspace`):

- **Forms**: `form-new-organisation-desktop-light/-dark.webp` exist only in the old palette (0.12.0 has no
  `/organizations/new` route). Capture another populated form in 0.12.0 (for example member card settings or the new
  event form), name it `form-<name>-desktop-light/-dark.webp`, then add the Forms cell back to the README gallery.
- **Display (TV) screen**: not captured at all. Needs a kiosk/display route at 1920x1080 in both themes.
- Older gaps from the 2026-11-13 pass, still open: `public-ticket`, `workspace-empty-state`, `settings-organisation`,
  `workspace-organisations` (old palette kept on disk; none is used in the README).
