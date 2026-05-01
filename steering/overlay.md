# Kiro Overlay — Visual Effects & Interaction Blocker

Since Kiro Powers cannot include `.js` files, the overlay must be injected at runtime via `browser_javascript_execute` after every `browser_navigate`.

## When to Inject

**Inject the overlay immediately after every `browser_navigate` call**, before doing anything else on the page. The pattern is:

1. `browser_navigate` → URL
2. `browser_wait` → 1 second (let page load)
3. `browser_javascript_execute` → inject the overlay (copy the full script below)
4. Continue with your task

**Also re-inject after:**
- Any full page reload
- Navigating to a new URL
- After `browser_go_back` or `browser_go_forward`

You do NOT need to re-inject after:
- `browser_click` (same page)
- `browser_type` (same page)
- `browser_scroll` (same page)
- SPA client-side navigation (the script persists in the same document)

## The Overlay Script

Copy this entire block and pass it as the argument to `browser_javascript_execute` after each navigation:

```javascript
(function(){if(window.__kiroOverlayInjected)return;window.__kiroOverlayInjected=true;var b=document.createElement('div');b.id='__kiro-blocker';b.style.cssText='position:fixed;top:0;left:0;width:100vw;height:100vh;z-index:2147483646;cursor:not-allowed;background:transparent;pointer-events:auto;';var blockKey=function(e){if(e.key==='F12'||(e.ctrlKey&&e.shiftKey&&e.key==='I'))return;e.stopPropagation();e.preventDefault();};var badge=document.createElement('div');badge.id='__kiro-badge';badge.innerHTML='<div style="position:fixed;bottom:16px;right:16px;z-index:2147483647;display:flex;align-items:center;gap:8px;background:rgba(15,23,42,0.92);backdrop-filter:blur(12px);-webkit-backdrop-filter:blur(12px);color:#f1f5f9;font-family:-apple-system,BlinkMacSystemFont,Segoe UI,Roboto,sans-serif;font-size:13px;font-weight:500;padding:10px 16px;border-radius:12px;box-shadow:0 4px 24px rgba(0,0,0,0.25),0 0 0 1px rgba(255,255,255,0.08);pointer-events:none;user-select:none;line-height:1;"><span id=__kiro-dot style="display:inline-block;width:8px;height:8px;border-radius:50%;background:#22d3ee;box-shadow:0 0 8px rgba(34,211,238,0.6);animation:__kiroPulse 2s ease-in-out infinite;"></span><span id=__kiro-text>Kiro is driving</span><span id=__kiro-sub style="color:#94a3b8;font-size:11px;margin-left:2px;">— watching only</span></div>';var s=document.createElement('style');s.textContent='@keyframes __kiroPulse{0%,100%{opacity:1;box-shadow:0 0 8px rgba(34,211,238,0.6);}50%{opacity:0.4;box-shadow:0 0 4px rgba(34,211,238,0.3);}}@keyframes __kiroRipple{0%{transform:translate(-50%,-50%) scale(0.5);opacity:0.8;}100%{transform:translate(-50%,-50%) scale(2.5);opacity:0;}}.__kiro-ripple{position:fixed;width:28px;height:28px;border:2px solid rgba(34,211,238,0.7);border-radius:50%;pointer-events:none;z-index:2147483647;animation:__kiroRipple 0.6s ease-out forwards;}';var ring=document.createElement('div');ring.id='__kiro-ring';ring.style.cssText='position:fixed;width:28px;height:28px;border:2px solid rgba(34,211,238,0.5);border-radius:50%;pointer-events:none;z-index:2147483647;transition:left 0.15s ease-out,top 0.15s ease-out,opacity 0.3s ease;transform:translate(-50%,-50%);box-shadow:0 0 12px rgba(34,211,238,0.2);opacity:0;left:-100px;top:-100px;';function inject(){if(!document.body){var mo=new MutationObserver(function(){if(document.body){mo.disconnect();inject();}});mo.observe(document.documentElement,{childList:true});return;}document.head.appendChild(s);document.body.appendChild(b);document.body.appendChild(badge);document.body.appendChild(ring);document.addEventListener('keydown',blockKey,true);document.addEventListener('keyup',blockKey,true);document.addEventListener('keypress',blockKey,true);}b.addEventListener('mousemove',function(e){ring.style.left=e.clientX+'px';ring.style.top=e.clientY+'px';ring.style.opacity='1';});b.addEventListener('mousedown',function(e){var r=document.createElement('div');r.className='__kiro-ripple';r.style.left=e.clientX+'px';r.style.top=e.clientY+'px';document.body.appendChild(r);setTimeout(function(){r.remove();},600);});window.__kiro={unlock:function(){b.style.pointerEvents='none';b.style.cursor='default';document.removeEventListener('keydown',blockKey,true);document.removeEventListener('keyup',blockKey,true);document.removeEventListener('keypress',blockKey,true);document.getElementById('__kiro-sub').textContent='— user control';var d=document.getElementById('__kiro-dot');d.style.background='#4ade80';d.style.boxShadow='0 0 8px rgba(74,222,128,0.6)';},lock:function(){b.style.pointerEvents='auto';b.style.cursor='not-allowed';document.addEventListener('keydown',blockKey,true);document.addEventListener('keyup',blockKey,true);document.addEventListener('keypress',blockKey,true);document.getElementById('__kiro-sub').textContent='— watching only';var d=document.getElementById('__kiro-dot');d.style.background='#22d3ee';d.style.boxShadow='0 0 8px rgba(34,211,238,0.6)';},hide:function(){b.style.display='none';badge.style.display='none';ring.style.display='none';},show:function(){b.style.display='block';badge.style.display='block';ring.style.display='block';},status:function(m){document.getElementById('__kiro-text').textContent=m;}};if(document.readyState==='loading'){document.addEventListener('DOMContentLoaded',inject);}else{inject();}'Kiro overlay injected'})()
```

