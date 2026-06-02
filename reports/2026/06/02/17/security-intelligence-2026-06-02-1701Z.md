# Security Intelligence Report - 2026-06-02 17:01 UTC

Report window: 2026-06-02 16:00-17:35 UTC, with day-to-date and rolling 24-hour enrichment.

## Executive Summary

- NVD hourly intake: 37 CVEs published between 16:00 and 17:35 UTC: 1 critical, 13 high, 11 medium, 3 low, 9 unknown.
- NVD day-to-date intake: 130 CVEs: 7 critical, 39 high, 63 medium, 8 low, 13 unknown.
- NVD rolling 24-hour intake: 320 CVEs: 14 critical, 126 high, 115 medium, 47 low, 18 unknown.
- CISA KEV: catalog version 2026.06.01; no new KEV additions observed after Oracle WebLogic Server CVE-2024-21182 on 2026-06-01. Verified current KEV status for Cisco SD-WAN CVE-2026-20182, FortiClient EMS CVE-2026-35616, cPanel CVE-2026-41940, PAN-OS CVE-2026-0257, Citrix NetScaler CVE-2026-3055, Drupal CVE-2026-9082, LiteLLM CVE-2026-42208, Nx CVE-2026-48027, and TanStack CVE-2026-45321.
- Critical new hourly CVE: OpenMed CVE-2026-47117, unauthenticated RCE through Hugging Face model loading with `trust_remote_code=True`; patch is OpenMed 1.5.2.
- Other high-priority hourly CVEs: Amazon Kiro IDE CVE-2026-10591, Bitdefender Napoca CVE-2026-10047/CVE-2026-10046, elixir-mint Mint HTTP/2 DoS CVE-2026-49754/CVE-2026-48862, OpenTelemetry eBPF Instrumentation parser flaws CVE-2026-45686/CVE-2026-45685/CVE-2026-45678, NiceGUI local file disclosure CVE-2026-45553, and VIVOTEK FD8136 authenticated RCE indicators.
- Active exploitation priorities: Cisco Catalyst SD-WAN CVE-2026-20182, FortiClient EMS CVE-2026-35616 with EKZ Infostealer deployment, cPanel/WHM CVE-2026-41940 with Sorry ransomware/nuclear.x86 activity, Palo Alto PAN-OS CVE-2026-0257, Citrix NetScaler CVE-2026-3055, Drupal Core CVE-2026-9082, Oracle WebLogic CVE-2024-21182, and Microsoft Netlogon CVE-2026-41089.
- Exploit monitoring: Sploitus homepage static fetch still exposes only the search shell, not an official "Exploits of the Week" block. The top-10 list below is reconstructed from indexed Sploitus pages, ExploitDB, Packet Storm references, GitHub search, and prior enrichment. Treat it as exploit indicators, not validation that the code is safe or functional.
- GitHub monitoring: reviewed security advisories published since 16:00 UTC returned no entries. Strict newly-created `CVE-2026 PoC exploit created:>=2026-06-02` returned no repositories, but the broader pushed query found newly created/pushed unvalidated indicators including `TYehan/CVE-2026-23744`, `lorenzocamilli/CVE-2026-45332-PoC`, cPanel CVE-2026-41940, Linux Copy Fail CVE-2026-31431, npm tar CVE-2026-31802, Frigate CVE-2026-25643, Chrome CVE-2026-2441, and Notepad CVE-2026-20841.
- Malware and supply chain: VX-Underground web root returned 403, but GitHub metadata showed no new push after `MalwareSourceCode` on 2026-05-30. MalwareBazaar browse page reported 248 submissions in the past 24 hours with Mirai as the most-seen family. Red Hat `@redhat-cloud-services` npm packages remain a high-priority Miasma/Mini Shai-Hulud credential-stealing worm event.
- Confidence: High for NVD, CISA KEV, vendor, and GitHub advisory-backed records; Medium for active exploitation claims based on a government warning plus secondary reporting where Microsoft/CISA have not corroborated; Low for unreviewed GitHub exploit repositories.

