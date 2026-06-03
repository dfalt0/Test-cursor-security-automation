# Security Intelligence Report - 2026-06-03 04:00 UTC

Report window: 2026-06-03 03:00-04:35 UTC
Repository: dfalt0/Test-cursor-security-automation
Branch: cursor/security-intelligence-agent-42ab

## Executive Summary

- Total CVEs discovered in the current NVD window: 0 new CVEs between 03:00 and 04:35 UTC.
- Day-to-date NVD volume: 12 CVEs on 2026-06-03 (4 medium, 6 low, 2 unknown severity).
- Rolling 24-hour NVD volume: 213 CVEs, including 13 critical and 76 high severity records.
- Critical findings requiring action: Cisco Catalyst SD-WAN CVE-2026-20182, cPanel/WHM CVE-2026-41940, MCPJam Inspector CVE-2026-23744, Progress Sitefinity CVE-2026-7312/CVE-2026-7198, authentik CVE-2026-49448, LibreChat CVE-2026-32625, Spacelabs Sentinel CVE-2026-0611, and OpenMed CVE-2026-47117.
- Active exploitation findings: Cisco SD-WAN CVE-2026-20182, cPanel/WHM CVE-2026-41940, Drupal Core CVE-2026-9082, Microsoft Defender CVE-2026-41091/CVE-2026-45498, Linux Kernel CVE-2022-0492, Android Framework CVE-2025-48595, and likely MCPJam Inspector CVE-2026-23744 based on public PoC publication plus CrowdSec exploitation-attempt telemetry.
- New CISA KEV status: CISA KEV catalog remains at version 2026.06.02. The newest additions are CVE-2022-0492 Linux Kernel cgroups v1 privilege escalation/container escape and CVE-2025-48595 Android Framework integer overflow/local privilege escalation, both added 2026-06-02 and due 2026-06-05.
- Malware and threat activity: MalwareBazaar reports 201 submissions in the past 24 hours with Mirai as the most-seen family. Current malware intelligence includes cPanel/WHM exploitation leading to Mirai and "Sorry" ransomware, SANS ISC reporting on SmartApeSG/ClickFix delivery of an unidentified RAT followed by NetSupport RAT, SVG phishing using ECMAScript MIME evasion, and Sophos reporting an AI-assisted malware/EDR-evasion lab linked to ransomware and data theft operations.

## Source Collection Notes

- NVD API was queried for the current hour, day-to-date, and rolling 24-hour windows.
- CISA KEV JSON feed was queried directly and parsed.
- GitHub Advisory API showed no advisories newly published after 2026-06-03 03:00 UTC; latest API results remained June 1 and late May GitHub Advisory Database entries. NVD references were used for June 2 GitHub-origin advisories such as authentik and LibreChat.
- GitHub repository search found one newly created current-day MCPJam PoC repository and multiple pushed-today exploit indicators; all GitHub-only exploit claims are treated as unvalidated until corroborated.
- Sploitus homepage returned only its search shell, so Sploitus "Top 10" is reconstructed from indexed Sploitus exploit pages and correlated exploit-feed results rather than an official homepage block.
- Direct ExploitDB CSV fetch succeeded. Latest direct ExploitDB additions remain 2026-06-01 entries for Drupal Core CVE-2026-9082 and WordPress OrderConvo CVE-2025-10162.
- Packet Storm direct fetch was not relied on as a primary source in this run; prior runs observed anti-abuse blocks. Packet Storm-sourced entries are cited only when Sploitus or search indexing exposes them.
- VX-Underground GitHub API showed latest `vxunderground/MalwareSourceCode` push remains 2026-05-30. No newer malware source release was observed in the VX GitHub organization/user repositories checked.

## Top Vulnerabilities

### 1. CVE-2026-20182 - Cisco Catalyst SD-WAN Controller/Manager authentication bypass

- Severity: Critical, CVSS 10.0.
- Affected software: Cisco Catalyst SD-WAN Controller and Catalyst SD-WAN Manager.
- Exploit availability: Public exploit references and Sploitus indicators exist; Cisco confirms limited exploitation.
- Active exploitation: Yes. Cisco PSIRT became aware of limited exploitation in May 2026; CISA lists the issue in KEV.
- Recommended action: Run Cisco evidence-preservation guidance where compromise is suspected, collect `request admin-tech` bundles from control components, review control-connection and NETCONF activity, restrict management/control-plane access, and upgrade to a fixed release.
- Confidence: High.
- Sources: https://sec.cloudapps.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-sdwan-rpa2-v69WY2SW, https://www.cisa.gov/known-exploited-vulnerabilities-catalog

