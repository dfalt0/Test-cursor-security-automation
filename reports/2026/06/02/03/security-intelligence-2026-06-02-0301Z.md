# Security Intelligence Report - 2026-06-02 03:01 UTC

Prepared for: hourly security report automation
Repository: dfalt0/Test-cursor-security-automation
Branch: cursor/security-intelligence-agent-6173
Analyst confidence model: High = primary source or multiple authoritative confirmations; Medium = credible secondary plus primary vulnerability data; Low = single-source or unvalidated public PoC signal.

## Executive Summary

- Total CVEs discovered in the 2026-06-02 00:00-03:15 UTC NVD window: 11.
  - Severity mix: 7 medium, 4 low, 0 high, 0 critical.
  - All 11 current-window CVEs have public disclosure or PoC indicators in NVD references; most are low-impact web application issues from VulDB/Wordfence.
- 24-hour NVD context, 2026-06-01 03:00 to 2026-06-02 03:15 UTC: 378 published CVEs.
  - Severity mix: 19 critical, 128 high, 152 medium, 37 low, 42 unknown.
- Critical findings requiring immediate enterprise attention:
  1. CVE-2026-41089 - Microsoft Windows Netlogon unauthenticated RCE, CVSS 9.8, CCB reports active exploitation.
  2. CVE-2024-21182 - Oracle WebLogic Server, added to CISA KEV on 2026-06-01 with a 2026-06-04 due date.
  3. CVE-2026-0257 - Palo Alto PAN-OS GlobalProtect authentication bypass, CISA KEV, Rapid7/Palo Alto observed exploitation.
  4. CVE-2026-40965 - Cloud Foundry UAA EC private key exposure via public `/token_keys`, CVSS 10.0.
  5. CVE-2026-44211 - Cline Kanban cross-origin WebSocket hijacking affecting local AI agent services, CVSS 9.6.
  6. CVE-2026-8644, CVE-2026-9311, CVE-2026-9319 - IBM WebSphere Application Server critical spoofing/RCE/deserialization set.
- Active exploitation findings:
  - High confidence: CISA KEV Oracle WebLogic CVE-2024-21182; Palo Alto PAN-OS CVE-2026-0257; Microsoft Defender CVE-2026-41091 and CVE-2026-45498; Cisco Catalyst SD-WAN CVE-2026-20182.
  - Medium confidence: Microsoft Netlogon CVE-2026-41089, because CCB states active exploitation while Microsoft/NVD had not yet reflected exploitation status in fetched data; WP Maps Pro CVE-2026-8732 based on public PoC plus security reporting.
- New malware/ransomware intelligence:
  - VX-Underground MalwareSourceCode most recent commit remains 2026-05-30, adding `Python/Stealer.Python.GMBA.Manipulator.7z`.
  - Microsoft Threat Intelligence published analysis of The Gentlemen ransomware, tracked as Storm-2697, a Go-based RaaS with self-propagation and double-extortion capabilities.
  - Breachsense reported 646 ransomware leak-site victim claims across 61 groups in May 2026; Qilin remained the top listed group.
- Important vendor/security releases:
  - Android June 2026 bulletin: critical Framework/System EoP/DoS vulnerabilities; patch level 2026-06-05 or later.
  - Ivanti June 2026 Neurons for ITSM security update: vendor reports no known exploitation at publication.
  - GitHub Enterprise Server 3.20.3: critical pre-auth SSRF CVE-2026-9312 and high-severity kernel/SSRF fixes.
  - GitLab 19.0.1, 18.11.4, 18.10.7: Duo AI access control, DoS, and authorization fixes.
  - Apple released 26.5.1 updates on 2026-06-01 with no published CVEs.

## Source Coverage and Collection Notes

- CISA KEV JSON feed fetched successfully: catalogVersion `2026.06.01`, dateReleased `2026-06-01T16:59:32.7272Z`, count 1608.
- NVD 2.0 API fetched successfully for current and 24-hour windows.
- GitHub repository search was performed via authenticated read-only GitHub CLI.
- Sploitus homepage/static access did not reliably expose an "Exploits of the Week" block during this run. The Sploitus section below is a reconstructed top-10 from indexed Sploitus exploit result pages and should be treated as Medium confidence for ranking, High confidence that each listed Sploitus URL was indexed.
- VX-Underground website was reachable as an index, and GitHub repository metadata was checked via GitHub API. No malware samples were downloaded or executed.
- MalwareBazaar authenticated API was not used because prior automation runs returned 401 without credentials; this report relies on public malware/ransomware reporting and VX GitHub metadata.

