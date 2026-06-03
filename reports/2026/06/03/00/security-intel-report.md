# Hourly Security Intelligence Report - 2026-06-03 00:03 UTC

## Report Metadata

- Automation trigger: cron, 2026-06-03 00:02 UTC
- Repository verified: `dfalt0/Test-cursor-security-automation`
- Branch: `cursor/security-intelligence-agent-c981`
- Report path: `reports/2026/06/03/00/security-intel-report.md`
- Collection window emphasized: 2026-06-02 23:00-2026-06-03 00:35 UTC, with June 2 day-end and carry-forward exploitation context
- Confidence model: High = primary source or multiple authoritative sources; Medium = primary source plus unvalidated exploit/search indicator; Low = single secondary/indexed signal only

## Executive Summary

- Total CVEs discovered in the current NVD window: 16 (1 Critical, 4 High, 4 Medium, 4 Low, 3 Unknown/unscored).
- June 3 day-to-date NVD volume at collection time: 0 CVEs. The current-hour records were published late on June 2 and are included in this 00 UTC report because they fall in the cross-midnight window.
- June 2 final NVD volume observed in this run: 225 CVEs (14 Critical, 76 High, 88 Medium, 29 Low, 18 Unknown).
- Current-hour critical finding: CVE-2026-32625 in LibreChat MCP server URL handling, allowing low-privileged authenticated users to exfiltrate server secrets such as `JWT_SECRET`, `CREDS_KEY`, and `CREDS_IV`; GitHub advisory includes a PoC and patched version v0.8.4-rc1.
- Highest current-hour enterprise/dev-tool risks: LibreChat CVE-2026-32625, LibreChat CVE-2026-31942/CVE-2026-44653, alf.io CVE-2026-35482/CVE-2026-41412, QloApps CVE-2026-25861, GLPI CVE-2026-40108, and Go CVE-2026-27145/CVE-2026-42504/CVE-2026-42507 fixed in Go 1.26.4 and 1.25.11.
- Active exploitation findings: CISA KEV remains catalog version 2026.06.02 with June 2 additions CVE-2022-0492 (Linux kernel cgroups v1 release_agent privilege escalation/container escape) and CVE-2025-48595 (Android Framework integer overflow/code execution/local privilege escalation), both due 2026-06-05. Carry-forward active/public-exploit priorities include Drupal CVE-2026-9082, cPanel CVE-2026-41940, Palo Alto PAN-OS CVE-2026-0257, Oracle WebLogic CVE-2024-21182, Microsoft Defender CVE-2026-41091, and Citrix NetScaler CVE-2026-3055 where applicable.
- New malware/campaign intelligence: MalwareBazaar reports 231 submissions in the past 24 hours with Mirai as the most-seen family; SANS ISC reports a phishing wave using SVG attachments with embedded JavaScript and `application/ecmascript` MIME labeling to evade simple attachment scanning.
- Exploit-release intelligence: Sploitus homepage static fetch still exposes only the search UI, so the Sploitus top-10 below is reconstructed from indexed Sploitus exploit pages and should be treated as exploit-reference intelligence, not proof that every repository is functional or safe.

## Top Vulnerabilities

