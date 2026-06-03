# Security Intelligence Report - 2026-06-03 06:00 UTC

Report window: 2026-06-03 05:00-06:35 UTC.  
Analyst stance: Prioritize confirmed active exploitation, KEV entries, public exploit material, enterprise/cloud exposure, and patch availability. Public GitHub PoC repositories are treated as indicators until independently validated.

## Executive Summary

- Total CVEs newly published in the current NVD hourly window: 0.
- NVD day-to-date total for 2026-06-03 00:00-06:35 UTC: 13 CVEs: 1 high, 4 medium, 6 low, 2 unknown.
- Rolling 24h NVD total: 214 CVEs: 13 critical, 77 high, 84 medium, 20 low, 20 unknown.
- Critical findings requiring continued action: Cisco FMC CVE-2026-20131, Cisco Catalyst SD-WAN CVE-2026-20182, Citrix NetScaler CVE-2026-3055, MCPJam Inspector CVE-2026-23744, HP Poly CVE-2026-0826, Rocket.Chat CVE-2026-29198, Progress Sitefinity CVE-2026-7312/CVE-2026-7198, authentik CVE-2026-49448/CVE-2026-42849, OpenClaude CVE-2026-42074, and OpenMed CVE-2026-47117.
- Active exploitation findings: CISA KEV catalog version 2026.06.02 remains current with latest additions CVE-2022-0492 and CVE-2025-48595. Carry-forward active exploitation remains confirmed for Cisco FMC CVE-2026-20131, Cisco SD-WAN CVE-2026-20182, Cisco FMC/SD-WAN-related edge device activity, Citrix NetScaler CVE-2026-3055, Drupal CVE-2026-9082, cPanel CVE-2026-41940, and MCPJam Inspector CVE-2026-23744.
- New exploit indicators since the prior report: GitHub repository `9Bakabaka/CVE-2026-49943-PoC` was created at 2026-06-03 05:39 UTC for BIRD CVE-2026-49943; README content is minimal, so confidence in exploit functionality is low. The current-day created MCPJam PoC `jf-gondim/mcp-pwn` remains notable. No new ExploitDB rows dated 2026-06-03 were found.
- Malware and supply-chain intelligence: MalwareBazaar reports 198 submissions in the past 24h, with Mirai the most seen family. VX-Underground GitHub repositories showed no new malware-source push after 2026-05-30. Sophos reporting describes an AI-assisted ransomware/malware testing lab focused on EDR evasion and AD discovery. The Red Hat `@redhat-cloud-services` npm Miasma/Mini Shai-Hulud supply-chain compromise remains high-priority for secret rotation.

## Source Coverage and Confidence

Primary and high-confidence sources checked:

- NVD 2.0 API for current hour, day-to-date, rolling 24h, and selected CVEs: `https://services.nvd.nist.gov/rest/json/cves/2.0`
- CISA KEV JSON feed: `https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json`
- Sploitus homepage: `https://sploitus.com/`
- GitHub Security Advisories API and GitHub repository search
- ExploitDB CSV from Offensive Security GitLab mirror
- VX-Underground GitHub user repositories
- MalwareBazaar browse page: `https://bazaar.abuse.ch/browse/`
- Vendor/research sources: Cisco PSIRT, CISA, Rapid7, GitHub Security Advisories, GNU FreeIPMI announcement, BIRD upstream NEWS, Amazon Threat Intelligence, CrowdSec, CERT Polska, Red Hat, Wiz, Snyk, Aikido, Sophos/Help Net Security.

Sploitus limitation: The Sploitus homepage was reachable, but the static page did not expose an "Exploits of the Week" top-10 block. The Sploitus section below is therefore a reconstructed exploit watchlist from indexed Sploitus result pages plus exploit-feed and GitHub correlation. Confidence is high for the existence of indexed Sploitus pages, medium for ordering, and item-level confidence varies by source validation.

## Top Vulnerabilities

### 1. CVE-2026-20131 - Cisco Secure Firewall Management Center RCE

