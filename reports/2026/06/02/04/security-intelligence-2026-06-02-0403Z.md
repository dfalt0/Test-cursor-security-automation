# Security Intelligence Hourly Report - 2026-06-02 04:03 UTC

Repository: `dfalt0/Test-cursor-security-automation`  
Branch: `cursor/security-intelligence-agent-7fb3`  
Automation trigger: hourly cron, 2026-06-02 04:02:48 UTC  
Analyst: Cursor security intelligence agent

## Executive Summary

- NVD CVEs published from 2026-06-02 00:00-04:30 UTC: 20 total; 0 Critical, 0 High, 6 Medium, 13 Low, 1 Unknown.
- Rolling 24-hour NVD enrichment window, 2026-06-01 04:30-2026-06-02 04:30 UTC: 365 total; 19 Critical, 102 High, 127 Medium, 74 Low, 43 Unknown.
- Critical findings requiring immediate review:
  - CVE-2026-0257, Palo Alto Networks PAN-OS/Prisma Access GlobalProtect authentication bypass: vendor marks exploit maturity as ATTACKED, CISA KEV-listed, Rapid7 observed successful exploitation and published a validation PoC.
  - CVE-2026-20182, Cisco Catalyst SD-WAN Controller/Manager authentication bypass: CISA KEV-listed; Cisco reports limited exploitation and no workaround.
  - CVE-2024-21182, Oracle WebLogic Server: newly added to CISA KEV on 2026-06-01 with a 2026-06-04 due date.
  - CVE-2026-20223, Cisco Secure Workload unauthorized API access: CVSS 10.0, no workaround, Sploitus-indexed PoC indicator.
  - CVE-2026-40965, Cloud Foundry UAA EC private key disclosure: CVSS 10.0, public `/token_keys` exposure for EC signing keys.
  - CVE-2026-45131 and CVE-2026-45132, CloudPirates Helm Charts GitHub Actions supply-chain flaws: CVSS 10.0, fork PR code could exfiltrate secrets/PAT/SSH signing material before patch commit `fcf9302`.
- Active exploitation and malware:
  - Confirmed active exploitation: PAN-OS CVE-2026-0257 and Cisco SD-WAN CVE-2026-20182.
  - KEV exploitation signal: Oracle WebLogic CVE-2024-21182, Drupal Core CVE-2026-9082, Nx Console CVE-2026-48027, TanStack CVE-2026-45321, and others remain priority carryovers.
  - Malware campaign signal: FortiClient EMS CVE-2026-35616 exploitation has been reported to deploy EKZ Infostealer via trusted EMS workflows; treat exposed EMS servers as potential incident-response triggers.
- Important vendor/security releases:
  - Zyxel published 2026-06-02 patches for CVE-2026-3870 and CVE-2026-3871 UPnP buffer overflows affecting specific CPE firmware.
  - GitLab 19.0.1, 18.11.4, and 18.10.7 security releases remain relevant for CVE-2026-4868 and related authorization/DoS issues.
  - ProjectDiscovery nuclei-templates v10.4.4 added checks for multiple critical/KEV issues including Cisco SD-WAN CVE-2026-20182 and Drupal CVE-2026-9082.

## Collection Notes and Source Reliability

- Sploitus homepage check returned only the site search shell and did not expose a literal "Exploits of the Week" block. The Sploitus Top 10 below is reconstructed from indexed Sploitus exploit pages found during this run and should be treated as exploit-intelligence indicators, not proof of functional exploit code.
- Exploit-DB RSS returned HTTP 500 during this run. Exploit-DB coverage below is limited to NVD/Sploitus references that explicitly mention Exploit-DB or public exploit material.
- GitHub PoC repositories were reviewed by metadata and README only. No code was executed.
- VX-Underground website and GitHub organization were checked. The GitHub `vxunderground/MalwareSourceCode` repository remains updated recently and includes `Python/Stealer.Python.GMBA.Manipulator.7z`; no new June 2 ransomware source-code leak was confirmed in this run.
- A web search found secondary reporting claiming CVE-2026-41089 Netlogon active exploitation by Belgium CCB, but a targeted search of `cert.be` did not corroborate that claim. This report treats CVE-2026-41089 as Critical with public PoC indicators, but not as confirmed active exploitation.

