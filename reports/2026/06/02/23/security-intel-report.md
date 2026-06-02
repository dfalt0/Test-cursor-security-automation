# Hourly Security Intelligence Report - 2026-06-02 23:02 UTC

## Report Metadata

- Automation trigger: cron, 2026-06-02 23:01 UTC
- Repository verified: `dfalt0/Test-cursor-security-automation`
- Branch: `cursor/security-intelligence-agent-e295`
- Report path: `reports/2026/06/02/23/security-intel-report.md`
- Collection window emphasized: 2026-06-02 22:00-23:35 UTC, with day-to-date and carry-forward exploitation context
- Confidence model: High = primary source or multiple authoritative sources; Medium = primary source plus unvalidated exploit/search indicator; Low = single secondary/indexed signal only

## Executive Summary

- Total CVEs discovered in the current NVD window: 10 (5 High, 4 Medium, 1 rejected duplicate/unknown).
- Day-to-date NVD volume for 2026-06-02: 209 CVEs (13 Critical, 75 High, 94 Medium, 12 Low, 15 Unknown).
- Current-hour critical findings: none newly published in NVD between 22:00 and 23:35 UTC.
- Highest current-hour enterprise/operational risks: Docker Desktop CVE-2026-8936, Drager Infinity M540 CVE-2022-4992, Drager Protector CVE-2021-4480/CVE-2021-4481, libwebsockets CVE-2026-10650 with public PoC, OpenCTI CVE-2026-35212, and blender-mcp CVE-2026-10661.
- Active exploitation findings: CISA KEV remains version 2026.06.02 with June 2 additions CVE-2022-0492 (Linux kernel cgroups v1 release_agent privilege escalation/container escape) and CVE-2025-48595 (Android Framework integer overflow/code execution/local privilege escalation), both due 2026-06-05. Carry-forward KEV/exploitation priorities include cPanel CVE-2026-41940, Drupal CVE-2026-9082, Palo Alto PAN-OS CVE-2026-0257, Oracle WebLogic CVE-2024-21182, and Microsoft Defender CVE-2026-41091.
- New malware/campaign intelligence: MalwareBazaar reports 229 submissions in the past 24 hours with Mirai as the most-seen family; SANS ISC reports an SVG phishing wave using embedded JavaScript with `application/ecmascript` MIME labeling to evade simple attachment scanning.
- Exploit-release intelligence: Sploitus homepage static fetch still exposes only the search UI, so the Sploitus top-10 below is reconstructed from indexed Sploitus exploit pages and should be treated as exploit-reference intelligence, not proof that every repository is safe or functional.

## Top Vulnerabilities

| Priority | CVE | Severity | Affected software | Exploit availability | Active exploitation | Confidence | Recommended action |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | CVE-2022-0492 | KEV / High | Linux kernel cgroups v1 `release_agent` | Historical public exploit material exists | Yes - CISA KEV | High | Patch kernels and audit container runtimes for privileged/cgroup v1 exposure; restrict container capabilities and host cgroup mounts. |
| 2 | CVE-2025-48595 | KEV | Android Framework | No public PoC found in this run | Yes - CISA KEV | High | Apply the June 2026 Android security bulletin updates and prioritize managed/mobile fleet remediation. |
| 3 | CVE-2026-8936 | High, 8.2 | Docker Desktop grpcfuse kernel module | No public exploit found | No | High | Update Docker Desktop to 4.76.0 or later; prioritize developer workstations using bind mounts and containers that can create deep directory trees. |
| 4 | CVE-2022-4992 | High, 8.6/8.8 | Drager Infinity Acute Care System and Standalone Infinity M540 patient monitors | No public exploit found | No | High | Segment medical-device networks, review Drager guidance, monitor for spoofed/tampered network messages, and plan vendor remediation. |
| 5 | CVE-2021-4480 / CVE-2021-4481 | High, 8.2 | Drager Protector Software before 6.4.2 | No public exploit found | No | High | Upgrade to 6.4.2 or later and audit local file permissions on Protector hosts. |
| 6 | CVE-2026-10650 | Medium, 5.3 | libwebsockets SSH protocol handler up to 4.5.8 | Public PoC repository and fix commit | No | High | Apply commit `3f9f0c6`/vendor release when available; treat exposed SSH protocol handler deployments as DoS-exposed. |
| 7 | CVE-2026-35212 | Medium, 5.3 | OpenCTI before 7.260227.0 | No public exploit found | No | High | Upgrade OpenCTI to 7.260227.0+; sanitize shared STIX/email-message observables and review session-theft controls. |
| 8 | CVE-2026-10661 | Medium, 4.3 | blender-mcp Hunyuan3D image input handling | Public issue includes reproduction and capture server steps | No | Medium | Apply PR #205/fixed versions; restrict MCP tools that can read local paths and review prompt-injection exposure. |

