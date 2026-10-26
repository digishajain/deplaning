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

- **Titles:** any product or program management role: Product Manager at any
  level, Senior/Lead/Principal/Staff PM, AI PM, Product Owner, Product Lead,
  Director/Head of Product, Technical Program Manager, Program Manager on AI
  or tech programs, AI Solution Owner, Forward Deployed PM, AI practice or
  incubation leads with product ownership.
- **Sectors** (use these exact labels): `AI lab / foundation`, `Tech for good`,
  `Education`, `International development`, `Civic tech`.
- **Work mode:** `Remote` (preferred), `Hybrid`, or `On-site`.

## Visa sponsorship (required)

Digisha has an approved I-140. A new employer needs to (1) file an H-1B
transfer, which skips the lottery and keeps her priority date, and (2) restart
the green card with a new PERM and I-140. Record both on every row.

`visa` (H-1B):

- `Sponsors`: the posting says the employer sponsors, or the employer has many
  recent H-1B LCA filings (roughly 10+ a year).
- `Has sponsored`: a few H-1B filings in the last two years.
- `Unclear`: the evidence conflicts, for example filings exist but a posting
  says no sponsorship.
- `Unknown`: no posting language and no filings found.
- `No`: the posting says no sponsorship or requires authorization without sponsorship.

The posting's own wording beats filing data. To check filings, search for
`"<employer>" H-1B LCA`, using sources such as ellis.com, myvisajobs.com and
visaverge.com, which compile Department of Labor disclosure data. Write
`visa_note` as one sentence with the evidence, and `visa_url` as the source,
or null.

`gc` (green card): `Files green cards` when the employer has PERM filings on
record or a posting says it sponsors green cards; `No filings found` when it
files H-1Bs but shows no PERM filings; `Unknown`; `No` when the posting rules
out sponsorship. Search `"<employer>" PERM green card` on the same sites.
Write `gc_note` as one sentence with the evidence.

Prefer roles at `Sponsors` and `Has sponsored` employers when
searching. Remote roles open to candidates outside the US are worth noting,
since they may not need a visa.

## Fit score (0–100)

| Part | Points |
|---|---|
| Remote: Remote 30, Hybrid 12, On-site 5 | 30 |
| Level, judged by requirements and pay, not just title: senior-level PM 25, Director 20, mid-level PM 12, adjacent program or practice role 10 | 25 |
| AI at the core of the role 25; AI as a tool 12; none 0 | 25 |
| Sector match: AI-for-good, education or international development 20; other civic or tech for good 15 | 20 |

Store the parts as `fit_parts` ({remote, level, ai, sector}) and their sum as `fit`.

## Resume match (0–100)

How well the AIPM resume (summarized above) covers the role's stated
requirements: seniority, AI product delivery, domain, people management and
any hard requirements. Write `strengths` (1–3 short phrases citing real
resume facts) and `gaps` (1–2 phrases). The dashboard shows the average of
`fit` and `resume_match` as the overall match.

## Prep

`prep` is a list of action ids from `data/actions.json` (the dashboard's
`actions` dataset). Pick 2–4 that close this role's gaps, and always include
`visa-ask` unless the visa is `No`. `prep_specific` is one optional
role-specific step, or null. Add a new action to the actions dataset only
when no existing one fits.

## Row shape (`data/jobs.json`)

```json
{"id":"org-short-title","org":"","title":"","sector":"","work_mode":"Remote","location":"",
 "salary_min":null,"salary_max":null,"posted":"YYYY-MM-DD or null","first_seen":"YYYY-MM-DD",
 "status":"Likely open | Verify | Likely closed","fit":0,"fit_note":"","url":"",
 "fit_parts":{"remote":0,"level":0,"ai":0,"sector":0},"resume_match":0,"strengths":[],"gaps":[],
 "prep":["visa-ask"],"prep_specific":null,
 "visa":"Sponsors | Has sponsored | Unclear | Unknown | No","visa_note":"","visa_url":null,
 "gc":"Files green cards | No filings found | Unknown | No","gc_note":""}
```

`status`: use `Likely open` when a dated posting is from the last 30 days.
Use `Verify` when the date is unknown or the posting comes only from an
aggregator. Use `Likely closed` when the deadline has passed or the posting is
marked expired.

## Where to search

The boards, newsletters and people in `data/sources.json`, plus employer
careers pages. LinkedIn needs a login, so the refresh reaches LinkedIn only
through public posts and job pages that web search returns.
