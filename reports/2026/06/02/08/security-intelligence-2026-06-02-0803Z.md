# Security Intelligence Report - 2026-06-02 08:03 UTC

## Executive Summary

- Reporting window: primary hourly delta from 2026-06-02 07:00-08:35 UTC, with carry-forward for newly exploited or still-urgent enterprise items observed in the previous 24 hours.
- NVD CVE volume: 1 CVE published in the hourly window; 25 CVEs day-to-date; 354 CVEs in the rolling 24-hour window.
- NVD severity mix:
  - Hourly: 1 unknown/unscored.
  - Day-to-date: 1 critical, 7 medium, 15 low, 2 unknown.
  - Rolling 24h: 20 critical, 101 high, 123 medium, 66 low, 44 unknown.
- Critical findings requiring immediate review:
  - CVE-2026-41089, Microsoft Windows Netlogon RCE: CCB Belgium says active exploitation is now occurring; Microsoft patched this in the May 2026 Patch Tuesday release.
  - CVE-2026-20182, Cisco Catalyst SD-WAN Controller/Manager auth bypass: Cisco PSIRT confirms limited exploitation; CISA KEV-listed; Sploitus indexes multiple public PoC/exploit references.
  - CVE-2026-0257, Palo Alto Networks PAN-OS GlobalProtect auth bypass: vendor marks exploit maturity as ATTACKED; Rapid7 observed exploitation; CISA KEV-listed.
  - CVE-2026-35616, FortiClient EMS API auth/authz bypass: Fortinet confirms exploitation; Arctic Wolf/BleepingComputer report EKZ infostealer delivery through managed endpoint workflows.
  - CVE-2026-41940, cPanel/WHM auth bypass/RCE: Sploitus indexes multiple exploit frameworks, including a Metasploit module indicator; Shadowserver tracks .Sorry ransomware and WHMStealer compromise tags.
  - CVE-2026-26980, Ghost CMS unauthenticated SQL injection: public exploit exists; active exploitation is driving ClickFix malware delivery across 700+ compromised sites.
- New hourly vulnerability:
  - CVE-2026-8293, Really Simple Security WordPress plugin before 9.5.10.1, two-factor OTP bypass through REST endpoints. NVD lists it in the 07:00-08:35 UTC window; WPScan plugin listing corroborates the issue class and fixed version, but wider CVE-index coverage is still sparse. Confidence: Medium.
- New malware/supply-chain activity:
  - Red Hat `@redhat-cloud-services` npm packages were compromised on June 1 with the Miasma credential-stealing worm; Aikido and StepSecurity report 32 packages / 96 versions affected.
  - SANS ISC reports a SmartApeSG ClickFix chain leading to an unidentified RAT and NetSupport RAT.
  - VX-Underground GitHub repositories had no newer push after `vxunderground/MalwareSourceCode` on 2026-05-30 in this check.

## Source Coverage and Caveats

- Queried/checked: NVD API, CISA KEV JSON, Sploitus homepage and indexed Sploitus result pages, ExploitDB search results, Packet Storm search results, GitHub Advisory API, GitHub repository search, VX-Underground GitHub repositories, SANS ISC, Shadowserver, MalwareBazaar web pages, Microsoft/CCB reporting, Cisco PSIRT/Talos, Palo Alto PSIRT/Rapid7, Fortinet PSIRT/Arctic Wolf reporting, Cloud Foundry advisory, GitLab release notes, GitHub advisories, Broadcom/VMware KBs, Patchstack/Tenable/WPScan style WordPress vulnerability sources.
- Sploitus caveat: direct homepage fetch returned only the static landing/search UI and did not expose an "Exploits of the Week" block. The Sploitus Top 10 below is therefore a reconstructed list of indexed Sploitus exploit indicators, not a verified official ranking from the homepage.
- GitHub PoC caveat: repository existence is treated only as an indicator. No repository code was executed or trusted as functional exploit code.
- MalwareBazaar caveat: web pages were accessible, but the API requires authentication in this environment; sample-level enrichment was not performed.

## Top Vulnerabilities

### 1. CVE-2026-41089 - Microsoft Windows Netlogon RCE

