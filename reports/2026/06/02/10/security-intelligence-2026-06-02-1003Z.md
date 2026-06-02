# Security Intelligence Report - 2026-06-02 10:03 UTC

Collection window: 2026-06-02 09:00-10:35 UTC, with rolling 24-hour enrichment from 2026-06-01 10:35 UTC.

Repository: `dfalt0/Test-cursor-security-automation`

## Executive Summary

- NVD publications: 18 CVEs newly published in the 09:00-10:35 UTC hour: 2 high and 16 medium. Day-to-date NVD total is 43 CVEs: 1 critical, 2 high, 33 medium, 5 low, and 2 unknown. Rolling 24-hour NVD total is 327 CVEs: 18 critical, 106 high, 138 medium, 31 low, and 34 unknown.
- Critical findings requiring immediate review: Cisco Catalyst SD-WAN CVE-2026-20182, Microsoft Netlogon CVE-2026-41089, Palo Alto PAN-OS CVE-2026-0257, Fortinet FortiClient EMS CVE-2026-35616, Drupal Core CVE-2026-9082, cPanel/WHM CVE-2026-41940, LiteSpeed cPanel Plugin CVE-2026-48172, Cloud Foundry UAA CVE-2026-40965, Kirki WordPress CVE-2026-8206, Oracle WebLogic CVE-2024-21182, Ghost CMS CVE-2026-26980, and the Nx/TanStack/Miasma supply-chain cluster.
- Newly published high-severity CVEs this hour: Red Hat OpenShift Route CVE-2026-1784, an HAProxy configuration injection issue, and Prefect CVE-2026-3514, an authentication bypass in API health/ready path exemption logic.
- Active exploitation findings: Cisco SD-WAN, PAN-OS GlobalProtect, FortiClient EMS, Drupal Core, cPanel/WHM, LiteSpeed cPanel Plugin, Microsoft Netlogon, Ghost CMS, and Microsoft Defender CVE-2026-41091/CVE-2026-45498 are reported or cataloged as exploited. Confidence varies by source; see individual records.
- New malware and campaign intelligence: FortiClient EMS exploitation continues to be tied to EKZ Infostealer delivery. The `@redhat-cloud-services` Miasma/Mini Shai-Hulud npm compromise remains a high-priority supply-chain incident. Ghost CMS exploitation is feeding ClickFix malware delivery through compromised legitimate sites. VX-Underground GitHub activity shows no new MalwareSourceCode commit after 2026-05-30, but the repository metadata was updated during this hour.
- Important vendor releases/advisories: LiteSpeed WHM Plugin 5.3.1.0 / cPanel plugin 2.4.7, Mender Server 4.1.1 / 4.0.2, Prefect fix commit `e21617125335025b4b27e7d6f0ca028e8e8f3b79`, Cisco fixed SD-WAN releases, Palo Alto fixed PAN-OS/Prisma Access releases, Fortinet FortiClient EMS 7.4.7/hotfix guidance, Drupal fixed 10.4.10/10.5.10/10.6.9/11.1.10/11.2.12/11.3.10, Cloud Foundry UAA v78.13.0/cf-deployment v56.1.0, and Kirki 6.0.7.

## Source Coverage and Caveats

