<div align="center">
  <img src="icon.png" alt="Playwright Browser Power" width="200" />
  
  # Playwright Browser Power for Kiro
  
  **by Abdelrahman Mohsen**
</div>

Give Kiro real eyes — a complete browser automation power that lets Kiro see what it builds, steal UI from any website, and run comprehensive test suites.

## Three Superpowers (Most → Least Impressive)

### 🎨 #1: UI Stealer — Copy Any Design Instantly
**The most unique feature — no other power does this.**

- Browse to **any website** (Stripe, Airbnb, Linear, etc.)
- Select components you like (navbar, hero, pricing cards, etc.)
- Kiro **extracts the complete design** — HTML structure, computed CSS, animations, assets
- **Recreates it in your project**, adapted to your tech stack (React, Vue, Svelte, etc.)
- Apply instant modifications: "make it dark mode", "use my brand colors", "add glassmorphism"
- **Interactive selection mode** — draw a box around what you want, Kiro builds it

**Why it's impressive:** Turns any website into your component library. See a design you like? Steal it in seconds.

### 👁️ #2: Visual Builder — See What You Build in Real-Time
**Build UI with instant visual feedback — like pair programming with a designer.**

- Launch a **real browser** and navigate to your app (localhost or any URL)
- Take **screenshots** and analyze the visual output
- Kiro **identifies issues**: layout problems, broken styles, rendering bugs, spacing issues
- **Fix the code** and verify by taking another screenshot
- **Iterate until perfect** — build → see → fix → verify cycle
- Works with **hot reload** — Kiro waits for changes and re-checks automatically

**Why it's impressive:** No more alt-tabbing between code and browser. Kiro sees what you build and fixes it visually.

### 🧪 #3: Testing Suite — Complete Test Automation
**E2E, visual regression, accessibility, performance — all in one.**

- **E2E testing** — walk through user flows (signup, login, checkout) and verify each step
- **Visual regression** — compare before/after screenshots, detect pixel-level differences
- **Accessibility audits** — full WCAG compliance checks with specific fixes
- **Performance testing** — measure load times, TTFB, LCP, identify bottlenecks
- **API testing** — monitor network requests, mock responses, test error states
- **Generate test code** — Kiro writes Playwright tests for CI/CD

**Why it's impressive:** Replaces 5+ testing tools. One power for all web testing needs.

## Installation

### Option 1: Install as a Kiro Power (Recommended)

1. Open Kiro Powers panel (👻⚡ icon)
2. Search for "Playwright Browser"
3. Click "Install"
4. Done! The power activates automatically

**See [INSTALL.md](INSTALL.md) for detailed installation instructions, platform-specific notes, and troubleshooting.**

### Option 2: Manual MCP Configuration

Copy the `mcp.json` configuration to your workspace's `.kiro/settings/mcp.json`:

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": [
        "@playwright/mcp@latest",
        "--caps=vision,pdf,devtools,network,storage,testing",
        "--viewport-size=1280x720",
        "--console-level=error",
        "--ignore-https-errors"
      ]
    }
  }
}
```

## Prerequisites

- **Node.js 18+** — the only real prerequisite
- **Chromium browser** — auto-installed on first use by Kiro
- **Dev server running** — for testing localhost apps

Kiro handles browser installation automatically. Just have Node.js installed.

## Quick Start

### Example 1: Visual Feedback Loop

```
You: "open localhost:3000"
```

Kiro will:
1. Navigate to your app
2. Take a screenshot
3. Check console for errors
4. Analyze the page structure
5. Report what it sees

```
You: "the header looks wrong, fix it"
```

Kiro will:
1. Identify the issue
2. Fix the code
3. Wait for hot reload
4. Take a new screenshot
5. Verify the fix

### Example 2: UI Stealing

```
You: "open stripe.com and steal the navbar"
```

Kiro will:
1. Navigate to stripe.com
2. Identify the navbar
3. Extract HTML, CSS, and assets
4. Ask how you want it built
5. Recreate it in your project

```
You: "make it dark mode with my brand colors"
```

Kiro adapts the component to your specifications.

### Example 3: E2E Testing

```
You: "test the login flow"
```

Kiro will:
1. Navigate to the login page
2. Fill in credentials
3. Submit the form
4. Verify successful login
5. Take screenshots at each step
6. Report any issues

```
You: "check accessibility"
```

Kiro runs a full WCAG audit and reports issues.

### Example 4: Component Development

```
You: "create a hero section with heading and CTA"
Kiro: [writes the code]