| Priority | CVE | Severity | Affected software | Exploit availability | Active exploitation | Confidence | Recommended action |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | CVE-2026-32625 | Critical, 9.6 | LibreChat MCP server integration <= 0.8.3 | Public advisory PoC | No confirmed exploitation | High | Upgrade LibreChat to v0.8.4-rc1 or later; disable user-created MCP servers until patched; rotate JWT and credential-encryption secrets if exposed. |
| 2 | CVE-2022-0492 | KEV / High | Linux kernel cgroups v1 `release_agent` | Historical public exploit material exists | Yes - CISA KEV | High | Patch kernels, restrict privileged containers and cgroup v1 host mounts, and hunt for container escape attempts. |
| 3 | CVE-2025-48595 | KEV | Android Framework | No public PoC found in this run | Yes - CISA KEV | High | Apply June 2026 Android security bulletin updates across managed/mobile fleets before the 2026-06-05 KEV due date. |
| 4 | CVE-2026-35482 | High, 8.0 | alf.io before 2.0-M5-2606 | Public GitHub advisory PoC | No confirmed exploitation | High | Upgrade to 2.0-M5-2606; review admin extension access and server-side script execution logs. |
| 5 | CVE-2026-25861 | High, 8.2 | QloApps through 1.7.0 | Patch commit and VulnCheck advisory; no exploit seen | No | High | Apply commit 64e9722 or vendor release; reset/re-hash credentials if password-hash compromise is plausible. |
| 6 | CVE-2026-31942 | High, 7.1 | LibreChat API keys endpoint <= 0.7.6 | Public advisory PoC | No confirmed exploitation | High | Upgrade LibreChat to 0.8.3-rc1+ and audit API-key updates for unexpected userId overrides. |
| 7 | CVE-2026-40108 | High, 7.1 | GLPI 11.0.0 through 11.0.6 | Public advisory, no weaponized PoC observed | No | High | Upgrade GLPI to 11.0.7; review technician-created ITIL cost records for stored XSS payloads. |
| 8 | CVE-2026-27145 / CVE-2026-42504 / CVE-2026-42507 | Unscored in NVD; security release | Go crypto/x509, mime, net/textproto | No exploit found | No | High | Update build images and developer toolchains to Go 1.26.4 or 1.25.11; rebuild affected services. |
| 9 | CVE-2026-41412 | Medium, 4.9 | alf.io before 2.0-M5-2606 | Public advisory PoC | No confirmed exploitation | High | Upgrade to 2.0-M5-2606; restrict extension authors and egress from alf.io servers. |
| 10 | CVE-2026-44653 | Medium, 6.5 | LibreChat v0.8.3 shared MCP server views | Public advisory PoC | No confirmed exploitation | High | Upgrade to v0.8.4 and verify MCP API responses redact admin-managed secrets. |

## Current-Hour NVD Additions

NVD current window: 2026-06-02T23:00:00.000 through 2026-06-03T00:35:00.000 returned 16 records: 1 Critical, 4 High, 4 Medium, 4 Low, and 3 Unknown/unscored.

| CVE | Severity | Summary | Primary/current sources |
| --- | --- | --- | --- |
| CVE-2026-10662 | Low 2.1 | blender-mcp ZIP File Handler `zip_file_url` handling can trigger SSRF-like behavior via `requests.get`. | NVD, GitHub issue #203, PR #205, VulDB |
| CVE-2026-10688 | Low 2.0 | blender-mcp `execute_blender_code` argument handling issue categorized as code injection but scored low due local/low-impact constraints. | NVD, GitHub issue #201, VulDB |
| CVE-2026-10717 | Low 1.8 | Seagate openSeaChest `--showSCSIDefects` out-of-bounds read/write with malicious or pathological SCSI defect data. | NVD, Seagate product security page |
| CVE-2026-10718 | Medium 4.6 | Seagate openSeaChest Trim/Unmap operation out-of-bounds write. | NVD, Seagate product security page |
| CVE-2026-10719 | Low 1.8 | Seagate openSeaChest `--showSupportedFormats` one-byte out-of-bounds write via malicious NVMe namespace data. | NVD, Seagate product security page |
| CVE-2026-25861 | High 8.2 | QloApps through 1.7.0 uses weak MD5-based password hashing with static key material, enabling credential compromise if hashes are exposed. | NVD, QloApps commit/pull request, VulnCheck |
| CVE-2026-27145 | Unknown | Go `crypto/x509` hostname verification could scale quadratically with large DNS SAN lists. | NVD, Go issue 79694, Go 1.26.4/1.25.11 release notes |
| CVE-2026-31942 | High 7.1 | LibreChat IDOR in `PUT /api/keys` lets authenticated users overwrite other users' API keys by injecting `userId`. | NVD, GitHub Security Advisory GHSA-5jcj-rh68-cgj7 |
| CVE-2026-32625 | Critical 9.6 | LibreChat MCP server URL validation expands `${VAR}` placeholders from `process.env` and immediately connects to attacker-controlled URLs, leaking server secrets. | NVD, GitHub Security Advisory GHSA-4pcc-j6m6-wcwx |
| CVE-2026-35482 | High 8.0 | alf.io extension script sandbox escape through injected unrestricted Java `Class` object enables authenticated administrator RCE. | NVD, GitHub Security Advisory GHSA-3w8f-mcf6-cm7h |
| CVE-2026-40108 | High 7.1 | GLPI 11.0.0-11.0.6 technician-stored XSS in ITIL costs. | NVD, GitHub Security Advisory GHSA-rhmv-j773-4gvh |
| CVE-2026-41412 | Medium 4.9 | alf.io `simpleHttpClient.postFileAndSaveResponse()` lets extension scripts read arbitrary local files and exfiltrate them. | NVD, GitHub Security Advisory GHSA-6m62-53cw-4373 |
| CVE-2026-42504 | Unknown | Go `mime` header decoding of malicious encoded words can consume excessive CPU. | NVD, Go issue 79217, Go 1.26.4/1.25.11 release notes |
| CVE-2026-42507 | Unknown | Go `net/textproto` errors can include attacker-controlled input and permit misleading log/error content injection. | NVD, Go issue 79346, Go 1.26.4/1.25.11 release notes |
| CVE-2026-44653 | Medium 6.5 | LibreChat users with VIEW access to shared MCP servers can retrieve decrypted admin-managed secrets. | NVD, GitHub Security Advisory GHSA-6vqg-rgpm-qvf9 |
| CVE-2026-44654 | Medium 5.7 | LibreChat shared-agent editor can delete globally reused file records through `DELETE /api/files`. | NVD, GitHub Security Advisory GHSA-f8jg-v856-mf6q |