## Current-Hour NVD Additions

NVD current window: 2026-06-02T22:00:00.000 through 2026-06-02T23:35:00.000 returned 10 records: 5 High, 4 Medium, and 1 Unknown/rejected duplicate.

| CVE | Severity | Summary | Primary/current sources |
| --- | --- | --- | --- |
| CVE-2022-4992 | High 8.6 | Drager M540 network message handling can permit spoofed/tampered data and denial-of-service conditions on patient-monitoring systems. | NVD, VulnCheck, Drager security page |
| CVE-2021-4480 | High 8.2 | Drager Protector Software insecure file permissions allow local arbitrary code execution with elevated privileges. | NVD, VulnCheck, Drager security page |
| CVE-2021-4481 | High 8.2 | Drager Protector Software local privilege escalation via insecure file permissions. | NVD, VulnCheck, Drager security page |
| CVE-2026-8936 | High 8.2 | Docker Desktop VM panic via unbounded recursion in grpcfuse when deep nested bind-mounted directories trigger dentry invalidation. | NVD, Docker Desktop 4.76.0 release notes |
| CVE-2024-14036 | High 7.5 | Drager Core/M540 Converter Service adjacent-network malformed SDC discovery messages can trigger high CPU load/DoS. | NVD, VulnCheck, Drager security page |
| CVE-2025-15653 | Medium 6.8 | Drager Zeus anesthesia workstation local/physical USB interface manipulation can impair therapy functions. | NVD, VulnCheck/Drager references |
| CVE-2026-10650 | Medium 5.3 | libwebsockets SSH parser resource consumption via oversized `msg_len`; public PoC path and fix commit observed. | NVD, GitHub commit, public PoC repository |
| CVE-2026-35212 | Medium 5.3 | OpenCTI XSS in email-message observable body rendering before 7.260227.0. | NVD, GitHub Security Advisory GHSA-rg6r-x26x-63vq |
| CVE-2026-10661 | Medium 4.3 | blender-mcp arbitrary file read/data exfiltration through Hunyuan3D `input_image_url` local path handling. | NVD, GitHub issue #202, PR #205 |
| CVE-2026-42029 | Unknown | Rejected duplicate CVE. | NVD |

## Exploits Released and Public PoC Indicators

### Sploitus Top 10 - reconstructed from indexed Sploitus entries

The Sploitus homepage fetch did not expose an "Exploits of the Week" block. The following list is reconstructed from targeted indexed Sploitus result pages and deduplicated by vulnerability family.