- CISA KEV feed: checked JSON catalog version `2026.06.01`, released `2026-06-01T16:59:32.7272Z`, with 1608 total entries. Latest additions include Oracle WebLogic CVE-2024-21182, PAN-OS CVE-2026-0257, Nx/TanStack supply-chain CVEs, LiteSpeed cPanel Plugin CVE-2026-48172, and Drupal CVE-2026-9082.
- NVD API: queried hourly, day-to-date, rolling 24-hour, and per-CVE detail windows.
- Sploitus: homepage and query pages still do not expose an official "Exploits of the Week" block to non-browser fetches. The "Sploitus Top 10" below is reconstructed from indexed Sploitus result pages, not an official homepage extraction.
- ExploitDB: parsed the official exploitdb GitLab CSV and sorted by publication date. Latest entries listed below are marked `verified=0` by ExploitDB.
- Packet Storm: no Packet Storm additions are asserted in this report because prior direct fetches returned anti-abuse blocking and no new primary Packet Storm data was collected in this run.
- GitHub: queried global advisories and repository search. No reviewed GitHub advisories were published after 09:00 UTC in the query results. GitHub PoC repositories are treated as indicators only; functionality and safety are not assumed.
- VX-Underground: checked GitHub repositories through the authenticated GitHub API. Latest `vxunderground/MalwareSourceCode` commit remains `1623926` from 2026-05-30 adding `Python/Stealer.Python.GMBA.Manipulator.7z`.
- Red Hat: the public Red Hat CVE page for CVE-2026-1784 was reachable but sparse via fetch, and Bugzilla 2436075 required authentication. NVD and the public Red Hat CVE URL are used for the OpenShift record.

## Top Vulnerabilities

| Priority | CVE / Issue | Severity | Affected software | Exploit availability | Active exploitation | Recommended action | Confidence |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Critical | CVE-2026-20182 | CVSS 10.0 | Cisco Catalyst SD-WAN Controller/Manager | Multiple Sploitus PoCs and Metasploit/Rapid7 references | Yes; Cisco PSIRT/Talos/Rapid7/CISA KEV reporting | Upgrade to Cisco fixed releases, preserve admin-tech/log artifacts before upgrade, review control-connection and auth logs | High |
| Critical | CVE-2026-41089 | CVSS 9.8 | Microsoft Windows Server domain controllers / Netlogon | Public GitHub indicator exists; functionality unvalidated | Reported active by Belgium CCB and secondary outlets; not in CISA KEV at collection time | Patch all domain controllers with May 2026 updates, restrict Netlogon/RPC exposure, hunt anomalous LSASS/Netlogon activity | Medium |
| Critical | CVE-2026-0257 | CVSS-B 7.8 but enterprise-critical | Palo Alto Networks PAN-OS GlobalProtect / Prisma Access | Public Rapid7 testing reference in reporting; no new Sploitus hit this hour | Yes; Palo Alto lists exploit maturity `ATTACKED`; CISA KEV | Upgrade to listed PAN-OS/Prisma Access fixed versions; disable or reconfigure authentication override cookies where needed | High |
| Critical | CVE-2026-35616 | CVSS 9.1/9.8 depending source | Fortinet FortiClient EMS 7.4.5-7.4.6 | Exploited in the wild; no public PoC required for risk | Yes; Arctic Wolf reports EKZ Infostealer delivery through EMS workflows | Apply Fortinet hotfix/upgrade to 7.4.7; restrict EMS management API; investigate EMS policy/script changes and FortiClient-launched PowerShell | High |
| Critical | CVE-2026-9082 | Drupal highly critical; NVD 6.5 | Drupal Core PostgreSQL-backed sites | Multiple Sploitus PoCs/scanners; ExploitDB 52608 | Yes; Drupal advisory updated for in-the-wild attempts; CISA KEV | Upgrade Drupal immediately; prioritize PostgreSQL-backed internet-facing sites; audit DB and role-change logs | High |
| Critical | CVE-2026-41940 | CVSS 9.8 | WebPros cPanel & WHM / WP2 | Sploitus Metasploit, ExploitDB, and GitHub indicators | CISA KEV with known ransomware campaign use and "Sorry" ransomware reporting | Apply cPanel/WP2 updates, review WHM sessions and webshell/backdoor indicators, rotate credentials after compromise checks | High |
| Critical | CVE-2026-48172 | CVSS 10.0 v4 / 9.8 v3 | LiteSpeed User-End cPanel Plugin 2.3-2.4.4 | Sploitus auditor indicator; exploit path publicly described | Yes; LiteSpeed says actively exploited; CISA KEV | Upgrade to LiteSpeed WHM Plugin 5.3.1.0 / cPanel plugin 2.4.7+, or uninstall user-end plugin; grep logs for `cpanel_jsonapi_func=redisAble` and investigate hits | High |
| Critical | CVE-2026-40965 | CVSS 10.0 | Cloud Foundry UAA / cf-deployment using EC JWT keys | No public PoC confirmed; exploit path is direct via public `/token_keys` | No exploitation observed in checked sources | Upgrade UAA to v78.13.0+ or cf-deployment v56.1.0+; rotate EC JWT signing keys and invalidate tokens | High |
| High | CVE-2026-3514 | CVSS 7.5 | Prefect 3.6.19 API auth middleware | Public fix commit and technical details; no Sploitus hit | No active exploitation confirmed | Upgrade to a fixed Prefect build containing commit `e21617125335025b4b27e7d6f0ca028e8e8f3b79`; verify auth is enabled and endpoints ending in health/ready require auth unless exact probe paths | High |
| High | CVE-2026-1784 | CVSS 8.8 | Red Hat OpenShift Route / HAProxy router configuration | No public PoC found this hour | No active exploitation confirmed | Track Red Hat remediation, restrict who can create/modify Route resources, audit suspicious route `spec.path` values and HAProxy config changes | Medium |
| High | CVE-2026-49009 | NVD 3.1 but vendor describes severe hosted multi-tenant impact | Northern.tech Mender Server 4.1.0, 4.0.1 and below | GitHub PoC describes authenticated path traversal to worker RCE; functionality unvalidated | No active exploitation confirmed | Upgrade Mender Server to 4.1.1/4.0.2+; review artifact-generation API access and enforce signed artifacts | Medium |
| Critical | CVE-2026-26980 | CVSS 9.4 in public reporting | Ghost CMS 3.24.0 through 6.19.0 | Public exploitation campaign details | Yes; 700+ sites reported hijacked for ClickFix malware delivery | Upgrade Ghost to 6.19.1+; rotate Admin API keys, Content API keys, passwords, and sessions; remove injected JavaScript loaders | Medium |