## Exploits Released and Public PoC Indicators

### Sploitus Top 10 - reconstructed from indexed Sploitus entries

The Sploitus homepage fetch did not expose an "Exploits of the Week" block. The following list is reconstructed from targeted indexed Sploitus result pages and deduplicated by vulnerability family.

| Rank | Exploit indicator | CVE(s) | Affected software | Exploit type | Maturity / PoC status | Weaponization potential | Confidence |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | LibreChat MCP server secrets exfiltration | CVE-2026-32625 | LibreChat <= 0.8.3 | Authenticated server-side secret exfiltration via MCP URL env expansion | Primary GitHub advisory includes curl/netcat PoC; no Sploitus hit found yet | Critical for self-hosted LibreChat with user registration/MCP enabled | High |
| 2 | Copy Fail / Dirty Frag toolkit | CVE-2026-31431 and related Copy Fail IDs | Linux kernel | Local privilege escalation/page-cache write; container escape potential | Multiple public GitHub/Sploitus-indexed PoCs and toolkits | High where attackers have local/container foothold | High |
| 3 | cPanel/WHM auth bypass PoC | CVE-2026-41940 | cPanel/WHM cpsrvd | Authentication bypass and WHM/root-session access indicator | GitHub/Sploitus-indexed Go/Python PoC indicators; Metasploit references observed in prior runs | Critical for internet-facing WHM | High |
| 4 | Drupal Core PostgreSQL SQL injection | CVE-2026-9082 | Drupal Core with PostgreSQL | Unauthenticated SQL injection; potential RCE under dangerous PostgreSQL roles | ExploitDB 52608 plus Sploitus mass-scanner/exploitation entries | High for exposed Drupal/PostgreSQL | High |
| 5 | MCPJam Inspector unauthenticated RCE | CVE-2026-23744 | MCPJam Inspector <= 1.4.2 | Missing auth at `/api/mcp/connect`, reverse shell payloads | New GitHub repo `MrR0b0t19/CVE-2026-23744-PoC` created 2026-06-02 23:19 UTC; prior Sploitus/PacketStorm indicators | High for exposed inspector services | Medium |
| 6 | Apache Camel deserialization/header-injection chain | CVE-2026-33453, CVE-2026-40473, CVE-2026-40858 | Apache Camel 4.18.0 components | RCE/deserialization and header-injection chain | Sploitus-indexed PoC claims with commands | High if vulnerable endpoints are reachable | Medium |
| 7 | Next.js WebSocket upgrade SSRF | CVE-2026-44578 | Self-hosted Next.js ranges | SSRF via upgrade handler | Sploitus-indexed scanner/exploit | Medium to high depending cloud metadata exposure | Medium |
| 8 | Microsoft Office OLE bypass claim | CVE-2026-21509 | Microsoft Office / Microsoft 365 Apps | Document-based security feature bypass | Sploitus-indexed GitHub repo; content contains exaggerated/possibly unreliable claims | Treat as low-confidence exploit indicator unless corroborated by Microsoft/KEV | Low |
| 9 | GNU inetutils telnetd auth bypass claim | CVE-2026-24061 | GNU inetutils telnetd | Remote auth bypass/root shell claim | GitHub repo pushed 2026-06-02 23:53; not validated | High if real and telnetd exposed, but source is unvalidated | Low |
| 10 | alf.io extension sandbox escape/file-read PoCs | CVE-2026-35482, CVE-2026-41412 | alf.io <= 2.0-M5-2509-1 | Authenticated admin RCE and arbitrary file read/exfil | Primary GitHub advisories include working PoC scripts | High after admin compromise or abuse of delegated admin role | High |

