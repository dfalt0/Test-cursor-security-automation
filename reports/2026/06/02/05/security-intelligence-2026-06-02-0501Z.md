# Security Intelligence Report - 2026-06-02 05:01 UTC

Report window: 2026-06-02 04:00-05:35 UTC, with 24-hour enrichment back to 2026-06-01 05:35 UTC.

Repository: `dfalt0/Test-cursor-security-automation`

## Executive Summary

- Total CVEs discovered in NVD during this hour: 4 (1 critical, 3 medium).
- Total CVEs discovered in NVD since 00:00 UTC: 24 (1 critical, 17 medium, 5 low, 1 unknown).
- Total CVEs discovered in NVD over the last 24 hours: 369 (19 critical, 121 high, 150 medium, 36 low, 43 unknown).
- Critical newly published this hour: CVE-2026-8206, a WordPress Kirki plugin account-takeover vulnerability in versions 6.0.0-6.0.6.
- Active exploitation / KEV priorities:
  - CVE-2026-41089 - Microsoft Windows Netlogon RCE; CCB Belgium states active exploitation as of 2026-05-29.
  - CVE-2026-0257 - Palo Alto Networks PAN-OS GlobalProtect authentication bypass; Palo Alto rates exploit maturity as ATTACKED and CISA KEV lists it.
  - CVE-2026-20182 - Cisco Catalyst SD-WAN Controller/Manager authentication bypass; Cisco PSIRT confirms limited exploitation and CISA KEV lists it.
  - CVE-2026-9082 - Drupal Core PostgreSQL SQL injection; KEV-listed with public PoC material and ExploitDB/Sploitus coverage.
  - CVE-2024-21182 - Oracle WebLogic Server; newest CISA KEV addition, added 2026-06-01.
- Malware intelligence: VX-Underground's GitHub `MalwareSourceCode` repository remains the most recently updated VX repository observed, updated 2026-06-02 01:08 UTC and last pushed 2026-05-30; no new VX public ransomware report was confirmed during this run.
- Important security releases / advisories: Patchstack Kirki 6.0.7, Palo Alto PAN-OS hotfix trains, Cisco Catalyst SD-WAN fixed releases, Cloud Foundry UAA v78.13.0 / cf-deployment v56.1.0, IBM WebSphere interim fixes / fix packs, Drupal 10.4.10+ and 11.x fixed branches.

## Source Coverage and Caveats

- NVD API was queried for the hourly, day-to-date, and 24-hour windows.
- CISA KEV JSON feed was queried; catalog version observed: 2026.06.01, released 2026-06-01T16:59:32.7272Z, count 1608.
- Sploitus homepage was fetched, but it exposed only the search UI shell and did not expose a machine-readable or visible "Exploits of the Week" block. The Sploitus Top 10 below is therefore a best-effort reconstruction from indexed Sploitus exploit pages discovered through targeted search. Confidence for ordering is Low; confidence that the listed pages are Sploitus-indexed exploit indicators is Medium.
- GitHub repository search results are indicators only. No GitHub PoC was executed or functionally validated.
- Public PoC repositories can be malicious or misleading; treat them as indicators requiring sandbox review before use.

## Top Vulnerabilities

### 1. CVE-2026-41089 - Microsoft Windows Netlogon RCE

- Severity: Critical, CVSS 9.8.
- Affected software: Windows Server domain controllers, Windows Server 2012 onward per CCB summary.
- Exploit availability: Public GitHub PoC indicator observed (`0xABCD01/CVE-2026-41089`, created 2026-06-01, 48 stars at query time). Functionality unvalidated.
- Active exploitation: Yes, per CCB Belgium primary advisory update on 2026-05-29.
- Patch available: Yes, Microsoft May 2026 security updates.
- Recommended action: Emergency patch all domain controllers, restrict Netlogon/RPC exposure to trusted networks, and monitor Netlogon/LSASS crash or malformed RPC telemetry.
- Confidence: High for active exploitation and patch urgency; Medium for public PoC maturity.
- Sources: CCB Belgium, GitHub search, Microsoft MSRC reference via CCB.

