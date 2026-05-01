---
name: playwright-browser
displayName: "Playwright Browser — Visual AI Assistant"
description: "Give Kiro real eyes. Launch browsers, navigate to any page, take screenshots, analyze UI visually, inspect console/network/devtools, interact with elements, test user flows, generate PDFs, steal UI components from any website, and iteratively fix issues. Kiro becomes a design-aware, visually intelligent coding partner that can see what it builds."
keywords:
  - playwright
  - browser testing
  - open localhost
  - browse localhost
  - screenshot
  - visual feedback
  - steal ui
  - steal component
  - e2e test
  - browser automation
  - console errors
  - network requests
  - debug ui
  - accessibility test
author: Abdelrahman Mohsen
---

<div align="center">
  <img src="icon.svg" alt="Playwright Browser Power" width="200" />
  
  # Playwright Browser — Visual AI Assistant
  
  **by Abdelrahman Mohsen**
</div>

## Overview

This power gives Kiro real eyes. Using Microsoft's official Playwright MCP server, Kiro can launch a real browser, navigate to any page, take screenshots, analyze the visual output, interact with elements, inspect console/network/devtools, steal UI components from any website, run full E2E tests, and fix issues — all through a visual feedback loop.

**Three superpowers in one:**
1. **Visual Builder** — See what you build, fix what's wrong, iterate visually
2. **UI Stealer** — Browse any website, pick components you like, Kiro extracts and recreates them in your project
3. **Testing Suite** — E2E tests, visual regression, accessibility audits, performance checks, all from the browser

**This power activates automatically** when you say things like:
- "open localhost:3000" / "browse to this URL" / "show me the page"
- "steal that navbar" / "grab that hero section" / "I want that card design"
- "run e2e tests" / "test the login flow" / "check accessibility"
- "make it look better" / "fix the UI" / "check responsive"

No special commands. Just talk naturally.

## When to Use This Power

✅ **Perfect for:**
- Building UI components and want visual feedback
- Stealing/cloning UI from existing websites
- Running E2E tests on web applications
- Debugging visual issues (layout, styling, responsiveness)
- Accessibility audits (WCAG compliance)
- Performance testing (load times, network analysis)
- Generating PDFs from web pages
- Recording user flow videos
- Testing forms, authentication, and user interactions
- Visual regression testing

❌ **Not ideal for:**
- Unit testing (use Jest, Vitest instead)
- API-only testing without UI (use Postman power)
- Mobile app testing (use Appium)
- Load testing at scale (use k6, JMeter)
- Backend testing without browser

## Quick Start Examples

### Example 1: Visual Development Loop
```
User: "open localhost:3000"
Kiro: [navigates, screenshots, reports what it sees]

User: "the button is too small, make it bigger"
Kiro: [fixes CSS, waits for reload, re-screenshots, confirms]
```

### Example 2: Steal a Component
```
User: "go to stripe.com and grab their pricing cards"
Kiro: [opens browser, takes screenshot, extracts HTML/CSS, recreates in your project]
```

### Example 3: Run E2E Test
```
User: "test the login flow"
Kiro: [navigates, fills form, submits, verifies, screenshots each step]
```

### Example 4: Accessibility Audit
```
User: "check accessibility on the dashboard"
Kiro: [runs WCAG audit, reports issues with specific fixes]
```

## Onboarding — First-Time Setup

**Kiro handles setup automatically.** The user should never have to manually install anything.

### Auto-Setup (runs on first use)

When any browser tool call fails with errors about missing browsers or executables:

1. **Kiro immediately runs**: `npx playwright install chromium`
2. **On Linux, if still failing**: `npx playwright install-deps chromium`
3. **Retries the original operation** — user never has to repeat their request

**The only prerequisite is Node.js 18+.** Everything else is auto-installed.

