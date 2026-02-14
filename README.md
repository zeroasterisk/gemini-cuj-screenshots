# CUJ Screenshots - Gemini CLI Extension

Capture Critical User Journey (CUJ) screenshots and GIFs from web apps using headless Chromium.

## Installation

```bash
gemini extensions install https://github.com/zeroasterisk/gemini-cuj-screenshots
```

Or for local development:
```bash
git clone https://github.com/zeroasterisk/gemini-cuj-screenshots
cd gemini-cuj-screenshots
gemini extensions link .
```

## What It Does

1. Launches headless Chromium via Playwright
2. Navigates through defined user journeys
3. Captures screenshots at each step
4. Stitches screenshots into animated GIFs
5. Outputs to docs folder for commit

## Prerequisites

- **Python 3.10+**
- **Playwright**: `pip install playwright && playwright install chromium`
- **ImageMagick**: For GIF creation
  - macOS: `brew install imagemagick`
  - Ubuntu: `sudo apt install imagemagick`
  - Fedora: `sudo dnf install ImageMagick`

## Usage

After installing the extension, Gemini CLI will automatically use this skill when you:
- Make UI changes and want to verify them visually
- Need to create demo GIFs
- Want to document user flows

Just ask Gemini to "capture the CUJ" or "take screenshots of the app tour."

## Manual Capture

Run the included script:
```bash
uv run --with playwright python skills/cuj-screenshots/scripts/capture-cujs.py
```

## The Dev Loop

```
Make UI change → Run CUJs → Review screenshots → 
  ├─ Looks good? → Update GIFs, commit, share link
  └─ Looks wrong? → Fix bug, repeat
```

## Files

- `gemini-extension.json` - Extension manifest
- `GEMINI.md` - Context provided to Gemini in every session
- `skills/cuj-screenshots/SKILL.md` - Detailed skill documentation
- `skills/cuj-screenshots/scripts/capture-cujs.py` - Capture script with prerequisite checks

## Also Available As

- **npx skills**: `npx skills add zeroasterisk/zaf --skill cuj-screenshots`
- **Gist**: https://gist.github.com/zeroasterisk/3a4a53e02a251cb312256c0c9a5e8c9a

## License

Apache 2.0