## Top Vulnerabilities

### 1. CVE-2026-41089 - Microsoft Windows Netlogon RCE

- Severity: Critical, CVSS 9.8.
- Affected software: Windows Server 2012 through 2025 when acting as domain controllers.
- Vulnerability type: stack-based buffer overflow in Windows Netlogon Remote Protocol.
- Exploit availability: public GitHub PoC indicator found: `0xABCD01/CVE-2026-41089`, created 2026-06-01, updated 2026-06-02, 42 stars at collection time.
- Active exploitation: CCB Belgium states active exploitation as of its 2026-05-29 advisory update; BleepingComputer and other sources report the CCB warning. Microsoft/NVD source data fetched for this run did not yet mark active exploitation.
- Patch available: yes, May 2026 Patch Tuesday.
- Recommended action: patch all domain controllers immediately; isolate untrusted Netlogon/RPC exposure; monitor anomalous domain-controller RPC/Netlogon traffic and sudden privileged account creation.
- Confidence: Medium for active exploitation, High for severity/affected product/patch.
- Sources:
  - NVD: https://nvd.nist.gov/vuln/detail/CVE-2026-41089
  - CCB Belgium advisory: https://ccb.belgium.be/advisories/warning-microsoft-patch-tuesday-may-2026-patches-118-vulnerabilities-16-critical-102
  - BleepingComputer: https://www.bleepingcomputer.com/news/microsoft/critical-windows-netlogon-remote-code-execution-flaw-now-exploited-in-attacks/
  - GitHub repo indicator: https://github.com/0xABCD01/CVE-2026-41089

### 2. CVE-2024-21182 - Oracle WebLogic Server KEV Addition

- Severity: NVD CVSS 7.5 high; operational priority critical because CISA KEV indicates known exploitation.
- Affected software: Oracle WebLogic Server 12.2.1.4.0 and 14.1.1.0.0.
- Vulnerability type: unspecified WebLogic Server Core vulnerability reachable unauthenticated over T3/IIOP.
- Exploit availability: no validated public PoC identified in this run.
- Active exploitation: yes, CISA KEV added 2026-06-01.
- KEV listed: yes; remediation due 2026-06-04.
- Patch available: yes, Oracle July 2024 Critical Patch Update or later applicable fixes.
- Recommended action: immediately verify WebLogic patch state; restrict T3/IIOP to trusted networks; hunt for unusual WebLogic access and serialized/T3 traffic.
- Confidence: High.
- Sources:
  - CISA alert: https://www.cisa.gov/news-events/alerts/2026/06/01/cisa-adds-one-known-exploited-vulnerability-catalog
  - CISA KEV JSON feed
  - NVD: https://nvd.nist.gov/vuln/detail/CVE-2024-21182
  - Oracle CPU: https://www.oracle.com/security-alerts/cpujul2024.html

### 3. CVE-2026-0257 - Palo Alto PAN-OS GlobalProtect Authentication Bypass

- Severity: NVD CVSS 9.1 critical; vendor originally scoped to configuration-dependent GlobalProtect exposure.
- Affected software: PAN-OS and Prisma Access GlobalProtect portal/gateway where authentication override cookies are enabled with specific certificate reuse.
- Vulnerability type: authentication bypass enabling unauthorized VPN connection.
- Exploit availability: public PoC signals exist on GitHub; Rapid7 validated a proof-of-concept during incident analysis.
- Active exploitation: yes; Rapid7 MDR observed exploitation beginning 2026-05-17, Palo Alto updated exploitation status 2026-05-29, CISA KEV added 2026-05-29.
- Patch available: yes; update to fixed PAN-OS/Prisma Access branches or disable authentication override/use dedicated certificate as temporary mitigation.
- Recommended action: treat as perimeter emergency; patch, rotate/reissue auth override certificates, inspect GlobalProtect logs for forged-cookie activity and anomalous VPN assignments.
- Confidence: High.
- Sources:
  - Palo Alto advisory: https://security.paloaltonetworks.com/CVE-2026-0257
  - Rapid7: https://www.rapid7.com/blog/post/etr-rapid7-observed-exploitation-of-pan-os-globalprotect-authentication-bypass-vulnerability-cve-2026-0257/
  - CISA KEV JSON feed

### 4. CVE-2026-40965 - Cloud Foundry UAA EC Private Key Exposure

