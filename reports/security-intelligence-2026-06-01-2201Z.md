# Security Intelligence Report - 2026-06-01 22:01 UTC

## Executive Summary

- **NVD CVEs published during this collection window:** 261 total through 22:01 UTC.
  - Critical: 16
  - High: 86
  - Medium: 113
  - Low: 25
  - Unknown/unscored: 21
- **Critical findings:** Oracle WebLogic CVE-2024-21182 was added to CISA KEV today; PAN-OS CVE-2026-0257 remains actively exploited and is KEV-listed; IBM published three new critical WebSphere Application Server advisories; AITER/ROCm, CloudPirates Helm charts, Cline, OTRS, Poly/HP, and Android XR also had critical disclosures.
- **Active exploitation findings:** Confirmed active exploitation for CVE-2024-21182 (CISA KEV) and CVE-2026-0257 (Palo Alto Networks "ATTACKED" status, CISA KEV, Rapid7 observations). Cisco SD-WAN CVE-2026-20182 remains a recent KEV/high-priority issue from the previous week.
- **New exploit/PoC signals:** GitHub repositories created today reference CVE-2026-0257, CVE-2026-31431, CVE-2026-41089, CVE-2026-45659, and CVE-2026-23744. Treat these as indicators requiring validation; repository existence does not prove exploit reliability or safety.
- **New malware intelligence:** vx-underground's GitHub organization shows a May 30 addition of `Python/Stealer.Python.GMBA.Manipulator.7z` to `MalwareSourceCode`. This is malware archive activity, not confirmation of a current campaign.
- **Important vendor/security releases:** IBM WebSphere Application Server, Palo Alto PAN-OS/Prisma Access, Ivanti Neurons for ITSM, GitLab CE/EE, Android/XR June bulletin, Apple iOS/macOS 26.5.1 with no published CVEs, recent Fortinet PSIRT May advisories, and Cisco Catalyst SD-WAN KEV follow-up remain operationally relevant.

## Collection Notes and Confidence

- **High confidence:** CISA KEV JSON/catalog, NVD API, vendor advisories from Oracle, Palo Alto Networks, IBM, Ivanti, Microsoft, GitHub advisories, Apache/GitLab/Fortinet pages where directly fetched or corroborated.
- **Medium confidence:** GitHub repository signals and Sploitus-indexed search results, because they indicate public material but not exploit quality.
- **Low confidence:** Dark-web/ransomware victim claims from secondary reporting when not corroborated by victim statements or primary leak-site review.
- Sploitus homepage did not expose an "Exploits of the Week" block in static fetch. The Sploitus section below reconstructs the top exploit leads from indexed Sploitus search results plus corroborating exploit feeds and is explicitly marked as reconstructed.

## Top Vulnerabilities

### 1. CVE-2024-21182 - Oracle WebLogic Server unspecified/authentication-related vulnerability

- **Severity:** High, CVSS 7.5; **Critical priority** due to KEV and active exploitation.
- **Affected software:** Oracle WebLogic Server 12.2.1.4.0 and 14.1.1.0.0, Core component.
- **Impact:** Unauthenticated network attacker via T3/IIOP can compromise WebLogic Server confidentiality and gain unauthorized access to critical data.
- **Exploit availability:** Public PoC references appear in third-party indexes; validate before use.
- **Active exploitation:** Yes. Added to CISA KEV on 2026-06-01.
- **Patch available:** Yes. Oracle July 2024 Critical Patch Update or later applicable fixes.
- **Recommended action:** Immediately identify WebLogic systems exposing T3/IIOP, apply Oracle CPU fixes, restrict T3/IIOP exposure, and review access logs for anomalous protocol activity.
- **Confidence:** High.
- **Sources:** CISA KEV feed/catalog; CISA alert `https://www.cisa.gov/news-events/alerts/2026/06/01/cisa-adds-one-known-exploited-vulnerability-catalog`; Oracle CPU `https://www.oracle.com/security-alerts/cpujul2024.html`; NVD `https://nvd.nist.gov/vuln/detail/CVE-2024-21182`.

