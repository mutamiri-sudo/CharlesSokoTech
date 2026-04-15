# Insurance City — PHA Email Campaign

**Client:** Insurance City (commercial property & casualty brokerage)
**Role:** Founder / AI Engineer / Delivery PM — scoped, designed, built, and deployed solo
**Status:** Live in production since April 15, 2026 — running unattended on a 30-day schedule
**Stack:** Anthropic Claude · Node.js · Nodemailer · Office 365 SMTP · Vercel · Calendly · Windows Task Scheduler

---

## The Business Problem

Insurance City is a two-person commercial insurance brokerage licensed in Texas, Oklahoma, and Louisiana. They identified Public Housing Authorities as an underserved niche where carriers often misprice property coverage — creating a real opportunity to win renewals at the Q2 renewal window.

But reaching all **649 PHAs** across three states with personalized outreach in the 30-day window before renewals was impossible manually. They needed:
- Personalized outreach at scale without looking like spam
- A way to surface replies and bookings without the founder checking inbox hourly
- Safe sending from a cold Office 365 tenant (no domain reputation to burn)
- Full audit trail for compliance
- Zero monthly SaaS cost — the client couldn't justify $30–$200/mo for Instantly.ai / Apollo / Outreach

---

## The System I Built

A two-layer architecture that separates LLM judgment from deterministic execution:

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
         → Client's Outlook            (sent / replied / bounced / booked)
```

### Key components

| Component | What it does |
|---|---|
| **Contact store** | 649 PHAs segmented Tier B (163, 5-email sequence) / Tier C (486, 3-email sequence) |
| **Ramp-up scheduler** | 25 sends/day (Days 1–3) → 35/day (Days 4–6) → 50/day (Day 7+) to protect domain reputation |
| **SMTP sender** | Nodemailer + Office 365 STARTTLS; per-send deduplication; PID-based process lock to prevent concurrent runs |
| **State tracker** | JSON-backed record of every send, reply, bounce, opt-out with timestamps |
| **Live dashboard** | Vercel-hosted, no-login, auto-refreshing — client sees campaign health in real time |
| **Booking flow** | Calendly CTAs in every email → land on Daniel's Outlook calendar automatically |
| **Automation** | Windows Task Scheduler fires the daily batch at 10:03 AM CST, Apr 15 – May 15 |

---

## Architecture Decision Worth Calling Out

**I kept the LLM out of the send loop.**

The LLM does what LLMs are good at — judgment, language, review. The deterministic scheduler does what deterministic code is good at — counting, timing, retrying, locking, enforcing rate limits.

That separation is what makes the system safe to run unattended on a 30-day schedule for a client who isn't a technical user. An LLM that decides when to send would be an LLM I'd have to babysit. A deterministic scheduler that sends LLM-drafted content is a system I can walk away from.

---

## Incident + Response (Day 1)

Day 1 had a scheduling overlap: the Windows task fired at 10:03 AM CST at the same moment I kicked off a manual verification run, and both processes loaded the tracker independently and started sending the same contacts. Eighteen PHAs received two copies of Email #1 about thirty seconds apart.

**What I did:**
1. Diagnosed from the tracker JSON timestamps within minutes
2. Patched two layers of defense:
   - **Process lock:** PID-based lock file; second concurrent run aborts cleanly
   - **Per-send dedup:** tracker re-read before every send; skips if `(step, today)` already logged for that contact
3. Reduced tomorrow's send cap from 25 to 15 to keep the warm-up curve on target
4. Sent the client a transparent incident note the same day with the root cause, the fix, and the volume adjustment

Including this incident in a portfolio piece is intentional. Consulting clients don't buy "it'll never fail" — they buy "when something goes sideways, this person will see it, fix it, and tell me honestly."

---

## Outcomes

- ✅ Live since **April 15, 2026**
- ✅ Day 1: **25 PHAs reached, 0 bounces**
- ✅ Replaced an estimated **3 weeks** of manual outreach work with an unattended 30-day automation
- ✅ **$0/mo** SaaS cost (custom Node.js vs. Instantly.ai at $30/mo)
- ✅ Full audit trail — every send timestamped and recoverable
- ✅ Client has a live dashboard they can show their carrier partners

---

## Live Links

- **Campaign Dashboard:** https://campaign-dashboard-mu-two.vercel.app
- **Landing Page:** https://insurance-city-nextjs.vercel.app
- **PHA Contact List (internal):** https://pha-list.vercel.app
