# Charles Mutamiri — AI Product Portfolio

**Product Manager | Generative AI Consultant | LLM & Agentic AI**

I build and ship production AI-powered products — from concept through deployment. This portfolio showcases real-world projects I've designed, built, and deployed using modern AI tools and frameworks.

---

## Featured Projects

### 1. Insurance City — PHA Email Campaign (LLM + Agentic Orchestration) ⭐
**Stack:** Anthropic Claude · Node.js · Nodemailer · Office 365 SMTP · Vercel · Calendly API

An LLM-orchestrated outbound campaign platform built for a commercial insurance brokerage to reach **649 Public Housing Authorities across Texas, Oklahoma, and Louisiana** with personalized property-insurance renewal outreach.

**What the system does:**
- LLM layer (Claude) handles judgment work: contact segmentation (Tier B mid-size vs. Tier C small), sequence copy generation in the client's voice, brand-voice review before send
- Deterministic execution engine handles the rest: JSON-backed state tracker, ramp-up scheduler (25 → 35 → 50 sends/day to protect domain reputation), SMTP sender with per-send dedup and PID-based process lock, Vercel-hosted live dashboard
- Bookings flow to Calendly → client's Outlook calendar automatically
- Replies monitored through shared Sales inbox

**Architecture decision worth calling out:** I kept the LLM out of the send loop. It drafts, reviews, and segments — but a deterministic scheduler decides *when* anything goes out. That separation is what makes the system safe to run unattended on a 30-day schedule for a non-technical client.

**Outcomes:**
- Live since April 15, 2026 — running unattended on a 30-day schedule
- Day 1: 25 PHAs reached, 0 bounces
- Replaced ~3 weeks of manual outreach work
- $0/mo SaaS cost (chose custom Node.js sender over Instantly.ai for audit-trail control)

🔗 **Live Dashboard:** [campaign-dashboard-mu-two.vercel.app](https://campaign-dashboard-mu-two.vercel.app)
🔗 **Landing Page:** [insurance-city-nextjs.vercel.app](https://insurance-city-nextjs.vercel.app)

📂 [View project details →](projects/insurance-city-pha-campaign.md)

---

### 2. PRD Agent — AI-Powered Product Requirements Generator
**Stack:** Claude API · Node.js · Prompt Engineering · AI Evals

An LLM-powered agent that automates the product requirements process. Give it a business problem, and it generates epic definitions, user stories with acceptance criteria, Gherkin test scenarios, story points, priority, success metrics, and compliance/regulatory flags (built for fintech/regulated environments).

**How it works:**
- Custom prompt architecture with context injection from requirement documents
- Automated AI eval pipeline that validates outputs against acceptance criteria
- Reduced user story writing time by 60% in production use

📂 [View project details →](projects/prd-agent.md)

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

### 4. Insurance City — Agentic Operations Dashboard
**Stack:** Node.js · Express · React · HawkSoft API · REST APIs

A real-time operations dashboard built for the same client as Project 1. Replaced manual spreadsheet tracking with automated, live data pipelines.

**What it does:**
- Automates 5 data pipelines: New Business, Cancellations, Pending Renewals, Pipeline, and Agency Performance
- Pulls live data from HawkSoft API every morning — zero manual effort
- Eliminated 10 hours/week of manual reporting

**Architecture:**
```
HawkSoft API → Node.js/Express Backend → REST API → React Frontend
     ↓                                                    ↓
  Scheduled Jobs                                    Live Dashboard
  (Auto-refresh)                                   (Agency Staff)
```

🔗 **Live:** [hawksoft-dashboard.vercel.app](https://hawksoft-dashboard.vercel.app)

📂 [View project details →](projects/insurance-city-dashboard.md)

---

### 5. SAFe Cert RAG — Retrieval-Augmented Study Assistant
**Stack:** Node.js · React · RAG Architecture · Vector Embeddings · Claude API

A RAG-powered Q&A tool I built while studying for SAFe Practitioner 6.0 certification. Ingests the SAFe reference library, embeds it, and answers exam-style questions with citations back to source material.

🔗 **Repo:** [github.com/mutamiri-sudo/safe-cert-rag](https://github.com/mutamiri-sudo/safe-cert-rag)

---

### 6. VOLT Supply — E-Commerce Backend & Product Sync Engine
**Stack:** JavaScript · Shopify API · DigiKey API · Railway · Node.js

Backend system for an electronics supply e-commerce store. Automates product catalog management, pricing, and inventory sync between DigiKey (distributor) and Shopify (storefront).

**Key features:**
- Automated product sync between DigiKey distributor catalog and Shopify storefront
- Dynamic pricing engine with markup rules and margin management
- SEO-optimized product feed generation for Google Shopping
- Deployed on Railway with automated scheduling

📂 [View project details →](projects/volt-supply.md)

---

### 7. NeuroTracker Africa — Affiliate Landing Page & Funnel
**Stack:** Next.js · Vercel · Conversion-optimized copy · AI-assisted content

A conversion-optimized affiliate landing page for a cognitive-training platform launching into the African market. Built end-to-end — copy, design, deploy, analytics.

🔗 **Live:** [neurotrackerx-landing.vercel.app](https://neurotrackerx-landing.vercel.app)

📂 [View project details →](projects/neurotracker-landing.md)

---

### 8. DLA GovCon Course — Productized Consulting Offering
**Stack:** Course production · Sales funnel · Marketing automation

A 7-module course teaching small businesses how to win Defense Logistics Agency contracts. Three tiers ($297 / $997 / $2,497) with an upsell pipeline from the companion published book.

📂 [View project details →](projects/dla-govcon-course.md)

---

### 9. HVAC Website — Client Service Platform
**Stack:** AI-Native Development · Lovable · Vercel

A client-facing website for an HVAC services business, built using AI-native development tools. Translated business requirements directly into deployed software using Lovable. Demonstrates rapid prototyping and AI-assisted product delivery.

📂 [View project details →](projects/hvac-website.md)

---

### 10. "$38 Billion Opportunity" — Published Book
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
