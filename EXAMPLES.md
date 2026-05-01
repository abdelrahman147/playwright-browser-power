# Real-World Examples

Complete examples showing how to use the Playwright Browser Power for common tasks.

## Table of Contents

1. [Visual Development](#visual-development)
2. [UI Component Stealing](#ui-component-stealing)
3. [E2E Testing](#e2e-testing)
4. [Accessibility Audits](#accessibility-audits)
5. [Performance Testing](#performance-testing)
6. [Form Testing](#form-testing)
7. [Authentication Flows](#authentication-flows)
8. [Responsive Design](#responsive-design)
9. [API Mocking](#api-mocking)
10. [PDF Generation](#pdf-generation)

---

## Visual Development

### Example 1: Building a Hero Section

**Scenario:** You're building a landing page hero section and want visual feedback.

```
You: "create a hero section with a heading, subheading, and CTA button"

Kiro: [creates the component in your project]

You: "open localhost:3000"

Kiro: [navigates, takes screenshot, reports]
"I can see the hero section. The heading is 'Welcome to Our App', 
subheading is 'Build amazing things', and there's a blue CTA button."

You: "the spacing between heading and subheading is too tight"

Kiro: [updates CSS, waits for hot reload, takes new screenshot]
"I've increased the margin-bottom on the heading from 0.5rem to 1.5rem. 
Here's how it looks now."

You: "perfect! now make the CTA button bigger and more prominent"

Kiro: [updates button styles, verifies visually]
"I've increased the button padding and font size. The button is now 
more prominent and easier to click."

You: "check how it looks on mobile"

Kiro: [resizes viewport to 375x812, takes screenshot]
"On mobile (iPhone X size), the layout stacks vertically. The button 
spans the full width. Everything is readable and accessible."
```

**Result:** A polished hero section built with real-time visual feedback.

---

## UI Component Stealing

### Example 2: Stealing Stripe's Pricing Cards

**Scenario:** You love Stripe's pricing cards and want to recreate them.

```
You: "go to stripe.com/pricing"

Kiro: [navigates, takes screenshot]
"I'm on Stripe's pricing page. I can see three pricing tiers with 
cards showing features and pricing."

You: "steal the pricing cards"

Kiro: [takes detailed screenshot, extracts HTML/CSS]
"I've extracted the pricing card structure. Each card has:
- Header with plan name
- Large price display
- Feature list with checkmarks
- CTA button at bottom
- Subtle shadow and border
- Hover effect with slight elevation

How would you like me to recreate this?"

You: "build it in React with Tailwind CSS, use my brand colors"

Kiro: [creates PricingCard.tsx component]
"I've created a PricingCard component using Tailwind. I've adapted 
the colors to match your brand (blue primary, gray secondary). 
The structure and spacing match Stripe's design."

You: "show me how it looks"

Kiro: [navigates to your app, takes screenshot]
"Here's your pricing section. The cards have the same visual hierarchy 
and polish as Stripe's, but with your brand colors."

You: "make the hover effect more subtle"

Kiro: [adjusts hover transition]
"I've reduced the hover elevation from 8px to 4px and made the 
transition smoother (300ms ease-in-out)."
```

**Result:** Professional pricing cards adapted to your brand.

---

## E2E Testing

### Example 3: Testing a Login Flow

**Scenario:** You need to test your login functionality end-to-end.

```
You: "test the login flow"

Kiro: [navigates to /login, takes screenshot]
"I'm on the login page. I can see email and password fields, 
and a 'Sign In' button."

Kiro: [fills in test credentials]
"Filling in email: test@example.com"

Kiro: [enters password]
"Entering password"

Kiro: [clicks sign in button, waits for navigation]
"Clicking 'Sign In' button..."

Kiro: [takes screenshot of dashboard]
"✅ Login successful! I'm now on the dashboard at /dashboard. 
I can see the user menu with 'test@example.com' displayed."

You: "now test with invalid credentials"

Kiro: [navigates back to login]
"Testing with invalid credentials..."

Kiro: [fills invalid email, submits]
"❌ Login failed as expected. Error message displayed: 
'Invalid email or password'. The form didn't navigate away."

You: "test the 'Forgot Password' link"

Kiro: [clicks forgot password link]
"Clicked 'Forgot Password'. Navigated to /reset-password. 
Form is asking for email address."

You: "generate Playwright test code for this"

Kiro: [creates login.spec.ts]
"I've created login.spec.ts with three test cases:
1. Successful login with valid credentials
2. Failed login with invalid credentials  
3. Forgot password flow

The tests include all assertions and can run in your CI pipeline."
```

**Result:** Comprehensive login testing with automated test code.

---

## Accessibility Audits

### Example 4: WCAG Compliance Check

**Scenario:** You need to ensure your app meets WCAG 2.1 AA standards.

```
You: "check accessibility on the dashboard"

Kiro: [runs accessibility audit]
"I've found 8 accessibility issues:

🔴 Critical (2):
1. Missing alt text on logo image
   - Location: Header navigation
   - Fix: Add alt='Company Logo'
   
2. Form inputs missing labels
   - Location: Search form
   - Fix: Add <label> elements or aria-label

🟡 Moderate (4):
3. Low color contrast on secondary buttons
   - Current: 3.2:1, Required: 4.5:1
   - Fix: Darken button text color
   
4. Missing skip navigation link
   - Fix: Add 'Skip to main content' link
   
5. Heading hierarchy skips from h1 to h3
   - Fix: Use h2 for section headings
   
6. Links not descriptive ('Click here')
   - Fix: Use descriptive link text

🟢 Minor (2):
7. Missing lang attribute on HTML element
8. Page title could be more descriptive"

You: "fix the critical issues"

Kiro: [adds alt text and labels]
"I've fixed the critical issues:
1. Added alt='Company Logo' to the logo image
2. Added proper labels to all form inputs
3. Added aria-label to the search input

Running accessibility audit again..."

Kiro: [re-runs audit]
"✅ No critical issues remaining! 
4 moderate issues and 2 minor issues still present."

You: "fix the color contrast issue"

Kiro: [adjusts button colors]
"I've darkened the secondary button text from gray-500 to gray-700. 
New contrast ratio: 4.8:1 (passes WCAG AA)."
```

**Result:** WCAG-compliant dashboard with documented fixes.

---

## Performance Testing

### Example 5: Measuring Page Load Performance

**Scenario:** Your landing page feels slow and you want to identify bottlenecks.

```
You: "measure performance on the homepage"

Kiro: [navigates with performance tracing]
"Performance metrics for homepage:

⏱️ Load Times:
- First Contentful Paint (FCP): 1.2s
- Largest Contentful Paint (LCP): 2.8s ⚠️
- Time to Interactive (TTI): 3.5s ⚠️
- Total Load Time: 4.2s

📊 Resource Breakdown:
- JavaScript: 1.2MB (largest: bundle.js - 800KB)
- CSS: 180KB
- Images: 2.4MB ⚠️
- Fonts: 240KB

🐌 Slow Resources:
1. hero-image.jpg - 1.8MB, 2.1s
2. bundle.js - 800KB, 1.5s
3. analytics.js - 120KB, 0.8s"

You: "what's causing the slow LCP?"

Kiro: [analyzes LCP element]
"The LCP element is the hero image (hero-image.jpg). It's:
- 1.8MB uncompressed
- Not lazy loaded
- Loaded after JavaScript
- Not using modern formats (WebP/AVIF)

Recommendations:
1. Compress to WebP (would be ~400KB)
2. Add priority loading
3. Use responsive images
4. Consider above-the-fold optimization"

You: "optimize the hero image"

Kiro: [converts to WebP, adds priority loading]
"I've optimized the hero image:
- Converted to WebP format
- Added loading='eager' and fetchpriority='high'
- Created responsive sizes
- Reduced from 1.8MB to 380KB

Testing performance again..."

Kiro: [re-measures]
"✅ Performance improved!
- LCP: 2.8s → 1.4s (50% faster)
- Total Load: 4.2s → 2.8s
- Page size: 4.0MB → 2.4MB"
```

**Result:** 50% faster page load with specific optimizations.

---

## Form Testing

### Example 6: Testing a Multi-Step Form

**Scenario:** You have a multi-step signup form that needs thorough testing.

```
You: "test the signup form"

Kiro: [navigates to /signup]
"I'm on step 1 of 3: Personal Information"

Kiro: [fills in fields]
"Filling in:
- First Name: John
- Last Name: Doe
- Email: john@example.com"

Kiro: [clicks Next]
"Clicked 'Next'. Now on step 2 of 3: Account Details"

Kiro: [fills password fields]
"Setting password and confirming..."

Kiro: [clicks Next]
"Clicked 'Next'. Now on step 3 of 3: Preferences"

Kiro: [selects preferences]
"Selected preferences and clicked 'Complete Signup'"

Kiro: [waits for success]
"✅ Signup successful! Redirected to /welcome"

You: "test validation on step 1"

Kiro: [goes back to signup]
"Testing validation..."

Kiro: [submits empty form]
"❌ Validation working correctly:
- 'First name is required' shown
- 'Email is required' shown
- Form didn't advance to step 2"

Kiro: [enters invalid email]
"Entered 'notanemail' in email field"

Kiro: [tries to submit]
"❌ Email validation working:
- 'Please enter a valid email' shown
- Form didn't advance"

You: "test the back button"

Kiro: [fills step 1, goes to step 2, clicks back]
"✅ Back button works correctly:
- Returned to step 1
- Form data preserved (fields still filled)
- Can edit and proceed again"

You: "test browser back button"

Kiro: [uses browser back]
"⚠️ Issue found: Browser back button clears form data.
Recommendation: Implement session storage to preserve form state."
```

**Result:** Comprehensive form testing with bug discovered.

---

## Authentication Flows

### Example 7: Testing OAuth Login

**Scenario:** Your app uses Google OAuth and you need to test the flow.

```
You: "test Google OAuth login"

Kiro: [navigates to /login]
"I'm on the login page. I can see 'Sign in with Google' button."

Kiro: [clicks OAuth button]
"Clicked 'Sign in with Google'. Redirecting to Google..."

Kiro: [waits for Google page]
"Now on Google's OAuth consent screen (accounts.google.com)"

Kiro: [fills in test Google account]
"Using test account: test@gmail.com"

Kiro: [clicks Allow]
"Clicked 'Allow' to grant permissions"

Kiro: [waits for redirect back]
"Redirected back to your app at /auth/callback"

Kiro: [waits for final redirect]
"✅ OAuth flow complete! Now on /dashboard
User is logged in as 'test@gmail.com'"

You: "check what permissions were granted"

Kiro: [inspects session data]
"Permissions granted:
- Email address
- Basic profile info
- No access to Google Drive or Calendar"

You: "test the logout flow"

Kiro: [clicks logout]
"Clicked 'Logout'. Session cleared. Redirected to /login.
Verified: No user data in localStorage or cookies."

You: "test OAuth with denied permissions"

Kiro: [starts OAuth flow again]
"Starting OAuth flow..."

Kiro: [clicks Deny on Google]
"Clicked 'Deny' on Google consent screen"

Kiro: [checks error handling]
"✅ Error handled correctly:
- Redirected back to /login
- Error message shown: 'Login cancelled'
- No broken state"
```

**Result:** Complete OAuth flow testing including error cases.

---

## Responsive Design

### Example 8: Testing Across Breakpoints

**Scenario:** You need to verify your app works on all device sizes.

```
You: "test responsive design on the homepage"

Kiro: [tests desktop - 1920x1080]
"Desktop (1920x1080):
✅ Navigation horizontal
✅ 3-column grid layout
✅ Sidebar visible
✅ All content readable"

Kiro: [resizes to tablet - 768x1024]
"Tablet (768x1024):
✅ Navigation still horizontal
✅ 2-column grid layout
✅ Sidebar collapsed to hamburger menu
⚠️ Some text slightly cramped"

Kiro: [resizes to mobile - 375x812]
"Mobile (375x812):
✅ Navigation hamburger menu
✅ Single column layout
✅ Touch targets adequate size
❌ Issue: Hero image overflows container"

You: "fix the mobile image overflow"

Kiro: [adds max-width: 100%]
"Fixed image overflow with max-width: 100% and height: auto"

Kiro: [re-tests mobile]
"✅ Mobile (375x812) - Fixed:
- Image now fits container
- No horizontal scroll
- All content accessible"

You: "test landscape orientation"

Kiro: [rotates to 812x375]
"Mobile Landscape (812x375):
✅ Layout adapts correctly
✅ Navigation accessible
⚠️ Hero section very short (consider min-height)"

You: "test on small phones"

Kiro: [resizes to 320x568]
"Small Phone (iPhone SE - 320x568):
✅ Layout works
✅ Text readable
❌ Issue: Buttons too close together (touch targets)"

You: "increase button spacing on small screens"

Kiro: [adds mobile-specific spacing]
"Added margin-bottom: 1rem between buttons on screens < 375px"

Kiro: [verifies]
"✅ All breakpoints now working correctly:
- Desktop: 1920px+
- Laptop: 1024px-1919px
- Tablet: 768px-1023px
- Mobile: 375px-767px
- Small: 320px-374px"
```

**Result:** Fully responsive design tested across all breakpoints.

---

## API Mocking

### Example 9: Testing with Mocked API Responses

**Scenario:** You want to test how your UI handles different API states.

```
You: "test the user profile page with mocked API"

Kiro: [navigates to /profile]
"Loading profile page..."

You: "mock the API to return a loading state"

Kiro: [intercepts API, delays response]
"Mocking /api/user to delay 5 seconds..."

Kiro: [observes UI]
"✅ Loading state working:
- Skeleton loader displayed
- No error messages
- UI remains responsive"

You: "now mock it to return an error"

Kiro: [mocks 500 error]
"Mocking /api/user to return 500 Internal Server Error"

Kiro: [observes error handling]
"✅ Error handling working:
- Error message displayed: 'Failed to load profile'
- Retry button shown
- No crash or blank screen"

You: "mock it with incomplete data"

Kiro: [mocks partial response]
"Mocking /api/user with missing fields (no avatar, no bio)"

Kiro: [observes UI]
"✅ Handles missing data:
- Default avatar shown
- 'No bio yet' placeholder
- No undefined errors"

You: "mock it with a very long name"

Kiro: [mocks long string]
"Mocking name with 100 characters..."

Kiro: [checks layout]
"⚠️ Issue: Long name breaks layout
- Text overflows container
- Pushes other elements off screen

Recommendation: Add text-overflow: ellipsis"

You: "fix the overflow"

Kiro: [adds ellipsis]
"Added truncation with ellipsis for names > 50 characters"

Kiro: [verifies]
"✅ Long names now truncated gracefully with '...'"
```

**Result:** Robust error handling and edge case coverage.

---

## PDF Generation

### Example 10: Generating Documentation PDFs

**Scenario:** You need to generate PDF documentation from your web app.

```
You: "generate a PDF of the user guide"

Kiro: [navigates to /docs/user-guide]
"I'm on the user guide page"

Kiro: [generates PDF]
"Generating PDF with:
- A4 page size
- Margins: 1 inch
- Header: 'User Guide'
- Footer: Page numbers
- Print-optimized CSS"

Kiro: [saves PDF]
"✅ PDF generated: user-guide.pdf (2.4 MB, 24 pages)

Contents:
- Table of contents with links
- All images included
- Code blocks formatted
- Syntax highlighting preserved"

You: "make it printer-friendly"

Kiro: [regenerates with print CSS]
"Regenerated with print optimizations:
- Black and white mode
- Removed backgrounds
- Increased contrast
- Optimized for printing"

Kiro: [saves new PDF]
"✅ Print-friendly PDF: user-guide-print.pdf (1.1 MB, 24 pages)
- 54% smaller file size
- Better for printing
- Maintains readability"

You: "generate PDFs for all documentation pages"

Kiro: [iterates through docs]
"Generating PDFs for all docs pages..."

Kiro: [completes batch]
"✅ Generated 8 PDFs:
1. user-guide.pdf (2.4 MB)
2. api-reference.pdf (3.1 MB)
3. tutorials.pdf (1.8 MB)
4. faq.pdf (0.9 MB)
5. troubleshooting.pdf (1.2 MB)
6. changelog.pdf (0.6 MB)
7. contributing.pdf (0.8 MB)
8. license.pdf (0.2 MB)

Total: 11.0 MB"
```

**Result:** Complete documentation set in PDF format.

---

## Tips for Success

### General Tips
- Always check console errors first
- Wait 2-3 seconds after code changes
- Use snapshots for structure, screenshots for visuals
- Test on multiple viewports
- Save session state to avoid re-logging in

### Testing Tips
- Start with happy path, then test edge cases
- Mock API responses to test error states
- Generate test code after manual testing
- Use video recording for complex flows
- Document bugs with screenshots

### Performance Tips
- Use headless mode for faster execution
- Reduce viewport size to save memory
- Use browser_snapshot instead of screenshots when possible
- Close unused tabs
- Clear storage between tests

### Debugging Tips
- Check console messages immediately
- Take snapshots to see page structure
- Use annotation mode to identify elements
- Monitor network requests
- Check accessibility tree for hidden issues

---

**Want more examples?** Check the [steering files](steering/) for detailed workflows!

**Version:** 2.0.0 | **Last Updated:** May 1, 2026
