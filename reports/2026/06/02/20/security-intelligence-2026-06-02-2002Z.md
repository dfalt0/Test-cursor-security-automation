# Security Intelligence Report - 2026-06-02 20:02 UTC

Automation run: `03015b72-ed4b-4a70-ae12-7df8f53b90ea`  
Repository: `dfalt0/Test-cursor-security-automation`  
Branch: `cursor/security-intelligence-agent-c4e4`  
Analyst posture: CTI/vulnerability intelligence, enterprise prioritization

## Executive Summary

- **NVD intake:** 0 CVEs were published in the 19:00-20:35 UTC window. Day-to-date NVD intake remains **146 CVEs**: 9 critical, 44 high, 72 medium, 9 low, and 12 unknown. Rolling 24h intake is **280 CVEs**: 12 critical, 109 high, 127 medium, 20 low, and 12 unknown.
- **Critical findings requiring action:** No brand-new NVD CVEs appeared this hour, but high-priority items disclosed earlier today or newly refreshed by exploit activity remain urgent: Progress Sitefinity CVE-2026-7312/CVE-2026-7198, Spacelabs Sentinel CVE-2026-0611, OpenClaude CVE-2026-42074, OpenMed CVE-2026-47117, GNU Inetutils telnetd CVE-2026-24061, Cisco SD-WAN CVE-2026-20182, cPanel/WHM CVE-2026-41940, and Drupal CVE-2026-9082.
- **Active exploitation / KEV:** CISA KEV catalog version `2026.06.02` added **CVE-2022-0492** (Linux kernel cgroups v1 release_agent privilege escalation/container escape) and **CVE-2025-48595** (Android Framework local code execution / elevation of privilege) earlier today; both have a 2026-06-05 due date. Carry-forward KEV/active exploitation priorities include Cisco SD-WAN CVE-2026-20182, cPanel/WHM CVE-2026-41940, FortiClient EMS CVE-2026-35616, PAN-OS CVE-2026-0257, Drupal CVE-2026-9082, and Oracle WebLogic CVE-2024-21182.
- **Exploit release signal:** Sploitus homepage static fetch did not expose an "Exploits of the Week" block; the Sploitus Top 10 below is reconstructed from indexed Sploitus result pages and should be treated as exploit-intelligence indicators. ExploitDB direct CSV still shows the latest entries as 2026-06-01 (Drupal CVE-2026-9082 and WordPress OrderConvo CVE-2025-10162). GitHub strict created-today search returned 0 repos, but a newly pushed CVE-2026-24061 telnetd auth-bypass PoC indicator appeared at 19:54 UTC.
- **Malware intelligence:** VX-Underground GitHub content shows no new MalwareSourceCode commit since 2026-05-30. MalwareBazaar browse reports **249 submissions in the past 24h**, with **Mirai** the most-seen family. cPanel/WHM CVE-2026-41940 remains tied to "Sorry" ransomware and `nuclear.x86`/Mirai activity in secondary reporting.

## Source Coverage and Validation Notes

- **Primary/structured sources checked:** NVD API, CISA KEV JSON, GitHub reviewed advisories API, GitHub repository search, ExploitDB CSV, Sploitus homepage and indexed Sploitus result pages, VX-Underground GitHub repositories, MalwareBazaar browse, vendor/research advisories for Progress Sitefinity, Spacelabs, OpenClaude, Cisco, Microsoft/CCB, cPanel, Drupal, Fortinet, AWS Kiro, Android, and VulnCheck.
- **Confidence model:** "High" means primary vendor/government/NVD confirmation and clear remediation. "Medium" means strong secondary corroboration or public exploit indicators, but limited direct vendor confirmation for exploitation. "Low" means unvalidated repository/search indicator or non-standard CVE placeholder.
- **GitHub/Sploitus caution:** Repository existence and Sploitus indexing do **not** prove exploit functionality. PoC references below are indicators requiring sandboxed review before operational use.

