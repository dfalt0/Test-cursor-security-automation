# Security Intelligence Report - 2026-06-01 23:57 UTC

Repository verified: `dfalt0/Test-cursor-security-automation`

## Executive Summary

- NVD CVEs published on 2026-06-01: 377 total.
  - Critical: 20
  - High: 104
  - Medium: 114
  - Low: 73
  - Unknown/unscored: 66
- Critical findings requiring immediate action:
  - CVE-2026-41089 - Microsoft Windows Netlogon unauthenticated RCE on domain controllers; public reporting attributes active exploitation to CCB warning. Confidence: Medium-High.
  - CVE-2024-21182 - Oracle WebLogic Server unauthorized access; added to CISA KEV on 2026-06-01 with 2026-06-04 due date. Confidence: High.
  - CVE-2026-0300 - Palo Alto Networks PAN-OS User-ID Authentication Portal unauthenticated RCE; vendor marks exploit maturity as ATTACKED. Confidence: High.
  - CVE-2026-0257 - Palo Alto Networks PAN-OS GlobalProtect authentication bypass; vendor confirms limited exploit attempts and CISA KEV due date was 2026-06-01. Confidence: High.
  - CVE-2026-20182 - Cisco Catalyst SD-WAN Controller/Manager authentication bypass, CVSS 10.0; Cisco confirms limited exploitation. Confidence: High.
  - CVE-2026-8732 - WP Maps Pro unauthenticated admin-account creation; active exploitation reported by WordPress security reporting. Confidence: Medium-High.
  - GHSA-qf6p-p7ww-cwr9 - Gogs authenticated RCE via `git rebase` argument injection; no patch and Metasploit module available. Confidence: High for exploit availability; Medium for exploitation status.
- New malware/ransomware intelligence:
  - FortiGuard Labs published a PureLogs phishing campaign using RAR attachments, obfuscated JavaScript, PowerShell, and `MsBuild.exe` process hollowing.
  - Microsoft Threat Intelligence published analysis of The Gentlemen ransomware, tracked to Storm-2697, with self-propagation and double-extortion behavior.
  - VX-Underground `MalwareSourceCode` added `Python/Stealer.Python.GMBA.Manipulator.7z` on 2026-05-30.
- Important vendor/security releases:
  - GitLab released 19.0.1, 18.11.4, and 18.10.7 on 2026-05-27.
  - GitHub Enterprise Server 3.20.3 was released on 2026-05-26 and fixes critical SSRF plus high-severity Dirty Frag kernel issues.
  - Apple released iOS/macOS 26.5.1 on 2026-06-01 with no published CVE entries.
  - HP Poly fixed CVE-2026-0826 in VVX/Trio firmware releases; Rapid7 released a technical write-up and Metasploit module.

## Collection Notes and Confidence

- Sploitus homepage fetch did not expose a structured "Exploits of the Week" block. The Sploitus section below is therefore a reconstructed top-10 set from indexed Sploitus exploit pages and corroborating exploit-source searches. Confidence: Medium.
- GitHub repository search for newly created repositories matching `CVE-2026 exploit PoC` created after 2026-05-25 returned no results via GitHub CLI. Public PoC/exploit references below are from advisories, Metasploit references, ExploitDB, Sploitus, and search-indexed GitHub content. Confidence: Medium.
- Packet Storm direct search results were sparse; Packet Storm-sourced items were identified via Sploitus or search snippets where available. Confidence: Low-Medium.
- Active exploitation is marked only when a vendor, CISA KEV, or a named security organization/source reported exploitation. Search-only claims without primary support are treated as Medium or Low confidence.

## Top Vulnerabilities

