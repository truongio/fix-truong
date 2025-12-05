# AGENTS.md

Multi-agent task coordination for the Neck & Posture Exercise App.

## Project Context

A minimalist exercise timer app built as a single HTML file. No build system, no dependencies - just open `index.html` in a browser.

---

## Premium Desktop Redesign (December 2024)

### Design Direction
**Minimal & Editorial** style with **Abstract Illustrations** prioritizing **Visual Impact**

Inspired by: Apple product pages, Kinfolk magazine, premium fitness brands like Peloton.

### Color System

#### Mobile (Default)
```css
--bg: #FAFAFA;
--text: #0A0A0A;
--text-dim: #525252;
--text-muted: #A3A3A3;
--accent: #0A0A0A;
--accent-warm: #C2410C;      /* Timer warnings, accent dots */
--success: #059669;          /* Completion states */
```

#### Desktop (1024px+)
Same palette - cool monochrome with warm orange accent for highlights.

### Typography System

| Element | Font | Size | Weight | Notes |
|---------|------|------|--------|-------|
| Hero title | Playfair Display | clamp(4rem, 12vw, 14rem) | 400 | Start screen |
| Exercise name | Inter | clamp(2.5rem, 5vw, 5rem) | 800 | Uppercase |
| Stat numbers | Inter | clamp(3rem, 6vw, 6rem) | 800 | Timer/reps |
| Labels | Inter | 0.75-0.85rem | 600 | Uppercase, wide tracking |
| Instructions | Inter | 1.1rem | 400 | Sentence case |
| Buttons | Inter | 1rem | 600 | Uppercase, 0.1em tracking |

### Layout Structure

#### Desktop Grid (1024px+)
```
Exercise Screen:
+--------------------------------------------------+
|  [Part Label]                    [Timer] [Sound] |  <- Header (auto height)
+--------------------------------------------------+
|                    |                              |
|   ILLUSTRATION     |   [Side Label]               |
|   (55% width)      |   EXERCISE NAME              |
|                    |   [Stats: Reps/Seconds]      |  <- Main (1fr)
|                    |   [Instructions]             |
|                    |   [Prev] [DONE]              |
|                    |                              |
+--------------------------------------------------+
|  [========Progress Bar========]        3 of 7    |  <- Footer (auto height)
+--------------------------------------------------+
```

#### CSS Grid
```css
.exercise-screen.active {
  display: grid;
  grid-template-rows: auto 1fr auto;
  grid-template-columns: 55% 45%;
}
```

### Abstract Illustrations

Replaced stick figures with geometric abstract shapes:

| Exercise | Shape Concept | Animation |
|----------|---------------|-----------|
| Chin Tucks | Receding concentric circles | `anim-tuck` |
| Neck Circles | Rotating arc segments | `anim-circle` |
| Upper Trap | Tilted oval + pressure point | `anim-tilt` |
| Levator Scap | Diagonal tension lines | `anim-tilt` |
| Doorway Pec | Radiating lines from corner | `anim-step-forward` |
| Chin Tuck Nod | Rising arc with apex dot | `anim-lift-head` |
| Wall Angels | Vertical + sliding horizontal bars | `anim-slide-up` |

#### Shape Design Principles
- Monochrome strokes (#0A0A0A primary, greys for depth)
- Accent color (#C2410C) for focal points
- Subtle ambient animations (pulse, float)
- viewBox="0 0 100 100" maintained

### Animations

#### Easing Functions
```css
--ease-out-expo: cubic-bezier(0.16, 1, 0.3, 1);
--ease-in-out-expo: cubic-bezier(0.87, 0, 0.13, 1);
```

#### Key Animations
| Animation | Duration | Trigger |
|-----------|----------|---------|
| Staggered entry | 0.6s per element | Exercise change |
| Button hover lift | 0.5s | Hover |
| Button fill sweep | 0.5s | Hover (::before) |
| Countdown pulse | 0.8s infinite | Last 5 seconds |
| Sidebar slide | 0.5s | Hover left edge |

### Interactive Components

#### Sidebar (Desktop)
- Partially visible (30px showing) by default
- Slides fully open on hover
- Shows exercise list with completion states
- Visual indicator bar when collapsed

#### Done/Skip Button
- Black background, white text
- Green (#059669) fill sweep on hover via ::before
- Lift effect (translateY -4px) + shadow on hover

#### Progress Bar (Footer)
- Replaces dot indicators on desktop
- Linear track with filled portion
- Shows "X of Y" text

### Spacing System

```css
--space-xs: 8px;
--space-sm: 16px;
--space-md: 24px;
--space-lg: 40px;
--space-xl: 60px;
--space-2xl: 80px;
```

Desktop uses generous padding (60-80px) for editorial feel.

---

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
- Create abstract geometric shapes (not stick figures)
- Use monochrome palette with #C2410C accent
- Apply animation classes sparingly

### Logic/Behavior Tasks
- Modify JavaScript functions (showExercise, handleDone, etc.)
- Add new exercise types
- Change timer/counter behavior
- Update state management

---

## Agent Guidelines

### When modifying exercises:
1. Keep instructions concise (fits in ~80px height box on mobile)
2. Match illustration key to exercise
3. Test all exercise types work after changes

### When modifying styles:
1. Test on both mobile (375px) and desktop (1024px+)
2. Desktop: Maintain monochrome palette with warm accent
3. Keep animations purposeful and elegant
4. Use CSS variables for consistency

### When modifying illustrations:
1. Use viewBox="0 0 100 100"
2. Create abstract geometric shapes, not literal figures
3. Primary stroke: #0A0A0A, accent: #C2410C
4. Apply animation classes from existing set
5. Test that SVG renders at large size (500px)

### When modifying desktop layout:
1. Maintain 55%/45% grid split
2. Ensure all content fits without scrolling
3. Keep exercise names under ~20 characters or reduce font size
4. Test progress bar updates correctly

---

## File Structure (Updated)

| Component | Location (approximate) |
|-----------|------------------------|
| CSS Variables | `:root` block (~lines 18-52) |
| Mobile Styles | Lines 54-790 |
| Desktop Media Query | `@media (min-width: 1024px)` (~lines 800-1510) |
| HTML Structure | Lines 1515-1590 |
| Abstract Illustrations | `illustrations` object (~lines 1595-1715) |
| Exercise Data | `exercises` array (~lines 1720-1780) |
| App Logic | JavaScript functions (~lines 1780-2150) |

---

## Testing

No test framework. Manual testing:

### Mobile Testing
1. Open `index.html` in browser
2. Use DevTools to set viewport to 375px width
3. Click through all exercises
4. Test timer countdown
5. Test rep counting
6. Test navigation (prev/next)
7. Test keyboard shortcuts

### Desktop Testing (1024px+)
1. View at full desktop width
2. Verify 55%/45% layout split
3. Test sidebar hover interaction (left edge)
4. Verify progress bar in footer
5. Check all exercise names fit without overflow
6. Test button hover animations
7. Verify staggered entry animations on exercise change
8. Test completion screen layout
