# Security Intelligence Report

**Automation:** daily-security-intelligence-report
**Run ID:** 03015b72-ed4b-4a70-ae12-7df8f53b90ea
**Report time (UTC):** 2026-06-03T07:06:33Z
**Analyst window:** 2026-06-03T06:00:00Z to 2026-06-03T07:30:00Z
**Confidence methodology:** High = multiple primary sources agree; Medium = single authoritative source or strong secondary correlation; Low = indicator only (GitHub PoC, Sploitus index, unvalidated exploit repo).

---

## Executive Summary

| Metric | Count / Status |
|--------|----------------|
| CVEs published (current hour) | 1 |
| CVEs published (2026-06-03 day-to-date) | 14 |
| CVEs published (rolling 24h) | 215 |
| Critical CVEs (24h, CVSS >= 9.0) | 11 |
| CISA KEV catalog version | 2026.06.02 (no change this hour) |
| New KEV additions (prior 24h) | CVE-2022-0492, CVE-2025-48595 |
| Active exploitation signals | Netlogon CVE-2026-41089 (Belgian CCB); carry-forward KEV/exploited set |
| New malware campaigns | Miasma npm worm (Red Hat); SVG phishing wave (SANS ISC) |
| Important vendor advisories | CISA KEV bulletin (2026-06-02); Red Hat RHSB-2026-006; Android June 2026 bulletin |

**Highest-priority actions today:** Meet **five CISA KEV deadlines on 2026-06-03** (legacy Microsoft + Defender). Patch **domain controllers** for **CVE-2026-41089** (Netlogon RCE, exploitation warning). Remediate **CVE-2022-0492** and **CVE-2025-48595** (KEV due 2026-06-05). Audit **@redhat-cloud-services** npm installs for Miasma compromise.

---

## Top Vulnerabilities

### 1. CVE-2026-41089 - Windows Netlogon RCE (Critical)

| Field | Value |
|-------|-------|
| Severity | CVSS 9.8 (Critical) |
| Affected software | Windows Server 2016 through 2025 (Netlogon / CLDAP) |
| Exploit available | Public GitHub indicators (`hnytgl/CVE-2026-41089`, `0xABCD01/CVE-2026-41089`); not independently validated |
| Active exploitation | **Yes** - Belgian Centre for Cybersecurity (CCB) exploitation warning (2026-05-29 advisory); **not** CISA KEV-listed as of 2026.06.02 |
| KEV listed | No |
| Patch available | Yes - Microsoft cumulative updates per MSRC |
| Confidence | **High** (active exploitation), **Medium** (public PoC functionality) |
| Recommended action | Emergency patch all domain controllers; restrict CLDAP/Netlogon exposure; monitor for anomalous DC authentication |

### 2. CVE-2026-20182 - Cisco Catalyst SD-WAN Auth Bypass (Critical)

| Field | Value |
|-------|-------|
| Severity | CVSS 10.0 |
| Affected software | Cisco Catalyst SD-WAN Controller and Manager |
| Exploit available | Yes - Sploitus/Metasploit indicators; Rapid7 analysis |
| Active exploitation | Yes - CISA KEV; Emergency Directive 26-03 |
| KEV listed | Yes (due 2026-05-17, overdue) |
| Patch available | Yes - Cisco advisory |
| Confidence | **High** |
| Recommended action | Apply Cisco fixes per ED 26-03; hunt for unauthorized admin sessions |

### 3. CVE-2026-41940 - cPanel/WHM Auth Bypass (Critical)

| Field | Value |
|-------|-------|
| Severity | CVSS 9.8 |
| Affected software | cPanel and WHM (post 11.40) |
| Exploit available | Yes - Metasploit module, PacketStorm, multiple GitHub PoCs |
| Active exploitation | Yes - CISA KEV; known ransomware campaign use |
| KEV listed | Yes |
| Patch available | Yes - WebPros security update |
| Confidence | **High** |
| Recommended action | Upgrade to patched builds; assume compromise if internet-exposed and unpatched |

### 4. CVE-2026-0257 - Palo Alto PAN-OS Auth Bypass (Critical)

| Field | Value |
|-------|-------|
| Severity | CVSS 9.1 |
| Affected software | PAN-OS GlobalProtect portal/gateway |
| Exploit available | Yes - public PoCs on GitHub |
| Active exploitation | Yes - vendor confirmed attacks; CISA KEV |
| KEV listed | Yes (due 2026-06-01, overdue) |
| Patch available | Yes |
| Confidence | **High** |
| Recommended action | Apply Palo Alto mitigations/patches immediately |

### 5. CVE-2022-0492 - Linux Kernel cgroups Privilege Escalation (High)

