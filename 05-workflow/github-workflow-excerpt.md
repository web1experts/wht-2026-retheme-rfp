# Vendor GitHub workflow

**Published to bidders as:** `05-workflow/` in the public bidding repository (alongside this RFP).

All work is tracked in **GitHub Issues** on WindhorseTour's **GitHub Project** board. **The vendor creates and maintains issues** — scoped for **1–2 day** completion; no multi-topic mega-issues.

**Every PR must link to an issue.** No unlinked PRs.

| Activity | Minimum expectation |
|----------|---------------------|
| **Work location** | **100%** in GitHub — every change on a branch tied to a **PR** |
| **Issues** | Vendor-created; **1–2 day** slices; on the GitHub Project board |
| **Commits** | At least **daily** on active feature branches when code changes; messages reference `#issue` |
| **Pushes** | At least **daily** per active developer when code changes |
| **PRs** | Small, issue-specific slices — **≤ ~400 lines** diff preferred; no multi-thousand-line dumps |
| **PR content** | Linked issue, test evidence, LHCI/Playwright status, **§11** AI disclosure |
| **Review** | WindhorseTour reviews all PRs; vendor does not merge to `develop` without approval |
| **Net-new code** | No copy-paste from `travelverse-child` — reimplement from Figma (RFP §3.2) |
| **Security** | No secrets in repos — GitHub Actions secrets / WindhorseTour vault patterns |

PRs must be **small enough for meaningful review**. WindhorseTour may reject and require re-split. PRs **> ~400 lines** require written approval before review.

Long-lived branches **> 5 business days** without a PR require written explanation.

**Branch naming:** `task/`, `bug/`, or `feature/` + issue number + short name.

**PR AI review prompts:** [pr-review-prompts.md](pr-review-prompts.md)
