# Security Intelligence Report - 2026-06-02 19:03 UTC

## Executive Summary

- **Collection window:** 2026-06-02 18:00-19:35 UTC, with day-to-date and rolling-24h enrichment for prioritization.
- **New CVEs discovered in this hour:** 0 via NVD between 18:00 and 19:35 UTC.
- **Day-to-date NVD volume:** 146 CVEs published on 2026-06-02: 9 critical, 43 high, 63 medium, 19 low, 12 unknown.
- **Rolling 24h NVD volume:** 336 CVEs: 17 critical, 129 high, 135 medium, 43 low, 12 unknown.
- **Critical findings requiring review:** CISA KEV additions for Linux Kernel CVE-2022-0492 and Android Framework CVE-2025-48595; Progress Sitefinity CVE-2026-7312/CVE-2026-7198; OpenMed CVE-2026-47117; OpenClaude CVE-2026-42074; Spacelabs Sentinel CVE-2026-0611.
- **Active exploitation findings:** High confidence for CISA KEV-listed CVE-2022-0492, CVE-2025-48595, CVE-2024-21182, CVE-2026-20182, CVE-2026-41940, CVE-2026-35616, CVE-2026-3055, and CVE-2026-9082. Public PoC indicators exist for several, but GitHub-only repositories remain unvalidated.
- **New malware campaigns:** No new VX-Underground GitHub push after 2026-05-30. MalwareBazaar reported 249 submissions in the past 24h, with Mirai the most-seen family. FortiClient EMS EKZ Infostealer and cPanel/Sorry ransomware remain high-priority carry-forward items.
- **Important vendor/security releases:** CISA KEV 2026.06.02, Android June 2026 bulletin, Progress Sitefinity May advisory, Spacelabs Sentinel advisory, AWS Kiro IDE 0.11 bulletin, OpenClaude 0.5.1, Bitdefender Napoca EOL advisories, Mint 1.9.0, MISP LDAP/OTP fix, Roche navify Digital Pathology 2.4.1.

## Source Coverage and Notes

- **Tier 1 exploit sources:** Sploitus static homepage exposed only the search shell, so the Sploitus Top 10 below is reconstructed from indexed Sploitus result pages and cross-checked against NVD/ExploitDB/GitHub where possible. ExploitDB CSV was queried directly. GitHub Security Advisory API and GitHub repository search were queried. CISA KEV JSON and NVD APIs were queried directly.
- **Malware sources:** VX-Underground site and GitHub metadata, MalwareBazaar browse statistics, and carry-forward reporting around FortiClient EMS EKZ Infostealer/cPanel Sorry ransomware were reviewed.
- **Confidence model:** "High" means primary source and/or KEV plus corroborating technical references. "Medium" means credible source or multiple indicators but incomplete primary confirmation. "Low" means single indexed/search result, unvalidated PoC, or unclear CVE assignment.

## Top Vulnerabilities

