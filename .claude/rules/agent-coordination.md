---
autoload: true
maturity: beta
---

# ADD Rule: Agent Coordination Protocol

When multiple agents work on a project, they follow the orchestrator pattern with trust-but-verify.

## Orchestrator Role

The orchestrator (primary Claude session) is responsible for:

1. Breaking work into bounded tasks for sub-agents
2. Assigning each task with clear inputs, scope, and success criteria
3. Independently verifying sub-agent output
4. Maintaining the overall project state and progress

## Sub-Agent Dispatching

When dispatching work to a sub-agent, always provide:

```
TASK: {what to do}
SCOPE: {which files, which feature, what boundaries}
SPEC REFERENCE: {specs/{feature}.md, acceptance criteria IDs}
SUCCESS CRITERIA:
  - {testable criterion 1}
  - {testable criterion 2}
INPUT FILES: {files the agent needs to read}
OUTPUT: {what the agent should produce — files, test results, summary}
RESTRICTIONS: {what the agent should NOT do}
```

## Trust-But-Verify

After any sub-agent completes work:

1. **Read the output** — Review files changed, tests written, code produced
2. **Run tests independently** — Do NOT trust the sub-agent's test output alone
3. **Check spec compliance** — Does the output satisfy the acceptance criteria?
4. **Run quality gates** — Lint, coverage
5. **Only then** accept the work into the main branch

## WIP Limits (POC maturity — this project)

| Maturity | Max Parallel Agents | Max Features In-Progress |
|----------|--------------------|--------------------------| 
| poc | 1 | 1 |

At POC maturity: one agent at a time, one feature in progress. Coordination overhead exceeds benefit at this stage.

## Learning-on-Verify

When the orchestrator verifies sub-agent work, record what happened in `.add/learnings.md`:

```markdown
## Checkpoint: Verification Catch — {date}
- **Agent:** {test-writer|implementer|other}
- **Error:** {what went wrong}
- **Correct approach:** {what should have been done}
- **Pattern to avoid:** {generalized lesson for future work}
```

## Knowledge Tiers Before Dispatching

Before dispatching sub-agents, read all 3 knowledge tiers and include relevant lessons:

1. **Tier 1:** Plugin-global best practices
2. **Tier 2:** `~/.claude/add/library.md` — user's cross-project wisdom
3. **Tier 3:** `.add/learnings.md` — project-specific discoveries
