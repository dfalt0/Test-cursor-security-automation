# Security Intelligence Report - 2026-06-02 12:01 UTC

Repository: dfalt0/Test-cursor-security-automation
Branch: cursor/security-intelligence-agent-39de
Report window: 2026-06-02 10:00-12:30 UTC, with 24-hour enrichment from 2026-06-01 12:30 UTC
Confidence key: High = primary source plus corroboration; Medium = primary source only or strong secondary corroboration; Low = unvalidated public indicator.

## Executive Summary

- NVD published 13 CVEs in the 10:00-12:30 UTC window: 2 critical, 1 high, 8 medium, and 2 unknown severity.
- NVD published 56 CVEs day-to-date on 2026-06-02: 3 critical, 3 high, 31 medium, 15 low, and 4 unknown severity.
- Rolling 24-hour NVD volume was 330 CVEs: 21 critical, 93 high, 126 medium, 54 low, and 36 unknown severity.
- New critical CVEs in this run:
  - CVE-2025-53209: WordPress Masteriyo LMS PRO privilege escalation, CVSS 9.8, fixed in 2.20.1.
  - CVE-2026-34906: Simple SA Wirtualna Uczelnia unauthenticated SSTI to RCE, CVSS 9.3.
- Active exploitation and emergency remediation remain highest priority for Cisco Catalyst SD-WAN CVE-2026-20182, Palo Alto PAN-OS CVE-2026-0257, Drupal core CVE-2026-9082, Microsoft Netlogon CVE-2026-41089, FortiClient EMS CVE-2026-35616, cPanel/WHM CVE-2026-41940, LiteSpeed cPanel plugin CVE-2026-48172, and Oracle WebLogic CVE-2024-21182.
- New GitHub PoC indicator observed since the prior run: Jenderal92/CVE-2026-8206, described as a mass exploitation tool for the critical Kirki WordPress plugin account-takeover issue. Treat as unvalidated and potentially malicious until reviewed in a sandbox.
- Malware and campaign updates: FortiClient EMS exploitation continues to be associated with EKZ Infostealer delivery; cPanel/WHM exploitation continues to be associated with ransomware, Mirai variants, miners, and backdoors; VX-Underground GitHub has no newer MalwareSourceCode commit than 2026-05-30.

## Top Vulnerabilities

