# ⏱ Budibase Stopwatch Plugin (Svelte)

Stopwatch plugin for Budibase built with **Svelte 5**.

## Features
- HH:MM:SS display
- Start / Pause / Stop
- Pause button blinks
- Emits:
  - startTime
  - elapsedSeconds
  - elapsedMinutes

## Installation
⚠️ Self-hosted Budibase only

1. Download the latest release ZIP
2. Budibase → Settings → Plugins → Upload
3. Upload ZIP
4. Add Stopwatch component to a screen

## Development
npm install
npm run dev
npm run build

## Accessibility

This plugin follows Budibase accessibility best practices:

- All interactive elements are native `<button>` elements
- Buttons have visible text labels (Start, Pause, Stop)
- Pause state is visually indicated via animation
- Color is not the only indicator of state
- Keyboard navigation is supported
- Screen readers correctly announce button labels

No custom keyboard shortcuts are used.

## Changelog

### v1.1.0
- Added configurable plugin settings
- Added auto-start option
- Added display format selector
- Added pause-state emission option
- Marketplace schema alignment

### v1.0.0
- Initial release
- Start / Pause / Stop controls
- HH:MM:SS display
- Emits elapsed minutes and seconds
