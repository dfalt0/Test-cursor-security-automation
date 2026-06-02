# Security Intelligence Report - 2026-06-02 21:02 UTC

## Executive Summary

- Total CVEs discovered in the current NVD collection window (2026-06-02 20:00-21:35 UTC): 42.
  - Severity mix: 1 critical, 19 high, 12 medium, 3 low, 7 unknown.
- Day-to-date NVD volume: 188 CVEs: 11 critical, 65 high, 86 medium, 12 low, 14 unknown.
- Rolling 24-hour NVD volume: 304 CVEs: 14 critical, 120 high, 134 medium, 22 low, 14 unknown.
- Critical findings this hour:
  - CVE-2026-5076, ARMember Premium for WordPress insecure password-reset key storage, CVSS 9.8. The issue becomes account-takeover critical when chained with ARMember SQL injection issues such as CVE-2026-5073/CVE-2026-5074.
- Active exploitation and KEV findings:
  - CISA KEV catalog version remains 2026.06.02. The newest June 2 KEV additions remain CVE-2022-0492, Linux kernel cgroups v1 release_agent privilege escalation/container escape, and CVE-2025-48595, Android Framework integer overflow/local code execution/EoP. Both have CISA due date 2026-06-05.
  - Carry-forward active exploitation remains highest priority for Cisco SD-WAN CVE-2026-20182, cPanel/WHM CVE-2026-41940, Drupal Core CVE-2026-9082, Citrix NetScaler CVE-2026-3055, and PAN-OS CVE-2026-0257.
  - Windows Netlogon CVE-2026-41089 is still treated as actively exploited with medium confidence: SANS Stormcast cites Belgium CCB exploitation warning, but this run did not identify a Microsoft active-exploitation confirmation or CISA KEV listing.
- New malware and campaign intelligence:
  - MalwareBazaar browse telemetry shows 228 submissions in the past 24 hours, with Mirai as the most-seen family.
  - VX-Underground GitHub repositories show no newer MalwareSourceCode push than 2026-05-30; latest visible malware-source addition remains `Python/Stealer.Python.GMBA.Manipulator.7z`.
  - SANS ISC reports an unidentified RAT leading to NetSupport RAT from SmartApeSG ClickFix infrastructure, and continues to discuss TeamPCP/TanStack/Nx credential-stealer supply-chain activity.
  - cPanel/WHM exploitation continues to drive Sorry ransomware, Mirai/nuclear.x86, Filemanager backdoor, and cryptominer activity in secondary and Shadowserver-linked reporting.
- Important security releases/advisories:
  - React Router published multiple advisories affecting Framework Mode/RSC/Remix paths, including CVE-2026-42211 RCE requiring an existing prototype pollution primitive and CVE-2026-42342 resource-exhaustion DoS.
  - Medplum 5.1.14 fixes authenticated FHIR Subscription endpoint SSRF, CVE-2026-49120.
  - GLPI 11.0.7 fixes knowledge-base stored XSS, CVE-2026-5385.
  - SolarWinds Web Help Desk 2026.2 fixes CVE-2026-28299 DoS.

## Top Vulnerabilities

