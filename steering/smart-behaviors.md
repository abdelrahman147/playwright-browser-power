# Smart Behaviors — Agent Intelligence Rules

Read this file on first activation. These rules make the browser power feel intelligent and proactive rather than mechanical.

## Auto-Detection Rules

### Auto-Install Playwright Browsers
**This is the FIRST thing to handle.** If any browser tool call fails, check the error message:

**Error patterns that mean "browsers not installed":**
- "Executable doesn't exist"
- "browserType.launch: Browser not found"
- "Cannot find browser"
- "ENOENT" with a path containing "chromium" or "chrome"
- "Failed to launch browser"
- "Browser closed unexpectedly"
- Any error on the very first browser tool call

**When you see any of these, immediately run:**
```bash
npx playwright install chromium
```

Do NOT ask the user for permission — just install it. It's a ~150MB download of the Chromium binary, completely safe, and required for this power to work.

**If that still fails on Linux**, also run:
```bash
npx playwright install-deps chromium
```

**If `npx` itself is not found**, Node.js isn't installed. Tell the user:
- Windows: "Install Node.js 18+ from https://nodejs.org"
- macOS: "Run `brew install node` or download from https://nodejs.org"
- Linux: "Run `sudo apt install nodejs npm` or use nvm"

**After successful install**, retry the original browser operation. Don't make the user repeat their request.

### Auto-Detect Dev Server URL
When the user says "open my app" or "check my site" without specifying a URL:

1. Look at the project's package.json for scripts:
   - `dev`, `start`, `serve` scripts often reveal the port
   - Look for `--port` flags or `PORT` env vars
2. Check common framework defaults:
   - `vite.config.*` → likely port 5173
   - `next.config.*` → likely port 3000
   - `angular.json` → likely port 4200
   - `vue.config.*` or Vite with Vue → likely port 5173
   - `svelte.config.*` → likely port 5173
   - `.env` files → look for `PORT=` variable
3. If you can determine the likely URL, try it. If navigation fails, ask the user.
4. If you can't determine it, ask: "What URL is your app running on? Common defaults are localhost:3000, localhost:5173, etc."

### Auto-Detect What to Inspect
When the user says "check the page" or "how does it look" without specifics:

Run the full health check sequence:
1. `browser_console_messages` → report any errors
2. `browser_snapshot` → verify structure
3. `browser_screen_capture` → show visual state
4. `browser_network_requests` → check for failed requests
5. Summarize findings proactively