## Top Vulnerabilities

| Priority | CVE | Severity | Affected software | Exploit availability | Active exploitation | Recommended action | Confidence |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | CVE-2026-0257 | High CVSS 7.8, operationally Critical | Palo Alto Networks PAN-OS and Prisma Access GlobalProtect portals/gateways with authentication override cookie exposure | Public validation PoC from Rapid7; GitHub PoC-style repo `bolubey/CVE-2026-0257` | Yes; Palo Alto says limited exploit attempts, Rapid7 observed exploitation, CISA KEV added 2026-05-29 | Upgrade to fixed PAN-OS/Prisma Access releases; disable Authentication Override or use a dedicated cookie certificate; hunt for Rapid7 IOCs | High |
| 2 | CVE-2026-20182 | Critical | Cisco Catalyst SD-WAN Controller/Manager | ProjectDiscovery templates; public exploit indicators; vendor advisory | Yes; Cisco reports limited exploitation; CISA KEV added 2026-05-14 | Upgrade fixed releases; collect admin-tech and engage Cisco TAC if exposed/compromise suspected | High |
| 3 | CVE-2024-21182 | Critical/KEV | Oracle WebLogic Server 12.2.1.4.0, 14.1.1.0.0 | Exploit details not validated in this run | KEV-listed 2026-06-01 | Apply Oracle CPU guidance immediately; restrict T3/IIOP exposure; due date 2026-06-04 | High |
| 4 | CVE-2026-20223 | CVSS 10.0 Critical | Cisco Secure Workload Cluster Software 3.9 and earlier, 3.10, 4.0 | Sploitus-indexed Python/Bash PoC indicator | Not confirmed | Upgrade 3.10 to 3.10.8.3 or 4.0 to 4.0.3.17; SaaS fixed by Cisco | High |
| 5 | CVE-2026-40965 | CVSS 10.0 Critical | Cloud Foundry UAA v76.12.0 through v78.12.0; cf-deployment v30.0.0 through v56.0.0 using EC JWT keys | No exploit repo validated; public unauthenticated endpoint exposure | Not confirmed | Upgrade uaa_release >= v78.13.0 or cf-deployment >= v56.1.0; rotate exposed EC signing keys/tokens | High |
| 6 | CVE-2026-7858 | CVSS 9.8 Critical | Dassault Systemes Teamwork Cloud and Magic Collaboration Studio 2022x-2026x | No public exploit validated | Not confirmed | Obtain remediation from 3DS advisory portal and patch internet/extranet exposed collaboration servers | High |
| 7 | CVE-2026-49121 | CVSS 9.2 Critical | AI Tensor Engine for ROCm (AITER) <= 0.1.14 | VulnCheck advisory with technical detail; GitHub issue/PR references | Not confirmed | Patch when fixed release is available; block unauthenticated cluster access to ZMQ XPUB/subscription endpoints | High |
| 8 | CVE-2026-44211 | CVSS 9.6 Critical | Cline Kanban server versions 2.13.0 and prior | GitHub advisory includes PoC JavaScript | Not confirmed | Disable exposed Kanban server where possible; watch for vendor patch; restrict localhost WebSocket access | High |
| 9 | CVE-2026-45131 / CVE-2026-45132 | CVSS 10.0 Critical | CloudPirates Open Source Helm Charts workflows before commit `fcf9302` | GitHub advisory gives exploit path | No exploited versions reported by advisory | Review fork PR workflow patterns; rotate exposed registry/PAT/SSH credentials if vulnerable workflow ran | High |
| 10 | CVE-2026-9311 / CVE-2026-9319 / CVE-2026-8644 | Critical | IBM WebSphere Application Server 8.5 and 9.0 | No public exploit validated | Not confirmed | Apply IBM fixes; prioritize public WebSphere and WS-Security/JAX-WS endpoints | Medium |

### New June 2 CVEs of Note

