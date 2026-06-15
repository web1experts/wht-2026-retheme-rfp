# Production stack versions

> **Disclaimer:** Living reference — versions below reflect the **`WindhorseTour/wht-wp` codebase** as committed to the repo. Production should match at deploy time; validate after access if versions matter for your bid. Policy inventory: **RFP §3.3**.

**As of:** 2026-06-15

## Maintenance notes

- WindhorseTour **generally updates all plugins in the first week of each calendar month**.
- We are **testing and migrating to WordPress 7**. Production runs WordPress **6.x** today; core may move to **7.x** during the re-theme program. Plan for regression testing after WordPress and plugin updates.

---

## WordPress core & legacy theme

| Component | Version | Notes |
|-----------|---------|--------|
| **WordPress core** | 6.9.4 | WP **7** migration in progress |
| **travelverse-child** | 1.0.0 | Legacy production theme — **reference only** (replaced by new block theme) |
| **TravelVerse** (parent) | 1.0.4 | Legacy parent theme |

---

## WP Travel Engine (core, Pro, add-ons)

| Plugin | Version |
|--------|---------|
| **WP Travel Engine** (core) | 6.8.0 |
| **WP Travel Engine Pro** (`wptravelengine-pro`) | 1.0.13 |
| Advanced Itinerary Builder | 2.2.7 |
| Cost Inclusion / Exclusion | 1.0.1 |
| Currency Converter | 1.2.3 |
| File Downloads | 2.1.1 |
| Trip Fixed Starting Dates | 2.6.8 |
| User History | 2.2.1 |

---

## Integrations & plugins (RFP §3.3)

| Plugin / integration | Version |
|----------------------|---------|
| **Rank Math** | 1.0.271.1 |
| **Rank Math Pro** | 3.0.114 |
| **ACF Pro** | 6.8.2 |
| **`wht-wp`** (custom) | in-repo |
| **HubSpot enquiry** | custom (theme + code) |
| **GTM4WP** (`duracelltomi-google-tag-manager`) | 1.22.3 |
| **CleanTalk** | 6.80 |
| **Mailgun** | 2.2.0 |
| **Perfmatters** | 2.6.3 |
| **Cloudflare** | — |
| **Kinsta** (hosting + MU-plugins) | — |
| **Contact Form 7** | 6.1.6 |
| **Smush Pro** | 4.1.0 |
| **wpDataTables** | 7.4 |
| **TripAdvisor review widgets** | 13.2.9 |
| **Advanced Access Manager** | 7.1.2 |
| **AAM Complete Package** | 7.1.0 |

### HubSpot enquiry (not a standalone plugin)

Server-side CRM capture lives in legacy theme code today (`travelverse-child/inc/functions/hubspot-crm/`) plus WordPress-side integration the vendor will update in the new theme. WindhorseTour owns HubSpot field creation; see [qa-log.md](qa-log.md) (Andrei — HubSpot forms).

---

## Kinsta MU-plugins & WindhorseTour custom MU-plugins

| Component | Version | Notes |
|-----------|---------|--------|
| **Kinsta MU-plugins** | Kinsta-managed | Hosting layer |
| **wht-wpte-override** | in-repo | WPTE currency / geo overrides |
| **wht-geo-currency-trace** | in-repo | Debug tooling (optional) |
| **migrate-inclusions-exclusions** | in-repo | One-off / migration helper |
| **wpte-currency-converter-custom** | in-repo | Currency converter extensions |

---

## Dev / ops tooling (out of vendor bid scope per §3.3)

| Plugin | Version |
|--------|---------|
| wp-crontrol | 1.21.0 |
| user-switching | 1.12.0 |
| wp-sweep | 1.1.9 |
| WP Migrate DB Pro | premium — not fully vendored in git |
| WP Migrate DB Anonymization | bundled with Migrate DB |

---

## Other plugins installed (not in §3.3 table)

| Plugin | Version | Notes |
|--------|---------|--------|
| Google Site Kit | 1.179.0 | Analytics / Search Console |
| WPMU DEV Dashboard | 4.11.30 | License / update manager (Smush, etc.) |
| Optimization Detective | installed | Partial checkout in repo |

---

*Update this page when the monthly plugin refresh lands or when WordPress 7 migration reaches staging/production.*