| Priority | CVE | Severity | Affected software | Exploit availability | Active exploitation | Recommended action | Confidence |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Critical | CVE-2026-5076 plus CVE-2026-5073 chain | CVSS 9.8 critical / 7.5 high | ARMember Premium WordPress plugin through 7.3.1 | No Sploitus/GitHub PoC found in this run; exploitability is credible when chained with SQL injection | Not observed | Disable ARMember Premium or update to a vendor-fixed build newer than 7.3.1 when confirmed; audit WordPress admin accounts and `wp_usermeta` access | High for vulnerability, medium for weaponization |
| Critical | CVE-2026-20182 | CVSS 10.0 critical | Cisco Catalyst SD-WAN Controller/Manager | Public exploit indicators and Sploitus references observed in prior/current searches | KEV-listed and exploited | Complete Cisco fixed-version rollout and CISA ED 26-03 hunt/hardening guidance; inspect SD-WAN control-plane sessions | High |
| Critical | CVE-2026-41940 | CVSS 9.8 critical | cPanel & WHM / WP2 | Metasploit, Sploitus, GitHub PoCs, watchTowr PoC | KEV-listed, ransomware and botnet use | Patch immediately, rotate credentials, audit WHM sessions, web roots, cron, SSH keys, `.sorry` files, Mirai/nuclear.x86, and Filemanager backdoors | High |
| Critical | CVE-2026-41089 | CVSS 9.8 critical | Microsoft Windows Server Netlogon | Sploitus exploit write-up and GitHub indicators | SANS cites CCB exploitation warning; not KEV | Ensure May 2026 cumulative updates on all domain controllers and monitor CLDAP/Netlogon crash or LSASS anomalies | Medium |
| Critical | CVE-2026-3055 | CVSS 9.8 critical | Citrix NetScaler ADC/Gateway configured as SAML IDP | Public technical analysis and exploit indicators | Reported large-scale exploitation; CISA reference present in NVD | Patch all exposed NetScaler SAML IDP appliances, rotate SAML/session material, and review memory-disclosure impact | High |
| Critical | CVE-2026-7312 / CVE-2026-7198 | CVSS 10.0 / 9.8 critical | Progress Sitefinity 14.x/15.x | No direct PoC confirmed in this run | Not observed | Apply Progress Sitefinity May 2026 advisory fixes; prioritize internet-facing and Insight-integrated deployments | High |
| Critical | CVE-2026-24061 | CVSS 9.8 critical in Sploitus/NVD references | GNU Inetutils telnetd 1.9.3 through 2.7 indicators | Sploitus and Metasploit-style exploit indicators | Not observed | Disable Telnet, remove inetutils-telnetd exposure, or update to fixed packages; hunt for `USER=-f root` negotiation artifacts | Medium |
| Critical | CVE-2026-25643 | Critical RCE indicator | Frigate NVR through 0.16.3 | Sploitus, Packet Storm, GitHub repo pushed at 20:15 UTC | Not observed | Upgrade to Frigate 0.16.4 or later; restrict API/config endpoints and review go2rtc stream changes | Medium |
| High | CVE-2026-1829 | CVSS 8.8 high | Content Visibility for Divi Builder through 4.02 | Public verification claim found; no major exploit DB row | Not observed | Update plugin using WordPress changeset 3543621 or later; restrict contributor-level access until patched | Medium |
| High | CVE-2026-49120 | CVSS 8.5 high | Medplum before 5.1.14 | No public PoC found in this run | Not observed | Upgrade Medplum to 5.1.14; block subscription callback access to cloud metadata and RFC1918 ranges | High |
| High | CVE-2026-42211 | CVSS 8.1 high | React Router 7.0.0 through 7.14.1 in Framework Mode | No public PoC confirmed | Not observed | Upgrade React Router to 7.14.2 or later and remove prototype-pollution primitives from app code | High |
| High | CVE-2026-42342 | CVSS 7.5 high | React Router 7.0.0 through 7.14.x and @remix-run/server-runtime 2.10.0 through 2.17.4 | No public PoC confirmed | Not observed | Upgrade React Router to 7.15.0 and @remix-run/server-runtime to 2.17.5 | High |
| High | CVE-2026-48594 / CVE-2026-48595 / CVE-2026-48597 | CVSS 8.2 high | elixir-tesla Tesla middleware/adapters | GitHub advisories/commits; no exploit DB row | Not observed | Update Tesla from advisory-fixed commits; audit redirect/decompression/adapter usage in webhook/proxy/importer services | High |

## Exploits Released

### Sploitus Top 10 Reconstruction

Sploitus homepage static fetch only exposed the search shell and did not expose an "Exploits of the Week" block. The following top-10 list is reconstructed from indexed Sploitus result pages and should be treated as exploit-intelligence indicators, not proof that every exploit is safe or fully functional.

