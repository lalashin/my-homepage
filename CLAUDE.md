# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Type**: Static personal portfolio website  
**Tech Stack**: HTML5, CSS3, Vanilla JavaScript (no build process)  
**Purpose**: Front-end developer's portfolio with focus on accessibility and clean code

## Development Setup

No build tools or dependencies required. Simply open `index.html` in a browser to preview.

### Local Development
```bash
# View in browser (live-serve or similar HTTP server recommended)
# Avoid file:// protocol for proper CORS with Google Fonts
python -m http.server 8000  # or: npx serve
# Then open http://localhost:8000
```

## Architecture & Key Patterns

### CSS System
- **Theme via CSS Variables** (`style.css` lines 1-24):
  - Color palette: coral (primary), cream/blush (backgrounds), text shades
  - Shadows: `--shadow-sm`, `--shadow-md`, `--shadow-lg` for depth
  - Spacing: `--max-width: 720px` (container limit), `--header-h: 68px` (sticky header height)
  - Border radius: `--radius` (22px), `--radius-sm` (16px), `--radius-pill` (999px)
- **No CSS frameworks** — Grid and Flexbox used directly
- **Responsive breakpoints**: 640px (hamburger menu), 600px (interest grid columns), 768px (hero layout)

### HTML Structure
- **Semantic HTML** with proper heading hierarchy and ARIA labels
- **Accessibility features**:
  - Skip-link (`.skip-link`) for keyboard navigation
  - `aria-expanded` on nav toggle button
  - `aria-label` on nav region
  - `aria-hidden="true"` on decorative elements
  - Landmark regions: `<header>`, `<main>`, `<footer>`, `<section>`

### JavaScript (Vanilla, No Frameworks)
- **IIFE pattern** (`script.js`): All code wrapped in self-executing function for encapsulation
- **Navigation toggle**: Click handler with class toggling (`is-open`) and aria-expanded state management
- **Auto-generated footer year**: Updates `#year` element annually
- **Event delegation**: Nav links close menu on click; handles dynamic interaction without frameworks

## File Structure

| File | Purpose |
|------|---------|
| `index.html` | Main portfolio page with hero, intro, interests, contact sections |
| `index1.html` | Additional page (purpose not documented) |
| `style.css` | All styling; CSS Variables define theme, no external CSS libraries |
| `script.js` | Navigation interactivity and footer year update |

## Common Tasks

### Add a New Section
1. Add HTML structure to `index.html` with section ID
2. Use existing utility classes: `.section`, `.container`, `.section-title`
3. Mirror color/shadow patterns from existing sections (use `--shadow-md`, `--coral` variables)

### Update Color Scheme
1. Modify CSS Variables in `style.css` lines 1-24 (`:root`)
2. Variables follow naming pattern: `--{hue}-{shade}` or `--{semanticname}`
3. All colors are derived from the CSS Variables — no hardcoded colors elsewhere

### Improve Mobile Experience
1. Check responsive breakpoints in media queries (`@media max-width: 640px`, `@media min-width: 768px`)
2. Mobile-first approach: base styles apply to mobile; breakpoints expand layout for larger screens

### Accessibility Audit
- Check all links have descriptive text (not "click here")
- Verify heading order (h1 → h2 → h3) is logical
- Confirm all interactive elements (buttons, nav) have proper ARIA attributes
- Test with keyboard navigation (Tab, Shift+Tab, Enter)

## Notes for Future Development

- **No state management needed**: Current vanilla JS is sufficient for navigation toggle
- **No preprocessor**: CSS is plain CSS; if complexity grows, consider CSS Modules or similar
- **Performance is strong**: Single stylesheet, minimal JS, Google Fonts only external dependency
- **Contact info is placeholder**: `hello@example.com` and `github.com/username` need updates with real values
- The `index1.html` file exists but is not linked or documented—clarify its purpose before making changes
