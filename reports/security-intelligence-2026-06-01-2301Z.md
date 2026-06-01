# Security Intelligence Daily Report - 2026-06-01 23:01 UTC

## Collection Scope and Caveats

- Report window: 2026-06-01 UTC, with recent high-priority context from the preceding week where exploitation or patch deadlines changed today.
- Primary sources checked: CISA KEV JSON feed, NVD API, GitHub Security Advisories API, vendor advisories, GitHub repository search, ExploitDB/Sploitus/Packet Storm indexed results, VX-Underground GitHub, and security research reporting.
- Source limitations:
  - Sploitus homepage is client-rendered and did not expose an "Exploits of the Week" block to static fetch. The Sploitus Top 10 below is reconstructed from indexed Sploitus exploit pages and deduplicated.
  - VX-Underground web root returned HTTP 403 to automated fetch, but the GitHub profile and repositories were accessible.
  - MalwareBazaar community API returned HTTP 401 from this environment; abuse.ch web documentation was accessible, but recent sample API data was not.
  - GitHub PoC repositories are treated as indicators only. No exploit code was executed or functionally validated.

## Executive Summary

- Total CVEs published in NVD on 2026-06-01 UTC: 339.
- NVD critical findings: 25 with CVSS >= 9.0.
- NVD high findings: 94 with CVSS 7.0-8.9.
- CISA KEV additions today: 1 - CVE-2024-21182 (Oracle WebLogic Server).
- Active exploitation / attacked status:
  - High confidence: CVE-2024-21182 is newly listed in CISA KEV.
  - High confidence: CVE-2026-0257 PAN-OS GlobalProtect is marked "ATTACKED" by Palo Alto Networks and was added to CISA KEV on 2026-05-29.
  - High confidence: CVE-2026-20182 Cisco Catalyst SD-WAN has Cisco PSIRT reporting limited exploitation and CISA KEV inclusion.
  - Medium confidence: CVE-2026-41089 Windows Netlogon RCE has public reporting citing Belgium CCB exploitation warnings; Microsoft/NVD confirmed severity and patch, but Microsoft advisory fetch did not confirm active exploitation in this collection.
- New malware/supply-chain activity:
  - Miasma / Mini Shai-Hulud-style credential-stealing worm compromised `@redhat-cloud-services` npm packages on 2026-06-01, reported by Aikido, StepSecurity, Wiz, and Panther.
  - VX-Underground GitHub added `Python/Stealer.Python.GMBA.Manipulator.7z` to `vxunderground/MalwareSourceCode` on 2026-05-30.
- Important vendor/security releases observed: Oracle WebLogic KEV remediation, Palo Alto PAN-OS fixed releases, Cisco SD-WAN emergency guidance, Cloud Foundry UAA fix, IBM WebSphere interim fixes, Apache Solr/ActiveMQ advisories, HP Poly VoIP RCE disclosure, GitHub advisories for Vitest/PraisonAI/Cline/CloudPirates, Google Android XR June bulletin, Fortinet May PSIRT advisories.

## Top Vulnerabilities

### 1. CVE-2024-21182 - Oracle WebLogic Server - KEV added today

- Severity: High, CVSS 7.5.
- Affected software: Oracle WebLogic Server 12.2.1.4.0 and 14.1.1.0.0.
- Vulnerability type: unauthenticated network-accessible information disclosure / unauthorized access to critical data.
- Exploit availability: not confirmed in this run; KEV listing implies known exploitation.
- Active exploitation: yes, by CISA KEV classification.
- KEV listed: yes, added 2026-06-01; due date 2026-06-04.
- Patch available: yes, Oracle July 2024 CPU.
- Confidence: High.
- Recommended action: patch immediately or isolate T3/IIOP exposure; verify WebLogic versions and Oracle CPU application status.
- Sources: CISA KEV JSON, NVD, Oracle July 2024 CPU.