- Severity: Critical, CVSS 9.8 per NVD/MSRC-derived records.
- Affected software: Windows Server 2012 through 2025 when acting as domain controllers.
- Exploit availability: No validated public PoC confirmed in this run; SANS Stormcast and third-party reporting discuss plausible exploit activity and GitHub code indicators. Treat any public code as unvalidated.
- Active exploitation: Yes. CCB Belgium updated its May Patch Tuesday advisory on 2026-05-29 to state that CVE-2026-41089 is actively exploited in the wild.
- KEV status: Not present among the newest CISA KEV feed entries observed in this run.
- Patch available: Yes. Microsoft May 2026 Patch Tuesday.
- Confidence: High for vulnerability and active exploitation based on CCB/NVD; Medium for public exploit availability.
- Recommended action: Emergency patch all domain controllers; restrict Netlogon/RPC/LDAP exposure to trusted networks; hunt for LSASS/Netlogon crashes and anomalous RPC/LDAP traffic.
- Sources: CCB Belgium, NVD, BleepingComputer, SANS ISC Stormcast.

### 2. CVE-2026-20182 - Cisco Catalyst SD-WAN Controller/Manager Auth Bypass

- Severity: Critical, CVSS 10.0.
- Affected software: Cisco Catalyst SD-WAN Controller and Manager across deployment models, regardless of configuration.
- Exploit availability: Public PoC/exploit references indexed by Sploitus; multiple entries describe UDP/DTLS 12346 authentication bypass, SSH key injection, and NETCONF access.
- Active exploitation: Yes. Cisco PSIRT reports limited exploitation; Cisco Talos tracks activity under UAT-8616.
- KEV status: Yes, per CISA KEV carry-forward reporting.
- Patch available: Yes. Cisco fixed releases are available; Cisco states there are no workarounds.
- Confidence: High.
- Recommended action: Upgrade to fixed Cisco SD-WAN releases immediately; collect admin-tech/control connection evidence if compromise is suspected; review NETCONF and SSH key changes.
- Sources: Cisco PSIRT, Cisco Talos, CISA KEV, Sploitus.

### 3. CVE-2026-0257 - Palo Alto Networks PAN-OS GlobalProtect Auth Bypass

- Severity: High by vendor score; operational priority critical due to exploited VPN edge exposure.
- Affected software: PAN-OS GlobalProtect portal/gateway configurations using authentication override cookies with reused certificates; Panorama and Cloud NGFW are not impacted.
- Exploit availability: Rapid7 confirms a validated PoC; no Sploitus match found in this run.
- Active exploitation: Yes. Palo Alto marks exploit maturity as ATTACKED; Rapid7 observed successful exploitation beginning May 17.
- KEV status: Yes, added 2026-05-29.
- Patch available: Yes; mitigations include disabling authentication override or using a dedicated certificate for the feature until upgraded.
- Confidence: High.
- Recommended action: Patch GlobalProtect appliances, disable vulnerable auth override configurations, rotate related certificates/cookies, and hunt for suspicious GlobalProtect cookie-based logins.
- Sources: Palo Alto Networks advisory, Rapid7, CISA KEV.

### 4. CVE-2026-35616 - FortiClient EMS API Auth/Authz Bypass

- Severity: Critical/High; Fortinet PSIRT scores 9.1, other enrichment scores up to 9.8.
- Affected software: FortiClient EMS 7.4.5 through 7.4.6.
- Exploit availability: Exploited in the wild; public technical analyses exist.
- Active exploitation: Yes. Fortinet confirms exploitation; Arctic Wolf observed EKZ infostealer delivery through FortiClient-managed VPN scripting workflows.
- KEV status: Reported as KEV-listed in April by multiple sources.
- Patch available: Yes; FortiClient EMS 7.4.7 or hotfixes for 7.4.5/7.4.6.
- Confidence: High.
- Recommended action: Patch EMS immediately, restrict EMS management exposure, audit Remote Access Profiles and `on_connect` scripts, and hunt for `Certificate not found in request header` followed by certificate update events.
- Sources: Fortinet PSIRT FG-IR-26-099, BleepingComputer, Arctic Wolf-derived reporting.