| CVE | Severity | Affected software | Notes | Confidence |
| --- | --- | --- | --- | --- |
| CVE-2026-3870 | Medium, 6.5 | Zyxel VMG4005-B50B firmware <= 5.13(ABRL.5.4)C0 | Adjacent-network UPnP AddPortMapping buffer overflow DoS; patch 5.13(ABRL.5.5)C0 | High |
| CVE-2026-3871 | Medium, 6.5 | Zyxel NR7101, Nebula LTE3301-PLUS, Nebula NR7101, VMG4005-B50B | Adjacent-network UPnP DeletePortMapping buffer overflow DoS; firmware patches available | High |
| CVE-2026-9048 / CVE-2026-9050 | Medium, 4.3 | Slider Revolution WordPress plugin | Authenticated Contributor+ information exposure and unauthorized data modification; update plugin | Medium |
| CVE-2026-10100 / CVE-2026-3722 | Medium | WordPress plugins Simple Custom Login Page and Auto Image Attributes | Stored XSS issues requiring privileged/contributor access | Medium |

## Exploits Released

### Sploitus Top 10 Reconstructed

| Rank | Sploitus indicator | CVE | Affected software | Exploit type | Maturity assessment | Public PoC availability | Weaponization potential | Confidence |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | `42F02C70-7699-5973-9CBB-9AC8D65C6251` | CVE-2026-20223 | Cisco Secure Workload | Unauthorized API access / Site Admin access | PoC-style commands shown; vendor advisory confirms vulnerability | Yes, indicator only | High due CVSS 10 and enterprise software | High |
| 2 | Multiple indexed Sploitus pages | CVE-2026-9082 | Drupal Core with PostgreSQL JSON:API | SQL injection; possible privilege escalation/RCE in some configurations | Multiple detector/scanner PoCs; CISA KEV carryover | Yes | High for exposed Drupal/PostgreSQL sites | High |
| 3 | `DD481546-AB6A-54AA-B91D-10A0FE3ADFA2` | CVE-2026-4882 | User Registration Advanced Fields WordPress plugin <= 1.6.20 | Unauthenticated arbitrary file upload leading to webshell/RCE | "Full auto exploit" claims; Wordfence reference | Yes, unvalidated | High for WordPress targets | Medium |
| 4 | `300A3F87-96E3-5A9A-BC5B-46F2890EF41B` | CVE-2026-8181 | Burst Statistics WordPress plugin 3.4.0-3.4.1.1 | Authentication bypass/admin takeover | PoC/tooling claims; Wordfence reference | Yes, unvalidated | High for internet WordPress | Medium |
| 5 | `2FC7FD64-4D38-5415-A621-B0095202AE73` | CVE-2026-4631 | Cockpit 327-359 | Unauthenticated SSH command-line argument injection/RCE | Code-analysis exploit indicator; GHSA/fixed version referenced | Yes, unvalidated | High for exposed Cockpit | Medium |
| 6 | `98A530E3-D6DF-5A1C-A625-F5D67AF2C8F7` | CVE-2026-42945 | Claimed nginx HTTP/2 parsing issue | RCE toolkit claim | No primary vendor/NVD corroboration in this run | Yes, unvalidated | Potentially high if real; currently low-confidence | Low |
| 7 | `3873BA24-292D-55CB-9F36-921E576A8E90` | CVE-2026-26335 | Calero VeraSMART pre-2022 R1 | ASP.NET ViewState deserialization RCE via hard-coded keys | Exploit workflow described | Yes, unvalidated | High for exposed legacy VeraSMART | Medium |
| 8 | `B6E4E8D1-B299-56A2-9043-5FBF111F3729` | CVE-2026-32746 | GNU InetUtils telnetd <= 2.7 | Pre-auth buffer overflow crash/RCE potential | PoC claims crash, not code execution | Yes, crash PoC | Medium to High; telnet exposure dependent | Medium |
| 9 | `DD7B8E38-E9E8-52C9-B4F5-22CF6E561E60` | CVE-2026-22679 | Weaver E-cology 10.0 before build 20260312 | Unauthenticated command injection/RCE | Claims Shadowserver exploitation; not independently verified here | Yes, unvalidated | High for exposed E-cology | Low-Medium |
| 10 | `6D575D35-4574-521C-A014-D7751E0556C5` | CVE-2026-42897 | Microsoft CSS-Exchange Health Checker tooling | Mitigation visibility blind spot | PoC/demo for detection gap; not direct product compromise | Yes | Medium operational risk; lower exploitability | Medium |