### ExploitDB additions

Direct ExploitDB CSV parsing showed no 2026-06-02 or 2026-06-03 rows. Latest direct CSV rows remain:

- EDB-ID 52607, 2026-06-01: WordPress OrderConvo 14 path traversal, CVE-2025-10162, unverified.
- EDB-ID 52608, 2026-06-01: Drupal Core 10.5.5 error-based SQL injection, CVE-2026-9082, unverified.
- EDB-ID 52603/52604/52605, 2026-05-30: YAMCS yamcs-core issues including CVE-2026-42568, CVE-2026-44595, and CVE-2026-44596.
- EDB-ID 52606, 2026-05-30: Notepad++ 8.9.6 arbitrary code execution, CVE-2026-48778.

### GitHub PoC/repository monitoring

- Strict GitHub repository search for `CVE-2026 exploit PoC created:>=2026-06-03` returned 0 repositories.
- Broader `CVE-2026 PoC created:>=2026-06-02` returned 2 repositories:
  - `MrR0b0t19/CVE-2026-23744-PoC` (created/pushed 2026-06-02 23:19 UTC, no description; likely MCPJam indicator from prior monitoring, not validated).
  - `lorenzocamilli/CVE-2026-45332-PoC` (created 2026-06-02 17:15 UTC, no description; not validated).
- Broader `CVE-2026 exploit pushed:>=2026-06-02` returned 18 repositories. Notable unvalidated indicators include:
  - `obrunolima1910/CVE-2026-24061` (pushed 2026-06-02 23:53; claims GNU inetutils-telnetd auth bypass/root shell).
  - `MrForkBomb/CIFSwitch-Checker-CVE-2026-46243` (checker/detection script, not exploit execution).
  - `Defacto-ridgepole254/CVE-2026-41940-Exploit-PoC` (cPanel/WHM auth bypass PoC indicator).
  - `Dullpurple-sloop726/CVE-2026-31431-Linux-Copy-Fail` and `Liverwortenuresis371/copyfail-rs` (Copy Fail LPE indicators).
  - `Recorded-texteditor120/CVE-2026-31802` (npm tar path traversal/arbitrary overwrite indicator).
  - `DyniePro/CVE-2026-25643` (Frigate NVR RCE indicator).
- Caution: these GitHub results are indicators only. No repository was cloned or executed, and public PoC repositories can be malicious or fabricated.

## Malware Intelligence

| Source | Finding | Assessment | Confidence |
| --- | --- | --- | --- |
| MalwareBazaar | 231 submissions in the past 24 hours; Mirai is the most-seen malware family; corpus size shown as 1,091,537 samples. Current statistics page shows high-volume YARA matches including Linux malware, script injection, ransomware, and anti-VM rules with last matches on 2026-06-02. | Continued IoT/Linux botnet churn and active malware sample sharing; prioritize edge/IoT credential hygiene, egress blocking, and enrichment of Mirai/YARA-derived detections. | High |
| SANS ISC | New wave of phishing emails delivering SVG attachments with embedded JavaScript redirects and `application/ecmascript` MIME type. | Update mail gateway/YARA/content rules to treat SVG as active content and detect ECMAScript-family script MIME types, not only `text/javascript`. | High |
| VX-Underground | Direct site fetch timed out. GitHub metadata showed `vxunderground/MalwareSourceCode` latest commit remains 2026-05-30 (`Add files via upload`), with no newer malware-source push in this run. | No new VX-sourced malware release was confirmed during this run. | Medium |
| Ransomware/open-source monitoring | Search results surfaced low-confidence ransomware victim claims for ShadowByt3$, Play, and Qilin, plus strategic reports from Unit 42 and CrowdStrike on faster AI-assisted eCrime and extortion operations. | Useful trend context, but no new high-confidence, primary-source ransomware campaign was validated for enterprise emergency action in this hour. | Low to Medium |

