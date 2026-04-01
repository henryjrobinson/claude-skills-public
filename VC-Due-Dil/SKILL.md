---
name: angel-investor-due-diligence
description: >
  Comprehensive due diligence analysis for early-stage angel investment opportunities, 
  syndicate deals, and startup evaluations. Triggers on: any request to evaluate or 
  analyze a startup investment, "should I invest in X", "DD on this company", "analyze 
  this deal", "look into this startup", or when the user shares a pitch deck or deal 
  memo and asks for analysis. Conducts multi-dimensional research using web search, 
  interviews the user for information only they have access to, and produces a full 
  investor-grade due diligence report. Use this skill for any angel investing, syndicate, 
  or early-stage startup evaluation request — even if the user just says "what do you 
  think about investing in [company]?"
---

# Angel Investor Due Diligence Skill

## Purpose
Perform analyst-grade due diligence on early-stage investment opportunities using all 
available public information, supplemented by targeted interviews to fill gaps that only 
the investor can provide. Output a structured DD report with a clear investment thesis, 
key risks, "What Needs To Be Believed" (WNTBB) summary, and explicit flags for what 
still requires human follow-up.

---

## Execution Protocol

### Step 0: Intake
Ask the user for the following before starting (collect in one message):
1. **Company name** and website URL
2. **Stage/round** (pre-seed, seed, Series A, etc.)
3. **Deal source** — direct, syndicate (which one?), warm intro?
4. **Any materials already received** — pitch deck, exec summary, data room, deal memo. 
   Ask user to paste key metrics or upload files if they have them.
5. **Check size** and **valuation/terms** if known (SAFE cap, discount, priced round)
6. **Your thesis angle** — why are you even looking at this? Industry expertise? 
   Someone vouched for it? FOMO? (Knowing this helps identify your blind spots.)

If the user wants to start research immediately with limited info, proceed — but note 
what's missing and interview them later in the process.

---

### Step 1: Rapid Reconnaissance (~5 web searches)
Gather baseline signal before deep diving. Search in parallel:
- `[Company] startup funding` → Crunchbase, AngelList, press
- `[Company] reviews` → G2, Capterra, App Store, Trustpilot
- `[Founder names] background` → LinkedIn, previous companies, exits
- `[Company] news` → recent press coverage, controversies
- `[Industry] market size trends 2024 2025` → TAM validation

Flag immediately if:
- Company has no web presence
- Founder backgrounds don't check out
- Obvious legal/regulatory landmines
- Saturated commodity market with no differentiation

---

### Step 2: Deep Dive Research (10 Dimensions)
Conduct thorough web research across all dimensions. Use `web_search` and `web_fetch` 
to gather information. For each dimension, produce: **Findings**, **Confidence** 
(High/Medium/Low/Unknown), and **Red Flags** if any.

#### D1: FOUNDING TEAM
The most important dimension at early stage. A great team in a bad market beats a bad 
team in a great market — usually.

Research:
- LinkedIn profiles for all co-founders: prior companies, exits, tenure, titles
- GitHub profiles (for technical founders): repos, activity, open-source credibility
- Twitter/X for founder voice, thought leadership, engagement with customers
- Any prior startups: check for failures (fine), pivots (fine), fraud (not fine)
- Domain expertise: have they lived the problem they're solving?
- Team completeness: technical + commercial co-founder? Holes in leadership?
- Advisor network: are the advisors credible and actually engaged?

Key questions to assess:
- Do they have unfair distribution or domain advantages?
- Have they shipped product before under pressure?
- Do investors/operators in the space vouch for them publicly?

#### D2: MARKET
- TAM/SAM/SOM — validate their numbers, not just accept the deck
- Market growth rate and tailwinds: regulation, tech shift, demographic change
- Market timing: why now? Is this 5 years too early or riding a current wave?
- Market structure: fragmented (good for new entrant) or concentrated (tough)
- Regulatory risk or regulatory tailwind?

Research: industry reports (search for "[industry] market size report 2024"), 
comparable public companies' investor relations, academic sources.

#### D3: PRODUCT & TECHNOLOGY
- Stage: concept, MVP, beta, GA, scaling?
- Core differentiator: IP, data moat, network effect, switching costs, unique algo?
- Patent search: Google Patents, USPTO — any granted or pending IP?
- GitHub search for technical credibility if open-source components
- Technical debt risks: can it scale? Cloud-native? Proprietary vs. commodity stack?
- Demo/product walkthrough: does the product actually exist and work?