## Exploits Released

### Reconstructed Sploitus Top 10

These are indexed Sploitus exploit pages observed through search results during the run. This is not confirmed to be Sploitus' official "Exploits of the Week" block.

| Rank | Sploitus entry | CVE(s) | Affected software | Exploit type | Maturity / weaponization potential |
| --- | --- | --- | --- | --- | --- |
| 1 | `13DF22F3-E9C6-58EE-B458-EB585C4D715D` | CVE-2026-20182 | Cisco Catalyst SD-WAN Controller/Manager | Remote auth bypass, SSH key injection / NETCONF access | Weaponization potential very high; aligns with Rapid7/Cisco/Talos exploitation narrative |
| 2 | `MSF:AUXILIARY-ADMIN-NETWORKING-CISCO_SDWAN_VHUB_AUTH_BYPASS-` | CVE-2026-20182 | Cisco Catalyst SD-WAN Controller/Manager | Metasploit auxiliary module | Mature framework indicator; use only in authorized validation environments |
| 3 | `458CE696-FE39-500F-9131-2E24B1BC2E12` | CVE-2026-9082 | Drupal Core on PostgreSQL | Error-based SQL injection PoC | Public PoC; active exploitation confirmed by vendor/KEV |
| 4 | `1774D6F8-2B0F-5C66-A7AB-BE7B8E7A0B85` | CVE-2026-9082 | Drupal Core on PostgreSQL | Mass scanner and exploitation tool | High weaponization potential due scanner/extraction features |
| 5 | `MSF:EXPLOIT-MULTI-HTTP-CPANEL_WHM_AUTH_BYPASS_RCE-` | CVE-2026-41940 | cPanel/WHM | Remote auth bypass/RCE module | High maturity if Metasploit module is accurate; ransomware relevance via KEV |
| 6 | `5594483C-6BE4-5815-989A-419B36AC3894` | CVE-2026-41940 | cPanel/WHM | IOC/YARA/forensic package for Sorry ransomware campaign | Defensive package, but confirms operationalized campaign details |
| 7 | `EDB-ID:52574` | CVE-2026-41940 | cPanel/WHM | CRLF injection auth bypass exploit | Public exploit; high operational risk |
| 8 | `36AAEAF3-4B32-5BE1-817C-7C65B5B446FE` | CVE-2026-48172 | LiteSpeed User-End cPanel Plugin | Local auditor/checker | Primarily defensive, but publicizes exploit conditions and detection logic |
| 9 | `E416E089-6938-57DA-B17F-340BD5B389C3` | CVE-2026-31431 | Linux kernel Copy Fail | Local privilege escalation PoC | High local/container escape risk where vulnerable kernels remain deployed |
| 10 | `A6500AE2-6D3D-5689-B049-BFCE1470ED76` | CVE-2026-31431 | Kubernetes nodes sharing vulnerable Linux kernel/page cache paths | Container escape PoC | High weaponization potential in shared-cluster environments |

