# Testing Suite — Full E2E, Visual, Accessibility & Performance Testing

This power turns Kiro into a complete browser testing tool. Use it when the user wants to test their app thoroughly.

## Trigger Phrases

- "run e2e tests" / "test the login flow" / "test the checkout"
- "check accessibility" / "wcag audit" / "a11y check"
- "performance test" / "is it slow?" / "check load time"
- "visual regression" / "did anything change?" / "compare before and after"
- "test the API" / "check network requests" / "mock the API"
- "generate test code" / "write playwright tests"
- "record a test" / "record the flow"

---

## E2E Testing

### Quick Flow Test
Test a user flow by walking through it step by step:

1. `browser_navigate` → starting page
2. Inject overlay, set status: `window.__kiro.status('Testing flow...')`
3. `browser_take_screenshot` → document starting state
4. For each step in the flow:
   - Perform the action (`browser_click`, `browser_type`, `browser_select_option`, etc.)
   - `browser_wait_for` → wait for navigation or content change
   - `browser_take_screenshot` → document the state
   - `browser_console_messages` → check for errors
   - `browser_snapshot` → verify expected elements are present
5. Report: pass/fail for each step with screenshots as evidence

### Login Flow Test
```
1. browser_navigate → /login
2. browser_snapshot → find email and password fields
3. browser_type → email field with "test@example.com"
4. browser_type → password field with "password123"
5. browser_click → submit button
6. browser_wait_for → time: 3
7. browser_snapshot → verify redirected to dashboard / see welcome message
8. browser_console_messages → check for auth errors
9. browser_take_screenshot → document final state
```

### Form Validation Test
```
1. browser_navigate → form page
2. browser_click → submit button (empty form)
3. browser_snapshot → verify error messages appear
4. browser_take_screenshot → document error state
5. browser_type → fill one field with invalid data (e.g., bad email)
6. browser_click → submit
7. browser_snapshot → verify field-specific error
8. browser_type → fill all fields with valid data
9. browser_click → submit
10. browser_wait_for → time: 2
11. browser_snapshot → verify success state
12. browser_take_screenshot → document success
```

### Multi-Page Navigation Test
```
1. browser_navigate → home page
2. browser_snapshot → find nav links
3. For each nav link:
   - browser_click → the link
   - browser_wait_for → time: 2
   - browser_snapshot → verify correct page loaded
   - browser_console_messages → check for errors
   - browser_navigate_back → return to home
4. Report which pages work and which have issues
```

---

## Accessibility Testing

### Full Accessibility Audit
The `browser_snapshot` IS the accessibility tree — it's the most powerful a11y tool available.

```
1. browser_navigate → page
2. browser_snapshot → get full accessibility tree
3. Analyze the tree for:
```

**Check these items:**

| Check | How to verify | Severity |
|-------|--------------|----------|
| Images have alt text | Look for `img` without alt in snapshot | Critical |
| Buttons have labels | Look for buttons with no text/aria-label | Critical |
| Inputs have labels | Look for inputs without associated labels | Critical |
| Heading hierarchy | h1 → h2 → h3, no skips | Major |
| Landmark regions | nav, main, footer present | Major |
| Link text is descriptive | No "click here" or "read more" alone | Minor |
| Color contrast | Use JS to check contrast ratios | Major |
| Focus order | Tab through elements, check logical order | Major |
| ARIA roles | Custom widgets have proper roles | Major |

### JavaScript Accessibility Checks

Run via `browser_evaluate`:

```javascript
() => {
  const issues = [];

  // Images without alt
  const imgs = document.querySelectorAll('img:not([alt])');
  if (imgs.length) issues.push({ type: 'critical', issue: 'Images without alt text', count: imgs.length, elements: [...imgs].map(i => i.src.split('/').pop()).slice(0, 5) });

  // Buttons without accessible names
  const btns = [...document.querySelectorAll('button')].filter(b => !b.textContent.trim() && !b.getAttribute('aria-label') && !b.getAttribute('aria-labelledby'));
  if (btns.length) issues.push({ type: 'critical', issue: 'Buttons without accessible names', count: btns.length });

  // Inputs without labels
  const inputs = [...document.querySelectorAll('input:not([type="hidden"]), select, textarea')].filter(i => !i.labels?.length && !i.getAttribute('aria-label') && !i.getAttribute('aria-labelledby'));
  if (inputs.length) issues.push({ type: 'critical', issue: 'Form inputs without labels', count: inputs.length, elements: inputs.map(i => i.type + ':' + (i.name || 'unnamed')).slice(0, 5) });

  // Heading hierarchy
  const headings = [...document.querySelectorAll('h1,h2,h3,h4,h5,h6')];
  const levels = headings.map(h => parseInt(h.tagName[1]));
  for (let i = 1; i < levels.length; i++) {
    if (levels[i] - levels[i-1] > 1) {
      issues.push({ type: 'major', issue: 'Heading level skipped', detail: 'h' + levels[i-1] + ' → h' + levels[i], at: headings[i].textContent.trim().slice(0, 40) });
      break;
    }
  }
  if (!headings.some(h => h.tagName === 'H1')) issues.push({ type: 'major', issue: 'No h1 element found' });

  // Landmarks
  const landmarks = { nav: !!document.querySelector('nav'), main: !!document.querySelector('main'), footer: !!document.querySelector('footer') };
  const missing = Object.entries(landmarks).filter(([,v]) => !v).map(([k]) => k);
  if (missing.length) issues.push({ type: 'major', issue: 'Missing landmark regions', missing });

  // Links with generic text
  const genericLinks = [...document.querySelectorAll('a')].filter(a => ['click here', 'read more', 'learn more', 'here'].includes(a.textContent.trim().toLowerCase()));
  if (genericLinks.length) issues.push({ type: 'minor', issue: 'Links with generic text', count: genericLinks.length });

  // Tab index issues
  const badTabIndex = document.querySelectorAll('[tabindex]:not([tabindex="0"]):not([tabindex="-1"])');
  if (badTabIndex.length) issues.push({ type: 'minor', issue: 'Elements with positive tabindex (breaks natural tab order)', count: badTabIndex.length });

  return JSON.stringify({ totalIssues: issues.length, issues }, null, 2);
}
```

