# Security Intelligence Report - 2026-06-02 09:01 UTC

Collection window: 2026-06-02 08:00-09:35 UTC, with rolling 24-hour enrichment from 2026-06-01 09:35 UTC.

Repository: `dfalt0/Test-cursor-security-automation`

## Executive Summary

- NVD publications: 0 CVEs newly published in the 08:00-09:35 UTC hour. Day-to-date NVD total is 25 CVEs: 1 critical, 7 medium, 15 low, and 2 unknown. Rolling 24-hour NVD total is 309 CVEs: 19 critical, 90 high, 107 medium, 59 low, and 34 unknown.
- Critical findings requiring immediate review: Cisco Catalyst SD-WAN CVE-2026-20182, Microsoft Netlogon CVE-2026-41089, Palo Alto PAN-OS CVE-2026-0257, Fortinet FortiClient EMS CVE-2026-35616, Drupal Core CVE-2026-9082, cPanel/WHM CVE-2026-41940, Cloud Foundry UAA CVE-2026-40965, Kirki WordPress CVE-2026-8206, Oracle WebLogic CVE-2024-21182, and the Nx/TanStack/Mini Shai-Hulud supply-chain cluster.
- Active exploitation findings: Cisco SD-WAN, PAN-OS GlobalProtect, FortiClient EMS, Drupal Core, cPanel/WHM, Microsoft Netlogon, and Microsoft Defender CVE-2026-41091/CVE-2026-45498 are reported or cataloged as exploited. Confidence varies by source; see individual records.
- New malware and campaign intelligence: Arctic Wolf reporting ties FortiClient EMS exploitation to EKZ Infostealer delivery through legitimate endpoint-management workflows. VX-Underground GitHub activity shows no new push this hour; latest MalwareSourceCode addition remains `Python/Stealer.Python.GMBA.Manipulator.7z` from 2026-05-30. Mini Shai-Hulud/Miasma npm supply-chain activity expanded into `@redhat-cloud-services` packages in public reporting.
- Important vendor releases/advisories: Cisco fixed SD-WAN releases; Palo Alto fixed PAN-OS/Prisma Access releases; Fortinet FortiClient EMS 7.4.7/hotfix guidance; Drupal fixed 10.4.10/10.5.10/10.6.9/11.1.10/11.2.12/11.3.10; Cloud Foundry UAA v78.13.0/cf-deployment v56.1.0; GitLab 19.0.1/18.11.4/18.10.7; Kirki 6.0.7.

## Source Coverage and Caveats

- CISA KEV feed: checked JSON catalog version `2026.06.01`, released `2026-06-01T16:59:32.7272Z`.
- NVD API: queried hourly, day-to-date, and rolling 24-hour publication windows.
- Sploitus: homepage and query pages still expose only the static search UI to non-browser fetches. The "Sploitus Top 10" below is reconstructed from indexed Sploitus result pages, not an official homepage "Exploits of the Week" extraction.
- ExploitDB: parsed the official exploitdb GitLab CSV. All latest entries listed below are marked `verified=0` by ExploitDB.
- Packet Storm: direct fetch returned an anti-abuse block; no Packet Storm additions are asserted in this report.
- GitHub: queried global advisories and repository search. GitHub PoC repositories are treated as indicators only; functionality and safety are not assumed.
- VX-Underground: checked GitHub repositories through the authenticated GitHub API. The vx-underground web root was not relied on.
- Wazuh CTI/OpenCVE/AttackerKB/GreyNoise/Shadowserver/SANS-style searches were used for enrichment where indexed results were available; primary vendor and CISA/NVD sources take precedence.

## Top Vulnerabilities