### 2. CVE-2026-0257 - Palo Alto Networks PAN-OS GlobalProtect Authentication Bypass

- Severity: High by vendor CVSS-B 7.8, but operationally critical due to internet-facing VPN impact.
- Affected software: PAN-OS 10.2, 11.1, 11.2, 12.1 and Prisma Access versions with GlobalProtect authentication override cookies enabled and unsafe certificate reuse.
- Exploit availability: Rapid7 validated a proof-of-concept; public references exist. Treat as weaponized.
- Active exploitation: Yes. Palo Alto marks exploit maturity ATTACKED; CISA KEV lists it.
- Patch available: Yes. Fixed versions include PAN-OS 12.1.7 or 12.1.4-h6, 11.2.12 or branch hotfixes, 11.1.15 or branch hotfixes, 10.2.18-h6 / 10.2.16-h7 / 10.2.13-h21 / 10.2.10-h36 / 10.2.7-h34.
- Recommended action: Upgrade immediately, disable authentication override if not required, or dedicate a certificate exclusively to authentication override cookies.
- Confidence: High.
- Sources: Palo Alto advisory, CISA KEV, Rapid7 reporting.

### 3. CVE-2026-20182 - Cisco Catalyst SD-WAN Controller/Manager Authentication Bypass

- Severity: Critical, CVSS 10.0.
- Affected software: Cisco Catalyst SD-WAN Controller and Manager across deployment types.
- Exploit availability: Public exploit material and Rapid7 technical detail exist; Cisco provides IoC guidance.
- Active exploitation: Yes. Cisco PSIRT confirms limited exploitation; CISA KEV lists it.
- Patch available: Yes. Fixed releases include 20.9.9.1, 20.12.7.1 / 20.12.6.2 / 20.12.5.4, 20.15.5.2, 20.18.2.2, 26.1.1.1 depending on branch.
- Recommended action: Collect `admin-tech` before upgrade, upgrade control components, validate unauthorized peering events, and review `auth.log` for unexpected `vmanage-admin` public-key logins.
- Confidence: High.
- Sources: Cisco advisory, CISA KEV, Rapid7/Tenable reporting.

### 4. CVE-2026-8206 - WordPress Kirki Plugin Account Takeover

- Severity: Critical, CVSS 9.8.
- Affected software: Kirki - Freeform Page Builder, Website Builder & Customizer plugin versions 6.0.0-6.0.6.
- Exploit availability: GitHub PoC indicator observed (`O99099O/CVE-2026-8206-Poc-`, created 2026-06-01). Functionality unvalidated.
- Active exploitation: Not confirmed.
- Patch available: Yes, update to 6.0.7 or later.
- Recommended action: Update or temporarily disable the plugin, audit password reset events, and review for unexpected administrator account access.
- Confidence: High for vulnerability and patch; Low for PoC reliability; Low for exploitation status.
- Sources: NVD, Patchstack, WordPress plugin trac references, GitHub search.

### 5. CVE-2026-9082 - Drupal Core PostgreSQL SQL Injection

- Severity: NVD medium CVSS 6.5, Drupal "Highly Critical" 20/25 due to unauthenticated SQL injection and potential chained impact.
- Affected software: PostgreSQL-backed Drupal Core branches 8.9.0-10.4.9, 10.5.0-10.5.9, 10.6.0-10.6.8, 11.0.0-11.1.9, 11.2.0-11.2.11, 11.3.0-11.3.9.
- Exploit availability: Yes. ExploitDB entry 52608, multiple Sploitus-indexed PoC variants, and GitHub PoC indicators.
- Active exploitation: Yes by CISA KEV status and public reporting; KEV added 2026-05-22.
- Patch available: Yes, update to Drupal 10.4.10, 10.5.10, 10.6.9, 11.1.10, 11.2.12, 11.3.10 or later.
- Recommended action: Patch PostgreSQL-backed Drupal first; if delayed, disable JSON:API where possible, add WAF detections for PostgreSQL-specific payloads, and inspect logs for SQLSTATE errors and `/jsonapi` probes.
- Confidence: High for exploit availability and remediation; Medium for specific in-the-wild activity scale.
- Sources: Drupal/OSV, CISA KEV, ExploitDB, Sploitus, public research.