## Top Vulnerabilities

### 1. CVE-2026-20182 - Cisco Catalyst SD-WAN Controller / Manager authentication bypass

- Severity: Critical, CVSS 10.0.
- Affected software: Cisco Catalyst SD-WAN Controller and Manager.
- Exploit availability: Public exploit/PoC indicators and Sploitus references; Rapid7/Talos reporting provides technical exploitation context.
- Active exploitation: Yes. Cisco Talos tracks active in-the-wild exploitation under UAT-8616; CISA KEV listed.
- Recommended action: Upgrade all supported releases to Cisco fixed versions, collect admin-tech files before remediation where feasible, open TAC cases for compromise review, and hunt for SSH key additions plus NETCONF configuration changes.
- Confidence: High.

### 2. CVE-2026-35616 - Fortinet FortiClient EMS improper access control

- Severity: Critical, CVSS 9.1.
- Affected software: FortiClient EMS 7.4.5 and 7.4.6.
- Exploit availability: Public Sploitus/exploit indicators; watchTowr and Horizon3 describe pre-auth API bypass mechanics.
- Active exploitation: Yes. Arctic Wolf observed exploitation to push EKZ Infostealer disguised as `FortiEndpoint_Patch.exe` / `p.exe` through EMS-managed workflows.
- Recommended action: Apply Fortinet hotfixes or upgrade to 7.4.7+, restrict EMS management access, hunt for `Certificate not found in request header`, unauthorized Remote Access Profile changes, suspicious patch executables, and credential exfiltration.
- Confidence: High.

### 3. CVE-2026-41940 - cPanel & WHM authentication bypass

- Severity: Critical, CVSS 9.8.
- Affected software: cPanel & WHM and WP Squared / WP2.
- Exploit availability: Public Metasploit/Sploitus/GitHub indicators; exploit maturity is high because ransomware and botnet activity are reported.
- Active exploitation: Yes. Reporting ties exploitation to Sorry ransomware and `nuclear.x86` botnet/miner activity; CISA KEV lists known ransomware use.
- Recommended action: Patch immediately, rotate hosting/API/SSH credentials, hunt for forged session files under cPanel session paths, `.sorry` extensions, ransom notes, Go HTTP clients against cPanel ports, and Mirai-like ELF payloads.
- Confidence: High.

### 4. CVE-2026-0257 - Palo Alto Networks PAN-OS GlobalProtect authentication bypass

- Severity: High, CVSS 7.8; critical operational priority for internet-facing GlobalProtect.
- Affected software: PAN-OS / Prisma Access GlobalProtect portals and gateways when authentication override cookies and a vulnerable certificate configuration are present.
- Exploit availability: Rapid7 validated proof-of-concept behavior; public PoC indicators exist.
- Active exploitation: Yes. Rapid7 observed exploitation starting 2026-05-17; Palo Alto Networks notes limited exploit attempts; CISA KEV listed.
- Recommended action: Upgrade to fixed PAN-OS/Prisma Access releases, disable authentication override cookies if patching is delayed, dedicate a cookie certificate, and review VPN logs for forged-cookie authentication, spoofed MAC `aa:bb:cc:dd:ee:ff`, `GP-CLIENT`, and `DESKTOP-GP01`.
- Confidence: High.

### 5. CVE-2026-47117 - OpenMed remote code execution via PII model loading

- Severity: Critical, NVD CVSS 9.8; VulnCheck CVSS v4 9.3.
- Affected software: OpenMed before 1.5.2.
- Exploit availability: No Sploitus/GitHub exploit hit confirmed during this run, but exploitation requires only control of a model name/repository path that routes to a `trust_remote_code=True` Hugging Face model load.
- Active exploitation: Not observed.
- Recommended action: Upgrade OpenMed to 1.5.2 or later, restrict privacy-filter model loading to trusted allowlisted repositories, and audit logs for attacker-controlled `model_name` values containing `privacy-filter`.
- Confidence: High for vulnerability and patch; Medium for exposure prevalence.

