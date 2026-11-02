# Privacy & Security

> **KiwiBot will eventually be privacy- and security-hardened, but growth comes first for now (0014).** Nothing on this page is in force yet. It describes the **target state** that hardening will work towards. The early baseline, meaning the cheap protections worth having from the start, is deferred: [D34–D36](decisions/deferred.md).
>
> Safeguards in the meantime: human review and approval (0021, 0025), a private repository (0006) and small, reviewable changes (0017). None of these is a security measure in itself.

## Target principles

1. **Local by default.** Audio, transcripts and memory stay on the host (consistent with local-first day-to-day operation, 0005).
2. **Cloud is explicit.** Every cloud call can be traced to a routing rule or a request, and is logged (routing D08, logging D11). Building already uses frontier models (0005).
3. **Least privilege.** Each service and token gets only the access it needs.
4. **No inbound exposure.** Nothing is port-forwarded to the internet.

## Data inventory (draft)

| Data | Where stored | Retention | Leaves the house? |
|------|--------------|-----------|-------------------|
| Raw audio | Memory only (not persisted) | Discarded after STT | Never |
| Transcripts / conversations | Local DB | Configurable (`memory.retention_days`) | Only the current request, when routed to cloud |
| Long-term memory | Local DB | Until deleted | Only non-`private` items, when relevant and routed to cloud |
| Cloud call log | Local | TODO | No |

## Secrets

Part of the deferred baseline (D34). Already followed in practice: secrets stay out of git.


- API keys and tokens live in `.env` (or an OS secret store), never in git.
- `.gitignore` must include `.env`, local config files, `data/` and model files.
- Rotate keys if the host is compromised or the repo is ever made public.

## Network (deferred, D35)

- Services bind to the LAN or localhost only.
- Remote access is through a VPN only.
- **TODO:** Consider isolating IoT devices on their own VLAN.

## Physical-world safety (deferred, D27)

- Confirmation is required for locks, garage doors, alarm arm/disarm and anything safety-related.
- **TODO:** Voice identification or a PIN for sensitive actions.

## Kill switches (deferred, D36)

- A `local_only` switch blocks all cloud calls (draft; routing is deferred, D08).
- **TODO:** Mute or privacy button on satellites.
