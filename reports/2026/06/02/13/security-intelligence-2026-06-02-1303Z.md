# Security Intelligence Report - 2026-06-02 13:03 UTC

## Executive Summary

- Reporting window: primary hourly window 2026-06-02 12:00-13:30 UTC, with day-to-date and rolling 24-hour enrichment.
- NVD new CVEs, day-to-date: 66 total - 4 critical, 12 high, 41 medium, 5 low, 4 unknown.
- NVD new CVEs, latest hourly window: 10 total - 1 critical, 7 high, 1 medium, 1 unknown.
- Critical findings requiring review: WP Job Portal CVE-2026-42684, Masteriyo LMS PRO CVE-2025-53209, Wirtualna Uczelnia CVE-2026-34906, Kirki CVE-2026-8206, Cisco SD-WAN CVE-2026-20182, cPanel/WHM CVE-2026-41940, Microsoft Netlogon CVE-2026-41089, PAN-OS CVE-2026-0257, Oracle WebLogic CVE-2024-21182, Citrix NetScaler CVE-2026-3055, and NGINX CVE-2026-42945/CVE-2026-9256.
- Active exploitation findings: Cisco confirms limited exploitation of CVE-2026-20182; CISA KEV confirms exploitation for Oracle WebLogic CVE-2024-21182, PAN-OS CVE-2026-0257, Cisco SD-WAN CVE-2026-20182, Microsoft Defender CVE-2026-41091/CVE-2026-45498, cPanel/WHM CVE-2026-41940, Drupal CVE-2026-9082, Nx CVE-2026-48027, and TanStack CVE-2026-45321. Netlogon, NGINX, and Citrix active exploitation claims were observed in secondary reporting and should be treated as medium-confidence until validated directly by the vendor or CISA.
- New malware/campaign intelligence: Red Hat Cloud Services npm namespace compromise/Miasma supply-chain worm remains the most urgent developer ecosystem item; cPanel "Sorry" ransomware activity remains tied to CVE-2026-41940; VX-Underground GitHub repositories showed no new pushed malware-source updates after 2026-05-30.
- Important security releases/advisories: F5/NGINX rewrite-module fixes; Citrix NetScaler ADC/Gateway fixes for CVE-2026-3055/CVE-2026-4368; Cisco SD-WAN fixed releases and IOC guidance; Microsoft Defender engine/platform fixes; GitHub advisories for Vitest and praisonai-platform; Patchstack/Wordfence WordPress disclosures.

## Source Coverage and Access Notes

- CISA KEV JSON feed fetched successfully: catalogVersion 2026.06.01, 1608 entries.
- NVD API fetched successfully for 2026-06-02 12:00-13:30 UTC, 2026-06-02 day-to-date, and rolling 24 hours.
- GitHub Advisory Database fetched via authenticated GitHub API.
- GitHub repository search found no newly created repositories for query `CVE-2026 PoC exploit created:2026-06-02`, but found multiple recently pushed, unvalidated exploit indicators.
- ExploitDB CSV fetched directly from the Exploit Database GitLab mirror and sorted by publication date.
- Packet Storm direct web fetch returned an anti-abuse block; Packet Storm results below are limited to search/feed-derived context and should be rechecked manually if needed.
- Sploitus homepage did not expose an "Exploits of the Week" block in static fetch. The Sploitus section below is a reconstructed top-10 from indexed Sploitus result pages observed during this run, not an official homepage extraction.
- VX-Underground website search was limited; GitHub repository metadata was checked through `vxunderground` user repositories.

## Top Vulnerabilities

### 1. CVE-2026-20182 - Cisco Catalyst SD-WAN Controller/Manager authentication bypass

- Severity: Critical, CVSS reported as 10.0 in exploit references; CISA KEV listed.
- Affected software: Cisco Catalyst SD-WAN Controller and Manager.
- Exploit availability: Public Sploitus-indexed PoC references and Metasploit auxiliary module indicator.
- Active exploitation: High confidence. Cisco PSIRT states that in May 2026 it became aware of limited exploitation.
- Recommended action: Patch immediately to fixed Cisco releases, retain logs, run Cisco IOC checks, and open TAC cases for suspected compromise with CVE-2026-20182 in the title.
- Confidence: High.