### Platform Notes
- **Windows**: Chromium installs to `%LOCALAPPDATA%\ms-playwright\`. No system deps needed.
- **macOS**: Chromium installs to `~/Library/Caches/ms-playwright/`. No system deps needed.
- **Linux**: May need `npx playwright install-deps chromium` for system libraries.
- **Docker/CI**: Use `npx playwright install --with-deps chromium` for both.

### Installing Other Browsers (Optional)
```bash
npx playwright install firefox
npx playwright install webkit
npx playwright install  # all browsers
```

## Workflow Guide

**Choose the right workflow for your task:**

| Your Goal | Steering File to Read | Keywords to Trigger |
|-----------|----------------------|---------------------|
| Build UI and see it live | `visual-feedback-loop.md` | "open localhost", "show me", "how does it look" |
| Copy UI from another site | `ui-stealing.md` | "steal", "grab", "copy that navbar" |
| Run automated tests | `testing-suite.md` | "test the login", "run e2e tests" |
| Improve design quality | `design-thinking.md` | "make it look better", "improve design" |
| Quick common tasks | `quick-recipes.md` | "check accessibility", "generate PDF" |
| Agent best practices | `smart-behaviors.md` | Read for error recovery and auto-detection |

## Available Steering Files

| File | When to read |
|------|-------------|
| `overlay.md` | **Read on first activation.** Contains the injectable overlay script and usage patterns. |
| `visual-feedback-loop.md` | The core build → see → fix → verify cycle. |
| `design-thinking.md` | When analyzing design quality or the user says "make it look better". |
| `ui-stealing.md` | **When the user wants to steal/copy/grab UI components from any website.** |
| `testing-suite.md` | **When the user wants E2E tests, visual regression, accessibility, or performance testing.** |
| `quick-recipes.md` | Ready-to-go step sequences for 20+ common tasks. |
| `smart-behaviors.md` | Agent intelligence rules — auto-detection, error recovery, proactive suggestions. |

## Available MCP Server

### playwright
- **Package**: `@playwright/mcp` (Microsoft's official Playwright MCP server)
- **Transport**: stdio
- **Mode**: Headed (visible browser window — user watches Kiro work)
- **Capabilities enabled**: vision, pdf, devtools, network, storage, testing
- **Default viewport**: 1280x720
- **Console level**: error (auto-captures JS errors)
- **HTTPS errors**: ignored (works with self-signed certs)

## Visual Overlay System

The overlay is injected at runtime via `browser_evaluate` after each navigation. **Read `overlay.md` for the full script.**

It provides:
- **"Kiro is driving" badge** — pulsing cyan dot in bottom-right corner
- **Interaction blocker** — prevents user from accidentally clicking while Kiro works
- **Cursor ring** — cyan circle follows Playwright's mouse
- **Click ripples** — visual feedback on clicks

### Control API (via `browser_evaluate`)
| Method | What it does |
|--------|-------------|
| `__kiro.unlock()` | Give user control (badge turns green) |
| `__kiro.lock()` | Kiro takes back control |
| `__kiro.hide()` | Hide overlay for clean screenshots |
| `__kiro.show()` | Show overlay again |
| `__kiro.status('msg')` | Update badge text |

## UI Stealing System

**Read `ui-stealing.md` for the full workflow.**

When the user says "steal that navbar" or "I want that card design" or "grab that hero section":

1. Kiro opens the target website in the headed browser
2. User sees the page and describes which component they want
3. Kiro takes a screenshot and snapshot to identify the component
4. Kiro extracts the full HTML structure, computed CSS, and assets
5. Kiro recreates the component in the user's project, adapted to their tech stack
6. User can add a prompt like "make it dark mode" or "use my brand colors"

### Interactive Selection Mode
The user can also use Kiro's annotation tools:
1. Kiro calls `browser_annotate` — opens annotation mode
2. User draws a box around the component they want
3. Kiro extracts everything inside that selection
4. User describes modifications in chat
5. Kiro builds the component

## Testing Suite

**Read `testing-suite.md` for the full workflow.**

This power turns Kiro into a complete testing tool:

### E2E Testing
- Walk through user flows (signup, login, checkout, etc.)
- Verify each step with screenshots and assertions
- Generate Playwright test code for CI

### Visual Regression
- Take baseline screenshots
- Compare after changes
- Detect pixel-level differences

### Accessibility Testing
- Full WCAG audit via accessibility snapshots
- Check contrast ratios, labels, roles, headings
- Generate accessibility reports

### Performance Testing
- Measure page load times, TTFB, LCP
- Identify largest resources
- Check network waterfall
- Suggest optimizations

### API Testing
- Monitor network requests
- Mock API responses
- Test error states
- Verify request/response payloads

## Core Tool Reference

### Navigation & Page State
| Tool | Purpose |
|------|---------|
| `browser_navigate` | Go to any URL |
| `browser_snapshot` | Get accessibility tree (fast, structured — default inspection tool) |
| `browser_navigate_back` | Browser back button |
| `browser_wait_for` | Wait for time, text to appear, or text to disappear |

### Vision (Screenshots & Coordinates)
| Tool | Purpose |
|------|---------|
| `browser_take_screenshot` | Take a screenshot (supports PNG or JPEG format) |
| `browser_mouse_click_xy` | Click at exact x,y coordinates |
| `browser_mouse_move_xy` | Move mouse to coordinates |
| `browser_mouse_drag_xy` | Drag from point A to point B |

**Screenshot format options:**
- `type: "png"` - High quality, large files (~500KB-1MB) - default
- `type: "jpeg"` - Good quality, small files (~50-150KB) - recommended for most use cases

### Element Interaction
| Tool | Purpose |
|------|---------|
| `browser_click` | Click an element by accessibility ref |
| `browser_type` | Type into an input field |
| `browser_fill_form` | Fill multiple form fields at once |
| `browser_select_option` | Select from a dropdown |
| `browser_hover` | Hover over an element |
| `browser_press_key` | Press keyboard keys |
| `browser_file_upload` | Upload files |

### Annotation & Selection
| Tool | Purpose |
|------|---------|
| `browser_annotate` | Open annotation mode — user draws on the page |
| `browser_highlight` | Highlight a specific element with a colored overlay |
| `browser_hide_highlight` | Remove a highlight |

### JavaScript & Console
| Tool | Purpose |
|------|---------|
| `browser_evaluate` | Run any JS in the page context |
| `browser_console_messages` | Get console logs/warnings/errors |

### Network
| Tool | Purpose |
|------|---------|
| `browser_network_requests` | List all network requests |
| `browser_network_request` | Get full details of a specific request |
| `browser_route` | Mock/intercept network requests |
| `browser_network_state_set` | Toggle online/offline mode |

### Tabs
| Tool | Purpose |
|------|---------|
| `browser_tabs` | List, create, close, or select tabs |

### Testing & Assertions
| Tool | Purpose |
|------|---------|
| `browser_verify_element_visible` | Assert element is visible |
| `browser_verify_text_visible` | Assert text is visible |
| `browser_verify_list_visible` | Assert list items are visible |
| `browser_verify_value` | Assert element value (checkbox, input, etc.) |

### Storage
| Tool | Purpose |
|------|---------|
| `browser_cookie_list/get/set/delete/clear` | Cookie management |
| `browser_localstorage_list/get/set/delete/clear` | localStorage management |
| `browser_sessionstorage_list/get/set/delete/clear` | sessionStorage management |
| `browser_storage_state` | Save full storage state to file |
| `browser_set_storage_state` | Restore storage state from file |

### PDF & Video
| Tool | Purpose |
|------|---------|
| `browser_pdf_save` | Export page as PDF |
| `browser_start_video` / `browser_stop_video` | Record browser session as video |
| `browser_video_chapter` | Add chapter markers to video recording |

### DevTools & Advanced
| Tool | Purpose |
|------|---------|
| `browser_start_tracing` / `browser_stop_tracing` | Performance tracing |
| `browser_run_code_unsafe` | Run arbitrary Playwright code |
| `browser_generate_locator` | Generate test locators for elements |
| `browser_resize` | Resize browser window |

## Best Practices

### Snapshot First, Screenshot Second
`browser_snapshot` is fast and lightweight. Use it as default. Only use `browser_take_screenshot` when you need visual details.

### Use JPEG for Smaller Screenshots
PNG screenshots can be 500KB-1MB each. Use JPEG format to reduce file size by 80-90%:
- **PNG** (default): High quality, large files (~500KB-1MB)
- **JPEG**: Good quality, small files (~50-150KB)

**When to use JPEG:**
- Visual verification and feedback
- UI component screenshots
- Before/after comparisons
- E2E test screenshots

**When to use PNG:**
- Need transparency
- Pixel-perfect comparisons
- Text-heavy screenshots (better clarity)

**Example:**
```javascript
// Small file size (JPEG)
browser_take_screenshot({ type: "jpeg" })