### 2. CVE-2026-0257 - Palo Alto Networks PAN-OS GlobalProtect authentication bypass

- **Severity:** Palo Alto CVSS-BT 7.8 High; **Critical priority** due to internet-facing VPN impact, active exploitation, and KEV listing.
- **Affected software:** PAN-OS 10.2, 11.1, 11.2, 12.1 and Prisma Access configurations with GlobalProtect portal/gateway, authentication override cookies enabled, and vulnerable certificate reuse.
- **Impact:** Remote unauthenticated attacker can forge authentication override cookies and establish unauthorized VPN access.
- **Exploit availability:** Public GitHub repositories created today reference the CVE; treat as unvalidated. Sploitus/GitHub signals indicate public PoC activity.
- **Active exploitation:** Yes. Palo Alto Networks marks exploit maturity as **ATTACKED**; CISA KEV added 2026-05-29; Rapid7 reported exploitation starting 2026-05-17.
- **Patch available:** Yes. Upgrade to fixed PAN-OS/Prisma Access versions listed by Palo Alto.
- **Recommended action:** Patch immediately; disable authentication override or issue a dedicated cookie certificate if patching is delayed; hunt for unexpected GlobalProtect sessions.
- **Confidence:** High.
- **Sources:** Palo Alto advisory `https://security.paloaltonetworks.com/CVE-2026-0257`; CISA KEV feed; NVD; Rapid7 exploitation reporting.

### 3. CVE-2026-9311 and CVE-2026-9330 - IBM WebSphere Application Server remote code execution

- **Severity:** Critical/High; CVE-2026-9311 CVSS 9.0, CVE-2026-9330 CVSS 8.5.
- **Affected software:** IBM WebSphere Application Server traditional 8.5 and 9.0.
- **Impact:** CVE-2026-9311 allows RCE via security-control bypass; CVE-2026-9330 allows RCE through improper validation during SAML Web SSO deserialization when combined with a suitable gadget chain.
- **Exploit availability:** No validated public exploit observed in this run.
- **Active exploitation:** Not reported by IBM in the advisory.
- **Patch available:** Interim fix/fix pack resolving APAR PH71453; target fix packs 9.0.5.29 and 8.5.5.30.
- **Recommended action:** Apply IBM interim fixes, prioritize externally reachable WebSphere and SAML SSO-enabled deployments, and monitor HTTP/SAML endpoints.
- **Confidence:** High.
- **Sources:** IBM `https://www.ibm.com/support/pages/node/7274733`; NVD Jun 1 feed.

### 4. CVE-2026-9319 - IBM WebSphere Application Server JAX-WS/WS-Security deserialization RCE

- **Severity:** Critical, CVSS 9.0.
- **Affected software:** IBM WebSphere Application Server traditional 8.5 and 9.0.
- **Impact:** Potential RCE due to deserialization of untrusted data via JAX-WS endpoints with WS-Security.
- **Exploit availability:** No validated public exploit observed in this run.
- **Active exploitation:** Not reported by IBM.
- **Patch available:** Interim fix/fix pack resolving APAR PH71454; target fix packs 9.0.5.29 and 8.5.5.30.
- **Recommended action:** Patch, inventory WS-Security-enabled JAX-WS endpoints, and review exposed SOAP services.
- **Confidence:** High.
- **Sources:** IBM `https://www.ibm.com/support/pages/node/7274738`; NVD Jun 1 feed.

### 5. CVE-2026-8644 - IBM WebSphere Application Server identity spoofing

- **Severity:** Critical, CVSS 9.1.
- **Affected software:** IBM WebSphere Application Server 8.5 and 9.0.
- **Impact:** Identity spoofing / authentication bypass by spoofing.
- **Exploit availability:** No validated public exploit observed in this run.
- **Active exploitation:** Not reported by IBM.
- **Patch available:** Interim fix/fix pack resolving APAR PH71422; target fix packs 9.0.5.29 and 8.5.5.30.
- **Recommended action:** Patch and audit authentication-sensitive applications.
- **Confidence:** High.
- **Sources:** IBM `https://www.ibm.com/support/pages/node/7274740`; NVD Jun 1 feed.