### 2. CVE-2026-41089 - Microsoft Windows Netlogon remote code execution

- Severity: Critical, CVSS 9.8 in NVD/MSRC.
- Affected software: Windows Server domain controllers, Windows Server 2012 through 2025 version ranges listed by NVD.
- Exploit availability: Recently pushed GitHub PoC repository indicator `0xABCD01/CVE-2026-41089`; functionality not validated.
- Active exploitation: Medium confidence. Secondary reporting cites the Centre for Cybersecurity Belgium; CISA KEV feed fetched this run did not list this CVE.
- Recommended action: Ensure May 2026 Microsoft patches are deployed to all domain controllers, prioritize exposed or high-value AD sites, and monitor Netlogon/NRPC anomalies.
- Confidence: Medium.

### 3. CVE-2026-0257 - Palo Alto Networks PAN-OS authentication bypass

- Severity: Critical by prioritization due to KEV, VPN authentication bypass, enterprise perimeter impact.
- Affected software: PAN-OS GlobalProtect configurations covered by Palo Alto advisory.
- Exploit availability: Public exploit/attacked status indicators exist in prior runs; no new repository was validated this hour.
- Active exploitation: High confidence due to CISA KEV listing.
- Recommended action: Patch or apply Palo Alto mitigations, verify GlobalProtect authentication override certificate configuration, and review VPN connection anomalies.
- Confidence: High.

### 4. CVE-2024-21182 - Oracle WebLogic Server unspecified vulnerability

- Severity: Critical by prioritization due to CISA KEV addition and unauthenticated network access via T3/IIOP.
- Affected software: Oracle WebLogic Server.
- Exploit availability: No new PoC validated in this run.
- Active exploitation: High confidence due to CISA KEV listing on 2026-06-01.
- Recommended action: Apply Oracle CPU guidance immediately; CISA due date is 2026-06-04.
- Confidence: High.

### 5. CVE-2026-41940 - cPanel & WHM authentication bypass

- Severity: Critical, KEV listed, known ransomware use.
- Affected software: WebPros cPanel & WHM and WP2.
- Exploit availability: Multiple Sploitus-indexed exploit entries, Metasploit module indicator, and recently pushed GitHub PoC repository indicators.
- Active exploitation: High confidence. CISA KEV lists known ransomware campaign use; Sploitus-indexed reporting references "Sorry" ransomware.
- Recommended action: Patch all supported branches, inspect WHM/cpsrvd logs for CRLF/session-cache abuse, hunt for `.sorry` ransomware indicators, and rotate credentials for compromised panels.
- Confidence: High.

### 6. CVE-2026-42684 - Ahmad WP Job Portal blind SQL injection

- Severity: Critical, CVSS 9.3.
- Affected software: WordPress WP Job Portal through 2.5.1.
- Exploit availability: No Sploitus or GitHub PoC validated during this run; NVD/Patchstack disclosure is fresh.
- Active exploitation: Not observed.
- Recommended action: Inventory WordPress sites using WP Job Portal, disable or patch when a fixed release is available, and monitor for SQL injection probes.
- Confidence: High for disclosure, Low for exploitation.

### 7. CVE-2025-53209 - Masteriyo LMS PRO privilege escalation

- Severity: Critical, CVSS 9.8.
- Affected software: Masteriyo LMS PRO through 2.20.0.
- Exploit availability: No public PoC validated during this run.
- Active exploitation: Not observed.
- Recommended action: Disable or update the plugin, restrict administrator creation paths, and review recent WordPress user-role changes.
- Confidence: High for disclosure, Low for exploitation.

### 8. CVE-2026-34906 - Wirtualna Uczelnia server-side template injection RCE

