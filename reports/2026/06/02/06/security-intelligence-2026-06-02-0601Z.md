# Security Intelligence Report - 2026-06-02 06:01 UTC

Report window: 2026-06-02 05:00-06:35 UTC, with 24-hour enrichment back to 2026-06-01 06:35 UTC.

Repository: `dfalt0/Test-cursor-security-automation`

## Executive Summary

- Total CVEs discovered in NVD during this hour: 0.
- Total CVEs discovered in NVD since 00:00 UTC: 24 (1 critical, 7 medium, 15 low, 1 unknown).
- Total CVEs discovered in NVD over the last 24 hours: 363 (20 critical, 102 high, 124 medium, 74 low, 43 unknown).
- Critical newly published day-to-date: CVE-2026-8206, a WordPress Kirki plugin account-takeover vulnerability affecting versions 6.0.0 through 6.0.6.
- Active exploitation / KEV priorities:
  - CVE-2026-41089 - Microsoft Windows Netlogon RCE; CCB Belgium states active exploitation as of its 2026-05-29 advisory update.
  - CVE-2026-0257 - Palo Alto Networks PAN-OS GlobalProtect authentication bypass; Palo Alto rates exploit maturity as ATTACKED and CISA KEV lists it.
  - CVE-2026-20182 - Cisco Catalyst SD-WAN Controller/Manager authentication bypass; Cisco PSIRT confirms limited exploitation and CISA KEV lists it.
  - CVE-2024-21182 - Oracle WebLogic Server unspecified vulnerability; newest CISA KEV addition, added 2026-06-01.
  - CVE-2026-41940 - cPanel & WHM / WP2 authentication bypass remains KEV-listed with ransomware and backdoor campaign reporting.
- New malware campaigns: No new VX-Underground public malware/ransomware publication was confirmed during this exact hour. Carry-forward malware priorities remain TeamPCP supply-chain credential theft, Akira ransomware tradecraft, The Gentlemen ransomware, and cPanel-related "Sorry" ransomware activity.
- Important security releases / advisories: Android June 2026 bulletin, Zyxel CPE UPnP buffer overflow advisory, Cloud Foundry UAA v78.13.0 / cf-deployment v56.1.0, PAN-OS fixed hotfix trains, Cisco SD-WAN fixed releases, WordPress Kirki 6.0.7, Apache ActiveMQ/Solr/Airflow June 1 disclosures, and GitHub advisories for CloudPirates, Langroid, and Cline.

## Source Coverage and Caveats

- NVD API was queried for the hourly, day-to-date, and 24-hour windows.
- CISA KEV JSON feed was queried; catalog version observed: 2026.06.01, released 2026-06-01T16:59:32.7272Z, count 1608.
- Sploitus homepage/static access still did not expose a machine-readable or visible "Exploits of the Week" block. The Sploitus Top 10 below is therefore a best-effort reconstruction from indexed Sploitus exploit pages discovered through targeted search. Confidence for ordering is Low; confidence that listed pages are Sploitus-indexed exploit indicators is Medium.
- GitHub repository search results are indicators only. No GitHub PoC was executed, sandboxed, or functionally validated.
- Public PoC repositories can be malicious or misleading; treat them as indicators requiring sandbox review before use.
- VX-Underground website and GitHub telemetry were checked. GitHub repository metadata shows no new push after the prior run for the core VX repos reviewed here; repo "updated_at" changes alone are not treated as new malware-family publication.

## Top Vulnerabilities

### 1. CVE-2026-41089 - Microsoft Windows Netlogon RCE