| Rank | Sploitus indicator | CVE / identifier | Affected software | Exploit type | Maturity | Weaponization potential |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | cPanel/WHM CRLF auth bypass RCE | CVE-2026-41940 | cPanel & WHM / WP2 | Pre-auth auth bypass to admin/RCE | Metasploit/Sploitus/GitHub indicators, active campaigns | Very high |
| 2 | GNU Inetutils Telnet auth bypass | CVE-2026-24061 | GNU inetutils telnetd | Telnet NEW-ENVIRON argument injection auth bypass | Multiple Sploitus entries, Metasploit-style module | Very high where telnetd is exposed |
| 3 | Windows Netlogon stack buffer overflow | CVE-2026-41089 | Windows Server Netlogon/domain controllers | Pre-auth network RCE/DoS | Sploitus write-up and GitHub indicators | Very high |
| 4 | Frigate NVR remote command execution | CVE-2026-25643 | Frigate NVR <= 0.16.3 | Config manipulation to command execution | Sploitus, Packet Storm, GitHub pushed indicator | High |
| 5 | MCPJam Inspector RCE | CVE-2026-23744 | MCPJam Inspector <= 1.4.2 | Unauthenticated command execution via `/api/mcp/connect` | Sploitus and Packet Storm indicators | High |
| 6 | Drupal Core SQL injection | CVE-2026-9082 | Drupal Core on PostgreSQL | Unauthenticated SQL injection, possible RCE in misconfigured PostgreSQL | ExploitDB 52608, Sploitus, public GitHub PoCs | High |
| 7 | Linux Copy Fail privilege escalation | CVE-2026-31431 | Linux kernel / AF_ALG or related Copy Fail indicators | Local privilege escalation | Sploitus and newly pushed GitHub indicators | High post-compromise |
| 8 | Notepad++ arbitrary code execution | CVE-2026-48778 | Notepad++ <= 8.9.6 | Local/user-context code execution via config tampering | ExploitDB 52606, Packet Storm/Sploitus | Medium |
| 9 | WP Google Map Pro admin creator | CVE-2026-8732 | WordPress WP Google Map Pro indicators | Unauthenticated token/admin creation claim | Sploitus/GitHub indicators; CVE/product status needs validation | Medium to high, low confidence |
| 10 | better-sqlcipher loadExtension RCE | CVE-2026-BetterSQLCipher-RCE (non-standard/unassigned) | better-sqlcipher | Dynamic extension loading RCE claim | Sploitus/GitHub indicator; non-standard CVE string | Medium, low confidence |

### ExploitDB Additions

- Direct ExploitDB CSV, sorted by publication date, showed no rows dated 2026-06-02.
- Latest direct ExploitDB additions remain:
  - EDB-ID 52608, 2026-06-01: Drupal Core 10.5.5 error-based SQL injection, CVE-2026-9082, webapps/php, unverified.
  - EDB-ID 52607, 2026-06-01: WordPress OrderConvo 14 path traversal, CVE-2025-10162, webapps/multiple, unverified.
  - EDB-ID 52606, 2026-05-30: Notepad++ 8.9.6 arbitrary code execution, CVE-2026-48778, remote/windows, unverified.

### New GitHub PoC / Exploit Indicators

GitHub strict search for `CVE-2026 PoC exploit created:2026-06-02` returned 0 repositories. Broader pushed-today searches returned the following unvalidated indicators:

- `DyniePro/CVE-2026-25643`, pushed 2026-06-02 20:15 UTC: Frigate NVR <= 0.16.3 command-execution exploit indicator.
- `Dullpurple-sloop726/CVE-2026-31431-Linux-Copy-Fail`, pushed 2026-06-02 20:54 UTC: Linux Copy Fail local privilege escalation indicator.
- `Defacto-ridgepole254/CVE-2026-41940-Exploit-PoC`, pushed 2026-06-02 20:54 UTC: cPanel/WHM auth-bypass PoC indicator.
- `tracyliving606/RegPwn`, pushed 2026-06-02 20:29 UTC: Windows LPE indicator for CVE-2026-24291.
- `obrunolima1910/CVE-2026-24061`, pushed 2026-06-02 19:54 UTC: GNU inetutils telnetd auth-bypass exploit indicator.
- `Jenderal92/CVE-2026-8206`, created 2026-06-02 10:53 UTC: Kirki WordPress mass-exploitation tool indicator.

