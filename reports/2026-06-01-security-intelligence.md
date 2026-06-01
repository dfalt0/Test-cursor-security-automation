# Daily Security Intelligence Report - 2026-06-01

Collection time: 2026-06-01 21:04-21:55 UTC  
Automation trigger: hourly cron  
Analyst stance: prioritize enterprise-impacting CVEs, active exploitation, public exploit material, malware delivery, supply-chain compromise, and urgent vendor security releases.

## Source Coverage and Caveats

Primary and high-priority sources checked during this run included CISA KEV JSON, GitHub Advisory Database/API, vendor advisories, ExploitDB, Sploitus indexed exploit pages, Rapid7, Palo Alto Networks, GitHub security advisories, Arctic Wolf, Cisco PSIRT, NVD-indexed records, and GitHub/web-indexed public PoC repositories.

Important caveats:

- Sploitus' static homepage fetch did not expose a readable "Exploits of the Week" top-10 block. The Sploitus homepage rendered only shell navigation text, so this report records the top exploit indicators found through Sploitus-indexed exploit pages and correlated exploit sources instead of claiming a definitive homepage ranking.
- A web search result contradicted the CISA JSON feed for CVE-2024-21182. The machine-readable CISA KEV JSON was current at `catalogVersion: 2026.06.01`, `dateReleased: 2026-06-01T16:59:32Z`, and included CVE-2024-21182. This report treats the CISA JSON feed as authoritative.
- GitHub repositories and Sploitus entries are treated as indicators, not proof of reliable exploitability. Functional confidence is higher only where vendor, researcher, or reviewed advisory sources corroborate the behavior.

## Executive Summary

- Total CVE/advisory records triaged in this report: 24
- Critical findings: 12
- High findings: 8
- Active exploitation or KEV-listed findings: 10
- New malware/supply-chain activity: 4 major clusters
- Most urgent enterprise actions:
  1. Patch or isolate Oracle WebLogic Server affected by CVE-2024-21182, newly added to CISA KEV on 2026-06-01.
  2. Patch Palo Alto Networks PAN-OS GlobalProtect CVE-2026-0257 and disable risky authentication override cookie configurations until fixed.
  3. Patch Windows Server domain controllers for CVE-2026-41089 due to third-party active exploitation reporting.
  4. Patch FortiClient EMS CVE-2026-35616 and hunt for EKZ Infostealer delivery through FortiClient-managed scripts.
  5. Audit developer machines and CI for TanStack/Nx Console compromise artifacts and rotate all exposed credentials.
  6. Patch HP Poly VVX/Trio VoIP devices or disable ICE where not required due to new unauthenticated root RCE disclosure CVE-2026-0826.

## Top Vulnerabilities

