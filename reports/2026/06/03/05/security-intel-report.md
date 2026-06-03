# Security Intelligence Report - 2026-06-03 05:03 UTC

## Executive Summary

- Collection window: primary hourly window 2026-06-03 04:00-05:35 UTC, with day-to-date and rolling 24h context through 05:35 UTC.
- NVD new CVEs: 1 CVE in the last hour (1 high), 13 CVEs day-to-date (3 high, 7 medium, 1 low, 2 unknown), and 214 CVEs in the rolling 24h context (13 critical, 81 high, 90 medium, 10 low, 20 unknown).
- Critical findings: no new critical CVE in the last hour; the highest new hourly item is FreeIPMI CVE-2026-50031. Critical carry-forward priorities remain Cisco FMC CVE-2026-20131, Cisco SD-WAN CVE-2026-20182, Citrix NetScaler CVE-2026-3055, cPanel CVE-2026-41940, Drupal CVE-2026-9082, MCPJam CVE-2026-23744, Rocket.Chat CVE-2026-29198, Progress Sitefinity CVE-2026-7312/CVE-2026-7198, Spacelabs Sentinel CVE-2026-0611, OpenMed CVE-2026-47117, authentik CVE-2026-49448, and LibreChat CVE-2026-32625.
- Active exploitation findings: CISA KEV remains at catalogVersion 2026.06.02 with new June 2 additions CVE-2022-0492 and CVE-2025-48595. Cisco FMC CVE-2026-20131, Cisco SD-WAN CVE-2026-20182, Citrix NetScaler CVE-2026-3055, cPanel CVE-2026-41940, and Drupal CVE-2026-9082 remain immediate exploited/weaponized priorities. CrowdSec reports exploitation attempts against MCPJam Inspector CVE-2026-23744.
- New malware and supply-chain intelligence: MalwareBazaar showed 201 submissions in the past 24h with Mirai as the most-seen family. VX-Underground GitHub had no new MalwareSourceCode push after 2026-05-30, but its ThreatIntelligenceDiscordBot repository was updated on 2026-06-03. The Red Hat @redhat-cloud-services npm compromise/Miasma campaign remains the top supply-chain malware item: 96 versions across 32 official packages, delivered via compromised GitHub Actions OIDC workflows.
- Important security releases/advisories: FreeIPMI 1.6.18 fixes exploitable ipmi-oem buffer overflows; Fortinet FG-IR-26-127 fixes FortiWeb privileged RCE; Docker Desktop release notes address grpcfuse CVE-2026-8936; GitHub advisories published high-severity Docker Desktop, QloApps, Drager, and related records.

## Top Vulnerabilities

### 1. Cisco Secure Firewall Management Center - CVE-2026-20131

- Severity: Critical, CVSS 10.0.
- Affected software: Cisco Secure FMC and Cisco Security Cloud Control Firewall Management.
- Exploit availability: Public PoC/exploit activity reported by Zscaler ThreatLabz; Cisco states attempted exploitation.
- Active exploitation: Yes. Cisco PSIRT updated its advisory with exploitation awareness; CISA KEV-listed; reporting links activity to Interlock ransomware before public disclosure.
- Recommended action: Patch immediately, restrict management interface exposure, inspect for Java deserialization exploit payloads and unexpected root-level changes, and rotate credentials if compromise is suspected.
- Confidence: High, based on Cisco, NVD/CISA, and Zscaler/Help Net Security corroboration.

### 2. Cisco Catalyst SD-WAN Controller/Manager - CVE-2026-20182

- Severity: Critical by prioritization because it is KEV-listed, authentication bypass, enterprise network perimeter/control-plane impact.
- Affected software: Cisco Catalyst SD-WAN Controller and Manager releases listed in Cisco advisory and CISA ED 26-03 guidance.
- Exploit availability: Public exploit indicators in exploit aggregators; treated as high maturity due KEV and emergency directive.
- Active exploitation: Yes, per CISA KEV/emergency directive context.
- Recommended action: Complete CISA ED 26-03 actions, patch affected appliances, hunt for unauthorized administrative access, and review controller logs for authentication anomalies.
- Confidence: High.