| Priority | CVE / ID | Severity | Affected software | Exploit availability | Active exploitation | Recommended action | Confidence |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Critical | CVE-2026-41089 | Critical, CVSS 9.8 | Microsoft Windows Server domain controllers / Netlogon | No public PoC validated in this run | Reported by CCB via security media; Microsoft advisory page was JS-only in fetch | Apply May 2026 updates to all DCs; restrict untrusted RPC/Netlogon exposure; hunt for Netlogon/LSASS crashes and anomalous MS-NRPC traffic | Medium-High |
| Critical | CVE-2024-21182 | High, CVSS 7.5, KEV | Oracle WebLogic Server 12.2.1.4.0, 14.1.1.0.0 | PoC references reported by third-party vulnerability platforms; not validated as functional | Yes, CISA KEV added 2026-06-01 | Apply Oracle July 2024 CPU or latest supported CPU; restrict T3/IIOP to trusted networks; review WebLogic access logs | High |
| Critical | CVE-2026-0300 | Critical, CVSS-BT 9.3 | Palo Alto Networks PAN-OS User-ID Authentication Portal | Vendor does not publish exploit; attacks observed | Yes, Palo Alto marks ATTACKED | Upgrade to fixed PAN-OS releases; restrict or disable User-ID Authentication Portal; enable Threat ID 510019 where supported | High |
| Critical | CVE-2026-0257 | High, CVSS-BT 7.8, KEV | PAN-OS GlobalProtect portal/gateway with auth override cookies and certificate configuration | No public PoC validated | Yes, vendor confirms limited exploit attempts | Upgrade to fixed PAN-OS/Prisma Access versions; disable auth override or use dedicated cookie certificate; require re-auth after upgrade | High |
| Critical | CVE-2026-20182 | Critical, CVSS 10.0, KEV | Cisco Catalyst SD-WAN Controller and Manager | Public exploitation claims exist; Cisco advisory provides IoC checks | Yes, Cisco PSIRT confirms limited exploitation | Preserve admin-tech/logs before upgrade; upgrade to fixed releases; validate control connections; open Cisco TAC case if IoCs appear | High |
| Critical | CVE-2026-0826 | Critical, CVSSv4 9.2 | HP Poly VVX and Trio VoIP phones with ICE enabled | Metasploit module developed by Rapid7 | No active exploitation observed in this run | Update VVX to UCS 6.4.8; Trio 8300 to 8.1.7; Trio 8500/8800 to 7.2.8; disable ICE where not required | High |
| Critical | CVE-2026-48188 | Critical, CVSS 9.1 | OTRS 7/8/2023-2026 before 2026.4.x; ((OTRS)) CE 6.0.x | No public PoC confirmed | No active exploitation observed | Upgrade to OTRS 2026.4.1+; disable MySQL/MariaDB `NO_BACKSLASH_ESCAPES`; restrict web UI exposure | High |
| Critical | CVE-2026-7858 | Critical, CVSS 9.8 | Dassault Systemes Teamwork Cloud / Magic Collaboration Studio 2022x-2026x | No working exploit validated | No active exploitation observed | Access vendor remediation portal; restrict management/API exposure; monitor vendor advisory for patch details | Medium |
| Critical | CVE-2026-40965 | Critical, CVSS 10.0 | Cloud Foundry UAA v76.12.0-v78.12.0; CF Deployment v30.0.0-v56.0.0 using EC JWT keys | No public exploit validated | No active exploitation observed | Upgrade UAA to v78.13.0+ or cf-deployment v56.1.0+; rotate exposed EC signing keys/tokens | High |
| Critical | CVE-2026-44211 | Critical, CVSS 9.6 | Cline Kanban local WebSocket server | Advisory includes PoC-style JavaScript; weaponization is straightforward | No active exploitation observed | Update to fixed Cline release; disable kanban/bypass permissions where possible; inventory localhost listeners in AI developer tools | High |
| Critical | CVE-2026-49121 | Critical, CVSS 9.2 | ROCm AITER MessageQueue / distributed inference workers | Public GitHub issue includes technical exploitation path | No active exploitation observed | Avoid unauthenticated cluster networks; replace pickle transport or add HMAC; bind to localhost for single-host deployments; monitor upstream fix | Medium |
| High | CVE-2026-42588 | High, CVSS 8.1 | Apache ActiveMQ Classic Jolokia bridge | Technique is clear from NVD/advisory; authenticated RCE path | No active exploitation observed for this CVE | Upgrade to ActiveMQ 5.19.7 or 6.2.6; restrict `/api/jolokia/`; review low-privilege web console accounts | High |
| High | CVE-2026-49157 | High, CVSS 8.8 | Apache ActiveMQ default Jolokia authorization | No public PoC validated | No active exploitation observed | Upgrade to ActiveMQ 5.19.7 or 6.2.6; remove low-privilege access to admin Jolokia operations | High |
| High | CVE-2026-44825 | High, CVSS 8.1 | Apache Solr 9.4.0-9.10.1 and 10.0.0 when `bin/solr auth enable` was used | Publicly known default credentials condition | No active exploitation observed | Delete/change template users `superadmin`, `admin`, `search`, `index`; upgrade when 9.11.0/10.1.0 are available | High |
| Critical | CVE-2026-8732 | Critical, CVSS 9.8 | WP Maps Pro WordPress plugin <= 6.1.0 | Exploit details publicly described | Yes, active exploitation reported; rogue admin creation | Upgrade to 6.1.1+; audit admin users and `wp-admin/admin-ajax.php?action=wpgmp_temp_access_support` requests | Medium-High |
| Critical | GHSA-qf6p-p7ww-cwr9 | Critical, CVSSv4 9.4 | Gogs <= 0.14.2 and 0.15.0-dev supporting rebase merge | Metasploit module and PoC repository available | No confirmed in-the-wild exploitation | No vendor patch; disable registration, set repo creation limit to 0, disable "Rebase before merging", restrict untrusted users | High |

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
    "sources": ["https://security.paloaltonetworks.com/CVE-2026-0300"]
  },
  {
    "cve": "CVE-2026-0257",
    "cvss": "7.8",
    "vendor": "Palo Alto Networks",
    "product": "PAN-OS GlobalProtect",
    "affected_versions": "PAN-OS/Prisma Access versions before fixed hotfixes where auth override cookies are enabled",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://security.paloaltonetworks.com/CVE-2026-0257",
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
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://sec.cloudapps.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-sdwan-rpa2-v69WY2SW",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"
    ]
  },
  {
    "cve": "CVE-2026-0826",
    "cvss": "9.2",
    "vendor": "HP Poly",
    "product": "VVX and Trio VoIP phones",
    "affected_versions": "VVX 150/250/350/450 and Trio 8300/8500/8800 with vulnerable firmware and ICE enabled",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["Metasploit module referenced in Rapid7 disclosure"],
    "patch_available": true,
    "sources": ["https://www.rapid7.com/blog/post/ve-cve-2026-0826-critical-unauthenticated-stack-buffer-overflow-hp-poly-vvx-trio-voip-phones-fixed/"]
  },
  {
    "cve": "CVE-2026-40965",
    "cvss": "10.0",
    "vendor": "Cloud Foundry",
    "product": "UAA / CF Deployment",
    "affected_versions": "uaa_release v76.12.0-v78.12.0; cf-deployment v30.0.0-v56.0.0 when EC signing keys are used",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://www.cloudfoundry.org/blog/cve-2026-40965-uaa-ec-private-key-disclosure/"]
  },
  {
    "cve": "CVE-2026-44211",
    "cvss": "9.6",
    "vendor": "Cline",
    "product": "Cline Kanban server",
    "affected_versions": "Cline versions with Kanban WebSocket server lacking Origin validation",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://github.com/cline/cline/security/advisories/GHSA-5c57-rqjx-35g2"],
    "patch_available": true,
    "sources": [
      "https://github.com/cline/cline/security/advisories/GHSA-5c57-rqjx-35g2",
      "https://advisories.gitlab.com/npm/cline/CVE-2026-44211/"
    ]
  },
  {
    "cve": "CVE-2026-8732",
    "cvss": "9.8",
    "vendor": "FlipperCode",
    "product": "WP Maps Pro WordPress plugin",
    "affected_versions": "<= 6.1.0",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://securityaffairs.com/192977/hacking/cve-2026-8732-the-wp-maps-pro-flaw-that-lets-anyone-create-a-wordpress-admin-without-a-password.html",
      "https://freshysites.com/security-bulletins/wp-maps-pro-plugin-vulnerability-cve-2026-8732/"
    ]
  }
]
```

## Exploits Released

### Sploitus Reconstructed Top 10

| Rank | CVE / ID | Affected software | Exploit type | Maturity / public PoC | Weaponization potential | Confidence |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | CVE-2026-31431 | Linux kernel AF_ALG `algif_aead` ("Copy Fail") | Local privilege escalation / page-cache write | Public PoCs and Sploitus entries | High for local/container escape paths where vulnerable kernel/module is present | High |
| 2 | CVE-2026-31431 / CVE-2026-43284 / CVE-2026-43500 | Linux kernel Copy Fail / Dirty Frag | LPE scanner and exploit coverage | Sploitus entry claims detection/full PoC for some variants | High in multi-tenant Linux and container environments with prerequisites | Medium-High |
| 3 | CVE-2026-30368 | Lightspeed Classroom | Weak authentication leading to student-device command control | Public PoC write-up indexed by Sploitus | Medium; environment-specific but direct operational abuse | Medium |
| 4 | CVE-2026-35029 | LiteLLM <= 1.83.0 | Broken access control / config endpoint secrets and file read | Packet Storm/Sploitus advisory | Medium-High for self-hosted LLM gateways | Medium |
| 5 | CVE-2026-31899 | CairoSVG | Recursive `<use>` amplification denial of service | Public PoC indexed by Sploitus | Medium; DoS against services rendering untrusted SVG | Medium |
| 6 | CVE-2025-6965 | SQLite / Windows `winsqlite3.dll` | Heap overflow / DoS, possible RCE context | ExploitDB entry indexed by Sploitus | Medium; depends on reachable parser/use case | Low-Medium |
| 7 | CVE-2025-56005 | PLY 3.11 | Unsafe pickle deserialization / arbitrary code execution | Packet Storm/Sploitus PoC | Medium; requires attacker-controlled parser table path | Medium |
| 8 | CVE-2026-40933 | Flowise MCP adapters | Authenticated command injection / RCE | GitHub advisory PoC and third-party reporting | High for self-hosted multi-user Flowise | High |
| 9 | GHSA-qf6p-p7ww-cwr9 | Gogs | Authenticated RCE via `git rebase --exec` argument injection | Metasploit module and public PoC | High on self-hosted Git instances with untrusted users | High |
| 10 | CVE-2026-32746 | GNU InetUtils telnetd 2.7 | Buffer overflow PoC verifying memory corruption | ExploitDB 52556; PoC does not provide RCE | Medium-Low until reliable code execution exists; telnetd exposure is still high-risk | Medium |

### ExploitDB Additions / Notable Indexed Entries

- ExploitDB 52556: GNU InetUtils `telnetd` 2.7 buffer overflow, CVE-2026-32746. Public PoC verifies overflow and response analysis; it explicitly does not achieve code execution.
- ExploitDB 52499: SQLite 3.50.1 heap overflow, CVE-2025-6965, targeting Windows contexts using `winsqlite3.dll`. Treat exploit claims cautiously until independently validated.

### Packet Storm

- Packet Storm-specific current listings were not reliably enumerable during this run.
- Sploitus indexed Packet Storm-derived entries for LiteLLM CVE-2026-35029 and CairoSVG CVE-2026-31899.

### New GitHub PoCs / Exploit Repositories

- Direct GitHub CLI search for repositories created after 2026-05-25 matching `CVE-2026 exploit PoC` returned no repositories.
- Public exploit code or exploit modules identified through other channels:
  - Rapid7 Metasploit module for HP Poly CVE-2026-0826.
  - Rapid7 Metasploit module and community Python PoC for Gogs GHSA-qf6p-p7ww-cwr9.
  - Public issue/advisory PoC details for Flowise CVE-2026-40933.
  - Public Linux Copy Fail/Dirty Frag PoCs referenced by Sploitus.
  - Metasploit framework Langflow module for CVE-2026-27966 was indexed in search results.

## Malware Intelligence

### VX-Underground

- Website root access was not relied on; GitHub organization data was queried directly.
- `vxunderground/MalwareSourceCode`:
  - Latest pushed commit: `1623926c24245e52378f36a6a8d3bd403166a87d`
  - Date: 2026-05-30T07:10:59Z
  - Added file: `Python/Stealer.Python.GMBA.Manipulator.7z`
  - Assessment: archival malware-source addition. Treat as research/malware artifact; do not download or execute outside a controlled malware-analysis environment.
- Other org repos (`VX-API`, `VXUG-Papers`, `ThreatIntelligenceDiscordBot`, `OCRMe`) showed recent GitHub metadata updates but no new pushed code in the current window.

### PureLogs Phishing Campaign

- Source: FortiGuard Labs.
- Campaign: fake purchase-order emails deliver `PO 2026-P0803.rar` containing `kpankocrs.js`.
- Execution chain:
  - JavaScript launches hidden PowerShell.
  - PowerShell performs in-memory .NET loading and process hollowing into `C:\Windows\Microsoft.NET\Framework\v4.0.30319\MsBuild.exe`.
  - Downloader retrieves PureLogs plugin module from `77[.]83[.]39[.]211:8443`.
- Capabilities:
  - Browser credential/cookie theft.
  - Discord token theft.
  - Cryptocurrency wallet collection.
  - Application credential collection for tools including Outlook, FileZilla, OpenVPN, ProtonVPN.
- Key IOCs:
  - C2: `hxxps://77[.]83[.]39[.]211:8443`
  - URLs: `/ping`, `/plugin`, `/userinfo`, `/browser`, `/discord`, `/crypto`, `/application`, `/filesearch/req`, `/finish`
  - SHA-256 samples:
    - `kpankocrs.js`: `3D510977D60A44322F88100B515F06CB5ED83BABC64247068D1A489595FAA6C5`
    - PowerShell stage: `670384FAFB23140D96F2F8FE04A13FC8CC8E2A6E5E8C973E39B58D103C5FEA92`
    - Runtime payload: `B90988400CCED319D260C4937F334ECC364785ED5C593CD2139965E62CA58173`
    - Downloader: `E20B35A8C30E076CDD0E1DF05BA1FF2E418DBD39A674F084787CC0AF2FDA9E95`
    - PureLogs plugin: `07CD03E2082BCB0B890CC59CE4C770D1A095AC6F1AE9CF999F5542555C56F841`