### 6. CVE-2026-49121 - AI Tensor Engine for ROCm (AITER) unauthenticated RCE

- **Severity:** NVD High 8.1; VulnCheck rates Critical 9.2 CVSSv4.
- **Affected software:** AITER through 0.1.14.
- **Impact:** Unauthenticated RCE through `MessageQueue.recv()` pickle deserialization in `shm_broadcast.py`; attacker reaching the writer XPUB endpoint or supplying a forged handle can execute code as inference worker processes.
- **Exploit availability:** Technical issue/PR references exist; no independent exploit validation performed.
- **Active exploitation:** Not observed in this run.
- **Patch available:** Upstream issue/PR activity referenced; verify fixed release before deployment.
- **Recommended action:** Restrict cluster-network access to AITER worker messaging paths, avoid untrusted pickle ingestion, track ROCm/AITER release guidance, and isolate inference workers.
- **Confidence:** Medium-High.
- **Sources:** VulnCheck `https://www.vulncheck.com/advisories/ai-tensor-engine-for-rocm-aiter-unauthenticated-rce-via-messagequeue-recv-pickle-deserialization`; NVD Jun 1 feed.

### 7. CVE-2026-49157 / CVE-2026-45505 / CVE-2026-42588 - Apache ActiveMQ security set

- **Severity:** High, CVSS 8.8/8.8/8.1.
- **Affected software:** Apache ActiveMQ Classic before 5.19.7 and 6.x before 6.2.6 for CVE-2026-49157; other ActiveMQ Broker/All/Classic versions per Apache advisories.
- **Impact:** Jolokia authorization misconfiguration, code injection/input validation issues, and JMX-HTTP bridge exposure can lead to unauthorized operations or code-impact paths depending on configuration.
- **Exploit availability:** No validated public exploit observed in this run.
- **Active exploitation:** Not observed.
- **Patch available:** Yes, per Apache release/advisory threads.
- **Recommended action:** Upgrade ActiveMQ, restrict Jolokia/JMX management access, and audit broker management endpoints.
- **Confidence:** Medium-High.
- **Sources:** NVD Jun 1 feed; Apache lists referenced by NVD.

### 8. CVE-2026-44825 - Apache Solr hardcoded credentials in Basic Authentication setup tool

- **Severity:** High, CVSS 8.1.
- **Affected software:** Apache Solr 9.4.0 through 9.10.1 and 10.0.0.
- **Impact:** Remote attacker can gain full administrative access to the cluster via predictable credentials generated by `bin/solr auth enable`.
- **Exploit availability:** No validated public exploit observed in this run.
- **Active exploitation:** Not observed.
- **Patch available:** Yes, per Apache advisory.
- **Recommended action:** Upgrade Solr, rotate generated Basic Auth credentials, review Solr admin/API logs, and restrict admin interfaces.
- **Confidence:** Medium-High.
- **Sources:** NVD Jun 1 feed; Apache advisory `https://lists.apache.org/thread/5xg6xr99glocp3zsg9ht2zlbwlrst7ch`.

### 9. CVE-2026-47294 - Microsoft Office SharePoint deserialization RCE

- **Severity:** High, CVSS 8.0.
- **Affected software:** Microsoft Office SharePoint, on-premises SharePoint variants per MSRC/NVD.
- **Impact:** Authorized attacker can execute code over the network via deserialization of untrusted data.
- **Exploit availability:** GitHub repository created today references a related SharePoint CVE (CVE-2026-45659); no validated exploit for CVE-2026-47294 observed.
- **Active exploitation:** Not observed in this run.
- **Patch available:** Yes through Microsoft security updates.
- **Recommended action:** Apply Microsoft updates, review low-privileged Site Member access, and monitor SharePoint for unusual deserialization/code execution indicators.
- **Confidence:** Medium-High.
- **Sources:** MSRC `https://msrc.microsoft.com/update-guide/vulnerability/CVE-2026-47294`; NVD Jun 1 feed.

### 10. CVE-2026-7770 - IBM i Access Client Solutions RCE