### Auto-Detect When to Use Vision vs Snapshot
- User asks about **structure, content, text, elements, accessibility** → use `browser_snapshot`
- User asks about **appearance, design, colors, layout, spacing, how it looks** → use `browser_screen_capture`
- User asks to **fix** something → use both (snapshot for structure, screenshot for visual verification)
- When in doubt → use `browser_snapshot` first (it's faster), then `browser_screen_capture` if needed

## Proactive Behaviors

### Overlay Management
The overlay is injected at runtime via `browser_javascript_execute` after every navigation. **Read `overlay.md` for the full injectable script.**

After injecting, use the `window.__kiro` API to manage it:

**Before taking screenshots for analysis:**
```javascript
window.__kiro.hide();
```
Then after the screenshot:
```javascript
window.__kiro.show();
```

**Show progress to the user** by updating the badge text:
```javascript
window.__kiro.status('Analyzing layout...');
// ... do work ...
window.__kiro.status('Fixing spacing...');
// ... do work ...
window.__kiro.status('Verifying fix...');
```
Reset it when done:
```javascript
window.__kiro.status('Kiro is driving');
```

**When the user needs to interact with the page** (login, select something, etc.):
```javascript
window.__kiro.unlock(); // User gets control, badge turns green
```
Then when Kiro takes back over:
```javascript
window.__kiro.lock(); // Kiro gets control, badge turns cyan
```

**Important**: The overlay blocks user mouse/keyboard input by default. Playwright's own actions (via `browser_click`, `browser_type`, etc.) bypass the overlay because Playwright dispatches events at a lower level. So Kiro can interact normally while the user watches.

### After Writing UI Code
When you've just written or edited HTML/CSS/JSX/TSX/Vue/Svelte code:
1. If the browser is already open to the relevant page, automatically wait 2 seconds and re-check
2. If the browser isn't open, suggest: "Want me to open the browser and check how that looks?"

### After Fixing a Bug
When you've just fixed a reported visual bug:
1. Always re-verify with a screenshot — never just say "fixed"
2. Compare the new state against what was reported
3. Check that the fix didn't break adjacent elements

### When You See Console Errors
If `browser_console_messages` returns errors:
1. Report them immediately — don't wait for the user to ask
2. If the errors are in files you can access, offer to fix them
3. Prioritize render-blocking errors over warnings

### When You See Failed Network Requests
If `browser_network_requests` shows 4xx/5xx responses:
1. Report which endpoints failed
2. Check if it's a CORS issue, missing API, or server error
3. Suggest fixes based on the error type

### When the Page Looks Broken
If a screenshot shows a clearly broken page (blank, error screen, massive layout shift):
1. Check console errors first — that's almost always the cause
2. Check network requests for failed loads
3. Don't try to fix CSS when the real problem is a JS crash

## Understanding User Intent

### Translating Casual Requests

| User says | What to do |
|-----------|-----------|
| "open my app" | Auto-detect URL, navigate, do full health check |
| "check it" / "how does it look" | Screenshot + snapshot + console check |
| "take a screenshot" | Just `browser_screen_capture`, show the result |
| "what's on the page" | `browser_snapshot` for structure |
| "is it working?" | Full health check: console + network + snapshot + screenshot |
| "fix the UI" | Screenshot → identify issues → fix → re-verify |
| "make it look better" | Read `design-thinking.md`, do design review, suggest improvements |
| "test the form" | Navigate → find form → fill it → submit → check result |
| "check mobile" | Resize viewport to 375x812, screenshot, report issues |
| "compare with this site" | Open reference in new tab, screenshot both, compare |
| "save as PDF" | Navigate, wait for full render, `browser_pdf_save` |
| "check for errors" | `browser_console_messages` + `browser_network_requests` |
| "click the button" | `browser_snapshot` to find it, `browser_click` to click it |
| "scroll down" | `browser_scroll` down, then screenshot the new view |
| "go back" | `browser_go_back`, then screenshot |
| "open a new tab" | `browser_tab_new` + `browser_navigate` |
| "what's the console say" | `browser_console_messages` |
| "mock the API" | `browser_route` with the pattern and mock data |
| "check dark mode" | Toggle dark mode via JS, screenshot, compare |
| "is it accessible?" | `browser_snapshot` (it IS the accessibility tree) + JS checks |
| "scrape this page" | Navigate, snapshot for structure, JS execute for data extraction |
| "read this page" | Navigate, snapshot for text content |
| "install playwright" / "setup browser" | Run `npx playwright install chromium` immediately, report success |
| "let me click" / "give me control" | `browser_javascript_execute` → `window.__kiro.unlock()` — user gets mouse/keyboard |
| "take over" / "you drive" | `browser_javascript_execute` → `window.__kiro.lock()` — Kiro resumes control |
| "hide the badge" / "clean screenshot" | `browser_javascript_execute` → `window.__kiro.hide()` |

### When the User Gives a URL Directly
If the user pastes a URL like "check https://example.com" or "open localhost:3000/dashboard":
1. Navigate immediately — don't ask for confirmation
2. Do the full health check
3. Report what you find

### When the User Describes a Problem
If the user says "the button is in the wrong place" or "the header looks weird":
1. Navigate to the page (or use current page if already there)
2. Screenshot to see the current state
3. Identify the specific issue they're describing
4. Fix it
5. Re-screenshot to verify

## Error Recovery

### Browser Not Installed / Launch Failure
This is the most common first-time error. Handle it silently:
1. Run `npx playwright install chromium` — don't ask, just do it
2. If on Linux and it still fails, run `npx playwright install-deps chromium`
3. Retry the original operation
4. Only tell the user if it still fails after both attempts
5. If `npx` is missing, Node.js isn't installed — that's the one thing the user must fix themselves

### Navigation Fails
1. Check if the URL is correct (typos, wrong port)
2. Ask the user if their dev server is running
3. Try common alternative ports (3000, 5173, 4200, 8080, 8000)
4. If all fail, tell the user exactly what happened

### Page Crashes After Code Change
1. Check `browser_console_messages` for the error
2. The error usually points to the exact file and line
3. Fix the error, wait for hot reload, re-navigate

### Element Not Found
1. `browser_snapshot` to see what's actually on the page
2. The element might have a different name/ref than expected
3. It might not have rendered yet — `browser_wait` and retry
4. It might be behind a loading state or conditional render

### Browser Becomes Unresponsive
1. Try `browser_navigate` to the same URL (force reload)
2. If that fails, the MCP server may need a restart
3. Tell the user to reconnect the MCP server from the Kiro MCP panel

## Multi-Page Awareness

### When Working on Multi-Page Apps
- Keep track of which page you're on
- After fixing something, check if the fix affects other pages
- Use `browser_tab_new` to keep multiple pages open for comparison
- Use `browser_tab_list` to see what's open
- Close tabs you're done with to keep things clean

### When Working on Single-Page Apps (SPAs)
- Navigation within the app may not trigger a full page load
- Use `browser_click` on nav links instead of `browser_navigate` for internal routes
- After client-side navigation, `browser_wait` briefly then `browser_snapshot`
- Watch for hydration issues in SSR frameworks (Next.js, Nuxt, SvelteKit)

## Context Efficiency

### Minimize Context Usage
- Prefer `browser_snapshot` over `browser_screen_capture` when possible (text is cheaper than images)
- Don't take redundant screenshots — if nothing changed, don't re-capture
- Use targeted `browser_javascript_execute` for specific checks instead of full screenshots
- Close unused tabs with `browser_tab_close`

### When to Use Full Screenshots
- First visit to a page (establish baseline)
- After a batch of visual fixes (verify the result)
- When the user explicitly asks to see the page
- When analyzing design/layout issues (colors, spacing, alignment)
- When comparing before/after states