- Recommended actions:
  - Block listed C2 and hashes.
  - Hunt for `wscript.exe -> powershell.exe -> MsBuild.exe` process chains.
  - Alert on PowerShell with `ExecutionPolicy Bypass`, hidden window, dropped scripts in `C:\Temp`.
  - Review browser/Discord/crypto-wallet credential access from suspicious processes.
- Confidence: High.

### The Gentlemen Ransomware / Storm-2697

- Source: Microsoft Threat Intelligence.
- Family: The Gentlemen ransomware-as-a-service, operated by Storm-2697.
- Notable behaviors:
  - Go-based Windows encryptor obfuscated with Garble.
  - Per-file Curve25519 / XChaCha20 cryptographic design.
  - Double extortion.
  - Optional self-propagation using SMB shares, PsExec, WMIC, scheduled tasks, service creation, and remote PowerShell defense-evasion commands.
  - Targets backup, database, virtualization, EDR, SAP, Exchange, and remote-access processes/services before encryption.
- Reported sectors/geographies: education, transportation, healthcare, and financial sectors across North America, South America, Europe, Africa, and Asia.
- Recommended actions:
  - Validate EDR coverage for suspicious scheduled tasks, PsExec/WMI lateral movement, and Defender tampering.
  - Hunt for ransom note `README-GENTLEMEN.txt` and file extension `.umc16h`.
  - Harden admin shares, restrict lateral movement, and verify immutable/offline backups.