| Rank | Exploit indicator | CVE(s) | Affected software | Exploit type | Maturity / PoC status | Weaponization potential | Confidence |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | Copy Fail / Dirty Frag toolkit | CVE-2026-31431, CVE-2026-43284, CVE-2026-43500 | Linux kernel | Local privilege escalation/page-cache write; container escape potential | Multiple public PoCs and toolkits | High where unpatched local/container access exists | High |
| 2 | cPanel/WHM auth bypass/RCE | CVE-2026-41940 | cPanel/WHM cpsrvd | CRLF injection, auth bypass, WHM root access/RCE | Python/Go PoCs and Metasploit module indexed | Critical; mass exploitation/botnet references observed | High |
| 3 | MCPJam Inspector unauthenticated RCE | CVE-2026-23744 | MCPJam Inspector <= 1.4.2 | Missing auth at `/api/mcp/connect`, reverse shell payloads | Sploitus and PacketStorm-indexed PoCs | High for exposed inspector services | High |
| 4 | Drupal Core PostgreSQL SQL injection | CVE-2026-9082 | Drupal Core with PostgreSQL | Unauthenticated SQL injection; possible RCE in some PostgreSQL configurations | ExploitDB 52608 and Sploitus PoCs | High for internet-facing Drupal/PostgreSQL | High |
| 5 | Sparx Pro Cloud Server / Enterprise Architect chain | CVE-2026-42096 through CVE-2026-42100 | Sparx PCS <= 6.1 build 167 / Enterprise Architect <= 17.1 | Auth bypass, SQL query execution, RCE/DoS components | Public PoC and PacketStorm/Sploitus references | High for exposed PCS deployments | High |
| 6 | Next.js/Drupal patch-to-exploit lab | CVE-2026-44574, CVE-2026-44577, CVE-2026-44578, CVE-2026-44579, CVE-2026-9082 | Next.js and Drupal | SSRF, auth bypass, DoS, SQLi | Lab PoCs indexed by Sploitus | Medium to high depending on exposed vulnerable app paths | Medium |
| 7 | Microsoft Defender RedSun LPE | CVE-2026-33825, CVE-2026-41091 | Microsoft Malware Protection Engine | Link-following LPE to SYSTEM | Public PoC repository indexed | High on unpatched Windows endpoints with local foothold | Medium |
| 8 | Exim Dead.Letter scanner/lab | CVE-2026-45185 | Exim 4.97-4.99.2 GnuTLS builds | UAF/RCE detection and validation lab | Scanner/Nuclei validation lab; not full weaponized RCE in observed entries | Medium; valuable for exposure detection | Medium |
| 9 | nginx-ui zero-credential chain | CVE-2026-27944, CVE-2026-33032, CVE-2026-3888 | nginx-ui and snapd chain references | Backup disclosure, MCP RCE, local privilege escalation | Docker lab and writeups indexed | High if internet-facing nginx-ui remains unpatched | Medium |
| 10 | libwebsockets SSH handler resource exhaustion | CVE-2026-10650 | libwebsockets up to 4.5.8 | Remote resource consumption/DoS | Public PoC path and upstream fix commit | Medium; DoS more likely than code execution | High |

### ExploitDB additions

Direct ExploitDB CSV parsing showed no 2026-06-02 rows. Latest observed rows remain:

- EDB-ID 52608, 2026-06-01: Drupal Core 10.5.5 error-based SQL injection, CVE-2026-9082, unverified.
- EDB-ID 52607, 2026-06-01: WordPress OrderConvo 14 path traversal, CVE-2025-10162, unverified.
- EDB-ID 52606, 2026-05-30: Notepad++ 8.9.6 arbitrary code execution, CVE-2026-48778, unverified.
- EDB-ID 52605/52604/52603, 2026-05-30: YAMCS yamcs-core issues including CVE-2026-44596, CVE-2026-44595, CVE-2026-42568.

### GitHub PoC/repository monitoring

- Strict GitHub repository search for `CVE-2026 PoC exploit created:2026-06-02` returned 0 repositories.
- Broader `CVE-2026 exploit pushed:>=2026-06-02` returned 18 repositories. Notable unvalidated indicators include:
  - `MrForkBomb/CIFSwitch-Checker-CVE-2026-46243` (created 2026-06-02; detection script, not exploit execution).
  - `Defacto-ridgepole254/CVE-2026-41940-Exploit-PoC` (cPanel/WHM auth bypass PoC indicator).
  - `Dullpurple-sloop726/CVE-2026-31431-Linux-Copy-Fail` and `Liverwortenuresis371/copyfail-rs` (Copy Fail LPE indicators).
  - `Recorded-texteditor120/CVE-2026-31802` (npm tar path traversal indicator).
  - `DyniePro/CVE-2026-25643` (Frigate NVR RCE indicator).
