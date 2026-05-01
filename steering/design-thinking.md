# Design Thinking — Analyze, Suggest, and Improve UI

Read this when the user asks to improve the design, make something look better, or when you notice design issues during the visual feedback loop.

## The 2-Second Test

Before any systematic analysis, look at the screenshot as a first-time visitor:
- What draws your eye first? Is that the right thing?
- Does it feel professional or rough?
- Is the purpose of the page immediately clear?
- Does it feel cluttered or clean?

Your gut reaction matters. If something feels off, it probably is.

## 7 Design Principles to Evaluate

### 1. Visual Hierarchy
Is it clear what to look at first? Do headings stand out? Do primary CTAs pop?

**Quick fixes**: Increase heading size, add color to primary buttons, reduce visual weight of secondary elements, add whitespace between sections.

### 2. Spacing & Rhythm
Is spacing consistent? Do related elements feel grouped? Is there breathing room?

**Use a spacing scale**: 4px, 8px, 16px, 24px, 32px, 48px, 64px. Pick values from this scale and use them consistently.

**Quick fixes**: Increase container padding, add margin between sections, align to a grid.

### 3. Typography
Too many font sizes? (aim for 3-5). Body text readable? (16px+ for body). Line height comfortable? (1.4-1.6 for body).

**Quick fixes**: Reduce font size variations, increase body text to 16px, set `line-height: 1.6`, improve contrast.

### 4. Color & Contrast
Cohesive palette? Sufficient contrast? (WCAG AA: 4.5:1 for text). Colors used consistently?

**Quick fixes**: Reduce color count (1 primary, 1 secondary, neutrals), increase contrast ratios, use color consistently for interactive elements.

### 5. Alignment & Consistency
Elements on a grid? Similar elements look similar? Consistent border-radius? Consistent shadows?

**Quick fixes**: Align to a common grid, standardize component styles, pick one border-radius (8px is safe) and use everywhere.

### 6. Responsive Behavior
Works at current viewport? Horizontal scrollbars? (almost always a bug). Images scale? Text readable?

**Quick fixes**: Use flexbox/grid, set max-widths, use responsive images, adjust font sizes for mobile.

### 7. Whitespace
Enough breathing room? Sections clearly separated? Page feels balanced?

**Quick fixes**: Increase padding, add section spacing (48-64px between major sections), reduce content density.

## Design Review Workflow

### Step 1: Capture
`browser_screen_capture` — get the current state.

### Step 2: 2-Second Test
First impression analysis (see above).

### Step 3: Systematic Review
Go through each of the 7 principles. For each, note what's working and what could improve.

### Step 4: Prioritize by Impact
1. **High impact, low effort** → do first (spacing, font sizes, colors)
2. **High impact, high effort** → plan (layout restructuring)
3. **Low impact, low effort** → do if time allows (micro-interactions)
4. **Low impact, high effort** → skip unless asked

### Step 5: Present to User
- Lead with what's working (positive feedback builds trust)
- Suggest 3-5 specific improvements ranked by impact
- For each, explain WHY it improves the design, not just WHAT to change
- Ask which ones they want implemented

### Step 6: Implement & Verify
For each approved improvement: fix → wait → screenshot → confirm → next.

## Translating User Language

| User says | Design action |
|-----------|--------------|
| "make it look better" | Improve spacing, typography, color consistency |
| "make it modern" | Clean layout, whitespace, subtle shadows, rounded corners, system fonts |
| "make it professional" | Consistent styling, proper alignment, restrained palette |
| "make it pop" | Stronger hierarchy, bolder colors, more contrast |
| "it feels cramped" | Add whitespace and padding everywhere |
| "it looks boring" | Add color accents, better typography, visual interest |
| "it looks messy" | Fix alignment, consistency, spacing |
| "make it clean" | Reduce visual noise, increase whitespace, simplify |
| "make it like [site]" | Open reference in new tab, screenshot, analyze patterns, replicate |
| "center it" | Vertically + horizontally center content |
| "make it responsive" | Test mobile/tablet/desktop, fix breakpoints |
| "add some style" | Better typography, color palette, subtle shadows, hover states |
| "it needs work" | Full design review using the 7 principles |