- Severity: Critical, CVSS 10.0.
- Affected software: Cisco Secure Firewall Management Center web management interface.
- Exploit availability: Public technical detail and observed exploitation; exploit attempts seen by Amazon MadPot.
- Active exploitation: Yes. Amazon Threat Intelligence reports Interlock ransomware exploitation beginning 36 days before public disclosure; CISA KEV-listed.
- Recommended action: Patch all FMC deployments immediately, restrict management interface exposure, review Cisco advisory IOCs, hunt for Java deserialization artifacts, webshells, unusual PUT callbacks, and Interlock tooling.
- Confidence: High.

### 2. CVE-2026-20182 - Cisco Catalyst SD-WAN Controller/Manager Authentication Bypass

- Severity: Critical, CVSS 10.0.
- Affected software: Cisco Catalyst SD-WAN Controller and Manager.
- Exploit availability: Public research and Metasploit reporting exist; Cisco includes compromise-check guidance.
- Active exploitation: Yes. Cisco PSIRT confirmed limited exploitation; CISA KEV-listed and tied to Emergency Directive 26-03 guidance.
- Recommended action: Upgrade to a fixed Cisco release; there are no workarounds. Review control-connection logs, unauthorized peering, NETCONF activity, SSH key changes, and SD-WAN fabric configuration changes.
- Confidence: High.

### 3. CVE-2026-3055 - Citrix NetScaler ADC/Gateway SAML IDP Memory Overread

- Severity: Critical, CVSSv4 9.3.
- Affected software: NetScaler ADC and NetScaler Gateway configured as SAML Identity Provider.
- Exploit availability: Public analysis and active exploitation reporting.
- Active exploitation: Yes. KEV-listed; security reporting indicates large-scale exploitation.
- Recommended action: Apply Citrix fixes, assess SAML IDP exposure, inspect appliance logs for anomalous SAML traffic and post-exploitation activity.
- Confidence: High.

### 4. CVE-2026-23744 - MCPJam Inspector Unauthenticated RCE

- Severity: Critical, CVSS 9.8.
- Affected software: MCPJam Inspector 1.4.2 and earlier.
- Exploit availability: Public GitHub advisory includes a direct HTTP exploit pattern; current-day GitHub PoC `jf-gondim/mcp-pwn`; Sploitus/PacketStorm indicators.
- Active exploitation: Yes, per CrowdSec surge of exploitation attempts against exposed `/api/mcp/connect`.
- Recommended action: Upgrade to 1.4.3 or later, bind development tools to localhost, firewall port 6274, and hunt for spawned processes from MCPJam Inspector.
- Confidence: High for vulnerability and active attempts; medium for newly created PoC repository functionality.

### 5. CVE-2026-0826 - HP Poly VVX/Trio Unauthenticated RCE

- Severity: Critical, CVSSv4 9.2.
- Affected software: HP Poly VVX 150/250/350/450 and Trio 8300/8500/8800 when ICE is enabled.
- Exploit availability: Rapid7 developed a Metasploit exploit module and demonstrated unauthenticated root RCE.
- Active exploitation: Not confirmed in the sources checked.
- Recommended action: Disable ICE where not required and upgrade VVX to UCS 6.4.8, Trio 8300 to UCS 8.1.7, and Trio 8500/8800 to UCS 7.2.8.
- Confidence: High.

### 6. CVE-2026-29198 - Rocket.Chat OAuth2 NoSQL Injection / Account Takeover

- Severity: Critical, CVSS 9.8.
- Affected software: Rocket.Chat before 8.3.0, 8.2.1, 8.1.2, 8.0.3, 7.13.5, 7.12.6, 7.11.6, and 7.10.9.
- Exploit availability: New GitHub PoC indicator `hieuminhnv/CVE-2026-29198-POC`; GitHub advisory and NVD detail the pre-auth OAuth token attack.
- Active exploitation: Not confirmed.
- Recommended action: Patch Rocket.Chat branches immediately; review OAuth token issuance, admin access, Apps-Engine installation, and suspicious API tokens.
- Confidence: High for vulnerability; medium for PoC functionality.

### 7. CVE-2026-50031 - FreeIPMI `ipmi-oem` Buffer Overflows

