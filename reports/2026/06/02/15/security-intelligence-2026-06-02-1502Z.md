# Security Intelligence Report - 2026-06-02 15:02 UTC

## Executive Summary

- Reporting window: primary hourly window 2026-06-02 14:00-15:35 UTC, with day-to-date and rolling 24-hour enrichment.
- NVD new CVEs, latest hourly window: 27 total - 2 critical, 13 high, 9 medium, 0 low, 3 unknown.
- NVD new CVEs, day-to-date: 93 total - 6 critical, 25 high, 41 medium, 15 low, 6 unknown.
- NVD new CVEs, rolling 24 hours: 325 total - 18 critical, 118 high, 124 medium, 47 low, 18 unknown.
- Critical findings requiring review: Collibra Agent CVE-2026-10621/CVE-2026-10622 unauthenticated RCE chain, Progress Sitefinity CVE-2026-7312/CVE-2026-7198 critical OData flaws, Cisco SD-WAN CVE-2026-20182, Microsoft Netlogon CVE-2026-41089, Palo Alto Networks PAN-OS CVE-2026-0257, Fortinet FortiClient EMS CVE-2026-35616, Drupal CVE-2026-9082, Oracle WebLogic CVE-2024-21182, and Red Hat npm/Miasma supply-chain compromise.
- Active exploitation findings: Cisco confirms limited exploitation of CVE-2026-20182; Palo Alto marks CVE-2026-0257 exploit maturity as ATTACKED and CISA KEV-listed; Fortinet confirms exploitation of CVE-2026-35616 and Arctic Wolf reports EKZ Infostealer delivery; CISA KEV lists Oracle WebLogic CVE-2024-21182, Drupal CVE-2026-9082, and Cisco SD-WAN CVE-2026-20182; Belgian CCB reports active exploitation of Microsoft Netlogon CVE-2026-41089, but it was not present in the fetched CISA KEV feed.
- New malware/campaign intelligence: EKZ Infostealer campaign abuses FortiClient EMS management workflows to push fake Fortinet update payloads; Miasma compromised at least 32 `@redhat-cloud-services` npm packages with valid SLSA provenance and credential-stealing, self-propagating preinstall payloads. VX-Underground GitHub repositories showed no new pushed malware-source update after 2026-05-30.
- Important security releases/advisories: Progress Sitefinity 15.4.8630/15.3.8531/15.2.8441/15.1.8335/15.0.8234/14.4.8152/13.3.7652; Collibra Platform Agent fixed SaaS/self-hosted releases; MISP commit for OTP enforcement under LDAP mixed auth; GitLab 19.0.1/18.11.4/18.10.7 remains current; FortiClient EMS hotfix/7.4.7 guidance; Cisco SD-WAN fixed releases and IOC guidance.

## Source Coverage and Access Notes

- NVD API fetched successfully for 2026-06-02 14:00-15:35 UTC, 2026-06-02 day-to-date, and rolling 24 hours.
- CISA KEV JSON feed fetched successfully: catalogVersion 2026.06.01, 1608 entries. No new 2026-06-02 KEV addition was observed in the fetched feed.
- GitHub Advisory Database and repository searches were fetched through authenticated GitHub API.
- GitHub strict repository search for `CVE-2026 PoC exploit created:>=2026-06-02` returned no results; broader pushed-on/after searches found several unvalidated exploit indicators.
- ExploitDB CSV was fetched from the Exploit Database GitLab mirror and sorted by publication/addition date. Latest direct rows remained 2026-06-01 Drupal CVE-2026-9082 and WordPress OrderConvo CVE-2025-10162.
- Sploitus homepage static fetch did not expose an official "Exploits of the Week" block. The Sploitus Top 10 section below is reconstructed from indexed Sploitus result pages and current corroborating exploit searches, not an official homepage extraction.
- Packet Storm direct access was not relied on because prior runs encountered anti-abuse blocking from this environment.
- VX-Underground web/GitHub checks used `vxunderground` GitHub metadata. MalwareSourceCode latest pushed commit remained 2026-05-30.
- MalwareBazaar public site was reachable as an overview page; API access in prior runs returned 401 without credentials, so abuse.ch/MalwareBazaar references are treated as public context only.
- Search snippets sometimes conflicted with fresh NVD data. Primary/vendor sources were preferred where available, notably Progress Community for Sitefinity and CERT/CC VU#873170 for Collibra.

## Top Vulnerabilities

### 1. CVE-2026-10621 and CVE-2026-10622 - Collibra Agent unauthenticated RCE chain

