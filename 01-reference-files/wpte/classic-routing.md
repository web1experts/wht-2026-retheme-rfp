# WPTE — classic trip template routing

> **Disclaimer:** This describes WindhorseTour’s **current understanding** of WPTE + block-theme integration for bidding. It is **not** a guarantee of production behavior. Validate against your own environment, WPTE version, and the live codebase after NDA access. If you find conflicts, raise them in Slack before bid lock.

How **WP Travel Engine (WPTE)** works with the new block theme. Required for tour PDP, archive, and booking behavior in the RFP.

## Required theme settings

| Setting | Value |
|---------|--------|
| `add_theme_support( 'wptravelengine-templates' )` | **yes** — WPTE uses the theme’s `single-trip.php` |
| WPTE `enable_fse_template` | **no** — classic PHP templates, not WPTE FSE trip blocks |

## Template resolution

When `wptravelengine-templates` is supported, WordPress loads the theme’s `single-trip.php`. Theme overrides live under:

`yourtheme/wp-travel-engine/<template-name>`

Fallback: plugin `includes/templates/<template-name>` via `wte_locate_template()`.

## Single-trip hook order (do not break)

| Hook | Default callbacks |
|------|-------------------|
| `wp_travel_engine_before_trip_content` | `trip_content_wrapper_start` |
| `wte_single_trip_content` | title → gallery → content → tabs_nav → tabs_content |
| `wte_single_trip_footer` | `display_single_trip_footer` |
| `wp_travel_engine_trip_sidebar` | `trip_content_sidebar` (booking rail) |

Use WPTE hooks and documented overrides — do not replace enquiry or booking DOM (RFP §7, §8).

## Typical theme overrides

| Override | Purpose |
|----------|---------|
| `trip-content-wrapper-start.php` | Layout grid (content + booking rail) |
| `title.php` | Tour title; optional meta strip |
| `tabs-nav.php` / `tabs-content.php` | Tab set — preserve `.nb-tab-trigger` / `aria-controls` |
| Plugin settings | e.g. `related_trip_show_by=trip_types` |

## Integration notes

- **Inclusions tab:** WPTE may check legacy `cost.cost_includes` for tab visibility while add-on data lives in `trip_cost_inclusions` meta — plan a filter or documented workaround.
- **WPTE upgrades:** Pin versions and regression-test enquiry + booking after plugin updates.
