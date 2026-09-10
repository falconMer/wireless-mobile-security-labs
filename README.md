# Wireless, Mobile & Linux Security Labs

A broad security lab covering wireless reconnaissance, WPA/WPA2 attacks, Bluetooth analysis, Android reverse engineering, traffic interception, and Linux privilege hardening.

> **Academic context:** Computer Science / Cybersecurity engineering coursework at Amar Telidji University, Laghouat (2025-2026).

## What this repository demonstrates

- Analyzed Wi-Fi management/data traffic and WPA/WPA2 four-way handshakes.
- Demonstrated offline dictionary-attack risk against weak PSKs using provided captures.
- Built/detected a simulated rogue AP / Evil Twin environment with Kismet.
- Investigated classic Bluetooth security artifacts and legacy pairing risks.
- Reverse engineered Android APKs with JADX and apktool to inspect embedded configuration, local token storage, permissions, debug/backup settings, and exported components.
- Tested mobile HTTPS interception with Mitmproxy and preserved the result that the target app itself was **not** successfully intercepted in that setup.
- Applied Linux file attributes and fine-grained capabilities as hardening/least-privilege controls.

## Tools & technologies

`Wireshark` · `aircrack-ng` · `airodump-ng` · `tshark` · `Kismet` · `JADX` · `apktool` · `Mitmproxy` · `Android` · `chattr` · `getcap` · `setcap`

## Included academic work

| Lab | Portfolio write-up | Original PDF |
|---|---|---|
| Wireless, Mobile & Linux Security | [`docs/wireless-mobile-linux-security.md`](docs/wireless-mobile-linux-security.md) | [PDF report](docs/wireless-mobile-linux-security.pdf) |

## Repository structure

```text
.
├── README.md
└── docs/
    ├── *.md   # GitHub-friendly lab write-ups
    └── *.pdf  # Original lab reports (privacy-redacted where noted)
```

The Markdown write-ups and supplied PDF reports form the complete available portfolio evidence. Screenshots, diagrams, and tool output are preserved inside the reports; standalone source code, captures, notebooks, and other artifacts are included only if supplied.

## Evidence policy

Privacy note: the hardcoded Google API key in the page 23 extracted-information table has been redacted. Its location, purpose, and security implications remain documented.

This repository uses only the supplied 38-page academic report and the evidence documented inside it. No additional wireless captures, APKs, screenshots, proxy traces, or source files are claimed. Failed or inconclusive tests are preserved as such instead of being rewritten as successful demonstrations.

## Responsible use

All security testing described here was performed in controlled academic environments or against deliberately vulnerable training artifacts.