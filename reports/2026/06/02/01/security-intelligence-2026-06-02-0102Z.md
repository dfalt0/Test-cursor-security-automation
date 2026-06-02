# Security Intelligence Report - 2026-06-02 01:02 UTC

Repository verified: `dfalt0/Test-cursor-security-automation`

Report window: 2026-06-02 00:00-01:30 UTC, with late-2026-06-01 high-impact carry-forward items included for enterprise triage.

## Executive Summary

- Current UTC-day NVD publications checked at report time: 6 CVEs.
  - Critical: 0
  - High: 0
  - Medium: 4
  - Low: 2
- Late 2026-06-01 NVD publications remain material: 377 CVEs, including 19 Critical and 130 High by the NVD API metric selection used in this run.
- Critical / urgent findings requiring review:
  - CVE-2024-21182 - Oracle WebLogic Server unauthorized access; added to CISA KEV on 2026-06-01 with a 2026-06-04 remediation due date. Confidence: High.
  - CVE-2026-0300 - Palo Alto Networks PAN-OS User-ID Authentication Portal unauthenticated RCE; vendor marks exploit maturity `ATTACKED` and confirms limited exploitation. Confidence: High.
  - CVE-2026-0257 - Palo Alto Networks PAN-OS GlobalProtect authentication bypass; CISA KEV-listed with 2026-06-01 due date. Confidence: High.
  - CVE-2026-20182 - Cisco Catalyst SD-WAN Controller/Manager authentication bypass, CVSS 10.0; Cisco PSIRT confirms limited exploitation and published IoC guidance. Confidence: High.
  - CVE-2026-42945 - NGINX Rift heap overflow RCE; multiple Sploitus/GitHub PoC/scanner entries observed. Public exploit maturity appears high, but functional validation was not performed. Confidence: Medium-High.
  - CVE-2026-42208 - LiteLLM SQL injection; CISA KEV-listed, multiple Sploitus entries, credential exposure risk for LLM gateways. Confidence: High.
  - CVE-2026-39987 - Marimo pre-auth terminal WebSocket RCE; Sploitus entry claims in-the-wild exploitation within 10 hours. Confidence: Medium because active exploitation was not corroborated by CISA/vendor in this run.
  - CVE-2026-0826 - HP Poly VVX/Trio unauthenticated RCE; Rapid7 published exploit details and Metasploit module on 2026-06-01. Confidence: High.
- New malware / threat activity:
  - FortiClient EMS CVE-2026-35616 exploitation is being reported as a delivery path for EKZ Infostealer through trusted endpoint management workflows. Confidence: Medium-High; reporting is consistent but the direct Arctic Wolf source was represented through syndicated summaries during this run.
  - VX-Underground `MalwareSourceCode` latest pushed item remains `Python/Stealer.Python.GMBA.Manipulator.7z`, added 2026-05-30. Confidence: High.
  - Gamaredon / GammaWorm reporting continues around NTFS alternate data streams and CVE-2025-8088-themed archive delivery against Ukrainian entities. Confidence: Medium.
- Important vendor/security releases:
  - Android Security Bulletin - June 2026: critical Framework/System vulnerabilities and high Android/partner component issues; patch levels 2026-06-01 and 2026-06-05. Confidence: High.
  - Qualcomm June 2026 bulletin: critical Secure Processor issues CVE-2026-25276 and CVE-2026-25277 plus high Display/Boot/DSP/Software Center issues. Confidence: High.
  - GitLab CE/EE 19.0.1, 18.11.4, and 18.10.7 address Duo AI, DoS, and authorization flaws. Confidence: Medium-High.
  - GitHub Enterprise Server late-May security releases address SSRF and unauthenticated DoS issues. Confidence: High from NVD/vendor release-note references.

## Collection Notes and Confidence

- Sploitus homepage content did not expose a structured "Exploits of the Week" block in fetchable output. The Sploitus Top 10 below is therefore reconstructed from indexed Sploitus exploit pages and corroborating search results. Confidence: Medium.
- GitHub PoC repositories were identified via GitHub search metadata only. No repository was cloned or executed. Treat these as indicators requiring malware review and exploit validation. Confidence: Medium.
- Packet Storm direct fetch returned an anti-automation page; Packet Storm coverage is represented only where indexed through Sploitus or search snippets. Confidence: Low-Medium.
- Active exploitation is marked only when CISA KEV, a vendor, or a named security organization/source reported exploitation. Search-result-only claims are kept at Medium or Low confidence.