You: "open localhost:3000"
Kiro: [navigates, takes screenshot, reports]

You: "spacing is too tight, increase padding"
Kiro: [fixes, waits, re-screenshots, verifies]
```

## When to Use This Power

✅ **Perfect for:**
- Building UI components with visual feedback
- Stealing/cloning UI from existing websites
- Running E2E tests on web applications
- Debugging visual issues (layout, styling, responsiveness)
- Accessibility audits (WCAG compliance)
- Performance testing (load times, network analysis)
- Generating PDFs from web pages
- Recording user flow videos

❌ **Not ideal for:**
- Unit testing (use Jest, Vitest instead)
- API-only testing without UI (use Postman power)
- Mobile app testing (use Appium)
- Load testing at scale (use k6, JMeter)

## Framework Integration

### React / Next.js
```bash
npm run dev
# Then: "open localhost:3000"
```

### Vue / Nuxt
```bash
npm run dev
# Then: "open localhost:5173"
```

### Svelte / SvelteKit
```bash
npm run dev
# Then: "open localhost:5173"
```

### Angular
```bash
ng serve
# Then: "open localhost:4200"
```

### Plain HTML
```bash
npx serve .
# Then: "open localhost:3000"
```

## Steering Files

The power includes 7 steering files with detailed workflows:

| File | Purpose |
|------|---------|
| `overlay.md` | Injectable overlay script and control API |
| `visual-feedback-loop.md` | Core build → see → fix → verify cycle |
| `ui-stealing.md` | Extract and recreate components from any website |
| `testing-suite.md` | E2E, visual regression, accessibility, performance testing |
| `design-thinking.md` | Analyze and improve UI design |
| `quick-recipes.md` | 17+ ready-to-go workflows for common tasks |
| `smart-behaviors.md` | Agent intelligence rules and auto-detection |

Kiro reads these automatically when needed, or you can reference them explicitly:

```
You: "read the ui-stealing workflow"
```

### 🚀 Quick Links

- **New to this power?** Start with [Quick Start](#quick-start)
- **Installation issues?** Check [INSTALL.md](INSTALL.md) troubleshooting
- **Have questions?** See [FAQ.md](FAQ.md)
- **Want examples?** Read [EXAMPLES.md](EXAMPLES.md)
- **Need quick reference?** Print [QUICK-REFERENCE.md](QUICK-REFERENCE.md)

## Features

### Browser Control
- Navigate to any URL
- Click, type, scroll, hover
- Fill forms, upload files
- Browser history (back/forward)
- Multi-tab management

### Visual Inspection
- Take screenshots (full page or viewport)
  - **Tip:** Use `type: "jpeg"` for 80-90% smaller file sizes (50-150KB vs 500KB-1MB PNG)
- Get accessibility snapshots (structured page content)
- Highlight elements
- Annotation mode (draw on the page)

### Testing & Debugging
- Console messages (errors, warnings, logs)
- Network requests (monitor, mock, intercept)
- Performance tracing
- Storage management (cookies, localStorage, sessionStorage)

### Advanced
- Generate PDFs
- Record video with chapter markers
- Execute arbitrary JavaScript
- Connect to existing browser via CDP
- Generate test locators

## Configuration

### Change Browser

Edit `mcp.json` to use Firefox or WebKit:

```json
"--browser=firefox"
```

### Change Viewport

```json
"--viewport-size=375x812"  // Mobile
"--viewport-size=768x1024" // Tablet
"--viewport-size=1920x1080" // Desktop
```

### Headless Mode

Add `--headless` for invisible browser (CI environments):

```json
"args": [
  "@playwright/mcp@latest",
  "--headless",
  ...
]
```

### Connect to Existing Browser

```json
"--cdp-endpoint=http://localhost:9222"
```

## Common Issues & Solutions

### Browser won't launch

**Cause:** Chromium not installed  
**Solution:** Kiro auto-installs on first use

Manual fix if needed:
```bash
npx playwright install chromium
```

On Linux, you may also need system dependencies:
```bash
npx playwright install-deps chromium
```

### Screenshots are blank

**Cause:** Page hasn't finished loading  
**Solution:** Tell Kiro to wait longer

```
You: "wait 3 seconds then screenshot"
```

### Navigation fails

**Possible causes:**
- Dev server isn't running
- Wrong port number
- URL typo

**Solutions:**
- Check if your dev server is running (`npm run dev`)
- Verify the URL and port are correct
- Try common alternatives (3000, 5173, 4200, 8080)
- Use `http://` instead of `https://` for localhost

