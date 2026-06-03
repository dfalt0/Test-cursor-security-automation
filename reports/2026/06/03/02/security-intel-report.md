# Security Intelligence Report - 2026-06-03 02:03 UTC

Collection window: 2026-06-03 01:00-02:35 UTC, with rolling 24 hour enrichment from 2026-06-02 02:35 UTC.

Confidence levels: High means confirmed by a primary vendor, CISA KEV, or multiple authoritative sources. Medium means corroborated by at least one reliable source plus secondary context. Low means an unvalidated public repository, search result, or single weak signal.

## Executive Summary

- NVD current-hour intake: 4 newly published CVEs between 01:00 and 02:35 UTC: 0 critical, 0 high, 1 medium, 1 low, and 2 unknown severity entries.
- NVD day-to-date intake: 9 CVEs on 2026-06-03 through 02:35 UTC: 0 critical, 0 high, 3 medium, 4 low, and 2 unknown.
- NVD rolling 24 hour context: 223 CVEs, including 14 critical, 76 high, 89 medium, 24 low, and 20 unknown severity entries.
- Critical/high enterprise priorities from the rolling window: Progress Sitefinity CVE-2026-7312/CVE-2026-7198, Kirki WordPress CVE-2026-8206, authentik CVE-2026-49448/CVE-2026-42849, LibreChat CVE-2026-32625, OpenMed CVE-2026-47117, OpenClaude CVE-2026-42074, Spacelabs Sentinel CVE-2026-0611, React Router CVE-2026-42211, and Amazon Kiro IDE CVE-2026-10591.
- Confirmed active exploitation/KEV priorities: Cisco Catalyst SD-WAN CVE-2026-20182, cPanel/WHM CVE-2026-41940, FortiClient EMS CVE-2026-35616, Citrix NetScaler CVE-2026-3055, LiteSpeed cPanel plugin CVE-2026-48172, Drupal Core CVE-2026-9082, Android Framework CVE-2025-48595, and Linux Kernel cgroups CVE-2022-0492.
- Malware/threat activity: Arctic Wolf reports EKZ Infostealer delivery through exploited FortiClient EMS; SANS ISC reports SVG phishing using `application/ecmascript` MIME evasion and NetSupport RAT activity; MalwareBazaar showed 212 submissions in the past 24 hours with Mirai as the most seen family.

## Source Coverage and Collection Notes

- NVD CVE API was queried for current-hour, day-to-date, and rolling 24 hour windows.
- CISA KEV JSON catalog version 2026.06.02 was queried directly. Latest KEV additions remain CVE-2022-0492 and CVE-2025-48595, both due 2026-06-05.
- GitHub Security Advisories API returned no advisories newly published after 2026-06-03 01:00 UTC in this run.
- GitHub repository search for `CVE-2026 PoC exploit pushed:>=2026-06-03` returned 7 unvalidated repositories pushed today; none were cloned or executed.
- ExploitDB direct CSV latest entries remained dated 2026-06-01: Drupal Core CVE-2026-9082 EDB-ID 52608 and WordPress OrderConvo CVE-2025-10162 EDB-ID 52607. No 2026-06-03 row was observed.
- Sploitus homepage fetch exposed only the search UI and did not provide a static "Exploits of the Week" block. The Sploitus Top 10 below is reconstructed from indexed Sploitus pages and targeted searches.
- VX-Underground GitHub repositories showed no new push after `vxunderground/MalwareSourceCode` on 2026-05-30; latest MalwareSourceCode commit observed was `1623926` adding uploaded files.

## Top Vulnerabilities

### 1. Cisco Catalyst SD-WAN Controller/Manager authentication bypass - CVE-2026-20182

- Severity: Critical; CVSS 10.0; CISA KEV listed.
- Affected software: Cisco Catalyst SD-WAN Controller and Manager/vSmart/vManage fixed releases listed by Cisco.
- Exploit availability: Public exploit material exists; Rapid7 describes exploitation mechanics and Sploitus indexes a PoC/Metasploit-style workflow.
- Active exploitation: Confirmed. Cisco PSIRT states limited exploitation was observed in May 2026.
- Recommended action: Upgrade control components immediately, collect admin-tech bundles before upgrade where possible, preserve auth/control logs, check for unauthorized `vmanage-admin` SSH keys and NETCONF activity, and open Cisco TAC cases for suspicious systems.
- Confidence: High.
- Sources: Cisco PSIRT, CISA KEV, Rapid7, Sploitus.