- Severity: Critical, CVSS 10.0.
- Affected software: uaa_release v76.12.0 through v78.12.0; CF Deployment v30.0.0 through v56.0.0 when EC keys are used for JWT signing.
- Vulnerability type: public `/token_keys` endpoint exposes EC private key components, enabling JWT forgery risk.
- Exploit availability: no standalone exploit needed if endpoint is reachable and affected EC keys are configured.
- Active exploitation: not observed in reviewed sources.
- Patch available: yes; upgrade uaa_release to v78.13.0 or later, or cf-deployment to v56.1.0 or later.
- Recommended action: immediately inspect whether EC signing keys were exposed, rotate UAA signing keys/secrets, invalidate potentially forged sessions/tokens, upgrade.
- Confidence: High.
- Sources:
  - Cloud Foundry advisory: https://www.cloudfoundry.org/blog/cve-2026-40965-uaa-ec-private-key-disclosure/
  - NVD current 24-hour critical listing

### 5. CVE-2026-44211 - Cline Kanban Cross-Origin WebSocket Hijacking

- Severity: Critical, CVSS 9.6 in NVD/current reporting.
- Affected software: Cline AI coding assistant/Kanban server versions 2.13.0 and prior in fetched NVD record; vendor advisory recommends updating to fixed versions.
- Vulnerability type: localhost WebSocket service lacks Origin validation, allowing a malicious website to connect to `127.0.0.1:3484`, leak workspace data, and inject terminal/agent input.
- Exploit availability: vendor GitHub advisory includes browser PoC patterns.
- Active exploitation: not observed in reviewed sources.
- Patch available: yes; update Cline, disable unnecessary local Kanban services, restrict browser-to-localhost attack surface where feasible.
- Recommended action: prioritize developer workstation fleets using AI coding agents; update Cline; alert on browser-originated localhost WebSocket access where telemetry allows.
- Confidence: High.
- Sources:
  - GitHub advisory: https://github.com/cline/cline/security/advisories/GHSA-5c57-rqjx-35g2
  - NVD 24-hour critical listing
  - GitLab advisory DB: https://advisories.gitlab.com/npm/cline/CVE-2026-44211/

### 6. CVE-2026-8644, CVE-2026-9311, CVE-2026-9319 - IBM WebSphere Application Server

- Severity: Critical; CVSS 9.1, 9.0, 9.0.
- Affected software: IBM WebSphere Application Server 8.5 and 9.0.
- Vulnerability types: identity spoofing, RCE via security-control bypass, and potential RCE via JAX-WS WS-Security deserialization.
- Exploit availability: no public PoC validated in this run.
- Active exploitation: not observed in reviewed sources.
- Patch available: IBM support advisories were referenced by NVD; direct IBM pages previously timed out in automation memory and were not relied on for detail beyond NVD refs.
- Recommended action: prioritize Internet-facing WebSphere and WS-Security/JAX-WS endpoints for patch review and compensating controls.
- Confidence: Medium-High.
- Sources:
  - NVD 24-hour critical listing
  - IBM support references: `https://www.ibm.com/support/pages/node/7274740`, `7274733`, `7274738`

### 7. CVE-2026-8732 - WP Maps Pro Administrator Creation / Site Takeover

- Severity: Critical, CVSS 9.8 in public PoC/reporting.
- Affected software: WP Maps Pro / wp-google-map-gold <= 6.1.0 with GOLD addon and vulnerable temp-access workflow.
- Vulnerability type: unauthenticated administrator creation/passwordless magic-login workflow; some PoCs chain to code execution when PHP executes in uploads.
- Exploit availability: public GitHub PoCs found, and Sploitus indexed an exploit page dated 2026-05-30.
- Active exploitation: reported by vulnerability-intelligence sources; not independently confirmed by CISA/vendor in this run.
- Patch available: reported patched in 6.1.1.
- Recommended action: update immediately; audit for suspicious administrator accounts, especially vendor-looking support accounts; review webshells/uploads and outbound callbacks.
- Confidence: Medium.
- Sources:
  - Sploitus: https://sploitus.com/exploit?id=105190B4-DF97-59F6-91BF-BF55716FCF79
  - GitHub repo indicators: `p3Nt3st3r-sTAr/CVE-2026-8732-POC`, `CryptReaper12/CVE-2026-8732`
  - Threat-modeling report: https://threat-modeling.com/vulnerability-intelligence-report-june-1-2026/

### 8. CVE-2026-43494 - Linux Kernel PinTheft LPE

