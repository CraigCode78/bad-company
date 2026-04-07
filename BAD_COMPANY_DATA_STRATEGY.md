# Bad Company: Data Strategy

**Version:** 2.0  
**Date:** April 2026  
**Status:** For team discussion  
**Supersedes:** DATA_SOURCES.md v1.0  
**Contributors:** Craig Hepburn (source research), Upendra Shardanand (scoring matrix), Connor Hepburn (product pager)

---

## Guiding Principles

**Volume is not the constraint. Depth, defensibility, and multi-feature leverage are.**

Every source in this document was selected against four tests:

1. Does it tell us something no other source already covers?
2. Is it free, open access, or achievable via a data partnership at low cost?
3. Is it maintained by an independent, credible organisation and updated regularly?
4. Can it be defended to a journalist, a lawyer, or a company that disputes its score?

A source that fails any one of these tests does not belong in the first batch.

---

## Scoring Framework

All sources have been scored across six dimensions (Upendra's matrix, April 2026):

| Dimension | What it measures | Scale |
|---|---|---|
| **Authority** | Official govt / major institution / established NGO / community / niche | 1–5 |
| **Breadth** | Millions of entities / tens of thousands / thousands / hundreds / narrow | 1–5 |
| **Depth** | Rich multi-dimensional data / good detail / moderate / single dimension / minimal | 1–5 |
| **Ease of Integration** | REST API / API with friction / bulk download / scraping / manual | 1–5 |
| **Outrage Potential** | Inherently shareable / strong sharing impulse / moderately interesting / useful but boring / infrastructure | 1–5 |
| **Multi-Feature Leverage** | Feeds 5+ features / 3–4 / 2 / 1 well / narrow single use | 1–5 |

Maximum score: 30. Sources scoring 20+ are the strongest candidates for the first build.

---

## Dead Sources — Do Not Integrate

| Source | Status | Replacement |
|---|---|---|
| Fakespot | Shut down July 2025 | ReviewMeta |
| GoodGuide | Shut down June 2020 | None needed |
| Open Ownership Register | Closed November 2024 | OpenCorporates |

---

## Tier 1: Build Now

All free. All defensible. Build these before anything else.

---

### CFPB Consumer Complaints
**Score: 27/30 — highest-scoring source in the full matrix**

- **URL:** https://www.consumerfinance.gov/data-research/consumer-complaints/
- **Category:** Consumer Finance / Enforcement
- **Access:** Free REST API, daily updates
- **Coverage:** 4 million+ complaints against financial companies — banks, lenders, debt collectors, credit bureaus
- **Features served:** Ethics scorecard, Police Report, consumer harm feed
- **Bad Company use:** Primary consumer enforcement signal. "4,000 complaints against X in the last 12 months" is directly shareable. Complements FTC and Violation Tracker for a complete enforcement picture. Missing from our original eight — should have been Tier 1 from day one.
- **Notes:** CFPB's independence has been politically contested in 2025/26. Data remains publicly available regardless of agency structure.

---

### FEC Campaign Finance
**Score: 26/30 — second highest in the full matrix**

- **URL:** https://api.open.fec.gov
- **Category:** Political
- **Access:** Free REST API, excellent documentation
- **Coverage:** All federal election contributions by PAC, individual, and committee. Complete federal election history.
- **Features served:** Political donation tracker, ethics scorecard
- **Bad Company use:** Powers the Political Donation Tracker feature directly. Official federal records — maximum authority. "Company donated $X to candidate Y" is viral content. Use FEC for federal; Follow the Money for state-level gap-fill.
- **Notes:** The cleanest, best-documented API in the entire stack. Connor should integrate this early.

---

### Violation Tracker
**Score: 25/30**

- **URL:** https://violationtracker.goodjobsfirst.org
- **Global version:** https://violationtrackerglobal.goodjobsfirst.org
- **UK version:** https://violationtracker.goodjobsfirst.org/uk
- **Category:** Enforcement (Aggregator)
- **Access:** Free, web search and bulk download
- **Coverage:** 700,000+ civil and criminal cases from 450+ US federal and state agencies since 2000. Total penalties exceed $1 trillion. Covers banking, consumer protection, environmental, wage and hour, safety, discrimination, price-fixing, bribery. Global and UK versions available.
- **Features served:** Police Report, ethics scorecard, labour, environmental, consumer, and governance scoring — more features than any other single source
- **Bad Company use:** The single best cross-dimensional misconduct database available at no cost. Penalty amounts provide financial weighting. Historical trajectory data supports the trajectory scoring model.
- **Notes:** No formal API — well-structured for scraping. Integrate Violation Tracker before building individual agency connectors; it already aggregates FTC, EPA, OSHA, and 450+ others.

---

### EPA ECHO
**Score: 25/30**

- **URL:** https://echo.epa.gov
- **Category:** Environmental
- **Access:** Free REST API (echo.epa.gov/tools/web-services)
- **Coverage:** 800,000+ regulated facilities. Compliance records, violations, inspections, enforcement actions across Clean Air Act, Clean Water Act, and hazardous waste laws.
- **Features served:** Ethics scorecard, Police Report, environmental scoring
- **Bad Company use:** Official EPA enforcement data with a proper free API. Environmental violations drive consumer outrage. "Company fined $X for releasing Y into local waterways" is high-outrage content.
- **Notes:** Requires mapping facility-level data to parent companies. Violation Tracker already aggregates a portion of EPA data — cross-check for duplication.

---

### SEC EDGAR
**Score: 25/30**

- **URL:** https://data.sec.gov
- **Category:** Governance
- **Access:** Free REST API, no authentication required
- **Coverage:** 20 million+ filings including 10-K annual reports, 8-K material event filings, proxy statements, executive pay disclosures. All US public companies.
- **Features served:** Governance scoring, ethics scorecard, executive pay tracking
- **Bad Company use:** Self-reported litigation and legal risk direct from the company. Executive pay ratios from proxy statements. 8-K filings capture material governance events in real time. Risk disclosure language analysis is a strong AI task for the model.
- **Notes:** US public companies only. Requires NLP to extract relevant content from long documents. The most technically rich free source in the stack.

---

### Federal Register API
**Score: 25/30**

- **URL:** https://www.federalregister.gov/developers/api/v1
- **Category:** Regulatory / Bad Government
- **Access:** Free REST API, excellent documentation
- **Coverage:** All US federal regulatory changes, proposed rules, final rules, executive orders.
- **Features served:** Consumer harm news feed, Your Rights Right Now, Bad Government pillar (4+ features)
- **Bad Company use:** Essential infrastructure for the Bad Government pillar. Tracks deregulation events in real time. "Consumer protection rule X was quietly removed on [date]" is exactly the content Bad Company should surface.
- **Notes:** Less viral to average users than enforcement data but non-negotiable for the Bad Government pillar. Pairs with Congress.gov for the full regulatory cycle.

---

### FTC Cases and Proceedings
**Score: 24/30**

- **URL:** https://www.ftc.gov/enforcement/cases-proceedings
- **Category:** Consumer Enforcement
- **Access:** Free REST API and web
- **Coverage:** All FTC enforcement actions for deceptive advertising, dark patterns, subscription traps, fake reviews, privacy violations, anti-competitive behaviour. Expanded dark pattern enforcement since 2022.
- **Features served:** Sponsored content flag, influencer checker, Police Report, subscription trap warning, consumer manipulation scoring
- **Bad Company use:** Primary US consumer manipulation enforcement anchor. Integrate via Violation Tracker first — it already aggregates FTC data — and use FTC direct only for feature-specific lookups.
- **Notes:** US-only. Pair with CMA (UK) for full English-language market coverage.

---

### CPSC Recalls API
**Score: 24/30**

- **URL:** https://www.cpsc.gov/Recalls
- **Category:** Product Safety
- **Access:** Free REST API with JSON output
- **Coverage:** All US Consumer Product Safety Commission product recalls.
- **Features served:** Product safety alerts, ethics scorecard, Police Report
- **Bad Company use:** Product recalls are among the most shareable consumer safety signals available. "Company X recalled Y product due to Z injury risk" needs no interpretation. Free JSON API makes integration straightforward.
- **Notes:** Pairs with SaferProducts.gov for pre-recall incident signals.

---

### Congress.gov API
**Score: 24/30**

- **URL:** https://api.congress.gov
- **Category:** Legislative
- **Access:** Free REST API, Library of Congress maintained
- **Coverage:** Full US legislative tracking — bills, votes, members, committees.
- **Features served:** Your Rights Right Now, consumer harm news feed, Bad Government pillar
- **Bad Company use:** Tracks specific consumer protection bills and their status. Voting records on consumer legislation are shareable. Pairs with Federal Register API to show the full cycle: proposed, passed, implemented, reversed.
- **Notes:** Supplement with ProPublica Congress API for better developer experience on specific queries.

---

### OSHA Enforcement
**Score: 23/30**

- **URL:** https://www.osha.gov/data
- **Category:** Labour
- **Access:** Free data portal and bulk download
- **Coverage:** Millions of workplace safety inspections, citations, and penalties across US employers.
- **Features served:** Ethics scorecard, labour scoring, Police Report
- **Bad Company use:** Official workplace safety data. "Company cited for X worker deaths" is maximum outrage. Essential for the Labour dimension.
- **Notes:** US-only. No single REST API. Violation Tracker aggregates OSHA data — use both, treat Violation Tracker as the primary integration point.

---

### Open Food Facts API
**Score: 21/30**

- **URL:** https://world.openfoodfacts.org/data
- **Category:** Food / Ingredients
- **Access:** Free REST API
- **Coverage:** 3 million+ food products globally. Ingredients, Eco-Score, NOVA processing classification, Nutri-Score.
- **Features served:** Ethics scorecard, ingredient checker, product transparency
- **Bad Company use:** Largest free food product database available. Eco-Score provides an environmental signal at product level. Essential for consumer-facing product transparency features.
- **Notes:** Community-maintained — quality varies. Strongest for packaged food in European markets.

---

### SaferProducts.gov API
**Score: 21/30**

- **URL:** https://www.saferproducts.gov/RestWebServices
- **Category:** Product Safety
- **Access:** Free REST API
- **Coverage:** Consumer product incident reports submitted before recalls are issued — pre-recall signals.
- **Features served:** Product safety early warning
- **Bad Company use:** "Consumers have filed 47 injury reports against this product" is compelling before a formal recall exists. Pairs with CPSC Recalls as a two-stage product safety signal.

---

### CourtListener API
**Score: 21/30**

- **URL:** https://www.courtlistener.com/api/
- **Category:** Legal
- **Access:** Free REST API, RECAP archive
- **Coverage:** Millions of federal court opinions and filings.
- **Features served:** Class action lookup, legal depth
- **Bad Company use:** Legal records carry maximum authority. Free API makes this significantly easier to integrate than ClassAction.org scraping. Use ClassAction.org for consumer-facing "you may be owed money" surface; use CourtListener for the underlying legal record depth.

---

### ToS;DR API
**Score: 20/30**

- **URL:** https://api.tosdr.org
- **Category:** Terms of Service
- **Access:** Free REST API (intermittent — monitor reliability)
- **Coverage:** Community-reviewed Terms of Service ratings (A–E) for major digital services.
- **Features served:** TOS summariser, hidden fee revealer, subscription trap warning, return gotcha flag — 4+ features from a single source
- **Bad Company use:** High multi-feature leverage. Pre-rated ToS data feeds multiple scam detection features without requiring real-time NLP.
- **Notes:** Build a fallback given API reliability issues.

---

### Google Safe Browsing
**Score: 20/30**

- **URL:** https://developers.google.com/safe-browsing
- **Category:** Site Safety
- **Access:** Free REST API (10,000 requests/day free tier)
- **Coverage:** Billions of URLs checked for phishing, malware, and deceptive content.
- **Features served:** Sketchy site flag
- **Bad Company use:** Pure safety infrastructure for the Chrome extension. Every URL visited is checked in real time. Zero-friction integration.
- **Notes:** Monitor usage at scale — may need a paid tier as user base grows.

---

### ClassAction.org
**Score: 18/30**

- **URL:** https://www.classaction.org
- **Category:** Legal
- **Access:** Free, web scraping required
- **Coverage:** Active and settled class action lawsuits, daily updates.
- **Features served:** Class action lookup
- **Bad Company use:** "You might be owed money from this company" is one of the most shareable consumer signals possible. Use alongside CourtListener for depth.
- **Notes:** No API — scraping required. CourtListener is the better integration for depth.

---

## Tier 2: Build Next

High value but require scraping, partnerships, or have access constraints. Build after Tier 1 is stable.

| Source | Score | URL | Access | Key use | Notes |
|---|---|---|---|---|---|
| OpenSecrets | 25/30 | opensecrets.org/bulk-data | Free bulk CSV | Political lobbying and dark money | API deprecated; use bulk CSV |
| ICIJ Offshore Leaks | 21/30 | offshoreleaks.icij.org | Free search | Tax haven and governance override signal | 810,000 entities; event-driven coverage |
| iFixit Repairability | 21/30 | ifixit.com/api/2.0/doc | Free REST API | Product repairability scores | Electronics-focused; unique data |
| BHRRC | ~23/30 est. | business-humanrights.org | Free JSON API | Labour and human rights allegations | Not in Upendra's matrix — score and add |
| Climate Trace | 20/30 | climatetrace.org | Free data portal | Satellite-based GHG; not self-reported | Use as CDP verification layer |
| Follow the Money | 20/30 | followthemoney.org | Free bulk download | State-level campaign finance | Fills FEC gap for state elections |
| CDP | 19/30 | cdp.net/en/data/scores | Partial free | Climate A–D scores for 23,000 companies | Pursue NGO data partnership |
| KnowTheChain | 18/30 | knowthechain.org | Free reports | Forced labour benchmarks 0–100 | Annual; three sectors only |
| World Benchmarking Alliance | 17/30 | worldbenchmarkingalliance.org | Free Excel | 2,000 companies; 18 social indicators | Annual; public disclosure derived |
| Good On You | 18/30 | goodonyou.eco | Partnership API | 6,000 brand ethical ratings | Partnership needed for API access |
| B Corp Directory | 16/30 | bcorporation.net | Free directory | Positive certification signal | Positive signal; low outrage |
| SBTi Target Dashboard | 15/30 | sciencebasedtargets.org | Free weekly Excel | Net-zero target validation | Binary signal; weekly updates |
| EPA TRI | 20/30 | epa.gov/toxics-release-inventory | Free bulk | Toxic chemical releases by facility | Annual reporting |
| Boycat | 17/30 | Partnership | Free | Boycott data; 3M users | Growing; geopolitically comprehensive |
| CA DROP Platform | 16/30 | cppa.ca.gov | Free | Data broker deletion; 500+ brokers | Launched January 2026 |
| EPA CPDat | 20/30 | epa.gov | Free database | Chemical product safety | Feeds ingredient checker |

---

## Tier 3: Paid / Partnership — Build Later

Do not block V1 on these. Revisit when funding and partnerships allow.

| Source | Score | Cost | Why it matters | When to pursue |
|---|---|---|---|---|
| Keepa | 24/30 | €15–53.5K/month | Gold standard Amazon price history | When Save Money pillar is priority |
| RepRisk | 21/30 | Enterprise | Real-time AI ESG monitoring; 130,000 companies | When funding allows |
| MSCI ESG | 18/30 | Enterprise | Institutional-grade ESG for 8,500 companies | When investor-facing product is in scope |
| Sustainalytics | 18/30 | Enterprise | Deep ESG risk for 20,000+ companies | Same as MSCI |
| Consumer Reports | 18/30 | Membership | Most trusted independent product testing | Pursue partnership; mission alignment |
| SerpApi | 19/30 | $50–250/month | Cross-retailer pricing via Google Shopping | When cross-site price comparison is in build |
| Parent Company API | 20/30 | Usage-based | Maps brands to parent companies — gates all Shop Your Values features | High priority once feature set is confirmed |

---

## Infrastructure Approach

All source data is stored as structured markdown files in this repository. This is intentional.

Markdown files are the native medium of AI agents. No database connection, no schema, no driver, no query plan required. Any model, any pipeline, and any team member can read them immediately. When a source changes, the file is edited and committed — no migrations, no downtime.

As the file count grows, a vector database layer (Pinecone, Weaviate, or Chroma) will be added as a retrieval index on top of the markdown files. The markdown files remain the source of truth at all times.

**Connor: evaluate Wikirate (wikirate.org) before building individual source scrapers.** It already aggregates data from KnowTheChain, Violation Tracker, and WBA via a single free REST API and may significantly reduce the number of individual connectors required.

---

## Open Questions for Team Discussion

**1. BHRRC tier placement.**
Based on independent research, BHRRC should likely be Tier 1 alongside Violation Tracker — open JSON API, 20,000+ companies, real-time allegations. It was not in Upendra's matrix. Needs to be scored and added to the spreadsheet before the next discussion.

**2. CDP access.**
The 2025 access change means full disclosure data is now behind a paywall. Do we pursue the NGO data partnership now, or build around public scores and fill the gap with Climate Trace until funding allows?

**3. Parent Company API.**
Without a parent company mapping layer, every Shop Your Values feature breaks when a user searches for a brand name rather than its parent company. This is a Tier 2 dependency that gates multiple features. Needs a decision on cost and timing before V3 feature scoping.

**4. CFPB independence.**
The CFPB has faced political pressure in 2025/26. Data remains publicly available regardless, but the team should monitor the agency's operational status and have a contingency plan for the consumer complaints data.

**5. Wikirate evaluation.**
Connor to assess whether Wikirate's aggregation layer reduces integration complexity sufficiently to change the build sequence. This could meaningfully compress the Tier 1 build timeline.

---

## Version History

| Version | Date | Change |
|---|---|---|
| 1.0 | April 2026 | Initial eight-source first batch (Craig Hepburn independent research) |
| 2.0 | April 2026 | Full consolidation with Upendra's scoring matrix and Connor's product pager. Expanded to full Tier 1/2/3 structure. Dead sources flagged. BHRRC gap identified. Five open questions documented. |

---

*Bad Company — Internal Documentation. Not for external distribution.*