### Keyboard Navigation Test
```
1. browser_navigate → page
2. browser_press_key → "Tab" (repeatedly)
3. After each Tab:
   - browser_snapshot → check which element has focus
   - Verify focus is visible (focus ring/outline)
   - Verify logical order (left-to-right, top-to-bottom)
4. browser_press_key → "Enter" on focused buttons/links
5. Verify actions trigger correctly
6. browser_press_key → "Escape" on modals/dropdowns
7. Verify they close properly
```

---

## Performance Testing

### Page Load Performance
Run via `browser_evaluate`:

```javascript
() => {
  const nav = performance.getEntriesByType('navigation')[0];
  const paint = performance.getEntriesByType('paint');
  const resources = performance.getEntriesByType('resource');

  const fcp = paint.find(p => p.name === 'first-contentful-paint');
  const lcp = performance.getEntriesByType('largest-contentful-paint');

  return JSON.stringify({
    timing: {
      ttfb: Math.round(nav.responseStart - nav.startTime) + 'ms',
      domContentLoaded: Math.round(nav.domContentLoadedEventEnd - nav.startTime) + 'ms',
      fullLoad: Math.round(nav.loadEventEnd - nav.startTime) + 'ms',
      firstContentfulPaint: fcp ? Math.round(fcp.startTime) + 'ms' : 'N/A',
    },
    resources: {
      total: resources.length,
      totalTransferSize: Math.round(resources.reduce((s, r) => s + (r.transferSize || 0), 0) / 1024) + 'KB',
      byType: resources.reduce((acc, r) => {
        const ext = r.name.split('.').pop()?.split('?')[0] || 'other';
        acc[ext] = (acc[ext] || 0) + 1;
        return acc;
      }, {}),
      slowest: resources.sort((a, b) => b.duration - a.duration).slice(0, 5).map(r => ({
        name: r.name.split('/').pop()?.slice(0, 50),
        duration: Math.round(r.duration) + 'ms',
        size: Math.round((r.transferSize || 0) / 1024) + 'KB'
      })),
      largest: resources.sort((a, b) => (b.transferSize || 0) - (a.transferSize || 0)).slice(0, 5).map(r => ({
        name: r.name.split('/').pop()?.slice(0, 50),
        size: Math.round((r.transferSize || 0) / 1024) + 'KB',
        duration: Math.round(r.duration) + 'ms'
      }))
    }
  }, null, 2);
}
```

### Performance Scoring
After collecting metrics, score them:

| Metric | Good | Needs Work | Poor |
|--------|------|-----------|------|
| TTFB | < 200ms | 200-600ms | > 600ms |
| FCP | < 1.8s | 1.8-3s | > 3s |
| DOM Content Loaded | < 2s | 2-4s | > 4s |
| Full Load | < 3s | 3-6s | > 6s |
| Total Transfer Size | < 500KB | 500KB-2MB | > 2MB |
| Resource Count | < 30 | 30-80 | > 80 |

### DOM Complexity Check
```javascript
() => {
  const all = document.querySelectorAll('*');
  let maxDepth = 0;
  all.forEach(el => {
    let depth = 0, node = el;
    while (node.parentElement) { depth++; node = node.parentElement; }
    maxDepth = Math.max(maxDepth, depth);
  });
  return JSON.stringify({
    totalElements: all.length,
    maxDepth,
    bodyChildren: document.body.children.length,
    rating: all.length < 800 ? 'Good' : all.length < 1500 ? 'Moderate' : 'Heavy — may cause jank'
  }, null, 2);
}
```

