# Security Intelligence Report - 2026-06-03 03:00 UTC

Report window: 2026-06-03 02:00-03:35 UTC
Repository: dfalt0/Test-cursor-security-automation
Branch: cursor/security-intelligence-agent-03c4

## Executive Summary

- Total CVEs discovered in the current NVD window: 3 new CVEs between 02:00 and 03:35 UTC.
- Day-to-date NVD volume: 12 CVEs on 2026-06-03.
- Rolling 24-hour NVD volume: 217 CVEs, including 12 critical and 66 high severity records.
- Critical findings requiring action: Cisco Catalyst SD-WAN CVE-2026-20182, MCPJam Inspector CVE-2026-23744, cPanel/WHM CVE-2026-41940, FortiClient EMS CVE-2026-35616, GNU Inetutils telnetd CVE-2026-24061, Frigate NVR CVE-2026-25643, Drupal Core CVE-2026-9082, and LiteSpeed cPanel Plugin CVE-2026-48172.
- Active exploitation findings: Cisco SD-WAN CVE-2026-20182, cPanel/WHM CVE-2026-41940, FortiClient EMS CVE-2026-35616, Microsoft Defender CVE-2026-41091/CVE-2026-45498, GNU Inetutils telnetd CVE-2026-24061, Drupal Core CVE-2026-9082, and likely MCPJam Inspector CVE-2026-23744 based on CrowdSec telemetry plus new PoC/exploit publication signals.
- New CISA KEV status: CISA KEV catalog remains at version 2026.06.02. The newest additions are CVE-2022-0492 Linux Kernel cgroups v1 privilege escalation/container escape and CVE-2025-48595 Android Framework integer overflow/local privilege escalation, both added 2026-06-02 and due 2026-06-05.
- Important KEV deadlines today: CVE-2026-41091 and CVE-2026-45498 in Microsoft Defender, plus legacy Microsoft/Adobe/IE vulnerabilities added by CISA on 2026-05-20, are due 2026-06-03.
- Malware and threat activity: MalwareBazaar reports 213 submissions in the past 24 hours with Mirai as the most-seen family. Current malware intelligence includes EKZ Infostealer delivery through exploited FortiClient EMS, cPanel/WHM exploitation leading to Mirai and "Sorry" ransomware, and SANS ISC reporting on SmartApeSG/ClickFix delivery of an unidentified RAT followed by NetSupport RAT.

## Source Collection Notes

- NVD API was queried for the current hour, day-to-date, and rolling 24-hour windows.
- CISA KEV JSON feed was queried directly and parsed.
- GitHub Advisory API returned no advisories newly published after 2026-06-03 02:00 UTC; latest relevant advisories remain the June 1 and late May GitHub Advisory Database entries.
- GitHub repository search found one newly created current-hour PoC repository and several newly pushed exploit indicators; all GitHub-only exploit claims are treated as unvalidated.
- Sploitus homepage returned only its search shell, so Sploitus "top 10" is reconstructed from indexed Sploitus exploit pages.
- Direct ExploitDB CSV fetch succeeded. Latest direct ExploitDB additions remain 2026-06-01 entries for Drupal Core CVE-2026-9082 and WordPress OrderConvo CVE-2025-10162.
- Packet Storm direct date-page fetch returned an anti-abuse block, but Sploitus indexed multiple Packet Storm-sourced entries.
- VX-Underground web root access was not used; GitHub API showed latest MalwareSourceCode commit remains 2026-05-30 adding `Python/Stealer.Python.GMBA.Manipulator.7z`.

## Top Vulnerabilities

### 1. CVE-2026-20182 - Cisco Catalyst SD-WAN Controller/Manager authentication bypass

