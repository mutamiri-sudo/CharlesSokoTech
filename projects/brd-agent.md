# BRD Agent — AI-Powered Business Requirements Breakdown

## Overview
A production LLM-powered agent that takes a Business Requirements Document (BRD) and breaks it down into the sprint-ready artifacts a delivery team actually works from — epics, user stories, acceptance criteria, Gherkin test scenarios, and compliance flags. Built on the Claude API with custom prompt architecture designed for regulated financial services environments.

## Problem
BRDs are dense. They capture *what the business needs* but not *what the team builds next sprint*. Translating a BRD into a structured backlog — epics, stories, acceptance criteria, test scenarios — is one of the most time-consuming parts of product management and business analysis. In regulated industries (fintech, insurance, mortgage), each story also needs compliance flags and audit-ready traceability back to the BRD it came from.

## Solution
Feed the agent a BRD. It returns a complete, sprint-ready breakdown:

| Output | Description |
|--------|-------------|
| Strategic Theme | Business context pulled from the BRD, aligned to stakeholder objectives |
| Epics | High-level feature groupings derived from BRD sections |
| User Stories | Structured "As a / I want / So that" with clear ownership |
| Acceptance Criteria | Testable conditions for each story |
| Gherkin Scenarios | Given/When/Then test cases for QA handoff |
| Compliance Flags | Regulatory considerations surfaced from BRD language |
| Traceability | Each story linked back to the BRD section it originated from |
| Success Metrics | KPIs and measurement criteria tied to business outcomes |

## Technical Approach
- **Prompt Architecture:** Multi-stage prompt chain that first parses the BRD into structured sections, then decomposes each section into backlog artifacts
- **Context Injection:** Full BRD loaded into context so every generated story is grounded in source language — reduces hallucinated requirements
- **AI Evals:** Automated validation pipeline checks every story against quality standards (testability, clarity, INVEST criteria)
- **Traceability:** Every output artifact carries a reference back to the BRD line or section it was derived from — audit-ready by default
- **Human-in-the-Loop:** Review checkpoints before any output reaches the team's tracker (Jira, Azure DevOps, Linear)

## Results
- 60% reduction in BRD-to-backlog translation time
- Consistent output quality across different product domains
- Compliance-aware outputs for regulated environments
- Full BRD → story traceability with no manual mapping

## Stack
Claude API · Node.js · Prompt Engineering · AI Evals · Context Engineering
