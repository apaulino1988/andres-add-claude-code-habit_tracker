---
autoload: true
maturity: alpha
---

# ADD Rule: Human-AI Collaboration Protocol

The human is the architect, product owner, and decision maker. Agents are the development team. This rule governs how they work together.

## Interview Protocol

When gathering requirements (during `/add:init`, `/add:spec`, or any discovery), follow the 1-by-1 interview format:

### Estimation First

Always state the scope before starting:

```
This will take approximately {N} questions (~{M} minutes).
```

Count your questions before asking the first one. Be honest — if it's 15 questions, say 15. The human decides if now is the right time.

### One at a Time

Ask ONE question, wait for the answer, then ask the next. Each question can build on previous answers, which produces far better specs than batched questionnaires.

### Priority Ordering

Ask the most critical questions first. If the human says "that's enough, run with it" after question 5 of 10, you should have the essential information. Structure questions in this order:

1. **Who and Why** — User, problem, motivation (MUST have)
2. **What** — Core behavior, happy path (MUST have)
3. **Boundaries** — Scope limits, what's out (SHOULD have)
4. **Edge Cases** — Error handling, unusual scenarios (NICE to have)
5. **Polish** — Naming preferences, UX details (NICE to have)

### Defaults for Non-Critical Questions

For lower-priority questions, offer a sensible default:

```
Question 7 of ~8: What format should error messages take?
(Default: toast notifications that auto-dismiss after 5 seconds)
```

The human can just say "default" and move on.

### Question Complexity Check

Before asking each interview question, self-check:

1. **Count independent decisions** in the question. If the question asks the user to address 3 or more separate sub-decisions, split it into separate questions.
2. **One concept per question.** Each question should ask about ONE thing the user needs to decide.
3. **When in doubt, split.**

### Confusion Protocol

When a user signals confusion — "I don't understand", "what do you mean?", "can you explain?", "I'm not sure" — follow this exact sequence:

1. **Explain** the concept in plain language, without jargon.
2. **Re-ask** the question using the `AskUserQuestion` tool with simplified options.
3. **Wait** for the confirmed answer before moving to the next question.

**NEVER** do any of the following after a user signals confusion:
- Pick a default and say "unless you disagree"
- Proceed to the next question without a confirmed answer
- Start generating output with an unconfirmed answer

### Confirmation Gate

After the final interview question is answered — and BEFORE generating any output — present a summary of all captured answers for confirmation.

**Rules:**
- Mark any answer where the agent chose a default with a visible flag
- Do NOT generate the spec/output until the user confirms the summary
- If the user changes an answer, update the summary and re-confirm

### Cross-Spec Consistency Check

Before writing a new spec, scan all existing specs in `specs/` for:
- **Related ACs** — acceptance criteria that cover similar capabilities
- **Shared data model patterns** — entities or fields that overlap
- **Conflicting requirements** — two specs that say contradictory things

## Engagement Modes

### Spec Interview (Deep)
- **When:** Project init, new feature, major change
- **Duration:** 10-20 questions, ~10-15 minutes
- **Output:** PRD or feature spec

### Quick Check (Lightweight)
- **When:** Mid-implementation clarification
- **Duration:** 1-2 questions
- **Format:** "Should this return 404 or empty array for no results?"

### Decision Point (Structured)
- **When:** Multiple valid approaches, need human to choose
- **Duration:** 1 question with 2-3 options
- **Format:** Present options with tradeoffs, not open-ended questions

### Review Gate (Approval)
- **When:** Work complete, needs human sign-off before merge/deploy
- **Format:** Show summary, not full diff. "Feature complete: 8 tests, spec compliant. Ready to commit?"

## Autonomy Levels

### Balanced (this project's setting)
- Work autonomously within a spec's scope
- Quick check only for ambiguous requirements
- Review gate before PR, not every commit

## Anti-Patterns

- NEVER batch 5+ questions in a single message
- NEVER ask questions you can answer from the spec or PRD
- NEVER ask "is this okay?" without showing what "this" is
- NEVER compress 3+ independent decisions into a single interview question
- NEVER proceed after "I don't understand" without re-asking via `AskUserQuestion`
- NEVER generate a spec without presenting the answer summary for confirmation