- Severity: Critical, CVSS 10.0.
- Affected software: Cisco Catalyst SD-WAN Controller and Catalyst SD-WAN Manager.
- Exploit availability: Public exploit references and Sploitus indicators exist; Cisco confirms limited exploitation.
- Active exploitation: Yes. Cisco PSIRT became aware of limited exploitation in May 2026; CISA lists the issue in KEV.
- Recommended action: Run Cisco evidence-preservation guidance where compromise is suspected, collect `request admin-tech` bundles from control components, review control-connection/NETCONF activity, restrict management/control-plane access, and upgrade to a fixed release.
- Confidence: High.
- Sources: https://sec.cloudapps.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-sdwan-rpa2-v69WY2SW, https://www.cisa.gov/known-exploited-vulnerabilities-catalog

### 2. CVE-2026-23744 - MCPJam Inspector unauthenticated RCE

- Severity: Critical, CVSS 9.8.
- Affected software: `@mcpjam/inspector` versions 1.4.2 and earlier.
- Exploit availability: Public PoC/exploit code is available. A new GitHub repository `jf-gondim/mcp-pwn` was created during this report hour and claims a PoC. Sploitus also indexes Packet Storm and GitHub-derived exploit material. ProjectDiscovery has a verified Nuclei template.
- Active exploitation: CrowdSec reports exploitation attempts/surging scans; treat exposed instances as actively targeted.
- Recommended action: Upgrade to 1.4.3 or later, bind the service to 127.0.0.1, block external access to `/api/mcp/connect`, and hunt for unexpected MCP server installation or child-process execution from developer workstations.
- Confidence: High for vulnerability and PoC availability; Medium-High for broad exploitation based on telemetry reporting.
- Sources: https://github.com/MCPJam/inspector/security/advisories/GHSA-232v-j27c-5pp6, https://nvd.nist.gov/vuln/detail/CVE-2026-23744, https://raw.githubusercontent.com/projectdiscovery/nuclei-templates/main/http/cves/2026/CVE-2026-23744.yaml, https://www.crowdsec.net/vulntracking-report/cve-2026-23744, https://sploitus.com/exploit?id=PACKETSTORM%3A217697

### 3. CVE-2026-41940 - cPanel/WHM authentication bypass and RCE

- Severity: Critical, CVSS 9.8.
- Affected software: cPanel & WHM and WP2.
- Exploit availability: Metasploit module, standalone PoCs, Sploitus entries, and GitHub indicators are public.
- Active exploitation: Yes. CISA KEV lists known ransomware use; reporting links exploitation to Mirai deployment and "Sorry" ransomware.
- Recommended action: Patch cPanel/WHM to fixed branches immediately, hunt for unauthorized WHM sessions/session-file anomalies, review SSH key or account changes, and investigate `.sorry` ransomware indicators and Mirai post-compromise activity.
- Confidence: High.
- Sources: https://www.cisa.gov/known-exploited-vulnerabilities-catalog, https://sploitus.com/exploit?id=MSF%3AEXPLOIT-MULTI-HTTP-CPANEL_WHM_AUTH_BYPASS_RCE-, https://www.secpod.com/blog/the-cpanel-crisis-one-bug-millions-exposed-as-mirai-and-sorry-ransomware-deploy-in-24-hours/

### 4. CVE-2026-35616 - FortiClient EMS pre-authentication API bypass to endpoint code execution

- Severity: Critical, CVSS 9.1.
- Affected software: FortiClient EMS 7.4.5 and 7.4.6.
- Exploit availability: Sploitus indexes exploit material; the issue is exploited in the wild.
- Active exploitation: Yes. Arctic Wolf reports exploitation to deploy EKZ Infostealer disguised as a Fortinet patch.
- Recommended action: Apply Fortinet hotfixes or upgrade to a fixed release, review EMS administrative/API activity, hunt for malicious PowerShell pushed through FortiClient management workflows, and rotate browser/SSO credentials from managed endpoints that may have received EKZ.
- Confidence: High.
- Sources: https://arcticwolf.com/resources/blog/forticlient-ems-exploited-via-cve-2026-35616-to-deliver-ekz-infostealer-disguised-as-a-fortinet-patch/, https://sploitus.com/exploit?id=F57708C0-5A99-5B20-9856-EF70613A9E51

