# Upstream Anthropic Repos — Watched for Daily Updates

Cowork checks these repos daily for new releases, tags, and significant issue activity.
Each has a public release feed the task can poll without authentication.

---

## Core Repos

| Repo | What to watch | Release feed |
|---|---|---|
| anthropics/anthropic-sdk-python | Python SDK version bumps, new API features, breaking changes | https://github.com/anthropics/anthropic-sdk-python/releases.atom |
| anthropics/anthropic-sdk-typescript | TypeScript/Node SDK updates | https://github.com/anthropics/anthropic-sdk-typescript/releases.atom |
| anthropics/claude-code | Claude Code CLI releases, changelog | https://github.com/anthropics/claude-code/releases.atom |
| anthropics/model-spec | Constitution/model spec updates | https://github.com/anthropics/model-spec/releases.atom |
| anthropics/anthropic-cookbook | New recipes, integrations, example patterns | https://github.com/anthropics/anthropic-cookbook/releases.atom |

---

## What Cowork Should Pull Daily

For each repo above:
1. Check the release feed for any new entries since yesterday
2. If new release found: extract tag name, release date, and release notes summary
3. Write a one-line entry to `intel/releases.md` under today's date section
4. Update `intel/changelog.md` with a summary of what changed

For model-spec repo specifically:
- Check for commits to main, not just releases (model spec updates may not get a formal release tag)
- Pull the diff summary if there are new commits

---

## Notes on Access

All feeds above are public and require no authentication.
GitHub release atom feeds follow the pattern: `https://github.com/<org>/<repo>/releases.atom`

If a repo returns a 404 on the atom feed, it may have no releases yet — skip and log in changelog.
If Anthropic adds new public repos relevant to Claude products, add them here.
