# ArthSaathi — startup action plan
**Prepared:** July 2026 · Confidential
**Team:** Prashant (CEO/Founder) · Pratik · Ashish · Shashi

---

## 1. What we're building

ArthSaathi is a personal finance app for India. It connects all of a user's financial accounts — loans, investments, credit cards, bank accounts — through the RBI's Account Aggregator (AA) framework, gives them a complete financial picture for the first time, and delivers CFP-grade advice in Hindi and English via AI.

One-line pitch:
> "500 million Indians manage money across 7 apps. ArthSaathi gives them one screen that shows everything — and an AI that tells them exactly what to do next."

---

## 2. What is Account Aggregator (AA)?

Account Aggregator is a data-sharing framework created by the Reserve Bank of India (RBI) in 2021. It lets individuals share their financial data — bank account statements, loan details, investment holdings, insurance policies — across institutions, with their explicit consent, in a standardized digital format.

Without AA: a bank wanting to verify your income asks for 6 months of bank statements as a PDF. You print them, sign them, scan them, send them. Data arrives late, manually, and only one institution sees it.

With AA: the same data travels digitally, in real-time, directly from your bank to whoever you authorized — in seconds, with one consent tap.

Three types of participants in the AA ecosystem:
- FIP (Financial Information Provider): institutions that hold your data — banks, mutual fund houses, insurance companies
- FIU (Financial Information User): apps that request your data with your consent — ArthSaathi would register as an FIU
- AA (Account Aggregator): the RBI-licensed intermediary that routes consent and data between FIP and FIU, without storing any of it

One important point: AA is read-only. No app can move, withdraw, or transact on your money through it. It can only read and display.

Where the ecosystem stands today (Source: Sahamati, Dec 2025):
- 2.6 billion accounts enabled across FIPs
- 252 million users who have linked at least one account
- 151 live FIPs (including all major public and private sector banks)
- 435 registered FIUs

The pipes are live. The consumer product on top of them doesn't exist yet.

---

## 3. The team

| Role | Person | Responsibility |
|---|---|---|
| Founder / CEO | Prashant | Product vision, business development, bank/NBFC relationships, regulatory, fundraising |
| Tech Lead | Pratik | Architecture, React Native app, backend, API integrations, project coordination |
| Developer | Ashish | Backend, Node.js, database, AA integration |
| Developer | Shashi | Frontend, React Native, UI/UX |

All four — Prashant, Pratik, Ashish, and Shashi — draw salary and consulting fees from the company at the same level, funded from the angel raise. This is not a founder-takes-equity-only structure. Everyone gets paid from Day 1 once the round closes. IP goes to the company from Day 1. This has to be in writing before any build work starts.

---

## 4. Why now

- 435 FIUs are registered, 151 banks are live as FIPs, 252M+ users have linked accounts on AA. Nearly all AA usage today is B2B — lenders pulling borrower data to verify income. Consumer-facing AA apps are almost nonexistent. (Source: Sahamati, Dec 2025)
- India has roughly 7,000 FPSB-certified financial planners and 1,300 SEBI-registered investment advisers for a population of 1.4 billion. (Source: FPSB India, SEBI, 2024) A CFP charges ₹2,000–8,000/hour for advisory sessions, or ₹10,000–50,000 for a comprehensive financial plan. (Source: FPSB India member surveys) Most households can't afford structured advice.
- Millions of Indians carry loans across 2-3 different institutions simultaneously — personal loans, home loans, vehicle loans — and have no visibility into their combined debt picture. (Source: TransUnion CIBIL Report, 2024)
- Fi Money and Jupiter need banking licenses. CRED is rewards. ET Money is MF. OneScore is credit only. Nobody has built a unified dashboard + AI advisor + product marketplace on top of AA for consumers.

---

## 5. MVP — what we build first

Build two things well. Everything else waits.

### Module 1 — Unified financial dashboard (via AA)
- User goes through one AA consent flow
- App fetches all bank accounts, loans, investments, credit cards
- Single screen: net worth, total EMI burden, investment portfolio, credit utilisation, monthly cash flow
- Auto-updates, no manual data entry

### Module 2 — AI financial advisor
- Conversational, Hindi + English
- AI has full context of the user's AA-fetched data
- Specific and actionable, not generic tips
- Example: "Your HDFC card is charging 42% interest. You have ₹60K sitting in savings. Pay the card off — saves you ₹14,000 this year."
- Year 1: powered by frontier LLM APIs (OpenAI, Anthropic, Google — or a combination). Year 2: migrates to ArthSaathi's own fine-tuned model. (See Section 13)

Why only these two: every other module is something users will want once they trust ArthSaathi with their financial data. The dashboard + advisor combination earns that trust. It also demos in 60 seconds, which matters for angel pitches.

### What's not in the MVP
- Aadhaar eKYC (PAN only first — simpler to set up, sufficient for most flows)
- Investment rebalancing
- Goals planner
- Insurance POSP integration
- White-label for banks
- Full marketplace (just DSA referral links to start)