| Priority | CVE | Severity | Affected software | Exploit availability | Active exploitation | Recommended action | Confidence |
|---|---|---:|---|---|---|---|---|
| Critical | CVE-2022-0492 | CVSS 7.8 High; KEV critical by exploitation | Linux kernel cgroups v1 `release_agent` privilege escalation/container escape | Public Metasploit/Sploitus and Packet Storm indicators | Yes, CISA KEV added 2026-06-02 | Patch affected kernels, disable/limit cgroups v1 where possible, audit privileged/SYS_ADMIN containers, prioritize by 2026-06-05 KEV due date | High |
| Critical | CVE-2025-48595 | CVSS 8.4 High; KEV critical by exploitation | Android Framework integer overflow leading to local code execution/EoP | No public exploit validated in this run | Yes, CISA KEV added 2026-06-02 | Apply Android June 2026 bulletin updates, prioritize managed/mobile fleets by KEV due date 2026-06-05 | High |
| Critical | CVE-2026-7312 | 10.0 Critical | Progress Sitefinity, multiple 14.x/15.x versions, Insight integration/non-default configuration | No public exploit validated | No confirmed exploitation found | Apply Progress Sitefinity advisory updates; review Sitefinity Insight integration exposure and stored credentials | High |
| Critical | CVE-2026-7198 | 9.8 Critical | Progress Sitefinity 15.4.8623 before 15.4.8630 | No public exploit validated | No confirmed exploitation found | Upgrade to fixed Sitefinity release; restrict unauthenticated access to affected web services until patched | High |
| Critical | CVE-2026-47117 | 9.3 Critical | OpenMed before 1.5.2 | Vulnerability details and patch links public; no weaponized exploit validated | No confirmed exploitation found | Upgrade OpenMed to 1.5.2; block untrusted model names/repos and review any Hugging Face `trust_remote_code=True` paths | High |
| Critical | CVE-2026-42074 | 9.3 Critical | OpenClaude before 0.5.1 | GitHub advisory and patch public; PoC conditions described by advisory | No confirmed exploitation found | Upgrade to 0.5.1; disable unsandboxed command execution defaults and review agent tool policies | High |
| Critical | CVE-2026-0611 | 9.2 Critical | Spacelabs Healthcare Sentinel 10.5.x/11.x before 11.6.0 when .NET Remoting port 8989 is network-exposed | VulnCheck and vendor advisory public; no exploit code validated | No confirmed exploitation found | Upgrade to 11.6.0; ensure TCP/8989 is not externally exposed; hunt for ASPX webshell writes | High |
| High | CVE-2026-10591 | 8.6 High | Amazon Kiro IDE before 0.11 | Advisory public; no standalone exploit validated | No confirmed exploitation found | Upgrade to Kiro IDE 0.11+; review workspace auto-execution paths such as `.vscode/tasks.json` | High |
| High | CVE-2026-10047 / CVE-2026-10046 | 8.5 High | Bitdefender Napoca bare-metal hypervisor, EOL | Technical advisories public; local malicious guest required | No confirmed exploitation found | Remove/replace unsupported Napoca deployments; segment risky guest workloads | High |
| High | CVE-2026-10611 | 8.2 High | MISP LDAP mixed auth with OTP enforcement | Patch commit public | No confirmed exploitation found | Apply MISP commit/release containing OTP-after-plugin-auth fix; test LDAP+OTP login flow | High |
| High | CVE-2026-41940 | 9.3 Critical | cPanel & WHM/WP2 | Public exploit, watchTowr PoC, ExploitDB/Metasploit/Sploitus indicators | Yes, KEV and ransomware use known | Patch all affected cPanel versions; hunt for unexpected control-panel logins, webshells, and Sorry ransomware artifacts | High |
| High | CVE-2026-35616 | 9.8 Critical | Fortinet FortiClient EMS 7.4.5-7.4.6 | No new PoC validated this hour; exploitation reports public | Yes, KEV and EKZ Infostealer campaign reporting | Upgrade to 7.4.7+; audit EMS policies, VPN scripts, PowerShell logs, and `FortiEndpoint_Patch.exe` artifacts | High |

## Exploits Released

### Sploitus Reconstructed Top 10

Static Sploitus homepage collection did not expose an official "Exploits of the Week" block. The following are the top indexed Sploitus exploit indicators observed and correlated during this run:

| Rank | Indicator | Affected software | Exploit type | Maturity | PoC availability | Weaponization potential | Confidence |
|---:|---|---|---|---|---|---|---|
| 1 | CVE-2022-0492 | Linux kernel / Docker cgroups | Local privilege escalation/container escape | Metasploit module indexed | Public | High in container environments with privileged/SYS_ADMIN exposure | High |
| 2 | CVE-2026-9082 | Drupal Core 10.5.5 | Error-based SQL injection | ExploitDB 52608 indexed | Public | High for unpatched internet-facing Drupal JSON:API deployments | High |
| 3 | CVE-2026-48778 | Notepad++ 8.9.6 | Local/user-context code execution via config manipulation | Packet Storm indexed | Public | Medium; requires user/config path access | Medium |
| 4 | CVE-2026-BetterSQLCipher-RCE | better-sqlcipher | `loadExtension()` arbitrary code execution | GitHub/Sploitus indicator; non-standard CVE string | Public claimed | Medium to high if application exposes attacker-controlled extension paths | Low |
| 5 | CVE-2026-45659 | Microsoft SharePoint | Deserialization/code execution | Sploitus page claims private/public download link | Unvalidated | High if exploit is real; treat repo/download as potentially malicious | Low |
| 6 | CVE-2026-21858 | n8n automation platform | Full-chain RCE/auth bypass/file read | Sploitus indexed reconstruction | Public claimed | High for exposed vulnerable n8n instances | Low |
| 7 | CVE-2026-0386 | Windows PowerShell/Invoke-WebRequest behavior | Client-side code execution/XSS-like behavior | Sploitus indexed write-up | Public claimed | Medium; requires victim interaction/command behavior | Low |
| 8 | CVE-2025-6965 | SQLite / Windows `winsqlite3.dll` | Heap overflow/DoS, possible RCE | ExploitDB/Sploitus indicator | Public | Medium; environmental constraints unclear | Medium |
| 9 | CVE-2025-48757 | Supabase/vibe-coded apps exposure research | Secrets/auth/data exposure scanner | Sploitus indexed tooling | Public tool | Medium; more scanner than exploit | Medium |
| 10 | CVE-2026-29014 | MetInfo CMS 8.1 | PHP code injection | Packet Storm/Sploitus indexed | Public | High for unpatched CMS exposure | Medium |