### 5. CVE-2026-24061 - GNU Inetutils telnetd authentication bypass

- Severity: Critical, CVSS 9.8.
- Affected software: GNU Inetutils telnetd versions 1.9.3 through 2.7.
- Exploit availability: Metasploit module, public GitHub PoCs, Sploitus entries, and Rapid7 module are available.
- Active exploitation: GreyNoise observed exploitation shortly after disclosure and continued telnet-focused scanning; a newly pushed GitHub exploit indicator appeared during this report window.
- Recommended action: Disable telnetd wherever possible, block TCP/23 at boundaries, upgrade to a fixed Inetutils release, and hunt for TELNET NEW-ENVIRON `USER` values beginning with `-f`.
- Confidence: High.
- Sources: https://www.rapid7.com/db/modules/exploit/linux/telnet/gnu_inetutils_auth_bypass/, https://www.labs.greynoise.io/grimoire/2026-02-10-telnet-falls-silent/, https://sploitus.com/exploit?id=MSF%3AEXPLOIT-LINUX-TELNET-GNU_INETUTILS_AUTH_BYPASS-

### 6. CVE-2026-25643 - Frigate NVR authenticated RCE and container escape risk

- Severity: Critical.
- Affected software: Frigate NVR prior to 0.16.4.
- Exploit availability: Public exploit and Packet Storm/Sploitus entries exist; GitHub repo `DyniePro/CVE-2026-25643` was pushed during this report hour.
- Active exploitation: No confirmed active exploitation in primary sources reviewed, but exploit maturity is high.
- Recommended action: Upgrade to Frigate 0.16.4 or later, ensure Frigate is not exposed without authentication, remove unsafe `exec:` stream configuration, and reduce container privileges.
- Confidence: High for vulnerability and exploit availability; Medium for exploitation status.
- Sources: https://github.com/blakeblackshear/frigate/security/advisories/GHSA-4c97-5jmr-8f6x, https://nvd.nist.gov/vuln/detail/CVE-2026-25643, https://sploitus.com/exploit?id=PACKETSTORM%3A216188

### 7. CVE-2026-9082 - Drupal Core PostgreSQL SQL injection

- Severity: Drupal rates highly critical; NVD CVSS observed as medium due to scoring context.
- Affected software: Drupal Core PostgreSQL-backed deployments in affected 8.x through 11.x ranges.
- Exploit availability: ExploitDB EDB-ID 52608 and multiple Sploitus-indexed PoCs/scanners.
- Active exploitation: CISA KEV-listed in recent reporting and widely weaponized PoC availability; treat internet-facing PostgreSQL-backed Drupal as high priority.
- Recommended action: Upgrade to fixed Drupal releases, prioritize PostgreSQL-backed and JSON:API-enabled sites, and review web logs for malformed JSON:API filter array keys and SQL error responses.
- Confidence: High for exploit availability; High for KEV status based on CISA catalog carry-forward.
- Sources: https://sploitus.com/exploit?id=EDB-ID%3A52608, https://gitlab.com/exploit-database/exploitdb/-/raw/main/files_exploits.csv, https://www.drupal.org/sa-core-2026-004

### 8. CVE-2026-41091 and CVE-2026-45498 - Microsoft Defender exploited flaws due today

- Severity: High/Medium operational urgency due to KEV and active exploitation.
- Affected software: Microsoft Malware Protection Engine and Microsoft Defender Antimalware Platform.
- Exploit availability: Publicly disclosed and exploited in the wild per Microsoft/CISA reporting.
- Active exploitation: Yes.
- Recommended action: Verify Malware Protection Engine version at least 1.1.26040.8 and Antimalware Platform version at least 4.18.26040.7 across all Windows endpoints and servers.
- Confidence: High.
- Sources: https://www.helpnetsecurity.com/2026/05/21/microsoft-defender-vulnerabilities-cve-2026-41091-cve-2026-45498/, https://www.cisa.gov/known-exploited-vulnerabilities-catalog