- Severity: High operational risk despite local attack vector.
- Affected software: Linux kernel RDS zero-copy path with RDS/RDS_TCP and io_uring conditions; public PoCs target x86_64 and require local code execution.
- Vulnerability type: RDS page-pin reference bug chained with io_uring fixed buffers for page-cache overwrite and root privilege escalation.
- Exploit availability: public PoCs found on GitHub (`0xBlackash/CVE-2026-43494`, `jayhutajulu1/CVE-2026-43494-PinTheft-PoC`, `letsr00t/CVE-2026-43494-PinTheft-PoC`).
- Active exploitation: not observed in reviewed sources.
- Patch available: upstream kernel stable commits including `e174929793195e0cd6a4adb0cad731b39f9019b4`.
- Recommended action: patch kernels; disable or block `rds`/`rds_tcp` modules where unused; consider `kernel.io_uring_disabled` hardening for multi-user/high-risk servers after compatibility review.
- Confidence: High for PoC/technical details, Medium for enterprise exposure breadth.
- Sources:
  - NVD: https://nvd.nist.gov/vuln/detail/CVE-2026-43494
  - oss-security: https://www.openwall.com/lists/oss-security/2026/05/21/2
  - GitHub PoC indicators from search

### 9. CVE-2026-27606 - Rollup Arbitrary File Write via Path Traversal

- Severity: High.
- Affected software: Rollup < 2.80.0, >=3.0.0 < 3.30.0, >=4.0.0 < 4.59.0.
- Vulnerability type: output filename path traversal allows arbitrary writes during builds; malicious plugins/untrusted repos can turn this into developer/CI compromise.
- Exploit availability: GitHub Security Advisory includes exploit/vendor-advisory classification and path traversal examples.
- Active exploitation: not observed in reviewed sources.
- Patch available: yes, 2.80.0, 3.30.0, 4.59.0.
- Recommended action: update Rollup in developer and CI dependency graphs; avoid building untrusted repos with privileged write access.
- Confidence: High.
- Sources:
  - GitHub advisory: https://github.com/rollup/rollup/security/advisories/GHSA-mw96-cpmx-2vgc
  - NVD: https://nvd.nist.gov/vuln/detail/CVE-2026-27606
  - OSV: https://osv.dev/vulnerability/CVE-2026-27606

### 10. CVE-2026-20182 - Cisco Catalyst SD-WAN Controller Authentication Bypass

- Severity: Critical operational priority; CISA KEV.
- Affected software: Cisco Catalyst SD-WAN Controller/Manager control connection handshaking.
- Vulnerability type: unauthenticated remote authentication bypass leading to administrative privileges.
- Exploit availability: no public PoC validated in this run.
- Active exploitation: yes; Cisco says PSIRT became aware of limited exploitation in May 2026, CISA KEV added 2026-05-14.
- Patch available: Cisco fixed software; no workaround.
- Recommended action: complete upgrades, retain logs, run Cisco's control connection checks, open TAC cases for suspected compromise.
- Confidence: High.
- Sources:
  - Cisco advisory: https://sec.cloudapps.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-sdwan-rpa2-v69WY2SW
  - CISA KEV JSON feed

## Current NVD Delta - 2026-06-02 00:00-03:15 UTC

| CVE | Severity | CVSS | Product / Component | Summary | Exploit/PoC Indicator | Priority |
| --- | --- | ---: | --- | --- | --- | --- |
| CVE-2026-10301 | Medium | 4.3 | itsourcecode Fees Management System 1.0 | XSS via `index.php?page` | Public exploit noted by VulDB/NVD | Low |
| CVE-2026-10302 | Medium | 6.3 | itsourcecode Fees Management System 1.0 | SQL injection via `/manage_fee.php` `ID` | Public exploit noted by VulDB/NVD | Medium |
| CVE-2026-10514 | Low | 2.4 | 1Panel-dev CordysCRM <= 1.6.2 | XSS in request param trimming config | GitHub issue/patch refs | Low |
| CVE-2026-10528 | Low | 3.3 | Orthanc DICOM Server <= 1.12.11 | Local stack-based buffer overflow in DCMTK parser | Public exploit noted by VulDB/NVD | Low |
| CVE-2026-9048 | Medium | 4.3 | Slider Revolution 7.0.0-7.0.14 | Contributor+ sensitive info exposure via AJAX action | Wordfence advisory | Medium |
| CVE-2026-9050 | Medium | 4.3 | Slider Revolution 6.0.0-6.7.55, 7.0.0-7.0.14 | Contributor+ unauthorized plugin deactivation | Wordfence advisory | Medium |
| CVE-2026-10529 | Low | 2.4 | westboy CicadasCMS rolling release | XSS in task scheduling management module | Public exploit noted by VulDB/NVD | Low |
| CVE-2026-10548 | Medium | 5.3 | NousResearch hermes-agent <= 2026.4.23 | Local improper authentication in credential pool sync | Public gist reference | Medium |
| CVE-2026-10550 | Medium | 6.3 | elunez eladmin <= 2.7 | Remote command injection via `uploadPath` with low privileges | Public issue reference | Medium |
| CVE-2026-10558 | Medium | 6.3 | SourceCodester Pizzafy Ecommerce System 1.0 | Admin local file inclusion via `page` | GitHub write-up reference | Medium |
| CVE-2026-10559 | Medium | 6.3 | SourceCodester Pizzafy Ecommerce System 1.0 | Frontend file inclusion/null byte injection via `page` | GitHub write-up reference | Medium |

