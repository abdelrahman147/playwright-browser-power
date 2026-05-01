# Quick Recipes — Ready-to-Go Workflows

Each recipe is a sequence of tool calls for a specific task. Pick the one that matches what you need.

---

## Recipe 1: Open a Page and Report

**Trigger**: "open my app", "check localhost", "browse to X", "show me the page"

1. `browser_navigate` → URL
2. `browser_wait` → 2s
3. `browser_javascript_execute` → `window.__kiro.status('Checking for errors...')`
4. `browser_console_messages` → check errors
5. `browser_javascript_execute` → `window.__kiro.status('Reading page structure...')`
6. `browser_snapshot` → page structure
7. `browser_javascript_execute` → `window.__kiro.hide()` (clean screenshot)
8. `browser_screen_capture` → visual state
9. `browser_javascript_execute` → `window.__kiro.show()`
10. Report: what's on the page, any errors, overall impression

---

## Recipe 2: Full Health Check

**Trigger**: "is everything working?", "check the page", "any issues?"

1. `browser_navigate` → URL
2. `browser_wait` → 2s
3. `browser_console_messages` → JS errors
4. `browser_snapshot` → structure + accessibility
5. `browser_screen_capture` → visual state
6. `browser_network_requests` → failed requests
7. Report organized by severity: errors → warnings → suggestions

---

## Recipe 3: Responsive Check (3 Viewports)

**Trigger**: "check responsive", "how does it look on mobile?", "test breakpoints"

**Desktop (1280x720)** — default viewport:
1. `browser_navigate` → URL
2. `browser_wait` → 2s
3. `browser_screen_capture` → desktop view

**Tablet (768x1024)**:
4. `browser_javascript_execute`:
```javascript
// Simulate tablet viewport
document.querySelector('meta[name="viewport"]')?.setAttribute('content', 'width=768');
document.documentElement.style.maxWidth = '768px';
document.documentElement.style.margin = '0 auto';
```
5. `browser_wait` → 1s
6. `browser_screen_capture` → tablet view

**Mobile (375x812)**:
7. `browser_javascript_execute`:
```javascript
document.querySelector('meta[name="viewport"]')?.setAttribute('content', 'width=375');
document.documentElement.style.maxWidth = '375px';
document.documentElement.style.margin = '0 auto';
```
8. `browser_wait` → 1s
9. `browser_screen_capture` → mobile view

10. Report issues at each breakpoint

**Better alternative**: Open 3 separate tabs, each navigated to the same URL, and use JS to set different widths. This lets you compare side by side.

---

## Recipe 4: Fill and Submit a Form

**Trigger**: "test the form", "fill out the form", "check form validation"

1. `browser_navigate` → form page
2. `browser_snapshot` → identify all form fields and their refs
3. For each field:
   - `browser_click` → the field
   - `browser_type` → appropriate test data
4. `browser_screen_capture` → verify filled state
5. `browser_click` → submit button
6. `browser_wait` → 2s
7. `browser_snapshot` → check success/error messages
8. `browser_screen_capture` → verify result

### Validation Test:
Repeat with invalid data (empty required fields, bad email format, etc.) to verify error states.

---

## Recipe 5: Compare Two Pages

**Trigger**: "compare these pages", "make mine look like this", "check the reference"

1. `browser_tab_new` + `browser_navigate` → first URL
2. `browser_wait` → 2s
3. `browser_screen_capture` → capture page 1
4. `browser_tab_new` + `browser_navigate` → second URL
5. `browser_wait` → 2s
6. `browser_screen_capture` → capture page 2
7. Compare: layout, spacing, typography, colors, components
8. Report differences with specific suggestions

---

## Recipe 6: Debug a Visual Bug

**Trigger**: "something looks wrong", "there's a bug", "this doesn't look right"

1. `browser_navigate` → affected page
2. `browser_wait` → 2s
3. `browser_console_messages` → JS errors (often the root cause)
4. `browser_screen_capture` → see current state
5. `browser_snapshot` → check DOM structure
6. `browser_javascript_execute` → inspect the problematic element:
```javascript
const el = document.querySelector('.problematic-element');
if (el) {
  const s = getComputedStyle(el);
  const r = el.getBoundingClientRect();
  JSON.stringify({
    display: s.display, visibility: s.visibility, opacity: s.opacity,
    width: r.width + 'px', height: r.height + 'px',
    position: s.position, overflow: s.overflow,
    zIndex: s.zIndex, transform: s.transform
  }, null, 2);
} else { 'Element not found in DOM'; }
```
7. Identify root cause → fix → `browser_wait` → re-verify