| Priority | CVE / Issue | Severity | Affected software | Exploit availability | Active exploitation | Recommended action | Confidence |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Critical | CVE-2026-20182 | CVSS 10.0 | Cisco Catalyst SD-WAN Controller/Manager | Sploitus PoC, Rapid7/Metasploit references | Yes; Cisco PSIRT confirms limited exploitation and Talos tracks UAT-8616 activity; CISA KEV | Upgrade to Cisco fixed releases, preserve admin-tech/log artifacts before upgrade, review control-connection and auth logs | High |
| Critical | CVE-2026-41089 | CVSS 9.8 | Microsoft Windows Server domain controllers / Netlogon | Public GitHub indicator exists; functionality unvalidated | Reported active by Belgium CCB and multiple secondary outlets; not in CISA KEV feed at collection time | Patch all domain controllers with May 2026 updates, restrict Netlogon/RPC exposure, hunt anomalous LSASS/Netlogon activity | Medium |
| Critical | CVE-2026-0257 | CVSS-B 7.8 but enterprise-critical | Palo Alto Networks PAN-OS GlobalProtect / Prisma Access | No Sploitus result found in this run | Yes; Palo Alto says exploit maturity `ATTACKED`, limited attempts; CISA KEV | Upgrade to listed PAN-OS/Prisma Access fixed versions; disable or reconfigure authentication override cookies where needed | High |
| Critical | CVE-2026-35616 | CVSS 9.1/9.8 depending source | Fortinet FortiClient EMS 7.4.5-7.4.6 | Exploited in the wild; no public PoC required for risk | Yes; watchTowr observed zero-day exploitation and Arctic Wolf reports EKZ Infostealer deployment | Apply Fortinet hotfix/upgrade to 7.4.7; investigate EMS policy changes, FortiClient-launched PowerShell, and IOC `83.138.53.110` | High |
| Critical | CVE-2026-9082 | Drupal highly critical 23/25; NVD 6.5 | Drupal Core PostgreSQL-backed sites | Multiple Sploitus PoCs/scanners; ExploitDB 52608 | Yes; Drupal advisory updated for in-the-wild attempts; CISA KEV | Upgrade Drupal immediately; prioritize PostgreSQL-backed internet-facing sites; audit DB and role-change logs | High |
| Critical | CVE-2026-41940 | CVSS 9.8 | WebPros cPanel & WHM / WP2 | Sploitus Metasploit and ExploitDB indicators | CISA KEV with known ransomware campaign use | Apply cPanel/WP2 updates, review WHM sessions and webshell/backdoor indicators, rotate credentials after compromise checks | High |
| Critical | CVE-2026-40965 | CVSS 10.0 | Cloud Foundry UAA / cf-deployment using EC JWT keys | No public PoC confirmed; exploit path is direct via public `/token_keys` | No exploitation observed in checked sources | Upgrade UAA to v78.13.0+ or cf-deployment v56.1.0+; rotate EC JWT signing keys and invalidate tokens | High |
| High | CVE-2026-8206 | CVSS 9.8 | Kirki WordPress plugin 6.0.0-6.0.6 | No Sploitus result found; Patchstack advisory | No active exploitation confirmed; expected mass-exploit risk | Update Kirki to 6.0.7+ or disable plugin; inspect password-reset activity | High |
| Critical | CVE-2024-21182 | CISA KEV | Oracle WebLogic Server | Exploit status not independently verified in this run | Yes by KEV listing on 2026-06-01 | Apply Oracle CPU/mitigations by 2026-06-04 KEV due date; restrict T3/IIOP exposure | High |
| High | CVE-2026-47428 / CVE-2026-47429 | GitHub critical advisories | Vitest browser/UI server | GitHub advisory only | No exploitation observed | Upgrade `@vitest/browser` to 4.1.6+/5.0.0-beta.3+ and `vitest` to 4.1.0+ | High |
| High | CVE-2026-25643 | Critical by advisory | Frigate NVR <= 0.16.3 | GitHub PoC repo `DyniePro/CVE-2026-25643` pushed 08:54 UTC; unvalidated | No active exploitation confirmed | Upgrade to Frigate 0.16.4+; ensure internet-exposed instances require auth and avoid privileged containers where possible | Medium |

## Exploits Released

### Reconstructed Sploitus Top 10

These are indexed Sploitus exploit pages observed through search results during the run. This is not confirmed to be Sploitus' official "Exploits of the Week" block.

