# Security Intelligence Report - 2026-06-02 00:05 UTC

## Report metadata

- Automation run: 2026-06-02 00:05 UTC
- Reporting window: primary collection from 2026-06-01 00:00 UTC through 2026-06-02 00:05 UTC, with urgent exploited carryover from late May 2026 included for remediation priority.
- Repository: `dfalt0/Test-cursor-security-automation`
- Report path: `reports/2026/06/02/00/security-intelligence-report-2026-06-02T0005Z.md`
- Confidence scale: High = primary source plus corroboration; Medium = credible source or aggregator plus partial corroboration; Low = single-source or unvalidated repository indicator.

## Executive summary

- Total newly published NVD CVEs observed for the window: 377.
  - Critical: 20
  - High: 104
  - Medium: 114
  - Low: 73
  - Unknown/unscored: 66
- New KEV activity: CISA KEV catalog version `2026.06.01` added CVE-2024-21182, an Oracle WebLogic Server vulnerability, on 2026-06-01 with a 2026-06-04 due date.
- Active exploitation priorities:
  - Cisco Catalyst SD-WAN Controller/Manager CVE-2026-20182: CVSS 10.0, CISA KEV, Cisco PSIRT confirms limited exploitation, and Talos reports UAT-8616 activity plus broader SD-WAN webshell/tooling activity.
  - Palo Alto PAN-OS CVE-2026-0300 and CVE-2026-0257: Palo Alto marks both as `ATTACKED`; CISA KEV lists both.
  - Fortinet FortiCloud SSO authentication bypass FG-IR-26-060: Fortinet states exploitation in the wild and server-side FortiCloud SSO mitigation.
  - cPanel/WHM CVE-2026-41940: CISA KEV, ransomware use known in KEV, and multiple public exploit artifacts including Metasploit/ExploitDB/Sploitus indicators.
  - Drupal Core CVE-2026-9082 and LiteLLM CVE-2026-42208: both CISA KEV-listed with public PoC or detector material.
- New malware and threat intelligence:
  - TeamPCP/Mini Shai-Hulud supply-chain operations remain enterprise-actionable, affecting npm, PyPI, VS Code extensions, GitHub Actions/OIDC, and developer credentials. CISA KEV lists related Nx Console and TanStack issues with known ransomware-campaign-use marked `Known`.
  - CrowdStrike reports a coordinated takedown of the Glassworm developer-targeting botnet on 2026-05-26; infections now beacon to `164.92.88[.]210`.
  - Huntress and The DFIR Report document The Gentlemen ransomware operations using scheduled tasks, PowerShell, Defender tampering, event log clearing, EtherRAT/TukTuk, SaaS/decentralized C2, Rclone exfiltration, and GPO-based ransomware deployment.
- Important security releases/advisories:
  - Android XR June 2026 bulletin published with CVE-2026-0072.
  - Apple released iOS 26.5.1 and macOS Tahoe 26.5.1 on 2026-06-01 with no published CVE entries.
  - GitHub changelog highlights npm staged publishing and install-time controls on 2026-05-22.
  - Fortinet PSIRT published May 12 advisories including FG-IR-26-136, a critical unauthenticated FortiSandbox authorization issue.
  - GitHub Security Advisories on 2026-06-01 include critical Vitest and praisonai-platform advisories; several were not yet present in NVD at collection time.

## Highest-priority vulnerability records

### 1. CVE-2024-21182 - Oracle WebLogic Server unspecified vulnerability

```json
{
  "cve": "CVE-2024-21182",
  "cvss": "7.5 HIGH (NVD)",
  "vendor": "Oracle",
  "product": "WebLogic Server",
  "affected_versions": "Oracle WebLogic Server versions covered by Oracle July 2024 CPU guidance",
  "exploit_available": "unknown",
  "active_exploitation": true,
  "kev_listed": true,
  "poc_links": [],
  "patch_available": true,
  "sources": [
    "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
    "https://www.oracle.com/security-alerts/cpujul2024.html",
    "https://nvd.nist.gov/vuln/detail/CVE-2024-21182"
  ]
}
```

- Priority: Critical operational priority because it was newly added to CISA KEV on 2026-06-01.
- Recommended action: apply Oracle CPU guidance immediately, restrict T3/IIOP exposure, and verify WebLogic inventory for internet-facing or partner-facing deployments.
- Confidence: High.

### 2. CVE-2026-20182 - Cisco Catalyst SD-WAN Controller/Manager authentication bypass

