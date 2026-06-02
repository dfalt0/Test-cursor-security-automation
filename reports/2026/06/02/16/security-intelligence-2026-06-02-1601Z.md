# Security Intelligence Report - 2026-06-02 16:01 UTC

Report window: 2026-06-02 15:00-16:35 UTC, with day-to-date and rolling 24-hour enrichment.

## Executive Summary

- NVD hourly intake: 0 CVEs published between 15:00 and 16:35 UTC.
- NVD day-to-date intake: 93 CVEs: 6 critical, 25 high, 41 medium, 15 low, 6 unknown.
- NVD rolling 24-hour intake: 325 CVEs: 18 critical, 118 high, 124 medium, 47 low, 18 unknown.
- CISA KEV: catalog version 2026.06.01; no new KEV additions observed in this hourly run. The newest KEV item remains Oracle WebLogic Server CVE-2024-21182 from 2026-06-01.
- Active exploitation priorities: Cisco Catalyst SD-WAN CVE-2026-20182, FortiClient EMS CVE-2026-35616 with EKZ Infostealer deployment, cPanel/WHM CVE-2026-41940 with ransomware/botnet activity, Palo Alto PAN-OS CVE-2026-0257, Citrix NetScaler CVE-2026-3055, Drupal Core CVE-2026-9082, and Microsoft Netlogon CVE-2026-41089.
- New/important NVD items from the current day include Progress Sitefinity CVE-2026-7312 and CVE-2026-7198, Kirki WordPress plugin CVE-2026-8206, Masteriyo LMS PRO CVE-2025-53209, Wirtualna Uczelnia CVE-2026-34906, WP Job Portal CVE-2026-42684, Roche navify CVE-2026-9844, and MISP CVE-2026-10611.
- GitHub monitoring: strict newly created search for `CVE-2026 PoC exploit created:>=2026-06-02` returned no repositories. Broader pushed search showed unvalidated exploit indicators updated near this run for Chrome CVE-2026-2441, Windows Notepad CVE-2026-20841, GNU inetutils telnetd CVE-2026-24061, Redis/DarkReplica CVE-2026-23631, cPanel CVE-2026-41940, Linux Copy Fail CVE-2026-31431, and Netlogon CVE-2026-41089.
- Malware intelligence: VX-Underground GitHub repositories showed no new pushed malware-source update after MalwareSourceCode on 2026-05-30; repository metadata was updated at 15:35 UTC but the latest pushed timestamp remained unchanged.
- Confidence: High for NVD/CISA/vendor-confirmed items; Medium for active exploitation claims based on single government warning plus secondary reporting; Low for unvalidated GitHub PoC repositories.

## Top Vulnerabilities

### 1. CVE-2026-20182 - Cisco Catalyst SD-WAN Controller / Manager authentication bypass

- Severity: Critical, CVSS 10.0.
- Affected software: Cisco Catalyst SD-WAN Controller and Manager.
- Exploit availability: Public exploit/PoC indicators on Sploitus; Cisco advisory and Talos/Rapid7/Tenable reporting provide exploitation context.
- Active exploitation: Yes. Cisco PSIRT confirmed limited exploitation; Cisco Talos tracks activity as UAT-8616.
- KEV status: Listed by CISA on 2026-05-14 under Emergency Directive 26-03.
- Recommended action: Upgrade all supported releases to Cisco fixed versions, collect admin-tech files before remediation where feasible, open TAC cases for compromise review, and follow CISA hunt/hardening guidance.
- Confidence: High.

### 2. CVE-2026-35616 - Fortinet FortiClient EMS improper access control

- Severity: Critical, CVSS 9.1-9.8 depending on source.
- Affected software: FortiClient EMS 7.4.5 and 7.4.6.
- Exploit availability: Public Sploitus exploit indicator; watchTowr and Horizon3 describe pre-auth API bypass mechanics.
- Active exploitation: Yes. Fortinet/watchTowr observed exploitation; Arctic Wolf reported EKZ Infostealer deployed through FortiClient EMS-managed workflows.
- KEV status: Reported by multiple sources as CISA KEV-listed.
- Recommended action: Apply Fortinet hotfixes or upgrade to 7.4.7+, then hunt for EMS log messages such as certificate-header anomalies and endpoints receiving `FortiEndpoint_Patch.exe` or similar fake patch payloads.
- Confidence: High.