Do not execute these repositories in production or analyst workstations. Treat them as collection leads and validate in disposable sandboxes because public PoC repositories are frequently trojanized.

## Malware Intelligence

### VX-Underground

- `vxunderground/MalwareSourceCode` remains the most recently pushed visible repository, pushed 2026-05-30 and updated 2026-06-02. The latest visible malware-source addition remains `Python/Stealer.Python.GMBA.Manipulator.7z`.
- No newer VX-Underground GitHub push was observed in this run.
- VX-Underground web root/search did not provide a new June 2 ransomware or malware report during this run.

### MalwareBazaar / Abuse.ch

- MalwareBazaar browse page reported 228 malware submissions in the past 24 hours.
- Most-seen malware family: Mirai.
- Operational note: this aligns with cPanel exploitation reporting that Mirai/nuclear.x86 variants are being deployed on compromised hosting infrastructure.

### Campaigns and Threat Activity

- cPanel/WHM CVE-2026-41940:
  - Shadowserver-linked reporting continues to reference at least 44,000 likely compromised cPanel instances seen attacking honeypots.
  - Sorry ransomware remains the major ransomware activity: Go-based Linux encryptor, `.sorry` extension, ChaCha20 with RSA-2048 key wrapping, README.md ransom notes, Tox contact.
  - Additional payloads reported across secondary sources: Mirai/nuclear.x86, Filemanager backdoor, cryptominers, and possible AdaptixC2 deployments.
- SANS ISC:
  - Stormcast for 2026-06-02 cites Windows Netlogon CVE-2026-41089 exploitation warning from Belgium CCB.
  - SANS diary "Unidentified RAT pushes NetSupport RAT" documents SmartApeSG ClickFix infrastructure leading to an initial RAT and malicious NetSupport Manager package.
  - TeamPCP supply-chain campaign remains relevant: TanStack/Nx Console/OIDC credential abuse, developer secret theft, and downstream compromise concerns.
- Ransomware broader context:
  - BlackFog's May 2026 ransomware report counted 95 publicly disclosed ransomware attacks across 17 countries, with healthcare as the most impacted sector and Qilin leading named victim claims with 11.

## Security Releases and Vendor Advisories

- Microsoft:
  - CVE-2026-41089, Windows Netlogon stack buffer overflow, was fixed in May 2026 Patch Tuesday. Treat domain controllers as emergency patch scope due to SANS/CCB active-exploitation warning.
- Cisco:
  - CVE-2026-20182 remains KEV-listed for Cisco Catalyst SD-WAN Controller/Manager. Follow Cisco advisory and CISA ED 26-03 hunt/hardening guidance.
- cPanel/WebPros:
  - CVE-2026-41940 remains KEV-listed and ransomware-linked. Apply fixed WHM/cPanel builds and perform compromise assessment, not patch-only remediation.
- Progress:
  - Sitefinity advisory covers CVE-2026-7312, CVE-2026-7198, CVE-2026-7195, CVE-2026-7201, and CVE-2026-7313.
- WordPress ecosystem:
  - ARMember Premium CVE-2026-5076 and SQL injection chain CVE-2026-5073 were added in the current NVD hour from Wordfence CNA data.
  - Content Visibility for Divi Builder CVE-2026-1829 has a WordPress plugin changeset reference.
- Medplum:
  - Version 5.1.14 fixes CVE-2026-49120 SSRF via FHIR Subscription endpoint handling.
- React Router / Remix:
  - CVE-2026-42211 patched in React Router 7.14.2.
  - CVE-2026-42342 patched in React Router 7.15.0 and @remix-run/server-runtime 2.17.5.
  - CVE-2026-33245 and CVE-2026-34077 affect unstable RSC redirect handling and are patched in React Router 7.13.2.
