# Security Intelligence Report - 2026-06-02 14:01 UTC

## Executive Summary

- Reporting window: primary hourly window 2026-06-02 13:00-14:35 UTC, with day-to-date and rolling 24-hour enrichment.
- NVD new CVEs, latest hourly window: 0 total.
- NVD new CVEs, day-to-date: 66 total - 4 critical, 12 high, 31 medium, 15 low, 4 unknown.
- NVD new CVEs, rolling 24 hours: 328 total - 22 critical, 102 high, 118 medium, 50 low, 36 unknown.
- Critical findings requiring review: Cisco SD-WAN CVE-2026-20182, cPanel/WHM CVE-2026-41940, Microsoft Netlogon CVE-2026-41089, PAN-OS CVE-2026-0257, Oracle WebLogic CVE-2024-21182, Linux CIFSwitch CVE-2026-46243, Cloud Foundry UAA CVE-2026-40965, WP Job Portal CVE-2026-42684, Masteriyo LMS PRO CVE-2025-53209, Wirtualna Uczelnia CVE-2026-34906, Kirki CVE-2026-8206, OpenShift CVE-2026-1784, and Apache Kafka/Calcite CVE-2026-41115/CVE-2026-46718.
- Active exploitation findings: Cisco confirms limited exploitation of CVE-2026-20182; CISA KEV confirms exploitation for Oracle WebLogic CVE-2024-21182, PAN-OS CVE-2026-0257, Cisco SD-WAN CVE-2026-20182, Microsoft Defender CVE-2026-41091/CVE-2026-45498, cPanel/WHM CVE-2026-41940, Drupal CVE-2026-9082, Nx CVE-2026-48027, and TanStack CVE-2026-45321. Netlogon active exploitation remains medium confidence because it is not in the fetched CISA KEV feed.
- New malware/campaign intelligence: Miasma/Red Hat Cloud Services npm supply-chain compromise is still the most urgent developer ecosystem campaign; new corroboration reports 32 compromised packages, 96 malicious versions, valid SLSA provenance attestations, and hundreds of affected GitHub repositories. VX-Underground GitHub repositories showed no new pushed malware-source updates after 2026-05-30.
- Important security releases/advisories: Cisco SD-WAN fixed releases and IOC guidance; Android June 2026 security bulletin; Cloud Foundry UAA private-key exposure fix; Apache Kafka/Calcite advisories; GitHub advisories for Vitest and praisonai-platform; ExploitDB June 1 Drupal/WordPress exploit additions.

## Source Coverage and Access Notes

- CISA KEV JSON feed fetched successfully: catalogVersion 2026.06.01, 1608 entries.
- NVD API fetched successfully for 2026-06-02 13:00-14:35 UTC, 2026-06-02 day-to-date, and rolling 24 hours.
- GitHub Advisory Database and repository searches were fetched via authenticated GitHub API.
- GitHub strict repository search for `CVE-2026 PoC exploit created:>=2026-06-02` returned no results; broader pushed-on/after searches found multiple unvalidated exploit indicators.
- ExploitDB CSV fetched directly from the Exploit Database GitLab mirror and sorted by publication date.
- Packet Storm direct web access remains limited by anti-abuse behavior in this environment; Packet Storm-derived references below should be treated as feed/search context only.
- Sploitus homepage fetch timed out or did not expose an "Exploits of the Week" block in static content. The Sploitus Top 10 below is a reconstructed list from prior indexed Sploitus observations plus current exploit-search corroboration, not an official homepage extraction.
- VX-Underground web root was reachable as a directory-style archive page; GitHub repository metadata was checked through the `vxunderground` user repositories.

## Top Vulnerabilities

### 1. CVE-2026-20182 - Cisco Catalyst SD-WAN Controller/Manager authentication bypass

- Severity: Critical, CVSS 10.0; CISA KEV listed.
- Affected software: Cisco Catalyst SD-WAN Controller and Manager across on-prem, Cisco-managed cloud, Cloud-Pro, and government deployments.
- Exploit availability: Public Sploitus-indexed PoC references and Metasploit-module indicators were observed in prior runs; GitHub and exploit references remain active.
- Active exploitation: High confidence. Cisco PSIRT states it became aware of limited exploitation in May 2026.
- Recommended action: Patch to fixed Cisco releases, collect admin-tech files and logs before upgrades, run Cisco `show control connections`/history IOC checks, and open TAC cases for suspected compromise with CVE-2026-20182 in the title.
- Confidence: High.

