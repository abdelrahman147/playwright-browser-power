<div align="center">
  <img src="icon.png" alt="Playwright Browser Power" width="180" />
  
  # Playwright Browser Power
  
  ### Give Kiro Real Eyes 👁️
  
  **Launch browsers, take screenshots, steal UI components, run E2E tests, and debug visually.**
  
  [![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)
  [![Kiro Power](https://img.shields.io/badge/Kiro-Power-purple.svg)](https://kiro.dev)
  [![Playwright](https://img.shields.io/badge/Playwright-MCP-green.svg)](https://playwright.dev)
  
  [Installation](#installation) • [Quick Start](#quick-start) • [Features](#features) • [Documentation](#documentation)
  
</div>

---

## 🎯 What Is This?

A Kiro Power that gives AI real browser automation capabilities. Kiro can now:

- 🌐 **Launch real browsers** and navigate to any page
- 📸 **Take screenshots** and analyze UI visually  
- 🎨 **Steal UI components** from any website and recreate them
- 🧪 **Run E2E tests** with full automation
- 🐛 **Debug visually** with console/network/devtools inspection
- ♿ **Check accessibility** (WCAG compliance)
- 📊 **Test performance** (load times, network analysis)

**Built on Microsoft's official Playwright MCP server.**

---

## ⚡ Three Superpowers

### 🎨 UI Stealer — Copy Any Design Instantly

Browse to **any website**, select components you like, and Kiro extracts the complete design (HTML, CSS, animations, assets) and recreates it in your project.

```
You: "open stripe.com and steal the pricing cards"
Kiro: [extracts design, recreates in your tech stack]

You: "make it dark mode with my brand colors"
Kiro: [adapts the component]
```

**Why it's unique:** Turns any website into your component library.

### 👁️ Visual Builder — See What You Build

Build UI with instant visual feedback. Kiro opens your localhost, takes screenshots, identifies issues, and fixes them.

```
You: "open localhost:3000"
Kiro: [navigates, screenshots, analyzes]

You: "the header spacing is wrong, fix it"
Kiro: [fixes code, waits for reload, verifies]
```

**Why it's powerful:** No more alt-tabbing. Kiro sees what it builds.

### 🧪 Testing Suite — Complete Test Automation

E2E tests, visual regression, accessibility audits, performance testing — all in one power.

```
You: "test the login flow"
Kiro: [walks through flow, screenshots each step, reports issues]

You: "check accessibility"
Kiro: [runs WCAG audit, provides specific fixes]
```

**Why it's complete:** Replaces 5+ testing tools.

---

## 📦 Installation

### Option 1: Install as Kiro Power (Recommended)

1. Open Kiro Powers panel
2. Search for "Playwright Browser"
3. Click "Install"
4. Done!

### Option 2: Manual Installation

Add to `.kiro/settings/mcp.json`:

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

**Prerequisites:** Node.js 18+ (Chromium auto-installs on first use)

📖 **Detailed installation guide:** [INSTALL.md](INSTALL.md)

---

## 🚀 Quick Start

### Visual Development

```
You: "create a hero section with heading and CTA"
Kiro: [writes code]

You: "open localhost:3000"
Kiro: [navigates, screenshots, reports]

You: "increase the padding"
Kiro: [fixes, waits, re-screenshots, verifies]
```

### UI Stealing

```
You: "go to tailwindcss.com and grab the navbar"
Kiro: [extracts HTML/CSS, recreates in your project]

You: "make it responsive"
Kiro: [adds responsive styles, tests at multiple viewports]
```

### E2E Testing

```
You: "test the signup flow"
Kiro: [fills form, submits, verifies, screenshots each step]

You: "test with invalid email"
Kiro: [tests validation, verifies error messages]
```

### Accessibility Audit

```
You: "check accessibility on the dashboard"
Kiro: [runs WCAG audit, reports issues with fixes]
```

---

## ✨ Features

### Browser Control
- Navigate to any URL (localhost or remote)
- Click, type, scroll, hover, drag
- Fill forms, upload files
- Multi-tab management
- Browser history (back/forward)

### Visual Inspection
- Screenshots (full page or viewport)
- Accessibility snapshots (structured page content)
- Element highlighting
- Annotation mode (draw on page)

### Testing & Debugging
- Console messages (errors, warnings, logs)
- Network requests (monitor, mock, intercept)
- Performance tracing
- Storage management (cookies, localStorage, sessionStorage)
- Visual regression testing

### Advanced
- Generate PDFs from web pages
- Record videos with chapter markers
- Execute arbitrary JavaScript
- Connect to existing browser via CDP
- Generate test locators for CI/CD

---

## 🎯 When to Use

✅ **Perfect for:**
- Building UI with visual feedback
- Stealing/cloning UI from websites
- E2E testing web applications
- Debugging visual issues
- Accessibility audits (WCAG)
- Performance testing
- Generating PDFs
- Recording user flows

❌ **Not ideal for:**
- Unit testing (use Jest/Vitest)
- API-only testing (use Postman)
- Mobile app testing (use Appium)
- Load testing at scale (use k6/JMeter)

---

## 🛠️ Framework Integration

Works with all modern web frameworks:

| Framework | Command | Default Port |
|-----------|---------|--------------|
| React / Next.js | `npm run dev` | 3000 |
| Vue / Nuxt | `npm run dev` | 5173 |
| Svelte / SvelteKit | `npm run dev` | 5173 |
| Angular | `ng serve` | 4200 |
| Plain HTML | `npx serve .` | 3000 |

Then just say: `"open localhost:PORT"`

---

## 📚 Documentation

### Core Docs
- **[POWER.md](POWER.md)** - Complete feature documentation
- **[INSTALL.md](INSTALL.md)** - Installation guide for all platforms
- **[FAQ.md](FAQ.md)** - Frequently asked questions
- **[EXAMPLES.md](EXAMPLES.md)** - Real-world examples
- **[QUICK-REFERENCE.md](QUICK-REFERENCE.md)** - Cheat sheet

### Steering Files (Advanced Workflows)
- **[overlay.md](steering/overlay.md)** - Visual overlay system
- **[visual-feedback-loop.md](steering/visual-feedback-loop.md)** - Build → see → fix cycle
- **[ui-stealing.md](steering/ui-stealing.md)** - Component extraction workflow
- **[testing-suite.md](steering/testing-suite.md)** - Complete testing guide
- **[design-thinking.md](steering/design-thinking.md)** - UI analysis and improvement
- **[quick-recipes.md](steering/quick-recipes.md)** - 20+ ready-to-go workflows
- **[smart-behaviors.md](steering/smart-behaviors.md)** - Agent intelligence rules

---

## 🔧 Configuration

### Change Browser

```json
"--browser=firefox"  // or webkit, msedge
```

### Change Viewport

```json
"--viewport-size=375x812"   // Mobile
"--viewport-size=768x1024"  // Tablet
"--viewport-size=1920x1080" // Desktop
```

### Headless Mode (CI)

```json
"--headless"
```

---

## 🐛 Troubleshooting

### Browser won't launch
```bash
npx playwright install chromium
# On Linux, also run:
npx playwright install-deps chromium
```

### Screenshots are blank
Wait longer for page to load:
```
You: "wait 3 seconds then screenshot"
```

### Navigation fails
- Check if dev server is running
- Verify URL and port are correct
- Use `http://` instead of `https://` for localhost

### More help
See [FAQ.md](FAQ.md) for detailed troubleshooting.

---

## 🎨 Keywords That Activate This Power

Just talk naturally — Kiro understands:

- **Navigation:** "open", "browse", "go to", "check page"
- **Visual:** "screenshot", "how does it look", "show me"
- **UI Stealing:** "steal", "grab", "copy", "I want that navbar"
- **Testing:** "test", "check", "verify", "run e2e tests"
- **Design:** "make it look better", "improve design", "fix UI"
- **Debug:** "console errors", "network requests", "what's wrong"

---

## 🤝 Contributing

Contributions welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

We accept:
- 🐛 Bug reports
- 📝 Documentation improvements
- 🎯 New steering files
- 💡 Examples and use cases
- 🧪 Testing and feedback

---

## 📄 License

Apache 2.0 — Built on Microsoft's official Playwright MCP server.

---

## 👨‍💻 Author

**Created by [Abdelrahman Mohsen](https://github.com/abdelrahman147)**

Built with:
- [Playwright](https://playwright.dev/) by Microsoft
- [@playwright/mcp](https://github.com/microsoft/playwright-mcp) MCP server
- [Kiro](https://kiro.dev/) AI IDE

---

## 🌟 Support

- 💬 **Questions?** Check the [FAQ](FAQ.md)
- 🐛 **Issues?** See [Troubleshooting](#-troubleshooting)
- 💡 **Need help?** Open an issue

---

<div align="center">
  
  **Ready to give Kiro eyes?**
  
  [Install Now](#-installation) • [View Examples](EXAMPLES.md) • [Read Docs](POWER.md)
  
  Made with 👁️ by Abdelrahman Mohsen
  
</div>
