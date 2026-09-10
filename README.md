# Wireless, Mobile & Linux Security Labs

A broad security lab covering wireless reconnaissance, WPA/WPA2 attacks, Bluetooth analysis, Android reverse engineering, traffic interception, and Linux privilege hardening.

> **Academic context:** Completed as part of Computer Science / Cybersecurity engineering coursework at Amar Telidji University, Laghouat (2025-2026). This repository is intended as a technical portfolio of controlled university lab work.

## What this repository demonstrates

- Analyzed Wi-Fi management/data traffic and WPA/WPA2 handshake risks, including offline dictionary-attack scenarios.
- Investigated rogue access point / Evil Twin concepts and Bluetooth security artifacts.
- Reverse engineered Android APKs to inspect resources, hardcoded backend data, local token storage, permissions, and exported components.
- Tested mobile HTTPS interception behavior and reviewed certificate-validation/pinning implications.
- Applied Linux hardening with file attributes and fine-grained capabilities as an alternative to broad SUID privileges.

## Tools & technologies

`Wireshark` · `aircrack-ng` · `airodump-ng` · `tshark` · `JADX` · `apktool` · `Mitmproxy` · `Android` · `Linux capabilities` · `chattr` · `getcap` · `setcap`

## Included lab reports

| # | Lab | Report |
|---:|---|---|
| 1 | Wireless Mobile Linux Security | [`docs/wireless-mobile-linux-security.md`](docs/wireless-mobile-linux-security.md) |

## Repository structure

```text
.
├── README.md
├── docs/        # GitHub text editions of the academic lab reports
└── src/         # Add original code/configs/scripts here when available
```

## Notes

The reports document the work actually completed in the university labs. For GitHub portability, the reports are included as searchable Markdown text editions; the original PDF screenshots and figures are not embedded in these conversions. The `src/` directory is intentionally left as a place to add original source code, configuration files, packet captures, notebooks, or scripts where those artifacts are available. No source code has been fabricated from the reports.

## Responsible use

Security techniques in this repository were performed in controlled academic environments. Use attack and exploitation techniques only on systems you own or have explicit authorization to test.