### 3. CVE-2026-41940 - cPanel & WHM authentication bypass

- Severity: Critical, CVSS 9.8.
- Affected software: cPanel & WHM and WP2 (WordPress Squared).
- Exploit availability: Public Metasploit/Sploitus indicators and GitHub PoCs; Exploit maturity is high due ransomware/botnet use.
- Active exploitation: Yes. Reports tie exploitation to Sorry ransomware and nuclear.x86 botnet activity.
- KEV status: Listed by CISA with known ransomware use.
- Recommended action: Patch immediately with vendor releases, hunt for forged root session files, suspicious access to ports 2082/2083/2086/2087/2095/2096, `nuclear.x86`, miner scripts, and `.sorry` artifacts.
- Confidence: High.

### 4. CVE-2026-0257 - Palo Alto Networks PAN-OS GlobalProtect authentication bypass

- Severity: High, CVSS 7.8, but operational priority is critical for internet-facing GlobalProtect.
- Affected software: PAN-OS / Prisma Access GlobalProtect portals and gateways when authentication override cookies and a specific certificate configuration are present.
- Exploit availability: Rapid7 validated a working proof of concept; public PoC indicators exist.
- Active exploitation: Yes. Rapid7 observed successful exploitation from 2026-05-17; CISA added the issue to KEV on 2026-05-29.
- KEV status: Listed by CISA.
- Recommended action: Upgrade to vendor-fixed PAN-OS/Prisma Access releases, disable authentication override cookies if patching is delayed, use a dedicated cookie certificate, and review VPN logs for forged-cookie authentication.
- Confidence: High.

### 5. CVE-2026-41089 - Microsoft Windows Netlogon stack buffer overflow

- Severity: Critical, CVSS 9.8.
- Affected software: Windows Server 2012 through 2025, especially domain controllers.
- Exploit availability: Public GitHub PoC indicator `0xABCD01/CVE-2026-41089`; functionality not validated.
- Active exploitation: Reported by Belgium CCB and secondary reporting; Microsoft advisory reportedly has not yet been updated to mark exploitation.
- KEV status: Not observed in fetched CISA KEV catalog.
- Recommended action: Patch domain controllers first with May 2026 cumulative updates, restrict Netlogon/RPC exposure, and hunt for LSASS/Netlogon crashes and anomalous MS-NRPC or CLDAP traffic.
- Confidence: Medium for active exploitation, High for severity and patch availability.

### 6. CVE-2026-7312 and CVE-2026-7198 - Progress Sitefinity web services flaws

- Severity: Critical. CVE-2026-7312 CVSS 10.0; CVE-2026-7198 CVSS 9.8.
- Affected software: Progress Sitefinity versions listed by NVD, including 14.x and 15.x branches; CVE-2026-7312 requires active Sitefinity Insight integration and non-default configuration, while CVE-2026-7198 affects Sitefinity 15.4.8623 before 15.4.8630.
- Exploit availability: No public exploit confirmed during this run.
- Active exploitation: Not observed.
- KEV status: Not listed.
- Recommended action: Inventory Sitefinity deployments, prioritize internet-facing instances with Insight integration, apply Progress product updates, and monitor for credential exposure or unauthorized content access.
- Confidence: High for NVD record, Medium for affected-version completeness because direct vendor search results did not expose the new CVE pages.

### 7. CVE-2026-8206 - Kirki WordPress plugin account takeover