- GLPI:
  - GLPI 11.0.7 fixes CVE-2026-5385 stored XSS in knowledge-base content.
- SolarWinds:
  - Web Help Desk 2026.2 release notes/security advisory cover CVE-2026-28299 DoS.
- GitHub Security Advisories:
  - Latest reviewed advisories visible via GitHub API in this run were mostly June 1 updates; June 2 updates included Ech0 GHSA-4h9q-p5j4-xvvh (high) and GHSA-cp79-9mwr-wr49 (medium), both without CVE IDs at collection time.
- ProjectDiscovery:
  - Nuclei templates v10.4.4, released 2026-05-28, added multiple CVE-2026 templates, including critical DbGate, TYPO3, Apache Tomcat Tribes, Apache Camel, and Drupal CVE-2026-9082 KEV coverage.

## Recommended Actions

1. Emergency patch and hunt:
   - Cisco SD-WAN CVE-2026-20182, cPanel/WHM CVE-2026-41940, Citrix NetScaler CVE-2026-3055, Drupal Core CVE-2026-9082, PAN-OS CVE-2026-0257, and Windows Netlogon CVE-2026-41089.
2. Treat cPanel/WHM as incident response, not only vulnerability management:
   - Rotate WHM/root/customer credentials, inspect sessions, cron, SSH keys, web roots, WHM logs, `.sorry` extensions, Mirai/nuclear.x86, Filemanager webshells, and miner artifacts.
3. Patch or remove newly exposed WordPress components:
   - ARMember Premium, Content Visibility for Divi Builder, Kirki, WP Google Map Pro, and other recently exploited/high-risk plugins. Audit new administrator accounts and suspicious `admin-ajax.php` requests.
4. Patch developer/platform dependencies:
   - React Router/Remix, Medplum, GLPI, Tesla, and OpenClaude/Kiro/MCPJam/Frigate-style developer tooling exposures. Prioritize public admin/API panels and internal tools reachable from untrusted networks.
5. Address June 2 KEV additions:
   - CVE-2022-0492: patch Linux kernels/container hosts; restrict cgroups v1 release_agent abuse paths.
   - CVE-2025-48595: deploy Android June 2026 security update to managed fleets.
6. Harden against public PoC risk:
   - Do not run GitHub PoC repos outside disposable sandboxes. Validate with static review, network isolation, and reproducible lab targets.
7. Continue supply-chain monitoring:
   - Search for compromised npm/VS Code extension artifacts, TanStack/Nx indicators, suspicious OIDC token use, and unexpected developer-secret access.

## Unified Vulnerability Records

