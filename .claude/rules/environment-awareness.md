---
autoload: true
maturity: beta
---

# ADD Rule: Environment Awareness

Every project has an environment strategy defined during `/add:init`. All skills and commands must respect it.

## This Project's Environment Tier: 2 (Local + Production)

```
local → main → production (GitHub Pages)
```

- Unit and integration tests run locally
- E2E tests run locally
- Push to main triggers GitHub Actions → GitHub Pages deploy
- Quality gates: lint + tests (local) → CI (GitHub Actions) → smoke check (post-deploy)

## Environment Configuration

Defined in `.add/config.json`:

```json
{
  "environments": {
    "tier": 2,
    "local": {
      "run": "open index.html",
      "test": "npx jest",
      "e2e": "npx playwright test",
      "url": "file:///index.html"
    },
    "production": {
      "deploy_trigger": "push to main",
      "verify": ["smoke_tests"],
      "url": "TBD (yourname.github.io/habit-tracker)",
      "requires_approval": false
    }
  }
}
```

## Deployment Rules

- **Local:** Agents work freely — open index.html, run tests
- **Production:** Auto-deploys via GitHub Actions on push to main
- Post-deploy: verify the GitHub Pages URL loads correctly (smoke check)
- If deploy fails: alert the human

## Test-Per-Environment Matrix

| Test Type | Local | Production |
|-----------|-------|------------|
| Unit | Yes | No |
| Integration | Yes | No |
| E2E | Yes | No |
| Smoke | No | Yes |

## Secrets and Configuration

- No secrets needed — this is a static client-side app
- No `.env` files needed
- No backend credentials to manage
