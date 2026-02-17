🌤 DreamStreak

Discipline, but soft.

DreamStreak is a cross-platform discipline tracking app designed for people who want to stay consistent during a cut, habit challenge, or focused performance phase.

It is not a calorie tracker.
It does not track macros.
It tracks whether you showed up and executed your non-negotiables.

✨ The Idea

Consistency is the real challenge during a cut.

Most fitness apps focus on:

Calories

Macros

Dark, aggressive “grindset” UI

Or long motivational journalling

DreamStreak focuses on behaviour.

You:

Set clear daily standards

Check in once per day

Protect your streak

Finish the challenge clean

That’s it.

🎯 Core Concept

You create a challenge with:

A defined duration (7–90 days or custom)

A set of daily goals

Selected non-negotiables

Your streak continues only if your non-negotiables are completed.

Each day you:

Open the app

Complete your goals

Close the day

Protect the chain

🚀 Features
🧱 Challenge Setup

Choose challenge duration (7, 14, 30, 60, 90, or custom)

Add daily goals:

Binary (Done / Not done)

Numeric (e.g., steps, sleep hours)

Mark goals as non-negotiable

Select reminder style:

Coach

Rival

Calm

Set reminder times

📅 Daily Check-In

Clean, minimal checklist

Progress indicator

Mascot reacts as goals are completed

One-tap day completion

No clutter

🔥 Streak System

Streak continues when all non-negotiables are completed

Current streak + best streak

Milestone celebrations (3, 7, 14, 30, 60, 90)

Optional streak shield (planned feature)

📊 Progress Visualisation

Heatmap calendar

Goal adherence percentage bars

Streak card

Challenge countdown

Milestone timeline

🔔 Reminder System

No journalling. No typing motivational essays.

Users select a reminder mode:

Coach

Direct. Grounded. Clear.

“2 goals left. Close the day clean.”

Rival

Competitive. Firm.

“Day 9 of 30. Don’t break the chain.”

Calm

Supportive. Low pressure.

“Quick check-in. Finish strong.”

Reminders are generated dynamically based on:

Remaining goals

Streak length

Time of day

Challenge progress

🎨 Design Philosophy

DreamStreak uses a Pastel Dreamland Adventure aesthetic.

Warm off-white backgrounds

Soft lavender + sky accents

Subtle gradients

Rounded surfaces

Light shadows

Calm typography

Plenty of whitespace

It feels gentle, structured, and modern.

Not aggressive.
Not childish.
Not overwhelming.

🫧 The Mascot

A minimal blob mascot appears throughout the app.

Expressions:

Neutral

Locked-in

Proud

Hype

Side-eye

Oof

It reacts to:

Goal completion

Milestones

Streak breaks

End-of-day nudges

The mascot adds warmth without distracting from the discipline loop.

🏗 Tech Stack

DreamStreak is built as a cross-platform system.

🌐 Web

Next.js

TypeScript

Tailwind CSS

📱 Mobile

Expo (React Native)

expo-router

expo-linear-gradient

expo-notifications

react-native-svg

🗄 Backend

Supabase (Auth + Postgres)

📦 Shared Logic

Shared TypeScript types

Zod validation schemas

Streak calculation logic

Reminder message generator

🧠 Architecture Overview
apps/
web/ → Next.js application
mobile/ → Expo application

packages/
shared/ → Business logic, streak algorithm, types
ui/ → Design tokens & reusable components

backend/
Supabase → Auth + Database

One backend.
Shared logic across platforms.
Consistent data everywhere.

🛣 Roadmap
Phase 1 – Web MVP

Challenge setup

Daily check-in

Streak logic

Progress heatmap

Basic reminders

Phase 2 – Mobile App

Expo implementation

Push notifications

Shared backend sync

Phase 3 – Polish

Expanded mascot expressions

Milestone animations

Theme switcher

Weekly recap system

Advanced streak modes

🧭 Vision

DreamStreak is built for people who:

Want to finish what they start

Care about consistency

Prefer calm design over aggressive grind culture

Value structure without complexity

It makes discipline aesthetic.

No chaos.
No overcomplication.
Just clean execution, day after day.