| Field | Value |
|-------|-------|
| Severity | CVSS 7.8 |
| Affected software | Linux Kernel (cgroups v1 release_agent) |
| Exploit available | Public techniques; container escape context |
| Active exploitation | Yes - **new CISA KEV addition 2026-06-02** |
| KEV listed | Yes (due **2026-06-05**) |
| Patch available | Yes - kernel mitigations per vendor |
| Confidence | **High** (KEV) |
| Recommended action | Apply kernel/vendor mitigations; restrict unprivileged cgroup usage in containers |

### 6. CVE-2025-48595 - Android Framework Integer Overflow (High)

| Field | Value |
|-------|-------|
| Severity | CVSS 8.4 |
| Affected software | Android Framework |
| Exploit available | Vendor bulletin; limited public PoC |
| Active exploitation | Yes - **new CISA KEV addition 2026-06-02** |
| KEV listed | Yes (due **2026-06-05**) |
| Patch available | Yes - Android 2026-06-01 security bulletin |
| Confidence | **High** (KEV) |
| Recommended action | Deploy June 2026 Android security patch level to managed devices |

### 7. CVE-2024-21182 - Oracle WebLogic (High)

| Field | Value |
|-------|-------|
| Severity | CVSS 7.5 |
| Affected software | Oracle WebLogic Server |
| Exploit available | Historical; actively targeted |
| Active exploitation | Yes - CISA KEV (added 2026-06-01) |
| KEV listed | Yes (due **2026-06-04**) |
| Patch available | Yes - Oracle July 2024 CPU |
| Confidence | **High** |
| Recommended action | Patch before 2026-06-04 KEV deadline; restrict T3/IIOP |

### 8. CVE-2026-50052 - Varnish Cache HTTP/2 DoS (New this hour)

| Field | Value |
|-------|-------|
| Severity | Pending NVD CVSS (published 2026-06-03 ~07:00 UTC) |
| Affected software | Varnish Cache before 9.0.3; Vinyl Cache before 9.0.1 |
| Exploit available | No public PoC observed |
| Active exploitation | Not observed |
| KEV listed | No |
| Patch available | Yes - upgrade to 9.0.3 / 9.0.1 |
| Confidence | **Medium** (NVD primary) |
| Recommended action | Patch reverse-proxy/CDN tiers running Varnish; monitor for HTTP/2 abuse |

### 9. CVE-2026-25643 - Frigate NVR RCE (Critical)

| Field | Value |
|-------|-------|
| Severity | CVSS 9.1 |
| Affected software | Frigate NVR <= 0.16.3 |
| Exploit available | **New** - `DyniePro/CVE-2026-25643` pushed 2026-06-03T06:56:57Z (unvalidated) |
| Active exploitation | Not confirmed |
| KEV listed | No |
| Patch available | Yes - upgrade Frigate |
| Confidence | **Low** (PoC), **Medium** (NVD/vendor) |
| Recommended action | Upgrade Frigate; do not run unvalidated PoC tooling in production |

### 10. CVE-2026-9082 - Drupal Core SQLi (Critical)

| Field | Value |
|-------|-------|
| Severity | CVSS 9.8 |
| Affected software | Drupal Core (PostgreSQL backend) |
| Exploit available | Yes - ExploitDB 52608, Sploitus |
| Active exploitation | Yes - CISA KEV |
| KEV listed | Yes |
| Patch available | Yes - SA-CORE-2026-004 |
| Confidence | **High** |
| Recommended action | Patch Drupal immediately; hunt for webshells on PostgreSQL-backed sites |

---

## Exploits Released

### Sploitus Top 10 (Reconstructed)

**Caveat:** Sploitus homepage is a JavaScript shell; no visible "Exploits of the Week" block in static fetch. Entries below are reconstructed from indexed Sploitus exploit pages and cross-referenced feeds. Treat as **indicators**, not validated weaponization.

