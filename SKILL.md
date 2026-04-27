---
name: nonprofit-website-builder
description: Build beautiful, functional multi-page HTML websites for nonprofit and public-interest organizations from information provided in chat. Use this skill whenever the user describes a nonprofit, NGO, charity, foundation, community organization, social enterprise, or any public-interest group and wants a website created for it. Also trigger when the user says things like "make a website for this organization", "build a site for our nonprofit", "create a website for this charity", "I need a website for a public welfare group", or provides organization details (mission, history, projects, team) and asks for a website. Even if the user just says "create a website" and the context involves a nonprofit or community org, use this skill.
---

# Nonprofit Website Builder

Build polished, multi-page HTML websites for nonprofit organizations based on information the user provides in chat. The output is a set of linked HTML files ready to open in any browser.

## Workflow

### Step 1: Gather Organization Info

The user provides org details directly in chat. Extract and organize:

- **Organization name**
- **Website URL** (if they have one; can be placeholder)
- **Email address** (required — goes in the top bar)
- **Mission / vision statement**
- **History / founding story**
- **Projects / programs** (name, description, impact)
- **Team members** (name, role, optional bio)
- **Contact info** (address, phone, social media)
- **Logo or branding colors** (if provided; otherwise auto-generate a palette)

If critical info is missing (e.g., no email, no mission), ask once — don't interview endlessly. Fill reasonable defaults for non-critical gaps (e.g., placeholder team bios, generic contact form).

### Step 2: Choose Design Direction

Pick a cohesive visual style based on the organization's domain. This is NOT random — match the aesthetic to what the org does:

| Org Type | Style Direction | Palette Tendency |
|---|---|---|
| Environmental / Wildlife | Organic, earthy, nature textures | Greens, warm browns, sky blues |
| Education / Youth | Bright, playful, energetic | Warm yellows, blues, coral |
| Health / Medical | Clean, trustworthy, calming | Soft blues, whites, teal |
| Human Rights / Advocacy | Bold, high-contrast, editorial | Deep navy, white, strong accent |
| Arts / Culture | Expressive, gallery-like, elegant | Muted tones with one bold accent |
| Community / Social Services | Warm, approachable, inclusive | Warm neutrals, orange, soft green |
| Technology / Innovation | Modern, minimal, forward-looking | Cool grays, electric blue, white |
| Disaster Relief / Humanitarian | Urgent yet hopeful, strong imagery feel | Red/orange accents, warm neutrals |

These are starting points — adapt freely. The key is intentionality: every color, font, and layout choice should feel like it belongs to THIS organization.

### Step 3: Build the Website

Generate these HTML files, all linked together via a shared navigation bar:

```
website/
├── index.html        (Home — hero section, org summary, call to action)
├── mission.html      (Mission & Vision — what the org stands for)
├── history.html      (History — founding story, timeline of milestones)
├── projects.html     (Projects — cards/grid of programs with descriptions)
├── team.html         (Team — member cards with photos placeholder and bios)
└── contact.html      (Contact — info, embedded map placeholder, contact form)
```

### Critical Layout Requirements

**Top Contact Bar (on EVERY page):**
```
┌──────────────────────────────────────────────────────────┐
│  ✉ info@org.com          │          🌐 www.org.com       │
├──────────────────────────────────────────────────────────┤
│  LOGO   ORG NAME     Home  Mission  History  ...        │
└──────────────────────────────────────────────────────────┘
```

The email and website URL MUST appear in a slim bar at the very top of every page, above the main navigation. This is non-negotiable — it's the first thing visitors see. Use a contrasting background color (typically darker than the nav) so it stands out.

**Navigation Bar:**
- Sticky/fixed below the top contact bar
- Clear active state for current page
- Mobile-responsive hamburger menu

**Footer (on EVERY page):**
- Org name, brief tagline
- Quick links to all pages
- Social media icons (placeholder links)
- Copyright line

### Step 4: Design & Code Quality Standards

**Typography:**
- Import 2 Google Fonts: one display/heading font, one body font
- Choose fonts that match the org's personality — avoid Inter, Roboto, Arial
- Clear hierarchy: h1 > h2 > h3 > body with deliberate size steps

**Color System:**
- Define a CSS custom property palette in a `<style>` block shared concept (duplicated in each file since these are standalone HTMLs):
  ```css
  :root {
    --color-primary: #...;
    --color-secondary: #...;
    --color-accent: #...;
    --color-bg: #...;
    --color-bg-alt: #...;
    --color-text: #...;
    --color-text-light: #...;
    --color-top-bar: #...;
    --color-top-bar-text: #...;
  }
  ```

**Responsive Design:**
- Mobile-first media queries
- Breakpoints: 768px (tablet), 1024px (desktop)
- Navigation collapses to hamburger on mobile
- Grid layouts adapt from multi-column to single column

**Animations & Polish:**
- Subtle fade-in on scroll for content sections (use IntersectionObserver)
- Hover effects on cards, buttons, and nav links
- Smooth scroll behavior
- Hero section with slight parallax or gradient animation

**Accessibility:**
- Semantic HTML (header, nav, main, section, article, footer)
- Alt text placeholders for images
- Sufficient color contrast (WCAG AA minimum)
- Focus-visible styles for keyboard nav

### Page-Specific Guidelines

**index.html (Home):**
- Full-width hero with org name, tagline, and a CTA button ("Learn More" or "Get Involved")
- 3-4 highlight cards summarizing key programs
- Impact stats section (numbers + short labels, e.g., "10,000+ Lives Touched")
- Testimonial or quote section

**mission.html (Mission):**
- Large, prominent mission statement
- Vision section
- Core values displayed as icon + text cards

**history.html (History):**
- Visual timeline of milestones (CSS-only, vertical with alternating left/right items)
- Founding story narrative section

**projects.html (Projects):**
- Grid of project cards with:
  - Placeholder image area (colored div with icon)
  - Project name, description, impact metric
  - "Learn More" button (can link to # or a detail section)

**team.html (Team):**
- Grid of team member cards
  - Circular placeholder avatar (initials-based or colored)
  - Name, role, short bio
  - Social/email links if provided

**contact.html (Contact):**
- Contact details (address, phone, email) in a clean layout
- A styled HTML contact form (name, email, subject, message) — non-functional but well-designed
- Map placeholder (styled gray box with "Map" label)
- Office hours if provided

### Step 5: Output

1. Create all HTML files in `/home/claude/website/`
2. Test that links between pages work (relative paths: `href="mission.html"`)
3. Copy all files to `/mnt/user-data/outputs/`
4. Present the files to the user with `present_files`, starting with `index.html`

Tell the user they can open `index.html` in their browser and navigate the full site. Briefly mention which pages are included — don't write a long walkthrough of every detail.

## Shared CSS Strategy

Since these are standalone HTML files (no build step), each file contains its own `<style>` block. To keep them consistent:

- Use identical CSS custom properties across all files
- The top bar, nav, and footer CSS are identical across files
- Page-specific styles come after the shared styles

A practical approach: write a mental "base stylesheet" and paste it into each file, then add page-specific styles. This duplication is intentional and necessary for standalone HTML files.

## What NOT To Do

- Don't use frameworks (React, Vue, Tailwind CDN) — pure HTML/CSS/JS only
- Don't use placeholder "Lorem ipsum" text — write real copy derived from the org's info
- Don't use stock photo URLs that might break — use colored placeholder divs with icons or SVG illustrations instead
- Don't create a single-page app — these must be separate HTML files that link to each other
- Don't forget the top contact bar — it's the user's #1 requirement
- Don't make all nonprofit sites look the same — vary the design based on the org type