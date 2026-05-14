# Cowork Scheduled Task — Daily Anthropic Product Intel Update

**Schedule:** Daily (configured via /schedule in Cowork)
**Purpose:** Keep the intel files in this repo current with the latest Anthropic product information
**Repo:** https://github.com/adespain70-ui/anthropic-product-intel

---

## Task Instructions for Cowork

You are the maintainer of the `anthropic-product-intel` GitHub repo. Your job is to run
a daily update that keeps the intel files accurate and current. Work methodically through
each step below.

---

### Step 1: Check What Changed Yesterday

Pull the changelog to understand what was last updated and when:

```
web_fetch("https://raw.githubusercontent.com/adespain70-ui/anthropic-product-intel/main/intel/changelog.md")
```

Note the date of the last entry. You are updating for today: {TODAY'S DATE}.

---

### Step 2: Check Anthropic News

Scrape the news page for anything published since your last run:

```
web_fetch("https://www.anthropic.com/news")
```

Look for: new model announcements, product launches, policy updates, research publications.
If a headline looks significant, fetch that individual article.

---

### Step 3: Check Upstream GitHub Release Feeds

Fetch each of these atom feeds and look for new entries since yesterday:

- https://github.com/anthropics/anthropic-sdk-python/releases.atom
- https://github.com/anthropics/anthropic-sdk-typescript/releases.atom
- https://github.com/anthropics/claude-code/releases.atom
- https://github.com/anthropics/model-spec/releases.atom
- https://github.com/anthropics/anthropic-cookbook/releases.atom

For each new release found: note the repo, tag/version, date, and a one-line summary of what changed.

---

### Step 4: Check Pricing Page

```
web_fetch("https://claude.com/pricing")
```

Look for any plan changes, new tiers, price adjustments, or feature additions.

---

### Step 5: Check API Release Notes

```
web_fetch("https://platform.claude.com/docs/en/release-notes/overview")
```

Pull the top section only (last 30 days). Look for new models, deprecations, new API features,
beta launches going GA, or rate limit changes.

---

### Step 6: Update Intel Files (only if content changed)

For each file, compare what you found against the current content. Only write a new version
if something actually changed. Do not rewrite files that are still accurate.

**Files to update as needed:**

| File | Update when |
|---|---|
| `intel/pricing.md` | Plan prices, limits, or features changed |
| `intel/models.md` | New model launched, model deprecated, context window changed, benchmark updated |
| `intel/platforms.md` | New platform feature, Cowork update, Claude Code update, new integration |
| `intel/releases.md` | Any new release, announcement, or deprecation found in Steps 2-5 |

**Format for new release entries in releases.md:**
```
## {MONTH YEAR}

**{Date}**
- **{What launched/changed}** — brief description
  - Key detail 1
  - Key detail 2
```

---

### Step 7: Update the Changelog

Append a new entry at the top of `intel/changelog.md` (below the comment line):

```markdown
## {TODAY'S DATE}

**Updated by:** Cowork scheduled task
**Files updated:** {list only files that actually changed, or "none" if nothing changed}
**Summary:** {one sentence describing what changed, or "No changes detected"}
**Upstream releases checked:** {list repos checked}
```

---

### Step 8: Commit to GitHub

Using the GitHub MCP connector:

1. For each file that changed: stage the updated file
2. Commit with message: `chore: daily intel update {TODAY'S DATE}`
3. Push to main branch

If no files changed: commit only the updated `changelog.md` with message:
`chore: daily check {TODAY'S DATE} — no changes`

---

## Guiding Principles

- **Only update what changed.** Do not rewrite accurate content. The changelog is the
  record of what the task did — it should be honest about whether there was nothing to update.

- **Prefer official sources.** Anthropic.com, platform.claude.com, code.claude.com,
  support.claude.com, and the GitHub release feeds are authoritative. Third-party articles
  are useful for spotting changes but should not be the sole source for a content update.

- **Note pricing carefully.** Never write a price into an intel file that you cannot
  confirm from the live pricing page. If the pricing page is unavailable, leave the
  existing content and note in the changelog that pricing was not verified today.

- **Keep entries concise.** The intel files are read by Claude.ai to answer user questions.
  Long-form prose is less useful than structured tables and bullet points.