- **Severity:** High, CVSS 8.8.
- **Affected software:** IBM i Access Family 1.1.5.0 through 1.1.9.12 / IBM i Access Client Solutions when configured to listen for requests from IBM i Navigator.
- **Impact:** Remote code execution when specific listening configuration is enabled.
- **Exploit availability:** No validated public exploit observed.
- **Active exploitation:** Not observed.
- **Patch available:** IBM advisory available.
- **Recommended action:** Patch IBM i ACS, disable unnecessary listener behavior, and restrict access to trusted administration networks.
- **Confidence:** Medium-High.
- **Sources:** IBM `https://www.ibm.com/support/pages/node/7274214`; NVD Jun 1 feed.

### 11. CVE-2026-9614 - Ivanti Neurons for ITSM improper access control

- **Severity:** High, CVSS 8.8.
- **Affected software:** Ivanti Neurons for ITSM cloud and on-premises.
- **Impact:** Remote authenticated attacker can gain administrative access.
- **Exploit availability:** No validated public exploit observed.
- **Active exploitation:** Ivanti states it is not aware of customers being exploited through the issue disclosed today.
- **Patch available:** Yes, per Ivanti advisory/security update.
- **Recommended action:** Apply Ivanti fix as soon as available for on-premises; confirm cloud tenant status with Ivanti; review administrator account activity.
- **Confidence:** Medium-High.
- **Sources:** Ivanti June 2026 ITSM security update; NVD Jun 1 feed.

### 12. CVE-2026-41089 - Microsoft Windows Netlogon unauthenticated RCE

- **Severity:** Critical, CVSS 9.8.
- **Affected software:** Windows Server 2012 through 2025 versions per NVD/MSRC.
- **Impact:** Stack-based buffer overflow in Windows Netlogon allows unauthenticated network code execution.
- **Exploit availability:** GitHub repository created today claims a PoC; not validated.
- **Active exploitation:** Not confirmed in this run.
- **Patch available:** Microsoft May 2026 updates.
- **Recommended action:** Ensure all domain controllers received May 2026 updates, restrict Netlogon/RPC access to required networks, and watch for anomalous MS-NRPC traffic.
- **Confidence:** Medium-High for vulnerability; Medium for PoC.
- **Sources:** NVD `https://nvd.nist.gov/vuln/detail/CVE-2026-41089`; GitHub search result `0xABCD01/CVE-2026-41089`.

## Unified CVE Records

```json
[
  {
    "cve": "CVE-2024-21182",
    "cvss": "7.5",
    "vendor": "Oracle",
    "product": "WebLogic Server",
    "affected_versions": "12.2.1.4.0, 14.1.1.0.0",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://github.com/k4it0k1d/CVE-2024-21182", "https://github.com/kursadalsan/CVE-2024-21182"],
    "patch_available": true,
    "sources": ["CISA KEV", "Oracle CPU July 2024", "NVD"]
  },
  {
    "cve": "CVE-2026-0257",
    "cvss": "7.8 CVSSv4 / critical operational priority",
    "vendor": "Palo Alto Networks",
    "product": "PAN-OS GlobalProtect / Prisma Access",
    "affected_versions": "PAN-OS 10.2, 11.1, 11.2, 12.1 ranges with authentication override cookie exposure; Prisma Access 10.2/11.2 ranges",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://github.com/bolubey/CVE-2026-0257", "https://github.com/Mr-Robot-LP/CVE-2026-0257"],
    "patch_available": true,
    "sources": ["Palo Alto Networks advisory", "CISA KEV", "Rapid7", "NVD", "GitHub search"]
  },
  {
    "cve": "CVE-2026-9319",
    "cvss": "9.0",
    "vendor": "IBM",
    "product": "WebSphere Application Server",
    "affected_versions": "8.5, 9.0",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["IBM advisory 7274738", "NVD"]
  },
  {
    "cve": "CVE-2026-49121",
    "cvss": "8.1 NVD / 9.2 VulnCheck CVSSv4",
    "vendor": "ROCm",
    "product": "AI Tensor Engine for ROCm (AITER)",
    "affected_versions": "<= 0.1.14",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": "pending/verify upstream fixed release",
    "sources": ["VulnCheck", "NVD", "ROCm issue references"]
  },
  {
    "cve": "CVE-2026-41089",
    "cvss": "9.8",
    "vendor": "Microsoft",
    "product": "Windows Netlogon",
    "affected_versions": "Windows Server 2012 through 2025 vulnerable builds per NVD/MSRC",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://github.com/0xABCD01/CVE-2026-41089"],
    "patch_available": true,
    "sources": ["NVD", "MSRC", "GitHub search"]
  }
]
```