### 6. CVE-2024-21182 - Oracle WebLogic Server Unspecified Vulnerability

- Severity: Critical operational priority due to CISA KEV listing and unauthenticated network access via T3/IIOP.
- Affected software: Oracle WebLogic Server.
- Exploit availability: Not confirmed in this run.
- Active exploitation: Yes by KEV listing.
- Patch available: Yes, Oracle CPU guidance.
- Recommended action: Apply Oracle updates or mitigations immediately; restrict T3/IIOP exposure and review WebLogic logs for suspicious remote access.
- Confidence: High for KEV and urgency; Medium for exploit details because CISA describes the weakness as unspecified.
- Sources: CISA KEV JSON, Oracle CPU July 2024 reference.

### 7. CVE-2026-40965 - Cloud Foundry UAA EC Private Key Exposure

- Severity: Critical, CVSS 10.0.
- Affected software: uaa_release v76.12.0 through v78.12.0 and cf-deployment v30.0.0 through v56.0.0 when EC keys are used for JWT signing.
- Exploit availability: No public exploit validated, but exploitation is trivial if `/token_keys` is exposed and EC JWT signing is configured.
- Active exploitation: Not confirmed.
- Patch available: Yes, uaa_release v78.13.0 or cf-deployment v56.1.0 or later.
- Recommended action: Upgrade, rotate exposed EC signing keys, invalidate tokens, and verify no RSA-only deployments are misclassified.
- Confidence: High.
- Sources: Cloud Foundry advisory, GitHub Advisory Database, NVD.

### 8. CVE-2026-9319 / CVE-2026-9311 / CVE-2026-8644 - IBM WebSphere Application Server Critical Set

- Severity: Critical, CVSS 9.0-9.1.
- Affected software: IBM WebSphere Application Server 8.5 and 9.0.
- Exploit availability: No functional public exploit validated in this run.
- Active exploitation: Not confirmed.
- Patch available: IBM interim fixes are available; fix packs 9.0.5.29 and 8.5.5.30 are targeted in IBM guidance.
- Recommended action: Apply IBM interim fixes for the relevant APARs, prioritize internet-accessible JAX-WS/WS-Security endpoints, and restrict network exposure.
- Confidence: High for vulnerability details; Medium for patch timing because some fix packs are targeted availability.
- Sources: IBM support bulletins, GitHub Advisory Database, NVD.

### 9. CVE-2026-46243 - CIFSwitch Linux Local Privilege Escalation

- Severity: High operational priority where prerequisites align.
- Affected software: Linux systems with vulnerable kernel CIFS client, `cifs-utils` default `cifs.spnego` rule, loadable/built-in CIFS module, and unprivileged user/mount namespaces enabled.
- Exploit availability: Public PoC (`manizada/CIFSwitch`) reported by oss-security and indexed in public reporting.
- Active exploitation: Not confirmed.
- Patch available: Kernel-side fix commit `3da1fdf4efbc` queued/backported by distributions.
- Recommended action: Apply distribution kernel updates; if delayed, block CIFS module loading if unused, override the `cifs.spnego` request-key rule, or disable unprivileged user namespaces.
- Confidence: Medium-High.
- Sources: oss-security, seclists, BleepingComputer.

### 10. CVE-2026-43494 - PinTheft Linux Kernel Local Privilege Escalation

