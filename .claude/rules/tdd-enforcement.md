---
autoload: true
maturity: beta
---

# ADD Rule: Test-Driven Development

All implementation follows strict TDD. The cycle is RED → GREEN → REFACTOR → VERIFY.

## The Cycle

### RED Phase — Write Failing Tests

1. Read the spec's acceptance criteria and user test cases
2. Write test(s) that assert the expected behavior
3. Run the tests — they MUST fail
4. If tests pass before implementation, the tests are wrong (testing existing behavior, not new)

### GREEN Phase — Minimal Implementation

1. Write the MINIMUM code to make failing tests pass
2. No extra features, no "while I'm here" additions
3. No optimization — just make it work
4. Run tests — they MUST pass

### REFACTOR Phase — Improve Quality

1. Clean up code without changing behavior
2. Extract functions, rename variables, remove duplication
3. Run tests after EVERY refactor — they must still pass
4. Apply project naming conventions and patterns

### VERIFY Phase — Independent Confirmation

1. Run the FULL test suite, not just new tests
2. Run linter (eslint for this project)
3. Verify spec compliance — do the changes satisfy the acceptance criteria?
4. If any gate fails, fix before proceeding

## Mandatory Rules

- NEVER write implementation before tests exist and FAIL
- NEVER skip the RED phase — "I'll add tests later" is not allowed
- NEVER commit with failing tests on the branch
- When a sub-agent implements code, the orchestrator MUST run tests independently
- Each TDD cycle should be a single, atomic commit

## Test Naming

Tests must reference the spec:

```javascript
// Unit tests (Jest)
describe('AC-001: User can add a habit', () => {
  it('should add habit to the list', ...);
});

describe('TC-001: Add habit flow', () => {
  it('step 1: type habit name in input', ...);
  it('step 2: submit the form', ...);
  it('step 3: see habit in list', ...);
});
```

## Coverage Requirements

Coverage targets are set in `.add/config.json` during project init. For this project:

- Unit tests: 80% line coverage
- Integration tests: Critical paths covered
- E2E tests: All user test cases from specs have corresponding tests