---

## Recipe 7: Accessibility Audit

**Trigger**: "check accessibility", "is it accessible?", "a11y check"

1. `browser_navigate` → page
2. `browser_snapshot` → THE accessibility tree (this IS the audit)
3. Check for:
   - Missing button/link labels
   - Images without alt text
   - Inputs without labels
   - Heading hierarchy (h1 → h2 → h3, no skips)
   - Missing landmark regions (nav, main, footer)
   - Missing ARIA roles on custom interactive elements
4. `browser_javascript_execute` → deeper checks:
```javascript
JSON.stringify({
  imagesWithoutAlt: [...document.querySelectorAll('img:not([alt])')].map(i => i.src.split('/').pop()),
  buttonsWithoutLabel: [...document.querySelectorAll('button')].filter(b =>
    !b.textContent.trim() && !b.getAttribute('aria-label')).length,
  inputsWithoutLabel: [...document.querySelectorAll('input:not([type="hidden"])')].filter(i =>
    !i.labels?.length && !i.getAttribute('aria-label')).map(i => i.type + ':' + (i.name || 'unnamed')),
  headingOrder: [...document.querySelectorAll('h1,h2,h3,h4,h5,h6')].map(h => h.tagName + ': ' + h.textContent.trim().slice(0, 40)),
  missingLandmarks: {
    hasNav: !!document.querySelector('nav'),
    hasMain: !!document.querySelector('main'),
    hasFooter: !!document.querySelector('footer')
  }
}, null, 2)
```
5. Report findings with specific fixes

---

## Recipe 8: Generate PDF

**Trigger**: "save as PDF", "generate PDF", "export page"

1. `browser_navigate` → page
2. `browser_wait` → 3s (ensure full render including images/fonts)
3. `browser_pdf_save` → generates the PDF
4. Report file location

---

## Recipe 9: Test a User Flow

**Trigger**: "test the signup flow", "walk through checkout", "test the user journey"

1. `browser_navigate` → starting page
2. `browser_screen_capture` → document start state
3. For each step:
   - Perform action (`browser_click`, `browser_type`, etc.)
   - `browser_wait` → for transitions
   - `browser_screen_capture` → document state
   - `browser_console_messages` → check for errors
4. Report the full flow with findings at each step

---

## Recipe 10: Network Debug

**Trigger**: "check API calls", "why isn't data loading?", "debug network"

