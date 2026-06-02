---
report_type: hourly
generated_at: "2026-06-02T22:02:00Z"
window_start: "2026-06-02T21:00:00Z"
window_end: "2026-06-02T22:35:00Z"
new_since_last_hour: 11
ongoing_from_earlier_today: 188
severity_counts:
  critical: 2
  high: 5
  medium: 4
  low: 0
  unknown: 0
day_to_date_counts:
  total: 199
  critical: 13
  high: 70
  medium: 90
  low: 12
  unknown: 14
kev_catalog_version: "2026.06.02"
confidence: High
---

# Hourly Security Intelligence Report - 2026-06-02 22:00 UTC

## Changes This Hour

- NVD published 11 CVEs in the 21:00-22:35 UTC collection window: 2 Critical, 5 High, and 4 Medium.
- The most important new disclosures are an authentik identity-provider authentication-bypass cluster and BrowserStack Runner unauthenticated adjacent-network RCE.
- CISA KEV remains catalog version 2026.06.02. The latest June 2 KEV additions remain CVE-2022-0492 (Linux kernel cgroups v1 container escape / privilege escalation) and CVE-2025-48595 (Android Framework local code execution / elevation of privilege), both due 2026-06-05.
- No newly created GitHub PoC repository was found for CVE-2026-49448, CVE-2026-42849, CVE-2026-49143, CVE-2026-10620, or CVE-2026-5076. GitHub did show newly updated Copy Fail repositories for CVE-2026-31431.
- Sploitus homepage continues to expose only the search shell in static fetches. "Exploits of the Week" below is reconstructed from indexed Sploitus result pages and is treated as an indicator list, not proof that every exploit is functional.

## Executive Summary

- Total CVEs discovered this hour: 11.
- Critical findings this hour: 2 - CVE-2026-49448 and CVE-2026-42849, both affecting authentik.
- Active exploitation findings: no new active-exploitation claim was validated for the current-hour CVEs. Carry-forward active exploitation remains highest priority for Cisco SD-WAN CVE-2026-20182, cPanel/WHM CVE-2026-41940, Citrix NetScaler CVE-2026-3055, Windows Netlogon CVE-2026-41089, Drupal CVE-2026-9082, Oracle WebLogic CVE-2024-21182, Linux kernel CVE-2022-0492, and Android Framework CVE-2025-48595.
- New malware and phishing intelligence: SANS ISC reports a new SVG phishing wave using embedded JavaScript with `application/ecmascript` MIME-type evasion; MalwareBazaar shows 228 submissions in the past 24 hours with Mirai as the most seen family; VX-Underground GitHub repositories show no newer MalwareSourceCode push after 2026-05-30.
- Important vendor/security releases: authentik patched multiple authentication and SAML/XSS issues; Progress published Sitefinity updates for five Critical/High CVEs; BrowserStack Runner has an archived vulnerable package with no patched version; ExploitDB direct CSV latest entries remain June 1 Drupal and WordPress exploits.

Confidence: High for NVD, CISA KEV, GitHub Security Advisory, ExploitDB CSV, SANS ISC, MalwareBazaar, and vendor advisory statements. Medium for Sploitus "top 10" ordering because the homepage did not expose a native weekly list and indexed result pages were used.

## Top Vulnerabilities

### 1. CVE-2026-49448 - authentik SourceStage authentication bypass

- Severity: Critical, CVSS 9.8.
- Affected software: authentik prior to 2025.12.6, 2026.2.4, and 2026.5.1.
- Vulnerability type: authentication bypass / Source stage bypass by empty POST.
- Exploit availability: public advisory includes reproducible vulnerable behavior; no newly created GitHub PoC repository found in this run.
- Active exploitation: not observed.
- Patch available: yes - upgrade to 2025.12.6, 2026.2.4, or 2026.5.1.
- Recommended action: emergency patch for any authentik deployment using Source stages for SSO or federated login flows.
- Confidence: High.

