# UI Stealing — Extract & Recreate Components from Any Website

This is one of the most powerful features. The user browses to any website, picks a component they like, and Kiro extracts it and recreates it in their project.

## Trigger Phrases

Activate this workflow when the user says:
- "steal that navbar" / "grab that hero" / "I want that card"
- "copy that design" / "clone that section" / "take that component"
- "make me something like [website]" / "I want a navbar like [site]"
- "extract that UI" / "rip that layout"
- "open [url] and steal the [component]"

## Workflow 1: User Describes What They Want

When the user says something like "steal the navbar from stripe.com":

### Step 1: Navigate to the Target Site
1. `browser_navigate` → the URL
2. `browser_wait_for` → `time: 3` (let everything load including fonts, images, animations)
3. Inject the overlay (from `overlay.md`)
4. `browser_evaluate` → `window.__kiro.status('Scanning page...')`

### Step 2: Identify the Component
1. `browser_take_screenshot` → see the full page
2. `browser_snapshot` → get the structure
3. Based on what the user described (e.g., "navbar"), identify the element in the snapshot
4. `browser_highlight` → highlight the identified component so the user can confirm

### Step 3: Ask for Confirmation
Tell the user: "I've highlighted what I think is the navbar. Is this the component you want? If not, you can describe it more specifically or I can open annotation mode for you to select it."

### Step 4: Extract the Component
Once confirmed, run this extraction via `browser_evaluate`:

```javascript
(element) => {
  // Get the target element
  const el = element;
  if (!el) return { error: 'Element not found' };

  // Extract computed styles for the element and all children
  function getStyles(node) {
    if (node.nodeType !== 1) return null;
    const computed = getComputedStyle(node);
    const styles = {};
    const important = [
      'display', 'flex-direction', 'justify-content', 'align-items', 'gap', 'flex-wrap',
      'grid-template-columns', 'grid-template-rows', 'grid-gap',
      'position', 'top', 'right', 'bottom', 'left', 'z-index',
      'width', 'height', 'min-width', 'max-width', 'min-height', 'max-height',
      'margin', 'margin-top', 'margin-right', 'margin-bottom', 'margin-left',
      'padding', 'padding-top', 'padding-right', 'padding-bottom', 'padding-left',
      'background', 'background-color', 'background-image', 'background-size',
      'color', 'font-family', 'font-size', 'font-weight', 'line-height', 'letter-spacing', 'text-align', 'text-decoration', 'text-transform',
      'border', 'border-radius', 'border-color', 'border-width', 'border-style',
      'box-shadow', 'opacity', 'overflow', 'cursor', 'transition', 'transform',
      'list-style', 'white-space', 'word-break'
    ];
    important.forEach(prop => {
      const val = computed.getPropertyValue(prop);
      if (val && val !== 'none' && val !== 'normal' && val !== 'auto' && val !== '0px' && val !== 'rgba(0, 0, 0, 0)' && val !== 'rgb(0, 0, 0)') {
        styles[prop] = val;
      }
    });
    return styles;
  }

  // Get bounding box
  const rect = el.getBoundingClientRect();

  // Get outer HTML
  const html = el.outerHTML;

  // Get all image sources
  const images = [...el.querySelectorAll('img')].map(img => ({
    src: img.src,
    alt: img.alt,
    width: img.naturalWidth,
    height: img.naturalHeight
  }));

  // Get all links
  const links = [...el.querySelectorAll('a')].map(a => ({
    text: a.textContent.trim(),
    href: a.href
  }));

  // Get SVG icons
  const svgs = [...el.querySelectorAll('svg')].map(svg => svg.outerHTML);

  // Get the element's styles
  const rootStyles = getStyles(el);

  // Get direct children styles
  const childrenStyles = [...el.children].map(child => ({
    tag: child.tagName.toLowerCase(),
    class: child.className,
    styles: getStyles(child),
    text: child.textContent.trim().slice(0, 100)
  }));

  return JSON.stringify({
    tag: el.tagName.toLowerCase(),
    classes: el.className,
    dimensions: { width: Math.round(rect.width), height: Math.round(rect.height) },
    html: html.slice(0, 5000),
    styles: rootStyles,
    children: childrenStyles.slice(0, 20),
    images,
    links: links.slice(0, 20),
    svgs: svgs.slice(0, 10),
    textContent: el.textContent.trim().slice(0, 500)
  }, null, 2);
}
```

Pass the `target` parameter pointing to the element's snapshot ref.

### Step 5: Analyze and Understand the Design
From the extracted data, understand:
- **Layout**: Is it flexbox? Grid? What's the direction, alignment, gap?
- **Colors**: Background, text, accent colors
- **Typography**: Font family, sizes, weights
- **Spacing**: Padding, margins, gaps
- **Components**: What sub-components exist (logo, nav links, buttons, etc.)
- **Responsive hints**: Are there media queries? Flex-wrap?

### Step 6: Ask User for Modifications
Before building, ask:
- "What tech stack should I use? (HTML/CSS, React, Vue, Svelte, Tailwind, etc.)"
- "Any modifications? Different colors, text, layout changes?"
- "Should I use your existing design system/variables?"