```json
{
  "cve": "CVE-2026-20182",
  "cvss": "10.0 CRITICAL (NVD/Cisco)",
  "vendor": "Cisco",
  "product": "Catalyst SD-WAN Controller and Manager",
  "affected_versions": "Multiple 20.x and 26.x releases; see Cisco fixed release matrix",
  "exploit_available": true,
  "active_exploitation": true,
  "kev_listed": true,
  "poc_links": [
    "https://sploitus.com/exploit?id=13DF22F3-E9C6-58EE-B458-EB585C4D715D",
    "https://sploitus.com/exploit?id=MSF%3AAUXILIARY-ADMIN-NETWORKING-CISCO_SDWAN_VHUB_AUTH_BYPASS-"
  ],
  "patch_available": true,
  "sources": [
    "https://sec.cloudapps.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-sdwan-rpa2-v69WY2SW",
    "https://blog.talosintelligence.com/sd-wan-ongoing-exploitation/",
    "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
    "https://nvd.nist.gov/vuln/detail/CVE-2026-20182"
  ]
}
```

- Exploit status: weaponized. Cisco confirms limited exploitation; Talos reports active exploitation by UAT-8616 and broader exploitation of related SD-WAN vulnerabilities with webshells and tooling.
- Recommended action: collect `admin-tech` and preserve logs before upgrade, upgrade to a fixed release, inspect auth logs for unauthorized `vmanage-admin` public-key access, validate peering events, and follow Cisco TAC/CISA emergency guidance.
- Confidence: High.

### 3. CVE-2026-0300 - Palo Alto PAN-OS User-ID Authentication Portal RCE

```json
{
  "cve": "CVE-2026-0300",
  "cvss": "9.3 CRITICAL (NVD/Palo Alto)",
  "vendor": "Palo Alto Networks",
  "product": "PAN-OS User-ID Authentication Portal",
  "affected_versions": "PAN-OS 10.2, 11.1, 11.2, 12.1 ranges listed in advisory",
  "exploit_available": "not confirmed public",
  "active_exploitation": true,
  "kev_listed": true,
  "poc_links": [],
  "patch_available": true,
  "sources": [
    "https://security.paloaltonetworks.com/CVE-2026-0300",
    "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
    "https://nvd.nist.gov/vuln/detail/CVE-2026-0300"
  ]
}
```

- Exploit status: Palo Alto marks exploit maturity `ATTACKED` and states limited exploitation against exposed User-ID Authentication Portals.
- Recommended action: patch to fixed PAN-OS releases, restrict User-ID Authentication Portal to trusted/internal zones, disable the portal if unused, and deploy Threat ID 510019 where applicable.
- Confidence: High.

### 4. CVE-2026-0257 - Palo Alto PAN-OS GlobalProtect authentication bypass

```json
{
  "cve": "CVE-2026-0257",
  "cvss": "7.8 HIGH (NVD/Palo Alto)",
  "vendor": "Palo Alto Networks",
  "product": "PAN-OS GlobalProtect portal and gateway",
  "affected_versions": "PAN-OS 10.2, 11.1, 11.2, 12.1 and Prisma Access ranges listed in advisory",
  "exploit_available": "not confirmed public",
  "active_exploitation": true,
  "kev_listed": true,
  "poc_links": [],
  "patch_available": true,
  "sources": [
    "https://security.paloaltonetworks.com/CVE-2026-0257",
    "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
    "https://nvd.nist.gov/vuln/detail/CVE-2026-0257"
  ]
}
```

- Exploit status: Palo Alto marks exploit maturity `ATTACKED` and reports limited attempts against unpatched devices without mitigations.
- Recommended action: upgrade to fixed versions; if immediate patching is not possible, disable authentication override cookies or use a dedicated certificate exclusively for authentication override cookies.
- Confidence: High.

### 5. CVE-2026-41940 - cPanel & WHM authentication bypass

