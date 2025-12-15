# Conference Timer

A browser-based countdown timer for conferences / events with OBS integration.

<img width="1038" height="1484" alt="control panel" src="https://github.com/user-attachments/assets/4570037f-d598-4906-87cf-e4857ca5b3fc" />


## Features

- Countdown timer with customizable duration
- Clock mode (displays current time)
- Custom messages displayed below the timer
- Visual warnings when time is running low
- "Game Over" overlay effect
- Flash/attention animation
- OBS WebSocket integration for source control

## Files

- `countdown.html` - Timer display (add as OBS browser source)
- `control.html` - Control panel (use as OBS dock or separate window)

## Setup with OBS

### 1. Add the Timer Display as a Browser Source

1. In OBS, add a new **Browser** source to your scene
2. Check "Local file" and browse to `countdown.html`
3. Set dimensions (e.g., 1920x1080)
4. Recommended: Set background to transparent

### 2. Add the Control Panel as an OBS Dock

1. In OBS, go to **Docks** > **Custom Browser Docks...**
2. Add a new dock:
   - **Dock Name:** Timer Control
   - **URL:** Full path to `control.html` (e.g., `file:///C:/path/to/control.html`)
3. Click **Apply**
4. Position the dock in your OBS layout

### 3. Connect OBS WebSocket (Optional)

To control OBS sources directly from the timer panel:

1. Ensure **OBS WebSocket** is enabled (Tools > WebSocket Server Settings)
2. In the control panel, expand "OBS Controls"
3. Enter your host (`localhost`), port (`4455`), and password if set
4. Click **Connect**

## URL Parameters for Display

Customize `countdown.html` with URL parameters:

| Parameter | Default | Description |
|-----------|---------|-------------|
| `duration` | `600` | Initial duration in seconds or `mm:ss` format |
| `mode` | `countdown` | `countdown` or `clock` |
| `fontSize` | `25vw` | Timer font size |
| `color` | `#ffffff` | Default text color |
| `warningColor` | `#ff9800` | Color when below warning threshold |
| `dangerColor` | `#f44336` | Color when below danger threshold |
| `bg` | `transparent` | Background color |
| `warningTime` | `60` | Seconds remaining to trigger warning |
| `dangerTime` | `30` | Seconds remaining to trigger danger |
| `label` | (empty) | Text label above timer |
| `hideControls` | `false` | Hide on-screen controls |
| `countUp` | `false` | Count up instead of down |

**Example:**
```
countdown.html?duration=15:00&color=%2300ff00&hideControls=true
```

## Control Panel Features

- **Main Controls:** Start, Pause, Stop, Reset
- **Adjust Time:** Add or subtract minutes on the fly
- **Quick Presets:** 5, 10, 15, 20, 30, 60 minute presets
- **Custom Duration:** Enter any duration in `mm:ss` or seconds
- **Custom Message:** Display text below the timer
- **Flash Timer:** Grab attention with a flash animation
- **Clock Mode:** Switch to displaying current time
- **Game Over:** Show a dramatic "GAME OVER" overlay
- **OBS Controls:** Toggle source visibility, switch scenes

## How It Works

The control panel and display communicate via the browser's BroadcastChannel API. Both pages must be open in the same browser context (OBS counts as one context when using browser sources and docks).