### 2. CVE-2026-41940 - cPanel/WHM authentication bypass and RCE

- Severity: Critical, CVSS 9.8.
- Affected software: cPanel & WHM and WP2/WP Squared.
- Exploit availability: Standalone PoCs and GitHub indicators are public; Sploitus has indexed cPanel exploit material in previous runs.
- Active exploitation: Yes. CISA KEV lists known ransomware use. Multiple reports link exploitation to "Sorry" ransomware, Mirai variants, crypto-mining, backdoor deployment, and credential theft.
- Recommended action: Patch cPanel/WHM and WP Squared immediately, assume internet-facing unpatched servers may be compromised, review `/var/cpanel/sessions/raw/`, audit WHM users and SSH keys, rotate credentials, and hunt for `.sorry` encrypted files and Mirai/nuclear.x86 indicators.
- Confidence: High for exploitation and ransomware risk; Medium for exact exposed-host counts from secondary reporting.
- Sources: https://www.cisa.gov/known-exploited-vulnerabilities-catalog, https://support.cpanel.net/hc/en-us/articles/40073787579671-cPanel-WHM-Security-Update-04-28-2026, https://www.bitsight.com/blog/critical-vulnerability-alert-cve-2026-41940-cPanel-WHM-WPSquared, https://cybelangel.com/blog/cve-2026-41940-mass-cpanel-attack-hits-40-000-servers/

### 3. CVE-2026-23744 - MCPJam Inspector unauthenticated RCE

- Severity: Critical, CVSS 9.8.
- Affected software: `@mcpjam/inspector` versions 1.4.2 and earlier.
- Exploit availability: Public PoC/exploit code is available. GitHub repository `jf-gondim/mcp-pwn` was created 2026-06-03 and claims a PoC. The GitHub advisory itself includes a curl PoC.
- Active exploitation: CrowdSec reports exploitation attempts and scanning for exposed MCPJam Inspector instances. Treat externally reachable developer tooling as actively targeted.
- Recommended action: Upgrade to 1.4.3 or later where available, bind the service to 127.0.0.1, block external access to `/api/mcp/connect`, and hunt for unexpected MCP server installation or child-process execution from developer workstations.
- Confidence: High for vulnerability and PoC availability; Medium-High for broad exploitation based on telemetry reporting.
- Sources: https://github.com/MCPJam/inspector/security/advisories/GHSA-232v-j27c-5pp6, https://nvd.nist.gov/vuln/detail/CVE-2026-23744, https://www.crowdsec.net/vulntracking-report/cve-2026-23744, https://github.com/jf-gondim/mcp-pwn

### 4. CVE-2026-7312 and CVE-2026-7198 - Progress Sitefinity critical web-service flaws

- Severity: Critical, CVSS 10.0 for CVE-2026-7312 and 9.8 for CVE-2026-7198.
- Affected software: Progress Sitefinity CMS and Sitefinity Insight, including supported 14.x and 15.x branches and older supported/retired ranges noted by Progress.
- Exploit availability: No public exploit repo was found in current GitHub searches for CVE-2026-7312; exploit maturity remains lower than the cPanel/MCPJam items.
- Active exploitation: No active exploitation confirmed in the sources reviewed.
- Recommended action: Apply Progress product updates for supported branches, prioritize internet-facing Sitefinity OData/ServiceStack deployments, and review exposed credential-handling and access-control paths.
- Confidence: High for vulnerability and patch availability; Medium for exploitation status.
- Sources: https://community.progress.com/s/article/Sitefinity-Security-Advisory-for-Addressing-Security-Vulnerabilities-CVE-2026-7312-CVE-2026-7198-CVE-2026-7195-CVE-2026-7201-CVE-2026-7313-May-2026, https://nvd.nist.gov/vuln/detail/CVE-2026-7312, https://nvd.nist.gov/vuln/detail/CVE-2026-7198

### 5. CVE-2026-49448 - authentik SourceStage bypass