## Top Vulnerabilities

| Priority | CVE / ID | Severity | Affected software | Exploit availability | Active exploitation | Recommended action | Confidence |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Critical | CVE-2024-21182 | High, CVSS 7.5, KEV | Oracle WebLogic Server 12.2.1.4.0, 14.1.1.0.0 | Public PoC references exist but were not functionally validated | Yes, CISA KEV added 2026-06-01 | Apply Oracle CPU/latest supported patch; restrict T3/IIOP; review WebLogic access logs for anomalous unauthenticated access | High |
| Critical | CVE-2026-0300 | Critical, CVSS-BT 9.3, KEV | Palo Alto Networks PAN-OS User-ID Authentication Portal on PA-Series/VM-Series | Vendor does not publish exploit; attacks observed | Yes, vendor exploit maturity `ATTACKED` and limited exploitation observed | Upgrade to fixed PAN-OS releases; restrict or disable User-ID Authentication Portal; enable Threat ID 510019 where supported | High |
| Critical | CVE-2026-0257 | High, CVSS-BT 7.8, KEV | PAN-OS GlobalProtect configurations using auth override cookies | GitHub repo signal found; not validated | Yes, KEV-listed; vendor previously confirmed limited attempts | Upgrade to fixed PAN-OS/Prisma Access versions; disable risky auth override settings; review VPN connection anomalies | High |
| Critical | CVE-2026-20182 | Critical, CVSS 10.0, KEV | Cisco Catalyst SD-WAN Controller/Manager | Sploitus lists an assessment/exploit framework for DTLS peering bypass | Yes, Cisco PSIRT confirms limited exploitation | Preserve admin-tech/logs before upgrade; upgrade to fixed releases; check `auth.log` and control-connection `challenge-ack` indicators; engage Cisco TAC for suspected compromise | High |
| Critical | CVE-2026-42945 | Critical, reported CVSS 9.2 | NGINX Open Source 0.6.27-1.30.0 and NGINX Plus R32-R36 with vulnerable rewrite/set config | Multiple Sploitus/GitHub PoC, scanner, and lab entries | No vendor/CISA active exploitation confirmation found | Upgrade to NGINX 1.30.1/1.31.0 or relevant NGINX Plus hotfix; hunt for exposed rewrite+set patterns; test scanners only in authorized environments | Medium-High |
| Critical | CVE-2026-42208 | Critical, KEV | BerriAI LiteLLM proxy versions around 1.81.16-1.83.6/1.83.7 advisory range | Multiple Sploitus scanner/repro entries; SQLi payload patterns public | CISA KEV-listed; active exploitation not revalidated in this run | Upgrade to fixed LiteLLM; rotate all LLM/cloud API keys stored by exposed proxies; hunt for SQL metacharacters in Authorization headers | High |
| Critical | CVE-2026-39987 | Critical, KEV carry-forward | Marimo Python notebook before fixed release, `/terminal/ws` | Sploitus entry includes detection/exploitation details | Sploitus claims exploitation; not corroborated by CISA/vendor during this run | Upgrade to fixed Marimo release; block unauthenticated notebook/terminal exposure; audit for unexpected terminal WebSocket connections and cloud credential access | Medium |
| Critical | CVE-2026-0826 | Critical, CVSSv4 9.2 | HP Poly VVX and Trio VoIP phones with ICE enabled | Rapid7 developed Metasploit module and published technical details | No active exploitation observed in checked sources | Update Poly VVX/Trio firmware; disable ICE if not required; monitor VoIP segments for anomalous management traffic | High |
| High | CVE-2026-23918 | High, CVSS 8.8 | Apache HTTP Server 2.4.66 `mod_http2` | Sploitus PoC demonstrates reliable DoS; RCE described as theoretical/impractical by indexed PoC | No active exploitation observed | Upgrade to Apache 2.4.67; disable HTTP/2 as temporary mitigation where patching is delayed | Medium-High |
| High | CVE-2026-31431 | High, CVSS 7.8, KEV | Linux kernel `algif_aead` / `authencesn` page-cache write issue | Multiple Sploitus PoCs and detection packages | CISA KEV-listed; no new exploitation confirmation in this window | Apply kernel backports; disable or block `AF_ALG` / `algif_aead` where feasible; use container seccomp controls | High |
| Critical | CVE-2026-25276 / CVE-2026-25277 | Qualcomm rating Critical, CVSS 8.8 High | Qualcomm Secure Processor / Strongbox across many chipsets | No public PoC observed | No active exploitation observed | Push OEM firmware/security updates; prioritize enterprise-managed Android, XR, automotive, fixed wireless, and embedded fleets | High |
| Critical | CVE-2025-65018 and other Android June criticals | Android bulletin Critical | Android Framework/System components | No public PoC observed | No active exploitation stated by Android bulletin | Apply Android 2026-06-01/2026-06-05 patch levels; prioritize devices with sensitive enterprise access | High |
| Medium | CVE-2026-9048 / CVE-2026-9050 | Medium | Slider Revolution WordPress plugin | No PoC validated; NVD/GitHub advisory details public | No active exploitation observed | Update Slider Revolution; review Contributor accounts and plugin administration events | High |

