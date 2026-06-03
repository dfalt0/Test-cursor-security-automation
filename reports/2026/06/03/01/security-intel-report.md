# Security Intelligence Report - 2026-06-03 01:02 UTC

Collection window: 2026-06-03 00:00-01:35 UTC, with rolling 24 hour enrichment from 2026-06-02 01:02 UTC.

Confidence levels: High means confirmed by a primary vendor, CISA KEV, or multiple authoritative sources. Medium means corroborated by at least one reliable source plus secondary context. Low means an unvalidated public repository, search result, or single weak signal.

## Executive Summary

- NVD current-hour intake: 5 newly published CVEs, all medium severity. No new critical or high NVD CVEs were published between 00:00 and 01:35 UTC.
- NVD rolling 24 hour context: 224 CVEs, including 12 critical, 64 high, 84 medium, 6 low, and 58 unknown severity entries.
- Critical/high enterprise priorities from the rolling window: Progress Sitefinity CVE-2026-7312 and CVE-2026-7198, Kirki WordPress CVE-2026-8206, OpenMed CVE-2026-47117, Spacelabs Sentinel CVE-2026-0611, authentik CVE-2026-49448, LibreChat CVE-2026-32625, and React Router CVE-2026-42211.
- Confirmed active exploitation/KEV priorities: Cisco Catalyst SD-WAN CVE-2026-20182, cPanel/WHM CVE-2026-41940, FortiClient EMS CVE-2026-35616, Drupal Core CVE-2026-9082, Citrix NetScaler CVE-2026-3055, Linux Kernel CVE-2022-0492, and Android Framework CVE-2025-48595.
- Exploit intelligence: Sploitus static homepage did not expose an "Exploits of the Week" block, so the Sploitus Top 10 below is reconstructed from indexed Sploitus exploit pages. Treat GitHub/Sploitus repositories as indicators until code provenance and behavior are reviewed.
- Malware/threat activity: FortiClient EMS exploitation is tied to EKZ Infostealer delivery; SANS ISC reports SVG phishing with `application/ecmascript` MIME evasion; MalwareBazaar showed 231 submissions in the past 24 hours with Mirai as the most seen family.

## Source Coverage and Collection Notes

- NVD CVE API was queried for the current hour and rolling 24 hour windows.
- CISA KEV JSON catalog version 2026.06.02 was queried directly. Latest additions remain CVE-2022-0492 and CVE-2025-48595, both due 2026-06-05.
- GitHub Security Advisories updated after 2026-06-03 00:00 UTC included X.Org, DesktopCommanderMCP, code-index-mcp, Passeum Ticketing, EmergencyWP, QloApps, Docker/Desktop-related entries, and LibreChat carry-forward advisories.
- GitHub repository search found 0 newly created `CVE-2026 PoC exploit` repositories for 2026-06-03, and 7 repositories pushed today matching `CVE-2026 PoC exploit`.
- ExploitDB direct CSV latest entries remained 2026-06-01: Drupal Core CVE-2026-9082, EDB-ID 52608, and WordPress OrderConvo CVE-2025-10162, EDB-ID 52607.
- Sploitus homepage fetch returned only the search UI; the "Exploits of the Week" block was not available from the static page. Sploitus entries were reconstructed from indexed exploit pages.
- VX-Underground GitHub repositories showed no new push after `vxunderground/MalwareSourceCode` on 2026-05-30. `vx-underground.org` content availability was not relied on because previous runs observed access restrictions.

## Top Vulnerabilities

### 1. Cisco Catalyst SD-WAN Controller/Manager authentication bypass - CVE-2026-20182

- Severity: Critical; CVSS 10.0 reported in exploit intelligence; CISA KEV listed.
- Affected software: Cisco Catalyst SD-WAN Controller and Manager/vSmart/vManage fixed releases listed by Cisco.
- Exploit availability: Public exploit material and Metasploit/Sploitus indicators are available.
- Active exploitation: Confirmed. Cisco PSIRT and Talos describe limited exploitation for CVE-2026-20182 and broader exploitation of prior SD-WAN vulnerabilities.
- Recommended action: Treat as emergency. Upgrade all SD-WAN control components to Cisco fixed releases, collect admin-tech bundles, and open a Cisco TAC case for IOC scanning.
- Confidence: High.
- Sources: CISA KEV, Cisco PSIRT, Cisco remediation guide, Cisco Talos, Sploitus.