## What the Overlay Does

### Visual Elements
1. **"Kiro is driving" badge** — floating pill in bottom-right corner with pulsing cyan dot
2. **Cursor ring** — cyan circle that follows the mouse so the user sees where Kiro is looking
3. **Click ripples** — expanding ring animation on every click for visual feedback

### Interaction Blocking
- Transparent full-screen div captures all mouse events (user sees `cursor: not-allowed`)
- Keyboard events are blocked (except F12 and Ctrl+Shift+I for devtools)
- Playwright's own actions bypass this because they dispatch events at a lower level

## Control API

After injecting, you can control the overlay via `browser_javascript_execute`:

### Hide for Clean Screenshots
```javascript
window.__kiro.hide()
```
Then after capturing:
```javascript
window.__kiro.show()
```

### Show Progress Status
```javascript
window.__kiro.status('Analyzing layout...')
```
```javascript
window.__kiro.status('Fixing spacing...')
```
```javascript
window.__kiro.status('Kiro is driving')  // reset to default
```

### Give User Control
When the user needs to interact (login, select something):
```javascript
window.__kiro.unlock()
```
Badge turns green and says "user control". Mouse and keyboard are unblocked.

### Take Back Control
```javascript
window.__kiro.lock()
```
Badge turns cyan, input blocked again.

## Integration with Workflows

### Standard Navigation Pattern
Every time you navigate to a new page, follow this sequence:
1. `browser_navigate` → URL
2. `browser_wait` → 1s
3. `browser_javascript_execute` → the overlay script above
4. `browser_javascript_execute` → `window.__kiro.status('Checking page...')`
5. Continue with your task

### Screenshot Pattern
When taking screenshots for analysis:
1. `browser_javascript_execute` → `window.__kiro.hide()`
2. `browser_screen_capture`
3. `browser_javascript_execute` → `window.__kiro.show()`

### Fix-and-Verify Pattern
1. `browser_javascript_execute` → `window.__kiro.status('Fixing: [issue]...')`
2. Edit the code
3. `browser_wait` → 2s (hot reload)
4. `browser_javascript_execute` → `window.__kiro.status('Verifying fix...')`
5. `browser_javascript_execute` → `window.__kiro.hide()`
6. `browser_screen_capture`
7. `browser_javascript_execute` → `window.__kiro.show()`
8. `browser_javascript_execute` → `window.__kiro.status('Kiro is driving')`