### 2. CVE-2026-41940 - cPanel & WHM authentication bypass

- Severity: Critical by KEV status, known ransomware use, and internet-facing hosting-control-plane impact.
- Affected software: WebPros cPanel & WHM and WP2.
- Exploit availability: Multiple Sploitus-indexed exploit indicators, Metasploit-module references, and recently pushed GitHub PoC claims. `Defacto-ridgepole254/CVE-2026-41940-Exploit-PoC` was pushed again at 2026-06-02 13:39 UTC.
- Active exploitation: High confidence. CISA KEV lists known ransomware campaign use.
- Recommended action: Patch all supported branches, inspect WHM/cpsrvd logs for CRLF/session-cache abuse, hunt for `.sorry` ransomware indicators, and rotate credentials for compromised panels.
- Confidence: High for exploitation and patch priority, Low for individual GitHub repository trustworthiness.

### 3. CVE-2026-41089 - Microsoft Windows Netlogon remote code execution

- Severity: Critical, CVSS 9.8 in NVD/MSRC.
- Affected software: Windows Server domain controllers, Windows Server 2012 through 2025 version ranges listed by NVD.
- Exploit availability: GitHub PoC indicators remain present, including `0xABCD01/CVE-2026-41089` and `0xBlackash/CVE-2026-41089`; functionality not validated.
- Active exploitation: Medium confidence. Secondary reporting cites active exploitation, but the fetched CISA KEV catalog did not list this CVE.
- Recommended action: Confirm May 2026 Microsoft patches are applied to all domain controllers, prioritize high-value AD sites, and monitor Netlogon/NRPC anomalies.
- Confidence: Medium.

### 4. CVE-2026-0257 - Palo Alto Networks PAN-OS authentication bypass

- Severity: Critical by prioritization due to KEV status, VPN authentication bypass, and enterprise perimeter impact.
- Affected software: PAN-OS GlobalProtect configurations covered by Palo Alto advisory.
- Exploit availability: Public exploit/attacked status indicators exist in previous runs; no new validated repository was found this hour.
- Active exploitation: High confidence due to CISA KEV listing.
- Recommended action: Patch or apply Palo Alto mitigations, verify GlobalProtect authentication override certificate configuration, and review VPN connection anomalies.
- Confidence: High.

### 5. CVE-2024-21182 - Oracle WebLogic Server unspecified vulnerability

- Severity: Critical by prioritization due to CISA KEV addition and unauthenticated network access via T3/IIOP.
- Affected software: Oracle WebLogic Server.
- Exploit availability: No new PoC was validated in this run.
- Active exploitation: High confidence due to CISA KEV listing on 2026-06-01.
- Recommended action: Apply Oracle CPU guidance immediately; the CISA KEV due date is 2026-06-04.
- Confidence: High.

### 6. CVE-2026-46243 - Linux CIFSwitch local privilege escalation

- Severity: High, CVSS 7.8 in NVD, but prioritized as Critical/High operationally where local user or workload execution is common.
- Affected software: Linux kernel CIFS SPNEGO handling plus cifs-utils default request-key/upcall behavior on affected distributions.
- Exploit availability: Public PoC confirmed at `manizada/CIFSwitch`; oss-security disclosure confirms the PoC is intended to validate mitigations.
- Active exploitation: Not observed in primary sources during this run.
- Recommended action: Apply kernel fixes containing commit `3da1fdf4efbc` or distribution backports, remove/block CIFS/cifs-utils where unused, override the default `cifs.spnego` request-key rule if Kerberos CIFS is not required, and disable unprivileged user namespaces where feasible.
- Confidence: High for disclosure and PoC availability, Low for exploitation.

### 7. CVE-2026-40965 - Cloud Foundry UAA EC private key exposure