```json
{
  "cve": "CVE-2026-41940",
  "cvss": "9.3 CRITICAL (NVD)",
  "vendor": "WebPros",
  "product": "cPanel & WHM and WP2",
  "affected_versions": "Prior to cPanel fixed trains including 11.110.0.97, 11.118.0.63, 11.126.0.54, 11.132.0.29, 11.134.0.20, 11.136.0.5 and later fixed versions",
  "exploit_available": true,
  "active_exploitation": true,
  "kev_listed": true,
  "poc_links": [
    "https://sploitus.com/exploit?id=MSF%3AEXPLOIT-MULTI-HTTP-CPANEL_WHM_AUTH_BYPASS_RCE-",
    "https://sploitus.com/exploit?id=EDB-ID%3A52574",
    "https://raw.githubusercontent.com/projectdiscovery/nuclei-templates/main/http/cves/2026/CVE-2026-41940.yaml"
  ],
  "patch_available": true,
  "sources": [
    "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
    "https://raw.githubusercontent.com/projectdiscovery/nuclei-templates/main/http/cves/2026/CVE-2026-41940.yaml",
    "https://nvd.nist.gov/vuln/detail/CVE-2026-41940"
  ]
}
```

- Exploit status: weaponized. Sploitus indexes Metasploit and ExploitDB artifacts; ProjectDiscovery has a verified template; CISA KEV marks known ransomware campaign use.
- Recommended action: patch exposed WHM/cPanel immediately, review administrator accounts and session activity, and hunt for `.sorry` ransomware indicators where hosting systems were exposed.
- Confidence: High.

### 6. CVE-2026-9082 - Drupal Core SQL injection

```json
{
  "cve": "CVE-2026-9082",
  "cvss": "9.8 CRITICAL (NVD/ProjectDiscovery)",
  "vendor": "Drupal",
  "product": "Drupal Core with PostgreSQL-backed affected paths",
  "affected_versions": "8.9.0 before 10.4.10, 10.5.0 before 10.5.10, 10.6.0 before 10.6.9, 11.0.0 before 11.1.10, 11.2.0 before 11.2.12, 11.3.0 before 11.3.10",
  "exploit_available": true,
  "active_exploitation": true,
  "kev_listed": true,
  "poc_links": [
    "https://raw.githubusercontent.com/projectdiscovery/nuclei-templates/main/http/cves/2026/CVE-2026-9082.yaml",
    "https://sploitus.com/exploit?id=458CE696-FE39-500F-9131-2E24B1BC2E12"
  ],
  "patch_available": true,
  "sources": [
    "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
    "https://raw.githubusercontent.com/projectdiscovery/nuclei-templates/main/http/cves/2026/CVE-2026-9082.yaml",
    "https://www.drupal.org/sa-core-2026-004",
    "https://nvd.nist.gov/vuln/detail/CVE-2026-9082"
  ]
}
```

- Exploit status: public PoC/detector and mass-scan tooling indicators exist. Do not assume every GitHub repository is safe or functional.
- Recommended action: patch affected Drupal branches immediately, prioritize PostgreSQL-backed internet-facing Drupal sites with JSON:API/REST/views exposure, and monitor for SQL error probes.
- Confidence: High.

### 7. CVE-2026-42208 - BerriAI LiteLLM pre-authentication SQL injection

```json
{
  "cve": "CVE-2026-42208",
  "cvss": "9.3 CRITICAL (NVD/GHSA)",
  "vendor": "BerriAI",
  "product": "LiteLLM",
  "affected_versions": ">= 1.81.16 and < 1.83.7-stable per advisory indicators",
  "exploit_available": true,
  "active_exploitation": true,
  "kev_listed": true,
  "poc_links": [
    "https://sploitus.com/exploit?id=2DA57135-57BB-597F-8C0D-BCCBAEE544E5",
    "https://github.com/BerriAI/litellm/security/advisories/GHSA-r75f-5x8p-qvmc"
  ],
  "patch_available": true,
  "sources": [
    "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
    "https://github.com/BerriAI/litellm/security/advisories/GHSA-r75f-5x8p-qvmc",
    "https://nvd.nist.gov/vuln/detail/CVE-2026-42208",
    "https://sploitus.com/exploit?id=2DA57135-57BB-597F-8C0D-BCCBAEE544E5"
  ]
}
```

- Exploit status: public lab reproduction and exploitation notes are indexed; KEV listing indicates exploitation.
- Recommended action: upgrade LiteLLM, rotate credentials stored in or proxied through exposed LiteLLM deployments, and inspect proxy database access logs for SQLi indicators in bearer tokens.
- Confidence: High.

### 8. CVE-2026-44211 - Cline cross-origin WebSocket hijack