- Severity: Critical, CVSS 9.3.
- Affected software: Wirtualna Uczelnia, endpoint `redirectToUrl`, parameter `redirectUrlParameter`.
- Exploit availability: No public PoC validated during this run.
- Active exploitation: Not observed.
- Recommended action: Apply vendor/CERT.PL remediation, restrict access to affected endpoints until patched, and review application logs for template-injection payloads.
- Confidence: High for disclosure, Low for exploitation.

### 9. CVE-2026-8206 - Kirki WordPress privilege escalation/account takeover

- Severity: Critical, CVSS 9.8.
- Affected software: Kirki plugin versions 6.0.0 through 6.0.6.
- Exploit availability: Recently created GitHub repository `Jenderal92/CVE-2026-8206` claims a mass exploitation tool; not validated and should be treated as potentially malicious.
- Active exploitation: Not confirmed by primary sources in this run.
- Recommended action: Update Kirki, audit password-reset and administrator-account events, and block suspicious requests to the affected forgot-password handler.
- Confidence: High for disclosure, Low for GitHub exploit validity.

### 10. CVE-2026-3055 - Citrix NetScaler ADC/Gateway memory overread

- Severity: Critical, CVSS v4.0 9.3 in secondary/vendor-linked reporting.
- Affected software: Customer-managed NetScaler ADC/Gateway configured as a SAML IdP; affected versions before 14.1-60.58/14.1-66.59, 13.1-62.23, and 13.1-FIPS/NDcPP 13.1-37.262.
- Exploit availability: Public technical analysis exists; public exploit functionality was not validated in this run.
- Active exploitation: Medium to High confidence. Citrix primary advisory confirms affected versions and fixes; secondary reporting and Fortinet-linked reporting claim exploitation.
- Recommended action: Patch customer-managed appliances, check for `add authentication samlIdPProfile`, rotate session/admin credentials after suspected exposure, and inspect for abnormal SAML/WS-Fed requests.
- Confidence: Medium.

### 11. CVE-2026-42945 and CVE-2026-9256 - NGINX rewrite-module heap buffer overflows

- Severity: Critical by CVSS v4 and infrastructure impact.
- Affected software: NGINX Open Source/Plus and downstream F5 NGINX products using vulnerable rewrite-module patterns.
- Exploit availability: CVE-2026-42945 has public GitHub technical material referenced by NVD; CVE-2026-9256 has public analysis but no validated exploit in this run.
- Active exploitation: Medium confidence. Active exploitation appears in secondary reporting; F5 primary advisory confirms vulnerability and fixes.
- Recommended action: Upgrade to fixed NGINX Open Source 1.30.2/1.31.1 or applicable NGINX Plus/F5 releases; replace unnamed PCRE captures such as `$1`/`$2` in rewrite rules where patching is delayed; ensure ASLR is enabled.
- Confidence: Medium.

## Exploits Released

### Sploitus Top 10 - reconstructed from indexed result pages

Static Sploitus homepage fetch did not expose the official "Exploits of the Week" list. These are the top 10 Sploitus-indexed entries observed from search results during this run.

| Rank | CVE | Affected software | Exploit type | Exploit maturity | Public PoC | Weaponization potential |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | CVE-2026-20182 | Cisco Catalyst SD-WAN Controller/Manager | Unauthenticated auth bypass, NETCONF/SSH access | PoC/exploit framework | Yes | Critical - perimeter/control-plane compromise |
| 2 | CVE-2026-20182 | Cisco Catalyst SD-WAN Controller/Manager | Assessment framework with bypass tiers | PoC/checker | Yes | Critical |
| 3 | CVE-2026-20182 | Cisco Catalyst SD-WAN Controller/Manager | Metasploit auxiliary indicator | Framework module indicator | Yes | Critical |
| 4 | CVE-2026-20182 | Cisco Catalyst SD-WAN Controller/Manager | Persistent SSH key/NETCONF manipulation | Weaponized description | Yes | Critical |
| 5 | CVE-2026-41940 | cPanel & WHM | CRLF auth bypass/RCE | Metasploit module indicator | Yes | Critical - root WHM access |
| 6 | CVE-2026-41940 | cPanel & WHM | Ransomware IOC pack and exploit analysis | Operational campaign analysis | Yes | Critical - known ransomware |
| 7 | CVE-2026-41940 | cPanel & WHM | `cPanelSniper` exploitation framework | Weaponized PoC indicator | Yes | Critical |
| 8 | CVE-2026-41940 | cPanel & WHM | Bulk scanner/post-exploitation toolkit | Weaponized PoC indicator | Yes | Critical |
| 9 | CVE-2026-41940 | cPanel & WHM | French-language auth bypass exploit writeup | PoC indicator | Yes | Critical |
| 10 | CVE-2026-21858 | n8n | Content-type confusion to file read/session forgery/RCE | Reconstruction/exploit code indicator | Yes | High to Critical |