- Severity: Critical, CVSS 10.0.
- Affected software: Cloud Foundry UAA v76.12.0 through v78.12.0 and CF Deployment v30.0.0 through v56.0.0 when EC keys are used for JWT signing.
- Exploit availability: Public advisory details the exposed `/token_keys` behavior; exploit code was not required to understand the exposure.
- Active exploitation: Not observed.
- Recommended action: Upgrade UAA to v78.13.0 or later and cf-deployment to v56.1.0 or later, rotate exposed EC signing keys, and invalidate affected tokens.
- Confidence: High.

### 8. CVE-2026-42684 - Ahmad WP Job Portal blind SQL injection

- Severity: Critical, CVSS 9.3.
- Affected software: WordPress WP Job Portal through 2.5.1.
- Exploit availability: No validated PoC was found this hour.
- Active exploitation: Not observed.
- Recommended action: Inventory WordPress sites using WP Job Portal, disable or patch when a fixed release is available, and monitor for SQL injection probes.
- Confidence: High for disclosure, Low for exploitation.

### 9. CVE-2025-53209 - Masteriyo LMS PRO privilege escalation

- Severity: Critical, CVSS 9.8.
- Affected software: Masteriyo LMS PRO through 2.20.0.
- Exploit availability: No public PoC validated during this run.
- Active exploitation: Not observed.
- Recommended action: Disable or update the plugin, restrict administrator creation paths, and review recent WordPress user-role changes.
- Confidence: High for disclosure, Low for exploitation.

### 10. CVE-2026-34906 - Wirtualna Uczelnia SSTI remote code execution

- Severity: Critical, CVSS 9.3.
- Affected software: Wirtualna Uczelnia, endpoint `redirectToUrl`, parameter `redirectUrlParameter`.
- Exploit availability: No public PoC validated during this run.
- Active exploitation: Not observed.
- Recommended action: Apply vendor/CERT.PL remediation, restrict access to affected endpoints until patched, and review application logs for template-injection payloads.
- Confidence: High for disclosure, Low for exploitation.

### 11. CVE-2026-8206 - Kirki WordPress privilege escalation/account takeover

- Severity: Critical, CVSS 9.8.
- Affected software: Kirki plugin versions 6.0.0 through 6.0.6.
- Exploit availability: Recently created GitHub repository `Jenderal92/CVE-2026-8206` claims a mass exploitation tool; not validated and should be treated as potentially malicious.
- Active exploitation: Not confirmed by primary sources.
- Recommended action: Update Kirki, audit password-reset and administrator-account events, and block suspicious requests to the affected forgot-password handler.
- Confidence: High for disclosure, Low for GitHub exploit validity.

### 12. CVE-2026-1784 - Red Hat OpenShift Route HAProxy header injection

- Severity: High, CVSS 8.8.
- Affected software: OpenShift Route resources using HAProxy routing behavior.
- Exploit availability: Public exploit was not validated; NVD links Red Hat CVE and Bugzilla references.
- Active exploitation: Not observed.
- Recommended action: Apply Red Hat/OpenShift fixes, review Route `spec.path` usage for untrusted input, and monitor HAProxy configuration changes for unexpected header manipulation.
- Confidence: High for disclosure, Low for exploitation.

### 13. CVE-2026-41115 and CVE-2026-46718 - Apache Kafka and Apache Calcite advisories

- Severity: Unknown in NVD at query time, but enterprise impact warrants tracking.
- Affected software: Apache Kafka authorization handling for CONSUMER_GROUP_DESCRIBE; Apache Calcite unsafe reflection before 1.42.
- Exploit availability: No public exploit validated in this run.
- Active exploitation: Not observed.
- Recommended action: Monitor Apache advisory pages, upgrade Calcite to 1.42 where used, and assess Kafka ACL assumptions around consumer group describe/read access.
- Confidence: Medium pending full scoring.

## Exploits Released

### Sploitus Top 10 - reconstructed from indexed result pages

Static Sploitus homepage access did not expose the official "Exploits of the Week" list in this environment. The following captures the top exploit indicators carried forward from indexed Sploitus pages and current corroborating searches.

