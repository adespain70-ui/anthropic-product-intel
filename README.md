# anthropic-product-intel

A community-maintained, daily-updated knowledge base for Claude and Anthropic product information — structured for use as a Claude skill.

Maintained by [Anne DeSpain](https://annedespain.com) / [DeSpain Consulting](https://despain-consulting.com).

---

## What This Is

This repo provides structured, up-to-date reference files covering:

- **Pricing** — plans, API token rates, billing details
- **Models** — current lineup, capabilities, context windows, benchmarks, deprecations
- **Platforms** — Claude.ai, Claude Code, and Cowork feature comparison
- **Releases** — recent announcements, launches, and changelog from Anthropic

A Cowork scheduled task runs daily, scrapes official Anthropic sources and GitHub release
feeds, and commits updates to the intel files. The changelog records what changed (or
confirms nothing changed) every day.

---

## How It Works

```
intel/
├── changelog.md     ← read this first; tells you what changed and when
├── pricing.md       ← plans, API rates, billing
├── models.md        ← model lineup, capabilities, deprecations
├── platforms.md     ← Claude.ai / Claude Code / Cowork comparison
└── releases.md      ← recent launches and announcements

upstream/
└── watched-repos.md ← Anthropic GitHub repos monitored for releases

skill/
└── SKILL.md         ← Claude skill file; install this in your Claude account
```

---

## Using the Skill

The `skill/SKILL.md` file is a Claude skill that routes product questions to the right
intel file, fetches it with a single `web_fetch` call, and falls back to live scraping
when needed. It is designed for minimal token consumption.

**To install:** Copy the contents of `skill/SKILL.md` into a new skill in your Claude
account (Settings > Skills > New Skill).

**Raw skill URL:**
```
https://raw.githubusercontent.com/adespain70-ui/anthropic-product-intel/main/skill/SKILL.md
```

---

## Upstream Sources Monitored

Official Anthropic sources scraped daily:
- https://www.anthropic.com/news
- https://claude.com/pricing
- https://platform.claude.com/docs/en/release-notes/overview

Anthropic GitHub release feeds:
- anthropics/anthropic-sdk-python
- anthropics/anthropic-sdk-typescript
- anthropics/claude-code
- anthropics/model-spec
- anthropics/anthropic-cookbook

---

## Contributing

PRs welcome. If you spot outdated content or a missing release:
- Open an issue with the correct information and source URL
- Or submit a PR directly to the relevant intel file

Please include a source URL for any factual claims.

---

## License

Content is derived from publicly available Anthropic documentation and news.
Repo structure and skill architecture by Anne DeSpain, DeSpain Consulting LLC.