## Exploits Released

### Sploitus Top 10 - Reconstructed

Sploitus homepage static content did not expose a current "Exploits of the Week" list. The following are the top 10 exploit leads observed from Sploitus-indexed web search plus corroborating exploit/GitHub/ExploitDB signals. Maturity and weaponization are analytic judgments, not Sploitus assertions.

| Rank | Lead | Affected software | Exploit type | Maturity | Public PoC | Weaponization potential | Confidence |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | CVE-2026-0257 | PAN-OS GlobalProtect | Auth bypass / VPN initial access | Active exploitation | Yes, GitHub indicators | Very high due to VPN edge impact | High |
| 2 | CVE-2024-21182 | Oracle WebLogic | Unauthenticated network compromise / data access | Active exploitation | Public PoC references | High for internet-exposed WebLogic | High |
| 3 | CVE-2026-41089 | Windows Netlogon | Unauthenticated RCE | Claimed PoC | GitHub indicator | Very high for AD/domain controllers if functional | Medium |
| 4 | CVE-2026-42167 | ProFTPD mod_sql | Pre-auth SQLi to auth bypass/RCE in some configs | Public PoC | Yes | High for exposed FTP with mod_sql | Medium-High |
| 5 | CVE-2026-31431 | Linux kernel "Copy Fail" | Local privilege escalation | Public PoC/research | Yes | High post-compromise; local access required | Medium |
| 6 | CVE-2026-23744 | MCPJam Inspector | Unauthenticated RCE on dev tooling | Public PoC/repo activity | Yes | High for exposed AI/MCP dev tools | Medium-High |
| 7 | CVE-2026-26335 | Calero VeraSMART | ViewState deserialization RCE | Exploit write-up indexed | Yes | Medium-High; requires keys/conditions | Medium |
| 8 | CVE-2026-41091 | Microsoft Defender "RedSun" | Local privilege escalation | PoC indexed by Sploitus | Yes | Medium-High post-compromise; KEV context from May | Medium |
| 9 | CVE-2025-6965 | SQLite/winsqlite3 | Heap overflow / DoS, possible RCE context | ExploitDB/Sploitus indexed | Yes | Medium; environment-dependent | Medium |
| 10 | CVE-2025-56005 | PLY 3.11 | Pickle deserialization code execution | PacketStorm/Sploitus indexed | Yes | Medium; developer/CI supply-chain angle | Medium |

### ExploitDB Additions

- No ExploitDB entries with `date_published`, `date_added`, or `date_updated` of 2026-06-01 or 2026-05-31 were present in the raw ExploitDB CSV index.
- Recent 2026-05-30 entries:
  - EDB-52603: YAMCS `yamcs-core` 5.12.7 LDAP Injection, CVE-2026-42568.
  - EDB-52604: YAMCS `yamcs-core` 5.12.7 User Enumeration, CVE-2026-44595.
  - EDB-52605: YAMCS `yamcs-core` 5.12.7 No Rate Limiting, CVE-2026-44596.
  - EDB-52606: Notepad++ 8.9.6 Arbitrary Code Execution, CVE-2026-48778.
- Notable 2026-05-29 entries:
  - Wing FTP Server 8.1.3 authenticated RCE, CVE-2026-44403.
  - MixPHP 2.2.17 unsafe deserialization RCE, CVE-2026-42471.
  - Linux kernel local privilege escalation, CVE-2026-46300 / CVE-2026-43500 / CVE-2026-43284.
  - Quick Playground for WordPress 1.3.1 unauthenticated RCE, CVE-2026-1830.
  - Langflow 1.3.0 RCE, CVE-2026-0770.
  - Microsoft NTLMv2 hash capture, CVE-2026-32202.

