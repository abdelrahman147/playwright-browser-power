# Frequently Asked Questions (FAQ)

## General Questions

### What is the Playwright Browser Power?

A Kiro Power that gives AI agents the ability to see and interact with web browsers. It enables visual feedback loops, UI component extraction, E2E testing, and accessibility audits through browser automation.

### Do I need to know Playwright to use this?

No! Just talk naturally to Kiro. Say things like "open localhost:3000" or "test the login flow" and Kiro handles the Playwright commands automatically.

### Is this the same as Playwright's regular API?

It uses Microsoft's official Playwright MCP server under the hood, but you interact with it through natural language instead of writing code.

### Can I use this for production testing?

Yes! It's perfect for E2E testing, visual regression, accessibility audits, and performance testing. You can even generate Playwright test code from your interactions.

## Installation & Setup

### What are the prerequisites?

Only **Node.js 18+**. Everything else (Chromium browser, Playwright MCP server) installs automatically on first use.

### Do I need to install Playwright separately?

No. The power uses `npx @playwright/mcp@latest` which downloads and runs Playwright automatically.

### Why is Chromium being downloaded?

Playwright needs a browser to automate. Chromium is downloaded once (~170MB) and reused for all future sessions.

### Can I use Firefox or Safari instead?

Yes! Edit `mcp.json` and change `--browser=chromium` to `--browser=firefox` or `--browser=webkit`. Then run `npx playwright install firefox` or `npx playwright install webkit`.

### Where are browsers installed?

- **Windows:** `%LOCALAPPDATA%\ms-playwright\`
- **macOS:** `~/Library/Caches/ms-playwright/`
- **Linux:** `~/.cache/ms-playwright/`

### How much disk space does it need?

- Chromium: ~170MB
- Firefox: ~80MB
- WebKit: ~60MB
- Playwright MCP: ~50MB

## Usage Questions

### How do I open my local development server?

Just say: `"open localhost:3000"` (or whatever port your dev server uses)

Kiro will automatically:
- Navigate to the URL
- Take a screenshot
- Check for console errors
- Report what it sees

### Can Kiro see what's on the page?

Yes! Kiro can:
- Take screenshots (visual inspection)
- Read the accessibility tree (structure)
- Check console messages (errors/warnings)
- Monitor network requests
- Inspect element properties

### How do I steal UI from another website?

Say: `"go to stripe.com and steal the navbar"`

Kiro will:
1. Open the website
2. Take a screenshot
3. Extract HTML structure
4. Extract computed CSS
5. Recreate it in your project

### Can I test my app automatically?

Yes! Say: `"test the login flow"`

Kiro will:
- Navigate to your login page
- Fill in the form
- Submit it
- Verify the result
- Take screenshots at each step

### How do I check accessibility?

Say: `"check accessibility"` or `"run WCAG audit"`

Kiro will:
- Scan the page
- Check WCAG compliance
- Report issues with severity
- Suggest specific fixes

### Can I generate PDFs?

Yes! Say: `"generate a PDF of this page"`

Kiro will create a PDF with proper formatting, headers, and footers.

### Can I record videos of user flows?

Yes! Say: `"record a video of the signup flow"`

Kiro will:
- Start video recording
- Walk through the flow
- Add chapter markers
- Save the video

## Troubleshooting

### Browser won't launch

**Try these in order:**

1. **Check Node.js:**
```bash
node --version  # Should be 18+
```

2. **Install Chromium manually:**
```bash
npx playwright install chromium
```

3. **On Linux, install dependencies:**
```bash
npx playwright install-deps chromium
```

4. **Restart Kiro**

### Screenshots are blank

**Causes:**
- Page hasn't finished loading
- JavaScript errors preventing render
- Network issues

**Solutions:**
- Say: `"wait 3 seconds then screenshot"`
- Check console: `"check console errors"`
- Try a simpler page first

### "Navigation failed" error

**Causes:**
- Dev server not running
- Wrong port number
- Firewall blocking localhost
- HTTPS on localhost without cert

**Solutions:**
1. Verify dev server is running: `npm run dev`
2. Check the port: `3000`, `5173`, `4200`, `8080`
3. Use `http://` not `https://` for localhost
4. Try: `"open http://localhost:3000"`