### ExploitDB and Packet Storm

- Exploit-DB RSS failed with HTTP 500 during collection. No direct new Exploit-DB addition could be verified in this run.
- NVD references Exploit-DB for CVE-2018-25427 Arm Whois buffer overflow in the 24-hour window, but this appears to be historical exploit material newly enriched by VulnCheck rather than a new 2026 enterprise exposure.
- Packet Storm search showed site update volume but no specific new June 2 exploit release could be validated from primary Packet Storm pages during this run.

### New GitHub PoC Indicators

| Repository | Created | Claim | Validation status | Action |
| --- | --- | --- | --- | --- |
| `0xABCD01/CVE-2026-41089` | 2026-06-01 | Windows Netlogon CLDAP stack buffer overflow PoC, CVSS 9.8 | NVD confirms CVE is Critical; active exploitation claim not corroborated by primary CCB search | Monitor, do not execute; patch May 2026 Microsoft updates on domain controllers |
| `bolubey/CVE-2026-0257` | 2026-06-01 | PAN-OS GlobalProtect cookie forgery | CVE and active exploitation confirmed by Palo Alto/Rapid7/CISA; repo functionality not tested | Treat as public PoC signal; prioritize edge devices |
| `alisster00/CVE-2026-23744-RCE` | 2026-06-02 | MCPJam Inspector v1.4.2 RCE | NVD confirms CVE-2026-23744 as MCPJam RCE patched in 1.4.3; repo not tested | Upgrade MCPJam Inspector; block unauthenticated access |
| `ahmadsadeeq/TelnetdBypass-` | 2026-06-01 | GNU InetUtils telnetd auth bypass scanner | NVD confirms CVE-2026-24061 Critical; repo not tested | Remove/external-block telnetd; upgrade GNU InetUtils |
| `jabir-dev/CVE-2026-BetterSQLCipher-RCE` | 2026-06-01 | better-sqlcipher loadExtension RCE | Uses placeholder CVE-2026-XXXXX in README; no CVE corroborated in this run | Low-confidence indicator; track upstream only |

## Malware Intelligence

| Finding | Details | Confidence |
| --- | --- | --- |
| FortiClient EMS to EKZ Infostealer | Secondary reporting attributes May 2026 EKZ Infostealer deployment to FortiClient EMS CVE-2026-35616 exploitation. Fortinet advisory snippets state exploitation in the wild and hotfix guidance for 7.4.5/7.4.6. Abuse path reportedly uses EMS administrative workflows to push malicious PowerShell to managed endpoints. | Medium |
| VX-Underground MalwareSourceCode | GitHub metadata shows `vxunderground/MalwareSourceCode` pushed 2026-05-30 and updated 2026-06-02; recursive tree contains `Python/Stealer.Python.GMBA.Manipulator.7z`. No new June 2 ransomware leak confirmed. | High for repo state, Medium for malware impact |
| Nx Console and TanStack supply-chain KEV carryover | CISA KEV lists CVE-2026-48027 and CVE-2026-45321 with known ransomware campaign use. Both relate to malicious package/extension publication and credential harvesting. | High |
| Public PoC repositories may be malicious | GitHub PoC repositories were not executed; handle all cloned exploit code as potentially trojanized. | High |

## Security Releases and Advisories

