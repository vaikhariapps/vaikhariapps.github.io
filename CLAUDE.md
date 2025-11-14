# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Vaikhari** is a static website and initiative dedicated to creating simple, intuitive applications for productivity and learning. The name comes from Hindu philosophy, representing sound at its most tangible, articulated form.

**Technology Stack:**
- HTML5 + CSS3 (vanilla, no frameworks)
- Font Awesome 6.7.2 (CDN-based icons only)
- No build system, package manager, or JavaScript frameworks
- Pure static website ready for direct server deployment

**Current Status:** Landing page with one featured app (Simple Pomo - Pomodoro timer)

---

## Directory Structure

```
vaikhari-apps/
├── index.html                 # Main landing page
├── simple-pomo/
│   └── privacy-policy.html   # Simple Pomo privacy policy
├── assets/images/            # Brand assets and app icons (11 images)
└── .claude/                   # Claude CLI configuration
```

The structure is designed to be extensible: new apps should follow the pattern `app-name/privacy-policy.html` and be added to the apps grid in `index.html`.

---

## Design System & Architecture

### Color Palette (CSS Custom Properties)
```css
--primary-dark: #1A3A70      /* Navy blue - primary text and headers */
--teal: #17A697              /* Teal green - accents and borders */
--light-blue: #5DADE2        /* Light blue - gradients and highlights */
--gold: #FFC107              /* Golden yellow - CTAs and emphasis */
--light-bg: #F8F9FA          /* Off-white - page background */
--text-dark: #2C3E50         /* Dark gray - body text */
```

All color references should use these CSS variables for consistency.

### Responsive Breakpoints
- **Desktop:** Full layout with flex row hero and multi-column grids
- **Tablet (≤768px):** Single-column layouts, hidden desktop nav, stacked buttons
- **Mobile (≤480px):** Reduced font sizes, compact spacing, smaller icons

### Landing Page Structure
1. **Header** - Sticky navigation with logo and links to About/Apps/Contact
2. **Hero** - Welcome with animated lotus icon and primary CTAs
3. **About** - Vaikhari philosophy and initiative values
4. **Apps** - Grid cards showcasing applications with feature lists
5. **Contact** - Social links (Twitter/X, Facebook, Instagram, Email)
6. **Footer** - Copyright and navigation links

### Privacy Policy Pages
Template structure for app privacy policies (see `simple-pomo/privacy-policy.html`):
- **Header Navigation** - Links back to main Vaikhari site
- **Page Header** - App icon, title, breadcrumb with Vaikhari branding
- **Main Content** - 13 standard sections (Introduction, Data Collection, Permissions, etc.)
- **Footer** - Links to privacy policy and back to main site

Both index and privacy policy pages use the same color system and gradient headers for visual consistency.

---

## Common Development Tasks

### Adding a New App
1. Create new directory: `app-name/`
2. Add `privacy-policy.html` using the template from `simple-pomo/privacy-policy.html`
3. Update `assets/images/` with app icon (recommended size: 150x150px for cards)
4. Add app card to the apps grid in `index.html`:
   ```html
   <div class="app-card">
       <img src="assets/images/app-name.png" alt="App Name Logo">
       <h3>App Name</h3>
       <p>Short description</p>
       <ul class="app-features">
           <li>Feature 1</li>
           <li>Feature 2</li>
           <li>Feature 3</li>
       </ul>
   </div>
   ```
5. Ensure `app-name/privacy-policy.html` references images correctly with `../assets/images/` paths

### Updating Branding
- Colors: Modify CSS variables in `:root` selector (both `index.html` and `privacy-policy.html`)
- Logo: Replace `lotus-removebg-preview.png` in assets/images folder
- Typography: Update `font-family` in body styles
- Remember to keep CSS variable names consistent across all HTML files

### Adding Social Links
Edit the social links section in the contact area:
```html
<a href="URL" class="social-link" title="Platform Name" target="_blank" rel="noopener noreferrer">
    <i class="fa-brands fa-icon-name"></i>
</a>
```
Verify Font Awesome icon class names at fontawesome.com

### Updating Navigation
- Main menu links in header reference anchor sections: `#about`, `#apps`, `#contact`
- Privacy policy header navigation uses relative paths: `../index.html` for home
- Update footer links when adding new pages

---

## Key Files & Their Purposes

| File | Purpose | Size |
|------|---------|------|
| `index.html` | Main landing page with all sections | 18.4 KB |
| `simple-pomo/privacy-policy.html` | Privacy policy template | 17.4 KB |
| `assets/images/*` | Logo, app icons, branding assets | ~6 MB (11 files) |

---

## Important Implementation Details

### CSS Animations
Three custom animations used throughout:
- **fadeInDown** - Header animations (top to bottom)
- **fadeInUp** - Content animations (bottom to top, with staggered delays)
- **float** - Hero icon continuous floating effect

Use `animation: namehere duration ease direction;` for consistency.

### Flexbox & Grid Usage
- **Header:** Flex for horizontal navigation
- **Hero:** Flex with gap for spacing; switches to column on tablet
- **Apps Grid:** CSS Grid with `grid-template-columns: repeat(auto-fit, minmax(300px, 1fr))` for responsive cards
- **Social Links:** Flex with wrap for responsive alignment

### External Dependencies
Only **Font Awesome 6.7.2** from CDN is loaded:
```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.7.2/css/all.min.css">
```
No other external libraries or frameworks. Keep it minimal.

### Privacy & Data
- **Zero data collection** - This is a fundamental principle reflected in Simple Pomo's policy
- No analytics, tracking, or third-party services
- All app data stored locally on user devices
- Ensure future apps maintain this privacy-first approach

---

## Permissions & Constraints

Claude CLI is configured to allow only `mkdir` and `tree` bash commands in `.claude/settings.local.json`. Other operations must use appropriate tools (Read, Edit, Write, etc.).

---

## Testing & Quality

No testing infrastructure exists (appropriate for static HTML/CSS). Validation approach:
- Check responsive design at breakpoints: 480px, 768px, 1200px+
- Verify all links work (internal anchors and relative paths)
- Test all animations in different browsers
- Validate HTML/CSS with W3C validators
- Test Font Awesome icons render correctly

---

## Future Considerations

1. **Scalability:** Current structure supports adding multiple apps - just follow the `app-name/` directory pattern
2. **Localization:** All text is in English; prepare to extract strings if multi-language support needed
3. **SEO:** Add meta descriptions, og tags, and structured data as apps grow
4. **Build System:** Consider static site generator (Hugo, Jekyll) only if build process becomes necessary
5. **Performance:** Monitor image sizes in assets/ directory as they grow

---

## Quick Reference

- **Browser Support:** Modern browsers (CSS Grid, Flexbox, CSS Custom Properties)
- **Deployment:** Direct static file hosting (no build step required)
- **Font Awesome:** Always use Font Awesome icon classes for consistency
- **Color References:** Always use CSS variables, never hardcode hex values
- **Links:** Use relative paths for internal navigation, absolute for external
- **Mobile-First:** All new components should work on mobile (480px) first, then enhance for larger screens