## Design Comparison Workflow

When matching a reference design:

1. `browser_tab_new` → navigate to reference URL
2. `browser_screen_capture` → capture reference
3. Switch back to user's app tab
4. `browser_screen_capture` → capture current state
5. Compare systematically: layout, spacing, typography, colors, components
6. List differences, implement fixes one by one
7. Re-screenshot and compare after each batch

## 10 Quick Fixes That Always Help

These almost universally improve a page:

1. **`max-width: 1200px; margin: 0 auto`** on the main container — prevents ultra-wide lines
2. **`line-height: 1.6`** on body text — instant readability boost
3. **48-64px** between major sections — breathing room
4. **One border-radius value** (8px) used everywhere — consistency
5. **One primary color** for all CTAs and interactive elements — clarity
6. **`box-shadow: 0 1px 3px rgba(0,0,0,0.1)`** on cards — subtle depth
7. **System font stack**: `-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif`
8. **16px minimum** for body text — readability
9. **Consistent padding** inside all containers (16px mobile, 24px tablet, 32px desktop)
10. **Reduce color count** — one primary, one secondary, grays for everything else

## JavaScript Snippets for Design Analysis

Run these via `browser_javascript_execute` for data-driven design decisions:

```javascript
// All unique font sizes on the page (should be 3-5)
[...new Set([...document.querySelectorAll('*')].map(el =>
  getComputedStyle(el).fontSize))].sort()

// All unique text colors (should be 3-5)
[...new Set([...document.querySelectorAll('*')].map(el =>
  getComputedStyle(el).color))].filter(c => c !== 'rgb(0, 0, 0)').sort()

// All unique background colors
[...new Set([...document.querySelectorAll('*')].map(el =>
  getComputedStyle(el).backgroundColor))].filter(c => c !== 'rgba(0, 0, 0, 0)').sort()

// Elements overflowing the viewport (horizontal scroll bugs)
[...document.querySelectorAll('*')].filter(el =>
  el.getBoundingClientRect().right > window.innerWidth
).map(el => ({ tag: el.tagName, class: el.className, width: Math.round(el.getBoundingClientRect().width) }))

// Spacing between sections
const sections = document.querySelectorAll('section, [class*="section"], main > div');
[...sections].map((el, i) => {
  if (i === 0) return null;
  const gap = el.getBoundingClientRect().top - sections[i-1].getBoundingClientRect().bottom;
  return { between: `${sections[i-1].className || sections[i-1].tagName} → ${el.className || el.tagName}`, gap: Math.round(gap) + 'px' };
}).filter(Boolean)

// Check contrast ratio of text elements
function luminance(r, g, b) {
  const [rs, gs, bs] = [r, g, b].map(c => { c /= 255; return c <= 0.03928 ? c / 12.92 : Math.pow((c + 0.055) / 1.055, 2.4); });
  return 0.2126 * rs + 0.7152 * gs + 0.0722 * bs;
}
function contrastRatio(l1, l2) { return (Math.max(l1, l2) + 0.05) / (Math.min(l1, l2) + 0.05); }
// Use on specific elements to check WCAG compliance
```

## Color Palette Suggestions

When the user needs a color palette and doesn't have one:

### Safe Professional Palettes
- **Blue**: Primary `#2563EB`, Dark `#1E40AF`, Light `#DBEAFE`
- **Green**: Primary `#059669`, Dark `#047857`, Light `#D1FAE5`
- **Purple**: Primary `#7C3AED`, Dark `#6D28D9`, Light `#EDE9FE`
- **Neutral**: Text `#111827`, Secondary `#6B7280`, Border `#E5E7EB`, Background `#F9FAFB`

### Dark Mode Equivalents
- Background: `#0F172A` or `#1E293B`
- Text: `#F1F5F9`
- Secondary text: `#94A3B8`
- Border: `#334155`
- Card background: `#1E293B` or `#334155`
