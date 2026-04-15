# Insurance City — AI-Powered Marketing Consultation

**Engagement type:** Marketing consultation for an independent insurance agency in Dallas
**Role:** Solo consultant — strategy, build, deployment, ongoing delivery
**Status:** Live in production since April 2026
**Stack:** Anthropic Claude · Node.js · Nodemailer · Office 365 · HawkSoft API · Vercel · Calendly

---

## The Story

An independent insurance agency in Dallas came to me with a familiar mid-market problem: they had a strong book of business, a licensed territory that stretched across Texas, Oklahoma, and Louisiana, and two people to run it. They were doing good work for the clients they had — but every hour spent on manual reporting and outreach was an hour not spent closing new business.

They didn't need a consultant to tell them *what* their problem was. They knew. They needed someone who could actually build the fix.

We scoped the engagement in two phases:

**Phase 1 — See the business clearly.** Replace manual spreadsheet tracking with a real-time operations dashboard so the founder could see pipeline health, renewals, and cancellations without asking anyone.

**Phase 2 — Fill the pipeline.** Launch an AI-powered outbound marketing campaign targeting a specific underserved niche — Public Housing Authorities in their licensed territory — at a volume the two-person shop could never have reached manually.

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

With reporting handled, we turned to pipeline. The agency had identified Public Housing Authorities as an underserved niche — carriers often mispriced PHA property coverage, which meant real opportunity to win renewals. But there are **649 PHAs across Texas, Oklahoma, and Louisiana**, and reaching them all with personalized outreach in the 30-day window before Q2 renewals was impossible manually.

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

**Combined business outcome:** A two-person independent agency now runs its reporting on autopilot and executes enterprise-grade outbound marketing at a volume that would have required a dedicated BDR team.

---

## Why This Matters

This engagement is a microcosm of what good AI consulting looks like in the mid-market: the problem isn't "deploy an LLM," it's "understand the business, separate the parts AI does well from the parts that need deterministic code, ship a system that actually runs in production, and be transparent when it breaks."

One consultant. One agency. Two phases. Real metrics. Live dashboard. Running unattended.
