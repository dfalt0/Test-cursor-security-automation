# Security Intelligence Report - 2026-06-02 02:02 UTC

Repository: `dfalt0/Test-cursor-security-automation`  
Branch: `cursor/security-intelligence-agent-a784`  
Report window: primary hourly delta `2026-06-02T00:00:00Z` to `2026-06-02T02:10:00Z`; 24-hour enrichment `2026-06-01T02:00:00Z` to `2026-06-02T02:10:00Z`

## Executive Summary

- NVD hourly delta: 6 newly published CVEs, all medium or low severity (4 medium, 2 low). No new critical CVEs appeared in the narrow hourly NVD window.
- NVD 24-hour enrichment: 377 CVEs, including 16 critical, 121 high, 143 medium, 35 low, and 62 without NVD severity at query time.
- Critical findings requiring enterprise review:
  - CVE-2026-40965 - Cloud Foundry UAA EC private key disclosure through `/token_keys`, CVSS 10.0. Patch available.
  - CVE-2026-20182 - Cisco Catalyst SD-WAN Controller/Manager authentication bypass, CVSS 10.0, CISA KEV, Cisco-confirmed limited exploitation. Patch available.
  - CVE-2026-0257 - Palo Alto Networks PAN-OS GlobalProtect authentication bypass, vendor exploit maturity `ATTACKED`, CISA KEV. Patch and mitigations available.
  - CVE-2024-21182 - Oracle WebLogic Server, newest CISA KEV addition on 2026-06-01, due 2026-06-04.
  - CVE-2026-9311 / CVE-2026-9319 / CVE-2026-8644 - IBM WebSphere Application Server critical RCE/spoofing issues surfaced in NVD/GitHub Advisory data; IBM pages timed out during direct fetch, so confidence is medium until vendor pages are rechecked.
- Active exploitation and campaign intelligence:
  - CISA KEV catalog version `2026.06.01` lists 1608 entries. Recent additions include Oracle WebLogic CVE-2024-21182, PAN-OS CVE-2026-0257, Nx Console CVE-2026-48027, TanStack CVE-2026-45321, Daemon Tools Lite CVE-2026-8398, LiteSpeed cPanel Plugin CVE-2026-48172, and Drupal Core CVE-2026-9082.
  - Cisco and Palo Alto both explicitly report limited exploitation/attack attempts for their current network-infrastructure advisories.
  - SANS ISC continues to track the TeamPCP supply-chain campaign affecting TanStack/Nx and downstream developer ecosystems.
  - VX-Underground GitHub activity still shows the latest `MalwareSourceCode` commit as `Python/Stealer.Python.GMBA.Manipulator.7z` added on 2026-05-30.

Confidence: High for NVD, MITRE CVE, CISA KEV, Cloud Foundry, Cisco, Palo Alto, Android, Fortinet, GitHub Advisory, and VX-Underground GitHub observations. Medium for IBM WebSphere due to direct IBM page fetch timeouts but corroboration in NVD/GitHub Advisory data. Low for unvalidated GitHub PoC repositories and Sploitus weekly ranking reconstruction.

## Source Coverage and Limitations

Checked sources included NVD, MITRE CVE Program API, CISA KEV JSON, GitHub Advisory Database API, GitHub repository search, Sploitus homepage/search indicators, ExploitDB search, Packet Storm search, ProjectDiscovery search, VulnCheck-indexed search results, AttackerKB search, VX-Underground GitHub organization, SANS ISC, The DFIR Report, Shadowserver, GreyNoise, AlienVault OTX search, Microsoft MSRC search, Cisco PSIRT, Fortinet PSIRT, Broadcom/VMware search, GitLab search, GitHub Blog/Changelog search, Wazuh CTI search, and OpenCVE search.

Limitations:

- Sploitus homepage fetch exposed only the static search shell and did not expose an official "Exploits of the Week" block. The Sploitus Top 10 section below is therefore a reconstructed exploit-watchlist from indexed exploit indicators, not a first-party Sploitus ranking.
- MalwareBazaar API returned HTTP 401 Unauthorized from this environment.
- IBM support pages for WebSphere advisories timed out during direct fetch. NVD and GitHub Advisory records were used for interim triage.
- Packet Storm search did not reveal current CVE-2026 additions; results were mostly historical entries.

## Top Vulnerabilities

