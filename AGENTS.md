# AGENTS.md

Multi-agent task coordination for the Neck & Posture Exercise App.

## Project Context

A minimalist exercise timer app built as a single HTML file. No build system, no dependencies - just open `index.html` in a browser.

## Task Breakdown

### UI/Design Tasks
- Modify CSS styles in the `<style>` section
- Update color scheme via CSS variables in `:root`
- Adjust layout, spacing, typography
- Add/modify animations (`@keyframes`)

### Exercise Content Tasks
- Edit `exercises` array in JavaScript
- Modify exercise names, instructions, durations, reps
- Change exercise order or groupings (parts)

### Illustration Tasks
- Edit SVG strings in `illustrations` object
- Create new stick figure drawings
- Adjust animation classes on SVG elements

### Logic/Behavior Tasks
- Modify JavaScript functions (showExercise, handleDone, etc.)
- Add new exercise types
- Change timer/counter behavior
- Update state management

## Agent Guidelines

### When modifying exercises:
1. Keep instructions concise (fits in ~80px height box)
2. Match illustration key to exercise
3. Test all exercise types work after changes

### When modifying styles:
1. Test on mobile viewport (375px width)
2. Maintain high contrast (white on black)
3. Keep animations subtle and non-distracting

### When modifying illustrations:
1. Use viewBox="0 0 100 100"
2. Keep stroke-width consistent (2px default)
3. Apply animation classes sparingly
4. Test that SVG renders correctly

## File Locations

| Component | Location |
|-----------|----------|
| Styles | `index.html` lines 7-390 |
| HTML structure | `index.html` lines 393-512 |
| Illustrations | `index.html` lines 516-630 |
| Exercise data | `index.html` lines 633-734 |
| App logic | `index.html` lines 736-900 |

## Testing

No test framework. Manual testing:
1. Open `index.html` in browser
2. Click through all exercises
3. Test timer countdown
4. Test rep counting
5. Test navigation (prev/next)
6. Test keyboard shortcuts
7. Test on mobile viewport
