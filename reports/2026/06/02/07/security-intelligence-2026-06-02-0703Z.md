# Security Intelligence Report - 2026-06-02 07:03 UTC

Automation run: hourly cron at 2026-06-02T07:02:22Z  
Repository: dfalt0/Test-cursor-security-automation  
Collection window emphasized: 2026-06-02 06:00-07:30 UTC, with 24-hour context for exploitation and patch priority.

## Executive Summary

- Total CVEs discovered in the latest NVD hourly window: 0 newly published CVEs from 06:00-07:30 UTC.
- NVD day-to-date total for 2026-06-02: 24 CVEs: 1 critical, 17 medium, 5 low, 1 unknown.
- Rolling 24-hour NVD context: 363 CVEs: 16 critical, 110 high, 139 medium, 35 low, 63 unknown.
- Critical findings requiring enterprise attention:
  - CVE-2026-8206, Kirki WordPress plugin account takeover, CVSS 9.8, published in NVD at 04:17 UTC and in GitHub Advisory Database at 06:30 UTC.
  - CVE-2026-41089, Microsoft Windows Netlogon RCE, active exploitation confirmed by CCB Belgium, patched in May 2026 Patch Tuesday.
  - CVE-2026-20182, Cisco Catalyst SD-WAN Controller/Manager authentication bypass, KEV-listed, limited exploitation confirmed by Cisco, public Sploitus and Metasploit indicators.
  - CVE-2026-0257, Palo Alto PAN-OS GlobalProtect authentication bypass, KEV-listed and actively exploited.
  - CVE-2024-21182, Oracle WebLogic Server unspecified vulnerability, newest CISA KEV addition on 2026-06-01.
  - CVE-2026-41940, cPanel/WHM authentication bypass, KEV-listed, public exploit code, ransomware/backdoor activity.
  - CVE-2026-9082, Drupal Core PostgreSQL SQL injection, KEV-listed, public PoC and active exploit attempts reported by Drupal advisory update.
- Active exploitation findings: Netlogon, Cisco SD-WAN, PAN-OS, Oracle WebLogic, Drupal Core, cPanel/WHM, FortiClient EMS, and carry-forward supply-chain KEV items for Nx Console and TanStack.
- New malware or ransomware intelligence: no new vx-underground GitHub pushes after 2026-05-30; carry-forward cPanel "Sorry" ransomware and Filemanager backdoor activity remain high priority.
- Important vendor/security releases: GitHub Advisory Database published four 06:30 UTC advisories, led by Kirki CVE-2026-8206 and MLflow CVE-2026-3198. GitLab's May 27 security release remains relevant for self-managed instances.

## Top Vulnerabilities

### 1. CVE-2026-8206 - Kirki WordPress Plugin Account Takeover

- Severity: Critical, CVSS 9.8.
- Affected software: Kirki - Freeform Page Builder, Website Builder and Customizer plugin, versions 6.0.0 through 6.0.6.
- Issue: unauthenticated attackers can provide an arbitrary email address when requesting password reset by username, causing reset links for registered users to be sent to attacker-controlled email.
- Exploit availability: no validated full exploit observed in this run, but the primitive is straightforward and GitHub Advisory Database published GHSA-gr32-6rr4-7px2 at 06:30 UTC.
- Active exploitation: not confirmed.
- Patch available: update to 6.0.7 or later.
- Confidence: High. Corroborated by NVD/GitHub Advisory Database and Patchstack.
- Recommended action: inventory WordPress sites using Kirki, update immediately, review admin password-reset events and web logs.

### 2. CVE-2026-41089 - Microsoft Windows Netlogon RCE

- Severity: Critical, CVSS 9.8.
- Affected software: Windows Server 2012-2025 domain controllers.
- Issue: unauthenticated remote attacker can send a crafted Netlogon request to potentially execute code with SYSTEM privileges.
- Exploit availability: no public working exploit validated in this run.
- Active exploitation: confirmed by CCB Belgium update on 2026-05-29.
- Patch available: Microsoft May 2026 security updates.
- Confidence: High for exploitation status because CCB states it is actively exploited in the wild.
- Recommended action: patch domain controllers immediately, restrict RPC exposure, and hunt for anomalous Netlogon/MS-NRPC traffic.

