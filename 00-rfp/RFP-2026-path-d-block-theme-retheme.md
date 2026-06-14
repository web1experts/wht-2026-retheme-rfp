# Request for Proposal (RFP)

## WindhorseTour — 2026 Website Re-theme


|                      |                                                                                                                          |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| **Questions**        | **Slack anytime** — formal Q&A window closes **7 days** after RFP issue; answers affecting all bidders posted in channel |
| **Proposal due**     | **14 days** after receiving the RFP                                                                                      |
| **Selection**        | **~1–2 weeks** after proposal due — WindhorseTour; **kickoff** at contract signing (date set then, not at bid time)      |
| **Point of contact** | **Harley** (WindhorseTour) — sole client contact                                                                         |
| **Communication**    | **Slack only** (no email) — shared channel                                                                               |


**Who we are:** A small team, not a large procurement organization. Harley is your **only** day-to-day contact. We decide quickly; we expect the same transparency from you.

Keep your proposal short **≤ 20 pages**. Answers over boilerplate.

---

## 1. What we are doing

WindhorseTour is rebranding to:

1. Ship the new UX and visual design across priority templates.
2. Protect or improve **inquiry conversion** (forms, CTAs, mobile).
3. Implement a **consistent component system** from Figma (`wht-figma`).
4. Keep the site **maintainable** in standard WordPress idioms.
5. Meet performance and accessibility bars on **WindhorseTour Lighthouse CI** and **Playwright**.

Architecture default (details in public bidding repo `**01-reference-files/`**):

1. **New WordPress block theme** with `theme.json`
2. WPTE **classic** trip templates (`wptravelengine-templates` on; FSE trip templates off)
3. **Phased production rollout** (theme router)

---

## 2. Scope of work

You are bidding to **build, test, and deploy** the re-theme. Proposals must price **all** items below. This is the contract scope — nothing is optional or deferrable unless WindhorseTour adds it by written change order.

1. **Block theme build** — Figma (`wht-figma`) → `theme.json`, design tokens, net-new CSS, build pipeline
2. **Global chrome** — header, footer, navigation (shared shell across templates)
3. **Templates** — re-theme every template file below; Figma frame IDs where design exists (see §4)
  - Home — `front-page.php` (Figma `04.00`)
  - Tour PDP — `single-trip.php` (Figma `00.00` private · `00.01` group)
  - Trip archive — `archive-trip.php`
  - Search results (SRP) — `template-srp.php`
  - Page fallback — `page.php`
  - Travel guide hub — `page-china-travel-guide.php` (Figma `01.00`)
  - Travel guide archive — `page-travel-guide-archive.php` (Figma `01.01`)
  - Travel guide category — `taxonomy-travel_tip_category.php` (Figma `02.00` · `02.01`)
  - Travel article — `single-travel-tips.php` (Figma `02.02`)
  - Level 1 landing — `level1-landing-page.php` (Figma `03.00` · `03.01`)
  - Tour landing — `single-tour-landing-page.php`
  - Attractions index — `page-attractions.php`
  - Single attraction — `single-attraction.php`
  - FAQ hub — `page-faq.php`
  - FAQ category — `page-faq-category.php` · `taxonomy-faq_category.php`
  - FAQ search — `page-faq-search.php`
  - Single FAQ — `single-faq.php`
  - Blog — `page-blog.php` · `single.php` (Figma `20.00` where applicable)
  - Inquiry confirmation — `page-inquiry-confirmation.php`
  - Tailor-made — `page-tailor-made.php`
  - Shortlist — `page-shortlist.php`
  - Site search — `page-search.php`
  - Page layouts — `page-sidebar-left.php` · `page-without-sidebar.php`
  - Not found — `404.php`
4. **WP Travel Engine (WPTE) integration** — WPTE is an **existing plugin**; tour data and booking logic already live in WPTE. Scope is **theme integration only** — classic trip templates, template overrides, and preserved enquiry/booking behavior (not plugin replacement or tour data migration)
5. **HubSpot enquiry** — port existing enquiry flows without regression
6. **Phased production rollout** — theme router; promotion through WindhorseTour environments; **phased rollout schedule** with milestone **working days from kickoff** and payment mapping
7. **Native WordPress theme** — new block theme only; preserve required behaviors (§3.1, §3.4); do not port Drupal-era patterns (§3.2; scope boundaries **Appendix A**)
8. **URL parity** — maintain custom URL field behavior (§3.1)
9. **Manual testing** — QA, staging acceptance, defect remediation
10. **Automated testing** — writing and extending Playwright specs in `wht-wp-playwright/`
11. **Handoff documentation** — template map, test matrix, runbook in `wht-wp-docs/`
12. **Staff roles required** to complete the work
13. **Total cost** — fixed bid for all scope above (submit per **Appendix B**)
14. **Overall program duration** — total **working days** from kickoff through M8 (defined **§9**)

**Deliverables:** Items 1–11 — production-ready theme, integrations, automated tests, and handoff documentation. Quality bars (Playwright, LHCI, WCAG, Figma fidelity) are **§8**. Delivery timing and payments map to **§9** and **Appendix B**.

Price all §2 scope via **Appendix B** (fixed total + phase breakdown; **Playwright automation QA priced separately** from development). A brief work-stream summary in prose is optional — no per-line hours table required. Submit your **proposed contract** as a separate PDF (or appended).