### ExploitDB additions

Direct ExploitDB CSV fetch showed the latest entries as:

- EDB-ID 52608, 2026-06-01: Drupal Core 10.5.5 error-based SQL injection, CVE-2026-9082.
- EDB-ID 52607, 2026-06-01: WordPress OrderConvo 14 path traversal, CVE-2025-10162.
- No 2026-06-02-dated ExploitDB entry was present in the CSV fetched during this run.

### New or recently pushed GitHub PoC indicators

Treat all repositories below as unvalidated and potentially malicious until reviewed in a sandbox.

- `0xABCD01/CVE-2026-41089` - Netlogon PoC claim; pushed 2026-06-02 08:30 UTC; 93 stars at query time.
- `DyniePro/CVE-2026-25643` - Frigate NVR RCE claim; pushed 2026-06-02 13:00 UTC.
- `Jenderal92/CVE-2026-8206` - Kirki mass exploitation tool claim; created 2026-06-02 10:53 UTC.
- `MrForkBomb/CIFSwitch-Checker-CVE-2026-46243` - Linux CIFSwitch exposure checker; created 2026-06-02 11:39 UTC.
- `Defacto-ridgepole254/CVE-2026-41940-Exploit-PoC` - cPanel/WHM auth bypass PoC claim; pushed 2026-06-02 09:32 UTC.
- `Dullpurple-sloop726/CVE-2026-31431-Linux-Copy-Fail` and `Liverwortenuresis371/copyfail-rs` - Linux Copy Fail LPE exploit/detector claims; pushed 2026-06-02.
- `Recorded-texteditor120/CVE-2026-31802` - npm tar path traversal PoC claim; pushed 2026-06-02.
- `Jumpthereness578/CVE-2026-2991` - KiviCare authentication bypass PoC claim; pushed 2026-06-02.
- Strict search for repositories created on 2026-06-02 matching `CVE-2026 PoC exploit` returned an empty result set; the above are from the broader pushed-on/after search.

## Malware Intelligence

### Red Hat Cloud Services npm package compromise / Miasma supply-chain worm

- Status: Active supply-chain incident in secondary reporting; Red Hat reportedly removed affected packages and described impact as limited to internal development tooling.
- Malware behavior: Mini Shai-Hulud-style worm/credential harvester targeting AWS, Azure, GCP, GitHub, npm, Vault, SSH, Kubernetes, and local secrets. Reports describe GitHub Actions propagation and trusted publishing/Sigstore abuse.
- Enterprise impact: CI/CD credential exposure, repository workflow tampering, cloud identity theft, and downstream build compromise.
- Recommended action: Identify installations of `@redhat-cloud-services/*` packages since 2026-06-01, reinstall with scripts disabled where possible, rotate CI/CD/cloud/npm/GitHub credentials, audit unexpected `.github/workflows` changes, and inspect package-lock/npm cache artifacts.
- Confidence: Medium. Multiple secondary sources agree; primary Red Hat/NPM advisory details should be monitored continuously.

### cPanel "Sorry" ransomware linked to CVE-2026-41940

