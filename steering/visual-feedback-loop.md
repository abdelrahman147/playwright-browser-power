# Visual Feedback Loop — The Core Workflow

This is the primary workflow. Every UI task should follow this loop. Never consider a UI task "done" until you've visually verified it in the browser.

```
Write Code → Open Browser → See Result → Analyze → Fix → Re-verify → Done
```

## Phase 1: Connect

### Find the URL
If the user told you → use it directly.
If you don't know → auto-detect from project config (see smart-behaviors.md) or ask.

Common defaults:
| Framework | Default URL |
|-----------|------------|
| Vite / SvelteKit | http://localhost:5173 |
| Next.js | http://localhost:3000 |
| Angular | http://localhost:4200 |
| Vue CLI | http://localhost:8080 |
| Create React App | http://localhost:3000 |
| Django | http://localhost:8000 |
| Rails | http://localhost:3000 |
| Static files | Suggest `npx serve .` on port 3000 |

### Navigate
1. `browser_navigate` → the URL
2. `browser_wait` → 2 seconds (let page render, hydrate, load fonts/images)

## Phase 2: Full Assessment

Do ALL THREE checks on every first visit:

### 1. Console Check (catches 60% of issues)
`browser_console_messages`
- Uncaught errors = something is broken, fix before anything else
- 404s for assets = missing files, wrong paths
- CORS errors = API configuration issue
- Deprecation warnings = note but don't prioritize

### 2. Structural Check (fast, lightweight)
`browser_snapshot`
- Are all expected elements present?
- Is text content correct?
- Do interactive elements exist (buttons, links, inputs)?
- Are there accessibility issues (missing labels, roles)?

### 3. Visual Check (the real picture)
`browser_screen_capture`
- Overall layout and composition
- Colors, typography, spacing
- Image rendering
- Visual hierarchy and alignment
- Anything that looks "off"

## Phase 3: Triage Issues

Rank by severity — fix in this order:

### P0 — Broken (fix NOW)
- Blank page or crash
- JavaScript errors preventing render
- Missing critical content
- App won't load at all

### P1 — Major (fix next)
- Layout significantly wrong
- Wrong colors/typography that changes the feel
- Missing important sections or components
- Broken interactions (buttons, forms, navigation)

### P2 — Minor (fix after P1)
- Spacing inconsistencies
- Minor alignment issues
- Missing hover/focus states
- Small responsive problems

### P3 — Polish (fix last)
- Pixel-perfect adjustments
- Animation/transition refinements
- Edge case visual states
- Loading state improvements

## Phase 4: Fix → Verify Loop

For each issue:

### 1. Fix
Edit the source file(s). Be precise — change only what's needed for this issue.
Update the overlay status so the user knows what's happening: `browser_javascript_execute` → `window.__kiro.status('Fixing: [issue description]...')`

### 2. Wait
`browser_wait` → 1-2 seconds. The dev server needs time to detect the change, recompile, and hot-reload.

### 3. Verify
- Before capturing, hide the overlay for a clean shot: `browser_javascript_execute` → `window.__kiro.hide()`
- `browser_snapshot` for structural fixes
- `browser_screen_capture` for visual fixes
- Show the overlay again: `browser_javascript_execute` → `window.__kiro.show()`
- Confirm the fix worked AND didn't break anything else

### 4. Decide
- Fix worked → move to next issue
- Fix didn't work → analyze why, try different approach
- Fix caused new problems → revert and rethink

## Phase 5: Final Verification

Once all issues are addressed:

1. **Full screenshot** — final visual confirmation
2. **Console check** — no new errors introduced
3. **Key pages** — if multi-page app, spot-check other important routes
4. **Key interactions** — click through the main user flows
5. **Report** — brief summary of what was found and fixed

## When to Use This Workflow

- **Building new UI** → write code → verify visually → iterate
- **Fixing reported bugs** → navigate → confirm bug → fix → verify fix
- **Improving design** → screenshot → analyze → suggest → implement → verify
- **Responsive work** → check multiple viewports → fix → re-verify each
- **After any code change that affects UI** → re-verify the affected page

## Anti-Patterns

- ❌ Screenshotting after every single line change (batch fixes instead)
- ❌ Skipping the console check (JS errors cause most visual bugs)
- ❌ Assuming the fix worked without re-verifying
- ❌ Screenshotting before hot reload completes (stale state)
- ❌ Using only screenshots when a snapshot would suffice (wastes context)
- ❌ Saying "I fixed it" without visual proof