| Priority | CVE | Severity | Affected software | Exploit availability | Active exploitation | Recommended action | Confidence |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Critical | CVE-2026-20182 | CVSS 10.0 critical | Cisco Catalyst SD-WAN Controller and Manager | No public working PoC confirmed in this run | Yes - CISA KEV and Cisco limited exploitation | Collect `admin-tech`, retain logs, check `auth.log` and control-connection IOCs, then upgrade to fixed SD-WAN releases | High |
| Critical | CVE-2026-0257 | CVSS-BT 7.8 high; KEV/attacked | PAN-OS GlobalProtect portal/gateway and Prisma Access configurations using authentication override cookies | Public reporting and exploit indicators exist; do not assume any single repo is safe | Yes - Palo Alto says limited exploit attempts; CISA KEV | Upgrade to fixed PAN-OS/Prisma Access releases; disable Authentication Override or use dedicated cookie certificate as interim mitigation | High |
| Critical | CVE-2024-21182 | KEV-listed | Oracle WebLogic Server | Historical exploit interest likely; no new PoC validated in this run | Yes - KEV-listed | Apply Oracle mitigation/update guidance by CISA due date 2026-06-04 | High |
| Critical | CVE-2026-40965 | CVSS 10.0 critical | Cloud Foundry UAA `v76.12.0` through `v78.12.0`; CF Deployment `v30.0.0` through `v56.0.0`, EC JWT signing only | No public exploit validated in this run; exploitation is low-complexity key disclosure via public endpoint | Not observed in sources checked | Upgrade UAA to `v78.13.0+` or CF Deployment to `v56.1.0+`; rotate any exposed EC JWT signing keys and tokens | High |
| Critical | CVE-2026-9311 / CVE-2026-9319 | CVSS 9.0 critical | IBM WebSphere Application Server 8.5/9.0 | No public PoC validated in this run | Not observed in sources checked | Recheck IBM support pages and patch WebSphere per IBM advisory nodes `7274733` and `7274738` | Medium |
| Critical | CVE-2026-8644 | CVSS 9.1 critical | IBM WebSphere Application Server 8.5/9.0 | No public PoC validated in this run | Not observed in sources checked | Patch per IBM node `7274740`; prioritize internet-facing or federation-sensitive deployments | Medium |
| High | CVE-2026-45505 / CVE-2026-49157 | CVSS 8.8 high | Apache ActiveMQ | Apache/NVD references indicate code injection/default permission impacts; public defensive advisories exist | CISA/third-party search mentions active/exploited ActiveMQ history, but this run did not validate KEV for these IDs | Upgrade ActiveMQ Classic/Broker to fixed versions and restrict broker/admin surfaces | Medium |
| High | CVE-2026-9614 | CVSS 8.8 high | Ivanti Neurons for ITSM cloud/on-prem | No public PoC validated in this run | Not observed in sources checked | Patch per Ivanti advisory; review remote authenticated admin access paths | Medium |
| High | CVE-2026-10302 | CVSS 6.3 medium; exploit published | itsourcecode Fees Management System 1.0 `/manage_fee.php` SQL injection | Yes - GitHub issue and VulDB/MITRE mark exploit/PoC published | Not observed in sources checked | If deployed, remove from internet exposure, patch or replace, and inspect logs for SQL injection attempts | High |
| High | Android June 2026 bulletin | Critical/high grouped | Android Framework/System and Qualcomm closed-source components | No public exploit validated in this run | Not observed in sources checked | Require 2026-06-05 patch level or OEM equivalent across managed Android fleet | High |

## Hourly NVD Delta

| CVE | Severity | CVSS | Product | Exploit/Patch notes | Sources |
| --- | --- | --- | --- | --- | --- |
| CVE-2026-10302 | Medium | 6.3 | itsourcecode Fees Management System 1.0 | SQL injection in `/manage_fee.php`; MITRE/VulDB state exploit has been published | NVD, MITRE, VulDB, GitHub issue |
| CVE-2026-10301 | Medium | 4.3 | itsourcecode Fees Management System 1.0 | XSS in `index.php`; public exploit indicator in NVD/GitHub issue | NVD, GitHub Advisory |
| CVE-2026-9048 | Medium | 4.3 | Slider Revolution WordPress plugin 7.0.0-7.0.14 | Contributor-level sensitive information exposure; vendor/Wordfence references | NVD, GitHub Advisory, Wordfence |
| CVE-2026-9050 | Medium | 4.3 | Slider Revolution WordPress plugin 6.0.0-6.7.55 and 7.0.0-7.0.14 | Contributor-level unauthorized modification of data | NVD, GitHub Advisory, Wordfence |
| CVE-2026-10528 | Low | 3.3 | Orthanc DICOM Server up to 1.12.11 | Local DCMTK parser stack buffer overflow; fix reference present | NVD, Orthanc bug/commit |
| CVE-2026-10514 | Low | 2.4 | 1Panel-dev CordysCRM up to 1.6.2 | XSS; fixed in v1.7.0 | NVD, GitHub advisory/release |