## Security Releases and Vendor Advisories

| Vendor/source | Release/advisory | Impact | Action |
| --- | --- | --- | --- |
| LibreChat / GitHub Security Advisories | CVE-2026-32625, CVE-2026-31942, CVE-2026-44653, CVE-2026-44654 published Jun 2. | MCP server configuration and API-key authorization flaws can leak server secrets, alter users' API keys, expose admin-managed MCP secrets, or delete shared files. | Upgrade to the fixed LibreChat versions, disable untrusted MCP server creation until patched, rotate secrets if logs show malicious MCP URLs or unexpected API-key updates. |
| alf.io / GitHub Security Advisories | CVE-2026-35482 and CVE-2026-41412 published Jun 2; fixed in 2.0-M5-2606. | Authenticated administrator extension scripts can escape sandbox for OS command execution or arbitrary file read/exfiltration. | Upgrade to 2.0-M5-2606, restrict extension admin roles, and review extension/audit logs. |
| Go | Go 1.26.4 and 1.25.11 released Jun 2 with security fixes in `crypto/x509`, `mime`, and `net/textproto`. | Potential CPU exhaustion and misleading log/error content risks in Go applications handling certificates, MIME headers, or textproto errors. | Update Go toolchains/base images and rebuild services. |
| GLPI | GitHub advisory CVE-2026-40108; fixed in 11.0.7. | Stored XSS in ITIL costs by technician-level users. | Upgrade to GLPI 11.0.7 and inspect ITIL cost entries. |
| QloApps | Commit 64e9722 and VulnCheck advisory for CVE-2026-25861. | Weak MD5-based password hashing can make stolen hashes easier to crack. | Apply vendor fix and plan password reset/re-hashing. |
| CISA KEV | Catalog version 2026.06.02 with CVE-2022-0492 and CVE-2025-48595 due 2026-06-05. | Confirmed exploitation of Linux kernel cgroups v1 and Android Framework vulnerabilities. | Treat as emergency remediation for affected container/Linux and Android fleets. |
| Microsoft | Windows Secure Boot certificate rollover guidance remains operationally important for June 2026; no new current-hour MSRC advisory was validated in this run. | Systems that miss certificate updates risk future boot-level update/trust issues. | Ensure Windows/OEM firmware update processes are current. |
| Cisco/Fortinet/VMware/GitLab/Broadcom | No new current-hour primary advisory was identified during this run. | Carry-forward perimeter-product exploit pressure remains high. | Continue monitoring and prioritize prior KEV/actively exploited edge products. |

## Recommended Actions - Highest to Lowest

1. Patch LibreChat immediately where MCP is enabled or user registration is open. Upgrade for CVE-2026-32625 and related MCP/API-key advisories; rotate `JWT_SECRET`, credential encryption keys, OAuth/API keys, and provider tokens if malicious MCP server URLs or unexpected API-key updates are detected.
2. Remediate CISA KEV additions CVE-2022-0492 and CVE-2025-48595 before the 2026-06-05 due date; prioritize Linux/container hosts with cgroups v1 exposure and Android managed fleets.
3. Patch or isolate internet-facing cPanel/WHM, Drupal/PostgreSQL, MCPJam Inspector, Palo Alto GlobalProtect, Oracle WebLogic, Microsoft Defender, Citrix NetScaler, and other assets with known active exploitation or public exploit indicators.
4. Upgrade alf.io to 2.0-M5-2606, restrict extension author/admin roles, and hunt for suspicious extension scripts, command execution, outbound exfiltration, and access to sensitive files.
5. Update Go toolchains and container base images to Go 1.26.4 or 1.25.11; rebuild internet-facing Go services that parse certificates, MIME headers, or textproto input.
6. Patch GLPI to 11.0.7 and QloApps to the fixed commit/release; review for stored XSS payloads and plan credential reset/re-hash workflows where password hashes may have been exposed.
7. Update email controls for SVG attachments containing script blocks, including `application/ecmascript`; consider stripping, sandboxing, or blocking SVG attachments except for explicit business allowlists.
8. Treat all public GitHub PoCs as hostile until reviewed in a sandbox. Do not execute the newly observed repos on analyst workstations.
9. Continue hourly monitoring for Sploitus, ExploitDB, PacketStorm, GitHub, and vendor mirrors for the LibreChat/alf.io/Go current-hour CVEs, because exploit indexing often lags NVD publication by several hours.