### 9. CVE-2026-10704 - SourceCodester Pizzafy E-Commerce System SQL injection

- Severity: High, CVSS 7.3.
- Affected software: SourceCodester Pizzafy E-Commerce System 1.0 administrative login component `/admin/admin_class_novo.php`.
- Exploit availability: NVD states public exploit disclosure; NVD references a GitHub write-up.
- Active exploitation: No active exploitation confirmed.
- Recommended action: Remove internet exposure for the admin panel, apply vendor or community patch if available, replace raw SQL handling with parameterized queries, and monitor for SQLi payloads in admin login requests.
- Confidence: Medium. NVD/VulDB data is current, but secondary search indexes lagged or confused this ID with older Pizzafy CVEs.
- Sources: https://nvd.nist.gov/vuln/detail/CVE-2026-10704, https://github.com/nuiifornet/A033/blob/main/pizzafy-vulnerability.md

### 10. CVE-2026-10703 - EIPStackGroup OpENer use-after-free

- Severity: Medium, CVSS 6.3.
- Affected software: EIPStackGroup OpENer up to 2.3.0, SendRRData Handler in `cipmessagerouter.c`.
- Exploit availability: NVD states public PoC availability and references `poc.zip` in the GitHub issue.
- Active exploitation: No active exploitation confirmed.
- Recommended action: Segment EtherNet/IP/CIP traffic, restrict access to trusted industrial networks, review issue 566 and vendor response, and patch or disable exposed OpENer services where possible.
- Confidence: Medium.
- Sources: https://nvd.nist.gov/vuln/detail/CVE-2026-10703, https://github.com/EIPStackGroup/OpENer/issues/566

## Exploits Released

### Sploitus Top 10 (reconstructed from indexed pages)

| Rank | CVE | Affected software | Exploit type | Exploit maturity | Public PoC | Weaponization potential |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | CVE-2026-23744 | MCPJam Inspector <= 1.4.2 | Unauthenticated RCE via `/api/mcp/connect` | Packet Storm/Sploitus/GitHub/Nuclei | Yes | Critical for exposed developer workstations and AI tooling |
| 2 | CVE-2026-41940 | cPanel/WHM | CRLF/session auth bypass to WHM/root | Metasploit and standalone frameworks | Yes | Critical; ransomware and Mirai post-compromise observed |
| 3 | CVE-2026-24061 | GNU Inetutils telnetd | Remote auth bypass to root shell | Metasploit/Rapid7/GitHub | Yes | Critical for legacy/embedded/OT telnet exposure |
| 4 | CVE-2026-25643 | Frigate NVR <= 0.16.3 | Config injection RCE/container escape | Packet Storm/Sploitus/GitHub | Yes | High where Frigate is internet-exposed or admin creds are compromised |
| 5 | CVE-2026-35616 | FortiClient EMS 7.4.5/7.4.6 | Pre-auth API bypass to managed endpoint code execution | Exploited in the wild; Sploitus PoC | Yes | Critical because EMS can push code to many endpoints |
| 6 | CVE-2026-9082 | Drupal Core PostgreSQL backend | SQL injection via JSON:API/entity query | ExploitDB 52608 and multiple PoCs | Yes | High-to-critical depending on database permissions/config |
| 7 | CVE-2026-31431 | Linux Kernel "Copy Fail" | Local privilege escalation/page-cache write | Multiple Sploitus/GitHub PoCs | Yes | High for servers/containers where AF_ALG and SUID path are reachable |
| 8 | CVE-2026-48172 | LiteSpeed cPanel Plugin | Privilege escalation/auditor tooling | Sploitus indexed | Yes | High on shared hosting/cPanel servers |
| 9 | CVE-2026-48778 | Notepad++ 8.9.6 | User-assisted arbitrary code execution | Packet Storm/Sploitus | Yes | Medium; depends on user action/config abuse |
| 10 | CVE-2026-48800 | Notepad++ <= 8.9.6 | User-assisted arbitrary code execution via shortcuts.xml | Sploitus/GitHub advisory | Yes | Medium; phishing or local file manipulation path |