- Severity: Critical by impact and prioritization. NVD scoring was still unknown at collection time, but CERT/CC describes a remote unauthenticated chain to remote code execution.
- Affected software: Collibra Platform Agent in Collibra Platform and Collibra Platform Self-Hosted.
- Affected versions: Fixed SaaS releases listed by CERT/CC are 2026.05, 2026.04.5, 2026.03.4, 2026.02.6, 2025.11.7, and 2025.10.9. Fixed self-hosted releases are 2026.03 build 2026.03.356 and 2025.10 build 2025.10.399.
- Vulnerability details: CVE-2026-10622 exposes privileged `/rest/*` endpoints without proper authentication/authorization; CVE-2026-10621 is a Zip Slip path traversal in `POST /rest/restore`. CERT/CC states attackers can chain them to write attacker-controlled files, including JSP web shells, to arbitrary locations.
- Exploit availability: No standalone public exploit repository was validated this hour, but the public CERT/CC advisory includes enough chain detail to raise weaponization risk.
- Active exploitation: Not observed in primary sources during this run.
- Recommended action: Patch Collibra Agent immediately, restrict Agent REST/management interfaces to trusted networks, review web-accessible directories for unexpected JSP/files, and hunt for ZIP restore activity from untrusted sources.
- Confidence: High for disclosure and impact; Low for active exploitation.

### 2. CVE-2026-7312 and CVE-2026-7198 - Progress Sitefinity critical OData web-service flaws

- Severity: Critical. CVE-2026-7312 has CVSS 10.0; CVE-2026-7198 has CVSS 9.8.
- Affected software: Progress Sitefinity CMS and Sitefinity Insight, versions 8.x through 15.x depending on CVE and configuration.
- Affected versions and fixes: Progress advises updating to supported product updates 15.4.8630, 15.3.8531, 15.2.8441, 15.1.8335, 15.0.8234, 14.4.8152, or 13.3.7652; latest version at advisory release was 15.4.8631.
- Vulnerability details: CVE-2026-7312 is insufficiently protected credentials in OData Web Services; CVE-2026-7198 is improper access control in OData Web Services that may allow unauthenticated access to restricted content with full confidentiality, integrity, and availability impact.
- Related Sitefinity high-severity CVEs: CVE-2026-7195 (improper input validation, CVSS 8.8), CVE-2026-7201 (authorization bypass through user-controlled key, CVSS 8.8), and CVE-2026-7313 (ServiceStack credential exposure, CVSS 8.7).
- Exploit availability: No public exploit or PoC was validated during this run.
- Active exploitation: Not observed.
- Recommended action: Inventory internet-facing Sitefinity and Sitefinity Cloud deployments, apply vendor updates, restrict unauthenticated OData exposure where possible, and review logs for abnormal OData access to restricted content and credential-bearing resources.
- Confidence: High for vendor disclosure and fixes; Low for exploitation.

### 3. CVE-2026-20182 - Cisco Catalyst SD-WAN Controller/Manager authentication bypass

- Severity: Critical, CVSS 10.0; CISA KEV listed.
- Affected software: Cisco Catalyst SD-WAN Controller (formerly vSmart) and Cisco Catalyst SD-WAN Manager (formerly vManage).
- Exploit availability: Sploitus-indexed exploit material and ProjectDiscovery nuclei-template release notes were observed. Search results also reference Metasploit/module indicators. Treat third-party exploit repositories as untrusted until sandboxed.
- Active exploitation: High confidence. Cisco PSIRT states it became aware of limited exploitation in May 2026.
- Recommended action: Patch to fixed Cisco releases, preserve admin-tech files before upgrades, run Cisco `show control connections` and history IOC checks, and open TAC cases for suspected compromise with CVE-2026-20182 in the title.
- Confidence: High.

### 4. CVE-2026-35616 - Fortinet FortiClient EMS authentication/authorization bypass

- Severity: Critical by exploitation and management-plane impact; NVD CVSS 9.1.
- Affected software: FortiClient EMS 7.4.5 through 7.4.6; FortiClient EMS 7.2 is not affected per Fortinet.
- Exploit availability: ProjectDiscovery nuclei template exists for detection; public exploitation details and Fortinet/Arctic Wolf reports are available.
- Active exploitation: High confidence. Fortinet observed exploitation in the wild, and Arctic Wolf observed the flaw being used to push EKZ Infostealer through FortiClient EMS-managed VPN scripting workflows.
- Recommended action: Apply Fortinet hotfixes or upgrade to FortiClient EMS 7.4.7 or later, restrict management port 8013 to trusted networks, audit EMS logs for `Certificate not found in request header` followed by unexpected `fortinet-ca2` updates, and inspect Remote Access Profile changes for unauthorized `on_connect` scripts.
- Confidence: High.

### 5. CVE-2026-41089 - Microsoft Windows Netlogon remote code execution

