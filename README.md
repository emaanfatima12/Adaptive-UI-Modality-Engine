# Adaptive UI Modality Engine

A single-page web app that detects how you are interacting with it (mouse, touch, keyboard or pen) and reshapes its interface to suit that input method. Built as Lab 3 of a multimodal interaction course.

## What it does

The page watches your input and switches between four modalities. Each one changes target sizes, spacing, focus styling and hints.

| Modality | Detected by | Adaptation |
|----------|-------------|------------|
| Mouse | Mouse movement or click | Compact layout (36px targets), hover effects on |
| Touch | Finger tap | Large targets (60px), wide spacing, hover effects off |
| Keyboard | Tab, arrow keys, Enter or Space | Thick focus ring, medium targets (44px) |
| Pen | Stylus hover or press | Medium targets (48px) |

## Features

- Live readout of the active modality, with a description and a usage hint
- Adaptive demo controls: buttons, text field, switch, slider and chips
- Target-size checker that measures the real button height against the WCAG 2.2 guidance (24px minimum, 44px recommended)
- Time spent in each modality, and the number of actions made with each input
- Timestamped event log with JSON export
- Device capabilities panel (pointer type, hover support, touch points, color scheme, viewport)
- Settings: lock the layout to one modality, light and dark theme, text size from 90% to 140%, and reduced motion
- Settings are saved in the browser using `localStorage`

## How it works

- Input type is read from the `pointerType` property of Pointer Events (`mouse`, `touch` or `pen`), which is more reliable than listening for separate mouse and touch events.
- Keyboard use is detected from navigation keys (Tab, arrows, Enter, Space). Typing inside a text field is ignored.
- The detected modality is set as `data-modality` on the `<body>`. CSS custom properties (`--target`, `--gap`, `--accent`, `--ring-width`) are redefined for each modality, so the layout adapts without JavaScript touching individual elements.
- Focus rings use `:focus-visible`, so they appear for keyboard users and not on every mouse click.

## How to run

No installation or build step is needed.

1. Download or clone this repository.
2. Open `index.html` in a modern browser (Chrome, Edge, Firefox or Safari).

## How to test each modality

- **Mouse:** move the mouse over the page.
- **Touch:** on a touchscreen, tap the page. Without one, open Chrome DevTools, press `Ctrl+Shift+M` for device emulation, and click around.
- **Keyboard:** press `Tab` and watch the focus ring.
- **Pen:** use a stylus on a supported device.
- **Any mode without the hardware:** go to Settings, then Detection, and pick a mode to lock the layout.

## Technologies

HTML, CSS (custom properties, `color-mix`, `:focus-visible`), and vanilla JavaScript (Pointer Events, `matchMedia`, `localStorage`).