| Rank | CVE | Affected software | Exploit type | Exploit maturity | Public PoC | Weaponization potential |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | CVE-2026-20182 | Cisco Catalyst SD-WAN Controller/Manager | Unauthenticated authentication bypass to privileged SD-WAN control-plane account | PoC/exploit framework indicator | Yes | Critical - network fabric control |
| 2 | CVE-2026-20182 | Cisco Catalyst SD-WAN Controller/Manager | NETCONF/SSH control-plane manipulation | Weaponized description | Yes | Critical |
| 3 | CVE-2026-20182 | Cisco Catalyst SD-WAN Controller/Manager | Metasploit auxiliary module indicator | Framework module indicator | Yes | Critical |
| 4 | CVE-2026-41940 | cPanel & WHM | CRLF/session-cache authentication bypass | Metasploit module indicator | Yes | Critical - root hosting panel compromise |
| 5 | CVE-2026-41940 | cPanel & WHM | Ransomware IOC pack and exploit analysis | Operational campaign analysis | Yes | Critical - known ransomware use |
| 6 | CVE-2026-41940 | cPanel & WHM | Bulk scanner/post-exploitation toolkit | Weaponized PoC indicator | Yes | Critical |
| 7 | CVE-2026-46243 | Linux kernel/cifs-utils | Local privilege escalation through forged cifs.spnego upcall | Working public PoC | Yes | High - root from local code execution |
| 8 | CVE-2026-31431 | Linux kernel Copy Fail | Local privilege escalation/arbitrary page cache write | Recently pushed GitHub PoC claims | Yes | High |
| 9 | CVE-2026-25643 | Frigate NVR | Remote code execution claim | Recently pushed GitHub PoC indicator | Unvalidated | High if exposed |
| 10 | CVE-2026-21858 | n8n | Content-type confusion to file read/session forgery/RCE | Reconstruction/exploit code indicator | Yes | High to Critical |

### ExploitDB additions

Direct ExploitDB CSV fetch showed the latest entries as:

- EDB-ID 52608, 2026-06-01: Drupal Core 10.5.5 error-based SQL injection, CVE-2026-9082.
- EDB-ID 52607, 2026-06-01: WordPress OrderConvo 14 path traversal, CVE-2025-10162.
- EDB-ID 52606, 2026-05-30: Notepad++ 8.9.6 arbitrary code execution.
- No 2026-06-02-dated ExploitDB row was present in the CSV fetched during this run.

### New or recently pushed GitHub PoC indicators

Treat all repositories below as unvalidated and potentially malicious until reviewed in a sandbox.

- `yoyosh/DarkReplica` - CVE-2026-23631 Redis exploit claim; pushed 2026-06-02 13:59 UTC.
- `Ez4rd1x1/CVE-2026-8181` - newly created/pushed CVE repository; description absent.
- `Defacto-ridgepole254/CVE-2026-41940-Exploit-PoC` - cPanel/WHM auth bypass PoC claim; pushed 2026-06-02 13:39 UTC.
- `Dullpurple-sloop726/CVE-2026-31431-Linux-Copy-Fail` and `Liverwortenuresis371/copyfail-rs` - Linux Copy Fail LPE exploit/detector claims; pushed after 13:37 UTC.
- `MrForkBomb/CIFSwitch-Checker-CVE-2026-46243` - CIFSwitch exposure checker; created 2026-06-02 and pushed 13:03 UTC.
- `manizada/CIFSwitch` - public CIFSwitch PoC from the researcher; created 2026-05-28, pushed 2026-06-01 16:33 UTC.
- `DyniePro/CVE-2026-25643` - Frigate NVR RCE claim; pushed 2026-06-02 13:00 UTC.
- Strict search for repositories created on 2026-06-02 matching `CVE-2026 PoC exploit` returned an empty result set; the above are from broader pushed-on/after searches.

## Malware Intelligence

### Red Hat Cloud Services npm package compromise / Miasma supply-chain worm