### 3. CVE-2026-20182 - Cisco Catalyst SD-WAN Controller/Manager Authentication Bypass

- Severity: Critical, CVSS 10.0.
- Affected software: Cisco Catalyst SD-WAN Controller and Manager fixed release trains listed in Cisco advisory cisco-sa-sdwan-rpa2-v69WY2SW.
- Issue: peering authentication flaw in control connection handshaking can allow unauthenticated administrative access and NETCONF control-plane manipulation.
- Exploit availability: public Sploitus indicators, including assessment scripts and a Metasploit auxiliary module indicator.
- Active exploitation: Cisco PSIRT confirms limited exploitation; CISA KEV date added 2026-05-14.
- Patch available: yes, no workarounds per Cisco; follow ED 26-03 hunt and hardening guidance.
- Confidence: High.
- Recommended action: patch, preserve logs, run Cisco control connection checks, and open Cisco TAC cases for suspected compromise.

### 4. CVE-2026-0257 - Palo Alto PAN-OS GlobalProtect Authentication Bypass

- Severity: High/Critical operational risk; NVD and Palo Alto classify the GlobalProtect authentication bypass as high severity, while KEV and active exploitation make it remediation-critical.
- Affected software: PAN-OS GlobalProtect portals/gateways with authentication override cookies enabled and vulnerable certificate configuration.
- Issue: attackers can bypass security restrictions and establish unauthorized VPN connections.
- Exploit availability: public PoC indicators reported by secondary sources; no universal exploit validated here.
- Active exploitation: CISA KEV date added 2026-05-29.
- Patch available: yes; upgrade to Palo Alto fixed versions or disable authentication override/use a dedicated certificate.
- Confidence: High for exploitation and patch status via vendor advisory plus CISA KEV.
- Recommended action: patch internet-facing GlobalProtect, rotate authentication-override certificate material, and review VPN logs for suspicious cookie authentication.

### 5. CVE-2024-21182 - Oracle WebLogic Server Unspecified Vulnerability

- Severity: KEV-listed active exploitation; CVSS not re-scored during this run.
- Affected software: Oracle WebLogic Server; CISA notes network access via T3/IIOP.
- Issue: unauthenticated network attacker may compromise WebLogic and gain unauthorized data access.
- Exploit availability: not validated in this run.
- Active exploitation: CISA KEV date added 2026-06-01.
- Patch available: apply Oracle CPU guidance.
- Confidence: High for KEV status, Medium for technical exploit details because CISA describes the issue as unspecified.
- Recommended action: prioritize internet-facing WebLogic, block unnecessary T3/IIOP exposure, and apply Oracle CPU mitigations.

### 6. CVE-2026-41940 - cPanel/WHM Authentication Bypass and Ransomware Activity

- Severity: Critical, CVSS 9.8.
- Affected software: cPanel and WHM, WP Squared.
- Issue: authentication bypass in login flow/CRLF session handling can grant unauthorized control-panel access.
- Exploit availability: Sploitus entries include Metasploit module indicator, ExploitDB entry EDB-ID 52574, and public scanner/PoC references.
- Active exploitation: KEV-listed; public reporting ties exploitation to "Sorry" ransomware and Filemanager backdoor campaigns.
- Patch available: update to fixed cPanel tracks including 11.110.0.97, 11.118.0.63, 11.126.0.54, 11.132.0.29, 11.134.0.20, 11.136.0.5 or later, and WP Squared fixed versions.
- Confidence: High.
- Recommended action: force-update cPanel, treat vulnerable exposed hosts as potentially compromised, rotate credentials/SSH keys, and restore from clean backups where ransomware indicators exist.

### 7. CVE-2026-9082 - Drupal Core PostgreSQL SQL Injection