```json
{
  "cve": "CVE-2026-44211",
  "cvss": "9.6 CRITICAL (NVD)",
  "vendor": "Cline",
  "product": "Cline Kanban servers",
  "affected_versions": "2.13.0 and prior",
  "exploit_available": "not confirmed",
  "active_exploitation": false,
  "kev_listed": false,
  "poc_links": [],
  "patch_available": false,
  "sources": [
    "https://github.com/cline/cline/security/advisories/GHSA-5c57-rqjx-35g2",
    "https://nvd.nist.gov/vuln/detail/CVE-2026-44211"
  ]
}
```

- Risk: newly published critical developer-tool vulnerability with no patch at NVD publication time.
- Recommended action: disable or isolate affected Cline Kanban servers, restrict network exposure, and monitor for unauthorized WebSocket interactions until patched.
- Confidence: High for disclosure; Medium for exploitability in specific environments.

### 9. CVE-2026-49121 - ROCm AITER unauthenticated RCE

```json
{
  "cve": "CVE-2026-49121",
  "cvss": "9.2 CRITICAL (NVD)",
  "vendor": "ROCm",
  "product": "AI Tensor Engine for ROCm (AITER)",
  "affected_versions": "through 0.1.14",
  "exploit_available": "advisory-level technical detail",
  "active_exploitation": false,
  "kev_listed": false,
  "poc_links": [
    "https://github.com/ROCm/aiter/issues/3076",
    "https://github.com/ROCm/aiter/pull/3170"
  ],
  "patch_available": true,
  "sources": [
    "https://www.vulncheck.com/advisories/ai-tensor-engine-for-rocm-aiter-unauthenticated-rce-via-messagequeue-recv-pickle-deserialization",
    "https://github.com/ROCm/aiter/issues/3076",
    "https://github.com/ROCm/aiter/pull/3170",
    "https://nvd.nist.gov/vuln/detail/CVE-2026-49121"
  ]
}
```

- Risk: unauthenticated RCE in AI/ML infrastructure via pickle deserialization in `MessageQueue.recv()`.
- Recommended action: update AITER, block untrusted network access to affected message queues, and inventory ROCm/AI build and inference environments.
- Confidence: High.

### 10. CVE-2026-40965 - Cloud Foundry UAA private key exposure

```json
{
  "cve": "CVE-2026-40965",
  "cvss": "10.0 CRITICAL (NVD)",
  "vendor": "Cloud Foundry",
  "product": "UAA",
  "affected_versions": "v76.12.0 through v78.12.0",
  "exploit_available": "not applicable; key exposure endpoint",
  "active_exploitation": false,
  "kev_listed": false,
  "poc_links": [],
  "patch_available": true,
  "sources": [
    "https://www.cloudfoundry.org/blog/cve-2026-40965-uaa-ec-private-key-disclosure/",
    "https://nvd.nist.gov/vuln/detail/CVE-2026-40965"
  ]
}
```

- Risk: EC private keys inadvertently exposed through `/token_keys`, potentially invalidating token trust.
- Recommended action: patch UAA, rotate exposed EC signing keys, revoke/reissue tokens where exposure is confirmed, and review access logs for `/token_keys`.
- Confidence: High.

## Additional newly published critical NVD items to triage

| CVE | Severity | Product / vendor | Why it matters | Recommended action | Confidence |
| --- | --- | --- | --- | --- | --- |
| CVE-2026-48188 | 9.1 Critical | OTRS / ((OTRS)) Community Edition | Unauthenticated SQL injection can lead to authentication bypass under specific MySQL/MariaDB `NO_BACKSLASH_ESCAPES` configuration. | Apply OTRS Security Advisory 2026-02 and check database SQL mode. | High |
| CVE-2026-7858 | 9.8 Critical | No Magic Teamwork Cloud / CATIA Magic Collaboration Studio | Unauthenticated deserialization RCE in enterprise modeling/collaboration software. | Apply Dassault Systemes advisory fixes and restrict management exposure. | High |
| CVE-2026-0826 | 9.2 Critical | HP Poly Voice products | Remote code execution on Linux platform when ICE is enabled. | Apply HP advisory HPSBPY04083 and review external voice device exposure. | High |
| CVE-2026-8931 | 9.4 Critical | Disig Web Signer | RCE in versions 2.0.3 through 2.5.3. | Upgrade to vendor fixed release; prioritize signing workstations and shared servers. | High |
| CVE-2026-45131 / CVE-2026-45132 | 10.0 Critical | CloudPirates Helm Charts GitHub Actions workflows | Fork PR workflows exposed Docker Hub/PAT/SSH signing credentials in privileged contexts. | Apply fixed commit, rotate CI/CD credentials, review workflow permissions. | High |
| CVE-2026-0072 | NVD 10.0 Critical; Android XR bulletin rates High | Android XR | Local EoP/input text exposure in XR component. | Apply Android XR 2026-06-01/2026-06-05 patch level. | Medium-High due source severity discrepancy |
| CVE-2026-8644 / CVE-2026-9311 / CVE-2026-9319 | 9.0-9.1 Critical | IBM WebSphere Application Server | Identity spoofing and RCE/deserialization issues in WebSphere 8.5/9.0. | Apply IBM support fixes and restrict administrative/application interfaces. | High |
| CVE-2026-25879 | 9.8 Critical | Langroid | LLM-driven SQL agent can execute dangerous SQL leading to code execution or filesystem access when over-privileged DB roles are used. | Upgrade to 0.63.0+ and restrict database roles used by agents. | High |
| CVE-2026-9092 | 9.1 Critical | Casdoor | Account takeover via unverified upstream email binding. | Upgrade beyond 2.362.0 and require verified email claims from identity providers. | High |