- Severity: Critical, CVSS 9.8.
- Affected software: Kirki Freeform Page Builder / Website Builder / Customizer plugin for WordPress, versions 6.0.0 through 6.0.6.
- Exploit availability: Newly created GitHub mass-exploitation indicator `Jenderal92/CVE-2026-8206`; public functionality not validated.
- Active exploitation: Secondary reporting cites blocked attempts; treat as likely emerging exploitation.
- KEV status: Not listed.
- Recommended action: Update to 6.0.7 or later, enumerate newly created admin users, force password resets for privileged accounts, and inspect web logs for password-reset abuse.
- Confidence: High for vulnerability/patch details, Medium for exploitation.

### 8. CVE-2026-21858 - n8n webhook request handling file access / RCE chain

- Severity: Critical, CVSS 10.0 in public research.
- Affected software: n8n >= 1.65.0 and < 1.121.0.
- Exploit availability: Sploitus indicator and public write-ups describe a file-read to session-forgery to workflow-command-execution chain.
- Active exploitation: Public scanning reported by research sources; not observed in CISA KEV during this run.
- KEV status: Not listed in fetched CISA catalog.
- Recommended action: Upgrade to n8n 1.121.0 or later, preferably latest stable, and restrict or disable public webhook/form endpoints until patched.
- Confidence: High for vulnerability and patch; Medium for exploitation.

### 9. CVE-2026-42208 - BerriAI LiteLLM pre-authentication SQL injection

- Severity: Critical, CVSS 9.3-9.8 in sources.
- Affected software: LiteLLM versions in the 1.81.16 through pre-1.83.7 range per GHSA/Sploitus details.
- Exploit availability: Sploitus lists multiple exploit/lab indicators.
- Active exploitation: CISA KEV-listed according to public reporting; public exploit material exists.
- KEV status: Listed in CISA KEV feed historically.
- Recommended action: Upgrade to the fixed LiteLLM release, rotate proxy/database/API credentials that may have been exposed, and inspect Authorization headers for SQL metacharacter probes.
- Confidence: High.

### 10. CVE-2024-21182 - Oracle WebLogic Server unspecified vulnerability

- Severity: Critical operational priority due KEV and short remediation deadline.
- Affected software: Oracle WebLogic Server.
- Exploit availability: No public exploit validated during this run.
- Active exploitation: Yes, per CISA KEV addition.
- KEV status: Added 2026-06-01, due 2026-06-04.
- Recommended action: Apply Oracle CPU guidance immediately or remove affected T3/IIOP exposure; prioritize internet-facing WebLogic.
- Confidence: High.

### 11. CVE-2026-9082 - Drupal Core SQL injection

- Severity: Critical operational priority due KEV, public exploit, and possible RCE/privilege escalation path.
- Affected software: Drupal Core 10.5.5 and affected branches per Drupal advisory.
- Exploit availability: ExploitDB EDB-ID 52608 and GitHub PoC indicators.
- Active exploitation: KEV-listed and active attempts reported in prior enrichment.
- KEV status: Listed by CISA.
- Recommended action: Apply Drupal security releases, audit database logs and web access logs for SQLi probes, and rotate credentials where compromise is suspected.
- Confidence: High.

### 12. CVE-2025-53209 - Masteriyo LMS PRO privilege escalation

- Severity: Critical, CVSS 9.8.
- Affected software: Masteriyo LMS PRO <= 2.20.0.
- Exploit availability: Public PoC-style analysis and Patchstack advisory.
- Active exploitation: Not confirmed in this run, but mass exploitation is plausible for WordPress plugin privilege escalation.
- KEV status: Not listed.
- Recommended action: Upgrade to 2.20.1 or later and audit WordPress administrator accounts.
- Confidence: High for vulnerability, Medium for exploitation likelihood.

### 13. CVE-2026-34906 - Wirtualna Uczelnia server-side template injection

- Severity: Critical, CVSS 9.3.
- Affected software: Wirtualna Uczelnia up to `wu#2016.437.295#0#20260327_105545`.
- Exploit availability: No public exploit confirmed during this run.
- Active exploitation: Not observed.
- KEV status: Not listed.
- Recommended action: Patch affected education-sector deployments, restrict access to vulnerable endpoints, and inspect requests to `redirectToUrl` / `redirectUrlParameter`.
- Confidence: High for NVD record.