| Rank | Sploitus entry | CVE(s) | Affected software | Exploit type | Maturity / weaponization potential |
| --- | --- | --- | --- | --- | --- |
| 1 | `13DF22F3-E9C6-58EE-B458-EB585C4D715D` | CVE-2026-20182 | Cisco Catalyst SD-WAN Controller/Manager | Remote auth bypass, SSH key injection / NETCONF access | Weaponization potential high; aligns with Rapid7/Cisco/Talos exploitation narrative |
| 2 | `458CE696-FE39-500F-9131-2E24B1BC2E12` | CVE-2026-9082 | Drupal Core on PostgreSQL | Error-based SQL injection PoC | Public PoC; active exploitation confirmed by vendor update/KEV |
| 3 | `89259320-7066-518A-B075-CE8CD77E926F` | CVE-2026-9082 | Drupal Core on PostgreSQL | JSON:API SQL injection PoC | Public PoC; high scanning/validation potential |
| 4 | `1774D6F8-2B0F-5C66-A7AB-BE7B8E7A0B85` | CVE-2026-9082 | Drupal Core on PostgreSQL | Mass scanner and exploitation tool | High weaponization potential due scanner/extraction features |
| 5 | `3AC8A3A3-D354-5C33-AC06-C1420289BA8D` | CVE-2026-44574, CVE-2026-44577, CVE-2026-44578, CVE-2026-44579, CVE-2026-9082 | Next.js and Drupal lab bundle | Patch-to-exploit PoCs | Multi-CVE lab bundle; validate before use |
| 6 | `MSF:EXPLOIT-MULTI-HTTP-CPANEL_WHM_AUTH_BYPASS_RCE-` | CVE-2026-41940 | cPanel/WHM | Remote auth bypass/RCE module | High maturity if Metasploit module is accurate; ransomware relevance via KEV |
| 7 | `EDB-ID:52574` | CVE-2026-41940 | cPanel/WHM | CRLF injection auth bypass | Public exploit; high operational risk |
| 8 | `44EB5F23-5722-5A31-9188-7E5749ABA7FF` | CVE-2026-41940 | cPanel/WHM | Scanner | Useful for mass exposure discovery; may accelerate targeting |
| 9 | `21CF749E-BFFC-545D-BF25-09BAEAE71E0D` | CVE-2026-31431 | Linux kernel AF_ALG AEAD | Local privilege escalation | Public LPE; requires local access but broad Linux impact |
| 10 | `61F5A984-F6DE-5060-8EDF-0256034BFF43` | CVE-2026-21858 | n8n automation platform | File read, session forgery, RCE chain | Public reconstructed full-chain details; validate against vendor state |

### ExploitDB Additions

Latest ExploitDB CSV entries at collection time:

| EDB ID | Date | Description | CVE(s) | Type/platform | Verified |
| --- | --- | --- | --- | --- | --- |
| 52608 | 2026-06-01 | Drupal Core 10.5.5 - Error-Based SQL Injection | CVE-2026-9082 | webapps/php | 0 |
| 52607 | 2026-06-01 | WordPress OrderConvo 14 - Path Traversal | CVE-2025-10162 | webapps/multiple | 0 |
| 52606 | 2026-05-30 | Notepad++ 8.9.6 - Arbitrary Code Execution | CVE-2026-48778 | remote/windows | 0 |
| 52605 | 2026-05-30 | YAMCS yamcs-core 5.12.7 - No Rate Limiting | CVE-2026-44596 | webapps/multiple | 0 |
| 52604 | 2026-05-30 | YAMCS yamcs-core 5.12.7 - User Enumeration | CVE-2026-44595 | webapps/multiple | 0 |
| 52603 | 2026-05-30 | YAMCS yamcs-core 5.12.7 - LDAP Injection | CVE-2026-42568 | webapps/multiple | 0 |
| 52601 | 2026-05-29 | Microsoft - NTLMv2 Hash Capture | CVE-2026-32202 | remote/windows | 0 |
| 52600 | 2026-05-29 | MikroORM 7.0.13 - SQL Injection | CVE-2026-44680 | webapps/multiple | 0 |
| 52598 | 2026-05-29 | Prodigy Commerce 3.3.0 - Local File Inclusion | CVE-2026-0926 | webapps/multiple | 0 |
| 52597 | 2026-05-29 | Langflow 1.3.0 - Remote Code Execution | CVE-2026-0770 | webapps/multiple | 0 |

### New GitHub PoC / Exploit Indicators

