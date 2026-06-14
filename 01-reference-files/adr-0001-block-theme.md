# ADR 0001: 2026 re-theme — block theme (Path D)

> **Status:** Accepted  
> **Date:** 2026-06-04  
> **Deciders:** Engineering leadership ([#2104](https://github.com/WindhorseTour/wht-wp/issues/2104) closed 2026-06-09)  
> **Related:** [#2104 — Architectural approach for re-theme](https://github.com/WindhorseTour/wht-wp/issues/2104), [#2105 — Theme rebranding analysis](https://github.com/WindhorseTour/wht-wp/pull/2105)

## Context

WindhorseTour is committed to a **major UX and visual rebrand** (Figma design system, HTML prototypes in [wht-figma](https://github.com/WindhorseTour/wht-figma), conversion-focused inquiry flows). The site runs **WordPress + WP Travel Engine (WPTE)** with substantial custom logic (enquiry, HubSpot, search/filters, custom URLs) in `travelverse-child`.

Architecture planning ([#2104](https://github.com/WindhorseTour/wht-wp/issues/2104)) evaluated multiple paths. Key constraints:

- **Business:** UX, conversion, modern design, mobile usability — not a technical rebuild for its own sake ([#2104 comment — product](https://github.com/WindhorseTour/wht-wp/issues/2104#issuecomment)).
- **Engineering:** Address critical Drupal-era debt from [#1609](https://github.com/WindhorseTour/wht-wp/issues/1609) as part of a **theme rebuild**, not an in-place reskin on legacy patterns.
- **WPTE:** Trip pages, booking, and enquiry remain plugin-driven; trip rendering uses **classic PHP templates and hooks** regardless of outer theme stack.
- **Timeline:** Q3 2026 launch target; implementation estimates for Path D and Path E (Bedrock + Sage) are **within ~5–10%** of each other (~12–17 calendar weeks, ~420–630 dev hours per [#2104](https://github.com/WindhorseTour/wht-wp/issues/2104#issuecomment)).
- **Evidence:** A Roots + WPTE spike (git tag `archive/spike-2104-roots`; branch `task/2104-roots-migration-spike`, not merged) proved WPTE parity is achievable via **theme template overrides + CSS**. Condensed learnings: `wht-wp-docs/02-theme/2026-06-re-theme/spike-learnings/`.

## Decision

We will **rebuild the public theme as a new native WordPress block theme (Path D)**:

1. **New block theme** with `theme.json` as the design-token contract, aligned to Figma / `wht-figma` (`tokens.json`, `component-registry.json`).
2. **`add_theme_support( 'wptravelengine-templates' )`** so WPTE does not hijack the template hierarchy unexpectedly.
3. **WPTE classic routing for trip surfaces** — custom `single-trip.php` (and related archive/tax templates as needed) using WPTE-documented template overrides and hooks. **`enable_fse_template` (WPTE FSE) stays off** for launch (that is Path C, not Path D).
4. **Site Editor** for marketing/content surfaces where it reduces editor friction (pages, patterns, global styles); trip PDP layout follows Figma + registry, implemented in theme templates/partials.
5. **Drop dependence on TravelVerse parent** for production; `travelverse-child` is legacy — migrate required business logic into the new theme or `wht-wp` plugin as appropriate, not a reskin.
6. **No Bedrock / Sage (Path E)** for this initiative. The Roots spike is archived at tag `archive/spike-2104-roots`; production build follows this ADR.

### In scope for the Path D build

- Design system → `theme.json` + block patterns / ACF blocks as needed
- Global chrome (header, footer, nav)
- Key templates: home, tour PDP, listings/SRP, landings, travel guide surfaces per rebrand priority
- WPTE: trips, enquiry, booking widget, packages — **behavior preserved**
- HubSpot enquiry interceptors and critical integrations (port, do not rewrite without cause)
- Playwright updates for changed selectors/URLs as templates ship

### Explicitly out of scope for this ADR (separate tracks)

- **Headless** (Path F) — not this launch
- **WPTE FSE block trip templates** (Path C) — defer; may revisit post-launch if WPTE FSE matures
- **In-place reskin** of `travelverse-child` (Path A) — rejected
- **Lighthouse 90+** — aspirational in #2104; requires a **dedicated performance program** (third-party tags, asset diet, caching), not guaranteed by theme choice alone
- **Customer portal** — aspirational; not a driver for Sage/Bedrock

## Consequences

### Positive

- Native WordPress APIs (`theme.json`, block templates, Site Editor) — broader hiring pool than Bedrock + Sage
- Clean break from TravelVerse parent and accumulated `travelverse-child` coupling
- Natural home for Figma / wht-figma tokens in `theme.json`
- Opportunity to resolve #1609 debt items during template/port work, not layer rebranding on Drupal-era patterns
- WPTE trip behavior stays on proven classic path (spike-validated pattern: overrides + CSS)

### Negative / tradeoffs

- **Full rebuild scope** (~420–600+ hours) remains large; product must still separate v1 vs v1.1 deferrals
- Block theme + classic WPTE trip templates is a **hybrid** — team must document which surfaces are Site Editor vs PHP templates
- Custom URL / rewrite / HubSpot / SRP logic must be **actively ported**; block theme does not eliminate that work
- Playwright and content QA load increases during cutover
- Team members with Sage experience will ramp on block-theme patterns instead (accepted given cost parity and hiring rationale)

### Follow-up

- [x] ADR **Accepted** — [#2104](https://github.com/WindhorseTour/wht-wp/issues/2104) closed; Path D chosen over Roots (Path E)
- [x] Roots spike archived at git tag `archive/spike-2104-roots` (branch `task/2104-roots-migration-spike` not merged)
- [ ] Create production theme slug/repo path (e.g. `wp-content/themes/wht/` or new theme name) and branch strategy from `develop`
- [ ] Publish scope doc: re-theme vs must-fix debt vs v1.1 deferrals (per product comment on #2104)
- [ ] Confirm WPTE setting: `enable_fse_template` = **no** in all environments
- [ ] Map `component-registry.json` → theme templates / `theme.json` / block patterns (crosswalk)
- [ ] Plan `travelverse-child` deprecation timeline and cutover checklist (enquiry, checkout, redirects, cache)

## Alternatives considered

| Path | Summary | Why not chosen |
|------|---------|----------------|
| **A — In-place reskin** | Figma/CSS on `travelverse-child` | Inherits #1609 debt; contradicts rebuild + “commit to WordPress” goal |
| **B — New classic theme** | PHP theme, no FSE | Loses `theme.json` / Site Editor; no advantage over D for similar effort |
| **C — Block theme + WPTE FSE** | `enable_fse_template` for trips | WPTE FSE coverage partial/unproven for our PDP; D → C possible later |
| **E — Bedrock + Sage (Roots)** | Composer layout + Blade + Vite | ~same cost as D; narrower hiring pool; spike showed no unique WPTE trip win |
| **F — Headless** | WP API + separate frontend | Implausible for Q3 2026; WPTE/booking rewrite; portal not near-term |

## Notes for implementers

- **Figma:** [WHT Design System](https://www.figma.com/design/NsELpT3ljQd9jVgvbfk2P1/WHT-Design-System)  
- **Registry / tokens:** `wht-figma/00 - Key Files/` (also mirrored under `wht-wp-docs/02-theme/00-design-system/` on design branches)  
- **WPTE template overrides:** `wp-content/themes/<theme>/wp-travel-engine/` or root templates per [WPTE developer docs](https://docs.wptravelengine.com/article/wp-travel-engine-developer-documentation/)  
- **Living docs / spikes:** `wht-wp-docs/02-theme/2026-06-re-theme/` (not superseded by this ADR; spikes are historical input)