- Confidence: High.

## Ransomware, Breach, and Threat Actor Activity

- Abyss ransomware reportedly listed Limburg-Weilburg County Administration in Germany on 2026-06-01. Confidence: Medium; sourced from public threat-intelligence reposts.
- DentaQuest/ShinyHunters reporting indicates an alleged 233 GB data corpus surfaced after a ransom deadline. Confidence: Medium; incident acknowledgment exists but data scope requires victim/regulator confirmation.
- Carnival Corporation disclosed a breach affecting approximately 5,995,277 people, involving personal information such as name, contact details, date of birth, and government-issued ID/passport numbers. Confidence: Medium-High; source includes public reporting citing Maine AG filing.

## Security Releases and Vendor Advisories

### Microsoft

- No June Patch Tuesday release occurred on 2026-06-01; next scheduled Patch Tuesday is 2026-06-09.
- Priority carry-over:
  - Patch CVE-2026-41089 on all domain controllers immediately.
  - Verify Microsoft Defender Malware Protection Engine is at least 1.1.26040.8 for recent Defender flaws, including CVE-2026-41091 and CVE-2026-45498.
- Confidence: Medium-High.

### Cisco

- Cisco Catalyst SD-WAN advisory for CVE-2026-20182 remains emergency priority.
- No workaround; fixed releases are required.
- Preserve logs/admin-tech before upgrades to retain forensic evidence.
- Confidence: High.