- No repositories matched `CVE-2026 exploit PoC created:>=2026-06-02`.
- One repository matched `CVE-2026 RCE exploit pushed:>=2026-06-02`: `DyniePro/CVE-2026-25643`, a Python repository for Frigate NVR command execution/container escape, created 2026-03-07 and pushed 2026-06-02T08:54:03Z. Treat as unvalidated and potentially unsafe.
- Carry-forward public PoC indicators remain relevant for Linux LPE CVE-2026-43494 (PinTheft) and CVE-2026-31635 (DirtyDecrypt). These were not newly created in this hour.

## Malware Intelligence

- FortiClient EMS to EKZ Infostealer: Arctic Wolf observed CVE-2026-35616 abuse against FortiClient EMS-managed environments. Threat actors used the management plane to push PowerShell/script activity and a payload named `FortiEndpoint_Patch.exe`/`p.exe`, tracked as EKZ Infostealer, targeting browser credentials and cookies. Confidence: High.
- VX-Underground: latest `vxunderground/MalwareSourceCode` commit is `1623926` from 2026-05-30, adding `Python/Stealer.Python.GMBA.Manipulator.7z`. No newer VX GitHub push was observed this run. Confidence: High.
- Mini Shai-Hulud / Miasma supply chain: public reporting describes malicious `@redhat-cloud-services` npm package versions published around 2026-06-01, with credential-harvesting and self-propagation behavior related to prior Mini Shai-Hulud/TanStack/Nx activity. Confidence: Medium until Red Hat/npm primary advisory is reviewed.
- BrainCipher ransomware: public leak-site indexing reports a Squamish.net victim claim posted 2026-06-01T15:20:09Z. Broader "coordinated telecom/energy" claims remain unverified by official sources. Confidence: Low to Medium.
- cPanel/WHM CVE-2026-41940: CISA KEV marks known ransomware campaign use. Organizations should assume exposed unpatched control panels are high-value ransomware initial-access targets. Confidence: High.

## Security Releases and Advisories

- Microsoft: CVE-2026-41089 was patched in the May 2026 Patch Tuesday release. CCB/secondary reporting now says it is exploited in the wild; Microsoft had not been observed updating CISA KEV status for this CVE at collection time. Defender CVE-2026-41091 and CVE-2026-45498 remain CISA KEV with due date 2026-06-03.
- Cisco: Cisco advisory `cisco-sa-sdwan-rpa2-v69WY2SW` provides fixed releases for CVE-2026-20182 and states no workarounds are available. Cisco recommends preserving admin-tech and logs before upgrade.
- Fortinet: FortiClient EMS CVE-2026-35616 is patched via Fortinet hotfix / 7.4.7 path. Active exploitation and EKZ delivery raise priority above standard patch windows.
- Palo Alto Networks: PAN-OS CVE-2026-0257 fixed versions are available across PAN-OS 10.2, 11.1, 11.2, 12.1 and Prisma Access; Palo Alto lists exploit maturity as `ATTACKED`.
- Drupal: SA-CORE-2026-004 fixes CVE-2026-9082 in 10.4.10, 10.5.10, 10.6.9, 11.1.10, 11.2.12, and 11.3.10. Drupal updated the advisory on 2026-05-22 for detected exploit attempts.
- Cloud Foundry: CVE-2026-40965 fixed by `uaa_release` v78.13.0+ and `cf-deployment` v56.1.0+ for deployments using EC JWT signing keys.
- GitLab: 19.0.1, 18.11.4, and 18.10.7 address Duo AI workflow runner identity confusion (CVE-2026-4868) and several authorization/DoS issues.
- GitHub advisories: critical Vitest CVE-2026-47428/CVE-2026-47429 and PraisonAI Platform authorization flaws published 2026-06-01 should be triaged in developer environments and SaaS backends.
- WordPress ecosystem: Kirki 6.0.7 remediates CVE-2026-8206; Patchstack rates it high priority with expected mass-exploitation risk.

## Recommended Actions