## Top Vulnerabilities

| Priority | CVE | Severity | Affected software | Exploit availability | Active exploitation / KEV | Recommended action | Confidence |
|---:|---|---|---|---|---|---|---|
| 1 | CVE-2026-20182 | Critical, CVSS 10.0 | Cisco Catalyst SD-WAN Controller / Manager | Public exploit indicators on Sploitus and researcher coverage | Cisco reports limited exploitation; CISA KEV | Upgrade to fixed Cisco releases, preserve logs, run Cisco IOC checks, open TAC case for suspected compromise, restrict NETCONF exposure | High |
| 2 | CVE-2026-41940 | Critical, CVSS 9.8 | cPanel & WHM after 11.40 before fixed release tracks | Metasploit/watchTowr and GitHub PoC indicators; Sploitus indexed | Mass exploitation reported; CISA KEV; ransomware/botnet activity | Force update to patched cPanel/WHM builds, restrict ports 2082/2083/2086/2087/2095/2096, hunt for new admin accounts, `.sorry` files, `nuclear.x86`, and persistence changes | High |
| 3 | CVE-2026-24061 | Critical, CVSS 9.8 | GNU Inetutils telnetd through 2.7 | GitHub PoC repos; newly pushed `obrunolima1910/CVE-2026-24061` at 19:54 UTC | Active-exploitation claims from government/secondary reporting; not observed in CISA KEV in this run | Disable telnetd, block TCP/23, upgrade Inetutils or apply distro patches, monitor TELNET NEW-ENVIRON `USER` values starting with `-` | Medium |
| 4 | CVE-2026-7312 / CVE-2026-7198 | Critical, CVSS 10.0 / 9.8 | Progress Sitefinity OData/web services | No public exploit confirmed in this run | No active exploitation observed | Apply Progress Sitefinity June 2 product updates; prioritize internet-facing Sitefinity, Sitefinity Insight integrations, and 15.4 deployments | High |
| 5 | CVE-2026-0611 | Critical, CVSS 9.8 | Spacelabs Healthcare Sentinel 10.5.x and 11.x before 11.6.0 | No public exploit confirmed; RCE path described by VulnCheck/NVD | No active exploitation observed | Upgrade to Sentinel 11.6.0 or vendor guidance; ensure .NET Remoting port 8989 is not network-accessible | High |
| 6 | CVE-2026-42074 | Critical, CVSS 9.3 | OpenClaude before 0.5.1 | Advisory includes PoC-like model-controlled sandbox bypass details | No active exploitation observed | Upgrade to 0.5.1+, set `allowUnsandboxedCommands=false`, rotate credentials accessible to agent hosts | High |
| 7 | CVE-2026-9082 | Critical, CVSS 9.8 | Drupal core PostgreSQL-backed deployments | ExploitDB EDB-ID 52608 and multiple Sploitus/GitHub PoC indicators | CISA KEV; exploitation attempts reported in Sploitus-indexed content | Upgrade Drupal to fixed branches; confirm PostgreSQL backend exposure; review JSON:API access and database logs | High |
| 8 | CVE-2022-0492 | High, CVSS 7.8 | Linux kernel cgroups v1 release_agent | PacketStorm/Metasploit Docker cgroups container-escape references | Added to CISA KEV on 2026-06-02 | Patch kernels/container hosts, disable/limit cgroups v1 release_agent exposure, review container runtime hardening | High |
| 9 | CVE-2025-48595 | High, CVSS 8.4 | Android Framework | No public exploit observed in this run | Added to CISA KEV on 2026-06-02 | Apply Android June 2026 security bulletin updates and prioritize managed/mobile fleet coverage | High |
| 10 | CVE-2026-23744 | Critical, CVSS 9.8 | MCPJam Inspector <= 1.4.2 | PacketStorm/Sploitus RCE exploit indicator | No active exploitation observed | Upgrade to 1.4.3+, bind local development tools to localhost, restrict `/api/mcp/connect` exposure | High |
| 11 | CVE-2026-47117 | Critical, CVSS 9.8 | OpenMed before 1.5.2 | No public exploit confirmed; NVD/VulnCheck advisory describes unauthenticated model-loading RCE | No active exploitation observed | Upgrade to 1.5.2+, block untrusted Hugging Face model loading paths, audit exposed OpenMed services | High |
| 12 | CVE-2026-10591 | High, CVSS 8.8 | Amazon Kiro IDE before 0.11 | No public exploit confirmed | No active exploitation observed | Upgrade Kiro IDE to 0.11+, audit workspace auto-execution paths such as `.vscode/tasks.json` | High |