- Severity: Critical, CVSS 9.8.
- Affected software: Windows Server domain controllers, Windows Server 2012 onward per CCB Belgium summary.
- Exploit availability: Public GitHub PoC indicator observed (`0xABCD01/CVE-2026-41089`, created 2026-06-01, 51 stars and 25 forks at query time). Functionality unvalidated.
- Active exploitation: Yes, per CCB Belgium primary advisory update on 2026-05-29.
- Patch available: Yes, Microsoft May 2026 security updates.
- Recommended action: Emergency patch all domain controllers, restrict Netlogon/RPC exposure to trusted networks, and monitor Netlogon/RPC anomalies, LSASS or Netlogon crashes, and suspicious domain-controller authentication activity.
- Confidence: High for active exploitation and patch urgency; Medium for public PoC maturity.
- Sources: CCB Belgium, GitHub repository search, Microsoft MSRC reference via CCB.

### 2. CVE-2026-0257 - Palo Alto Networks PAN-OS GlobalProtect Authentication Bypass

- Severity: Vendor CVSS-B 7.8 High, operationally critical because it targets internet-facing VPN access.
- Affected software: PAN-OS 10.2, 11.1, 11.2, 12.1 and Prisma Access versions with GlobalProtect authentication override cookies enabled and unsafe certificate reuse.
- Exploit availability: Public references and independent validation exist; treat as weaponized.
- Active exploitation: Yes. Palo Alto marks exploit maturity ATTACKED, states limited exploit attempts against unpatched/unmitigated devices, and CISA KEV lists it.
- Patch available: Yes. Fixed versions include PAN-OS 12.1.7 or 12.1.4-h6, 11.2.12 or branch hotfixes, 11.1.15 or branch hotfixes, and 10.2.18-h6 / 10.2.16-h7 / 10.2.13-h21 / 10.2.10-h36 / 10.2.7-h34.
- Recommended action: Upgrade immediately, disable authentication override if not required, or use a dedicated certificate exclusively for authentication override cookies.
- Confidence: High.
- Sources: Palo Alto advisory, CISA KEV.

### 3. CVE-2026-20182 - Cisco Catalyst SD-WAN Controller/Manager Authentication Bypass

- Severity: Critical, CVSS 10.0.
- Affected software: Cisco Catalyst SD-WAN Controller and Manager across on-prem, Cisco-managed cloud, Cloud-Pro, and FedRAMP deployments.
- Exploit availability: Public exploit material and technical detail exist; Cisco provides IoC guidance.
- Active exploitation: Yes. Cisco PSIRT confirms limited exploitation; CISA KEV lists it.
- Patch available: Yes. Fixed releases include 20.9.9.1, 20.12.7.1 / 20.12.6.2 / 20.12.5.4, 20.15.5.2 / 20.15.4.4, 20.18.2.2, and 26.1.1.1 depending on branch.
- Recommended action: Preserve `admin-tech` and relevant logs before upgrade, upgrade control components, validate unauthorized peering events, and review `auth.log` for unexpected `vmanage-admin` public-key logins.
- Confidence: High.
- Sources: Cisco advisory, CISA KEV.

### 4. CVE-2024-21182 - Oracle WebLogic Server Unspecified Vulnerability

- Severity: Critical operational priority due to CISA KEV listing and unauthenticated network access via T3/IIOP.
- Affected software: Oracle WebLogic Server.
- Exploit availability: Not confirmed in this run.
- Active exploitation: Yes by KEV listing.
- Patch available: Yes, Oracle CPU guidance.
- Recommended action: Apply Oracle updates or mitigations immediately; restrict T3/IIOP exposure and review WebLogic logs for suspicious remote access.
- Confidence: High for KEV and urgency; Medium for exploit details because CISA describes the weakness as unspecified.
- Sources: CISA KEV JSON, Oracle CPU July 2024 reference.

### 5. CVE-2026-8206 - WordPress Kirki Plugin Account Takeover

- Severity: Critical, CVSS 9.8.
- Affected software: Kirki - Freeform Page Builder, Website Builder & Customizer plugin versions 6.0.0 through 6.0.6.
- Exploit availability: GitHub PoC indicator observed (`O99099O/CVE-2026-8206-Poc-`, created 2026-06-01). Functionality unvalidated.
- Active exploitation: Not confirmed.
- Patch available: Yes, update to 6.0.7 or later.
- Recommended action: Update or temporarily disable the plugin, audit password reset activity, and review for unexpected administrator access.
- Confidence: High for vulnerability and patch; Low for PoC reliability; Low for exploitation status.
- Sources: NVD, WordPress trac, Wordfence/Patchstack references, GitHub search.