- Severity: Critical, CVSS 9.8 in NVD/MSRC.
- Affected software: Windows Server 2012 through 2025 domain controllers and affected Netlogon/MS-NRPC-exposed server builds.
- Exploit availability: GitHub PoC indicators remain present, including `0xABCD01/CVE-2026-41089`; functionality was not validated. Public reporting describes exploitability but no trusted exploit was executed or reviewed in this run.
- Active exploitation: Medium confidence. Belgian CCB states active exploitation as of its May 29 update, and SANS ISC Stormcast highlights Netlogon exploitation, but the fetched CISA KEV feed did not list this CVE.
- Recommended action: Apply May 2026 Microsoft cumulative updates to all domain controllers in coordinated maintenance windows, restrict Netlogon/RPC exposure, monitor for Netlogon crashes/restarts and anomalous MS-NRPC traffic from non-domain-controller hosts, and prepare AD incident response if suspicious traffic is found.
- Confidence: Medium for exploitation, High for severity and patch availability.

### 6. CVE-2026-0257 - Palo Alto Networks PAN-OS GlobalProtect authentication bypass

- Severity: High by vendor CVSS 7.8, Critical by prioritization due to active exploitation against perimeter VPN access; CISA KEV listed.
- Affected software: PAN-OS GlobalProtect portals/gateways and Prisma Access configurations where authentication override cookies are enabled and cookie certificates are reused with other features. Panorama and Cloud NGFW are not affected per Palo Alto.
- Exploit availability: Public PoC indicators exist in Rapid7/secondary reporting; no new repository was validated this hour.
- Active exploitation: High confidence. Palo Alto marks exploit maturity as ATTACKED and Rapid7 observed successful exploitation across customer environments.
- Recommended action: Upgrade to fixed PAN-OS/Prisma Access versions, disable authentication override if not required, generate a dedicated authentication-override certificate if the feature must remain enabled, and hunt for cookie authentication to local admin accounts, hostnames `GP-CLIENT`/`DESKTOP-GP01`, and spoofed MAC `aa:bb:cc:dd:ee:ff`.
- Confidence: High.

### 7. CVE-2026-9082 - Drupal Core PostgreSQL SQL injection

- Severity: Critical by CISA KEV and Drupal "Highly Critical" rating, despite differing NVD scoring in some views.
- Affected software: PostgreSQL-backed Drupal Core sites across 8.x through 11.3.9 branches; Drupal 7 not affected per public reporting.
- Exploit availability: High. ExploitDB EDB-ID 52608 was added 2026-06-01; Sploitus indexed multiple exploit pages; GitHub PoC indicators are present.
- Active exploitation: High confidence through CISA KEV and public active-exploitation reporting.
- Recommended action: Upgrade to fixed Drupal branches 11.3.10, 11.2.12, 11.1.10, 10.6.9, 10.5.10, or 10.4.10 as applicable; disable JSON:API as a temporary reduction for one exploit path; review logs for unexpected HTTP 500 responses on `/user/login` and `/jsonapi/` routes.
- Confidence: High.

### 8. CVE-2024-21182 - Oracle WebLogic Server vulnerability

- Severity: Critical by prioritization because CISA KEV added it on 2026-06-01 with due date 2026-06-04.
- Affected software: Oracle WebLogic Server, network access via T3/IIOP.
- Exploit availability: No new PoC was validated this hour.
- Active exploitation: High confidence due to CISA KEV listing.
- Recommended action: Apply Oracle CPU guidance immediately, restrict T3/IIOP exposure to trusted networks, and review WebLogic access/authentication logs for anomalous unauthenticated network activity.
- Confidence: High.

### 9. CVE-2026-10611 - MISP LDAP mixed-auth OTP bypass

- Severity: High, CVSS 8.2 in NVD.
- Affected software: MISP deployments using LDAP mixed authentication with OTP enforcement.
- Vulnerability details: A MISP commit on 2026-06-02 fixes a security issue where users authenticated by a plugin such as LDAP could establish a session during `beforeFilter` before `UsersController::login()` enforces OTP, allowing OTP bypass by browsing to another URL.
- Exploit availability: No weaponized PoC was validated; the commit clearly describes the bypass condition.
- Active exploitation: Not observed.
- Recommended action: Apply the MISP fix/release containing commit `39b3cb15aac4318afdd2ab63b96c2eac12b271fe`, review authentication plugin settings, and test that OTP challenge is enforced for LDAP/mixed-auth users before session establishment.
- Confidence: High for disclosure and patch; Low for exploitation.

### 10. CVE-2026-35717 - VIVOTEK FD8136 authenticated RCE research reference