### 2. CVE-2026-42849 - authentik Simple Flow Executor reflected XSS

- Severity: Critical, CVSS 9.3.
- Affected software: authentik prior to 2025.12.5 and 2026.2.3.
- Vulnerability type: reflected XSS in AutosubmitStage/Simple Flow Executor; possible session/token theft when OAuth2 redirect URI or state vectors are attacker-influenced.
- Exploit availability: technical write-up and vendor advisory; no new GitHub PoC repository found in this run.
- Active exploitation: not observed.
- Patch available: yes - upgrade to 2025.12.5 / 2026.2.3 or later; harden OAuth2 redirect URI matching.
- Recommended action: patch and review OAuth2 providers for permissive `matching_mode: regex` redirect patterns.
- Confidence: High.

### 3. CVE-2026-49443 and CVE-2026-47201 - authentik source-connection and SAML trust issues

- Severity: High, CVSS 8.8 and 8.5.
- Affected software: authentik prior to 2025.12.6, 2026.2.4, and 2026.5.1 for CVE-2026-49443; prior to 2025.12.5, 2026.2.3, and 2026.5.1 for CVE-2026-47201.
- Vulnerability type: source connection manipulation and SAML XML Signature Wrapping.
- Exploit availability: public GitHub Security Advisories; no new exploit repository found this hour.
- Active exploitation: not observed.
- Patch available: yes.
- Recommended action: patch alongside CVE-2026-49448; audit source-connection permissions and SAML Source ACS trust boundaries.
- Confidence: High.

### 4. CVE-2026-49143 - BrowserStack Runner unauthenticated RCE

- Severity: High, CVSS 8.8.
- Affected software: `browserstack-runner` npm package through 0.9.5.
- Vulnerability type: unauthenticated adjacent-network RCE in `/_log` HTTP handler via `vm.runInNewContext()` plus `eval()` sandbox escape.
- Exploit availability: GitHub Security Advisory contains PoC curl payload; no new standalone GitHub PoC repository found in this run.
- Active exploitation: not observed.
- Patch available: none in GHSA; repository is archived/read-only.
- Recommended action: remove package, block port 8888, run only on isolated localhost if absolutely required, and rotate BrowserStack keys exposed to affected runner hosts.
- Confidence: High.

### 5. CVE-2026-7312 / CVE-2026-7198 - Progress Sitefinity web-services criticals

- Severity: Critical, CVSS 10.0 and 9.8.
- Affected software: Progress Sitefinity 14.x and 15.x ranges for CVE-2026-7312; Sitefinity 15.4.8623 before 15.4.8630 for CVE-2026-7198.
- Vulnerability type: credential exposure and improper access control in web services.
- Exploit availability: no public PoC verified in this run.
- Active exploitation: not observed.
- Patch available: yes - Progress product updates, latest referenced version 15.4.8631.
- Recommended action: prioritize external Sitefinity instances, especially those with Sitefinity Insight integration or exposed web-services endpoints.
- Confidence: High.

### 6. CVE-2022-0492 and CVE-2025-48595 - June 2 CISA KEV additions

- Severity: High.
- Affected software: Linux kernel cgroups v1 release_agent and Android Framework.
- Vulnerability type: local privilege escalation / container escape and local code execution / elevation of privilege.
- Exploit availability: CVE-2022-0492 has historical exploit references including Packet Storm/Docker container escape; Android CVE exploit details were not public in this run.
- Active exploitation: yes, CISA KEV-listed.
- Patch available: yes through vendor/kernel/Android updates.
- Recommended action: patch or mitigate by 2026-06-05; prioritize container hosts with cgroups v1 enabled and managed Android fleets.
- Confidence: High.

### 7. CVE-2026-41940 - cPanel/WHM authentication bypass to root-equivalent access