| Priority | CVE / ID | Severity | Affected software | Exploit availability | Active exploitation | Confidence | Recommended action |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Critical | CVE-2024-21182 | KEV-listed; Oracle advisory severity not fully revalidated in this run | Oracle WebLogic Server 12.2.1.4.0 and 14.1.1.0.0 | Public exploit references reported historically; not revalidated as functional in this run | Yes - CISA KEV dateAdded 2026-06-01 | High for KEV; Medium for exploit maturity | Apply Oracle July 2024 CPU/mitigations immediately; restrict T3/IIOP exposure. |
| Critical | CVE-2026-0257 | Palo Alto CVSS-B 7.8 High, urgency Highest, exploit maturity Attacked | PAN-OS GlobalProtect portal/gateway with authentication override cookies and affected certificate configuration | Public GitHub PoC observed (`sfewer-r7/CVE-2026-0257`) | Yes - Palo Alto reports limited exploit attempts; CISA KEV added 2026-05-29 | High | Upgrade to fixed PAN-OS releases; disable or harden authentication override cookies. |
| Critical | CVE-2026-41089 | CVSS 9.8 Critical | Microsoft Windows Server Netlogon on domain controllers | No public PoC confirmed in this run | Reported active exploitation by CCB Belgium; Microsoft/NVD record confirms critical RCE and patches | Medium-High | Emergency patch domain controllers; monitor Netlogon anomalies and DC process crashes. |
| Critical | CVE-2026-35616 | CVSS 9.1/9.8 Critical depending source | Fortinet FortiClient EMS 7.4.5-7.4.6 | Public detection/analysis and ProjectDiscovery nuclei template noted; exploitation observed | Yes - exploited to deliver EKZ Infostealer | High | Apply Fortinet hotfix/7.4.7 or later; restrict TCP 8013; hunt FortiClient script abuse. |
| Critical | CVE-2026-0826 | CVSSv4 9.2 Critical | HP Poly VVX 150/250/350/450 and Trio 8300/8500/8800 with ICE enabled | Rapid7 reports Metasploit exploit module developed; technical RCE details published | No active exploitation observed | High | Upgrade VVX to UCS 6.4.8, Trio 8300 to 8.1.7, Trio 8500/8800 to 7.2.8; disable ICE if unnecessary. |
| Critical | CVE-2026-45321 | CVSS 9.6 Critical; CISA KEV; ransomware use Known in KEV feed | 42 `@tanstack/*` npm packages | Malicious packages were published via legitimate trusted-publisher path | Yes - KEV and supply-chain malware | High | Remove affected versions, rebuild from clean lockfiles, rotate all CI/developer credentials, audit cloud/GitHub access. |
| Critical | CVE-2026-48027 | Critical; CISA KEV; ransomware use Known in KEV feed | Nx Console VS Code/OpenVSX extension 18.95.0 | Malicious extension payload and IOCs published by Nx advisory | Yes - KEV and credential theft campaign | High | Update Nx Console to 18.100.0+, kill persistence, remove artifacts, rotate all credentials on affected hosts. |
| Critical | CVE-2026-23744 | CVSS 9.8 Critical | MCPJam Inspector <= 1.4.2 | Public GHSA PoC and multiple GitHub/Sploitus PoCs | No confirmed active exploitation observed | High for PoC; Medium for patch state | Do not expose port 6274; bind to localhost; update if fixed build is available; otherwise remove/contain. |
| Critical | CVE-2026-42945 | CVSS about 9.2 Critical in public PoCs | NGINX Open Source 0.6.27-1.30.0 and NGINX Plus R32-R36 under specific rewrite config | Multiple GitHub PoCs, including `DepthFirstDisclosures/Nginx-Rift` | Third-party active exploitation reporting; not confirmed from vendor in this run | Medium-High | Upgrade to 1.30.1/1.31.0 or vendor backports; audit rewrite configs; also patch CVE-2026-9256. |
| Critical | CVE-2026-9256 | Critical in public reporting | NGINX rewrite module, including environments patched only for CVE-2026-42945 | Public reporting, research advisory; PoC not directly validated here | Third-party active exploitation reporting | Medium | Upgrade to NGINX Open Source 1.30.2/1.31.1 or NGINX Plus fixed builds. |
| Critical | CVE-2026-32746 | CVSS 9.8 in ExploitDB entry | GNU InetUtils telnetd through 2.7 | ExploitDB verified PoC EDB-52556, public Docker lab; PoC verifies overflow, not full shell | No active exploitation confirmed | High for PoC; Medium for weaponization | Remove/disable telnetd, restrict port 23, apply vendor/backport fix when available. |
| Critical | CVE-2026-20223 | Cisco-reported CVSS 10.0 | Cisco Secure Workload internal REST APIs | No public exploit confirmed | No exploitation reported in checked sources | High | Patch on-prem Secure Workload to fixed branches; SaaS patched by Cisco; no workaround. |

## New KEV and Active Exploitation Highlights

### CISA KEV delta observed

The CISA KEV JSON feed (`catalogVersion: 2026.06.01`) included the following recent high-priority additions:

- CVE-2024-21182 - Oracle WebLogic Server unspecified vulnerability
  - dateAdded: 2026-06-01
  - dueDate: 2026-06-04
  - description: unauthenticated network access via T3/IIOP can compromise WebLogic Server and expose critical data.
  - confidence: High for KEV status.
- CVE-2026-0257 - Palo Alto Networks PAN-OS GlobalProtect authentication bypass
  - dateAdded: 2026-05-29
  - dueDate: 2026-06-01
  - vendor confirms limited exploit attempts.
  - confidence: High.
- CVE-2026-48027 - Nx Console embedded malicious code
  - dateAdded: 2026-05-27
  - known ransomware campaign use: Known in KEV feed.
  - confidence: High.
- CVE-2026-45321 - TanStack malicious package publication
  - dateAdded: 2026-05-27
  - known ransomware campaign use: Known in KEV feed.
  - confidence: High.
- CVE-2026-8398 - Daemon Tools Lite embedded malicious code
  - dateAdded: 2026-05-27
  - confidence: Medium; no primary vendor page was fetched during this run beyond CISA notes.
- CVE-2026-48172 - LiteSpeed cPanel Plugin privilege escalation
  - dateAdded: 2026-05-26
  - confidence: High for KEV status.
- CVE-2026-9082 - Drupal Core SQL injection
  - dateAdded: 2026-05-22
  - confidence: High for KEV status.
- CVE-2026-34926 - Trend Micro Apex One directory traversal
  - dateAdded: 2026-05-21
  - confidence: High for KEV status.

## Exploits Released and Public PoC Activity

### Exploit-source top 10 indicators

Because Sploitus did not expose a static top-10 homepage block, the following list combines Sploitus-indexed exploit entries with ExploitDB, Packet Storm/search-indexed entries, GitHub PoCs, and researcher disclosures found during the Sploitus-first collection pass.

| Rank | Indicator | Source type | Affected software | Exploit type | Maturity | Weaponization potential | Confidence |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | CVE-2026-23744 | Sploitus indexed exploit, GHSA, GitHub PoCs | MCPJam Inspector <= 1.4.2 | Unauthenticated RCE via `/api/mcp/connect` | Public PoC with command execution | High if service exposed on 0.0.0.0:6274 | High |
| 2 | CVE-2026-0257 | GitHub PoC and Palo Alto advisory | PAN-OS GlobalProtect | Auth bypass via forged authentication override cookie | Public PoC; vendor says attacked | High for exposed GlobalProtect with risky config | High |
| 3 | CVE-2026-0826 | Rapid7 disclosure | HP Poly VVX/Trio | Unauthenticated root RCE via SIP/SDP ICE parsing | Metasploit module developed; detailed technical analysis | High where ICE enabled | High |
| 4 | CVE-2026-2329 | Sploitus indexed Metasploit module | Grandstream GXP1600 phones | Unauthenticated root RCE via HTTP API overflow | Metasploit module, `GreatRanking` | High for exposed vulnerable phones | High |
| 5 | CVE-2026-42945 | GitHub PoCs | NGINX rewrite module | Heap overflow, possible RCE/DoS | Multiple PoCs, some claiming RCE | High for vulnerable rewrite configs; DoS more reliable | Medium-High |
| 6 | CVE-2026-32746 | ExploitDB EDB-52556 | GNU InetUtils telnetd <= 2.7 | Pre-auth buffer overflow | Verified PoC confirms overflow/leak, not shell | High on exposed telnetd, though telnet exposure should be rare | High |
| 7 | CVE-2026-35616 | Arctic Wolf/Horizon3/ProjectDiscovery reference | FortiClient EMS | Pre-auth API access/control leading to code deployment | Active exploitation, public detection template | Very high because EMS can push code fleet-wide | High |
| 8 | CVE-2025-6965 | Sploitus/ExploitDB indexed | SQLite/winsqlite contexts | Heap overflow / DoS, potential RCE claims | Public exploit entry | Medium; claims require environment validation | Medium |
| 9 | CVE-2025-24999 | Sploitus/Packet Storm indexed | Microsoft SQL Server 2022/2025 | Privilege escalation | Public PoC/advisory | Medium in database environments | Medium |
| 10 | CVE-2024-31317 | Sploitus/GitHub lab indexed | Google Android | Privilege escalation via Zygote setting injection | Public lab/PoC | Medium; older patched Android versions affected | Medium |