### Palo Alto Networks

- CVE-2026-0300 and CVE-2026-0257 are both marked ATTACKED by the vendor.
- Apply fixed PAN-OS versions and mitigation guidance.
- Confidence: High.

### GitLab

- Patch release 19.0.1, 18.11.4, 18.10.7 published 2026-05-27.
- Highest-priority issue: CVE-2026-4868, improper access control in Duo AI workflow runners (GitLab EE).
- Other fixed CVEs include CVE-2026-1402, CVE-2026-6713, CVE-2026-5296, CVE-2026-2601, CVE-2026-8716, and CVE-2026-2710.
- Recommended action: upgrade self-managed GitLab to the relevant patched branch. GitLab.com is patched by vendor.
- Confidence: High.

### GitHub Enterprise Server

- GHES 3.20.3 released 2026-05-26.
- Fixes include:
  - CVE-2026-9312 - critical pre-auth SSRF in upload endpoint.
  - CVE-2026-43284 and CVE-2026-43500 - high-severity Dirty Frag Linux kernel LPE issues.
  - CVE-2026-8606 - timing side-channel plus SSRF in package lookup feature.
- Operational note: manual GPG signing key rotation is required before upgrade.
- Confidence: High.

### Apple

- Apple security releases page lists iOS 26.5.1 and macOS Tahoe 26.5.1 on 2026-06-01 with no published CVE entries.
- No new actively exploited Apple CVE was identified for this report window.
- Confidence: High.