- Severity: Operationally critical despite NVD 6.5 because Drupal rates it Highly Critical and active attempts are reported.
- Affected software: Drupal Core with PostgreSQL backend in multiple 8.9, 10.x, and 11.x ranges before fixed releases.
- Issue: anonymous SQL injection in the database abstraction API/entity query condition handling for PostgreSQL.
- Exploit availability: ExploitDB EDB-ID 52608, Sploitus PoC, GitHub PoCs, and ProjectDiscovery nuclei template.
- Active exploitation: Drupal advisory update states exploit attempts are detected in the wild.
- Patch available: Drupal 10.4.10, 10.5.10, 10.6.9, 11.1.10, 11.2.12, 11.3.10 or later.
- Confidence: High.
- Recommended action: patch PostgreSQL-backed Drupal immediately, disable JSON:API if patching is delayed, and hunt for unexpected HTTP 500s on /user/login and /jsonapi routes.

### 8. CVE-2026-40965 - Cloud Foundry UAA EC Private Key Disclosure

- Severity: Critical, CVSS 10.0.
- Affected software: uaa_release v76.12.0 through v78.12.0; CF Deployment v30.0.0 through v56.0.0 when EC JWT signing keys are used.
- Issue: EC private key material exposed through public /token_keys endpoint.
- Exploit availability: no exploit code required for exposed endpoint retrieval if affected configuration exists.
- Active exploitation: not confirmed.
- Patch available: uaa_release v78.13.0 or greater; cf-deployment v56.1.0 or greater.
- Confidence: High.
- Recommended action: patch, rotate exposed EC signing keys, invalidate tokens signed with exposed keys, and confirm RSA-key-only deployments are not affected.

### 9. CVE-2026-3198 - MLflow Gateway API Authorization Exposure

- Severity: Medium, CVSS 6.5.
- Affected software: MLflow 3.9.0 with basic-auth.
- Issue: multiple Gateway API list endpoints are missing from authorization handler coverage, allowing authenticated users without intended permissions to enumerate secrets, endpoints, and model definitions.
- Exploit availability: advisory-level detail; no weaponized exploit validated.
- Active exploitation: not confirmed.
- Patch available: monitor MLflow upstream; related MLflow authentication/authorization flaws have fixes in later releases, but this specific advisory should be tracked to a vendor-patched version.
- Confidence: Medium because GitHub Advisory Database is unreviewed but aligns with NVD/huntr details.
- Recommended action: restrict MLflow Gateway access, avoid exposing MLflow servers broadly, and upgrade once the relevant fix is published.

### 10. CVE-2026-35616 - FortiClient EMS RCE

- Severity: Critical, CVSS 9.1.
- Affected software: FortiClient EMS 7.4.5 and 7.4.6.
- Issue: improper access control permits unauthenticated code/command execution via crafted requests.
- Exploit availability: exploitation observed, but no public exploit validated in this run.
- Active exploitation: confirmed by Fortinet reporting and CISA KEV carry-forward; recent reporting indicates malware deployment in fresh attacks.
- Patch available: Fortinet hotfixes; permanent fix in newer FortiClient EMS releases.
- Confidence: High.
- Recommended action: patch EMS immediately, restrict management interface exposure, and hunt for malware persistence and anomalous EMS API activity.

## Exploits Released

### Sploitus Top 10 Indicators

Sploitus homepage fetch did not expose a distinct "Exploits of the Week" block during this run. The following is a reconstructed top-10 set from targeted Sploitus search results and should be treated as exploit-intelligence indicators requiring validation before operational use.