### ExploitDB additions

- EDB-ID 52556 - CVE-2026-32746, GNU InetUtils telnetd 2.7 buffer overflow
  - Type: remote
  - EDB verified: yes
  - Date: 2026-05-07
  - PoC verifies out-of-bounds write/BSS leak and possible crash; it explicitly does not include shellcode or ROP.
  - Recommendation: disable telnetd, restrict port 23, and track GNU/distribution patches.

### New GitHub PoCs and exploit repositories

- `sfewer-r7/CVE-2026-0257`
  - PAN-OS GlobalProtect auth override cookie forging PoC.
  - Treat as high-risk because Palo Alto reports exploit attempts.
- `DepthFirstDisclosures/Nginx-Rift`
  - CVE-2026-42945 RCE PoC for NGINX rewrite module.
  - 825 stars and 155 forks observed in indexed snippet.
- `F2u0a0d3/CVE-2026-42945-nginx-rift-poc`
  - CVE-2026-42945 PoC with detect/probe/exploit modes.
  - Low star count but operationally sensitive.
- `z4yd3/PoC-CVE-2026-23744`, `boroeurnprach/CVE-2026-23744-PoC`, `rootdirective-sec/CVE-2026-23744-Lab`, `d3vn0mi/CVE-2026-23744-POC`
  - Multiple MCPJam Inspector PoCs/labs.
  - Public PoC availability is high; exploit reliability should be validated only in authorized test environments.

## Malware Intelligence

### EKZ Infostealer via FortiClient EMS CVE-2026-35616

Source: Arctic Wolf Labs, SecurityWeek/Horizon3 corroboration.

- Campaign: threat actor exploited FortiClient EMS to modify EMS-managed configuration and push malicious FortiClient VPN scripts to managed endpoints.
- Malware: EKZ Infostealer, delivered as `FortiEndpoint_Patch.exe` / hosted as `p.exe`.
- TTPs:
  - EMS logs: `Certificate not found in request header` followed within seconds by `Certificate user: fortinet-ca2 ... successfully updated`.
  - FortiClient process lineage: `fortitray.exe` or `ipsec.exe` -> `cmd.exe` -> `powershell.exe` -> `FortiEndpoint_Patch.exe`.
  - Browser credential theft from Chromium, Edge, Firefox/Gecko-family browsers; Chromium v20 AES-256 key extraction via `IElevator::DecryptData`.
  - Exfiltration of staged `C:\ProgramData\log.txt` over HTTP.
- IOCs:
  - Payload URL: `hxxp[:]//83.138.53[.]110/dl/p.exe`
  - Delivery filename: `FortiEndpoint_Patch.exe`
  - SHA-256: `0da123adf9251957a4b850a3f6bd6a753dd4892be176a84a18450e899534cc5e`
  - Additional hashes: `d91c00fad521e76efa89715cca89db487d5676f2c767c883482f9c8f82bd383a`, `fd65051c61a904a304919c04a8c8633c001183ac73ac461cd4d9057946f02bf5`, `2927bc31b4f8254c6b332fc03110a6373cad00ffa2ff9de427c26bb222017bb2`, `2f25ea1b622abf3212141af932c2ec4cbd6b2b5903c2a531121f691227d98cff`
- Confidence: High.

### TanStack npm package compromise - CVE-2026-45321