- Severity: High, CVSS 7.5.
- Affected software: FreeIPMI before 1.6.18, specifically `ipmi-oem` commands handling malicious IPMI response messages.
- Exploit availability: No public exploit found in sources checked; NVD and GNU/Savannah references confirm vulnerability and release.
- Active exploitation: Not observed.
- Recommended action: Upgrade to FreeIPMI 1.6.18; restrict IPMI/BMC management access to trusted networks; treat connections to untrusted or compromised BMCs as hostile.
- Confidence: High.

### 8. CVE-2026-49943 - BIRD Internet Routing Daemon BGP AS_PATH Mask DoS

- Severity: Medium, CVSS 6.3.
- Affected software: CZ.NIC BIRD through 2.19.0, BGP AS_PATH mask matching in `nest/a-path.c`.
- Exploit availability: GitHub repo `9Bakabaka/CVE-2026-49943-PoC` created 2026-06-03 05:39 UTC, but README only states "PoC of CVE-2026-49943"; functionality not validated.
- Active exploitation: Not observed.
- Recommended action: Review BIRD filter usage for `bgp_path ~ [= ... =]`, assess RFC 8654 extended-message exposure to established peers, and track upstream fixes/mitigations.
- Confidence: Medium for vulnerability, low for PoC maturity.

### 9. CVE-2026-7312 / CVE-2026-7198 - Progress Sitefinity Critical Web Service Issues

- Severity: Critical, CVSS 10.0 and 9.8.
- Affected software: Progress Sitefinity versions in 14.x through 15.4 ranges per vendor advisory; exploitation requirements vary by non-default configuration and Insight integration.
- Exploit availability: No new exploit validated in this run.
- Active exploitation: Not confirmed.
- Recommended action: Apply Progress Sitefinity updates, verify Sitefinity Insight integration status, and limit exposed web services.
- Confidence: High.

### 10. CVE-2026-42096 / CVE-2026-42097 - Sparx Pro Cloud Server SQL/Auth Bypass

- Severity: Critical/high; CVE-2026-42097 CVSSv4 9.2 in PacketStorm/Sploitus result.
- Affected software: Sparx Pro Cloud Server 6.1 build 167 and earlier; Enterprise Architect 17.1 and earlier in related disclosures.
- Exploit availability: Packet Storm entry indexed by Sploitus; Full Disclosure and CERT Polska include technical detail.
- Active exploitation: CCB Belgium warns active exploitation.
- Recommended action: Patch or isolate Sparx PCS, disable internet exposure, restrict database access, and review logs for unauthenticated `SparxCloudLink.sseap` requests without expected model query parameters.
- Confidence: High.

## CVEs Published Day-to-Date

NVD 2026-06-03 00:00-06:35 UTC returned 13 CVEs:

| CVE | Severity | Summary | Exploit signal | Recommended action |
| --- | --- | --- | --- | --- |
| CVE-2026-50031 | High 7.5 | FreeIPMI `ipmi-oem` response-message buffer overflows before 1.6.18 | No public exploit found | Upgrade to 1.6.18 |
| CVE-2026-10694 | Medium 5.5 | SourceCodester Online Food Ordering System file inclusion | NVD/VulDB says exploit public | Remove exposure or patch/replace app |
| CVE-2026-10704 | Medium 5.5 | SourceCodester Pizzafy admin SQL injection | NVD/VulDB says exploit public | Patch/replace and review DB access |
| CVE-2026-7421 | Medium 4.4 | WordPress Passeum Ticketing stored XSS requiring admin-level access | No active exploitation found | Update/remove plugin |
| CVE-2026-9732 | Medium 4.3 | WordPress EmergencyWP CSRF settings modification | No active exploitation found | Update/remove plugin |
| CVE-2026-10705 | Low 2.3 | dask HLL resource consumption | Pull request pending | Track patch |
| CVE-2026-10690 | Low 2.1 | DesktopCommanderMCP SSRF in `readFileFromUrl` | Public issue/patch | Apply patch commit/release |
| CVE-2026-10691 | Low 2.1 | DesktopCommanderMCP ReDoS in search handling | Public issue/patch | Upgrade to 0.2.39 |
| CVE-2026-10692 | Low 2.1 | code-index-mcp ReDoS in regex handling | Public issue/patch | Upgrade to 2.14.1 |
| CVE-2026-10693 | Low 2.1 | SourceCodester Online Boat Reservation improper authorization | Public disclosure | Patch/replace |
| CVE-2026-10703 | Low 2.1 | EIPStackGroup OpENer UAF in SendRRData handling | Public issue with `poc.zip` attachment | Restrict exposure; track vendor response |
| CVE-2026-9334 | Unknown | Cpanel::JSON::XS type confusion before 4.41 | No active exploitation found | Upgrade to 4.41 |
| CVE-2026-9516 | Unknown | Cpanel::JSON::XS invalid pointer/DoS before 4.41 | No active exploitation found | Upgrade to 4.41 |