#### D4: TRACTION & METRICS
This is your liar detector. Cross-reference everything the founder claims.

Look for / ask about:
- Revenue (ARR/MRR) and growth rate MoM
- Customer count and logo quality
- Retention/churn — NRR > 100% is exceptional; < 80% is a red flag
- DAU/MAU ratio for consumer
- Net Promoter Score or qualitative customer love signals
- LOIs, pilots, signed contracts vs. verbal commitments
- Burn multiple: net burn / net new ARR (< 1.5x is good; > 2x is a concern)

Web research: press releases, customer case studies, app store download ranks, 
SimilarWeb for web traffic, LinkedIn for employee headcount growth.

#### D5: BUSINESS MODEL & UNIT ECONOMICS
- Revenue model: SaaS, transactional, marketplace, hardware+software, usage-based?
- Pricing: is it defensible or will customers push back at scale?
- CAC and LTV: even rough estimates tell you a lot
- Gross margin profile: software (70-80%+ good), marketplace (varies), hardware (30-50%)
- Path to profitability: what does the model look like at scale?
- Are they dependent on any single customer (>20% revenue = concentration risk)?

#### D6: COMPETITIVE LANDSCAPE
Never accept the founder's competitive slide as truth.

Research:
- Search `[problem space] startup landscape 2024 2025`
- G2/Capterra category grids
- CB Insights market maps (some are public)
- Direct search for competitors in App Store, Product Hunt, AngelList
- Incumbent players: could Google/Salesforce/Microsoft just build this?

Assess:
- Is the moat defensible or is this a feature, not a company?
- What happens if a well-funded competitor enters?
- Are there well-funded direct competitors already scaling? Who raised, how much?

#### D7: FINANCIALS & FUNDRAISING HISTORY
- Current burn rate and runway
- Use of funds: is this round sized appropriately for the milestones they'll hit?
- Cap table cleanliness: founder dilution, employee pool, previous investors
- Prior round terms: down round risk? Liquidation preferences that could wash out angels?
- Revenue vs. expenses trajectory
- Any convertible notes with punishing terms (e.g., 2x liquidation preference)?

Crunchbase public data will show funding history. User must provide actual financials 
from data room — flag this explicitly.

#### D8: DEAL TERMS & VALUATION
This is where most angels get taken.

Assess:
- Entry valuation vs. comparables at same stage/traction
- Instrument: priced equity vs. SAFE vs. convertible note
  - SAFE: What cap? Pro-rata rights? MFN clause?
  - Note: Interest rate, maturity, conversion discount?
- Dilution math: what does your ownership look like at Series A after conversion?
- Pro-rata rights for follow-on?
- Information rights (you want these)
- Any side letters with other investors getting better terms?
- Lead investor quality: is a credible VC/super-angel leading and doing real work?

Search publicly for "SAFE valuation cap benchmarks [year]" and "[industry] seed 
valuations 2024" to compare.

#### D9: LEGAL, IP, & GOVERNANCE
- Incorporation state: Delaware C-Corp is the standard; anything else is a flag
- IP assignment: do founders own all the IP? (Check: university spinout? 
  Prior employer claim?)
- Pending litigation or regulatory investigations
- Key employee agreements: vesting schedules? Non-competes?
- GDPR/CCPA compliance if handling user data
- Any outstanding debt that's senior to equity?

Patent search: https://patents.google.com — search company name and founder names.

#### D10: INVESTOR SYNDICATE & SENTIMENT
- Who else is investing? Quality of co-investors is a signal
- Lead investor: known entity? Track record? Do they add value beyond capital?
- AngelList syndicate: what's the lead's deal history? Returns disclosed?
- Are known operators/domain experts in the deal? Why?
- Any investors who passed? (Hard to find but worth asking directly)
- Has this been shopped widely with no takers? (Yellow flag)

Search: `[investor name] portfolio`, AngelList syndicate reviews, Twitter/X for 
investor statements about the company.

---

### Step 3: Investor Interview
After completing research, interview the user to fill information gaps that only they 
can answer. Compile all unknown/missing items from Step 2 and ask in one organized 
message. Typical questions include:

- Have you spoken to any customers directly? What did they say?
- Do you have access to the data room? What do the financials show?
- What does the cap table look like (can you share)?
- Who is the lead investor and have you verified their commitment?
- Have you met the full founding team, or just the CEO?
- What's your personal thesis for this specific company — why do you like it?
- What would make you walk away?
- Is there any competitive deal pressure (closing date, allocation limits)?

---

### Step 4: Synthesis & Report
Produce a structured Due Diligence Report in the following format:

---

## DUE DILIGENCE REPORT: [Company Name]
**Date:** [today]  
**Stage/Round:** [X]  
**Valuation/Terms:** [X]  
**Check Size Considered:** [X]  

### Executive Summary
2-3 sentence investment thesis or anti-thesis. What is this company, why could it 
be big, and what is the single biggest risk?

### Investment Scorecard
Score each dimension 1-5 and note confidence level:

| Dimension | Score (1-5) | Confidence | Key Finding |
|---|---|---|---|
| Team | | | |
| Market | | | |
| Product/Tech | | | |
| Traction | | | |
| Business Model | | | |
| Competition | | | |
| Financials | | | |
| Deal Terms | | | |
| Legal/IP | | | |
| Investor Quality | | | |
| **TOTAL** | **/50** | | |

**Scoring guide:** 5 = exceptional, 4 = strong, 3 = adequate, 2 = weak, 1 = red flag

### What Needs To Be Believed (WNTBB)
List the 3-5 core assumptions that must prove true for this investment to return 3x+. 
Be brutally honest. If any of these feel like they require magical thinking, say so.

Example format:
1. ✅ / ⚠️ / ❌ — [Assumption] — [Confidence: evidence for/against]

### Key Risks & Mitigants
For each major risk: What's the risk? How likely? How fatal? Any mitigant?

### Red Flags
Explicit list of anything that raised a concern, even if not disqualifying.

### Green Flags
Genuine differentiators or exceptional signals.

### Data Gaps (Requires Human Action)
Explicit list of items that could not be assessed via public research and require:
- 🔐 **Paid data** (PitchBook, CB Insights): [specific data needed]
- 📞 **Reference calls**: [specific people worth calling]
- 📁 **Data room access**: [specific documents to request]
- 👥 **Customer interviews**: [how many, what to ask]
- ⚖️ **Legal review**: [anything flagged for a lawyer]

### Investment Recommendation
**Pass / Conditional Pass / Invest** — with clear reasoning.

If "Conditional Pass": list the exact conditions that would upgrade to "Invest."

---

## Notes on LLM Limitations

The following information CANNOT be reliably sourced through web research alone:
- **Actual financials** (burn rate, P&L, cap table detail) — requires data room
- **Customer reference calls** — requires phone/email outreach
- **Founder reference checks** — requires network calls
- **Term sheet fine print** — requires document review
- **Proprietary PitchBook/Crunchbase Pro data** — requires paid subscriptions
- **Background checks** — requires services like Checkr or legal due diligence firms
- **Technical architecture review** — requires a technical advisor or engineer

These items are explicitly flagged in every report under "Data Gaps."

---

## Quick Mode (Time-Limited Diligence)

If the user is on a tight timeline (e.g., closing in 48 hours), prioritize:
1. Founder background check (30 min)
2. Market validation (20 min)
3. Competitive landscape (20 min)
4. Deal terms sanity check (10 min)
5. Lead investor credibility (10 min)

Skip detailed financial modeling at pre-seed/seed — the numbers are projections anyway.

---

## Sector-Specific Add-Ons

Adjust research based on sector when mentioned:

**B2B SaaS:** Prioritize ARR growth rate, NRR, CAC payback period, ICP clarity
**Consumer/Marketplace:** Prioritize DAU/MAU, retention cohorts, viral coefficient, 
GMV take rate
**Deep Tech/Biotech:** Prioritize IP position, technical advisory board, regulatory 
pathway, time to revenue
**Fintech:** Prioritize regulatory compliance, bank partnerships, unit economics on 
financial products
**Hardware:** Prioritize BOM costs, supply chain, manufacturing partner, margin profile
**AI/ML:** Prioritize data moat, fine-tuning vs. wrapper risk, defensibility vs. 
foundation model providers
