# What's new for SpaceWorks 1.0

**SpaceWorks 1.0.0** is the first stable release of the product (owner decision 672). This design system is its **stable baseline**. The two version numbers are different things: *SpaceWorks 1.0.0* is the product; the design system keeps its own semver, which is **v2.5.1** (`VERSION` and the latest published kit tag, 15 November 2026); these docs add no new kit tag. See [CR-RELEASE-01](current-rules.md#cr-release-01). The product release is not out yet: its pull request is open and only the owner merges.

## The look does not change

Everything visual stays as it is: tokens, light and dark themes, the three type families, components, icons, logo, Patch, motion values and brand rules. A screen built to [Current rules](current-rules.md) for 0.12.0 is already built to 1.0.

## New: UX rules

[SpaceWorks UX rules](ux-rules.md) set how screens **behave**, adapted from the MIT-licensed ui-ux-pro-max skill:

- Ten categories in priority order, from accessibility and touch down to charts, each rule a MUST or SHOULD with its reason.
- Mapped to the places people use Space Works: the staff console (including the front-desk and other narrow consoles), the member area, public pages, sign-in screens and kiosks, and to the [patterns](patterns/README.md) that implement them.
- Navigation rules for a role-gated product: one home per feature, gated items absent, inner levels inside their feature, every view a URL, back that restores filters and page.
- A table of every point where the source suggests something different (toast timing, Undo, disabled opacity, asterisks, icons in the sidebar, springy motion, palettes) — Space Works wins in each.
- A [pre-delivery UX checklist](ux-rules.md#pre-delivery-ux-checklist) to run per screen: every role and area combination, queues and detail pages, forms, light and dark, Lingui, motion, devices, keyboard and screen readers.

The unmodified source rule sets and their licence are in [`references/ui-ux-pro-max/`](../references/ui-ux-pro-max/LICENSE-NOTICE.md).

## What the product's 1.0 UX work covers

The [release entry](releases/spaceworks-1.0.0.md) lists it with an honest status. In short: role-scoped navigation with one group per feature, error boundaries on every route, real pagination where lists were capped, confirmation dialogs on one-click destructive actions, failed loads shown as errors rather than empty lists, phone sign-in and account restore on the web, and clearer access for staff who come through an organisation. All of it is written with tests queued; none of it is verified yet. The inner-level queues, filters and detail pages, the unified Requests hub, and the consolidated role homes, calendar and "My stuff" are **still in progress**.

## For maintainers

`VERSION` is not bumped by these documents. The UX rules are new normative guidance, which the [versioning policy](releases/versioning.md) counts as a **minor** change; the release owner decides the number when this branch is rebased onto `dev` and published.