### Elements not found

**Causes:**
- Page structure changed
- Element not visible yet
- Wrong selector

**Solutions:**
- Take a snapshot: `"take a snapshot"`
- Wait for element: `"wait for the button to appear"`
- Use visual selection: `"annotate the page"`

### Browser crashes

**Causes:**
- Memory issues
- Corrupted installation
- Infinite loops in page JS

**Solutions:**
1. Restart Kiro
2. Reinstall browser: `npx playwright install chromium --force`
3. Reduce viewport size
4. Check for infinite loops in your code

### "Target closed" error

**Cause:** Browser window was closed manually

**Solution:** Let Kiro manage the browser. Say `"open localhost:3000"` again.

### Slow performance

**Causes:**
- Heavy page with lots of resources
- Slow network
- Large viewport size

**Solutions:**
- Use headless mode (edit `mcp.json`, add `--headless`)
- Reduce viewport size
- Disable images if not needed
- Check network tab for slow requests

## Configuration

### How do I change the viewport size?

Edit `mcp.json`:

```json
"--viewport-size=1920x1080"  // Desktop
"--viewport-size=375x812"    // iPhone X
"--viewport-size=768x1024"   // iPad
```

### How do I enable headless mode?

Edit `mcp.json` and add `--headless` to the args array.

**Pros:**
- Faster execution
- Lower memory usage
- Works in CI/CD

**Cons:**
- Can't see what's happening
- Harder to debug

### How do I change the browser?

Edit `mcp.json`:

```json
"--browser=firefox"  // or "webkit", "msedge"
```

Then install:
```bash
npx playwright install firefox
```

### Can I connect to an existing browser?

Yes! If you have a browser running with remote debugging:

```json
"--cdp-endpoint=http://localhost:9222"
```

### How do I ignore HTTPS errors?

Already enabled by default with `--ignore-https-errors`. This lets you test localhost with self-signed certificates.

## Advanced Usage

### Can I run multiple browsers at once?

Not directly through this power. Each MCP server instance manages one browser. For parallel testing, use Playwright's native test runner.

### Can I test on mobile devices?

You can emulate mobile viewports:

```json
"--viewport-size=375x812"  // iPhone X
"--viewport-size=414x896"  // iPhone 11 Pro Max
"--viewport-size=360x640"  // Android
```

For real device testing, use Appium or BrowserStack.

### Can I mock network requests?

Yes! Say: `"mock the API to return error 500"`

Kiro can intercept and modify network requests using `browser_route`.

### Can I test authentication flows?

Yes! Kiro can:
- Fill login forms
- Handle OAuth redirects
- Save/restore cookies
- Manage session storage
- Test protected routes

### Can I generate test code?

Yes! After testing manually, say: `"generate Playwright test code for this"`

Kiro will create a `.spec.js` file with all the steps and assertions.

### Can I use this in CI/CD?

Yes! Use headless mode and ensure browsers are installed:

```yaml
# GitHub Actions
- name: Install Playwright
  run: npx playwright install --with-deps chromium
```

## Integration

### Does it work with React?

Yes! Works with any framework:
- React / Next.js
- Vue / Nuxt
- Svelte / SvelteKit
- Angular
- Plain HTML

Just start your dev server and say `"open localhost:PORT"`.

### Can I use it with TypeScript?

Yes! The power works with any tech stack. It interacts with the rendered HTML/CSS/JS, not your source code.

### Does it work with Tailwind CSS?

Yes! Kiro can see and extract Tailwind classes when stealing UI components.

### Can I use it with component libraries?

Yes! Works with:
- Material-UI
- Ant Design
- Chakra UI
- Bootstrap
- Any component library