## Exploits Released / Public PoC Signals

### Sploitus Top 10 - Reconstructed From Indexed Sploitus Results

The Sploitus homepage fetch timed out or exposed only the generic search UI; no authoritative homepage "Exploits of the Week" block was available to static collection. The following top-10 is reconstructed from indexed Sploitus exploit result pages found during targeted search and ranked by enterprise relevance, severity, and exploit maturity.

| Rank | CVE | Affected Software | Exploit Type | Exploit Maturity | Public PoC | Weaponization Potential |
| ---: | --- | --- | --- | --- | --- | --- |
| 1 | CVE-2026-8732 | WP Maps Pro <= 6.1.0 | Unauth admin creation / possible RCE chain | Functional multi-phase script claimed | Yes - Sploitus/GitHub | High for exposed WordPress sites |
| 2 | CVE-2026-42208 | BerriAI LiteLLM | SQL injection in AI gateway/auth path | Exploit brief indexed; KEV-listed | Yes - Sploitus/GHSA refs | High for AI gateway/API deployments |
| 3 | CVE-2026-41091 | Microsoft Defender | Link-following LPE to SYSTEM | Public PoC family (RedSun) indexed | Yes - Sploitus/GitHub refs | High post-compromise; KEV/exploited |
| 4 | CVE-2026-29014 | MetInfo CMS <= 8.1 | PHP code injection | Packet Storm PoC indexed by Sploitus | Yes | High where MetInfo is internet-facing |
| 5 | CVE-2026-29000 | pac4j-jwt | JWT authentication bypass | Library-level PoC tests vulnerable/patched versions | Yes | Medium-High for Java apps using affected library |
| 6 | CVE-2026-23869 | React Server Components / Flight Protocol | Unauth remote DoS | Automated scanner/exploit tooling claimed | Yes | Medium; availability impact on web apps |
| 7 | CVE-2026-27944 | Nginx UI | Sensitive data exposure / weak PoC | Unfinished PoC per indexed page | Yes, incomplete | Medium; validate before actioning |
| 8 | CVE-2026-48800 | Notepad++ <= 8.9.6 | Arbitrary code execution via config/shortcut manipulation | PoC script indexed | Yes | Medium; user/workstation targeting |
| 9 | CVE-2026-42897 | Microsoft Exchange Health Checker / EOMT diagnostic blind spot | Diagnostic bypass/mitigation visibility gap | PoC PowerShell mock config | Yes | Low-Medium; affects validation not core exploitability |
| 10 | CVE-2024-31317 | Google Android Zygote | Local privilege escalation to SYSTEM | Lab PoC indexed | Yes | Medium; older Android patch levels |

### ExploitDB Additions / Signals

- No confirmed June 2 ExploitDB addition was identified by web search.
- Recent indexed ExploitDB raw entries surfaced by search:
  - CVE-2026-24897 - Erugo <= 0.2.14 authenticated RCE, ExploitDB 52529, dated 2026-02-02.
  - CVE-2026-2441 - Google Chrome CSSFontFeatureValuesMap UAF, ExploitDB 52542, dated 2026-02-23.
  - CVE-2026-0740 - Ninja Forms Uploads unauthenticated PHP file upload, ExploitDB 52560, dated 2026-04-09.

### Packet Storm Signals

- Sploitus indexed Packet Storm exploit `PACKETSTORM:218222` for MetInfo CMS <= 8.1 PHP code injection, CVE-2026-29014, public disclosure 2026-04-01.
- Direct Packet Storm search results were noisy/legacy during this run; no additional June 2 packetstormsecurity.com file was validated.

### New GitHub PoC / Exploit Repository Signals