### 2. cPanel & WHM authentication bypass/RCE - CVE-2026-41940

- Severity: Critical; CVSS 10.0 in exploit writeups; CISA KEV listed with known ransomware campaign use.
- Affected software: WebPros cPanel & WHM and WP2.
- Exploit availability: Public exploit code, ExploitDB EDB-ID 52574, Packet Storm/Metasploit/Sploitus indicators, and multiple GitHub PoC repositories.
- Active exploitation: Confirmed. CISA KEV lists ransomware use, and Shadowserver reports ongoing cPanel/WHM compromise/scanning activity.
- Recommended action: Patch immediately, restrict WHM management ports, review WHM session artifacts, search for `sorry-ransomware`, `whmstealer`, and related backdoors, and rotate hosting-panel credentials.
- Confidence: High.
- Sources: CISA KEV, cPanel advisory, Shadowserver, Sploitus, ExploitDB, Packet Storm.

### 3. Fortinet FortiClient EMS improper access control - CVE-2026-35616

- Severity: Critical; CVSS 9.1.
- Affected software: FortiClient EMS 7.4.5 and 7.4.6.
- Exploit availability: Exploited in the wild; public technical reporting describes campaign behavior.
- Active exploitation: Confirmed by Fortinet and Arctic Wolf. Observed exploitation delivered EKZ Infostealer disguised as a Fortinet endpoint patch.
- Recommended action: Apply Fortinet hotfixes or upgrade to 7.4.7+, restrict EMS API exposure, inspect Remote Access Profiles and endpoint policies for malicious PowerShell/script changes, and hunt for `FortiEndpoint_Patch.exe`/`p.exe`.
- Confidence: High.
- Sources: Fortinet PSIRT FG-IR-26-099, CISA KEV, Arctic Wolf, NVD.

### 4. Android Framework integer overflow - CVE-2025-48595

- Severity: High; CISA KEV listed.
- Affected software: Android Framework on Android 14, 15, 16, and 16-QPR2.
- Exploit availability: No public PoC confirmed in this run.
- Active exploitation: Confirmed limited/targeted exploitation per Google/Android bulletin wording and CISA KEV.
- Recommended action: Move Android fleets to the 2026-06-05 security patch level or later. Prioritize executive, administrator, and high-risk mobile users.
- Confidence: High.
- Sources: CISA KEV, Android Security Bulletin June 2026, BleepingComputer, Help Net Security.

### 5. Linux Kernel cgroups v1 release_agent privilege escalation/container escape - CVE-2022-0492

- Severity: High; CVSS 7.8; CISA KEV listed on 2026-06-02.
- Affected software: Linux kernel cgroup v1 configurations, particularly permissive container environments.
- Exploit availability: Public exploitation knowledge has existed since 2022; new relevance comes from KEV addition.
- Active exploitation: Confirmed by CISA KEV listing, but public exploitation details for current activity are limited.
- Recommended action: Patch kernels, disable or constrain cgroup v1 where possible, enforce seccomp/AppArmor/SELinux, and block containers from running privileged or creating unsafe user namespaces.
- Confidence: High for KEV status; Medium for current campaign details.
- Sources: CISA KEV, Linux kernel commit, Unit 42, Wiz.

### 6. Progress Sitefinity credential exposure/access control cluster - CVE-2026-7312 and CVE-2026-7198

- Severity: Critical; CVE-2026-7312 CVSS 10.0, CVE-2026-7198 CVSS 9.8.
- Affected software: Progress Sitefinity 14.x and 15.x ranges listed in the Progress advisory.
- Exploit availability: No public functional exploit was confirmed in this run.
- Active exploitation: Not confirmed.
- Recommended action: Apply the Progress Sitefinity security advisory fixes, review Sitefinity Insight integration secrets, rotate exposed credentials, and audit backend access logs.
- Confidence: High for vulnerability details; Medium for exploitability in the wild.
- Sources: NVD, Progress community advisory.

### 7. Kirki WordPress plugin account takeover - CVE-2026-8206