| Vendor/source | Release/advisory | Impact | Action |
| --- | --- | --- | --- |
| Palo Alto Networks | CVE-2026-0257 advisory updated 2026-05-29 | GlobalProtect auth bypass, exploit maturity ATTACKED | Patch fixed PAN-OS/Prisma Access releases; apply mitigations immediately |
| Rapid7 | Observed exploitation of CVE-2026-0257 | Confirms waves on 2026-05-17 and 2026-05-21, IOCs available | Hunt for cookie logins to local admin, GP-CLIENT/DESKTOP-GP01, spoofed MAC `aa:bb:cc:dd:ee:ff`, listed IPs |
| Cisco | CVE-2026-20182 and CVE-2026-20223 advisories | SD-WAN auth bypass exploited; Secure Workload CVSS 10 unauthorized API access | Upgrade; no workarounds |
| Oracle/CISA | CVE-2024-21182 added to KEV on 2026-06-01 | WebLogic unauthenticated remote compromise risk via T3/IIOP | Apply CPU, restrict protocols, due 2026-06-04 |
| Cloud Foundry | CVE-2026-40965 UAA advisory | EC private keys exposed by public `/token_keys` endpoint | Upgrade and rotate keys/tokens |
| Zyxel | 2026-06-02 UPnP CPE firmware advisory | CVE-2026-3870 and CVE-2026-3871 adjacent-network DoS | Obtain firmware patches from Zyxel/ISP |
| GitHub Security Advisories | Cline, CloudPirates, Langroid | Critical dev-tool and CI/CD supply-chain issues | Patch/disable; rotate secrets if workflows ran |
| GitLab | 19.0.1, 18.11.4, 18.10.7 patch release | Duo AI workflow runner access control and multiple auth/DoS issues | Upgrade self-managed instances |
| ProjectDiscovery | nuclei-templates v10.4.4 | Adds critical/KEV detection templates including Cisco SD-WAN and Drupal | Update scanner content; also upgrade nuclei >= 3.8.0 for CVE-2026-41645 |
| Fortinet | FortiGuard PSIRT and FortiClient EMS reports | CVE-2026-35616 exploited in the wild; FortiAuthenticator CVE-2026-44277 Critical | Patch EMS/FortiAuthenticator; hunt for EKZ deployment artifacts |

## Recommended Actions, Ranked

1. Emergency patch and hunt: PAN-OS/Prisma Access CVE-2026-0257. Confirm GlobalProtect authentication override configuration, upgrade fixed releases, rotate cookie certificates if reused, and hunt Rapid7 IOCs.
2. Emergency patch and compromise assessment: Cisco SD-WAN CVE-2026-20182. Upgrade fixed versions, review control connections, collect admin-tech, and engage Cisco TAC for exposed systems.
3. Patch by CISA due date: Oracle WebLogic CVE-2024-21182 by 2026-06-04. Restrict T3/IIOP exposure and review logs for suspicious unauthenticated access attempts.
4. Patch Cisco Secure Workload CVE-2026-20223. Public PoC indicators and CVSS 10 warrant urgent remediation even without confirmed exploitation.
5. Rotate secrets after patching Cloud Foundry UAA CVE-2026-40965. Treat EC JWT signing keys exposed via `/token_keys` as compromised.
6. Review CI/CD supply-chain exposure: CloudPirates-style `pull_request_target` workflows, PAT use, checkout of fork-controlled code, and SSH signing keys written to disk.
7. Patch AI/dev tooling: Cline CVE-2026-44211, Langroid CVE-2026-25879, MCPJam CVE-2026-23744, and AITER CVE-2026-49121 where used in developer or ML infrastructure.
8. Update scanner content safely: ProjectDiscovery nuclei templates for new KEV/critical checks, and nuclei engine >= 3.8.0.
9. Apply June 2 Zyxel firmware patches for affected CPE models and disable/restrict UPnP on untrusted LAN/WLAN segments.
10. Treat all public PoC repositories as untrusted. Review statically in an isolated environment; never run directly on analyst workstations.

## Unified Vulnerability Records