| Priority | CVE | Severity | Affected software | Exploit availability | Active exploitation | Recommended action | Confidence |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Critical | CVE-2026-20182 | Critical, CVSS 10.0 | Cisco Catalyst SD-WAN Controller and Manager | Public GitHub indicators and Sploitus/Rapid7-derived indicators observed in prior runs | Yes, Cisco PSIRT reports limited exploitation; CISA KEV listed | Preserve admin-tech/logs, hunt for IoCs, and upgrade to fixed SD-WAN releases immediately | High |
| Critical | CVE-2026-41089 | Critical, CVSS 9.8 | Microsoft Windows Netlogon on domain controllers | Public GitHub PoC indicators: 0xABCD01/CVE-2026-41089 and 0xBlackash/CVE-2026-41089 | CCB Belgium and secondary reporting state active exploitation; not observed in CISA KEV during this run | Patch all domain controllers, restrict Netlogon/RPC exposure, and monitor anomalous RPC/Netlogon traffic | Medium |
| Critical | CVE-2026-0257 | High, CVSS 7.8 but attacked | Palo Alto PAN-OS GlobalProtect with auth override cookie configurations | Multiple public GitHub PoC indicators, including sfewer-r7/CVE-2026-0257 | Yes, vendor says ATTACKED and limited exploit attempts; CISA KEV listed | Apply fixed PAN-OS/Prisma Access versions or disable/regenerate auth override cookies per vendor guidance | High |
| Critical | CVE-2026-9082 | Critical, Drupal highly critical 23/25, NVD CVSS 9.8 | Drupal core on PostgreSQL backends | Public Sploitus entry, ExploitDB/PoC references, and multiple GitHub PoCs | Yes, Drupal update says exploit attempts detected in the wild; CISA KEV listed | Upgrade to fixed Drupal branch releases and review PostgreSQL-backed sites for suspicious JSON:API/query activity | High |
| Critical | CVE-2026-35616 | Critical, CVSS 9.8/9.1 | Fortinet FortiClient EMS 7.4.5-7.4.6 | Multiple public detection/exploit repositories | Yes, watchTowr observed exploitation and Arctic Wolf ties abuse to EKZ Infostealer delivery | Apply Fortinet hotfix/full patch, restrict EMS management exposure, and hunt for FortiEndpoint_Patch.exe/p.exe activity | High |
| Critical | CVE-2026-41940 | Critical, CVSS 9.8 | cPanel and WHM | Public exploit code and Sploitus entry observed | Yes, multi-actor exploitation with ransomware, botnet, miner, backdoor, and espionage reporting; CISA KEV listed | Patch to fixed cPanel versions, rotate credentials, audit sessions, and hunt webshell/backdoor/ransomware artifacts | High |
| Critical | CVE-2026-48172 | Critical operational risk | LiteSpeed cPanel user-end plugin v2.3-v2.4.4 | Public GitHub indicators observed | Yes, LiteSpeed says actively exploited; CISA KEV listed | Upgrade to WHM plugin 5.3.1.0/cPanel plugin 2.4.7 or remove user-end plugin and review logs | High |
| Critical | CVE-2024-21182 | Critical KEV priority | Oracle WebLogic Server | No new PoC confirmed in this run | CISA KEV added 2026-06-01 | Apply Oracle CPU guidance or isolate affected T3/IIOP exposure; due date 2026-06-04 in KEV | High |
| High | CVE-2025-53209 | Critical, CVSS 9.8 | WordPress Masteriyo LMS PRO <= 2.20.0 | No Sploitus/GitHub PoC found in this run | No active exploitation confirmed | Update to Masteriyo LMS PRO 2.20.1 or later; prioritize internet-facing WordPress sites | High |
| High | CVE-2026-34906 | Critical, CVSS 9.3 | Simple SA Wirtualna Uczelnia <= wu#2016.437.295#0#20260327_105545 | No Sploitus/GitHub PoC found in this run | No active exploitation confirmed | Patch or isolate Wirtualna Uczelnia; monitor redirectToUrl/redirectUrlParameter abuse and reverse shell indicators | High |
| High | CVE-2026-8206 | Critical, CVSS 9.8 | Kirki WordPress plugin 6.0.0-6.0.6 | New GitHub repo Jenderal92/CVE-2026-8206 claims mass exploitation; unvalidated | No primary active exploitation confirmation found | Update Kirki to latest fixed release and inspect password-reset/account changes | Medium |
| High | CVE-2026-40965 | Critical, CVSS 10.0 | Cloud Foundry UAA v76.12.0-v78.12.0 and cf-deployment v30.0.0-v56.0.0 using EC JWT keys | No public exploit confirmed | No active exploitation confirmed | Upgrade UAA to v78.13.0+ and cf-deployment to v56.1.0+; rotate exposed EC signing keys/tokens | High |
| High | CVE-2026-46718 | Unknown in NVD, security impact high by class | Apache Calcite 1.5.0 before 1.42 | No public exploit confirmed | No active exploitation confirmed | Upgrade Apache Calcite to 1.42 or later | Medium |
| High | CVE-2026-3514 | High, CVSS 7.5 | Prefect 3.6.19 | Commit and advisory references available; no standalone PoC confirmed | No active exploitation confirmed | Upgrade Prefect and audit unauthenticated access to names ending in health/ready | Medium |
| Medium | CVE-2026-5422 | Medium, CVSS 6.8 | Jupyter Server 2.17.0 | huntr details; no standalone PoC confirmed | No active exploitation confirmed | Upgrade when fixed release is available; restrict file browsing roots and review sibling-prefix path traversal risk | Medium |

## Exploits Released and PoC Indicators

### Sploitus Top 10 / Indexed Exploit Reconstruction

The Sploitus homepage did not expose a static "Exploits of the Week" top-10 block to automated fetching. The following is a reconstructed top set from indexed Sploitus result pages and should be treated as exploit-intelligence indicators, not proof that each exploit is functional.

