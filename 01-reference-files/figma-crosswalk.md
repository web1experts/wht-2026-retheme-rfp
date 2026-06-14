# Template ↔ Figma crosswalk

> **Disclaimer:** This is a **living reference** — WindhorseTour’s mapping at RFP issue, not part of the contract. Figma and templates may change. The **[RFP](../00-rfp/RFP-2026-path-d-block-theme-retheme.md)** (§2, §9) wins if anything conflicts. Validate frames and template names in Figma and the codebase after access.

Maps **§2** theme templates to Figma frame IDs in the [WHT Design System](https://www.figma.com/design/NsELpT3ljQd9jVgvbfk2P1/WHT-Design-System). HTML previews: [`00-new-theme-mockup/`](00-new-theme-mockup/).

| Theme template | Figma frame(s) | Milestone (§9) |
|----------------|----------------|----------------|
| `front-page.php` | `04.00` | M4 |
| `single-trip.php` (private tour PDP) | `00.00` | M1 |
| `single-trip.php` (group tour PDP) | `00.01` | M2 |
| `page-inquiry-confirmation.php` | — | M1 |
| `page-tailor-made.php` | — | M2 |
| `page-china-travel-guide.php` | `01.00` | M3 |
| `page-travel-guide-archive.php` | `01.01` | M3 |
| `taxonomy-travel_tip_category.php` | `02.00` · `02.01` | M3 |
| `single-travel-tips.php` | `02.02` | M3 |
| `level1-landing-page.php` | `03.00` · `03.01` | M6 |
| `single-tour-landing-page.php` | — | M6 |
| `page-attractions.php` | — | M6 |
| `single-attraction.php` | — | M6 |
| Global chrome (header, footer, nav) | `20.00` | M0 |
| `page-blog.php` · `single.php` | `20.00` where applicable | M7 |
| `archive-trip.php` | — | M5 |
| `template-srp.php` | — | M5 |
| `page-search.php` | — | M5 |
| FAQ suite (`page-faq.php`, category, search, `single-faq.php`) | — | M7 |
| `page-shortlist.php`, `page.php`, sidebar layouts, `404.php` | — | M7 |

Design tokens and component registry: **`wht-figma`** (access after NDA if needed).
