# Security Intelligence Report - 2026-06-02 18:01 UTC

## Executive Summary

- Reporting window: primary delta from 2026-06-02 17:00-18:35 UTC, with carry-forward correlation for still-active KEV, exploit, ransomware, and supply-chain items.
- Total CVEs discovered in target NVD window: 16 (2 critical, 4 high, 9 medium, 1 low). Day-to-date NVD count: 146 CVEs (9 critical, 43 high, 63 medium, 19 low, 12 unknown). Rolling 24-hour count: 336 CVEs (17 critical, 128 high, 135 medium, 43 low, 13 unknown).
- Critical findings: Spacelabs Healthcare Sentinel CVE-2026-0611 unauthenticated RCE via exposed .NET Remoting; OpenClaude CVE-2026-42074 model-controlled sandbox bypass; new CISA KEV additions for Android Framework CVE-2025-48595 and Linux Kernel CVE-2022-0492.
- Active exploitation findings: CISA KEV catalog version 2026.06.02 added CVE-2022-0492 and CVE-2025-48595 on 2026-06-02. Carry-forward active exploitation remains material for cPanel/WHM CVE-2026-41940, FortiClient EMS CVE-2026-35616, Cisco SD-WAN CVE-2026-20182, PAN-OS CVE-2026-0257, Drupal Core CVE-2026-9082, Citrix NetScaler CVE-2026-3055, and Oracle WebLogic CVE-2024-21182.
- New malware campaigns: no new vx-underground GitHub push after 2026-05-30, but MalwareBazaar reports 249 submissions in the last 24 hours with Mirai as the most-seen family. Continue prioritizing cPanel "Sorry" ransomware/nuclear.x86, FortiClient EMS EKZ Infostealer, and Red Hat npm "Miasma" supply-chain malware.
- Important vendor/security releases: CISA KEV 2026.06.02, Android June 2026 bulletin, Spacelabs Sentinel 11.6.0 advisory, OpenClaude GitHub advisories, NVIDIA NVTabular advisory, Dell ThinOS DSA-2026-214, TP-Link Tapo firmware release notes, and ExploitDB latest CSV entries.

## Source Coverage and Caveats

- Sploitus homepage was fetched directly, but the static page exposed only the search shell and did not expose an official "Exploits of the Week" block. The Sploitus Top 10 below is therefore an indexed-search reconstruction, not an official ranking.
- GitHub reviewed advisories published or updated after 17:00 UTC returned no entries. Strict repo search for newly created `CVE-2026 PoC exploit created:>=2026-06-02` returned no repositories; broader pushed-search results are treated as unvalidated indicators.
- GitHub PoC repositories and Sploitus entries were not executed. Public PoC availability is reported as an indicator, not proof of functionality.
- OpenClaude patch status is inconsistent across sources: NVD references OpenClaude prior to 0.5.1 and a v0.5.1 release/commit, while the primary GitHub advisory fetched during this run still lists "Patched versions: None." Treat remediation as requiring verification against the upstream repository and configuration hardening.
- Some search snippets contradicted current direct feeds. CISA KEV JSON is treated as authoritative over stale search snippets for KEV status.

## Top Vulnerabilities