### 6. CVE-2026-23744 - MCPJam Inspector unauthenticated RCE

- Severity: Critical, CVSS 9.8.
- Affected software: MCPJam Inspector <= 1.4.2.
- Exploit availability: Multiple Sploitus entries, Packet Storm references, and newly pushed GitHub indicators including `TYehan/CVE-2026-23744`. Public code appears to target `/api/mcp/connect`.
- Active exploitation: Not confirmed in this run, but weaponization potential is very high for exposed developer workstations because the service binds to `0.0.0.0` by default in affected versions.
- Recommended action: Upgrade to 1.4.3 or later, bind local development tools to `127.0.0.1`, firewall port 6274, and review developer machines for unexpected MCP server definitions or spawned shells.
- Confidence: High for public exploit availability, Low for in-the-wild exploitation.

### 7. CVE-2026-10591 - Amazon Kiro IDE insufficient file-write restrictions

- Severity: High, CVSS 8.8.
- Affected software: Amazon Kiro IDE before 0.11.
- Exploit availability: No public Sploitus hit observed. The vendor describes command execution via crafted instructions causing writes to execution-sensitive paths such as `.vscode/tasks.json`.
- Active exploitation: Not observed.
- Recommended action: Upgrade Kiro IDE to 0.11 or later, review workspace trust and auto-execution settings, and watch for unexpected `.vscode/tasks.json` or similar execution-trigger files written by agent workflows.
- Confidence: High.

### 8. CVE-2026-7312 / CVE-2026-7198 - Progress Sitefinity web services flaws

- Severity: Critical. CVE-2026-7312 CVSS 10.0; CVE-2026-7198 CVSS 9.8.
- Affected software: Progress Sitefinity CMS / Sitefinity Insight across supported 13.3, 14.x, and 15.x branches; Progress released product updates through 15.4.8630/15.4.8631 paths.
- Exploit availability: No public exploit confirmed during this run.
- Active exploitation: Not observed.
- Recommended action: Apply Progress product updates immediately, especially for internet-facing Sitefinity instances and deployments using Sitefinity Insight integration or OData web services.
- Confidence: High.

### 9. CVE-2026-10047 / CVE-2026-10046 - Bitdefender Napoca hypervisor out-of-bounds writes

- Severity: High, CVSS 8.5.
- Affected software: Bitdefender Napoca bare-metal hypervisor, end-of-life.
- Exploit availability: No public exploit confirmed. Technical advisories describe guest-controlled real-mode memory offset issues.
- Active exploitation: Not observed.
- Recommended action: Discontinue Napoca use because Bitdefender states no fix is planned for the end-of-life product; isolate any remaining deployments pending retirement.
- Confidence: High.

### 10. CVE-2026-45686 / CVE-2026-45685 / CVE-2026-45678 - OpenTelemetry eBPF Instrumentation parser DoS

- Severity: High, CVSS 7.5 for listed parser crash flaws.
- Affected software: OpenTelemetry eBPF Instrumentation (OBI) before 0.9.0.
- Exploit availability: No public exploit confirmed during this run.
- Active exploitation: Not observed.
- Recommended action: Upgrade OBI to 0.9.0 or later; prioritize environments instrumenting untrusted network traffic where crafted Memcached, MongoDB, or PostgreSQL payloads could crash telemetry collection.
- Confidence: High.

### 11. CVE-2026-45553 - NiceGUI local file disclosure through `ui.restructured_text`

- Severity: High, CVSS 7.5.
- Affected software: NiceGUI before 3.12.0 when attacker-controlled reStructuredText reaches `ui.restructured_text()`.
- Exploit availability: No public Sploitus hit observed.
- Active exploitation: Not observed.
- Recommended action: Upgrade to NiceGUI 3.12.0, avoid rendering untrusted reStructuredText, and audit for Docutils include/csv-table/raw directives reading local files.
- Confidence: High.