## Unified Vulnerability Records

```json
[
  {
    "cve": "CVE-2026-32625",
    "cvss": "9.6 Critical (CVSS v3.1)",
    "vendor": "LibreChat",
    "product": "LibreChat MCP server integration",
    "affected_versions": "LibreChat <= 0.8.3",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/danny-avila/LibreChat/security/advisories/GHSA-4pcc-j6m6-wcwx"
    ],
    "patch_available": true,
    "sources": [
      "https://nvd.nist.gov/vuln/detail/CVE-2026-32625",
      "https://github.com/danny-avila/LibreChat/security/advisories/GHSA-4pcc-j6m6-wcwx"
    ]
  },
  {
    "cve": "CVE-2022-0492",
    "cvss": "7.8 High (NVD historical; KEV-listed)",
    "vendor": "Linux",
    "product": "Kernel cgroups v1 release_agent",
    "affected_versions": "Linux kernels exposing vulnerable cgroups v1 release_agent behavior; vendor backport status varies",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://packetstormsecurity.com/files/176099/docker_cgroup_escape.rb.txt"
    ],
    "patch_available": true,
    "sources": [
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://nvd.nist.gov/vuln/detail/CVE-2022-0492",
      "https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=24f6008564183aa120d07c03d9289519c2fe02af"
    ]
  },
  {
    "cve": "CVE-2025-48595",
    "cvss": "Not fully scored in current feed; KEV-listed Android Framework integer overflow",
    "vendor": "Google/Android",
    "product": "Android Framework",
    "affected_versions": "Android versions covered by the June 2026 Android Security Bulletin",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://source.android.com/docs/security/bulletin/2026/2026-06-01",
      "https://nvd.nist.gov/vuln/detail/CVE-2025-48595"
    ]
  },
  {
    "cve": "CVE-2026-35482",
    "cvss": "8.0 High (CVSS v3.1)",
    "vendor": "alf.io",
    "product": "alf.io extension script engine",
    "affected_versions": "alf.io <= 2.0-M5-2509-1",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/alfio-event/alf.io/security/advisories/GHSA-3w8f-mcf6-cm7h"
    ],
    "patch_available": true,
    "sources": [
      "https://nvd.nist.gov/vuln/detail/CVE-2026-35482",
      "https://github.com/alfio-event/alf.io/security/advisories/GHSA-3w8f-mcf6-cm7h"
    ]
  },
  {
    "cve": "CVE-2026-25861",
    "cvss": "8.2 High (CVSS v4.0)",
    "vendor": "QloApps",
    "product": "QloApps",
    "affected_versions": "QloApps through 1.7.0",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://nvd.nist.gov/vuln/detail/CVE-2026-25861",
      "https://github.com/Qloapps/QloApps/commit/64e9722e7e6a8fda77dd53964d988fb6b5c3d174",
      "https://www.vulncheck.com/advisories/qloapps-weak-password-hashing-via-md5-in-tools-php"
    ]
  },
  {
    "cve": "CVE-2026-31942",
    "cvss": "7.1 High (CVSS v3.1)",
    "vendor": "LibreChat",
    "product": "LibreChat API keys management endpoint",
    "affected_versions": "LibreChat <= 0.7.6",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/danny-avila/LibreChat/security/advisories/GHSA-5jcj-rh68-cgj7"
    ],
    "patch_available": true,
    "sources": [
      "https://nvd.nist.gov/vuln/detail/CVE-2026-31942",
      "https://github.com/danny-avila/LibreChat/security/advisories/GHSA-5jcj-rh68-cgj7"
    ]
  },
  {
    "cve": "CVE-2026-40108",
    "cvss": "7.1 High (CVSS v4.0)",
    "vendor": "GLPI",
    "product": "GLPI ITIL Costs",
    "affected_versions": "GLPI 11.0.0 through 11.0.6",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://nvd.nist.gov/vuln/detail/CVE-2026-40108",
      "https://github.com/glpi-project/glpi/security/advisories/GHSA-rhmv-j773-4gvh"
    ]
  },
  {
    "cve": "CVE-2026-41412",
    "cvss": "4.9 Medium (CVSS v3.1)",
    "vendor": "alf.io",
    "product": "alf.io simpleHttpClient extension script helper",
    "affected_versions": "alf.io <= 2.0-M5-2509-1",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/alfio-event/alf.io/security/advisories/GHSA-6m62-53cw-4373"
    ],
    "patch_available": true,
    "sources": [
      "https://nvd.nist.gov/vuln/detail/CVE-2026-41412",
      "https://github.com/alfio-event/alf.io/security/advisories/GHSA-6m62-53cw-4373"
    ]
  },
  {
    "cve": "CVE-2026-44653",
    "cvss": "6.5 Medium (CVSS v3.1)",
    "vendor": "LibreChat",
    "product": "LibreChat shared MCP server views",
    "affected_versions": "LibreChat v0.8.3",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/danny-avila/LibreChat/security/advisories/GHSA-6vqg-rgpm-qvf9"
    ],
    "patch_available": true,
    "sources": [
      "https://nvd.nist.gov/vuln/detail/CVE-2026-44653",
      "https://github.com/danny-avila/LibreChat/security/advisories/GHSA-6vqg-rgpm-qvf9"
    ]
  },
  {
    "cve": "CVE-2026-27145",
    "cvss": "Unscored in NVD current feed",
    "vendor": "Go",
    "product": "crypto/x509",
    "affected_versions": "Go versions before 1.26.4 and 1.25.11 in supported branches",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://nvd.nist.gov/vuln/detail/CVE-2026-27145",
      "https://go.dev/doc/devel/release",
      "https://go.dev/issue/79694"
    ]
  },
  {
    "cve": "CVE-2026-42504",
    "cvss": "Unscored in NVD current feed",
    "vendor": "Go",
    "product": "mime",
    "affected_versions": "Go versions before 1.26.4 and 1.25.11 in supported branches",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://nvd.nist.gov/vuln/detail/CVE-2026-42504",
      "https://go.dev/doc/devel/release",
      "https://go.dev/issue/79217"
    ]
  },
  {
    "cve": "CVE-2026-42507",
    "cvss": "Unscored in NVD current feed",
    "vendor": "Go",
    "product": "net/textproto",
    "affected_versions": "Go versions before 1.26.4 and 1.25.11 in supported branches",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://nvd.nist.gov/vuln/detail/CVE-2026-42507",
      "https://go.dev/doc/devel/release",
      "https://go.dev/issue/79346"
    ]
  },
  {
    "cve": "CVE-2026-23744",
    "cvss": "Critical in prior reporting; current GitHub indicator unvalidated",
    "vendor": "MCPJam",
    "product": "MCPJam Inspector",
    "affected_versions": "MCPJam Inspector <= 1.4.2 per prior monitoring",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/MrR0b0t19/CVE-2026-23744-PoC"
    ],
    "patch_available": true,
    "sources": [
      "https://github.com/MrR0b0t19/CVE-2026-23744-PoC"
    ]
  }
]
```

## Source Notes and Collection Evidence

- NVD API windows queried:
  - Current: 2026-06-02T23:00:00.000 to 2026-06-03T00:35:00.000 - 16 CVEs.
  - June 3 day-to-date: 2026-06-03T00:00:00.000 to 2026-06-03T00:35:00.000 - 0 CVEs.
  - June 2 final observed: 225 CVEs.
  - Rolling 24h: 219 CVEs (14 Critical, 76 High, 86 Medium, 25 Low, 18 Unknown).
- CISA KEV JSON queried directly from `https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json`; catalog version observed: 2026.06.02.
- GitHub API searches were read-only; no PoC repositories were cloned or executed.
- ExploitDB CSV source: `https://gitlab.com/exploit-database/exploitdb/-/raw/main/files_exploits.csv`.
- MalwareBazaar browse/statistics pages were fetched directly; VX-Underground web root timed out, so VX assessment used GitHub repository metadata only.
