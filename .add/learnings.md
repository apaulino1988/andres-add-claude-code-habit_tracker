# Project Learnings — Andres Paulino Daily Habit Tracker

> **Tier 3: Project-Specific Knowledge**
>
> This file is maintained automatically by ADD agents. Entries are added at checkpoints
> (after verify, TDD cycles, deployments, away sessions) and reviewed during retrospectives.
>
> This is one of three knowledge tiers agents read before starting work:
> 1. **Tier 1: Plugin-Global** (`knowledge/global.md`) — universal ADD best practices
> 2. **Tier 2: User-Local** (`~/.claude/add/library.md`) — your cross-project wisdom
> 3. **Tier 3: Project-Specific** (this file) — discoveries specific to this project
>
> **Agents:** Read ALL three tiers before starting any task.
> **Humans:** Review with `/add:retro --agent-summary` or during full `/add:retro`.

## Technical Discoveries
<!-- Things learned about the tech stack, libraries, APIs, infrastructure -->
<!-- Format: - {date}: {discovery}. Source: {how we learned this}. -->

## Architecture Decisions
<!-- Decisions made and their rationale -->
<!-- Format: - {date}: Chose {X} over {Y} because {reason}. -->

- 2026-04-09: Chose vanilla JavaScript (no framework) over React/Vue because the app is small, has no build step, and opens directly in a browser as a static file. This is the right complexity level for a habit tracker MVP.
- 2026-04-09: Chose localStorage over any backend/server because the user wants the app to work offline and share easily without sign-in. Data is per-device which is acceptable for this use case.
- 2026-04-09: Chose GitHub Pages for hosting because it's free, gives a permanent shareable URL, and auto-deploys via GitHub Actions on push to main — ideal for non-technical sharing.

## What Worked
<!-- Patterns, approaches, tools that proved effective -->

## What Didn't Work
<!-- Patterns, approaches, tools that caused problems -->

## Agent Checkpoints
<!-- Automatic entries from verification, TDD cycles, deploys, away sessions -->
<!-- These are processed and archived during /add:retro -->

## Profile Update Candidates
<!-- Cross-project patterns flagged for promotion to ~/.claude/add/profile.md -->
<!-- Only promoted during /add:retro with human confirmation -->