Source: TanStack GitHub Security Advisory, CISA KEV.

- 84 malicious versions across 42 `@tanstack/*` packages were published on 2026-05-11 from 19:20 to 19:26 UTC.
- Attack chain: `pull_request_target` misconfiguration, GitHub Actions cache poisoning, and OIDC token extraction from runner memory.
- Payload: obfuscated `router_init.js`, approximately 2.3 MB, harvesting AWS, GCP, Kubernetes, Vault, npm, GitHub, and SSH credentials.
- IOCs:
  - Malicious git ref: `github:tanstack/router#79ac49eedf774dd4b0cfa308722bc463cfe5885c`
  - Fictitious package: `@tanstack/setup`
  - Payload: `router_init.js`
  - Exfiltration domains: `filev2.getsession.org`, `seed1.getsession.org`, `seed2.getsession.org`, `seed3.getsession.org`
  - Second-stage URLs: `https://litter.catbox.moe/h8nc9u.js`, `https://litter.catbox.moe/7rrc6l.mjs`
- Confidence: High.

### Nx Console VS Code/OpenVSX compromise - CVE-2026-48027

Source: Nx GitHub Security Advisory, Nx blog snippet, CISA KEV.

- Malicious Nx Console 18.95.0 was published to Visual Studio Marketplace and OpenVSX on 2026-05-18.
- Visual Studio Marketplace exposure: approximately 18 minutes by advisory timeline; OpenVSX approximately 36 minutes.
- Root cause: Nx contributor credentials were reportedly stolen via the earlier TanStack supply-chain compromise.
- Targeted credentials:
  - Vault tokens, Kubernetes/AWS metadata, npm tokens, GitHub tokens, 1Password CLI sessions, private keys, Docker/GCP credentials.
- Persistence/IOC paths:
  - macOS/Linux: `~/.local/share/kitty/cat.py`, `~/Library/LaunchAgents/com.user.kitty-monitor.plist`, `/var/tmp/.gh_update_state`, `/tmp/kitty-*`
  - Windows: `%USERPROFILE%\.local\share\kitty\cat.py`, `%TEMP%\kitty-*`, `%TEMP%\.gh_update_state`, `%USERPROFILE%\.bun\bin\bun.exe`
- Confidence: High.

### Daemon Tools Lite embedded malicious code - CVE-2026-8398

Source: CISA KEV feed.

- CISA added CVE-2026-8398 on 2026-05-27.
- KEV description: embedded malicious code vulnerability in Daemon Tools Lite with high confidentiality, integrity, and availability impact.
- No additional primary vendor details were fetched in this run.
- Confidence: High for KEV listing, Medium for campaign details.

## Security Releases and Vendor Advisories

### Microsoft

- CVE-2026-41089 - Windows Netlogon RCE
  - NVD/MSRC-linked record: CVSS 9.8, stack-based buffer overflow, unauthorized network attacker can execute code.
  - Third-party national authority reporting says active exploitation began after May 2026 Patch Tuesday.
  - Action: emergency patch all domain controllers; monitor Netlogon traffic, crashes, and post-exploitation admin changes.
- CVE-2026-41091 and CVE-2026-45498 - Microsoft Defender
  - Recent CISA KEV entries from 2026-05-20.
  - Action: validate Defender platform/signature updates and endpoint management coverage.

### Cisco

- CVE-2026-20223 - Cisco Secure Workload
  - Critical, CVSS 10.0 in Cisco/SC Media reporting.
  - Unauthenticated remote access to internal REST APIs can grant full administrative control.
  - No exploitation reported in checked sources.
  - Action: patch on-prem branches; SaaS patched by Cisco; no workaround.
- CVE-2026-20182 - Cisco Catalyst SD-WAN Controller/Manager
  - CISA KEV entry; Cisco advisory states limited exploitation became known in May 2026.
  - Action: upgrade to fixed release; retain and review logs; follow CISA emergency guidance.
