---
title: "feat: AI Consulting Website"
status: active
origin: docs/brainstorms/2026-06-01-ai-consulting-website-requirements.md
date: 2026-06-01
---

# feat: AI Consulting Website

## Summary

Build a single-page consulting website for Andrey Sidorenko's AI consulting practice. Replace the existing portfolio site entirely. Use modern vanilla HTML/CSS without frameworks. Position as a deep technical specialist who ships production AI fast.

---

## Problem Frame

Andrey is launching an AI consulting practice targeting SMEs in DACH/Eastern Europe. The current portfolio site (2018 web dev projects, Bootstrap 3) doesn't serve this purpose. He needs a professional site that establishes credibility without looking like generic AI consultant template sites — no gradient blobs, no "unlock the power of AI" messaging.

(see origin: docs/brainstorms/2026-06-01-ai-consulting-website-requirements.md)

---

## Requirements

**R1.** Single-page site with 5 sections: Hero, About, Services, Portfolio/Proof, Contact  
**R2.** "Engineering pragmatism" visual direction — functional, direct, monospace accents, muted colors  
**R3.** Messaging leads with specifics (TabularARGN, MOSTLY AI), avoids buzzwords  
**R4.** Mobile responsive  
**R5.** Static site hosted on GitHub Pages  
**R6.** No backend, no contact forms — email link only

---

## Key Technical Decisions

### KTD1: Modern vanilla CSS, no framework

**Decision:** Use CSS Grid, Flexbox, and custom properties instead of Bootstrap or other frameworks.

**Rationale:** Fits the "engineering pragmatism" aesthetic — no bloat, full control, demonstrates technical competence. The site is simple enough that a framework adds complexity without benefit. Removing Bootstrap 3 also modernizes the codebase.

### KTD2: Replace index.html entirely

**Decision:** The new consulting site becomes the main `index.html`. Old portfolio content remains in `projects/` but is no longer linked from the main page.

**Rationale:** The old portfolio (weather app, wiki viewer, quote generator) reflects 2018 web dev learning projects, not current professional positioning as an AI research leader. Clean break is better than awkward coexistence.

### KTD3: Font choices for "engineering pragmatism"

**Decision:** JetBrains Mono (or similar monospace) for code/technical accents. Inter or IBM Plex Sans for body text. Both from Google Fonts.

**Rationale:** Monospace fonts signal technical credibility without being gimmicky. Inter/IBM Plex are clean, highly legible, and commonly used in developer tools and documentation.

### KTD4: Keep Font Awesome for service icons

**Decision:** Retain Font Awesome (upgrade to v6) for the 4 service icons.

**Rationale:** Already in use, well-maintained, provides appropriate technical icons (code brackets, cogs, integration symbols, chalkboard). Lighter than adding a separate icon library.

### KTD5: Color palette

