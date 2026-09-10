# Wireless, Mobile & Linux Security Lab

> Portfolio write-up derived from the original 38-page university lab report provided by Smail Mersad. The original report contains screenshots and packet/tool output; this GitHub edition uses only results from that report and does not invent additional assets.

**Academic context:** Amar Telidji University, Computer Science / Cybersecurity Engineering, 2025-2026.

## Scope

This multi-part lab covers Wi-Fi reconnaissance and attacks, WPA/WPA2 handshake analysis, rogue access points, Bluetooth traffic analysis, Android application reverse engineering and configuration review, mobile traffic interception, and Linux hardening.

## 1. Wi-Fi reconnaissance with airodump-ng

A WPA2-PSK network capture was analyzed to identify the SSID, BSSID, channel, cipher/authentication mode, and management traffic. The exercise demonstrates that management frames expose useful network metadata even when user data is encrypted.

Mitigation discussion included strong WPA2/WPA3 passphrases, disabling WPS, and monitoring abnormal wireless activity.

## 2. 802.11 management/data frame analysis

Wireshark filters were used to inspect several 802.11 frame types and their security implications:

- Beacon frames — network discovery and metadata exposure.
- Probe requests — possible client-history/tracking information.
- Probe responses — rogue AP / Evil Twin opportunity.
- Authentication/association traffic — connection-state exposure and resource-abuse considerations.
- Encrypted data frames — confidentiality depends on key strength.

The report also analyzes classic Bluetooth capture data, distinguishing it from BLE ATT traffic and discussing legacy PIN pairing and exposed link-key risks.

## 3. WPA2 four-way handshake

EAPOL handshake messages were decoded with Wireshark/tshark. The report identifies ANonce, SNonce, MIC, and key-information fields and explains the role of Messages 1–4.

The important security point is that the PSK is not transmitted directly, but captured handshake material enables **offline password guessing** when the passphrase is weak.

## 4. Offline WPA/WPA2 dictionary attacks

Aircrack-ng was used against provided capture files containing valid handshakes with `rockyou.txt`. Weak dictionary-based test passphrases were recovered, illustrating that practical WPA/WPA2-PSK security depends strongly on passphrase entropy.

The report recommends long random passphrases, disabling WPS, monitoring deauthentication abuse, and preferring WPA3-SAE where supported.

## 5. Rogue AP / Evil Twin defense

`mac80211_hwsim` was used to simulate a legitimate AP and a rogue AP advertising the same `CorpLab` SSID with different BSSIDs. Kismet detected both APs.

The client was configured through `wpa_supplicant` to connect only to the known legitimate BSSID, showing one way to prevent the test client from associating with the rogue AP. The report also recommends WPA2/WPA3-Enterprise with certificate validation for stronger AP authentication.

## 6. Android APK reverse engineering with JADX

A deliberately vulnerable banking APK was decompiled with JADX. The analysis found backend configuration values in application resources, including cloud/Firebase identifiers, and examined session data stored through `SharedPreferences` plus client-side cryptographic logic.

The report's key finding is architectural: values shipped inside an APK cannot be treated as secrets because client applications can be reverse engineered. Sensitive authorization and validation should be enforced server-side, API keys should be restricted, and sensitive local data should use Android's protected storage/Keystore mechanisms.

## 7. Mobile HTTPS interception test with Mitmproxy

A physical Android phone was configured to use a Kali VM running `mitmweb` as its Wi-Fi proxy. Normal browser traffic appeared in Mitmproxy, proving the proxy path worked.

The target DVBA application's traffic did **not** appear in Mitmproxy and the login attempt failed. The report correctly avoids claiming a successful application MITM. It records possible explanations such as certificate rejection, strict TLS validation, proxy bypass, or the request failing before transmission.

This unsuccessful result is preserved because it is still meaningful experimental evidence: the lab confirmed the interception environment while distinguishing what was and was not demonstrated against the application.

## 8. AndroidManifest security review with apktool

A password-manager APK's `AndroidManifest.xml` was decoded and reviewed. Findings included:

- unnecessary/high-risk permission exposure;
- `allowBackup="true"`;
- `debuggable="true"`;
- custom permissions weaker than signature-level protection;
- an exported password-list activity;
- an exported file/content provider.

The report discusses how exported sensitive components can allow other applications to interact with internal functionality through Android IPC, and recommends non-exported components by default, internal authentication/authorization checks, production-safe backup/debug settings, and least-privilege permissions.

## 9. Linux file protection with chattr

`chattr` and `lsattr` were used to demonstrate special file attributes beyond normal `chmod` permissions:

- `+i` / `-i` for immutable files;
- `+a` / `-a` for append-only files.

The exercise relates these controls to protecting critical configuration and log files against modification, deletion, and tampering.

## 10. Linux capabilities and least privilege

`getcap` and `setcap` were used with the `ping` binary. `CAP_NET_RAW` was assigned so a normal user could create the raw network packets required for ICMP without granting the entire program full root privilege.

This demonstrates the security advantage of decomposing privilege into narrow Linux capabilities instead of relying on all-or-nothing SUID-root execution.

## Tools & technologies

`Wireshark` · `aircrack-ng` · `airodump-ng` · `tshark` · `Kismet` · `mac80211_hwsim` · `wpa_supplicant` · `JADX` · `apktool` · `Mitmproxy` · Android · `chattr` · `lsattr` · `getcap` · `setcap`

## Takeaway

The lab demonstrates security across several layers: wireless metadata and authentication, password strength, rogue infrastructure, Bluetooth pairing, mobile application reverse engineering, TLS behavior, Android component exposure, and Linux least privilege. It also preserves negative test results instead of overstating them, which is important in real security analysis.