## Exploits Released and Public PoC Indicators

### Sploitus Top 10 Reconstruction

Sploitus did not expose an official weekly list via static fetch. The following entries are ranked by observed exploit-source freshness, enterprise relevance, and weaponization potential from ExploitDB, GitHub, ProjectDiscovery, AttackerKB, and NVD/MITRE references.

| Rank | Indicator | Affected software | Exploit type | Maturity | Public PoC | Weaponization potential | Confidence |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | CVE-2026-20182 | Cisco Catalyst SD-WAN Controller/Manager | Auth bypass/admin access | Vendor-confirmed exploitation; no public PoC validated | Not validated | Very high for exposed SD-WAN control planes | High |
| 2 | CVE-2026-0257 | Palo Alto PAN-OS GlobalProtect | Auth bypass/VPN access | Vendor `ATTACKED`; KEV | Public indicators, no repo validated | Very high for internet-facing GlobalProtect | High |
| 3 | CVE-2026-41940 | cPanel & WHM | Pre-auth auth bypass | AttackerKB/ProjectDiscovery/watchTowr technical analysis and template | Yes | Very high for hosting providers | High |
| 4 | CVE-2026-1731 | BeyondTrust RS/PRA | Pre-auth command injection/RCE | AttackerKB and ProjectDiscovery detection template | Yes/derived | Very high for remote-support appliances | High |
| 5 | CVE-2026-43284 / CVE-2026-43500 / CVE-2026-46300 | Linux kernel chain | Local privilege escalation | ExploitDB 52591 with claimed exploit chain | Yes | High post-compromise escalation risk | Medium |
| 6 | CVE-2026-32202 | Microsoft Windows Shell/File Explorer | NTLMv2 hash capture | ExploitDB 52601 | Yes | Medium-high for phishing/SMB relay chains | Medium |
| 7 | CVE-2026-32746 | GNU inetutils telnetd 2.7 | Remote buffer overflow proof | ExploitDB 52556 states PoC verifies overflow, not RCE | Yes | Medium; legacy telnetd exposure | Medium |
| 8 | CVE-2026-2441 | Google Chrome | Use-after-free | ExploitDB 52542 claims active exploitation | Yes | High if claim is validated; browser exploit safety unknown | Low-Medium |
| 9 | CVE-2026-10302 | Fees Management System | SQL injection | MITRE/NVD/VulDB mark exploit published | Yes | Medium for exposed niche web apps | High |
| 10 | CVE-2026-41089 | Netlogon CLDAP stack buffer overflow | GitHub repo created 2026-06-01 with 35 stars | Unvalidated GitHub PoC | Yes, unvalidated | Potentially high, but repo safety/functionality unknown | Low |

### ExploitDB Additions Observed

- ExploitDB 52591 - Linux Kernel local privilege escalation chain for CVE-2026-43284 / CVE-2026-43500 / CVE-2026-46300.
- ExploitDB 52601 - Microsoft NTLMv2 hash capture for CVE-2026-32202.
- ExploitDB 52556 - telnetd 2.7 buffer overflow PoC for CVE-2026-32746; source text says it does not achieve code execution.
- ExploitDB 52542 - Google Chrome CSSFontFeatureValuesMap use-after-free for CVE-2026-2441; active-exploitation claim requires additional vendor/telemetry validation.
- ExploitDB 52546 - Windows HTTP.sys/Windows 11 24H2 local exploit/DoS indicator for CVE-2026-21250.

### New GitHub PoC and Offensive Repositories

GitHub repository search (`created:>=2026-06-01`) returned:

- `0xABCD01/CVE-2026-41089` - CVE-labeled PoC for Netlogon CLDAP stack buffer overflow; created 2026-06-01, updated 2026-06-02, 35 stars. Treat as unvalidated and potentially malicious until reviewed in a sandbox.
- `Jeydori/Danphe3.2-RCE-via-Dynamic-Report-module-CVE-PoC` - RCE PoC-labeled repository, created 2026-06-01, 0 stars. Unvalidated.
- `MrXploit267/MLflow-RCE` - MLflow RCE PoC-labeled repository, created 2026-06-01, 0 stars. Unvalidated.
- `Sylpbqraz/SharpAllowedToAct-Modify` - post-exploitation/RBCD tooling, not a CVE PoC, created 2026-06-01. Offensive tooling indicator.

Public PoC repositories are indicators only; do not execute without isolation, static review, and outbound-network controls.

## Malware Intelligence

| Finding | Details | Recommended action | Confidence |
| --- | --- | --- | --- |
| VX-Underground malware source archive update | `vxunderground/MalwareSourceCode` latest commit `1623926c2424` on 2026-05-30 added `Python/Stealer.Python.GMBA.Manipulator.7z`. Repository updated metadata on 2026-06-02. | Track for detections if your malware lab consumes VX archives; avoid direct handling outside malware-safe workflows | High |
| TeamPCP supply-chain campaign | SANS ISC reports TanStack/Nx supply-chain activity, credential theft, developer secret harvesting, and downstream impact. CISA KEV lists Nx Console CVE-2026-48027 and TanStack CVE-2026-45321 with known ransomware campaign use. | Audit developer endpoints, VS Code extensions, npm/PyPI package provenance, CI/CD secrets, OIDC trust policies, and token rotation | High |
| Fake Claude pages distributing ACR Stealer | SANS ISC reported fake Claude download pages delivering Windows malware consistent with ACR Stealer, including C2/domain indicators. | Hunt for fake AI-tool download lures, PowerShell script execution, unusual archive downloads, and listed C2 domains | High |
| The Gentleman ransomware via EtherRAT/TukTuk | The DFIR Report details malicious MSI/Sysinternals lures, EtherRAT, TukTuk, Rclone exfiltration, Defender tampering, GPO-based deployment, and The Gentleman ransomware. | Monitor for suspicious MSI installers, GoTo Resolve/RMM abuse, Rclone staging, GPO changes, shadow copy deletion, and broad scheduled task deployment | High |
| MalwareBazaar | API returned HTTP 401 Unauthorized from this environment. | Re-run with an authenticated abuse.ch API key if sample-level malware feed coverage is required | High for access limitation |

## Security Releases and Vendor Advisories

- Microsoft: MSRC search returned individual CVE pages but no single new June 2 emergency release validated in this run. Existing KEV due dates remain relevant for Microsoft Defender CVE-2026-41091 and CVE-2026-45498 from CISA's 2026-05-20 additions.
- Cisco: CVE-2026-20182 is critical, KEV-listed, and Cisco reports limited exploitation. No workaround; upgrade to fixed SD-WAN releases and preserve logs before upgrade.
- Fortinet: FortiAuthenticator improper access control advisory FG-IR-26-128 and FortiAP command injection FG-IR-26-131 remain the latest notable Fortinet PSIRT items found (published 2026-05-12). Patch FortiAuthenticator to 8.0.3/6.6.9/6.5.7+ and FortiAP/FortiAP-U/FortiAP-W2 to fixed trains.
- Palo Alto Networks: CVE-2026-0257 updated 2026-05-29 with exploit status; urgency highest. Patch PAN-OS/Prisma Access or disable/auth-harden GlobalProtect authentication override cookies.
- Cloud Foundry: CVE-2026-40965 patch available in UAA `v78.13.0+` and CF Deployment `v56.1.0+`; rotate potentially exposed EC signing keys.
- Android/Qualcomm: Android June 2026 bulletin published 2026-06-01; security patch level 2026-06-05 addresses all listed issues, including critical Framework/System and Qualcomm closed-source component vulnerabilities.
- GitHub: Advisory API returned new June 2 advisories for Slider Revolution, Fees Management System, Orthanc, CordysCRM, and Qualcomm/Android-related CVEs. GitHub product changelog search found no new June 2 GitHub platform security incident.
- GitLab: Search returned no June 2026 GitLab security release result in this run.
- Broadcom/VMware: Broadcom security advisory portal search was access-limited; Cloud Foundry CVE records are assigned by VMware and accessible via Cloud Foundry/MITRE/NVD.

## Recommended Actions

