# ZeroHack CVE Intelligence

Open-source CVE vulnerability intelligence from [ZeroHack](https://zerohack.org) — AI-enriched, multi-source data ready for security teams, SOCs, researchers, and automation. Auto-synced from the ZeroHack CVE pipeline (10+ sources + AI enrichment).

![data files](https://img.shields.io/badge/data-JSON-blue)

---

## What's inside

| Path | Contents |
|------|----------|
| `cves/YYYY/` | One JSON file per CVE with the full 80+ field schema |
| `curated/kev/` | CISA Known Exploited Vulnerabilities snapshot |
| `curated/epss/` | FIRST.org EPSS scores (daily snapshot) |
| `curated/exploits/` | ExploitDB feed |
| `stats/summary.json` | Aggregate counts by severity, tier, source |
| `stats/changelog.json` | Additions / updates from the last 30 days |
| `docs/SCHEMA.md` | Full field-by-field JSON schema |
| `docs/SOURCES.md` | Data provenance per field |

## Example record

```json
{
  "cveId": "CVE-2026-12345",
  "title": "Remote Code Execution in Apache Log4j",
  "severity": "CRITICAL",
  "cvss": 9.8,
  "epss": 0.97,
  "isZeroDay": true,
  "cisaKev": true,
  "exploitedInWild": true,
  "pocAvailable": true,
  "weaponized": true,
  "mitreAttack": ["T1190 Exploit Public-Facing App"],
  "malwareFamilies": ["Mirai", "Khonsari"],
  "iocIps": ["185.220.101.1"],
  "iocDomains": ["evil-c2.example.com"],
  "solution": "Upgrade to Log4j 2.17.0+"
}
```

## Quick start

```bash
# Single CVE (no API key needed)
curl -O https://raw.githubusercontent.com/ZeroHackOrg/cves/main/cves/2026/CVE-2026-12345.json

# Browse a year
git clone --depth 1 https://github.com/ZeroHackOrg/cves.git
ls cves/2026/
```

## Data sources

NVD API v2, CISA KEV, FIRST.org EPSS, GitHub Security Advisories, ExploitDB, VulnCheck, MalwareBazaar, URLhaus, AlienVault OTX, and AI enrichment (Groq / Gemini).

| Field | Source |
|-------|--------|
| CVSS vector, severity, CWE | NVD |
| Exploited-in-wild, KEV | CISA KEV |
| EPSS / EPSS percentile | FIRST.org |
| PoC, fix versions | GitHub Security Advisories |
| Exploit IDs, Metasploit modules | ExploitDB |
| IOCs, threat actors | VulnCheck, MalwareBazaar, URLhaus, OTX |
| Summary, detection rules, solution | AI (Groq / Gemini) |

## Update schedule

| Feed | Cadence |
|------|---------|
| `cves/` | Weekly push (auto) from the ZeroHack worker |
| `curated/kev/` | Synced with CISA catalog |
| `curated/epss/` | Daily snapshot |
| `stats/` | Every export run |

Each commit message is `sync: YYYY-MM-DD HH:MM · N updated`.

## Community contributions

Found a missing IOC, PoC, or a correction? We welcome contributions:

1. Open an **issue** with the CVE ID (use the issue templates).
2. Or open a **pull request** editing the CVE JSON directly.
3. Maintainers review and merge — corrections flow back into the ZeroHack pipeline and the next sync.

Please read [docs/CONTRIBUTING.md](docs/CONTRIBUTING.md) first.

## Schema & quality

- Every file validates against [docs/SCHEMA.md](docs/SCHEMA.md).
- Data is non-destructive: fields present in the source pipeline are never dropped.
- `updatedAt` reflects the last pipeline write; missing fields are omitted, never stubbed.

## Related

- [zerohack.org](https://zerohack.org) — enterprise cybersecurity platform & CVE database
- [ZeroHackOrg](https://github.com/ZeroHackOrg) — other open-source projects

## License

© ZeroHack Security. See [LICENSE](LICENSE).