### 5. CVE-2026-41940 - cPanel/WHM Auth Bypass/RCE

- Severity: Critical, Sploitus entries cite CVSS 9.8-10.0.
- Affected software: cPanel/WHM cpsrvd in vulnerable branches before fixed releases.
- Exploit availability: Public exploit frameworks and a Metasploit module indicator indexed by Sploitus.
- Active exploitation: Yes, based on Sploitus exploit descriptions and Shadowserver compromised-website tagging for .Sorry ransomware/WHMStealer.
- KEV status: Not confirmed from the newest KEV entries viewed in this run.
- Patch available: Yes, fixed branch releases are referenced in exploit/vulnerability reporting.
- Confidence: High for public exploit availability and compromise activity; Medium for exact affected branch boundaries in this report.
- Recommended action: Patch cPanel/WHM, inspect WHM sessions and authentication logs, rotate root/API credentials, and review Shadowserver-style webshell/backdoor indicators.
- Sources: Sploitus, Shadowserver, watchTowr-linked references in exploit pages.

### 6. CVE-2026-26980 - Ghost CMS Unauthenticated SQL Injection

- Severity: Critical, CVSS 9.4 in exploit reporting.
- Affected software: Ghost CMS 3.24.0 through 6.19.0.
- Exploit availability: Yes. ExploitDB/Sploitus index Ghost CMS 6.19.0 SQLi exploit material.
- Active exploitation: Yes. Qianxin XLab/Malwarebytes/Rescana/SocPrime report 700+ Ghost sites compromised and used for ClickFix malware.
- KEV status: Not confirmed in KEV feed view.
- Patch available: Yes, Ghost 6.19.1.
- Confidence: High.
- Recommended action: Upgrade Ghost to 6.19.1 or later, rotate Admin API keys/session tokens/passwords, search content for injected JavaScript, and block known ClickFix loader domains.
- Sources: Sploitus, ExploitDB indicator, Malwarebytes, Qianxin XLab-derived reporting, SocPrime.

### 7. CVE-2026-8206 - Kirki WordPress Privilege Escalation

- Severity: Critical, CVSS 9.8 per Patchstack; NVD record appears in day-to-date critical counts.
- Affected software: Kirki Freeform Page Builder, Website Builder and Customizer WordPress plugin 6.0.0 through 6.0.6.
- Exploit availability: No validated exploit found in this run; Patchstack warns the vulnerability class is commonly mass-exploited.
- Active exploitation: Not observed in this run.
- KEV status: Not observed.
- Patch available: Yes, 6.0.7 or later.
- Confidence: High for CVE existence/impact after resolving search-result confusion with Tenable/Patchstack/NVD-derived references.
- Recommended action: Patch all Kirki installations to 6.0.7+, audit password reset events, and review administrator account changes.
- Sources: NVD API, Tenable, Patchstack.

### 8. CVE-2026-8293 - Really Simple Security WordPress 2FA OTP Bypass

- Severity: High by WPScan plugin listing; NVD hourly record currently unscored.
- Affected software: Really Simple Security WordPress plugin before 9.5.10.1.
- Exploit availability: Not found.
- Active exploitation: Not observed.
- KEV status: Not observed.
- Patch available: Yes, 9.5.10.1.
- Confidence: Medium because NVD lists the CVE and WPScan lists the underlying 2FA OTP bypass/fixed version, but broader CVE-specific indexing is sparse and some search results confused it with older Really Simple Security CVEs.
- Recommended action: Upgrade to 9.5.10.1 or later; verify 2FA flows and review recent login/session anomalies.
- Sources: NVD API, WPScan plugin listing.

### 9. CVE-2026-40965 - Cloud Foundry UAA EC Private Key Disclosure

- Severity: Critical, CVSS 10.0.
- Affected software: Cloud Foundry UAA v76.12.0 through v78.12.0 and CF Deployment v30.0.0 through v56.0.0 when EC keys are used for JWT signing.
- Exploit availability: Public endpoint exposure makes exploitation straightforward; no weaponized PoC needed to retrieve exposed material on vulnerable deployments.
- Active exploitation: Not observed.
- KEV status: Not observed.
- Patch available: Yes, uaa_release v78.13.0+ or CF Deployment v56.1.0+.
- Confidence: High.
- Recommended action: Upgrade, rotate exposed EC signing keys, invalidate tokens, and audit `/token_keys` access logs.
- Sources: Cloud Foundry advisory, NVD.