### ExploitDB Additions

Direct ExploitDB CSV latest rows:

- **EDB-ID 52608** - Drupal Core 10.5.5 Error-Based SQL Injection, CVE-2026-9082, published 2026-06-01, platform PHP/webapps.
- **EDB-ID 52607** - WordPress OrderConvo 14 Path Traversal, CVE-2025-10162, published 2026-06-01, platform multiple/webapps.
- No ExploitDB row dated 2026-06-02 was observed in the direct CSV during this run.

### New GitHub PoC / Exploit Indicators

- GitHub Security Advisories API returned **0 reviewed advisories** published after 2026-06-02 14:00 UTC and after 18:00 UTC.
- Strict repo search `CVE-2026 PoC exploit created:>=2026-06-02` returned **0 repositories**.
- Broader `CVE-2026 exploit pushed:>=2026-06-02` returned unvalidated indicators including:
  - `TYehan/CVE-2026-23744` - MCPJam Inspector RCE PoC, created/pushed 2026-06-02 16:57 UTC.
  - `Jenderal92/CVE-2026-8206` - claimed Kirki mass exploitation tool, created 2026-06-02 10:53 UTC.
  - `Defacto-ridgepole254/CVE-2026-41940-Exploit-PoC` - cPanel/WHM auth bypass PoC indicator, pushed 2026-06-02 16:44 UTC.
  - `Dullpurple-sloop726/CVE-2026-31431-Linux-Copy-Fail` and `Liverwortenuresis371/copyfail-rs` - Linux Copy Fail LPE indicators, pushed 2026-06-02.
  - `0xABCD01/CVE-2026-41089` - Netlogon CLDAP PoC indicator, pushed 2026-06-02.
  - `Recorded-texteditor120/CVE-2026-31802` - npm tar path traversal indicator, pushed 2026-06-02.
- These GitHub repositories were **not executed or validated**. Treat them as indicators only; public PoC repositories may be trojanized.

## Malware Intelligence

- **VX-Underground:** Direct site fetch was available but no new malware-source push was observed. GitHub `vxunderground/MalwareSourceCode` latest commit remains 2026-05-30 (`Python/Stealer.Python.GMBA.Manipulator.7z`). No new June 2 malware family or ransomware source leak was confirmed from VX GitHub metadata.
- **MalwareBazaar:** 249 submissions in the past 24 hours; Mirai was the most-seen malware family; corpus size 1,091,518 samples.
- **FortiClient EMS / EKZ Infostealer:** Carry-forward high-priority active exploitation. Reporting indicates threat actors abused FortiClient EMS management paths to deploy `FortiEndpoint_Patch.exe`/EKZ Infostealer via PowerShell/VPN scripting workflows.
- **cPanel / Sorry ransomware:** Carry-forward high-priority ransomware exploitation. CVE-2026-41940 remains KEV-listed with known ransomware use and public exploit material.
- **Supply chain:** CISA KEV continues to track malicious package/extension incidents for TanStack (CVE-2026-45321), Nx Console (CVE-2026-48027), and Daemon Tools Lite (CVE-2026-8398). Known ransomware campaign use is marked for TanStack and Nx Console in the KEV feed.

## Security Releases and Advisories

- **CISA KEV:** Catalog version 2026.06.02, released 2026-06-02T17:04:13Z, count 1610. New June 2 additions: CVE-2022-0492 and CVE-2025-48595; both due 2026-06-05.
- **Android:** June 2026 security bulletin includes CVE-2025-48595; apply device/vendor updates.
- **Progress Sitefinity:** Advisory covers CVE-2026-7312, CVE-2026-7198, CVE-2026-7195, CVE-2026-7201, and CVE-2026-7313 across Sitefinity 14.x/15.x releases.
- **Spacelabs Healthcare:** Sentinel advisory for unauthenticated .NET Remoting RCE on explicitly exposed port 8989; fixed in 11.6.0.
- **OpenClaude:** Version 0.5.1 patches model-controlled sandbox bypass via `dangerouslyDisableSandbox`.
- **OpenMed:** Version 1.5.2 patches RCE through PII privacy-filter model loading and `trust_remote_code=True`.
- **AWS Kiro IDE:** Version 0.11 fixes insufficient file write tool restrictions.
- **Bitdefender:** Napoca hypervisor advisories published for CVE-2026-10047 and CVE-2026-10046; product noted as end-of-life/unsupported in NVD descriptions.
- **Elixir Mint:** Version 1.9.0 fixes HTTP/2 CONTINUATION and PUSH_PROMISE memory exhaustion flaws CVE-2026-49754 and CVE-2026-48862.
- **MISP:** Patch commit addresses LDAP mixed authentication OTP bypass CVE-2026-10611.
- **Roche:** navify Digital Pathology before 2.4.1 affected by default credentials in RabbitMQ management modules CVE-2026-9844.

