---
title: UX rules
description: Space Works UX rules adapted from ui-ux-pro-max — behaviour rules by priority, mapped to Space Works screens and patterns, plus the pre-delivery UX checklist.
---
# SpaceWorks UX rules (adapted from ui-ux-pro-max)

**Scope: behaviour only.** These rules cover how Space Works screens behave: access, input, feedback, navigation, motion behaviour, responsive layout and data display. They do **not** change the visual design system. Tokens, colours, typography, radius, components, icons, logo, mascot and brand stay exactly as the [current rules](current-rules.md), [brand spec](ui-brand-spec.md), [theming](theming.md) and [motion](motion.md) define them. Where the source material suggests a different visual choice, **the existing design system wins**, and this page says so at that rule. The full list of differences is in [§11](#11-where-the-source-and-space-works-differ).

**Precedence.** [Current rules](current-rules.md) → owner decisions in the [decision record](decisions.md) → [UX spec](ux-spec.md) and [patterns](patterns/README.md) → this page → the source reference. This page adds rules; it does not replace a pattern contract. If a rule here appears to contradict a pattern, the pattern wins and the contradiction is a documentation bug.

**Source.** Adapted from the MIT-licensed [ui-ux-pro-max skill](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) © nextlevelbuilder. The unmodified rule sets are kept in [`references/ui-ux-pro-max/`](../references/ui-ux-pro-max/LICENSE-NOTICE.md); the backtick key at the end of each rule (for example `color-contrast`) is its key there. Added 2026-11-19 (decision 937) for SpaceWorks 1.0.0.

**Language.** **MUST** = a review blocks the change. **SHOULD** = expected; a deviation is stated in the PR with its reason.

## Surfaces used below

| Surface | What it is | Layout |
| --- | --- | --- |
| **Staff** | The staff console, including the narrow consoles (front desk / handout-only, machine-only, governance-only) | [L1 AppShell](patterns/README.md#app-shell) + L2–L7 |
| **Member** | The member area (`/member`, home, tabs, history, account) | L1 + L2–L6 ([S16](ux-spec.md#s16-member-area-home-and-tabs-member-membertab--r1-home-r26-card-r16-account)) |
| **Public** | Catalogue, item, event, verify and organisation pages | [L9](patterns/README.md#public-layouts) |
| **Auth** | Sign-in, sign-up, phone sign-in, MFA, account restore, invitations | [L8](patterns/README.md#authentication-layouts) |
| **Kiosk** | Kiosk stations, central desk kiosks and displays | [L10](patterns/README.md#kiosk-layout) |

"All" means every surface. Screens are role-gated and module-gated: a rule applies to every role and module combination that can reach the screen, not only to the Space Manager view.

---

## 1. Accessibility — CRITICAL

Target: WCAG 2.2 AA, with the stronger house rules in [Accessibility](accessibility.md#wcag-minimums-and-stronger-house-rules). That page owns the criterion map and the test scripts; these rules are the everyday floor.

- **UX-1.1 MUST** Text meets 4.5:1 and meaningful icons, control boundaries and focus rings meet 3:1, **measured in light and dark separately**. *Why:* a pair that passes in light often fails in dark. *Where:* all. Use only the token pairs the [contrast matrix](../tokens/contrast-matrix.md) allows; never fix contrast with a local colour. `color-contrast`, `color-accessible-pairs`
- **UX-1.2 MUST** Every interactive element shows the house focus ring on keyboard focus; never remove it. Sticky headers, bulk bars, toasts and drawers must not hide the focused control. *Why:* keyboard users lose their place. *Where:* all; especially Staff tables with sticky header + bulk bar. `focus-states`, `focus-not-obscured`
- **UX-1.3 MUST** Icon-only controls have an accessible name that matches what they do ("Close", "Row actions for Bosch drill"); decorative icons beside visible text are hidden from assistive technology. *Where:* all; row menus, toolbars, kiosk keypad. [IconButton](components/icon-button.md). `aria-labels`, `icon-context`
- **UX-1.4 MUST** Tab order follows the visual order; the full task works with the keyboard alone. Tabs use roving focus with arrows and Home/End; Escape closes a dialog, drawer or menu and returns focus to its opener. *Where:* all. See the [quality bar](ux-spec.md#4-ux-quality-bar-every-screen-app-wide-implementation-must-pass-every-applicable-item). `keyboard-nav`, `escape-routes`
- **UX-1.5 MUST** One `h1` per screen and headings in order without skipped levels; landmarks for navigation, main and complementary content; a skip link to `#main-content`. *Why:* screen-reader users navigate by headings. *Where:* all. `heading-hierarchy`, `skip-links`
- **UX-1.6 MUST** Status is never colour alone: every pill has a word, overdue chips say "Overdue 3 days", required evidence says "Required". *Where:* all; queues, request states, payment states, kiosk results. See [CR-STATUS-01](current-rules.md#cr-status-01). `color-not-only`
- **UX-1.7 MUST** A changed count or status (queue size, sync count, scan result) is announced once, as a full phrase, in one polite status region, without moving focus. No frame-by-frame chatter. *Where:* Staff queues, Kiosk, Member notices. `contextual-live-badge-updates`
- **UX-1.8 MUST** Respect reduced motion before first paint: every animation has a still equivalent carrying the same information. *Where:* all. See [motion rules](motion.md#rules). `reduced-motion`
- **UX-1.9 MUST** Every drag action (reorder, drop upload, draggable sheet) has a single-pointer alternative and a keyboard path; a draggable sheet still has a Close button. *Where:* Staff form builders, card/badge designers, uploads. `dragging-alternative`
- **UX-1.10 MUST** Sign-in and recovery allow password managers, autofill, full-code paste and a show-password control; one-time codes use one input with `autocomplete="one-time-code"`. No puzzles or memory tests as the only path. *Where:* Auth (password, phone code, MFA, restore). `accessible-authentication`
- **UX-1.11 MUST** Do not ask again for information already given in the same process (address, identity, member chosen in step 1) unless re-entry is essential for security. *Where:* Staff handover and checkout flows, Public request and registration flows. `redundant-entry`
- **UX-1.12 SHOULD** Help links that repeat across a set of pages keep the same relative order. *Where:* Staff settings, Public footer. `consistent-help`
- **UX-1.13 MUST** Anything that moves on its own (rotating notices, display carousels) can be paused and stops on focus and under reduced motion. *Where:* Public, Kiosk displays. `auto-rotation-controls`
- **UX-1.14 MUST** Content still works at 200% text, with the WCAG text-spacing overrides, at 400% zoom and in forced colours. Do not hide content to make a width check pass. *Where:* all. `dynamic-type`

## 2. Touch and interaction — CRITICAL

- **UX-2.1 MUST** Targets are at least **44 px** on web, **56 px** on kiosks (48 dp Android, 44 pt iOS in the native apps). Extend the hit area rather than enlarging the visual when the icon is small. *Why:* front-desk staff work on tablets and phones at the counter; kiosks are used standing. The house targets are stricter than the WCAG 24 px minimum and win. `touch-target-size`, `web-target-size`
- **UX-2.2 MUST** Keep at least 8 px between adjacent targets; never require a precise tap on a thin edge or a small glyph. *Where:* row actions, chip removal, pagers. `touch-spacing`, `no-precision-required`
- **UX-2.3 MUST** Nothing depends on hover. Tooltips, row actions and previews are reachable by tap and keyboard. *Where:* all; Staff tables most of all. `hover-vs-tap`
- **UX-2.4 MUST** Every mutation shows a pending label on its own control ("Saving…", "Recording issue…") and disables only that control until it settles. A repeated click must not send a second write. *Why:* double handovers and double payments are audited records that cannot be undone. *Where:* all. `loading-buttons`, `submit-feedback`
- **UX-2.5 MUST** Errors appear next to the thing that failed, with a recovery (see §8). *Where:* all. `error-feedback`
- **UX-2.6 SHOULD** Pressed and active feedback appears within about 100 ms. In Space Works this is the **colour** change of the state tokens; do not add scale, ripple or lift (see §11). `press-feedback`, `tap-feedback-speed`
- **UX-2.7 MUST** No swipe-only or gesture-only action: every critical action has a visible control. No horizontal swipe on main content. *Where:* Member, Public, Kiosk. `gesture-alternative`, `gesture-conflicts`
- **UX-2.8 SHOULD** Clickable non-button elements (clickable table rows, cards) show the pointer cursor and are also reachable as a real link or button inside the row. `cursor-pointer`
- **UX-2.9 MUST** Fixed bottom bars (handout bottom tabs, sticky primary on handover/cart/register) respect `env(safe-area-inset-bottom)` and never cover the last row of content. `safe-area-awareness`, `fixed-element-offset`
- **UX-2.10 MUST** Cameras start only on explicit intent ("Start scanning"), except task-mode scan steps where scanning is the step, and there is always a manual-entry fallback under the camera. *Where:* Staff scanner, issue/return, Kiosk check-in. From the [quality bar](ux-spec.md#4-ux-quality-bar-every-screen-app-wide-implementation-must-pass-every-applicable-item).

## 3. Performance — HIGH

- **UX-3.1 MUST** Reserve space for anything that loads late (images, cards, stat values, tables) so the page does not jump; declare image dimensions or aspect ratio. Target CLS below 0.1. *Where:* all; Public catalogue images most of all. `image-dimension`, `content-jumping`
- **UX-3.2 MUST** Lists page on the server: DRF page size 24 with "1–24 of 248" and Previous/Next ([Pagination](components/pagination.md)). Never load "everything" into a client list. Virtualise only a genuinely unpaged long client list (50+ rows). *Why:* SpaceWorks lists run to hundreds of rows. `virtualize-lists`
- **UX-3.3 MUST** While the next page or a refetch loads, keep the last good rows and the truthful range on screen (TanStack Query `placeholderData: keepPreviousData`); never blank the table. *Where:* Staff queues and tables, Member history. `progressive-loading`
- **UX-3.4 MUST** Loading uses the one Space Works loader with a meaningful status label, or skeletons in the final geometry where a component specifies them. A skeleton never replaces the loader's status label and never implies progress. No flashing indicator for near-instant work. See [voice: loading](voice-and-content.md#empty-filtered-loading-and-success-states). `loading-states`
- **UX-3.5 SHOULD** Split code by route; lazy-load heavy editors (designers, builders, charts) and below-the-fold media; load third-party scripts async. `bundle-splitting`, `lazy-loading`, `third-party-scripts`
- **UX-3.6 SHOULD** Debounce search and filter input and throttle scroll/resize work; keep input latency under 100 ms. `debounce-throttle`, `input-latency`
- **UX-3.7 MUST** Offline and slow-network states are explicit: say what still works, what needs a connection and what is queued. Never auto-replay a payment, evidence upload or handover. *Where:* Kiosk (encrypted command queue), Staff check-in. See [voice: offline](voice-and-content.md#offline-queued-and-conflict-messages) and [§5.8 of the UX spec](ux-spec.md#58-offline-and-kiosk-integrity). `offline-support`, `network-fallback`

## 4. Style — follow the existing design system

The source's style selection, product palettes, style catalogue and `--design-system` generator are **not used**. Space Works has one style: use the tokens, components and brand rules as they are ([current rules](current-rules.md), [brand spec](ui-brand-spec.md), [components](components/README.md)). Three behaviour points survive from this category:

- **UX-4.1 MUST** One filled primary action per view region (page header, drawer footer, sticky card, callout), never pointing at the current screen. See [P11 action hierarchy](patterns/README.md#action-hierarchy). `primary-action`
- **UX-4.2 MUST** No emoji as structural icons; icons come from the one set in [brand spec §G](ui-brand-spec.md#g-icons). Text glyphs in microcopy ("✓ Available", "↗") follow [microcopy](ux-spec.md#132-microcopy-style). `no-emoji-icons`, `icon-style-consistent`
- **UX-4.3 MUST** Light and dark are designed and checked together; no screen ships tested in one theme only. `dark-mode-pairing`

## 5. Layout and responsive — HIGH

- **UX-5.1 MUST** Every screen is exactly one shell plus one layout (L1–L10) with its slots filled; no bespoke page grid, header or empty/error handling outside the layout. *Why:* layouts carry the responsive, empty, error and loading behaviour once. See the [patterns entry contract](patterns/README.md#entry-contract).
- **UX-5.2 MUST** No horizontal page scroll at 375 px; `viewport` allows zoom (never `maximum-scale=1` or `user-scalable=no`). Wide tables scroll inside their own keyboard-reachable container or become stacked cards under `md`. `horizontal-scroll`, `viewport-meta`
- **UX-5.3 MUST** Use the house breakpoints: **375** phone, **768** tablet, **1024** sidebar becomes drawer, **1280** desktop. Do not invent per-screen breakpoints. `breakpoint-consistency`
- **UX-5.4 MUST** On phones the header collapses to the primary action plus "⋯", drawers go full screen and the sticky primary sits at the bottom where the task is the page (handover, request cart, register). *Where:* Staff, Member. `content-priority`
- **UX-5.5 SHOULD** Use `min-h-dvh` (not `100vh`) for full-height screens so mobile browser chrome does not cut content. *Where:* Auth, Kiosk, Public. `viewport-units`
- **UX-5.6 MUST** Avoid nested scroll regions except the defined ones (sidebar body, table container, drawer body). `scroll-behavior`
- **UX-5.7 SHOULD** Long reading text keeps a readable measure (about 60–75 characters on desktop); do not run paragraphs edge to edge. *Where:* Public, help/docs, settings helpers. `line-length-control`
- **UX-5.8 MUST** Chips and badges wrap before their labels shrink; a "+3" overflow is an operable disclosure, never a hidden value. Truncated labels expose the full text to pointer and keyboard users. *Where:* Staff filters, Member tags, Public item chips. `chip-collection-reflow`, `compact-label-overflow`
- **UX-5.9 MUST** URLs, IDs, QR payloads and user-written text wrap (`overflow-wrap: anywhere` on a shrinkable child) instead of breaking the layout; never `word-break: break-all` on prose. `long-token-wrapping`
- **UX-5.10 SHOULD** Kiosk screens work in both orientations the hardware allows. `orientation-support`
- **UX-5.11 MUST** Spacing, container widths, z-index layers and gutters come from the layouts and tokens; the source's `max-w-6xl`, 4/8 pt scale and z-index example are not imported. `spacing-scale`, `container-width`, `z-index-management`

## 6. Typography and colour — follow the existing design system

Use the three families and weights in [CR-TYPE-01](current-rules.md#cr-type-01), the type scale in [brand spec §D](ui-brand-spec.md#d-typography), the token colours in [theming](theming.md), opaque text per [CR-OPACITY-01](current-rules.md#cr-opacity-01) and the dark family in [CR-DARK-01](current-rules.md#cr-dark-01). Where the source's numbers (16 px body, 1.5–1.75 line height, a 12 px floor, desaturated dark variants) differ, the brand scale and tokens win; raise a concern as a design-system issue, not a local override. Behaviour points that survive:

- **UX-6.1 MUST** Numbers in columns, money, timers and counts use tabular figures and right alignment in tables. `number-tabular`
- **UX-6.2 SHOULD** Prefer wrapping to truncation; when you must truncate, the full text is available on hover **and** focus. `truncation-strategy`
- **UX-6.3 MUST** Hierarchy comes from size, weight and spacing, not from colour alone. `visual-hierarchy`

## 7. Animation behaviour — MEDIUM

All values, curves and the catalogue are in [motion](motion.md) and [motion flow](motion-flow.md), governed by [CR-MOTION-01](current-rules.md#cr-motion-01). These rules are about *when* and *how* motion behaves.

- **UX-7.1 MUST** Motion shows what changed (a layer arriving, a move, loading, a confirmed result); if removing it loses no information, keep it short or drop it. `motion-meaning`, `excessive-motion`
- **UX-7.2 MUST** Nothing on an interaction path blocks input longer than 240 ms; motion is interruptible, and a new state replaces an in-flight one without waiting for an animation-end event. `no-blocking-animation`, `interruptible`, `cancellable-state-transitions`
- **UX-7.3 MUST** Transform and opacity only; no animated width, height, top or left, and no layout shift from motion. `transform-performance`, `layout-shift-avoid`
- **UX-7.4 MUST** Enter decelerates, exit accelerates and exits are shorter, using the shared tokens only. `easing`, `exit-faster-than-enter`, `motion-consistency`
- **UX-7.5 MUST** Product hover and press are **colour only**. The source's scale-on-press, spring physics, stagger reveals, parallax and shared-element transitions are not used in product chrome (see §11). The logo box-open is the single brand exception.
- **UX-7.6 MUST** Layers use the catalogue's motion (dialog pop, drawer from its own side, menu dropping from its trigger, sheet from its docked edge; [layers](motion.md#layers-dialogs-drawers-menus-toasts)), stay inert while closing and return focus to the opener on close. `modal-motion`
- **UX-7.7 MUST** Kiosk and TV screens zero motion distances and keep only fades; no loops outside the loader. `parallax-subtle`

## 8. Forms and feedback — MEDIUM

Copy patterns for every message here are in [voice and content](voice-and-content.md#validation-errors-and-recovery).

- **UX-8.1 MUST** Every input has a visible, persistent label; a placeholder is never the label. *Where:* all. [TextField](components/text-field.md). `input-labels`
- **UX-8.2 MUST** Mark **optional** fields inline ("Optional"); required fields carry no asterisk ([P18](ux-spec.md#p18-create-form-with-live-preview-r3)). Required evidence carries a "Required" chip before the user reaches the button. *The source suggests asterisks; Space Works wins.* `required-indicators`
- **UX-8.3 MUST** Validate on blur or submit, not on every keystroke. Show the error under its field, tied with `aria-describedby`, keep the entered value, and say what to enter. `inline-validation`, `error-placement`, `error-clarity`
- **UX-8.4 MUST** After a failed submit with several errors, show a focusable summary at the top linking to each field and move focus to it; with one error, focus the field. Inline errors stay. `error-summary`, `focus-management`
- **UX-8.5 MUST** Distinguish a validation error from a service failure. A failed fetch is never shown as an empty list: show the error block with a Retry that repeats the read. *Where:* all queues and pickers. `error-recovery`
- **UX-8.6 MUST** Write failures that may have partly succeeded say so ("Box assigned, but issue failed.") and offer recovery scoped to the remaining step. Never blindly retry a payment, evidence upload or handover. `timeout-feedback`
- **UX-8.7 MUST** Destructive or irreversible actions use a danger-tone confirmation that names the object and the consequence ("Revoke Priya's certificate? It stops verifying immediately."); the button that opens it ends in "…". Irreversible settings live in the [danger zone](patterns/README.md#danger-zone). `confirmation-dialogs`, `destructive-emphasis`
- **UX-8.8 MUST** Undo is offered only for reversible actions (inline where the row stays, toast where it leaves the view), using the awaited compensation. **Never** offer Undo for evidence, handovers, audit, payments or settlements; a correction is a new recorded operation. See [CR-CONTENT-01](current-rules.md#cr-content-01) and [P30](patterns/README.md#confirmation-undo). `undo-support`
- **UX-8.9 MUST** Toasts confirm only off-screen effects and row-leaving reversible actions; effects that stay visible confirm in place. Success toasts last **8 s** and pause while hovered or focused; errors persist. Toasts never take focus and use a polite live region. See [Toast](components/toast.md). *The source's 3–5 s is not used.* `toast-dismiss`, `toast-accessibility`
- **UX-8.10 MUST** Empty states say what is absent and the next **permitted** step; filtered-empty is different and offers "Clear filters". No Add action for a read-only role. See [P17](patterns/README.md#empty-results). `empty-states`
- **UX-8.11 MUST** When a hard rule disables the primary, say why beside it ("Add the return photo and a remark to continue."). Disabled is the opaque disabled state of [CR-DISABLED-01](current-rules.md#cr-disabled-01), not reduced opacity; read-only stays readable and labelled. `disabled-states`, `read-only-distinction`
- **UX-8.12 MUST** One save model per section: an explicit Discard/Save that appears when dirty for field groups, or instant toggles that confirm. Leaving a dirty form or closing a dirty drawer asks first. `sheet-dismiss-confirm`, `form-autosave`
- **UX-8.13 SHOULD** Use semantic input types and `autocomplete` (`email`, `tel`, `one-time-code`, `current-password`, `new-password`) so phones show the right keyboard and password managers work. `input-type-keyboard`, `autofill-support`, `password-toggle`
- **UX-8.14 SHOULD** Long or advanced options are disclosed progressively; multi-step flows show a step rail, echo each completed step's value and allow going back ([L7 FlowLayout](patterns/README.md#flow-layout)). `progressive-disclosure`, `multi-step-progress`
- **UX-8.15 MUST** IME-safe Enter: a custom Enter-to-submit handler ignores composition (`isComposing`) and there is always an explicit submit button. *Where:* chat, comments, search. `ime-composition-enter`
- **UX-8.16 MUST** Every user-facing string, including aria-labels, status words and error text, goes through Lingui as a whole sentence with named placeholders and real plurals; run `lingui extract` with the change. Dates, numbers and money use the shared formatters. See [product rules §11](product-rules.md#11-language-accessibility-themes-and-motion).

## 9. Navigation — HIGH

The app-wide rules are in [UX spec §2.0](ux-spec.md#20-app-wide-navigation-rules-all-shells); the sidebar look is [CR-SIDEBAR-01](current-rules.md#cr-sidebar-01).

- **UX-9.1 MUST** Navigation is generated from the gating source (role actions plus enabled modules), never hand-built per screen. A role sees only what it can use; the server checks again. See [product rules §4](product-rules.md#4-role-based-views) and [§3](product-rules.md#3-areas-and-modules). `nav-hierarchy`
- **UX-9.2 MUST** **One home per feature:** each destination appears under exactly one sidebar group, the same group for every role that can see it, named with the area name users know. *Why:* a page that moves between headings per role cannot be taught or documented. `navigation-consistency`
- **UX-9.3 MUST** Gated destinations are **absent, never disabled**. The exception is reports, where an unavailable report says which area enables it. *The source suggests explaining hidden destinations; Space Works hides them.* `empty-nav-state`
- **UX-9.4 MUST** Inner levels belong inside their feature: queues, filters and record detail live as tabs, filters and detail pages within the feature's page, not as new sidebar items. In-page tabs are views of one object or filters of one list, and they are URLs. `bottom-nav-top-level`
- **UX-9.5 MUST** Every key screen, tab, filter set and page number is a URL that can be shared, bookmarked and opened from a notification. A typed or bookmarked URL the role cannot use shows a clear denial; a space switch lands on the role's home instead. `deep-linking`
- **UX-9.6 MUST** Back is predictable: detail pages have a back link to the list they came from, and going back restores the list's filters, page and scroll. Never silently reset to Home. `back-behavior`, `state-preservation`, `back-stack-integrity`
- **UX-9.7 MUST** The current location is marked from the route with `aria-current="page"` and is always visible (its group auto-expands and scrolls into view). `nav-state-active`
- **UX-9.8 MUST** Sidebar counts are limited to the Inbox unread count and the Requests needs-action count; everything else is counted on its page. `tab-badge`
- **UX-9.9 MUST** Five or fewer destinations use bottom tabs on phones (front desk, member area with "More"); otherwise a drawer. Bottom tabs carry icon plus label; the desktop sidebar stays text-only. `bottom-nav-limit`, `adaptive-navigation`
- **UX-9.10 MUST** Breadcrumbs only on public sub-pages; detail pages use the back link. *The source's breadcrumb-at-three-levels rule is not used.* `breadcrumb-web`
- **UX-9.11 MUST** After a route change, focus moves to the page heading or main region and the title updates. `focus-on-route-change`
- **UX-9.12 MUST** Search is always reachable: the sidebar search trigger opens the command palette (Ctrl/⌘K) from anywhere in Staff. `search-accessible`
- **UX-9.13 MUST** Sign out and other dangerous account actions are separated from normal navigation (user menu, danger zone). `destructive-nav-separation`
- **UX-9.14 MUST** Multi-space users always see which space they are in (switcher card with space and role, or "(organization access)"); switching spaces never shows the previous space's data. Cross-venue sections say "Across venues". See [§5.7 of the UX spec](ux-spec.md#57-multi-tenant-switching).
- **UX-9.15 MUST** Modals are not used for primary navigation; a task that is the page uses a page or the task-mode shell. `modal-vs-navigation`

## 10. Charts and data — LOW (but every dashboard and report)

Series colours, edges and casings are [CR-CHART-01](current-rules.md#cr-chart-01); the source's palettes are not used. Danger is an explicit negative role, never an ordinary series.

- **UX-10.1 MUST** Match the chart to the question (trend → line, comparison → bar); no pie or donut above five categories. `chart-type`, `no-pie-overuse`
- **UX-10.2 MUST** Every chart has a visible legend near it, labelled axes with units, and a text summary or table alternative for screen readers. `legend-visible`, `axis-labels`, `data-table`, `screen-reader-summary`
- **UX-10.3 MUST** Series are distinguishable without colour (dash patterns, markers, direct labels). `pattern-texture`, `color-guidance`
- **UX-10.4 MUST** Exact values are reachable by hover, tap **and** keyboard; tooltips do not rely on hover alone. `tooltip-keyboard`, `focusable-elements`
- **UX-10.5 MUST** Charts have loading, empty ("No loans yet this month") and error-with-Retry states, never a blank axis frame or a broken chart. `loading-chart`, `empty-data-state`, `error-state-chart`
- **UX-10.6 MUST** Numbers, dates and currency on axes and labels use the shared locale formatters; time series state their granularity. `number-formatting`, `time-scale-clarity`
- **UX-10.7 SHOULD** Data tables sort with `aria-sort`; data-heavy reports offer CSV export. Stat cards above a table are also its filters. `sortable-table`, `export-option`
- **UX-10.8 SHOULD** Charts simplify on phones (fewer ticks, horizontal bars) and aggregate very large datasets with drill-down that keeps a back path. `responsive-chart`, `large-dataset`, `drill-down-consistency`

## 11. Where the source and Space Works differ

Space Works wins in every row. Do not "fix" a screen towards the source.

| Source suggestion | Space Works rule | Authority |
| --- | --- | --- |
| Toasts auto-dismiss in 3–5 s | Success 8 s, paused on hover/focus; errors persist | [Toast](components/toast.md), [P30](ux-spec.md#p30-undo-and-confirmation-behaviour-r8-r28) |
| Offer Undo for destructive or bulk actions | No Undo for evidence, handovers, audit, payments or settlements | [CR-CONTENT-01](current-rules.md#cr-content-01) |
| Disabled = 0.38–0.5 opacity | Opaque disabled state; reason shown beside the control | [CR-DISABLED-01](current-rules.md#cr-disabled-01) |
| Required fields marked with an asterisk | Optional fields marked "Optional"; no asterisk | [P18](ux-spec.md#p18-create-form-with-live-preview-r3) |
| Navigation items need icon + label | Desktop sidebar is text-only; bottom tabs use icon + label | [CR-SIDEBAR-01](current-rules.md#cr-sidebar-01) |
| Explain an unavailable destination instead of hiding it | Gated items are absent (reports explain their area) | [UX spec §5.4](ux-spec.md#54-permission-and-module-density) |
| Breadcrumbs for three or more levels | Back link on detail; breadcrumbs on public sub-pages only | [Interaction model](ux-spec.md#131-interaction-model-summary) |
| Spring physics, scale on press, stagger, parallax, shared-element transitions | Colour-only hover and press; token curves 120/180/240 ms | [CR-MOTION-01](current-rules.md#cr-motion-01), [motion](motion.md#rules) |
| 44 pt / 48 dp targets | 44 px web, 56 px kiosk, 48 dp Android, 44 pt iOS | [Accessibility](accessibility.md#wcag-minimums-and-stronger-house-rules) |
| Breakpoints 375 / 768 / 1024 / 1440 | 375 / 768 / 1024 / 1280 | [UX spec §1A](ux-spec.md#1a-reusable-layouts-closed-set--every-screen-composes-exactly-one) |
| Dark mode = desaturated tonal variants | One neutral black family; bright brand fills identical in both themes | [CR-DARK-01](current-rules.md#cr-dark-01), [CR-STATUS-01](current-rules.md#cr-status-01) |
| Product palettes, font pairings, style catalogue | Space Works tokens, three families, one style | [Current rules](current-rules.md) |
| Accessible chart palettes from the dataset | Five bright series with edges and casings | [CR-CHART-01](current-rules.md#cr-chart-01) |
| 16 px body, 1.5–1.75 line height, 12 px floor | Brand type scale | [Brand spec §D](ui-brand-spec.md#d-typography) |

The source's native-app tables (haptics, Dynamic Island, iOS/Android navigation idioms) apply only to the native apps, through their own [adoption guides](adoption/README.md).

---

## Pre-delivery UX checklist

Run it per screen, beside the [UX quality bar](ux-spec.md#4-ux-quality-bar-every-screen-app-wide-implementation-must-pass-every-applicable-item) and the [accessibility test scripts](accessibility.md#test-scripts). It replaces the source's native-app checklist for web work.

**Roles, areas and spaces**
- [ ] Checked as every role that can reach the screen, including the narrow consoles (front desk, machine-only, organisation-derived access) and a custom role holding only this feature's actions.
- [ ] Checked with the feature's area switched off: no nav item, tab, widget, search hit, report row or dead link remains.
- [ ] The feature has one home in the sidebar, under the same group for every role.
- [ ] As a multi-space user: the switcher shows space and role; switching lands on the role's home and shows no rows from the previous space.
- [ ] A bookmarked URL the role cannot use shows the denial, not a crash or an empty page.

**Queues, filters and detail pages**
- [ ] Lists page on the server ("1–24 of 248"); the last good rows stay while the next page loads; a stale last page recovers with Previous.
- [ ] Filters, tab and page live in the URL; back from a detail page restores them and the scroll position.
- [ ] Empty, filtered-empty (with "Clear filters"), loading, error-with-Retry and offline states are all distinct. A failed fetch is never shown as empty.
- [ ] Each row has one inline next step; the rest is in the row menu. Bulk actions use the sticky bulk bar and confirm when irreversible.
- [ ] Detail pages: back link, identity, title, status word, meta line; tabs are URLs; gated tabs are absent.

**Forms, actions and feedback**
- [ ] Visible labels; optional fields marked; errors under fields on blur/submit; error summary after a multi-error submit.
- [ ] Every mutation has a pending label, disables only its own control and cannot double-submit.
- [ ] Destructive actions confirm with object and consequence; no Undo on evidence, handovers, audit, payments or settlements.
- [ ] Disabled primaries say why; partial failures say what was saved.
- [ ] Every new string is a Lingui message (whole sentence, named placeholders, real plurals), `lingui extract` has been run, and the screen was viewed in a second locale or pseudo-locale for overflow.

**Themes, motion and devices**
- [ ] Viewed and contrast-checked in **light and dark** separately, including hover, focus, disabled and error states.
- [ ] Reduced motion set before load: still equivalents, no loops, nothing blocks input.
- [ ] 375 px phone with no horizontal page scroll; 768 tablet; 1024 drawer switch; 1280 desktop; kiosk at its real size with 56 px targets.
- [ ] 200% text and 400% zoom without lost content; forced colours keep borders and focus.

**Keyboard and assistive technology**
- [ ] Full task by keyboard; focus visible and never hidden by sticky UI or toasts; Escape closes layers and returns focus.
- [ ] Icon-only controls named; status changes announced once; route changes move focus to the page heading.
- [ ] Sign-in and recovery work with a password manager and pasted codes.

**Wiring**
- [ ] Every user-reachable action has a screen (no API-only feature that users are told exists), and every screen is reachable from navigation, a link or a notification.
- [ ] Error boundaries catch a crashing screen with a friendly card and a reload, not a white page.
- [ ] Help article and docs updated with light and dark screenshots when what people see or do changed ([product rules §11](product-rules.md#11-language-accessibility-themes-and-motion)).