### Packet Storm

- Direct Packet Storm date fetch was blocked by anti-automation. Sploitus-indexed search surfaced a PacketStorm item for PLY 3.11 arbitrary code execution (CVE-2025-56005). Treat as medium-confidence until primary Packet Storm page is reviewed manually.

### New GitHub PoC / Exploit Indicators

Repositories created or updated around 2026-06-01 from GitHub search:

- `bolubey/CVE-2026-0257`, `Mr-Robot-LP/CVE-2026-0257`, `jennydokumi30/CVE-2026-0257` - PAN-OS GlobalProtect auth bypass indicators.
- `0xABCD01/CVE-2026-41089` - Microsoft Netlogon RCE PoC claim; 30 stars at collection time.
- `tematemaru/CVE-2026-31431-simple-test` - Linux kernel LPE test code indicator.
- `daniel30padd/CVE-2026-45659` - SharePoint RCE-related repository.
- `Least-Significant-Bit/CVE-2026-23744`, `sbouabid-sec/CVE-2026-23744-POC`, `SrGinebras/CVE-2026-23744-RCE-for-MCPjam-inspector-v1.4.2`, and `afifudinmtop/MCPJam-Inspector-1.4.2-Remote-Code-Execution-CVE-2026-23744` - MCPJam Inspector RCE indicators.
- `JianrongXiao-Linksys/dnsmasq-cve-2026` - dnsmasq CVE verification tooling indicator.
- Multiple low-star/zero-star repositories for Threema/better-sqlcipher claims and other CVE IDs; unvalidated.

**Caution:** Do not clone or execute these repositories in production or analyst workstations without sandboxing. Public CVE PoCs are frequently incomplete, malicious, or repackaged.

## Malware Intelligence

### VX-Underground

- Direct site fetch returned HTTP 403, but indexed search confirmed the site structure and GitHub checks were available.
- `vxunderground/MalwareSourceCode` latest commit observed:
  - Date: 2026-05-30
  - Commit: `1623926`
  - Added: `Python/Stealer.Python.GMBA.Manipulator.7z`
- This indicates a new archived stealer-related source/sample addition. It is not by itself evidence of active deployment.
- Other vxunderground repositories:
  - `VX-API` unchanged at commit history level since 2023 despite repository metadata update on Jun 1.
  - `VXUG-Papers` no recent commit activity observed.

### Ransomware / Threat Actor Activity

- Secondary reporting and threat-monitoring references indicate recent leak-site claims involving BravoX, Genesis, DragonForce, and Payload ransomware activity.
- BravoX has emerged as a 2026 RaaS actor using double extortion and atypical persistence/tunneling tradecraft per InfoGuard Labs.
- Payload ransomware reporting describes Windows-focused encryption using ChaCha20 and Curve25519 with anti-forensic behavior.
- Confidence is **Low-to-Medium** for individual victim claims because primary victim confirmation was not observed in this run.

## Security Releases and Vendor Advisories

### Microsoft

- CVE-2026-47294 SharePoint deserialization RCE published in the Jun 1 NVD feed with MSRC advisory link.
- CVE-2026-41089 Windows Netlogon unauthenticated RCE remains a critical May 2026 Patch Tuesday issue with new GitHub PoC signal today.
- Recommended action: confirm May/June security update deployment on SharePoint and all domain controllers.

### Cisco

- No new Cisco advisory specifically dated Jun 1 identified.
- Recent important Cisco issues:
  - CVE-2026-20182 Cisco Catalyst SD-WAN Controller/Manager authentication bypass, KEV-listed, May 2026; Cisco advisory includes compromise-check guidance and TAC case workflow.
  - CVE-2026-20223 Cisco Secure Workload zero-auth API/full admin control reported in May.
- Recommended action: verify SD-WAN controller remediation, retain logs, and run Cisco IoC checks.

### Fortinet

