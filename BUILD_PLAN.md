# Build Plan and Artifacts Documentation

## Overview

This repository contains Bitcoin transcripts in Markdown format. The actual site build process is handled by the [bitcointranscripts.github.io](https://github.com/bitcointranscripts/bitcointranscripts.github.io) repository, which uses Hugo to generate the static site.

## Repository Structure

### Content Structure
- **Root directories**: Each directory represents a conference, podcast, or event series
- **Markdown files**: Individual transcripts (`.md`, `.es.md`, `.pt.md` for translations)
- **Index files**: `_index.md` files for Hugo navigation structure
- **Metadata**: Front matter in YAML format for Hugo

### Key Files
- `README.md` - Contribution guidelines and project documentation
- `twitter_handles.json` - Mapping of speaker names to Twitter handles
- `LICENSE.md` - Project license
- `.gitignore` - Only ignores `*.DS_Store` files

## Build Process

### Local Development
This repository does **not** contain build scripts or site generation code. The content is consumed by:
- **Hugo site**: [bitcointranscripts.github.io](https://github.com/bitcointranscripts/bitcointranscripts.github.io)
- **Submodule relationship**: This repo is used as a submodule in the Hugo site repo

### Site Generation (External)
The actual build happens in `bitcointranscripts.github.io`:
- Uses Hugo static site generator
- Processes markdown files with front matter
- Generates multilingual site (English, Spanish, Portuguese)
- Publishes to GitHub Pages

## CI/CD Workflows

### 1. Markdown Linter (`markdown-linter.yml`)
**Trigger**: On every push
**Purpose**: Validates markdown syntax and formatting
**Tools**: 
- Uses `ruzickap/action-my-markdown-linter@v1`
- Runs on `ubuntu-latest`

**Artifacts**: None (linter only)

### 2. Tweet for New Transcript (`tweet-for-new-transcript.yml`)
**Trigger**: Push to `master` branch
**Purpose**: Automatically tweets when new transcripts are added

**Process**:
1. Detects new `.md` files (excludes `_index.md`)
2. Extracts front matter (title, speakers, transcript_by, translation_by)
3. Maps names to Twitter handles via `twitter_handles.json`
4. Constructs tweet with transcript URL
5. Posts tweet via `Eomm/why-don-t-you-tweet@v1`

**Required Secrets**:
- `TWITTER_CONSUMER_API_KEY`
- `TWITTER_CONSUMER_API_SECRET`
- `TWITTER_ACCESS_TOKEN`
- `TWITTER_ACCESS_TOKEN_SECRET`

**Artifacts**: None (social media action)

**Output**: Tweet posted to @bitcoinwritings Twitter account

### 3. Sync Submodule Updates (`sync-parent-repo-with-submodule-updates.yml`)
**Trigger**: Push to `master` branch
**Purpose**: Updates the parent Hugo site repository when content changes

**Process**:
1. Sets up SSH keys for GitHub authentication
2. Checks out `bitcointranscripts.github.io` repository
3. Pulls and updates submodules recursively
4. Commits changes (if any) with message "content update"
5. Pushes to trigger Hugo site rebuild

**Required Secrets**:
- `SSH_PRIVATE_KEY` - SSH key for GitHub repository access
- `PRIVATE_TOKEN` - GitHub token for repository checkout

**Artifacts**: None (submodule sync only)

**Output**: Updates parent repository, triggering site rebuild

## Artifacts

### Build Artifacts
**None** - This repository is content-only. No build artifacts are generated here.

### Generated Content
The actual site artifacts are generated in `bitcointranscripts.github.io`:
- Static HTML files
- CSS/JS assets
- Generated site structure
- Published to GitHub Pages

### Content Files
- **Markdown transcripts**: Source content files
- **Index files**: Navigation structure (`_index.md`)
- **Metadata**: Front matter in each transcript file
- **Twitter handles**: JSON mapping file

## Dependencies

### External Dependencies
- **GitHub Actions**: CI/CD platform
- **Hugo**: Site generator (in parent repo)
- **Twitter API**: For automated tweets
- **Markdown Linter**: For content validation

### Repository Dependencies
- **Parent repo**: `bitcointranscripts/bitcointranscripts.github.io`
  - Uses this repo as a submodule
  - Handles actual site generation

## Build Commands

### None in this repository
This repository contains no build scripts. Content is consumed by the Hugo site generator in the parent repository.

### To build the site locally:
1. Clone `bitcointranscripts.github.io`
2. Initialize submodules: `git submodule update --init --recursive`
3. Run Hugo: `hugo server` (or `hugo` for production build)

## Content Structure Requirements

### Directory Structure
```
├── _index.md          # Required: Directory index with front matter
├── page-top.md        # Optional: Top-level page
└── /subdirectory      # Optional: Nested directories
    ├── _index.md      # Required: Index for nested directory
    └── transcript.md  # Transcript files
```

### Transcript File Format
- **Naming**: `YYYY-MM-DD-descriptive-name.md`
- **Front matter**: YAML front matter required:
  ```yaml
  ---
  title: Transcript Title
  transcript_by: Contributor Name
  speakers: ['Speaker One', 'Speaker Two']
  categories: ['category']
  tags: ['tag1', 'tag2']
  date: YYYY-MM-DD
  media: https://youtube.com/watch?v=...
  ---
  ```

### Translation Files
- **Spanish**: `filename.es.md`
- **Portuguese**: `filename.pt.md`
- **Front matter**: Include `translation_by` field

## Workflow Summary

```
Content Added → Git Push
    ↓
Markdown Linter (validates syntax)
    ↓
Tweet Workflow (if new transcript)
    ↓
Submodule Sync (updates parent repo)
    ↓
Parent Repo Build (Hugo generates site)
    ↓
GitHub Pages Deployment
```

## Notes

- No local build required for content contributors
- All build/deployment happens via GitHub Actions
- Content validation happens automatically on push
- Site is automatically updated when content changes
- Twitter notifications sent automatically for new transcripts