### 2. cPanel & WHM authentication bypass/RCE - CVE-2026-41940

- Severity: Critical; CVSS 9.8; CISA KEV listed with known ransomware campaign use.
- Affected software: WebPros cPanel & WHM and WP2.
- Exploit availability: Public Metasploit module and public technical exploit details are available; GitHub PoC indicators were pushed today.
- Active exploitation: Confirmed by CISA KEV and multiple security reports; reporting links exploitation to Sorry ransomware/Mirai-style follow-on activity.
- Recommended action: Patch cPanel branches immediately, restrict ports 2083/2087 to trusted access paths, inspect WHM session files and access logs, hunt for web shells/backdoors and `.sorry` encrypted files, and rotate panel/root credentials after compromise assessment.
- Confidence: High.
- Sources: CISA KEV, Rapid7, cPanel/WebPros advisory, ExploitDB/Metasploit indicators.

### 3. Fortinet FortiClient EMS improper access control - CVE-2026-35616

- Severity: Critical; CVSS 9.1; CISA KEV listed.
- Affected software: FortiClient EMS 7.4.5 and 7.4.6.
- Exploit availability: Public technical analysis and scanner/exploit discussions exist; NVD references Fortinet and KEV.
- Active exploitation: Confirmed. watchTowr reported zero-day exploitation; Arctic Wolf observed exploitation delivering EKZ Infostealer disguised as a Fortinet endpoint patch.
- Recommended action: Apply Fortinet hotfixes or upgrade to 7.4.7+, restrict EMS management exposure, review Remote Access Profiles and endpoint policies for malicious scripts, and hunt for `FortiEndpoint_Patch.exe`, `p.exe`, `Certificate not found in request header`, unexpected `fortinet-ca2` certificate changes, and HTTP exfiltration to suspicious VPS infrastructure.
- Confidence: High.
- Sources: Fortinet PSIRT, NVD, CISA KEV, Arctic Wolf, watchTowr, Bishop Fox.

### 4. Citrix NetScaler ADC/Gateway SAML IdP memory overread - CVE-2026-3055

- Severity: Critical; CVSS v4.0 9.3; CISA KEV listed.
- Affected software: Customer-managed NetScaler ADC/Gateway configured as SAML Identity Provider.
- Exploit availability: Public technical analysis and Metasploit indicator are available; FortiGuard reports persistent global probing/exploitation attempts.
- Active exploitation: Confirmed by KEV and FortiGuard/Rapid7 updates.
- Recommended action: Patch to fixed NetScaler builds, check configuration for `add authentication samlIdPProfile`, terminate sessions after patching, rotate SAML keys/credentials if exposure is suspected, and hunt `/saml/login` and `/wsfed/passive` anomalies.
- Confidence: High.
- Sources: Citrix advisory CTX696300, CISA KEV, FortiGuard outbreak alert, Rapid7.

### 5. LiteSpeed user-end cPanel plugin root privilege escalation - CVE-2026-48172

- Severity: Critical; CVSS v4 10.0 in secondary scoring and CVSS v3.1 8.8/9.8 in other references; CISA KEV listed.
- Affected software: LiteSpeed user-end cPanel plugin versions 2.3 through 2.4.4.
- Exploit availability: Vendor-confirmed exploitability through `lsws.redisAble`; public technical analyses exist.
- Active exploitation: Confirmed by LiteSpeed vendor blog.
- Recommended action: Upgrade to LiteSpeed WHM Plugin 5.3.1.0+ bundled with cPanel plugin 2.4.7+, or uninstall the user-end plugin if patching is not possible. Search logs with `grep -rE "cpanel_jsonapi_func=redisAble" /var/cpanel/logs /usr/local/cpanel/logs/ 2>/dev/null` and assess affected shared-hosting tenants for root-level tampering.
- Confidence: High.
- Sources: LiteSpeed vendor blog, CISA KEV, CyCognito, HivePro.