```json
[
  {
    "cve": "CVE-2026-0257",
    "cvss": "7.8",
    "vendor": "Palo Alto Networks",
    "product": "PAN-OS / Prisma Access GlobalProtect",
    "affected_versions": "PAN-OS 12.1 < 12.1.4-h6 or < 12.1.7; 11.2 < fixed hotfix trains; 11.1 < fixed hotfix trains; 10.2 < fixed hotfix trains; Prisma Access 10.2/11.2 before fixed releases",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://www.rapid7.com/blog/post/etr-rapid7-observed-exploitation-of-pan-os-globalprotect-authentication-bypass-vulnerability-cve-2026-0257/",
      "https://github.com/bolubey/CVE-2026-0257"
    ],
    "patch_available": true,
    "sources": [
      "https://security.paloaltonetworks.com/CVE-2026-0257",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://www.rapid7.com/blog/post/etr-rapid7-observed-exploitation-of-pan-os-globalprotect-authentication-bypass-vulnerability-cve-2026-0257/"
    ]
  },
  {
    "cve": "CVE-2026-20182",
    "cvss": "Critical",
    "vendor": "Cisco",
    "product": "Catalyst SD-WAN Controller and Manager",
    "affected_versions": "Multiple Cisco Catalyst SD-WAN releases before fixed software",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://github.com/projectdiscovery/nuclei-templates/releases/tag/v10.4.4"
    ],
    "patch_available": true,
    "sources": [
      "https://sec.cloudapps.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-sdwan-rpa2-v69WY2SW",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"
    ]
  },
  {
    "cve": "CVE-2024-21182",
    "cvss": "Not specified in CISA KEV feed",
    "vendor": "Oracle",
    "product": "WebLogic Server",
    "affected_versions": "Oracle WebLogic Server 12.2.1.4.0 and 14.1.1.0.0 per Oracle July 2024 CPU family matrix",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://www.oracle.com/security-alerts/cpujul2024.html"
    ]
  },
  {
    "cve": "CVE-2026-20223",
    "cvss": "10.0",
    "vendor": "Cisco",
    "product": "Secure Workload",
    "affected_versions": "3.9 and earlier; 3.10 before 3.10.8.3; 4.0 before 4.0.3.17",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://sploitus.com/exploit?id=42F02C70-7699-5973-9CBB-9AC8D65C6251"
    ],
    "patch_available": true,
    "sources": [
      "https://www.cisco.com/c/en/us/support/docs/csa/cisco-sa-csw-pnbsa-g8WEnuy.html"
    ]
  },
  {
    "cve": "CVE-2026-40965",
    "cvss": "10.0",
    "vendor": "Cloud Foundry Foundation",
    "product": "UAA / cf-deployment",
    "affected_versions": "uaa_release v76.12.0 through v78.12.0; CF Deployment v30.0.0 through v56.0.0 when EC JWT signing keys are used",
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
    "cve": "CVE-2026-7858",
    "cvss": "9.8",
    "vendor": "Dassault Systemes",
    "product": "Teamwork Cloud / Magic Collaboration Studio",
    "affected_versions": "No Magic Release 2022x through 2026x; CATIA Magic Release 2022x through 2026x",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://www.3ds.com/trust-center/security/security-advisories/cve-2026-7858",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-7858"
    ]
  },
  {
    "cve": "CVE-2026-49121",
    "cvss": "9.2",
    "vendor": "ROCm",
    "product": "AI Tensor Engine for ROCm (AITER)",
    "affected_versions": "<= 0.1.14",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/ROCm/aiter/issues/3076",
      "https://github.com/ROCm/aiter/pull/3170"
    ],
    "patch_available": true,
    "sources": [
      "https://www.vulncheck.com/advisories/ai-tensor-engine-for-rocm-aiter-unauthenticated-rce-via-messagequeue-recv-pickle-deserialization",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-49121"
    ]
  },
  {
    "cve": "CVE-2026-44211",
    "cvss": "9.6",
    "vendor": "Cline",
    "product": "Cline Kanban server",
    "affected_versions": "2.13.0 and prior",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/cline/cline/security/advisories/GHSA-5c57-rqjx-35g2"
    ],
    "patch_available": false,
    "sources": [
      "https://github.com/cline/cline/security/advisories/GHSA-5c57-rqjx-35g2",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-44211"
    ]
  },
  {
    "cve": "CVE-2026-45131",
    "cvss": "10.0",
    "vendor": "CloudPirates",
    "product": "Open Source Helm Charts GitHub Actions workflow",
    "affected_versions": "Before commit fcf9302",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/CloudPirates-io/helm-charts/security/advisories/GHSA-c47r-c7gw-cvph"
    ],
    "patch_available": true,
    "sources": [
      "https://github.com/CloudPirates-io/helm-charts/security/advisories/GHSA-c47r-c7gw-cvph",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-45131"
    ]
  },
  {
    "cve": "CVE-2026-45132",
    "cvss": "10.0",
    "vendor": "CloudPirates",
    "product": "Open Source Helm Charts GitHub Actions workflow",
    "affected_versions": "Before commit fcf9302",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/CloudPirates-io/helm-charts/security/advisories/GHSA-r874-j8fr-x2pj"
    ],
    "patch_available": true,
    "sources": [
      "https://github.com/CloudPirates-io/helm-charts/security/advisories/GHSA-r874-j8fr-x2pj",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-45132"
    ]
  },
  {
    "cve": "CVE-2026-3870",
    "cvss": "6.5",
    "vendor": "Zyxel",
    "product": "VMG4005-B50B",
    "affected_versions": "5.13(ABRL.5.4)C0 and earlier",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://www.zyxel.com/global/en/support/security-advisories/zyxel-security-advisory-for-buffer-overflow-vulnerabilities-in-the-upnp-function-of-certain-4g-lte-5g-nr-cpe-and-dsl-ethernet-cpe-06-02-2026",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-3870"
    ]
  },
  {
    "cve": "CVE-2026-3871",
    "cvss": "6.5",
    "vendor": "Zyxel",
    "product": "NR7101 / Nebula LTE3301-PLUS / Nebula NR7101 / VMG4005-B50B",
    "affected_versions": "NR7101 <= 1.00(ABUV.11)C0; LTE3301-PLUS <= 1.18(ACCA.6)C0; Nebula NR7101 <= 1.16(ACCC.1)C0; VMG4005-B50B <= 5.13(ABRL.5.4)C0",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://www.zyxel.com/global/en/support/security-advisories/zyxel-security-advisory-for-buffer-overflow-vulnerabilities-in-the-upnp-function-of-certain-4g-lte-5g-nr-cpe-and-dsl-ethernet-cpe-06-02-2026",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-3871"
    ]
  }
]
```