- Searches for current-hour CVEs CVE-2026-8936, CVE-2022-4992, CVE-2026-35212, CVE-2026-10661, and CVE-2026-10650 found no newly created high-confidence exploit repositories beyond the already cited upstream issue/PoC paths.
- Caution: these GitHub results are indicators only. No repository was cloned or executed.

## Malware Intelligence

| Source | Finding | Assessment | Confidence |
| --- | --- | --- | --- |
| MalwareBazaar | 229 submissions in the past 24 hours; Mirai is the most-seen malware family; corpus size shown as 1,091,535 samples. | Continued IoT botnet churn; prioritize edge/IoT credential hardening and block known Mirai infrastructure from internal egress where applicable. | High |
| SANS ISC | New wave of phishing emails delivering SVG attachments with embedded JavaScript redirects and `application/ecmascript` MIME type. | Update mail gateway/YARA/content rules to treat SVG as active content and flag ECMAScript-family MIME script blocks, not only `text/javascript`. | High |
| VX-Underground | Web root was reachable in search/fetch but direct deeper fetch timed out in this run; prior GitHub checks showed no newer MalwareSourceCode push after 2026-05-30. | No new VX-sourced malware release was confirmed during this run. | Medium |
| cPanel CVE-2026-41940 exploit ecosystem | Sploitus-indexed remediation/exploit pages reference `nuclear.x86` botnet and XMRig-style miner deployment on compromised cPanel servers. | Treat exposed unpatched cPanel/WHM as already targeted; hunt for forged root sessions, `nuclear.x86`, suspicious WHM API access, and miner artifacts. | Medium |

## Security Releases and Vendor Advisories

| Vendor/source | Release/advisory | Impact | Action |
| --- | --- | --- | --- |
| Docker | Docker Desktop 4.76.0 on 2026-06-01 fixes CVE-2026-8936. | Container-created deep bind-mounted directory trees can trigger VM panic through grpcfuse recursion. | Upgrade Docker Desktop endpoints to 4.76.0+. |
| Drager / VulnCheck | Multiple current-hour Drager medical-device/software CVEs: CVE-2022-4992, CVE-2021-4480, CVE-2021-4481, CVE-2024-14036, CVE-2025-15653. | Medical-device availability, telemetry integrity, and local privilege escalation risks. | Review Drager security guidance, segment clinical networks, and coordinate vendor remediation. |
| GitHub Security Advisories | OpenCTI GHSA-rg6r-x26x-63vq / CVE-2026-35212 published Jun 1; patched in 7.260227.0. | XSS could lead to CSRF and large-scale session theft. | Upgrade OpenCTI and sanitize ingested/shared observables. |
| Android | June 2026 Android security bulletin referenced by CISA KEV for CVE-2025-48595. | Local privilege escalation/code execution risk with evidence of exploitation. | Push mobile fleet updates urgently. |
| Linux kernel/vendors | CISA KEV CVE-2022-0492 added Jun 2 with due date Jun 5. | Container escape/privilege escalation through cgroups v1 release_agent. | Patch, disable/restrict cgroups v1 where possible, and harden container runtime privileges. |
| ExploitDB | Latest direct CSV entries are Jun 1, not Jun 2. | Drupal Core SQLi and WordPress OrderConvo path traversal remain the newest direct ExploitDB additions. | Treat as public PoC/exploit availability for affected assets. |
| Microsoft | No new Microsoft advisory was found in the current hour; carry-forward Defender CVE-2026-41091 remains Sploitus/KEV relevant. | Local SYSTEM escalation with public PoC indicator. | Confirm Defender engine/platform versions meet fixed versions. |
| Cisco/Fortinet/VMware/GitLab | No new current-hour primary advisory was identified in this run. | Continue monitoring; carry-forward FortiClient EMS, Citrix, Palo Alto, and Oracle items remain higher priority where present. | Maintain emergency patch queues for prior KEV/actively exploited edge products. |

## Recommended Actions - Highest to Lowest

