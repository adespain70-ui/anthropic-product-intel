---
name: anthro-product-intel
description: >
  The single, complete skill for any question about Claude or Anthropic products. Use this
  skill whenever the user asks about Claude features, limits, pricing, plans, model capabilities,
  platform differences (Claude.ai chat, Claude Code, Cowork), API usage, SDK integration,
  MCP servers, latest news, research, safety, or trust/compliance. Trigger on "how does
  Claude...", "what's the difference between...", "does Claude support...", "what's new in
  Claude...", "how do I install Claude Code...", "what plan do I need...", or any question
  where accurate up-to-date Claude/Anthropic knowledge matters. Always use this skill rather
  than relying on training data memory — your training data may be outdated or wrong on
  product details.
---

# Claude Live Knowledge

The complete reference skill for all Claude and Anthropic product knowledge. Combines a
community-maintained GitHub knowledge base (updated daily by Cowork) with live scraping
of official Anthropic sources — so you always answer from fresh, accurate information
rather than potentially stale training data.

**GitHub knowledge base:**
`https://raw.githubusercontent.com/adespain70-ui/anthropic-product-intel/main/`

---

## Step 1: Check the Changelog First (Always)

Before anything else, fetch the changelog. It is a small file (~200 tokens) that tells
you what changed recently and which intel files were updated today.

```
web_fetch("https://raw.githubusercontent.com/adespain70-ui/anthropic-product-intel/main/intel/changelog.md")
```

Use the changelog to decide which intel files are worth fetching. If nothing relevant
changed recently, the intel files are still valid — fetch the one matching the question type.

---

## Step 2: Route the Question

Map the question to the right source. Use the GitHub intel file first — it is structured
for fast, low-token reads. Fall back to a live scrape only if the file is missing, stale
(older than 48 hours per the changelog), or the question requires real-time precision
(e.g., exact current pricing).

### GitHub Intel Files (fetch only the one you need)

| Question type | GitHub intel file |
|---|---|
| Pricing, plans, billing | `intel/pricing.md` |
| Models, capabilities, context windows | `intel/models.md` |
| Platform features and differences | `intel/platforms.md` |
| Recent releases, announcements, what's new | `intel/releases.md` |

Raw URL pattern:
```
https://raw.githubusercontent.com/adespain70-ui/anthropic-product-intel/main/intel/<filename>
```

### Live Scrape Sources (fallback or real-time precision)

| Question type | Primary source |
|---|---|
| Latest news, releases, announcements | https://www.anthropic.com/news |
| General product overview | https://www.anthropic.com/ |
| Research, papers, alignment work | https://www.anthropic.com/research |
| Safety, privacy, trust, compliance | https://trust.anthropic.com/ |
| Constitutional AI, model card, values | https://www.anthropic.com/constitution |
| Cowork product overview | https://claude.com/product/cowork |
| Claude.ai home / plans overview | https://claude.com/ |
| Pricing page | https://claude.com/pricing |

### Docs Navigation Sources (fetch the map, then navigate to specific pages)

| Question type | Docs map URL |
|---|---|
| Claude API, models, SDK, tool use, streaming, rate limits | https://docs.claude.com/en/docs_site_map.md |
| Claude Code install, config, MCP, Node.js requirements | https://docs.anthropic.com/en/docs/claude-code/claude_code_docs_map.md |
| Claude.ai plans, feature limits, support | https://support.claude.com |

---

## Step 3: Check Session Cache

Before fetching any URL, check whether you already retrieved it earlier in this
conversation. If the content is already in context, use it. Do not re-fetch the same
URL in the same session.

---

## Step 4: Fetch the Content

**For GitHub intel files:** Use `web_fetch` directly on the raw URL. These are plain
markdown, no JS rendering needed.

**For live Anthropic sources:**
Preferred — use Firecrawl `firecrawl_scrape` if available (handles JS-rendered pages):
```
firecrawl_scrape(url="<source_url>", formats=["markdown"])
```
Fallback — use `web_fetch` if Firecrawl is unavailable.