- Severity: Critical, CVSS 9.8 to 10.0 depending source.
- Affected software: cPanel/WHM versions after 11.40 before fixed branch builds.
- Exploit availability: public PoCs, Sploitus entries, Metasploit module, watchTowr research.
- Active exploitation: yes; associated with Sorry ransomware reporting and CISA KEV.
- Patch available: yes.
- Recommended action: patch immediately, firewall ports 2082-2096 to management networks, rotate credentials and review web-hosting fleet compromise indicators.
- Confidence: High.

### 8. CVE-2026-41089 - Microsoft Windows Netlogon RCE

- Severity: Critical, CVSS 9.8.
- Affected software: Windows Server domain controllers from 2012 onward until patched May 2026 builds.
- Exploit availability: no verified public exploit in this run.
- Active exploitation: medium-confidence; CCB Belgium states active exploitation as of 2026-05-29, while Microsoft/NVD primary records initially listed no known exploitation at release.
- Patch available: yes - May 2026 cumulative updates.
- Recommended action: emergency patch domain controllers, restrict Netlogon/RPC exposure, monitor LSASS/Netlogon anomalies, and verify build levels.
- Confidence: Medium for exploitation status, High for vulnerability and patch status.

## Exploits Released

### Sploitus Top 10 - reconstructed from indexed pages

| Rank | CVE / topic | Affected software | Exploit type | Maturity | Public PoC | Weaponization potential |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | CVE-2026-41940 | cPanel/WHM | Unauth auth bypass / RCE as root-equivalent | Weaponized; Metasploit and multiple PoCs | Yes | Critical - ransomware-linked hosting compromise |
| 2 | CVE-2026-9082 | Drupal Core on PostgreSQL | Unauthenticated SQL injection via JSON:API/entity query | Multiple PoCs and ExploitDB EDB-52608 | Yes | High - internet-facing CMS fleet risk |
| 3 | CVE-2026-23744 | MCPJam Inspector <= 1.4.2 | Unauthenticated RCE via `/api/mcp/connect` | Packet Storm entry and PoCs | Yes | High - developer tooling exposure |
| 4 | CVE-2026-31431 | Linux kernel Copy Fail | Local privilege escalation via AF_ALG/splice page-cache write | Multiple Sploitus entries and GitHub repos | Yes | High - local/container escape chain potential |
| 5 | CVE-2026-41091 | Microsoft Defender RedSun | Local privilege escalation via link following | Public PoC referenced by Sploitus | Yes | High on Windows endpoints |
| 6 | CVE-2026-45185 | Exim 4.99.2 | STARTTLS/BDAT validation lab/template for UAF/RCE class | Validation template/lab | Partial | Medium to High for exposed MTAs |
| 7 | CVE-2026-1492 | WordPress User Registration & Membership plugin | Unauthenticated admin account creation | Public exploit write-up | Yes | High - WordPress fleet abuse |
| 8 | CVE-2026-27944 + CVE-2026-3888 | Nginx UI + snapd | Backup disclosure chained to LPE | Exploit chain write-up | Yes | Medium - chain requires environment fit |
| 9 | CVE-2026-42897 | Microsoft Exchange Health Checker | Mitigation audit blind spot / validation tooling | Diagnostic PoC | Yes | Medium - aids defensive validation more than direct compromise |
| 10 | CVE-2026-10620 / CVE-2026-10619 | Student Admission / management systems | SQLi and improper authentication | Public VulDB/GitHub issue references | Yes | Low to Medium - niche software |

Sploitus source notes:
- Homepage static fetch returned only search UI text.
- Indexed entries directly observed this run include cPanel/WHM CVE-2026-41940, Drupal CVE-2026-9082, MCPJam CVE-2026-23744, Linux Copy Fail CVE-2026-31431, Defender CVE-2026-41091, Exim CVE-2026-45185, WordPress CVE-2026-1492, and Nginx UI/snapd chain CVE-2026-27944/CVE-2026-3888.
- No Sploitus indexed entries were found for the fresh authentik or BrowserStack Runner CVEs at collection time.

