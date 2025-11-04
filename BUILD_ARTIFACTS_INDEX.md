# Build Artifacts and Files Index

## Build-Related Files in Repository

### Configuration Files

#### `.gitignore`
- **Location**: `/workspace/bitcointranscripts/.gitignore`
- **Purpose**: Defines ignored files
- **Contents**: Only ignores `*.DS_Store` files
- **Artifacts**: None (configuration only)

### CI/CD Workflows

#### `.github/workflows/markdown-linter.yml`
- **Type**: GitHub Actions workflow
- **Trigger**: On every push
- **Purpose**: Validates markdown syntax
- **Runs on**: `ubuntu-latest`
- **Tools Used**: `ruzickap/action-my-markdown-linter@v1`
- **Artifacts Produced**: None (validation only)
- **Output**: Linter status (pass/fail)

#### `.github/workflows/tweet-for-new-transcript.yml`
- **Type**: GitHub Actions workflow
- **Trigger**: Push to `master` branch
- **Purpose**: Automatically tweets new transcripts
- **Runs on**: `ubuntu-latest`
- **Tools Used**: 
  - `Ana06/get-changed-files@v1.2` - Detects new files
  - `Eomm/why-don-t-you-tweet@v1` - Posts tweets
- **Secrets Required**:
  - `TWITTER_CONSUMER_API_KEY`
  - `TWITTER_CONSUMER_API_SECRET`
  - `TWITTER_ACCESS_TOKEN`
  - `TWITTER_ACCESS_TOKEN_SECRET`
- **Artifacts Produced**: None (social media action)
- **Output**: Tweet posted to Twitter

#### `.github/workflows/sync-parent-repo-with-submodule-updates.yml`
- **Type**: GitHub Actions workflow
- **Trigger**: Push to `master` branch
- **Purpose**: Syncs content updates to parent Hugo site repo
- **Runs on**: `ubuntu-latest`
- **Process**:
  1. Sets up SSH authentication
  2. Checks out parent repo (`bitcointranscripts.github.io`)
  3. Updates submodules
  4. Commits and pushes changes
- **Secrets Required**:
  - `SSH_PRIVATE_KEY`
  - `PRIVATE_TOKEN`
- **Artifacts Produced**: None (sync action)
- **Output**: Updated parent repository

### Data Files

#### `twitter_handles.json`
- **Type**: JSON configuration
- **Purpose**: Maps speaker/contributor names to Twitter handles
- **Used By**: `tweet-for-new-transcript.yml` workflow
- **Format**: `{ "Name": "twitterhandle" }`
- **Artifacts**: None (data file)

### Documentation Files

#### `README.md`
- **Type**: Markdown documentation
- **Purpose**: Project documentation and contribution guidelines
- **Artifacts**: None (documentation)

#### `LICENSE.md`
- **Type**: License file
- **Purpose**: Project license information
- **Artifacts**: None (legal document)

## Build Artifacts Summary

### Generated Artifacts
**NONE** - This repository does not generate any build artifacts.

### Artifacts Generated Elsewhere
The actual site build artifacts are generated in `bitcointranscripts.github.io`:
- Static HTML files
- CSS/JavaScript assets
- Generated site structure
- Published to GitHub Pages at `https://btctranscripts.com`

## Content Files (Not Build Artifacts)

### Transcript Files
- **Pattern**: `*.md`, `*.es.md`, `*.pt.md`
- **Location**: Various directories
- **Purpose**: Content files (not build artifacts)
- **Count**: 1700+ markdown files

### Index Files
- **Pattern**: `_index.md`, `_index.es.md`, `_index.pt.md`
- **Purpose**: Hugo navigation structure
- **Count**: Multiple per directory

## Build Process Flow

```
┌─────────────────────────────────────┐
│  Content Repository (This Repo)     │
│  - Markdown files                   │
│  - No build artifacts               │
└──────────────┬──────────────────────┘
               │
               │ Git Push
               ↓
┌─────────────────────────────────────┐
│  GitHub Actions Workflows           │
│  1. Markdown Linter                 │
│  2. Tweet Workflow                  │
│  3. Submodule Sync                  │
└──────────────┬──────────────────────┘
               │
               │ Submodule Update
               ↓
┌─────────────────────────────────────┐
│  Parent Repository                  │
│  bitcointranscripts.github.io       │
│  - Hugo Site Generator              │
│  - Generates static site            │
└──────────────┬──────────────────────┘
               │
               │ Build
               ↓
┌─────────────────────────────────────┐
│  Build Artifacts                    │
│  - Static HTML                      │
│  - CSS/JS assets                    │
│  - Site structure                   │
└──────────────┬──────────────────────┘
               │
               │ Deploy
               ↓
┌─────────────────────────────────────┐
│  GitHub Pages                       │
│  https://btctranscripts.com         │
└─────────────────────────────────────┘
```

## File Search Results

### Build-Related Files Found
- ✅ `.github/workflows/markdown-linter.yml`
- ✅ `.github/workflows/tweet-for-new-transcript.yml`
- ✅ `.github/workflows/sync-parent-repo-with-submodule-updates.yml`
- ✅ `.gitignore`
- ✅ `twitter_handles.json`

### Build Scripts Found
- ❌ No Makefile
- ❌ No package.json
- ❌ No requirements.txt
- ❌ No shell scripts (.sh)
- ❌ No Python scripts (.py)
- ❌ No Dockerfile
- ❌ No build configuration files (.toml, .yaml, .yml for build)

### Transcript Files Mentioning "Build"
- Multiple transcript files discuss Bitcoin build systems, reproducible builds, etc.
- These are content files, not build artifacts

## Conclusion

This repository is a **content-only** repository with:
- ✅ CI/CD workflows for validation and automation
- ✅ Configuration files for workflows
- ❌ No build scripts
- ❌ No build artifacts
- ❌ No traditional build system

The actual build process is handled by the parent Hugo site repository.
