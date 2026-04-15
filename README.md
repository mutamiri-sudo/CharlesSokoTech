# Charles Mutamiri — AI Product Portfolio

**Product Manager | Generative AI Consultant | LLM & Agentic AI**

I build and ship production AI-powered products — from concept through deployment. This portfolio showcases real-world projects I've designed, built, and deployed using modern AI tools and frameworks.

---

## Featured Projects

### 1. [Insurance City](https://theinsurancecity.com/) — AI-Powered Marketing Consultation ⭐
**Engagement:** Marketing consultation for a multi-million dollar insurance brokerage in Dallas — [theinsurancecity.com](https://theinsurancecity.com/)
**Stack:** Anthropic Claude · Node.js · HawkSoft API · Nodemailer · Office 365 SMTP · Vercel · Calendly

A two-phase consulting engagement for a Dallas-based multi-million dollar independent insurance brokerage with a licensed territory across Texas, Oklahoma, and Louisiana. Scoped, built, and delivered solo.

**Phase 1 — Real-time operations dashboard.** Replaced ten hours/week of manual spreadsheet reporting with a live dashboard pulling directly from their HawkSoft agency management system. Five pipelines (New Business, Cancellations, Pending Renewals, Pipeline, Agency Performance) auto-refreshed every morning.

**Phase 2 — AI-powered outbound campaign.** Designed and built an LLM-orchestrated email system to reach **649 Public Housing Authorities (PHAs)** across their territory with personalized property-insurance renewal outreach — a volume that would have required a dedicated business development team to execute manually.

**The AI architecture worth calling out:** I kept the LLM out of the send loop. Claude handles judgment — contact segmentation, sequence copy, brand-voice review. A deterministic Node.js engine handles execution — daily ramp-up (25 → 35 → 50/day), state tracking, deliverability safeguards, per-send dedup, process locking. The founder monitors both phases through **live real-time dashboards** — no logins, always fresh.

**Next steps (Phase 3+):**
- Extend the campaign framework to the brokerage's other commercial lines (habitational, non-profit, municipal, artisan contractors)
- Layer in **AI-enabled outbound voice calls** — an AI agent that qualifies prospects, answers baseline questions, and books warm calls directly onto the producer's calendar. Email opens the door; AI voice closes the gap between interest and conversation.
- Graduate the PHA playbook into a repeatable niche-marketing product the brokerage can run for every vertical in their pipeline

**Outcomes:**
- Dashboard: eliminated ~10 hrs/week of manual reporting
- Campaign: live since Apr 15, 2026 — running unattended on a 30-day schedule
- Day 1: 25 PHAs reached, 0 bounces, $0/mo SaaS cost
- Replaced an estimated 3 weeks of manual outreach work
- Full audit trail — every send timestamped and recoverable

🔗 **Campaign Dashboard (live metrics):** [campaign-dashboard-mu-two.vercel.app](https://campaign-dashboard-mu-two.vercel.app)
🔗 **Ops Dashboard:** [hawksoft-dashboard.vercel.app](https://hawksoft-dashboard.vercel.app)
🔗 **Agency Landing Page:** [insurance-city-nextjs.vercel.app](https://insurance-city-nextjs.vercel.app)

📂 [View full case study →](projects/insurance-city-pha-campaign.md)

---

### 2. BRD Agent — AI-Automated Requirements-to-Backlog Pipeline
**Stack:** Claude Code · Claude API · Node.js · Jira REST API · Prompt Engineering · AI Evals

A Claude Code–powered agent that automates the entire manual workflow of turning a Business Requirements Document into a fully-structured Jira backlog. Instead of a PO / BA spending 1–2 weeks manually adding requirements to Jira as features and then breaking them down into user stories, the agent does it end-to-end:

- Parses the BRD into structured sections
- Creates features in Jira directly via API
- Breaks each feature down into user stories with acceptance criteria
- Generates Gherkin test scenarios for QA handoff
- Tags compliance-relevant stories for regulatory review
- Links everything back to the BRD section it came from (audit-ready traceability)

**Customizable:** plug in your own BRD templates, Jira schema, story-writing conventions, and compliance rules (SOX, HIPAA, NAIC, CFPB, etc.).

**Architectural principle:** LLM for judgment, deterministic code for execution. Claude handles decomposition and language. A deterministic Jira integration layer handles the API calls and linking. Human-in-the-loop checkpoint before anything writes to Jira.

📂 [View project details →](projects/brd-agent.md)

---

### 3. Gherkin Scenario Generator — Jira / Jira Align Integration
**Stack:** Claude API · Node.js · Jira REST API · Jira Align API

A personal project exploring how LLMs can cut the time Product Owners spend on test documentation. Pulls user stories and acceptance criteria from Jira / Jira Align, generates BDD-style Gherkin scenarios, and writes them back to the story.

**Why I built it:**
In my day job as a PO, writing Gherkin scenarios for a full backlog was one of the most time-consuming parts of sprint prep. I wanted to test whether an LLM could meaningfully reduce that overhead without sacrificing scenario quality.

**Outcomes:**
- Measurable reduction in documentation time per story
- Scenarios preserve Given/When/Then rigor for QA handoff
- Proved the pattern for LLM + enterprise tool integration (applies to Confluence, Azure DevOps, etc.)

📂 [View project details →](projects/gherkin-generator.md)

---

### 4. SAFe Cert RAG — Retrieval-Augmented Study Assistant
**Stack:** Node.js · React · RAG Architecture · Vector Embeddings · Claude API

A RAG-powered Q&A tool I built while studying for SAFe Practitioner 6.0 certification. Ingests the SAFe reference library, embeds it, and answers exam-style questions with citations back to source material.

🔗 **Repo:** [github.com/mutamiri-sudo/safe-cert-rag](https://github.com/mutamiri-sudo/safe-cert-rag)

---

### 5. VOLT Supply — E-Commerce Backend & Product Sync Engine
**Stack:** JavaScript · Shopify API · DigiKey API · Railway · Node.js

Backend system for an electronics supply e-commerce store. Automates product catalog management, pricing, and inventory sync between DigiKey (distributor) and Shopify (storefront).

**Key features:**
- Automated product sync between DigiKey distributor catalog and Shopify storefront
- Dynamic pricing engine with markup rules and margin management
- SEO-optimized product feed generation for Google Shopping
- Deployed on Railway with automated scheduling

📂 [View project details →](projects/volt-supply.md)

---

### 6. NeuroTracker — Affiliate Landing Page & Funnel
**Stack:** Next.js · Vercel · Conversion-optimized copy · AI-assisted content

A conversion-optimized affiliate landing page for a cognitive-training platform targeting high-performance sports audiences. Built end-to-end — copy, design, deploy, analytics.

🔗 **Live:** [neurotrackerx-landing.vercel.app](https://neurotrackerx-landing.vercel.app)

📂 [View project details →](projects/neurotracker-landing.md)

---

### 7. DLA GovCon Course — Productized Consulting Offering
**Stack:** Course production · Sales funnel · Marketing automation

A 7-module course teaching small businesses how to win Defense Logistics Agency contracts. Three tiers ($297 / $997 / $2,497) with an upsell pipeline from the companion published book.

📂 [View project details →](projects/dla-govcon-course.md)

---

### 8. HVAC Website — Client Service Platform
**Stack:** AI-Native Development · Lovable · Vercel

A client-facing website for an HVAC services business, built using AI-native development tools. Translated business requirements directly into deployed software using Lovable. Demonstrates rapid prototyping and AI-assisted product delivery.

📂 [View project details →](projects/hvac-website.md)

---

### 9. "$38 Billion Opportunity" — Published Book
**Format:** Published Book (Amazon)

*A Beginner's Guide to Winning DLA Contracts* — Translated complex government procurement processes into a clear, actionable framework. Demonstrates end-to-end product ownership from concept to market.

📂 [View project details →](projects/dla-book.md)

---

## About Me

Product Manager / Product Owner / BA with **8+ years** across **Synchrony Financial, LoanDepot, KPMG, General Motors, American Express, and Ping Golf (via Insight Global)**. Now consulting as a Generative AI Product Consultant, building production AI tools and agentic systems for mid-market clients.

**What I work with daily:** Claude API · Claude Code · Cursor · Lovable · Bolt.new · Prompt Engineering · Agentic Workflows · RAG Architecture · AI Evals · Node.js · React · Next.js

**Certifications:** CSM · PMI-ACP · SAFe 6 POPM

📧 mutamiri@gmail.com
🔗 [LinkedIn](https://www.linkedin.com/in/charlesnmutamiri/)
