# CUJ Screenshots Extension

You have access to the CUJ (Critical User Journey) screenshots skill. Use it to capture visual documentation of web app user journeys.

## When to Use This

**Always run CUJ captures after UI changes.** This is part of the dev loop, not just documentation.

### Triggered By:
- Any frontend component change
- CSS/styling updates
- New features that affect user flow
- Bug fixes that change visible behavior
- Before sharing work with humans ("here's what it looks like now")

### The Loop:
```
Make UI change → Run CUJs → Review screenshots → 
  ├─ Looks good? → Update GIFs, commit, share link
  └─ Looks wrong? → Fix bug, repeat
```

## How to Capture CUJs

Run the capture script:
```bash
uv run --with playwright python scripts/capture-cujs.py
```

Or create custom captures using Playwright:
```python
import asyncio
from playwright.async_api import async_playwright

async def capture():
    async with async_playwright() as p:
        browser = await p.chromium.launch(headless=True)
        context = await browser.new_context(
            viewport={"width": 390, "height": 844},
            device_scale_factor=2
        )
        page = await context.new_page()
        await page.goto("http://localhost:5173")
        await page.screenshot(path="screenshot.png")
        await browser.close()

asyncio.run(capture())
```

## Create GIFs

After capturing screenshots, stitch them into a GIF:
```bash
convert -delay 150 -loop 0 /tmp/cuj-screenshots/*.png output.gif
```

## Prerequisites

Before running, ensure:
- Python 3.10+
- Playwright: `pip install playwright && playwright install chromium`
- ImageMagick: `brew install imagemagick` (macOS) or `apt install imagemagick` (Linux)
- Frontend running on localhost:5173
- Backend running on localhost:8000 (if needed)

## Output

Update `docs/CUJs.md` with embedded GIFs:

```markdown
## CUJ 1: App Tour

**Goal:** Navigate the main app layout.

**Steps:**
1. Open app
2. Click through tabs
3. Return to start

![App Tour](./gifs/cuj1-app-tour.gif)
```