### 12. CVE-2024-21182 - Oracle WebLogic Server unspecified vulnerability

- Severity: Critical operational priority because CISA KEV lists active exploitation and a 2026-06-04 due date.
- Affected software: Oracle WebLogic Server per Oracle CPU guidance.
- Exploit availability: No public exploit validated during this run.
- Active exploitation: Yes, per CISA KEV.
- Recommended action: Apply Oracle CPU guidance immediately or remove affected T3/IIOP exposure; prioritize internet-facing WebLogic.
- Confidence: High.

### 13. CVE-2026-41089 - Microsoft Windows Netlogon stack buffer overflow

- Severity: Critical, CVSS 9.8.
- Affected software: Windows Server 2012 through 2025, especially domain controllers.
- Exploit availability: Public GitHub PoC indicators such as `0xABCD01/CVE-2026-41089`; functionality not validated.
- Active exploitation: Reported by Belgium CCB and secondary reporting; not observed in the fetched CISA KEV catalog.
- Recommended action: Patch domain controllers first with Microsoft cumulative updates, restrict Netlogon/RPC exposure, and hunt for LSASS/Netlogon crashes and anomalous MS-NRPC or CLDAP traffic.
- Confidence: Medium for active exploitation, High for severity and patch availability.

## Exploits Released

### Sploitus reconstructed top 10

The Sploitus homepage static fetch did not expose an official "Exploits of the Week" block. The following is reconstructed from indexed Sploitus exploit pages, public exploit sources, and corroborating searches; entries are indicators, not proof that code is safe or functional.

| Rank | CVE | Affected software | Exploit type | Maturity | PoC availability | Weaponization potential |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | CVE-2026-20182 | Cisco Catalyst SD-WAN Controller/Manager | Remote auth bypass to admin/NETCONF access | Active exploitation, KEV | Yes, Sploitus/GitHub indicators | Very high |
| 2 | CVE-2026-41940 | cPanel & WHM | Pre-auth authentication bypass/RCE | Ransomware/botnet use, KEV | Yes, Metasploit/Sploitus/GitHub | Very high |
| 3 | CVE-2026-35616 | FortiClient EMS | Pre-auth API bypass to managed-endpoint code execution | Active exploitation, malware campaign, KEV | Yes, Sploitus indicator | Very high |
| 4 | CVE-2026-0257 | PAN-OS GlobalProtect | Forged authentication override cookie | Active exploitation, KEV | Public/validated PoC indicators | High |
| 5 | CVE-2026-23744 | MCPJam Inspector | Unauthenticated `/api/mcp/connect` RCE | Multiple public exploit entries | Yes, Sploitus/Packet Storm/GitHub | Very high for exposed developer systems |
| 6 | CVE-2026-21858 | n8n | Webhook file read leading to session forgery/RCE | Public exploit chain | Yes, Sploitus indicator | High |
| 7 | CVE-2026-42208 | LiteLLM | Pre-auth SQL injection in bearer-token path | KEV/public exploit lab | Yes, multiple Sploitus indicators | High |
| 8 | CVE-2026-9082 | Drupal Core | Error-based SQL injection | ExploitDB, KEV | Yes, EDB-ID 52608 | High |
| 9 | CVE-2026-31431 | Linux kernel Copy Fail | Local privilege escalation | Public PoC/checkers | Yes, Sploitus/GitHub indicators | Medium-high |
| 10 | CVE-2026-7299 | Appsmith | Stored XSS in SQL editor autocomplete | Public GitHub exploit reference in NVD | Yes, GitHub indicator | Medium |

### ExploitDB additions

Direct ExploitDB CSV retrieval showed latest high-interest rows by ID:

- EDB-ID 52608: Drupal Core 10.5.5 error-based SQL injection, CVE-2026-9082 by external correlation, unverified in CSV.
- EDB-ID 52607: WordPress OrderConvo 14 path traversal, CVE-2025-10162 by external correlation, unverified in CSV.
- EDB-ID 52606: Notepad++ 8.9.6 arbitrary code execution, CVE-2026-48778 by external correlation, unverified in CSV.
- EDB-ID 52605/52604/52603: YAMCS yamcs-core 5.12.7 no-rate-limit, user-enumeration, and LDAP-injection entries, CVE-2026-44596/CVE-2026-44595/CVE-2026-42568 by external correlation.
- EDB-ID 52601: Microsoft NTLMv2 hash capture, CVE-2026-32202 by external correlation.
- EDB-ID 52600: MikroORM 7.0.13 SQL injection, CVE-2026-44680 by external correlation.

The CSV returned null date/CVE fields for these rows, so publication timing and CVE mapping should be confirmed with the ExploitDB web interface before date-sensitive action.

### New GitHub PoC indicators

Reviewed security advisories query for `publishedSince: 2026-06-02T16:00:00Z` returned no entries. Strict newly-created query returned no repositories, but broader pushed query found these unvalidated indicators:

- `TYehan/CVE-2026-23744` - MCPJam Inspector <= 1.4.2 RCE PoC indicator, created/pushed at 16:57-16:58 UTC.
- `lorenzocamilli/CVE-2026-45332-PoC` - no corroborating CVE record found during this run; treat as low-confidence until validated.
- `Defacto-ridgepole254/CVE-2026-41940-Exploit-PoC` - cPanel/WHM auth bypass PoC indicator, pushed at 16:44 UTC.
- `Dullpurple-sloop726/CVE-2026-31431-Linux-Copy-Fail` and `Liverwortenuresis371/copyfail-rs` - Linux Copy Fail local privilege escalation indicators.
- `Recorded-texteditor120/CVE-2026-31802` - npm tar path traversal/arbitrary file overwrite indicator.
- `DyniePro/CVE-2026-25643` - Frigate NVR command execution indicator.
- `fartlover37/CVE-2026-2441-PoC` and `hamzamalik3461/CVE-2026-20841` - Chrome and Windows Notepad exploit indicators carried over from just before the window.

Treat all GitHub PoCs as potentially malicious until code review and sandbox validation are completed.

## Malware Intelligence

- VX-Underground: `https://vx-underground.org/` returned HTTP 403 in this environment. GitHub `/users/vxunderground/repos` showed `MalwareSourceCode` as the most recently pushed repository, last pushed 2026-05-30 07:11 UTC and updated 2026-06-02 15:35 UTC; no new pushed malware-source update was observed in this run.
- MalwareBazaar: public browse page reported 248 submissions in the past 24 hours, Mirai as the most-seen malware family in the past 24 hours, and 1,091,512 samples in corpus.
- FortiClient EMS / EKZ Infostealer: Arctic Wolf observed CVE-2026-35616 exploitation to deploy EKZ Infostealer disguised as a Fortinet endpoint patch. EKZ targets browser credentials, cookies, and autofill data and exfiltrates over HTTP.
- cPanel / Sorry ransomware: Public reporting ties CVE-2026-41940 exploitation to Sorry ransomware and `nuclear.x86` Mirai-variant botnet/miner payloads. Hunt for `.sorry` extensions, `README.md` ransom notes, forged cPanel sessions, `nuclear.x86`, and suspicious SSH key modifications.
- Red Hat npm / Miasma: Multiple sources report 32 `@redhat-cloud-services` npm packages and 96 versions compromised by a credential-stealing worm related to Mini Shai-Hulud. Payloads target cloud credentials, CI/CD tokens, Kubernetes service-account tokens, npm/PyPI tokens, SSH private keys, Docker/GPG credentials, and `.env` files. Isolate systems that installed affected packages since 2026-06-01 and rotate secrets after containment.
- TanStack / Nx supply chain carry-forward: CISA KEV continues to list TanStack CVE-2026-45321 and Nx Console CVE-2026-48027 with known ransomware use for Nx. Keep dependency and extension inventory checks active.