### 10. CVE-2026-47428 / CVE-2026-47429 - Vitest Browser/UI Critical Issues

- Severity: Critical.
- Affected software: `@vitest/browser` 4.0.17-4.1.5 and 5.0.0-beta.0-5.0.0-beta.2 for CVE-2026-47428; `vitest` before 4.1.0 for CVE-2026-47429.
- Exploit availability: Advisory includes confirmed local RCE proof path for browser mode token recovery and file write/config reload.
- Active exploitation: Not observed.
- KEV status: Not observed.
- Patch available: Yes, `@vitest/browser` 4.1.6 / 5.0.0-beta.3 and `vitest` 4.1.0+.
- Confidence: High.
- Recommended action: Patch developer/test environments, do not expose Vitest servers, and rotate any credentials present on developer systems where vulnerable browser/UI servers were reachable.
- Sources: GitHub Advisory Database, Vitest security advisories.

## Exploits Released

### Sploitus Top 10 Indexed Exploit Indicators

Direct Sploitus homepage extraction did not expose an official "Exploits of the Week" block. The following is a reconstructed top set from indexed Sploitus result pages, prioritized by enterprise impact, exploitation status, and weaponization potential.

| Rank | Indicator | Affected software | Exploit type | Maturity | Public PoC | Weaponization potential | Confidence |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | CVE-2026-20182 | Cisco Catalyst SD-WAN Controller/Manager | Auth bypass to privileged SD-WAN control-plane access | Weaponized; active limited exploitation | Yes | Critical: management plane takeover | High |
| 2 | CVE-2026-41940 | cPanel/WHM | CRLF/session-file auth bypass to root WHM access/RCE | Weaponized; multiple frameworks | Yes | Critical: internet-facing hosting control plane | High |
| 3 | CVE-2026-26980 | Ghost CMS | Unauthenticated SQL injection | Weaponized; active ClickFix campaign | Yes | Critical: API key theft and site poisoning | High |
| 4 | CVE-2026-9082 | Drupal core/PostgreSQL | SQL injection via JSON:API filter keys | Public PoCs and scanners | Yes | High: data theft/privilege escalation/RCE in some configurations | High |
| 5 | CVE-2026-42945 | NGINX rewrite module | Heap buffer overflow / RCE PoC | Public PoC | Yes | High for exposed affected NGINX configurations | Medium |
| 6 | CVE-2026-21858 | n8n | Content-type confusion leading to file read, session forgery, RCE chain | Public reconstructed exploit | Yes | High for workflow automation platforms | Medium |
| 7 | CVE-2026-29014 | MetInfo CMS 8.1 | PHP code injection | PacketStorm/Sploitus exploit | Yes | High for exposed CMS targets | Medium |
| 8 | CVE-2026-29000 | pac4j JWT | JWT authentication bypass via unsigned/JWE-wrapped tokens | PoC | Yes | High if vulnerable JWT validation patterns exist | Medium |
| 9 | CVE-2026-25940 | jsPDF / PDF viewers | Malicious PDF JavaScript execution path | PoC | Yes | Medium; user interaction/viewer dependent | Medium |
| 10 | CVE-2026-42897 | Exchange Health Checker | Detection blind-spot PoC for rewrite rule parsing | PoC | Yes | Medium; defensive bypass/verification impact | Medium |

### ExploitDB and Packet Storm

- ExploitDB search results did not show a new June 2 CVE-2026 ExploitDB addition. Recent ExploitDB indicators surfaced:
  - EDB-ID 52512: Throttlestop kernel driver Windows local privilege escalation, CVE-2025-7771.
  - EDB-ID 52510: Avast Antivirus 25.11 unquoted service path, no CVE.
  - EDB-ID 52511: WordPress plugin broken access control, CVE-2025-67586.
  - EDB-ID 52555 surfaced via Sploitus for Ghost CMS 6.19.0 SQLi, CVE-2026-26980.