- Severity: Unknown in NVD at collection time, but impact is potentially High/Critical where legacy devices remain reachable.
- Affected software: VIVOTEK FD8136 firmware FD8136-VVTK-0300a.
- Vulnerability details: NVD describes a stack-based buffer overflow in `export_language.cgi` that allows authenticated remote attackers to execute arbitrary code as root via crafted POST requests to `/cgi-bin/admin/export_language.cgi`.
- Exploit availability: Public GitHub research path `xchg-rax-rax/vulnerability-research/CVE-2026-35717` exists, but fetch only confirmed the repository/path, not exploit content. Treat as public research indicator, not validated weaponized code.
- Active exploitation: Not observed.
- Recommended action: Remove legacy cameras from untrusted networks, require VPN/management segmentation, verify firmware status with vendor guidance, and watch for POST requests to the affected endpoint.
- Confidence: Medium.

### 11. CVE-2026-9844 - Roche navify Digital Pathology default credentials

- Severity: High, CVSS 8.8.
- Affected software: Roche Diagnostics navify Digital Pathology from 2.0.0 before 2.4.1, RabbitMQ management interface modules.
- Exploit availability: No public PoC validated.
- Active exploitation: Not observed.
- Recommended action: Upgrade to 2.4.1 or later, rotate any exposed RabbitMQ/application credentials, and confirm management interfaces are not internet-facing.
- Confidence: High for disclosure, Low for exploitation.

### 12. Current-hour WordPress/Patchstack high-severity cluster

- Severity: High, mainly CVSS 8.1-8.8.
- Affected software: Askka theme CVE-2026-39555 PHP object injection, WaveRide CVE-2026-39553 local file inclusion, Blueprint CVE-2026-39552 local file inclusion, plus additional WordPress themes/plugins reported through Patchstack and NVD.
- Exploit availability: No validated PoC was found this hour.
- Active exploitation: Not observed.
- Recommended action: Run WordPress asset inventory for affected commercial themes/plugins, disable affected components if no fixed release is available, and monitor logs for file-inclusion and serialized-object payloads.
- Confidence: Medium to High for disclosure, Low for exploitation.

## Exploits Released

### Sploitus Top 10 - reconstructed from indexed result pages

Static Sploitus homepage access did not expose the official "Exploits of the Week" list in this environment. The following captures top exploit indicators from indexed Sploitus pages and current corroborating searches.

| Rank | CVE | Affected software | Exploit type | Exploit maturity | Public PoC | Weaponization potential |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | CVE-2026-20182 | Cisco Catalyst SD-WAN Controller/Manager | Unauthenticated control-plane authentication bypass | Sploitus-indexed PoC/framework indicator | Yes | Critical - SD-WAN fabric control |
| 2 | CVE-2026-9082 | Drupal Core with PostgreSQL | Unauthenticated SQL injection / mass scanner | ExploitDB and Sploitus-indexed exploit | Yes | Critical - database dump and possible RCE in some configurations |
| 3 | CVE-2026-0257 | PAN-OS GlobalProtect | Authentication-cookie forgery / VPN auth bypass | Attacked; public PoC indicators | Yes, unvalidated | Critical - perimeter VPN initial access |
| 4 | CVE-2026-35616 | FortiClient EMS | API auth bypass / management-plane command execution | In-the-wild exploitation; nuclei detection template | Detection template; exploitation observed | Critical - fleet-wide endpoint execution |
| 5 | CVE-2026-41940 | cPanel and WHM | Authentication bypass | Recently pushed GitHub PoC claim | Yes, unvalidated | Critical - hosting control-plane compromise |
| 6 | CVE-2026-41089 | Windows Netlogon | Unauthenticated network RCE | GitHub PoC indicators; CCB active exploitation warning | Yes, unvalidated | Critical - domain controller compromise |
| 7 | CVE-2026-31431 | Linux Copy Fail | Local privilege escalation / page-cache write | Recently pushed GitHub PoC claims | Yes, unvalidated | High |
| 8 | CVE-2026-31802 | npm tar | Path traversal / arbitrary overwrite | Recently pushed GitHub PoC claim | Yes, unvalidated | High in build environments |
| 9 | CVE-2026-21858 | n8n | Content-type confusion to file read, session forgery, RCE | Sploitus-indexed reconstruction/exploit indicator | Yes | High to Critical |
| 10 | CVE-2026-35717 | VIVOTEK FD8136 | Authenticated stack overflow / root RCE | GitHub research indicator | Unvalidated | High where exposed |

### ExploitDB additions

Direct ExploitDB CSV fetch sorted by date showed:

- EDB-ID 52608, 2026-06-01: Drupal Core 10.5.5 error-based SQL injection, CVE-2026-9082.
- EDB-ID 52607, 2026-06-01: WordPress OrderConvo 14 path traversal, CVE-2025-10162.
- EDB-ID 52606, 2026-05-30: Notepad++ 8.9.6 arbitrary code execution, CVE-2026-48778.
- EDB-ID 52605 through 52603, 2026-05-30: YAMCS 5.12.7 no rate limiting, user enumeration, and LDAP injection.
- No 2026-06-02-dated ExploitDB row was present in the fetched CSV.

### New or recently pushed GitHub PoC indicators

Treat all repositories below as unvalidated and potentially malicious until reviewed in a sandbox.

- `Defacto-ridgepole254/CVE-2026-41940-Exploit-PoC` - cPanel/WHM authentication bypass PoC claim; pushed 2026-06-02 13:39 UTC.
- `Dullpurple-sloop726/CVE-2026-31431-Linux-Copy-Fail` - Linux Copy Fail LPE exploit claim; pushed 2026-06-02 13:38 UTC.
- `Liverwortenuresis371/copyfail-rs` - Linux Copy Fail detector/exploit claim; pushed 2026-06-02 13:37 UTC.
- `Jumpthereness578/CVE-2026-2991` - KiviCare auth bypass PoC claim; pushed 2026-06-02 13:18 UTC.
- `Recorded-texteditor120/CVE-2026-31802` - npm tar symlink/path traversal PoC claim; pushed 2026-06-02 13:15 UTC.
- `fartlover37/CVE-2026-2441-PoC` - Chrome Blink UAF PoC claim; pushed 2026-06-02 12:56 UTC.
- `hamzamalik3461/CVE-2026-20841` - Windows Notepad RCE claim; pushed 2026-06-02 12:54 UTC.
- `0xABCD01/CVE-2026-41089` - Netlogon PoC claim; created 2026-06-01 and pushed 2026-06-02 08:30 UTC, 99 stars at collection time.
- Strict `created:>=2026-06-02` search for `CVE-2026 PoC exploit` returned no repositories.

## Malware Intelligence

### VX-Underground

- GitHub user repository metadata showed `vxunderground/MalwareSourceCode` as the most recently pushed VX repository, pushed 2026-05-30 and updated 2026-06-02 metadata-side.
- Latest visible MalwareSourceCode commit remained `1623926` on 2026-05-30 with message "Add files via upload". Prior memory identifies the added archive as `Python/Stealer.Python.GMBA.Manipulator.7z`.
- No new pushed malware-source update was observed after the previous hourly run.

### EKZ Infostealer via FortiClient EMS

- Arctic Wolf reports threat actors exploiting FortiClient EMS CVE-2026-35616 to alter FortiClient-managed VPN profiles and execute malicious scripts across managed endpoints.
- Payload: EKZ Infostealer, delivered as `FortiEndpoint_Patch.exe` or `p.exe`, a MinGW-compiled Windows credential stealer.
- Capabilities: extracts credentials, cookies, and autofill data from Chromium-family and Firefox/Gecko-family browsers; stages output in `C:\ProgramData\log.txt`; exfiltrates via HTTP POST.
- Notable indicators from Arctic Wolf: payload host `83.138.53.110`, SHA-256 `0da123adf9251957a4b850a3f6bd6a753dd4892be176a84a18450e899534cc5e`, and suspicious process chain `fortitray.exe` or `ipsec.exe` -> `cmd.exe` -> `powershell.exe` -> `FortiEndpoint_Patch.exe`.
- Recommended defensive focus: FortiClient EMS management logs, Remote Access Profile changes, VPN on-connect script configuration, ProgramData credential-staging artifacts, and browser credential access from unexpected binaries.

### Miasma Red Hat npm supply-chain compromise

- Wiz and Snyk report that at least 32 `@redhat-cloud-services` package releases were compromised on 2026-06-01, with about 80,000 combined weekly downloads.
- Root cause: a compromised Red Hat employee GitHub account pushed malicious orphan commits to RedHatInsights repositories, adding workflows with `id-token: write` that published packages to npm with valid SLSA provenance attestations.
- Payload behavior: npm `preinstall` hook executes an obfuscated JavaScript payload derived from Mini Shai-Hulud/TeamPCP tradecraft, harvests developer secrets, enumerates GCP/Azure identities, and attempts self-propagation to packages the victim can publish.
- Hunting indicators: GitHub repositories with description `Miasma: The Spreading Blight`; unexpected workflows requesting `id-token: write`; affected `@redhat-cloud-services` versions in lockfiles; new npm/GitHub/cloud tokens; anomalous GCP/Azure identity metadata queries.
- Recommended action: pin away from affected versions, reinstall with scripts disabled, clean hosts before rotating credentials, rotate npm/GitHub/SSH/cloud credentials exposed to affected workstations or CI runners, and scope OIDC trust to specific protected workflows/branches.