## Exploits Released

### Sploitus reconstructed Top 10

| Rank | CVE(s) | Affected software | Exploit type | Maturity | Public PoC | Weaponization potential |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | CVE-2026-31431 | Linux kernel AF_ALG/splice "Copy Fail" | Local privilege escalation/page-cache arbitrary write | Mature, multiple PoCs and analysis | Yes | High; root escalation and container escape paths |
| 2 | CVE-2026-42096/CVE-2026-42097 | Sparx Pro Cloud Server | SQL execution plus auth bypass | PacketStorm/Sploitus indexed exploit detail | Yes | High; unauthenticated database read/write in exposed PCS |
| 3 | CVE-2026-23744 | MCPJam Inspector | Unauthenticated RCE via `/api/mcp/connect` | Validated advisory pattern; GitHub PoC | Yes | High; internet-exposed dev tools and active scans |
| 4 | CVE-2026-20182 | Cisco Catalyst SD-WAN | Auth bypass/control-plane compromise | KEV; Cisco confirmed exploitation | Public exploit reporting | High; enterprise network control plane |
| 5 | CVE-2026-3055 | Citrix NetScaler | SAML IDP memory overread/RCE risk | KEV; public research | Public analysis | High; internet-edge appliance targeting |
| 6 | CVE-2026-9082 | Drupal Core | SQL injection | ExploitDB EDB-ID 52608 | Yes | High; web RCE/privilege escalation potential |
| 7 | CVE-2026-41940 | cPanel & WHM/WP2 | Auth bypass | KEV; ransomware use known | Public tooling indicators | High; hosting control panel compromise |
| 8 | CVE-2026-49943 | BIRD | BGP AS_PATH mask stack overflow DoS | New GitHub-only minimal PoC indicator | Unvalidated | Medium; requires established BGP peer and specific filters |
| 9 | CVE-2026-29198 | Rocket.Chat | Pre-auth OAuth2 NoSQL injection/ATO | GitHub advisory plus new PoC repo | Unvalidated PoC indicator | High; bearer token theft/admin takeover |
| 10 | CVE-2026-0826 | HP Poly VVX/Trio | SIP/SDP stack overflow RCE | Rapid7 validated Metasploit module | Yes | High when ICE enabled and SIP reachable |

### ExploitDB additions

Direct ExploitDB CSV sorting by `date_published` found no entries dated 2026-06-03. Latest notable rows remain:

- EDB-ID 52608, 2026-06-01: Drupal Core 10.5.5 error-based SQL injection, CVE-2026-9082.
- EDB-ID 52607, 2026-06-01: WordPress OrderConvo 14 path traversal, CVE-2025-10162.
- 2026-05-30 rows include YAMCS LDAP injection/user enumeration/no-rate-limit, Notepad++ arbitrary code execution, and other lower-confidence items.

### New GitHub PoC indicators

- `9Bakabaka/CVE-2026-49943-PoC`: created 2026-06-03 05:39 UTC; minimal README only; low confidence in functionality.
- `jf-gondim/mcp-pwn`: created 2026-06-03 02:31 UTC; claims MCPJam CVE-2026-23744 unauthenticated RCE; medium confidence due to matching GHSA exploit pattern.
- `hieuminhnv/CVE-2026-29198-POC`: created 2026-06-03 03:43 UTC; Rocket.Chat OAuth2 NoSQL injection PoC; medium confidence due to matching GitHub advisory/NVD details.
- `hnytgl/CVE-2026-41089`: current-day Netlogon RCE exploit indicator; functionality unvalidated.
- `06-ux/CVE-2026-9256-POC`: current-day NGINX heap buffer overflow PoC indicator; functionality unvalidated.

