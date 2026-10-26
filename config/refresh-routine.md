# Daily refresh: Impact AI Job Board

Dashboard: https://claude.ai/artifact/U7LDu6TvAuMDuxQbuz2QAu

A scheduled Claude routine runs this every morning. It finds new postings,
scores them, and updates the `jobs` dataset on the dashboard.

## Who the board is for

Digisha Jain: Senior Product Manager / AI Solution Owner (Slalom). Shipped
multi-agent AI platforms, MCP-based AI SDLC, and AI enablement programs for
100+ consultants. Public-sector delivery background (FDA, California OPR, DMHC).
Co-founded GEET, a girls' education nonprofit, and holds a Georgetown certificate
in education policy.

## What counts as a match

- **Titles:** Senior Product Manager, AI Product Manager, Lead/Principal PM,
  Product Lead, Director of Product, AI Solution Owner, Forward Deployed PM.
  Include close variants such as incubation, AI programs, or AI adoption lead
  when they involve product ownership.
- **Sectors** (use these exact labels): `AI lab / foundation`, `Tech for good`,
  `Education`, `International development`, `Civic tech`.
- **Work mode:** `Remote` (preferred), `Hybrid`, or `On-site`.

## Fit score (0–100)

| Part | Points |
|---|---|
| Remote: Remote 30, Hybrid 12, On-site 5 | 30 |
| Level: Senior/Lead/Principal PM or AI PM 25, Director 20, PM 12, adjacent non-PM 10 | 25 |
| AI at the core of the role 25; AI as a tool 12; none 0 | 25 |
| Sector match: AI-for-good, education or international development 20; other civic or tech for good 15 | 20 |

`fit_note` is one sentence on why the role fits, plus the main catch.

## Row shape (`data/jobs.json`)

```json
{"id":"org-short-title","org":"","title":"","sector":"","work_mode":"Remote","location":"",
 "salary_min":null,"salary_max":null,"posted":"YYYY-MM-DD or null","first_seen":"YYYY-MM-DD",
 "status":"Likely open | Verify | Likely closed","fit":0,"fit_note":"","url":""}
```

`status`: use `Likely open` when a dated posting is from the last 30 days.
Use `Verify` when the date is unknown or the posting comes only from an
aggregator. Use `Likely closed` when the deadline has passed or the posting is
marked expired.