---

## 6. What can launch without license dependency

Several things can go live before the FIU registration is done — and some before the company is even registered. The clock starts ticking on user acquisition from Day 1.

### No license needed — launch immediately
- Landing page with waitlist and financial calculator tools (EMI calculator, SIP calculator, loan eligibility — just math, no regulatory activity)
- Financial literacy content (blog, newsletter — content publishing, no license)
- Credit card affiliate links via EarnKaro, BankBazaar, CreditMantri — ArthSaathi acts as a content publisher linking to products, not advising. ₹500–3,000 per approved card application. (Source: EarnKaro and BankBazaar public partner terms)
- Basic budgeting tool with user-entered data (no AA, no advice, no license)

### After simple registration (2-4 weeks, low barrier)
- Loan referrals via DSA — just a referral link with a commission. Bajaj Finserv and Tata Capital DSA registration takes 2-3 weeks via their online portals.
- Insurance referrals via IRDAI POSP — 15-hour online training + exam via Turtlemint or Coverfox, 2-3 weeks.

### After FIU registration (4-6 weeks via Setu)
- AA-powered unified dashboard (the core product)
- AI advisor with live AA account data

### Not in Year 1
- Direct investment advice requiring SEBI RIA license — complex, expensive (₹3L+ registration fee, minimum qualification requirements), 6+ month process. Not worth pursuing early.

---

## 7. The 7 modules in detail

Add a new module only after the previous one has 1,000 active users. This is not conservative — it's how you avoid shipping 7 half-built features that nobody returns for. Modules 1 and 2 are the MVP. Modules 3-7 follow in sequence.

---

### Module 1 — Unified Financial Dashboard
Status: MVP · Launch: Month 3-4 · License: FIU registration (Setu, 4-6 weeks)

The core product. One AA consent flow; the app fetches everything — every bank account, every loan, every investment, every credit card — and shows it on a single screen. No manual data entry. Updates automatically.

- Net worth (assets minus liabilities, live from AA)
- All bank balances in one view
- Total EMI burden and upcoming payment calendar
- Investment portfolio value across mutual funds, PPF, NPS, EPF, SGB
- Credit card utilisation across all cards
- Monthly cash flow (income vs. spend, derived from bank transactions)
- Last-synced timestamp per institution

Revenue here is indirect — no direct commission from the dashboard itself. It earns trust, and trust drives every downstream marketplace conversion.

Most users have never seen their complete financial picture in one place. The first time someone opens ArthSaathi and sees ₹4.7L in HDFC + ₹1.2L in SBI + ₹8.3L in Zerodha + ₹22L remaining on home loan — all on one screen — that's the moment they stay.

---

### Module 2 — AI Financial Advisor
Status: MVP · Launch: Month 3-4 · License: None for general financial information; SEBI RIA needed for direct investment advice (avoid — frame all outputs as information, not directives)

Conversational AI that has read every number in the user's AA dashboard before they ask the first question. Responds in Hindi, English, or both — however the user writes.

- Full AA data context in every response (knows your actual accounts, not hypotheticals)
- Specific and actionable: "You have ₹60K idle in savings and a credit card charging 42% — pay the card off first, saves ₹14,000 this year"
- Proactive alerts: "Your HDFC home loan EMI increases by ₹3,200 next month — your floating rate reset is due"
- Hindi-English code-switching: handles "mera SBI account mein kitna hai and should I do FD?" naturally
- Conversation history — remembers what the user asked last week
- Year 1: frontier LLM APIs. Year 2: ArthSaathi's own FLM (see Section 13)

Revenue is indirect in Year 1 — the advisor is the primary retention driver. In Year 2, a premium tier gates deeper features (unlimited queries, proactive alerts, tax planning).

On compliance: frame all AI outputs as "information" and "options," not directives. "Based on your accounts, prepaying the loan could save X" is fine. "You should invest in Fund Y" crosses into SEBI RIA territory. Every response needs a one-line disclaimer at the bottom.

---

### Module 3 — Loan Suite
Status: Post MVP · Launch trigger: 1,000 active users on dashboard · License: DSA registration (already planned; needed for referral commissions, not for the tracker itself)

A complete loan management hub built on top of the AA data already flowing in. Every active loan the user has is pulled automatically — no manual entry.

- All loans in one view: personal, home, vehicle, education, credit card outstanding
- EMI calendar — upcoming payment dates across all lenders
- Remaining tenure tracker per loan
- Prepayment calculator: "If you pay ₹50,000 extra on your HDFC loan today, you save ₹1.4L in interest and close 8 months early"
- Refinancing alert: "SBI is offering home loans at 8.5% — your current rate is 9.2%. Switching could save ₹3,200/month" (referral via DSA)
- Debt payoff prioritizer: recommends which loan to close first based on interest rate, tenure, and cash flow

Every refinancing or new loan taken through ArthSaathi earns 0.5-1.5% of disbursement — this is the primary DSA commission source.