### ExploitDB Additions

Latest ExploitDB CSV entries at collection time:

| EDB ID | Date | Description | CVE(s) | Type/platform | Verified |
| --- | --- | --- | --- | --- | --- |
| 52608 | 2026-06-01 | Drupal Core 10.5.5 - Error-Based SQL Injection | CVE-2026-9082 | webapps/php | 0 |
| 52607 | 2026-06-01 | WordPress OrderConvo 14 - Path Traversal | CVE-2025-10162 | webapps/multiple | 0 |
| 52606 | 2026-05-30 | Notepad++ 8.9.6 - Arbitrary Code Execution | CVE-2026-48778 | remote/windows | 0 |
| 52605 | 2026-05-30 | YAMCS yamcs-core 5.12.7 - No Rate Limiting | CVE-2026-44596 | webapps/multiple | 0 |
| 52604 | 2026-05-30 | YAMCS yamcs-core 5.12.7 - User Enumeration | CVE-2026-44595 | webapps/multiple | 0 |
| 52603 | 2026-05-30 | YAMCS yamcs-core 5.12.7 - LDAP Injection | CVE-2026-42568 | webapps/multiple | 0 |
| 52601 | 2026-05-29 | Microsoft - NTLMv2 Hash Capture | CVE-2026-32202 | remote/windows | 0 |
| 52600 | 2026-05-29 | MikroORM 7.0.13 - SQL Injection | CVE-2026-44680 | webapps/multiple | 0 |
| 52598 | 2026-05-29 | Prodigy Commerce 3.3.0 - Local File Inclusion | CVE-2026-0926 | webapps/multiple | 0 |
| 52597 | 2026-05-29 | Langflow 1.3.0 - Remote Code Execution | CVE-2026-0770 | webapps/multiple | 0 |

### New GitHub PoC / Exploit Indicators

- No repositories matched `CVE-2026 exploit PoC created:>=2026-06-02` in the direct GitHub search query.
- Repositories pushed after 09:00 UTC that require safe validation include:
  - `Dullpurple-sloop726/CVE-2026-31431-Linux-Copy-Fail`, a Rust Linux Copy Fail LPE indicator, pushed 2026-06-02T09:32:18Z.
  - `Defacto-ridgepole254/CVE-2026-41940-Exploit-PoC`, a cPanel/WHM auth bypass PoC indicator, pushed 2026-06-02T09:32:38Z.
  - `Liverwortenuresis371/copyfail-rs`, a Rust Copy Fail indicator, pushed 2026-06-02T09:31:20Z.
  - `INTELEON404/CVE-2026-49009`, a Mender Server authenticated path traversal to RCE indicator, created 2026-06-02T08:42:36Z and pushed 2026-06-02T09:03:11Z.
  - `tracyliving606/RegPwn`, a Windows local privilege escalation indicator for CVE-2026-24291, pushed 2026-06-02T09:07:35Z.
  - `Recorded-texteditor120/CVE-2026-31802`, an npm tar symlink/path overwrite indicator, pushed 2026-06-02T09:08:48Z.
  - `AzDevops143/fragnesia-cve-2026-46300`, a sparse JavaScript repository pushed 2026-06-02T10:05:07Z; details unvalidated.