## Malware Intelligence

### VX-Underground

- VX-Underground web root is not reliably accessible from automation, but GitHub API monitoring works.
- Latest pushed VX repository remains `vxunderground/MalwareSourceCode`, pushed 2026-05-30, with prior observed addition `Python/Stealer.Python.GMBA.Manipulator.7z`.
- No new VX malware source push was observed in this hour.
- Confidence: Medium, because GitHub repository metadata is available but website content access is limited.

### MalwareBazaar / Abuse.ch

- MalwareBazaar browse page reports 198 submissions in the past 24 hours.
- Most seen malware family: Mirai.
- Recommended action: Continue edge/IoT telemetry review for Mirai-like scanning, default credential attempts, and botnet propagation.
- Confidence: High for dashboard counts.

### Ransomware and malware campaigns

- Sophos/Help Net Security reporting describes an AI-assisted malware testing framework linked to ransomware/data-theft operations. Capabilities include Cobalt Strike profiles, Telegram C2, shellcode injection tooling, Sliver infrastructure, Active Directory discovery, and iterative EDR evasion testing against Sophos, CrowdStrike, and Microsoft Defender. Sophos did not name the ransomware group due to active investigations.
- Amazon Threat Intelligence reporting on Cisco FMC CVE-2026-20131 ties exploitation to Interlock ransomware, with exploitation beginning before public disclosure.
- Miasma / Mini Shai-Hulud supply-chain compromise: Red Hat, Wiz, Snyk, Aikido, and BleepingComputer report compromise of `@redhat-cloud-services` npm packages, with a credential-stealing worm derived from Mini Shai-Hulud. Red Hat says affected versions were removed and customer action may not be required based on current findings; third-party researchers recommend treating affected build environments as compromised and rotating exposed secrets.

## Security Releases and Advisories

- GNU FreeIPMI: FreeIPMI 1.6.18 released 2026-06-02, fixing exploitable `ipmi-oem` buffer overflows in Dell active-directory and Fujitsu SEL long-text commands.
- HP Poly: Rapid7/HP advisory for CVE-2026-0826; fixed firmware versions are available for VVX and Trio series.
- Cisco: CVE-2026-20182 SD-WAN fixed releases are available; Cisco states no workaround. Cisco FMC CVE-2026-20131 remains KEV/ransomware-linked and should be patched/hunted.
- CISA KEV: Catalog version 2026.06.02 remains current. Latest additions are CVE-2022-0492 Linux kernel cgroups `release_agent` privilege escalation/container escape and CVE-2025-48595 Android Framework integer overflow/local privilege escalation, both due 2026-06-05.
- Google/Android: Android Framework CVE-2025-48595 is KEV-listed and referenced by the Android June 2026 bulletin.
- Progress Sitefinity: Vendor advisory addresses CVE-2026-7312, CVE-2026-7198, CVE-2026-7195, CVE-2026-7201, and CVE-2026-7313.
- GitHub Security Advisories: Latest API items in this run were dated 2026-06-01, including PraisonAI/praisonai-platform issue cluster, Vitest critical issues, DOMPurify XSS, and Nezha issues; no newer GHSA item appeared in the API response.
- ExploitDB: No 2026-06-03 additions found by direct CSV sorting.

## Unified Vulnerability Records

