# Claude Models — Anthropic Product Intel

**Last updated:** 2026-05-14
**Source:** https://platform.claude.com/docs/en/about-claude/models/overview

---

## Current Recommended Models (May 2026)

| Model | API Model ID | Tier | Context Window | Max Output | Best For |
|---|---|---|---|---|---|
| Claude Opus 4.7 | `claude-opus-4-7` | Flagship | 1M tokens | 64K tokens | Complex reasoning, agentic coding, architecture decisions, large codebase analysis |
| Claude Opus 4.6 | `claude-opus-4-6` | Previous flagship | 1M tokens | 64K tokens | Graduate-level reasoning, computer use, research-grade analysis |
| Claude Sonnet 4.6 | `claude-sonnet-4-6` | Balanced | 1M tokens | 128K tokens | Daily driver for dev, writing, analysis, enterprise API; best value |
| Claude Haiku 4.5 | `claude-haiku-4-5-20251001` | Fast/Efficient | 200K tokens | 64K tokens | High-volume classification, routing, summarization, simple code edits |
| Claude Mythos Preview | Invite-only | Research | 1M tokens | — | Defensive cybersecurity (Project Glasswing; no self-serve signup) |

---

## Model Selection Guide

**Start here:** Sonnet 4.6 handles 90%+ of tasks at 40% lower cost than Opus 4.6 with nearly identical benchmark scores (SWE-bench: 79.6% vs 80.8%).

**Move to Opus 4.7 when:**
- Complex multi-file refactoring or large codebase architecture
- Long-chain planning in agentic workflows
- Graduate-level scientific reasoning (GPQA Diamond: Opus 4.6 scores 91.3%)
- Maximum image understanding (Opus 4.7 has 3x vision resolution vs 4.6)

**Use Haiku 4.5 when:**
- High-volume, low-latency, cost-sensitive tasks
- Classification, routing, customer support bots
- Subtask execution in multi-agent workflows where simple steps don't need full Sonnet

---

## Key Model Details

### Claude Opus 4.7 (launched April 16, 2026)
- Anthropic's most capable generally available model
- Step-change improvement in agentic coding over Opus 4.6
- 3x vision resolution vs Opus 4.6
- Self-verification capability
- New `xhigh` effort level (default for Opus 4.7 in Claude Code)
- Adaptive Thinking (model decides whether to think; replaces extended thinking toggle)
- 70% CursorBench coding score vs 58% for Opus 4.6
- Requires Claude Code v2.1.111 or later (`claude update` to upgrade)
- Default for Enterprise pay-as-you-go and Anthropic API users as of April 23, 2026

### Claude Sonnet 4.6 (launched February 17, 2026)
- Best value in the Claude lineup
- SWE-bench Verified: 79.6% (within 1.2 points of Opus 4.6)
- Improved agentic search performance vs Sonnet 4.5
- Extended thinking supported
- 1M context window (GA, standard pricing)
- 128K max output (higher than Opus)
- Preferred over Sonnet 4.5 by 70% of developers in evaluations

### Claude Haiku 4.5 (launched October 15, 2025)
- 97 tokens/second throughput
- 200K context window (not 1M)
- 64K max output
- SWE-bench coding average: 73.3%
- Significantly cheaper than Sonnet for high-volume use cases

---

## Context Windows

- **1M tokens:** Opus 4.7, Opus 4.6, Sonnet 4.6, Mythos Preview
- **200K tokens:** Haiku 4.5, Sonnet 4.5 (deprecated), older models
- **Claude Code (Max/Team Premium/Enterprise):** 1M on Opus 4.6+ at no surcharge, no beta header required (GA since March 2026)
- **Server-side compaction** (beta): Available for Mythos Preview, Opus 4.7, Opus 4.6, Sonnet 4.6 — auto-condenses earlier conversation to extend beyond context limits

---

## Deprecated / Retiring Models

| Model | Status |
|---|---|
| Claude Sonnet 4 (`claude-sonnet-4-20250514`) | Deprecated; API retirement June 15, 2026 |
| Claude Opus 4 (`claude-opus-4-20250514`) | Deprecated; API retirement June 15, 2026 |
| Claude Sonnet 3.7 | Retired (upgrade to Sonnet 4.6) |
| Claude Haiku 3.5 | Retired (upgrade to Haiku 4.5) |
| Claude Haiku 3 | Retired April 20, 2026 (upgrade to Haiku 4.5) |

**Migrate from Sonnet 4 → Sonnet 4.6 and Opus 4 → Opus 4.7 before June 15, 2026.**

---

## API Model Aliases (Anthropic API and Claude Platform on AWS)

| Alias | Resolves to |
|---|---|
| `opus` | Opus 4.7 |
| `sonnet` | Sonnet 4.6 |
| `haiku` | Haiku 4.5 |

Note: On Bedrock, Vertex, and Foundry, aliases resolve to older versions. Use full model names to pin specific versions on those platforms.

---

## Effort Levels (Claude Code)

Supported on Opus 4.7, Opus 4.6, and Sonnet 4.6.
Levels: `low`, `medium`, `high`, `xhigh`
- Opus 4.7 default: `xhigh`
- Opus 4.6 and Sonnet 4.6 default: `high`

The `opusplan` alias uses Opus for planning mode and auto-switches to Sonnet for execution.