## Current UTC-Day CVEs Published by NVD

| CVE | Severity | Product / component | Public exploit noted by source | Recommended action | Confidence |
| --- | --- | --- | --- | --- | --- |
| CVE-2026-10301 | Medium, CVSS 4.3 | itsourcecode Fees Management System 1.0 `index.php` XSS | NVD/VulDB state exploit is public | Patch/remove exposed app; treat as low enterprise priority unless deployed | High |
| CVE-2026-10302 | Medium, CVSS 6.3 | itsourcecode Fees Management System 1.0 `/manage_fee.php` SQL injection | NVD/VulDB state exploit is public | Patch/remove exposed app; review DB access logs if deployed | High |
| CVE-2026-10514 | Low, CVSS 2.4 | 1Panel-dev CordysCRM <= 1.6.2 XSS | NVD says exploit disclosed; patch exists | Upgrade to CordysCRM 1.7.0+ | High |
| CVE-2026-10528 | Low, CVSS 3.3 | Orthanc DICOM Server <= 1.12.11 DCMTK parser local stack overflow | NVD says exploit disclosed; local attack required | Deploy upstream patch; prioritize medical imaging hosts with local multi-user exposure | High |
| CVE-2026-9048 | Medium, CVSS 4.3 | Slider Revolution WordPress plugin 7.0.0-7.0.14 sensitive information exposure | No working PoC validated | Update plugin; rotate social/API credentials stored in sliders if Contributor accounts are untrusted | High |
| CVE-2026-9050 | Medium, CVSS 4.3 | Slider Revolution WordPress plugin 6.0.0-6.7.55 and 7.0.0-7.0.14 unauthorized plugin deactivation | No working PoC validated | Update plugin; audit plugin activation/deactivation events | High |

## Unified Vulnerability Records (Selected)