```json
[
  {
    "cve": "CVE-2026-20131",
    "cvss": "10.0",
    "vendor": "Cisco",
    "product": "Secure Firewall Management Center",
    "affected_versions": "See Cisco advisory cisco-sa-fmc-rce-NKhnULJh",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://aws.amazon.com/blogs/security/amazon-threat-intelligence-teams-identify-interlock-ransomware-campaign-targeting-enterprise-firewalls/"],
    "patch_available": true,
    "sources": ["https://sec.cloudapps.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-fmc-rce-NKhnULJh", "https://www.cisa.gov/known-exploited-vulnerabilities-catalog?field_cve=CVE-2026-20131", "https://nvd.nist.gov/vuln/detail/CVE-2026-20131"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-20182",
    "cvss": "10.0",
    "vendor": "Cisco",
    "product": "Catalyst SD-WAN Controller and Manager",
    "affected_versions": "See Cisco advisory cisco-sa-sdwan-rpa2-v69WY2SW",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://www.cisco.com/c/en/us/support/docs/csa/cisco-sa-sdwan-rpa2-v69WY2SW.html", "https://www.cisa.gov/known-exploited-vulnerabilities-catalog?field_cve=CVE-2026-20182", "https://nvd.nist.gov/vuln/detail/CVE-2026-20182"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-3055",
    "cvss": "9.3",
    "vendor": "Citrix",
    "product": "NetScaler ADC and NetScaler Gateway",
    "affected_versions": "SAML IDP configurations; see Citrix CTX696300",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://labs.watchtowr.com/please-we-beg-just-one-weekend-free-of-appliances-citrix-netscaler-cve-2026-3055-memory-overread-part-2/"],
    "patch_available": true,
    "sources": ["https://support.citrix.com/support-home/kbsearch/article?articleNumber=CTX696300", "https://www.cisa.gov/known-exploited-vulnerabilities-catalog?field_cve=CVE-2026-3055", "https://nvd.nist.gov/vuln/detail/CVE-2026-3055"],
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
    "poc_links": ["https://github.com/MCPJam/inspector/security/advisories/GHSA-232v-j27c-5pp6", "https://github.com/jf-gondim/mcp-pwn"],
    "patch_available": true,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2026-23744", "https://www.crowdsec.net/vulntracking-report/cve-2026-23744"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-0826",
    "cvss": "9.2",
    "vendor": "HP Poly",
    "product": "VVX and Trio Voice products",
    "affected_versions": "VVX 150/250/350/450 and Trio 8300/8500/8800 when ICE is enabled; see HP advisory",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://www.rapid7.com/blog/post/ve-cve-2026-0826-critical-unauthenticated-stack-buffer-overflow-hp-poly-vvx-trio-voip-phones-fixed/"],
    "patch_available": true,
    "sources": ["https://support.hp.com/us-en/document/ish_15052661-15052687-16/hpsbpy04083", "https://nvd.nist.gov/vuln/detail/CVE-2026-0826"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-29198",
    "cvss": "9.8",
    "vendor": "Rocket.Chat",
    "product": "Rocket.Chat",
    "affected_versions": "<8.3.0, <8.2.1, <8.1.2, <8.0.3, <7.13.5, <7.12.6, <7.11.6, <7.10.9",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://github.com/RocketChat/Rocket.Chat/security/advisories/GHSA-8p25-fm45-pjrw", "https://github.com/hieuminhnv/CVE-2026-29198-POC"],
    "patch_available": true,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2026-29198", "https://github.com/RocketChat/Rocket.Chat/pull/39492"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-50031",
    "cvss": "7.5",
    "vendor": "GNU",
    "product": "FreeIPMI",
    "affected_versions": "< 1.6.18",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://lists.gnu.org/archive/html/info-gnu/2026-06/msg00000.html", "https://nvd.nist.gov/vuln/detail/CVE-2026-50031"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-49943",
    "cvss": "6.3",
    "vendor": "CZ.NIC",
    "product": "BIRD Internet Routing Daemon",
    "affected_versions": "through 2.19.0",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://github.com/9Bakabaka/CVE-2026-49943-PoC"],
    "patch_available": false,
    "sources": ["https://gitlab.nic.cz/labs/bird/-/blob/master/NEWS", "https://nvd.nist.gov/vuln/detail/CVE-2026-49943"],
    "confidence": "Medium"
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
    "sources": ["https://community.progress.com/s/article/Sitefinity-Security-Advisory-for-Addressing-Security-Vulnerabilities-CVE-2026-7312-CVE-2026-7198-CVE-2026-7195-CVE-2026-7201-CVE-2026-7313-May-2026", "https://nvd.nist.gov/vuln/detail/CVE-2026-7312"],
    "confidence": "High"
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
    "sources": ["https://community.progress.com/s/article/Sitefinity-Security-Advisory-for-Addressing-Security-Vulnerabilities-CVE-2026-7312-CVE-2026-7198-CVE-2026-7195-CVE-2026-7201-CVE-2026-7313-May-2026", "https://nvd.nist.gov/vuln/detail/CVE-2026-7198"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-49448",
    "cvss": "9.8",
    "vendor": "authentik",
    "product": "authentik",
    "affected_versions": "prior to 2025.12.6, 2026.2.4, and 2026.5.1",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://github.com/goauthentik/authentik/security/advisories/GHSA-xp7f-xjjx-gwm8", "https://nvd.nist.gov/vuln/detail/CVE-2026-49448"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-42074",
    "cvss": "9.3",
    "vendor": "OpenClaude",
    "product": "OpenClaude CLI",
    "affected_versions": "< 0.5.1",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://github.com/Gitlawb/openclaude/security/advisories/GHSA-m77w-p5jj-xmhg", "https://nvd.nist.gov/vuln/detail/CVE-2026-42074"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-47117",
    "cvss": "9.3",
    "vendor": "OpenMed",
    "product": "OpenMed",
    "affected_versions": "< 1.5.2",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://www.vulncheck.com/advisories/openmed-remote-code-execution-via-pii-model-loading", "https://github.com/maziyarpanahi/openmed/releases/tag/v1.5.2", "https://nvd.nist.gov/vuln/detail/CVE-2026-47117"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2025-48595",
    "cvss": "Unknown",
    "vendor": "Android",
    "product": "Framework",
    "affected_versions": "See Android June 2026 bulletin",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://source.android.com/docs/security/bulletin/2026/2026-06-01", "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2022-0492",
    "cvss": "Unknown",
    "vendor": "Linux",
    "product": "Kernel cgroups v1 release_agent",
    "affected_versions": "Systems with vulnerable cgroups v1 release_agent exposure; see vendor kernels",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=24f6008564183aa120d07c03d9289519c2fe02af", "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-31431",
    "cvss": "7.8",
    "vendor": "Linux",
    "product": "Kernel",
    "affected_versions": "Mainstream kernels with AF_ALG/splice issue before fixed stable releases",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://sploitus.com/exploit?id=336099EB-D841-5918-884E-BDD159524698"],
    "patch_available": true,
    "sources": ["https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json", "https://nvd.nist.gov/vuln/detail/CVE-2026-31431"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-41940",
    "cvss": "Unknown",
    "vendor": "WebPros",
    "product": "cPanel & WHM and WP2",
    "affected_versions": "See cPanel/WP2 advisories",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://support.cpanel.net/hc/en-us/articles/40073787579671-cPanel-WHM-Security-Update-04-28-2026", "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-9082",
    "cvss": "Unknown",
    "vendor": "Drupal",
    "product": "Core",
    "affected_versions": "See Drupal SA-CORE-2026-004",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://www.exploit-db.com/exploits/52608"],
    "patch_available": true,
    "sources": ["https://www.drupal.org/sa-core-2026-004", "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-42096",
    "cvss": "8.7",
    "vendor": "Sparx Systems",
    "product": "Pro Cloud Server",
    "affected_versions": "<= 6.1 build 167 tested vulnerable",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": false,
    "poc_links": ["https://sploitus.com/exploit?id=PACKETSTORM%3A221993", "https://seclists.org/fulldisclosure/2026/May/17"],
    "patch_available": false,
    "sources": ["https://cert.pl/en/posts/2026/05/CVE-2026-42096/", "https://ccb.belgium.be/advisories/warning-actively-exploited-critical-and-multiple-high-vulnerabilities-sparx-pro-cloud"],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-42097",
    "cvss": "9.2",
    "vendor": "Sparx Systems",
    "product": "Pro Cloud Server",
    "affected_versions": "<= 6.1 build 167 tested vulnerable",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": false,
    "poc_links": ["https://sploitus.com/exploit?id=PACKETSTORM%3A221993", "https://seclists.org/fulldisclosure/2026/May/17"],
    "patch_available": false,
    "sources": ["https://cert.pl/en/posts/2026/05/CVE-2026-42096/", "https://ccb.belgium.be/advisories/warning-actively-exploited-critical-and-multiple-high-vulnerabilities-sparx-pro-cloud"],
    "confidence": "High"
  }
]
```