1. Remediate CISA KEV additions CVE-2022-0492 and CVE-2025-48595 before the 2026-06-05 due date; treat affected Linux/container hosts and Android fleets as actively exploited exposure classes.
2. Patch or isolate internet-facing cPanel/WHM, Drupal/PostgreSQL, MCPJam Inspector, Palo Alto GlobalProtect, Oracle WebLogic, and Citrix NetScaler assets with known public exploit or active exploitation signals.
3. Upgrade Docker Desktop to 4.76.0+ across developer endpoints, especially where untrusted containers or shared bind mounts are used.
4. Review Drager clinical environments for vulnerable Infinity M540, Core/M540 Converter, Protector Software, and Zeus workstation deployments; enforce segmentation and vendor remediation workflows.
5. Patch libwebsockets deployments using the SSH protocol handler and monitor for oversized SSH packet/resource exhaustion attempts.
6. Upgrade OpenCTI to 7.260227.0+ and review CTI-sharing workflows for HTML/body rendering exposure and session controls.
7. Apply blender-mcp fixes and restrict AI/MCP tools that can read local files, especially when tools can be influenced by untrusted prompts or remote content.
8. Update email security controls for SVG attachments containing script blocks, including `application/ecmascript`, and consider detonating or stripping active SVG content.
9. Treat GitHub PoC repositories as hostile until reviewed; do not execute public exploit code on analyst workstations without sandboxing.
10. Continue hourly monitoring for ExploitDB/PacketStorm mirrors of the current-hour CVEs, since newly published NVD records often lag exploit mirroring by several hours.

## Unified Vulnerability Records

