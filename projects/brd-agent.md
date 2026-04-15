# BRD Agent — AI-Powered Business Requirements Document Generator

## Overview
A production LLM-powered agent that automates the most time-consuming part of product and business analysis work: writing structured Business Requirements Documents (BRDs). Built on the Claude API with custom prompt architecture designed for regulated financial services environments.

## Problem
Business analysts and product managers spend hours writing BRDs — business context, stakeholder needs, functional and non-functional requirements, user stories, acceptance criteria, and test scenarios — often repeating patterns across similar initiatives. In regulated industries (fintech, insurance, mortgage), every requirement also needs compliance flags and audit-ready documentation.

## Solution
The BRD Agent takes a single business problem statement and generates a complete, sprint-ready BRD:

| Output | Description |
|--------|-------------|
| Executive Summary | Business context, objective, and stakeholder alignment |
| Scope & Assumptions | In-scope / out-of-scope boundaries, dependencies, constraints |
| Functional Requirements | What the system must do, mapped to business outcomes |
| Non-Functional Requirements | Performance, security, compliance, availability |
| User Stories | Structured "As a / I want / So that" with acceptance criteria |
| Gherkin Scenarios | Given/When/Then test cases for QA handoff |
| Compliance Flags | Regulatory considerations for fintech / insurance / mortgage |
| Success Metrics | KPIs and measurement criteria tied back to the business objective |

## Technical Approach
- **Prompt Architecture:** Multi-stage prompt chain with context injection from uploaded source documents
- **AI Evals:** Automated output validation pipeline that checks generated requirements against quality standards
- **Context Management:** RAG-adjacent patterns — structured system prompts grounding LLM outputs in source documents to reduce hallucinations
- **Human-in-the-Loop:** Review checkpoints before any output reaches downstream systems

## Results
- 60% reduction in BRD and user-story writing time
- Consistent output quality across different business domains
- Compliance-aware outputs for regulated environments

## Stack
Claude API · Node.js · Prompt Engineering · AI Evals · Context Engineering