### 6. Drupal Core PostgreSQL JSON:API SQL injection - CVE-2026-9082

- Severity: CISA KEV listed; Drupal labels the issue highly critical for affected PostgreSQL-backed sites.
- Affected software: Drupal 8.9.0 through 11.3.9 branches before fixed releases when using PostgreSQL.
- Exploit availability: ExploitDB EDB-ID 52608 and Sploitus exploit page are available.
- Active exploitation: Confirmed by KEV and CrowdSec tracking.
- Recommended action: Upgrade to fixed Drupal branch release, verify database backend, prioritize public `/jsonapi/` endpoints, and hunt for malformed JSON:API filter parameter keys and unusual PostgreSQL query errors.
- Confidence: High.
- Sources: Drupal advisory, CISA KEV, ExploitDB, Sploitus, CrowdSec.

### 7. Kirki WordPress account takeover - CVE-2026-8206

- Severity: Critical; CVSS 9.8 in NVD.
- Affected software: Kirki plugin 6.0.0 through 6.0.6; fixed in 6.0.7.
- Exploit availability: Public attack details and GitHub/Sploitus-style indicators exist; functional safety of repositories remains unvalidated.
- Active exploitation: Confirmed by Wordfence/Defiant reporting via BleepingComputer; Wordfence blocked more than 222 attempts in 24 hours.
- Recommended action: Upgrade to 6.0.7+, disable vulnerable plugin where patching is delayed, reset credentials for privileged accounts if exposed, and review password reset email changes and new admin users.
- Confidence: High for exploitation and vulnerability; Low for safety/functionality of public PoC repositories.
- Sources: NVD, Wordfence/Defiant via BleepingComputer, WordPress plugin trac, Tenable.

### 8. Android Framework integer overflow - CVE-2025-48595

- Severity: High; CISA KEV listed.
- Affected software: Android Framework on Android 14, 15, 16, and 16-QPR2.
- Exploit availability: No public PoC confirmed in this run.
- Active exploitation: Confirmed by CISA KEV. Android June bulletin includes it in the June patch set.
- Recommended action: Move managed Android fleets to 2026-06-05 security patch level or later, prioritizing high-risk users and devices outside managed app stores.
- Confidence: High.
- Sources: CISA KEV, Android Security Bulletin June 2026.

### 9. Linux Kernel cgroups v1 release_agent privilege escalation/container escape - CVE-2022-0492

- Severity: High; CVSS 7.8; CISA KEV listed on 2026-06-02.
- Affected software: Linux kernel cgroups v1 release_agent feature, especially risky in permissive or privileged containers.
- Exploit availability: Public exploit knowledge has existed since 2022; KEV addition renews urgency.
- Active exploitation: Confirmed by KEV listing; current public campaign details remain limited.
- Recommended action: Patch kernels, disable/constrain cgroup v1, block privileged containers, enforce seccomp/AppArmor/SELinux, and hunt for unexpected writes to `release_agent` and container escape artifacts.
- Confidence: High for KEV; Medium for current campaign details.
- Sources: CISA KEV, Linux kernel commit, NVD.

### 10. NGINX Rift heap buffer overflow - CVE-2026-42945

- Severity: Critical; CVSS v4.0 9.2.
- Affected software: NGINX Open Source 0.6.27 through 1.30.0, NGINX Plus R32 through R36, and multiple F5/NGINX downstream products.
- Exploit availability: Public DepthFirst proof-of-concept and Sploitus-indexed exploit pages exist.
- Active exploitation: Not confirmed in this run.
- Recommended action: Upgrade NGINX OSS to 1.30.1/1.31.0 or NGINX Plus fixed builds; restart workers. If patching is delayed, replace vulnerable unnamed PCRE captures (`$1`, `$2`) in rewrite chains containing `?` with named captures.
- Confidence: High for vulnerability and PoC; Medium for broad applicability because vulnerable configuration patterns must be present.
- Sources: DepthFirst, Sploitus, Axonius, F5/NGINX reporting.