**Decision:** Near-black background for hero (#0d1117 or similar), off-white for content sections (#f6f8fa), dark gray for text (#24292f). Accent color: muted blue (#2f81f7) for links and highlights.

**Rationale:** Inspired by GitHub's dark/light modes — familiar to technical audiences, high contrast, professional without being cold. Avoids gradients and neon.

---

## Scope Boundaries

### In Scope
- Complete replacement of index.html
- New CSS file (consulting.css or similar)
- All 5 sections per requirements
- Mobile-first responsive design
- Placeholder slots for: headshot image, arXiv paper links, GitHub repos, MOSTLY AI public links

### Deferred to Follow-Up Work
- German language version
- Blog/content section
- Client testimonials (none exist yet)
- Animated interactions beyond basic hover states
- Removing orphaned files (old projects/, css/portfolio.css) — user can clean up later

### Outside This Scope
- Multi-page architecture
- Contact forms or calendar booking
- CMS or build tooling
- SEO optimization beyond basic meta tags

---

## Implementation Units

### U1. Base HTML structure and CSS foundation

**Goal:** Create the new index.html skeleton and CSS file with reset, custom properties, and typography.

**Requirements:** R1, R2, R5

**Dependencies:** None

**Files:**
- `index.html` (replace existing)
- `css/consulting.css` (create new)

**Approach:**
- HTML5 semantic structure with `<header>`, `<main>`, `<section>`, `<footer>`
- CSS reset (modern minimal reset, not normalize.css)
- Define CSS custom properties for colors, fonts, spacing
- Import Google Fonts (Inter + JetBrains Mono)
- Keep Font Awesome v6 via CDN
- Remove Bootstrap and jQuery dependencies

**Patterns to follow:** Modern HTML5 boilerplate patterns. Reference GitHub's UI for color variable naming.

**Test scenarios:**
- Page loads without console errors
- Fonts render correctly
- CSS variables are applied (inspect in dev tools)

---

### U2. Sticky navigation

**Goal:** Build the fixed top navigation with logo and section links.

**Requirements:** R1, R4

**Dependencies:** U1

**Files:**
- `index.html` (nav section)
- `css/consulting.css` (nav styles)

**Approach:**
- `position: sticky` with `top: 0`
- Simple horizontal nav: Logo/name on left, section links on right
- Mobile: hamburger menu with CSS-only toggle (no JS) or simple stacked links
- Links: About, Services, Portfolio, Contact
- Smooth scroll via `scroll-behavior: smooth` on html

**Patterns to follow:** CSS-only hamburger menus using checkbox hack if needed for mobile.

**Test scenarios:**
- Nav stays fixed when scrolling
- All section links navigate to correct anchors
- Mobile: nav is usable on 375px width screen
- Smooth scroll works between sections

---

### U3. Hero section

**Goal:** Build the hero with bold headline and value proposition.

**Requirements:** R1, R2, R3

**Dependencies:** U1, U2

**Files:**
- `index.html` (hero section)
- `css/consulting.css` (hero styles)

**Approach:**
- Full viewport height (`min-height: 100vh`)
- Dark background (#0d1117)
- Centered content: headline + 1-2 sentence value prop
- Example headline: "I build production AI systems"
- Example subtext: "Previously Head of AI Research at MOSTLY AI. Now available for prototype sprints, product development, and technical training."
- No background image or parallax — clean solid color
- CTA: scroll indicator or "See my work" anchor link

**Patterns to follow:** Minimalist hero patterns from Stripe, Linear, or Vercel landing pages.

**Test scenarios:**
- Hero fills viewport on desktop
- Text is readable (sufficient contrast)
- Hero scales appropriately on mobile
- No horizontal scroll on any viewport

---

### U4. About section

**Goal:** Build the bio section with headshot and credentials.

**Requirements:** R1, R2, R3

**Dependencies:** U1

**Files:**
- `index.html` (about section)
- `css/consulting.css` (about styles)
- `images/headshot.jpg` (user will add)

**Approach:**
- Light background (#f6f8fa)
- Two-column layout on desktop: photo left, bio text right (CSS Grid)
- Single column on mobile: photo above text
- Bio: 3-4 sentences, first person, confident tone
- Credentials listed: PhD, MOSTLY AI role, years of experience
- Circular or rounded-square photo frame

**Patterns to follow:** Simple profile layouts from personal sites of respected engineers.

**Test scenarios:**
- Layout shifts to single column below 768px
- Photo placeholder displays if image missing
- Text is scannable (appropriate line height, paragraph spacing)

---

### U5. Services section

**Goal:** Build the 4-service grid with icons and descriptions.

**Requirements:** R1, R2

**Dependencies:** U1

**Files:**
- `index.html` (services section)
- `css/consulting.css` (services styles)

**Approach:**
- Section title: "Services" or "How I Can Help"
- 4-column CSS Grid on desktop, 2x2 on tablet, single column on mobile
- Each service card: icon (Font Awesome) + title + 1-2 sentence description
- Services:
  1. AI Prototype Sprint — `fa-rocket` or `fa-bolt`
  2. AI Product Development — `fa-code`
  3. AI System Integration — `fa-plug` or `fa-link`
  4. Technical AI Training — `fa-chalkboard-teacher`
- Subtle card styling (light border or shadow), not heavy boxes
- Equal visual weight — no service emphasized over others

**Patterns to follow:** Feature grids from developer tool landing pages.

**Test scenarios:**
- All 4 services visible on desktop in single row
- Grid reflows to 2x2 on tablet (768px-1024px)
- Grid becomes single column on mobile (<768px)
- Icons render correctly
- Cards have consistent height regardless of content length

---

### U6. Portfolio/Proof section

**Goal:** Build the evidence section with links to papers, GitHub, and public work.

**Requirements:** R1, R3

**Dependencies:** U1

**Files:**
- `index.html` (portfolio section)
- `css/consulting.css` (portfolio styles)

**Approach:**
- Section title: "Work" or "Evidence" (not "Portfolio" — too generic)
- Three subsections or a simple list:
  1. **Research:** Links to arXiv papers (TabularARGN, LLM tabular generation, benchmarking framework)
  2. **Code:** GitHub profile link, potentially specific repos
  3. **MOSTLY AI:** Links to any public blog posts, talks, or press (placeholder if none identified)
- Clean link styling with subtle hover effects
- Optional: small description for each paper/link
- No client logos or fake testimonials

**Patterns to follow:** "Selected work" sections from researcher personal sites.

**Test scenarios:**
- All links open in new tab (`target="_blank"`)
- Links have appropriate hover states
- Section is scannable — visitor can quickly see what's available

---

### U7. Contact and footer

**Goal:** Build the contact section and site footer.

**Requirements:** R1, R6

**Dependencies:** U1

**Files:**
- `index.html` (contact and footer sections)
- `css/consulting.css` (contact/footer styles)

**Approach:**
- Contact section: simple heading ("Let's Talk" or "Contact"), email address as mailto link, brief text
- Location: Vienna, Austria
- Footer: social links row (LinkedIn, GitHub, Google Scholar, optionally Twitter)
- Use Font Awesome for social icons
- Copyright line (minimal: "© 2026 Andrey Sidorenko")
- Dark footer background to bookend with hero

**Patterns to follow:** Minimal footers from developer portfolios.

**Test scenarios:**
- Email link opens mail client
- Social links open correct profiles in new tabs
- Footer is visible on all pages without excessive scrolling past content

---

### U8. Responsive polish and final QA

**Goal:** Ensure the site works well across all viewport sizes and fix any remaining issues.

**Requirements:** R4

**Dependencies:** U2, U3, U4, U5, U6, U7

**Files:**
- `css/consulting.css` (media queries, fixes)
- `index.html` (any structural fixes)

**Approach:**
- Test at key breakpoints: 375px (mobile), 768px (tablet), 1024px (small desktop), 1440px (large desktop)
- Verify no horizontal scroll at any width
- Check touch targets are appropriately sized on mobile (min 44px)
- Verify navigation works on mobile
- Test in Chrome, Firefox, Safari
- Add meta viewport tag if not present
- Add basic meta tags (description, og:image placeholder)

**Test scenarios:**
- Site renders correctly at 375px width
- Site renders correctly at 1440px width
- No console errors in any browser
- All interactive elements have visible focus states
- Page passes basic Lighthouse accessibility audit

---

## Open Questions (Deferred to Implementation)

1. **Exact paper links:** Need to identify the specific arXiv URLs for TabularARGN, LLM tabular generation paper, and benchmarking framework paper.
2. **MOSTLY AI public content:** Need to research what blog posts, talks, or press coverage exists that can be linked.
3. **Exact copy:** Final headline, bio text, and service descriptions will be refined during implementation based on what reads well.

---

## Sources & Research

- Origin requirements document captures design direction and messaging principles
- Existing site examined for structure and assets to preserve (favicon, potential images)
- GitHub UI/colors referenced as inspiration for the "engineering pragmatism" palette

---

## Verification

The site is complete when:
1. Opening `index.html` locally shows all 5 sections rendering correctly
2. Site is responsive from 375px to 1440px without horizontal scroll
3. All links (email, social, papers) work correctly
4. Visual direction matches requirements: clean, functional, no gradients/stock imagery
5. Messaging is specific (names actual projects/roles) not generic buzzwords
