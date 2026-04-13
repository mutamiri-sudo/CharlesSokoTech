# PRD Agent — AI-Powered Product Requirements Generator

## Overview
A production LLM-powered agent that automates the most time-consuming part of product management: writing structured product requirements. Built on the Claude API with custom prompt architecture designed for regulated financial services environments.

## Problem
Product managers spend hours writing user stories, acceptance criteria, and test scenarios — often repeating patterns across similar features. In regulated industries (fintech, insurance, mortgage), every story also needs compliance flags and audit-ready documentation.

## Solution
The PRD Agent takes a single business problem statement and generates a complete sprint-ready package:

| Output | Description |
|--------|-------------|
| Strategic Theme | Business context and objective alignment |
| Epics | High-level feature groupings |
| User Stories | Structured with "As a / I want / So that" format |
| Acceptance Criteria | Testable conditions for each story |
| Gherkin Scenarios | Given/When/Then test cases |
| Compliance Flags | Regulatory considerations for fintech/insurance |
| Success Metrics | KPIs and measurement criteria |

## Technical Approach
- **Prompt Architecture:** Multi-stage prompt chain with context injection from uploaded requirement documents
- **AI Evals:** Automated output validation pipeline that checks generated stories against acceptance criteria quality standards
- **Context Management:** RAG-adjacent patterns — structured system prompts grounding LLM outputs in source documents to reduce hallucinations
- **Human-in-the-Loop:** Review checkpoints before any output reaches downstream systems

## Results
- 60% reduction in user story writing time
- Consistent output quality across different product domains
- Compliance-aware outputs for regulated environments

## Stack
Claude API · Node.js · Prompt Engineering · AI Evals · Context Engineering