### ExploitDB additions

- Latest direct ExploitDB CSV entries added/published on 2026-06-01:
  - EDB-ID 52608: Drupal Core 10.5.5 error-based SQL injection, CVE-2026-9082.
  - EDB-ID 52607: WordPress OrderConvo 14 path traversal, CVE-2025-10162.
- No direct ExploitDB CSV row newer than 2026-06-01 was present at collection time.

### New GitHub PoC and exploit indicators

- `jf-gondim/mcp-pwn`: created 2026-06-03T02:31:57Z, pushed 2026-06-03T02:47:15Z. Claims PoC exploit for CVE-2026-23744 MCPJam Inspector unauthenticated RCE. Treat as unvalidated but high-priority due to corroborating primary advisory, Sploitus, Packet Storm, and Nuclei template signals.
- `DyniePro/CVE-2026-25643`: pushed 2026-06-03T02:57:50Z. Claims Frigate NVR RCE exploit. Treat as unvalidated but corroborated by primary GitHub advisory and Sploitus/Packet Storm.
- `obrunolima1910/CVE-2026-24061`: pushed 2026-06-03T02:39:12Z. Claims GNU inetutils telnetd auth bypass exploit. Treat as unvalidated; mature exploit material already exists in Metasploit/Rapid7.
- `Dullpurple-sloop726/CVE-2026-31431-Linux-Copy-Fail`: pushed 2026-06-03T00:48:07Z. Copy Fail LPE exploit indicator.
- `Defacto-ridgepole254/CVE-2026-41940-Exploit-PoC`: pushed 2026-06-03T00:48:30Z. cPanel/WHM auth bypass PoC indicator.
- `tracyliving606/RegPwn`: pushed 2026-06-03T00:24:20Z. Claims Windows LPE for CVE-2026-24291.
- `Liverwortenuresis371/copyfail-rs`: pushed 2026-06-03T00:47:14Z. Copy Fail/CVE-2026-31431 Rust exploit/detection indicator.

## Malware Intelligence

- VX-Underground: Latest GitHub push in `vxunderground/MalwareSourceCode` remains 2026-05-30, adding `Python/Stealer.Python.GMBA.Manipulator.7z`. No newer pushed malware source release was observed.
- MalwareBazaar: 213 submissions in the past 24 hours; Mirai is the most-seen family.
- EKZ Infostealer: Arctic Wolf reports FortiClient EMS exploitation (CVE-2026-35616) used to deploy a fake Fortinet endpoint patch that steals browser credentials, cookies, and autofill data. This is high-risk because EMS can distribute payloads through trusted endpoint-management workflows.
- cPanel/WHM malware and ransomware: CVE-2026-41940 exploitation is associated with Mirai deployment and "Sorry" ransomware. Sploitus indexed public IOC/YARA/forensic material for the Sorry ransomware campaign.
- SmartApeSG/ClickFix: SANS ISC reports an unidentified RAT that installs NetSupport RAT, with traffic to `89.110.110[.]119:443` and NetSupport RAT C2 at `185.163.47[.]217:443`.
- Phishing: SANS ISC/secondary reporting describes SVG phishing using `application/ecmascript` MIME evasion to bypass attachment/script detection rules and redirect victims in the browser.

## Security Releases and Vendor Advisories