| Rank | CVE(s) | Affected software | Exploit type | Maturity | Public PoC availability | Weaponization potential |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | CVE-2026-9082 | Drupal core on PostgreSQL | Unauthenticated SQL injection leading to data theft/RCE paths | Weaponized | Yes, Sploitus and GitHub PoCs | Very high; active exploitation and KEV |
| 2 | CVE-2026-41940 | cPanel/WHM | Pre-auth authentication bypass to admin/root-level control | Weaponized | Yes, Sploitus and public exploit references | Very high; ransomware/backdoor campaigns |
| 3 | CVE-2026-45659 | Microsoft SharePoint | Deserialization RCE by authorized attacker | Unvalidated Sploitus indicator | Sploitus-listed; snippet claims private/not public while also showing usage text | High if functional; verify carefully |
| 4 | CVE-2026-20660 | Apple Safari/macOS download handling | Path traversal via gzip FNAME | PoC-level | Sploitus-listed | Medium; client-side preconditions |
| 5 | CVE-2026-43284 / CVE-2026-43500 | Linux kernel | Local privilege escalation via page-cache corruption chain | PoC/weaponized LPE | Sploitus and ExploitDB indicators | High for post-compromise escalation |
| 6 | CVE-2026-4660 | HashiCorp go-getter/Terraform module flows | Arbitrary file read through git checkout pathspec injection | PoC-level | Sploitus-listed | High for CI/CD secret exposure |
| 7 | CVE-2026-32710 | MariaDB | Heap buffer overflow to privilege escalation | PoC-level | Sploitus-listed | High where vulnerable DB versions exposed to SQL users |
| 8 | CVE-2026-40176 / CVE-2026-40261 | Composer Perforce VCS driver | Command injection | PoC-level | Sploitus-listed | High in build/dependency pipelines using Perforce repositories |
| 9 | CVE-2026-34159 | llama.cpp RPC server | Zero-click RCE | PoC-level | Sploitus-listed | High where RPC exposed |
| 10 | CVE-2026-32746 | GNU inetutils telnetd | Pre-auth buffer overflow | PoC-level, not full RCE per ExploitDB text | ExploitDB/Sploitus indicators | Medium to high; depends on telnetd exposure |

### ExploitDB Additions

Direct ExploitDB CSV retrieval showed these latest relevant entries (no direct 2026-06-02 addition observed in the CSV during this run):

- EDB-ID 52591, 2026-05-29: Linux Kernel local privilege escalation, CVE-2026-46300/CVE-2026-43500/CVE-2026-43284.
- EDB-ID 52584, 2026-05-27: Casdoor 3.54.1 arbitrary file write via path traversal, CVE-2026-6815.
- EDB-ID 52581, 2026-05-27: MeiG Smart FORGE_SLT711 OS command injection, CVE-2026-36356.
- EDB-ID 52585, 2026-05-27: Linux Kernel local privilege escalation, CVE-2026-43500/CVE-2026-43284.
- EDB-ID 52580, 2026-05-27: Realtek rtl819x local privilege issue, CVE-2026-36355.

### New GitHub PoC / Repository Indicators

All GitHub repositories below are unvalidated and may be incomplete, non-functional, or malicious. Review only in an isolated environment.

- New since this run:
  - https://github.com/Jenderal92/CVE-2026-8206 - created 2026-06-02 10:53 UTC, pushed 11:46 UTC, claims "mass exploitation tool" for Kirki CVE-2026-8206.
  - https://github.com/0xBlackash/CVE-2026-41089 - created 2026-06-02 10:35 UTC for Microsoft Netlogon CVE-2026-41089.
- Recently active carry-forward indicators:
  - https://github.com/0xABCD01/CVE-2026-41089 - Netlogon PoC indicator, pushed 2026-06-02 08:30 UTC.
  - https://github.com/sfewer-r7/CVE-2026-0257 - PAN-OS GlobalProtect authentication bypass PoC indicator.
  - https://github.com/7h30th3r0n3/CVE-2026-9082-Drupal-PoC and https://github.com/ambionics/cve-2026-9082-drupal-postgresql-rce - Drupal CVE-2026-9082 PoC indicators.
  - https://github.com/Alaatk/CVE-2026-35616 and https://github.com/BishopFox/CVE-2026-35616-check - FortiClient EMS CVE-2026-35616 exploit/detection indicators.
  - https://github.com/HORKimhab/CVE-2026-48172 and https://github.com/retmakarunia/CVE-2026-48172 - LiteSpeed cPanel plugin CVE-2026-48172 indicators.