1. Emergency patch and hunt: Cisco Catalyst SD-WAN CVE-2026-20182, PAN-OS CVE-2026-0257, FortiClient EMS CVE-2026-35616, Drupal CVE-2026-9082, cPanel/WHM CVE-2026-41940, and Microsoft Netlogon CVE-2026-41089.
2. Treat affected management planes as possible compromise points: preserve logs before patching Cisco SD-WAN, review FortiClient EMS policy/script changes, inspect WHM sessions and webshell indicators, and rotate credentials after containment.
3. Patch identity and developer infrastructure: Cloud Foundry UAA CVE-2026-40965, Microsoft Defender KEV CVE-2026-41091/CVE-2026-45498, GitLab 19.0.1/18.11.4/18.10.7, Vitest, PraisonAI, and GitHub Actions workflows affected by Mini Shai-Hulud-style patterns.
4. Inventory internet-facing Drupal PostgreSQL sites, GlobalProtect portals/gateways, Cisco SD-WAN controllers, FortiClient EMS servers, cPanel/WHM instances, and AD domain controllers; prioritize external exposure and privileged-management roles.
5. Monitor public PoC repositories cautiously. Do not execute untrusted PoC code outside isolated malware-analysis sandboxes; several CVE PoC repositories historically contain trojanized payloads.
6. Supply-chain response: identify installs of affected TanStack/Nx/Red Hat npm package versions, remove persistence before revoking tokens where Mini Shai-Hulud guidance applies, then rotate GitHub/npm/cloud/SSH credentials and audit CI/CD workflows.

## Unified Vulnerability Records