### 6. CVE-2026-40965 - Cloud Foundry UAA EC Private Key Exposure

- Severity: Critical, CVSS 10.0.
- Affected software: uaa_release v76.12.0 through v78.12.0 and cf-deployment v30.0.0 through v56.0.0 when EC keys are used for JWT signing.
- Exploit availability: No public exploit validated, but exploitation is straightforward if `/token_keys` is exposed and EC JWT signing is configured.
- Active exploitation: Not confirmed.
- Patch available: Yes, uaa_release v78.13.0 or cf-deployment v56.1.0 or later.
- Recommended action: Upgrade, rotate exposed EC signing keys, invalidate tokens, and verify RSA-only deployments are not misclassified.
- Confidence: High.
- Sources: Cloud Foundry advisory, NVD.

### 7. CVE-2026-25879 - Langroid Prompt-to-SQL Injection Leading to RCE

- Severity: Critical, CVSS 9.8.
- Affected software: Langroid before 0.63.0, specifically SQLChatAgent configurations connected to databases with code-execution or filesystem-capable privileges.
- Exploit availability: GitHub Advisory includes a reproduction/PoC using LLM prompt injection to coerce dangerous SQL such as PostgreSQL `COPY ... FROM PROGRAM`.
- Active exploitation: Not confirmed.
- Patch available: Yes, Langroid 0.63.0 or later.
- Recommended action: Upgrade, restrict database roles used by LLM agents to least privilege, enforce SQL allowlists, and review agent traces for unexpected DDL, file, or command-execution primitives.
- Confidence: High for vulnerability and PoC; Low for active exploitation.
- Sources: GitHub Advisory Database, NVD.

### 8. CVE-2026-45131 / CVE-2026-45132 - CloudPirates Helm Charts CI Secret Exposure

- Severity: Critical, CVSS 10.0.
- Affected software: CloudPirates Open Source Helm Charts workflows before commit `fcf9302`.
- Exploit availability: Advisory describes a practical attack path against `pull_request_target` workflows that execute fork-controlled code with secrets.
- Active exploitation: Not confirmed.
- Patch available: Yes, commit `fcf9302` and workflow redesign.
- Recommended action: Audit GitHub Actions workflows for `pull_request_target` plus fork checkout, rotate exposed Docker Hub / GitHub / SSH tokens, and gate privileged workflows with reviewer approval.
- Confidence: High for vulnerability; Low for observed exploitation.
- Sources: GitHub advisories GHSA-c47r-c7gw-cvph and GHSA-r874-j8fr-x2pj, NVD.

### 9. CVE-2026-44211 - Cline Kanban Server Cross-Origin WebSocket Hijack

- Severity: Critical, CVSS 9.6.
- Affected software: Cline Kanban server versions 2.13.0 and prior.
- Exploit availability: GitHub Advisory includes browser-based WebSocket PoC snippets that leak workspace state and write attacker-supplied bytes to terminal sessions.
- Active exploitation: Not confirmed.
- Patch available: Noted as unavailable at advisory publication; verify current Cline release status before deployment.
- Recommended action: Disable exposed Kanban/runtime WebSocket service until patched, bind to trusted interfaces only, enforce Origin checks, and avoid browsing untrusted sites while local Cline services are running.
- Confidence: High for vulnerability and PoC; Low for active exploitation.
- Sources: GitHub Advisory Database, NVD.

### 10. CVE-2026-7858 - 3DS Teamwork Cloud / Magic Collaboration Studio Deserialization RCE

