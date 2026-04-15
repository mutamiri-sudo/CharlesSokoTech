# BRD Agent — AI-Automated Requirements-to-Backlog Pipeline

**Type:** Personal project (not a client engagement)
**Role:** Sole designer + builder

## Overview
A Claude Code–powered agent that automates the entire manual path from a Business Requirements Document (BRD) to a fully-structured Jira backlog. The agent reads the BRD, creates features in Jira, and breaks each feature down into epics, user stories, acceptance criteria, and Gherkin test scenarios — end-to-end, with zero manual data entry.

Fully customizable: plug in your own BRD templates, your team's story-writing conventions, your Jira project schema, and your compliance rules.

## The Manual Process This Replaces

Before this agent, the workflow looked like this:

1. Read the BRD (2–4 hours for a real one)
2. Identify features
3. Manually create each feature in Jira — title, description, priority, labels
4. For every feature, draft user stories
5. Manually create each story — paste the "As a / I want / So that," add acceptance criteria
6. Write Gherkin scenarios for QA handoff
7. Link stories back to the right feature, epic, and BRD section for traceability
8. Tag compliance-relevant stories for regulatory review

For a typical BRD that's **1–2 weeks of PO/BA time** — and it's error-prone (dropped AC, missing compliance tags, broken traceability).

## What the Agent Does Instead

Feed it the BRD. Claude Code automates the rest:

| Stage | What's Automated |
|-------|------------------|
| BRD Parsing | Parses the BRD into structured sections (scope, functional requirements, NFRs, compliance) |
| Feature Creation | Creates the feature records directly in Jira via API |
| Story Decomposition | Breaks each feature into user stories with "As a / I want / So that" structure |
| Acceptance Criteria | Generates testable AC for every story |
| Gherkin Scenarios | Writes Given/When/Then test cases for QA handoff |
| Compliance Flags | Tags stories touching regulated areas (fintech, insurance, mortgage) |
| Traceability | Every story linked back to the BRD section it came from — audit-ready by default |
| Story Creation | Writes stories into Jira with proper epic/feature parent links |

## Customizable

The agent is built as a configurable pipeline, not a one-off script:

- **Story-writing conventions:** plug in your team's definition of ready, INVEST standards, preferred voice
- **Jira schema:** configure project key, issue types, custom fields, workflows
- **BRD templates:** tune the parser for your org's BRD format (or bring your own sections)
- **Compliance rules:** add your own regulatory tags (SOX, HIPAA, NAIC, CFPB, etc.)
- **QA handoff format:** Gherkin, plain AC, test-case format — pick what your team uses

Same architectural principle I use everywhere: **LLM for judgment, deterministic code for execution.** Claude handles the decomposition and language. A deterministic Jira integration layer handles the API calls, field mapping, and linking.

## Technical Approach
- **Multi-stage prompt chain:** parse BRD → identify features → decompose into stories → validate against quality standards
- **Context injection:** full BRD loaded so every generated story is grounded in source language — no hallucinated requirements
- **Jira REST API integration:** direct writes for features, stories, AC, Gherkin, labels, parent links
- **AI Evals:** automated validation checks every story against INVEST / testability / clarity standards before it's written to Jira
- **Human-in-the-Loop:** review checkpoint before anything hits the Jira project — nothing writes without PO approval
- **Traceability engine:** every story carries a reference back to the BRD line or section it was derived from

## Why I Built It

In my day job as a PO / BA, translating a BRD into a fully-populated Jira backlog is one of the most time-consuming ceremonies in the delivery lifecycle. I wanted to test whether Claude Code could meaningfully automate it end-to-end — not just suggest stories, but actually write them into Jira with proper linking and compliance tagging — without sacrificing quality or traceability.

This agent is the proof of concept. It's a blueprint I'd extend for a client engagement where a PO/BA team is spending >20% of their time on BRD-to-backlog decomposition.

## Results
- **Replaces 1–2 weeks of manual PO/BA work per BRD** with an automated pipeline
- Consistent output quality across different product domains
- Compliance-aware outputs for regulated environments
- Full BRD → feature → story → AC → Gherkin traceability, no manual mapping
- Customizable to any team's conventions, tools, and regulatory context

## Stack
Claude Code · Claude API · Node.js · Jira REST API · Prompt Engineering · AI Evals · Context Engineering