**Notes:**

- **Required bid:** block theme per §1 — full §2 scope, one fixed price and schedule (**Appendix B**). This is the primary proposal WindhorseTour will evaluate for award.
- **Optional alternative bid:** If you believe a different technical approach can deliver the same §2 outcomes (templates, WPTE, HubSpot, Playwright/LHCI acceptance, **§9** milestones), you may submit a **second fixed price and schedule** for that approach — in addition to, not instead of, the required block-theme bid. Same scope bar; explain what differs and how you still meet **§8**. WindhorseTour may evaluate it; award is not guaranteed.

---

## 3. Requirements

### 3.1 URL policy and native WordPress

**Public URLs do not change** at launch — no unapproved changes; Rank Math handles edge redirects. WindhorseTour uses a **custom URL field** for manual URLs (not WP permalink patterns for new content). That behavior must be **respected and maintained** — reimplemented idiomatically in the new theme, without Drupal-era machinery. New content URLs are created manually via the agreed field/meta, not permalink-pattern-driven.

### 3.2 Legacy theme — replace, do not migrate

The live site uses `**travelverse-child`** (legacy). That theme — PHP, CSS, JS, and everything under its `inc/` folder — is **replaced by your new block theme**, not refactored file-by-file. The new theme must be **100% native WordPress** — port **behavior** only; reimplement **idiomatically**. See **Appendix A** for bidding boundaries so scope is clear before you price §2.

**Do not carry forward into new theme code:** copy-paste from `travelverse-child`; per-post rewrite-rule generation; `flush_rewrite_rules()` on routine saves; hard-coded FAQ/regional paths; Drupal-era URL machinery instead of §3.1.

**CSS and code:** All theme CSS, PHP, and JS are **net-new** — written for the block theme from Figma / `wht-figma`, not copied or pasted from `travelverse-child` or legacy sources. Use a documented build pipeline (minification, PurgeCSS or equivalent). Propose your CSS/JS build tooling in §14.

**Proposal must include:** URL parity strategy (§3.1), metadata/SEO approach (§3.4), and one paragraph confirming **greenfield block theme** delivery per Appendix A (not legacy theme remediation).

### 3.3 Plugins, integrations, and performance

The vendor’s performance obligation is a **lean theme** (minimal CSS/JS, markup, block output) that meets **§8 LHCI floors**. Vendors may submit **written recommendations** to improve performance elsewhere (plugins, Perfmatters, Cloudflare, scripts) — WindhorseTour decides what to implement. **Do not change production plugin or CDN settings without written approval.**


| Plugin / integration                                              | Purpose                                                                                    | v1 policy                                                               |
| ----------------------------------------------------------------- | ------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------- |
| **WP Travel Engine** (core, Pro, active add-ons)                  | Tours, booking, packages, itineraries, currency, fixed dates, file downloads, user history | **Must stay** — theme integration only (§2 item 4)                      |
| **Rank Math** (+ Pro)                                             | SEO, redirects, schema, sitemap                                                            | **Must stay**                                                           |
| **ACF Pro**                                                       | Custom URL fields, content meta                                                            | **Must stay** for v1 (§3.1); vendor may propose native meta replacement |
| `**wht-wp`** (custom)                                             | Site-specific AJAX, pricing helpers                                                        | **Must stay** — vendor may extend/fix                                   |
| **HubSpot enquiry** (theme + custom code)                         | Inquiry forms, CRM sync                                                                    | **Must stay** — behavior preserved (§2 item 5)                          |
| **GTM4WP**                                                        | Google Tag Manager                                                                         | **Do not break** — config out of vendor scope                           |
| **CleanTalk**                                                     | Spam protection                                                                            | **Do not break**                                                        |
| **Mailgun**                                                       | Transactional email                                                                        | **Do not break**                                                        |
| **Perfmatters**                                                   | JS/CSS optimization (delay, RUCSS, Script Manager)                                         | **Recommend only** — WindhorseTour approves prod changes                |
| **Cloudflare**                                                    | CDN, caching, WAF                                                                          | **Recommend only** — WindhorseTour-operated                             |
| **Kinsta** (hosting + MU-plugins)                                 | Managed WordPress hosting                                                                  | **WindhorseTour-operated**                                              |
| **Contact Form 7**                                                | Legacy forms                                                                               | **Legacy** — do not expand; enquiry is HubSpot                          |
| **Smush Pro**                                                     | Image compression                                                                          | **Likely remove post-v1** — do not remove during v1 without approval    |
| **wpDataTables**                                                  | Embedded data tables                                                                       | **Must stay**                                                           |
| **TripAdvisor review widgets**                                    | Review badges / widgets                                                                    | **Likely remove post-v1**                                               |
| **Advanced Access Manager** (+ package)                           | Admin access control                                                                       | **Must stay**                                                           |
| **wp-crontrol**, **user-switching**, **Migrate DB**, **wp-sweep** | Dev / ops tooling                                                                          | **Out of vendor scope**                                                 |


**Proposal must include:** Which rows above you will touch (if any), performance recommendations with rationale, and confirmation that must-stay integrations remain working after re-theme.

### 3.4 Metadata, SEO, and FAQ markup

