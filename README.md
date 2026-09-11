<div align="center">

# 🛡️💝 ZeroHack CVE Intelligence

**Built with ❤️ by ZeroHack for a safer tomorrow 🛡️**

**Production-grade, AI-enriched vulnerability intelligence — engine-ready JSON for SOCs, SIEMs, threat hunters and security automation.**

Open data from the [ZeroHack](https://zerohack.org) CVE pipeline: **10+ independent sources**, merged into a single non-destructive record, then **deep-enriched with LLM analysis** (summaries, MITRE ATT&CK, detection rules, remediation). No API key required to consume the data here.

[![zerohack.org](https://img.shields.io/badge/ZEROHACK-ORG-0d1117?style=for-the-badge&logo=firebase&logoColor=white)](https://zerohack.org)
[![Data](https://img.shields.io/badge/data-JSON-334155?style=for-the-badge)](https://github.com/ZeroHackOrg/cves)
[![Sources](https://img.shields.io/badge/sources-10%2B-00B0BD?style=for-the-badge)]()
[![Fields](https://img.shields.io/badge/schema-80%2B_fields-7C3AED?style=for-the-badge)](docs/SCHEMA.md)
[![Sync](https://img.shields.io/badge/sync-weekly-0d1117?style=for-the-badge)]()
[![Community](https://img.shields.io/badge/PRs-welcome-22c55e?style=for-the-badge)](docs/CONTRIBUTING.md)
[![Made with love](https://img.shields.io/badge/Made_with-❤️-red?style=for-the-badge)]()
[![Always free](https://img.shields.io/badge/data-free_forever-16a34a?style=for-the-badge)]()

</div>

---

## 🌅 Our mission — building a safe tomorrow

The internet shouldn't be a place where the good guys lose by running slower than the bad guys. 🌍

Every morning, threat actors wake up and weaponize yesterday's CVE — a patch is already out, so why don't teams know? Because **intelligence is fragmented, buried, and late.** ZeroHack exists to change that. We fuse every authoritative source into **one clean, enriched record**, and we give it away **free, forever, in the open** — so the people defending the world are never one search away from "ahh, another day of guessing."

> 🫡 **The goal is simple:** when this goes live, *you* and *your team* spend zero hours stitching intel together — and every scanner, SIEM and analyst starting their day already knows what to fix first. That is how we build a safe tomorrow, one CVE at a time. 💛

## 🎯 What this repository is

Every day, security teams lose time stitching together NVD, CISA, EPSS, exploit feeds and threat intel by hand. ZeroHack does that stitching for you and publishes the result **here, in the open**:

- **One JSON file per CVE** with the full **80+ field schema** — scoring, affected software, exploit status, detection rules, IOCs, MITRE mapping, remediation, and more.
- **Deduplicated & merged** — each source owns its fields; empties never clobber real data (non-destructive merge contract).
- **AI-enriched** — LLMs (Groq / Gemini) generate executive summaries, YARA / Sigma / Suricata rules, workarounds and solutions, so the record goes beyond a raw feed.
- **Always fresh** — auto-synced weekly; `updatedAt` reflects the last pipeline write.
- **Community-powered** — corrections flow back into the pipeline; the dataset gets better the more it's used.

```
                    CORE FEEDS                EXPLOIT & POC               IOC & THREAT INTEL
 ┌─────────┐ ┌────────┐ ┌───────────┐   ┌────────────┐ ┌──────────┐ ┌───────────┐  ┌──────────┐ ┌─────────┐ ┌────────────┐
 │   NVD   │ │  CISA  │ │  FIRST    │   │   GitHub   │ │ExploitDB │ │ VulnCheck │  │Malware   │ │ URLhaus │ │ AlienVault │
 │ API v2  │ │  KEV   │ │   EPSS    │   │ Advisories │ │(modules) │ │  (IOCs)   │  │Bazaar    │ │ (URLs)  │ │  OTX (IOCs)│
 │ (CVSS)  │ │(known  │ │(score +%) │   │ (PoC, fix) │ │          │ │           │  │(hashes)  │ │         │ │            │
 └────┬────┘ └───┬────┘ └────┬──────┘   └─────┬──────┘ └────┬─────┘ └─────┬─────┘  └────┬─────┘ └────┬────┘ └─────┬──────┘
      └──────────┴───────────┴───────────────┴─────────────┴─────────────┴───────┴────┴──────────┴────┴───────────┘
                                             ▼
                              ┌─────────────────────────────┐
                              │   NORMALIZE + MERGE 💊       │
                              │   source-owns-fields merge   │
                              │   nothing is ever clobbered  │
                              └──────────────┬──────────────┘
                                             ▼
                              ┌─────────────────────────────┐
                              │   AI ENRICHMENT 🧠           │
                              │  summaries · detection      │
                              │  MITRE · YARA/Sigma/Suricata│
                              │  workaround · solution      │
                              └──────────────┬──────────────┘
                                             ▼
                         ┌───────────────────┴───────────────────┐
                         ▼                                       ▼
             HOT `cves` + ARCHIVE               ✨ JSON per CVE — verified,
             AI-enriched, ready to            versioned & pushed to
             query in real time               ZeroHackOrg/cves weekly
```

---

## 🤝 Trusted data sources & partners

ZeroHack aggregates from **10 independent, authoritative feeds** — every field traces back to the source that owns it (full provenance in [`docs/SOURCES.md`](docs/SOURCES.md)). 💚 No proprietary lock-in, no black box — what you see is exactly what the source published.

### Core scoring feeds

| Source | Contribution | Badge |
|--------|--------------|-------|
| **NVD / NIST** — [nvd.nist.gov](https://nvd.nist.gov) | CVSS vector, severity, CWE, descriptions | ![NVD](https://img.shields.io/badge/NVD-NIST_Scoring-1B3E6F?style=for-the-badge) |
| **CISA KEV** — [cisa.gov/kev](https://www.cisa.gov/known-exploited-vulnerabilities-catalog) | Known Exploited Vulnerabilities | ![CISA KEV](https://img.shields.io/badge/CISA-Known_Exploited_Feeds-B01E2E?style=for-the-badge) |
| **FIRST EPSS** — [first.org/epss](https://www.first.org/epss/) | Exploit Prediction Scoring (score + percentile) | ![FIRST](https://img.shields.io/badge/FIRST-EPSS_Scores-00A0DF?style=for-the-badge) |

### Exploit & PoC feeds

| Source | Contribution | Badge |
|--------|--------------|-------|
| **GitHub Security Advisories** — [github.com/advisories](https://github.com/advisories) | PoC URLs, patched version ranges | ![GitHub](https://img.shields.io/badge/GitHub-Security_Advisories-181717?style=for-the-badge&logo=github&logoColor=white) |
| **ExploitDB** — [exploit-db.com](https://www.exploit-db.com) | Exploit IDs, Metasploit module paths | ![ExploitDB](https://img.shields.io/badge/ExploitDB-Public_Exploits-0d1117?style=for-the-badge) |
| **VulnCheck** — [vulncheck.com](https://vulncheck.com) | Exploit status, additional IOCs | ![VulnCheck](https://img.shields.io/badge/VulnCheck-Exploit_Intel-7C3AED?style=for-the-badge) |

### IOC & threat-actor feeds

| Source | Contribution | Badge |
|--------|--------------|-------|
| **MalwareBazaar** — [bazaar.abuse.ch](https://bazaar.abuse.ch) | File hashes, mutexes per CVE | ![MalwareBazaar](https://img.shields.io/badge/MalwareBazaar-Hashes_%26_IOCs-00B0BD?style=for-the-badge) |
| **URLhaus** — [urlhaus.abuse.ch](https://urlhaus.abuse.ch) | Malicious URLs, IPs, domains | ![URLhaus](https://img.shields.io/badge/URLhaus-Malicious_URLs-FF4F00?style=for-the-badge) |
| **AlienVault OTX** — [otx.alienvault.com](https://otx.alienvault.com) | Multi-format threat pulses & indicators | ![OTX](https://img.shields.io/badge/AlienVault_OTX-Threat_Pulses-009FDB?style=for-the-badge) |
| **MITRE ATT&CK** — [attack.mitre.org](https://attack.mitre.org) | Tactic/technique mappings | ![MITRE](https://img.shields.io/badge/MITRE-ATT%26CK_Mapping-B32735?style=for-the-badge) |

### AI enrichment layer (merged on top, never overwrites sources)

| Engine | Contribution | Badge |
|--------|--------------|-------|
| **Groq** — [groq.com](https://groq.com) | LLM executive summaries, mitigation text | ![Groq](https://img.shields.io/badge/Groq-LLM_Summaries-F55036?style=for-the-badge) |
| **Google Gemini** — [deepmind.google](https://deepmind.google) | Detection rules, YARA/Sigma/Suricata | ![Gemini](https://img.shields.io/badge/Gemini-AI_Enrichment-4285F4?style=for-the-badge) |

---

## 📦 What's inside

| Path | Contents |
|------|----------|
| `cves/YYYY/` | **One JSON file per CVE** — full 80+ field enriched schema |
| `curated/kev/` | CISA Known Exploited Vulnerabilities snapshot |
| `curated/epss/` | FIRST.org EPSS scores (daily snapshot) |
| `curated/exploits/` | ExploitDB feed |
| `stats/summary.json` | Aggregate counts by severity, tier, source |
| `stats/changelog.json` | Additions / updates from the last 30 days |
| `docs/SCHEMA.md` | Full field-by-field JSON schema |
| `docs/SOURCES.md` | Field-level data provenance |
| `docs/CONTRIBUTING.md` | Contribution guide & review process |

## ⚡ Example record — highlights

```json
{
  "cveId":               "CVE-2026-12345",
  "severity":            "CRITICAL",
  "cvss":                9.8,
  "cvssVector":          "CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H",
  "epss":                0.97,
  "isZeroDay":           true,
  "cisaKev":             true,
  "exploitedInWild":     true,
  "pocAvailable":        true,
  "weaponized":          true,
  "metasploitModule":    "exploit/multi/http/log4j_header_injection",
  "mitreAttack":         ["T1190 Exploit Public-Facing App", "T1059 Execution"],
  "malwareFamilies":     ["Mirai", "Khonsari"],
  "iocIps":              ["185.220.101.1"],
  "iocDomains":          ["evil-c2.example.com"],
  "yaraRules":           ["rule log4j_exploit { ... }"],
  "sigmaRules":          ["log4j_rce.yml"],
  "solution":            "Upgrade to Log4j 2.17.0+"
}
```

The full canonical schema (80+ fields) is documented live at **[zerohack.org/docs/#cve-object](https://zerohack.org/docs/#cve-object)** and mirrors [`types/index.ts`](https://github.com/ZeroHackOrg/zerohack/blob/main/types/index.ts).

## 🔌 CVE API — ZeroHack Researcher Portal

Need this data as a **REST API** with pagination, filtering and real-time webhooks? The ZeroHack Researcher portal exposes the same enriched records:

| Endpoint | Description |
|----------|-------------|
| `GET /api/v2/cves` | List CVEs — pagination, severity & exploit filters |
| `GET /api/v2/cves/:cveId` | Full enriched record |
| `GET /api/v2/cves/zero-days` | Unpatched zero-days feed |
| `GET /api/v2/cves/kev` | CISA KEV catalogue |
| `GET /api/v2/cves/:cveId/iocs` · `/exploits` · `/mitre` | Threat intel per CVE |
| `POST /webhooks` | Real-time alerts → SIEM, Slack, Discord, Telegram |

- Explore the interactive docs → **[zerohack.org/docs](https://zerohack.org/docs)** 📚
- Live researcher CVE workspace → **[researcher.zerohack.org/cve-intel](https://researcher.zerohack.org/cve-intel)** 🚀
- Public CVE database → **[zerohack.org/cves](https://zerohack.org/cves)** 🔎

## 🚀 Quick start

```bash
# Single CVE — no API key needed
curl -O https://raw.githubusercontent.com/ZeroHackOrg/cves/main/cves/2026/CVE-2026-12345.json

# Browse a year of data
git clone --depth 1 https://github.com/ZeroHackOrg/cves.git
ls cves/2026/
```

⚡ **Get answers before attackers get options.** 3 seconds from repo → JSON → fix list.

## 🌍 Community & collaboration

ZeroHack intelligence is built **with the community, for the community.** Found a missing IOC, a new PoC, or a correction?

- 🔍 **Spot a gap?** Open an [issue](https://github.com/ZeroHackOrg/cves/issues/new/choose) with the CVE ID — use the `cve-correction` or `new-intel` template.
- 🤝 **Know something we don't?** Send a pull request editing the CVE JSON directly.
- ✅ **Want visibility?** Accepted corrections are credited and flow back into the ZeroHack pipeline (and the next sync).
- 📣 **Discuss & connect** — build in public with ZeroHack: open source hubs on [zerohack.org](https://zerohack.org), and suggest new data sources via issues in this repo.
- 💝 **Why contribute?** Because a safer internet is a **shared** job. Every correction you send gets verified, credited, and pushes the whole planet one step ahead of the attackers.

[![Good first issue](https://img.shields.io/badge/Contribute-Good_First_Issues-22c55e?style=for-the-badge)](https://github.com/ZeroHackOrg/cves/issues)
[![Code of conduct](https://img.shields.io/badge/Code_of_Conduct-Read_More-334155?style=for-the-badge)](docs/CONTRIBUTING.md)

## 📅 Update schedule

| Feed | Cadence |
|------|---------|
| `cves/` | Weekly push (auto) from the ZeroHack worker |
| `curated/kev/` | Synced with the CISA catalog |
| `curated/epss/` | Daily snapshot |
| `stats/` | Every export run |

Commits are machine-readable: `sync: YYYY-MM-DD HH:MM · N updated`.

## ✅ Quality guarantees

- Every file validates against [`docs/SCHEMA.md`](docs/SCHEMA.md).
- **Non-destructive by contract** — fields present in the pipeline are never dropped; missing fields are omitted, never stubbed.
- `updatedAt` reflects the last pipeline write.
- Corrections you submit are preserved on the next sync (community data preservation).

---

<div align="center">

## 💝 Made with love by ZeroHack 🛡️

**Building a safe tomorrow — together.** 🌍

*Free forever. Open by default. Human-first, always.*

**Built by [ZeroHack Security](https://zerohack.org)** · Enterprise-grade CVE intelligence, open to everyone.

[![ZeroHackOrg](https://img.shields.io/badge/ZeroHackOrg-More_Projects-0d1117?style=for-the-badge&logo=github&logoColor=white)](https://github.com/ZeroHackOrg)
[![Star](https://img.shields.io/badge/Star_Us-⭐-facc15?style=for-the-badge)](https://github.com/ZeroHackOrg/cves)

</div>

## License

© ZeroHack Security. **Proprietary** — enriched data and derivatives may not be republished, mirrored, or resold without written permission. CVE IDs, descriptions, and affected-product data remain subject to the original CVE/NVD licenses. See [LICENSE](LICENSE).