| Priority | CVE | Severity | Affected software | Exploit availability | Active exploitation | Recommended action | Confidence |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | CVE-2025-48595 | Critical by KEV priority; NVD high 8.4 | Android Framework, Android 14/15/16/16 QPR2 | No public PoC confirmed in this run | Yes - CISA KEV added 2026-06-02; Google bulletin/search reporting describes limited targeted exploitation | Ensure Android security patch level 2026-06-05 or later across managed fleets; prioritize high-risk users and mobile device management compliance checks | High |
| 2 | CVE-2022-0492 | Critical by KEV priority; NVD high | Linux Kernel cgroups v1 release_agent privilege escalation/container escape | Yes - Sploitus indexed Metasploit Docker cgroups container escape module | Yes - CISA KEV added 2026-06-02 | Patch Linux kernels; inventory privileged containers and cgroups v1 exposure; disable unnecessary privileged containers and monitor release_agent writes | High |
| 3 | CVE-2026-0611 | Critical 9.2 | Spacelabs Healthcare Sentinel 10.5.x and 11.x before 11.6.0 | No Sploitus/GitHub PoC observed; VulnCheck advisory provides exploitation path | Not observed | Upgrade Sentinel to 11.6.0 or later; verify .NET Remoting port 8989 is not network-accessible; segment clinical networks | High |
| 4 | CVE-2026-42074 | Critical 9.3 | OpenClaude npm package / AI coding-agent BashTool sandbox decision logic | Yes - primary GitHub advisory contains PoC logic and tests | Not observed | Treat all agent hosts as high risk; disable unsandboxed commands, review tool schemas, rotate credentials exposed to vulnerable agents, and verify upstream patch status | High |
| 5 | CVE-2026-41940 | Critical 9.8 | cPanel & WHM and WP Squared | Yes - Sploitus, Metasploit, ExploitDB, watchTowr references, multiple GitHub indicators | Yes - KEV; mass exploitation with "Sorry" ransomware and nuclear.x86/Mirai variant | Patch to fixed cPanel/WHM trains immediately; hunt for `.sorry` files, unauthorized SSH keys, UID 0 accounts, and suspicious session metadata | High |
| 6 | CVE-2026-35616 | Critical/High operational priority | FortiClient Enterprise Management Server | Public exploitation details reported; no new PoC executed | Yes - KEV and Arctic Wolf EKZ Infostealer campaign | Upgrade FortiClient EMS to 7.4.7 or later; restrict management access; hunt for FortiEndpoint_Patch.exe/p.exe and EMS certificate log anomalies | High |
| 7 | CVE-2026-20182 | Critical 10.0 | Cisco Catalyst SD-WAN Controller/Manager | Public exploit indicators in prior runs; CISA emergency directive context | Yes - KEV and limited exploitation reports | Apply Cisco fixes and CISA ED 26-03 hunt/hardening guidance; check internet exposure and admin account anomalies | High |
| 8 | CVE-2026-3055 | Critical 9.8 | Citrix NetScaler ADC/Gateway SAML IDP configurations | Public reporting indicates exploitation; no new PoC validated | Yes - KEV; secondary reporting cites Fortinet large-scale exploitation | Patch NetScaler; review SAML IDP exposure, sessions, and appliance indicators; isolate vulnerable appliances | Medium |
| 9 | CVE-2026-9082 | Critical by exploit/KEV priority | Drupal Core PostgreSQL-backed JSON:API deployments | Yes - ExploitDB EDB-ID 52608 and multiple Sploitus PoCs | Yes - KEV and active attempts from prior runs | Upgrade Drupal to fixed releases; prioritize PostgreSQL-backed sites with JSON:API enabled; review web logs for filter-key SQLi attempts | High |
| 10 | CVE-2026-0257 | Critical/High operational priority | Palo Alto Networks PAN-OS VPN/authentication flow | Public indicators exist; no new PoC validated this hour | Yes - KEV | Apply Palo Alto fixes; audit VPN sessions and unauthorized access; restrict management and VPN exposure | High |
| 11 | CVE-2026-1871 | High 7.1 | TP-Link Tapo C200 v5 RTSP authentication handling | No public PoC observed; vendor release-note references only | Not observed | Update Tapo C200 firmware; restrict camera RTSP access to trusted networks | Medium |
| 12 | CVE-2026-24221 / CVE-2026-24237 | High 7.8 | NVIDIA NVTabular deserialization | No public PoC observed | Not observed | Apply NVIDIA advisory updates; avoid processing untrusted artifacts in vulnerable NVTabular pipelines | High |
| 13 | CVE-2026-10611 | High 8.2 | MISP with LDAP mixed authentication and OTP enforcement | No public PoC observed | Not observed | Apply MISP commit/fix; review LDAP mixed-auth and OTP enforcement configurations | Medium |
| 14 | CVE-2026-49943 | Medium 6.3 | CZ.NIC BIRD Internet Routing Daemon through 2.19.0 | No public PoC observed | Not observed | Track BIRD upstream fixes; apply route-filter sanity limits for long AS_PATH/community data; monitor BGP process crashes | Medium |

## Exploits Released

### Sploitus Top 10 (Indexed Reconstruction)

