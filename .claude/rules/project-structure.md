---
autoload: true
maturity: poc
---

# ADD Rule: Project Structure

Every ADD project follows a standard directory layout. Consistency means agents know where things are without discovery.

## This Project's Layout

```
my-first-ai-project/
│
├── index.html                      # Main app entry point
├── css/                            # Stylesheets
├── js/                             # JavaScript modules
│
├── .add/                           # ADD methodology state (COMMITTED TO GIT)
│   ├── config.json                 # Project configuration
│   ├── learnings.md                # Project-specific agent knowledge base
│   ├── retros/                     # Retrospective archives
│   └── away-logs/                  # Away session archives (NOT committed)
│
├── .claude/                        # Claude Code configuration (COMMITTED)
│   ├── settings.json               # Permissions, status line
│   └── rules/                      # ADD methodology rules
│
├── docs/                           # Project documentation
│   ├── prd.md                      # Product Requirements Document
│   ├── plans/                      # Implementation plans
│   └── milestones/                 # Milestone tracking
│
├── specs/                          # Feature specifications
│   └── {feature}.md                # One spec per feature
│
├── tests/                          # Test artifacts
│   ├── screenshots/                # E2E visual verification
│   │   ├── {feature}/              # Organized by feature
│   │   └── errors/                 # Failure screenshots (NOT committed)
│   ├── e2e/                        # Playwright tests
│   ├── unit/                       # Unit tests (Jest)
│   └── integration/                # Integration tests
│
├── .github/workflows/              # GitHub Actions CI/CD
│   └── deploy.yml                  # Auto-deploy to GitHub Pages
│
├── CLAUDE.md                       # Project context for Claude
├── CHANGELOG.md                    # Keep a Changelog format
└── .gitignore                      # Git exclusions
```

## What Gets Committed

Everything EXCEPT:

```gitignore
.add/away-logs/           # Ephemeral
tests/screenshots/errors/ # Debugging artifacts
node_modules/             # Dependencies
.env*                     # Secrets
```

These MUST be committed (agents on other devices need them):
- `.add/config.json`, `.add/learnings.md`, `.add/retros/`
- `docs/prd.md`, `docs/plans/`, `specs/`
- `tests/screenshots/{feature}/` (passing visual evidence)
- `.claude/settings.json`, `.claude/rules/`

## Cross-Project Persistence

```
~/.claude/add/
├── profile.md                  # User preferences
├── library.md                  # Cross-project knowledge
└── projects/                   # Project index
    └── habit-tracker.json      # This project's snapshot
```

## Directory Creation Rules

- Skills MUST NOT create directories ad-hoc — use the established structure
- Feature-specific subdirectories under `tests/screenshots/` are created by the test-writer when the first test for that feature is written
