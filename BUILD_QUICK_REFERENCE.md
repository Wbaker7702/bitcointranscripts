# Build System Quick Reference

## TL;DR

**This repository contains NO build artifacts or build scripts.**

- Content-only repository (Markdown transcripts)
- Build happens in parent repo: `bitcointranscripts.github.io`
- CI/CD workflows handle validation and automation
- No local build required for contributors

## Key Files

| File | Purpose | Artifacts |
|------|---------|-----------|
| `.github/workflows/markdown-linter.yml` | Validates markdown | None |
| `.github/workflows/tweet-for-new-transcript.yml` | Auto-tweets new content | None |
| `.github/workflows/sync-parent-repo-with-submodule-updates.yml` | Syncs to parent repo | None |
| `twitter_handles.json` | Twitter handle mapping | None |
| `.gitignore` | Ignore rules | None |

## Workflow Triggers

- **Every push**: Markdown linting
- **Push to master**: Tweet + Submodule sync

## Build Process

```
This Repo (Content) → GitHub Actions → Parent Repo (Hugo) → GitHub Pages
```

## Artifacts

**None in this repository.** Site artifacts generated in parent repo.

## Commands

**None.** This repo has no build commands.

---

For detailed information, see:
- `BUILD_PLAN.md` - Comprehensive build documentation
- `BUILD_ARTIFACTS_INDEX.md` - Complete file index