- Severity: Critical, CVSS 9.8.
- Affected software: No Magic Teamwork Cloud and CATIA Magic Collaboration Studio Release 2022x through 2026x.
- Exploit availability: No public exploit validated in this run.
- Active exploitation: Not confirmed.
- Patch available: Vendor advisory available.
- Recommended action: Patch collaboration servers, restrict management/service ports, and review authentication and deserialization error logs for suspicious payloads.
- Confidence: High for vulnerability details; Low for exploitation status.
- Sources: 3DS advisory, NVD.

### 11. CVE-2026-8931 - Disig Web Signer RCE

- Severity: Critical, CVSS 9.4.
- Affected software: Disig Web Signer versions 2.0.3 through 2.5.3.
- Exploit availability: No public GitHub exploit found in this run.
- Active exploitation: Not confirmed.
- Patch available: Yes, vendor update references Web Signer 2.5.5.
- Recommended action: Update endpoint signing components, prioritize systems used for qualified electronic signatures, and monitor for unexpected signer process execution.
- Confidence: High for vulnerability and patch; Low for exploitation status.
- Sources: Disig/qesportal advisories, NVD.

### 12. Android June 2026 Security Bulletin - Framework/System Critical Set

- Severity: Multiple Critical and High vulnerabilities.
- Affected software: Android Framework, System, Google Play system update components, kernel, and partner components.
- Exploit availability: No public exploit validated in this run.
- Active exploitation: Not confirmed by the bulletin.
- Patch available: Yes, Android security patch levels 2026-06-01 and 2026-06-05.
- Recommended action: Prioritize fleet updates to 2026-06-05 or later; require OEM confirmation for Qualcomm/MediaTek/Unisoc/Imagination closed-source component coverage.
- Confidence: High.
- Sources: Android Security Bulletin, Qualcomm bulletin reference.

### 13. CVE-2026-3870 / CVE-2026-3871 - Zyxel UPnP Buffer Overflows

- Severity: Medium, CVSS 6.5.
- Affected software: Zyxel VMG4005-B50B, NR7101, Nebula LTE3301-PLUS, and Nebula NR7101 firmware versions listed by Zyxel.
- Exploit availability: No public exploit validated in this run.
- Active exploitation: Not confirmed.
- Patch available: Yes. Firmware patches include VMG4005-B50B 5.13(ABRL.5.5)C0, NR7101 1.00(ABUV.12)B4, LTE3301-PLUS 1.18(ACCA.8)V0, and Nebula NR7101 1.16(ACCC.3)V0.
- Recommended action: Coordinate with ISP/vendor support for firmware, especially for customized ISP devices; reduce LAN/WLAN exposure to untrusted clients.
- Confidence: High.
- Sources: Zyxel advisory, NVD.

### 14. CVE-2026-41940 - cPanel & WHM / WP2 Authentication Bypass

- Severity: Critical, CVSS 9.8.
- Affected software: WebPros cPanel & WHM and WP2 / WordPress Squared.
- Exploit availability: Public research and exploit reporting exist; KEV-listed.
- Active exploitation: Yes by CISA KEV and public reporting; associated reports describe backdoors, cryptominers, botnet activity, and "Sorry" ransomware deployment.
- Patch available: Yes, vendor security update guidance.
- Recommended action: Patch immediately, then perform compromise assessment for web shells, SSH key persistence, unauthorized root password changes, cryptominers, and ransomware staging. Do not treat patching as cleanup.
- Confidence: High for KEV and campaign priority; Medium for exact payload prevalence.
- Sources: CISA KEV, cPanel/WebPros guidance via KEV notes, SANS/search-indexed campaign reporting.

## Newly Published NVD Records This Hour

No NVD CVEs were published in the 2026-06-02 05:00-06:35 UTC query window.

## Day-to-Date NVD Highlights