- Treat all public PoC repositories as potentially hostile. Do not execute outside isolated malware-analysis sandboxes.

## Malware Intelligence

- FortiClient EMS to EKZ Infostealer: Arctic Wolf reports CVE-2026-35616 abuse against FortiClient EMS deployments. Threat actors abused endpoint-management workflows to push payloads named `FortiEndpoint_Patch.exe`/`p.exe`, tracked as EKZ Infostealer, targeting browser credentials, cookies, and autofill data. Confidence: High.
- Miasma / Mini Shai-Hulud supply chain: Wiz and other researchers report at least 32 `@redhat-cloud-services` npm packages compromised on 2026-06-01. Payloads execute through install hooks, use GitHub Actions/OIDC tradecraft, and harvest GitHub/npm/cloud/SSH/Kubernetes/Vault secrets. Confidence: High for package compromise; attribution to TeamPCP vs copycat remains Medium.
- Ghost CMS ClickFix campaign: Public reporting says exploitation of Ghost CMS CVE-2026-26980 has compromised 700+ sites, using stolen Admin API keys to inject JavaScript that redirects visitors to fake Cloudflare verification flows and malware droppers. Confidence: Medium because primary Ghost/XLab source was not directly fetched in this run.
- cPanel/WHM CVE-2026-41940: CISA KEV marks known ransomware campaign use; public reporting ties mass exploitation to "Sorry" ransomware and Mirai variants. Confidence: High for exploitation/KEV, Medium for exact current victim counts.
- VX-Underground: latest `vxunderground/MalwareSourceCode` commit is `1623926` from 2026-05-30, adding `Python/Stealer.Python.GMBA.Manipulator.7z`. No newer malware source commit was observed this run. Confidence: High.

## Security Releases and Advisories

- Microsoft: CVE-2026-41089 was patched in the May 2026 Patch Tuesday release. Belgium CCB/secondary reporting says it is exploited in the wild; CISA KEV did not list this CVE at collection time. Microsoft Defender CVE-2026-41091 and CVE-2026-45498 remain CISA KEV entries with 2026-06-03 due dates.
- Cisco: Cisco advisory `cisco-sa-sdwan-rpa2-v69WY2SW` provides fixed releases for CVE-2026-20182 and states no workarounds are available. Cisco recommends preserving admin-tech and logs before upgrade.
- Fortinet: FortiClient EMS CVE-2026-35616 is patched through Fortinet hotfix / 7.4.7 path. Active EKZ deployment raises priority above standard patch windows.
- Palo Alto Networks: PAN-OS CVE-2026-0257 fixed versions are available across PAN-OS 10.2, 11.1, 11.2, 12.1 and Prisma Access; Palo Alto lists exploit maturity as `ATTACKED`.
- LiteSpeed: LiteSpeed patched CVE-2026-48172 in cPanel user-end plugin 2.4.5 and recommends LiteSpeed WHM Plugin 5.3.1.0 bundled with cPanel plugin 2.4.7 or later. LiteSpeed states versions 2.3 through 2.4.4 were actively exploited.
- Red Hat OpenShift: NVD published CVE-2026-1784 for Route `spec.path` validation allowing controlled HAProxy configuration injection. Track Red Hat remediation and restrict Route modification privileges.
- Prefect: GitHub commit `e21617125335025b4b27e7d6f0ca028e8e8f3b79` fixes CVE-2026-3514 by replacing suffix-based auth bypass matching with exact health/ready path checks using ASGI scope path.
- Mender: Mender Server 4.1.1 and 4.0.2 fix CVE-2026-49009 and CVE-2026-33552. Hosted Mender was already patched per vendor; Enterprise and Community self-hosted deployments should upgrade.
- Drupal: SA-CORE-2026-004 fixes CVE-2026-9082 in 10.4.10, 10.5.10, 10.6.9, 11.1.10, 11.2.12, and 11.3.10. Drupal updated the advisory for detected exploit attempts.
- Cloud Foundry: CVE-2026-40965 fixed by `uaa_release` v78.13.0+ and `cf-deployment` v56.1.0+ for deployments using EC keys for JWT signing.
- GitLab/GitHub developer tooling: Continue triage of GitLab 19.0.1/18.11.4/18.10.7, Vitest critical advisories, and npm package compromise exposure in CI/CD environments.

