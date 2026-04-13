# Insurance City — Agentic Operations Dashboard

## Overview
A real-time operations dashboard built for an independent insurance agency. Replaced manual spreadsheet-based reporting with automated, live data pipelines that surface critical business metrics every morning.

## Problem
The agency spent 2+ hours daily manually pulling data from their management system (HawkSoft), copying it into spreadsheets, and formatting reports for the team. Data was always stale by the time it reached decision-makers.

## Solution
An automated dashboard that pulls live data from HawkSoft API and presents it in a clean React frontend — zero manual effort required.

### Data Pipelines
1. **New Business** — Tracks new policies written, premium volume, and agent performance
2. **Cancellations** — Monitors policy cancellations with reason codes and retention opportunities
3. **Pending Renewals** — Surfaces upcoming renewals requiring agent attention
4. **Pipeline** — Tracks quotes and applications in progress
5. **Agency Performance** — Aggregated KPIs across all business lines

## Architecture
```
┌─────────────────┐     ┌──────────────────────┐     ┌─────────────────┐
│  HawkSoft API   │────▶│  Node.js/Express API  │────▶│  React Frontend │
│  (Data Source)   │     │  (Backend + Cron)     │     │  (Dashboard)    │
└─────────────────┘     └──────────────────────┘     └─────────────────┘
                              │
                              ▼
                        Scheduled Jobs
                        (Morning auto-refresh)
```

## Results
- Eliminated 10 hours/week of manual reporting
- Replaced a daily 2-hour manual task with zero-effort automation
- Agency staff now start each day with live, accurate data

## Live Site
🔗 [insurance-city-nextjs.vercel.app](https://insurance-city-nextjs.vercel.app)

## Stack
Node.js · Express · React · HawkSoft API · REST APIs · GitHub · Railway/Vercel