- Microsoft: Defender exploited flaws CVE-2026-41091 and CVE-2026-45498 are due in CISA KEV today. Verify Malware Protection Engine >= 1.1.26040.8 and Antimalware Platform >= 4.18.26040.7.
- Cisco: Catalyst SD-WAN CVE-2026-20182 has fixed releases; no workaround fully remediates. Follow Cisco TAC evidence-preservation guidance before remediation if compromise is suspected.
- Fortinet: FortiClient EMS CVE-2026-35616 has hotfix/full-fix guidance; exploited for EKZ Infostealer delivery.
- GitLab: Security versions 19.0.1, 18.11.4, and 18.10.7, released 2026-05-27, address multiple Duo AI, Wiki DoS, GraphQL/API authorization, Operations, Pipeline, and authentication endpoint vulnerabilities. Self-managed GitLab should upgrade.
- GitHub: GitHub Advisory API showed no advisories newly published after 02:00 UTC. Relevant carry-forward: GHES 3.20.3 and maintained branches address critical/high issues including CVE-2026-9312 and CVE-2026-8606; GitHub Advisory Database also shows critical PraisonAI Platform and Axios CVE-2026-44494 advisories from late May/June 1.
- VMware/Broadcom: Recent advisory coverage includes VMware Tanzu for Valkey versions prior to 7.2.13, 8.0.9, 8.1.7, and 9.0.4; apply the Broadcom-recommended updates.
- Drupal: Apply fixed Drupal Core releases for SA-CORE-2026-004/CVE-2026-9082, especially PostgreSQL-backed deployments.
- cPanel/WebPros and LiteSpeed: Patch cPanel/WHM CVE-2026-41940 immediately and upgrade LiteSpeed User-End cPanel Plugin >= 2.4.7 and WHM Plugin >= 5.3.1.0 for CVE-2026-48172.

## Unified Vulnerability Records