## Recommended Actions

1. Emergency patch and hunt: Cisco Catalyst SD-WAN CVE-2026-20182, PAN-OS CVE-2026-0257, FortiClient EMS CVE-2026-35616, Drupal CVE-2026-9082, cPanel/WHM CVE-2026-41940, LiteSpeed cPanel Plugin CVE-2026-48172, Ghost CMS CVE-2026-26980, and Microsoft Netlogon CVE-2026-41089.
2. Treat management planes as possible compromise points: preserve Cisco SD-WAN logs before patching, review FortiClient EMS policy/script changes, inspect WHM/cPanel sessions and webshell indicators, inspect LiteSpeed/cPanel logs for `redisAble`, and rotate credentials after compromise checks.
3. Patch newly published high-severity enterprise/dev infrastructure: Prefect CVE-2026-3514, Red Hat OpenShift Route CVE-2026-1784, and Mender Server CVE-2026-49009 where artifact generation is enabled.
4. Supply-chain response: identify installs of affected TanStack/Nx/Red Hat npm package versions, remove persistence before revoking tokens where Mini Shai-Hulud/Miasma guidance applies, then rotate GitHub/npm/cloud/SSH/Kubernetes/Vault credentials and audit CI/CD workflows.
5. Inventory internet-facing Drupal PostgreSQL sites, GlobalProtect portals/gateways, Cisco SD-WAN controllers, FortiClient EMS servers, cPanel/WHM and LiteSpeed/cPanel instances, Ghost CMS instances, Mender servers, OpenShift Route controllers, and AD domain controllers; prioritize external exposure and privileged-management roles.
6. Monitor public PoC repositories cautiously. Public GitHub repositories are indicators only, not proof of functional exploit code; they may be trojanized.

## Unified Vulnerability Records

