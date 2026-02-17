# DreamStreak Build Phases

This document breaks DreamStreak into clear phases. Each phase contains a checklist of tasks and implementation rules you can hand to an AI and keep the codebase clean and readable.

This project prioritises:

- Simple, predictable code
- Small, reusable components
- Clear naming
- Minimal magic
- A calm, pastel UI that stays consistent

---

## Global Build Rules

### Code style

- Use TypeScript everywhere.
- Prefer small functions over large ones.
- Keep each file focused on one purpose.
- Avoid deep nesting. Return early.
- Avoid clever abstractions. Favour explicit code.
- Use straight apostrophes only (').
- Avoid em dashes.

### Components

- Prefer composition over big components.
- Keep UI components presentational where possible.
- Keep state and side effects at page or feature level.
- Extract repeated UI into components early.

### Naming

- Use clear names that match the domain:
  - Challenge, Goal, DailyLog, Completion, Reminder
- Avoid vague names like data, item, thing.

### UI consistency

- Use design tokens (colours, spacing, radius) through a single source.
- Use subtle gradients sparingly.
- Keep layouts clean with generous whitespace.

### Validation

- Validate input at boundaries (forms and API).
- Prefer Zod schemas for shared validation.

### Testing (optional but recommended)

- Add simple unit tests for:
  - streak logic
  - reminder message generator
  - daily score calculation

---

## Phase 0: Product Decisions and Requirements Lock

### Goal

Lock the rules so you do not refactor everything later.

### Tasks

- Define default streak rule:
  - Streak continues only if all non-negotiables are completed that day.
- Decide initial goal types:
  - Binary (done/not done)
  - Numeric (value with target)
- Decide required screens for MVP:
  - Setup
  - Today
  - Progress
  - Reminders
  - Settings
- Decide reminder modes:
  - Coach
  - Rival
  - Calm
- Define milestone days:
  - 3, 7, 14, 30, 60, 90
- Define challenge duration options:
  - 7, 14, 21, 30, 60, 90, custom

### Deliverables

- A short written spec of rules and screen list.
- Confirm the data fields required for each domain entity.

---

## Phase 1: Domain Model and Shared Logic Foundation

### Goal

Create the clean core logic once and reuse it everywhere.

### Tasks

#### 1. Define domain types

Create shared types for:

- User
- Challenge
- Goal
- DailyLog
- GoalCompletion
- ReminderSettings

Include fields needed for:

- goal type (binary/numeric)
- target values for numeric goals
- non-negotiable flag
- dates for challenge range
- daily completion date keys

#### 2. Zod schemas

Create Zod schemas for:

- ChallengeCreateInput
- GoalCreateInput
- DailyCheckInInput
- ReminderSettingsInput

Keep schemas simple and readable.

#### 3. Streak logic module

Implement pure functions:

- `getDayKey(date): string`
- `isGoalComplete(goal, completion): boolean`
- `calculateDayStatus(goals, completions): { isPerfectDay, isPassDay, score }`
- `calculateStreak(dailyLogs, goals): { current, best }`
- `getMilestone(streak): number | null`

Rules:

- No side effects.
- No UI concerns.
- Small functions only.

#### 4. Reminder message generator module

Implement:

- `generateReminderMessage(params): string`

Inputs should include:

- mode (coach/rival/calm)
- remainingGoalsCount
- remainingGoalNames (max 2 in message)
- streak
- dayIndex
- totalDays
- timeOfDay (morning/evening)

Output:

- short, clean strings
- no quotes, no emojis inside notifications by default

#### 5. Mascot state mapper

Implement a small pure function:

- `getMascotMood(context): MascotMood`

Example moods:

- neutral
- lockedIn
- proud
- hype
- sideEye
- oof

Context inputs:

- goalsRemaining
- streakChanged
- milestoneHit
- dayCompleted
- dayFailed

### Deliverables

- Shared types and schemas
- Pure logic modules (streak, messages, mascot mood)
- Minimal tests for core logic (recommended)

---

## Phase 2: Backend Setup and Data Persistence

### Goal

Persist user data so web and mobile stay in sync.

### Tasks

#### 1. Authentication

- Enable auth provider in your backend.
- Create a simple auth flow: sign in, sign out.
- Do not build complex roles in v1.

#### 2. Database tables

Create tables for:

- challenges
- goals
- daily_logs
- goal_completions
- reminder_settings

Include:

- user_id on all user-owned tables
- created_at, updated_at timestamps where useful
- indexes on (user_id, date) for logs

#### 3. API layer

Expose a clean set of operations:

- Challenge:
  - create
  - get active
  - list
  - complete/close
- Goals:
  - list by challenge
  - create
  - update
  - archive
- Daily logs:
  - get by day
  - upsert day log
  - list for date range (for heatmap)
- Reminder settings:
  - get
  - update

Rules:

- Keep request/response shapes aligned with shared types.
- Validate inputs using shared Zod schemas.
- Use clear error messages.

### Deliverables

- Database schema
- API endpoints
- Auth works end-to-end
- Seed script or simple dev setup instructions (optional)

---

## Phase 3: Web MVP UI

### Goal

Deliver a clean usable web MVP with the full discipline loop.

### Screens to build

- Setup
- Today
- Progress
- Reminders
- Settings

### Shared UI components to build early

Build these first to keep pages clean:

- `PageShell` (consistent padding, max width)
- `Card` (surface, border, shadow, radius)
- `SectionHeader` (title + optional subtitle)
- `PrimaryButton`, `SecondaryButton`
- `Toggle`
- `ProgressRing` (simple)
- `Badge` (streak, milestones)
- `GoalRow` (goal label + control)
- `HeatmapGrid` (reads day statuses)
- `Mascot` (SVG component with mood prop)

Rules:

- Keep components small and prop-driven.
- Avoid over-configurable components in v1.

### 1. Setup screen

Tasks:

- Challenge duration selector
- Goal template picker + custom goal add
- Non-negotiable toggles
- Reminder mode selection
- Reminder time selection (basic)
- Create challenge action

Output:

- Create challenge + goals + reminder settings
- Navigate to Today screen

### 2. Today screen

Tasks:

- Load today's log
- Render goals list
- Allow marking goals complete
  - binary toggle
  - numeric input with target
- Show progress ring and short summary
- "Complete day" action to close check-in
- Update mascot mood live based on remaining goals

### 3. Progress screen

Tasks:

- Streak card (current, best)
- Heatmap for current challenge date range
- Goal adherence bars
- Milestone display

### 4. Reminders screen

Tasks:

- Mode selector (coach/rival/calm)
- Toggle reminders on/off
- Time configuration (morning, evening)
- Preview messages (using generator)

Web note:

- Web push can be unreliable. In v1, this screen can still exist and store settings even if delivery is mobile-first.

### 5. Settings screen

Tasks:

- Edit goals (rename, archive)
- View challenge info
- Sign out

### Deliverables

- Web app MVP working with backend
- Clean components
- No unreadable mega-components
- Clear empty states and loading states

---

## Phase 4: Mobile App MVP (Expo)

### Goal

Replicate the web MVP on mobile with shared backend sync.

### Tasks

#### 1. Navigation

- Implement routes that mirror web screens:
  - Setup, Today, Progress, Reminders, Settings

#### 2. Shared UI tokens

- Reuse the same design tokens.
- Keep pastel theme consistent.
- Use subtle gradients in headers and streak card.

#### 3. Mobile UI components

Build mobile equivalents:

- ScreenShell
- Card
- Buttons
- Toggle
- GoalRow
- Heatmap
- Mascot

Rule:

- Keep naming consistent with web components.

#### 4. Data and caching

- Fetch challenge and daily logs.
- Use a simple caching strategy so the app feels fast.
- Avoid complex offline mode in v1.

### Deliverables

- Mobile MVP with same features as web
- Smooth daily check-in UX
- Shared data visible on web and mobile

---

## Phase 5: Notifications and Reminder Delivery

### Goal

Make reminders actually deliver reliably through mobile.

### Tasks

#### 1. Local notifications first

- Schedule local notifications based on reminder settings.
- Trigger morning and evening reminders.
- Ensure notifications include goal-based context:
  - remaining goals
  - streak
  - day x of y

#### 2. Push notifications second (optional)

- Add push later if needed.
- Keep the system simple:
  - a small worker schedules pushes based on user settings

#### 3. In-app nudges

- If check-in is incomplete late day:
  - show a banner in Today screen
  - mascot uses side-eye mood

### Deliverables

- Notifications working on mobile
- Reminder preview matches delivered message
- No overly complex scheduling system

---

## Phase 6: Polish Pass

### Goal

Make the app feel premium without adding complexity.

### Tasks

#### 1. Mascot polish

- Add micro animations:
  - fade in
  - small bounce on completion
  - sparkle on milestone
- Add a few more expressions if needed.

#### 2. Milestone celebrations

- Small modal or screen for:
  - 3, 7, 14, 30, 60, 90 streaks
- Keep it short and clean.

#### 3. Visual refinements

- Improve spacing rhythm
- Ensure colour usage stays consistent
- Make the heatmap feel satisfying

#### 4. Accessibility pass

- Button sizes and tap targets
- Contrast checks
- Keyboard navigation on web

### Deliverables

- Premium feel
- No new major features
- UI remains readable and calm

---

## Phase 7: Theme Support (Future)

### Goal

Enable theme switching without rewriting the UI.

### Tasks

- Convert colours into theme tokens.
- Implement theme selection:
  - Pastel Dreamland (default)
  - Dark (later)
  - Additional palettes (later)

Rules:

- No hard-coded colours in components.
- Components only consume tokens.

### Deliverables

- Theme system with clean token swapping
- Default theme remains Pastel Dreamland

---

## Definition of Done (for each phase)

A phase is done when:

- The scope is complete.
- The code is readable and consistent.
- Components stay small and focused.
- There is no duplicated logic across web and mobile.
- Shared logic stays pure and tested where it matters.
- The UI remains clean and not cluttered.

---

## AI Handoff Instructions Template

When passing a phase to an AI, include:

- The phase name and scope
- The specific checklist items from this document
- The global build rules at the top
- A reminder to keep components small and readable
- A reminder to avoid overengineering and keep logic shared

Example prompt starter:

- "Implement Phase X only. Follow the Global Build Rules. Keep code simple. Use small components. Use shared logic modules for streak and reminders. Do not change unrelated code."