### ExploitDB additions

- Direct ExploitDB CSV latest rows remain:
  - EDB-ID 52608 - Drupal Core 10.5.5 error-based SQL injection, CVE-2026-9082, published 2026-06-01, verified flag 0.
  - EDB-ID 52607 - WordPress OrderConvo 14 path traversal, CVE-2025-10162, published 2026-06-01, verified flag 0.
- No 2026-06-02 ExploitDB row was present in the direct CSV at collection time.

### New GitHub PoC indicators

- Strict search `CVE-2026 PoC exploit created:2026-06-02` returned no repositories.
- Fresh CVE searches for CVE-2026-49448, CVE-2026-42849, CVE-2026-49143, CVE-2026-10620, and CVE-2026-5076 returned no new repositories.
- Updated but not newly created Copy Fail indicators:
  - `Dullpurple-sloop726/CVE-2026-31431-Linux-Copy-Fail`, updated 2026-06-02T20:54:20Z.
  - `Liverwortenuresis371/copyfail-rs`, updated 2026-06-02T20:53:36Z.

## Malware Intelligence

- VX-Underground: direct web fetch returned HTTP 403; GitHub account polling succeeded. `vxunderground/MalwareSourceCode` remains the most recent pushed repository with latest commit `1623926c24245e52378f36a6a8d3bd403166a87d` on 2026-05-30. No new VX malware-source push was observed this hour.
- MalwareBazaar: browse page reports 228 malware submissions in the past 24 hours and Mirai as the most seen malware family. Treat this as commodity botnet pressure against exposed IoT/Linux services.
- SANS ISC: new SVG phishing wave uses SVG attachments containing JavaScript redirectors. The campaign uses Base64/XOR obfuscation and `application/ecmascript` MIME type to evade controls that only match common JavaScript MIME types. Recommendation: detonate SVGs in browser-like sandboxes and block/script-scan inbound SVG attachments.
- Supply chain: the Miasma / Shai-Hulud variant campaign affecting 32 `@redhat-cloud-services` npm packages remains important from earlier June 2 reporting. If those packages were installed after 2026-06-01 10:54 UTC, rotate CI, GitHub, cloud, npm, and SSH credentials and audit package-lock/yarn-lock provenance.
- Ransomware: cPanel/WHM CVE-2026-41940 remains associated with "Sorry" ransomware reporting in Sploitus-linked public analysis; no new ransomware family was validated this hour.

## Security Releases

- authentik: fixes are available for CVE-2026-49448, CVE-2026-49443, CVE-2026-47201, and CVE-2026-42849 across versions 2025.12.5/2025.12.6, 2026.2.3/2026.2.4, and 2026.5.1 depending CVE.
- BrowserStack Runner: GHSA-6vr3-7wcx-v5g5 states affected versions are `<= 0.9.5`, patched versions are "None", and the repository is archived. Remove or isolate the package.
- Progress Sitefinity: vendor advisory published 2026-06-02 for CVE-2026-7312, CVE-2026-7198, CVE-2026-7195, CVE-2026-7201, and CVE-2026-7313; product updates are available for supported versions.
- Microsoft: May 2026 cumulative updates address CVE-2026-41089; CCB Belgium updated its advisory on 2026-05-29 to state active exploitation.
- Citrix/Fortinet: Citrix CTX696300 patches NetScaler CVE-2026-3055; FortiGuard outbreak reporting continues to observe exploitation against SAML IdP configurations.
- Cisco: Cisco Catalyst SD-WAN CVE-2026-20182 remains KEV-listed and actively targeted; verify controllers/managers are on fixed builds and inspect control connections.
- GitHub Security Advisories: recent global advisory feed includes high/critical developer-tooling and AI-agent-framework items from June 1, including PraisonAI Platform critical authorization/token issues and Vitest critical browser/UI server issues; these remain relevant to development environments.