GitHub search for repositories created on or after 2026-06-01 returned the following notable results. These are indicators only; code was not cloned or executed.

| Repository | Created | Updated | Stars | Indicator | Assessment |
| --- | --- | --- | ---: | --- | --- |
| `0xABCD01/CVE-2026-41089` | 2026-06-01 | 2026-06-02 | 42 | Netlogon CVE-2026-41089 PoC claim | High-risk, unvalidated |
| `bolubey/CVE-2026-0257` | 2026-06-01 | 2026-06-02 | 0 | PAN-OS GlobalProtect auth bypass | High-risk, unvalidated |
| `CryptReaper12/CVE-2026-8732` | 2026-06-02 | 2026-06-02 | 0 | WP Maps Pro exploit claim | High-risk, unvalidated |
| `alisster00/CVE-2026-23744-RCE` | 2026-06-02 | 2026-06-02 | 0 | MCPJam v1.4.2 command execution claim | Needs validation |
| `p3Nt3st3r-sTAr/CVE-2026-8732-POC` | 2026-06-01 | 2026-06-02 | 7 | WP Maps Pro PoC | High-risk, unvalidated |
| `BS2010-AirborneTroops/NEXT-SSRF` | 2026-06-01 | 2026-06-01 | 0 | Next.js WebSocket upgrade SSRF CVE-2026-44578 scanner/exploit | Needs validation |
| `Vikramaditya015/samsung-android-lpe` | 2026-06-01 | 2026-06-01 | 0 | Samsung Android LPE CVE set | Needs validation |

## Malware Intelligence

### VX-Underground

- Website status: reachable as a directory/index page during this run.
- GitHub user repository check:
  - `vxunderground/MalwareSourceCode` most recent commit: `1623926`, 2026-05-30T07:10:59Z, message "Add files via upload".
  - Added file: `Python/Stealer.Python.GMBA.Manipulator.7z`.
  - No sample content was downloaded.
- Other vxunderground repositories with recent metadata updates:
  - `vxunderground/VX-API`, updated 2026-06-01.
  - `vxunderground/VXUG-Papers`, updated 2026-06-01.
- Assessment: new stealer source archive warrants malware-analysis review in an isolated environment if the organization tracks commodity Python stealers. Confidence: High for repository metadata, Low for malware behavior without sample analysis.

### Ransomware / Threat Activity

- The Gentlemen ransomware:
  - Microsoft Threat Intelligence tracks operators as Storm-2697.
  - Go-based RaaS with double-extortion activity, Garble obfuscation, and optional self-propagation via up to 21 lateral movement techniques.
  - Reported targeting includes education, transportation, healthcare, and financial industries across multiple regions.
  - Recommended detections: unusual PsExec/WMI/PowerShell Remoting spread activity, shadow copy deletion, backup service termination, mass file encryption, and new hidden SMB shares.
  - Source: https://www.microsoft.com/en-us/security/blog/2026/05/28/the-gentlemen-ransomware-dissecting-a-self-propagating-go-encryptor/
- Ransomware leak-site statistics:
  - Breachsense reported 646 claimed ransomware victims in May 2026 across 61 groups and 73 countries, with Qilin listed as top group for a fifth straight month.
  - Treat these as leak-site claims, not independently verified breach counts.
  - Source: https://www.breachsense.com/ransomware-reports/may-2026/

## Security Releases and Vendor Advisories

### Microsoft

- May 2026 Patch Tuesday remains operationally urgent due to active exploitation reports for CVE-2026-41089 Netlogon RCE.
- Microsoft Defender exploited KEV cluster:
  - CVE-2026-41091 - link-following LPE to SYSTEM.
  - CVE-2026-45498 - Defender DoS/update disruption.
  - Fixed engine/platform versions referenced in public reporting: Malware Protection Engine 1.1.26040.8 or later; Defender Antimalware Platform 4.18.26040.7 or later.
- No new Microsoft Patch Tuesday release on June 2 was identified.

### Cisco

- No new June 2 critical Cisco advisory found.
- Continue priority action for Cisco Catalyst SD-WAN:
  - CVE-2026-20182 KEV/limited exploitation, no workaround.
  - Cisco Catalyst SD-WAN Manager May 14 advisory also includes critical/high issues such as CVE-2026-20224 XXE and privilege escalation flaws.

### Fortinet

- No new June 2 Fortinet PSIRT advisory found.
- Continue priority action for CVE-2026-44277 FortiAuthenticator critical improper access control / unauthorized command execution.
- Fixed versions in Fortinet advisory FG-IR-26-128: FortiAuthenticator 8.0.3+, 6.6.9+, 6.5.7+; workaround: disable API access on exposed interfaces.