| Rank | Indicator | Affected software | Exploit type | Maturity | Public PoC | Weaponization potential | Confidence |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | CVE-2026-20182, Sploitus ID 13DF22F3-E9C6-58EE-B458-EB585C4D715D | Cisco Catalyst SD-WAN Controller/Manager | Auth bypass, NETCONF access, SSH key injection | Detailed PoC/assessment script | Yes | Very high | High |
| 2 | CVE-2026-20182, Sploitus Metasploit auxiliary indicator | Cisco Catalyst SD-WAN | Auth bypass check/exploitation helper | Metasploit module indicator | Yes | Very high | Medium |
| 3 | CVE-2026-41940, Sploitus Metasploit RCE indicator | cPanel/WHM | CRLF auth bypass to root/admin session | Metasploit module indicator | Yes | Very high | High |
| 4 | CVE-2026-41940, Sploitus ransomware/IOC entry | cPanel/WHM | Auth bypass plus ransomware campaign intelligence | IOC/YARA/forensics pack | Yes | Very high | High |
| 5 | CVE-2026-41940, Sploitus EDB-ID 52574 | cPanel/WHM | CRLF injection auth bypass | ExploitDB PoC | Yes | Very high | High |
| 6 | CVE-2026-9082, Sploitus ID 458CE696-FE39-500F-9131-2E24B1BC2E12 | Drupal Core PostgreSQL | Anonymous SQL injection | Reproduction lab/PoC | Yes | High | High |
| 7 | CVE-2026-21858, Sploitus ID 61F5A984-F6DE-5060-8EDF-0256034BFF43 | n8n Form Webhook | File read to auth/session forgery and RCE chain | Detailed exploit chain | Yes | High | Medium |
| 8 | CVE-2026-29014, Sploitus PacketStorm 218222 | MetInfo CMS 8.1 | PHP code injection/RCE | Packet Storm exploit | Yes | High | Medium |
| 9 | CVE-2025-6965, Sploitus EDB-ID 52499 | SQLite/winsqlite3 on Windows Server contexts | Heap overflow/DoS, possible RCE claims | ExploitDB PoC | Yes | Medium | Medium |
| 10 | CVE-2026-0386, Sploitus ID 2E50244E-0C43-5A91-80C4-732ED4954808 | PowerShell Invoke-WebRequest/mshtml behavior | Script execution/client-side execution scenario | Research PoC | Yes | Medium | Low |

### ExploitDB Additions

Latest ExploitDB CSV date-sorted entries:

- 2026-06-01: EDB-ID 52607, WordPress OrderConvo 14 path traversal, CVE-2025-10162, unverified.
- 2026-06-01: EDB-ID 52608, Drupal Core 10.5.5 error-based SQL injection, CVE-2026-9082, unverified.
- 2026-05-30: YAMCS yamcs-core 5.12.7 LDAP injection, no rate limiting, and user enumeration entries.
- 2026-05-30: Notepad++ 8.9.6 arbitrary code execution, CVE-2026-48778.

### New GitHub PoCs

- GitHub repository search for `CVE-2026 PoC exploit created:>=2026-06-02` returned no newly created repositories.
- Recently pushed unvalidated CVE-2026 exploit/PoC repositories include:
  - fartlover37/CVE-2026-2441-PoC, Chrome/Blink use-after-free PoC claim, pushed 2026-06-02T05:52Z.
  - hamzamalik3461/CVE-2026-20841, Windows Notepad RCE claim, pushed 2026-06-02T05:49Z.
  - Defacto-ridgepole254/CVE-2026-41940-Exploit-PoC, cPanel/WHM auth bypass PoC claim, pushed 2026-06-02T06:35Z.
  - Dullpurple-sloop726/CVE-2026-31431-Linux-Copy-Fail, Linux LPE Rust claim, pushed 2026-06-02T06:34Z.
  - Recorded-texteditor120/CVE-2026-31802, npm tar path traversal claim, pushed 2026-06-02T06:11Z.
  - Jumpthereness578/CVE-2026-2991, KiviCare auth bypass claim, pushed 2026-06-02T06:14Z.
  - Liverwortenuresis371/copyfail-rs, Linux Copy-Fail LPE claim, pushed 2026-06-02T06:34Z.
- Confidence: Low to Medium for repository functionality. These are indicators only; public CVE PoC repositories can be malicious or fabricated.

### ProjectDiscovery/Nuclei

- ProjectDiscovery has templates for CVE-2026-9082 and CVE-2026-41940. Both are high-value defender detections and should be run only under authorized scanning scopes.

## Malware Intelligence