| Rank | Indicator | Affected software | Exploit type | Maturity | PoC availability | Weaponization potential | Confidence |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | CVE-2022-0492 Docker cgroups Container Escape | Linux Kernel / Docker privileged container contexts | Local privilege escalation / container escape | Mature Metasploit module indicator | Public module indexed by Sploitus | High where privileged containers or vulnerable kernels persist | High |
| 2 | CVE-2026-41940 cPanel/WHM auth bypass RCE | cPanel & WHM / WP Squared | Remote auth bypass to admin/session abuse/RCE | Mature; Sploitus lists Metasploit and ExploitDB paths | Public PoCs and scanner/exploit indicators | Very high; already tied to ransomware and botnet payloads | High |
| 3 | CVE-2026-9082 Drupal Core SQL injection | Drupal Core with PostgreSQL/JSON:API | Unauthenticated SQL injection | Multiple PoCs and ExploitDB EDB-ID 52608 | Public PoC/lab code indicators | High for exposed Drupal sites, especially if chained to privilege escalation/RCE | High |
| 4 | CVE-2026-48778 Notepad++ arbitrary code execution | Notepad++ 8.9.6 | Local/user-context arbitrary code execution via config manipulation | Packet Storm/ExploitDB-style script | Public exploit script indicator | Medium; requires local/config-write precondition | Medium |
| 5 | CVE-2026-42568 YAMCS LDAP injection | YAMCS LDAP auth module | Authentication bypass via LDAP injection | Public write-up/exploit indicator | Public PoC indicator | High if LDAP auth is enabled and YAMCS is reachable | Medium |
| 6 | CVE-2026-35570 OpenClaude sandbox path traversal bypass | OpenClaude v0.1.7 | Sandbox/path traversal bypass | Public technical write-up | Public PoC steps | Medium to high for agent hosts with sensitive files | Medium |
| 7 | CVE-2026-8206 Kirki WordPress account takeover | Kirki WordPress plugin | Account takeover/privilege escalation | Sploitus indicator with sparse detail | Public indicator only | High if functional, due WordPress admin takeover potential | Low |
| 8 | CVE-2026-20980/20981/20982 Android chain | Android/system components | AT command/system command/file-write chain | Public PoC demo indicator | Public PoC indicator | Medium to high; platform/version constraints need validation | Low |
| 9 | CVE-2026-BetterSQLCipher-RCE | better-sqlcipher | Claimed RCE via loadExtension | Non-standard CVE placeholder; unvalidated | Public GitHub-style indicator | Unknown; treat as suspicious until CVE assignment and vendor confirmation | Low |
| 10 | CVE-2026-0073 Android authentication algorithm | Android | Authentication algorithm implementation issue | Sparse Sploitus indicator | Public indicator only | Unknown pending primary validation | Low |

### ExploitDB Direct CSV Additions

Direct CSV fetch from ExploitDB GitLab showed latest IDs by numeric order; date fields were null in the CSV:

- EDB-ID 52608: Drupal Core 10.5.5 - Error-Based SQL Injection, CVE-2026-9082.
- EDB-ID 52607: WordPress OrderConvo 14 - Path Traversal, CVE-2025-10162.
- EDB-ID 52606: Notepad++ 8.9.6 - Arbitrary Code Execution, CVE-2026-48778.
- EDB-ID 52605/52604/52603: YAMCS yamcs-core 5.12.7 No Rate Limiting, User Enumeration, LDAP Injection; CVE-2026-44596, CVE-2026-44595, CVE-2026-42568.
- EDB-ID 52601: Microsoft NTLMv2 Hash Capture, CVE-2026-32202.
- EDB-ID 52600: MikroORM 7.0.13 SQL Injection, CVE-2026-44680.

### New GitHub PoC / Repository Indicators