### Step 7: Build the Component
Create the component in the user's project:
1. Write the component code adapted to their tech stack
2. Use semantic HTML
3. Make it responsive
4. Replace placeholder content with the user's content
5. Apply any requested modifications

### Step 8: Verify
1. If the user has a dev server running, navigate to the page with the new component
2. Take a screenshot
3. Open the reference site in another tab
4. Compare side by side
5. Fix any differences

## Workflow 2: Interactive Selection (Annotation Mode)

When the user wants to visually pick a component:

### Step 1: Navigate and Prepare
1. `browser_navigate` → the URL
2. `browser_wait_for` → `time: 3`
3. Inject overlay, then `__kiro.unlock()` so user can interact

### Step 2: Open Annotation Mode
1. `browser_annotate` — this opens Playwright's annotation UI
2. The user draws a rectangle around the component they want
3. Playwright returns the annotated screenshot and the elements within the selection

### Step 3: Extract from Selection
Use the returned annotation data to identify the target element, then run the extraction script from Workflow 1.

### Step 4: User Adds a Prompt
Ask the user: "I've captured that component. How do you want me to build it? For example:
- 'Make it dark mode with my brand colors'
- 'Convert to React with Tailwind'
- 'Keep the layout but change the content to...'
- 'Make it responsive, the original isn't'"

### Step 5: Build with Modifications
Build the component incorporating the user's prompt. This is where the AI shines — not just copying, but adapting.

## Workflow 3: Full Page Steal

When the user says "I want a landing page like [site]":

### Step 1: Full Page Analysis
1. Navigate to the site
2. Take a full-page screenshot: `browser_take_screenshot` with `fullPage: true`
3. `browser_snapshot` for full structure
4. Scroll through the page, taking screenshots of each section

### Step 2: Break Down Sections
Identify all major sections:
- Header/Navbar
- Hero section
- Features section
- Testimonials
- Pricing
- Footer
- etc.

### Step 3: Extract Each Section
For each section, run the extraction script. Build a complete picture of:
- Overall color palette
- Typography system
- Spacing system
- Component patterns

### Step 4: Build Section by Section
Ask the user which sections they want, then build each one:
1. Build the section
2. Verify visually
3. Move to the next
4. Final full-page comparison

## Extraction JavaScript Snippets

### Get Full Color Palette from a Page
```javascript
() => {
  const colors = new Set();
  document.querySelectorAll('*').forEach(el => {
    const s = getComputedStyle(el);
    [s.color, s.backgroundColor, s.borderColor].forEach(c => {
      if (c && c !== 'rgba(0, 0, 0, 0)' && c !== 'transparent') colors.add(c);
    });
  });
  return JSON.stringify([...colors].sort(), null, 2);
}
```

### Get Typography System
```javascript
() => {
  const fonts = new Map();
  document.querySelectorAll('*').forEach(el => {
    const s = getComputedStyle(el);
    const key = s.fontSize + '|' + s.fontWeight + '|' + s.fontFamily.split(',')[0].trim();
    if (!fonts.has(key)) {
      fonts.set(key, {
        fontSize: s.fontSize, fontWeight: s.fontWeight,
        fontFamily: s.fontFamily.split(',')[0].trim(),
        lineHeight: s.lineHeight, letterSpacing: s.letterSpacing,
        example: el.textContent.trim().slice(0, 50),
        tag: el.tagName
      });
    }
  });
  return JSON.stringify([...fonts.values()].sort((a,b) => parseFloat(b.fontSize) - parseFloat(a.fontSize)), null, 2);
}
```

### Get Spacing System
```javascript
() => {
  const spacings = new Set();
  document.querySelectorAll('*').forEach(el => {
    const s = getComputedStyle(el);
    ['padding', 'margin', 'gap'].forEach(prop => {
      const val = s.getPropertyValue(prop);
      if (val && val !== '0px') spacings.add(prop + ': ' + val);
    });
  });
  return JSON.stringify([...spacings].sort(), null, 2);
}
```

### Extract All Images and Assets
```javascript
() => {
  const assets = {
    images: [...document.querySelectorAll('img')].map(img => ({ src: img.src, alt: img.alt, size: img.naturalWidth + 'x' + img.naturalHeight })),
    backgroundImages: [...document.querySelectorAll('*')].map(el => getComputedStyle(el).backgroundImage).filter(bg => bg !== 'none'),
    svgCount: document.querySelectorAll('svg').length,
    iconFonts: [...new Set([...document.querySelectorAll('[class*="icon"], [class*="fa-"], [class*="material-"]')].map(el => el.className))]
  };
  return JSON.stringify(assets, null, 2);
}
```

## Tips for Better Stealing

- **Always extract computed styles, not class names** — class names are meaningless without the CSS file
- **Capture SVGs inline** — they're usually icons and can be directly reused
- **Note the font stack** — suggest Google Fonts alternatives if the original uses custom fonts
- **Check for animations** — hover states, transitions, scroll animations
- **Respect copyright** — remind the user this is for inspiration/learning, not wholesale copying of branded content
- **Adapt, don't copy** — the goal is to understand the design patterns and recreate them, not to clone pixel-for-pixel