- Severity: Critical, CVSS 9.8.
- Affected software: authentik <= 2025.12.5, <= 2026.2.3, and <= 2026.5.0.
- Exploit availability: Public GitHub Security Advisory includes detailed vulnerable flow and PoC test logic.
- Active exploitation: No active exploitation confirmed in the reviewed sources.
- Recommended action: Upgrade to authentik 2025.12.6, 2026.2.4, or 2026.5.1; review authentication flows using Source stages; hunt for anomalous empty POSTs to flow executor endpoints and unexpected sessions without IdP interaction.
- Confidence: High.
- Sources: https://github.com/goauthentik/authentik/security/advisories/GHSA-xp7f-xjjx-gwm8, https://nvd.nist.gov/vuln/detail/CVE-2026-49448

### 6. CVE-2026-32625 - LibreChat MCP server URL secret exfiltration

- Severity: Critical, CVSS 9.6.
- Affected software: LibreChat <= 0.8.3.
- Exploit availability: Public GitHub Security Advisory includes PoC curl flow for leaking `JWT_SECRET`, `CREDS_KEY`, and `CREDS_IV` through attacker-controlled MCP server URLs.
- Active exploitation: No active exploitation confirmed in the reviewed sources.
- Recommended action: Upgrade to v0.8.4-rc1 or later, remove environment-variable expansion from untrusted MCP server URL input, rotate exposed secrets if vulnerable instances allowed low-privileged user registration, and review outbound HTTP requests containing secret values.
- Confidence: High.
- Sources: https://github.com/danny-avila/LibreChat/security/advisories/GHSA-4pcc-j6m6-wcwx, https://nvd.nist.gov/vuln/detail/CVE-2026-32625

### 7. CVE-2026-0611 - Spacelabs Sentinel unauthenticated RCE

- Severity: Critical, CVSS 9.2.
- Affected software: Spacelabs Sentinel 10.5.x and 11.x.x before fixed 11.6.x releases.
- Exploit availability: Vendor advisory says the issue was reproducible with a proof-of-concept exploit supplied through VulnCheck/GM SecTec collaboration.
- Active exploitation: No active exploitation confirmed in reviewed sources.
- Recommended action: Upgrade Sentinel to 11.6.2, block port 8989, keep Sentinel off the public internet, segment clinical networks, and monitor for arbitrary file read/write behavior on Sentinel hosts.
- Confidence: High for vulnerability and patch; Medium for exploit availability because the PoC is referenced but not publicly hosted in the reviewed sources.
- Sources: https://spacelabshealthcare.com/wp-content/uploads/2026/06/079-0273-00-RevA-Security-Advisory-Sentinel-.NET-Remoting-Vulnerability.pdf, https://www.vulncheck.com/advisories/spacelabs-healthcare-sentinel-x-unauthenticated-rce-via-net-remoting, https://nvd.nist.gov/vuln/detail/CVE-2026-0611

### 8. CVE-2026-47117 - OpenMed remote code execution via PII model loading

- Severity: Critical, CVSS 9.3.
- Affected software: OpenMed before 1.5.2.
- Exploit availability: VulnCheck advisory explains the unauthenticated attack path using user-supplied Hugging Face model names and `trust_remote_code=True`.
- Active exploitation: No active exploitation confirmed in reviewed sources.
- Recommended action: Upgrade to OpenMed 1.5.2 or later, disable arbitrary remote model loading, restrict access to model-loading endpoints, and review logs for unexpected Hugging Face repository names containing `privacy-filter`.
- Confidence: High.
- Sources: https://www.vulncheck.com/advisories/openmed-remote-code-execution-via-pii-model-loading, https://nvd.nist.gov/vuln/detail/CVE-2026-47117

### 9. CVE-2022-0492 and CVE-2025-48595 - newest CISA KEV additions

- Severity: High operational urgency due to KEV listing and short due date.
- Affected software: Linux Kernel cgroups v1 `release_agent` path for CVE-2022-0492; Android Framework for CVE-2025-48595.
- Exploit availability: Public technical detail exists for CVE-2022-0492; Android bulletin confirms patch availability for CVE-2025-48595.
- Active exploitation: Yes by KEV definition.
- Recommended action: For Linux/container environments, audit cgroups v1 exposure and container runtime hardening, patch kernels, and prevent untrusted containers from writing cgroup `release_agent`. For Android fleets, deploy the June 2026 Android security update and prioritize devices with work-profile or privileged-app exposure.
- Confidence: High.
- Sources: https://www.cisa.gov/known-exploited-vulnerabilities-catalog, https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=24f6008564183aa120d07c03d9289519c2fe02af, https://source.android.com/docs/security/bulletin/2026/2026-06-01