- No reviewed GitHub advisories were returned for publication or update after 17:00 UTC.
- No newly created repositories matched the strict `CVE-2026 PoC exploit created:>=2026-06-02` search.
- Broader pushed search found unvalidated indicators, including:
  - `0xABCD01/CVE-2026-41089` - Netlogon PoC claim, pushed 2026-06-02 08:30 UTC, updated around 17:59 UTC.
  - `Defacto-ridgepole254/CVE-2026-41940-Exploit-PoC` - cPanel/WHM exploit PoC claim, pushed 16:44 UTC.
  - `Dullpurple-sloop726/CVE-2026-31431-Linux-Copy-Fail` and `Liverwortenuresis371/copyfail-rs` - Linux Copy Fail/CVE-2026-31431 indicators, pushed around 16:42-16:43 UTC.
  - `Recorded-texteditor120/CVE-2026-31802` - npm tar path traversal indicator, pushed 16:19 UTC.
  - `fartlover37/CVE-2026-2441-PoC`, `hamzamalik3461/CVE-2026-20841`, and `Jumpthereness578/CVE-2026-2991` - older repos with recent pushes.
- Confidence: Low for functionality and safety. Public PoC repositories can be malicious or trojanized; do not execute outside isolated malware-analysis infrastructure.

## Malware Intelligence

- vx-underground:
  - Direct root web access remains restricted/not useful for automation in prior runs; GitHub API monitoring succeeded.
  - Latest pushed repository remains `vxunderground/MalwareSourceCode`, pushed 2026-05-30 07:11 UTC.
  - Latest commit `1623926` added `Python/Stealer.Python.GMBA.Manipulator.7z`.
  - No new vx-underground GitHub malware-source push was observed during this 18:00 UTC run.
- MalwareBazaar:
  - Browse page reported 249 submissions in the past 24 hours.
  - Most seen malware family in the past 24 hours: Mirai.
- Ransomware/botnet activity:
  - cPanel/WHM CVE-2026-41940 remains tied to mass exploitation, "Sorry" ransomware encrypting Linux-hosted content with `.sorry` extension, and nuclear.x86/Mirai variant activity. Continue treating patched-but-not-hunted systems as potentially compromised.
- Infostealer activity:
  - FortiClient EMS CVE-2026-35616 exploitation continues to be associated with EKZ Infostealer, a Windows browser credential stealer disguised as `FortiEndpoint_Patch.exe`/`p.exe` and pushed through EMS management workflows.
- Supply-chain attacks:
  - Red Hat npm "Miasma" campaign remains high priority. Multiple reports describe compromise of 32 `@redhat-cloud-services` packages and 96 malicious versions, using GitHub Actions trusted publishing/OIDC with valid provenance and Mini Shai-Hulud-derived credential theft. Affected environments should remove compromised packages, rebuild from known-good lockfiles, inspect CI runners/developer hosts, and rotate cloud, npm, GitHub, SSH, Vault, Kubernetes, Docker, PyPI, and GPG secrets.

## Security Releases and Vendor Advisories

- CISA KEV 2026.06.02:
  - Added CVE-2022-0492 (Linux Kernel cgroups v1 release_agent privilege escalation/container escape). Due date: 2026-06-05.
  - Added CVE-2025-48595 (Android Framework integer overflow/code execution leading to local privilege escalation). Due date: 2026-06-05.
- Android Security Bulletin - June 2026:
  - Includes CVE-2025-48595 in Framework, affecting Android 14, 15, 16, and 16 QPR2. Apply 2026-06-05 or later patch level where available.
- Spacelabs Healthcare / VulnCheck:
  - Sentinel 10.5.x and 11.x before 11.6.0 vulnerable to unauthenticated RCE through deprecated .NET Remoting HTTP channel when port 8989 is deliberately exposed. Upgrade to 11.6.0 and ensure port 8989 is not reachable.
- OpenClaude:
  - GitHub advisory GHSA-m77w-p5jj-xmhg / CVE-2026-42074 describes model-controlled `dangerouslyDisableSandbox` leading to sandbox bypass and host command execution. Primary advisory still listed no patched version during fetch; NVD references v0.5.1. Verify upstream fix and set `allowUnsandboxedCommands` to false where applicable.
  - GitHub advisory GHSA-c73c-x77g-854r / CVE-2026-42073 describes MCP OAuth callback state-check bypass leading to local callback server DoS.
- NVIDIA:
  - NVTabular CVE-2026-24221 and CVE-2026-24237 are high-severity deserialization issues with code-execution/data-tampering potential.