## Exploits Released / Public PoC Indicators

### Sploitus Top 10 (reconstructed)

Static fetch of `https://sploitus.com/` only returned the application shell and did not expose "Exploits of the Week". The following are the top distinct indexed exploit indicators collected from Sploitus search results, deduplicated by vulnerability and scored for enterprise weaponization potential.

| Rank | CVE / ID | Affected software | Exploit type | Maturity | Public PoC | Weaponization potential | Notes |
|---:|---|---|---|---|---|---|---|
| 1 | CVE-2026-41940 | cPanel & WHM | Pre-auth auth bypass to RCE/root | Metasploit / public script indicators | Yes | Critical | Active ransomware/Mirai activity; KEV-listed |
| 2 | CVE-2026-9082 | Drupal core, PostgreSQL backend | Unauthenticated SQL injection, possible RCE by configuration | ExploitDB EDB-ID 52608 plus multiple PoCs | Yes | Critical | KEV-listed; internet-facing CMS risk |
| 3 | CVE-2026-23744 | MCPJam Inspector <= 1.4.2 | Unauthenticated RCE via MCP server installation request | PacketStorm exploit indexed by Sploitus | Yes | Critical | Dev-tool exposure risk; fixed in 1.4.3 |
| 4 | CVE-2026-31431 | Linux kernel "Copy Fail" | Local privilege escalation / possible container escape path | Multiple public PoCs/ports | Yes | High | Local access required; broad Linux/cloud impact |
| 5 | CVE-2026-2329 | GrandStream GXP1600 | Unauthenticated remote code execution | Metasploit module indicator | Yes | High | Network/VoIP device exposure risk |
| 6 | CVE-2026-48778 | Notepad++ | Arbitrary code execution | ExploitDB/Sploitus indicator | Yes | Medium | User interaction likely; workstation exposure |
| 7 | CVE-2026-42568 | YAMCS yamcs-core | LDAP injection | ExploitDB/Sploitus indicator | Yes | Medium | Requires affected YAMCS deployment context |
| 8 | CVE-2026-47668 | DbGate / dbgate-serve <= 7.1.8 | Unauthenticated or weak-auth JSON runner RCE | Public PoC indicator | Yes | High | Validate auth posture before prioritizing |
| 9 | CVE-2026-1560 | WordPress Lazy Blocks <= 4.2.0 | Authenticated RCE via REST preview | Public PoC indicator | Yes | Medium | Requires contributor-like access; CVE details need validation |
| 10 | CVE-2026-BetterSQLCipher-RCE | better-sqlcipher | `loadExtension()` arbitrary code execution | Public repository indicator | Yes | Low/Medium | Non-standard/unassigned ID; treat as research indicator pending CVE/vendor validation |

### ExploitDB additions

- Direct ExploitDB CSV latest rows remain **2026-06-01**:
  - EDB-ID 52608: Drupal Core 10.5.5 error-based SQL injection, CVE-2026-9082.
  - EDB-ID 52607: WordPress OrderConvo 14 path traversal, CVE-2025-10162.
- No direct ExploitDB CSV row dated 2026-06-02 was observed in this run.

### GitHub PoC / repository indicators

