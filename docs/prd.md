# Andres Paulino Daily Habit Tracker — Product Requirements Document

**Version:** 0.1.0
**Created:** 2026-04-09
**Author:** Andres Paulino
**Status:** Draft

## 1. Problem Statement

People who want to improve themselves struggle to maintain visibility into their daily routines. Without a simple, always-available tool, it's easy to lose track of which habits are being kept, which are slipping, and whether progress is being made over time.

This project provides a lightweight, browser-based habit tracker that requires no account, no server, and no installation — just open a link and start tracking.

## 2. Target Users

**Primary user:** Anyone who wants to build better habits or change existing ones.

They want to:
- Log the habits they intend to maintain daily (e.g., "read 10 pages", "drink water")
- Check habits off each day as they complete them
- See streaks to stay motivated and identify consistency patterns
- Share the app easily with friends and family (non-technical users included)

## 3. Success Metrics

| Metric | Target | Measurement |
|--------|--------|-------------|
| Add a habit and see it in the list | Works on first use | Manual test — add habit, verify display |
| Check off a habit daily | Persists after page refresh | Manual test — check off, reload, verify state |
| Streak count displayed and accurate | Correct after 2+ consecutive days | Manual test — simulate 2-day check-off |
| Shareable via URL | Non-technical user can open link and use app | Share GitHub Pages URL, user confirms it works |

## 4. Scope

### In Scope (MVP)

- **Add habit:** Text input to create a new named habit
- **List habits:** Display all added habits in a clean, readable list
- **Daily check-off:** Mark each habit as done for today; persists via localStorage
- **Streak counter:** Show how many consecutive days a habit has been completed
- **localStorage persistence:** All data survives page refresh — no server needed
- **Responsive design:** Works on mobile and desktop; touch-friendly
- **Cross-browser support:** Chrome, Firefox, Safari, Edge (latest versions)
- **Shareable URL:** Deployed to GitHub Pages for easy link-sharing

### Out of Scope

- Reminders or push notifications
- Categories or habit grouping
- Charts or progress graphs
- User accounts or authentication
- Sync across multiple devices
- Habit deletion or edit history

## 5. Architecture

### Tech Stack

| Layer | Technology | Version | Notes |
|-------|-----------|---------|-------|
| Markup | HTML5 | 5 | Single page, no build step |
| Styling | CSS3 | 3 | Custom properties, flexbox/grid, responsive |
| Logic | JavaScript | ES2022 | Vanilla JS — no framework, no bundler |
| Storage | localStorage | Browser API | All data stored client-side on user's device |

### Infrastructure

| Component | Choice | Notes |
|-----------|--------|-------|
| Git Host | GitHub | Remote TBD — create repo first |
| Hosting | GitHub Pages | Free static hosting, permanent shareable URL |
| CI/CD | GitHub Actions | Auto-deploy on push to main |
| Containers | None | Static site — no containers needed |
| IaC | None | No infrastructure to manage |

### Environment Strategy

| Environment | Purpose | URL | Deploy Trigger |
|-------------|---------|-----|----------------|
| Local | Development — open file in browser | `file:///index.html` | Manual |
| Production | Live / shareable | TBD (`yourname.github.io/habit-tracker`) | Push to `main` |

**Environment Tier:** 2 (Local + Production)

All user data is stored in the browser's localStorage. Each user's data is local to their device — nothing is shared or synced between users.

## 6. Milestones & Roadmap

### Current Maturity: POC

### Roadmap

| Milestone | Goal | Target Maturity | Status | Success Criteria |
|-----------|------|-----------------|--------|------------------|
| M1: MVP | Core habit tracking works end-to-end, deployed | Alpha | NOW | All 4 MVP features functional and live on GitHub Pages |
| M2: Polish | UX improvements, mobile refinement based on feedback | Alpha | NEXT | Positive feedback from non-technical test users |

### Milestone Detail

#### M1: MVP [NOW]
**Goal:** Build and deploy the core habit tracker — add habits, list them, check off daily, and track streaks.
**Appetite:** Small (1-2 sessions)
**Target maturity:** Alpha (promote after M1 ships and is verified)
**Features:**
- Habit input — add habits by name via text field
- Habit list — display all habits with today's check-off state
- Daily check-off — mark a habit done today; persists in localStorage
- Streak counter — consecutive-day streak displayed per habit
- Banner — "Andres Paulino Daily Habit Tracker using ADD and Claude Code"

**Success criteria:**
- [ ] User can add a habit and see it listed immediately
- [ ] User can check off a habit and the state persists after page refresh
- [ ] Streak increments after checking off on consecutive days
- [ ] Streak resets to zero after a missed day
- [ ] App works on mobile Chrome and desktop Chrome/Firefox/Safari/Edge
- [ ] Deployed to GitHub Pages with a shareable public URL
- [ ] Banner visible at the top of the page

### Maturity Promotion Path

| From | To | Requirements |
|------|-----|-------------|
| poc → alpha | M1 shipped, deployed URL working, basic tests written |
| alpha → beta | 50%+ test coverage, PR workflow in use, feature specs written |
| beta → ga | 80%+ coverage, CI/CD gates active, 30+ days stability |

## 7. Key Features

### Feature 1: Habit Management
Users type a habit name into a text input and submit it. The habit is added to a list below and saved in localStorage. Habits persist across page refreshes and browser sessions on the same device.

### Feature 2: Daily Check-Off
Each habit shows a checkbox for "today." Checking it marks the habit complete for the current calendar day. The state is stored in localStorage and resets automatically the following day (detected by comparing stored date to current date at page load).

### Feature 3: Streak Tracking
The app tracks how many consecutive calendar days each habit has been checked off. The streak count is shown next to each habit. Missing a day resets the streak to zero. Streaks persist in localStorage alongside habit data.

## 8. Non-Functional Requirements

- **Performance:** App loads in under 1 second (static file — no network requests beyond initial page load)
- **Security:** No user data is ever transmitted — all data stays in localStorage on the user's device
- **Accessibility:** Readable font sizes, sufficient contrast between palette colors, keyboard-navigable inputs and checkboxes (min 44px tap targets on mobile)
- **Browser Support:** Chrome (latest), Firefox (latest), Safari (latest), Edge (latest)
- **Mobile:** Responsive layout, touch-friendly check-off targets
- **Visual Design:**
  - Color palette: Light Blue `#60B4D8`, Purple `#7C5CBF`, Gold `#D4AF37`
  - Tone: Simple, professional
  - Banner at top: "Andres Paulino Daily Habit Tracker using ADD and Claude Code"

## 9. Open Questions

- What should happen to a habit's streak when the user opens the app after missing multiple days? (Reset to 0, or show "missed X days" as context?)
- Should habits be reorderable, or fixed in the order they were added?
- Should there be a way to delete a habit in v1? (Currently out of scope, but may cause UX friction if users can't remove habits they no longer want.)

## 10. Revision History

| Date | Version | Author | Changes |
|------|---------|--------|---------|
| 2026-04-09 | 0.1.0 | Andres Paulino | Initial draft from /add:init interview |