### Fortinet

- No new June 1 Fortinet PSIRT zero-day was validated in this run.
- Carry-over priority: CVE-2026-24858 FortiCloud SSO auth bypass was exploited in January 2026 and remains relevant for unpatched Fortinet devices.
- FortiGuard Labs published PureLogs campaign analysis with protections and IOCs.
- Confidence: Medium-High.

### VMware / Broadcom

- No new June 1 critical exploited VMware advisory was validated.
- Carry-over: VMware Aria Operations CVE-2026-22719 remains KEV-listed from March 2026.
- Broadcom impact notes for Dirty Frag/Fragnesia indicate Photon-based virtual appliances are generally not affected, while vSphere Kubernetes Service Ubuntu nodes may require mitigation under select conditions.
- Confidence: Medium.

### Apache

- Apache ActiveMQ:
  - Upgrade to 5.19.7 or 6.2.6 for CVE-2026-42588 and CVE-2026-49157.
- Apache Solr:
  - CVE-2026-44825 affects BasicAuth bootstrapped with `bin/solr auth enable`; remove or rotate default template users immediately.
  - Future 9.11.0/10.1.0 releases are expected to remove the issue.
- Confidence: High.

### HP Poly

- CVE-2026-0826 fixed in:
  - VVX: UCS 6.4.8
  - Trio 8300: UCS 8.1.7
  - Trio 8500/8800: UCS 7.2.8
- Disable ICE where not required.
- Confidence: High.

## Recommended Actions (Ranked)

1. Emergency patch and hunt for active exploitation:
   - Windows domain controllers: CVE-2026-41089.
   - Oracle WebLogic: CVE-2024-21182, especially internet-facing T3/IIOP.
   - PAN-OS: CVE-2026-0300 and CVE-2026-0257.
   - Cisco Catalyst SD-WAN: CVE-2026-20182.
