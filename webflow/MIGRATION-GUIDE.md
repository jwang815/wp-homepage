# Waypoint Journeys — GitHub Pages to Webflow Migration Guide

This guide walks you through migrating the Waypoint Journeys homepage from GitHub Pages into Webflow with a **100% visual match**.

---

## Files Overview

| File | Purpose |
|------|---------|
| `styles.css` | All custom CSS (variables, layout, animations, responsive) |
| `scripts.js` | All JavaScript (slideshow, scroll effects, mobile menu, parallax) |
| `head-code.html` | Meta tags, fonts, and CSS — goes in Webflow Head Code |
| `body-code.html` | JavaScript — goes in Webflow Before `</body>` Code |
| `page-embed.html` | Full page HTML — used as Webflow Embed element(s) |

---

## Quick Start (Approach A — Full Embed)

This is the **fastest method** and guarantees a pixel-perfect 100% match.

### Step 1: Set Up Webflow Project

1. Log into [Webflow](https://webflow.com) and create a new project (or open your existing one)
2. Create a **new blank page** (name it "Home" or your preferred slug)
3. In Page Settings, set the page title to:
   ```
   Waypoint Journeys — Luxury Expeditions to the World's Last Wild Places
   ```

### Step 2: Add Head Code

1. Go to **Site Settings** (gear icon) → **Custom Code** → **Head Code**
2. Paste the contents of `head-code.html`
3. **Important**: Either:
   - Upload `styles.css` to Webflow's **Asset Manager** and replace `YOUR_ASSET_URL` with the actual URL, OR
   - Paste the entire contents of `styles.css` between the `<style>` tags in head-code.html

### Step 3: Add Body Code

1. In the same Custom Code page, scroll to **Before `</body>` tag**
2. Paste the contents of `body-code.html`
3. **Important**: Either:
   - Upload `scripts.js` to Webflow's **Asset Manager** and replace `YOUR_ASSET_URL` with the actual URL, OR
   - Keep the inline `<script>` block (already included in body-code.html)

### Step 4: Add Page Content

1. Go to the **Webflow Designer** and select your new page
2. Add an **Embed** element (HTML Embed) to the page body
3. Paste the entire contents of `page-embed.html` into the embed
4. Click **Save & Close**

### Step 5: Publish

1. Click **Publish** in the top-right corner
2. Verify the site matches the original GitHub Pages version

---

## Approach B — Section-by-Section (More Control)

If you want more granular control in the Webflow Designer, you can split the page into multiple Embed elements:

### Page Structure

Create these sections as **separate HTML Embed elements** in order:

1. **Navigation Embed** — Copy the `<!-- NAVIGATION -->` section from page-embed.html
2. **Mobile Menu Embed** — Copy the `<!-- Mobile Menu -->` div
3. **Hero Embed** — Copy the `<!-- HERO -->` section
4. **Philosophy Embed** — Copy the `<!-- PHILOSOPHY -->` section
5. **Expeditions Embed** — Copy the `<!-- EXPEDITIONS -->` section
6. **Stats Embed** — Copy the `<!-- STATS STRIP -->` section
7. **Testimonial Embed** — Copy the `<!-- TESTIMONIAL -->` section
8. **CTA Embed** — Copy the `<!-- CTA -->` section
9. **Footer Embed** — Copy the `<!-- FOOTER -->` section

Each section in `page-embed.html` is clearly marked with HTML comments for easy copy-paste.

---

## Design Specifications

### Color Palette

| Name | Hex | Usage |
|------|-----|-------|
| Charcoal | `#1A1A1A` | Primary dark background |
| Charcoal Deep | `#111111` | Darker sections (expeditions, CTA) |
| Sand | `#F5EDE0` | Light accent, philosophy background |
| Sand Light | `#FAF6F0` | Lighter accent |
| Gold | `#C4944A` | Primary brand accent |
| Gold Light | `#D4A85C` | Hover state gold |
| Teal | `#1B5E6B` | Secondary color |
| White | `#FFFFFF` | Hero text |
| Off-White | `#E8E0D4` | Subtle text |

### Typography

| Element | Font | Weight | Size |
|---------|------|--------|------|
| Headings (H1, H2) | Playfair Display | 500 | clamp(2rem, 3.5vw, 5rem) |
| Body Text | Source Sans 3 | 300-400 | 1.05rem |
| Labels/Tags | Source Sans 3 | 600 | 0.68-0.78rem |
| Nav Links | Source Sans 3 | 500 | 0.78rem |
| Buttons | Source Sans 3 | 600 | 0.72-0.82rem |

### Breakpoints

| Breakpoint | Changes |
|------------|---------|
| 1024px | Philosophy: single column, expedition grid stays 2-col |
| 768px | Mobile menu, single-col expeditions, 2x2 stats, reduced padding |
| 480px | Smaller fonts, tighter spacing |

---

## External Resources

### Images Used

All images are loaded from Unsplash CDN. If you want to self-host:

| Image | URL | Used In |
|-------|-----|---------|
| Desert Trail | `photo-1682686581660-3693f0c588d2` | Hero Slide 1 |
| Canyon | `photo-1506905925346-21bda4d32df4` | Hero Slide 2, Pakistan card |
| Clifftop Ruins | `photo-1587135941948-670b381f08ce` | Philosophy section |
| Tropical Lagoon | `photo-1559128010-7c1ad6e1b6a5` | Socotra card |
| Arctic Aurora | `photo-1531366936337-7c912a4589a7` | Stats background |

### Google Fonts

- **Playfair Display**: 400, 500, 600, 700 (regular + italic)
- **Source Sans 3**: 300, 400, 500, 600, 700

Both are loaded via the `<link>` tag in `head-code.html`.

---

## Interactive Features

The following features are handled by the JavaScript in `scripts.js` / `body-code.html`:

1. **Hero Slideshow** — Auto-rotates every 6 seconds with fade + Ken Burns zoom
2. **Navigation Scroll** — Nav gets dark background + blur after 80px scroll
3. **Mobile Hamburger Menu** — Toggle overlay menu on mobile
4. **Scroll Reveal** — Elements animate in as they enter the viewport
5. **Parallax Hero** — Hero content shifts with parallax on scroll
6. **Smooth Scrolling** — Internal anchor links scroll smoothly

---

## Webflow-Specific Notes

### Avoiding Style Conflicts

The CSS uses specific class names prefixed to avoid conflicts with Webflow's default styles:
- `.wp-nav` instead of `.nav` (Webflow may use `.nav` internally)
- `.wp-footer` instead of `.footer`

### Webflow Interactions (Optional)

If you prefer using Webflow's native Interactions instead of JavaScript for the scroll reveal animations:

1. Remove the "Scroll Reveal" section from the JavaScript
2. Remove the `reveal` and `reveal-delay-*` classes from the HTML
3. Set up Webflow interactions:
   - Trigger: "While scrolling in view"
   - Animation: Fade in + Move up 40px
   - Stagger child elements by 150ms

### CMS Integration (Optional)

To make expeditions dynamic using Webflow CMS:

1. Create a CMS Collection called "Expeditions" with fields:
   - Name (text)
   - Subtitle (text)
   - Tag (text, e.g., "Featured Expedition")
   - Date (text)
   - Price (text)
   - Image (image)
   - Link (URL)
2. Replace the static expedition cards with a CMS Collection List
3. Bind the fields to each card element

---

## Troubleshooting

### Styles not loading
- Make sure the CSS is either inline in the Head Code `<style>` tags, or properly linked as an external file from Webflow Assets

### JavaScript not working
- Ensure the script is in the "Before `</body>` tag" section, not the Head Code
- Check the browser console for errors (F12 → Console)

### Mobile menu not working
- The `closeMobileMenu` function must be globally accessible. The body-code.html attaches it to `window.closeMobileMenu`

### Fonts not rendering
- Verify the Google Fonts `<link>` tag is in the Head Code
- Check that Webflow isn't overriding font-family on body elements

---

## Verification Checklist

After publishing, verify these elements match the original:

- [ ] Hero slideshow rotates with fade effect
- [ ] Navigation becomes opaque on scroll
- [ ] Mobile hamburger menu works on mobile/tablet
- [ ] Philosophy section: 2-column layout on desktop, stacked on mobile
- [ ] Expedition cards: hover zoom effect works
- [ ] Stats section: 4-column on desktop, 2x2 on tablet/mobile
- [ ] Testimonial: centered with gold line and quotation mark
- [ ] CTA section: gold vertical line at top
- [ ] Footer: social icons with hover effect
- [ ] Scroll reveal animations fire on all sections
- [ ] Parallax effect on hero content
- [ ] Smooth scrolling for internal links
- [ ] All responsive breakpoints (1024px, 768px, 480px)