### 3. Citrix NetScaler ADC/Gateway - CVE-2026-3055

- Severity: Critical, CVSS v3.1 9.8 / CVSS v4.0 9.3 depending source.
- Affected software: NetScaler ADC and Gateway configured as SAML Identity Provider.
- Exploit availability: Public technical analysis and exploit references exist; Fortinet reports widespread exploitation attempts.
- Active exploitation: Yes. FortiGuard telemetry reports persistent targeting of exposed SAML endpoints; KEV-listed.
- Recommended action: Upgrade to fixed builds, terminate all active sessions, rotate credentials that may have transited the appliance, and hunt SAML/WS-Fed endpoint anomalies.
- Confidence: High. Note: primary sources characterize this as memory disclosure/session credential exposure, not generic RCE.

### 4. MCPJam Inspector - CVE-2026-23744

- Severity: Critical, CVSS 9.8.
- Affected software: MCPJam Inspector <= 1.4.2.
- Exploit availability: Yes. A new GitHub repository, `jf-gondim/mcp-pwn`, was created 2026-06-03 02:31 UTC and claims unauthenticated RCE PoC for `/api/mcp/connect`; GitHub advisory includes exploit detail.
- Active exploitation: Yes/attempted, per CrowdSec telemetry showing surging exploitation attempts since February.
- Recommended action: Upgrade to 1.4.3 or later, verify service binds only to 127.0.0.1, firewall port 6274 from untrusted networks, and rotate developer secrets on exposed hosts.
- Confidence: High for vulnerability and exploitation attempts; Medium for the new GitHub PoC's functional quality.

### 5. cPanel & WHM / WP2 - CVE-2026-41940

- Severity: Critical, authentication bypass; CISA KEV with known ransomware use.
- Affected software: WebPros cPanel & WHM and WP2 login-flow builds before vendor security update.
- Exploit availability: Yes, including GitHub PoC indicators pushed today.
- Active exploitation: Yes, KEV-listed and known ransomware campaign use.
- Recommended action: Apply vendor updates, review login/audit logs, force reset/rotation for panel credentials, and check for post-auth persistence/webshells.
- Confidence: High.

### 6. Drupal Core PostgreSQL SQL Injection - CVE-2026-9082

- Severity: Critical, CVSS 9.8.
- Affected software: Drupal Core with PostgreSQL backend across listed 8.9/9/10/11 branches before fixed versions.
- Exploit availability: Yes. ExploitDB EDB-ID 52608 and GitHub PoCs exist.
- Active exploitation: Yes by KEV prioritization; exploit attempts reported in prior enrichment.
- Recommended action: Patch Drupal immediately, prioritize PostgreSQL-backed internet-facing sites, review JSON:API/search endpoint traffic, and constrain DB privileges.
- Confidence: High.

### 7. Rocket.Chat OAuth2 NoSQL Injection - CVE-2026-29198

- Severity: Critical, CVSS 9.8.
- Affected software: Rocket.Chat < 8.3.0, < 8.2.1, < 8.1.2, < 8.0.3, < 7.13.5, < 7.12.6, < 7.11.6, and < 7.10.9 when OAuth apps/tokens exist.
- Exploit availability: New GitHub PoC indicator pushed today (`hieuminhnv/CVE-2026-29198-POC`); vendor advisory describes practical pre-auth token theft.
- Active exploitation: Not confirmed.
- Recommended action: Patch to fixed branch versions, audit OAuth app configuration and token issuance, revoke/rotate OAuth tokens if exposed.
- Confidence: Medium for exploit repository functionality, High for vulnerability and patch information.

### 8. FreeIPMI ipmi-oem buffer overflows - CVE-2026-50031