## Recommended Actions

1. Patch/mitigate all KEV and actively exploited perimeter/identity systems first: Cisco SD-WAN CVE-2026-20182, cPanel CVE-2026-41940, Citrix NetScaler CVE-2026-3055, Oracle WebLogic CVE-2024-21182, Drupal CVE-2026-9082, Linux CVE-2022-0492, Android CVE-2025-48595, and PAN-OS CVE-2026-0257.
2. Upgrade authentik immediately to the fixed release line that covers CVE-2026-49448, CVE-2026-49443, CVE-2026-47201, and CVE-2026-42849; audit OAuth2 redirect URI regexes and SAML source configurations.
3. Remove or isolate BrowserStack Runner through 0.9.5; the package is archived with no patched version. Block its test HTTP server from network access and rotate BrowserStack credentials from affected hosts.
4. Apply Progress Sitefinity 2026-06-02 updates, especially for internet-facing Sitefinity instances and sites using Sitefinity Insight or exposed OData/ServiceStack web services.
5. Continue cPanel/WHM compromise hunting for Sorry ransomware indicators, unexpected WHM sessions, modified hosting accounts, and post-auth webshells; firewall management ports to trusted networks.
6. Update mail-gateway controls to inspect SVG attachments as executable content, including `application/ecmascript`, `application/javascript`, `text/ecmascript`, inline `<script>`, `onload`, Base64/XOR blobs, and browser redirects.
7. Treat public GitHub PoC repositories as untrusted code. Review exploit repos in isolated sandboxes only and never run PoCs on analyst workstations with production credentials.

## Unified Vulnerability Records

```json
[
  {
    "cve": "CVE-2026-49448",
    "cvss": "9.8",
    "vendor": "authentik",
    "product": "authentik",
    "affected_versions": "< 2025.12.6, < 2026.2.4, < 2026.5.1",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://github.com/goauthentik/authentik/security/advisories/GHSA-xp7f-xjjx-gwm8"],
    "patch_available": true,
    "sources": ["NVD", "GitHub Security Advisory"]
  },
  {
    "cve": "CVE-2026-42849",
    "cvss": "9.3",
    "vendor": "authentik",
    "product": "authentik",
    "affected_versions": "< 2025.12.5, < 2026.2.3",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://github.com/goauthentik/authentik/security/advisories/GHSA-pgff-5mx8-fqj3", "https://docs.goauthentik.io/security/cves/CVE-2026-42849/"],
    "patch_available": true,
    "sources": ["NVD", "GitHub Security Advisory", "authentik"]
  },
  {
    "cve": "CVE-2026-49443",
    "cvss": "8.8",
    "vendor": "authentik",
    "product": "authentik",
    "affected_versions": "< 2025.12.6, < 2026.2.4, < 2026.5.1",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://github.com/goauthentik/authentik/security/advisories/GHSA-wr38-7xg8-fqxr"],
    "patch_available": true,
    "sources": ["NVD", "GitHub Security Advisory"]
  },
  {
    "cve": "CVE-2026-47201",
    "cvss": "8.5",
    "vendor": "authentik",
    "product": "authentik",
    "affected_versions": "< 2025.12.5, < 2026.2.3, < 2026.5.1",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://github.com/goauthentik/authentik/security/advisories/GHSA-c3m2-jqmq-pvp3"],
    "patch_available": true,
    "sources": ["NVD", "GitHub Security Advisory"]
  },
  {
    "cve": "CVE-2026-49143",
    "cvss": "8.8",
    "vendor": "BrowserStack",
    "product": "browserstack-runner",
    "affected_versions": "<= 0.9.5",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://github.com/browserstack/browserstack-runner/security/advisories/GHSA-6vr3-7wcx-v5g5", "https://www.vulncheck.com/advisories/browserstack-runner-unauthenticated-rce-via-log-http-handler"],
    "patch_available": false,
    "sources": ["NVD", "GitHub Security Advisory", "VulnCheck"]
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
    "sources": ["NVD", "Progress advisory"]
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
    "sources": ["NVD", "Progress advisory"]
  },
  {
    "cve": "CVE-2022-0492",
    "cvss": "7.8",
    "vendor": "Linux",
    "product": "Kernel cgroups v1",
    "affected_versions": "kernels with vulnerable cgroups v1 release_agent handling",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["http://packetstormsecurity.com/files/176099/Docker-cgroups-Container-Escape.html"],
    "patch_available": true,
    "sources": ["CISA KEV", "NVD", "kernel.org"]
  },
  {
    "cve": "CVE-2025-48595",
    "cvss": "8.4",
    "vendor": "Google",
    "product": "Android Framework",
    "affected_versions": "Android versions covered by June 2026 security bulletin",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": ["CISA KEV", "NVD", "Android Security Bulletin"]
  },
  {
    "cve": "CVE-2026-41940",
    "cvss": "9.8",
    "vendor": "cPanel",
    "product": "cPanel & WHM",
    "affected_versions": "versions after 11.40 before fixed branch builds",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://github.com/watchtowrlabs/watchTowr-vs-cPanel-WHM-AuthBypass-to-RCE.py", "https://sploitus.com/exploit?id=MSF%3AEXPLOIT-MULTI-HTTP-CPANEL_WHM_AUTH_BYPASS_RCE-"],
    "patch_available": true,
    "sources": ["NVD", "CISA KEV", "watchTowr", "Sploitus", "Exploit/Metasploit indicators"]
  },
  {
    "cve": "CVE-2026-41089",
    "cvss": "9.8",
    "vendor": "Microsoft",
    "product": "Windows Netlogon",
    "affected_versions": "Windows Server domain controllers 2012 through 2025 before May 2026 fixed builds",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["NVD", "Microsoft MSRC", "CCB Belgium"]
  }
]
```