## Unified Vulnerability Records

```json
[
  {
    "cve": "CVE-2022-0492",
    "cvss": "7.8",
    "vendor": "Linux",
    "product": "Kernel cgroups v1",
    "affected_versions": "Linux kernel 2.6.24 through multiple fixed stable releases; see vendor kernel fixes",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://sploitus.com/exploit?id=MSF%3AEXPLOIT-LINUX-LOCAL-DOCKER_CGROUP_ESCAPE-",
      "http://packetstormsecurity.com/files/176099/Docker-cgroups-Container-Escape.html"
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
    "cvss": "8.4",
    "vendor": "Android",
    "product": "Framework",
    "affected_versions": "Android devices pending June 2026 security bulletin patches",
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
      "https://nvd.nist.gov/vuln/detail/CVE-2026-7312",
      "https://community.progress.com/s/article/Sitefinity-Security-Advisory-for-Addressing-Security-Vulnerabilities-CVE-2026-7312-CVE-2026-7198-CVE-2026-7195-CVE-2026-7201-CVE-2026-7313-May-2026"
    ]
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
      "https://nvd.nist.gov/vuln/detail/CVE-2026-7198",
      "https://community.progress.com/s/article/Sitefinity-Security-Advisory-for-Addressing-Security-Vulnerabilities-CVE-2026-7312-CVE-2026-7198-CVE-2026-7195-CVE-2026-7201-CVE-2026-7313-May-2026"
    ]
  },
  {
    "cve": "CVE-2026-47117",
    "cvss": "9.3",
    "vendor": "OpenMed",
    "product": "OpenMed",
    "affected_versions": "Before 1.5.2",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://nvd.nist.gov/vuln/detail/CVE-2026-47117",
      "https://github.com/maziyarpanahi/openmed/releases/tag/v1.5.2",
      "https://www.vulncheck.com/advisories/openmed-remote-code-execution-via-pii-model-loading"
    ]
  },
  {
    "cve": "CVE-2026-42074",
    "cvss": "9.3",
    "vendor": "OpenClaude",
    "product": "OpenClaude CLI",
    "affected_versions": "Before 0.5.1",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/Gitlawb/openclaude/security/advisories/GHSA-m77w-p5jj-xmhg"
    ],
    "patch_available": true,
    "sources": [
      "https://nvd.nist.gov/vuln/detail/CVE-2026-42074",
      "https://github.com/Gitlawb/openclaude/commit/aab489055c53dd64369414116fe93226d2656273"
    ]
  },
  {
    "cve": "CVE-2026-0611",
    "cvss": "9.2",
    "vendor": "Spacelabs Healthcare",
    "product": "Sentinel",
    "affected_versions": "10.5.x and higher, 11.x before 11.6.0 when TCP/8989 is exposed",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://nvd.nist.gov/vuln/detail/CVE-2026-0611",
      "https://spacelabshealthcare.com/wp-content/uploads/2026/06/079-0273-00-RevA-Security-Advisory-Sentinel-.NET-Remoting-Vulnerability.pdf",
      "https://www.vulncheck.com/advisories/spacelabs-healthcare-sentinel-x-unauthenticated-rce-via-net-remoting"
    ]
  },
  {
    "cve": "CVE-2026-10591",
    "cvss": "8.6",
    "vendor": "Amazon",
    "product": "Kiro IDE",
    "affected_versions": "Before 0.11",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://nvd.nist.gov/vuln/detail/CVE-2026-10591",
      "https://aws.amazon.com/security/security-bulletins/2026-037-aws/",
      "https://kiro.dev/changelog/ide/0-11/"
    ]
  },
  {
    "cve": "CVE-2026-10611",
    "cvss": "8.2",
    "vendor": "MISP",
    "product": "MISP",
    "affected_versions": "LDAP mixed auth with mandatory OTP configurations before patch commit",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://nvd.nist.gov/vuln/detail/CVE-2026-10611",
      "https://github.com/MISP/MISP/commit/39b3cb15aac4318afdd2ab63b96c2eac12b271fe"
    ]
  },
  {
    "cve": "CVE-2026-41940",
    "cvss": "9.3",
    "vendor": "WebPros",
    "product": "cPanel & WHM / WP2",
    "affected_versions": "Multiple cPanel & WHM trains after 11.40 and before fixed releases including 136.0.5",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://github.com/watchtowrlabs/watchTowr-vs-cPanel-WHM-AuthBypass-to-RCE.py",
      "https://labs.watchtowr.com/the-internet-is-falling-down-falling-down-falling-down-cpanel-whm-authentication-bypass-cve-2026-41940/"
    ],
    "patch_available": true,
    "sources": [
      "https://nvd.nist.gov/vuln/detail/CVE-2026-41940",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://support.cpanel.net/hc/en-us/articles/40073787579671-cPanel-WHM-Security-Update-04-28-2026"
    ]
  },
  {
    "cve": "CVE-2026-35616",
    "cvss": "9.8",
    "vendor": "Fortinet",
    "product": "FortiClient EMS",
    "affected_versions": "7.4.5 through 7.4.6",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://nvd.nist.gov/vuln/detail/CVE-2026-35616",
      "https://fortiguard.fortinet.com/psirt/FG-IR-26-099",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"
    ]
  },
  {
    "cve": "CVE-2026-9082",
    "cvss": "9.8",
    "vendor": "Drupal",
    "product": "Drupal Core",
    "affected_versions": "8.9.0 before 10.4.10; 10.5.0 before 10.5.10; 10.6.0 before 10.6.9; 11.0.0 before 11.1.10; 11.2.0 before 11.2.12; 11.3.0 before 11.3.10",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://www.exploit-db.com/exploits/52608",
      "https://sploitus.com/exploit?id=EDB-ID%3A52608"
    ],
    "patch_available": true,
    "sources": [
      "https://nvd.nist.gov/vuln/detail/CVE-2026-9082",
      "https://www.drupal.org/sa-core-2026-004",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"
    ]
  }
]
```