```json
[
  {
    "cve": "CVE-2026-20182",
    "cvss": "10.0",
    "vendor": "Cisco",
    "product": "Catalyst SD-WAN Controller and Manager",
    "affected_versions": "Affected Catalyst SD-WAN Controller/Manager releases per Cisco advisory",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://sploitus.com/search?query=CVE-2026-20182"],
    "patch_available": true,
    "sources": ["https://sec.cloudapps.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-sdwan-rpa2-v69WY2SW", "https://www.cisa.gov/known-exploited-vulnerabilities-catalog"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-23744",
    "cvss": "9.8",
    "vendor": "MCPJam",
    "product": "Inspector",
    "affected_versions": "<= 1.4.2",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": false,
    "poc_links": ["https://github.com/jf-gondim/mcp-pwn", "https://sploitus.com/exploit?id=PACKETSTORM%3A217697", "https://raw.githubusercontent.com/projectdiscovery/nuclei-templates/main/http/cves/2026/CVE-2026-23744.yaml"],
    "patch_available": true,
    "sources": ["https://github.com/MCPJam/inspector/security/advisories/GHSA-232v-j27c-5pp6", "https://nvd.nist.gov/vuln/detail/CVE-2026-23744", "https://www.crowdsec.net/vulntracking-report/cve-2026-23744"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-41940",
    "cvss": "9.8",
    "vendor": "WebPros",
    "product": "cPanel & WHM and WP2",
    "affected_versions": "Multiple cPanel/WHM branches before fixed releases",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://sploitus.com/exploit?id=MSF%3AEXPLOIT-MULTI-HTTP-CPANEL_WHM_AUTH_BYPASS_RCE-", "https://sploitus.com/exploit?id=45A263F9-3CDF-57F8-9637-E0D5F28635FF"],
    "patch_available": true,
    "sources": ["https://www.cisa.gov/known-exploited-vulnerabilities-catalog", "https://www.secpod.com/blog/the-cpanel-crisis-one-bug-millions-exposed-as-mirai-and-sorry-ransomware-deploy-in-24-hours/"],
    "confidence": "High"
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
    "sources": ["https://arcticwolf.com/resources/blog/forticlient-ems-exploited-via-cve-2026-35616-to-deliver-ekz-infostealer-disguised-as-a-fortinet-patch/"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-24061",
    "cvss": "9.8",
    "vendor": "GNU",
    "product": "Inetutils telnetd",
    "affected_versions": "1.9.3 through 2.7",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://www.rapid7.com/db/modules/exploit/linux/telnet/gnu_inetutils_auth_bypass/", "https://sploitus.com/exploit?id=MSF%3AEXPLOIT-LINUX-TELNET-GNU_INETUTILS_AUTH_BYPASS-", "https://github.com/obrunolima1910/CVE-2026-24061"],
    "patch_available": true,
    "sources": ["https://www.labs.greynoise.io/grimoire/2026-02-10-telnet-falls-silent/", "https://www.rapid7.com/db/modules/exploit/linux/telnet/gnu_inetutils_auth_bypass/"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-25643",
    "cvss": "Critical",
    "vendor": "Blake Blackshear",
    "product": "Frigate NVR",
    "affected_versions": "Prior to 0.16.4",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://github.com/DyniePro/CVE-2026-25643", "https://sploitus.com/exploit?id=PACKETSTORM%3A216188"],
    "patch_available": true,
    "sources": ["https://github.com/blakeblackshear/frigate/security/advisories/GHSA-4c97-5jmr-8f6x", "https://nvd.nist.gov/vuln/detail/CVE-2026-25643"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-9082",
    "cvss": "6.5 / Drupal highly critical",
    "vendor": "Drupal",
    "product": "Drupal Core",
    "affected_versions": "PostgreSQL-backed Drupal Core 8.x through affected 11.x versions before fixed releases",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://sploitus.com/exploit?id=EDB-ID%3A52608"],
    "patch_available": true,
    "sources": ["https://www.drupal.org/sa-core-2026-004", "https://gitlab.com/exploit-database/exploitdb/-/raw/main/files_exploits.csv"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-41091",
    "cvss": "7.8",
    "vendor": "Microsoft",
    "product": "Defender Malware Protection Engine",
    "affected_versions": "< 1.1.26040.8",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://www.helpnetsecurity.com/2026/05/21/microsoft-defender-vulnerabilities-cve-2026-41091-cve-2026-45498/", "https://www.cisa.gov/known-exploited-vulnerabilities-catalog"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-45498",
    "cvss": "4.0",
    "vendor": "Microsoft",
    "product": "Defender Antimalware Platform",
    "affected_versions": "< 4.18.26040.7",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://www.helpnetsecurity.com/2026/05/21/microsoft-defender-vulnerabilities-cve-2026-41091-cve-2026-45498/", "https://www.cisa.gov/known-exploited-vulnerabilities-catalog"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2022-0492",
    "cvss": "High",
    "vendor": "Linux",
    "product": "Kernel",
    "affected_versions": "Kernels exposing cgroups v1 release_agent privilege escalation path",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://www.cisa.gov/known-exploited-vulnerabilities-catalog", "https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=24f6008564183aa120d07c03d9289519c2fe02af"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2025-48595",
    "cvss": "High",
    "vendor": "Android",
    "product": "Framework",
    "affected_versions": "Android Framework versions covered by June 2026 bulletin",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://www.cisa.gov/known-exploited-vulnerabilities-catalog", "https://source.android.com/docs/security/bulletin/2026/2026-06-01"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-48172",
    "cvss": "9.8",
    "vendor": "LiteSpeed Technologies",
    "product": "LiteSpeed cPanel Plugin and WHM Plugin",
    "affected_versions": "User-End cPanel Plugin < 2.4.7; WHM Plugin < 5.3.1.0",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://sploitus.com/exploit?id=36AAEAF3-4B32-5BE1-817C-7C65B5B446FE"],
    "patch_available": true,
    "sources": ["https://blog.litespeedtech.com/2026/05/21/security-update-for-litespeed-cpanel-plugin/", "https://www.cisa.gov/known-exploited-vulnerabilities-catalog"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-10704",
    "cvss": "7.3",
    "vendor": "SourceCodester",
    "product": "Pizzafy E-Commerce System",
    "affected_versions": "1.0",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://github.com/nuiifornet/A033/blob/main/pizzafy-vulnerability.md"],
    "patch_available": false,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2026-10704", "https://vuldb.com/vuln/368017"],
    "confidence": "Medium"
  },
  {
    "cve": "CVE-2026-10703",
    "cvss": "6.3",
    "vendor": "EIPStackGroup",
    "product": "OpENer",
    "affected_versions": "up to 2.3.0",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://github.com/EIPStackGroup/OpENer/issues/566"],
    "patch_available": false,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2026-10703", "https://github.com/EIPStackGroup/OpENer/issues/566"],
    "confidence": "Medium"
  },
  {
    "cve": "CVE-2026-10705",
    "cvss": "3.1",
    "vendor": "Dask",
    "product": "Dask dataframe HLL handler",
    "affected_versions": "up to 3.0",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": false,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2026-10705", "https://github.com/dask/dask/issues/12403", "https://github.com/dask/dask/pull/12401"],
    "confidence": "Medium"
  },
  {
    "cve": "CVE-2026-10690",
    "cvss": "6.3",
    "vendor": "wonderwhy-er",
    "product": "DesktopCommanderMCP",
    "affected_versions": "0.2.37",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://github.com/wonderwhy-er/DesktopCommanderMCP/issues/410"],
    "patch_available": true,
    "sources": ["https://github.com/wonderwhy-er/DesktopCommanderMCP/issues/410", "https://nvd.nist.gov/vuln/detail/CVE-2026-10690"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-10691",
    "cvss": "4.3",
    "vendor": "wonderwhy-er",
    "product": "DesktopCommanderMCP",
    "affected_versions": "up to 0.2.38",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2026-10691"],
    "confidence": "Medium"
  }
]
```