## Malware Intelligence

- VX-Underground:
  - Web root was reachable but did not show a new report list in this run.
  - GitHub user vxunderground latest MalwareSourceCode commit remains 2026-05-30 07:10:59 UTC.
  - Latest added file: `Python/Stealer.Python.GMBA.Manipulator.7z`.
  - No newer VX MalwareSourceCode commit was observed after the prior hourly run.
- FortiClient EMS / EKZ Infostealer:
  - Arctic Wolf reports CVE-2026-35616 exploitation used FortiClient EMS-managed endpoints to deliver EKZ Infostealer disguised as a Fortinet patch.
  - Key execution pattern: FortiClient components launching cmd.exe/powershell.exe and a payload such as FortiEndpoint_Patch.exe or p.exe.
- cPanel/WHM exploitation:
  - XLab, Help Net Security, and Picus reporting describe exploitation of CVE-2026-41940 by multiple actors for ransomware, Mirai variants, miners, and backdoors.
  - "Sorry" ransomware and Mr_Rot13 backdoor activity remain notable follow-up hunting themes.
- Supply chain:
  - Mini Shai-Hulud / TeamPCP remains the key software supply-chain campaign, affecting npm/PyPI packages including TanStack, Mistral AI, UiPath, OpenSearch-related packages, and Guardrails AI.
  - Primary TanStack postmortem attributes compromise to GitHub Actions trust-boundary weaknesses, cache poisoning, and OIDC token extraction from runner memory.

## Security Releases and Vendor Advisories

- Microsoft: May 2026 patches address CVE-2026-41089 Netlogon RCE; apply to Windows Server domain controllers immediately.
- Cisco: Cisco Catalyst SD-WAN fixed releases are available for CVE-2026-20182; no workaround; preserve logs/admin-tech before upgrade.
- Palo Alto Networks: PAN-OS fixes and mitigations are available for CVE-2026-0257; vendor marks exploit maturity as ATTACKED.
- Fortinet: FortiClient EMS hotfix/full remediation guidance for CVE-2026-35616; restrict management-plane exposure.
- Oracle: CISA KEV added CVE-2024-21182 for WebLogic Server on 2026-06-01; follow Oracle CPU guidance and prioritize before the KEV due date.
- Drupal: SA-CORE-2026-004 fixed CVE-2026-9082 in Drupal 10.4.10, 10.5.10, 10.6.9, 11.1.10, 11.2.12, and 11.3.10.
- LiteSpeed: cPanel plugin CVE-2026-48172 fixed in cPanel plugin 2.4.7 bundled with WHM plugin 5.3.1.0.
- Cloud Foundry: UAA CVE-2026-40965 fixed in uaa_release v78.13.0+ and cf-deployment v56.1.0+.
- CERT Polska / Simple SA: Wirtualna Uczelnia CVE-2026-34906 and CVE-2026-34907 disclosed for versions up to wu#2016.437.295#0#20260327_105545.
- Patchstack: Masteriyo LMS PRO CVE-2025-53209 fixed in 2.20.1.
- Apache: Apache Calcite CVE-2026-46718 affects 1.5.0 before 1.42; upgrade to 1.42. NVD also listed Apache Kafka CVE-2026-41115 during the run, but public Apache page corroboration was limited; track vendor updates before escalating beyond NVD-sourced status.

## Recommended Actions