### Ransomware and incident reporting

- The DFIR Report ransomware archive showed no new June 2 public ransomware report; the latest listed ransomware flash alert remained "EtherRat and TukTuk C2 End in The Gentleman Ransomware" from 2026-05-11.
- CISA KEV indicates known ransomware use for Nx Console CVE-2026-48027 and TanStack CVE-2026-45321 supply-chain entries, carried forward from previous reporting.
- FortiClient EMS/EKZ is credential theft rather than ransomware in the observed campaign, but credential theft from centralized management planes materially increases ransomware staging risk.

## Security Releases and Vendor Advisories

### Microsoft

- May 2026 Patch Tuesday remains urgent for CVE-2026-41089 Netlogon. NVD references Microsoft MSRC and affected Windows Server 2012 through 2025 version ranges.
- CCB Belgium updated its Microsoft advisory on 2026-05-29 to state CVE-2026-41089 is actively exploited in the wild.
- Action: prioritize all domain controllers and Tier 0 Windows servers; avoid half-patched AD forests.

### Cisco

- Cisco advisory `cisco-sa-sdwan-rpa2-v69WY2SW` for CVE-2026-20182 remains top priority.
- Cisco states there are no workarounds and confirms limited exploitation in May 2026.
- Action: upgrade, collect admin-tech before changes, and run Cisco control-connection IOC checks.

### Fortinet

- Fortinet PSIRT FG-IR-26-099 confirms CVE-2026-35616 exploitation in the wild and urges hotfixes for FortiClient EMS 7.4.5/7.4.6 or upgrade to 7.4.7+.
- FortiClient Cloud and FortiSASE were remediated by Fortinet.

### Palo Alto Networks

- Palo Alto advisory CVE-2026-0257 updated 2026-05-29: exploit maturity ATTACKED, urgency HIGHEST.
- Action: patch PAN-OS/Prisma Access, disable authentication override where possible, and use a dedicated cookie certificate if retained.

### Progress

- Progress published the Sitefinity May 2026 multi-CVE advisory on 2026-06-02.
- Fixes are available for supported Sitefinity versions; non-supported versions should upgrade.

### Collibra

- CERT/CC VU#873170 published 2026-06-02 for Collibra Agent CVE-2026-10621/CVE-2026-10622.
- Action: update Agent releases and restrict exposed management interfaces.

### GitLab and GitHub

- GitLab 19.0.1, 18.11.4, and 18.10.7 patch release from 2026-05-27 remains current; most severe issue in that release is CVE-2026-4868 Duo AI workflow runner improper access control, CVSS 8.2.
- GitHub Advisory Database latest reviewed advisories in the collection include `praisonai-platform` critical/high multi-tenant authorization issues (CVE-2026-47413, CVE-2026-47415, CVE-2026-47412), Vitest browser/UI critical issues (CVE-2026-47428, CVE-2026-47429), DOMPurify XSS CVE-2026-47423, and kas SHA-like branch checkout integrity issue CVE-2026-47191.

### VMware/Broadcom

- No new VMware/Broadcom exploited advisory was found for 2026-06-02 in current searches.
- Carry-forward: VMware Aria Operations CVE-2026-22719 remains a historical KEV item; Broadcom guidance on Dirty Frag/Fragnesia explains Photon OS appliances are generally not affected, while VKS Ubuntu nodes may need mitigations.

## Unified Vulnerability Records