### 10. CVE-2026-9082 - Drupal Core PostgreSQL SQL injection

- Severity: Drupal rates highly critical; NVD scoring observed in prior runs as context-dependent.
- Affected software: Drupal Core PostgreSQL-backed deployments in affected 8.x through 11.x ranges.
- Exploit availability: ExploitDB EDB-ID 52608 and multiple public PoC/scanner indicators.
- Active exploitation: Drupal updated its advisory on 2026-05-22 to state exploit attempts were being detected in the wild.
- Recommended action: Upgrade to fixed Drupal Core releases immediately, prioritize PostgreSQL-backed and JSON:API-enabled sites, and review web logs for malformed JSON:API filter array keys and SQL error responses.
- Confidence: High.
- Sources: https://www.drupal.org/sa-core-2026-004, https://gitlab.com/exploit-database/exploitdb/-/raw/main/files_exploits.csv, https://nvd.nist.gov/vuln/detail/CVE-2026-9082

### 11. CVE-2026-10704 - SourceCodester Pizzafy E-Commerce System SQL injection

- Severity: Medium in current NVD data, CVSS 5.5; public exploit disclosure raises operational priority for exposed admin panels.
- Affected software: SourceCodester Pizzafy E-Commerce System 1.0 administrative login component `/admin/admin_class_novo.php`.
- Exploit availability: NVD states public exploit disclosure and references a GitHub write-up.
- Active exploitation: No active exploitation confirmed.
- Recommended action: Remove internet exposure for the admin panel, apply a vendor or community patch if available, replace raw SQL handling with parameterized queries, and monitor for SQL injection payloads in admin login requests.
- Confidence: Medium. NVD/VulDB data is current, but search indexes returned some adjacent Pizzafy CVEs when queried by ID.
- Sources: https://nvd.nist.gov/vuln/detail/CVE-2026-10704, https://github.com/nuiifornet/A033/blob/main/pizzafy-vulnerability.md

### 12. CVE-2026-10690 - DesktopCommanderMCP SSRF

- Severity: Low, CVSS 2.1, but relevant because MCP-related tools continue to appear in exploit and developer-tool attack chains.
- Affected software: wonderwhy-er DesktopCommanderMCP 0.2.37.
- Exploit availability: NVD states public disclosure and references a GitHub issue/commit.
- Active exploitation: No active exploitation confirmed.
- Recommended action: Upgrade DesktopCommanderMCP, review URL-fetch functionality in MCP tools, and block internal metadata/IP access from developer automation hosts.
- Confidence: Medium.
- Sources: https://nvd.nist.gov/vuln/detail/CVE-2026-10690, https://github.com/wonderwhy-er/DesktopCommanderMCP/issues/410

## Exploits Released

### Sploitus Top 10 (reconstructed from indexed pages)

Sploitus homepage did not expose an official "Exploits of the Week" block in static fetch results. The table below reconstructs a top-10 queue from indexed Sploitus exploit pages, current GitHub search indicators, direct ExploitDB CSV data, and high-risk exploit-feed correlation.