- Severity: High where RDS and io_uring prerequisites are exposed.
- Affected software: Linux kernels with RDS zerocopy refcount bug, RDS/RDS_TCP loadable or enabled, io_uring enabled, and suitable SUID target; PoC is x86_64-specific.
- Exploit availability: Public PoC from V12/security community and forks.
- Active exploitation: Not confirmed.
- Patch available: Upstream fix commit `e17492979319`; distribution updates pending/available depending on distro.
- Recommended action: Patch kernel; if delayed, unload/blacklist `rds` and `rds_tcp`, and disable io_uring where feasible.
- Confidence: Medium.
- Sources: V12 PoC, BleepingComputer, TuxCare, GitHub search.

## Newly Published NVD Records This Hour

| CVE | Severity | CVSS | Affected software | Exploit / public disclosure | Action |
| --- | --- | --- | --- | --- | --- |
| CVE-2026-8206 | Critical | 9.8 | WordPress Kirki 6.0.0-6.0.6 | GitHub PoC indicator; Patchstack advisory | Update to 6.0.7+ |
| CVE-2026-10581 | Medium | 6.3 | DedeCMS 5.7.88 `/plus/download.php?open=1` | NVD says exploit published and may be used | Validate exposure and patch/mitigate SSRF |
| CVE-2026-10583 | Medium | 4.7 | GoClaw <= 3.11.3 TTS Configuration endpoint | Public issue/exploit disclosed | Restrict admin endpoints and update when fixed |
| CVE-2026-3198 | Medium | 6.5 | MLflow 3.9.0 basic-auth Gateway API list endpoints | Huntr advisory | Restrict authenticated users; apply MLflow fix when released |

## Exploits Released

### Sploitus Indexed Top 10 (Best-Effort Reconstruction)

The Sploitus homepage did not expose the requested "Exploits of the Week" block to static fetch. These are the highest-relevance Sploitus-indexed entries found by targeted searches during this run; order is not guaranteed by Sploitus.

| Rank | Sploitus indicator | Affected software | Exploit type | Maturity | Weaponization potential |
| --- | --- | --- | --- | --- | --- |
| 1 | CVE-2026-9082 (`89259320-7066-518A-B075-CE8CD77E926F`) | Drupal Core PostgreSQL | Unauthenticated SQL injection | Public PoC / scanner indicator | High for PostgreSQL-backed Drupal |
| 2 | CVE-2026-9082 (`458CE696-FE39-500F-9131-2E24B1BC2E12`) | Drupal Core PostgreSQL | SQL injection lab PoC | Public PoC | High |
| 3 | CVE-2026-9082 (`C5DAAA8D-8748-5503-A888-ABFFC1E3F3D7`) | Drupal Core PostgreSQL | SQL injection | Public PoC | High |
| 4 | Drupal SA-CORE-2026-004 lab (`108B5C3B-AD91-501B-9F9D-A7F4DC457879`) | Drupal Core PostgreSQL | Detector / lab | Detector PoC | Medium-High |
| 5 | CVE-2026-20223 | Cisco Secure Workload | Critical network exploit indicator | Public PoC indicator | High, enterprise product |
| 6 | CVE-2026-38526 | Krayin CRM v2.2.x | Authenticated PHP upload RCE | Public PoC | High after credential access |
| 7 | CVE-2026-41091 / CVE-2026-33825 | Microsoft Defender | Local privilege escalation | Public PoC indicator | Medium-High post-compromise |
| 8 | CVE-2026-24061 | inetutils-telnetd | Remote pre-auth root indicator | Public scanner/exploit indicator | High where exposed |
| 9 | CVE-2026-5760 | SGLang | SSTI to RCE via model/chat template | Public PoC | High for exposed AI inference services |
| 10 | CVE-2025-32432 | Craft CMS | Pre-auth RCE | ExploitDB/Sploitus indicator | High for exposed Craft CMS |

### ExploitDB Additions

- 2026-06-01: EDB-52607, WordPress OrderConvo 14 path traversal, CVE-2025-10162, unverified.
- 2026-06-01: EDB-52608, Drupal Core 10.5.5 error-based SQL injection, CVE-2026-9082, unverified.
- 2026-05-30: EDB-52606, Notepad++ 8.9.6 arbitrary code execution, CVE-2026-48778, unverified.
- 2026-05-29: EDB-52591, Linux Kernel local privilege escalation bundle, CVE-2026-46300 / CVE-2026-43500 / CVE-2026-43284, unverified.
- 2026-05-29: EDB-52587, strongSwan libsimaka heap buffer overflow, CVE-2026-35330, unverified.

