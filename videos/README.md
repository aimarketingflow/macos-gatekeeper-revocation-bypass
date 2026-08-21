# Video Materials

## YouTube Presentation

**Full video:** https://youtu.be/4MXjfBAxc9I

The video includes a conference-style presentation of the research findings, covering:

1. Background on macOS Gatekeeper and OCSP revocation checking
2. The three-channel blindness attack concept (NTP, DNS, OCSP)
3. Side-by-side comparison: bypass attack vs. control (blocked) behavior
4. Walkthrough of the Campaign 6.0 bypass attack
5. Demonstration of normal Gatekeeper behavior on a healthy Mac
6. Analysis of Apple's ticket responses and source code findings

## Raw Video Files

The following raw video files were recorded during testing. They are too large for this GitHub repository but are referenced here for completeness. High-resolution source files are available on request or via external storage.

| File | Description | Size |
|------|-------------|------|
| `VIDEO_0_side_by_side_comparison.mov` | Side-by-side comparison of the bypass attack and the control (blocked) behavior on the same DMG file | ~124 MB |
| `VIDEO_1_bypass_attack_072826.mp4` | Campaign 6.0 bypass attack recording: revoked-certificate app launches after DNS poisoning of OCSP responder | ~16 MB |
| `VIDEO_2_control_normal_behavior.mov` | Control recording on a healthy Mac: same DMG file is blocked by Gatekeeper with "Malware Blocked" dialog | ~30 MB |

All three videos show the same DMG file (`chatgpt-1-2026-041.dmg`) signed with the same revoked Developer ID certificate (serial `68A68AF8A434EE4FDE46F8680B23BDCC`, team `2DC432GLL2`).

The difference in outcome (launched vs. blocked) is determined solely by whether the Mac can reach `ocsp.apple.com` — demonstrating the Gatekeeper revocation bypass.