## Security Releases and Vendor Advisories

- Amazon: AWS bulletin 2026-037-AWS published CVE-2026-10591 for Kiro IDE before 0.11; fixed in Kiro IDE 0.11 with no workaround.
- VulnCheck/OpenMed: OpenMed CVE-2026-47117 affects versions before 1.5.2; patch release 1.5.2 is available.
- Progress: Sitefinity advisory published 2026-06-02 for CVE-2026-7312, CVE-2026-7198, CVE-2026-7195, CVE-2026-7201, and CVE-2026-7313; product updates available for supported versions and latest release path 15.4.8631.
- Bitdefender: Napoca CVE-2026-10047 and CVE-2026-10046 advisories published 2026-06-02; product is end-of-life and no fix is planned.
- OpenTelemetry: eBPF Instrumentation v0.9.0 includes security hardening for Java TLS ioctl handling, PostgreSQL BIND parsing, Memcached/MongoDB parser bounds checks, log enricher `writev` reads, ELF parsing, and fallback message buffers.
- NiceGUI: v3.12.0 prevents local file disclosure in `ui.restructured_text` and unauthenticated log-volume DoS in dynamic resource/ESM routes.
- Cisco: CVE-2026-20182 fixed releases available; no workaround; Cisco recommends TAC-supported compromise review.
- Palo Alto Networks: CVE-2026-0257 advisory and Rapid7 exploitation analysis updated with additional IOCs; fixes regenerate GlobalProtect authentication override cookies.
- Fortinet: CVE-2026-35616 hotfixes for EMS 7.4.5/7.4.6 and full fix in 7.4.7+; pair patching with endpoint compromise review.
- Oracle: WebLogic CVE-2024-21182 remains the newest KEV addition with 2026-06-04 due date.
- GitHub Security Advisories: Reviewed advisories query for `publishedSince: 2026-06-02T16:00:00Z` returned no entries.

## Unified Vulnerability Records