The new theme must output **consistent, correct metadata** on every template — not only “looks right” in the browser. WindhorseTour uses **Rank Math Pro** for SEO settings, schema, redirects, and sitemaps; the theme must **integrate with Rank Math**, not replace or fight it.

**Required on all re-themed templates (including FAQ):**

- **Document title** and **meta description** — Rank Math (or WordPress title APIs) must render as today; no duplicate, missing, or hard-coded `<title>` / description overrides in theme templates  
- **Canonical URLs** — align with §3.1; no theme output that conflicts with Rank Math canonical or custom URL behavior  
- **Open Graph / social** — where Rank Math or existing content provides tags, preserved on priority templates  
- **Heading structure** — one logical `**h1`** per page; FAQ and archive templates must not break crawlable question/answer structure  
- **FAQ surfaces** (`page-faq.php`, category, search, `single-faq.php`) — question titles, page titles, and visible Q&A content must match editor/Rank Math intent; stable FAQ URLs and listing behavior

**Acceptance:** Metadata regressions are in scope for remediation. **LHCI SEO** (§8.2) and **FAQ Playwright** coverage (§8.1, M7) are part of verification; WindhorseTour may also spot-check priority URLs on staging before milestone sign-off.

---

## 4. Environments and Tools


| Layer                         | Detail                                                                                                                                                                                                  |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Kinsta — DEV**              | `https://dev.windhorsetour.com` — deploys from `develop`                                                                                                                                                |
| **Kinsta — Staging**          | `https://stage.windhorsetour.com` — deploys from `main`                                                                                                                                                 |
| **Kinsta — Production**       | `https://windhorsetour.com` — tagged release only                                                                                                                                                       |
| **GitHub**                    | `WindhorseTour/wht-wp` — PRs to `develop`; WindhorseTour merges                                                                                                                                         |
| **Figma**                     | [WHT Design System](https://www.figma.com/design/NsELpT3ljQd9jVgvbfk2P1/WHT-Design-System?node-id=0-1&p=f&t=thbwbqovHiM5qQV2-0) — design source of truth; view via link; collaborator access per **§5** |
| **Design reference (public)** | `**01-reference-files/`** in the public bidding repository — HTML previews, template ↔ Figma crosswalk, **block-theme architecture summary (ADR)**; no NDA required to review                           |
| **Workflow (public)**         | `**05-workflow/`** in the public bidding repository — GitHub/PR workflow detail referenced by **§6.3**                                                                                                  |
| **Local**                     | Docker (`wht-wp-docker-setup/`) — full WordPress stack                                                                                                                                                  |
| **Playwright**                | `wht-wp-playwright/` → CI → `playwright.windhorsetour.com`                                                                                                                                              |
| **Lighthouse CI**             | `lhci.windhorsetour.com` — **acceptance authority**                                                                                                                                                     |


**Hosting policy:** **No external hosting** of the website is permitted at any time — no vendor-owned staging, demo, or production URLs. Vendors work on **local copies only** (Docker stack above) and WindhorseTour **DEV, staging, and production** environments. WindhorseTour provides access to the full stack (WordPress, database, CI, Playwright, LHCI) through the tools in this section.

Milestone sign-off = green on **WindhorseTour staging** automation.

---

## 5. People and access

1. **GitHub accounts** — WindhorseTour provisions an **individual GitHub account** for each person on the project. No shared logins.
2. **Proposal roster** — Your proposal must identify **each person** who will work on this project: name, role, **GitHub username (ID)**, and a brief summary of relevant experience (WordPress, WPTE, block themes, etc.).
3. **Pre-access review** — WindhorseTour reviews and approves **every person** before granting repo, Figma, or environment access. Substitutions require the same review.
4. **English** — The **project manager** (your primary integration contact with WindhorseTour) must be **fluent in spoken English**. All team members must **read and write English proficiently** (Slack, PRs, documentation, UI copy).
5. **Licenses** — WindhorseTour provides required tool licenses (Figma, etc.) for approved team members. **Do not include license costs in your bid.**

**Misrepresentation and unauthorized work:** Only **approved individuals** may perform work under their assigned WindhorseTour GitHub account. **Undisclosed subcontracting**, **impersonation**, or **work attributed to someone other than who did it** is grounds for **immediate removal from the project**, **withholding of unpaid milestone payments**, and — where WindhorseTour proves intentional misrepresentation — **recovery of costs and damages**. Work already accepted and **paid** is not clawed back solely for roster substitution errors if deliverables met §8. Disclose all subcontractors in your proposal; none may access the project without WindhorseTour approval (item 3 above).

**Materials, access, and NDA (bidding → contract):**


| Stage                   | What you get                                                                                                                                      | Requirement                                                                         |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| **Public bidding**      | This RFP, appendices, **NDA template**, and signing instructions via **public bidding materials** (URL WindhorseTour shares when you are invited) | **No NDA** required to read the RFP. Treat as confidential — do not redistribute.   |
| **Proposal**            | Consideration for next stage                                                                                                                      | Submit proposal PDF with **signed mutual NDA** (WindhorseTour template) by due date |
| **Finalist (optional)** | Read-only GitHub, Figma collaborator access                                                                                                       | Executed NDA; WindhorseTour selects finalists after proposal review                 |
| **Contract**            | WindhorseTour-provisioned GitHub accounts; full repo and environment access (§4)                                                                  | Signed contract + **per-person approval** (items 3–5 above)                         |


**NDA:** Template and **how to sign and submit** are in the **public bidding materials** only — not repeated elsewhere in this RFP. You may execute the NDA **at any time** (early access to repo, Figma, staging, DB) or **with your proposal** (required to advance). **No** repository, staging, or database access before an executed NDA. Questions during bidding: **Slack** once WindhorseTour invites you.

---

## 6. How we work together

Past projects failed on **visibility and cadence**, not only code quality. These expectations are non-negotiable.

### 6.1 Communication — Slack first


| Channel    | Use                                                                                                      |
| ---------- | -------------------------------------------------------------------------------------------------------- |
| **Slack**  | **All** questions, daily updates, blockers, file handoffs, proposal submission. **No email.**            |
| **GitHub** | Source of truth for code, issues, PRs, and **recorded decisions** (summarize Slack agreements in issues) |


**Questions:** Post anytime in the shared Slack channel — during RFP, contract, and warranty. Harley responds; answers that affect all bidders are posted in channel (formal Q&A window closes **7 days** after RFP issue; questions continue after that). **Threading:** We do not expect every conversation to be neatly threaded — post in the shared channel; use threads when helpful, not as a requirement.

**Response times:** WindhorseTour works **Monday–Friday**. If you have not received a reply within **one business day**, follow up in Slack — do not assume your message was seen.


| Do                                                    | Don't                            |
| ----------------------------------------------------- | -------------------------------- |
| Ask in **Slack** (channel or thread — either is fine) | Use email, WhatsApp, or WeChat   |
| Record decisions in **GitHub** after Slack alignment  | Let agreements live only in chat |
| Flag blockers **same day** in Slack + GitHub issue    | Surprise us at milestone review  |


During contract: WindhorseTour provides a Slack channel and GitHub label (e.g. `retheme-vendor`).

### 6.2 When you find problems


| Severity                        | Action                                                     | Timing        |
| ------------------------------- | ---------------------------------------------------------- | ------------- |
| Blocks progress                 | Slack Harley + open GitHub Issue, propose options          | Same day      |
| Wrong assumption in legacy code | Comment on issue + link finding; **do not silently copy**  | Before PR     |
| Scope creep / out-of-scope work | Stop; Slack + GitHub issue for approval                    | Before coding |
| Security or PII concern         | Slack Harley directly **and** issue (no secrets in either) | Immediate     |


**Surprises at demo = failure.** Early transparency = expected. Every blocker and scope question gets a **GitHub issue**.

### 6.3 Commits, Pushes, PRs

All work in **GitHub** — issues, branches, and PRs. WindhorseTour reviews PRs; vendor does not merge to `develop` without approval.

**Minimum (in this RFP):** **Daily commits** and **daily pushes** on active feature branches when code changes.

Everything else (issue sizing, PR content, security, net-new code rules, AI on PRs): `**05-workflow/`** in the **public bidding repository**. AI policy: **§11**.

WindhorseTour is open to **improving PR review efficiency and automation** — vendors may propose enhancements in their proposal (§14).

### 6.4 Daily report

Each active developer posts in Slack **daily** (weekdays):

- **Yesterday** — what shipped (PR links)  
- **Today** — plan  
- **Blocked** — issues + owner

### 6.5 Tooling

- **SDLC:** Proposal must describe IDE, CSS build pipeline, QC steps, and how Playwright/LHCI run in your workflow (§14). AI and agentic tools: **§11**.

---

## 7. Playwright — build with the theme

**Why Playwright:** Protect **functional consistency** through the re-theme — especially user flows for **inquiry**, **forms**, **filters**, **click-through**, and other conversion-critical paths. Visual polish is not enough; behavior must not regress.

Playwright is a **first-class deliverable**, not an end-of-project afterthought. Extend `**wht-wp-playwright/`** as each template ships.

Specs may follow theme work in a **separate PR on the same issue**, but must land within **one business day** (same day preferred). Work is not complete until tests are merged and critical paths pass on staging.

1. Use **reusable component-style** test patterns (shared fixtures, page objects, helpers) — not one-off copy-paste specs. Organize by feature area under `wht-wp-playwright/tests/`.
2. **Acceptance mapping** lives in `**wht-wp-docs/`** (repo docs), linked from tests — not a static table in this PDF.
3. Run `**npx playwright test**` locally before every PR touching UI, forms, trips, or filters.
4. **Viewports:** **Mobile and desktop required** on critical paths (inquiry, forms, filters, nav, booking) on **staging and production**; tablet optional where it adds coverage.
5. **Forms and filters:** Exercise real user controls — inputs, textareas, **selects/dropdowns**, **checkboxes**, **radio buttons**, **sliders/ranges**, date fields where present — including modal enquiry, booking, and SRP filter UI.
6. **Content-stable tests:** Prefer `**getByRole`**, `**getByLabel**`, stable IDs, and **WPTE enquiry + booking DOM contracts** — not tour names, prices, or CMS copy. Tests must pass when valid content values change.
7. **Dynamic UI:** Use polling/waits for lazy-loaded modals, enquiry forms, and filter results; shared fixtures for URLs — not brittle one-off page data.
8. **Zero tolerance** for increasing flaky tests — fix or quarantine with WindhorseTour-approved issue only.
9. Critical suite must stay **100% pass** on staging before milestone acceptance.
10. Vendor QA lead owns **weekly flake report** until cutover.

See **§8.1** (acceptance matrix by milestone).

---

## 8. Acceptance — automation and metrics

Milestone sign-off requires meeting the criteria below on **WindhorseTour staging** (and production where noted). Financial incentives and penalties for schedule and LHCI are **§9.1**.

### 8.1 Playwright (minimum matrix)

**PDP** = Product Detail Page (tour page). **PDP enquiry** = HubSpot enquiry form on the tour PDP (`tests/20-forms/`).


| Area                          | Spec area                                               | By  |
| ----------------------------- | ------------------------------------------------------- | --- |
| PDP enquiry (private)         | `tests/20-forms/`                                       | M1  |
| Inquiry confirmation          | `tests/20-forms/` (post-submit path)                    | M1  |
| PDP booking (private)         | `tests/30-tours/`                                       | M1  |
| PDP tabs/itinerary (private)  | `tests/30-tours/`                                       | M1  |
| PDP enquiry + booking (group) | `tests/20-forms/` · `tests/30-tours/` — group tour URLs | M2  |
| Tailor-made inquiry           | `tests/20-forms/`                                       | M2  |
| Travel guide surfaces         | Extend specs as M3 templates ship                       | M3  |
| Home                          | `tests/01-home-page/`                                   | M4  |
| SRP                           | `tests/42-srp-pages/`                                   | M5  |
| Landings & attractions        | Extend specs as M6 templates ship                       | M6  |
| FAQ                           | `tests/41-faq-pages/`                                   | M7  |
| Smoke                         | `tests/40-public-pages/`                                | M7  |


Critical paths: **mobile + desktop** viewports on staging and production (§7).

### 8.2 Lighthouse CI (WindhorseTour server)

Per **new-theme** URL on staging — median of 3 runs, **mobile + desktop**:


| Category                             | Floor  | Target  |
| ------------------------------------ | ------ | ------- |
| Performance                          | **90** | **100** |
| Accessibility · Best Practices · SEO | **95** | **100** |


Below floor = milestone blocked until remediated. **LHCI financial penalties:** **§9.1**.

Theme must minimize its own weight; third-party scripts are WindhorseTour-operated — document exceptions with approval.

### 8.3 Other acceptance criteria

- **WCAG 2.1 Level AA** — perceivable, operable, understandable, robust UI for keyboard and screen-reader users on all new theme output  
- **Metadata and SEO** — Rank Math–compatible titles, descriptions, canonicals, and FAQ markup per §3.4  
- **Figma fidelity** — Implement `**wht-figma` design-system components and tokens** in `theme.json`; layouts, typography, spacing, and component structure must **materially match** approved Figma frames at **1440 and 375**. WindhorseTour spot-checks priority templates at milestone sign-off. **Not** a paid ±pixel audit — **is** a bar against off-system styling, wrong or missing components, and visible design drift from Figma
- **WPTE enquiry + booking** — DOM contracts for enquiry submit and booking flow preserved  
- **No unapproved URL changes** (§3.1)

### 8.4 Defect SLAs (warranty and contract)

P0 (booking/enquiry/CI red): **4h** · P1 (LHCI floor break): **2 days** · P2: **5 days**

**Warranty:** **90 days** after final acceptance (M8) — defects per SLAs above at no additional fee.

---

## 9. Delivery schedule, milestones, and incentives

Read **§2** (scope), **§7** (Playwright), and **§8** (acceptance) before pricing the schedule below.

Vendors propose **working days from kickoff** for each milestone (**Appendix B**). Milestones below are **outcomes**, not fixed calendar weeks. **Kickoff** is set at **contract signing** — after proposal review and selection (~1–2 weeks after proposals are due). Contract milestone **due dates** = kickoff + cumulative working days from the accepted bid.

**Schedule definitions:**

- **Working day** — Monday–Friday, excluding **U.S. federal holidays** (WindhorseTour business calendar). Vendor duration bids use **cumulative working days from kickoff** (day 0 = kickoff).  
- **Calendar day / week** — natural days. **“More than 2 weeks late”** (§9.1) means more than **14 calendar days** after the agreed milestone due date.


| Phase                             | Outcome                                                                                                                                                                                                                                                       |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **M0 — Foundation**               | **Staging:** `theme.json`, design tokens, global chrome (Figma `20.00`), theme scaffold, phased theme router                                                                                                                                                  |
| **M1 — Private tour + inquiry**   | **Production:** private tour PDP (`single-trip.php`, Figma `00.00`) + chrome via theme router; `**page-inquiry-confirmation.php`** (post-submit inquiry flow)                                                                                                 |
| **M2 — Group tour + tailor-made** | **Production:** group tour PDP (`single-trip.php`, Figma `00.01`); `**page-tailor-made.php`** (tailor-made inquiry flow)                                                                                                                                      |
| **M3 — Travel guide / archives**  | **Production:** `page-china-travel-guide.php` (`01.00`), `page-travel-guide-archive.php` (`01.01`), `taxonomy-travel_tip_category.php` (`02.00` · `02.01`), `single-travel-tips.php` (`02.02`)                                                                |
| **M4 — Home**                     | **Production:** `front-page.php` (Figma `04.00`)                                                                                                                                                                                                              |
| **M5 — Listings & search**        | **Production:** `archive-trip.php`, `template-srp.php`, `page-search.php`                                                                                                                                                                                     |
| **M6 — Landings & attractions**   | **Production:** `level1-landing-page.php` (Figma `03.00` · `03.01`), `single-tour-landing-page.php`, `page-attractions.php`, `single-attraction.php`                                                                                                          |
| **M7 — FAQ, blog & remaining**    | **Production:** FAQ suite (`page-faq.php`, `page-faq-category.php`, `taxonomy-faq_category.php`, `page-faq-search.php`, `single-faq.php`), `page-blog.php` · `single.php`, `page-shortlist.php`, `page.php`, sidebar layouts, `404.php` — plus smoke coverage |
| **M8 — Cutover**                  | Final acceptance, warranty start, handoff complete                                                                                                                                                                                                            |


**Chrome** = shared header, footer, and navigation — the consistent shell across templates, not browser UI.

No prod promotion without **Playwright critical green + LHCI floors** (§8) on affected URLs.

### 9.1 Incentives and penalties

Excluding delays caused by documented WindhorseTour blockers (logged in GitHub with dates).

**On time:** Milestone accepted by the agreed date with **§8** criteria met — not **more than 2 weeks late**.

**Program completion bonuses** (percent of **total contract value**; **paid once at M8**; **aggregate cap 5%**):


| Tier  | Milestones on time | Bonus                                                    | Cumulative examples                                                     |
| ----- | ------------------ | -------------------------------------------------------- | ----------------------------------------------------------------------- |
| **1** | **M0–M2**          | **1%**                                                   | Tier 1 only → **1%**                                                    |
| **2** | **M3–M4**          | **2%** if Tier 1 earned; **1%** if Tier 1 was not earned | Tier 1 + 2 → **3%** · Tier 2 only (missed Tier 1) → **1%**              |
| **3** | **M8**             | **3%**                                                   | Adds to Tier 1–2 earnings (e.g. all three → **6%**, **paid at 5% cap**) |


Bonuses **stack** as shown. Maximum payout: **5% of total contract value**, regardless of calculated total.

**Bonus forfeiture:** If **any** milestone (M0–M8) is **more than 2 weeks late**, **all program completion bonuses are forfeited**.

**LHCI penalties:** **1% of total contract value per point** below **§8.2** floor, per category, measured on WindhorseTour LHCI server at milestone acceptance. **Aggregate LHCI penalty cap: 15% of total contract value.** No separate per-milestone late fee beyond bonus forfeiture above.

**Summary:**


| Type                         | Rate                                                                            | Cap                             |
| ---------------------------- | ------------------------------------------------------------------------------- | ------------------------------- |
| **Program completion bonus** | Tier 1 **1%** + Tier 2 **2%** (or **1%**) + Tier 3 **3%** — stacked; paid at M8 | **5% of total contract value**  |
| **Bonus forfeiture**         | Any milestone **> 2 weeks late** → all bonuses forfeited                        | —                               |
| **LHCI below floor**         | 1% of total contract value per point, per category                              | **15% of total contract value** |


Penalties apply only after failed remediation within defect SLAs (**§8.4**). WindhorseTour-caused blockers exclude bonus forfeiture and LHCI penalties for the affected period.

---

## 10. Similar work

Describe **three comparable projects** — live URLs, references WindhorseTour may contact, and what each demonstrates:

- Block theme rebuild  
- **WP Travel Engine** or comparable tour/booking plugin ([wptravelengine.com](https://wptravelengine.com/))  
- Figma / design-system implementation  
- Travel or high-consideration lead-gen (preferred)

Include **Lighthouse outcomes** and whether you used **AI tooling** on those projects. **WPTE experience is mandatory** — proposals without demonstrated WPTE (or equivalent) delivery will be deprioritized.

---

## 11. AI and agentic tooling (mandatory disclosure)

WindhorseTour uses AI internally. Vendors may use AI and **MCP-enabled tools** if disclosed and reviewed.


| Requirement           | Detail                                                                                                                                                                                               |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Pre-submit review** | Before requesting WindhorseTour review, run the prompts in `**05-workflow/pr-review-prompts.md`** (public bidding materials); paste the agent's **markdown output** into **PR comments** on every PR |
| **PR disclosure**     | Every PR states whether AI assisted (Y/N) and which tools (e.g. Copilot, Cursor, Figma AI, codegen)                                                                                                  |
| **Granularity**       | For material AI-generated blocks (>50 lines or whole files), list **files + approximate %** human-reviewed                                                                                           |
| **Design**            | Disclose any **agentic Figma-to-code** or bulk HTML conversion; WindhorseTour must know what is hand-crafted vs generated                                                                            |
| **Accountability**    | Named human approver on every merged PR — no “the bot did it”                                                                                                                                        |
| **Quality**           | AI output must meet same Playwright, LHCI, WCAG, and **no-Drupal-legacy** rules                                                                                                                      |
| **Prohibited**        | Pasting unreviewed AI dumps; hidden subcontractor AI farms without disclosure                                                                                                                        |


Proposal question: *Describe your AI policy and how you prevent unaudited generated code from reaching production.*

---

## 12. Legal — IP and third-party code


| Topic                          | Policy                                                                                                                                                                                                              |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Confidentiality**            | No portfolio/case-study use of WindhorseTour name, Figma, or URLs without written approval. NDA and access: **§5 only**.                                                                                            |
| **Subcontractors**             | Disclose all subcontractors and offshore resources in proposal; no work without WindhorseTour approval. Violations per §5 **Misrepresentation and unauthorized work**.                                              |
| **Ownership**                  | All custom work product = **WindhorseTour exclusive property** (work made for hire). Effective on payment per milestone.                                                                                            |
| **Data deletion**              | On final payment, vendor provides **written attestation** that all WindhorseTour materials (repo clones, DB dumps, Figma exports, credentials) are purged from vendor systems. WindhorseTour may verify on request. |
| **Pre-existing IP**            | Vendor lists any reusable internal libraries **before contract**. License to WindhorseTour must be perpetual, royalty-free, transferable.                                                                           |
| **Open source**                | Only licenses compatible with GPL distribution (WordPress). **SBOM or dependency list** for npm/Composer packages.                                                                                                  |
| **Third-party themes/plugins** | No sublicensed commercial themes embedded in deliverable. No “agency starter theme” encumbering WindhorseTour.                                                                                                      |
| **Reuse**                      | Borrowing from vendor past projects allowed only if disclosed and **no conflict** with other clients’ IP.                                                                                                           |


---

## 13. Documentation and decisions

- **Architecture decisions** → ADR in `wht-wp-docs/00-adrs/`  
- **Other decisions** → `wht-wp-docs/` (linked from GitHub issues)  
- **Acceptance / test matrix** → `wht-wp-docs/` + coded Playwright specs

---

## 14. Proposal requirements

We want **substance over length** — direct answers, not lengthy or fancy boilerplate. Keep the main proposal **≤ 20 pages** (contract and pricing appendices may be separate).

**Your proposal should confirm you can work under the terms in §3–§9 and §12**, or call out **any exceptions in writing** (scope, schedule incentives, penalties, IP, staging acceptance, etc.). We would rather know upfront than discover it in week three.

Submit one PDF addressing **all** items below. **Signed mutual NDA:** required — **§5 only**.

1. **Executive summary** — fixed pricing per **Appendix B** (development, manual QA, Playwright automation QA, total + phases); brief scope summary optional
2. **Team roster** — each named person, role, GitHub username (ID), and experience summary (§5); disclose all subcontractors
3. **Technical approach** — block theme (§1), WPTE classic routing, URL parity (§3.1), metadata/SEO (§3.4), greenfield delivery (§3.2, **Appendix A**), phased theme router
4. **Delivery plan** — cadence (§6), Playwright strategy (§7), LHCI approach, **working days per milestone** (Appendix B)
5. **Plugins and performance** — acknowledgment of §3.3 inventory; theme weight approach; written recommendations only for non-theme layers
6. **SDLC & tooling** — IDE, CSS build pipeline, QC steps, Playwright/LHCI in your workflow; `**05-workflow/`** (§6.3); optional PR review improvements
7. **AI policy** — answer the proposal question in **§11**
8. **Similar work** (§10) — including WPTE
9. **Commercial** — per **Appendix B**; **proposed contract** PDF; post-warranty T&M / BAU rates (required); acceptance of schedule incentives and **penalties** (**§9.1**)
10. **Risks** — short subsection. **Optional alternative bid** (§2 Notes): only if you submit a second fixed price + schedule for an alternate approach — not architecture commentary without pricing.

---

## 15. Evaluation


| Category                                                                                  | Weight |
| ----------------------------------------------------------------------------------------- | ------ |
| **Similar work** (§10; incl. WPTE and references)                                         | 25%    |
| **Price** (Appendix B; §2 scope priced clearly)                                           | 25%    |
| **Schedule** (milestone plan and dates; §9)                                               | 25%    |
| **Communication** (proposal clarity; §6 working agreements; English-speaking PM and team) | 25%    |


Technical approach, Playwright/LHCI commitment, AI disclosure, and legal terms are **requirements elsewhere in this RFP** — not separate scored categories. Shortlisted vendors: **90-minute technical interview** and **reference calls** before award.

---

## 16. Submission


|               |                                                                                                                                                              |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Where**     | **Slack** — WindhorseTour invites a shared channel when you are engaged to bid                                                                               |
| **Proposal**  | Upload PDF to Slack by **day 14** after receiving the RFP (**§14**). **Appendix B** pricing + **proposed contract** (separate PDF or appended). NDA: **§5**. |
| **Questions** | **Slack anytime** — formal Q&A window closes **day 7**; questions welcome throughout RFP and contract                                                        |
| **Format**    | PDF (≤ 20 pages + appendices)                                                                                                                                |


**No email submissions.**

Access and NDA: **§5**.

---

## Appendix A — Bidding scope (legacy theme context)

**Purpose:** Avoid mis-scoping and change orders. Read this before pricing **§2 item 7**.

The production site today runs `**travelverse-child`**. That theme (including `inc/`, templates, and CSS) is **reference only**. You deliver a **new block theme** (§2, §1). You are **not** hired to migrate, refactor, or remediate the legacy codebase file-by-file.

### Contract requirements (defined in the RFP — price once, here)


| You must deliver                                      | Defined in                |
| ----------------------------------------------------- | ------------------------- |
| All templates + chrome                                | §2 item 3 · §9 milestones |
| Custom URL field; no unapproved URL changes at launch | §3.1                      |
| Net-new theme code; behavior ported idiomatically     | §3.2                      |
| Rank Math–compatible metadata, titles, FAQ markup     | §3.4 · §3.3               |
| WPTE enquiry + booking preserved                      | §2 item 4 · §8            |
| HubSpot enquiry preserved                             | §2 item 5                 |
| Playwright + LHCI acceptance                          | §7 · §8                   |


**§2 item 7** means implementing the above in a native WordPress theme — **not** a separate “legacy audit” or `inc/` cleanup line item.

### Explicitly out of bid scope

- File-by-file work on `travelverse-child/inc/` or legacy CSS  
- Copy-pasting rewrite stacks, per-post rewrites, or `flush_rewrite_rules()` on save  
- Hard-coded regional/FAQ paths carried forward from the old theme

Use the legacy theme only to understand **behavior** WindhorseTour expects (URLs, FAQ, SRP/tour links, filters).

### Change-order boundary

Contract scope is **§2, §3, §7, §8, §9**, and agreed milestones only. Discovering Drupal-era code in the old theme **does not** expand scope unless WindhorseTour approves a **written change order**.

**Proposal (§14):** One paragraph confirming greenfield block theme delivery and how you satisfy **§3.1** and **§3.4** — not an audit of legacy files.

## Appendix B — Commercial submission template

Submit **Appendix B.1** tables in your proposal PDF (Excel optional). Submit your **proposed contract** (MSA, SOW, or equivalent) as a **separate PDF** or appended — include any material **deviations from this RFP** there or in your proposal cover letter.

### B.1 Pricing (§2 scope)

Provide **all three** tables below. **Phase prices must sum to total program price.**

**Playwright pricing:** Bid **Playwright automation QA** separately from development and manual QA in **tables 2 and 3** — do not bury in the Development column. **Total for phase** = Development + Manual QA + Playwright automation QA. Program totals must equal the sum of phase columns.

**Currency:** Bid **all prices in USD**. WindhorseTour pays from a **Chinese bank account in CNY (RMB)**. FX and invoicing mechanics are for the **executed contract** — do not rebid in another currency unless you state a material deviation.

**1. Staff hourly rates** — one row per role type you will use on this project (§2 item 12); rates in **USD**:


| Role type                     | Hourly rate | Notes (e.g. onshore/offshore, FTE %) |
| ----------------------------- | ----------- | ------------------------------------ |
| Project / account manager     |             |                                      |
| Technical lead / architect    |             |                                      |
| Senior WordPress developer    |             |                                      |
| WordPress developer           |             |                                      |
| Manual QA / test engineer     |             |                                      |
| Playwright automation engineer |             |                                      |
| Other (specify)               |             |                                      |


**2. Total program price** — fixed bid for **all** §2 scope (templates, WPTE, HubSpot, Playwright, §3 requirements, handoff, warranty period work through M8 acceptance). **Sum of the three rows below must equal total program price.**


|                              | Amount (USD) |
| ---------------------------- | ------------ |
| **Development**              |              |
| **Manual QA**                |              |
| **Playwright automation QA** |              |
| **Total program price**      |              |


**3. Price per phase** — tie payments to **§9 milestones**. **Working days** = §9 definition (cumulative from kickoff). **Total for phase** must equal the three price columns on each row.


| Phase  | Milestone outcome (§9)                                       | Development (USD) | Manual QA (USD) | Playwright automation QA (USD) | **Total for phase** (USD) | Working days from kickoff (cumulative) |
| ------ | ------------------------------------------------------------ | ----------------- | --------------- | ------------------------------ | ------------------------- | -------------------------------------- |
| **M0** | Foundation — staging: tokens, chrome, scaffold, theme router |                   |                 |                                |                           |                                        |
| **M1** | Private tour PDP + inquiry confirmation (production)         |                   |                 |                                |                           |                                        |
| **M2** | Group tour PDP + tailor-made (production)                    |                   |                 |                                |                           |                                        |
| **M3** | Travel guide / archives (production)                         |                   |                 |                                |                           |                                        |
| **M4** | Home (production)                                            |                   |                 |                                |                           |                                        |
| **M5** | Listings & search — archive, SRP, site search (production)   |                   |                 |                                |                           |                                        |
| **M6** | Landings & attractions (production)                          |                   |                 |                                |                           |                                        |
| **M7** | FAQ, blog, remaining templates + smoke (production)          |                   |                 |                                |                           |                                        |
| **M8** | Cutover, final acceptance, warranty start, handoff           |                   |                 |                                |                           |                                        |
|        | **Sum of phases (must equal table 2)**                       |                   |                 |                                |                           | **Total program (M8)**                 |


Also include in your commercial package:

- **Total working days** (§2 item 14) — must match M8 cumulative column above  
- **Earliest available start if selected** (optional) — for WindhorseTour planning only; not binding until contract  
- **Post-warranty T&M / BAU rates** (§14 item 9) — required  
- **§2 item 7** — included in total program price (not a separate legacy cleanup line item)

---

*RFP v1.16 — WindhorseTour confidential*