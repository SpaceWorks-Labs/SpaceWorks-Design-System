---
title: SpaceWorks 1.0.0 — stable
description: Draft release entry for the design-system baseline that ships with SpaceWorks 1.0.0, the first stable product release.
---
# SpaceWorks 1.0.0 — stable (design-system release entry)

**Two version axes, kept apart ([CR-RELEASE-01](../current-rules.md#cr-release-01)).** *SpaceWorks 1.0.0* is the **product** version (owner decision 672: the release ships as "SpaceWorks 1.0.0"). The **design-system** version is its own semver and is **not** 1.0.0 — kit v1 was a much earlier edition. This entry records which kit the product release uses and what the design system adds for it. It does not bump `VERSION`.

## [SpaceWorks 1.0.0 baseline] — draft, 2026-11-19

Status: **draft**. Tag: none yet. Commit: none yet (these files are uncommitted on `design-0.12.0`).
Kit version: **v2.5.1** (`VERSION` reads 2.5.1; tag v2.5.1, 15 November 2026). The UX rules and these notes are docs only, so they ship without a new kit tag, as SW-630 did for docs and screenshots. The release owner records the final kit tag here when the product release is cut.
Ships alongside: **SpaceWorks 1.0.0** (product; not released at the time of writing — the dev→main PR is open and only the owner merges). Artwork edition: v2.
Owner: Space Works design-system owner.

### Changed

- **Visual system: nothing.** Tokens, colours, typography, radius, components, icons, logo, mascot, motion values and brand rules are exactly as in the kit version above. No token, component or asset file is touched by this entry.

### Added

- **[SpaceWorks UX rules](../ux-rules.md)** (`docs/ux-rules.md`, decision 937). Behaviour rules adapted from the MIT-licensed ui-ux-pro-max skill, in its ten priority categories (accessibility, touch and interaction, performance, layout, forms and feedback, navigation, animation behaviour, charts and data; style, typography and colour reduced to pointers to the existing system). Each rule is MUST or SHOULD with its reason, mapped to the staff console, member area, public pages, auth screens and kiosks and to the pattern docs. A table lists every point where the source and Space Works differ; Space Works wins in each. Ends with a pre-delivery UX checklist for web, light/dark, Lingui, role-gated screens, queues/filters/detail pages and multiple spaces.
- **[`references/ui-ux-pro-max/`](../../references/ui-ux-pro-max/LICENSE-NOTICE.md)**: unmodified copies of the source's quick reference, pro rules, UX guidelines and app-interface data, with the MIT notice and source URL. Scripts and visual data were not copied.

### Product UX work in SpaceWorks 1.0.0

This is the product work these rules describe. Status is taken from the lane reports in the SpaceWorks repository (`handover/reports/codex/`). **Every lane below reports that no vitest, tsc or build was run** (the machine was low on memory); their tests are written and queued. Nothing here is claimed as verified until those runs and the final UI gate (decision 939) pass.

| Area | What changed | Status |
| --- | --- | --- |
| Role-scoped navigation, one group per feature | Each page has one sidebar heading for every role (Accountability under Insights, Staff & roles under People, Organized events under Organizations); "Today" heading; "Pickups" label; names come from one label source; nine one-item platform headings become "Platform". Accountability leaves the nav with the reports area off; unit-only, ID-programme and card-approval roles get their pages; `edit_inventory` implies `view_inventory`; the scanner opens for view-only inventory staff; the fundraising-only console gets personal channels; one kiosk route table. (UX-FIX-2, UI-FIX-ROLES) | Written; tests queued |
| Spaces and organisations | Organisation-derived staff land on a tab the server allows; their role shows as "… (organization access)"; switching spaces lands on the role's home instead of "Access denied". No cross-space cache leak was found. (UI-TENANCY) | Written; tests queued |
| Error boundaries | A friendly "Reload page" card around every member, public, help, docs and kiosk route, reset on navigation. Stale-chunk auto-reload is not done. (UX-FIX-1) | Written; tests queued |
| Pagination | Real paging on member ticket orders, area payment claims, the repair shelf and problem reports (problem reports moved to standard DRF pagination; its OpenAPI snapshot is not regenerated yet). (UX-FIX-1, UX-FIX-3) | Written; tests queued |
| Confirm dialogs | Danger confirmations for certificate revoke, claim-code revoke and rotating a station PIN. The rest of the audit's list (promos, add-ons, collaborators, ballots, invite links and others) is left. (UX-FIX-1) | Partly done; written, tests queued |
| Failed fetch is not "empty" | Shelf history, POS member picker, notification recipient picker and refund suggestions show an error with Retry instead of an empty result. (UX-FIX-1) | Written; tests queued |
| Reachability | Display screens, Background eraser, Wallet and Joining are reachable from settings; member links to ticket orders, machine jobs, application reviews and speaker slots. (UX-FIX-1, UX-FIX-3) | Written; tests queued |
| Phone sign-in and account restore | "Continue with phone" on the web member sign-in, shown only when SMS, member accounts and the phone sign-in switch are all on; account restore by email link, phone code or sign-in provider (Google, Apple, OIDC). (UI-FEATURES) | Written; tests queued |
| Translation | Hard-coded English moved to Lingui in the listed member, auth and kiosk components; some components remain. `lingui extract` still to run. (UX-FIX-1, UI-FEATURES) | Partly done |
| Inner-level queues, filters, detail pages and bulk actions per domain | DEEP-UX lanes 1–4 (decision 934) | **In progress** — no lane report yet |
| Unified Requests hub (all decision types) | DEEP-UX-5 (decisions 935, 936) | **In progress** — no lane report yet |
| Consolidated role homes, calendar and "My stuff" for every role | DEEP-UX-6 consolidation (decision 936) | **In progress** — no lane report yet |
| Final UI gate | Coverage per role, one group per feature, no lost actions, scoping and the [UX checklist](../ux-rules.md#pre-delivery-ux-checklist) (decision 939) | **Not started** |

### Accessibility and verification

- Design-system side: documentation only. No site build, link check or browser run was made for this entry.
- Product side: see the status column above. The release owner replaces "tests queued" with the actual run results before this entry is marked released.

### Migration

None for consumers of the kit: no token, component or path changed. Product teams adopt the UX rules for new and changed screens and use the checklist at review time.

### Assets

`docs/ux-rules.md`, `references/ui-ux-pro-max/` (four source files and `LICENSE-NOTICE.md`), `docs/whats-new-spaceworks-1.0.md` and this entry. All Markdown/CSV text.