- Severity: Critical; CVSS 9.8 in NVD.
- Affected software: Kirki Freeform Page Builder/Website Builder/Customizer versions 6.0.0 through 6.0.6.
- Exploit availability: Sploitus lists an exploit, and GitHub repository `Jenderal92/CVE-2026-8206` claims a mass exploitation tool. These are unvalidated indicators.
- Active exploitation: Not confirmed by primary sources in this run.
- Recommended action: Upgrade/remove affected Kirki versions, reset credentials for privileged WordPress users if exposure is suspected, and monitor password reset flows.
- Confidence: High for CVE and severity; Low for PoC functionality.
- Sources: NVD, WordPress plugin trac, GitHub search, Sploitus.

### 8. OpenMed remote code execution via PII model loading - CVE-2026-47117

- Severity: Critical; CVSS 9.8.
- Affected software: OpenMed before 1.5.2.
- Exploit availability: Technical advisory describes unauthenticated RCE through user-supplied Hugging Face model loading with `trust_remote_code=True`.
- Active exploitation: Not confirmed.
- Recommended action: Upgrade to 1.5.2+, restrict unauthenticated model-selection endpoints, and review for unexpected model repositories or outbound fetches.
- Confidence: High.
- Sources: NVD, VulnCheck, OpenMed commit/release.

### 9. Spacelabs Healthcare Sentinel unauthenticated RCE - CVE-2026-0611

- Severity: Critical; CVSS 9.8.
- Affected software: Spacelabs Sentinel 10.5.x and higher and 11.x.x before 11.6.0.
- Exploit availability: Technical advisory describes .NET Remoting channel abuse on port 8989 to write ASPX webshells.
- Active exploitation: Not confirmed.
- Recommended action: Upgrade to 11.6.0+, isolate port 8989 from untrusted networks, and hunt IIS webroot for unexpected ASPX files.
- Confidence: High.
- Sources: NVD, Spacelabs advisory PDF, VulnCheck.

### 10. LibreChat MCP environment-secret exfiltration - CVE-2026-32625

- Severity: Critical; CVSS 9.6.
- Affected software: LibreChat up to and including 0.8.3.
- Exploit availability: GitHub advisory includes proof-of-concept behavior around `${VAR}` placeholder resolution in user-supplied MCP server URLs.
- Active exploitation: Not confirmed.
- Recommended action: Upgrade per LibreChat advisory, remove untrusted MCP server configurations, rotate potentially exposed environment secrets, and restrict MCP configuration creation to trusted administrators.
- Confidence: High.
- Sources: NVD, GitHub Security Advisory GHSA-4pcc-j6m6-wcwx.

## Newly Published Current-Hour CVEs

| CVE | Severity | Affected software | Exploit/PoC signal | Action |
| --- | --- | --- | --- | --- |
| CVE-2026-10690 | Medium, CVSS 6.3 | DesktopCommanderMCP 0.2.37 `read_file` URL fetching | Public GitHub issue; NVD states exploit public; GHSA updated | Upgrade to fixed release/commit, block private IP/link-local URL fetching, and audit MCP servers connected to agents. |
| CVE-2026-10691 | Medium, CVSS 4.3 | DesktopCommanderMCP <= 0.2.38 `start_search` | Public issue/PR and v0.2.39 release | Upgrade to v0.2.39+, limit untrusted regex search input. |
| CVE-2026-10692 | Medium, CVSS 4.3 | code-index-mcp <= 2.14.0 `search_code_advanced` | Public issue/commit and v2.14.1 release | Upgrade to v2.14.1+, enforce regex complexity guards. |
| CVE-2026-7421 | Medium, CVSS 4.4 | Passeum Ticketing WordPress plugin <= 1.0 | Wordfence/trac references; no functional exploit confirmed | Patch/remove plugin; sanitize stored settings. |
| CVE-2026-9732 | Medium, CVSS 4.3 | EmergencyWP WordPress plugin <= 1.4.2 | Wordfence/trac references; no functional exploit confirmed | Patch/remove plugin; enforce nonce validation on settings saves. |

## Exploits Released

### Sploitus Top 10 (reconstructed)

Sploitus homepage did not expose an "Exploits of the Week" list in static fetch. The following top 10 are reconstructed from indexed Sploitus pages and prioritized by severity, exploit maturity, and enterprise relevance.

