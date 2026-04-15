# Gherkin Scenario Generator — Jira / Jira Align Integration

**Type:** Personal project (not a client engagement)
**Role:** Sole designer + builder
**Stack:** Claude API · Node.js · Jira REST API · Jira Align API · Prompt Engineering

---

## The Problem I Was Trying to Solve

In my day job as a Product Owner, writing Gherkin (Given / When / Then) test scenarios for a full backlog was one of the most time-consuming parts of sprint prep. The scenarios matter — QA depends on them, developers reference them, acceptance testing hangs on them — but the work itself is formulaic enough that I suspected an LLM could meaningfully reduce the overhead without sacrificing quality.

I built this tool to test that hypothesis on my own backlogs before recommending anything similar to a client.

---

## How It Works

1. **Pull** — Authenticates to Jira / Jira Align via REST API, pulls a target story's title, description, and acceptance criteria
2. **Prompt** — Feeds the story into a Claude prompt tuned for BDD scenario generation (positive path, negative path, edge cases, data variations)
3. **Validate** — Runs a lightweight structural check — does every scenario have Given/When/Then? Are the steps concrete enough to execute?
4. **Write back** — Posts the scenarios to a designated field on the story (configurable — custom field, description append, or a linked comment)

---

## What I Learned

- **The prompt matters more than the model.** A generic "write Gherkin for this story" prompt produced mushy scenarios. A prompt that explicitly asked for one positive path, one negative path, and at least two edge-case scenarios per story produced usable output consistently.
- **Validation is where the reliability lives.** Even with a good prompt, ~10% of outputs had a malformed step or missing Then clause. The post-generation validator catches those and re-prompts with the specific flaw called out.
- **Enterprise tool integration is the gating factor, not the LLM.** Getting Jira Align auth working cleanly took longer than tuning the prompt. The pattern (pull → LLM → validate → write back) applies directly to Confluence, Azure DevOps, Linear, ServiceNow — the LLM piece is the easy part.

---

## Outcome

- Measurable reduction in documentation time per story on my personal backlog
- Scenarios preserve Given/When/Then rigor for QA handoff
- Proved the pattern — this is a blueprint I'd extend for a client engagement where a team is spending >20% of sprint prep on scenario writing

---

## Why This Matters for My Consulting Work

Teams that are stuck on legacy tools like Jira Align (common in enterprise PE portfolio companies post-merger) often assume AI automation isn't feasible because their tools aren't "modern." This project is a proof point that the integration is the small hard part, not the LLM, and that real PO / QA time savings are available today.