| # | CVE / Topic | Affected software | Type | Maturity | PoC | Weaponization |
|---|-------------|-------------------|------|----------|-----|---------------|
| 1 | CVE-2026-46840 | Oracle REST Data Services | Unauth RCE | Weaponized indicator | Yes (Sploitus) | High |
| 2 | CVE-2026-41940 | cPanel/WHM | Auth bypass + RCE | Metasploit + PacketStorm | Yes | High |
| 3 | CVE-2026-42167 | ProFTPD mod_sql | Pre-auth SQLi to RCE | Public PoC | Yes | High |
| 4 | CVE-2026-32710 | MariaDB 11.4.x | Heap overflow / priv esc | Technical PoC | Yes | Medium |
| 5 | CVE-2026-20182 | Cisco SD-WAN | Auth bypass | Framework modules | Yes | High |
| 6 | CVE-2026-9082 | Drupal Core | SQLi / priv esc | ExploitDB-class | Yes | High |
| 7 | CVE-2026-31431 | Linux Kernel | LPE (Copy Fail) | Multiple GitHub | Yes | Medium |
| 8 | CVE-2026-35616 | FortiClient EMS | Auth bypass | Vendor confirmed exploited | Partial | High |
| 9 | CVE-2026-41091 | Microsoft Defender | Local priv esc | KEV | Limited | Medium |
| 10 | CVE-2026-23744 | MCPJam Inspector | Unauth RCE | GitHub PoCs | Yes | Medium |

### ExploitDB Additions

Direct GitLab CSV (`files_exploits.csv`) sorted by `date_published`:

| EDB-ID | Date | CVE | Description |
|--------|------|-----|-------------|
| 52608 | 2026-06-01 | CVE-2026-9082 | Drupal Core 10.5.5 error-based SQL injection |
| 52607 | 2026-06-01 | CVE-2025-10162 | WordPress OrderConvo 14 path traversal |

**No new ExploitDB entries dated 2026-06-03** in direct CSV pull.

### New GitHub PoC / Exploit Indicators (2026-06-03, unvalidated)

| Repository | CVE / Topic | Pushed (UTC) | Notes |
|------------|-------------|--------------|-------|
| DyniePro/CVE-2026-25643 | CVE-2026-25643 Frigate | 06:56:57 | New today; treat as malicious-code risk |
| fartlover37/CVE-2026-2441-PoC | CVE-2026-2441 | 06:52:57 | Unvalidated |
| wutang700/STProcessMonitorBYOVD | CVE-2025-70795 BYOVD | 06:50:55 | Offensive tooling |
| hamzamalik3461/CVE-2026-20841 | CVE-2026-20841 Notepad RCE | 06:50:17 | Unvalidated |
| obrunolima1910/CVE-2026-24061 | CVE-2026-24061 auth bypass | 06:36:52 | Unvalidated |
| jf-gondim/mcp-pwn | CVE-2026-23744 MCPJam | 02:47:15 | Carry-forward |
| hnytgl/CVE-2026-41089 | CVE-2026-41089 Netlogon | 02:59:47 | Carry-forward |

**Warning:** A non-trivial fraction of public CVE PoC repositories contain malicious or trojanized code. Run only in isolated lab environments.

---

## Malware Intelligence

### VX-Underground

| Source | Status |
|--------|--------|
| vx-underground.org | Web root returns 403 in this environment |
| GitHub `vxunderground` org | API accessible |

| Repository | Last push (UTC) | Notes |
|------------|-----------------|-------|
| MalwareSourceCode | 2026-05-30 | Latest commit adds `Python/Stealer.Python.GMBA.Manipulator.7z` - no new malware archive this hour |
| VXUG-Papers | 2026-06-02 | Research updates |
| ThreatIntelligenceDiscordBot | 2026-06-03 | Bot metadata update only |

**Confidence:** Medium (GitHub API only).

### Malware Campaigns and Ransomware

| Campaign | Details | Confidence |
|----------|---------|------------|
| Miasma npm worm | 32 `@redhat-cloud-services` packages compromised 2026-06-01 via hijacked GitHub Actions OIDC; credential-stealing preinstall payload; 300+ downstream GitHub repos reported compromised | High (Red Hat RHSB-2026-006, Wiz, Aikido) |
| SVG phishing wave | SANS ISC reports flood of SVG attachments with XOR-encoded JS redirect to `.cfd` phishing URLs | High (SANS ISC diary 2026-06-02) |
| Carry-forward | Nx Console CVE-2026-48027, TanStack CVE-2026-45321, cPanel CVE-2026-41940 ransomware use | High (CISA KEV) |

### Supply Chain

- **Red Hat Miasma:** Rotate all secrets if affected package versions were installed after 2026-06-01. Red Hat states build analysis shows no customer product impact required; Wiz/Aikido recommend aggressive rotation.
- **TeamPCP pattern:** Attack mirrors prior TanStack/Nx OIDC abuse with valid SLSA attestations.

### MalwareBazaar

API returned 404 without authentication in this run. Browse page scrape did not return 24h stats. **Carry-forward:** Mirai prevalent in prior-hour reporting.

---

## Security Releases

