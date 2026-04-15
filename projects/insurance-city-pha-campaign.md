# Insurance City — AI-Powered Marketing Consultation

**Client:** [Insurance City](https://theinsurancecity.com/) — theinsurancecity.com
**Engagement type:** Marketing consultation for a multi-million dollar insurance brokerage in Dallas
**Role:** Solo consultant — strategy, build, deployment, ongoing delivery
**Status:** Live in production since April 2026
**Stack:** Anthropic Claude · Node.js · Nodemailer · Office 365 · HawkSoft API · Vercel · Calendly

---

## The Story

A multi-million dollar independent insurance brokerage in Dallas came to me with a familiar mid-market problem: they had a strong book of business, a licensed territory across Texas, Oklahoma, and Louisiana, and a lean team running it. They were doing good work for the clients they had — but every hour spent on manual reporting and outreach was an hour not spent closing new business.

They didn't need a consultant to tell them *what* their problem was. They knew. They needed someone who could actually build the fix.

We scoped the engagement in two phases:

**Phase 1 — See the business clearly.** Replace manual spreadsheet tracking with a real-time operations dashboard so the founder could see pipeline health, renewals, and cancellations without asking anyone.

**Phase 2 — Fill the pipeline.** Launch an AI-powered outbound marketing campaign targeting a specific underserved niche — **Public Housing Authorities (PHAs)** in their licensed territory — at a volume that would have required a dedicated business development team to execute manually.

I delivered both.

---

## Phase 1 — Real-Time Operations Dashboard

The agency ran their day-to-day on HawkSoft (the industry-standard AMS for independent agencies). Every Monday, the founder was rebuilding the same five reports by hand from exported CSVs. That's ten hours a week of founder time spent on data entry instead of selling.

**What I built:**
- Node.js backend pulling live data from the HawkSoft API every morning
- Express REST layer serving five pipelines: New Business, Cancellations, Pending Renewals, Pipeline, and Agency Performance
- React frontend with the metrics the founder actually looked at — not a kitchen-sink dashboard, just the five views he was rebuilding manually
- Scheduled jobs so the dashboard is fresh when he opens his laptop Monday morning

**Architecture:**
```
HawkSoft API  →  Node.js / Express  →  REST API  →  React Frontend
     ↓                                                   ↓
Scheduled Jobs                                    Live Dashboard
(auto-refresh)                                    (agency staff)
```

**Outcome:** Eliminated ten hours/week of manual reporting. The founder now starts Monday with the agency's pulse on screen, not in a spreadsheet.

🔗 **Live:** https://hawksoft-dashboard.vercel.app

---

## Phase 2 — AI-Powered Outbound Campaign

With reporting handled, we turned to pipeline. The brokerage had identified **Public Housing Authorities (PHAs)** as an underserved niche — carriers often mispriced PHA property coverage, which meant real opportunity to win renewals. But there are **649 PHAs across Texas, Oklahoma, and Louisiana**, and reaching them all with personalized outreach in the 30-day window before Q2 renewals was impossible manually.

This is where the AI consulting work came in.

### The system I designed

A two-layer architecture that separates **LLM judgment** from **deterministic execution**:

```
                     ┌───────────────────────────────────────┐
                     │         LLM LAYER (Claude)            │
                     │  · Contact segmentation (Tier B / C)  │
                     │  · Sequence copy generation           │
                     │  · Brand-voice review pre-send        │
                     └──────────────────┬────────────────────┘
                                        │ approved drafts
                                        ▼
┌────────────────────────────────────────────────────────────────────┐
│              DETERMINISTIC EXECUTION ENGINE (Node.js)              │
│                                                                    │
│   Contact store  →  Daily scheduler  →  SMTP sender  →  Tracker    │
│   (649 PHAs)        (ramp-up curve)     (dedup guard)   (state)    │
│                                                                    │
└─────────────────┬──────────────────────────────┬──────────────────┘
                  │                              │
                  ▼                              ▼
         Calendly bookings              Vercel live dashboard
         → Founder's Outlook           (real-time campaign metrics)
```

### Key components

| Component | What it does |
|---|---|
| **Contact store** | 649 PHAs segmented Tier B (mid-size, 5-email sequence) / Tier C (small, 3-email sequence) |
| **Ramp-up scheduler** | 25 sends/day (Days 1–3) → 35/day (Days 4–6) → 50/day (Day 7+) to protect domain reputation |
| **SMTP sender** | Nodemailer + Office 365 STARTTLS; per-send deduplication; PID-based process lock |
| **State tracker** | JSON-backed record of every send, reply, bounce, opt-out with timestamps |
| **Real-time campaign dashboard** | Vercel-hosted, auto-refreshing — founder sees campaign health the moment it changes |
| **Booking flow** | Calendly CTAs in every email → land on the founder's Outlook calendar automatically |
| **Automation** | Windows Task Scheduler fires the daily batch at 10:03 AM CST, 30-day run |

### Architecture decision worth calling out

**I kept the LLM out of the send loop.**

Claude does what LLMs are good at — judgment, language, review. The deterministic scheduler does what deterministic code is good at — counting, timing, retrying, locking, enforcing rate limits.

That separation is what makes the system safe to run unattended for 30 days for a client who isn't a technical user. An LLM that decides when to send would be an LLM I'd have to babysit. A deterministic scheduler that sends LLM-drafted content is a system I can walk away from.

### Real-time metrics the client sees

The campaign dashboard shows, live, without any login:

- **Emails sent today / this campaign / by tier**
- **Unique contacts reached** vs. 649 target
- **Replies, bookings, bounces, opt-outs** — each click-through to detail
- **Daily send history** — a visual bar chart of every day's send volume
- **By-step breakdown** — who's received Email 1, 2, 3, 4, 5
- **Campaign health signals** — bounce rate, reply rate, opt-out rate

The founder can open it on his phone between meetings and know exactly where the campaign stands.

🔗 **Live campaign dashboard:** https://campaign-dashboard-mu-two.vercel.app
🔗 **Agency landing page:** https://insurance-city-nextjs.vercel.app

---

## Incident + Response (Day 1)

Day 1 had a scheduling overlap: the Windows task fired at 10:03 AM CST at the same moment I kicked off a manual verification run, and both processes sent to the same contacts in parallel. Eighteen PHAs received two copies of Email #1 about thirty seconds apart.

**What I did:**
1. Diagnosed from the tracker JSON timestamps within minutes
2. Patched two layers of defense:
   - **Process lock:** PID-based lock file; second concurrent run aborts cleanly
   - **Per-send dedup:** tracker re-read before every send; skips if `(step, today)` already logged
3. Reduced tomorrow's send cap from 25 to 15 to keep the warm-up curve on target
4. Sent the founder a transparent incident note the same day with the root cause, the fix, and the volume adjustment

Including this in the case study is intentional. Consulting clients don't buy "it'll never fail" — they buy "when something goes sideways, this person will see it, fix it, and tell me honestly."

---

## Outcomes

**Phase 1 — Dashboard**
- ✅ Eliminated ~10 hours/week of manual reporting
- ✅ Five live data pipelines replacing five manual spreadsheets
- ✅ Zero-touch weekly refresh

**Phase 2 — Campaign**
- ✅ Live since April 15, 2026 — unattended 30-day run
- ✅ Day 1: 25 PHAs reached, 0 bounces
- ✅ Replaced an estimated 3 weeks of manual outreach work
- ✅ $0/mo SaaS cost (custom Node.js vs. Instantly.ai at $30/mo)
- ✅ Full audit trail — every send timestamped and recoverable

**Combined business outcome:** A multi-million dollar brokerage now runs its reporting on autopilot and executes enterprise-grade niche outbound marketing at a volume and precision that would have required a dedicated business development team.

---

## Next Steps — Where This Engagement Is Heading

The PHA campaign is **Phase 2 of a larger build-out**. Once the 30-day run completes and we have reply / booking / conversion data, the roadmap is:

### Phase 3 — Expand to other commercial lines
The PHA playbook (niche segmentation → LLM-drafted sequences → deterministic send engine → live dashboard) is tier-agnostic. The same framework plugs into the brokerage's other commercial lines:
- Habitational / multi-family property
- Non-profit and social services
- Municipal and public-sector accounts
- Artisan contractors and trades
- Commercial auto and fleet

Each new line is a rebuild of the contact list and copy layer — the execution engine, dashboard, and deliverability infrastructure carry over.

### Phase 4 — AI-enabled outbound voice calls
Email opens the door. The biggest gap in a cold outbound funnel is the distance between "interested reply" and "actual conversation booked." I'm scoping an AI voice layer that:
- Calls prospects who opened or replied to the email campaign
- Qualifies them against the brokerage's ideal-customer profile in natural conversation
- Answers baseline questions (coverage types, licensure, carrier relationships)
- Books warm calls directly onto the producer's calendar — no human BDR needed

The architectural principle stays the same: **LLM for judgment, deterministic code for execution.** The AI agent handles the conversation. A deterministic calendar-integration layer handles the booking. A compliance layer handles the "this call is being recorded" disclosure and opt-out flow.

### Phase 5 — Productize the playbook
The end-state I'm aiming for with this client is a **repeatable niche-marketing product** they can run for every vertical in their pipeline — one consultant setup cost per vertical, then the system runs itself. That's the shape of AI consulting work I find most durable: not a one-off build, but an engine the client keeps turning.

---

## Why This Matters

This engagement is a microcosm of what good AI consulting looks like in the mid-market: the problem isn't "deploy an LLM," it's "understand the business, separate the parts AI does well from the parts that need deterministic code, ship a system that actually runs in production, and be transparent when it breaks."

One consultant. One agency. Two phases. Real metrics. Live dashboard. Running unattended.