### Palo Alto Networks

- CVE-2026-0257 GlobalProtect auth bypass remains active-exploitation priority; see Top Vulnerabilities.

### VMware / Broadcom

- No new June 2 VMware/Broadcom VMSA identified.
- Broadcom impact evaluation for Dirty Frag/Fragnesia indicates multiple VMware virtual appliances based on Photon OS are not affected, but customers should verify product-specific status.

### Ivanti

- June 2026 Ivanti Neurons for ITSM security update published.
- Vendor states it is not aware of customer exploitation through the vulnerability disclosed that day.
- On-prem Ivanti Neurons for ITSM customers should review the advisory and apply fixes promptly.

### GitLab

- GitLab 19.0.1, 18.11.4, and 18.10.7 released 2026-05-27.
- Notable fixes:
  - CVE-2026-4868 - Duo AI workflow runner improper access control, CVSS 8.2.
  - CVE-2026-1402 - Wiki DoS.
  - CVE-2026-6713, CVE-2026-5296, CVE-2026-2601, CVE-2026-8716, CVE-2026-2710 - authorization/name resolution issues.
- GitLab.com already patched; self-managed instances should upgrade.

### GitHub

- GitHub Enterprise Server 3.20.3 released 2026-05-26/27.
- Notable fixes:
  - CVE-2026-9312 - critical pre-auth SSRF in upload endpoint.
  - CVE-2026-43284 and CVE-2026-43500 - Dirty Frag kernel LPE issues.
  - CVE-2026-8606 - timing side-channel plus SSRF in Packages/security advisory package lookup.
- Operational note: GitHub rotated/revoked package signing keys; administrators must rotate trusted GPG public keys before applying the update.

### Google / Android

- Android Security Bulletin - June 2026 published 2026-06-01.
- Most severe June issue: critical Framework vulnerability that could lead to remote escalation of privilege with no additional execution privileges or user interaction.
- Security patch level 2026-06-05 or later addresses all June bulletin issues.

### Apple

- Apple security releases page listed iOS 26.5.1 and macOS Tahoe 26.5.1 on 2026-06-01 with "no published CVE entries."
- No newly disclosed June 2 Apple exploited zero-day identified.

### Cloud Foundry

- CVE-2026-40965 UAA EC private key exposure is critical; upgrade and rotate keys.

## Unified Vulnerability Records