| Rank | CVE/Item | Affected software | Exploit type | Maturity | PoC availability | Weaponization potential |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | CVE-2026-20182 | Cisco Catalyst SD-WAN Controller/Manager | Unauthenticated auth bypass, SSH key injection, NETCONF access | Public exploit and Metasploit indicator | Yes | Critical: perimeter/control-plane compromise. |
| 2 | CVE-2026-41940 | cPanel & WHM/WP2 | CRLF session-file injection, auth bypass, root WHM access/RCE | Multiple public tools, ExploitDB, Packet Storm, Metasploit | Yes | Critical: mass hosting compromise and ransomware linkage. |
| 3 | CVE-2026-42945 | NGINX-related indexed entry | CVSS 9.2 exploit listing | Indexed only in this run | Unvalidated | High if applicable to exposed infrastructure; needs source validation. |
| 4 | CVE-2026-45659 | Microsoft SharePoint | Deserialization/RCE claim | Sploitus entry includes private/download claim | Unvalidated; suspicious download link | High target value, but low confidence in code safety/functionality. |
| 5 | CVE-2026-7465 | Spectra Gutenberg Blocks | Arbitrary PHP function call | Sploitus entry includes lab PoC text | Yes, unvalidated | High for WordPress sites if versions match. |
| 6 | CVE-2026-8206 | Kirki WordPress plugin | Account takeover/privilege escalation | Sploitus plus GitHub repo indicator | Yes, unvalidated | High due WordPress deployment footprint. |
| 7 | CVE-2026-48778 | Notepad++ 8.9.6 | Local arbitrary code execution through config manipulation | Packet Storm/Sploitus | Yes | Medium: requires local/user-context trigger. |
| 8 | CVE-2026-48800 | Notepad++ <= 8.9.6 | Arbitrary code execution through shortcuts.xml | Sploitus/GitHub advisory | Yes | Medium: endpoint/user-context risk. |
| 9 | CVE-2026-BetterSQLCipher-RCE | better-sqlcipher | `loadExtension()` RCE claim | Sploitus/GitHub-style repo text | Unvalidated | Medium to high for apps exposing extension load paths; CVE format is not standard. |
| 10 | CVE-2026-5718 / CVE-2026-2144 / CVE-2026-21509 | Various indexed entries | Mixed exploit claims | Indexed only | Unvalidated | Medium; requires validation before operational use. |

### ExploitDB additions

- Latest direct ExploitDB CSV rows remained dated 2026-06-01.
- EDB-ID 52608: Drupal Core 10.5.5 error-based SQL injection, CVE-2026-9082, unverified.
- EDB-ID 52607: WordPress OrderConvo 14 path traversal, CVE-2025-10162, unverified.
- No direct CSV row dated 2026-06-03 was observed during this run.

### New GitHub PoC indicators

Strict GitHub search for `CVE-2026 PoC exploit created:>=2026-06-03` returned 0 repositories. Broader pushed-since search returned 7 unvalidated indicators:

- `Defacto-ridgepole254/CVE-2026-41940-Exploit-PoC` - cPanel/WHM auth bypass PoC claim; pushed 2026-06-03 00:48 UTC.
- `Dullpurple-sloop726/CVE-2026-31431-Linux-Copy-Fail` - Linux LPE claim; pushed 2026-06-03 00:48 UTC.
- `Liverwortenuresis371/copyfail-rs` - CVE-2026-31431 exploit/detection claim; pushed 2026-06-03 00:47 UTC.
- `Jumpthereness578/CVE-2026-2991` - KiviCare auth bypass PoC claim; pushed 2026-06-03 00:28 UTC.
- `Recorded-texteditor120/CVE-2026-31802` - npm tar path traversal PoC claim; pushed 2026-06-03 00:25 UTC.
- `fartlover37/CVE-2026-2441-PoC` - Chrome Blink CSS UAF PoC claim; pushed 2026-06-03 00:07 UTC.
- `hamzamalik3461/CVE-2026-20841` - Windows Notepad RCE claim; pushed 2026-06-03 00:05 UTC.

These repositories were not executed or cloned. Treat them as collection indicators and inspect for malicious payloads before use.

## Malware Intelligence