- Strict query `CVE-2026 PoC exploit created:2026-06-02` returned **0 repositories**.
- Broader pushed-today searches found unvalidated indicators:
  - `obrunolima1910/CVE-2026-24061`, pushed 2026-06-02 19:54 UTC; claims GNU Inetutils telnetd auth bypass.
  - `DyniePro/CVE-2026-25643`, pushed 2026-06-02 16:03 UTC; claims Frigate NVR RCE.
  - `Dullpurple-sloop726/CVE-2026-31431-Linux-Copy-Fail`, pushed 2026-06-02 16:43 UTC; Linux Copy Fail LPE.
  - `Defacto-ridgepole254/CVE-2026-41940-Exploit-PoC`, pushed 2026-06-02 16:44 UTC; cPanel/WHM auth bypass.
  - `Liverwortenuresis371/copyfail-rs`, pushed 2026-06-02 16:42 UTC; Linux Copy Fail related.
- These repositories were not cloned or executed. Treat as untrusted until reviewed for malicious behavior.

## Malware Intelligence

- **VX-Underground:** GitHub user/repository checks show `vxunderground/MalwareSourceCode` as the most recently pushed VX repository, last pushed 2026-05-30. Latest visible commit `1623926c24245e52378f36a6a8d3bd403166a87d` is "Add files via upload"; prior automation identified this as adding `Python/Stealer.Python.GMBA.Manipulator.7z`. No new VX malware-source commit was observed during this run.
- **MalwareBazaar / Abuse.ch:** Browse page reports **249 submissions in the past 24 hours** and **Mirai** as the most-seen malware family. This supports continued monitoring of IoT/Linux botnet activity.
- **Ransomware / botnet activity:** cPanel/WHM CVE-2026-41940 remains associated in secondary reporting with "Sorry" ransomware and `nuclear.x86` Mirai-based payload deployment. Confidence is medium-high due to multiple corroborating media/research sources plus KEV listing, but the report did not independently validate malware samples.
- **Supply chain:** CISA KEV carry-forward items include malicious-code/supply-chain entries for Nx Console CVE-2026-48027 and TanStack CVE-2026-45321 from 2026-05-27. Continue credential rotation and package-lock review where affected packages/extensions were installed.

## Security Releases and Vendor Advisories

- **Progress Sitefinity:** June 2 vendor advisory covers CVE-2026-7312, CVE-2026-7198, CVE-2026-7195, CVE-2026-7201, and CVE-2026-7313. Updates are available for supported versions.
- **Spacelabs Healthcare:** Sentinel CVE-2026-0611 affects 10.5.x and 11.x before 11.6.0; vendor/VulnCheck guidance indicates update to 11.6.0 and restrict port 8989.
- **OpenClaude:** CVE-2026-42074 fixed in 0.5.1; default sandbox-bypass behavior should be disabled where patching is delayed.
- **OpenMed:** CVE-2026-47117 fixed in 1.5.2.
- **AWS Kiro IDE:** CVE-2026-10591 remediated in version 0.11 or later.
- **Android:** June 2026 bulletin is referenced by NVD for CVE-2025-48595; CISA KEV due date is 2026-06-05.
- **Cisco:** Catalyst SD-WAN CVE-2026-20182 remains active/KEV; Cisco recommends fixed releases and TAC engagement for suspected compromise.
- **Microsoft:** No new MSRC release was identified in this hour; carry-forward May Patch Tuesday priority remains Windows Netlogon CVE-2026-41089 based on CCB Belgium's May 29 active-exploitation update.
- **Fortinet:** FortiClient EMS CVE-2026-35616 remains a KEV/exploitation carry-forward priority; patch per FortiGuard FG-IR-26-099.
- **GitHub reviewed advisories:** Latest reviewed advisories returned by the API were from 2026-06-01; no reviewed GitHub advisory published after 19:00 UTC was observed in the fetched page.

## Recommended Actions (ranked)