## Exploits released and public PoC indicators

### Sploitus top-10 reconstruction

Sploitus homepage static content did not expose an "Exploits of the Week" block during this run. The following top-10 is reconstructed from indexed Sploitus exploit pages, de-duplicated by CVE, and should be treated as exploit-intelligence indicators requiring validation.

| Rank | CVE / item | Affected software | Exploit type | Maturity | Public PoC | Weaponization potential | Confidence |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | CVE-2026-20182 | Cisco Catalyst SD-WAN Controller/Manager | Remote auth bypass / admin access | Weaponized; Metasploit auxiliary and GitHub PoC indicators | Yes | Very high; KEV and active exploitation | High |
| 2 | CVE-2026-41940 | cPanel & WHM | Remote auth bypass to WHM/root access | Weaponized; Metasploit, ExploitDB, scanners, ransomware reporting | Yes | Very high; KEV and ransomware use | High |
| 3 | CVE-2026-9082 | Drupal Core | Unauthenticated SQL injection | PoC, detector, mass-scan tooling | Yes | High; KEV and broad CMS exposure | High |
| 4 | CVE-2026-42208 | LiteLLM | Pre-auth SQL injection | Lab exploit and technical reproduction | Yes | High for exposed LiteLLM proxies with secrets | High |
| 5 | CVE-2026-42945 | NGINX "Rift" | Config-dependent heap overflow RCE | Lab RCE PoC with hardcoded offsets; production exploitation needs info leak/config match | Yes | Medium-high; constrained by config/ASLR | Medium-High |
| 6 | CVE-2026-31431 | Linux kernel "Copy Fail" | Local privilege escalation via AF_ALG/page-cache write | Public detector and LPE toolkit indicators | Yes | High post-compromise; patch kernels | Medium-High |
| 7 | CVE-2026-2329 | Grandstream GXP1600 | Unauthenticated RCE | Metasploit module indicator | Yes | High for exposed VoIP devices | Medium-High |
| 8 | CVE-2026-29014 | MetInfo CMS 7.9-8.1 | PHP code injection / RCE | Packet Storm indexed PoC | Yes | Medium; depends on MetInfo exposure | Medium |
| 9 | CVE-2026-20700 | Apple iPadOS dyld | Local/research PoC around PAC signing oracle | Research PoC | Yes | Medium; local and platform-specific | Medium |
| 10 | CVE-2025-6965 | SQLite/winsqlite3 | Heap overflow / DoS or potential RCE claims | ExploitDB indexed PoC | Yes | Medium; validate vendor impact before action | Low-Medium |

### ExploitDB additions

- Static fetch of the ExploitDB landing page did not expose recent rows. Indexed Sploitus entries reference ExploitDB IDs for cPanel/WHM CVE-2026-41940 (`EDB-ID:52574`) and SQLite CVE-2025-6965 (`EDB-ID:52499`).
- Treat these as public exploit indicators; do not execute PoCs without sandbox review.

### Packet Storm additions

- Direct Packet Storm fetch was blocked by the site. Indexed Sploitus entry `PACKETSTORM:218222` references MetInfo CMS CVE-2026-29014 PHP code injection.

### GitHub PoC monitoring