- FortiClient EMS/EKZ Infostealer: Arctic Wolf observed exploitation of CVE-2026-35616 to push a fake Fortinet endpoint patch (`FortiEndpoint_Patch.exe`/`p.exe`) that steals Chromium/Firefox credentials and exfiltrates over HTTP. Confidence: High.
- MalwareBazaar: Browse page showed 231 submissions in the past 24 hours; Mirai was the most seen malware family. Confidence: High for feed observation.
- SANS ISC SVG phishing: SANS reported phishing emails with SVG attachments containing JavaScript and `application/ecmascript` MIME type to evade simplistic JavaScript detection. Confidence: High.
- SANS ISC NetSupport RAT: SANS documented a SmartApeSG ClickFix infection chain ending in malicious NetSupport RAT persistence and C2 at `185.163.47[.]217:443`. Confidence: High.
- VX-Underground GitHub: Latest pushed repository remained `vxunderground/MalwareSourceCode` on 2026-05-30; no new VX GitHub push was observed during this run. Confidence: Medium.

## Security Releases and Advisories

- Microsoft: Search results showed MSRC entries for June 2026 Netlogon/SharePoint-related CVEs, but the MSRC pages rendered as dynamic "Loading" pages in static fetch. Carry forward Netlogon CVE-2026-41089 as medium-confidence active exploitation based on CCB/SANS secondary reporting until primary MSRC/CCB details are revalidated.
- Cisco: Cisco PSIRT/Talos confirmed limited exploitation of CVE-2026-20182 and issued fixed release guidance. No workaround; upgrade required.
- Fortinet: Fortinet PSIRT FG-IR-26-099 confirms CVE-2026-35616 exploitation in the wild and hotfix availability for EMS 7.4.5/7.4.6; 7.4.7+ contains the fix.
- GitHub Enterprise Server: GHES 3.20.3 remains an important security release with CVE-2026-9312 pre-auth SSRF, CVE-2026-8606 SSRF/timing side channel, and Linux "Dirty Frag" CVE-2026-43284/CVE-2026-43500 fixes. Administrators must handle the GHES package-signing GPG key rotation step.
- GitLab: No June 3 security release found. Latest observed security patch set remains May 27 versions 19.0.1, 18.11.4, and 18.10.7, including CVE-2026-4868 and CVE-2026-1402.
- Google/Android: June 2026 Android bulletin fixes 124 vulnerabilities, including actively exploited CVE-2025-48595. Deploy patch level 2026-06-05 or later.
- Progress: Sitefinity advisory addresses CVE-2026-7312, CVE-2026-7198, CVE-2026-7195, CVE-2026-7201, and CVE-2026-7313.
- Spacelabs Healthcare: Sentinel advisory fixes unauthenticated .NET Remoting RCE in 11.6.0.
- Authentik: Security advisories patch source-stage bypass, SAML XML signature wrapping, and related high/critical identity-provider issues in 2025.12.6, 2026.2.4, and 2026.5.1.

## Recommended Actions

1. Emergency patch and hunt: Cisco Catalyst SD-WAN CVE-2026-20182; collect logs/admin-tech and request Cisco TAC IOC scanning.
2. Emergency patch and compromise assessment: cPanel/WHM CVE-2026-41940; assume exposed instances may be targeted, inspect sessions/backdoors, and rotate credentials.
3. Patch and hunt FortiClient EMS CVE-2026-35616; search for EKZ Infostealer artifacts and unauthorized EMS policy/profile changes.
4. Deploy Android June 2026 patch level 2026-06-05+ for all managed Android 14+ devices, prioritizing high-risk users.
5. Review Linux container hosts for cgroup v1 exposure to CVE-2022-0492; patch kernels and enforce seccomp/AppArmor/SELinux.
6. Patch Progress Sitefinity, Spacelabs Sentinel, OpenMed, authentik, LibreChat, GHES, and GitLab where present.
7. For MCP tooling, inventory DesktopCommanderMCP/code-index-mcp/blender-mcp installations, patch current-hour CVEs, and restrict untrusted prompt-driven URL/file/regex actions.
8. Block or detonate SVG email attachments with embedded script; ensure detection includes `application/ecmascript`, `text/javascript`, and `application/javascript`.
9. Treat all public PoC repositories discovered today as hostile until reviewed in an isolated environment.

## Unified Vulnerability Records