- CVE-2026-20171 - Cisco Nexus 3000/9000 BGP DoS
  - Cisco PSIRT not aware of malicious use at publication.
  - Action: patch affected standalone NX-OS BGP deployments.

### Fortinet

- CVE-2026-35616 - FortiClient EMS
  - Active exploitation to deliver EKZ Infostealer.
  - Action: apply hotfix/fixed version, restrict management port 8013, hunt EMS logs and endpoint process trees.

### Palo Alto Networks

- CVE-2026-0257 - PAN-OS GlobalProtect authentication bypass
  - Vendor urgency: Highest.
  - Exploit maturity: Attacked.
  - Action: upgrade PAN-OS; disable authentication override or use dedicated secure certificate; expect user re-authentication after upgrade.

### HP Poly

- CVE-2026-0826 - VVX/Trio unauthenticated root RCE
  - Rapid7 disclosure on 2026-06-01.
  - Action: update UCS firmware; disable ICE where not needed.

### GitHub

- GitHub Advisory Database critical entries published on 2026-06-01 included:
  - CVE-2026-0826 - HP Poly critical RCE.
  - CVE-2026-47413 - praisonai-platform member-to-owner privilege escalation.
  - CVE-2026-47428 - Vitest browser-mode inline script/token theft leading to RCE chain.
  - CVE-2026-47429 - Vitest UI/API arbitrary file read and execution when exposed.
  - CVE-2026-8931, CVE-2026-7858, CVE-2026-48188 and multiple WordPress/plugin critical unreviewed advisories.
- GitHub Enterprise Server 3.20.3
  - Public reporting indicates fixes for critical pre-auth SSRF CVE-2026-9312 and required GPG key rotation before upgrade.
  - Action: GHES administrators should follow official GitHub release and GPG rotation guidance before patching.

### GitLab, VMware/Broadcom, Apple, Oracle, SAP, Juniper, Citrix

No newly confirmed emergency advisory from these vendors was validated during this run beyond Oracle WebLogic's CISA KEV addition and historical Oracle CPU reference. Continue monitoring vendor feeds.

## GitHub Security Advisory Highlights

### PraisonAI / praisonai-platform cluster

GitHub Advisory Database/API returned multiple praisonai-platform advisories on 2026-06-01:

- CVE-2026-47413 - any workspace member can add arbitrary user as owner.
  - Severity: Critical, CVSS 9.1.
  - Affected: `praisonai-platform < 0.1.4`.
  - Patched: 0.1.4.
  - Confidence: High.
- CVE-2026-47412 - any workspace member can delete entire workspace.
  - Severity: High, CVSS 8.1.
  - Patched: 0.1.4.
  - Confidence: High.
- CVE-2026-47415 - issue endpoints accept cross-workspace `issue_id`, enabling IDOR read/update/delete.
  - Severity: High, CVSS 8.3.
  - Patched: 0.1.4.
  - Confidence: High.

Recommendation: if PraisonAI Platform is deployed, upgrade to 0.1.4 or later and review logs for workspace/member tampering.

### Vitest critical advisories

- CVE-2026-47428 / GHSA-2h32-95rg-cppp
  - Vitest browser mode served `otelCarrier` as inline module script.
  - Impact: same-origin JavaScript execution can recover `VITEST_API_TOKEN` and chain to local/server-side code execution.
  - Affected: `@vitest/browser >=4.0.17 <4.1.6`, `>=5.0.0-beta.0 <5.0.0-beta.3`.
  - Patched: 4.1.6, 5.0.0-beta.3.
  - Confidence: High.
- CVE-2026-47429 / GHSA-5xrq-8626-4rwp
  - Vitest UI/API arbitrary file read and execution when the server is listening/exposed, especially on Windows path bypasses.
  - Affected: Vitest prior to 4.1.0 in vulnerable configurations.
  - Mitigation: upgrade; avoid exposing Vitest UI/browser API; use new `allowWrite` and `allowExec` controls.
  - Confidence: High.