### New GitHub PoC Indicators

- `0xABCD01/CVE-2026-41089`: Netlogon PoC indicator, created 2026-06-01, 48 stars. Treat as unvalidated and potentially unsafe.
- `O99099O/CVE-2026-8206-Poc-`: Kirki PoC indicator, created 2026-06-01, 0 stars. Treat as unvalidated.
- `letsr00t/CVE-2026-43494-PinTheft-PoC`: PinTheft PoC fork/indicator, created 2026-05-30.
- `Koshmare-Blossom/PinTheft-asm`: PinTheft x86_64 assembly implementation indicator, created 2026-05-28.

## Malware Intelligence

- VX-Underground website root was available through web search snippets, but no new June 2026 ransomware report was confirmed.
- VX GitHub user repository telemetry:
  - `vxunderground/MalwareSourceCode` updated 2026-06-02 01:08 UTC; last pushed 2026-05-30 07:11 UTC.
  - `vxunderground/VX-API` updated 2026-06-01 18:39 UTC; last pushed 2024-02-28.
  - `vxunderground/VXUG-Papers` updated 2026-06-01 14:50 UTC; last pushed 2021-12-07.
- Latest `MalwareSourceCode` tree sample still contains archival families/tools such as `Win32.Zeus`, `Win32.RedPetya`, `Win32.PentagonRAT.Builder`, `Win32.HiddenVNCBot`, and `Win32.PowerLoader`; Git tree metadata alone does not prove these were newly added this hour.
- Ransomware / supply-chain carry-forward:
  - CISA KEV continues to list Nx Console (CVE-2026-48027) and TanStack (CVE-2026-45321) malicious package / credential-stealing supply-chain incidents with known ransomware campaign use.
  - Daemon Tools Lite (CVE-2026-8398) remains in KEV as embedded malicious code.

## Security Releases and Vendor Advisories

- Microsoft: CCB Belgium updated May 2026 Patch Tuesday guidance to state CVE-2026-41089 is actively exploited. Patch all Windows Server domain controllers.
- Palo Alto Networks: PAN-OS CVE-2026-0257 updated 2026-05-29 with exploit maturity ATTACKED; fixed releases and mitigations available.
- Cisco: Catalyst SD-WAN CVE-2026-20182 advisory confirms limited exploitation and no workaround; fixed software available.
- Oracle: CISA added CVE-2024-21182 WebLogic Server to KEV on 2026-06-01 with 2026-06-04 due date.
- Drupal: CVE-2026-9082 PostgreSQL SQL injection has public PoCs; update supported branches immediately.
- Cloud Foundry: UAA CVE-2026-40965 requires update to uaa_release v78.13.0 / cf-deployment v56.1.0 and key rotation if EC signing keys were exposed.
- IBM: WebSphere Application Server 8.5/9.0 advisories for RCE/spoofing vulnerabilities require interim fixes or fix packs.
- WordPress ecosystem: Kirki 6.0.7 patches CVE-2026-8206 and related recent Kirki flaws.
- Apache ecosystem carry-forward from NVD 24h: ActiveMQ, Solr, MINA SSHD, and Fluss high-severity issues should be reviewed in enterprise inventories.

## Unified Vulnerability Records

