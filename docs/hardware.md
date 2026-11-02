# Hardware

## Main host

The host runs KiwiBot's local parts. Which parts those are depends on deferred decisions (D08–D10, D19). Host hardware itself is deferred (D28).

| Item | Current | Notes |
|------|---------|-------|
| CPU | TODO | |
| RAM | TODO | 32 GB+ recommended for 7–14B models alongside other services |
| GPU / accelerator | TODO | VRAM is the main constraint on local model size |
| Storage | TODO | SSD; models are typically 4–40 GB each |
| OS | TODO | |

### Rough VRAM guide (quantized, ~4-bit)

| Model size | Approx. VRAM |
|------------|--------------|
| 3–4B | 3–4 GB |
| 7–8B | 5–6 GB |
| 13–14B | 9–10 GB |
| 30–34B | 20–24 GB |
| 70B | 40+ GB |

These figures are approximate. Leave headroom for STT/TTS and context length.

## Mirror display: converted Lululemon Mirror

See [magicmirror.md](magicmirror.md) and [decision 0009](decisions/0009-magicmirror-on-converted-lululemon-mirror.md). Conversion process: [olm3ca/mirror](https://github.com/olm3ca/mirror). Build choices are deferred (D30).

| Item | Current | Notes |
|------|---------|-------|
| Mirror panel | TODO | BOE DV430FHM-NN5 (43") best documented |
| LCD driver board | TODO | eBay plug-and-play board, provides HDMI in |
| SBC | TODO | Runs MagicMirror² and the avatar |
| Buck converter | TODO | 12/24 V → 5 V, rated for the SBC |
| Mic | TODO | Required, since the conversion has none |
| Camera | TODO (optional) | The original camera is not reusable |

## Voice satellites

Deferred (D29).

| Room | Device | Mic | Speaker | Status |
|------|--------|-----|---------|--------|
| TODO | | | | |

Candidate options: Raspberry Pi with a mic HAT, ESP32-S3 voice kits, or reused tablets/phones.

## Network

- The host should have a static LAN IP or DHCP reservation.
- Satellites should be on the same LAN/VLAN as the host (or with routed access).
- Remote access is deferred (D35). The earlier draft used a VPN (e.g. WireGuard or Tailscale) rather than open ports. See [privacy-security.md](privacy-security.md).

## Power & reliability

Deferred (D33).

- **TODO:** UPS?
- **TODO:** Behaviour when the host is down. Should satellites give an audible error?