```json
[
  {
    "cve": "CVE-2022-0492",
    "cvss": "7.8 (NVD historical high; KEV-listed)",
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
      "https://nvd.nist.gov/vuln/detail/CVE-2022-0492"
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
    "cve": "CVE-2026-8936",
    "cvss": "8.2 High (NVD CVSS v4.0)",
    "vendor": "Docker",
    "product": "Docker Desktop grpcfuse kernel module",
    "affected_versions": "Docker Desktop before 4.76.0",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://docs.docker.com/desktop/release-notes/#4760",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-8936"
    ]
  },
  {
    "cve": "CVE-2022-4992",
    "cvss": "8.6 High (NVD CVSS v3.1); VulnCheck advisory reports 8.8 CVSS v4.0",
    "vendor": "Drager",
    "product": "Infinity Acute Care System and Standalone Infinity M540 patient monitors",
    "affected_versions": "Infinity Acute Care System <= VG4.2/VG4.1.1/VG4.0.3 and Standalone Infinity M540 <= VG4.2/VG4.1.1",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": false,
    "sources": [
      "https://www.vulncheck.com/advisories/dr-ger-infinity-m540-vg4-spoofed-network-message-handling-dos-tampering",
      "https://static.draeger.com/security",
      "https://nvd.nist.gov/vuln/detail/CVE-2022-4992"
    ]
  },
  {
    "cve": "CVE-2021-4480/CVE-2021-4481",
    "cvss": "8.2 High (NVD CVSS v3.1)",
    "vendor": "Drager",
    "product": "Protector Software",
    "affected_versions": "Protector Software before 6.4.2",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://static.draeger.com/security",
      "https://www.vulncheck.com/advisories/dr-ger-protector-software-local-privilege-escalation-via-insecure-file-permissions",
      "https://nvd.nist.gov/vuln/detail/CVE-2021-4480",
      "https://nvd.nist.gov/vuln/detail/CVE-2021-4481"
    ]
  },
  {
    "cve": "CVE-2026-10650",
    "cvss": "5.3 Medium (NVD CVSS v3.1)",
    "vendor": "warmcat",
    "product": "libwebsockets SSH protocol handler",
    "affected_versions": "libwebsockets up to 4.5.8",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/biniamf/pocs/tree/main/libwebsockets_sshd-parse-ic-unbounded-alloc"
    ],
    "patch_available": true,
    "sources": [
      "https://github.com/warmcat/libwebsockets/commit/3f9f0c6ecaf0e6f3f219d30632c5d1f2479d7498",
      "https://vuldb.com/cve/CVE-2026-10650",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-10650"
    ]
  },
  {
    "cve": "CVE-2026-35212",
    "cvss": "5.3 Medium (NVD CVSS v4.0); GitHub severity Moderate",
    "vendor": "OpenCTI",
    "product": "OpenCTI email-message observable rendering",
    "affected_versions": "OpenCTI before 7.260227.0",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://github.com/OpenCTI-Platform/opencti/security/advisories/GHSA-rg6r-x26x-63vq",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-35212"
    ]
  },
  {
    "cve": "CVE-2026-10661",
    "cvss": "4.3 Medium (NVD CVSS v3.1)",
    "vendor": "ahujasid",
    "product": "blender-mcp",
    "affected_versions": "blender-mcp commits up to 7636d13bded82eca58eb93c3f4cd8708dfdfbe8b per NVD reference",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/ahujasid/blender-mcp/issues/202"
    ],
    "patch_available": true,
    "sources": [
      "https://github.com/ahujasid/blender-mcp/issues/202",
      "https://github.com/ahujasid/blender-mcp/pull/205",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-10661"
    ]
  },
  {
    "cve": "CVE-2026-41940",
    "cvss": "9.8 Critical (reported by exploit/advisory sources)",
    "vendor": "cPanel",
    "product": "cPanel/WHM cpsrvd",
    "affected_versions": "cPanel/WHM 11.40 and later before fixed builds 11.110.0.97, 11.118.0.63, 11.126.0.54, 11.132.0.29, 11.134.0.20, 11.136.0.5",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://sploitus.com/exploit?id=8C342626-75CE-5DB6-935E-A431EECC0B39",
      "https://sploitus.com/exploit?id=MSF%3AEXPLOIT-MULTI-HTTP-CPANEL_WHM_AUTH_BYPASS_RCE-"
    ],
    "patch_available": true,
    "sources": [
      "https://sploitus.com/exploit?id=8C342626-75CE-5DB6-935E-A431EECC0B39",
      "https://sploitus.com/exploit?id=AD23DFC2-DC02-55EC-8817-4F88A42E20AC",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"
    ]
  },
  {
    "cve": "CVE-2026-9082",
    "cvss": "6.5 Medium in NVD; Drupal rates highly critical due to unauthenticated SQL injection/RCE paths",
    "vendor": "Drupal",
    "product": "Drupal Core PostgreSQL database abstraction layer",
    "affected_versions": "Drupal core >= 8.9.0 through vulnerable 10.x/11.x ranges before patched releases",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://sploitus.com/exploit?id=458CE696-FE39-500F-9131-2E24B1BC2E12",
      "https://gitlab.com/exploit-database/exploitdb/-/raw/main/files_exploits.csv"
    ],
    "patch_available": true,
    "sources": [
      "https://www.drupal.org/sa-core-2026-004",
      "https://sploitus.com/exploit?id=458CE696-FE39-500F-9131-2E24B1BC2E12",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"
    ]
  },
  {
    "cve": "CVE-2026-23744",
    "cvss": "9.8 Critical",
    "vendor": "MCPJam",
    "product": "MCPJam Inspector",
    "affected_versions": "MCPJam Inspector <= 1.4.2",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://sploitus.com/exploit?id=254A6F19-4F33-5786-90FC-3146F3468F08",
      "https://sploitus.com/exploit?id=PACKETSTORM%3A217697"
    ],
    "patch_available": true,
    "sources": [
      "https://sploitus.com/exploit?id=254A6F19-4F33-5786-90FC-3146F3468F08",
      "https://sploitus.com/exploit?id=PACKETSTORM%3A217697"
    ]
  }
]
```

## Source Notes

- NVD API current window returned the current-hour CVE set used above.
- CISA KEV feed: catalogVersion 2026.06.02, dateReleased 2026-06-02T17:04:13.1193Z, 1610 total records.
- ExploitDB CSV was parsed directly from the upstream repository.
- Sploitus homepage fetch returned only static search UI text; Sploitus entries were collected through targeted indexed result pages.
- Packet Storm direct browsing/search was partly limited by anti-abuse/terms interstitials; PacketStorm references are cited where indexed through Sploitus or search results.
- GitHub repository search results are unvalidated indicators; no PoC code was downloaded or executed.