```json
[
  {
    "cve": "CVE-2026-8206",
    "cvss": "9.8",
    "vendor": "Kirki / WordPress plugin ecosystem",
    "product": "Kirki - Freeform Page Builder, Website Builder & Customizer",
    "affected_versions": "6.0.0 through 6.0.6",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://github.com/O99099O/CVE-2026-8206-Poc-"],
    "patch_available": true,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2026-8206", "https://patchstack.com/database/wordpress/plugin/kirki/vulnerability/wordpress-kirki-plugin-6-0-0-6-0-6-unauthenticated-privilege-escalation-via-handle-forgot-password-vulnerability"]
  },
  {
    "cve": "CVE-2026-41089",
    "cvss": "9.8",
    "vendor": "Microsoft",
    "product": "Windows Netlogon",
    "affected_versions": "Windows Server 2012 and later domain controllers per CCB advisory",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": false,
    "poc_links": ["https://github.com/0xABCD01/CVE-2026-41089"],
    "patch_available": true,
    "sources": ["https://ccb.belgium.be/advisories/warning-microsoft-patch-tuesday-may-2026-patches-118-vulnerabilities-16-critical-102", "https://msrc.microsoft.com/update-guide/vulnerability/CVE-2026-41089"]
  },
  {
    "cve": "CVE-2026-0257",
    "cvss": "7.8",
    "vendor": "Palo Alto Networks",
    "product": "PAN-OS GlobalProtect",
    "affected_versions": "PAN-OS 10.2, 11.1, 11.2, 12.1 and Prisma Access ranges with authentication override cookie exposure",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://www.rapid7.com/blog/post/etr-rapid7-observed-exploitation-of-pan-os-globalprotect-authentication-bypass-vulnerability-cve-2026-0257/"],
    "patch_available": true,
    "sources": ["https://security.paloaltonetworks.com/CVE-2026-0257", "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"]
  },
  {
    "cve": "CVE-2026-20182",
    "cvss": "10.0",
    "vendor": "Cisco",
    "product": "Catalyst SD-WAN Controller and Manager",
    "affected_versions": "Multiple Cisco Catalyst SD-WAN releases before fixed releases listed by Cisco",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://www.rapid7.com/blog/post/ve-cve-2026-20182-critical-authentication-bypass-cisco-catalyst-sd-wan-controller-fixed/"],
    "patch_available": true,
    "sources": ["https://www.cisco.com/c/en/us/support/docs/csa/cisco-sa-sdwan-rpa2-v69WY2SW.html", "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"]
  },
  {
    "cve": "CVE-2024-21182",
    "cvss": "Not provided in KEV feed",
    "vendor": "Oracle",
    "product": "WebLogic Server",
    "affected_versions": "See Oracle CPU July 2024",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://www.oracle.com/security-alerts/cpujul2024.html", "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"]
  },
  {
    "cve": "CVE-2026-9082",
    "cvss": "6.5 (NVD), Drupal 20/25 Highly Critical",
    "vendor": "Drupal",
    "product": "Drupal Core PostgreSQL database abstraction API",
    "affected_versions": "8.9.0-10.4.9, 10.5.0-10.5.9, 10.6.0-10.6.8, 11.0.0-11.1.9, 11.2.0-11.2.11, 11.3.0-11.3.9 when using PostgreSQL",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://sploitus.com/exploit?id=458CE696-FE39-500F-9131-2E24B1BC2E12", "https://www.exploit-db.com/exploits/52608"],
    "patch_available": true,
    "sources": ["https://test.osv.dev/vulnerability/DRUPAL-CORE-2026-004", "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"]
  },
  {
    "cve": "CVE-2026-40965",
    "cvss": "10.0",
    "vendor": "Cloud Foundry",
    "product": "UAA / cf-deployment",
    "affected_versions": "uaa_release v76.12.0 through v78.12.0; cf-deployment v30.0.0 through v56.0.0; EC JWT signing keys only",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://www.cloudfoundry.org/blog/cve-2026-40965-uaa-ec-private-key-disclosure/", "https://github.com/advisories/GHSA-qc5f-2h9q-7m2g"]
  },
  {
    "cve": "CVE-2026-9319",
    "cvss": "9.0",
    "vendor": "IBM",
    "product": "WebSphere Application Server",
    "affected_versions": "8.5 and 9.0 with JAX-WS endpoints using WS-Security",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://www.ibm.com/support/pages/node/7274738", "https://github.com/advisories/GHSA-rqhj-2grh-m6c2"]
  },
  {
    "cve": "CVE-2026-46243",
    "cvss": "Not available in observed primary disclosure",
    "vendor": "Linux / cifs-utils",
    "product": "Linux kernel CIFS client and cifs-utils cifs.upcall path",
    "affected_versions": "Configuration-dependent; vulnerable kernel CIFS plus cifs-utils default cifs.spnego request-key rule and unprivileged namespaces",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://github.com/manizada/CIFSwitch"],
    "patch_available": true,
    "sources": ["https://seclists.org/oss-sec/2026/q2/767", "https://www.openwall.com/lists/oss-security/2026/05/28/2"]
  },
  {
    "cve": "CVE-2026-43494",
    "cvss": "Not consistently assigned in observed sources",
    "vendor": "Linux",
    "product": "Linux kernel RDS zerocopy and io_uring interaction",
    "affected_versions": "Configuration-dependent; RDS/RDS_TCP and io_uring enabled, vulnerable kernel, x86_64 PoC payload",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://github.com/v12-security/pocs/blob/main/pintheft/poc.c", "https://github.com/letsr00t/CVE-2026-43494-PinTheft-PoC"],
    "patch_available": true,
    "sources": ["https://www.bleepingcomputer.com/news/linux/exploit-released-for-new-pintheft-arch-linux-root-escalation-flaw/", "https://tuxcare.com/blog/cve-pintheft/"]
  },
  {
    "cve": "CVE-2026-10581",
    "cvss": "6.3",
    "vendor": "DedeCMS",
    "product": "DedeCMS 5.7.88",
    "affected_versions": "5.7.88",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://vuldb.com/vuln/367676"],
    "patch_available": false,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2026-10581", "https://vuldb.com/cve/CVE-2026-10581"]
  },
  {
    "cve": "CVE-2026-3198",
    "cvss": "6.5",
    "vendor": "MLflow",
    "product": "MLflow basic-auth Gateway API",
    "affected_versions": "3.9.0 with --app-name basic-auth",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": false,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2026-3198", "https://huntr.com/bounties/e57db731-97d3-40c3-a429-831ee959807f"]
  }
]
```