2. Validate KEV coverage:
   - Pull current CISA KEV into vulnerability management.
   - Confirm deadlines for WebLogic (2026-06-04), Microsoft Defender (2026-06-03), Trend Micro Apex One (2026-06-04), Langflow (2026-06-04), Nx/TanStack (2026-06-10).
3. Secure developer and AI tooling:
   - Update Cline, Flowise, Langflow, LiteLLM, and Gogs mitigations.
   - Disable unneeded local WebSocket/MCP stdio features.
   - Treat public workflow/chatflow templates as code execution artifacts.
4. Patch internet-facing and enterprise middleware:
   - HP Poly VoIP phones with ICE enabled.
   - OTRS / ((OTRS)) Community Edition.
   - ActiveMQ, Solr, GitLab, GHES, Cloud Foundry UAA.
5. Supply-chain incident response:
   - For TanStack/Nx exposure windows, rotate GitHub, npm, cloud, Vault, SSH, 1Password, Docker, and Kubernetes credentials accessible from affected hosts/CI runners.
   - Audit GitHub Actions OIDC trusted-publisher workflows and cache poisoning boundaries.
6. Malware and ransomware defense:
   - Deploy PureLogs IOCs and behavioral detections.
   - Hunt for The Gentlemen ransomware behaviors, especially PsExec/WMIC propagation, Defender tampering, and `.umc16h` extension.
   - Verify backups are immutable and restoration-tested.
7. WordPress exposure:
   - Patch WP Maps Pro to 6.1.1+.
   - Search for rogue `fc_user_` or unknown administrator accounts.
   - Review `admin-ajax.php` logs for `wpgmp_temp_access_support` / `wpgmp_temp_access_ajax`.

## Sources

- CISA KEV JSON: https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json
- CISA alert: https://www.cisa.gov/news-events/alerts/2026/06/01/cisa-adds-one-known-exploited-vulnerability-catalog
- NVD API: https://services.nvd.nist.gov/rest/json/cves/2.0
- Oracle CPU July 2024: https://www.oracle.com/security-alerts/cpujul2024.html
- Palo Alto CVE-2026-0257: https://security.paloaltonetworks.com/CVE-2026-0257
- Palo Alto CVE-2026-0300: https://security.paloaltonetworks.com/CVE-2026-0300
- Cisco SD-WAN advisory: https://sec.cloudapps.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-sdwan-rpa2-v69WY2SW
- Rapid7 HP Poly CVE-2026-0826: https://www.rapid7.com/blog/post/ve-cve-2026-0826-critical-unauthenticated-stack-buffer-overflow-hp-poly-vvx-trio-voip-phones-fixed/
- Rapid7 Gogs RCE: https://www.rapid7.com/blog/post/ve-authenticated-rce-via-argument-injection-gogs-unfixed/
- GitHub Nx Console advisory: https://github.com/nrwl/nx-console/security/advisories/GHSA-c9j4-9m59-847w
- GitHub TanStack advisory: https://github.com/TanStack/router/security/advisories/GHSA-g7cv-rxg3-hmpx
- Cloud Foundry UAA advisory: https://www.cloudfoundry.org/blog/cve-2026-40965-uaa-ec-private-key-disclosure/
- Cline advisory: https://github.com/cline/cline/security/advisories/GHSA-5c57-rqjx-35g2
- FortiGuard PureLogs campaign: https://www.fortinet.com/blog/threat-research/phishing-campaign-deploys-javascript-driven-purelogs-variant-to-steal-sensitive-data
- Microsoft The Gentlemen ransomware: https://www.microsoft.com/en-us/security/blog/2026/05/28/the-gentlemen-ransomware-dissecting-a-self-propagating-go-encryptor/
- GitLab patch release: https://docs.gitlab.com/releases/patches/patch-release-gitlab-19-0-1-released/
- GitHub Enterprise Server release notes: https://docs.github.com/en/enterprise-server@3.20/admin/release-notes
- Apple security releases: https://support.apple.com/en-us/100100
- Apache Solr oss-sec: https://seclists.org/oss-sec/2026/q2/731
- VX-Underground GitHub: https://github.com/vxunderground/MalwareSourceCode