- Severity: High, CVSS 7.5.
- Affected software: FreeIPMI ipmi-oem before 1.6.18 (NVD text states before 1.16.18) for Dell `get-active-directory-config` and Fujitsu `get-sel-entry-long-text` response handling.
- Exploit availability: No public weaponized exploit observed in this run; upstream describes the issues as exploitable buffer overflows.
- Active exploitation: Not observed.
- Recommended action: Upgrade FreeIPMI to 1.6.18 where deployed for server/IPMI management, restrict who can invoke ipmi-oem, and treat malicious/BMC-controlled responses as an attack vector.
- Confidence: Medium because NVD publication is fresh and version text appears inconsistent with upstream release numbering; upstream release note corroborates the fixed commands.

### 9. Fortinet FortiWeb - CVE-2026-40688

- Severity: High, CVSS 7.2.
- Affected software: FortiWeb 8.0.0-8.0.3, 7.6.0-7.6.6, and 7.4.0-7.4.11.
- Exploit availability: No public PoC observed.
- Active exploitation: Not observed, not KEV-listed.
- Recommended action: Upgrade to 8.0.4, 7.6.7, or 7.4.12 and restrict admin interface exposure.
- Confidence: High from Fortinet advisory.

### 10. Progress Sitefinity - CVE-2026-7312 / CVE-2026-7198

- Severity: Critical, CVE-2026-7312 CVSS 10.0 and CVE-2026-7198 CVSS 9.8.
- Affected software: Progress Sitefinity 14.x/15.x ranges listed in Progress advisory.
- Exploit availability: No public PoC observed during this run.
- Active exploitation: Not confirmed.
- Recommended action: Apply Progress fixed builds immediately, prioritize externally exposed Sitefinity instances and web-services endpoints.
- Confidence: High.

## Exploits Released

### Sploitus Top 10 / exploit watchlist

Sploitus homepage static fetch did not expose a literal "Exploits of the Week" block; this list is reconstructed from indexed Sploitus pages plus exploit-feed and GitHub correlation. Treat it as a top exploit watchlist, not a verified Sploitus ranking.

| Rank | Indicator | Affected software | Exploit type | Maturity | Public PoC | Weaponization potential |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | CVE-2026-31431 | Linux kernel Copy Fail | Local privilege escalation / page-cache write | Multiple Sploitus entries and GitHub ports | Yes | High for post-compromise/container escape paths |
| 2 | CVE-2026-9082 | Drupal Core PostgreSQL | SQL injection / possible RCE path | ExploitDB EDB-ID 52608 and GitHub PoCs | Yes | High for internet-facing Drupal/PostgreSQL |
| 3 | CVE-2026-23744 | MCPJam Inspector | Unauthenticated RCE | New GitHub PoC plus advisory exploit detail | Yes | High for exposed AI/dev tooling |
| 4 | CVE-2026-41940 | cPanel & WHM / WP2 | Authentication bypass | KEV, ransomware use, GitHub PoC indicators | Yes | Critical for hosting providers |
| 5 | CVE-2026-29198 | Rocket.Chat | Pre-auth OAuth2 NoSQL injection/account takeover | New GitHub PoC indicator; vendor advisory detail | Yes | High where OAuth apps exist |
| 6 | CVE-2026-3055 | NetScaler ADC/Gateway | SAML memory overread/session theft | Public analyses and active telemetry | Yes | Critical for perimeter SSO appliances |
| 7 | CVE-2026-41089 | Microsoft Netlogon | Claimed RCE indicators | GitHub repos; active exploitation confidence remains mixed outside regional advisories | Unvalidated | High if confirmed; monitor only until stronger primary evidence |
| 8 | CVE-2026-9256 | NGINX | Claimed heap overflow PoC repo | New GitHub repo indicator | Unvalidated | Medium/High pending vendor corroboration |
| 9 | CVE-2026-1357 | WordPress exploit bundle | Multi-CVE WordPress exploitation kit | Sploitus indexed | Yes | Medium/High, broad CMS targeting but mixed CVE quality |
| 10 | CVE-2026-50031 | FreeIPMI ipmi-oem | Buffer overflow via crafted IPMI response | Fresh upstream/NVD disclosure | No weaponized PoC observed | Medium; requires relevant IPMI/OEM command path |

### ExploitDB additions