- Dell:
  - ThinOS 10 DSA-2026-214 includes CVE-2026-40715 local privilege escalation and CVE-2026-40713 information exposure prior to ThinOS10 2602_10.0765.
- TP-Link:
  - Tapo C200 v5 CVE-2026-1871 RTSP authentication stack buffer overflow. Update firmware and restrict camera management/RTSP exposure.
- HCL:
  - iReflection CVE-2024-42206 addresses vulnerable/outdated third-party web application components.
- ExploitDB:
  - Latest direct CSV rows include Drupal CVE-2026-9082, Notepad++ CVE-2026-48778, YAMCS CVE-2026-42568/CVE-2026-44595/CVE-2026-44596, and MikroORM CVE-2026-44680.

## Recommended Actions

1. Patch and hunt KEV additions added today: Android CVE-2025-48595 and Linux Kernel CVE-2022-0492. For Linux/container platforms, combine kernel patching with privileged-container and cgroups v1 exposure review.
2. Treat exposed cPanel/WHM as incident-response priority, not just patch management. Patch fixed trains, then hunt for `.sorry` encrypted files, nuclear.x86/Mirai payloads, webshells, unauthorized SSH keys, added UID 0 accounts, and anomalous WHM sessions.
3. Upgrade FortiClient EMS to fixed versions and hunt for EKZ Infostealer indicators, including EMS certificate log anomalies, FortiClient diagnostic script abuse, `FortiEndpoint_Patch.exe`, `p.exe`, browser credential theft, and suspicious outbound POSTs.
4. Patch Cisco SD-WAN, PAN-OS, Drupal, Citrix NetScaler, Oracle WebLogic, LiteLLM, and other KEV items with missed due dates; validate external exposure and compromise indicators.
5. For Spacelabs Sentinel, confirm port 8989 is not exposed, schedule Sentinel 11.6.0 upgrades, and segment clinical systems from general enterprise networks.
6. For AI-agent/dev-tool environments, review OpenClaude exposure urgently: disable unsandboxed commands, minimize secrets on agent hosts, isolate agent execution, rotate credentials if prompt-injection exposure is plausible, and verify upstream remediation.
7. For Red Hat npm Miasma exposure, block affected package versions, rebuild clean artifacts, inspect CI runner persistence, and rotate all developer/build secrets potentially accessible during `npm install`.
8. Do not execute public PoC repositories from GitHub/Sploitus on analyst workstations. Use disposable sandboxes with network controls and inspect code for credential theft or persistence first.

## Unified Vulnerability Records