## Sources

- NVD CVE API: https://services.nvd.nist.gov/rest/json/cves/2.0
- CISA KEV JSON: https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json
- Sploitus: https://sploitus.com/
- ExploitDB CSV: https://gitlab.com/exploit-database/exploitdb/-/raw/main/files_exploits.csv
- GitHub advisories and repository search via GitHub API.
- authentik advisories: https://github.com/goauthentik/authentik/security/advisories/GHSA-xp7f-xjjx-gwm8, https://github.com/goauthentik/authentik/security/advisories/GHSA-pgff-5mx8-fqj3, https://github.com/goauthentik/authentik/security/advisories/GHSA-wr38-7xg8-fqxr, https://github.com/goauthentik/authentik/security/advisories/GHSA-c3m2-jqmq-pvp3
- BrowserStack Runner GHSA: https://github.com/browserstack/browserstack-runner/security/advisories/GHSA-6vr3-7wcx-v5g5
- Progress Sitefinity advisory: https://community.progress.com/s/article/Sitefinity-Security-Advisory-for-Addressing-Security-Vulnerabilities-CVE-2026-7312-CVE-2026-7198-CVE-2026-7195-CVE-2026-7201-CVE-2026-7313-May-2026
- SANS ISC: https://isc.sans.edu/diary/rss
- MalwareBazaar: https://bazaar.abuse.ch/browse/
- VX-Underground GitHub: https://github.com/vxunderground/MalwareSourceCode
- CCB Belgium Microsoft Patch Tuesday advisory: https://ccb.belgium.be/advisories/warning-microsoft-patch-tuesday-may-2026-patches-118-vulnerabilities-16-critical-102
- Fortinet/FortiGuard NetScaler outbreak report: https://filestore.fortinet.com/fortiguard/outbreak_alert/citrix_netscaler_memory_overread_vulnerability/report.pdf