```json
[
  {
    "cve": "CVE-2024-21182",
    "cvss": "7.5",
    "vendor": "Oracle",
    "product": "WebLogic Server",
    "affected_versions": "12.2.1.4.0, 14.1.1.0.0",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://github.com/k4it0k1d/CVE-2024-21182"],
    "patch_available": true,
    "sources": [
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://nvd.nist.gov/vuln/detail/CVE-2024-21182",
      "https://www.oracle.com/security-alerts/cpujul2024.html"
    ]
  },
  {
    "cve": "CVE-2026-0300",
    "cvss": "9.3",
    "vendor": "Palo Alto Networks",
    "product": "PAN-OS User-ID Authentication Portal",
    "affected_versions": "PAN-OS 10.2, 11.1, 11.2, 12.1 before fixed releases; exposed User-ID Authentication Portal required",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://security.paloaltonetworks.com/CVE-2026-0300",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"
    ]
  },
  {
    "cve": "CVE-2026-20182",
    "cvss": "10.0",
    "vendor": "Cisco",
    "product": "Catalyst SD-WAN Controller and Manager",
    "affected_versions": "Multiple 20.x/26.x SD-WAN releases before fixed releases",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://sploitus.com/exploit?id=5E018311-5338-53E4-A443-92BBE3A551B9"],
    "patch_available": true,
    "sources": [
      "https://sec.cloudapps.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-sdwan-rpa2-v69WY2SW",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"
    ]
  },
  {
    "cve": "CVE-2026-42945",
    "cvss": "9.2",
    "vendor": "F5 / NGINX",
    "product": "NGINX Open Source / NGINX Plus rewrite module",
    "affected_versions": "NGINX Open Source 0.6.27-1.30.0; NGINX Plus R32-R36 with vulnerable rewrite+set patterns",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://sploitus.com/exploit?id=03328B0E-8919-5D0E-879C-542DCDCC0771",
      "https://github.com/DepthFirstDisclosures/Nginx-Rift"
    ],
    "patch_available": true,
    "sources": [
      "https://sploitus.com/exploit?id=03328B0E-8919-5D0E-879C-542DCDCC0771",
      "https://github.com/DepthFirstDisclosures/Nginx-Rift"
    ]
  },
  {
    "cve": "CVE-2026-42208",
    "cvss": "9.3",
    "vendor": "BerriAI",
    "product": "LiteLLM",
    "affected_versions": "LiteLLM proxy versions in the vulnerable 1.81.16-1.83.x advisory range",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://sploitus.com/exploit?id=18D75F8D-7FA6-5462-8891-8883AD614E31"
    ],
    "patch_available": true,
    "sources": [
      "https://github.com/BerriAI/litellm/security/advisories/GHSA-r75f-5x8p-qvmc",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://sploitus.com/exploit?id=18D75F8D-7FA6-5462-8891-8883AD614E31"
    ]
  },
  {
    "cve": "CVE-2026-0826",
    "cvss": "9.2",
    "vendor": "HP Poly",
    "product": "VVX and Trio VoIP phones",
    "affected_versions": "Certain Poly Voice products when ICE is enabled, before fixed UCS releases",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["Metasploit module referenced by Rapid7"],
    "patch_available": true,
    "sources": [
      "https://www.rapid7.com/blog/post/ve-cve-2026-0826-critical-unauthenticated-stack-buffer-overflow-hp-poly-vvx-trio-voip-phones-fixed/"
    ]
  },
  {
    "cve": "CVE-2026-25276",
    "cvss": "8.8",
    "vendor": "Qualcomm",
    "product": "Secure Processor / Strongbox",
    "affected_versions": "Multiple Snapdragon, FastConnect, automotive, XR, modem, audio, and embedded chipsets listed in Qualcomm June 2026 bulletin",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://docs.qualcomm.com/product/publicresources/securitybulletin/june-2026-bulletin.html"
    ]
  },
  {
    "cve": "CVE-2026-25277",
    "cvss": "8.8",
    "vendor": "Qualcomm",
    "product": "Secure Processor / Strongbox",
    "affected_versions": "Multiple Snapdragon, FastConnect, automotive, XR, modem, audio, and embedded chipsets listed in Qualcomm June 2026 bulletin",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://docs.qualcomm.com/product/publicresources/securitybulletin/june-2026-bulletin.html"
    ]
  }
]
```

## Exploits Released

### Sploitus Top 10 (reconstructed)

| Rank | CVE / topic | Affected software | Exploit type | Exploit maturity | Public PoC availability | Weaponization potential | Confidence |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | CVE-2026-42945 | NGINX rewrite module | Unauthenticated RCE heap overflow | Multiple PoC/lab/scanner listings | Yes | High where vulnerable rewrite+set configuration exists | Medium-High |
| 2 | CVE-2026-20182 | Cisco Catalyst SD-WAN Controller/Manager | Auth bypass / internal high-privilege access | Assessment/exploit framework listed | Yes | Very high for exposed SD-WAN control planes | High |
| 3 | CVE-2026-42208 | BerriAI LiteLLM proxy | SQL injection / credential extraction | Multiple scanner/repro entries | Yes | High for internet-facing LLM gateways with stored provider keys | High |
| 4 | CVE-2026-39987 | Marimo notebook | Pre-auth WebSocket terminal RCE | Detection/exploit details listed | Yes | High for exposed notebooks, especially cloud-hosted dev/AI systems | Medium |
| 5 | CVE-2026-31431 | Linux kernel `algif_aead` | Local privilege escalation | Multiple PoCs/detection packages | Yes | High post-compromise/container escape adjacency, local creds required | High |
| 6 | CVE-2026-23918 | Apache HTTP Server `mod_http2` | HTTP/2 double-free DoS, theoretical RCE | Working DoS PoC listed | Yes | Medium; practical impact is reliable DoS unless paired with further primitives | Medium-High |
| 7 | CVE-2026-48172 | LiteSpeed cPanel/WHM plugin | Privilege escalation audit tooling | Auditor listed, not full exploit | Yes, detection/audit | Medium-High for shared hosting/cPanel environments | Medium |
| 8 | CVE-2026-24069 | Kiuwan SAST | Improper enforcement / locked-account bypass | Packet Storm-indexed advisory | Advisory, not exploit | Medium; SaaS/on-prem SAST access-control impact | Medium |
| 9 | CVE-2026-43284 / CVE-2026-43500 | Linux kernel Dirty Frag family | Page-cache write / LPE family | Combined tool lists detect/full PoC for some issues | Partial | High for local post-exploitation chains | Medium |
| 10 | CVE-2026-8732 | WP Maps Pro WordPress plugin | Unauthenticated admin creation | Exploit details publicly described; not found directly on Sploitus in this run | Public technical details | High for exposed WordPress sites; active exploitation reported elsewhere | Medium-High |

