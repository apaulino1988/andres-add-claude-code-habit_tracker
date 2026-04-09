---
autoload: true
maturity: poc
---

# ADD Rule: Continuous Learning

Agents accumulate knowledge through structured checkpoints. Knowledge is organized in three tiers and consumed before starting work.

## Knowledge Tiers

| Tier | File | Scope |
|------|------|-------|
| **Tier 1: Plugin-Global** | `knowledge/global.md` | Universal ADD best practices |
| **Tier 2: User-Local** | `~/.claude/add/library.md` | Cross-project wisdom |
| **Tier 3: Project-Specific** | `.add/learnings.md` | This project's discoveries |

**Precedence:** Project-specific (Tier 3) > User-local (Tier 2) > Plugin-global (Tier 1).

## Read Before Work

Before starting ANY skill or command, read:

1. Tier 2: `~/.claude/add/library.md` (if exists)
2. Tier 3: `.add/learnings.md` (if exists)
3. `.add/handoff.md` (if exists — note in-progress work)

## Checkpoint Triggers

Write to `.add/learnings.md` automatically at these moments:

1. **After `/add:verify` completes** — Record pass/fail, what was fixed
2. **After a TDD cycle completes** — Record velocity, spec quality, blockers
3. **After `/add:deploy` completes** — Record environment, smoke test results
4. **After spec implementation completes** — Record overall feature learnings
5. **When a sub-agent error is caught** — Record the error and correction

## Session Handoff Protocol

Write `.add/handoff.md` automatically after:

1. Completing a major work item
2. After a commit
3. When context is getting long (20+ tool calls)
4. When switching work streams
5. When the user departs

### Handoff Format

```
# Session Handoff
**Written:** {timestamp}

## In Progress
- {what was being worked on, with file paths and step progress}

## Completed This Session
- {what got done, with commit hashes if applicable}

## Decisions Made
- {choices made this session with brief rationale}

## Blockers
- {anything that's stuck or needs human input}

## Next Steps
1. {prioritized list of what should happen next}
```

**Never ask** the human "should I update the handoff?" — just do it.

## Knowledge Store Boundaries

| Store | Purpose |
|-------|---------|
| `CLAUDE.md` | Project architecture, tech stack, conventions |
| `.add/learnings.md` | Project-specific discoveries and decisions |
| `~/.claude/add/library.md` | Cross-project wisdom |
| `.add/handoff.md` | Current session state — in progress, next steps |
