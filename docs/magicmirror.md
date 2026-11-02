# MagicMirror Interface

One of KiwiBot's interfaces (0008) is a [MagicMirror²](https://magicmirror.builders/) instance running on a converted Lululemon Mirror. See [decision 0009](decisions/0009-magicmirror-on-converted-lululemon-mirror.md) for the reasoning. Whether it's the *primary* interface is deferred (D31).

The mirror is where the original name **Lulu** came from. "Lulu" may remain the mirror's interface name or a wake word (0003), so the module keeps the working name `MMM-Lulu`.

## Hardware: converting the Lululemon Mirror

The conversion follows the community project by **olm3ca**:

- 📘 **Main repo:** <https://github.com/olm3ca/mirror>
- 🔧 **BOE 43" board-swap guide (driver board + HDMI):** <https://github.com/olm3ca/mirror/issues/38>

Summary of the approach (read the originals before starting):

1. **Identify the panel.** BOE DV430FHM-NN5 (43") is the best-documented. Samsung LM40 panels are mostly solved, while LTI400HN01 is reported as difficult.
2. **Factory-reset the Mirror** before opening it (avoids backlight timeout issues).
3. **Tear down:** Remove the back plate and disconnect the LVDS, ethernet, and audio connections. The top scaler board (with camera) is removed.
4. **Install an LCD driver board** (eBay, plug-and-play with the Mirror's connections). This gives the panel an **HDMI input**.
5. **Reconnect the speakers** via JST 2.0 mm 4-pin headers (wire order per the guide: orange, black, blue, red).
6. **Power the SBC** from the Mirror's 12/24 V supply using a **buck converter** down to 5 V. Size it for the SBC, since a Pi 5 needs 5 A.
7. **Mount HDMI/USB-C pass-throughs** and modify the back plate. Use plastic standoffs so nothing metal touches the boards.

> ⚠️ This is irreversible. Take photos of every connector before unplugging anything.

### KiwiBot build notes (deferred, D30)

| Item | Plan |
|------|------|
| SBC | **TODO** (e.g. Raspberry Pi 5, or an x86 mini PC if the avatar needs more GPU) |
| Display | 1080×1920 portrait via HDMI from the SBC |
| Microphone | **TODO**: USB mic array (the conversion provides none) |
| Camera (optional) | **TODO**: USB camera, since the original is not reusable |
| Audio out | Mirror speakers via the driver board, or routed to the SBC/amp |
| Network | Wired Ethernet preferred (reuse the old ethernet cut-out), otherwise Wi-Fi |

## Software

- **MagicMirror²** runs on the SBC in kiosk mode, rotated to portrait.
- Standard modules (clock, weather, calendar) cover the basics.
- **`MMM-Lulu`** is the custom module that connects the mirror to KiwiBot.

### `MMM-Lulu` module (planned)

```
KiwiBot    ◀──── WebSocket ────▶  MMM-Lulu node_helper  ──▶  MMM-Lulu front-end (Electron)
 (main host)     events / commands       (on SBC)                 avatar + content panels
```

KiwiBot pushes **display events**, and the module renders them:

| Event | Purpose |
|-------|---------|
| `state` | Avatar state: `idle`, `listening`, `thinking`, `speaking` |
| `speech` | Text being spoken plus timing/viseme data for lip-sync |
| `show` | Display content (see below) |
| `clear` | Dismiss content |
| `notify` | Toast-style alerts (timer done, doorbell…) |

The mirror can also send events back: touch/gesture input (if added), presence detection, and "screen is showing X" context so the model can refer to what is on screen.

## Planned extensions

### 1. Visual avatar
A visible presence for KiwiBot that reacts to the conversation.
- Its states (idle, listening, thinking, speaking) are driven by Core events.
- Lip-sync uses TTS phoneme/viseme timing, or audio amplitude as a fallback.
- **Rendering options (deferred, D32):**
  - A 2D animated sprite or Lottie (lightest)
  - A Live2D character
  - A 3D VRM model via three.js / three-vrm (richest, heaviest on the SBC)
- Use bright elements on black so it appears to "float" in the mirror.

### 2. Display of requested materials
Let KiwiBot answer visually ("show me…").
- Recipes, documents and notes
- Images and web search results
- Calendar, to-dos and shopping list
- Camera feeds (doorbell, rooms) through the home-automation hub
- Timers and countdowns, maps, weather detail
- Rich model output: tables, charts, step-by-step instructions

This could be exposed to the model as a `display.show` skill (candidate; see [skills.md](skills.md)).

### 3. Other ideas
- Presence detection (camera or mmWave) to wake the display or greet someone
- Gesture or touch control
- A workout/fitness mode (fitting, given the hardware)
- Photo frame / ambient mode when idle
- Per-person views if speaker identification is added
