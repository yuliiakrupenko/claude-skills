---
name: competitor-intelligence
description: >
  Generic competitor intelligence skill for B2B fintech / payments companies.
  Trigger for: competitor research, weekly intelligence report, competitive
  landscape, feature comparison, "how do we stack up", "what are competitors
  doing", "run the report", "where do we stand", "what should we build".
  Runs in three modes: Mode A (weekly news digest), Mode B (product feature
  matrix), Mode C (full combined C-level report — default). Output is a
  self-contained HTML report with: strategic position dashboard, exec summary,
  own activity assessment, competitor digest with pipeline threat scores and
  recommended actions, narrative battlefield, feature matrix with
  Build/Partner/Ignore verdicts, and a three-card leadership action summary
  (CEO/CMO/CPO).
---

# Competitor Intelligence Skill — Generic Version

---

## STEP 0 — Determine mode and collect company context

### 0a — Determine mode

- "weekly report / what happened this week / run the report for week ending [date]" → Mode A
- "feature comparison / how do we stack up / product matrix / capabilities" → Mode B
- "full analysis / full report / everything / C-level report" → Mode C (default)

Extract or ask for the week-ending date. If not supplied, use today's date.
Format all dates as: DD Month YYYY (e.g. 12 June 2026).

---

### 0b — Collect company context (REQUIRED before proceeding)

**If the user has NOT provided company details, ask all of the following before doing any research.
Present as a friendly, structured intake. Do not proceed to Step 1 until you have answers
to at least the starred (*) questions.**

Ask:

---

**Let's set up your competitor intelligence report. A few quick questions:**

1. *(*)* **Company name** — What is your company called?

2. *(*)* **What does your company do?** — One or two sentences: product, customer type, geography.
   *(Example: "We provide pre-funded virtual payment cards for online travel agencies in the UK and Europe.")*

3. *(*)* **Who are your 5–8 direct competitors?** — List them by name.
   *(These will be the columns in the feature matrix and the subjects of the news digest.)*

4. **Any indirect competitors to watch?** — Companies that aren't direct rivals but overlap
   in narrative or customer base. *(Optional — leave blank if unsure.)*

5. *(*)* **What are your company's 2–3 strongest differentiators?**
   *(Example: "Travel-native reconciliation, Merchant Locking, Visa CCTP partnership.")*

6. *(*)* **What are your company's 2–3 known weaknesses or gaps?**
   *(Example: "No mobile app, pre-funded only — no credit, no AI features.")*
   These are tracked in every report — competitor moves against your weaknesses
   get flagged as high-priority threats.

7. **Primary customer type?** — e.g. OTAs, travel agencies, SMEs, enterprises, banks, fintechs.

8. **Primary geography?** — e.g. UK, EEA, US, Global.

9. **What is your commercial model?** — e.g. transaction fee, subscription, interchange rebate, SaaS.

10. **Card scheme(s) or payment rail(s) you operate on?** — e.g. Visa, Mastercard, SWIFT, SEPA.
    *(Optional — leave blank if not applicable.)*

11. **Any regulatory licences worth mentioning?** — e.g. FCA EMI, BaFin, Bank of Spain. *(Optional.)*

12. **Where does your company publish content?** — e.g. company blog URL, LinkedIn page URL.
    *(Used to check your own activity as part of every report.)*

13. **Google Drive folder ID for saving reports?** *(Optional — leave blank to skip Drive upload.)*

---

Once you have the answers, store them as [COMPANY_CONTEXT] and use them throughout
to replace every placeholder in this skill. Do not ask again in subsequent reports
within the same session — remember the context.

---

## PLACEHOLDER REFERENCE

Wherever you see these placeholders in the skill, replace them with the
values collected in Step 0b:

| Placeholder | Replace with |
|---|---|
| `[COMPANY_NAME]` | Company name (Q1) |
| `[COMPANY_DESCRIPTION]` | What the company does (Q2) |
| `[DIRECT_COMPETITORS]` | List of direct competitors (Q3) |
| `[INDIRECT_COMPETITORS]` | Indirect competitors (Q4) |
| `[DIFFERENTIATORS]` | Company's strongest differentiators (Q5) |
| `[KNOWN_WEAKNESSES]` | Company's known weaknesses/gaps (Q6) |
| `[CUSTOMER_TYPE]` | Primary customer type (Q7) |
| `[PRIMARY_GEOGRAPHY]` | Primary geography (Q8) |
| `[COMMERCIAL_MODEL]` | Commercial model (Q9) |
| `[CARD_SCHEMES]` | Card schemes / payment rails (Q10) |
| `[LICENCES]` | Regulatory licences (Q11) |
| `[CONTENT_CHANNELS]` | Blog URL + LinkedIn URL (Q12) |
| `[DRIVE_FOLDER_ID]` | Google Drive folder ID (Q13) |

---

## About [COMPANY_NAME]

[COMPANY_DESCRIPTION]

Known weaknesses — always track competitor moves against these:
[KNOWN_WEAKNESSES — list each as a bullet point]

Key differentiators — always reinforce these in counter-narratives:
[DIFFERENTIATORS — list each as a bullet point]

---

## Competitor Lists

### Direct competitors (always include in digest and matrix)
[DIRECT_COMPETITORS — list each as a bullet, with [COMPANY_NAME] first as the reference/first position]

### Indirect competitors (surface in callout box only)
[INDIRECT_COMPETITORS — list each as a bullet, or "None provided" if blank]

---

## STEP 1 — Research

### 1a — Market intelligence (Modes A and C)

Use web_search and web_fetch. Cover the 7-day window ending on the report date.

Priority sources:
- Industry trade press relevant to [COMPANY_NAME]'s sector
  *(For payments/fintech: Finextra, Sifted, AltFi, FinTech Futures, The Paypers,
  Financial IT, PYMNTS, Payments Dive)*
  *(For travel payments specifically: PhocusWire, Skift, Breaking Travel News, Travolution)*
- Company blogs / press rooms for each competitor in [DIRECT_COMPETITORS]
- LinkedIn company pages (posts, announcements, hiring signals)
- Job boards: LinkedIn Jobs, company careers pages (signals roadmap intent)
- Crunchbase, Tracxn for funding signals

For [COMPANY_NAME] specifically, always check:
- [CONTENT_CHANNELS] — date of most recent post
- LinkedIn company page — post frequency this week
- Trade press coverage in period

Search query templates per competitor:
- "[competitor] payment news [month] [year]"
- "[competitor] product launch [year]"
- "[competitor] partnership announcement [year]"
- "[competitor] funding [year]"
- "[competitor] jobs hiring [role] [year]" ← roadmap signal

Categories to track (in priority order):
1. Product launches & updates
2. Marketing campaigns & content / narrative shifts
3. Partnerships & M&As
4. Pricing changes
5. Funding news
6. Leadership & hiring signals (including job postings as roadmap proxy)

**Dating rule — CRITICAL:**
Every finding MUST include the publication/announcement date.
Format: DD Month YYYY. Month YYYY if exact day unknown.
Never include an undated finding. Mark unverifiable dates as: (Date unconfirmed — verify).
If an org had no verifiable news: state "No verifiable public activity found for week
ending [date]." Do not pad with old news or speculation.

### 1b — Product feature research (Modes B and C)

Sources: official product/pricing pages, press releases, Crunchbase/Tracxn/Wikipedia,
G2/Capterra reviews, app store listings.

Search templates:
- "[competitor] B2B payment features [year]"
- "[competitor] employees headcount revenue [year]"
- "[competitor] [customer_type] payment API"
- "[competitor] commercial model pricing tiers"
- "[competitor] jobs engineer product [year]" ← hiring as feature signal

Mark unverifiable fields: Unconfirmed — verify [date of search]
Never guess. Never leave blank.

---

## STEP 2 — Report structure

The report is a single self-contained HTML file with 7 sections (Mode C).
Modes A and B omit sections as noted below.