```json
[
  {
    "cve": "CVE-2025-48595",
    "cvss": "8.4 HIGH; critical operational priority due CISA KEV",
    "vendor": "Google",
    "product": "Android Framework",
    "affected_versions": "Android 14, 15, 16, and 16 QPR2 per Android June 2026 bulletin",
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
    "cve": "CVE-2022-0492",
    "cvss": "7.8 HIGH; critical operational priority due CISA KEV",
    "vendor": "Linux",
    "product": "Kernel cgroups v1 release_agent",
    "affected_versions": "Linux kernels before vendor-fixed releases; container hosts with cgroups v1 and privileged/container-root conditions are highest risk",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://sploitus.com/exploit?id=MSF%3AEXPLOIT-LINUX-LOCAL-DOCKER_CGROUP_ESCAPE-"
    ],
    "patch_available": true,
    "sources": [
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://nvd.nist.gov/vuln/detail/CVE-2022-0492",
      "https://unit42.paloaltonetworks.com/cve-2022-0492-cgroups/",
      "https://www.sysdig.com/blog/detecting-mitigating-cve-2022-0492-sysdig"
    ]
  },
  {
    "cve": "CVE-2026-0611",
    "cvss": "9.2 CRITICAL",
    "vendor": "Spacelabs Healthcare",
    "product": "Sentinel",
    "affected_versions": "Sentinel 10.5.x and higher, and 11.x.x before 11.6.0",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://www.vulncheck.com/advisories/spacelabs-healthcare-sentinel-x-unauthenticated-rce-via-net-remoting",
      "https://spacelabshealthcare.com/wp-content/uploads/2026/06/079-0273-00-RevA-Security-Advisory-Sentinel-.NET-Remoting-Vulnerability.pdf",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-0611"
    ]
  },
  {
    "cve": "CVE-2026-42074",
    "cvss": "9.3 CRITICAL",
    "vendor": "Gitlawb",
    "product": "OpenClaude",
    "affected_versions": "OpenClaude npm package; primary advisory listed latest/no patched version at fetch time, while NVD references versions prior to 0.5.1",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/Gitlawb/openclaude/security/advisories/GHSA-m77w-p5jj-xmhg"
    ],
    "patch_available": false,
    "sources": [
      "https://github.com/Gitlawb/openclaude/security/advisories/GHSA-m77w-p5jj-xmhg",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-42074",
      "https://osv.dev/vulnerability/GHSA-m77w-p5jj-xmhg"
    ]
  },
  {
    "cve": "CVE-2026-42073",
    "cvss": "6.5 MEDIUM",
    "vendor": "Gitlawb",
    "product": "OpenClaude MCP OAuth callback",
    "affected_versions": "OpenClaude v0.1.7 per primary advisory",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/Gitlawb/openclaude/security/advisories/GHSA-c73c-x77g-854r"
    ],
    "patch_available": false,
    "sources": [
      "https://github.com/Gitlawb/openclaude/security/advisories/GHSA-c73c-x77g-854r",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-42073"
    ]
  },
  {
    "cve": "CVE-2026-41940",
    "cvss": "9.8 CRITICAL",
    "vendor": "WebPros",
    "product": "cPanel & WHM and WP Squared",
    "affected_versions": "cPanel/WHM versions before fixed trains 11.110.0.97, 11.118.0.63, 11.126.0.54, 11.132.0.29, 11.134.0.20, 11.136.0.5",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://sploitus.com/exploit?id=MSF%3AEXPLOIT-MULTI-HTTP-CPANEL_WHM_AUTH_BYPASS_RCE-",
      "https://sploitus.com/exploit?id=EDB-ID%3A52574"
    ],
    "patch_available": true,
    "sources": [
      "https://support.cpanel.net/hc/en-us/articles/40073787579671-cPanel-WHM-Security-Update-04-28-2026",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://www.bleepingcomputer.com/news/security/critrical-cpanel-flaw-mass-exploited-in-sorry-ransomware-attacks/",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-41940"
    ]
  },
  {
    "cve": "CVE-2026-35616",
    "cvss": "9.1 CRITICAL/HIGH operational priority",
    "vendor": "Fortinet",
    "product": "FortiClient Enterprise Management Server",
    "affected_versions": "FortiClient EMS 7.4.5 through 7.4.6 per public reporting",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://arcticwolf.com/resources/blog/forticlient-ems-exploited-via-cve-2026-35616-to-deliver-ekz-infostealer-disguised-as-a-fortinet-patch/",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-35616"
    ]
  },
  {
    "cve": "CVE-2026-20182",
    "cvss": "10.0 CRITICAL",
    "vendor": "Cisco",
    "product": "Catalyst SD-WAN Controller/Manager",
    "affected_versions": "Affected Cisco Catalyst SD-WAN Controller/Manager releases per Cisco advisory",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://sec.cloudapps.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-sdwan-rpa2-v69WY2SW",
      "https://www.cisa.gov/news-events/directives/ed-26-03-mitigate-vulnerabilities-cisco-sd-wan-systems",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-20182"
    ]
  },
  {
    "cve": "CVE-2026-3055",
    "cvss": "9.8 CRITICAL",
    "vendor": "Citrix",
    "product": "NetScaler ADC and NetScaler Gateway",
    "affected_versions": "NetScaler deployments configured as SAML Identity Provider per vendor/research reporting",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-3055"
    ]
  },
  {
    "cve": "CVE-2026-9082",
    "cvss": "9.8 CRITICAL by ExploitDB/Sploitus indicator; NVD/Drupal context varies by configuration",
    "vendor": "Drupal",
    "product": "Drupal Core",
    "affected_versions": "Drupal core PostgreSQL-backed deployments before fixed 11.3.10, 11.2.12, 10.6.9, 10.5.10 per PoC/advisory reporting",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://sploitus.com/exploit?id=EDB-ID%3A52608",
      "https://www.exploit-db.com/exploits/52608"
    ],
    "patch_available": true,
    "sources": [
      "https://www.drupal.org/sa-core-2026-004",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-9082"
    ]
  },
  {
    "cve": "CVE-2026-0257",
    "cvss": "Critical/High operational priority",
    "vendor": "Palo Alto Networks",
    "product": "PAN-OS",
    "affected_versions": "Affected PAN-OS versions per Palo Alto advisory",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://security.paloaltonetworks.com/CVE-2026-0257",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-0257"
    ]
  },
  {
    "cve": "CVE-2026-1871",
    "cvss": "7.1 HIGH",
    "vendor": "TP-Link",
    "product": "Tapo C200 v5",
    "affected_versions": "Tapo C200 v5 firmware before vendor-fixed release",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://www.tp-link.com/en/support/download/tapo-c200/v5/#Firmware-Release-Notes",
      "https://www.tp-link.com/us/support/faq/5113/",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-1871"
    ]
  },
  {
    "cve": "CVE-2026-24221",
    "cvss": "7.8 HIGH",
    "vendor": "NVIDIA",
    "product": "NVTabular",
    "affected_versions": "Affected NVTabular versions per NVIDIA advisory",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://nvidia.custhelp.com/app/answers/detail/a_id/5851",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-24221"
    ]
  },
  {
    "cve": "CVE-2026-24237",
    "cvss": "7.8 HIGH",
    "vendor": "NVIDIA",
    "product": "NVTabular",
    "affected_versions": "Affected NVTabular versions per NVIDIA advisory",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://nvidia.custhelp.com/app/answers/detail/a_id/5851",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-24237"
    ]
  },
  {
    "cve": "CVE-2026-49943",
    "cvss": "6.3 MEDIUM",
    "vendor": "CZ.NIC",
    "product": "BIRD Internet Routing Daemon",
    "affected_versions": "BIRD through 2.19.0",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": false,
    "sources": [
      "https://bird.nic.cz",
      "https://gitlab.nic.cz/labs/bird/-/blob/master/NEWS",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-49943"
    ]
  },
  {
    "cve": "CVE-2026-33244",
    "cvss": "5.4 MEDIUM",
    "vendor": "Remix Software / React Router",
    "product": "React Router",
    "affected_versions": "React Router 7.5.1 through 7.13.1 when Framework Mode pre-rendering is enabled",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://github.com/remix-run/react-router/security/advisories/GHSA-f22v-gfqf-p8f3",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-33244"
    ]
  }
]
```