```json
{
  "cve": "CVE-2024-21182",
  "cvss": "7.5",
  "vendor": "Oracle",
  "product": "WebLogic Server",
  "affected_versions": "12.2.1.4.0, 14.1.1.0.0",
  "exploit_available": false,
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

### 2. CVE-2026-0257 - Palo Alto Networks PAN-OS GlobalProtect authentication bypass

- Severity: Critical in CVSS v3.1 (9.1) / High in CVSS v4.0 (7.8).
- Affected software: PAN-OS 10.2, 11.1, 11.2, 12.1 and Prisma Access versions with GlobalProtect portal/gateway plus authentication override cookie exposure.
- Vulnerability type: authentication bypass permitting unauthorized VPN connection.
- Exploit availability: exploitation attempts confirmed by vendor; no public PoC validated.
- Active exploitation: yes; Palo Alto marks exploit maturity "ATTACKED".
- KEV listed: yes, added 2026-05-29; CISA due date 2026-06-01.
- Patch available: yes, multiple hotfix/fixed releases.
- Confidence: High.
- Recommended action: upgrade to fixed PAN-OS/Prisma Access release; disable authentication override cookies or deploy dedicated cookie certificate as interim mitigation.
- Sources: Palo Alto advisory, CISA KEV, NVD.

### 3. CVE-2026-20182 - Cisco Catalyst SD-WAN Controller / Manager authentication bypass

- Severity: Critical, CVSS 10.0.
- Affected software: Cisco Catalyst SD-WAN Controller and Manager.
- Vulnerability type: unauthenticated remote authentication bypass leading to administrative privileges.
- Exploit availability: no public PoC validated.
- Active exploitation: yes; Cisco PSIRT reports limited exploitation and CISA KEV lists the issue.
- Patch available: yes, fixed software releases and Cisco SD-WAN Cloud remediation.
- Confidence: High.
- Recommended action: apply Cisco fixed releases, retain logs, run Cisco IOC guidance, and open TAC case if exposure or compromise is suspected.
- Sources: Cisco PSIRT, CISA KEV, NVD.

### 4. CVE-2026-41089 - Microsoft Windows Netlogon RCE

- Severity: Critical, CVSS 9.8.
- Affected software: supported Windows Server versions, especially domain controllers exposing Netlogon.
- Vulnerability type: stack-based buffer overflow allowing unauthenticated remote code execution over the network.
- Exploit availability: no public PoC validated in this run.
- Active exploitation: medium-confidence external reporting cites Belgium CCB active exploitation warning; Microsoft advisory active-exploitation status was not retrievable via static fetch.
- Patch available: yes, Microsoft May 2026 updates.
- Confidence: Medium for exploitation status, High for severity/patch.
- Recommended action: prioritize all domain controllers; restrict Netlogon/RPC reachability, monitor anomalous domain-controller traffic, and confirm May patches.
- Sources: NVD, public reporting referencing CCB, Microsoft Security Update Guide URL.

### 5. CVE-2026-40965 - Cloud Foundry UAA EC private key disclosure

- Severity: Critical, CVSS 10.0.
- Affected software: UAA v76.12.0 through v78.12.0; cf-deployment v30.0.0 through v56.0.0 when EC keys are used for JWT signing.
- Vulnerability type: private key exposure via public `/token_keys` endpoint.
- Exploit availability: exploit is trivial if endpoint and EC signing configuration are present; no separate PoC required.
- Active exploitation: not observed.
- Patch available: yes, uaa_release v78.13.0+ and cf-deployment v56.1.0+.
- Confidence: High.
- Recommended action: upgrade, rotate exposed EC signing keys, invalidate/reissue tokens, and check whether RSA-only deployments are unaffected.
- Sources: Cloud Foundry advisory, NVD.

### 6. CVE-2026-44825 - Apache Solr hardcoded BasicAuth credentials

- Severity: Critical/High; NVD recorded both 9.8 and 8.1 CVSS v3.1 metrics.
- Affected software: Apache Solr 9.4.0 through 9.10.1 and 10.0.0 when `bin/solr auth enable` bootstrapped BasicAuth and template accounts were not changed.
- Vulnerability type: hardcoded/default credentials granting full cluster administration.
- Exploit availability: credentials/condition knowledge may be sufficient; no distinct PoC needed.
- Active exploitation: not observed.
- Patch available: future Solr 9.11.0 / 10.1.0 noted; immediate mitigation is to remove or reset `superadmin`, `admin`, `search`, and `index` template users.
- Confidence: High.
- Recommended action: inspect `security.json` immediately for template users and rotate credentials; monitor Solr admin/API access.
- Sources: oss-sec, NVD, Apache issue SOLR-18233 reference.

### 7. CVE-2026-9311 / CVE-2026-9319 / CVE-2026-9330 - IBM WebSphere Application Server RCE cluster

- Severity:
  - CVE-2026-9311: Critical, CVSS 9.0.
  - CVE-2026-9319: Critical, CVSS 9.0.
  - CVE-2026-9330: High, CVSS 8.5.
- Affected software: IBM WebSphere Application Server 8.5 and 9.0.
- Vulnerability type: security-control bypass and deserialization issues leading to remote code execution.
- Exploit availability: no public PoC validated.
- Active exploitation: not observed.
- Patch available: IBM interim fixes for APAR PH71453/PH71454; fix packs targeted for 3Q2026.
- Confidence: High.
- Recommended action: apply interim fixes now for internet-facing or high-trust WebSphere deployments.
- Sources: IBM support bulletins, NVD.

### 8. CVE-2026-0826 - HP Poly Voice products unauthenticated RCE

- Severity: Critical, CVSS 9.2.
- Affected software: HP Poly Voice products on Linux platform when ICE is enabled.
- Vulnerability type: buffer overflow leading to unauthenticated RCE.
- Exploit availability: Rapid7 reports a Metasploit exploit module was developed to demonstrate root-level exploitation.
- Active exploitation: not observed.
- Patch available: HP support bulletin referenced by NVD/Rapid7.
- Confidence: High.
- Recommended action: patch Poly VVX/Trio/affected voice devices; disable/limit ICE where possible; restrict management and signaling network exposure.
- Sources: NVD, HP support bulletin, Rapid7 research.

### 9. CVE-2026-49121 - AI Tensor Engine for ROCm (AITER) pickle deserialization RCE

- Severity: Critical, CVSS 9.2 v4.0; NVD also includes CVSS 8.1 v3.1.
- Affected software: AITER through 0.1.14.
- Vulnerability type: unauthenticated remote code execution via `pickle.loads` in `MessageQueue.recv()` over ZMQ.
- Exploit availability: GitHub issue includes a proof-of-concept and VulnCheck advisory describes the exploit path.
- Active exploitation: not observed.
- Patch available: not confirmed; issue and PR tracker were open/known issue at collection time.
- Confidence: High for vulnerability details, Medium for patch status.
- Recommended action: isolate ROCm inference cluster networks, block untrusted ZMQ reachability, avoid multi-tenant exposure, and track upstream fix.
- Sources: NVD, ROCm GitHub issue #3076, VulnCheck advisory.

### 10. CVE-2026-44211 - Cline Kanban cross-origin WebSocket hijacking

- Severity: Critical, GitHub advisory CVSS 9.6; Oasis report cites CVSS 9.7.
- Affected software: Cline Kanban/local server workflow; GitLab advisory describes `kanban` npm package usage by `cline`.
- Vulnerability type: localhost WebSocket service lacks Origin validation/authentication; malicious web pages can read workspace data and inject input to AI-agent terminals.
- Exploit availability: public advisory contains JavaScript proof-of-concept snippets.
- Active exploitation: not observed.
- Patch available: third-party research says fixed in Cline 0.1.66; GitHub advisory fetch did not expose all version fields.
- Confidence: High.
- Recommended action: update Cline/kanban; disable Kanban/local listener when browsing; inventory all local AI/developer tools exposing localhost services.
- Sources: GitHub GHSA-5c57-rqjx-35g2, GitLab Advisory Database, Oasis Security.

### 11. CVE-2026-45131 / CVE-2026-45132 - CloudPirates Helm Charts GitHub Actions secret exposure

- Severity: Critical, CVSS 10.0 each.
- Affected software: CloudPirates `helm-charts` workflows before commit `fcf9302`.
- Vulnerability type: privileged GitHub Actions workflows expose Docker credentials, PAT, and SSH signing key to fork-controlled code.
- Exploit availability: exploit path is described in GHSA; no runtime PoC needed.
- Active exploitation: not observed.
- Patch available: yes, commit `fcf9302`.
- Confidence: High.
- Recommended action: rotate all potentially exposed CI/CD credentials, audit releases/images produced during exposure window, and add approval gates for privileged workflows.
- Sources: GitHub advisories GHSA-c47r-c7gw-cvph and GHSA-r874-j8fr-x2pj, NVD.

### 12. CVE-2026-47429 / CVE-2026-47428 - Vitest UI/browser critical vulnerabilities

- Severity:
  - CVE-2026-47429: Critical, GitHub CVSS 9.8.
  - CVE-2026-47428: Critical, GitHub CVSS 9.6.
- Affected software:
  - `vitest` before 4.1.0 for UI server arbitrary file read/execution.
  - `@vitest/browser` affected 4.0.17-4.1.5 and 5.0.0-beta.0-5.0.0-beta.2 for inline script injection via `otelCarrier`.
- Exploit availability: no public working exploit validated; vulnerable dev servers are often reachable on developer hosts/CI.
- Active exploitation: not observed.
- Patch available: yes via GitHub advisory fixed ranges.
- Confidence: High from GitHub Security Advisory API.
- Recommended action: upgrade Vitest packages; ensure dev/test servers are not exposed to untrusted networks.
- Sources: GitHub Security Advisories API.

## Exploits Released

### Sploitus Top 10 - reconstructed from indexed exploit pages

| Rank | CVE / topic | Affected software | Exploit type | Maturity | Weaponization potential | Confidence |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | CVE-2026-42945 | NGINX / NGINX Plus, "NGINX Rift" | unauthenticated RCE / heap corruption | multiple Sploitus-indexed PoCs/toolkits | High if underlying CVE is validated in environment | Medium; aggregator-only in this run |
| 2 | CVE-2026-38526 | Webkul Krayin CRM v2.2.x | authenticated RCE via unrestricted PHP upload | Sploitus-indexed PoC | High after credential compromise | Medium |
| 3 | CVE-2026-9082 | Drupal Core PostgreSQL backend | unauthenticated SQL injection PoCs/scanners | multiple Sploitus-indexed PoCs | High for exposed PostgreSQL-backed Drupal | Medium-High; CISA KEV also lists the CVE |
| 4 | CVE-2026-4631 | Cockpit 327-359 | unauthenticated RCE via SSH argument injection | Sploitus-indexed code analysis/PoC | High | Medium |
| 5 | CVE-2026-41651 | PackageKit / "Pack2TheRoot" | local privilege escalation | Sploitus-indexed PoC | Medium; local access required | Medium |
| 6 | CVE-2026-25940 | jsPDF / PDF viewers | crafted PDF JavaScript behavior | Sploitus-indexed PoC generator | Medium; viewer-dependent | Medium |
| 7 | CVE-2026-25964 | Tandoor Recipes <= 2.5.0 | authenticated local file disclosure | Sploitus-indexed PoC; GHSA validated | Medium | High for vuln details |
| 8 | CVE-2026-42897 | Microsoft Exchange Health Checker tool | mitigation blind-spot PoC | Sploitus-indexed PowerShell PoC | Low-Medium; defensive-tool impact | Medium |
| 9 | CVE-2026-29014 | MetInfo CMS <= 8.1 | PHP code injection | Sploitus entry sourced from Packet Storm | High for exposed CMS | Medium |
| 10 | CVE-2026-49491 | Pixa Bank 2.0 | SQL injection | NVD references Packet Storm file | Medium | Medium |

### ExploitDB additions / notable indexed entries

- EDB-52591: Linux kernel "Kukurigu" local privilege-escalation chain using CVE-2026-43284, CVE-2026-43500, and CVE-2026-46300; published 2026-05-29. Treat as high-risk local root PoC requiring careful validation.
- EDB-52556: GNU InetUtils `telnetd` 2.7 buffer overflow, CVE-2026-32746; published 2026-05-07. PoC demonstrates overflow and response analysis; code execution not proven by the entry.
- EDB-52542: Google Chrome CSSFontFeatureValuesMap use-after-free, CVE-2026-2441; published 2026-04-30. Entry claims zero-day exploitation; prioritize Chromium patching where not already current.

### New GitHub PoC / exploit indicators

Recent GitHub repository search for `CVE-2026` returned multiple newly updated/created repositories. These are unvalidated and may be malicious or inaccurate:

- `obrunolima1910/CVE-2026-24061` - claims GNU inetutils-telnetd remote auth bypass/root shell; updated 2026-06-01.
- `0xBlackash/CVE-2026-20841` and related repos - claim Windows Notepad RCE; newly created/updated 2026-06-01.
- `j0xh-sec/CVE-2026-49009` - claims Mender Server authenticated path traversal to RCE; updated 2026-06-01.
- `Defacto-ridgepole254/CVE-2026-41940-Exploit-PoC` - claims cPanel/WHM authentication bypass PoC; updated 2026-06-01; CVE is KEV-listed with known ransomware use.
- `Dullpurple-sloop726/CVE-2026-31431-Linux-Copy-Fail`, `Liverwortenuresis371/copyfail-rs`, and `tematemaru/CVE-2026-31431-simple-test` - Linux Copy Fail/KEV local privilege escalation PoC/test indicators.

## Malware Intelligence

### VX-Underground

- Website fetch: blocked by 403 during automated collection.
- GitHub profile/repositories: accessible.
- Recent activity:
  - `vxunderground/MalwareSourceCode` updated 2026-05-30 with `Python/Stealer.Python.GMBA.Manipulator.7z`.
  - Repository description: collection of malware source code for multiple platforms and languages.
- Assessment: research/archive addition, not necessarily a new active campaign. Treat as useful for detection engineering and reverse-engineering watchlists.
- Confidence: High for repository update, Low for operational threat activity.

### Miasma / Mini Shai-Hulud-style npm supply-chain compromise

- Reporting from Aikido, StepSecurity, Wiz, and Panther indicates a 2026-06-01 compromise of `@redhat-cloud-services` npm packages.
- Reported scope: approximately 32 packages, with reporting varying between 95 and 96 compromised versions; weekly downloads estimated from about 80,000 to 116,991 depending on source.
- Malware behavior:
  - install/preinstall execution;
  - multi-stage obfuscation;
  - credential harvesting from GitHub Actions, AWS, GCP, Azure, Kubernetes, Vault, npm, PyPI, Docker, SSH keys, GPG keys, `.env` files, and CI providers;
  - self-propagation using harvested npm tokens and `bypass_2fa`;
  - valid SLSA/provenance artifacts in some reports because publishing abused GitHub Actions OIDC/trusted publishing.
- Confidence: High due to multiple independent reports.
- Recommended action: if affected packages were installed since 2026-06-01, assume environment compromise; isolate hosts/runners, preserve evidence, rotate credentials in dependency order, and verify package lockfiles and caches.

### Ransomware activity

- Breachsense May 2026 ransomware report: 646 claimed victims, 61 active groups, 73 countries, 59 industries; Qilin led with 101 claimed victims, followed by DragonForce at 41, with SafePay and Bavaqai each at 25.
- Qilin remains a major operational concern, with multiple sources reporting high activity and EDR-killer/BYOVD tradecraft.
- DragonForce continues to appear in current victim-list reporting; recent healthcare victim claims require independent confirmation before treating as confirmed breach events.
- Confidence: Medium-High for aggregate May metrics; Medium for individual leak-site victim claims unless victim/vendor confirms.

## Security Releases and Vendor Advisories

### Microsoft

- CVE-2026-41089 Windows Netlogon RCE: May 2026 patch, CVSS 9.8; external reporting indicates possible active exploitation.
- CVE-2026-47294 Microsoft SharePoint: NVD published 2026-06-01; deserialization of untrusted data allows an authorized attacker to execute code over a network, CVSS 8.0. MSRC page is dynamically rendered and did not provide details via static fetch.

### Cisco

- CVE-2026-20182 Catalyst SD-WAN Controller/Manager authentication bypass: CISA KEV, limited exploitation, fixed releases and IOC guidance.
- Cisco IoT Field Network Director: CVE-2026-20167/20168/20169 for DoS, path traversal, and command injection; fixed in 5.0.0-117.
- Cisco Unity Connection: CVE-2026-20034 RCE and CVE-2026-20035 SSRF; fixed releases/patches available.
- Cisco SG350/SG350X SNMP DoS CVE-2026-20185: no patch because products are beyond software maintenance; replace or isolate.

### Fortinet

- FG-IR-26-134: FortiNDR SQL injection; published 2026-05-12; fixed in FortiNDR 7.6.3 / 7.4.10 or migration.
- FG-IR-26-125: FortiOS/FortiSwitchManager CAPWAP missing authentication; local subnet attacker under non-default configuration; fixed releases available.
- FG-IR-26-122: FortiOS/FortiPAM/FortiProxy/FortiSwitchManager CLI path traversal; fixed releases available; Fortinet notes virtual patch `FG-VD-59270.0day`.
- FG-IR-26-060: FortiCloud SSO authentication bypass was exploited by two malicious FortiCloud accounts earlier in 2026; Fortinet disabled/re-enabled server-side controls and requires upgrades.

### VMware / Broadcom

- Broadcom security advisory portal was accessible only as a landing page and showed access restrictions; no specific new VMware/Broadcom critical advisory was validated in this run.
- Recommendation: monitor Broadcom Support Portal with authenticated enterprise access for product-specific VMSA updates.

### GitHub / open source ecosystem

- GitHub Security Advisories published 2026-06-01 include critical Vitest, PraisonAI, and other development-tool issues.
- Notable:
  - CVE-2026-47429: Vitest UI server arbitrary file read/execution, CVSS 9.8.
  - CVE-2026-47428: `@vitest/browser` inline-script issue, CVSS 9.6.
  - CVE-2026-47410 / CVE-2026-47413 and related PraisonAI advisories: default JWT signing key, workspace takeover, sandbox escape, unauthenticated agent-server exposures.
  - CVE-2026-44211: Cline Kanban cross-origin WebSocket hijack.
  - CVE-2026-45131 / CVE-2026-45132: CloudPirates Helm Charts GitHub Actions secret exposure.

### GitLab

- No June 2026 GitLab security release was validated in search results.
- Latest relevant result observed: GitLab patch release 18.10.3 / 18.9.5 / 18.8.9 on 2026-04-08 containing multiple security fixes.

### Google / Android

- Android XR Security Bulletin published 2026-06-01 includes CVE-2026-0072, an Android 14 elevation-of-privilege issue rated High.
- May 2026 Android bulletin included CVE-2026-0073 critical RCE in `adbd`; ensure devices are at May/June security patch level as applicable.

### Oracle

- Oracle July 2024 CPU is relevant today because CISA added WebLogic CVE-2024-21182 to KEV. Oracle explicitly recommends applying CPUs without delay due to exploitation of already-patched vulnerabilities.

### Apache

- Apache Solr CVE-2026-44825: hardcoded BasicAuth template users; immediate credential/user mitigation required, future fixed versions noted.
- Apache ActiveMQ CVE-2026-49157: Jolokia default authorization grants non-admin accounts management operations; upgrade to 5.19.7 or 6.2.6.
- Apache ActiveMQ CVE-2026-45505 / CVE-2026-42588 class of Jolokia/code-injection issues: upgrade to fixed 5.19.x / 6.2.x streams.

### Cloud Foundry

- CVE-2026-40965 UAA EC private-key exposure: upgrade to uaa_release v78.13.0+ or cf-deployment v56.1.0+ and rotate keys.

### IBM

- WebSphere Application Server bulletins published 2026-06-01 for CVE-2026-9311, CVE-2026-9319, CVE-2026-9330; apply interim fixes.

### HP / Rapid7

- CVE-2026-0826 HP Poly Voice products unauthenticated RCE: Rapid7 reports Metasploit module; apply HP fixes and segment VoIP devices.

## Recommended Actions - ranked

1. Emergency patch or isolate CISA KEV and actively exploited edge/infrastructure systems: Oracle WebLogic CVE-2024-21182, PAN-OS CVE-2026-0257, Cisco SD-WAN CVE-2026-20182, and Drupal CVE-2026-9082 if present.
2. Patch Windows domain controllers for CVE-2026-41089 and hunt for Netlogon/RPC anomalies, even where active exploitation is not yet vendor-confirmed.
3. Investigate `@redhat-cloud-services` npm exposure immediately; rotate secrets from any developer host, CI runner, or build environment that installed affected versions on/after 2026-06-01.
4. Apply IBM WebSphere interim fixes for CVE-2026-9311/9319/9330 and restrict JAX-WS/SAML-exposed paths until fixed.
5. Remediate Apache Solr BasicAuth template credentials now by removing or resetting `superadmin`, `admin`, `search`, and `index` users; monitor admin API access.
6. Upgrade Cloud Foundry UAA/cf-deployment for CVE-2026-40965 and rotate EC JWT signing material.
7. Patch HP Poly voice devices for CVE-2026-0826 and restrict VoIP device management/signaling planes.
8. Isolate ROCm/AITER cluster networks and track/remediate CVE-2026-49121; do not expose ZMQ/cluster coordination surfaces to untrusted tenants.
9. Upgrade development tooling with critical advisories: Vitest, Cline/kanban, PraisonAI, and affected CI/CD workflow repositories; audit localhost listeners and privileged GitHub Actions workflows.
10. Treat all newly discovered GitHub PoC repositories with caution: inspect in sandboxes only, do not execute untrusted exploit code on analyst workstations, and prefer vendor/advisory validation over repository claims.

## Source Index

- CISA KEV JSON: https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json
- NVD API / detail pages: https://nvd.nist.gov/
- Oracle July 2024 CPU: https://www.oracle.com/security-alerts/cpujul2024.html
- Palo Alto CVE-2026-0257: https://security.paloaltonetworks.com/CVE-2026-0257
- Cisco SD-WAN advisory: https://sec.cloudapps.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-sdwan-rpa2-v69WY2SW
- Cloud Foundry UAA advisory: https://www.cloudfoundry.org/blog/cve-2026-40965-uaa-ec-private-key-disclosure/
- Apache Solr oss-sec: https://seclists.org/oss-sec/2026/q2/731
- IBM WebSphere CVE-2026-9319: https://www.ibm.com/support/pages/node/7274738
- IBM WebSphere CVE-2026-9311/CVE-2026-9330: https://www.ibm.com/support/pages/node/7274733
- ROCm AITER issue: https://github.com/ROCm/aiter/issues/3076
- VulnCheck AITER advisory: https://www.vulncheck.com/advisories/ai-tensor-engine-for-rocm-aiter-unauthenticated-rce-via-messagequeue-recv-pickle-deserialization
- Cline GHSA: https://github.com/cline/cline/security/advisories/GHSA-5c57-rqjx-35g2
- CloudPirates GHSAs: https://github.com/CloudPirates-io/helm-charts/security/advisories/GHSA-c47r-c7gw-cvph and https://github.com/CloudPirates-io/helm-charts/security/advisories/GHSA-r874-j8fr-x2pj
- Tandoor GHSA: https://github.com/TandoorRecipes/recipes/security/advisories/GHSA-6485-jr28-52xx
- Android XR June 2026 bulletin: https://source.android.com/docs/security/bulletin/xr/2026/2026-06-01
- Fortinet PSIRT portal: https://fortiguard.fortinet.com/psirt
- GitHub Security Advisories API: https://api.github.com/advisories
- VX-Underground GitHub: https://github.com/vxunderground
- Aikido Miasma reporting: https://www.aikido.dev/blog/red-hat-npm-packages-compromised-credential-stealing-worm
- StepSecurity Miasma reporting: https://www.stepsecurity.io/blog/multiple-redhat-cloud-services-npm-packages-compromised
- Wiz Miasma reporting: https://www.wiz.io/blog/miasma-supply-chain-attack-targeting-redhat-npm-packages
- Panther Miasma reporting: https://panther.com/blog/mini-shai-hulud-supply-chain-compromise-of-redhat-cloud-services-npm-packages-via-github-actions-oidc-abuse
- Breachsense May 2026 ransomware report: https://www.breachsense.com/ransomware-reports/may-2026/