```json
[
  {
    "cve": "CVE-2026-41089",
    "cvss": "9.8",
    "vendor": "Microsoft",
    "product": "Windows Server Netlogon",
    "affected_versions": "Windows Server 2012 through 2025 domain controllers per NVD affected CPEs",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": false,
    "poc_links": ["https://github.com/0xABCD01/CVE-2026-41089"],
    "patch_available": true,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2026-41089", "https://ccb.belgium.be/advisories/warning-microsoft-patch-tuesday-may-2026-patches-118-vulnerabilities-16-critical-102", "https://www.bleepingcomputer.com/news/microsoft/critical-windows-netlogon-remote-code-execution-flaw-now-exploited-in-attacks/"]
  },
  {
    "cve": "CVE-2024-21182",
    "cvss": "7.5",
    "vendor": "Oracle",
    "product": "WebLogic Server",
    "affected_versions": "12.2.1.4.0 and 14.1.1.0.0",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://www.cisa.gov/news-events/alerts/2026/06/01/cisa-adds-one-known-exploited-vulnerability-catalog", "https://nvd.nist.gov/vuln/detail/CVE-2024-21182", "https://www.oracle.com/security-alerts/cpujul2024.html"]
  },
  {
    "cve": "CVE-2026-0257",
    "cvss": "9.1",
    "vendor": "Palo Alto Networks",
    "product": "PAN-OS GlobalProtect / Prisma Access",
    "affected_versions": "Configuration-dependent GlobalProtect portal/gateway deployments using authentication override cookies with specific certificate reuse",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://github.com/bolubey/CVE-2026-0257"],
    "patch_available": true,
    "sources": ["https://security.paloaltonetworks.com/CVE-2026-0257", "https://www.rapid7.com/blog/post/etr-rapid7-observed-exploitation-of-pan-os-globalprotect-authentication-bypass-vulnerability-cve-2026-0257/", "CISA KEV JSON feed"]
  },
  {
    "cve": "CVE-2026-40965",
    "cvss": "10.0",
    "vendor": "Cloud Foundry Foundation",
    "product": "UAA",
    "affected_versions": "uaa_release v76.12.0-v78.12.0; CF Deployment v30.0.0-v56.0.0 when EC JWT signing keys are used",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://www.cloudfoundry.org/blog/cve-2026-40965-uaa-ec-private-key-disclosure/", "NVD 24-hour CVE feed"]
  },
  {
    "cve": "CVE-2026-44211",
    "cvss": "9.6",
    "vendor": "Cline",
    "product": "Cline Kanban server / AI coding agent service",
    "affected_versions": "2.13.0 and prior per NVD/current reporting",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://github.com/cline/cline/security/advisories/GHSA-5c57-rqjx-35g2"],
    "patch_available": true,
    "sources": ["https://github.com/cline/cline/security/advisories/GHSA-5c57-rqjx-35g2", "https://advisories.gitlab.com/npm/cline/CVE-2026-44211/"]
  },
  {
    "cve": "CVE-2026-8732",
    "cvss": "9.8",
    "vendor": "WP Maps Pro / FlipperCode",
    "product": "WP Maps Pro WordPress plugin",
    "affected_versions": "<= 6.1.0 per public PoCs/reporting",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": false,
    "poc_links": ["https://sploitus.com/exploit?id=105190B4-DF97-59F6-91BF-BF55716FCF79", "https://github.com/p3Nt3st3r-sTAr/CVE-2026-8732-POC"],
    "patch_available": true,
    "sources": ["https://sploitus.com/exploit?id=105190B4-DF97-59F6-91BF-BF55716FCF79", "https://threat-modeling.com/vulnerability-intelligence-report-june-1-2026/"]
  },
  {
    "cve": "CVE-2026-27606",
    "cvss": "High",
    "vendor": "Rollup",
    "product": "Rollup JavaScript module bundler",
    "affected_versions": "<2.80.0 || >=3.0.0 <3.30.0 || >=4.0.0 <4.59.0",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://github.com/rollup/rollup/security/advisories/GHSA-mw96-cpmx-2vgc"],
    "patch_available": true,
    "sources": ["https://github.com/rollup/rollup/security/advisories/GHSA-mw96-cpmx-2vgc", "https://nvd.nist.gov/vuln/detail/CVE-2026-27606", "https://osv.dev/vulnerability/CVE-2026-27606"]
  },
  {
    "cve": "CVE-2026-20182",
    "cvss": "Critical operational priority",
    "vendor": "Cisco",
    "product": "Catalyst SD-WAN Controller / Manager",
    "affected_versions": "Affected releases per Cisco advisory",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://sec.cloudapps.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-sdwan-rpa2-v69WY2SW", "CISA KEV JSON feed"]
  }
]
```

## Recommended Actions - Ranked

1. Emergency patch and hunt: Windows domain controllers for CVE-2026-41089; prioritize systems not fully updated from May 2026 Patch Tuesday.
2. Emergency patch and exposure reduction: Oracle WebLogic CVE-2024-21182; meet or beat CISA's 2026-06-04 KEV due date and restrict T3/IIOP.
3. Emergency perimeter remediation: PAN-OS GlobalProtect CVE-2026-0257; patch, disable authentication override or isolate certs, review VPN logins since 2026-05-17.
4. Validate and rotate identity secrets: Cloud Foundry UAA CVE-2026-40965; patch, rotate EC JWT signing keys, invalidate potentially affected tokens.
5. Patch developer tooling and local AI-agent services: Cline CVE-2026-44211, Rollup CVE-2026-27606, GitHub Enterprise Server 3.20.3, GitLab 19.0.1/18.11.4/18.10.7.
6. Patch exposed middleware: IBM WebSphere critical set and Cisco SD-WAN advisories; prioritize Internet-facing and externally reachable management planes.
7. Inspect WordPress estates for WP Maps Pro CVE-2026-8732; update to 6.1.1+, audit admin users and web uploads.
8. Harden Linux multi-user and CI hosts against public LPE chains: apply kernel updates for PinTheft/Dirty Frag/CIFSwitch-class issues; disable unused RDS/CIFS/io_uring exposure after compatibility review.
9. Monitor ransomware TTPs associated with The Gentlemen/Storm-2697: WMI, PsExec, scheduled task fan-out, backup service termination, shadow copy deletion, hidden SMB shares, and large outbound exfiltration.
10. Treat new GitHub PoC repositories as hostile until reviewed; do not clone or run untrusted exploit repositories on analyst workstations.