### 14. CVE-2026-3055 - Citrix NetScaler ADC/Gateway SAML IdP memory overread

- Severity: Critical, CVSS v4 9.3 in Citrix/Horizon3 reporting.
- Affected software: NetScaler ADC/Gateway 13.1 and 14.1 branches configured as SAML IdP.
- Exploit availability: Public technical detail and active scanning/exploitation telemetry.
- Active exploitation: Yes. Fortinet FortiGuard reported persistent exploitation and thousands of daily blocked attempts.
- KEV status: Reported by multiple sources as KEV-listed.
- Recommended action: Upgrade to 14.1-66.59 or later, 13.1-62.23 or later, or 13.1 FIPS/NDcPP 13.1-37.262 or later; rotate exposed session material if compromise is suspected.
- Confidence: High.

## Exploits Released

### Sploitus reconstructed top 10

The Sploitus homepage static fetch did not expose an official "Exploits of the Week" block. The following is reconstructed from indexed Sploitus exploit pages and corroborating searches; entries are indicators, not proof that the code is safe or functional.

| Rank | CVE | Affected software | Exploit type | Maturity | PoC availability | Weaponization potential |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | CVE-2026-20182 | Cisco Catalyst SD-WAN Controller/Manager | Remote auth bypass to admin/NETCONF access | Active exploitation, KEV | Yes, Sploitus indicator | Very high |
| 2 | CVE-2026-41940 | cPanel & WHM | Pre-auth authentication bypass/RCE | Ransomware/botnet use, KEV | Yes, Metasploit/Sploitus/GitHub | Very high |
| 3 | CVE-2026-35616 | FortiClient EMS | Pre-auth API bypass to managed-endpoint code execution | Active exploitation, malware campaign | Yes, Sploitus indicator | Very high |
| 4 | CVE-2026-0257 | PAN-OS GlobalProtect | Authentication bypass via forged override cookie | Active exploitation, KEV | Public/validated PoC indicators | High |
| 5 | CVE-2026-21858 | n8n | Webhook file read leading to session forgery/RCE | Public exploit chain | Yes, Sploitus indicator | High |
| 6 | CVE-2026-42208 | LiteLLM | Pre-auth SQL injection in bearer-token path | KEV/public exploit lab | Yes, multiple Sploitus indicators | High |
| 7 | CVE-2026-9082 | Drupal Core | Error-based SQL injection | ExploitDB, KEV | Yes, EDB-ID 52608 | High |
| 8 | CVE-2026-41091 / CVE-2026-33825 | Microsoft Defender | Local privilege escalation via link-following | KEV for Defender item | Yes, Sploitus indicator | Medium-high |
| 9 | CVE-2026-31431 | Linux kernel Copy Fail | Local privilege escalation | Public PoC/checkers | Yes, Sploitus/GitHub indicators | Medium-high |
| 10 | CVE-2026-43494 | Linux kernel PinTheft | Local privilege escalation via RDS/io_uring | Public PoC | Yes, GitHub indicator | Medium |

### ExploitDB additions

Direct ExploitDB CSV retrieval showed latest high-interest rows by ID:

- EDB-ID 52608: Drupal Core 10.5.5 error-based SQL injection, CVE-2026-9082, unverified in CSV.
- EDB-ID 52607: WordPress OrderConvo 14 path traversal, CVE-2025-10162, unverified in CSV.
- EDB-ID 52606: Notepad++ 8.9.6 arbitrary code execution, CVE-2026-48778, unverified in CSV.
- EDB-ID 52605/52604/52603: YAMCS yamcs-core 5.12.7 no-rate-limit, user-enumeration, and LDAP-injection entries, CVE-2026-44596/CVE-2026-44595/CVE-2026-42568.
- EDB-ID 52601: Microsoft NTLMv2 hash capture, CVE-2026-32202.
- EDB-ID 52600: MikroORM 7.0.13 SQL injection, CVE-2026-44680.