---

### Module 4 — Financial Health Score
Status: Post MVP · Launch trigger: Loan Suite at 1,000 active users · License: None (proprietary ArthSaathi score, not a regulated credit score)

A monthly composite score — ArthSaathi's own measure of overall financial health, separate from CIBIL which only measures credit repayment. Gives users a single number that reflects the full picture.

Score components:
| Component | Weight | What it measures |
|---|---|---|
| Credit utilisation | 20% | Credit card outstanding vs. limit (from AA) |
| Debt-to-income ratio | 25% | Total monthly EMI vs. income (from AA transactions) |
| Savings rate | 20% | Monthly savings as % of income |
| Emergency fund coverage | 15% | Liquid savings vs. 3-month expense benchmark |
| Investment diversification | 10% | Spread across equity, debt, gold |
| Loan repayment track record | 10% | On-time EMI payments (from AA loan data) |

- Score on a familiar 300-900 scale (mirrors CIBIL for intuitive reading)
- Month-on-month trend with explanation
- "What's dragging your score" — specific breakdown by component
- Personalized action: "Pay down your Axis card to below 30% utilisation — adds ~40 points"

The detailed score breakdown is a premium tier gate — free users see the number, paid users see the full breakdown. It also drives marketplace: "your debt-to-income is high because of the personal loan — here are refinancing options."

---

### Module 5 — Marketplace
Status: Post MVP · Launch trigger: Parallel with Modules 3-4 · License: DSA registration + IRDAI POSP + credit card affiliate + AMFI ARN (mutual fund distribution)

The revenue engine. All product recommendations surface inside the AI advisor's responses — not a separate product catalogue. When the AI says "your HDFC card rate is high," it follows up with "here are two cards with lower rates." Those are affiliate links.

| Category | Commission | License needed |
|---|---|---|
| Personal loans | 1-1.5% of disbursement | DSA registration |
| Home loans | 0.5-1% of disbursement | DSA registration |
| Credit cards | ₹500-3,000 per approved card | Affiliate agreement (EarnKaro, BankBazaar) |
| Term insurance | Up to 35% first-year premium | IRDAI POSP |
| Health insurance | Up to 15% per policy | IRDAI POSP |
| Mutual funds | 0.5-1% trail commission | AMFI ARN registration |
| Fixed deposits | Referral fee (varies by bank) | None |

On AMFI ARN: registering as a mutual fund distributor with AMFI is separate from, and much simpler than, a SEBI RIA license. It allows ArthSaathi to earn trail commissions on MF investments routed through the app. Registration takes 4-6 weeks. (Source: amfiindia.com) Add this to the action list — it's not yet tracked in the 30-day plan.

The Marketplace is the primary revenue driver across all milestones.

---

### Module 6 — Goals Planner
Status: Post MVP · Launch trigger: Financial Health Score at 1,000 active users · License: None for goal tracking; AMFI ARN sufficient for product recommendations toward goals

Structured savings goal management. Because the AI already knows the user's real financial situation from AA, goal recommendations are grounded in what they actually have — not generic rules of thumb.

Goal types:
- Emergency fund (benchmark: 3-6 months of expenses)
- Home purchase (down payment target + timeline)
- Child's education (projected cost + years to target)
- Retirement (target corpus + expected age)
- Vehicle purchase
- Vacation / large purchase
- Custom goal

- Auto-calculates required monthly savings based on current balance, timeline, and expected returns
- Progress tracking auto-updated from AA data — no manual entry
- "You're ₹12,000/month short of your home down payment goal — here's where that gap can come from"
- Goal-linked product suggestions: emergency fund → liquid mutual fund; education goal → ELSS for tax saving + growth
- AI milestone alerts: "You'll hit your emergency fund target 2 months early at current pace"

Revenue comes from marketplace conversions — goal-based product recommendations (MF SIPs, RDs, savings accounts).

---

### Module 7 — Investment Hub
Status: Post MVP · Launch trigger: Goals Planner at 1,000 active users · License: AMFI ARN for MF distribution. SEBI RIA not needed if outputs are framed as analytics, not direct advice.

A complete view of the user's investment portfolio, pulled from AA — mutual funds, stocks, PPF, NPS, EPF, Sovereign Gold Bonds. The insight here is cross-platform: Groww shows you your Groww holdings, Zerodha shows you your Zerodha holdings. ArthSaathi shows everything together.

- All holdings in one screen: equity, debt, gold, alternatives
- XIRR calculation per fund and overall portfolio
- Portfolio breakdown: equity vs. debt vs. gold vs. real estate
- Benchmark comparison: "Your portfolio XIRR is 11.2% vs. Nifty 50 at 14.3% over the same period"
- Tax impact summary: LTCG, STCG, and dividend tax estimates for the current financial year
- Diversification analysis: "82% of your equity is large cap — your stated risk profile supports adding mid/small cap"
- Rebalancing suggestion (informational): "Your target was 60:40 equity:debt — current is 74:26 after market run-up. Options: [explained]"