- No Fortinet PSIRT advisory dated Jun 1 identified.
- Recent May PSIRT items include:
  - FortiNDR SQL injection (FG-IR-26-134).
  - FortiAuthenticator improper access control allowing unauthorized code/command execution via crafted requests (FG-IR-26-128).
  - Multiple FortiOS/FortiPAM/FortiProxy/FortiSwitchManager issues from Apr/May.

### Palo Alto Networks

- CVE-2026-0257 updated May 29 with exploitation status. Fixed PAN-OS and Prisma Access versions are available.
- Recommended action: patch or mitigate immediately; monitor GlobalProtect authentication behavior.

### IBM

- Jun 1 WebSphere Application Server advisories:
  - CVE-2026-9311 / CVE-2026-9330 - RCE.
  - CVE-2026-9319 - JAX-WS WS-Security deserialization RCE.
  - CVE-2026-8644 - identity spoofing.
  - CVE-2026-7770 - IBM i Access Client Solutions RCE.

### Ivanti

- Jun 2026 Ivanti Neurons for ITSM update addresses CVE-2026-9614; Ivanti says it is not aware of customer exploitation at publication.
- Recommended action: update on-premises deployments and verify cloud tenant remediation.

### GitLab

- May 27 patch release 19.0.1, 18.11.4, 18.10.7 fixes seven security issues.
- Highest severity noted: CVE-2026-4868 Duo AI workflow runner improper access control, CVSS 8.2.
- Recommended action: upgrade self-managed GitLab CE/EE immediately.

### Google / Android

- Android XR Security Bulletin published Jun 1 with CVE-2026-0072, EoP, High, affecting Android 14 XR component; patch level 2026-06-01 or later.
- Android Automotive Jun 2026 bulletin indicates no AAOS-specific security patches.

### Apple

- iOS 26.5.1 and macOS Tahoe 26.5.1 released Jun 1 with **no published CVE entries** according to Apple security releases.

### Broadcom / VMware

- No Jun 1 VMware advisory identified.
- Most recent VMSA is VMSA-2026-0003 from May 14 for VMware Fusion local privilege escalation CVE-2026-41702, fixed in Fusion 26H1.

## Recommended Actions - Highest to Lowest Priority

1. **Patch or mitigate exploited KEV items immediately:**
   - Oracle WebLogic CVE-2024-21182.
   - Palo Alto PAN-OS/Prisma Access CVE-2026-0257.
   - Cisco Catalyst SD-WAN CVE-2026-20182 if not already remediated.
2. **Prioritize IBM WebSphere Jun 1 RCE advisories:**
   - Apply interim fixes for CVE-2026-9311, CVE-2026-9330, CVE-2026-9319, and CVE-2026-8644.
   - Inventory SAML SSO, JAX-WS, and WS-Security exposure.
3. **Protect identity and domain infrastructure:**
   - Verify May 2026 Microsoft patches on all domain controllers for CVE-2026-41089.
   - Restrict Netlogon/RPC exposure and monitor for anomalous MS-NRPC traffic.
4. **Patch enterprise collaboration and dev platforms:**
   - SharePoint CVE-2026-47294.
   - GitLab CE/EE 19.0.1/18.11.4/18.10.7.
   - Nextcloud high-severity advisories from Jun 1 if deployed.
5. **Restrict and update AI/dev tooling:**
   - AITER/ROCm CVE-2026-49121: isolate cluster messaging and track fixed release.
   - MCPJam Inspector CVE-2026-23744: upgrade to 1.4.3+, bind to localhost, block exposed ports.
   - Cline CVE-2026-44211: disable/expose Kanban server only on trusted local context and apply vendor fixes when available.
6. **Harden Apache middleware:**
   - Upgrade ActiveMQ and Solr; restrict Jolokia/JMX/Solr admin endpoints.
7. **Treat public PoC repositories as hostile until proven otherwise:**
   - Analyze only in disposable sandboxes.
   - Prefer vendor scanners or internally reviewed detection logic.
8. **Monitor ransomware pressure signals:**
   - Track BravoX, Genesis, DragonForce, and Payload ransomware claims for sector relevance, but avoid treating leak-site claims as confirmed incidents without corroboration.