The CSV returned null date fields for these rows, so publication timing should be confirmed with the ExploitDB web interface before using date-sensitive language.

### New GitHub PoC indicators

Strict newly-created query returned no repositories. Broader pushed query found these unvalidated indicators:

- `fartlover37/CVE-2026-2441-PoC` - Chrome Blink CSS use-after-free PoC, updated 2026-06-02 16:01 UTC.
- `hamzamalik3461/CVE-2026-20841` - Windows Notepad URL protocol RCE claim, updated 2026-06-02 15:58 UTC.
- `obrunolima1910/CVE-2026-24061` - GNU inetutils telnetd auth bypass/root-shell claim, updated 2026-06-02 15:45 UTC.
- `yoyosh/DarkReplica` - Redis CVE-2026-23631 exploit indicator, updated 2026-06-02 15:42 UTC.
- `0xABCD01/CVE-2026-41089` - Microsoft Netlogon PoC indicator, updated 2026-06-02 15:52 UTC.
- `Defacto-ridgepole254/CVE-2026-41940-Exploit-PoC` - cPanel/WHM auth bypass PoC indicator.
- `Dullpurple-sloop726/CVE-2026-31431-Linux-Copy-Fail` and `Liverwortenuresis371/copyfail-rs` - Linux Copy Fail LPE indicators.

Treat all GitHub PoCs as potentially malicious until code review and sandbox validation are completed.

## Malware Intelligence

- VX-Underground: `/users/vxunderground/repos` showed `MalwareSourceCode` as the most recently pushed repository, last pushed 2026-05-30 07:11 UTC; no new pushed malware-source update was observed in this run.
- FortiClient EMS / EKZ Infostealer: Arctic Wolf reported exploitation of CVE-2026-35616 to deploy EKZ Infostealer disguised as a Fortinet patch (`FortiEndpoint_Patch.exe` / `p.exe`) through managed endpoint workflows. EKZ targets browser credentials, cookies, and autofill data and exfiltrates over HTTP.
- cPanel / Sorry ransomware: Sploitus-indexed material and prior reporting tie CVE-2026-41940 exploitation to Sorry ransomware and nuclear.x86 botnet/miner activity. Continue hunting for `.sorry` notes, forged cPanel sessions, Go HTTP clients against cPanel ports, and known ELF/miner artifacts.
- Supply chain: Carry forward high priority for CISA KEV supply-chain items Nx Console CVE-2026-48027 and TanStack CVE-2026-45321, both listed with known ransomware use in the CISA feed.

## Security Releases and Vendor Advisories