Revenue comes from AMFI trail commissions on new SIP investments initiated through ArthSaathi, and from the tax impact report as a paid premium feature.

The compliance line here is the same as Module 2: "Here is your portfolio composition" and "here are rebalancing approaches" are information. "Buy Fund X" is direct advice requiring SEBI RIA. Stay on the right side.

---

### Module overview

| Module | MVP / Post | Launch trigger | License needed | Revenue type |
|---|---|---|---|---|
| 1. Unified Dashboard | MVP | Month 3-4 | FIU registration | Indirect (retention) |
| 2. AI Advisor | MVP | Month 3-4 | None (frame as info) | Indirect + premium tier |
| 3. Loan Suite | Post MVP | 1,000 dashboard users | DSA registration | DSA commissions |
| 4. Financial Health Score | Post MVP | Loan Suite at 1,000 | None | Premium tier gate |
| 5. Marketplace | Post MVP | Parallel with 3-4 | DSA + POSP + AMFI ARN | Primary revenue driver |
| 6. Goals Planner | Post MVP | Health Score at 1,000 | AMFI ARN | MF SIP commissions |
| 7. Investment Hub | Post MVP | Goals Planner at 1,000 | AMFI ARN | Trail commissions + premium |

---

## 8. 12-month roadmap

### Month 0 — Foundation
All four working in parallel.

- [ ] Company registered as Private Limited (not LLP — required for equity rounds)
- [ ] Salary and consulting agreements signed — scope, fees, IP assignment, timeline — for all four at same level
- [ ] Setu AA sandbox access requested (free, no registration needed)
- [ ] Angel pitch deck drafted (see Section 9)
- [ ] Landing page live with waitlist + calculator tools
- [ ] DSA registration started with Bajaj Finserv + Tata Capital (2-3 weeks, can start now)
- [ ] Affiliate links live on landing page (EarnKaro, BankBazaar)

### Month 1-2 — Pitch and build in parallel
- [ ] 3-5 angel conversations started
- [ ] Tech architecture finalized, stack locked; LLM API provider(s) selected
- [ ] AA consent flow built on Setu sandbox
- [ ] Unified dashboard in React Native — design and build
- [ ] AI advisor — basic integration with AA data
- [ ] FIU registration process started with Setu (20-30 working days once initiated)
- [ ] Apply to Antler India (next cohort — see Section 9B)
- [ ] Apply to 100X.VC
- [ ] Provisional patent filed (see Section 12)
- [ ] Start building FLM training dataset in background (see Section 13)

### Month 3 — Angel round closes
- [ ] ₹75L–1Cr raised
- [ ] Salary and fees for all four funded from round
- [ ] MVP beta with 20-30 real users
- [ ] DSA registration done, first referral links live
- [ ] FIU registration complete or near

### Month 4-5 — Beta and first revenue
- [ ] 200-500 users with AA consent completed
- [ ] First DSA commission earned
- [ ] IRDAI POSP license active, first insurance referrals live
- [ ] Waitlist conversion campaign running
- [ ] 10 user interviews minimum
- [ ] Accelerator decision (if Antler or 100X progresses)

### Month 6 — Milestone review
What we committed to showing angels:
- 500+ users with active AA connections
- ₹1-3L/month in DSA + affiliate revenue
- FIU registration complete
- Product stable, no critical bugs

### Month 7-9 — Expand
- [ ] Loan Suite launched
- [ ] Financial Health Score live
- [ ] Basic marketplace integrated (loan products, insurance options)
- [ ] 2,000+ active users
- [ ] ₹3-5L/month revenue
- [ ] FLM training dataset at 20,000+ examples — ready for fine-tuning

### Month 10-12 — Seed prep
- [ ] 5,000+ MAU with AA connections
- [ ] ₹5-8L/month revenue
- [ ] Goals Planner + Investment Hub in development
- [ ] 2-3 NBFC conversations for B2B pipeline
- [ ] Seed deck done: target ₹3-5Cr
- [ ] FLM fine-tuning initiated (Year 2 deployment target)
- [ ] Apply to Surge (Peak XV) — traction should be there by now

---

## 9. Fundraising plan

### 9A — Angel round

**Target:** ₹75L–1Cr
**Timeline:** Month 1-3
**Dilution:** 10-15% is standard at this stage

Angels investing at this stage get:
- First mover in a consumer AA product that doesn't exist yet
- Working prototype
- AI advisor integrated
- Trademark + provisional patent filed
- Revenue model earning from Day 1 (DSA commissions, affiliate links)
- FLM roadmap — proprietary model in Year 2 as a long-term cost and moat advantage
- Full technical team already committed

Use of funds:
| Item | Amount |
|---|---|
| Salary + consulting fees — Prashant, Pratik, Ashish, Shashi (6 months, same level) | ₹48-60L |
| AWS + LLM API costs (Setu, Firebase, AI providers) | ₹5L |
| Legal + compliance (FIU registration, CA, agreements, patent) | ₹8L |
| Marketing + beta acquisition | ₹5L |
| Buffer | ₹3-5L |
| **Total** | **₹69-83L** |