## Source Links

- CISA KEV JSON: https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json
- NVD API 2.0: https://services.nvd.nist.gov/rest/json/cves/2.0
- Palo Alto Networks CVE-2026-0257: https://security.paloaltonetworks.com/CVE-2026-0257
- Rapid7 CVE-2026-0257 exploitation report: https://www.rapid7.com/blog/post/etr-rapid7-observed-exploitation-of-pan-os-globalprotect-authentication-bypass-vulnerability-cve-2026-0257/
- Cisco Secure Workload CVE-2026-20223: https://www.cisco.com/c/en/us/support/docs/csa/cisco-sa-csw-pnbsa-g8WEnuy.html
- Cisco SD-WAN CVE-2026-20182: https://sec.cloudapps.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-sdwan-rpa2-v69WY2SW
- Oracle July 2024 CPU: https://www.oracle.com/security-alerts/cpujul2024.html
- Cloud Foundry UAA CVE-2026-40965: https://www.cloudfoundry.org/blog/cve-2026-40965-uaa-ec-private-key-disclosure/
- VulnCheck AITER CVE-2026-49121: https://www.vulncheck.com/advisories/ai-tensor-engine-for-rocm-aiter-unauthenticated-rce-via-messagequeue-recv-pickle-deserialization
- GitHub Cline advisory: https://github.com/cline/cline/security/advisories/GHSA-5c57-rqjx-35g2
- GitHub CloudPirates advisories: https://github.com/CloudPirates-io/helm-charts/security/advisories/GHSA-c47r-c7gw-cvph and https://github.com/CloudPirates-io/helm-charts/security/advisories/GHSA-r874-j8fr-x2pj
- GitHub Langroid advisory: https://github.com/langroid/langroid/security/advisories/GHSA-mxfr-6hcw-j9rq
- Zyxel 2026-06-02 advisory: https://www.zyxel.com/global/en/support/security-advisories/zyxel-security-advisory-for-buffer-overflow-vulnerabilities-in-the-upnp-function-of-certain-4g-lte-5g-nr-cpe-and-dsl-ethernet-cpe-06-02-2026
- ProjectDiscovery nuclei-templates v10.4.4: https://github.com/projectdiscovery/nuclei-templates/releases/tag/v10.4.4
- VX-Underground MalwareSourceCode: https://github.com/vxunderground/MalwareSourceCode