## Recommended Actions

1. **Immediately remediate June 2 KEV additions:** patch Linux kernel/cgroups exposure for CVE-2022-0492 and Android Framework CVE-2025-48595 by the 2026-06-05 KEV due date; treat container hosts and managed Android fleets as priority assets.
2. **Patch actively exploited edge/management products first:** Cisco SD-WAN CVE-2026-20182, cPanel CVE-2026-41940, FortiClient EMS CVE-2026-35616, Citrix NetScaler CVE-2026-3055, Drupal CVE-2026-9082, PAN-OS CVE-2026-0257, and Oracle WebLogic CVE-2024-21182.
3. **Upgrade newly disclosed critical enterprise/web apps:** Progress Sitefinity, OpenMed, OpenClaude, and Spacelabs Sentinel. For Sentinel, verify that .NET Remoting on TCP/8989 is not exposed.
4. **Review developer and AI tooling exposure:** upgrade Kiro IDE and OpenClaude; restrict autonomous file-write/command-execution tools; monitor for prompt-injection-to-command-execution paths.
5. **Treat public PoC repos as hostile until reviewed:** do not execute newly pushed GitHub PoCs in production or analyst workstations; inspect offline, sandbox, and compare against vendor/advisory details.
6. **Hunt for malware carry-forward items:** EKZ Infostealer artifacts related to FortiClient EMS and cPanel/Sorry ransomware indicators; review PowerShell, EMS policy changes, webshells, and suspicious cPanel login events.
7. **Supply-chain hygiene:** inventory TanStack, Nx Console, Daemon Tools Lite, and other packages/extensions referenced by KEV; rotate potentially exposed tokens where malicious versions may have run.

## Appendix: Validation Evidence

- NVD API queried for 2026-06-02 18:00-19:35 UTC: 0 CVEs.
- NVD API queried for 2026-06-02 00:00-19:35 UTC: 146 CVEs, including 9 critical and 43 high.
- CISA KEV JSON queried directly: catalog version 2026.06.02, 1610 entries; CVE-2022-0492 and CVE-2025-48595 added on 2026-06-02.
- GitHub Security Advisories queried for reviewed advisories after 14:00 UTC and 18:00 UTC: 0 results.
- ExploitDB direct CSV latest rows: EDB-ID 52608 and 52607 on 2026-06-01; no 2026-06-02 row observed.
- VX-Underground GitHub metadata: `MalwareSourceCode` latest commit 2026-05-30 adding `Python/Stealer.Python.GMBA.Manipulator.7z`.
- MalwareBazaar browse page: 249 submissions in past 24 hours; Mirai most seen.