- Status: CISA KEV marks known ransomware use for CVE-2026-41940.
- Malware behavior: Sploitus-indexed analysis describes a Linux Go encryptor using ChaCha20 and RSA-2048, `.sorry` extension, and Tox negotiation.
- Recommended action: Hunt for `.sorry` extensions, ransom notes named `README.md` in unusual web-hosting directories, suspicious WHM session files, and outbound Tox-related traffic.
- Confidence: High for KEV ransomware association, Medium for specific campaign details.

### VX-Underground

- GitHub activity: `vxunderground/MalwareSourceCode` latest pushed timestamp remains 2026-05-30 07:11 UTC; no new pushed malware-source repository updates were observed during this hour.
- Latest remembered item: `Python/Stealer.Python.GMBA.Manipulator.7z` added to MalwareSourceCode on 2026-05-30.
- Confidence: Medium. GitHub metadata was available; website/feed access was limited.

### Other ransomware/security research

- Microsoft Threat Intelligence research on "The Gentlemen" ransomware remains relevant: Go-based, Garble-obfuscated Windows RaaS with double-extortion behavior and self-propagation/lateral movement tradecraft.
- A public GitHub analysis repository for amateur Go ransomware using repeating-key XOR was observed in search results; useful for YARA/decryptor research, but not prioritized as enterprise-critical without broader campaign evidence.

## Security Releases and Vendor Advisories

- Microsoft: Defender engine/platform release notes list fixes for CVE-2026-41091, CVE-2026-45498, and CVE-2026-45584. Verify engine at least 1.1.26040.8 and platform at least 4.18.26040.7 where applicable. Netlogon CVE-2026-41089 remains patched through May 2026 updates per MSRC/NVD.
- Cisco: SD-WAN CVE-2026-20182 advisory includes limited-exploitation statement, fixed-release guidance, log retention, IOC checks, and TAC escalation guidance. Cisco Nexus BGP DoS CVE-2026-20171 and Cisco Unity Connection CVE-2026-20034/CVE-2026-20035 remain notable May advisories.
- Fortinet: No June 2 PSIRT release was identified. May 12 PSIRT items remain relevant, including FortiNDR SQL injection, FortiAP CLI command injection, and FortiAuthenticator improper access control CVE-2026-44277.
- Citrix/NetScaler: CTX696300 covers CVE-2026-3055/CVE-2026-4368 with fixed versions for affected customer-managed ADC/Gateway deployments.
- F5/NGINX: F5 advisory K000161019 confirms CVE-2026-42945 and fixed releases; secondary reporting covers CVE-2026-9256 follow-on fixes. Patch NGINX Open Source to 1.30.2/1.31.1 where applicable.
- GitHub/GitHub Advisory Database: Recent critical advisories include praisonai-platform CVE-2026-47413, Vitest CVE-2026-47428/CVE-2026-47429, and multiple high-severity praisonai-platform IDOR/authorization issues. Fixed versions are published in GHSA records.
- WordPress ecosystem: Patchstack/Wordfence disclosures dominate the 2026-06-02 CVE volume, including WP Job Portal CVE-2026-42684, Masteriyo LMS PRO CVE-2025-53209, Kirki CVE-2026-8206, and Slider Revolution CVE-2026-9048/CVE-2026-9050.

## Recommended Actions - Ranked

1. Emergency patch and hunt Cisco Catalyst SD-WAN Controller/Manager for CVE-2026-20182; treat internet-exposed control-plane systems as high risk.
2. Patch and hunt cPanel/WHM CVE-2026-41940, with ransomware triage for `.sorry` indicators and WHM session-file tampering.
3. Patch PAN-OS CVE-2026-0257 and Oracle WebLogic CVE-2024-21182 per KEV deadlines; verify perimeter exposure and authentication bypass conditions.
4. Validate Microsoft domain-controller patch posture for Netlogon CVE-2026-41089 and Defender engine/platform versions for CVE-2026-41091/CVE-2026-45498.
5. Patch or mitigate Citrix NetScaler CVE-2026-3055 where customer-managed appliances are configured as SAML IdP; rotate credentials after suspected memory disclosure.
6. Upgrade NGINX/F5 products for CVE-2026-42945/CVE-2026-9256 and replace vulnerable rewrite patterns where patching is delayed.
7. Address 2026-06-02 WordPress criticals: WP Job Portal CVE-2026-42684, Masteriyo LMS PRO CVE-2025-53209, Kirki CVE-2026-8206, and related high-severity Patchstack items.
8. For developer environments, prioritize Red Hat Cloud Services npm supply-chain response, Vitest critical advisories, praisonai-platform critical authorization flaws, and Cloud Foundry UAA CVE-2026-40965 private-key exposure.
9. Quarantine and analyze any downloaded GitHub PoC repositories before execution; never run recent CVE PoCs on production or analyst workstations.
10. Recheck Packet Storm and Sploitus manually if exploit-feed completeness is required for a formal daily brief, because both had static-fetch limitations in this run.