- Direct ExploitDB CSV retrieval from the historical GitHub raw path returned 404 and GitLab mirror fetch timed out during this run.
- Search/index validation still shows the latest notable ExploitDB item as Drupal Core CVE-2026-9082, EDB-ID 52608, dated 2026-06-01. No newer ExploitDB row was independently confirmed in this run.

### New GitHub PoCs and exploit repositories

- `jf-gondim/mcp-pwn` - created 2026-06-03 02:31 UTC; claims PoC exploit for MCPJam Inspector CVE-2026-23744 unauthenticated RCE. Treat as unvalidated but high priority because vendor advisory and CrowdSec telemetry corroborate the vulnerability and exploitation attempts.
- `hieuminhnv/CVE-2026-29198-POC` - created 2026-06-03 03:43 UTC; claims Rocket.Chat OAuth2 NoSQL injection PoC. Treat as unvalidated; vendor advisory confirms vulnerability mechanics.
- `hnytgl/CVE-2026-41089` - created 2026-06-03 02:29 UTC; claims Windows Netlogon CLDAP RCE. Treat as unvalidated; do not label as confirmed exploitation based solely on GitHub.
- `06-ux/CVE-2026-9256-POC` - created 2026-06-03 02:17 UTC; claims NGINX heap buffer overflow PoC. Treat as unvalidated pending vendor/security-advisory corroboration.
- Pushed-today unvalidated indicators also include cPanel CVE-2026-41940, Linux Copy Fail CVE-2026-31431 Rust implementations, npm tar CVE-2026-31802, Windows RegPwn CVE-2026-24291, Frigate CVE-2026-25643, and Vertex AI SDK CVE-2026-2472 repositories.

## Malware Intelligence

### VX-Underground

- `vxunderground/MalwareSourceCode` latest pushed timestamp remains 2026-05-30 07:11 UTC; no new malware-source push was observed in this run.
- `vxunderground/ThreatIntelligenceDiscordBot` showed repository metadata updated 2026-06-03 04:20 UTC but no new code push since 2024-04-24. This suggests metadata/activity but not a new malware tooling release.
- Confidence: Medium, based on GitHub API metadata only; vx-underground web root can return access restrictions from this environment.

### MalwareBazaar / abuse.ch

- MalwareBazaar browse page showed 201 submissions in the past 24h.
- Mirai was listed as the most-seen malware family in the past 24h.
- Recommended action: continue IoT/edge device monitoring for Mirai-style scanning, default-credential abuse, and ELF payload delivery.
- Confidence: High from MalwareBazaar page metadata.

### Red Hat npm / Miasma supply-chain campaign

- Multiple sources report 96 compromised versions across 32 official `@redhat-cloud-services` npm packages, published via compromised GitHub Actions OIDC workflows rather than a simple npm token theft.
- Malware behavior includes credential and secret collection: environment variables, GitHub/npm tokens, cloud credentials, SSH/private keys, Docker credentials, `.env` files, shell histories, and propagation attempts through repositories/packages.
- Recommended action: if affected package versions were installed since 2026-06-01, isolate build hosts, remove malicious package versions, rotate CI/CD, npm, GitHub, cloud, SSH, and container-registry credentials, and audit GitHub Actions OIDC/trusted publishing permissions.
- Confidence: High based on Aikido, JFrog, Wiz, Orca, and Cybersecurity Dive corroboration.

## Security Releases and Vendor Advisories

- FreeIPMI 1.6.18: fixes exploitable ipmi-oem buffer overflows in Dell and Fujitsu OEM commands. Patch server-management hosts and admin workstations with FreeIPMI tooling.
- Fortinet FG-IR-26-127: FortiWeb administrative-interface out-of-bounds write can allow privileged RCE; fixed in 8.0.4, 7.6.7, and 7.4.12.
- Cisco FMC CVE-2026-20131: no workaround; fixed software available; active exploitation acknowledged by Cisco.
- Docker Desktop release notes: addressed CVE-2026-8936 grpcfuse kernel-module VM panic and other Docker Desktop vulnerabilities; update developer endpoints.
- GitHub Advisory Database day-to-date: high-severity publications include Docker Desktop CVE-2026-8936, QloApps CVE-2026-25861 (weak crypto), and multiple Drager healthcare-device items. Medium items include MCP SSRF/regex DoS, WordPress plugin XSS/CSRF, and SourceCodester records.
- CISA KEV: catalogVersion 2026.06.02; newest additions remain Linux Kernel CVE-2022-0492 and Android Framework CVE-2025-48595, both due 2026-06-05. Microsoft Defender CVE-2026-41091/CVE-2026-45498 and older Microsoft/Adobe KEVs are due 2026-06-03.