- Status: Active supply-chain incident in multiple security-research reports; Red Hat reportedly removed affected packages and stated customer/partner production systems were not impacted.
- Malware behavior: Mini Shai-Hulud-style worm/credential harvester targeting GitHub Actions tokens, AWS/Azure/GCP credentials, SSH keys, npm/PyPI tokens, Docker credentials, Kubernetes configs, Vault tokens, GPG keys, and `.env` files.
- Scale: Current corroborating reports describe 32 compromised `@redhat-cloud-services` packages, 96 malicious versions, approximately 80,000-117,000 weekly downloads depending on source, and hundreds of affected GitHub repositories.
- Supply-chain note: Reports state malicious releases were published through GitHub Actions workflows with `id-token: write`, resulting in valid SLSA provenance attestations for tainted packages.
- Recommended action: Identify installations of `@redhat-cloud-services/*` packages since 2026-05-29, reinstall with scripts disabled where possible, rotate CI/CD/cloud/npm/GitHub credentials, audit GitHub Actions logs for unauthorized OIDC token requests, and inspect package-lock/npm cache artifacts.
- Confidence: Medium to High. Multiple sources agree on the package compromise mechanics; continue monitoring primary Red Hat/npm statements for final package lists.

### cPanel "Sorry" ransomware linked to CVE-2026-41940

- Status: CISA KEV marks known ransomware use for CVE-2026-41940.
- Malware behavior: Prior Sploitus-indexed analysis described a Linux Go encryptor using ChaCha20 and RSA-2048, `.sorry` extension, and Tox negotiation.
- Recommended action: Hunt for `.sorry` extensions, ransom notes named `README.md` in unusual web-hosting directories, suspicious WHM session files, and outbound Tox-related traffic.
- Confidence: High for KEV ransomware association, Medium for specific campaign details.

### VX-Underground

- GitHub activity: `vxunderground/MalwareSourceCode` latest pushed timestamp remains 2026-05-30 07:11 UTC; repository metadata updated at 2026-06-02 13:53 UTC but no new push was observed.
- Latest remembered item: `Python/Stealer.Python.GMBA.Manipulator.7z` added to MalwareSourceCode on 2026-05-30.
- Web archive check: VX-Underground root exposed archive categories, but no current malware report page was identified during this run.
- Confidence: Medium. GitHub metadata was available; website feed-style enumeration remains limited.

## Security Releases and Vendor Advisories

- Microsoft: Netlogon CVE-2026-41089 remains a critical domain-controller patching priority from May 2026 updates; Defender CVE-2026-41091/CVE-2026-45498 remain in CISA KEV with 2026-06-03 due date. SharePoint CVE-2026-47294 was present in the rolling 24-hour NVD window as high severity.
- Cisco: SD-WAN CVE-2026-20182 advisory confirms fixed releases, no workarounds, log/admin-tech preservation guidance, IOC checks, and limited exploitation. Patch before relying on upgrades as remediation if compromise is suspected.
- Fortinet: No new June 2 Fortinet PSIRT release was identified in this run; prior FortiClient EMS and FortiAuthenticator items remain watchlist items.
- VMware/Broadcom/Cloud Foundry: Cloud Foundry UAA CVE-2026-40965 has fixed UAA v78.13.0 and cf-deployment v56.1.0 guidance; Cloud Foundry cf-auth-proxy CVE-2026-40964 remains high severity.
- GitHub: Latest advisories continue to include critical Vitest CVE-2026-47428/CVE-2026-47429 and praisonai-platform authorization/JWT issues fixed in 0.1.4.
- GitLab: No new GitLab advisory was identified during this hour.
- Google/Android: Android June 2026 bulletin was published with 2026-06-01 and 2026-06-05 patch levels; most severe issue is a critical Framework remote elevation-of-privilege issue with no user interaction required, and multiple System/closed-source component criticals.
- Apache: Kafka CVE-2026-41115 and Calcite CVE-2026-46718 appeared in the day-to-date NVD window; Calcite users should upgrade to 1.42.
- WordPress ecosystem: Patchstack/Wordfence disclosures continue to dominate June 2 CVE volume, including WP Job Portal CVE-2026-42684, Masteriyo LMS PRO CVE-2025-53209, Kirki CVE-2026-8206, Thim Core CVE-2025-53345, and multiple high-severity local-file-inclusion/object-injection issues.