// High quality (PNG) - larger files
browser_take_screenshot({ type: "png" })
```

### Always Check Console After Navigation
`browser_console_messages` catches JS errors that cause most visual bugs.

### Wait for Hot Reload
After code edits, `browser_wait_for` with `time: 2` before re-inspecting.

### Use Annotation for Component Selection
When the user wants to pick a specific component, use `browser_annotate` to let them draw on the page.

### Record Video for Complex Flows
Use `browser_start_video` before testing a user flow, `browser_video_chapter` for markers, and `browser_stop_video` when done.

## Configuration

### Changing Browser
Edit `mcp.json`: `--browser=firefox`, `--browser=webkit`, or `--browser=msedge`

### Changing Viewport
Edit `--viewport-size=1280x720` to any resolution.

### Headless Mode
Add `--headless` for invisible browser.

### Connect to Existing Browser
Add `--cdp-endpoint=http://localhost:9222`.

## Framework Integration

### React / Next.js
```bash
# Start your dev server
npm run dev

# Then tell Kiro:
"open localhost:3000 and check the homepage"
```

### Vue / Nuxt
```bash
npm run dev
# "open localhost:5173"
```

### Svelte / SvelteKit
```bash
npm run dev
# "open localhost:5173"
```

### Angular
```bash
ng serve
# "open localhost:4200"
```

### Plain HTML
```bash
# Use any static server
npx serve .
# "open localhost:3000"
```

## Common Issues & Solutions

### Issue: "Executable doesn't exist" Error
**Cause:** Chromium not installed  
**Solution:** Kiro auto-runs `npx playwright install chromium` on first use  
**Manual fix:** Run `npx playwright install chromium` yourself  
**Platform note:** On Linux, may need `npx playwright install-deps chromium`