```json
[
  {
    "cve": "CVE-2026-10621",
    "cvss": "Unknown at collection time",
    "vendor": "Collibra",
    "product": "Collibra Agent",
    "affected_versions": "Fixed in Collibra Platform SaaS 2026.05/2026.04.5/2026.03.4/2026.02.6/2025.11.7/2025.10.9 and Self-Hosted 2026.03 build 2026.03.356 or 2025.10 build 2025.10.399",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://kb.cert.org/vuls/id/873170", "https://nvd.nist.gov/vuln/detail/CVE-2026-10621"]
  },
  {
    "cve": "CVE-2026-10622",
    "cvss": "Unknown at collection time",
    "vendor": "Collibra",
    "product": "Collibra Agent",
    "affected_versions": "Fixed in Collibra Platform SaaS 2026.05/2026.04.5/2026.03.4/2026.02.6/2025.11.7/2025.10.9 and Self-Hosted 2026.03 build 2026.03.356 or 2025.10 build 2025.10.399",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://kb.cert.org/vuls/id/873170", "https://nvd.nist.gov/vuln/detail/CVE-2026-10622"]
  },
  {
    "cve": "CVE-2026-7312",
    "cvss": "10.0",
    "vendor": "Progress",
    "product": "Sitefinity CMS / Sitefinity Insight",
    "affected_versions": "14.0.7700-14.4.8151, 15.0.8200-15.0.8233, 15.1.8300-15.1.8334, 15.2.8400-15.2.8440, 15.3.8500-15.3.8530, 15.4.8600-15.4.8629",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://community.progress.com/s/article/Sitefinity-Security-Advisory-for-Addressing-Security-Vulnerabilities-CVE-2026-7312-CVE-2026-7198-CVE-2026-7195-CVE-2026-7201-CVE-2026-7313-May-2026", "https://nvd.nist.gov/vuln/detail/CVE-2026-7312"]
  },
  {
    "cve": "CVE-2026-7198",
    "cvss": "9.8",
    "vendor": "Progress",
    "product": "Sitefinity CMS",
    "affected_versions": "Sitefinity 15.4.8623 before 15.4.8630",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://community.progress.com/s/article/Sitefinity-Security-Advisory-for-Addressing-Security-Vulnerabilities-CVE-2026-7312-CVE-2026-7198-CVE-2026-7195-CVE-2026-7201-CVE-2026-7313-May-2026", "https://nvd.nist.gov/vuln/detail/CVE-2026-7198"]
  },
  {
    "cve": "CVE-2026-20182",
    "cvss": "10.0",
    "vendor": "Cisco",
    "product": "Catalyst SD-WAN Controller and Manager",
    "affected_versions": "See Cisco advisory fixed-release matrix",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://sploitus.com/exploit?id=13DF22F3-E9C6-58EE-B458-EB585C4D715D"],
    "patch_available": true,
    "sources": ["https://www.cisco.com/c/en/us/support/docs/csa/cisco-sa-sdwan-rpa2-v69WY2SW.html", "https://www.cisa.gov/known-exploited-vulnerabilities-catalog"]
  },
  {
    "cve": "CVE-2026-35616",
    "cvss": "9.1",
    "vendor": "Fortinet",
    "product": "FortiClient EMS",
    "affected_versions": "FortiClient EMS 7.4.5 through 7.4.6",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://github.com/projectdiscovery/nuclei-templates/releases"],
    "patch_available": true,
    "sources": ["https://fortiguard.fortinet.com/psirt/FG-IR-26-099", "https://arcticwolf.com/resources/blog/forticlient-ems-exploited-via-cve-2026-35616-to-deliver-ekz-infostealer-disguised-as-a-fortinet-patch/"]
  },
  {
    "cve": "CVE-2026-41089",
    "cvss": "9.8",
    "vendor": "Microsoft",
    "product": "Windows Netlogon",
    "affected_versions": "Windows Server 2012 through 2025 version ranges listed by NVD/MSRC",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": false,
    "poc_links": ["https://github.com/0xABCD01/CVE-2026-41089"],
    "patch_available": true,
    "sources": ["https://msrc.microsoft.com/update-guide/vulnerability/CVE-2026-41089", "https://ccb.belgium.be/advisories/warning-microsoft-patch-tuesday-may-2026-patches-118-vulnerabilities-16-critical-102", "https://isc.sans.edu/"]
  },
  {
    "cve": "CVE-2026-0257",
    "cvss": "7.8",
    "vendor": "Palo Alto Networks",
    "product": "PAN-OS GlobalProtect",
    "affected_versions": "GlobalProtect portal/gateway configurations with authentication override cookies and certificate reuse; see Palo Alto fixed-version matrix",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://security.paloaltonetworks.com/CVE-2026-0257", "https://www.rapid7.com/blog/post/etr-rapid7-observed-exploitation-of-pan-os-globalprotect-authentication-bypass-vulnerability-cve-2026-0257/"]
  },
  {
    "cve": "CVE-2026-9082",
    "cvss": "Drupal Highly Critical; NVD values vary by source",
    "vendor": "Drupal",
    "product": "Drupal Core",
    "affected_versions": "PostgreSQL-backed Drupal 8.x through 11.3.9 branches",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://sploitus.com/exploit?id=1774D6F8-2B0F-5C66-A7AB-BE7B8E7A0B85", "https://www.exploit-db.com/exploits/52608"],
    "patch_available": true,
    "sources": ["https://www.drupal.org/sa-core-2026-004", "https://www.cisa.gov/known-exploited-vulnerabilities-catalog"]
  },
  {
    "cve": "CVE-2024-21182",
    "cvss": "Unknown in KEV feed; critical by KEV and unauthenticated WebLogic impact",
    "vendor": "Oracle",
    "product": "WebLogic Server",
    "affected_versions": "See Oracle July 2024 CPU",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://www.oracle.com/security-alerts/cpujul2024.html", "https://www.cisa.gov/known-exploited-vulnerabilities-catalog"]
  },
  {
    "cve": "CVE-2026-10611",
    "cvss": "8.2",
    "vendor": "MISP",
    "product": "MISP",
    "affected_versions": "LDAP mixed-auth deployments before commit 39b3cb15aac4318afdd2ab63b96c2eac12b271fe or containing release",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://github.com/MISP/MISP/commit/39b3cb15aac4318afdd2ab63b96c2eac12b271fe", "https://nvd.nist.gov/vuln/detail/CVE-2026-10611"]
  },
  {
    "cve": "CVE-2026-35717",
    "cvss": "Unknown at collection time",
    "vendor": "VIVOTEK",
    "product": "FD8136 firmware",
    "affected_versions": "FD8136-VVTK-0300a",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://github.com/xchg-rax-rax/vulnerability-research/tree/main/CVE-2026-35717"],
    "patch_available": false,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2026-35717", "https://github.com/xchg-rax-rax/vulnerability-research/tree/main/CVE-2026-35717"]
  },
  {
    "cve": "CVE-2026-9844",
    "cvss": "8.8",
    "vendor": "Roche Diagnostics",
    "product": "navify Digital Pathology",
    "affected_versions": "2.0.0 before 2.4.1",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://diagnostics.roche.com/global/en/legal/product-security-advisory.html", "https://nvd.nist.gov/vuln/detail/CVE-2026-9844"]
  },
  {
    "cve": "CVE-2026-39555",
    "cvss": "8.1",
    "vendor": "Elated-Themes",
    "product": "Askka WordPress theme",
    "affected_versions": "Through 1.3.1",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": false,
    "sources": ["https://patchstack.com/database/wordpress/theme/askka/vulnerability/wordpress-askka-theme-1-3-1-php-object-injection-vulnerability?_s_id=cve", "https://nvd.nist.gov/vuln/detail/CVE-2026-39555"]
  }
]
```