For docs map URLs: fetch the map first, identify the relevant specific page, then fetch
that page only. Do not bulk-fetch entire doc trees.

For the news page: scrape the index first, then fetch 1-2 individual articles only if
needed to answer the specific question.

---

## Step 5: Synthesize and Respond

- Lead with the answer — do not dump raw fetched content
- Note whether the answer came from the GitHub knowledge base or a live scrape
- Cite the source URL at the end of your response
- If a page fails to load, say so and link directly to it
- For pricing or plan questions, always direct to the live source for confirmation —
  never state prices from memory alone
- If the question spans multiple platforms, address each one

---

## Platform Differences Quick Reference

Verify against `intel/platforms.md` or live docs if details may have changed.

| | Claude.ai (chat) | Claude Code | Cowork |
|---|---|---|---|
| Primary use | Conversation, artifacts, research | Agentic coding across your codebase | Desktop task/file automation for knowledge workers |
| Interface | Web, mobile, desktop app | Terminal, VS Code, JetBrains, desktop app, web, iOS | Desktop app (macOS and Windows); mobile dispatch available on Pro and Max |
| Tools | Web search, artifacts, MCP apps | Bash, file system, git, MCP servers, CI/CD | Local files, connectors (Slack, Chrome, etc.), computer use (research preview) |
| Subagents | No | Yes (parallel sub-agents, background agents) | Yes (parallel sub-agents for complex tasks) |
| Scheduled tasks | No | No | Yes (via /schedule; requires desktop app to stay open) |
| Who it's for | General use, writing, analysis | Software developers (all skill levels) | Non-technical knowledge workers: researchers, analysts, operations, legal, finance |
| Requires | Any plan (Free has limits) | Pro, Max, Team, or Enterprise | Pro, Max, Team, or Enterprise; desktop app required |
| Key feature | Projects, artifacts, MCP connectors | CLAUDE.md context files, Agent Teams | Plugins, scheduled tasks, Projects with memory, mobile dispatch |

---

## Plans Quick Reference

Always verify current pricing at https://claude.com/pricing — never state prices from memory.

| Plan | Who it's for | Claude Code | Cowork | Notes |
|---|---|---|---|---|
| Free | Casual users | No | No | Usage limits apply |
| Pro | Individuals (~$20/mo) | Yes | Yes | 5x usage vs Free; Claude Code + Cowork consume limits faster |
| Max 5x | Power users (~$100/mo) | Yes | Yes | 5x more usage than Pro |
| Max 20x | Daily heavy users (~$200/mo) | Yes | Yes | 20x more usage than Pro; priority access to new features |
| Team | Organizations ($20-$25/seat/mo) | Yes | Yes | Min 5 seats; Standard and Premium seat tiers; per-member limits |
| Enterprise | Large orgs (custom) | Yes | Yes | SSO, domain capture, spend controls, SIEM/OpenTelemetry for Cowork |

Note: Claude paid plans and the Claude API/Console are **separate products** with separate
billing. A Pro subscription does not include API access.

Extra usage: Pro, Max 5x, and Max 20x subscribers can enable pay-as-you-go extra usage
after hitting session limits (Settings > Usage).

---

## Quick Reference: Key URLs

| Resource | URL |
|---|---|
| Claude home | https://claude.com/ |
| Cowork product page | https://claude.com/product/cowork |
| Pricing | https://claude.com/pricing |
| Max plan | https://claude.com/pricing/max |
| Team plan | https://claude.com/pricing/team |
| Claude API docs | https://docs.claude.com/en/api/overview |
| Claude Code docs | https://code.claude.com/docs/en/overview |
| Claude.ai support | https://support.claude.com |
| Cowork getting started | https://support.claude.com/en/articles/13345190-get-started-with-claude-cowork |
| Product news | https://www.anthropic.com/news |
| Enterprise sales | https://www.anthropic.com/contact-sales |
| npm (Claude Code) | https://www.npmjs.com/package/@anthropic-ai/claude-code |
| GitHub knowledge base | https://github.com/adespain70-ui/anthropic-product-intel |