### Issue: Screenshots Show Blank Page
**Cause:** Page hasn't finished loading  
**Solution:** Tell Kiro "wait 3 seconds then screenshot"  
**Prevention:** Kiro should automatically wait for `networkidle` state  
**Alternative:** Use `browser_wait_for` with `time: 3`

### Issue: "Target closed" Error
**Cause:** Browser window was closed manually  
**Solution:** Let Kiro manage the browser lifecycle  
**Recovery:** Say "open localhost:3000" again to restart

### Issue: Elements Not Found
**Cause:** Page structure changed or wrong selector  
**Solution:** Use `browser_snapshot` to see current page structure  
**Alternative:** Use `browser_annotate` to visually select elements  
**Debug:** Check console errors with `browser_console_messages`

### Issue: "Navigation failed" or "net::ERR_CONNECTION_REFUSED"
**Cause:** Dev server isn't running, wrong port, or URL typo  
**Solution:** 
1. Verify dev server is running (`npm run dev`)
2. Check the correct port (3000, 5173, 4200, 8080)
3. Try `http://localhost:PORT` instead of `https://`
4. Ensure no firewall blocking localhost

### Issue: Overlay Not Showing
**Cause:** Overlay script not injected after navigation  
**Solution:** Re-inject after navigation using `browser_evaluate`  
**Reference:** Read `overlay.md` for the full injection script  
**Auto-fix:** Handled automatically in `smart-behaviors.md` workflow

### Issue: Slow Performance or Timeouts
**Cause:** Heavy page, slow network, or resource-intensive operations  
**Solution:**
1. Increase timeout: `browser_wait_for` with longer time
2. Use headless mode for faster execution
3. Disable images/CSS if only testing functionality
4. Check network tab for slow requests

### Issue: Browser Crashes or Hangs
**Cause:** Memory issues, corrupted browser installation, or infinite loops  
**Solution:**
1. Restart Kiro
2. Reinstall browser: `npx playwright install chromium --force`
3. Check for infinite loops in page JavaScript
4. Reduce viewport size to save memory

## Success Indicators

You'll know this power is working well when:

✅ Kiro automatically opens your localhost without being told the port  
✅ Screenshots appear in chat showing your actual UI  
✅ Console errors are caught and reported immediately  
✅ UI components are extracted with accurate CSS  
✅ E2E tests run and report pass/fail with screenshots  
✅ Accessibility issues are identified with specific fixes  
✅ Visual changes are verified before and after code edits  
✅ Network requests are monitored and analyzed  
✅ PDFs are generated with correct formatting

## Works Great With

- **Figma Power** - Implement Figma designs, then use this power to verify visually
- **Stripe Power** - Build payment UI, test checkout flows with browser automation
- **Supabase Power** - Build auth UI, test login/signup flows end-to-end
- **Postman Power** - Mock API responses, test UI with different data states
- **Datadog/Dynatrace Powers** - Monitor production issues, reproduce with browser automation
- **Neon/Aurora Powers** - Test database-driven UIs with real data

## For AI Agents

### Default Workflow
1. **Always start with `browser_snapshot`** (fast, structured data)
2. **Only use `browser_take_screenshot`** when visual details matter
3. **Use JPEG format for screenshots** to reduce file size: `type: "jpeg"` (50-150KB vs 500KB-1MB for PNG)
4. **Check `browser_console_messages`** after every navigation
5. **Wait 2-3 seconds** after code changes for hot reload
6. **Use `browser_annotate`** when user says "that one" or points visually

### Error Recovery
- If navigation fails → check if dev server is running
- If screenshot is blank → wait longer, check console errors
- If element not found → take snapshot to see current structure
- If browser crashes → reinstall with `npx playwright install chromium`

### Best Practices
- Take screenshots BEFORE and AFTER code changes
- Always report what you see in screenshots
- Suggest improvements based on visual analysis
- Offer to run accessibility checks proactively
- Use `browser_snapshot` for structure, `browser_take_screenshot` for visuals
- Check console errors immediately after navigation
- Wait for hot reload before re-inspecting (2-3 seconds)
- Use annotation mode when user references visual elements

### Tool Selection Guide
| Task | Preferred Tool | Why |
|------|---------------|-----|
| Check page structure | `browser_snapshot` | Fast, structured, accessibility tree |
| Visual verification | `browser_take_screenshot` | See actual rendering |
| Find elements | `browser_snapshot` first | Get accessibility refs |
| Debug issues | `browser_console_messages` | Catch JS errors |
| Wait for changes | `browser_wait_for` | Hot reload, animations |
| Select visually | `browser_annotate` | User draws selection |

## Prerequisites

- **Node.js 18+** (the only real prerequisite)
- **Chromium** — auto-installed on first use
- **Dev server running** for localhost testing