### ExploitDB additions

- ExploitDB current homepage fetch did not expose a populated latest-exploits table to the scraper.
- Search-indexed recent additions observed:
  - EDB-52512 - Throttlestop Kernel Driver CVE-2025-7771 Windows local privilege escalation, dated 2026-04-22.
  - EDB-52510 - Avast Antivirus 25.11 unquoted service path Windows local privilege escalation, dated 2026-04-22.
- No new 2026-06-02 ExploitDB item was confidently identified in this run. Confidence: Medium.

### New GitHub PoC / exploit repository indicators

| Repository | Created | Signal | Validation status | Risk note |
| --- | --- | --- | --- | --- |
| `0xABCD01/CVE-2026-41089` | 2026-06-01 04:22 UTC | Claims Microsoft Netlogon CLDAP stack overflow PoC | Not cloned or executed | Treat as potentially malicious until code-reviewed; no functional validation |
| `bolubey/CVE-2026-0257` | 2026-06-01 12:02 UTC | Claims PAN-OS GlobalProtect auth bypass | Not cloned or executed | Could be scanner/PoC or malicious lure; validate offline |
| `ahmadsadeeq/TelnetdBypass-` | 2026-06-01 02:03 UTC | Claims CVE-2026-24061 GNU InetUtils Telnetd auth bypass scanner | Not cloned or executed | Low-star new repo; review before use |

## Malware Intelligence

### VX-Underground

- `vxunderground/MalwareSourceCode` remains the only recently pushed vx-underground repository observed through GitHub API.
- Latest commit: `1623926`, 2026-05-30, "Add files via upload".
- Added file: `Python/Stealer.Python.GMBA.Manipulator.7z`.
- No newer VX-Underground GitHub malware-source commit was observed during this run. Confidence: High.

### New / notable malware and campaigns

| Threat | Summary | Enterprise relevance | Recommended action | Confidence |
| --- | --- | --- | --- | --- |
| EKZ Infostealer via FortiClient EMS CVE-2026-35616 | Reporting describes actors abusing FortiClient EMS management workflows to push `FortiEndpoint_Patch.exe` to managed endpoints, launched by legitimate FortiClient process chains and exfiltrating browser data. | High for organizations with exposed/unpatched FortiClient EMS; turns endpoint management into a software-distribution channel. | Upgrade FortiClient EMS to fixed versions; restrict management port 8013; audit Remote Access Profile scripts and FortiClient logs `Trace\\scripts\\{GUID}.cmd`; rotate browser/session credentials from impacted endpoints. | Medium-High |
| GammaWorm / Gamaredon | Reporting describes fileless worm behavior using NTFS Alternate Data Streams and archive-themed delivery against Ukrainian entities, associated with Gamaredon/UAC-0010. | High for Ukraine, government, defense, judiciary, and partners; medium elsewhere. | Patch WinRAR; hunt for ADS-resident VBS/HTA, unusual startup persistence, and Cloudflare/Telegram-backed C2 patterns from reporting. | Medium |
| VX-Underground GMBA Manipulator stealer source archive | Malware source archive added to public repository. | Research/defensive relevance; potential reuse by lower-skill actors. | Monitor for derivative detections and hash/rule releases; do not download to production systems. | High |

## Security Releases and Vendor Advisories