Target angel networks:

| Network | Why | Cheque range | How to approach |
|---|---|---|---|
| 100X.VC | Pre-revenue, pre-product — exact fit. Standard deal: ₹25L for 1% SAFE (Source: 100x.vc public terms) | ₹25L | Apply at 100x.vc — rolling |
| Mumbai Angels | Strong fintech track record, backed 2 unicorns | ₹25L–1Cr | Warm intro preferred, direct also works |
| Indian Angel Network (IAN) | Largest network in India, fintech-friendly | ₹25L–2Cr | iangroupindia.com |
| LetsVenture | Platform-based, reaches many angels at once | ₹10L–2Cr | Create a profile at letsventure.com |
| Ah! Ventures | Pune-based, Prashant's home city, warm network likely | ₹10L–50L | Direct outreach |
| Fintech angels | Kunal Shah (CRED), Jitendra Gupta (Jupiter), Nitin Gupta (Uni Cards) — all active fintech angels | ₹10L–1Cr | LinkedIn + warm intro |

The pitch deck — 10 slides:
1. Problem — fragmented finance, no complete picture, advisor access gap
2. Solution — AA-powered dashboard + AI advisor
3. What is AA — 30-second explainer, 252M+ users already linked (Source: Sahamati, Dec 2025)
4. Product — demo screenshots or video
5. Market — India's retail loan book: ₹22 lakh crore (Source: RBI, 2023-24); insurance new business premium: ₹3.2 lakh crore (Source: IRDAI, 2023-24); even 1% capture of DSA + POSP commissions = large revenue
6. Business model — 4 revenue streams, DSA commissions from Day 1
7. Traction — prototype live, trademark + provisional patent filed, waitlist started
8. Competition — why this is different from Fi, Jupiter, CRED, ET Money
9. Team — all four, roles, commitment
10. Ask — ₹75L–1Cr, 12-month milestones, use of funds

---

### 9B — Accelerators

Apply to these alongside angel conversations. Accelerator acceptance makes angel conversations easier.

**Antler India** — best fit for this stage

Cohort-based residency for AI-first startups at idea or early stage. Investment: ₹4Cr for 11% equity + ₹2L grant + $1M Azure credits. (Source: Antler India public program page) AI-first, early stage, full-time residency — this fits. Apply at antler.co/location/india. Watch for cohort dates.

**100X.VC**

Pre-product, pre-revenue stage. ₹25L for 1% SAFE. (Source: 100x.vc) Zero traction required, rolling applications. Apply at 100x.vc.

**Surge (Peak XV / Sequoia)**

$1-3M for ~7-10%. The most well-known accelerator in India. Not the right timing — Surge requires defensible traction and the ability to deploy $1M in 90 days. Apply after Month 6 when there are 500+ active users and first revenue. (Source: peakxv.com/surge program requirements)

**Google for Startups Accelerator India**

AI-focused and equity-free. Google Cloud credits + mentorship, no dilution. Worth applying. Watch for the 2026-27 application cycle.

**RBI Regulatory Sandbox**

Allows testing regulated fintech products before full go-live. Could help with FIU registration timeline and adds credibility. Cohort-based, limited spots — apply if the timing aligns.

---

## 10. Company setup

Do this in Month 0. Nothing gets built until the company is registered and agreements are signed.

### Private Limited registration
- [ ] Engage a CA — budget ₹15-25K (Source: standard MCA21 registration with CA assistance)
- [ ] Decide on registered office address (Pune)
- [ ] DSC (Digital Signature Certificate) for all directors — 1-2 days
- [ ] DIN (Director Identification Number) for all directors
- [ ] File SPICe+ on MCA21
- [ ] Name approval — have 3 options ready (ArthSaathi is primary)
- [ ] Draft MOA + AOA
- Timeline: 2-3 weeks. Cost: ₹15-25K.

### Share structure (suggested)
| Shareholder | % |
|---|---|
| Prashant | 80% |
| ESOP Pool | 10% |
| Reserved (co-founder/advisor) | 10% |

Keep it simple at registration. The angel round dilutes from here.

