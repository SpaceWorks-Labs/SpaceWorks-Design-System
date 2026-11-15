# What's new in v2.5.1

Design System **v2.5.1**, released 15 November 2026. A patch to [v2.5](whats-new-v2.5.md): the theme toggle's
colours, one docs-hosting rule for every product, and screenshots in both themes on the landing page and the README.

## Fixed

- **Theme toggle colours.** v2.5.0 painted the toggle's pressed state with the accent pair, so in dark it became a
  teal chip with a teal icon while every other header control stayed neutral, and in light it was a white chip with
  an ink icon: the two themes looked like "on" and "off" rather than two equal choices. The pressed rule also
  overrode hover, so hover did nothing in dark. The toggle now has one treatment in both themes: panel fill,
  control-outline boundary (3.0:1 or more against the page in light, 4.7:1 or more in dark), ink icon, and an ink
  boundary on hover. `aria-pressed` still tells assistive technology which theme is on; the sun or moon shows it.
- **No old-theme flash during the circle reveal.** The toggle's colour transition ran inside the live snapshot of the
  new theme, so for a moment the toggle was drawn in the old theme's colours at the very point the circle grows from.
  While the reveal runs, the toggle now switches its colours with the page. Tokens only.

## Changed

- **Docs live in the product, at `<domain>/docs`.** One rule for every product: the design system is served at
  `system.<domain>`; every product serves its own docs on its own domain at the `/docs` route. There is no separate
  docs site, no `docs.<domain>` and no separate docs repository. Updated in
  [product rules](product-rules.md) (hosting, §8.3, §9 and §12.1) and [delivery](delivery.md).
- **Screenshots in both themes.** The landing page has a new "In both themes" section showing the site in light and
  dark side by side, at desktop and phone widths. The README gallery shows light and dark desktop captures in their
  own columns instead of one picture that follows the reader's GitHub theme. All 48 captures in
  `screenshots/site/` were refreshed from this release's build, so the Home row shows the v2.5 landing page.

## Checked

- **Credit is to SpaceWorks Labs only.** Beyond the text files cleaned in v2.5.0, the brand guidelines PDFs (every
  compressed stream decoded, plus their document info), PNG text chunks, WebP and GIF metadata, SVG and SVGZ
  content and the font tables were searched for a personal name, handle or user path. None was found.

## Version

`VERSION` reads `2.5.1`. See [Releases](releases/README.md), [Versioning and support](releases/versioning.md) and
[Current rules](current-rules.md).
