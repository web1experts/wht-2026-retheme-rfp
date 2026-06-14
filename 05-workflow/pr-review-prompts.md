# PR review — AI prompts

**Required (RFP §11):** Before requesting WindhorseTour review on a PR, run these prompts with your AI tooling. Paste the agent's **full markdown output** into the **PR comment section** on every PR.

Adapt tool-specific instructions (Cursor, Copilot, etc.) as needed. The checklist and output format below are the contract.

---

You are reviewing a PR for the WindhorseTour WordPress repo (`WindhorseTour/wht-wp`).

# PR Review

**When reviewing:** Read the linked GitHub issue and verify the PR against ticket scope and acceptance criteria.

---

## Review Checklist

### Scope & Cost Control
- [ ] PR is linked to exactly one ticket — flag if multiple or none
- [ ] Files changed are limited to what the ticket requires — flag unrelated edits
- [ ] Warn if more than 20 files changed
- [ ] PR targets the correct base branch (`develop` for feature work — not `main` directly unless release PR)

### Acceptance Criteria
- [ ] Every acceptance criteria item in the linked ticket is satisfied
- [ ] PR description includes test steps or testing notes

### WordPress Stability
- [ ] No direct DB queries missing `$wpdb->prepare()`
- [ ] No forms or AJAX handlers missing nonces
- [ ] No changes to `functions.php` or core plugin files without explicit ticket scope
- [ ] No risky use of `update_option()` / `delete_option()` on unfamiliar keys
- [ ] Scripts/styles enqueued via `wp_enqueue_*` (no raw `<script>` tags)
- [ ] No hardcoded URLs or credentials

### CRM Integration (flag for extra scrutiny)
- [ ] Any changes touching HubSpot, n8n, or webhook endpoints noted
- [ ] Webhook endpoints are authenticated
- [ ] All external API calls wrapped in error handling (try/catch)

### Code Quality
- [ ] No obvious bugs, edge cases, or missing error handling
- [ ] Follows WordPress/PHP coding standards
- [ ] No debug code, `console.log`, or commented-out code left in
- [ ] No unnecessary whitespace changes or unrelated refactors

### PR Hygiene
- [ ] Clear, descriptive title and PR description
- [ ] Linked ticket referenced in PR body
- [ ] No unresolved review comments

### Re-theme specific (RFP)
- [ ] No copy-paste of CSS, PHP, or JS from `travelverse-child` — net-new reimplementation
- [ ] No new Drupal-era patterns; Appendix D debt not reintroduced
- [ ] Playwright / LHCI impact noted if UI changed

---

## Output Format (mandatory)

**Every PR review must include markdown pasteable into GitHub** (PR comment). Do not end with analysis-only.

End with a subsection whose heading is exactly:

`### GitHub comment (copy-paste)`

Under that heading, output **raw** GitHub Flavored Markdown (no fence wrapping the whole comment):

```markdown
## PR Review: #XXXX — [Title]

### Ticket Alignment
[Does the diff match the linked ticket scope and all acceptance criteria?]

### Stability Risks
[WordPress safety issues, CRM integration concerns — or "None"]

### Issues Found
[Bugs, standards violations, security concerns — or "None"]

### Suggestions
[Optional improvements — or "None"]

### Verdict
- [ ] ✅ Approved — safe to merge
- [ ] ⚠️ Approved with notes — minor issues, address before or after merge
- [ ] 🔁 Changes Requested — must fix before merge
- [ ] 🚫 Blocked — scope violation / stability risk
```

**Source:** Adapted from WindhorseTour engineering prompts. Canonical copy may also live in the contractor repo after access is granted.