| Rank | CVE | Affected software | Exploit type | Exploit maturity | Public PoC | Weaponization potential |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | CVE-2026-23744 | MCPJam Inspector <= 1.4.2 | Unauthenticated RCE via `/api/mcp/connect` | GitHub advisory PoC, new GitHub repo, Sploitus/search indicators | Yes | Critical for exposed developer workstations and AI tooling |
| 2 | CVE-2026-41940 | cPanel/WHM and WP Squared | Authentication bypass to administrative/root access | KEV, GitHub indicators, public PoCs, ransomware reporting | Yes | Critical; ransomware and Mirai post-compromise observed |
| 3 | CVE-2026-31431 | Linux Kernel "Copy Fail" | Local privilege escalation/page-cache write | Multiple pushed GitHub PoC indicators and KEV carry-forward | Yes | High for servers/containers where primitives are reachable |
| 4 | CVE-2026-9082 | Drupal Core PostgreSQL backend | SQL injection via database abstraction/API paths | ExploitDB 52608 and multiple PoC/scanner indicators | Yes | High-to-critical depending on database permissions/config |
| 5 | CVE-2026-24061 | GNU Inetutils telnetd | Remote auth bypass to root shell | Metasploit/Rapid7/GitHub/Sploitus carry-forward | Yes | Critical for legacy/embedded/OT telnet exposure |
| 6 | CVE-2026-25643 | Frigate NVR <= 0.16.3 | Config injection RCE/container escape | Packet Storm/Sploitus/GitHub carry-forward | Yes | High where Frigate is internet-exposed or admin creds are compromised |
| 7 | CVE-2026-48778 | Notepad++ 8.9.6 | User-assisted arbitrary code execution | ExploitDB 52606/Packet Storm/Sploitus carry-forward | Yes | Medium; phishing or local file manipulation required |
| 8 | CVE-2026-21858 | n8n automation platform | Content-type confusion to file read/session forgery/RCE | Sploitus indexed exploit reconstruction | Yes | Critical if internet-exposed form webhook nodes are vulnerable |
| 9 | CVE-2026-10704 | SourceCodester Pizzafy E-Commerce System | Remote SQL injection in admin login | NVD/VulDB public exploit reference | Yes | Medium; exposed admin panels can be taken over |
| 10 | CVE-2026-10694 | SourceCodester Online Food Ordering System | Remote file inclusion via `page` parameter | NVD/VulDB public exploit reference | Yes | Medium; commodity web-app exploitation likely if exposed |

### ExploitDB additions

- Latest direct ExploitDB CSV entries published on 2026-06-01:
  - EDB-ID 52608: Drupal Core 10.5.5 error-based SQL injection, CVE-2026-9082.
  - EDB-ID 52607: WordPress OrderConvo 14 path traversal, CVE-2025-10162.
- Latest 2026-05-30 ExploitDB rows include Notepad++ 8.9.6 arbitrary code execution CVE-2026-48778 and multiple YAMCS yamcs-core issues.
- No direct ExploitDB CSV row newer than 2026-06-01 was present at collection time.

### New GitHub PoC and exploit indicators

- `jf-gondim/mcp-pwn`: created 2026-06-03T02:31:57Z, pushed 2026-06-03T02:47:15Z. Claims PoC exploit for CVE-2026-23744 MCPJam Inspector unauthenticated RCE. Treat as unvalidated but high-priority because the primary advisory contains PoC details and telemetry sources report exploitation attempts.
- `hnytgl/cve-2026-41089-detector`: created 2026-06-03T00:59:29Z, pushed 2026-06-03T02:21:31Z. Claims safe detector for Windows Netlogon CVE-2026-41089. Treat as unvalidated.
- `hnytgl/CVE-2026-41089`: created 2026-06-03T02:29:06Z, pushed 2026-06-03T02:59:47Z. Claims Windows Netlogon CLDAP RCE exploit. Treat as unvalidated; prior source review showed mixed confidence for active-exploitation claims.
- `Defacto-ridgepole254/CVE-2026-41940-Exploit-PoC`: pushed 2026-06-03T03:34:03Z. cPanel/WHM auth bypass PoC indicator; corroborated by KEV/ransomware reporting but repository itself is unvalidated.
- `Dullpurple-sloop726/CVE-2026-31431-Linux-Copy-Fail`: pushed 2026-06-03T03:33:43Z. Linux Copy Fail LPE exploit indicator.
- `Liverwortenuresis371/copyfail-rs`: pushed 2026-06-03T03:32:50Z. Copy Fail/CVE-2026-31431 Rust exploit/detection indicator.
- `DyniePro/CVE-2026-25643`: pushed 2026-06-03T02:57:50Z. Claims Frigate NVR RCE exploit; treat as unvalidated but correlated with primary advisory and exploit-feed signals from prior runs.
- `Recorded-texteditor120/CVE-2026-31802`: pushed 2026-06-03T03:11:46Z. Claims npm tar path traversal arbitrary file overwrite PoC; treat as unvalidated.
- `tracyliving606/RegPwn`: pushed 2026-06-03T03:10:37Z. Claims Windows LPE for CVE-2026-24291; treat as unvalidated.