---

## Visual Regression Testing

### Before/After Comparison
When the user makes changes and wants to verify nothing broke:

```
1. BEFORE the change:
   - browser_navigate → page
   - browser_take_screenshot → save as "before" (note the filename)
   - browser_snapshot → save structure

2. User makes their code change

3. AFTER the change:
   - browser_wait_for → time: 2 (hot reload)
   - browser_take_screenshot → save as "after"
   - browser_snapshot → compare structure

4. Compare:
   - Visual differences between screenshots
   - Structural differences in snapshots
   - Report what changed
```

### Multi-Page Regression Check
After a significant change (CSS refactor, dependency update, etc.):

```
1. List all important routes/pages
2. For each page:
   - browser_navigate → the route
   - browser_wait_for → time: 2
   - browser_take_screenshot → capture
   - browser_console_messages → check for new errors
   - browser_snapshot → check structure
3. Report any pages that look different or have new errors
```

---

## Network & API Testing

### API Health Check
```
1. browser_navigate → page that makes API calls
2. browser_wait_for → time: 3
3. browser_network_requests → list all requests
4. For each API request, check:
   - Status code (200 = good, 4xx/5xx = problem)
   - Response time
   - Response size
5. Report failed or slow requests
```

### Mock API for Testing
```
1. browser_route → set up mock:
   - pattern: "**/api/users"
   - status: 200
   - body: '{"users": [{"id": 1, "name": "Test User"}]}'
   - contentType: "application/json"
2. browser_navigate → page
3. browser_wait_for → time: 2
4. browser_take_screenshot → verify page renders with mock data
5. browser_snapshot → verify correct content displayed
```

### Test Error States
```
1. browser_route → mock a failure:
   - pattern: "**/api/data"
   - status: 500
   - body: '{"error": "Internal Server Error"}'
   - contentType: "application/json"
2. browser_navigate → page
3. browser_wait_for → time: 2
4. browser_take_screenshot → verify error UI appears
5. browser_snapshot → verify error message is shown
```

### Test Loading States
```
1. browser_route → mock a slow response:
   - pattern: "**/api/data"
   - (use browser_evaluate to add a delay before responding)
2. browser_navigate → page
3. browser_take_screenshot → capture loading state immediately
4. browser_wait_for → time: 3
5. browser_take_screenshot → capture loaded state
```

---

## Test Code Generation

When the user says "generate test code" or "write playwright tests":

### From a Recorded Flow
1. Walk through the user flow using browser tools
2. Note every action taken (navigate, click, type, assert)
3. Generate a Playwright test file:

```typescript
import { test, expect } from '@playwright/test';

test('user flow: [description]', async ({ page }) => {
  // Navigate
  await page.goto('http://localhost:3000');

  // Interact
  await page.getByRole('textbox', { name: 'Email' }).fill('test@example.com');
  await page.getByRole('textbox', { name: 'Password' }).fill('password123');
  await page.getByRole('button', { name: 'Sign In' }).click();

  // Assert
  await expect(page.getByRole('heading', { name: 'Dashboard' })).toBeVisible();
  await expect(page).toHaveURL(/dashboard/);
});
```

### Using browser_generate_locator
For each element you interact with during testing, use `browser_generate_locator` to get the best Playwright locator:
```
1. browser_snapshot → find the element
2. browser_generate_locator → target: the element's ref
3. Use the generated locator in the test code
```

---

## Video Recording

### Record a Test Flow
```
1. browser_start_video → begin recording
2. Walk through the user flow
3. browser_video_chapter → add chapter markers at key points:
   - title: "Login"
   - description: "User enters credentials and signs in"
4. browser_stop_video → save the recording
5. Share the video file with the user
```

This is useful for:
- Documenting bugs (record the reproduction steps)
- Creating demo videos
- Sharing test results with the team

---

## Complete Test Report Template

After running a full test suite, report results in this format:

```
## Test Report: [Page/Feature Name]

### Summary
- Total checks: X
- Passed: X
- Failed: X
- Warnings: X

### E2E Tests
- ✅ Login flow: passed
- ❌ Form submission: failed (error message not shown)
- ✅ Navigation: all links work

### Accessibility
- ❌ 3 images missing alt text
- ❌ 2 inputs without labels
- ✅ Heading hierarchy correct
- ⚠️ Missing footer landmark

### Performance
- ✅ TTFB: 120ms (good)
- ⚠️ FCP: 2.1s (needs work)
- ❌ Total size: 3.2MB (too large)
- ⚠️ 45 resources loaded

### Console
- ❌ 2 JavaScript errors
- ⚠️ 1 deprecation warning

### Network
- ✅ All API calls successful
- ⚠️ /api/users took 1.2s (slow)

### Recommendations
1. [Most impactful fix]
2. [Second priority]
3. [Third priority]
```