## Newly Published Current-Hour CVEs

| CVE | Severity | Affected software | Exploit/PoC signal | Action |
| --- | --- | --- | --- | --- |
| CVE-2026-10693 | Low, CVSS 2.1 | SourceCodester Online Boat Reservation System 1.0 administrative endpoint | NVD/VulDB state exploit disclosed; public Medium writeup reference | Treat as low priority unless deployed; restrict admin endpoints and apply vendor/community fix if available. |
| CVE-2026-10694 | Medium, CVSS 5.5 | SourceCodester Online Food Ordering System 2.0 `/index.php?page=` include handling | NVD says public exploit may be used; GitHub issue reference exists | Validate exposure, remove public access if deployed, and patch/replace application; monitor for LFI/file inclusion probes. |
| CVE-2026-9334 | Unknown in NVD at collection time | Cpanel::JSON::XS before 4.41 | Patch commit and MetaCPAN change reference; no exploitation observed | Upgrade Perl module to 4.41+ where `dupkeys_as_arrayref` may parse untrusted JSON. |
| CVE-2026-9516 | Unknown in NVD at collection time | Cpanel::JSON::XS before 4.41 | Patch commit and MetaCPAN change reference; no exploitation observed | Upgrade Perl module to 4.41+ where decode filters parse untrusted BOM-prefixed JSON. |

## Exploits Released

### Sploitus Top 10 (reconstructed)

Sploitus homepage did not expose an "Exploits of the Week" list in static fetch. The following top 10 are reconstructed from indexed Sploitus pages, direct search results, and enterprise relevance. Treat these as exploit intelligence indicators, not as validated safe tools.

| Rank | CVE/Item | Affected software | Exploit type | Maturity | PoC availability | Weaponization potential |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | CVE-2026-20182 | Cisco Catalyst SD-WAN Controller/Manager | Unauthenticated control-plane auth bypass with SSH key/NETCONF access | Public technical analysis plus Sploitus/Metasploit indicator | Yes | Critical: internet-exposed SD-WAN control-plane compromise. |
| 2 | CVE-2026-41940 | cPanel & WHM/WP2 | CRLF session injection auth bypass to root WHM/RCE | Metasploit module, public analysis, GitHub PoC indicators | Yes | Critical: mass hosting compromise and ransomware linkage. |
| 3 | CVE-2026-9082 | Drupal Core on PostgreSQL | Unauthenticated JSON:API SQL injection | ExploitDB 52608 and Sploitus page | Yes | High: public websites and rapid KEV exploitation. |
| 4 | CVE-2026-3055 | Citrix NetScaler ADC/Gateway | SAML IdP memory overread/session material leakage | Public technical analysis and Metasploit indicator | Yes | Critical for identity perimeter appliances. |
| 5 | CVE-2026-42945 | NGINX / F5 NGINX products | Heap buffer overflow/RCE/DoS in rewrite module | DepthFirst PoC, Sploitus, GitHub repos | Yes | High: edge infrastructure; requires vulnerable rewrite configuration. |
| 6 | CVE-2026-48172 | LiteSpeed user-end cPanel plugin | Authenticated cPanel user to root command execution | Vendor-confirmed exploitation; public analyses | Yes | Critical in shared-hosting environments. |
| 7 | CVE-2026-8206 | Kirki WordPress plugin | Unauthenticated password-reset account takeover | Active exploitation reports and GitHub/Sploitus indicators | Yes | High due WordPress install base and admin takeover impact. |
| 8 | CVE-2026-21858 | n8n | Content-type confusion/session forgery/RCE claim | Sploitus-indexed reconstruction | Unvalidated | High if real, but confidence remains low pending vendor/source validation. |
| 9 | CVE-2026-21509 | Microsoft Office OLE claim | Speculative OLE bypass claim | Sploitus-indexed text appears suspicious | Unvalidated | Medium: likely noisy/untrusted; do not treat as functional without validation. |
| 10 | CVE-2026-5718 / CVE-2026-2144 | Misc indexed CVEs | Generic exploit listings | Indexed only | Unvalidated | Medium to low until affected product and code provenance are verified. |