## Recommended Actions - Ranked

1. Emergency patch and hunt Cisco Catalyst SD-WAN Controller/Manager for CVE-2026-20182; preserve logs/admin-tech data before upgrades and validate control connections.
2. Patch and hunt cPanel/WHM CVE-2026-41940, with ransomware triage for `.sorry` indicators and WHM session-file tampering.
3. Patch PAN-OS CVE-2026-0257 and Oracle WebLogic CVE-2024-21182 per KEV deadlines; verify perimeter exposure and authentication bypass conditions.
4. Validate Microsoft domain-controller patch posture for Netlogon CVE-2026-41089 and Defender engine/platform versions for CVE-2026-41091/CVE-2026-45498.
5. Treat CIFSwitch CVE-2026-46243 as urgent on multi-user Linux hosts, CI runners, developer workstations, and container hosts where untrusted local code can execute; patch kernel or apply mitigations.
6. Rotate keys and upgrade Cloud Foundry UAA deployments affected by CVE-2026-40965, especially deployments using EC JWT signing keys.
7. Respond to Miasma/Red Hat npm supply-chain exposure by identifying affected package versions, rotating credentials, and auditing GitHub Actions/OIDC publishing paths.
8. Address 2026-06-02 WordPress criticals: WP Job Portal CVE-2026-42684, Masteriyo LMS PRO CVE-2025-53209, Kirki CVE-2026-8206, and related high-severity Patchstack items.
9. Apply OpenShift, Apache, Android, Qualcomm, and IBM updates based on asset exposure; prioritize internet-facing or privileged-service contexts.
10. Quarantine and analyze any downloaded GitHub PoC repositories before execution; do not run recent CVE PoCs on production or analyst workstations.

## Unified Vulnerability Records