```json
[
  {
    "cve": "CVE-2026-20182",
    "cvss": "10.0",
    "vendor": "Cisco",
    "product": "Catalyst SD-WAN Controller/Manager",
    "affected_versions": "Versions before Cisco fixed releases for vSmart/vManage control components",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://sploitus.com/exploit?id=13DF22F3-E9C6-58EE-B458-EB585C4D715D",
      "https://sploitus.com/exploit?id=MSF%3AAUXILIARY-ADMIN-NETWORKING-CISCO_SDWAN_VHUB_AUTH_BYPASS-"
    ],
    "patch_available": true,
    "sources": [
      "https://sec.cloudapps.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-sdwan-rpa2-v69WY2SW",
      "https://blog.talosintelligence.com/sd-wan-ongoing-exploitation/",
      "https://www.cisa.gov/known-exploited-vulnerabilities-catalog"
    ],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-41940",
    "cvss": "10.0",
    "vendor": "WebPros",
    "product": "cPanel & WHM and WP2",
    "affected_versions": "Affected cPanel & WHM and WP2 versions before vendor security updates",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://sploitus.com/exploit?id=F455C2B6-D79B-5920-95CC-911E5E56E4AC",
      "https://sploitus.com/exploit?id=EDB-ID%3A52574",
      "https://sploitus.com/exploit?id=PACKETSTORM%3A221269"
    ],
    "patch_available": true,
    "sources": [
      "https://support.cpanel.net/hc/en-us/articles/40073787579671-cPanel-WHM-Security-Update-04-28-2026",
      "https://www.cisa.gov/known-exploited-vulnerabilities-catalog",
      "https://www.shadowserver.org/what-we-do/network-reporting/compromised-website-report/"
    ],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-35616",
    "cvss": "9.1",
    "vendor": "Fortinet",
    "product": "FortiClient EMS",
    "affected_versions": "7.4.5 through 7.4.6",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://fortiguard.fortinet.com/psirt/FG-IR-26-099",
      "https://arcticwolf.com/resources/blog/forticlient-ems-exploited-via-cve-2026-35616-to-deliver-ekz-infostealer-disguised-as-a-fortinet-patch/",
      "https://www.cisa.gov/known-exploited-vulnerabilities-catalog"
    ],
    "confidence": "High"
  },
  {
    "cve": "CVE-2025-48595",
    "cvss": "High",
    "vendor": "Google",
    "product": "Android Framework",
    "affected_versions": "Android 14, 15, 16, and 16-QPR2 before 2026-06-05 patch level",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://source.android.com/docs/security/bulletin/2026/2026-06-01",
      "https://www.cisa.gov/known-exploited-vulnerabilities-catalog",
      "https://www.bleepingcomputer.com/news/security/google-fixes-one-actively-exploited-android-zero-day-124-flaws/"
    ],
    "confidence": "High"
  },
  {
    "cve": "CVE-2022-0492",
    "cvss": "7.8",
    "vendor": "Linux",
    "product": "Kernel cgroups v1 release_agent",
    "affected_versions": "Linux kernels through vulnerable cgroup v1 configurations before upstream fix",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://www.cisa.gov/known-exploited-vulnerabilities-catalog",
      "https://unit42.paloaltonetworks.com/cve-2022-0492-cgroups/",
      "https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=24f6008564183aa120d07c03d9289519c2fe02af"
    ],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-7312",
    "cvss": "10.0",
    "vendor": "Progress",
    "product": "Sitefinity",
    "affected_versions": "14.0.7700-14.4.8152, 15.0.8200-15.0.8234, 15.1.8300-15.1.8335, 15.2.8400-15.2.8441, 15.3.8500-15.3.8531, 15.4.8600-15.4.8630",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://community.progress.com/s/article/Sitefinity-Security-Advisory-for-Addressing-Security-Vulnerabilities-CVE-2026-7312-CVE-2026-7198-CVE-2026-7195-CVE-2026-7201-CVE-2026-7313-May-2026",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-7312"
    ],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-7198",
    "cvss": "9.8",
    "vendor": "Progress",
    "product": "Sitefinity",
    "affected_versions": "15.4.8623 before 15.4.8630",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://community.progress.com/s/article/Sitefinity-Security-Advisory-for-Addressing-Security-Vulnerabilities-CVE-2026-7312-CVE-2026-7198-CVE-2026-7195-CVE-2026-7201-CVE-2026-7313-May-2026",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-7198"
    ],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-8206",
    "cvss": "9.8",
    "vendor": "Kirki",
    "product": "Freeform Page Builder, Website Builder & Customizer WordPress plugin",
    "affected_versions": "6.0.0 through 6.0.6",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://sploitus.com/exploit?id=404E68B4-550F-51C1-B107-460F8E9F767F",
      "https://github.com/Jenderal92/CVE-2026-8206"
    ],
    "patch_available": true,
    "sources": [
      "https://nvd.nist.gov/vuln/detail/CVE-2026-8206",
      "https://plugins.trac.wordpress.org/browser/kirki/",
      "https://www.wordfence.com/threat-intel/"
    ],
    "confidence": "Medium"
  },
  {
    "cve": "CVE-2026-47117",
    "cvss": "9.8",
    "vendor": "OpenMed",
    "product": "OpenMed",
    "affected_versions": "Before 1.5.2",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://www.vulncheck.com/advisories/openmed-remote-code-execution-via-pii-model-loading",
      "https://github.com/maziyarpanahi/openmed/releases/tag/v1.5.2",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-47117"
    ],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-0611",
    "cvss": "9.8",
    "vendor": "Spacelabs Healthcare",
    "product": "Sentinel",
    "affected_versions": "10.5.x and higher and 11.x.x before 11.6.0",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://spacelabshealthcare.com/wp-content/uploads/2026/06/079-0273-00-RevA-Security-Advisory-Sentinel-.NET-Remoting-Vulnerability.pdf",
      "https://www.vulncheck.com/advisories/spacelabs-healthcare-sentinel-x-unauthenticated-rce-via-net-remoting",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-0611"
    ],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-49448",
    "cvss": "9.8",
    "vendor": "authentik",
    "product": "authentik identity provider",
    "affected_versions": "Before 2025.12.6, 2026.2.4, and 2026.5.1",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://github.com/goauthentik/authentik/security/advisories/GHSA-xp7f-xjjx-gwm8",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-49448"
    ],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-32625",
    "cvss": "9.6",
    "vendor": "LibreChat",
    "product": "LibreChat",
    "affected_versions": "Up to and including 0.8.3",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/danny-avila/LibreChat/security/advisories/GHSA-4pcc-j6m6-wcwx"
    ],
    "patch_available": true,
    "sources": [
      "https://github.com/danny-avila/LibreChat/security/advisories/GHSA-4pcc-j6m6-wcwx",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-32625"
    ],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-10690",
    "cvss": "6.3",
    "vendor": "wonderwhy-er",
    "product": "DesktopCommanderMCP",
    "affected_versions": "0.2.37",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/wonderwhy-er/DesktopCommanderMCP/issues/410"
    ],
    "patch_available": true,
    "sources": [
      "https://nvd.nist.gov/vuln/detail/CVE-2026-10690",
      "https://github.com/wonderwhy-er/DesktopCommanderMCP/issues/410",
      "https://github.com/sorlen008/DesktopCommanderMCP/commit/53699bebba9950047bca16ac4dc8f0568f596aaa"
    ],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-10692",
    "cvss": "4.3",
    "vendor": "johnhuang316",
    "product": "code-index-mcp",
    "affected_versions": "Up to 2.14.0",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/johnhuang316/code-index-mcp/issues/84"
    ],
    "patch_available": true,
    "sources": [
      "https://nvd.nist.gov/vuln/detail/CVE-2026-10692",
      "https://github.com/johnhuang316/code-index-mcp/releases/tag/v2.14.1"
    ],
    "confidence": "High"
  }
]
```

## Source Links

- NVD CVE API: https://services.nvd.nist.gov/rest/json/cves/2.0/
- CISA KEV catalog: https://www.cisa.gov/known-exploited-vulnerabilities-catalog
- CISA KEV JSON: https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json
- GitHub Security Advisories: https://github.com/advisories
- GitHub repository search: https://github.com/search
- ExploitDB CSV: https://gitlab.com/exploit-database/exploitdb/-/raw/main/files_exploits.csv
- Sploitus: https://sploitus.com/
- MalwareBazaar: https://bazaar.abuse.ch/browse/
- VX-Underground GitHub: https://github.com/vxunderground
- SANS ISC: https://isc.sans.edu/
- Cisco PSIRT: https://sec.cloudapps.cisco.com/security/center/
- Fortinet PSIRT: https://fortiguard.fortinet.com/psirt/FG-IR-26-099
- Android Security Bulletin: https://source.android.com/docs/security/bulletin/2026/2026-06-01
- Shadowserver: https://www.shadowserver.org/