1. Emergency patch and hunt: Cisco SD-WAN CVE-2026-20182, PAN-OS CVE-2026-0257, Drupal CVE-2026-9082, Microsoft Netlogon CVE-2026-41089, cPanel/WHM CVE-2026-41940, FortiClient EMS CVE-2026-35616, LiteSpeed cPanel plugin CVE-2026-48172, and Oracle WebLogic CVE-2024-21182.
2. For WordPress fleets, immediately inventory and update Kirki, Masteriyo LMS PRO, and other high-risk plugins from this run; review administrator/user account changes and password-reset events.
3. For identity/control-plane products, rotate potentially exposed secrets after patching: Cloud Foundry UAA EC signing keys, cPanel/WHM credentials, FortiClient EMS administrative/API secrets, and affected CI/CD tokens from Mini Shai-Hulud exposure.
4. Treat public GitHub PoCs as hostile until proven otherwise. Analyze in disposable sandboxes, disable outbound network access where possible, and do not run against production systems.
5. Add detections for:
   - Netlogon/RPC anomalies targeting domain controllers.
   - PAN-OS GlobalProtect authentication-override cookie anomalies.
   - Cisco SD-WAN control connection events with no challenge-ack and unexpected peer public IPs.
   - Drupal PostgreSQL SQL injection probes against JSON:API or user/login endpoints.
   - FortiClient EMS process chains involving fortitray.exe or ipsec.exe to cmd.exe/powershell.exe to suspicious patch binaries.
   - cPanel session anomalies, new admin accounts, webshells, miners, and `.sorry` ransomware artifacts.

## Unified Vulnerability Records