| CVE | Severity | CVSS | Affected software | Exploit / public disclosure | Action |
| --- | --- | --- | --- | --- | --- |
| CVE-2026-8206 | Critical | 9.8 | WordPress Kirki 6.0.0-6.0.6 | GitHub PoC indicator; WordPress/Wordfence references | Update to 6.0.7+ |
| CVE-2026-3198 | Medium | 6.5 | MLflow 3.9.0 basic-auth Gateway API list endpoints | Huntr advisory | Restrict authenticated users; apply MLflow fix when available |
| CVE-2026-3870 | Medium | 6.5 | Zyxel VMG4005-B50B UPnP AddPortMapping | Vendor advisory | Apply firmware 5.13(ABRL.5.5)C0 |
| CVE-2026-3871 | Medium | 6.5 | Zyxel NR7101 / LTE3301-PLUS / VMG4005-B50B UPnP DeletePortMapping | Vendor advisory | Apply listed firmware patches |
| CVE-2026-10581 | Low | 2.1 | DedeCMS 5.7.88 `/plus/download.php?open=1` | NVD says exploit published and may be used | Validate exposure and patch/mitigate SSRF |
| CVE-2026-10583 | Low | 2.0 | GoClaw <= 3.11.3 TTS Configuration endpoint | Public issue/exploit disclosed | Restrict admin endpoints and update when fixed |

## Exploits Released

### Sploitus Indexed Top 10 (Best-Effort Reconstruction)

The Sploitus homepage did not expose the requested "Exploits of the Week" block to static fetch. These are the highest-relevance Sploitus-indexed entries found by targeted searches during this run and carry-forward searches from the prior hourly run; order is not guaranteed by Sploitus.

| Rank | Sploitus indicator | Affected software | Exploit type | Maturity | Weaponization potential |
| --- | --- | --- | --- | --- | --- |
| 1 | CVE-2026-31431 (`052EF974-A427-5B17-8A55-8AE7C1C493E0`) | Linux kernel Copy Fail | Local privilege escalation | Public C PoC indicator | High post-compromise; broad Linux exposure where unpatched |
| 2 | CVE-2026-31431 (`EDA6BA70-68B9-5D54-9C53-1DE0BCA51BAA`) | Linux kernel Copy Fail | Local privilege escalation | Public PoC / scanner indicator | High |
| 3 | CVE-2026-31431 (`21CF749E-BFFC-545D-BF25-09BAEAE71E0D`) | Linux kernel Copy Fail | Local privilege escalation | Public bash/C implementation indicator | High |
| 4 | CVE-2026-2329 (`MSF:EXPLOIT-LINUX-HTTP-GRANDSTREAM_GXP1600_UNAUTH_RCE-`) | GrandStream GXP1600 phones | Unauthenticated RCE | Metasploit module indicator | High where exposed |
| 5 | CVE-2026-9082 (`89259320-7066-518A-B075-CE8CD77E926F`) | Drupal Core PostgreSQL | Unauthenticated SQL injection | Public PoC / scanner indicator | High for PostgreSQL-backed Drupal |
| 6 | CVE-2026-9082 (`458CE696-FE39-500F-9131-2E24B1BC2E12`) | Drupal Core PostgreSQL | SQL injection lab PoC | Public PoC | High |
| 7 | CVE-2026-20223 | Cisco Secure Workload | Critical network exploit indicator | Public PoC indicator | High, enterprise product |
| 8 | CVE-2026-38526 | Krayin CRM v2.2.x | Authenticated PHP upload RCE | Public PoC | High after credential access |
| 9 | CVE-2026-5760 | SGLang | SSTI to RCE via model/chat template | Public PoC | High for exposed AI inference services |
| 10 | CVE-2025-32432 | Craft CMS | Pre-auth RCE | ExploitDB/Sploitus indicator | High for exposed Craft CMS |

### ExploitDB Additions