### Does it integrate with testing frameworks?

You can generate Playwright test code that works with:
- Jest
- Vitest
- Mocha
- Jasmine

## Performance

### How fast is it?

- **Navigation:** 1-3 seconds
- **Screenshot:** 0.5-1 second
- **Snapshot:** 0.1-0.3 seconds
- **Console check:** 0.1 second

Headless mode is ~30% faster.

### Does it use a lot of memory?

- **Headed browser:** ~200-400MB
- **Headless browser:** ~100-200MB
- **MCP server:** ~50MB

### Can I speed it up?

Yes:
1. Use headless mode
2. Reduce viewport size
3. Use `browser_snapshot` instead of screenshots
4. Disable images/CSS if not needed
5. Close unused tabs

## Comparison

### How is this different from Selenium?

- **Playwright** is faster, more reliable, and modern
- **Better API** for automation
- **Auto-wait** for elements
- **Network interception** built-in
- **Multiple browsers** with one API

### How is this different from Puppeteer?

- **Playwright** supports Firefox and WebKit
- **Better cross-browser** support
- **More features** (network, storage, etc.)
- **Better debugging** tools

### How is this different from Cypress?

- **Playwright** is faster
- **Better for E2E** across multiple pages
- **Network mocking** is easier
- **Multiple tabs** supported
- **Can test any website**, not just your own

## Best Practices

### When should I use screenshots vs snapshots?

**Use `browser_snapshot` (fast) for:**
- Checking page structure
- Finding elements
- Reading text content
- Accessibility audits

**Use `browser_take_screenshot` (slower) for:**
- Visual verification
- Design review
- Bug reports
- Documentation

### How often should I check console errors?

After every navigation! Console errors often explain why things aren't working.

### Should I use headed or headless mode?

**Headed (default):**
- Development
- Debugging
- Visual verification
- Learning

**Headless:**
- CI/CD
- Automated testing
- Performance testing
- Background tasks

### How do I organize my tests?

1. **Manual exploration** - Use Kiro to explore and test
2. **Generate test code** - Ask Kiro to create `.spec.js` files
3. **Run in CI** - Use generated tests in your pipeline
4. **Maintain** - Update tests as features change

## Limitations

### What can't this power do?

- **Native mobile apps** (use Appium)
- **Desktop apps** (use Playwright for desktop)
- **Load testing at scale** (use k6, JMeter)
- **Real device testing** (use BrowserStack, Sauce Labs)
- **Cross-browser testing in parallel** (use Playwright test runner)

### Are there any security concerns?

- Only test sites you own or have permission to test
- Don't store credentials in code
- Use environment variables for secrets
- Be careful with production data
- Don't scrape sites without permission

### What about rate limiting?

When stealing UI from external sites:
- Be respectful of rate limits
- Don't hammer servers
- Cache results when possible
- Consider using their API instead

## Getting Help

### Where can I find more examples?

- Check the `steering/` folder for detailed workflows
- Read `quick-recipes.md` for 20+ common tasks
- See `README.md` for quick start examples
- Review `POWER.md` for complete documentation

### How do I report a bug?

1. Check this FAQ first
2. Review troubleshooting section
3. Open an issue with:
   - Your OS and Node version
   - Steps to reproduce
   - Error messages
   - Screenshots

### How do I request a feature?

Open an issue describing:
- What you want to do
- Why it's useful
- How you'd use it
- Examples of similar features

### Where can I get support?

- Read the documentation
- Check existing issues
- Open a new issue
- Ask in the Kiro community

## Contributing

### Can I contribute to this power?

Yes! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

### What kind of contributions are welcome?

- Bug reports
- Documentation improvements
- New steering files
- Examples and use cases
- Testing and feedback

### How do I add a new steering file?

1. Create a new `.md` file in `steering/`
2. Follow the template in CONTRIBUTING.md
3. Test it thoroughly
4. Submit a pull request

---

## Still have questions?

Open an issue with the `question` label and we'll help you out!