- Packet Storm search did not return a new June 2 CVE-2026 exploit; Sploitus indexed a PacketStorm-backed MetInfo CMS exploit for CVE-2026-29014.

### GitHub PoC / Repository Signals

- Newly created GitHub repositories for `CVE-2026 exploit PoC created:>=2026-06-02`: none returned.
- Recently pushed unvalidated GitHub repository indicators:
  - `fartlover37/CVE-2026-2441-PoC` - Chrome Blink CSS use-after-free PoC claim; pushed 2026-06-02 05:52 UTC.
  - `hamzamalik3461/CVE-2026-20841` - Windows Notepad RCE claim; pushed 2026-06-02 05:49 UTC.
  - `Defacto-ridgepole254/CVE-2026-41940-Exploit-PoC` - cPanel/WHM auth bypass PoC claim; pushed 2026-06-02 06:35 UTC.
  - `Dullpurple-sloop726/CVE-2026-31431-Linux-Copy-Fail` - Linux LPE claim; pushed 2026-06-02 06:34 UTC.
  - `Recorded-texteditor120/CVE-2026-31802` - npm tar path traversal claim; pushed 2026-06-02 06:11 UTC.
  - `Jumpthereness578/CVE-2026-2991` - KiviCare auth bypass claim; pushed 2026-06-02 06:14 UTC.
  - `Liverwortenuresis371/copyfail-rs` - Linux Copy Fail detection/exploit claim; pushed 2026-06-02 06:34 UTC.
- Assessment: Treat all of the above as unvalidated and potentially malicious until reviewed in an isolated environment.

## Malware Intelligence

### VX-Underground

- `vxunderground/MalwareSourceCode` remains the most recently pushed VX repository in this check, pushed 2026-05-30 and updated 2026-06-02.
- No newer VX GitHub push was observed after the prior `MalwareSourceCode` update. Direct VX web access was not used for downloading or executing malware artifacts.
- Confidence: High for GitHub metadata, Low for absence of VX web-site-only updates.

### ClickFix / Ghost CMS

- Active campaign: CVE-2026-26980 exploitation against Ghost CMS is being used to steal Admin API keys and inject JavaScript into legitimate sites.
- Scope: Multiple reports cite 700+ compromised education, technology, SaaS, media, blockchain, and fintech sites.
- Payload flow: Fake Cloudflare/CAPTCHA verification prompts instruct visitors to run Windows/PowerShell commands, leading to malware installation.
- Recommended action: Patch Ghost, rotate Admin API keys and credentials, remove injected scripts, block known loader domains, and monitor endpoints for ClickFix command execution.
- Confidence: High.

### SmartApeSG ClickFix to Unidentified RAT and NetSupport RAT

