# Installation Guide

## Quick Install (Recommended)

### Via Kiro Powers UI

1. Open Kiro IDE
2. Click the Powers panel (👻⚡ icon)
3. Search for "Playwright Browser"
4. Click "Install"
5. Done! The power activates automatically

### Via Local Directory

If you have the power files locally:

1. Open Kiro Powers UI
2. Click "Add Custom Power"
3. Select "Local Directory"
4. Browse to the `playwright-browser` folder
5. Click "Add"

## Manual Installation

### Option 1: Copy to Powers Directory

```bash
# Copy the entire playwright-browser folder to:
~/.kiro/powers/playwright-browser/

# Or for workspace-specific:
.kiro/powers/playwright-browser/
```

Then restart Kiro or reload powers.

### Option 2: MCP Configuration Only

If you just want the MCP server without the power documentation:

1. Open `.kiro/settings/mcp.json` (create if doesn't exist)
2. Add this configuration:

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

3. Restart Kiro

## Prerequisites

### Required
- **Node.js 18+** - [Download here](https://nodejs.org/)

### Auto-Installed
- **Chromium browser** - Installed automatically on first use
- **Playwright MCP server** - Installed via npx on first use

## First-Time Setup

### Automatic Setup (Recommended)

Kiro handles everything automatically:

1. Install the power
2. Say "open localhost:3000"
3. Kiro will:
   - Install Chromium if needed
   - Install Playwright MCP server
   - Launch the browser
   - Take a screenshot

**You don't need to do anything manually!**

### Manual Setup (If Automatic Fails)

#### Install Chromium

```bash
npx playwright install chromium
```

#### On Linux, Install System Dependencies

```bash
npx playwright install-deps chromium
```

#### Verify Installation

```bash
npx @playwright/mcp@latest --version
```

## Platform-Specific Notes

### Windows
- Chromium installs to: `%LOCALAPPDATA%\ms-playwright\`
- No system dependencies needed
- Works out of the box

### macOS
- Chromium installs to: `~/Library/Caches/ms-playwright/`
- No system dependencies needed
- May need to allow browser in Security & Privacy settings

### Linux
- Chromium installs to: `~/.cache/ms-playwright/`
- **May need system dependencies:**

```bash
# Ubuntu/Debian
npx playwright install-deps chromium

# Or manually:
sudo apt-get install -y \
  libnss3 \
  libnspr4 \
  libatk1.0-0 \
  libatk-bridge2.0-0 \
  libcups2 \
  libdrm2 \
  libxkbcommon0 \
  libxcomposite1 \
  libxdamage1 \
  libxfixes3 \
  libxrandr2 \
  libgbm1 \
  libasound2
```

### Docker/CI Environments

```dockerfile
# In your Dockerfile
RUN npx playwright install --with-deps chromium
```

Or in CI:

```yaml
# GitHub Actions example
- name: Install Playwright
  run: npx playwright install --with-deps chromium
```

## Configuration Options

### Change Browser

Edit `mcp.json` to use a different browser:

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": [
        "@playwright/mcp@latest",
        "--browser=firefox",  // or "webkit", "msedge"
        "--caps=vision,pdf,devtools,network,storage,testing",
        "--viewport-size=1280x720",
        "--console-level=error",
        "--ignore-https-errors"
      ]
    }
  }
}
```

Then install the browser:

```bash
npx playwright install firefox
# or
npx playwright install webkit
```

### Change Viewport Size

```json
"--viewport-size=375x812"   // iPhone X
"--viewport-size=768x1024"  // iPad
"--viewport-size=1920x1080" // Desktop HD
"--viewport-size=2560x1440" // Desktop 2K
```

### Enable Headless Mode

For CI/CD or when you don't need to see the browser:

```json
"args": [
  "@playwright/mcp@latest",
  "--headless",
  ...
]
```

### Connect to Existing Browser

If you have a browser running with remote debugging:

```json
"args": [
  "@playwright/mcp@latest",
  "--cdp-endpoint=http://localhost:9222",
  ...
]
```

### Adjust Console Logging

```json
"--console-level=error"   // Only errors (default)
"--console-level=warning" // Warnings and errors
"--console-level=info"    // Info, warnings, and errors
"--console-level=debug"   // Everything
```

## Verification

### Test the Installation

1. Open Kiro
2. In chat, type: `"open localhost:3000"`
3. You should see:
   - Browser window opens
   - Kiro navigates to the URL
   - Screenshot appears in chat
   - Console messages are reported

### Check MCP Server Status

1. Open Kiro Powers panel
2. Look for "Playwright Browser" power
3. Status should show "Active" or "Connected"

### Test Individual Features

```
# Test screenshot
"take a screenshot of google.com"

# Test navigation
"go to github.com"

# Test console
"check console errors on my app"

# Test accessibility
"run accessibility audit"
```

## Troubleshooting Installation

### "Command not found: npx"

**Cause:** Node.js not installed or not in PATH

**Solution:**
1. Install Node.js from [nodejs.org](https://nodejs.org/)
2. Restart your terminal
3. Verify: `node --version` and `npx --version`

### "Executable doesn't exist at ..."

**Cause:** Chromium not installed

**Solution:**
```bash
npx playwright install chromium
```

### "Permission denied" on Linux

**Cause:** Missing execute permissions

**Solution:**
```bash
chmod +x ~/.cache/ms-playwright/chromium-*/chrome-linux/chrome
```

### "Browser closed unexpectedly"

**Cause:** Missing system dependencies (Linux)

**Solution:**
```bash
npx playwright install-deps chromium
```

### MCP Server Won't Start

**Cause:** Port conflict or corrupted installation

**Solution:**
1. Restart Kiro
2. Clear npx cache: `npx clear-npx-cache`
3. Reinstall: `npx @playwright/mcp@latest --version`

### "Cannot find module '@playwright/mcp'"

**Cause:** Package not installed

**Solution:**
```bash
# Force install
npx @playwright/mcp@latest --version

# Or install globally
npm install -g @playwright/mcp
```

## Updating

### Update the Power

If installed via Powers UI:
1. Open Powers panel
2. Find "Playwright Browser"
3. Click "Check for updates"
4. Click "Update" if available

If installed manually:
1. Download latest version
2. Replace the `playwright-browser` folder
3. Restart Kiro

### Update Playwright MCP Server

The server auto-updates when using `@playwright/mcp@latest`.

To force update:
```bash
npx clear-npx-cache
npx @playwright/mcp@latest --version
```

### Update Chromium

```bash
npx playwright install chromium --force
```

## Uninstallation

### Remove the Power

Via Powers UI:
1. Open Powers panel
2. Find "Playwright Browser"
3. Click "Uninstall"

Manually:
```bash
rm -rf ~/.kiro/powers/playwright-browser/
```

### Remove MCP Configuration

Edit `.kiro/settings/mcp.json` and remove the `playwright` server entry.

### Remove Browsers

```bash
# Remove all Playwright browsers
npx playwright uninstall

# Remove specific browser
npx playwright uninstall chromium
```

## Getting Help

### Check Logs

Kiro logs are usually in:
- **macOS/Linux:** `~/.kiro/logs/`
- **Windows:** `%APPDATA%\Kiro\logs\`

### Common Log Locations

```bash
# MCP server logs
~/.kiro/logs/mcp-playwright.log

# Browser logs
~/.kiro/logs/browser.log
```

### Report Issues

If you encounter issues:

1. Check the troubleshooting section above
2. Review the logs
3. Try manual installation steps
4. Open an issue with:
   - Your OS and version
   - Node.js version (`node --version`)
   - Error messages
   - Steps to reproduce

## Next Steps

After installation:

1. ✅ Read the [README.md](README.md) for usage examples
2. ✅ Try the Quick Start examples
3. ✅ Explore the steering files for advanced workflows
4. ✅ Check out the [POWER.md](POWER.md) for complete documentation

---

**Ready to give Kiro eyes?** Start with: `"open localhost:3000"`