- 2026-06-01: EDB-52608, Drupal Core 10.5.5 error-based SQL injection, CVE-2026-9082, unverified.
- 2026-06-01: EDB-52607, WordPress OrderConvo 14 path traversal, CVE-2025-10162, unverified.
- 2026-05-30: EDB-52606, Notepad++ 8.9.6 arbitrary code execution, CVE-2026-48778, unverified.
- 2026-05-30: EDB-52605/52604/52603, YAMCS yamcs-core 5.12.7 no rate limiting / user enumeration / LDAP injection, CVE-2026-44596 / CVE-2026-44595 / CVE-2026-42568, unverified.
- 2026-05-29: EDB-52591, Linux Kernel local privilege escalation bundle, CVE-2026-46300 / CVE-2026-43500 / CVE-2026-43284, unverified.

### New GitHub PoC Indicators

- `0xABCD01/CVE-2026-41089`: Netlogon PoC indicator, created 2026-06-01, 51 stars and 25 forks at query time. Treat as unvalidated and potentially unsafe.
- `O99099O/CVE-2026-8206-Poc-`: Kirki PoC indicator, created 2026-06-01, 0 stars. Treat as unvalidated.
- `Dullpurple-sloop726/CVE-2026-31431-Linux-Copy-Fail`: Copy Fail Linux LPE exploit indicator updated 2026-06-02. Treat as unvalidated.
- `Liverwortenuresis371/copyfail-rs`: Copy Fail Rust exploit/detection indicator updated 2026-06-02. Treat as unvalidated.
- Direct GitHub repository searches during this run found no new repositories for `CVE-2026-9082`, `CVE-2026-8931`, `CVE-2026-7858`, `CVE-2026-10270`, or broad `CVE-2026 RCE PoC` created since 2026-06-01.

## Malware Intelligence

- VX-Underground GitHub telemetry:
  - `vxunderground/MalwareSourceCode` updated 2026-06-02 01:08 UTC; last pushed 2026-05-30 07:11 UTC.
  - `vxunderground/VX-API` updated 2026-06-01 18:39 UTC; last pushed 2024-02-28.
  - `vxunderground/VXUG-Papers` updated 2026-06-01 14:50 UTC; last pushed 2021-12-07.
- Latest sampled `MalwareSourceCode` tree entries remain archival families/tools such as `Win32.PentagonRAT.Builder`, `Win32.PowerLoader`, `Win32.RedPetya`, `Win32.SpyGateRAT`, `Win32.SubSevenLegacy`, and `Win32.Zeus`; Git tree metadata alone does not prove these were newly added this hour.
- Supply-chain activity:
  - SANS ISC continues to track TeamPCP activity, including malicious Nx Console and Python SDK incidents tied to credential theft, cloud propagation, and destructive potential.
  - CISA KEV continues to list Nx Console (CVE-2026-48027) and TanStack (CVE-2026-45321) malicious package / credential-stealing supply-chain incidents with known ransomware campaign use.
- Ransomware activity:
  - Microsoft Threat Intelligence's May 28 analysis of The Gentlemen ransomware identifies Storm-2697 as the RaaS operator and describes Go-based self-propagating encryption tradecraft.
  - SANS ISC's Akira ransomware kill-chain reconstruction remains relevant for detection engineering: SSL VPN brute force, Kerberoasting, RDP lateral movement, event-log clearing, service shutdown, and shadow-copy deletion.
  - cPanel CVE-2026-41940 remains a high-priority ransomware/backdoor carry-forward due public reporting of "Sorry" ransomware, web shells, SSH-key persistence, and cryptomining payloads.

## Security Releases and Vendor Advisories