1. **Emergency patch and hunt:** Cisco SD-WAN CVE-2026-20182, cPanel/WHM CVE-2026-41940, Drupal CVE-2026-9082, FortiClient EMS CVE-2026-35616, PAN-OS CVE-2026-0257, Oracle WebLogic CVE-2024-21182, CVE-2022-0492, and Android CVE-2025-48595 because of KEV or active exploitation signals.
2. **Disable or eliminate legacy exposed services:** Remove GNU Inetutils telnetd exposure for CVE-2026-24061; if telnet cannot be eliminated, apply vendor/distro fixes and block TCP/23 from untrusted networks.
3. **Patch June 2 critical enterprise apps:** Progress Sitefinity, Spacelabs Sentinel, OpenClaude, OpenMed, and Kiro IDE. Prioritize internet-facing deployments and systems with access to secrets or production code.
4. **Harden developer/AI tooling:** Bind local dev tools to localhost, restrict MCP/agent endpoints, disable unsandboxed command execution defaults, and rotate credentials accessible to coding agents or model-executed tools.
5. **Exploit repo safety:** Do not run new GitHub PoCs directly. Review source in an isolated sandbox, inspect install scripts/binaries, and block outbound access during triage.
6. **Malware monitoring:** Watch for Mirai-family ELF payloads, `nuclear.x86`, cPanel suspicious admin creation, `.sorry` encrypted files, and unexpected Linux web-hosting persistence changes.

## Unified Vulnerability Records

