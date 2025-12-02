# CLAUDE.md

This file provides guidance to Claude Code when working with this project.

## Project Overview

A minimalist single-page web app for guiding users through a daily neck & posture exercise routine. Built with vanilla HTML, CSS, and JavaScript - no build tools or frameworks.

## Tech Stack

- **HTML5** - Single file (`index.html`)
- **CSS** - Embedded in `<style>` tag
- **JavaScript** - Embedded in `<script>` tag
- **SVG** - Inline illustrations for each exercise

## Design Philosophy

- **Minimal & focused** - Pure black background, content at bottom of screen
- **Large typography** - Exercise names prominent, stats in bold colors
- **Subtle animations** - Breathing/movement animations on stick figure illustrations
- **Mobile-first** - Designed for phone use during exercise

## Key Features

- 10 exercises across 4 parts (Release, Open, Strengthen, Reset)
- Three exercise types:
  - `timed` - Countdown timer, auto-advances when done
  - `reps` - Count each rep with button press
  - `manual` - Show info, single DONE button to complete
- Progress dots showing position in workout
- Session timer in header
- Sound effects (toggleable)
- Keyboard shortcuts (Space/Enter, Arrow keys)

## File Structure

```
/
├── index.html      # Complete app (HTML + CSS + JS)
├── CLAUDE.md       # This file
└── AGENTS.md       # Multi-agent coordination docs
```

## Code Organization (within index.html)

1. **CSS** (~400 lines) - Styles, animations, responsive design
2. **HTML** (~60 lines) - Start screen, exercise screen, completion screen
3. **JavaScript** (~250 lines):
   - `illustrations` object - SVG strings for each exercise
   - `exercises` array - Exercise data (name, type, reps, duration, etc.)
   - State variables - currentExercise, currentSide, timeRemaining, etc.
   - Functions - showExercise(), startTimer(), handleDone(), etc.
   - Event listeners - buttons, keyboard

## Adding New Exercises

1. Add SVG to `illustrations` object
2. Add exercise object to `exercises` array with:
   - `name`, `part`, `instructions`
   - `type`: "timed", "reps", or "manual"
   - `duration` (for timed) or `reps` (for reps/manual)
   - `hold` (optional, for rep exercises with holds)
   - `sides` (1 or more)
   - `sideNames` (array, if sides > 1)
   - `rounds` (optional, for multiple rounds)
   - `illustration` (key into illustrations object)

## Styling Conventions

- Colors defined in CSS `:root` variables
- Yellow (`--accent`) for primary stats
- Orange (`--accent-orange`) for secondary/warning
- Green (`--success`) for done button
- Animations use `@keyframes` with `.anim-*` classes