## Malware Intelligence

- VX-Underground: Latest GitHub push in `vxunderground/MalwareSourceCode` remains 2026-05-30, adding `Python/Stealer.Python.GMBA.Manipulator.7z`. No newer pushed malware source release was observed in the checked VX repositories.
- MalwareBazaar: 201 submissions in the past 24 hours; Mirai is the most-seen family.
- cPanel/WHM malware and ransomware: CVE-2026-41940 exploitation is associated with "Sorry" ransomware and Mirai/nuclear.x86 botnet deployment. Because KEV records ransomware use for this CVE, patched status alone is insufficient; post-compromise review is required.
- SmartApeSG/ClickFix: SANS ISC reports an unidentified RAT that installs NetSupport RAT, with initial RAT traffic to `89.110.110[.]119:443` and NetSupport RAT C2 at `185.163.47[.]217:443`.
- SVG phishing: SANS ISC reports a new wave of SVG attachments using JavaScript/ECMAScript MIME handling and obfuscated redirect logic to send victims to phishing pages.
- AI-assisted malware lab: Help Net Security summarizes Sophos X-Ops findings that an active ransomware/data-theft actor used AI agents, Cursor, Claude Opus, MCP-connected Git workflows, Cobalt Strike/Sliver infrastructure, and a lab with Sophos/CrowdStrike/Microsoft Defender EDR testing to build and iterate payload evasion techniques. Sophos did not identify the ransomware group publicly.

## Security Releases and Vendor Advisories

- Microsoft: Defender exploited flaws CVE-2026-41091 and CVE-2026-45498 are due in CISA KEV on 2026-06-03. Verify Malware Protection Engine and Antimalware Platform update levels across all Windows endpoints and servers.
- Cisco: Catalyst SD-WAN CVE-2026-20182 has fixed releases and no full workaround. Follow Cisco TAC evidence-preservation guidance before remediation if compromise is suspected.
- Progress: Sitefinity security advisory released 2026-06-02 addresses CVE-2026-7312, CVE-2026-7198, CVE-2026-7195, CVE-2026-7201, and CVE-2026-7313 across Sitefinity CMS/Insight.
- authentik: GitHub advisory GHSA-xp7f-xjjx-gwm8 patches CVE-2026-49448 in 2025.12.6, 2026.2.4, and 2026.5.1.
- LibreChat: GitHub advisory GHSA-4pcc-j6m6-wcwx patches CVE-2026-32625 in v0.8.4-rc1.
- Spacelabs Healthcare: Sentinel advisory recommends updating to 11.6.2 and blocking port 8989 for CVE-2026-0611.
- OpenMed: VulnCheck advisory states OpenMed 1.5.2 fixes unauthenticated RCE via PII model loading.
- Drupal: Apply fixed Drupal Core releases for SA-CORE-2026-004/CVE-2026-9082, especially PostgreSQL-backed deployments.
- GitHub: GitHub Advisory API latest entries include critical PraisonAI Platform and Vitest advisories from June 1; no API entry newer than the current report window was observed.
- ExploitDB: No direct CSV entry newer than 2026-06-01 was present at collection time.

## Recommended Actions

