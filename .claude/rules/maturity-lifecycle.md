---
autoload: true
maturity: beta
description: "Master rule governing all ADD behavior based on project maturity level"
---

# ADD Rule: Maturity Lifecycle

This rule defines how ADD adapts to your project's stage of development. **It takes precedence over all other rules.** When maturity-lifecycle conflicts with another rule, maturity wins.

## This Project's Maturity: POC

A POC is exploring viability. Time-boxed, high uncertainty, goal is to validate the core idea. Success = learning and a working MVP, not completeness.

## Maturity Levels

### POC (Proof of Concept)
Exploring viability. Build fast, validate the idea. TDD optional but encouraged.

### Alpha
Building toward MVP. Core concept validated. Increment safety incrementally.

### Beta
Shipping to broader audiences. Feature-complete for 1.0. Focus on stability.

### GA (General Availability)
Production-grade, long-term support expected. High stability demands.

## Cascade Matrix for POC (Current Level)

| Dimension | POC Behavior |
|-----------|-------------|
| **PRD Depth** | Paragraph-level ✓ (done) |
| **Specs Required** | No — but recommended for clarity |
| **TDD Enforced** | Optional but encouraged |
| **Quality Gates** | Pre-commit lint only (Gate 1) |
| **Commit Discipline** | Conventional commits encouraged |
| **Reviewer Agent** | Skip — solo agent is fine |
| **Environment Tier** | Tier 1-2 (local + GitHub Pages) |
| **Away Mode Autonomy** | Full autonomy |
| **Interview Depth** | ~5 questions (fast exploration) ✓ (done) |
| **Parallel Agents** | 1 serial |
| **Cycle Planning** | Informal (ad-hoc batching) |

## Promotion Path

**POC → Alpha** (after M1 ships):
- Working MVP deployed to GitHub Pages
- Basic tests written
- Run `/add:retro` to trigger promotion assessment

**Alpha → Beta:**
- 50%+ test coverage
- PR workflow in use
- Specs written for all user-facing features

**Beta → GA:**
- 80%+ coverage
- CI/CD gates active
- 30+ days production stability

## Promotion Process

1. Run `/add:retro` — it will suggest promotion when evidence supports it
2. Agent performs gap analysis
3. Create promotion milestone (M{N} — "Promote to Alpha")
4. Execute milestone in 1-2 cycles
5. Update `.add/config.json` maturity field

## Reading the Room

Before any significant action, check `.add/config.json` maturity field.

**POC mindset:** Move fast, ask forgiveness not permission, skip reviews, TDD is "nice to have", build toward the working MVP.

**Conflict Resolution:** When another rule conflicts with maturity-lifecycle, maturity wins.

Examples:
- TDD rule says "always write tests first" but maturity is POC → TDD is optional
- Source control rule says "conventional commits required" but maturity is POC → freeform is OK