```json
[
  {
    "cve": "CVE-2026-20182",
    "cvss": "10.0",
    "vendor": "Cisco",
    "product": "Catalyst SD-WAN Controller and Manager",
    "affected_versions": "Multiple supported Catalyst SD-WAN releases before Cisco fixed builds",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://sploitus.com/search?query=CVE-2026-20182"],
    "patch_available": true,
    "sources": ["https://blog.talosintelligence.com/sd-wan-ongoing-exploitation/", "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"]
  },
  {
    "cve": "CVE-2026-35616",
    "cvss": "9.1",
    "vendor": "Fortinet",
    "product": "FortiClient EMS",
    "affected_versions": "7.4.5 and 7.4.6",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://sploitus.com/search?query=CVE-2026-35616"],
    "patch_available": true,
    "sources": ["https://arcticwolf.com/resources/blog/forticlient-ems-exploited-via-cve-2026-35616-to-deliver-ekz-infostealer-disguised-as-a-fortinet-patch/", "https://watchtowr.com/resources/fortinet-forticlient-ems-zero-day-cve-2026-35616-active-exploitation-underway/", "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"]
  },
  {
    "cve": "CVE-2026-41940",
    "cvss": "9.8",
    "vendor": "WebPros",
    "product": "cPanel & WHM and WP Squared",
    "affected_versions": "Supported cPanel & WHM versions after 11.40 per public reporting",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://github.com/Defacto-ridgepole254/CVE-2026-41940-Exploit-PoC"],
    "patch_available": true,
    "sources": ["https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json", "https://www.bleepingcomputer.com/news/security/critrical-cpanel-flaw-mass-exploited-in-sorry-ransomware-attacks/"]
  },
  {
    "cve": "CVE-2026-0257",
    "cvss": "7.8",
    "vendor": "Palo Alto Networks",
    "product": "PAN-OS GlobalProtect",
    "affected_versions": "GlobalProtect portal/gateway configurations with authentication override cookies and affected certificate configuration",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://security.paloaltonetworks.com/CVE-2026-0257", "https://www.rapid7.com/blog/post/etr-rapid7-observed-exploitation-of-pan-os-globalprotect-authentication-bypass-vulnerability-cve-2026-0257/", "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"]
  },
  {
    "cve": "CVE-2026-47117",
    "cvss": "9.8",
    "vendor": "OpenMed",
    "product": "OpenMed",
    "affected_versions": "Before 1.5.2",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://www.vulncheck.com/advisories/openmed-remote-code-execution-via-pii-model-loading", "https://github.com/maziyarpanahi/openmed/releases/tag/v1.5.2"]
  },
  {
    "cve": "CVE-2026-23744",
    "cvss": "9.8",
    "vendor": "MCPJam",
    "product": "Inspector",
    "affected_versions": "<= 1.4.2",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://sploitus.com/exploit?id=254A6F19-4F33-5786-90FC-3146F3468F08", "https://sploitus.com/exploit?id=PACKETSTORM%3A217697", "https://github.com/TYehan/CVE-2026-23744"],
    "patch_available": true,
    "sources": ["https://github.com/MCPJam/inspector/security/advisories/GHSA-232v-j27c-5pp6", "https://nvd.nist.gov/vuln/detail/CVE-2026-23744"]
  },
  {
    "cve": "CVE-2026-10591",
    "cvss": "8.8",
    "vendor": "Amazon",
    "product": "Kiro IDE",
    "affected_versions": "Before 0.11",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://aws.amazon.com/security/security-bulletins/2026-037-aws/", "https://kiro.dev/changelog/ide/0-11/"]
  },
  {
    "cve": "CVE-2026-7312",
    "cvss": "10.0",
    "vendor": "Progress",
    "product": "Sitefinity",
    "affected_versions": "14.0.7700-14.4.8152, 15.0.8200-15.0.8234, 15.1.8300-15.1.8335, 15.2.8400-15.2.8441, 15.3.8500-15.3.8531, 15.4.8600-15.4.8630",
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
    "product": "Sitefinity",
    "affected_versions": "15.4.8623 before 15.4.8630",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://community.progress.com/s/article/Sitefinity-Security-Advisory-for-Addressing-Security-Vulnerabilities-CVE-2026-7312-CVE-2026-7198-CVE-2026-7195-CVE-2026-7201-CVE-2026-7313-May-2026", "https://nvd.nist.gov/vuln/detail/CVE-2026-7198"]
  },
  {
    "cve": "CVE-2026-10047",
    "cvss": "8.5",
    "vendor": "Bitdefender",
    "product": "Napoca",
    "affected_versions": "End-of-life Napoca bare-metal hypervisor",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": false,
    "sources": ["https://www.bitdefender.com/support/security-advisories/out-of-bounds-write-in-napoca-real-mode-hook-handler-via-guest-controlled-sssp-va-13905", "https://nvd.nist.gov/vuln/detail/CVE-2026-10047"]
  },
  {
    "cve": "CVE-2026-45686",
    "cvss": "7.5",
    "vendor": "OpenTelemetry",
    "product": "eBPF Instrumentation",
    "affected_versions": "Before 0.9.0",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://github.com/open-telemetry/opentelemetry-ebpf-instrumentation/releases/tag/v0.9.0", "https://github.com/open-telemetry/opentelemetry-ebpf-instrumentation/security/advisories/GHSA-43g7-cwr8-q3jh"]
  },
  {
    "cve": "CVE-2026-45553",
    "cvss": "7.5",
    "vendor": "NiceGUI",
    "product": "NiceGUI",
    "affected_versions": "Before 3.12.0",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://github.com/zauberzeug/nicegui/releases/tag/v3.12.0", "https://github.com/zauberzeug/nicegui/security/advisories/GHSA-jfrm-rx66-g536"]
  },
  {
    "cve": "CVE-2024-21182",
    "cvss": "NVD pending/varies by Oracle advisory",
    "vendor": "Oracle",
    "product": "WebLogic Server",
    "affected_versions": "Oracle WebLogic Server per July 2024 CPU",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://www.oracle.com/security-alerts/cpujul2024.html", "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"]
  },
  {
    "cve": "CVE-2026-41089",
    "cvss": "9.8",
    "vendor": "Microsoft",
    "product": "Windows Netlogon",
    "affected_versions": "Windows Server 2012 through 2025, especially domain controllers",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": false,
    "poc_links": ["https://github.com/0xABCD01/CVE-2026-41089"],
    "patch_available": true,
    "sources": ["https://msrc.microsoft.com/update-guide/vulnerability/CVE-2026-41089", "https://threat-modeling.com/windows-netlogon-buffer-overflow-cve-2026-41089/"]
  },
  {
    "cve": "CVE-2026-9082",
    "cvss": "Critical",
    "vendor": "Drupal",
    "product": "Drupal Core",
    "affected_versions": "Drupal Core affected branches including 10.5.5 per exploit listing",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://www.exploit-db.com/exploits/52608"],
    "patch_available": true,
    "sources": ["https://www.drupal.org/sa-core-2026-004", "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"]
  }
]
```