```
PAGE 0 — COVER
  Title, reporting period, generated date, prepared for [COMPANY_NAME] Leadership Team
  One-sentence headline finding (the most important thing this week)

PAGE 1 — STRATEGIC POSITION DASHBOARD       ← All modes.
  First thing leadership reads. One page only.
  Three panels:
  A) Competitive position scorecard — for each of the 4 nearest competitors,
     a Win / Competitive / At Risk verdict for [COMPANY_NAME] in the [CUSTOMER_TYPE] segment,
     with a 1-line reason and a direction arrow (↑ improving / → stable / ↓ declining)
  B) What moved this week — up to 3 bullets, each one a signal that changed
     [COMPANY_NAME]'s competitive position (up or down), with the date
  C) The one decision — the single most important thing leadership must decide
     or act on before the next report. One sentence. Bold. No hedging.

SECTION 1 — EXECUTIVE SUMMARY              ← Modes A and C
  4–5 sentences written for C-level. Not a list of events — a narrative.
  Ends with a pace comparison sentence: who shipped most, where [COMPANY_NAME] sits.
  DO NOT repeat the dashboard content — add context and colour instead.

SECTION 2 — [COMPANY_NAME] OWN ACTIVITY    ← Modes A and C
  Separate highlighted section before competitor findings.
  What did [COMPANY_NAME] publish, announce, or do this week?
  Assessed on the same terms as every competitor.
  Table columns: Date | Category | Finding | Self-assessment | Action needed
  Self-assessment: Are we ahead, at parity, or behind competitors on this dimension?
  Action needed: specific, owned, time-bound

SECTION 3 — COMPETITOR INTELLIGENCE DIGEST ← Modes A and C
  One table. All competitor findings for the week.
  Columns: Organisation | Date | Category | Finding | Pipeline threat (H/M/L + reason) |
           Recommended action (Owner / Timeframe / Dept) | Source URL
  Pipeline threat:
    High = could cost us a deal in the next 90 days
    Medium = affects our positioning or narrative
    Low = noted, no immediate action needed
  Recommended action format: "[What to do] — [Owner: CEO/CMO/CPO/Sales] — [When]"
  Group [COMPANY_NAME] rows separately at top. Quiet-week callouts at bottom.

SECTION 4 — NARRATIVE BATTLEFIELD           ← Modes A and C
  What stories are competitors telling RIGHT NOW in the market?
  For each of the top 3 most active competitors this week:
    - Their current narrative / positioning (1–2 sentences)
    - The [CUSTOMER_TYPE] objection it creates for [COMPANY_NAME]
    - The counter-narrative [COMPANY_NAME] should own
  End with: "Narrative gaps [COMPANY_NAME] is currently not filling" — up to 3 bullets

SECTION 5 — PRODUCT FEATURE MATRIX         ← Modes B and C
  Sticky-header comparison table. [COMPANY_NAME] as first/highlighted column.
  All dimensions from Step 3 below.
  Add a "Build / Partner / Ignore" verdict for each GAP in [COMPANY_NAME]'s row:
    - Build: feasible within 6 months, high customer demand signal
    - Partner: too capital-intensive or specialist to build; find a provider
    - Ignore: no customer demand signal in the next 12 months
  Add a "Deal-loss signal" note on any gap where there is evidence it has cost
  [COMPANY_NAME] business. If no data: mark "No signal — verify with sales team"

SECTION 6 — LEADERSHIP ACTION SUMMARY      ← All modes.
  Three short lists (CEO / CMO / CPO), max 5 bullets each. Scannable. No prose.

  CEO: strategic decisions required, M&A/funding signals, "if we do nothing" consequence
  CMO: content topics to publish this week, competitor narratives to counter,
       channels where competitors are active and [COMPANY_NAME] is absent
  CPO: feature gaps with deal-loss signal → Build/Partner verdict,
       competitor product moves threatening core differentiators,
       hiring signals revealing competitor 6–12 month roadmap

SECTION 7 — SOURCE INDEX
  All URLs cited, grouped by organisation, with access dates.
```

---

## STEP 3 — Feature matrix dimensions

Cover ALL of the following as rows. Add or remove rows based on
what is relevant to [COMPANY_NAME]'s industry.

### Identity & market position
- Type (fintech / bank / infrastructure / travel-native / SaaS / etc.)
- Primary market (geography + verticals)
- Industry/vertical focus (Core / Peripheral / None)
- Date assessed

