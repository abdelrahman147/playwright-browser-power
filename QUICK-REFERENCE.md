# Quick Reference Card

## Common Commands

### Navigation
```
"open localhost:3000"
"go to github.com"
"navigate back"
"refresh the page"
```

### Visual Inspection
```
"take a screenshot"
"show me how it looks"
"what's on the page"
"check the layout"
```

### Testing
```
"test the login flow"
"run e2e tests"
"check accessibility"
"verify the form works"
```

### UI Stealing
```
"steal the navbar from stripe.com"
"grab that pricing card"
"copy the hero section"
"extract that component"
```

### Debugging
```
"check console errors"
"show network requests"
"what's the error"
"why isn't it working"
```

### Design
```
"make it look better"
"improve the design"
"check responsive layout"
"test on mobile view"
```

## Key Workflows

### 1. Visual Development Loop
```
1. "open localhost:3000"
2. "the button is too small"
3. [Kiro fixes it]
4. "perfect, now make it blue"
```

### 2. Component Stealing
```
1. "go to tailwindcss.com"
2. "steal the pricing cards"
3. "make it dark mode"
4. "use my brand colors"
```

### 3. E2E Testing
```
1. "test the signup flow"
2. "try with invalid email"
3. "verify error messages"
4. "generate test code"
```

### 4. Accessibility Audit
```
1. "check accessibility"
2. "fix critical issues"
3. "verify the fixes"
4. "generate report"
```

## Tool Selection

| Need | Use | Why |
|------|-----|-----|
| Page structure | `"take a snapshot"` | Fast, structured |
| Visual check | `"take a screenshot"` | See rendering |
| Find errors | `"check console"` | Catch JS errors |
| Wait for changes | `"wait 3 seconds"` | Hot reload |
| Select visually | `"annotate the page"` | Draw selection |

## Viewport Sizes

```
"test on mobile"     → 375x812 (iPhone X)
"test on tablet"     → 768x1024 (iPad)
"test on desktop"    → 1920x1080 (HD)
"test on 4K"         → 3840x2160 (4K)
```

## Common Ports

```
React/Next.js        → localhost:3000
Vite (Vue/Svelte)    → localhost:5173
Angular              → localhost:4200
Create React App     → localhost:3000
Webpack Dev Server   → localhost:8080
```

## Troubleshooting Quick Fixes

| Problem | Quick Fix |
|---------|-----------|
| Browser won't launch | `npx playwright install chromium` |
| Blank screenshot | `"wait 3 seconds then screenshot"` |
| Navigation failed | Check dev server is running |
| Element not found | `"take a snapshot"` to see structure |
| Browser crashed | Restart Kiro |
| Slow performance | Use headless mode |

## Keyboard Shortcuts (in Browser)

```
"press Enter"
"press Tab"
"press Escape"
"press Ctrl+A"  (or Cmd+A on Mac)
```

## File Operations

```
"generate PDF"
"record video"
"save screenshot as image.png"
"export page as PDF"
```

## Network Operations

```
"show network requests"
"mock the API to return 500"
"intercept the login request"
"check API response"
```

## Storage Operations

```
"show cookies"
"clear localStorage"
"save session state"
"restore previous session"
```

## Best Practices

✅ **Do:**
- Check console after navigation
- Wait for hot reload (2-3 seconds)
- Use snapshots for structure
- Use screenshots for visuals
- Test on multiple viewports

❌ **Don't:**
- Close browser manually
- Skip error checking
- Test without dev server
- Ignore console warnings
- Forget to wait for loading

## Quick Debugging

```
1. "check console errors"     → Find JS errors
2. "take a snapshot"           → See page structure
3. "show network requests"     → Check API calls
4. "take a screenshot"         → Visual verification
5. "check accessibility"       → Find a11y issues
```

## Framework-Specific

### React
```
"open localhost:3000"
"check for React errors"
"test the component"
```

### Vue
```
"open localhost:5173"
"check Vue warnings"
"test the view"
```

### Angular
```
"open localhost:4200"
"check Angular errors"
"test the module"
```

## Testing Patterns

### Form Testing
```
"fill in the form"
"submit the form"
"verify success message"
"check validation errors"
```

### Auth Testing
```
"test login with valid credentials"
"test login with invalid credentials"
"verify redirect after login"
"check protected routes"
```

### Responsive Testing
```
"test on mobile view"
"test on tablet view"
"test on desktop view"
"check all breakpoints"
```

## Performance Testing

```
"measure page load time"
"check largest contentful paint"
"show slow network requests"
"identify performance bottlenecks"
```

## Accessibility Testing

```
"check WCAG compliance"
"find missing alt text"
"check color contrast"
"verify keyboard navigation"
"test with screen reader"
```

## Advanced Features

### Video Recording
```
"start recording"
"add chapter marker: Login"
"add chapter marker: Dashboard"
"stop recording"
```

### Multi-Tab
```
"open new tab"
"switch to tab 2"
"close current tab"
"list all tabs"
```

### DevTools
```
"start performance trace"
"stop performance trace"
"analyze trace"
```

## Configuration Quick Reference

### Change Browser
Edit `mcp.json`:
```json
"--browser=firefox"  // or webkit, msedge
```

### Change Viewport
```json
"--viewport-size=1920x1080"
```

### Enable Headless
```json
"--headless"
```

### Adjust Console Level
```json
"--console-level=error"  // or warning, info, debug
```

## Emergency Commands

```
"restart the browser"
"clear all cookies"
"reset to default viewport"
"close all tabs"
"stop all recordings"
```

## Getting Help

```
"how do I test forms?"
"show me accessibility examples"
"what can you do with this page?"
"help with UI stealing"
```

## Useful Combinations

### Build + Test
```
1. "create a login form"
2. "open localhost:3000"
3. "test the form"
4. "fix the validation"
```

### Steal + Customize
```
1. "go to stripe.com"
2. "steal the pricing section"
3. "make it dark mode"
4. "use my colors"
```

### Test + Report
```
1. "test the checkout flow"
2. "check accessibility"
3. "generate test report"
4. "create test code"
```

---

## Pro Tips

💡 **Always check console first** - Most issues show up there  
💡 **Use snapshots for speed** - Screenshots are slower  
💡 **Wait after code changes** - Give hot reload time  
💡 **Test on multiple viewports** - Responsive issues are common  
💡 **Save session state** - Avoid re-logging in  
💡 **Use annotation mode** - When pointing at specific elements  
💡 **Record videos** - Great for bug reports  
💡 **Generate test code** - Turn manual tests into automated ones  

---

**Print this card** or keep it handy while using the Playwright Browser Power!

**Version:** 2.0.0 | **Last Updated:** May 1, 2026