## Unified Vulnerability Records

```json
[
  {
    "cve": "CVE-2024-21182",
    "cvss": "not revalidated in this run",
    "vendor": "Oracle",
    "product": "WebLogic Server",
    "affected_versions": "12.2.1.4.0, 14.1.1.0.0 per NVD/vendor references",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["historical public exploit references reported; not functionally validated"],
    "patch_available": true,
    "sources": ["CISA KEV JSON 2026.06.01", "Oracle July 2024 CPU reference", "NVD reference"]
  },
  {
    "cve": "CVE-2026-0257",
    "cvss": "CVSS-B 7.8 High; Palo Alto urgency Highest",
    "vendor": "Palo Alto Networks",
    "product": "PAN-OS GlobalProtect",
    "affected_versions": "PAN-OS 10.2, 11.1, 11.2, 12.1 fixed in listed hotfix/minor releases; Prisma Access affected branches",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://github.com/sfewer-r7/CVE-2026-0257"],
    "patch_available": true,
    "sources": ["Palo Alto advisory", "CISA KEV", "GitHub PoC search result"]
  },
  {
    "cve": "CVE-2026-41089",
    "cvss": "9.8",
    "vendor": "Microsoft",
    "product": "Windows Netlogon / Windows Server domain controllers",
    "affected_versions": "Supported Windows Server versions before May 2026 fixes",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["NVD", "MSRC reference", "CCB Belgium/secondary reporting"]
  },
  {
    "cve": "CVE-2026-35616",
    "cvss": "9.1 vendor/Horizon3; 9.8 NVD cited by Horizon3",
    "vendor": "Fortinet",
    "product": "FortiClient EMS",
    "affected_versions": "7.4.5 through 7.4.6 per Horizon3/Fortinet reporting",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["ProjectDiscovery nuclei template referenced by Arctic Wolf", "Horizon3 analysis"],
    "patch_available": true,
    "sources": ["Arctic Wolf", "Horizon3", "SecurityWeek", "Fortinet advisory reference"]
  },
  {
    "cve": "CVE-2026-0826",
    "cvss": "CVSSv4 9.2",
    "vendor": "HP Poly",
    "product": "VVX and Trio VoIP phones",
    "affected_versions": "VVX and Trio models with ICE enabled before listed UCS fixes",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["Rapid7 disclosure / Metasploit module described"],
    "patch_available": true,
    "sources": ["Rapid7", "GitHub Advisory Database"]
  },
  {
    "cve": "CVE-2026-45321",
    "cvss": "9.6",
    "vendor": "TanStack",
    "product": "42 @tanstack/* npm packages",
    "affected_versions": "84 malicious package versions listed in GHSA-g7cv-rxg3-hmpx",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["malicious package IOCs in advisory"],
    "patch_available": true,
    "sources": ["TanStack GitHub advisory", "CISA KEV"]
  },
  {
    "cve": "CVE-2026-48027",
    "cvss": "Critical",
    "vendor": "Nx",
    "product": "Nx Console VS Code/OpenVSX extension",
    "affected_versions": "18.95.0",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["malware/persistence IOCs in advisory"],
    "patch_available": true,
    "sources": ["Nx GitHub advisory", "Nx blog", "CISA KEV"]
  },
  {
    "cve": "CVE-2026-23744",
    "cvss": "9.8",
    "vendor": "MCPJam",
    "product": "Inspector",
    "affected_versions": "<= 1.4.2",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://github.com/MCPJam/inspector/security/advisories/GHSA-232v-j27c-5pp6", "multiple public GitHub PoCs", "Sploitus indexed exploit"],
    "patch_available": "unclear: fetched GHSA showed no patched version; other public writeups reference 1.4.3",
    "sources": ["GitHub advisory", "Sploitus indexed exploit", "GitHub PoC search results"]
  },
  {
    "cve": "CVE-2026-42945",
    "cvss": "about 9.2 in public reporting",
    "vendor": "F5/NGINX",
    "product": "NGINX rewrite module",
    "affected_versions": "Open Source 0.6.27-1.30.0; NGINX Plus R32-R36 per PoC/advisory snippets",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": false,
    "poc_links": ["https://github.com/DepthFirstDisclosures/Nginx-Rift", "https://github.com/F2u0a0d3/CVE-2026-42945-nginx-rift-poc"],
    "patch_available": true,
    "sources": ["GitHub PoC search results", "CyCognito/Security Boulevard snippets", "F5 advisory reference in snippets"]
  },
  {
    "cve": "CVE-2026-32746",
    "cvss": "9.8 in ExploitDB entry",
    "vendor": "GNU",
    "product": "InetUtils telnetd",
    "affected_versions": "through 2.7",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://www.exploit-db.com/exploits/52556"],
    "patch_available": "pending/follow distribution updates",
    "sources": ["ExploitDB EDB-52556"]
  }
]
```