### Agreements — sign before any work starts
- Salary agreement for Prashant (as director/employee of the company)
- Consulting agreements for Pratik, Ashish, Shashi: scope, monthly fee (same level as Prashant's salary), IP assignment, confidentiality, exit terms
- IP assignment: all code, designs, documents, and model training data are company property from Day 1
- NDA: all parties + anyone given access to the concept

---

## 11. Regulatory and compliance

### FIU registration (Account Aggregator)

ArthSaathi needs to register as a Financial Information User (FIU) with Sahamati + RBI to legally pull user financial data via the AA framework. It sounds bureaucratic. It's actually 4-6 weeks.

Register through Setu as a Technical Service Provider (TSP). Setu handles the Sahamati certification through Aujas — their empanelled certifier. Timeline: 20-30 working days after initiation. (Source: Setu documentation, setu.co) Start immediately after company registration.

Contact: partnerships@setu.co. Request sandbox access first — free, no registration needed.

Steps:
1. Company registered
2. Contact Setu, request FIU onboarding
3. Sahamati certification via Aujas
4. Sandbox testing
5. Production go-live

### DSA registration (loan commissions)
- Bajaj Finserv: online portal, 2-3 weeks, minimal documentation
- Tata Capital: similar, start in parallel
- HDFC: longer process, start Month 2
- Prashant can register personally before the company is ready, then transfer later

### Insurance POSP license
- Via Turtlemint (easiest path) or Coverfox
- Requires 10th pass certificate + 15-hour online training + exam
- 2-3 weeks, low cost
- Prashant can do this in Month 1 while the app is being built

### DPDP Act 2023
- India's data protection law covers financial apps
- Privacy Policy, T&C, data processing agreements — reportedly already drafted
- The AA consent framework is DPDP-compliant by design (consent-based architecture)
- FLM training on user data requires explicit additional consent — build this into the onboarding flow from the start

### VAPT (Security Audit)
- Mandatory before production launch
- Budget ₹2-3L for a CERT-In empanelled auditor (Source: CERT-In empanelled vendor pricing, 2024)
- Schedule for Month 4 — after MVP is built, before beta opens

---

## 12. Patent

India's Patents Act, Section 3(k), excludes "a mathematical or business method or a computer programme per se or algorithms." Pure software patents don't work here. However, the Indian Patent Office does grant patents on computer-implemented inventions (CIIs) when the invention has a "technical character" — meaning it produces a specific technical effect beyond just executing code on a computer.

For ArthSaathi, three areas are worth filing on:

1. Method for real-time multi-source financial data consolidation via AA consent + LLM-based advisory generation — the specific technical process of receiving AA-structured financial data from multiple FIPs simultaneously, normalizing across institution formats, constructing a real-time context window, and generating personalized financial advice via an AI model. Novel because no prior art exists with this specific architecture.

2. Financial Health Score computation method — if the scoring model uses a novel combination of inputs (credit utilisation, AA-derived debt-to-income, savings velocity, investment diversification across AA-linked accounts) with a specific technical implementation, it qualifies as a method patent, not just a formula.

3. Method for fine-tuning a multilingual language model on consent-based AA financial data for Indian personal finance advisory — the FLM training process using AA-structured data + anonymized user interaction data to fine-tune a multilingual model for Indian financial domain and Hindi-English code-switching. Technically specific and novel enough to include in the provisional filing.

What cannot be patented: the idea of an AI financial advisor (too abstract), the AA consent flow itself (not novel — Sahamati designed and published it), DSA commission business model (explicitly excluded as a business method), and the Financial Health Score as a concept without a specific technical implementation.

India's software patent system is uncertain — grants can take 4-7 years and are sometimes refused at the complete application stage. Filing is still worth it for two reasons: it establishes a priority date (competitors can't claim they invented the same approach after your filing date) and "patent pending" is a credibility signal in pitch decks.

Recommended path:
1. Engage a patent attorney with software/fintech experience — ₹15-25K for initial consultation and provisional strategy
2. File a provisional application within 30 days of company registration — government fee: ₹1,500-6,000 for small entities (Source: Indian Patent Office fee schedule); gives 12 months to file the complete specification
3. Total cost for provisional including attorney: ₹20-40K
4. If there's any international expansion plan, file a PCT (Patent Cooperation Treaty) application alongside the provisional — protects priority in 150+ countries, costs ₹1-2L additional

---

## 13. Fine-tuned Language Model (FLM)

### Why build one

Year 1: ArthSaathi's AI advisor runs on frontier LLM APIs — OpenAI, Anthropic, Google, or a combination. That's the right call for the MVP. Fast to set up, high quality, no ML overhead.

It doesn't scale, though. Four problems compound as the user base grows.

API calls run ₹0.5–3 per query depending on model and token count. (Source: OpenAI, Anthropic, Google published pricing, 2025) At 5,000 MAU each asking 5 questions/day: 25,000 queries × ₹1 average = ₹25,000/day = ₹7.5L/month in API costs alone. That's the entire Month 12 revenue target, gone.

Domain knowledge is the second problem. Frontier models know about 401(k)s and ISAs. They don't natively understand PPF, NPS, ELSS, or how Section 80C works in practice. Every query needs Indian context injected in the system prompt — extra tokens, extra latency, extra cost.

Third: real Indian users mix languages mid-sentence. "Mera HDFC account mein kitna hai, and should I pay off the loan or invest?" Frontier models handle this inconsistently.

And the privacy issue: every financial question travels to a third-party server. A proprietary model keeps data on ArthSaathi's own infrastructure — a cleaner story for users and for regulators under DPDP Act 2023.

### Base model options

The FLM starts with an open-source base model. Three viable choices:

| Base Model | Why it fits | Source |
|---|---|---|
| Llama 3.1 8B / 3.2 | Meta open-source, strong multilingual baseline, instruction-tuned, commercial use allowed | llama.meta.com |
| Mistral 7B | Strong multilingual, small footprint, fast inference, Apache 2.0 | mistral.ai |
| Sarvam-1 / Sarvam-2B | Indian company, trained natively on 10 Indian languages including Hindi, purpose-built for Indian context | sarvam.ai |

Sarvam AI is worth a direct conversation — they may be open to partnership or joint development, and their models already handle Hindi natively without fine-tuning. (Source: sarvam.ai)

### Training data

Available immediately, before any users are on the platform:
- RBI circulars, Master Directions, and guidelines (rbi.org.in)
- SEBI product regulations and circulars (sebi.gov.in)
- IRDAI regulations (irdai.gov.in)
- Income Tax Act provisions: Section 80C, 80D, 24B, HRA exemptions, LTCG/STCG rules
- AMFI mutual fund product documentation and regulations
- Synthetic Q&A pairs — generate 10,000–50,000 Hindi-English bilingual personal finance scenarios using frontier LLMs, then have a qualified finance professional verify accuracy
- Publicly available Indian financial literacy content

From the product once live, with explicit opt-in consent:
- Anonymized user questions and AI responses
- Patterns in what financial queries Indian users actually ask
- Common misunderstandings about NPS, ELSS, SGB, and similar products

A dataset of 50,000–100,000 high-quality examples is sufficient to fine-tune a 7B–8B model to strong domain expertise. (Source: published fine-tuning benchmarks, Hugging Face research, 2024)

### Phased build plan

| Phase | Timeline | What happens | Cost |
|---|---|---|---|
| Phase 1 — APIs | Year 1 | Frontier LLM APIs. Log queries + responses with user consent. Build dataset in background. | ₹15-75K/month, grows with users |
| Phase 2 — Fine-tune | Year 2, Q1 | Fine-tune base model on ArthSaathi dataset. Evaluate against frontier LLM on Indian finance benchmarks. | ₹2-5L one-time (GPU compute on AWS/GCP) |
| Phase 3 — Self-host | Year 2, Q2 | Deploy fine-tuned model on AWS. Run in parallel with frontier API; shift traffic gradually. | ₹20-40K/month vs. ₹75K-1.5L/month on APIs at 5,000 MAU |
| Phase 4 — On-device | Year 3 | Quantized model (INT4/INT8) on-device. No server query for basic questions. Full offline capability. | Primarily engineering cost |

Break-even on fine-tuning investment: roughly 2,000–3,000 MAU at typical query volumes — around the Month 9-10 milestone.

### The moat

The AA integration is replicable. Any company can register as an FIU and connect Setu. The UI is replicable. The FLM trained on ArthSaathi's proprietary dataset — real Indian users talking about their actual financial situations, with their consent — cannot be replicated without:

- The same volume of real Indian financial queries
- The same regulatory training corpus built and verified by domain experts
- The same training compute and ML expertise

This is what makes ArthSaathi defensible in Year 3+, not the MVP.

The FLM training method is included in the patent provisional filing as claim 3 (see Section 12). File both together.

### Resources
- Fine-tuning documentation: huggingface.co/docs/transformers/training
- Sarvam AI (potential partner): sarvam.ai
- AWS SageMaker for training + inference: aws.amazon.com/sagemaker

---

## 14. Revenue — when and how much

### From Month 0-1 (before the app is built)

Credit card affiliates via EarnKaro, BankBazaar, CreditMantri:
- Zero setup cost, no license required
- Referral links on the landing page and waitlist emails
- ₹500–3,000 per approved card application (Source: EarnKaro/BankBazaar published partner rates)
- Even 5-10 approvals a month = ₹5-20K. Small, but it proves Day 1 earning.

### From Month 3-4

DSA loan commissions (after DSA registration + first users):
- Personal loan: 1-1.5% of disbursement. On a ₹5L loan: ₹5,000–7,500 commission (Source: standard DSA partner agreements, Bajaj Finserv/Tata Capital)
- Home loan: 0.5-1% of disbursement. On a ₹30L loan: ₹15,000–30,000 (Source: same)
- Target: 20 referrals/month by Month 6 → ₹1.5-3L/month

Insurance POSP (after IRDAI license):
- Term insurance: up to 35% of first-year premium for regular-pay policies (Source: IRDAI commission regulations)
- Health policy: up to 15% per policy (Source: IRDAI regulations)
- Target: 10 policies/month by Month 6 → ₹30-75K/month

### Revenue targets

| Milestone | Monthly revenue | Primary source |
|---|---|---|
| Month 3 (angel close) | ₹0–50K | Affiliate links only |
| Month 6 (angel check-in) | ₹1–3L | DSA + affiliate + insurance |
| Month 12 (seed prep) | ₹5–8L | DSA + marketplace + POSP |

### B2B SaaS