### Overlay not showing

**Cause:** Overlay script not injected after navigation  
**Solution:** Kiro re-injects automatically

The overlay is injected after each navigation. If it's missing, Kiro needs to re-inject it. This is handled automatically in the `smart-behaviors.md` workflow.

### Elements not found

**Cause:** Page structure changed or wrong selector  
**Solution:** Use snapshot to see current structure

```
You: "take a snapshot to see the page structure"
```

### Console errors appearing

**This is actually good!** Kiro catches JavaScript errors automatically and reports them. This helps you fix bugs before they reach production.

## Success Indicators

You'll know this power is working well when:

✅ Kiro automatically opens your localhost  
✅ Screenshots appear showing your actual UI  
✅ Console errors are caught and reported  
✅ UI components are extracted with accurate CSS  
✅ E2E tests run with pass/fail screenshots  
✅ Accessibility issues are identified with fixes  
✅ Visual changes are verified before/after edits

## Works Great With

- **Figma Power** - Implement designs, verify visually
- **Stripe Power** - Build payment UI, test checkout flows
- **Supabase Power** - Build auth UI, test login/signup
- **Postman Power** - Mock APIs, test UI with different data
- **Datadog/Dynatrace** - Monitor production, reproduce issues

## Troubleshooting

### Browser won't launch

Kiro auto-installs Chromium on first use. If it fails:

```bash
npx playwright install chromium
```

On Linux, you may also need system dependencies:

```bash
npx playwright install-deps chromium
```

### Screenshots are blank

The page hasn't finished loading. Kiro should wait longer:

```
You: "wait 3 seconds then screenshot"
```

### Navigation fails

- Check if your dev server is running
- Verify the URL and port are correct
- Try common alternatives (3000, 5173, 4200, 8080)

### Overlay not showing

The overlay is injected after each navigation. If it's missing, Kiro needs to re-inject it. This is handled automatically in the `smart-behaviors.md` workflow.

### Advanced Troubleshooting

**"Target closed" error:**
- Browser window was closed manually
- Let Kiro manage the browser lifecycle
- Say "open localhost:3000" again to restart

**Slow performance:**
- Use headless mode for faster execution
- Reduce viewport size to save memory
- Check network tab for slow requests

**Browser crashes:**
1. Restart Kiro
2. Reinstall browser: `npx playwright install chromium --force`
3. Check for infinite loops in page JavaScript

## Examples

### Example 1: Build a Component Visually

```
You: "create a hero section with a heading, subheading, and CTA button"
Kiro: [writes the code]

You: "open localhost:3000"
Kiro: [navigates, takes screenshot, reports]

You: "the spacing is too tight, increase padding"
Kiro: [fixes, waits, re-screenshots, verifies]

You: "perfect, now make it responsive"
Kiro: [adds responsive styles, tests at multiple viewports]
```