## Source Links

- CISA KEV JSON: https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json
- NVD API 2.0: https://services.nvd.nist.gov/rest/json/cves/2.0
- Sploitus homepage: https://sploitus.com/
- ExploitDB CSV: https://gitlab.com/exploit-database/exploitdb/-/raw/main/files_exploits.csv
- GitHub global advisories API: https://api.github.com/advisories
- vx-underground GitHub: https://github.com/vxunderground
- MalwareBazaar browse: https://bazaar.abuse.ch/browse/
- VulnCheck Spacelabs advisory: https://www.vulncheck.com/advisories/spacelabs-healthcare-sentinel-x-unauthenticated-rce-via-net-remoting
- OpenClaude sandbox advisory: https://github.com/Gitlawb/openclaude/security/advisories/GHSA-m77w-p5jj-xmhg
- OpenClaude OAuth advisory: https://github.com/Gitlawb/openclaude/security/advisories/GHSA-c73c-x77g-854r
- Arctic Wolf FortiClient EMS/EKZ: https://arcticwolf.com/resources/blog/forticlient-ems-exploited-via-cve-2026-35616-to-deliver-ekz-infostealer-disguised-as-a-fortinet-patch/
- Android June 2026 bulletin: https://source.android.com/docs/security/bulletin/2026/2026-06-01
- Wiz Miasma supply-chain report: https://www.wiz.io/blog/miasma-supply-chain-attack-targeting-redhat-npm-packages
- cPanel ransomware reporting: https://www.bleepingcomputer.com/news/security/critrical-cpanel-flaw-mass-exploited-in-sorry-ransomware-attacks/