## Recommended Actions

1. Emergency patch or isolate Collibra Agent instances: prioritize any Agent REST interface reachable from untrusted networks, then hunt for arbitrary file writes/JSP web shells.
2. Patch Progress Sitefinity immediately: deploy vendor updates for all supported branches and restrict unauthenticated OData exposure until patched.
3. Complete Cisco SD-WAN CVE-2026-20182 remediation: upgrade to fixed releases, collect forensic bundles, and run Cisco IOC checks before and after upgrades.
4. Patch FortiClient EMS and hunt EKZ: apply hotfix/7.4.7+, restrict port 8013, inspect Remote Access Profiles, and sweep endpoints for `FortiEndpoint_Patch.exe`, `C:\ProgramData\log.txt`, and suspicious FortiClient-spawned PowerShell.
5. Patch Windows domain controllers for CVE-2026-41089: coordinate all-domain-controller patching, restrict Netlogon/RPC exposure, and monitor for anomalous MS-NRPC traffic and service instability.
6. Patch and mitigate PAN-OS GlobalProtect CVE-2026-0257: disable auth override where possible or use a dedicated certificate, then review VPN logs for known IOCs.
7. Patch Drupal PostgreSQL-backed sites for CVE-2026-9082: apply fixed branches and review `/user/login` and `/jsonapi/` logs for SQLi probes.
8. Treat Miasma as an active supply-chain incident: find affected `@redhat-cloud-services` lockfile versions, rebuild with scripts disabled, clean developer/CI hosts, rotate exposed credentials, and review GitHub Actions OIDC trust.
9. Apply Oracle WebLogic CVE-2024-21182 guidance before the CISA 2026-06-04 deadline and restrict T3/IIOP exposure.
10. Review current-hour high/unknown CVEs for exposure: MISP LDAP mixed auth, Roche navify, VIVOTEK FD8136, Gleam path traversal/package export issues, Siemens RUGGEDCOM, and WordPress theme/plugin LFI/object-injection issues.

## Confidence Summary

- High confidence: NVD counts, CISA KEV feed version/count, Progress Sitefinity advisory, CERT/CC Collibra advisory, Fortinet and Palo Alto exploitation status, Cisco limited exploitation, GitHub advisory metadata, ExploitDB CSV latest entries, Wiz/Snyk Miasma details, Arctic Wolf EKZ details.
- Medium confidence: Microsoft Netlogon active exploitation status, because CCB/SANS/secondary reporting corroborates exploitation but the fetched CISA KEV feed does not list CVE-2026-41089.
- Low confidence: Functionality or safety of individual GitHub PoC repositories, Sploitus "Top 10" ordering, and exploitation status for current-hour CVEs without primary exploitation reports.