## Recommended Actions

1. Patch and hunt Cisco Catalyst SD-WAN CVE-2026-20182 immediately. Preserve evidence before remediation where compromise is suspected.
2. Remove internet exposure and upgrade MCPJam Inspector to 1.4.3+; deploy the ProjectDiscovery Nuclei template only in authorized environments to find exposed instances.
3. Patch cPanel/WHM CVE-2026-41940 and hunt for unauthorized WHM access, Mirai payloads, and "Sorry" ransomware indicators.
4. Patch FortiClient EMS CVE-2026-35616, audit EMS policy/script changes, and rotate credentials from endpoints that may have received EKZ Infostealer.
5. Verify Microsoft Defender fixed engine/platform versions today because CVE-2026-41091 and CVE-2026-45498 hit the KEV due date.
6. Disable or patch GNU Inetutils telnetd; block TCP/23 and monitor NEW-ENVIRON `USER=-f` patterns.
7. Upgrade Frigate NVR to 0.16.4+ and ensure no unauthenticated internet exposure exists.
8. Patch Drupal Core PostgreSQL-backed deployments for CVE-2026-9082; review JSON:API logs for SQLi probes.
9. Remediate CISA's newest KEV additions: Linux cgroups CVE-2022-0492 and Android Framework CVE-2025-48595 by 2026-06-05.
10. Triage current-hour NVD items CVE-2026-10704, CVE-2026-10703, and CVE-2026-10705 according to asset exposure; prioritize Pizzafy only if deployed or externally reachable.

## Appendix: Current-Hour NVD CVEs

| CVE | Published | Severity | Summary |
| --- | --- | --- | --- |
| CVE-2026-10703 | 2026-06-03T02:16:15.660 | Medium 6.3 | EIPStackGroup OpENer up to 2.3.0 use-after-free in SendRRData Handler; NVD references public PoC. |
| CVE-2026-10704 | 2026-06-03T02:16:17.200 | High 7.3 | SourceCodester Pizzafy E-Commerce System 1.0 SQL injection in admin login path; public exploit disclosed. |
| CVE-2026-10705 | 2026-06-03T02:16:17.397 | Low 3.1 | Dask `nunique_approx` resource-consumption issue; exploitation difficult and fix PR pending. |