## Recommended Actions

1. Patch and hunt Cisco FMC CVE-2026-20131 and Cisco SD-WAN CVE-2026-20182 immediately; both are confirmed exploited and affect enterprise network/security control planes.
2. Patch/remediate KEV edge and infrastructure items: Citrix NetScaler CVE-2026-3055, cPanel CVE-2026-41940, Drupal CVE-2026-9082, Linux CVE-2026-31431/CVE-2022-0492, Android CVE-2025-48595, Palo Alto PAN-OS CVE-2026-0257, Oracle WebLogic CVE-2024-21182.
3. Find and isolate exposed AI/developer tooling: MCPJam Inspector CVE-2026-23744, OpenClaude CVE-2026-42074, LibreChat CVE-2026-32625, DesktopCommanderMCP/code-index-mcp day-to-date CVEs. Bind to localhost, require authentication, and review process-spawn telemetry.
4. Patch HP Poly voice devices or disable ICE where not required; Rapid7 has validated root RCE with a Metasploit module.
5. Patch Rocket.Chat to fixed branch releases and audit OAuth token issuance and admin API use.
6. Upgrade FreeIPMI to 1.6.18 on systems that use IPMI tooling, especially where administrators connect to untrusted BMCs.
7. Review BIRD BGP filters and peer exposure for CVE-2026-49943; treat the new GitHub PoC as an early indicator, not proof of exploit maturity.
8. Respond to Miasma/Red Hat npm supply-chain exposure by identifying any `@redhat-cloud-services` package installs since 2026-06-01, rebuilding from clean environments, and rotating CI/CD, cloud, SSH, npm, PyPI, and GitHub tokens where exposure is plausible.
9. Monitor MalwareBazaar/Mirai telemetry for increased IoT botnet propagation and credential stuffing against edge devices.
10. Treat all GitHub-only PoCs as untrusted code. Do not execute without sandboxing; inspect for credential theft, obfuscation, install hooks, and network callbacks.