- Microsoft: CCB Belgium updated May 2026 Patch Tuesday guidance to state CVE-2026-41089 is actively exploited. Patch all Windows Server domain controllers.
- Palo Alto Networks: PAN-OS CVE-2026-0257 updated 2026-05-29 with exploit maturity ATTACKED; fixed releases and mitigations available.
- Cisco: Catalyst SD-WAN CVE-2026-20182 advisory confirms limited exploitation, no workaround, and fixed software availability.
- Oracle: CISA added CVE-2024-21182 WebLogic Server to KEV on 2026-06-01 with 2026-06-04 due date.
- Google/Android: June 2026 Android Security Bulletin published; security patch levels 2026-06-01 and 2026-06-05 address Framework, System, kernel, and partner-component issues.
- Zyxel: CVE-2026-3870 and CVE-2026-3871 UPnP buffer overflow advisory published 2026-06-02 with firmware patches.
- Cloud Foundry: UAA CVE-2026-40965 requires update to uaa_release v78.13.0 / cf-deployment v56.1.0 and key rotation if EC signing keys were exposed.
- GitHub / developer tooling: CloudPirates Helm Charts, Langroid, and Cline advisories require CI-token hygiene, LLM-agent database privilege review, and local WebSocket origin-hardening respectively.
- IBM: WebSphere Application Server 8.5/9.0 critical deserialization / RCE / spoofing advisories remain high priority.
- WordPress ecosystem: Kirki 6.0.7 patches CVE-2026-8206; Patchstack/Wordfence also show multiple critical/high WordPress plugin records from the last 24 hours.
- Apache ecosystem: ActiveMQ, Solr, Airflow, MINA SSHD, and Fluss high-severity June 1 disclosures should be reviewed against enterprise inventories.

## Unified Vulnerability Records

```json
[
  {
    "cve": "CVE-2026-41089",
    "cvss": "9.8",
    "vendor": "Microsoft",
    "product": "Windows Netlogon / Windows Server domain controllers",
    "affected_versions": "Windows Server 2012 and later domain controllers per CCB summary",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/0xABCD01/CVE-2026-41089"
    ],
    "patch_available": true,
    "sources": [
      "https://ccb.belgium.be/advisories/warning-microsoft-patch-tuesday-may-2026-patches-118-vulnerabilities-16-critical-102",
      "https://msrc.microsoft.com/update-guide/vulnerability/CVE-2026-41089"
    ]
  },
  {
    "cve": "CVE-2026-0257",
    "cvss": "7.8",
    "vendor": "Palo Alto Networks",
    "product": "PAN-OS GlobalProtect",
    "affected_versions": "PAN-OS 10.2/11.1/11.2/12.1 and Prisma Access versions listed by vendor when authentication override cookies and unsafe certificate configuration are present",
    "exploit_available": true,
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
    "affected_versions": "Multiple Cisco Catalyst SD-WAN releases before fixed releases listed in Cisco advisory",
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
    "cve": "CVE-2024-21182",
    "cvss": "",
    "vendor": "Oracle",
    "product": "WebLogic Server",
    "affected_versions": "Oracle WebLogic Server versions covered by Oracle CPU guidance",
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
    "cve": "CVE-2026-8206",
    "cvss": "9.8",
    "vendor": "Kirki / WordPress plugin ecosystem",
    "product": "Kirki - Freeform Page Builder, Website Builder & Customizer",
    "affected_versions": "6.0.0 through 6.0.6",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/O99099O/CVE-2026-8206-Poc-"
    ],
    "patch_available": true,
    "sources": [
      "https://nvd.nist.gov/vuln/detail/CVE-2026-8206",
      "https://plugins.trac.wordpress.org/changeset/3530843/kirki"
    ]
  },
  {
    "cve": "CVE-2026-40965",
    "cvss": "10.0",
    "vendor": "Cloud Foundry",
    "product": "UAA / cf-deployment",
    "affected_versions": "uaa_release v76.12.0 through v78.12.0; cf-deployment v30.0.0 through v56.0.0 with EC JWT signing keys",
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
    "cve": "CVE-2026-25879",
    "cvss": "9.8",
    "vendor": "Langroid",
    "product": "Langroid SQLChatAgent / run_query",
    "affected_versions": "Langroid before 0.63.0",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/langroid/langroid/security/advisories/GHSA-mxfr-6hcw-j9rq"
    ],
    "patch_available": true,
    "sources": [
      "https://github.com/langroid/langroid/security/advisories/GHSA-mxfr-6hcw-j9rq",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-25879"
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
    "cve": "CVE-2026-7858",
    "cvss": "9.8",
    "vendor": "3DS / No Magic / CATIA Magic",
    "product": "Teamwork Cloud / Magic Collaboration Studio",
    "affected_versions": "Release 2022x through 2026x",
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
    "cve": "CVE-2026-8931",
    "cvss": "9.4",
    "vendor": "Disig",
    "product": "Web Signer",
    "affected_versions": "2.0.3 through 2.5.3",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://www.disig.sk/en/news/important-update-of-the-web-signer-application/",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-8931"
    ]
  },
  {
    "cve": "CVE-2026-3870",
    "cvss": "6.5",
    "vendor": "Zyxel",
    "product": "VMG4005-B50B UPnP AddPortMapping",
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
    "product": "NR7101 / LTE3301-PLUS / VMG4005-B50B UPnP DeletePortMapping",
    "affected_versions": "Firmware versions listed by Zyxel through NR7101 1.00(ABUV.11)C0, LTE3301-PLUS 1.18(ACCA.6)C0, Nebula NR7101 1.16(ACCC.1)C0, VMG4005-B50B 5.13(ABRL.5.4)C0",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://www.zyxel.com/global/en/support/security-advisories/zyxel-security-advisory-for-buffer-overflow-vulnerabilities-in-the-upnp-function-of-certain-4g-lte-5g-nr-cpe-and-dsl-ethernet-cpe-06-02-2026",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-3871"
    ]
  },
  {
    "cve": "CVE-2026-41940",
    "cvss": "9.8",
    "vendor": "WebPros",
    "product": "cPanel & WHM / WP2",
    "affected_versions": "cPanel & WHM and WP2 versions covered by vendor April 2026 security updates",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://support.cpanel.net/hc/en-us/articles/40073787579671-cPanel-WHM-Security-Update-04-28-2026"
    ]
  }
]
```