1. Patch and investigate Cisco Catalyst SD-WAN CVE-2026-20182 immediately. Preserve admin-tech/log evidence before upgrade when compromise is plausible, then validate control-plane peers and NETCONF activity.
2. Treat unpatched cPanel/WHM and WP Squared systems as potentially compromised. Patch, isolate, hunt for WHM session abuse, rotate credentials, and investigate ransomware/Mirai indicators.
3. Remove external exposure for MCP developer tooling. Patch MCPJam Inspector, bind to localhost, and hunt for unexpected `/api/mcp/connect` command execution.
4. Apply Progress Sitefinity updates for all supported branches and prioritize internet-facing OData/ServiceStack services.
5. Patch identity and AI/developer platforms with high-impact advisories: authentik, LibreChat, OpenMed, and Spacelabs Sentinel.
6. Complete CISA KEV due-date remediation for Microsoft Defender, Linux cgroups v1 CVE-2022-0492, Android Framework CVE-2025-48595, and any overdue cPanel/Drupal/LiteSpeed items.
7. Review newly pushed GitHub exploit repositories only in isolated analysis environments. Do not execute public PoCs on production systems, and treat GitHub-only claims as unvalidated.
8. Monitor for malware campaign indicators: Mirai/nuclear.x86 on cPanel hosts, `.sorry` encrypted files, NetSupport RAT C2 from SANS ISC, SVG phishing attachments with ECMAScript MIME types, and suspicious Cobalt Strike/Sliver traffic linked to EDR-evasion tooling.

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
    "cve": "CVE-2026-41940",
    "cvss": "9.8",
    "vendor": "WebPros",
    "product": "cPanel & WHM and WP Squared",
    "affected_versions": "cPanel & WHM vulnerable branches and WP Squared versions prior to vendor fixed releases",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://github.com/Defacto-ridgepole254/CVE-2026-41940-Exploit-PoC", "https://sploitus.com/search?query=CVE-2026-41940"],
    "patch_available": true,
    "sources": ["https://www.cisa.gov/known-exploited-vulnerabilities-catalog", "https://support.cpanel.net/hc/en-us/articles/40073787579671-cPanel-WHM-Security-Update-04-28-2026", "https://www.bitsight.com/blog/critical-vulnerability-alert-cve-2026-41940-cPanel-WHM-WPSquared"],
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
    "poc_links": ["https://github.com/MCPJam/inspector/security/advisories/GHSA-232v-j27c-5pp6", "https://github.com/jf-gondim/mcp-pwn", "https://sploitus.com/search?query=CVE-2026-23744"],
    "patch_available": true,
    "sources": ["https://github.com/MCPJam/inspector/security/advisories/GHSA-232v-j27c-5pp6", "https://nvd.nist.gov/vuln/detail/CVE-2026-23744", "https://www.crowdsec.net/vulntracking-report/cve-2026-23744"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-7312",
    "cvss": "10.0",
    "vendor": "Progress",
    "product": "Sitefinity CMS and Sitefinity Insight",
    "affected_versions": "Sitefinity 14.0.7700-14.4.8151, 15.0.8200-15.0.8233, 15.1.8300-15.1.8334, 15.2.8400-15.2.8440, 15.3.8500-15.3.8530, 15.4.8600-15.4.8629",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://community.progress.com/s/article/Sitefinity-Security-Advisory-for-Addressing-Security-Vulnerabilities-CVE-2026-7312-CVE-2026-7198-CVE-2026-7195-CVE-2026-7201-CVE-2026-7313-May-2026", "https://nvd.nist.gov/vuln/detail/CVE-2026-7312"],
    "confidence": "High"
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
    "sources": ["https://community.progress.com/s/article/Sitefinity-Security-Advisory-for-Addressing-Security-Vulnerabilities-CVE-2026-7312-CVE-2026-7198-CVE-2026-7195-CVE-2026-7201-CVE-2026-7313-May-2026", "https://nvd.nist.gov/vuln/detail/CVE-2026-7198"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-49448",
    "cvss": "9.8",
    "vendor": "goauthentik",
    "product": "authentik",
    "affected_versions": "<=2025.12.5, <=2026.2.3, <=2026.5.0",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://github.com/goauthentik/authentik/security/advisories/GHSA-xp7f-xjjx-gwm8"],
    "patch_available": true,
    "sources": ["https://github.com/goauthentik/authentik/security/advisories/GHSA-xp7f-xjjx-gwm8", "https://nvd.nist.gov/vuln/detail/CVE-2026-49448"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-32625",
    "cvss": "9.6",
    "vendor": "LibreChat",
    "product": "LibreChat",
    "affected_versions": "<= 0.8.3",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://github.com/danny-avila/LibreChat/security/advisories/GHSA-4pcc-j6m6-wcwx"],
    "patch_available": true,
    "sources": ["https://github.com/danny-avila/LibreChat/security/advisories/GHSA-4pcc-j6m6-wcwx", "https://nvd.nist.gov/vuln/detail/CVE-2026-32625"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-0611",
    "cvss": "9.2",
    "vendor": "Spacelabs Healthcare",
    "product": "Sentinel",
    "affected_versions": "10.5.x and 11.x.x before fixed 11.6.x releases",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://www.vulncheck.com/advisories/spacelabs-healthcare-sentinel-x-unauthenticated-rce-via-net-remoting"],
    "patch_available": true,
    "sources": ["https://spacelabshealthcare.com/wp-content/uploads/2026/06/079-0273-00-RevA-Security-Advisory-Sentinel-.NET-Remoting-Vulnerability.pdf", "https://nvd.nist.gov/vuln/detail/CVE-2026-0611"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-47117",
    "cvss": "9.3",
    "vendor": "OpenMed",
    "product": "OpenMed",
    "affected_versions": "< 1.5.2",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://www.vulncheck.com/advisories/openmed-remote-code-execution-via-pii-model-loading"],
    "patch_available": true,
    "sources": ["https://www.vulncheck.com/advisories/openmed-remote-code-execution-via-pii-model-loading", "https://nvd.nist.gov/vuln/detail/CVE-2026-47117"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2022-0492",
    "cvss": "7.8",
    "vendor": "Linux",
    "product": "Kernel",
    "affected_versions": "Linux kernel cgroups v1 release_agent configurations before upstream fix",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://nvd.nist.gov/vuln/detail/CVE-2022-0492"],
    "patch_available": true,
    "sources": ["https://www.cisa.gov/known-exploited-vulnerabilities-catalog", "https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=24f6008564183aa120d07c03d9289519c2fe02af"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2025-48595",
    "cvss": "Unknown",
    "vendor": "Google",
    "product": "Android Framework",
    "affected_versions": "Android versions covered by June 2026 Android security bulletin",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://www.cisa.gov/known-exploited-vulnerabilities-catalog", "https://source.android.com/docs/security/bulletin/2026/2026-06-01"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-9082",
    "cvss": "Context-dependent",
    "vendor": "Drupal",
    "product": "Drupal Core",
    "affected_versions": "Affected Drupal 8.x through 11.x ranges using PostgreSQL per SA-CORE-2026-004",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": false,
    "poc_links": ["https://gitlab.com/exploit-database/exploitdb/-/raw/main/exploits/php/webapps/52608.py", "https://sploitus.com/search?query=CVE-2026-9082"],
    "patch_available": true,
    "sources": ["https://www.drupal.org/sa-core-2026-004", "https://gitlab.com/exploit-database/exploitdb/-/raw/main/files_exploits.csv"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-10704",
    "cvss": "5.5",
    "vendor": "SourceCodester",
    "product": "Pizzafy E-Commerce System",
    "affected_versions": "1.0",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://github.com/nuiifornet/A033/blob/main/pizzafy-vulnerability.md"],
    "patch_available": false,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2026-10704", "https://vuldb.com/cve/CVE-2026-10704"],
    "confidence": "Medium"
  },
  {
    "cve": "CVE-2026-10694",
    "cvss": "5.5",
    "vendor": "SourceCodester",
    "product": "Online Food Ordering System",
    "affected_versions": "2.0",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://github.com/Mikkoseven/cve/issues/4"],
    "patch_available": false,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2026-10694", "https://vuldb.com/cve/CVE-2026-10694"],
    "confidence": "Medium"
  },
  {
    "cve": "CVE-2026-10690",
    "cvss": "2.1",
    "vendor": "wonderwhy-er",
    "product": "DesktopCommanderMCP",
    "affected_versions": "0.2.37",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://github.com/wonderwhy-er/DesktopCommanderMCP/issues/410"],
    "patch_available": true,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2026-10690", "https://github.com/wonderwhy-er/DesktopCommanderMCP/commit/53699bebba9950047bca16ac4dc8f0568f596aaa"],
    "confidence": "Medium"
  },
  {
    "cve": "CVE-2026-41091",
    "cvss": "Unknown",
    "vendor": "Microsoft",
    "product": "Defender",
    "affected_versions": "Microsoft Malware Protection Engine versions before fixed release",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://www.cisa.gov/known-exploited-vulnerabilities-catalog", "https://msrc.microsoft.com/update-guide/en-US/vulnerability/CVE-2026-41091"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-45498",
    "cvss": "Unknown",
    "vendor": "Microsoft",
    "product": "Defender",
    "affected_versions": "Microsoft Defender Antimalware Platform versions before fixed release",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://www.cisa.gov/known-exploited-vulnerabilities-catalog", "https://msrc.microsoft.com/update-guide/en-US/vulnerability/CVE-2026-45498"],
    "confidence": "High"
  }
]
```