Not Year 1. Bank sales cycles run 6-12 months and the pitch doesn't land without user volume. Focus entirely on B2C in Year 1. After 5,000 users with AA data on the platform, the NBFC pitch changes — "we already have X users who have consented to data sharing" is a different conversation than a cold deck.

---

## 15. Risk register

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Angel round takes longer than 3 months | Medium | High | Run angel + accelerator tracks in parallel. Keep burn low. |
| FIU registration delayed | Low | Medium | Setu as TSP compresses this to 4-6 weeks. Start immediately after company registration. |
| AA consent drop-off — users don't complete the flow | High | High | Invest in onboarding UX. One tap, not a form. |
| LLM API costs spike at scale | Medium | Medium | FLM roadmap mitigates this in Year 2. Year 1: rate limits, caching, cheaper models for simple queries. |
| Competitor (Fi, Jupiter) ships AA + AI feature | Low-Medium | High | Speed is the only moat right now. Get to 5,000 users before they notice. |
| DSA + AI advice conflict of interest (regulatory) | Medium | High | Full disclosure on every recommendation. Keep advisory and marketplace visually separate. |
| Bank FIP integration gaps | Medium | Medium | Test all major FIPs in sandbox. Manual entry as fallback for edge cases. |
| FLM training data quality | Medium | Medium | Every synthetic Q&A pair reviewed by a qualified finance professional before training. |
| Consulting team bandwidth — other active projects | Medium | High | Lock in weekly hour commitment in agreements before build starts. |

---

## 16. Immediate action items — next 30 days

### This week
| # | Action | Owner | Deadline |
|---|---|---|---|
| 1 | Engage a CA for Pvt Ltd registration | Prashant | Week 1 |
| 2 | Draft salary + consulting agreements — scope, fees, IP clause | Pratik | Week 1 |
| 3 | Request Setu AA sandbox access | Prashant | Week 1 |
| 4 | Start DSA registration — Bajaj Finserv | Prashant | Week 1 |
| 5 | Start IRDAI POSP training via Turtlemint | Prashant | Week 1 |
| 6 | Affiliate links live on landing page | Pratik | Week 1 |

### Week 2
| # | Action | Owner | Deadline |
|---|---|---|---|
| 7 | Salary + consulting agreements signed by everyone | All | Week 2 |
| 8 | Angel pitch deck — first draft | Pratik + Prashant | Week 2 |
| 9 | Landing page live with waitlist + calculator tools | Shashi | Week 2 |
| 10 | MVP tech architecture finalized; LLM API provider(s) selected | Pratik + Ashish | Week 2 |
| 11 | Apply to 100X.VC | Prashant | Week 2 |
| 12 | Start compiling RBI/SEBI/IRDAI documents for FLM dataset | Ashish | Week 2 |

### Week 3-4
| # | Action | Owner | Deadline |
|---|---|---|---|
| 13 | Company registration complete | Prashant + CA | Week 4 |
| 14 | FIU registration initiated with Setu | Prashant | Week 3 |
| 15 | Apply to Antler India | Prashant | Week 3 |
| 16 | Provisional patent filed (3 claims incl. FLM method) | Prashant + attorney | Week 4 |
| 17 | Pitch deck finalized + rehearsed | Prashant | Week 4 |
| 18 | Sprint 1 started — auth + onboarding | Ashish + Shashi | Week 3 |
| 19 | First 3 angel conversations booked | Prashant | Week 4 |

---

## 17. Key contacts and resources

| Resource | Link / Contact |
|---|---|
| Setu AA sandbox | docs.setu.co/data/account-aggregator |
| Setu partnership | partnerships@setu.co |
| Sahamati | sahamati.org.in |
| 100X.VC application | 100x.vc |
| Antler India | antler.co/location/india |
| Mumbai Angels | mumbaiangels.com |
| Indian Angel Network | iangroupindia.com |
| LetsVenture | letsventure.com |
| Ah! Ventures (Pune) | ahventures.in |
| Bajaj Finserv DSA | bajajfinservmarkets.in/dsa |
| Turtlemint POSP | turtlemint.com/posp |
| EarnKaro affiliate | earnkaro.com |
| BankBazaar affiliate | bankbazaar.com/partner |
| MCA21 (company registration) | mca.gov.in |
| RBI Regulatory Sandbox | rbi.org.in/innovation |
| Indian Patent Office | ipindia.gov.in |
| Sarvam AI (FLM base model / partner) | sarvam.ai |
| Hugging Face (fine-tuning resources) | huggingface.co |

---

## 18. The number that matters

One metric decides Year 1:

Users who completed AA consent and came back at least 3 times.

Not downloads. Not registrations. Not first logins.

Someone who went through the consent flow, saw their full financial picture, got a specific AI recommendation, and came back the next week — that's who the product is for. That's also the user angels will ask about. 1,000 of them by Month 6. 5,000 by Month 12. Everything in this plan points at that number.

---

*Version 4.0 · July 2026 · Update after each major milestone*