```json
[
  {
    "cve": "CVE-2026-20182",
    "cvss": "10.0",
    "vendor": "Cisco",
    "product": "Catalyst SD-WAN Controller and Manager",
    "affected_versions": "Multiple Catalyst SD-WAN releases before Cisco fixed releases including 20.9.9.1, 20.12.7.1, 20.15.5.2, 20.18.2.2, and 26.1.1.1 depending on branch",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://sec.cloudapps.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-sdwan-rpa2-v69WY2SW"
    ],
    "patch_available": true,
    "sources": [
      "Cisco PSIRT",
      "CISA KEV",
      "NVD",
      "GitHub/Sploitus indexed exploit indicators"
    ]
  },
  {
    "cve": "CVE-2026-41940",
    "cvss": "Critical",
    "vendor": "WebPros",
    "product": "cPanel & WHM and WP2",
    "affected_versions": "Affected versions covered by WebPros April 2026 cPanel/WHM security update",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://support.cpanel.net/hc/en-us/articles/40073787579671-cPanel-WHM-Security-Update-04-28-2026",
      "https://github.com/Defacto-ridgepole254/CVE-2026-41940-Exploit-PoC"
    ],
    "patch_available": true,
    "sources": [
      "CISA KEV",
      "NVD",
      "Exploit search",
      "GitHub repository search"
    ]
  },
  {
    "cve": "CVE-2026-41089",
    "cvss": "9.8",
    "vendor": "Microsoft",
    "product": "Windows Netlogon",
    "affected_versions": "Windows Server domain controller versions listed by MSRC/NVD",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/0xABCD01/CVE-2026-41089"
    ],
    "patch_available": true,
    "sources": [
      "MSRC",
      "NVD",
      "GitHub repository search",
      "Secondary exploitation reporting"
    ]
  },
  {
    "cve": "CVE-2026-0257",
    "cvss": "Critical",
    "vendor": "Palo Alto Networks",
    "product": "PAN-OS GlobalProtect",
    "affected_versions": "PAN-OS versions covered by Palo Alto advisory",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://security.paloaltonetworks.com/CVE-2026-0257"
    ],
    "patch_available": true,
    "sources": [
      "CISA KEV",
      "Palo Alto advisory",
      "NVD",
      "Exploit search"
    ]
  },
  {
    "cve": "CVE-2024-21182",
    "cvss": "Critical",
    "vendor": "Oracle",
    "product": "WebLogic Server",
    "affected_versions": "Oracle WebLogic Server versions covered by Oracle CPU July 2024 and CISA KEV entry",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "CISA KEV",
      "Oracle CPU",
      "NVD"
    ]
  },
  {
    "cve": "CVE-2026-46243",
    "cvss": "7.8",
    "vendor": "Linux",
    "product": "Kernel CIFS and cifs-utils upcall path",
    "affected_versions": "Affected Linux distributions where cifs-utils/default cifs.spnego request-key rule and unprivileged namespaces allow exploitation; fixed by kernel backports containing commit 3da1fdf4efbc",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/manizada/CIFSwitch",
      "https://www.openwall.com/lists/oss-security/2026/06/01/6"
    ],
    "patch_available": true,
    "sources": [
      "NVD",
      "oss-security",
      "GitHub PoC",
      "Linux kernel stable commits"
    ]
  },
  {
    "cve": "CVE-2026-40965",
    "cvss": "10.0",
    "vendor": "Cloud Foundry Foundation",
    "product": "UAA",
    "affected_versions": "uaa_release v76.12.0 through v78.12.0 and CF Deployment v30.0.0 through v56.0.0 with EC JWT signing keys",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://www.cloudfoundry.org/blog/cve-2026-40965-uaa-ec-private-key-disclosure/"
    ],
    "patch_available": true,
    "sources": [
      "Cloud Foundry advisory",
      "NVD"
    ]
  },
  {
    "cve": "CVE-2026-42684",
    "cvss": "9.3",
    "vendor": "Ahmad",
    "product": "WP Job Portal",
    "affected_versions": "WordPress WP Job Portal through 2.5.1",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": false,
    "sources": [
      "NVD",
      "Patchstack"
    ]
  },
  {
    "cve": "CVE-2025-53209",
    "cvss": "9.8",
    "vendor": "Themeisle",
    "product": "Masteriyo LMS PRO",
    "affected_versions": "Through 2.20.0",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": false,
    "sources": [
      "NVD",
      "Patchstack"
    ]
  },
  {
    "cve": "CVE-2026-34906",
    "cvss": "9.3",
    "vendor": "Simple",
    "product": "Wirtualna Uczelnia",
    "affected_versions": "Endpoint redirectToUrl parameter redirectUrlParameter as described by CERT.PL",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "NVD",
      "CERT.PL"
    ]
  },
  {
    "cve": "CVE-2026-8206",
    "cvss": "9.8",
    "vendor": "Kirki",
    "product": "Kirki WordPress plugin",
    "affected_versions": "6.0.0 through 6.0.6",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/Jenderal92/CVE-2026-8206"
    ],
    "patch_available": true,
    "sources": [
      "NVD",
      "Wordfence",
      "GitHub repository search"
    ]
  },
  {
    "cve": "CVE-2026-1784",
    "cvss": "8.8",
    "vendor": "Red Hat",
    "product": "OpenShift Route",
    "affected_versions": "Affected OpenShift Route resources as described by Red Hat CVE and Bugzilla",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "NVD",
      "Red Hat"
    ]
  },
  {
    "cve": "CVE-2026-41115",
    "cvss": "Unknown",
    "vendor": "Apache",
    "product": "Kafka",
    "affected_versions": "Kafka versions affected by CONSUMER_GROUP_DESCRIBE authorization validation issue",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "NVD",
      "Apache"
    ]
  },
  {
    "cve": "CVE-2026-46718",
    "cvss": "Unknown",
    "vendor": "Apache",
    "product": "Calcite",
    "affected_versions": "Apache Calcite 1.5.0 before 1.42",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "NVD",
      "Apache oss-security"
    ]
  },
  {
    "cve": "CVE-2026-47429",
    "cvss": "Critical",
    "vendor": "Vitest",
    "product": "Vitest UI server",
    "affected_versions": "vitest before 4.1.0",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/advisories/GHSA-5xrq-8626-4rwp"
    ],
    "patch_available": true,
    "sources": [
      "GitHub Advisory Database",
      "NVD"
    ]
  }
]
```