## Recommended Actions - Ranked

1. Patch/mitigate all KEV-listed internet-facing systems with due dates already passed or imminent:
   - Oracle WebLogic CVE-2024-21182
   - Palo Alto PAN-OS CVE-2026-0257
   - Nx Console CVE-2026-48027
   - TanStack CVE-2026-45321
   - LiteSpeed cPanel CVE-2026-48172
   - Drupal Core CVE-2026-9082
   - Trend Micro Apex One CVE-2026-34926
2. Emergency patch Windows Server domain controllers for CVE-2026-41089 and increase Netlogon/DC telemetry review.
3. Patch FortiClient EMS CVE-2026-35616 and hunt for EKZ Infostealer:
   - EMS certificate anomalies
   - FortiClient script files in `logs\Trace\scripts`
   - FortiClient-spawned PowerShell
   - `FortiEndpoint_Patch.exe`, `p.exe`, and `C:\ProgramData\log.txt`
4. Patch Palo Alto PAN-OS GlobalProtect CVE-2026-0257 and disable authentication override cookies where feasible until upgraded.
5. Audit all developer and CI environments for TanStack/Nx compromise windows:
   - Rebuild dependencies from clean lockfiles.
   - Rotate GitHub, npm, cloud, SSH, Vault, Docker, and CI secrets.
   - Review cloud and GitHub audit logs after 2026-05-11.
6. Patch HP Poly VVX/Trio devices and disable ICE where not needed.
7. Patch NGINX twice if necessary:
   - CVE-2026-42945 fixed by 1.30.1/1.31.0 or backports.
   - CVE-2026-9256 requires 1.30.2/1.31.1 or later.
   - Audit `rewrite`, unnamed captures, and question-mark replacement patterns.
8. Remove or isolate exposed development/test tools:
   - MCPJam Inspector on port 6274.
   - Vitest UI/browser API exposed to networks.
9. Disable legacy telnetd services; block port 23 and patch GNU InetUtils telnetd when distribution fixes land.
10. Patch Cisco management-plane products:
    - Cisco Secure Workload CVE-2026-20223.
    - Cisco SD-WAN CVE-2026-20182.
    - Cisco Nexus BGP DoS CVE-2026-20171.

## Items to Recheck Next Run

- Confirm whether the CISA public HTML catalog has caught up with the 2026-06-01 KEV JSON for CVE-2024-21182.
- Reattempt Sploitus dynamic "Exploits of the Week" extraction with a browser-capable client if available.
- Validate primary vendor advisories for:
  - CVE-2026-9256 NGINX Poolslip
  - CVE-2026-20223 Cisco Secure Workload
  - CVE-2026-9312 GitHub Enterprise Server
  - CVE-2026-8398 Daemon Tools Lite
- Check VX-Underground primary channels directly for any malware/ransomware releases not visible through search snippets.
