# 0009. MagicMirror on a converted Lululemon Mirror as the primary interface

- **Status:** Accepted
- **Date:** 2026-10-27
- **Tags:** features, hardware, implementation

## Context
KiwiBot needs a primary home interface beyond voice-only satellites. A screen lets KiwiBot show a visual presence (an avatar) and display things the user asks for, such as recipes, documents, cameras, timers and calendars.

A discontinued **Lululemon (Studio) Mirror** is available. It is a 40–43" 1080p panel behind a two-way mirror, with built-in speakers and a power supply. Its original Android software is locked down and no longer useful. There is a community-documented process for gutting the original electronics and driving the panel from our own hardware:

- **Hardware conversion guide:** [olm3ca/mirror — Enhancements for the Lululemon Mirror](https://github.com/olm3ca/mirror)
- **Step-by-step board swap (BOE 43" panel, eBay LCD driver board, HDMI input):** [olm3ca/mirror issue #38](https://github.com/olm3ca/mirror/issues/38)

[MagicMirror²](https://magicmirror.builders/) is an open-source, modular smart-mirror platform (Electron/Node.js) built for this kind of two-way-mirror display.

## Options considered
1. **Voice-only satellites (no screen).** This is the simplest option, but KiwiBot can't show anything.
2. **A tablet or wall display with a custom web UI.** This is cheap, but it means building the whole UI from scratch and doesn't reuse the mirror.
3. **A software-only revival of the original Mirror board** (e.g. [TimStewartJ/lululemon-mirror-repurpose](https://github.com/TimStewartJ/lululemon-mirror-repurpose)). There's no hardware surgery, but we'd be stuck on the original locked-down Android hardware, with no MagicMirror and limited compute.
4. **Converted Mirror with an LCD driver board and our own SBC running MagicMirror².** This reuses the panel, speakers and power supply, gives full control of the software and benefits from MagicMirror's module ecosystem.

## Decision
Option 4. Convert the Lululemon Mirror following the olm3ca process. That means replacing the original mainboard path with an LCD driver board that gives the panel an HDMI input, then driving it with our own single-board computer (SBC) running MagicMirror². KiwiBot integrates with MagicMirror through a custom module (working name `MMM-Lulu`). See [magicmirror.md](../magicmirror.md).

## Related decisions
- Depends on: 0008
- Affects: 0003 (the name comes from the mirror)

## Consequences
- **Irreversible hardware modification.** The olm3ca guide warns the conversion "could cause irreversible damage". Factory-reset the Mirror before starting, and photograph every connector.
- **The camera is lost.** The original camera uses MIPI CSI and is discarded with the scaler board. If KiwiBot needs vision (presence detection, gestures), we'll add a USB camera.
- **A separate microphone is needed.** The conversion doesn't cover a mic, so the Mirror needs its own mic (USB mic array or a satellite).
- **Speakers can be reused** through the driver board's speaker output (JST 2.0 mm 4-pin), or rerouted to the SBC or an amp if KiwiBot's TTS should play from the Mirror.
- **Power:** The SBC can be powered from the Mirror's 12/24 V supply through a buck converter, sized for the SBC (a Raspberry Pi 5 needs 5 V / 5 A, more than the 3 A in the guide).
- **Portrait orientation:** The panel is mounted portrait, so MagicMirror and the avatar layout must be designed for a tall 1080×1920 canvas.
- **Black is a mirror:** On a two-way mirror, black pixels look reflective, so UI and avatar designs should use a black background with bright elements.
- **Split compute:** The SBC only renders the display. STT, the LLM and TTS stay on the main KiwiBot host ([hardware.md](../hardware.md)), unless we decide otherwise later.
- The display layer is now a first-class component in [architecture.md](../architecture.md), and future extensions (avatar, content display) build on `MMM-Lulu`.