### ExploitDB additions

- Latest direct ExploitDB CSV rows remained dated 2026-06-01; no direct CSV row dated 2026-06-03 was observed.
- EDB-ID 52608: Drupal Core 10.5.5 error-based SQL injection, CVE-2026-9082, unverified.
- EDB-ID 52607: WordPress OrderConvo 14 path traversal, CVE-2025-10162, unverified.
- Other recent rows include YAMCS yamcs-core LDAP injection/no-rate-limit/user enumeration, Notepad++ arbitrary code execution, and Linux kernel local privilege escalation entries from 2026-05-29/30.

### New GitHub PoC indicators

Strict created-today search did not surface validated new repositories. Broader pushed-today search returned these unvalidated indicators:

- `Defacto-ridgepole254/CVE-2026-41940-Exploit-PoC` - cPanel/WHM auth bypass PoC claim; pushed 2026-06-03 00:48 UTC.
- `Dullpurple-sloop726/CVE-2026-31431-Linux-Copy-Fail` - Linux LPE claim; pushed 2026-06-03 00:48 UTC.
- `Liverwortenuresis371/copyfail-rs` - CVE-2026-31431 exploit/detection claim; pushed 2026-06-03 00:47 UTC.
- `Jumpthereness578/CVE-2026-2991` - KiviCare auth bypass PoC claim; pushed 2026-06-03 00:28 UTC.
- `Recorded-texteditor120/CVE-2026-31802` - npm tar path traversal PoC claim; pushed 2026-06-03 00:25 UTC.
- `fartlover37/CVE-2026-2441-PoC` - Chrome Blink CSS UAF PoC claim; pushed 2026-06-03 00:07 UTC.
- `hamzamalik3461/CVE-2026-20841` - Windows Notepad RCE claim; pushed 2026-06-03 00:05 UTC.

These repositories were not executed or cloned. Treat them as hostile until reviewed in an isolated environment.

## Malware Intelligence

- FortiClient EMS/EKZ Infostealer: Arctic Wolf observed CVE-2026-35616 exploitation to modify EMS policy/profile behavior and deploy `FortiEndpoint_Patch.exe`/`p.exe`, a browser credential stealer that exfiltrates over HTTP. Confidence: High.
- MalwareBazaar: Browse page showed 212 submissions in the past 24 hours; Mirai was the most seen malware family. Confidence: High for feed observation.
- SANS ISC SVG phishing: Current SANS front page/stormcast and diary coverage highlight SVG phishing attachments containing script and the `application/ecmascript` MIME type to evade simplistic JavaScript detection. Confidence: High.
- SANS ISC NetSupport RAT: SANS documented a SmartApeSG/ClickFix infection chain leading to NetSupport RAT persistence and C2 infrastructure including `185.163.47[.]217:443`. Confidence: High.
- VX-Underground GitHub: Latest pushed repository remained `vxunderground/MalwareSourceCode` on 2026-05-30; no new VX GitHub push was observed in this run. Confidence: Medium.

## Security Releases and Advisories

- Microsoft: No new MSRC item was validated during the 01:00-02:35 UTC collection window. Continue tracking Netlogon/SharePoint-related June 2026 exploitation claims only where primary or high-confidence sources corroborate them.
- Cisco: Cisco PSIRT advisory for CVE-2026-20182 remains a top emergency item. No workaround; fixed releases and IOC guidance are published.
- Fortinet: FortiClient EMS CVE-2026-35616 remains actively exploited and KEV-listed; hotfixes/7.4.7+ are required, and EKZ Infostealer hunting is recommended.
- Citrix/NetScaler: CTX696300 fixes CVE-2026-3055/CVE-2026-4368; active exploitation against SAML IdP configurations is confirmed by KEV/FortiGuard updates.
- Google/Android: June 2026 Android bulletin fixes CVE-2025-48595 and numerous critical/high Framework/System/driver issues; deploy 2026-06-05 patch level or later.
- Progress: Sitefinity advisory addresses CVE-2026-7312, CVE-2026-7198, CVE-2026-7195, CVE-2026-7201, and CVE-2026-7313.
- GitHub/GitHub Advisory Database: No advisories newly published after 01:00 UTC via API. Rolling 24 hour NVD/GHSA context includes authentik, LibreChat, Mint/Tesla, React Router, OpenTelemetry eBPF, NiceGUI, and GLPI advisories.
- GitLab: No June 3 security release was validated in this run; keep prior May 27 security patch set in standard remediation tracking.
- Docker Desktop: Rolling 24 hour NVD includes CVE-2026-8936 fixed in Docker Desktop 4.76.0.
- LiteSpeed: Vendor blog confirms CVE-2026-48172 active exploitation and patched cPanel plugin 2.4.7 / WHM plugin 5.3.1.0.
- Cpanel::JSON::XS: Version 4.41 addresses CVE-2026-9334 and CVE-2026-9516.