- SANS ISC reported an infection chain where a ClickFix script led to an unidentified RAT and a malicious NetSupport Manager RAT package.
- Indicators included encoded non-TLS C2 traffic to `89.110.110[.]119:443` and NetSupport RAT C2 at `185.163.47[.]217:443`.
- Recommended action: Hunt for `processor.vbs`, `token.bat`, `setup.cab`, NetSupport RAT persistence under `C:\ProgramData\UpdateInstaller\`, and suspicious non-TLS traffic on TCP/443.
- Confidence: High.

### Red Hat npm / Miasma Supply Chain Worm

- Aikido and StepSecurity report 32 official `@redhat-cloud-services` npm packages and 96 versions compromised on June 1.
- Malware: Miasma, a Mini Shai-Hulud-like credential-stealing worm with install-time execution.
- Targets: GitHub Actions secrets, AWS/GCP/Azure credentials, Kubernetes service tokens, npm/PyPI tokens, SSH keys, Docker credentials, GPG keys, `.env` files, and other developer secrets.
- Recommended action: If affected packages were installed since June 1, isolate systems, revoke/rotate all potentially exposed secrets, review CI/CD OIDC publishing workflows, and audit for persistence artifacts.
- Confidence: High.

### Ransomware / Web Compromise Carry-Forward

- Shadowserver compromised-website reporting tracks cPanel compromise tags linked to `.Sorry` ransomware, WHMStealer, and `mr_rot13` backdoors.
- DFIR Report carry-forward: EtherRAT and TukTuk C2 activity ended in The Gentlemen ransomware in a May 2026 intrusion.
- Confidence: Medium for carry-forward relevance to this hourly window; High for source credibility.

## Security Releases and Vendor Advisories

- Microsoft: May 2026 Patch Tuesday fixes CVE-2026-41089; CCB Belgium now says active exploitation is occurring. Patch domain controllers urgently.
- Cisco: CVE-2026-20182 fixed releases are available for Catalyst SD-WAN Controller/Manager; no workarounds. Cisco PSIRT/Talos confirm exploitation.
- Palo Alto Networks: CVE-2026-0257 advisory updated 2026-05-29 with exploit maturity ATTACKED. Upgrade PAN-OS or mitigate authentication override certificate reuse.
- Fortinet: FortiClient EMS CVE-2026-35616 hotfixes and 7.4.7 remediation; Fortinet observed exploitation in the wild.
- Cloud Foundry: UAA CVE-2026-40965 fixed in uaa_release v78.13.0+ and CF Deployment v56.1.0+.
- GitLab: Patch release 19.0.1, 18.11.4, 18.10.7 fixes CVE-2026-4868 and additional Duo AI, Wiki DoS, GraphQL/API, operations, pipelines, and auth endpoint issues.
- GitHub Advisory Database:
  - Vitest CVE-2026-47428 and CVE-2026-47429 critical issues.
  - DOMPurify CVE-2026-47423 high XSS sanitizer bypass.
  - PraisonAI/PraisonAI Platform multiple critical/high authorization, IDOR, hardcoded secret, and unsafe execution issues.
- Broadcom/VMware: Dirty Frag/Fragnesia Linux kernel CVEs CVE-2026-43284, CVE-2026-43500, CVE-2026-46300 affect vSphere Kubernetes Service Ubuntu nodes only under specific module/capability conditions; Photon-based nodes are not affected per Broadcom.
- WordPress ecosystem:
  - Kirki CVE-2026-8206: upgrade to 6.0.7+.
  - Really Simple Security CVE-2026-8293: upgrade to 9.5.10.1+.

## Unified Vulnerability Records

```json
[
  {
    "cve": "CVE-2026-41089",
    "cvss": "9.8",
    "vendor": "Microsoft",
    "product": "Windows Netlogon",
    "affected_versions": "Windows Server 2012 through 2025 domain controllers before May 2026 security updates",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://ccb.belgium.be/advisories/warning-microsoft-patch-tuesday-may-2026-patches-118-vulnerabilities-16-critical-102",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-41089",
      "https://isc.sans.edu/podcastdetail/9954"
    ]
  },
  {
    "cve": "CVE-2026-20182",
    "cvss": "10.0",
    "vendor": "Cisco",
    "product": "Catalyst SD-WAN Controller and Manager",
    "affected_versions": "Affected Cisco Catalyst SD-WAN Controller/Manager releases before Cisco fixed versions",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://sploitus.com/exploit?id=13DF22F3-E9C6-58EE-B458-EB585C4D715D",
      "https://sploitus.com/exploit?id=07C61CB0-89CE-531A-855A-9BC96274E470"
    ],
    "patch_available": true,
    "sources": [
      "https://sec.cloudapps.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-sdwan-rpa2-v69WY2SW",
      "https://blog.talosintelligence.com/sd-wan-ongoing-exploitation/",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"
    ]
  },
  {
    "cve": "CVE-2026-0257",
    "cvss": "7.8",
    "vendor": "Palo Alto Networks",
    "product": "PAN-OS GlobalProtect portal/gateway",
    "affected_versions": "PAN-OS GlobalProtect configurations with authentication override cookie and certificate reuse before fixed releases",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://www.rapid7.com/blog/post/etr-rapid7-observed-exploitation-of-pan-os-globalprotect-authentication-bypass-vulnerability-cve-2026-0257/"
    ],
    "patch_available": true,
    "sources": [
      "https://security.paloaltonetworks.com/CVE-2026-0257",
      "https://www.rapid7.com/blog/post/etr-rapid7-observed-exploitation-of-pan-os-globalprotect-authentication-bypass-vulnerability-cve-2026-0257/",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"
    ]
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
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://fortiguard.fortinet.com/psirt/FG-IR-26-099",
      "https://www.bleepingcomputer.com/news/security/hackers-exploit-forticlient-ems-flaw-to-push-infostealer-malware/"
    ]
  },
  {
    "cve": "CVE-2026-41940",
    "cvss": "10.0",
    "vendor": "cPanel",
    "product": "cPanel & WHM",
    "affected_versions": "Vulnerable cPanel/WHM cpsrvd branches before fixed releases",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": false,
    "poc_links": [
      "https://sploitus.com/exploit?id=MSF%3AEXPLOIT-MULTI-HTTP-CPANEL_WHM_AUTH_BYPASS_RCE-",
      "https://sploitus.com/exploit?id=45A263F9-3CDF-57F8-9637-E0D5F28635FF"
    ],
    "patch_available": true,
    "sources": [
      "https://www.shadowserver.org/what-we-do/network-reporting/compromised-website-report/",
      "https://sploitus.com/exploit?id=557FA01A-594C-58C2-A26E-F7295CF2C82F"
    ]
  },
  {
    "cve": "CVE-2026-26980",
    "cvss": "9.4",
    "vendor": "Ghost",
    "product": "Ghost CMS",
    "affected_versions": "Ghost CMS 3.24.0 through 6.19.0",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": false,
    "poc_links": [
      "https://sploitus.com/exploit?id=EDB-ID%3A52555",
      "https://sploitus.com/exploit?id=DE7C7340-4852-590A-92BC-B6C31FAA17B7"
    ],
    "patch_available": true,
    "sources": [
      "https://www.malwarebytes.com/blog/bugs/2026/05/700-education-and-tech-websites-hijacked-in-huge-clickfix-campaign",
      "https://blog.xlab.qianxin.com/ghost-cms-mass-compromised-via-cve-2026-26980-now-fueling-clickfix-attacks/"
    ]
  },
  {
    "cve": "CVE-2026-8206",
    "cvss": "9.8",
    "vendor": "Kirki",
    "product": "Kirki WordPress plugin",
    "affected_versions": "6.0.0 through 6.0.6",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://www.tenable.com/cve/CVE-2026-8206",
      "https://patchstack.com/database/wordpress/plugin/kirki/vulnerability/wordpress-kirki-plugin-6-0-0-6-0-6-unauthenticated-privilege-escalation-via-handle-forgot-password-vulnerability",
      "https://services.nvd.nist.gov/rest/json/cves/2.0"
    ]
  },
  {
    "cve": "CVE-2026-8293",
    "cvss": "7.5",
    "vendor": "Really Simple Plugins",
    "product": "Really Simple Security WordPress plugin",
    "affected_versions": "Before 9.5.10.1",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://wpscan.com/plugin/really-simple-ssl/",
      "https://services.nvd.nist.gov/rest/json/cves/2.0"
    ]
  },
  {
    "cve": "CVE-2026-40965",
    "cvss": "10.0",
    "vendor": "Cloud Foundry",
    "product": "UAA",
    "affected_versions": "uaa_release v76.12.0 through v78.12.0; CF Deployment v30.0.0 through v56.0.0 when EC JWT signing keys are used",
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
    "cve": "CVE-2026-9082",
    "cvss": "6.5",
    "vendor": "Drupal",
    "product": "Drupal core with PostgreSQL backend",
    "affected_versions": "Drupal 8.0.0 through 11.3.9 PostgreSQL-backed sites, fixed in 11.3.10, 11.2.12, 10.6.9, 10.5.10",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://sploitus.com/exploit?id=458CE696-FE39-500F-9131-2E24B1BC2E12",
      "https://sploitus.com/exploit?id=1774D6F8-2B0F-5C66-A7AB-BE7B8E7A0B85"
    ],
    "patch_available": true,
    "sources": [
      "https://www.drupal.org/sa-core-2026-004",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://sploitus.com/exploit?id=458CE696-FE39-500F-9131-2E24B1BC2E12"
    ]
  },
  {
    "cve": "CVE-2026-47428",
    "cvss": "9.6",
    "vendor": "Vitest",
    "product": "@vitest/browser",
    "affected_versions": ">=4.0.17 <4.1.6 and >=5.0.0-beta.0 <5.0.0-beta.3",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/vitest-dev/vitest/security/advisories/GHSA-2h32-95rg-cppp"
    ],
    "patch_available": true,
    "sources": [
      "https://github.com/vitest-dev/vitest/security/advisories/GHSA-2h32-95rg-cppp",
      "https://github.com/advisories/GHSA-2h32-95rg-cppp"
    ]
  },
  {
    "cve": "CVE-2026-4868",
    "cvss": "8.2",
    "vendor": "GitLab",
    "product": "GitLab EE Duo AI workflow runners",
    "affected_versions": "GitLab EE 18.8 before 18.10.7, 18.11 before 18.11.4, and 19.0 before 19.0.1",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://docs.gitlab.com/releases/patches/patch-release-gitlab-19-0-1-released/",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-4868"
    ]
  },
  {
    "cve": "CVE-2024-21182",
    "cvss": "9.8",
    "vendor": "Oracle",
    "product": "WebLogic Server",
    "affected_versions": "Oracle WebLogic Server versions covered by Oracle July 2024 CPU before relevant patches",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://www.oracle.com/security-alerts/cpujul2024.html",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://nvd.nist.gov/vuln/detail/CVE-2024-21182"
    ]
  }
]
```

## Recommended Actions

1. Emergency patch and hunt for actively exploited network-edge/control-plane issues:
   - Microsoft domain controllers for CVE-2026-41089.
   - Cisco Catalyst SD-WAN Controller/Manager for CVE-2026-20182.
   - Palo Alto GlobalProtect for CVE-2026-0257.
   - FortiClient EMS for CVE-2026-35616.
   - cPanel/WHM for CVE-2026-41940.
2. Remediate active malware campaign vectors:
   - Patch Ghost CMS to 6.19.1+, rotate Admin API keys, remove injected JavaScript, and hunt ClickFix execution.
   - Hunt SmartApeSG/NetSupport RAT indicators from SANS ISC.
3. Treat Red Hat `@redhat-cloud-services` npm package installs since 2026-06-01 as compromise events:
   - Isolate affected build/developer hosts.
   - Rotate CI, npm, GitHub, cloud, Kubernetes, SSH, Docker, GPG, and `.env` secrets.
   - Review GitHub Actions OIDC publishing trust and package provenance.
4. Patch critical application and developer-tool releases:
   - Cloud Foundry UAA CVE-2026-40965; rotate EC signing keys and invalidate tokens.
   - Vitest CVE-2026-47428/CVE-2026-47429; prevent test servers from being exposed.
   - GitLab 19.0.1/18.11.4/18.10.7 for Duo AI and authorization issues.
   - DOMPurify 3.4.5+ where version 3.4.4 is used for untrusted HTML.
5. Address WordPress plugin exposure:
   - Kirki 6.0.7+ for CVE-2026-8206.
   - Really Simple Security 9.5.10.1+ for CVE-2026-8293.
   - Audit recent password reset and administrator-account activity.
6. Validate exploit intelligence before operational use:
   - Do not run public GitHub PoCs outside isolated sandboxes.
   - Prioritize vendor advisories, CISA KEV, and observed-exploitation reporting over repository titles or README claims.

## Confidence Summary

- High confidence: NVD/CISA counts and KEV entries, Cisco/Palo Alto/Fortinet/Microsoft/Cloud Foundry/GitLab/GitHub advisory details, Ghost ClickFix campaign, Red Hat npm Miasma compromise.
- Medium confidence: Sploitus reconstructed top-10 ranking, some Sploitus-indexed exploit maturity details, Really Simple Security CVE-2026-8293 CVE-specific enrichment, exact cPanel fixed-version boundaries.
- Low confidence: Functional status of newly pushed GitHub PoC repositories; no code was executed or validated.