```json
[
  {
    "cve": "CVE-2026-20182",
    "cvss": "10.0",
    "vendor": "Cisco",
    "product": "Catalyst SD-WAN Controller and Manager",
    "affected_versions": "Multiple Catalyst SD-WAN release trains before Cisco fixed releases including 20.9.9.1, 20.12.5.4/20.12.6.2/20.12.7.1, 20.15.4.4/20.15.5.2, 20.18.2.2, and 26.1.1.1",
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
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://blog.talosintelligence.com/sd-wan-ongoing-exploitation/"
    ]
  },
  {
    "cve": "CVE-2026-41089",
    "cvss": "9.8",
    "vendor": "Microsoft",
    "product": "Windows Netlogon / domain controllers",
    "affected_versions": "Windows Server 2012 through 2025 when acting as domain controllers per NVD/public reporting",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/0xABCD01/CVE-2026-41089"
    ],
    "patch_available": true,
    "sources": [
      "https://msrc.microsoft.com/update-guide/vulnerability/CVE-2026-41089",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-41089",
      "https://www.securityweek.com/critical-windows-netlogon-vulnerability-in-attackers-crosshairs/"
    ]
  },
  {
    "cve": "CVE-2026-0257",
    "cvss": "7.8",
    "vendor": "Palo Alto Networks",
    "product": "PAN-OS GlobalProtect and Prisma Access",
    "affected_versions": "PAN-OS 10.2, 11.1, 11.2, 12.1 and Prisma Access versions below advisory fixed releases when GlobalProtect auth override cookie conditions are met",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://security.paloaltonetworks.com/CVE-2026-0257",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://securityaffairs.com/192951/security/u-s-cisa-adds-palo-alto-networks-pan-os-flaw-to-its-known-exploited-vulnerabilities-catalog.html"
    ]
  },
  {
    "cve": "CVE-2026-35616",
    "cvss": "9.1",
    "vendor": "Fortinet",
    "product": "FortiClient EMS",
    "affected_versions": "FortiClient EMS 7.4.5 and 7.4.6 per public reporting",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://arcticwolf.com/resources/blog/forticlient-ems-exploited-via-cve-2026-35616-to-deliver-ekz-infostealer-disguised-as-a-fortinet-patch/",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"
    ]
  },
  {
    "cve": "CVE-2026-9082",
    "cvss": "6.5 NVD / Drupal highly critical",
    "vendor": "Drupal",
    "product": "Drupal Core",
    "affected_versions": ">=8.9.0 <10.4.10, >=10.5.0 <10.5.10, >=10.6.0 <10.6.9, >=11.0.0 <11.1.10, >=11.2.0 <11.2.12, >=11.3.0 <11.3.10 when using PostgreSQL",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://sploitus.com/exploit?id=458CE696-FE39-500F-9131-2E24B1BC2E12",
      "https://sploitus.com/exploit?id=1774D6F8-2B0F-5C66-A7AB-BE7B8E7A0B85",
      "https://www.exploit-db.com/exploits/52608"
    ],
    "patch_available": true,
    "sources": [
      "https://www.drupal.org/sa-core-2026-004",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-9082"
    ]
  },
  {
    "cve": "CVE-2026-41940",
    "cvss": "9.8",
    "vendor": "WebPros",
    "product": "cPanel & WHM and WP2",
    "affected_versions": "Supported cPanel & WHM release tracks after 11.40 before vendor security updates per public reporting",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://sploitus.com/exploit?id=MSF%3AEXPLOIT-MULTI-HTTP-CPANEL_WHM_AUTH_BYPASS_RCE-",
      "https://sploitus.com/exploit?id=EDB-ID%3A52574",
      "https://github.com/Defacto-ridgepole254/CVE-2026-41940-Exploit-PoC"
    ],
    "patch_available": true,
    "sources": [
      "https://support.cpanel.net/hc/en-us/articles/40073787579671-cPanel-WHM-Security-Update-04-28-2026",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://www.bleepingcomputer.com/news/security/critrical-cpanel-flaw-mass-exploited-in-sorry-ransomware-attacks/"
    ]
  },
  {
    "cve": "CVE-2026-48172",
    "cvss": "10.0 v4 / 9.8 v3",
    "vendor": "LiteSpeed Technologies",
    "product": "LiteSpeed User-End cPanel Plugin",
    "affected_versions": "User-end plugin versions 2.3 through 2.4.4; fixed in user-end plugin 2.4.5+ with recommended bundle cPanel plugin 2.4.7 / WHM Plugin 5.3.1.0+",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://sploitus.com/exploit?id=36AAEAF3-4B32-5BE1-817C-7C65B5B446FE"
    ],
    "patch_available": true,
    "sources": [
      "https://blog.litespeedtech.com/2026/05/21/security-update-for-litespeed-cpanel-plugin/",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-48172"
    ]
  },
  {
    "cve": "CVE-2026-40965",
    "cvss": "10.0",
    "vendor": "Cloud Foundry",
    "product": "UAA / cf-deployment",
    "affected_versions": "uaa_release v76.12.0 through v78.12.0; CF Deployment v30.0.0 through v56.0.0 when using EC keys for JWT signing",
    "exploit_available": false,
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
      "https://patchstack.com/database/wordpress/plugin/kirki/vulnerability/wordpress-kirki-plugin-6-0-0-6-0-6-unauthenticated-privilege-escalation-via-handle-forgot-password-vulnerability",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-8206"
    ]
  },
  {
    "cve": "CVE-2024-21182",
    "cvss": "CISA KEV",
    "vendor": "Oracle",
    "product": "WebLogic Server",
    "affected_versions": "See Oracle advisory / CPU guidance",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json",
      "https://www.oracle.com/security-alerts/"
    ]
  },
  {
    "cve": "CVE-2026-3514",
    "cvss": "7.5",
    "vendor": "PrefectHQ",
    "product": "Prefect",
    "affected_versions": "Prefect 3.6.19 per NVD; vulnerable auth middleware used suffix-based health/ready exemptions",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/prefecthq/prefect/commit/e21617125335025b4b27e7d6f0ca028e8e8f3b79"
    ],
    "patch_available": true,
    "sources": [
      "https://nvd.nist.gov/vuln/detail/CVE-2026-3514",
      "https://github.com/prefecthq/prefect/commit/e21617125335025b4b27e7d6f0ca028e8e8f3b79",
      "https://huntr.com/bounties/c540e5e1-f74f-44f4-bfa0-9764ff6daa75"
    ]
  },
  {
    "cve": "CVE-2026-1784",
    "cvss": "8.8",
    "vendor": "Red Hat",
    "product": "OpenShift Route / HAProxy router",
    "affected_versions": "OpenShift Route configurations where insufficient `spec.path` checks allow controlled HAProxy configuration injection; exact fixed versions pending Red Hat advisory detail",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": false,
    "sources": [
      "https://nvd.nist.gov/vuln/detail/CVE-2026-1784",
      "https://access.redhat.com/security/cve/CVE-2026-1784",
      "https://bugzilla.redhat.com/show_bug.cgi?id=2436075"
    ]
  },
  {
    "cve": "CVE-2026-49009",
    "cvss": "3.1 NVD; severe in hosted multi-tenant context per vendor",
    "vendor": "Northern.tech",
    "product": "Mender Server",
    "affected_versions": "Mender Server 4.1.0, 4.0.1, and below; fixed in 4.1.1 and 4.0.2",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [
      "https://github.com/INTELEON404/CVE-2026-49009",
      "https://github.com/j0xh-sec/CVE-2026-49009"
    ],
    "patch_available": true,
    "sources": [
      "https://mender.io/blog/cve-2026-49009-cve-2026-33552-input-sanitization-and-access-control-issues-in-mender-server",
      "https://github.com/mendersoftware/mender-server/commit/484cc2a13ad44d93cdf0f3c2ea9155b9bac4a969",
      "https://nvd.nist.gov/vuln/detail/CVE-2026-49009"
    ]
  },
  {
    "cve": "CVE-2026-31431",
    "cvss": "7.8",
    "vendor": "Linux",
    "product": "Linux kernel AF_ALG AEAD / Copy Fail",
    "affected_versions": "Kernels carrying in-place AEAD behavior before upstream/stable fixes; distribution impact varies",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [
      "https://sploitus.com/exploit?id=E416E089-6938-57DA-B17F-340BD5B389C3",
      "https://sploitus.com/exploit?id=A6500AE2-6D3D-5689-B049-BFCE1470ED76",
      "https://github.com/theori-io/copy-fail-CVE-2026-31431"
    ],
    "patch_available": true,
    "sources": [
      "https://nvd.nist.gov/vuln/detail/CVE-2026-31431",
      "https://lore.kernel.org/linux-cve-announce/2026042214-CVE-2026-31431-3d65@gregkh/",
      "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"
    ]
  },
  {
    "cve": "CVE-2026-26980",
    "cvss": "9.4",
    "vendor": "Ghost",
    "product": "Ghost CMS",
    "affected_versions": "Ghost CMS 3.24.0 through 6.19.0 per public reporting; fixed in 6.19.1+",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": [
      "https://www.rescana.com/post/active-exploitation-alert-ghost-cms-cve-2026-26980-mass-attack-hijacks-700-sites-for-clickfix-malware-campaigns",
      "https://cybelangel.com/blog/cve-2026-26980-ghost-cms-flaw/",
      "https://socprime.com/active-threats/clickfix-campaign-hijacks-700-ghost-websites/"
    ]
  }
]
```
