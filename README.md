DreamStreak

Discipline, but soft.

DreamStreak is a cross-platform discipline tracking app built for people who want to stay consistent during a cut or habit challenge. It is not a calorie tracker. It does not count macros. It tracks whether you showed up and executed your non-negotiables.

The goal is simple:
Set clear daily standards.
Check in once per day.
Protect your streak.
Finish the challenge clean.

Why this exists

During a cut or any focused phase, the real battle is not calories. It is consistency.

Most fitness apps are either:

Overloaded with nutrition tracking

Dark, aggressive “grindset” style

Or built around journalling and motivation essays

DreamStreak focuses on behaviour. It gives you:

A structured challenge

A clean daily check-in

Visual progress

Calm, smart reminders

A minimal mascot that reacts to your performance

It keeps you accountable without being overwhelming.

Core Concept

You create a challenge with a defined duration and a set of daily goals. Some goals are marked as non-negotiable. Your streak continues only if those non-negotiables are completed.

Each day you:

Open the app

Complete your goals

Close the day

Protect the chain

The app tracks:

Current streak

Best streak

Daily completion score

Heatmap of your consistency

Goal adherence percentages

Challenge progress

Features
Challenge Setup

Choose duration (7, 14, 30, 60, 90, or custom)

Add daily goals (binary or numeric)

Mark goals as non-negotiable

Select reminder style (Coach, Rival, Calm)

Set reminder times

Daily Check-In

Clean checklist interface

Progress indicator

Mascot reacts as goals are completed

One-tap day completion

Streak System

Streak continues when all non-negotiables are completed

Visual streak card

Milestone celebrations

Optional streak shield (future feature)

Progress Visualisation

Heatmap calendar

Goal adherence bars

Milestone tracking

Challenge countdown

Reminder System

No journalling. No typing motivational essays.

Users select a reminder style:

Coach: direct and grounded

Rival: competitive and firm

Calm: supportive and low-pressure

Reminders are generated dynamically based on:

Remaining goals

Streak length

Time of day

Challenge progress

Design Philosophy

DreamStreak uses a Pastel Dreamland Adventure aesthetic.

Warm off-white backgrounds

Soft lavender and sky accents

Subtle gradients

Rounded surfaces

Light shadows

Calm typography

The visual identity is gentle but structured.

The minimal blob mascot appears throughout the app with different expressions:

Neutral

Locked-in

Proud

Hype

Side-eye

Oof

It adds personality without turning the app into a cartoon.

Tech Stack

DreamStreak is built as a cross-platform system.

Web

Next.js

TypeScript

Tailwind CSS

Mobile

Expo (React Native)

expo-router

expo-linear-gradient

expo-notifications

react-native-svg

Backend

Supabase (Auth + Postgres)

Shared Logic

Shared TypeScript types

Zod validation schemas

Streak calculation logic

Reminder message generator

The goal is one backend, shared logic, and consistent data across web and mobile.

Architecture Overview

apps/web → Next.js app

apps/mobile → Expo app

packages/shared → business logic and types

Supabase → authentication and database

The streak algorithm and reminder generator are shared across platforms to ensure consistent behaviour.

Project Status

This project is currently in active development.

Planned phases:

Web MVP (challenge setup, daily check-in, streak logic, progress)

Mobile app with push notifications

Mascot animation system

Theme support

Advanced streak modes and weekly recap

Vision

DreamStreak is designed to make discipline feel structured, calm, and aesthetic.

It is built for:

Cutting phases

Habit challenges

Consistency training

Anyone who wants to finish what they start

No chaos.
No overcomplication.
Just clean execution, day after day.