### Example 2: Steal a Component

```
You: "open tailwindcss.com and steal the pricing cards"
Kiro: [navigates, identifies pricing section, extracts design]

You: "build it in React with Tailwind, use my brand colors"
Kiro: [creates component adapted to your stack]

You: "show me how it looks"
Kiro: [navigates to your app, screenshots the new component]
```

### Example 3: Test a User Flow

```
You: "test the signup flow"
Kiro: [navigates to signup, fills form, submits, verifies success]

You: "now test with invalid email"
Kiro: [tests validation, verifies error messages appear]

You: "generate Playwright test code for this"
Kiro: [creates test file with all assertions]
```

### Example 4: Accessibility Audit

```
You: "check accessibility on the dashboard"
Kiro: [navigates, runs full WCAG audit, reports issues]

You: "fix the critical issues"
Kiro: [adds missing alt text, labels, ARIA attributes]

You: "verify the fixes"
Kiro: [re-runs audit, confirms issues resolved]
```

## Keywords That Activate This Power

The power activates automatically when you use these phrases:

- **Navigation**: "open", "browse", "navigate", "go to", "check page"
- **Visual**: "screenshot", "how does it look", "show me", "preview"
- **UI Stealing**: "steal", "grab", "copy", "clone", "extract", "I want that"
- **Testing**: "test", "check", "verify", "run tests", "e2e"
- **Design**: "make it look better", "improve design", "fix the UI"
- **Debugging**: "console errors", "network requests", "what's wrong"

Just talk naturally — Kiro understands intent.

## Technical Details

- **MCP Server**: `@playwright/mcp` (Microsoft's official Playwright MCP server)
- **Default Browser**: Chromium (Chrome)
- **Default Viewport**: 1280x720
- **Capabilities**: vision, pdf, devtools, network, storage, testing
- **Mode**: Headed (visible browser window)
- **Console Level**: error (auto-captures JavaScript errors)

## Documentation

- **[POWER.md](POWER.md)** - Complete power documentation with all features
- **[INSTALL.md](INSTALL.md)** - Detailed installation guide for all platforms
- **[FAQ.md](FAQ.md)** - Frequently asked questions and answers
- **[CONTRIBUTING.md](CONTRIBUTING.md)** - How to contribute to this power
- **[CHANGELOG.md](CHANGELOG.md)** - Version history and updates

### Steering Files

- **[overlay.md](steering/overlay.md)** - Injectable overlay script and control API
- **[visual-feedback-loop.md](steering/visual-feedback-loop.md)** - Core build → see → fix → verify cycle
- **[ui-stealing.md](steering/ui-stealing.md)** - Extract and recreate components from any website
- **[testing-suite.md](steering/testing-suite.md)** - E2E, visual regression, accessibility, performance testing
- **[design-thinking.md](steering/design-thinking.md)** - Analyze and improve UI design
- **[quick-recipes.md](steering/quick-recipes.md)** - 20+ ready-to-go workflows for common tasks
- **[smart-behaviors.md](steering/smart-behaviors.md)** - Agent intelligence rules and auto-detection

## Contributing

Found a bug or have a suggestion? See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

We welcome:
- Bug reports
- Documentation improvements
- New steering files
- Examples and use cases
- Testing and feedback

## License

This power uses Microsoft's official Playwright MCP server, which is licensed under Apache 2.0.

## Credits

**Created by Abdelrahman Mohsen**

Built on top of:
- [Playwright](https://playwright.dev/) by Microsoft
- [@playwright/mcp](https://github.com/microsoft/playwright-mcp) MCP server
- [Kiro](https://kiro.dev/) AI IDE

## Support

- **Questions?** Check the [FAQ](FAQ.md)
- **Issues?** See [Troubleshooting](#common-issues--solutions)
- **Need help?** Open an issue with the `question` label

---

**Ready to give Kiro eyes?** Install this power and start building visually.

**Version:** 2.0.0 | **Last Updated:** May 1, 2026