- Direct GitHub repository search for `CVE-2026 exploit PoC` returned no fresh repositories in the queried result set.
- However, Sploitus and ProjectDiscovery references point to public PoC/detector material for Cisco SD-WAN, cPanel/WHM, Drupal, NGINX Rift, LiteLLM, and Linux kernel LPE items.
- Caution: no GitHub PoC was executed or safety-reviewed. Public exploit repositories may be incomplete, non-functional, or malicious.

## Malware intelligence and threat activity

### TeamPCP / Mini Shai-Hulud supply-chain campaign

- Sources: SANS ISC diary 33016 and Unit 42 npm threat landscape update.
- What changed:
  - May waves affected npm, PyPI, VS Code extensions, GitHub Actions/OIDC trust paths, TanStack, Nx Console, `@antv`, and Microsoft-published `durabletask` package versions.
  - SANS reports Nx Console v18.95.0 was live briefly in the Visual Studio Marketplace and tied to a GitHub internal repository exfiltration event; affected developers and CI/CD should be treated as credential-exposure events.
  - Unit 42 reports Mini Shai-Hulud source-code publication/copycat risk and May 19 `@antv` wave with 639 malicious versions across 323 packages.
- Related KEV records:
  - CVE-2026-48027 (Nx Console embedded malicious code) - KEV date 2026-05-27, known ransomware campaign use `Known`.
  - CVE-2026-45321 (TanStack malicious publish path) - KEV date 2026-05-27, known ransomware campaign use `Known`.
- Recommended action:
  - Inventory Nx Console v18.95.0, affected TanStack, `@antv`, and `durabletask` versions.
  - Rotate GitHub, npm, cloud, Vault, Kubernetes, CI/CD, 1Password/Bitwarden, and developer tokens exposed on affected hosts.
  - Inspect `.vscode/tasks.json`, `~/.claude/settings.json`, GitHub Actions caches, OIDC trust policies, package lockfiles, and unusual public repository creation.
- Confidence: High.

### Glassworm developer botnet disruption

- Source: CrowdStrike.
- What changed: On 2026-05-26 at 14:00 UTC, CrowdStrike, Google, and Shadowserver disrupted four Glassworm C2 channels targeting developer ecosystems including OpenVSX/VS Code-like editors, npm/Python packages, and poisoned GitHub repositories.
- Enterprise action: hunt for infected machines beaconing to `164.92.88[.]210`, inspect developer workstations and CI hosts for GlasswormRAT indicators, and review OpenVSX/VS Code extension provenance.
- Confidence: High.

### The Gentlemen ransomware activity

- Sources: Huntress and The DFIR Report.
- What changed:
  - Huntress observed April/May incidents using scheduled tasks, PowerShell, Microsoft Defender tampering, AV exclusions, and clearing of Security/System/Application event logs.
  - The DFIR Report observed EtherRAT and TukTuk C2 leading to The Gentlemen ransomware, with Ethereum/Arweave/SaaS C2, GoTo Resolve, Rclone exfiltration to Wasabi, and domain-wide GPO ransomware deployment.
- Enterprise action:
  - Alert on Defender disablement, broad AV exclusions, event log clearing, suspicious scheduled tasks, unauthorized RMM, Rclone usage, and unexpected outbound access to blockchain/SaaS/tunnel services such as `1rpc.io`, `trycloudflare.com`, Supabase, ClickHouse, Arweave gateways, and GoTo Resolve.
- Confidence: High.

### VX-Underground review

- `vxunderground/MalwareSourceCode` was updated/pushed on 2026-05-30 and repository metadata updated on 2026-06-01.
- No specific new VX-Underground malware report was validated from the website during this run; website and archive access remained limited through static collection.
- Confidence: Medium for repository update metadata; Low for absence of new report.

## Security releases and vendor advisories