| Vendor | Release / Advisory | Date | Priority items |
|--------|-------------------|------|----------------|
| CISA | KEV catalog v2026.06.02 | 2026-06-02 | Added CVE-2022-0492, CVE-2025-48595 |
| Microsoft | KEV deadlines | **2026-06-03** | CVE-2026-41091, CVE-2026-45498, legacy MS08-067 / IE CVEs |
| Oracle | WebLogic KEV deadline | 2026-06-04 | CVE-2024-21182 |
| Android / Google | 2026-06-01 security bulletin | 2026-06-01 | CVE-2025-48595 |
| Red Hat | RHSB-2026-006 | 2026-06-01 | Miasma npm supply chain |
| Varnish | CVE-2026-50052 fix | 2026-06-03 | Upgrade to 9.0.3 |
| Cisco | SD-WAN advisory carry-forward | May 2026 | CVE-2026-20182 |
| Palo Alto | PAN-OS CVE-2026-0257 | May 2026 | Patches available |
| Drupal | SA-CORE-2026-004 | May 2026 | CVE-2026-9082 |

No new Microsoft Patch Tuesday release detected in the 06:00-07:30 UTC window.

---

## Recommended Actions

Priority ranked highest to lowest:

1. **CISA KEV deadlines today (2026-06-03):** Verify remediation for CVE-2026-41091, CVE-2026-45498 (Microsoft Defender), and legacy Microsoft KEV entries (CVE-2008-4250, CVE-2009-1537, CVE-2009-3459, CVE-2010-0249, CVE-2010-0806).
2. **Emergency - CVE-2026-41089:** Patch all Windows domain controllers; treat Belgian CCB active exploitation warning as actionable.
3. **Overdue KEV - CVE-2026-20182, CVE-2026-0257, CVE-2026-41940:** Complete Cisco SD-WAN, PAN-OS, and cPanel remediation if not done.
4. **KEV due 2026-06-04:** Oracle WebLogic CVE-2024-21182.
5. **KEV due 2026-06-05:** Linux CVE-2022-0492; Android CVE-2025-48595.
6. **Miasma response:** Inventory `@redhat-cloud-services` dependencies; rotate CI/CD and cloud credentials if compromised versions were installed.
7. **New edge exposure:** Patch Varnish CVE-2026-50052; upgrade Frigate for CVE-2026-25643; block untrusted GitHub PoC execution in build pipelines.
8. **Drupal / hosting:** Confirm CVE-2026-9082 and cPanel chains are patched on managed hosting fleets.
9. **Detection:** Monitor Netlogon/CLDAP, SD-WAN admin auth anomalies, GlobalProtect auth bypass, and npm preinstall script execution from Red Hat scopes.

---

## NVD Statistics

| Window | Total | Critical | High | Medium | Low | Unknown |
|--------|-------|----------|------|--------|-----|---------|
| Current hour (06:00-07:30 UTC) | 1 | 0 | 0 | 0 | 0 | 1 |
| 2026-06-03 day-to-date | 14 | 0 | 3 | 7 | 1 | 3 |
| Rolling 24h | 215 | 11 | 67 | 72 | 4 | 61 |

**Hourly publication:** CVE-2026-50052 (Varnish Cache HTTP/2 request parsing deficiency).

---

## Unified Vulnerability Records

