---
autoload: true
maturity: alpha
---

# ADD Rule: Quality Gates

Quality gates are checkpoints that code must pass before advancing. They are non-negotiable.

## Gate Levels

### Gate 1: Pre-Commit (every commit)

- [ ] Linter passes (`npx eslint .`)
- [ ] No merge conflicts
- [ ] No secrets or credentials in staged files
- [ ] No large files (> 1MB) accidentally staged

### Gate 2: Pre-Push (every push to remote)

- [ ] All unit tests pass (`npx jest`)
- [ ] Test coverage meets threshold (80% — configured in `.add/config.json`)
- [ ] No failing tests on the branch

### Gate 3: CI Pipeline (every PR — GitHub Actions)

- [ ] All Gate 1 and Gate 2 checks pass
- [ ] E2E tests pass (`npx playwright test`)
- [ ] Screenshots captured if UI changes

### Gate 4: Pre-Deploy (before any deployment)

- [ ] All Gate 3 checks pass
- [ ] Spec compliance verified (every acceptance criterion has a passing test)

### Gate 5: Post-Deploy (after GitHub Pages deploy)

- [ ] GitHub Pages URL loads correctly (smoke check)
- [ ] Key user flows accessible: add habit, check off, see streak

## Quality Gate Commands

```
/add:verify          — Run Gate 1 + Gate 2 (local verification)
/add:verify --ci     — Run Gate 1 through Gate 3 (CI-level)
/add:verify --deploy — Run Gate 1 through Gate 4 (pre-deploy)
/add:verify --smoke  — Run Gate 5 only (post-deploy)
```

## Spec Compliance Verification

After implementation, verify every acceptance criterion:

```
SPEC COMPLIANCE REPORT — specs/{feature}.md
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

AC-001: {criterion}
  Status: COVERED
  Tests: {test names}

RESULT: N/N criteria covered — COMPLETE
```

A feature is not complete until every acceptance criterion has at least one passing test.

## Screenshot Protocol

For E2E tests:

```javascript
await page.screenshot({
  path: `tests/screenshots/${category}/step-${step}-${description}.png`,
  fullPage: true
});
```

On failure:
```javascript
test.afterEach(async ({ page }, testInfo) => {
  if (testInfo.status !== 'passed') {
    await page.screenshot({
      path: `tests/screenshots/errors/${testInfo.title}-${Date.now()}.png`,
      fullPage: true
    });
  }
});
```

## POC Maturity Notes

At POC maturity (this project's current level):
- Gate 1 always applies (lint, no secrets)
- TDD is encouraged but not strictly enforced
- Coverage target is aspirational (80% is the goal; lower is acceptable for early iteration)
- Promote to Alpha via `/add:retro` once MVP is shipped and tests exist