- vx-underground:
  - Web root was reachable through WebFetch, but no new collection items were visible from the page tree.
  - GitHub user repository check showed MalwareSourceCode last pushed 2026-05-30T07:11Z and updated 2026-06-02T01:08Z; no new push since prior hourly run.
  - No new vx-underground ransomware campaign was identified.
- Ransomware:
  - cPanel/WHM CVE-2026-41940 remains tied to "Sorry" ransomware reporting. Multiple sources describe a Go-based Linux encryptor using ChaCha20 plus RSA-2048 and appending `.sorry`.
  - Attackers exploiting CVE-2026-41940 have also been reported deploying Filemanager backdoor and credential-stealing payloads.
- Malware campaigns:
  - FortiClient EMS CVE-2026-35616 carry-forward remains relevant because recent reporting describes malware deployment against unpatched EMS.
- Supply chain:
  - CISA KEV carry-forward: Nx Console CVE-2026-48027 and TanStack CVE-2026-45321 remain listed with known ransomware campaign use for malicious package/extension publication and credential theft.
  - Daemon Tools Lite CVE-2026-8398 remains a KEV-listed embedded malicious code vulnerability.

## Security Releases and Vendor Advisories

- Microsoft:
  - No June 2 Patch Tuesday release observed; June 2026 Patch Tuesday is expected on the second Tuesday of the month.
  - Carry-forward priority: May 2026 patches for CVE-2026-41089 Netlogon RCE and related critical Windows issues.
- Cisco:
  - No new June 2 advisory found. Cisco SD-WAN advisory cisco-sa-sdwan-rpa2-v69WY2SW was updated May 27 with compromise-check guidance and limited exploitation acknowledgement.
- Fortinet:
  - No June 2 critical PSIRT publication found. May and April Fortinet critical advisories remain important, especially FortiClient EMS CVE-2026-35616 and FortiAuthenticator/FortiSandbox issues.
- Palo Alto Networks:
  - CVE-2026-0257 vendor advisory remains active priority for GlobalProtect configurations using authentication override cookies.
- VMware/Broadcom:
  - No new June 2 VMware/Broadcom advisory found. Broadcom KBs continue to address Dirty Frag/Fragnesia Linux LPE impact evaluation for VMware portfolio and VKS Ubuntu nodes.
- Cloud Foundry:
  - CVE-2026-40965 advisory recommends uaa_release v78.13.0+ and cf-deployment v56.1.0+.
- GitHub:
  - GitHub Advisory Database published four advisories at 06:30 UTC: CVE-2026-8206 Kirki, CVE-2026-3198 MLflow, CVE-2026-10583 GoClaw SSRF, and CVE-2026-10581 DedeCMS SSRF.
- GitLab:
  - May 27 GitLab security release remains relevant: self-managed GitLab CE/EE should upgrade to 19.0.1, 18.11.4, or 18.10.7. GitLab.com and GitLab Dedicated do not require customer action.
- Drupal:
  - SA-CORE-2026-004 remains a critical operational patch for PostgreSQL-backed Drupal. Exploit attempts are detected in the wild per Drupal's May 22 advisory update.
- WordPress ecosystem:
  - Kirki 6.0.7 fixes CVE-2026-8206 and other Kirki issues around version 6.0.6. Prioritize hosted WordPress fleets.

## Recommended Actions

1. Patch or isolate Windows domain controllers for CVE-2026-41089 immediately; prioritize any unpatched DCs exposed to untrusted network segments.
2. Patch Cisco Catalyst SD-WAN Controller/Manager for CVE-2026-20182 and follow CISA ED 26-03 hunt/hardening guidance.
3. Patch PAN-OS GlobalProtect for CVE-2026-0257, disable authentication override if unnecessary, and rotate dedicated cookie certificates.
4. Apply Oracle WebLogic CPU mitigations for CVE-2024-21182 and restrict T3/IIOP exposure.
5. Force-update cPanel/WHM and WP Squared for CVE-2026-41940; treat vulnerable exposed hosts as potentially compromised and hunt for `.sorry`, Filemanager, webshell, SSH key, and Telegram exfiltration indicators.
6. Patch PostgreSQL-backed Drupal Core for CVE-2026-9082 and run authorized nuclei/IDS checks for exploitation attempts.
7. Update Kirki to 6.0.7 or later across WordPress environments; review password reset activity for administrators.
8. Patch Cloud Foundry UAA for CVE-2026-40965, rotate EC signing keys, and invalidate potentially forgeable tokens.
9. Patch FortiClient EMS CVE-2026-35616 and inspect for malware persistence on EMS hosts.
10. Review and remediate supply-chain KEV items for Nx Console, TanStack, and Daemon Tools Lite; rotate developer credentials where exposure is suspected.
11. Treat newly pushed GitHub PoC repositories as untrusted indicators. Do not execute without sandboxing and code review.