```json
[
  {
    "cve": "CVE-2026-20182",
    "cvss": "10.0",
    "vendor": "Cisco",
    "product": "Catalyst SD-WAN Controller / Manager",
    "affected_versions": "See Cisco advisory cisco-sa-sdwan-rpa2-v69WY2SW",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://sec.cloudapps.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-sdwan-rpa2-v69WY2SW"],
    "patch_available": true,
    "sources": ["NVD", "CISA KEV", "Cisco PSIRT", "Sploitus indexed results"]
  },
  {
    "cve": "CVE-2026-41940",
    "cvss": "9.8",
    "vendor": "cPanel",
    "product": "cPanel & WHM",
    "affected_versions": "After 11.40 before fixed release-track builds including 11.136.0.5",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://github.com/watchtowrlabs/watchTowr-vs-cPanel-WHM-AuthBypass-to-RCE.py", "https://sploitus.com/exploit?id=MSF%3AEXPLOIT-MULTI-HTTP-CPANEL_WHM_AUTH_BYPASS_RCE-"],
    "patch_available": true,
    "sources": ["NVD", "CISA KEV", "cPanel advisory", "BleepingComputer", "Help Net Security", "Sploitus"]
  },
  {
    "cve": "CVE-2026-24061",
    "cvss": "9.8",
    "vendor": "GNU",
    "product": "Inetutils telnetd",
    "affected_versions": "Through 2.7",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": false,
    "poc_links": ["https://github.com/obrunolima1910/CVE-2026-24061", "https://www.openwall.com/lists/oss-security/2026/01/20/2"],
    "patch_available": true,
    "sources": ["NVD", "Openwall", "GNU Inetutils commits", "GitHub search", "CCB/secondary reporting"]
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
    "sources": ["NVD", "Progress Sitefinity advisory"]
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
    "sources": ["NVD", "Progress Sitefinity advisory"]
  },
  {
    "cve": "CVE-2026-0611",
    "cvss": "9.8",
    "vendor": "Spacelabs Healthcare",
    "product": "Sentinel",
    "affected_versions": "10.5.x and 11.x before 11.6.0",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["NVD", "Spacelabs advisory", "VulnCheck"]
  },
  {
    "cve": "CVE-2026-42074",
    "cvss": "9.3",
    "vendor": "OpenClaude",
    "product": "openclaude",
    "affected_versions": "Before 0.5.1",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://github.com/Gitlawb/openclaude/security/advisories/GHSA-m77w-p5jj-xmhg", "https://osv.dev/vulnerability/GHSA-m77w-p5jj-xmhg"],
    "patch_available": true,
    "sources": ["NVD", "GitHub Security Advisory", "OSV", "GitLab Advisory Database"]
  },
  {
    "cve": "CVE-2026-9082",
    "cvss": "9.8",
    "vendor": "Drupal",
    "product": "Drupal core",
    "affected_versions": "8.9.0 before 10.4.10, 10.5.0 before 10.5.10, 10.6.0 before 10.6.9, 11.0.0 before 11.1.10, 11.2.0 before 11.2.12, 11.3.0 before 11.3.10",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://www.exploit-db.com/exploits/52608", "https://www.drupal.org/sa-core-2026-004"],
    "patch_available": true,
    "sources": ["NVD", "CISA KEV", "Drupal advisory", "ExploitDB", "Sploitus"]
  },
  {
    "cve": "CVE-2022-0492",
    "cvss": "7.8",
    "vendor": "Linux",
    "product": "Kernel cgroups v1",
    "affected_versions": "Kernel versions exposing vulnerable cgroup_release_agent_write / cgroups v1 release_agent behavior",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["http://packetstormsecurity.com/files/176099/Docker-cgroups-Container-Escape.html"],
    "patch_available": true,
    "sources": ["NVD", "CISA KEV", "PacketStorm", "Linux kernel commit"]
  },
  {
    "cve": "CVE-2025-48595",
    "cvss": "8.4",
    "vendor": "Google",
    "product": "Android Framework",
    "affected_versions": "See Android 2026-06-01 security bulletin",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": ["NVD", "CISA KEV", "Android Security Bulletin"]
  },
  {
    "cve": "CVE-2026-23744",
    "cvss": "9.8",
    "vendor": "MCPJam",
    "product": "Inspector",
    "affected_versions": "1.4.2 and earlier",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://github.com/MCPJam/inspector/security/advisories/GHSA-232v-j27c-5pp6", "https://sploitus.com/exploit?id=PACKETSTORM%3A217697"],
    "patch_available": true,
    "sources": ["NVD", "GitHub Security Advisory", "Sploitus", "PacketStorm indexed result"]
  },
  {
    "cve": "CVE-2026-47117",
    "cvss": "9.8",
    "vendor": "OpenMed",
    "product": "OpenMed",
    "affected_versions": "Before 1.5.2",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["NVD", "GitHub release", "VulnCheck"]
  },
  {
    "cve": "CVE-2026-10591",
    "cvss": "8.8",
    "vendor": "Amazon",
    "product": "Kiro IDE",
    "affected_versions": "Before 0.11",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["NVD", "AWS security bulletin", "Kiro changelog"]
  }
]
```

## References

- NVD API: `https://services.nvd.nist.gov/rest/json/cves/2.0`
- CISA KEV JSON: `https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json`
- Sploitus: `https://sploitus.com/`
- ExploitDB CSV: `https://gitlab.com/exploit-database/exploitdb/-/raw/main/files_exploits.csv`
- GitHub Advisories API: `https://api.github.com/advisories`
- Progress Sitefinity advisory: `https://community.progress.com/s/article/Sitefinity-Security-Advisory-for-Addressing-Security-Vulnerabilities-CVE-2026-7312-CVE-2026-7198-CVE-2026-7195-CVE-2026-7201-CVE-2026-7313-May-2026`
- VulnCheck Spacelabs advisory: `https://www.vulncheck.com/advisories/spacelabs-healthcare-sentinel-x-unauthenticated-rce-via-net-remoting`
- OpenClaude GHSA: `https://github.com/Gitlawb/openclaude/security/advisories/GHSA-m77w-p5jj-xmhg`
- Cisco SD-WAN advisory: `https://sec.cloudapps.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-sdwan-rpa2-v69WY2SW`
- Drupal SA-CORE-2026-004: `https://www.drupal.org/sa-core-2026-004`
- MalwareBazaar browse: `https://bazaar.abuse.ch/browse/`