## Recommended Actions

1. Patch and hunt for compromise on Windows domain controllers vulnerable to CVE-2026-41089; prioritize Netlogon/RPC exposure reduction and detection.
2. Upgrade or mitigate PAN-OS GlobalProtect CVE-2026-0257 immediately; verify authentication override cookie configuration and certificate reuse.
3. Upgrade Cisco Catalyst SD-WAN control components for CVE-2026-20182 after preserving `admin-tech`/logs; validate peering and `vmanage-admin` IoCs.
4. Remediate KEV-listed WebLogic CVE-2024-21182 and cPanel CVE-2026-41940; for cPanel, perform post-patch compromise assessment.
5. Patch internet-exposed WordPress/plugin ecosystems, especially Kirki CVE-2026-8206 and critical Patchstack-listed plugins from the last 24 hours.
6. Upgrade Cloud Foundry UAA/cf-deployment for CVE-2026-40965, rotate EC JWT signing keys, and invalidate potentially forged tokens.
7. Review developer/AI tooling exposure: Langroid SQL agents, Cline local WebSocket services, and CloudPirates-style GitHub Actions workflows that execute untrusted fork code with secrets.
8. Apply Android 2026-06-05 patch levels and verify OEM/chipset bulletin coverage for managed mobile fleets.
9. Update Zyxel CPE firmware for CVE-2026-3870/3871 and reduce LAN/WLAN exposure to untrusted clients.
10. Treat all GitHub PoC repositories as untrusted code; triage in disposable sandboxes only and prioritize vendor/KEV-backed evidence over repository names.

## Confidence Summary

- High confidence: NVD counts, CISA KEV catalog state, Palo Alto/Cisco/Cloud Foundry/Zyxel/Android/GitHub advisory facts, and CCB Belgium's Netlogon active-exploitation statement.
- Medium confidence: Sploitus reconstructed ranking and some public PoC maturity assessments.
- Low confidence: Functional quality of GitHub PoC repositories and exact prevalence of unverified ransomware payload claims outside primary advisories.
