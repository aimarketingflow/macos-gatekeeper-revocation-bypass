# macOS Gatekeeper Revocation Bypass via Network-Layer Attacks

**Author:** Hana Omori  
**Publication Date:** August 2026  
**Apple Security Bounty Ticket:** OE1107167498810  
**CVE Request:** [UNVERIFIED — CVE Request CAN-2026-2035261 submitted to MITRE CNA-LR, August 5, 2026; MITRE record not yet in repo]  
**YouTube Video:** https://youtu.be/4MXjfBAxc9I  
**GitHub Repository:** https://github.com/aimarketingflow/macos-gatekeeper-revocation-bypass

---

## Abstract

macOS Gatekeeper is designed to block applications signed with revoked Developer ID certificates by presenting a non-bypassable "Malware Blocked" dialog. However, when the OCSP revocation responder (`ocsp.apple.com`) is unreachable — achievable via DNS poisoning from any network position — `trustd` fails open after a 3-second timeout, `syspolicyd` applies its fail-open rule (rule 11, `allow=1`), and the revoked-certificate app launches with only a standard "downloaded from the Internet" prompt. Apple's open-source `trustd` code confirms this is the designed behavior, and Apple's only mitigation is a persistent OCSP cache that pins revoked responses — but only for certificates previously queried on that specific machine. Fresh Macs, newly revoked certificates, and persistent attacker networks have zero protection. CRLite, which could provide offline revocation fallback, is built into the code but disabled via feature flag. Apple closed the bounty ticket on August 3, 2026, stating "this is not security" and "no changes will be needed," and confirmed the closure on August 5, 2026.

---

## YouTube Video

A conference-style video presentation of the findings, including side-by-side comparison of the bypass attack and the control (blocked) behavior, is available at:

**https://youtu.be/4MXjfBAxc9I**

---

## Repository Contents

```
├── README.md                  # This file
├── INDEX.html                 # Navigable index of all materials (open in browser)
├── LICENSE                    # CC BY 4.0 full text
├── CITATION.bib               # BibTeX citation entry
├── PAPER.html                 # Full technical paper (open in browser)
├── TICKET_THREAD.html         # Complete Apple ticket thread (Jul 9 – Aug 6, 2026)
├── EVIDENCE_EXCERPT.txt       # Curated log excerpts from Campaign 6.0
├── figures/                   # Publication figures (PNG)
│   ├── figure-01-three-channel-blindness.png
│   ├── figure-02-security-boundary-crossed.png
│   ├── figure-03-triple-failure-flow.png
│   ├── figure-04-cache-coverage-matrix.png
│   └── figure-05-six-year-gap-timeline.png
└── videos/
    └── README.md              # Video descriptions and YouTube link
```

---

## Responsible Disclosure Timeline

All dates are backed by the Apple ticket thread (`TICKET_THREAD.html`) and the technical paper (`PAPER.html`).

| Date | Event | Source |
|------|-------|--------|
| Jul 9, 2026 | Initial report submitted to Apple Product Security: "DNS Poisoning of OCSP/Notarization Servers Downgrades Revoked Certificate Hard Block to User-Bypassable Prompt" | `TICKET_THREAD.html`, message 1 |
| Jul 13, 2026 | Apple responds: "does not demonstrate that a security boundary is crossed without user consent" | `TICKET_THREAD.html`, message 2 |
| Jul 14, 2026 | Researcher submits rebuttal with controlled comparison video and Sequoia negative control | `TICKET_THREAD.html`, messages 3–7 |
| Jul 15, 2026 | Researcher confirms WiFi-only DNS poisoning bypass (no Thunderbolt required) | `TICKET_THREAD.html`, messages 8–10 |
| Jul 17, 2026 | Apple acknowledges: "Thanks for the additional details. I will review them with the team." | `TICKET_THREAD.html`, message 11 |
| Jul 23, 2026 | Researcher discovers Apple's OCSP responder update and submits analysis of incomplete fix | `TICKET_THREAD.html`, messages 12–13 |
| Jul 24, 2026 | Researcher corrects mechanism identification (OCSP responder, not CRLite) | `TICKET_THREAD.html`, messages 14–15 |
| Jul 28, 2026 | Apple responds: "The behavior you observed is intended" and points to open-source `trustd` code | `TICKET_THREAD.html`, message 16 |
| Jul 29, 2026 | Apple rejects Campaign 6 evidence; researcher submits point-by-point rebuttal with side-by-side log comparison | `TICKET_THREAD.html`, messages 17–19 |
| Jul 30, 2026 | Researcher submits source code analysis of `trustd` (fail-open path, disabled CRLite, cache limitations) | `TICKET_THREAD.html`, message 20 |
| Aug 3, 2026 | Apple closes ticket: "this is working as expected and that no changes will be needed. Since this is not security we will no longer be tracking this issue." | `TICKET_THREAD.html`, message 21 |
| Aug 4, 2026 | Researcher notifies Apple of intent to publish; Apple does not object | `TICKET_THREAD.html`, messages 22–23 |
| Aug 5, 2026 | Apple's final response: "those checks run and complete... We are closing this report." | `TICKET_THREAD.html`, message 25 |
| Aug 5, 2026 | CVE request submitted to MITRE CNA-LR (CAN-2026-2035261) [UNVERIFIED — no local MITRE record in repo] | MITRE submission record |
| Aug 6, 2026 | Researcher's final response noting the contradiction in Apple's position | `TICKET_THREAD.html`, messages 26–27 |

---

## No Exploit Code or Weaponized Tooling

This repository contains **no exploit code, no weaponized tooling, no attack scripts, and no payload generators**. The package includes only:

- Analysis and documentation of observed system behavior
- Curated log excerpts from system daemons (`trustd`, `syspolicyd`)
- Screenshots and video demonstrations of Gatekeeper dialogs
- Apple's open-source code references (already publicly available)
- The complete Apple ticket thread documenting the disclosure process

The research methodology uses standard macOS diagnostic tools (pf firewall rules, `log stream`, `spctl`, `codesign`) to observe and document system behavior under controlled network conditions.

---

## License

This work is licensed under [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).

See `LICENSE` for the full legal code.

---

## Citation

```bibtex
@misc{flowgirl2026gatekeeper,
  title={macOS Gatekeeper Revocation Bypass via Network-Layer Attacks},
  author={Hana Omori},
  year={2026},
  month={August},
  howpublished={YouTube video},
  url={https://youtu.be/4MXjfBAxc9I},
  note={Apple Security Bounty Ticket OE1107167498810}
}
```

See `CITATION.bib` for the BibTeX entry file.