## Recommended Actions

1. Emergency patch and hunt for exploited perimeter/control-plane systems: Cisco FMC CVE-2026-20131, Cisco SD-WAN CVE-2026-20182, Citrix NetScaler CVE-2026-3055, cPanel CVE-2026-41940, and Drupal CVE-2026-9082.
2. Identify and lock down exposed developer/AI tooling: MCPJam Inspector <= 1.4.2, LibreChat <= 0.8.3, OpenClaude before 0.5.1, Kiro IDE before 0.11, and similar MCP/agent tools. Bind local tools to loopback and require authentication.
3. Treat Red Hat npm Miasma exposure as credential compromise, not just package hygiene. Rotate secrets after cleaning hosts and reviewing CI/CD OIDC permissions.
4. Patch FreeIPMI to 1.6.18 on server-management hosts and limit ipmi-oem command use to trusted administrators.
5. Patch FortiWeb to vendor fixed versions and restrict administrative interfaces to management networks.
6. Apply Docker Desktop updates to developer workstations, especially where untrusted containers can influence bind-mounted directories.
7. For Rocket.Chat, patch to fixed branches, revoke OAuth tokens, and audit OAuth app creation/token issuance logs.
8. Monitor GitHub-only exploit repositories as indicators, not proof: do not execute PoC code without sandboxing and source review because public CVE PoCs are frequently malicious or misleading.

## Unified Vulnerability Records