## Recommended Actions

1. Emergency patch and hunt Cisco Catalyst SD-WAN CVE-2026-20182; preserve logs/admin-tech and validate unauthorized peering/NETCONF/SSH-key activity.
2. Emergency patch and compromise-assess cPanel/WHM CVE-2026-41940 and LiteSpeed cPanel CVE-2026-48172; inspect hosting nodes for ransomware, web shells, malicious users, and root-level persistence.
3. Patch FortiClient EMS CVE-2026-35616 and hunt EKZ Infostealer artifacts and malicious EMS configuration/profile/script changes.
4. Patch Citrix NetScaler CVE-2026-3055, terminate sessions, and rotate credentials/keys where memory disclosure is suspected.
5. Patch Drupal PostgreSQL-backed sites for CVE-2026-9082 and inspect JSON:API/PostgreSQL logs for exploitation attempts.
6. Upgrade Kirki to 6.0.7+ or disable it; review WordPress admin accounts and password reset telemetry.
7. Deploy Android June 2026 patch level 2026-06-05+ to managed Android fleets.
8. Review Linux container hosts for cgroup v1 exposure to CVE-2022-0492; patch kernels and enforce container isolation controls.
9. Patch high-impact rolling 24 hour advisories where present: Progress Sitefinity, authentik, LibreChat, OpenMed, Spacelabs Sentinel, React Router, OpenShift, Kiro IDE, Docker Desktop, and Cpanel::JSON::XS.
10. Block or detonate SVG email attachments with embedded script; ensure detections include `application/ecmascript`, `application/javascript`, and `text/javascript`.
11. Treat all public PoC repositories discovered today as hostile until manually reviewed in a sandbox.

## Unified Vulnerability Records