```json
[
  {
    "cve": "CVE-2026-5076",
    "cvss": "9.8",
    "vendor": "ARMember",
    "product": "ARMember Premium WordPress plugin",
    "affected_versions": "through 7.3.1",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": false,
    "sources": [
      "https://www.wordfence.com/threat-intel/vulnerabilities/id/6b15eca5-fd47-4f8f-8ade-3a90e0bfc110?source=cve",
      "https://codecanyon.net/item/armember-complete-wordpress-membership-system/17785056",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-5076"
    ]
  },
  {
    "cve": "CVE-2026-5073",
    "cvss": "7.5",
    "vendor": "ARMember",
    "product": "ARMember Premium WordPress plugin",
    "affected_versions": "through 7.3.1",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": false,
    "sources": [
      "https://www.wordfence.com/threat-intel/vulnerabilities/id/b5f6d2a2-ad3e-4afc-b6fd-745881d85b6b?source=cve",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-5073"
    ]
  },
  {
    "cve": "CVE-2026-1829",
    "cvss": "8.8",
    "vendor": "WordPress plugin ecosystem",
    "product": "Content Visibility for Divi Builder",
    "affected_versions": "through 4.02",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://kbin.earth/m/wordpress@lemmy.world/p/1319677/ZAST-engine-has-identified-and-verified-CVE-2026-1829-in-Content-Visibility"
    ],
    "patch_available": true,
    "sources": [
      "https://plugins.trac.wordpress.org/changeset/3543621/content-visibility-for-divi-builder",
      "https://www.wordfence.com/threat-intel/vulnerabilities/id/2ea89c44-8ed0-4ab7-a049-4d1b03a898c7?source=cve",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-1829"
    ]
  },
  {
    "cve": "CVE-2026-49120",
    "cvss": "8.5",
    "vendor": "Medplum",
    "product": "Medplum",
    "affected_versions": "before 5.1.14",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://github.com/medplum/medplum/releases/tag/v5.1.14",
      "https://www.vulncheck.com/advisories/medplum-ssrf-via-fhir-subscription-endpoint",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-49120"
    ]
  },
  {
    "cve": "CVE-2026-42211",
    "cvss": "8.1",
    "vendor": "React Router",
    "product": "React Router",
    "affected_versions": "7.0.0 through 7.14.1 in Framework Mode",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://github.com/remix-run/react-router/security/advisories/GHSA-49rj-9fvp-4h2h",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-42211"
    ]
  },
  {
    "cve": "CVE-2026-42342",
    "cvss": "7.5",
    "vendor": "React Router",
    "product": "React Router / @remix-run/server-runtime",
    "affected_versions": "react-router 7.0.0 through 7.14.x; @remix-run/server-runtime 2.10.0 through 2.17.4",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://github.com/remix-run/react-router/security/advisories/GHSA-8x6r-g9mw-2r78",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-42342"
    ]
  },
  {
    "cve": "CVE-2026-41940",
    "cvss": "9.8",
    "vendor": "WebPros",
    "product": "cPanel & WHM / WP2",
    "affected_versions": "cPanel & WHM versions after 11.40 before fixed builds",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://github.com/watchtowrlabs/watchTowr-vs-cPanel-WHM-AuthBypass-to-RCE.py",
      "https://sploitus.com/exploit?id=MSF%3AEXPLOIT-MULTI-HTTP-CPANEL_WHM_AUTH_BYPASS_RCE-"
    ],
    "patch_available": true,
    "sources": [
      "https://support.cpanel.net/hc/en-us/articles/40073787579671-cPanel-WHM-Security-Update-04-28-2026",
      "https://www.cisa.gov/known-exploited-vulnerabilities-catalog?field_cve=CVE-2026-41940",
      "https://www.bleepingcomputer.com/news/security/critrical-cpanel-flaw-mass-exploited-in-sorry-ransomware-attacks/",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-41940"
    ]
  },
  {
    "cve": "CVE-2026-20182",
    "cvss": "10.0",
    "vendor": "Cisco",
    "product": "Catalyst SD-WAN Controller / Manager",
    "affected_versions": "multiple Catalyst SD-WAN Manager/Controller versions per Cisco advisory",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://sec.cloudapps.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-sdwan-rpa2-v69WY2SW",
      "https://www.cisa.gov/known-exploited-vulnerabilities-catalog?field_cve=CVE-2026-20182",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-20182"
    ]
  },
  {
    "cve": "CVE-2026-41089",
    "cvss": "9.8",
    "vendor": "Microsoft",
    "product": "Windows Server Netlogon",
    "affected_versions": "Windows Server 2012 through 2025 indicators per NVD/MSRC",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": false,
    "poc_links": [
      "https://sploitus.com/exploit?id=B2BDADC4-FAF4-5B4E-9900-9B404553DD85"
    ],
    "patch_available": true,
    "sources": [
      "https://msrc.microsoft.com/update-guide/vulnerability/CVE-2026-41089",
      "https://isc.sans.edu/podcastdetail/9954",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-41089"
    ]
  },
  {
    "cve": "CVE-2026-3055",
    "cvss": "9.8",
    "vendor": "Citrix",
    "product": "NetScaler ADC / NetScaler Gateway configured as SAML IDP",
    "affected_versions": "multiple ADC/Gateway builds per Citrix advisory",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://labs.watchtowr.com/please-we-beg-just-one-weekend-free-of-appliances-citrix-netscaler-cve-2026-3055-memory-overread-part-2/"
    ],
    "patch_available": true,
    "sources": [
      "https://support.citrix.com/support-home/kbsearch/article?articleNumber=CTX696300",
      "https://www.cisa.gov/known-exploited-vulnerabilities-catalog?field_cve=CVE-2026-3055",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-3055"
    ]
  },
  {
    "cve": "CVE-2026-24061",
    "cvss": "9.8",
    "vendor": "GNU",
    "product": "Inetutils telnetd",
    "affected_versions": "1.9.3 through 2.7 indicators",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://sploitus.com/exploit?id=MSF%3AEXPLOIT-LINUX-TELNET-GNU_INETUTILS_AUTH_BYPASS-",
      "https://sploitus.com/exploit?id=050660E6-A5E0-5EA8-B624-03701B9D145F"
    ],
    "patch_available": true,
    "sources": [
      "https://nvd.nist.gov/vuln/detail/CVE-2026-24061",
      "https://sploitus.com/exploit?id=050660E6-A5E0-5EA8-B624-03701B9D145F"
    ]
  },
  {
    "cve": "CVE-2026-25643",
    "cvss": "critical",
    "vendor": "Frigate",
    "product": "Frigate NVR",
    "affected_versions": "through 0.16.3",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/DyniePro/CVE-2026-25643",
      "https://sploitus.com/exploit?id=20EA02CB-C9C6-536C-917F-649A3D5CBC36"
    ],
    "patch_available": true,
    "sources": [
      "https://sploitus.com/exploit?id=20EA02CB-C9C6-536C-917F-649A3D5CBC36"
    ]
  },
  {
    "cve": "CVE-2026-9082",
    "cvss": "6.5 NVD / highly critical Drupal rating",
    "vendor": "Drupal",
    "product": "Drupal Core",
    "affected_versions": "10.4.x through 10.6.x and 11.x branches before fixed releases, PostgreSQL-backed sites",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://sploitus.com/exploit?id=C5DAAA8D-8748-5503-A888-ABFFC1E3F3D7",
      "https://github.com/lysophavin18/cve-2026-9082"
    ],
    "patch_available": true,
    "sources": [
      "https://www.drupal.org/sa-core-2026-004",
      "https://www.cisa.gov/known-exploited-vulnerabilities-catalog?field_cve=CVE-2026-9082",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-9082"
    ]
  },
  {
    "cve": "CVE-2022-0492",
    "cvss": "7.8",
    "vendor": "Linux",
    "product": "Kernel cgroups v1 release_agent",
    "affected_versions": "kernel versions before upstream fixes and affected downstream builds",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=24f6008564183aa120d07c03d9289519c2fe02af",
      "https://nvd.nist.gov/vuln/detail/CVE-2022-0492"
    ]
  },
  {
    "cve": "CVE-2025-48595",
    "cvss": "unknown",
    "vendor": "Android",
    "product": "Android Framework",
    "affected_versions": "Android versions covered by June 2026 bulletin",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://source.android.com/docs/security/bulletin/2026/2026-06-01",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://nvd.nist.gov/vuln/detail/CVE-2025-48595"
    ]
  }
]
```

## Source Notes

- Primary/direct sources used in this run: NVD API, CISA KEV JSON, GitHub Security Advisory API, GitHub repository search API, ExploitDB CSV, VX-Underground GitHub repositories, MalwareBazaar browse telemetry, vendor advisories listed above.
- Secondary/contextual sources used where primary sources did not expose campaign detail: SANS ISC, Shadowserver dashboard/help references, BleepingComputer, BlackFog, SecPod, Threat-Modeling/Cyware summaries, and Sploitus indexed result pages.
- Confidence handling:
  - "High" means confirmed by primary vendor/NVD/CISA plus credible exploitation or patch references.
  - "Medium" means credible but not fully corroborated across primary sources during this run.
  - "Low" means unassigned/non-standard CVE strings, repository-only claims, or exploit claims requiring sandbox validation.