```json
[
  {
    "cve": "CVE-2026-20182",
    "cvss": "10.0",
    "vendor": "Cisco",
    "product": "Catalyst SD-WAN Controller and Manager",
    "affected_versions": "Multiple Catalyst SD-WAN releases before fixed releases listed by Cisco",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://github.com/portbuster1337/CVE-2026-20182", "https://github.com/Nxploited/CVE-2026-20182"],
    "patch_available": true,
    "sources": ["https://sec.cloudapps.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-sdwan-rpa2-v69WY2SW", "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"]
  },
  {
    "cve": "CVE-2026-41089",
    "cvss": "9.8",
    "vendor": "Microsoft",
    "product": "Windows Netlogon",
    "affected_versions": "Windows Server 2012 through 2025 domain-controller deployments per NVD/MSRC",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": false,
    "poc_links": ["https://github.com/0xABCD01/CVE-2026-41089", "https://github.com/0xBlackash/CVE-2026-41089"],
    "patch_available": true,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2026-41089", "https://www.securityweek.com/critical-windows-netlogon-vulnerability-in-attackers-crosshairs/", "https://www.bleepingcomputer.com/news/microsoft/critical-windows-netlogon-remote-code-execution-flaw-now-exploited-in-attacks/"]
  },
  {
    "cve": "CVE-2026-0257",
    "cvss": "7.8",
    "vendor": "Palo Alto Networks",
    "product": "PAN-OS GlobalProtect",
    "affected_versions": "PAN-OS 10.2, 11.1, 11.2, 12.1 ranges and Prisma Access ranges before fixed releases",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://github.com/sfewer-r7/CVE-2026-0257"],
    "patch_available": true,
    "sources": ["https://security.paloaltonetworks.com/CVE-2026-0257", "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"]
  },
  {
    "cve": "CVE-2026-9082",
    "cvss": "9.8",
    "vendor": "Drupal",
    "product": "Drupal core",
    "affected_versions": "Drupal core 8.9.0-11.3.9 on PostgreSQL backends, with branch-specific fixed versions",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://github.com/7h30th3r0n3/CVE-2026-9082-Drupal-PoC", "https://github.com/ambionics/cve-2026-9082-drupal-postgresql-rce", "https://sploitus.com/exploit?id=1774D6F8-2B0F-5C66-A7AB-BE7B8E7A0B85"],
    "patch_available": true,
    "sources": ["https://www.drupal.org/sa-core-2026-004", "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"]
  },
  {
    "cve": "CVE-2026-35616",
    "cvss": "9.8",
    "vendor": "Fortinet",
    "product": "FortiClient EMS",
    "affected_versions": "7.4.5 through 7.4.6",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://github.com/Alaatk/CVE-2026-35616", "https://github.com/BishopFox/CVE-2026-35616-check"],
    "patch_available": true,
    "sources": ["https://watchtowr.com/resources/fortinet-forticlient-ems-zero-day-cve-2026-35616-active-exploitation-underway/", "https://arcticwolf.com/resources/blog/forticlient-ems-exploited-via-cve-2026-35616-to-deliver-ekz-infostealer-disguised-as-a-fortinet-patch/"]
  },
  {
    "cve": "CVE-2026-41940",
    "cvss": "9.8",
    "vendor": "cPanel",
    "product": "cPanel and WHM",
    "affected_versions": "cPanel and WHM after 11.40 and before fixed release trains listed by NVD/vendor",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://sploitus.com/exploit?id=45A263F9-3CDF-57F8-9637-E0D5F28635FF"],
    "patch_available": true,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2026-41940", "https://www.helpnetsecurity.com/2026/05/04/multiple-threat-actors-actively-exploit-cpanel-vulnerability-cve-2026-41940/", "https://blog.xlab.qianxin.com/mr_rot13-the-elusive-6-year-hacker-group-weaponizing-critical-cpanel-flaws-for-backdoor-deployment/"]
  },
  {
    "cve": "CVE-2026-48172",
    "cvss": "unknown",
    "vendor": "LiteSpeed",
    "product": "LiteSpeed cPanel user-end plugin",
    "affected_versions": "v2.3 through v2.4.4",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://github.com/HORKimhab/CVE-2026-48172", "https://github.com/retmakarunia/CVE-2026-48172"],
    "patch_available": true,
    "sources": ["https://blog.litespeedtech.com/2026/05/21/security-update-for-litespeed-cpanel-plugin/", "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"]
  },
  {
    "cve": "CVE-2025-53209",
    "cvss": "9.8",
    "vendor": "Themeisle",
    "product": "Masteriyo LMS PRO",
    "affected_versions": "<= 2.20.0",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://patchstack.com/database/wordpress/plugin/learning-management-system-pro/vulnerability/wordpress-masteriyo-lms-pro-2-20-0-privilege-escalation-vulnerability?_s_id=cve", "https://nvd.nist.gov/vuln/detail/CVE-2025-53209"]
  },
  {
    "cve": "CVE-2026-34906",
    "cvss": "9.3",
    "vendor": "Simple SA",
    "product": "Wirtualna Uczelnia",
    "affected_versions": "<= wu#2016.437.295#0#20260327_105545",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://cert.pl/posts/2026/06/CVE-2026-34906", "https://nvd.nist.gov/vuln/detail/CVE-2026-34906"]
  },
  {
    "cve": "CVE-2026-8206",
    "cvss": "9.8",
    "vendor": "WordPress plugin ecosystem",
    "product": "Kirki",
    "affected_versions": "6.0.0 through 6.0.6",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://github.com/Jenderal92/CVE-2026-8206", "https://github.com/O99099O/CVE-2026-8206-Poc-"],
    "patch_available": true,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2026-8206", "https://plugins.trac.wordpress.org/changeset/3530843/kirki"]
  },
  {
    "cve": "CVE-2026-40965",
    "cvss": "10.0",
    "vendor": "Cloud Foundry",
    "product": "UAA",
    "affected_versions": "uaa_release v76.12.0-v78.12.0 and cf-deployment v30.0.0-v56.0.0 with EC JWT keys",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://www.cloudfoundry.org/blog/cve-2026-40965-uaa-ec-private-key-disclosure/", "https://nvd.nist.gov/vuln/detail/CVE-2026-40965"]
  },
  {
    "cve": "CVE-2026-46718",
    "cvss": "unknown",
    "vendor": "Apache",
    "product": "Calcite",
    "affected_versions": "1.5.0 before 1.42",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://lists.apache.org/thread/9s37svo343w5ck1ovh478lkzcqk4949v", "https://nvd.nist.gov/vuln/detail/CVE-2026-46718"]
  }
]
```

## Source Notes

- NVD API queries were run for 2026-06-02 10:00-12:30 UTC, 2026-06-02 day-to-date, and a rolling 24-hour window.
- CISA KEV JSON feed version observed: 2026.06.01, released 2026-06-01T16:59:32.7272Z.
- Packet Storm direct fetch/search produced no reliable specific 2026-06-02 exploit list; report uses Packet Storm only as a monitored source with no confirmed new item.
- MalwareBazaar authenticated API access was not available in this environment, consistent with prior runs; malware coverage relies on public reporting, VX GitHub, and web-searchable threat research.