1. Patch and investigate Cisco Catalyst SD-WAN CVE-2026-20182 immediately. Preserve `admin-tech` and logs before upgrade; validate control-connection and `auth.log` indicators.
2. Patch Palo Alto PAN-OS/Prisma Access CVE-2026-0257 immediately. If upgrade cannot be completed, disable Authentication Override or use a dedicated certificate for override cookies.
3. Apply Oracle WebLogic CVE-2024-21182 mitigations/patches before the CISA due date of 2026-06-04.
4. Patch Cloud Foundry UAA CVE-2026-40965 and rotate EC JWT signing keys/tokens where EC signing was in use.
5. Recheck and patch IBM WebSphere critical advisories CVE-2026-9311, CVE-2026-9319, and CVE-2026-8644 as soon as IBM support pages are reachable.
6. Apply Android/OEM June 2026 patch levels to managed Android devices, especially devices with Qualcomm chipsets.
7. Audit developer workstations and CI/CD for TanStack/Nx/TeamPCP compromise indicators, including VS Code extension history, package-lock changes, secrets exposure, and OIDC trust assumptions.
8. Treat new GitHub PoC repositories as hostile until reviewed. Block direct execution on analyst workstations.
9. Patch niche web applications with public exploit references, including Fees Management System CVE-2026-10302/CVE-2026-10301 and Slider Revolution CVE-2026-9048/CVE-2026-9050, if present in inventory.
10. Continue monitoring Sploitus dynamically in a browser-capable collection path because static fetches do not expose the weekly/top exploit data.

## Unified Vulnerability Records

```json
[
  {
    "cve": "CVE-2026-20182",
    "cvss": "10.0",
    "vendor": "Cisco",
    "product": "Catalyst SD-WAN Controller and Manager",
    "affected_versions": "Multiple SD-WAN releases; fixed releases include 20.9.9.1, 20.12.7.1, 20.15.5.2, 20.18.2.2, 26.1.1.1 per Cisco advisory",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://sec.cloudapps.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-sdwan-rpa2-v69WY2SW",
      "https://cveawg.mitre.org/api/cve/CVE-2026-20182",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"
    ]
  },
  {
    "cve": "CVE-2026-0257",
    "cvss": "7.8 CVSS-BT/CVSS v4 high",
    "vendor": "Palo Alto Networks",
    "product": "PAN-OS GlobalProtect and Prisma Access",
    "affected_versions": "PAN-OS 12.1/11.2/11.1/10.2 before listed hotfixes; Prisma Access 10.2.0 before 10.2.10-h36 and 11.2.0 before 11.2.7-h13",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://security.paloaltonetworks.com/CVE-2026-0257",
      "https://cveawg.mitre.org/api/cve/CVE-2026-0257",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"
    ]
  },
  {
    "cve": "CVE-2024-21182",
    "cvss": "Not re-scored in this report",
    "vendor": "Oracle",
    "product": "WebLogic Server",
    "affected_versions": "See Oracle July 2024 CPU",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://www.oracle.com/security-alerts/cpujul2024.html",
      "https://nvd.nist.gov/vuln/detail/CVE-2024-21182"
    ]
  },
  {
    "cve": "CVE-2026-40965",
    "cvss": "10.0",
    "vendor": "Cloud Foundry Foundation",
    "product": "UAA / CF Deployment",
    "affected_versions": "uaa_release v76.12.0 through v78.12.0; CF Deployment v30.0.0 through v56.0.0; EC JWT signing configurations",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://www.cloudfoundry.org/blog/cve-2026-40965-uaa-ec-private-key-disclosure/",
      "https://cveawg.mitre.org/api/cve/CVE-2026-40965",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-40965",
      "https://github.com/advisories/GHSA-qc5f-2h9q-7m2g"
    ]
  },
  {
    "cve": "CVE-2026-10302",
    "cvss": "6.3",
    "vendor": "itsourcecode",
    "product": "Fees Management System",
    "affected_versions": "1.0",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/ltranquility/vuln_submit/issues/10"
    ],
    "patch_available": false,
    "sources": [
      "https://cveawg.mitre.org/api/cve/CVE-2026-10302",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-10302",
      "https://vuldb.com/cve/CVE-2026-10302"
    ]
  },
  {
    "cve": "CVE-2026-9311",
    "cvss": "9.0",
    "vendor": "IBM",
    "product": "WebSphere Application Server",
    "affected_versions": "8.5 and 9.0 per NVD/GitHub Advisory",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://www.ibm.com/support/pages/node/7274733",
      "https://github.com/advisories/GHSA-gfh5-5q87-hr66",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-9311"
    ]
  }
]
```