| Vendor/source | Item | Status | Recommended action | Confidence |
| --- | --- | --- | --- | --- |
| Microsoft MSRC | May 2026 Security Update Guide page was dynamically loaded and not fully retrievable by static fetch. NVD and prior collection show Microsoft items remain relevant, but no new June 1 MSRC critical item was primary-validated in this run. | Monitoring note | Continue normal MSRC API/update-guide monitoring; prioritize any internally deployed Microsoft products that overlap NVD/KEV. | Medium |
| Cisco PSIRT | CVE-2026-20182 advisory updated May 27 with fixed releases, no workarounds, IoC guidance, and exploitation statement. | Emergency priority | Patch, preserve logs, run Cisco validation checks, and engage TAC if IoCs are present. | High |
| Fortinet PSIRT | FG-IR-26-060 exploited FortiCloud SSO auth bypass; Fortinet PSIRT page also shows May 12 advisories including FG-IR-26-136 critical unauthenticated FortiSandbox authorization issue. | Active advisory | Upgrade affected Fortinet products, review FortiCloud SSO admin logs/accounts, and verify FortiSandbox exposure. | High |
| Palo Alto Networks | CVE-2026-0300 and CVE-2026-0257 marked `ATTACKED`; advisory index also lists multiple May 13 PAN-OS/GlobalProtect issues. | Active advisory | Patch PAN-OS/GlobalProtect and apply exposure-reduction mitigations. | High |
| Android | Android XR June 2026 bulletin published for CVE-2026-0072; patch level 2026-06-01 or later. | Security bulletin | Apply June Android/XR security patches as device vendors release them. | High |
| Apple | iOS 26.5.1 and macOS Tahoe 26.5.1 released 2026-06-01 with no published CVE entries. | Security release list update | Update normally; no CVE-specific emergency signal from Apple page. | High |
| GitHub | Changelog includes 2026-05-22 staged publishing and install-time controls for npm. GitHub Security Advisories on 2026-06-01 include critical Vitest and praisonai-platform advisories. | Supply-chain hardening and GHSA | Review npm publishing controls and patch affected dependencies. | High |
| GitLab | Release page points to patch release RSS; static fetch did not expose a new June 1 security release. | Monitoring note | Continue GitLab patch release RSS monitoring. | Medium |
| OpenCVE / Wazuh CTI | OpenCVE critical search surfaced June 1 Android and Casdoor entries; Wazuh CTI page confirmed vulnerability database availability but did not expose detailed rows through static fetch. | Enrichment | Cross-check critical assets against OpenCVE/Wazuh CTI where APIs/UI are available. | Medium |

## Recommended remediation priorities

1. Patch and hunt Cisco Catalyst SD-WAN CVE-2026-20182 immediately. Preserve logs before upgrade and validate peering/authentication IoCs.
2. Patch or mitigate Palo Alto PAN-OS CVE-2026-0300 and CVE-2026-0257 on any internet/untrusted exposed portals or GlobalProtect services.
3. Apply Oracle WebLogic remediation for CVE-2024-21182 due to new CISA KEV addition; restrict T3/IIOP and confirm exposed WebLogic inventory.
4. Patch cPanel/WHM CVE-2026-41940 and hunt for unauthorized WHM sessions, local admin creation, and `.sorry` ransomware indicators.
5. Patch Drupal Core CVE-2026-9082, prioritizing PostgreSQL-backed public sites and JSON:API/REST/custom query surfaces.
6. Patch LiteLLM CVE-2026-42208 and rotate credentials handled by exposed LiteLLM proxies.
7. Investigate developer and CI/CD exposure to TeamPCP/Mini Shai-Hulud: Nx Console, TanStack, `@antv`, `durabletask`, malicious npm/PyPI/VS Code artifacts, and OIDC trust misuse.
8. Hunt developer endpoints for Glassworm infection beaconing to `164.92.88[.]210` and review OpenVSX/VS Code extension inventories.
9. Hunt for The Gentlemen ransomware TTPs: scheduled task persistence, PowerShell Defender tampering, event log clearing, Rclone, unauthorized RMM, and SaaS/decentralized C2.
10. Triage newly published critical enterprise CVEs: Cline CVE-2026-44211, ROCm AITER CVE-2026-49121, Cloud Foundry UAA CVE-2026-40965, IBM WebSphere CVE-2026-8644/9311/9319, Teamwork Cloud CVE-2026-7858, and Casdoor CVE-2026-9092.

## Source access limitations

- Sploitus homepage did not expose a static "Exploits of the Week" list. Sploitus entries above are reconstructed from indexed exploit pages and direct exploit-page fetches.
- Packet Storm blocked direct automated static access; Packet Storm findings are from indexed Sploitus references.
- ExploitDB landing page did not expose recent rows through static fetch; ExploitDB items are from indexed Sploitus references.
- Microsoft MSRC update guide rendered as a dynamic loading page in static fetch; release details should be confirmed through MSRC API or authenticated/browser workflows where available.
- GitHub PoC repositories were not executed or malware-reviewed.
- Absence of a finding in blocked/dynamic sources should not be treated as proof of absence.