## Recommended Actions (Highest to Lowest Priority)

1. Patch and investigate actively exploited perimeter/identity systems: Cisco Catalyst SD-WAN CVE-2026-20182, PAN-OS CVE-2026-0257, Microsoft Netlogon CVE-2026-41089, Oracle WebLogic CVE-2024-21182.
2. Patch internet-facing Drupal PostgreSQL deployments for CVE-2026-9082 and hunt for JSON:API/login SQL error probes.
3. Update WordPress Kirki to 6.0.7+ and audit password reset / admin account activity.
4. Upgrade Cloud Foundry UAA / cf-deployment and rotate EC signing keys if `/token_keys` could have exposed private key material.
5. Apply IBM WebSphere interim fixes or compensating network restrictions for JAX-WS/WS-Security endpoints.
6. Patch Linux kernel fleets for CIFSwitch and PinTheft where prerequisites apply; disable unused CIFS/RDS/io_uring attack surface where feasible.
7. Review ExploitDB and Sploitus indicators in a sandbox before using any PoC for validation; do not run untrusted GitHub exploit code on production or analyst workstations.
8. Continue monitoring VX-Underground, MalwareBazaar/abuse.ch, Shadowserver, SANS ISC, and vendor PSIRTs for ransomware exploitation overlap with the KEV items above.

## Confidence Summary

- High confidence: NVD counts, CISA KEV entries, PAN-OS exploitation status, Cisco exploitation status, CCB Netlogon active exploitation statement, Cloud Foundry affected/fixed versions, Kirki patch version.
- Medium confidence: GitHub/Sploitus/ExploitDB PoC maturity and weaponization level, Drupal active exploitation scale, Linux LPE distribution exposure.
- Low confidence: Ordering of Sploitus reconstructed Top 10 because the homepage did not expose the requested list.