```json
[
  {
    "cve": "CVE-2026-50031",
    "cvss": "7.5 HIGH",
    "vendor": "GNU",
    "product": "FreeIPMI ipmi-oem",
    "affected_versions": "FreeIPMI before 1.6.18 (NVD text: before 1.16.18); ipmi-oem Dell get-active-directory-config and Fujitsu get-sel-entry-long-text response parsing",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://nvd.nist.gov/vuln/detail/CVE-2026-50031",
      "https://lists.gnu.org/archive/html/info-gnu/2026-06/msg00000.html",
      "https://savannah.gnu.org/bugs/index.php?68363",
      "https://savannah.gnu.org/bugs/index.php?68364"
    ],
    "confidence": "Medium"
  },
  {
    "cve": "CVE-2026-23744",
    "cvss": "9.8 CRITICAL",
    "vendor": "MCPJam",
    "product": "Inspector",
    "affected_versions": "<= 1.4.2",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/jf-gondim/mcp-pwn",
      "https://github.com/MCPJam/inspector/security/advisories/GHSA-232v-j27c-5pp6"
    ],
    "patch_available": true,
    "sources": [
      "https://www.crowdsec.net/vulntracking-report/cve-2026-23744",
      "https://github.com/MCPJam/inspector/security/advisories/GHSA-232v-j27c-5pp6",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-23744"
    ],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-29198",
    "cvss": "9.8 CRITICAL",
    "vendor": "Rocket.Chat",
    "product": "Rocket.Chat OAuth2 token endpoint",
    "affected_versions": "< 8.3.0, < 8.2.1, < 8.1.2, < 8.0.3, < 7.13.5, < 7.12.6, < 7.11.6, < 7.10.9 when OAuth apps/tokens are present",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/hieuminhnv/CVE-2026-29198-POC"
    ],
    "patch_available": true,
    "sources": [
      "https://github.com/RocketChat/Rocket.Chat/security/advisories/GHSA-8p25-fm45-pjrw",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-29198",
      "https://www.sentinelone.com/vulnerability-database/cve-2026-29198/"
    ],
    "confidence": "Medium"
  },
  {
    "cve": "CVE-2026-3055",
    "cvss": "9.8 CRITICAL / CVSS v4.0 9.3",
    "vendor": "Citrix / NetScaler",
    "product": "NetScaler ADC and Gateway configured as SAML IdP",
    "affected_versions": "NetScaler ADC/Gateway vulnerable builds before vendor fixed releases; SAML IdP exposure required",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://labs.watchtowr.com/please-we-beg-just-one-weekend-free-of-appliances-citrix-netscaler-cve-2026-3055-memory-overread-part-2/"
    ],
    "patch_available": true,
    "sources": [
      "https://support.citrix.com/external/article/CTX696300/netscaler-adc-and-netscaler-gateway-secu.html",
      "https://filestore.fortinet.com/fortiguard/outbreak_alert/citrix_netscaler_memory_overread_vulnerability/report.pdf",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-3055"
    ],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-20131",
    "cvss": "10.0 CRITICAL",
    "vendor": "Cisco",
    "product": "Secure Firewall Management Center / Security Cloud Control Firewall Management",
    "affected_versions": "Affected FMC and SCC Firewall Management releases per Cisco advisory",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://www.cisco.com/c/en/us/support/docs/csa/cisco-sa-fmc-rce-NKhnULJh.html",
      "https://www.zscaler.com/blogs/security-research/critical-remote-code-execution-vulnerability-cisco-secure-firewall",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-20131"
    ],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-20182",
    "cvss": "Critical",
    "vendor": "Cisco",
    "product": "Catalyst SD-WAN Controller and Manager",
    "affected_versions": "Affected SD-WAN Controller/Manager releases per Cisco and CISA ED 26-03",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://sec.cloudapps.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-sdwan-rpa2-v69WY2SW"
    ],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-41940",
    "cvss": "9.8 CRITICAL",
    "vendor": "WebPros",
    "product": "cPanel & WHM and WP2",
    "affected_versions": "Impacted cPanel & WHM/WP2 login-flow builds before vendor updates",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://github.com/Defacto-ridgepole254/CVE-2026-41940-Exploit-PoC"
    ],
    "patch_available": true,
    "sources": [
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://support.cpanel.net/hc/en-us/articles/40073787579671-cPanel-WHM-Security-Update-04-28-2026"
    ],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-9082",
    "cvss": "9.8 CRITICAL",
    "vendor": "Drupal",
    "product": "Drupal Core with PostgreSQL backend",
    "affected_versions": "Drupal Core 8.9.x, 9.x, 10.4.x, 10.5.x, 10.6.x, and 11.x branches before advisory fixed versions when PostgreSQL backend is used",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://sploitus.com/exploit?id=EDB-ID%3A52608",
      "https://github.com/7h30th3r0n3/CVE-2026-9082-Drupal-PoC"
    ],
    "patch_available": true,
    "sources": [
      "https://www.drupal.org/sa-core-2026-004",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://www.netspi.com/blog/executive-blog/critical-vulnerability/cve-2026-9082-drupal-core-postgresql-sql-injection-overview-and-takeaways/"
    ],
    "confidence": "High"
  },
  {
    "cve": "CVE-2022-0492",
    "cvss": "7.8 HIGH",
    "vendor": "Linux",
    "product": "Kernel cgroups v1 release_agent",
    "affected_versions": "Linux kernels with vulnerable cgroups v1 release_agent behavior before upstream/distro fixes",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=24f6008564183aa120d07c03d9289519c2fe02af",
      "https://nvd.nist.gov/vuln/detail/CVE-2022-0492"
    ],
    "confidence": "High"
  },
  {
    "cve": "CVE-2025-48595",
    "cvss": "Unknown / KEV-listed",
    "vendor": "Google Android",
    "product": "Android Framework",
    "affected_versions": "Android Framework builds before June 2026 Android security bulletin fixes",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://source.android.com/docs/security/bulletin/2026/2026-06-01",
      "https://nvd.nist.gov/vuln/detail/CVE-2025-48595"
    ],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-40688",
    "cvss": "7.2 HIGH",
    "vendor": "Fortinet",
    "product": "FortiWeb CGI daemon / administrative interface",
    "affected_versions": "FortiWeb 8.0.0-8.0.3, 7.6.0-7.6.6, 7.4.0-7.4.11",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://fortiguard.fortinet.com/psirt/FG-IR-26-127",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-40688"
    ],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-8936",
    "cvss": "HIGH",
    "vendor": "Docker",
    "product": "Docker Desktop grpcfuse kernel module",
    "affected_versions": "Docker Desktop versions before release containing grpcfuse recursion fix",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://docs.docker.com/desktop/release-notes/",
      "https://github.com/advisories/GHSA-m3jp-gxgq-rpr9"
    ],
    "confidence": "Medium"
  },
  {
    "cve": "CVE-2026-49448",
    "cvss": "9.8 CRITICAL",
    "vendor": "authentik",
    "product": "authentik Source stage",
    "affected_versions": "Prior to 2025.12.6, 2026.2.4, and 2026.5.1",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://github.com/goauthentik/authentik/security/advisories/GHSA-xp7f-xjjx-gwm8",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-49448"
    ],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-32625",
    "cvss": "9.6 CRITICAL",
    "vendor": "LibreChat",
    "product": "LibreChat MCP server integration",
    "affected_versions": "<= 0.8.3",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://github.com/danny-avila/LibreChat/security/advisories/GHSA-4pcc-j6m6-wcwx",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-32625"
    ],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-0611",
    "cvss": "9.8 CRITICAL",
    "vendor": "Spacelabs Healthcare",
    "product": "Sentinel",
    "affected_versions": "10.5.x and higher and 11.x.x before 11.6.0",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://spacelabshealthcare.com/wp-content/uploads/2026/06/079-0273-00-RevA-Security-Advisory-Sentinel-.NET-Remoting-Vulnerability.pdf",
      "https://www.vulncheck.com/advisories/spacelabs-healthcare-sentinel-x-unauthenticated-rce-via-net-remoting",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-0611"
    ],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-47117",
    "cvss": "9.8 CRITICAL",
    "vendor": "OpenMed",
    "product": "OpenMed privacy-filter model loading path",
    "affected_versions": "before 1.5.2",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://github.com/maziyarpanahi/openmed/releases/tag/v1.5.2",
      "https://github.com/maziyarpanahi/openmed/pull/59",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-47117"
    ],
    "confidence": "High"
  },
  {
    "cve": "CVE-2026-7312",
    "cvss": "10.0 CRITICAL",
    "vendor": "Progress",
    "product": "Sitefinity",
    "affected_versions": "14.0.7700-15.4.8630 ranges per Progress advisory",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://community.progress.com/s/article/Sitefinity-Security-Advisory-for-Addressing-Security-Vulnerabilities-CVE-2026-7312-CVE-2026-7198-CVE-2026-7195-CVE-2026-7201-CVE-2026-7313-May-2026",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-7312"
    ],
    "confidence": "High"
  }
]
```

## Source Coverage and Caveats

- Primary sources checked: NVD API, CISA KEV JSON, GitHub Advisory API, GitHub repository search, Cisco PSIRT, Fortinet PSIRT, GNU FreeIPMI release note, Docker release notes, Rocket.Chat and MCPJam GitHub advisories, MalwareBazaar, and VX-Underground GitHub repositories.
- Secondary/enrichment sources used: CrowdSec, Zscaler ThreatLabz, Help Net Security, Aikido, JFrog, Wiz, Orca, Cybersecurity Dive, NetSPI, SentinelOne vulnerability database, and indexed Sploitus/WebSearch snippets.
- Sploitus homepage did not expose a static "Exploits of the Week" top-10 block; the Sploitus section is a reconstructed watchlist with this caveat.
- GitHub exploit repositories are unvalidated unless corroborated by primary vendor advisories, CISA KEV, exploit databases, or independent telemetry.