### Organisation size
- Employees (approx.)
- Revenue / scale
- Stage / ownership
- Last funding event + date

### Geography & compliance
- Regulatory footprint (licences)
- Markets served

### Liquidity / commercial model
- Funding model (pre-funded / credit / post-pay / subscription / etc.)
- Credit lines available (Yes / Partial / No) — if applicable
- Commercial model ([COMMERCIAL_MODEL])

### Currency & geography support
- Currencies supported
- Countries covered

### Core product features (Yes / Partial / No + Build/Partner/Ignore for [COMPANY_NAME] gaps)
*(Adapt this list to [COMPANY_NAME]'s product category. The defaults below assume a B2B payments product.)*
- Virtual cards (VCC) — single-use
- Virtual cards (VCC) — multi-use
- Bank transfer / SWIFT
- SEPA / local payment rails
- Invoice payment
- FX / currency conversion
- Multi-currency wallets
- Physical cards
- Mobile app

### Controls & reconciliation
- Spend controls / approval rules
- MCC restrictions (if applicable)
- Merchant locking (if applicable)
- Custom card activation & expiry
- Automated reconciliation
- Reporting / data export

### API & integrations
- API availability
- Relevant platform integrations (GDS / ERP / accounting / CRM — adapt to [COMPANY_NAME]'s space)
- Webhooks / real-time events

### Advanced features
- AI / automation features
- Any emerging tech relevant to [COMPANY_NAME]'s sector (stablecoins, open banking, etc.)

### [DIFFERENTIATORS] — always include as dedicated rows
*(Add one row per differentiator listed in [DIFFERENTIATORS] so [COMPANY_NAME]'s
strengths are always visible and trackable across competitors.)*

### [KNOWN_WEAKNESSES] — always include as dedicated rows
*(Add one row per known weakness listed in [KNOWN_WEAKNESSES].
Mark any competitor who has closed this gap as a pipeline threat.)*

### Commercial model
- Pricing model
- Rebates offered (if applicable)
- Contract structure

---

## STEP 4 — HTML design rules

### General
- Single self-contained HTML file, all CSS in one `<style>` block
- Readable on desktop, printable as PDF
- Professional, C-level aesthetic
- Font: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif
- Body text: #1a1a1a. Secondary: #6b7280. Background: #f9fafb. Cards: #fff.
- Primary accent colour: use a colour that fits [COMPANY_NAME]'s brand if known,
  otherwise default to #1a6b3c (green)
- Threat pipeline: High = #dc2626 red, Medium = #d97706 amber, Low = #6b7280 gray
- Feature Yes = #16a34a, Partial = #d97706, No = #9ca3af

### Page 0 — Cover
- Large title, subtitle with week-ending date and generated date
- "Prepared for: [COMPANY_NAME] Leadership Team — Confidential"
- Headline finding in a prominent accent-colour box

### Page 1 — Strategic Position Dashboard
- Three side-by-side panels (or stacked on narrow screens)
- Panel A (Competitive scorecard): compact table, 4 rows
  Position badge: Win (green) / Competitive (amber) / At Risk (red)
  Direction: ↑ ↓ → with colour
- Panel B (What moved): numbered list, max 3 items, each with a date badge
- Panel C (The one decision): large bold text in a red-bordered box — impossible to miss

### Section 3 — Intelligence digest
- Table with 7 columns
- Pipeline threat column: badge (H/M/L) + small text reason below the badge
- Recommended action: bold action text, then owner and timeframe in smaller muted text

### Section 6 — Leadership action summary
- Three distinct coloured cards side by side:
  CEO card: dark navy #1e3a5f background, white text
  CMO card: dark purple #4c1d95 background, white text
  CPO card: dark green #14532d background, white text
- Each card: role label, then numbered list
- Maximum 5 bullets per card, 1 sentence each
- Font size 13px, line height 1.6

### Tables general
- border-collapse: collapse, alternating row shading
- Sticky header: background #1f2937, white text
- [COMPANY_NAME] rows/columns: #f0fdf4 background, 3px solid [accent colour] left border
- Font size 12.5px in tables
- Dates: shown below main content in #9ca3af at 10.5px

### Callout boxes
- Exec summary: #eff6ff bg, 4px solid #2563eb left border
- Quiet week: #f9fafb bg, 1px solid #e5e7eb border, italic
- Narrative battlefield: #fdf4ff bg, 1px solid #e9d5ff border
- Indirect competitors: #faf5ff bg, 1px solid #e9d5ff border
- The one decision: #fef2f2 bg, 4px solid #dc2626 left border

### Footer
- "This report was generated by Claude for [COMPANY_NAME] internal use only."
- "Report date: DD Month YYYY. All findings include source URLs."
- If [DRIVE_FOLDER_ID] provided: "Google Drive folder: [DRIVE_FOLDER_ID]"

---

## STEP 5 — Save report

1. Name the file: `competitor-intelligence-YYYY-MM-DD.html`
   (date = week-ending date)

2. If [DRIVE_FOLDER_ID] was provided:
   Use the Google Drive integration to upload to that folder.
   Confirm: "Saved to Google Drive as [filename]."

3. If Drive upload fails or no folder ID provided:
   Save to /mnt/user-data/outputs/[filename]
   Use present_files
   Tell user: "File ready for download above."

---

## STEP 6 — Output quality checklist

Before finishing, verify every item:

### Page 1 — Strategic Position Dashboard
- [ ] Competitive position verdict for each of the 4 nearest competitors
- [ ] Direction arrow on each position (↑ → ↓)
- [ ] "What moved this week" has dates on every bullet
- [ ] "The one decision" is present, bold, and impossible to miss

### Section 2 — Own activity
- [ ] [COMPANY_NAME] assessed on same terms as competitors
- [ ] Self-assessment verdict (ahead / at parity / behind) on each item
- [ ] Action needed is specific, owned, and time-bound

### Section 3 — Intelligence digest
- [ ] Every finding has a date
- [ ] Every finding has a source URL
- [ ] Pipeline threat: H/M/L with reason on every row
- [ ] Recommended action: what / owner / when on every row
- [ ] Quiet-week orgs called out explicitly

### Section 4 — Narrative battlefield
- [ ] Top 3 active competitors have: their narrative / the customer objection /
     [COMPANY_NAME]'s counter-narrative
- [ ] "Narrative gaps" list is present

### Section 5 — Feature matrix
- [ ] Build/Partner/Ignore verdict on every [COMPANY_NAME] gap
- [ ] Deal-loss signal note on every gap
- [ ] All competitors have data in every row
- [ ] [COMPANY_NAME] column highlighted and first
- [ ] Date assessed on every column
- [ ] Indirect competitors callout present

### Section 6 — Leadership action summary
- [ ] Three separate cards: CEO / CMO / CPO
- [ ] Maximum 5 bullets per card
- [ ] "If we do nothing" consequence in CEO card
- [ ] Specific content topics (not vague themes) in CMO card
- [ ] Build/Partner verdict in CPO card

### All
- [ ] All dates in DD Month YYYY format
- [ ] Report prominently dated on cover
- [ ] All [PLACEHOLDER] values replaced — none left as literal text
- [ ] Source index complete
- [ ] File saved or presented for download
- [ ] HTML renders as standalone file

---

## STEP 7 — Customisation flags

- Different competitors: adjust columns/rows as requested
- Different format: use docx skill for Word, xlsx for spreadsheet, pptx for deck
- Deeper dive on one competitor: run extra searches, add appendix section
- Additional matrix dimensions: add as new rows
- Different date range: adjust research window
- Sales battlecard only: produce a 1-page HTML battlecard focused on the top 2 threats,
  with counter-arguments for each known objection

---

## Trigger phrases

Run this skill when the user says:
- "run the weekly report"
- "run the full competitor analysis"
- "competitor intelligence for week ending [date]"
- "how do we stack up against [competitor]"
- "what are [competitor] doing"
- "competitive landscape"
- "feature comparison"
- "run the report"
- "full analysis"
- "what should we build"
- "where do we stand"
- "what's going on with competitors"