## Recommended Actions

1. Emergency patch and hunt: Cisco Catalyst SD-WAN CVE-2026-20182, FortiClient EMS CVE-2026-35616, cPanel/WHM CVE-2026-41940, PAN-OS CVE-2026-0257, Citrix NetScaler CVE-2026-3055, Drupal CVE-2026-9082, and Oracle WebLogic CVE-2024-21182.
2. Patch newly published critical and high-risk developer/cloud tooling issues: OpenMed CVE-2026-47117, MCPJam Inspector CVE-2026-23744, Amazon Kiro IDE CVE-2026-10591, OpenTelemetry eBPF Instrumentation 0.9.0 security fixes, and NiceGUI 3.12.0.
3. Apply Progress Sitefinity updates for CVE-2026-7312/CVE-2026-7198/CVE-2026-7195/CVE-2026-7201/CVE-2026-7313; prioritize public CMS deployments and Sitefinity Insight integrations.
4. Retire Bitdefender Napoca deployments because newly disclosed memory-corruption issues affect an end-of-life product with no planned fix.
5. Patch domain controllers for CVE-2026-41089 and hunt for Netlogon/LSASS anomalies. Treat active exploitation confidence as medium until Microsoft or CISA corroborates CCB reporting.
6. Quarantine systems that installed affected Red Hat `@redhat-cloud-services` packages since 2026-06-01; rotate CI/CD, cloud, registry, SSH, Kubernetes, Docker, GPG, and `.env` secrets only after containment.
7. Review public PoC repositories in an isolated sandbox before use. Newly pushed GitHub exploit repositories may be incomplete or malicious.
8. Continue monitoring CISA KEV for post-17:35 UTC updates, because no new KEV additions were visible in catalog version 2026.06.01 during this run.

## Source Notes

- NVD API 2.0, 2026-06-02 16:00-17:35 UTC, day-to-date, and rolling 24-hour windows.
- CISA Known Exploited Vulnerabilities JSON feed, catalog version 2026.06.01.
- Sploitus homepage and indexed Sploitus exploit result pages; top 10 reconstructed because the homepage did not expose an official weekly list to static fetch.
- ExploitDB CSV from exploit-database GitLab mirror.
- GitHub REST API repository searches and GraphQL security advisory search.
- VX-Underground GitHub repository metadata.
- MalwareBazaar public browse page.
- Vendor and research sources: AWS, VulnCheck, Progress, Bitdefender, OpenTelemetry, NiceGUI, Cisco Talos, Rapid7, Palo Alto Networks, Arctic Wolf, watchTowr, BleepingComputer, Aikido, and Panther.