| Vendor / project | Release / advisory | Key issues | Recommended action | Confidence |
| --- | --- | --- | --- | --- |
| CISA KEV | Catalog version 2026.06.01 | Newest KEV: CVE-2024-21182 Oracle WebLogic; recent KEVs include CVE-2026-0257, CVE-2026-48027, CVE-2026-45321, CVE-2026-8398 | Review KEV due dates and enforce emergency patch SLAs | High |
| Android | Android Security Bulletin - June 2026 | Critical Framework/System vulnerabilities; patch levels 2026-06-01 and 2026-06-05 | Push June Android updates to managed devices; prioritize devices with enterprise identity, VPN, email, and EDR access | High |
| Qualcomm | June 2026 Security Bulletin | Critical Secure Processor CVE-2026-25276/25277; high Display/Boot/DSP/Software Center issues | Track OEM firmware availability; update Android/embedded/automotive/XR/fixed-wireless devices | High |
| Palo Alto Networks | CVE-2026-0300 advisory updated 2026-05-28 | PAN-OS User-ID Authentication Portal unauthenticated RCE, attacked | Upgrade and restrict/disable exposed portal; enable Threat ID 510019 | High |
| Cisco | CVE-2026-20182 advisory updated 2026-05-27 | Catalyst SD-WAN auth bypass, limited exploitation | Preserve logs, upgrade to fixed releases, check IoCs, open TAC case for suspected compromise | High |
| GitLab | 19.0.1, 18.11.4, 18.10.7 | Duo AI access control, Wiki DoS, GraphQL authorization flaws | Upgrade self-managed GitLab; monitor Duo AI runner and Wiki abuse | Medium-High |
| GitHub Enterprise Server | Late-May 3.20.2/3.20.3 family releases | SSRF, unauthenticated DoS, and other GHES vulnerabilities | Upgrade GHES appliances and restrict internal network reachability from GHES | High |
| HP Poly / Rapid7 | CVE-2026-0826 disclosure | Unauthenticated VoIP phone RCE with Metasploit module | Update UCS firmware and disable ICE where unnecessary | High |
| Apache HTTP Server | 2.4.67 | CVE-2026-23918 HTTP/2 double-free | Upgrade or disable HTTP/2 pending patch | Medium-High |

## Recommended Actions (ranked)

1. Patch or isolate KEV-listed and exploited edge systems first: Oracle WebLogic CVE-2024-21182, PAN-OS CVE-2026-0300 / CVE-2026-0257, Cisco SD-WAN CVE-2026-20182, and LiteLLM CVE-2026-42208.
2. For Cisco SD-WAN, preserve `admin-tech` and relevant logs before upgrading, then validate `auth.log` and control-connection `challenge-ack` indicators.
3. Inventory NGINX deployments for CVE-2026-42945 exposure: version range plus rewrite rules containing `?` and `set` capture usage. Upgrade to fixed NGINX/Plus releases before using public scanners broadly.
4. Treat internet-facing AI/dev tooling as high priority: LiteLLM, Marimo, Flowise, Vitest UI/browser mode, PraisonAI, Cline, and similar developer agents/notebooks should not be exposed without authentication and network controls.
5. Apply Android June 2026 and Qualcomm/OEM firmware updates to managed mobile, XR, embedded, and automotive fleets as soon as OEM updates are available.
6. If FortiClient EMS is present, verify fixed versions, restrict EMS management access, and hunt for unauthorized VPN profile scripts or `FortiEndpoint_Patch.exe`-like payloads.
7. Review the three new GitHub PoC repositories only in isolated malware-analysis sandboxes; do not run code from new CVE repositories directly on analyst workstations.
8. Update HP Poly VVX/Trio devices, especially where VoIP management networks are reachable from user or guest segments.
9. For WordPress estates, update WP Maps Pro and Slider Revolution, then audit for newly created admins, plugin deactivation events, and exposed Contributor accounts.
10. Continue KEV monitoring hourly; CISA feed is currently more authoritative than search snippets for date-added status.

## Sources Checked

- CISA KEV JSON: https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json
- NVD API / detail pages: https://services.nvd.nist.gov/rest/json/cves/2.0
- GitHub Advisory Database: https://github.com/advisories
- GitHub repository search / API
- Sploitus indexed exploit pages: https://sploitus.com/exploit
- ExploitDB homepage and indexed search results: https://www.exploit-db.com/
- Packet Storm files page: https://packetstormsecurity.com/files/
- Palo Alto Networks CVE-2026-0300 advisory: https://security.paloaltonetworks.com/CVE-2026-0300
- Cisco CVE-2026-20182 advisory: https://sec.cloudapps.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-sdwan-rpa2-v69WY2SW
- Android June 2026 bulletin: https://source.android.com/docs/security/bulletin/2026/2026-06-01
- Qualcomm June 2026 bulletin: https://docs.qualcomm.com/product/publicresources/securitybulletin/june-2026-bulletin.html
- Rapid7 HP Poly CVE-2026-0826 disclosure: https://www.rapid7.com/blog/post/ve-cve-2026-0826-critical-unauthenticated-stack-buffer-overflow-hp-poly-vvx-trio-voip-phones-fixed/
- VX-Underground GitHub repositories: https://github.com/vxunderground