## Unified Vulnerability Records

```json
[
  {
    "cve": "CVE-2026-42684",
    "cvss": "9.3",
    "vendor": "Ahmad",
    "product": "WP Job Portal",
    "affected_versions": "through 2.5.1",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": false,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2026-42684", "https://patchstack.com/database/wordpress/plugin/wp-job-portal/vulnerability/wordpress-wp-job-portal-plugin-2-5-1-sql-injection-vulnerability"]
  },
  {
    "cve": "CVE-2025-53209",
    "cvss": "9.8",
    "vendor": "Themeisle",
    "product": "Masteriyo LMS PRO",
    "affected_versions": "through 2.20.0",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": false,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2025-53209", "https://patchstack.com/database/wordpress/plugin/learning-management-system-pro/vulnerability/wordpress-masteriyo-lms-pro-2-20-0-privilege-escalation-vulnerability"]
  },
  {
    "cve": "CVE-2026-34906",
    "cvss": "9.3",
    "vendor": "Simple / Wirtualna Uczelnia",
    "product": "Wirtualna Uczelnia",
    "affected_versions": "not specified in NVD summary",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2026-34906", "https://cert.pl/posts/2026/06/CVE-2026-34906"]
  },
  {
    "cve": "CVE-2026-8206",
    "cvss": "9.8",
    "vendor": "Kirki",
    "product": "Kirki WordPress plugin",
    "affected_versions": "6.0.0 through 6.0.6",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://github.com/Jenderal92/CVE-2026-8206"],
    "patch_available": true,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2026-8206", "https://www.wordfence.com/threat-intel/"]
  },
  {
    "cve": "CVE-2026-20182",
    "cvss": "10.0",
    "vendor": "Cisco",
    "product": "Catalyst SD-WAN Controller and Manager",
    "affected_versions": "pre-fixed releases listed by Cisco",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://sploitus.com/exploit?id=13DF22F3-E9C6-58EE-B458-EB585C4D715D", "https://sploitus.com/exploit?id=MSF%3AAUXILIARY-ADMIN-NETWORKING-CISCO_SDWAN_VHUB_AUTH_BYPASS-"],
    "patch_available": true,
    "sources": ["https://sec.cloudapps.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-sdwan-rpa2-v69WY2SW", "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"]
  },
  {
    "cve": "CVE-2026-41089",
    "cvss": "9.8",
    "vendor": "Microsoft",
    "product": "Windows Netlogon",
    "affected_versions": "Windows Server 2012 through 2025 ranges listed by NVD",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": false,
    "poc_links": ["https://github.com/0xABCD01/CVE-2026-41089"],
    "patch_available": true,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2026-41089", "https://msrc.microsoft.com/update-guide/vulnerability/CVE-2026-41089"]
  },
  {
    "cve": "CVE-2026-0257",
    "cvss": "not captured in this run",
    "vendor": "Palo Alto Networks",
    "product": "PAN-OS",
    "affected_versions": "see vendor advisory",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://security.paloaltonetworks.com/CVE-2026-0257", "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"]
  },
  {
    "cve": "CVE-2024-21182",
    "cvss": "not captured in this run",
    "vendor": "Oracle",
    "product": "WebLogic Server",
    "affected_versions": "see Oracle July 2024 CPU",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://www.oracle.com/security-alerts/cpujul2024.html", "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"]
  },
  {
    "cve": "CVE-2026-41940",
    "cvss": "9.8",
    "vendor": "WebPros",
    "product": "cPanel & WHM / WP2",
    "affected_versions": "pre-fixed cPanel supported branches",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://sploitus.com/exploit?id=MSF%3AEXPLOIT-MULTI-HTTP-CPANEL_WHM_AUTH_BYPASS_RCE-", "https://github.com/Defacto-ridgepole254/CVE-2026-41940-Exploit-PoC"],
    "patch_available": true,
    "sources": ["https://support.cpanel.net/hc/en-us/articles/40073787579671-cPanel-WHM-Security-Update-04-28-2026", "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"]
  },
  {
    "cve": "CVE-2026-3055",
    "cvss": "9.3",
    "vendor": "Cloud Software Group / Citrix",
    "product": "NetScaler ADC and NetScaler Gateway",
    "affected_versions": "14.1 before 14.1-60.58/14.1-66.59, 13.1 before 13.1-62.23, 13.1-FIPS/NDcPP before 13.1-37.262",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://support.citrix.com/external/article/CTX696300", "https://www.picussecurity.com/resource/blog/cve-2026-3055-cve-2026-4368-inside-the-netscaler-citrixbleed-3-memory-overread"]
  },
  {
    "cve": "CVE-2026-42945",
    "cvss": "9.2",
    "vendor": "F5 / NGINX",
    "product": "NGINX Open Source and NGINX Plus",
    "affected_versions": "NGINX OSS 1.0.0-1.30.0 and related NGINX Plus branches per F5",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": false,
    "poc_links": ["https://github.com/DepthFirstDisclosures/Nginx-Rift"],
    "patch_available": true,
    "sources": ["https://my.f5.com/manage/s/article/K000161019", "https://nvd.nist.gov/vuln/detail/CVE-2026-42945"]
  },
  {
    "cve": "CVE-2026-40965",
    "cvss": "10.0",
    "vendor": "Cloud Foundry",
    "product": "UAA",
    "affected_versions": "v76.12.0 through v78.12.0",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://www.cloudfoundry.org/blog/cve-2026-40965-uaa-ec-private-key-disclosure/", "https://nvd.nist.gov/vuln/detail/CVE-2026-40965"]
  },
  {
    "cve": "CVE-2026-47413",
    "cvss": "critical",
    "vendor": "praisonai",
    "product": "praisonai-platform",
    "affected_versions": "before 0.1.4",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://github.com/advisories/GHSA-8g2p-pqm3-fcfh"]
  },
  {
    "cve": "CVE-2026-47429",
    "cvss": "critical",
    "vendor": "Vitest",
    "product": "vitest",
    "affected_versions": "before 4.1.0",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://github.com/advisories/GHSA-5xrq-8626-4rwp"]
  }
]
```

## Primary Source Links

- NVD latest hour: https://services.nvd.nist.gov/rest/json/cves/2.0/?pubStartDate=2026-06-02T12:00:00.000&pubEndDate=2026-06-02T13:30:00.000
- NVD day-to-date: https://services.nvd.nist.gov/rest/json/cves/2.0/?pubStartDate=2026-06-02T00:00:00.000&pubEndDate=2026-06-02T13:30:00.000
- CISA KEV JSON: https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json
- Cisco SD-WAN advisory: https://sec.cloudapps.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-sdwan-rpa2-v69WY2SW
- Citrix NetScaler advisory: https://support.citrix.com/external/article/CTX696300
- F5 NGINX advisory: https://my.f5.com/manage/s/article/K000161019
- Microsoft Defender release notes: https://learn.microsoft.com/en-us/defender-endpoint/microsoft-defender-endpoint-releases
- GitHub Advisory Database API: https://api.github.com/advisories
- ExploitDB CSV: https://gitlab.com/exploit-database/exploitdb/-/raw/main/files_exploits.csv
- VX-Underground MalwareSourceCode: https://github.com/vxunderground/MalwareSourceCode