1. `browser_navigate` → page
2. `browser_wait` → 3s
3. `browser_network_requests` → list all requests
4. Look for:
   - 4xx/5xx status codes (failed requests)
   - Missing requests (API calls that should happen but don't)
   - Slow requests (high latency)
   - CORS errors
5. Report findings with suggested fixes

---

## Recipe 11: Mock an API

**Trigger**: "mock the API", "fake the data", "test with different data"

1. `browser_route`:
   - pattern: API endpoint (e.g., `"/api/users"`)
   - status: 200
   - body: JSON string of mock data
   - contentType: `"application/json"`
2. `browser_navigate` → page (or reload)
3. `browser_wait` → 2s
4. `browser_screen_capture` → verify page renders with mock data

---

## Recipe 12: Dark Mode Check

**Trigger**: "check dark mode", "test the theme", "toggle dark mode"

1. `browser_navigate` → page
2. `browser_screen_capture` → light mode
3. `browser_javascript_execute`:
```javascript
// Try common dark mode toggles
document.documentElement.classList.toggle('dark') ||
document.body.setAttribute('data-theme', 'dark') ||
(document.documentElement.style.colorScheme = 'dark');
'toggled'
```
4. `browser_wait` → 1s
5. `browser_screen_capture` → dark mode
6. Compare: contrast issues, missing dark styles, unreadable text, unstyled elements

---

## Recipe 13: Performance Quick Check

**Trigger**: "is it slow?", "check performance", "loading time"

1. `browser_navigate` → page
2. `browser_wait` → 3s
3. `browser_javascript_execute`:
```javascript
const nav = performance.getEntriesByType('navigation')[0];
const resources = performance.getEntriesByType('resource');
JSON.stringify({
  timing: {
    domContentLoaded: Math.round(nav.domContentLoadedEventEnd - nav.startTime) + 'ms',
    fullLoad: Math.round(nav.loadEventEnd - nav.startTime) + 'ms',
    firstByte: Math.round(nav.responseStart - nav.startTime) + 'ms'
  },
  resources: {
    total: resources.length,
    totalSize: Math.round(resources.reduce((s, r) => s + (r.transferSize || 0), 0) / 1024) + 'KB',
    largest: resources.sort((a, b) => (b.transferSize || 0) - (a.transferSize || 0)).slice(0, 5)
      .map(r => ({ name: r.name.split('/').pop()?.slice(0, 40), size: Math.round((r.transferSize || 0) / 1024) + 'KB', duration: Math.round(r.duration) + 'ms' }))
  }
}, null, 2)
```
4. Report findings + optimization suggestions

---

## Recipe 14: Scrape Page Content

**Trigger**: "scrape this page", "extract data", "read the page content"

1. `browser_navigate` → URL
2. `browser_wait` → 2s
3. `browser_snapshot` → get structured text content
4. If more specific data needed, `browser_javascript_execute`:
```javascript
// Extract all links
[...document.querySelectorAll('a[href]')].map(a => ({ text: a.textContent.trim(), href: a.href }))

// Extract all headings
[...document.querySelectorAll('h1,h2,h3')].map(h => ({ level: h.tagName, text: h.textContent.trim() }))

// Extract table data
[...document.querySelectorAll('table')].map(table => {
  const headers = [...table.querySelectorAll('th')].map(th => th.textContent.trim());
  const rows = [...table.querySelectorAll('tbody tr')].map(tr =>
    [...tr.querySelectorAll('td')].map(td => td.textContent.trim())
  );
  return { headers, rows };
})

// Extract all images
[...document.querySelectorAll('img')].map(img => ({ src: img.src, alt: img.alt }))
```
5. Return structured data to the user

---

## Recipe 15: Check Specific Element

**Trigger**: "check the header", "look at the footer", "inspect the card component"

1. `browser_navigate` → page (if not already there)
2. `browser_snapshot` → find the element in the tree
3. `browser_javascript_execute` → detailed inspection:
```javascript
const el = document.querySelector('SELECTOR_HERE');
if (el) {
  const s = getComputedStyle(el);
  const r = el.getBoundingClientRect();
  JSON.stringify({
    dimensions: { width: Math.round(r.width), height: Math.round(r.height) },
    position: { top: Math.round(r.top), left: Math.round(r.left) },
    styles: {
      display: s.display, flexDirection: s.flexDirection, gap: s.gap,
      padding: s.padding, margin: s.margin,
      background: s.backgroundColor, color: s.color,
      fontSize: s.fontSize, fontWeight: s.fontWeight,
      borderRadius: s.borderRadius, boxShadow: s.boxShadow
    },
    children: el.children.length,
    text: el.textContent.trim().slice(0, 100)
  }, null, 2);
} else { 'Element not found'; }
```
4. `browser_screen_capture` → visual context
5. Report findings

---

## Recipe 16: Test Authentication Flow

**Trigger**: "test login", "check auth", "test signup"

1. `browser_navigate` → login/signup page
2. `browser_screen_capture` → initial state
3. `browser_snapshot` → find form fields
4. Fill credentials:
   - `browser_click` → email/username field
   - `browser_type` → test credentials
   - `browser_click` → password field
   - `browser_type` → test password
5. `browser_screen_capture` → filled state
6. `browser_click` → submit/login button
7. `browser_wait` → 3s (auth can be slow)
8. `browser_console_messages` → check for auth errors
9. `browser_screen_capture` → result (success redirect or error state)
10. `browser_snapshot` → verify post-auth content

---

## Recipe 17: Check Animations & Transitions

**Trigger**: "check animations", "test hover states", "check transitions"

1. `browser_navigate` → page
2. `browser_screen_capture` → default state
3. `browser_hover` → element with hover effect
4. `browser_wait` → 0.5s (let transition complete)
5. `browser_screen_capture` → hover state
6. `browser_javascript_execute` → check transition properties:
```javascript
const el = document.querySelector('SELECTOR');
const s = getComputedStyle(el);
JSON.stringify({
  transition: s.transition,
  animation: s.animation,
  transform: s.transform,
  opacity: s.opacity
})
```
7. Report: are transitions smooth? Appropriate duration? Correct easing?