## Unified Vulnerability Records

```json
[
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
      "https://github.com/advisories/GHSA-gr32-6rr4-7px2",
      "https://patchstack.com/database/wordpress/plugin/kirki/vulnerability/wordpress-kirki-plugin-6-0-0-6-0-6-unauthenticated-privilege-escalation-via-handle-forgot-password-vulnerability",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-8206"
    ]
  },
  {
    "cve": "CVE-2026-41089",
    "cvss": "9.8",
    "vendor": "Microsoft",
    "product": "Windows Netlogon",
    "affected_versions": "Windows Server 2012 through 2025 domain controllers",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://ccb.belgium.be/advisories/warning-microsoft-patch-tuesday-may-2026-patches-118-vulnerabilities-16-critical-102",
      "https://www.crowdstrike.com/en-us/blog/patch-tuesday-analysis-may-2026/",
      "https://www.thezdi.com/blog/2026/5/12/the-may-2026-security-update-review"
    ]
  },
  {
    "cve": "CVE-2026-20182",
    "cvss": "10.0",
    "vendor": "Cisco",
    "product": "Catalyst SD-WAN Controller and Manager",
    "affected_versions": "Multiple releases before Cisco fixed release trains",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://sploitus.com/exploit?id=13DF22F3-E9C6-58EE-B458-EB585C4D715D",
      "https://sploitus.com/exploit?id=MSF%3AAUXILIARY-ADMIN-NETWORKING-CISCO_SDWAN_VHUB_AUTH_BYPASS-"
    ],
    "patch_available": true,
    "sources": [
      "https://sec.cloudapps.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-sdwan-rpa2-v69WY2SW",
      "https://www.cisa.gov/known-exploited-vulnerabilities-catalog?field_cve=CVE-2026-20182",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-20182"
    ]
  },
  {
    "cve": "CVE-2026-0257",
    "cvss": "High",
    "vendor": "Palo Alto Networks",
    "product": "PAN-OS GlobalProtect",
    "affected_versions": "GlobalProtect portal/gateway configurations with authentication override cookies and vulnerable certificate reuse",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://security.paloaltonetworks.com/CVE-2026-0257",
      "https://www.cisa.gov/news-events/alerts/2026/05/29/cisa-adds-one-known-exploited-vulnerability-catalog",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-0257"
    ]
  },
  {
    "cve": "CVE-2024-21182",
    "cvss": "Unknown",
    "vendor": "Oracle",
    "product": "WebLogic Server",
    "affected_versions": "Oracle WebLogic Server versions covered by Oracle CPU guidance",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://www.cisa.gov/news-events/alerts/2026/06/01/cisa-adds-one-known-exploited-vulnerability-catalog",
      "https://www.oracle.com/security-alerts/cpujul2024.html",
      "https://nvd.nist.gov/vuln/detail/CVE-2024-21182"
    ]
  },
  {
    "cve": "CVE-2026-41940",
    "cvss": "9.8",
    "vendor": "WebPros",
    "product": "cPanel & WHM and WP Squared",
    "affected_versions": "cPanel/WHM after 11.40 and before fixed release tracks; WP Squared before fixed versions",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://sploitus.com/exploit?id=MSF%3AEXPLOIT-MULTI-HTTP-CPANEL_WHM_AUTH_BYPASS_RCE-",
      "https://sploitus.com/exploit?id=EDB-ID%3A52574",
      "https://github.com/watchtowrlabs/watchTowr-vs-cPanel-WHM-AuthBypass-to-RCE.py"
    ],
    "patch_available": true,
    "sources": [
      "https://support.cpanel.net/hc/en-us/articles/40073787579671-cPanel-WHM-Security-Update-04-28-2026",
      "https://www.cisa.gov/known-exploited-vulnerabilities-catalog?field_cve=CVE-2026-41940",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-41940"
    ]
  },
  {
    "cve": "CVE-2026-9082",
    "cvss": "6.5 NVD / Drupal highly critical",
    "vendor": "Drupal",
    "product": "Drupal Core",
    "affected_versions": "8.9.0 before 10.4.10, 10.5.0 before 10.5.10, 10.6.0 before 10.6.9, 11.0.0 before 11.1.10, 11.2.0 before 11.2.12, 11.3.0 before 11.3.10",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://sploitus.com/exploit?id=458CE696-FE39-500F-9131-2E24B1BC2E12",
      "https://gitlab.com/exploit-database/exploitdb/-/raw/main/files_exploits.csv",
      "https://github.com/projectdiscovery/nuclei-templates/blob/main/http/cves/2026/CVE-2026-9082.yaml"
    ],
    "patch_available": true,
    "sources": [
      "https://www.drupal.org/sa-core-2026-004",
      "https://www.netspi.com/blog/executive-blog/critical-vulnerability/cve-2026-9082-drupal-core-postgresql-sql-injection-overview-and-takeaways/",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-9082"
    ]
  },
  {
    "cve": "CVE-2026-40965",
    "cvss": "10.0",
    "vendor": "Cloud Foundry",
    "product": "UAA",
    "affected_versions": "uaa_release v76.12.0 through v78.12.0; CF Deployment v30.0.0 through v56.0.0 when EC JWT signing keys are used",
    "exploit_available": true,
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
    "cve": "CVE-2026-3198",
    "cvss": "6.5",
    "vendor": "MLflow",
    "product": "MLflow",
    "affected_versions": "MLflow 3.9.0 with basic-auth",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": false,
    "sources": [
      "https://github.com/advisories/GHSA-r5m9-wm49-959f",
      "https://huntr.com/bounties/e57db731-97d3-40c3-a429-831ee959807f",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-3198"
    ]
  },
  {
    "cve": "CVE-2026-35616",
    "cvss": "9.1",
    "vendor": "Fortinet",
    "product": "FortiClient EMS",
    "affected_versions": "7.4.5 and 7.4.6",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://www.fortiguard.com/psirt",
      "https://www.cyber.gc.ca/en/alerts-advisories/fortinet-security-advisory-av26-313",
      "https://securityaffairs.com/192817/malware/cve-2026-35616-forticlient-ems-flaw-actively-exploited-in-malware-attacks.html"
    ]
  }
]
```

## Source Notes

- NVD API collection:
  - 2026-06-02 06:00-07:30 UTC: 0 CVEs.
  - 2026-06-02 00:00-07:30 UTC: 24 CVEs, with severity distribution 1 critical, 17 medium, 5 low, 1 unknown.
  - 2026-06-01 07:00 to 2026-06-02 07:30 UTC: 363 CVEs, with severity distribution 16 critical, 110 high, 139 medium, 35 low, 63 unknown.
- CISA KEV feed:
  - catalogVersion: 2026.06.01.
  - newest addition: CVE-2024-21182 Oracle WebLogic Server on 2026-06-01.
- GitHub Advisory Database:
  - new advisories since 06:00 UTC: CVE-2026-8206, CVE-2026-3198, CVE-2026-10583, CVE-2026-10581.
- ExploitDB:
  - latest date-sorted CSV entries include 2026-06-01 Drupal CVE-2026-9082 and WordPress OrderConvo path traversal.
- Limitations:
  - Sploitus homepage does not expose a formal "Exploits of the Week" list to static fetch; top-10 exploit indicators are reconstructed from targeted searches.
  - Public GitHub PoC repositories were not executed or cloned. Treat them as untrusted indicators.