```json
[
  {
    "cve": "CVE-2026-20182",
    "cvss": "10.0",
    "vendor": "Cisco",
    "product": "Catalyst SD-WAN Controller and Manager",
    "affected_versions": "Multiple Catalyst SD-WAN release trains before Cisco fixed releases including 20.9.9.1, 20.12.5.4/20.12.6.2/20.12.7.1, 20.15.4.4/20.15.5.2, 20.18.2.2, and 26.1.1.1",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://sploitus.com/exploit?id=13DF22F3-E9C6-58EE-B458-EB585C4D715D",
      "https://www.rapid7.com/blog/post/ve-cve-2026-20182-critical-authentication-bypass-cisco-catalyst-sd-wan-controller-fixed/"
    ],
    "patch_available": true,
    "sources": [
      "https://sec.cloudapps.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-sdwan-rpa2-v69WY2SW",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://blog.talosintelligence.com/sd-wan-ongoing-exploitation/"
    ]
  },
  {
    "cve": "CVE-2026-41089",
    "cvss": "9.8",
    "vendor": "Microsoft",
    "product": "Windows Netlogon / domain controllers",
    "affected_versions": "Windows Server 2012 through 2025 when acting as domain controllers per public reporting",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/0xABCD01/CVE-2026-41089"
    ],
    "patch_available": true,
    "sources": [
      "https://msrc.microsoft.com/update-guide/vulnerability/CVE-2026-41089",
      "https://www.bleepingcomputer.com/news/microsoft/critical-windows-netlogon-remote-code-execution-flaw-now-exploited-in-attacks/",
      "https://www.securityweek.com/critical-windows-netlogon-vulnerability-in-attackers-crosshairs/"
    ]
  },
  {
    "cve": "CVE-2026-0257",
    "cvss": "7.8",
    "vendor": "Palo Alto Networks",
    "product": "PAN-OS GlobalProtect and Prisma Access",
    "affected_versions": "PAN-OS 10.2, 11.1, 11.2, 12.1 and Prisma Access versions below advisory fixed releases when GlobalProtect auth override cookie conditions are met",
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
    "cve": "CVE-2026-35616",
    "cvss": "9.1",
    "vendor": "Fortinet",
    "product": "FortiClient EMS",
    "affected_versions": "FortiClient EMS 7.4.5 and 7.4.6 per public reporting",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://watchtowr.com/resources/fortinet-forticlient-ems-zero-day-cve-2026-35616-active-exploitation-underway/",
      "https://arcticwolf.com/resources/blog/forticlient-ems-exploited-via-cve-2026-35616-to-deliver-ekz-infostealer-disguised-as-a-fortinet-patch/",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"
    ]
  },
  {
    "cve": "CVE-2026-9082",
    "cvss": "6.5 NVD / Drupal 23 of 25",
    "vendor": "Drupal",
    "product": "Drupal Core",
    "affected_versions": ">=8.9.0 <10.4.10, >=10.5.0 <10.5.10, >=10.6.0 <10.6.9, >=11.0.0 <11.1.10, >=11.2.0 <11.2.12, >=11.3.0 <11.3.10 when using PostgreSQL",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://sploitus.com/exploit?id=458CE696-FE39-500F-9131-2E24B1BC2E12",
      "https://sploitus.com/exploit?id=1774D6F8-2B0F-5C66-A7AB-BE7B8E7A0B85",
      "https://www.exploit-db.com/exploits/52608"
    ],
    "patch_available": true,
    "sources": [
      "https://www.drupal.org/sa-core-2026-004",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://www.imperva.com/blog/imperva-customers-protected-against-cve-2026-9082-in-drupal-core/"
    ]
  },
  {
    "cve": "CVE-2026-41940",
    "cvss": "9.8",
    "vendor": "WebPros",
    "product": "cPanel & WHM and WP2",
    "affected_versions": "See cPanel/WP2 vendor release notes for affected builds",
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
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"
    ]
  },
  {
    "cve": "CVE-2026-40965",
    "cvss": "10.0",
    "vendor": "Cloud Foundry",
    "product": "UAA / cf-deployment",
    "affected_versions": "uaa_release v76.12.0 through v78.12.0; CF Deployment v30.0.0 through v56.0.0 when using EC keys for JWT signing",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://www.cloudfoundry.org/blog/cve-2026-40965-uaa-ec-private-key-disclosure/",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-40965"
    ]
  },
  {
    "cve": "CVE-2026-8206",
    "cvss": "9.8",
    "vendor": "Kirki",
    "product": "Kirki WordPress plugin",
    "affected_versions": "6.0.0 through 6.0.6",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://patchstack.com/database/wordpress/plugin/kirki/vulnerability/wordpress-kirki-plugin-6-0-0-6-0-6-unauthenticated-privilege-escalation-via-handle-forgot-password-vulnerability",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-8206"
    ]
  },
  {
    "cve": "CVE-2026-25643",
    "cvss": "Critical",
    "vendor": "Frigate",
    "product": "Frigate NVR",
    "affected_versions": "<=0.16.3",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/DyniePro/CVE-2026-25643"
    ],
    "patch_available": true,
    "sources": [
      "https://github.com/blakeblackshear/frigate/security/advisories/GHSA-4c97-5jmr-8f6x",
      "https://github.com/blakeblackshear/frigate/releases/tag/v0.16.4",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-25643"
    ]
  },
  {
    "cve": "CVE-2026-48027",
    "cvss": "KEV",
    "vendor": "Nx",
    "product": "Nx Console",
    "affected_versions": "Malicious Nx Console VS Code extension version 18.95.0 per CISA alert",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://www.cisa.gov/news-events/alerts/2026/05/28/supply-chain-compromises-impact-nx-console-and-github-repositories",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"
    ]
  },
  {
    "cve": "CVE-2026-45321",
    "cvss": "KEV",
    "vendor": "TanStack",
    "product": "TanStack npm packages",
    "affected_versions": "Malicious package versions from May 2026 supply-chain compromise; see GitHub advisory GHSA-g7cv-rxg3-hmpx",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://github.com/TanStack/router/security/advisories/GHSA-g7cv-rxg3-hmpx",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"
    ]
  },
  {
    "cve": "CVE-2024-21182",
    "cvss": "KEV",
    "vendor": "Oracle",
    "product": "WebLogic Server",
    "affected_versions": "See Oracle July 2024 CPU / NVD record",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://www.oracle.com/security-alerts/cpujul2024.html",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://nvd.nist.gov/vuln/detail/CVE-2024-21182"
    ]
  }
]
```

## Review Notes

- Highest remediation priority is driven by active exploitation and management-plane blast radius rather than only CVSS.
- GitHub and Sploitus exploit references are indicators requiring sandboxed validation; no repository should be executed on production or analyst workstations.
- Netlogon active exploitation is treated as medium-confidence because CCB/secondary reporting is strong, but CISA KEV did not list CVE-2026-41089 at collection time and Microsoft status should be rechecked.