```json
[
  {
    "cve": "CVE-2026-20182",
    "cvss": "10.0",
    "vendor": "Cisco",
    "product": "Catalyst SD-WAN Controller/Manager",
    "affected_versions": "Cisco Catalyst SD-WAN control components before the fixed releases listed in Cisco advisory cisco-sa-sdwan-rpa2-v69WY2SW",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://sploitus.com/exploit?id=13DF22F3-E9C6-58EE-B458-EB585C4D715D",
      "https://www.rapid7.com/blog/post/ve-cve-2026-20182-critical-authentication-bypass-cisco-catalyst-sd-wan-controller-fixed/"
    ],
    "patch_available": true,
    "sources": [
      "Cisco PSIRT",
      "CISA KEV",
      "Rapid7",
      "Sploitus"
    ]
  },
  {
    "cve": "CVE-2026-41940",
    "cvss": "9.8",
    "vendor": "WebPros",
    "product": "cPanel & WHM / WP2",
    "affected_versions": "cPanel & WHM versions after 11.40 before branch-specific emergency fixes; WP2 before 136.1.7",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://www.rapid7.com/db/modules/exploit/multi/http/cpanel_whm_auth_bypass_rce/",
      "https://www.rapid7.com/blog/post/etr-cve-2026-41940-cpanel-whm-authentication-bypass/"
    ],
    "patch_available": true,
    "sources": [
      "CISA KEV",
      "Rapid7",
      "cPanel/WebPros advisory",
      "ExploitDB/Metasploit indicators"
    ]
  },
  {
    "cve": "CVE-2026-35616",
    "cvss": "9.1",
    "vendor": "Fortinet",
    "product": "FortiClient EMS",
    "affected_versions": "FortiClient EMS 7.4.5 and 7.4.6",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://watchtowr.com/resources/fortinet-forticlient-ems-zero-day-cve-2026-35616-active-exploitation-underway/",
      "https://bishopfox.com/blog/api-authentication-bypass-in-forticlient-ems-7-4-5-7-4-6-cve-2026-35616"
    ],
    "patch_available": true,
    "sources": [
      "Fortinet PSIRT",
      "NVD",
      "CISA KEV",
      "Arctic Wolf",
      "watchTowr",
      "Bishop Fox"
    ]
  },
  {
    "cve": "CVE-2026-3055",
    "cvss": "9.3",
    "vendor": "Citrix / Cloud Software Group",
    "product": "NetScaler ADC and NetScaler Gateway",
    "affected_versions": "Customer-managed NetScaler ADC/Gateway 14.1 before 14.1-66.59 or 14.1-60.58, 13.1 before 13.1-62.23, 13.1-FIPS/NDcPP before 13.1-37.262 when configured as SAML IdP",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://support.citrix.com/external/article/CTX696300",
      "https://www.rapid7.com/blog/post/etr-cve-2026-3055-citrix-netscaler-adc-and-netscaler-gateway-out-of-bounds-read/"
    ],
    "patch_available": true,
    "sources": [
      "Citrix advisory",
      "CISA KEV",
      "FortiGuard outbreak alert",
      "Rapid7"
    ]
  },
  {
    "cve": "CVE-2026-48172",
    "cvss": "10.0/8.8 depending on scoring source",
    "vendor": "LiteSpeed Technologies",
    "product": "LiteSpeed user-end cPanel plugin",
    "affected_versions": "cPanel user-end plugin 2.3 through 2.4.4; upgrade to cPanel plugin 2.4.7 bundled with WHM plugin 5.3.1.0 or later",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://blog.litespeedtech.com/2026/05/21/security-update-for-litespeed-cpanel-plugin/"
    ],
    "patch_available": true,
    "sources": [
      "LiteSpeed vendor blog",
      "CISA KEV",
      "CyCognito",
      "HivePro"
    ]
  },
  {
    "cve": "CVE-2026-9082",
    "cvss": "6.5/Highly critical per Drupal advisory context",
    "vendor": "Drupal",
    "product": "Drupal Core JSON:API on PostgreSQL",
    "affected_versions": "Drupal 8.9.0 before 10.4.10, 10.5.x before 10.5.10, 10.6.x before 10.6.9, 11.0.x before 11.1.10, 11.2.x before 11.2.12, 11.3.x before 11.3.10 when PostgreSQL-backed",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://sploitus.com/exploit?id=1774D6F8-2B0F-5C66-A7AB-BE7B8E7A0B85",
      "https://www.crowdsec.net/vulntracking-report/cve-2026-9082-drupal-jsonapi-sql-injection"
    ],
    "patch_available": true,
    "sources": [
      "Drupal advisory",
      "CISA KEV",
      "ExploitDB 52608",
      "Sploitus",
      "CrowdSec"
    ]
  },
  {
    "cve": "CVE-2025-48595",
    "cvss": "High",
    "vendor": "Google / Android",
    "product": "Android Framework",
    "affected_versions": "Android 14, 15, 16, and 16-QPR2 before June 2026 patch levels",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "Android Security Bulletin June 2026",
      "CISA KEV"
    ]
  },
  {
    "cve": "CVE-2022-0492",
    "cvss": "7.8",
    "vendor": "Linux",
    "product": "Linux Kernel cgroups v1 release_agent",
    "affected_versions": "Linux kernel configurations exposing unsafe cgroups v1 release_agent behavior; especially risky in permissive container environments",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=24f6008564183aa120d07c03d9289519c2fe02af"
    ],
    "patch_available": true,
    "sources": [
      "CISA KEV",
      "Linux kernel commit",
      "NVD"
    ]
  },
  {
    "cve": "CVE-2026-8206",
    "cvss": "9.8",
    "vendor": "WordPress plugin ecosystem / Kirki",
    "product": "Kirki Freeform Page Builder, Website Builder & Customizer",
    "affected_versions": "Kirki 6.0.0 through 6.0.6; fixed in 6.0.7",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": false,
    "poc_links": [
      "https://www.bleepingcomputer.com/news/security/critical-kirki-flaw-exploited-to-hijack-wordpress-admin-accounts/"
    ],
    "patch_available": true,
    "sources": [
      "NVD",
      "Wordfence/Defiant via BleepingComputer",
      "WordPress plugin trac",
      "Tenable"
    ]
  },
  {
    "cve": "CVE-2026-42945",
    "cvss": "9.2",
    "vendor": "F5 / NGINX",
    "product": "NGINX Open Source, NGINX Plus, and downstream NGINX products",
    "affected_versions": "NGINX Open Source 0.6.27 through 1.30.0; NGINX Plus R32 through R36; selected F5 NGINX WAF/Ingress/Gateway products",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/DepthFirstDisclosures/Nginx-Rift/blob/main/README.md",
      "https://depthfirst.com/nginx-rift",
      "https://sploitus.com/exploit?id=5D544171-289B-5AF6-90DF-2C2B919DE93C"
    ],
    "patch_available": true,
    "sources": [
      "DepthFirst",
      "F5/NGINX reporting",
      "Sploitus",
      "Axonius"
    ]
  },
  {
    "cve": "CVE-2026-7312",
    "cvss": "10.0",
    "vendor": "Progress",
    "product": "Sitefinity",
    "affected_versions": "Progress Sitefinity 14.0.7700 to 14.4.8152, 15.0.8200 to 15.0.8234, 15.1.8300 to 15.1.8335, 15.2.8400 to 15.2.8441, 15.3.8500 to 15.3.8531, and 15.4.8600 to 15.4.8630",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "NVD",
      "Progress Sitefinity advisory"
    ]
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
    "poc_links": [
      "https://github.com/goauthentik/authentik/security/advisories/GHSA-xp7f-xjjx-gwm8"
    ],
    "patch_available": true,
    "sources": [
      "NVD",
      "GitHub Security Advisory"
    ]
  },
  {
    "cve": "CVE-2026-32625",
    "cvss": "9.6",
    "vendor": "LibreChat",
    "product": "LibreChat MCP server integration",
    "affected_versions": "LibreChat up to and including 0.8.3",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/danny-avila/LibreChat/security/advisories/GHSA-4pcc-j6m6-wcwx"
    ],
    "patch_available": true,
    "sources": [
      "NVD",
      "GitHub Security Advisory"
    ]
  },
  {
    "cve": "CVE-2026-10694",
    "cvss": "5.5",
    "vendor": "SourceCodester",
    "product": "Online Food Ordering System 2.0",
    "affected_versions": "Version 2.0 / index.php page include handling per NVD/VulDB",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/Mikkoseven/cve/issues/4"
    ],
    "patch_available": false,
    "sources": [
      "NVD",
      "VulDB",
      "GitHub issue"
    ]
  },
  {
    "cve": "CVE-2026-9334",
    "cvss": "Unknown in NVD at collection time",
    "vendor": "Cpanel::JSON::XS",
    "product": "Cpanel::JSON::XS Perl module",
    "affected_versions": "Before 4.41 when dupkeys_as_arrayref is enabled",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "NVD",
      "Cpanel::JSON::XS commit",
      "MetaCPAN changes"
    ]
  },
  {
    "cve": "CVE-2026-9516",
    "cvss": "Unknown in NVD at collection time",
    "vendor": "Cpanel::JSON::XS",
    "product": "Cpanel::JSON::XS Perl module",
    "affected_versions": "Before 4.41 when UTF-8 BOM-prefixed input and decode filter callback exception handling are reachable",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "NVD",
      "Cpanel::JSON::XS commit",
      "MetaCPAN changes"
    ]
  }
]
```