- Cisco: CVE-2026-20182 fixed releases available; no workaround; Cisco recommends TAC-supported compromise review.
- Palo Alto Networks: CVE-2026-0257 advisory updated 2026-05-29; fixes regenerate GlobalProtect authentication override cookies and require users to re-authenticate once after upgrade.
- Fortinet: CVE-2026-35616 hotfixes for EMS 7.4.5/7.4.6 and full fix in 7.4.7+; pair patching with endpoint compromise review.
- Citrix/NetScaler: CVE-2026-3055 fixed builds available for 14.1, 13.1, and 13.1 FIPS/NDcPP branches.
- Oracle: WebLogic CVE-2024-21182 remains the newest KEV addition with 2026-06-04 due date.
- Progress: NVD published Sitefinity CVE-2026-7312, CVE-2026-7198, CVE-2026-7195, CVE-2026-7201, and CVE-2026-7313 records around 14:17 UTC; direct vendor search did not expose matching advisory pages during this run.
- GitHub Security Advisories: Reviewed advisories query for `published >= 2026-06-02T15:00:00Z` returned no entries.
- ProjectDiscovery: nuclei-templates latest release remains v10.4.4 from 2026-05-28; repository last push observed 2026-06-02 04:33 UTC.

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
    "poc_links": ["https://sploitus.com/exploit?id=13DF22F3-E9C6-58EE-B458-EB585C4D715D"],
    "patch_available": true,
    "sources": ["https://www.cisco.com/c/en/us/support/docs/csa/cisco-sa-sdwan-rpa2-v69WY2SW.html", "https://blog.talosintelligence.com/sd-wan-ongoing-exploitation/", "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"]
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
    "poc_links": ["https://sploitus.com/exploit?id=F57708C0-5A99-5B20-9856-EF70613A9E51"],
    "patch_available": true,
    "sources": ["https://arcticwolf.com/resources/blog/forticlient-ems-exploited-via-cve-2026-35616-to-deliver-ekz-infostealer-disguised-as-a-fortinet-patch/", "https://watchtowr.com/resources/fortinet-forticlient-ems-zero-day-cve-2026-35616-active-exploitation-underway/", "https://horizon3.ai/attack-research/vulnerabilities/cve-2026-35616/"]
  },
  {
    "cve": "CVE-2026-41940",
    "cvss": "9.8",
    "vendor": "WebPros",
    "product": "cPanel & WHM and WP2",
    "affected_versions": "Supported cPanel & WHM versions after 11.40 per public reporting",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://sploitus.com/exploit?id=MSF%3AEXPLOIT-MULTI-HTTP-CPANEL_WHM_AUTH_BYPASS_RCE-", "https://sploitus.com/exploit?id=5594483C-6BE4-5815-989A-419B36AC3894"],
    "patch_available": true,
    "sources": ["https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json", "https://support.cpanel.net/hc/en-us/articles/40073787579671-cPanel-WHM-Security-Update-04-28-2026"]
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
    "sources": ["https://msrc.microsoft.com/update-guide/vulnerability/CVE-2026-41089", "https://www.securityweek.com/critical-windows-netlogon-vulnerability-in-attackers-crosshairs/", "https://dbugs.ptsecurity.com/vulnerability/PT-2026-40234"]
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
    "sources": ["https://services.nvd.nist.gov/rest/json/cves/2.0/?pubStartDate=2026-06-02T00:00:00.000Z&pubEndDate=2026-06-02T16:35:00.000Z"]
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
    "sources": ["https://services.nvd.nist.gov/rest/json/cves/2.0/?pubStartDate=2026-06-02T00:00:00.000Z&pubEndDate=2026-06-02T16:35:00.000Z"]
  },
  {
    "cve": "CVE-2026-8206",
    "cvss": "9.8",
    "vendor": "Kirki",
    "product": "Kirki WordPress plugin",
    "affected_versions": "6.0.0 through 6.0.6",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": false,
    "poc_links": ["https://github.com/Jenderal92/CVE-2026-8206"],
    "patch_available": true,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2026-8206", "https://threat-modeling.com/kirki-wordpress-plugin-account-takeover-cve-2026-8206/"]
  },
  {
    "cve": "CVE-2026-21858",
    "cvss": "10.0",
    "vendor": "n8n",
    "product": "n8n",
    "affected_versions": ">=1.65.0 and <1.121.0",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://sploitus.com/exploit?id=61F5A984-F6DE-5060-8EDF-0256034BFF43"],
    "patch_available": true,
    "sources": ["https://github.com/n8n-io/n8n/security/advisories/GHSA-v4pr-fm98-w9pg", "https://nvd.nist.gov/vuln/detail/CVE-2026-21858"]
  },
  {
    "cve": "CVE-2026-42208",
    "cvss": "9.3",
    "vendor": "BerriAI",
    "product": "LiteLLM",
    "affected_versions": "Affected LiteLLM 1.81.16 through pre-fixed 1.83.7 releases per GHSA",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://sploitus.com/exploit?id=2DA57135-57BB-597F-8C0D-BCCBAEE544E5", "https://sploitus.com/exploit?id=07B8B2D9-F4E3-5CBE-80A3-7287CAAD00E4"],
    "patch_available": true,
    "sources": ["https://github.com/BerriAI/litellm/security/advisories/GHSA-r75f-5x8p-qvmc", "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"]
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
  },
  {
    "cve": "CVE-2025-53209",
    "cvss": "9.8",
    "vendor": "Themeisle",
    "product": "Masteriyo LMS PRO",
    "affected_versions": "<=2.20.0",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://atomicedge.io/cve-proof/cve-2025-53209-learning-management-system-pro-version-2-20-0-critical-vulnerability-proof-of-concept/"],
    "patch_available": true,
    "sources": ["https://patchstack.com/database/wordpress/plugin/learning-management-system-pro/vulnerability/wordpress-masteriyo-lms-pro-2-20-0-privilege-escalation-vulnerability", "https://nvd.nist.gov/vuln/detail/CVE-2025-53209"]
  },
  {
    "cve": "CVE-2026-34906",
    "cvss": "9.3",
    "vendor": "Wirtualna Uczelnia",
    "product": "Wirtualna Uczelnia",
    "affected_versions": "Up to wu#2016.437.295#0#20260327_105545",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://services.nvd.nist.gov/rest/json/cves/2.0/?pubStartDate=2026-06-02T00:00:00.000Z&pubEndDate=2026-06-02T16:35:00.000Z"]
  },
  {
    "cve": "CVE-2026-3055",
    "cvss": "9.3",
    "vendor": "Citrix",
    "product": "NetScaler ADC and NetScaler Gateway",
    "affected_versions": "14.1 before fixed builds, 13.1 before 13.1-62.23, and 13.1 FIPS/NDcPP before 13.1-37.262 when configured as SAML IdP",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://support.citrix.com/external/article/CTX696300/netscaler-adc-and-netscaler-gateway-secu.html", "https://filestore.fortinet.com/fortiguard/outbreak_alert/citrix_netscaler_memory_overread_vulnerability/report.pdf", "https://horizon3.ai/attack-research/vulnerabilities/cve-2026-3055/"]
  }
]
```

## Recommended Actions

1. Emergency patch and hunt: Cisco Catalyst SD-WAN CVE-2026-20182, FortiClient EMS CVE-2026-35616, cPanel/WHM CVE-2026-41940, PAN-OS CVE-2026-0257, Citrix NetScaler CVE-2026-3055, Drupal CVE-2026-9082, and Oracle WebLogic CVE-2024-21182.
2. Patch domain controllers: deploy Microsoft updates for CVE-2026-41089, then hunt for Netlogon/LSASS anomalies. Treat active exploitation confidence as medium until Microsoft or CISA corroborates CCB reporting.
3. Address newly published critical web application/plugin CVEs: Progress Sitefinity CVE-2026-7312/CVE-2026-7198, Kirki CVE-2026-8206, Masteriyo CVE-2025-53209, and Wirtualna Uczelnia CVE-2026-34906.
4. Validate internet exposure for n8n, LiteLLM, and WordPress plugin estates; restrict public access while patching and rotate secrets where file-read or SQLi exposure is plausible.
5. Quarantine and review public PoC repositories before use. Several newly pushed GitHub repositories are likely offensive tooling or could be trojanized.
6. Continue monitoring CISA KEV for post-16:35 UTC updates, because no new KEV additions were visible in catalog version 2026.06.01 during this run.

## Source Notes

- NVD API 2.0, 2026-06-02 15:00-16:35 UTC, day-to-date, and rolling 24-hour windows.
- CISA Known Exploited Vulnerabilities JSON feed, catalog version 2026.06.01.
- Cisco PSIRT and Cisco Talos reporting for CVE-2026-20182.
- Rapid7 and Palo Alto Networks advisory content for CVE-2026-0257.
- Fortinet/watchTowr/Horizon3/Arctic Wolf reporting for CVE-2026-35616 and EKZ Infostealer.
- ExploitDB CSV from exploit-database GitLab mirror.
- GitHub REST API repository and advisory searches.
- VX-Underground GitHub repository metadata.
- Sploitus indexed exploit result pages; top 10 reconstructed because the homepage did not expose an official weekly list to static fetch.