## Appendix: Key Source URLs

- NVD API: `https://services.nvd.nist.gov/rest/json/cves/2.0`
- CISA KEV JSON: `https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json`
- Sploitus homepage: `https://sploitus.com/`
- Sploitus Copy Fail result: `https://sploitus.com/exploit?id=336099EB-D841-5918-884E-BDD159524698`
- Sploitus/PacketStorm Sparx result: `https://sploitus.com/exploit?id=PACKETSTORM%3A221993`
- ExploitDB CSV: `https://gitlab.com/exploit-database/exploitdb/-/raw/main/files_exploits.csv`
- MalwareBazaar: `https://bazaar.abuse.ch/browse/`
- Rapid7 HP Poly: `https://www.rapid7.com/blog/post/ve-cve-2026-0826-critical-unauthenticated-stack-buffer-overflow-hp-poly-vvx-trio-voip-phones-fixed/`
- GitHub MCPJam advisory: `https://github.com/MCPJam/inspector/security/advisories/GHSA-232v-j27c-5pp6`
- CrowdSec MCPJam: `https://www.crowdsec.net/vulntracking-report/cve-2026-23744`
- Rocket.Chat advisory: `https://github.com/RocketChat/Rocket.Chat/security/advisories/GHSA-8p25-fm45-pjrw`
- GNU FreeIPMI 1.6.18: `https://lists.gnu.org/archive/html/info-gnu/2026-06/msg00000.html`
- BIRD NEWS: `https://gitlab.nic.cz/labs/bird/-/blob/master/NEWS`
- Sophos/Help Net Security AI malware lab: `https://www.helpnetsecurity.com/2026/06/02/ai-agents-edr-evasion-techniques/`
- Red Hat Miasma bulletin: `https://access.redhat.com/security/vulnerabilities/RHSB-2026-006`
- Wiz Miasma analysis: `https://www.wiz.io/blog/miasma-supply-chain-attack-targeting-redhat-npm-packages`
- Aikido Miasma analysis: `https://www.aikido.dev/blog/red-hat-npm-packages-compromised-credential-stealing-worm`