```json
[
  {
    "cve": "CVE-2026-41089",
    "cvss": "9.8",
    "vendor": "Microsoft",
    "product": "Windows Netlogon",
    "affected_versions": "Windows Server 2016-2025 before fixed builds per MSRC",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": false,
    "poc_links": ["https://github.com/hnytgl/CVE-2026-41089"],
    "patch_available": true,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2026-41089", "https://msrc.microsoft.com/update-guide/vulnerability/CVE-2026-41089", "https://threat-modeling.com/windows-netlogon-buffer-overflow-cve-2026-41089/"]
  },
  {
    "cve": "CVE-2026-20182",
    "cvss": "10.0",
    "vendor": "Cisco",
    "product": "Catalyst SD-WAN",
    "affected_versions": "Unpatched SD-WAN Controller/Manager per Cisco advisory",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://sploitus.com/?query=CVE-2026-20182"],
    "patch_available": true,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2026-20182", "https://www.cisa.gov/known-exploited-vulnerabilities-catalog"]
  },
  {
    "cve": "CVE-2026-41940",
    "cvss": "9.8",
    "vendor": "WebPros",
    "product": "cPanel and WHM",
    "affected_versions": "Versions after 11.40 before vendor fix",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://sploitus.com/exploit?id=MSF%3AEXPLOIT-MULTI-HTTP-CPANEL_WHM_AUTH_BYPASS_RCE-", "https://github.com/Defacto-ridgepole254/CVE-2026-41940-Exploit-PoC"],
    "patch_available": true,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2026-41940", "https://www.cisa.gov/known-exploited-vulnerabilities-catalog"]
  },
  {
    "cve": "CVE-2026-0257",
    "cvss": "9.1",
    "vendor": "Palo Alto Networks",
    "product": "PAN-OS GlobalProtect",
    "affected_versions": "Per Palo Alto security advisory",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://github.com/bolubey/CVE-2026-0257"],
    "patch_available": true,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2026-0257", "https://security.paloaltonetworks.com/CVE-2026-0257"]
  },
  {
    "cve": "CVE-2022-0492",
    "cvss": "7.8",
    "vendor": "Linux",
    "product": "Kernel cgroups v1",
    "affected_versions": "Unpatched kernels with vulnerable cgroup release_agent",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2022-0492", "https://www.cisa.gov/known-exploited-vulnerabilities-catalog"]
  },
  {
    "cve": "CVE-2025-48595",
    "cvss": "8.4",
    "vendor": "Google",
    "product": "Android Framework",
    "affected_versions": "Devices before June 2026 patch level",
    "exploit_available": false,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2025-48595", "https://source.android.com/docs/security/bulletin/2026/2026-06-01"]
  },
  {
    "cve": "CVE-2024-21182",
    "cvss": "7.5",
    "vendor": "Oracle",
    "product": "WebLogic Server",
    "affected_versions": "Unpatched WebLogic per July 2024 CPU",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2024-21182", "https://www.oracle.com/security-alerts/cpujul2024.html"]
  },
  {
    "cve": "CVE-2026-50052",
    "cvss": "pending",
    "vendor": "Varnish Software",
    "product": "Varnish Cache / Vinyl Cache",
    "affected_versions": "Varnish Cache before 9.0.3; Vinyl before 9.0.1",
    "exploit_available": false,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": [],
    "patch_available": true,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2026-50052"]
  },
  {
    "cve": "CVE-2026-25643",
    "cvss": "9.1",
    "vendor": "Frigate",
    "product": "Frigate NVR",
    "affected_versions": "<= 0.16.3",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://github.com/DyniePro/CVE-2026-25643"],
    "patch_available": true,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2026-25643"]
  },
  {
    "cve": "CVE-2026-9082",
    "cvss": "9.8",
    "vendor": "Drupal",
    "product": "Drupal Core",
    "affected_versions": "8.0 through 11.3.9 with PostgreSQL",
    "exploit_available": true,
    "active_exploitation": true,
    "kev_listed": true,
    "poc_links": ["https://www.exploit-db.com/exploits/52608"],
    "patch_available": true,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2026-9082", "https://www.drupal.org/sa-core-2026-004"]
  },
  {
    "cve": "CVE-2026-46840",
    "cvss": "10.0",
    "vendor": "Oracle",
    "product": "REST Data Services (ORDS)",
    "affected_versions": "24.2.0 through 26.1.0",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": false,
    "poc_links": ["https://sploitus.com/exploit?id=3D6FBB98-36AB-5F6C-BD65-545B7A10A138"],
    "patch_available": true,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2026-46840", "https://sploitus.com/exploit?id=3D6FBB98-36AB-5F6C-BD65-545B7A10A138"]
  },
  {
    "cve": "CVE-2026-31431",
    "cvss": "7.8",
    "vendor": "Linux",
    "product": "Kernel (algif_aead / Copy Fail)",
    "affected_versions": "Kernels before 6.18.22 fix",
    "exploit_available": true,
    "active_exploitation": false,
    "kev_listed": true,
    "poc_links": ["https://github.com/Dullpurple-sloop726/CVE-2026-31431-Linux-Copy-Fail"],
    "patch_available": true,
    "sources": ["https://nvd.nist.gov/vuln/detail/CVE-2026-31431", "https://www.cisa.gov/known-exploited-vulnerabilities-catalog"]
  }
]
```

---

## Sources Consulted

**Tier 1:** NIST NVD API, CISA KEV JSON, Sploitus (indexed), ExploitDB GitLab CSV, GitHub search/API, vxunderground GitHub org
**Tier 2:** Microsoft MSRC references, Cisco/Palo Alto/Oracle/Red Hat advisories, SANS ISC, Android security bulletin
**Threat intel:** Belgian CCB Netlogon warning (secondary), Wiz/Aikido Miasma analysis, SANS ISC SVG phishing diary

**Limitations this run:** Sploitus homepage lacks static exploit-of-week data; vx-underground.org 403; MalwareBazaar API unauthenticated; PacketStorm not queried (historical anti-abuse blocks). GitHub PoCs are indicators only.

---

*End of report - generated by daily-security-intelligence-report automation.*
