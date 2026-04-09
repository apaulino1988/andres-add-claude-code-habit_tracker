# Andres Paulino Daily Habit Tracker

A browser-based daily habit tracker. Users add habits (e.g., "read 10 pages", "drink water"), check them off each day, and track streaks. Runs entirely in the browser using localStorage — no server, no accounts, no install required. Deployed on GitHub Pages for easy link-sharing with non-technical users.

## Methodology

This project follows **Agent Driven Development (ADD)** — specs drive agents, humans architect and decide, trust-but-verify ensures quality.

- **PRD:** `docs/prd.md`
- **Specs:** `specs/`
- **Plans:** `docs/plans/`
- **Config:** `.add/config.json`

Document hierarchy: PRD → Spec → Plan → User Test Cases → Automated Tests → Implementation

## Tech Stack

| Layer | Technology | Version |
|-------|-----------|---------|
| Markup | HTML5 | 5 |
| Styling | CSS3 | 3 |
| Logic | JavaScript | ES2022 (Vanilla — no framework) |
| Storage | localStorage | Browser API |

## Commands

### Development
```
open index.html          # Open app in browser (local dev)
npx jest                 # Run unit tests
npx playwright test      # Run E2E tests
npx eslint .             # Lint check
```

### ADD Workflow
```
/add:spec {feature}                  # Create a feature specification
/add:plan specs/{feature}.md         # Create an implementation plan
/add:tdd-cycle specs/{feature}.md    # Execute TDD cycle
/add:verify                          # Run quality gates
/add:deploy                          # Commit and deploy
/add:away {duration}                 # Human stepping away
/add:retro                           # Run retrospective
```

## Architecture

### Key Directories
```
index.html              # Main app entry point
css/                    # Stylesheets
js/                     # JavaScript modules
specs/                  # ADD feature specifications
docs/prd.md             # Product Requirements Document
docs/plans/             # ADD implementation plans
docs/milestones/        # Milestone tracking
.add/                   # ADD config and knowledge base
.add/config.json        # Project configuration
.add/learnings.md       # Agent knowledge base (auto-populates)
.github/workflows/      # GitHub Actions CI/CD
tests/                  # Unit, integration, E2E tests
tests/screenshots/      # Visual verification artifacts
```

### Environments

- **Local:** Open `index.html` directly in any browser
- **Production:** GitHub Pages — auto-deploys on push to `main` (URL TBD after repo creation)

## Quality Gates

- **Mode:** Standard
- **Coverage threshold:** 80%
- **Type checking:** N/A (Vanilla JavaScript)
- **E2E required:** Yes

All gates defined in `.add/config.json`. Run `/add:verify` to check.

## Source Control

- **Git host:** GitHub
- **Branching:** Feature branches off `main`
- **Commits:** Conventional commits (`feat:`, `fix:`, `test:`, `refactor:`, `docs:`)
- **CI/CD:** GitHub Actions — auto-deploys to GitHub Pages on push to `main`

## Collaboration

- **Autonomy level:** Balanced — work autonomously within specs, check in at PR time
- **Review gates:** PR review before merge to `main`
- **Deploy approval:** Not required (auto-deploy on merge to main)

## Branding

- **Banner:** "Andres Paulino Daily Habit Tracker using ADD and Claude Code"
- **Colors:** Light Blue (`#60B4D8`), Purple (`#7C5CBF`), Gold (`#D4AF37`)
- **Tone:** Simple, professional
- **Mobile:** Responsive, touch-friendly (min 44px tap targets)
- **Browsers:** Chrome, Firefox, Safari, Edge (latest)
