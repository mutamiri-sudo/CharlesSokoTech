# VOLT Supply — E-Commerce Backend & Product Sync Engine

## Overview
Backend automation system for an electronics supply e-commerce store. Manages the full product lifecycle from distributor catalog to customer-facing storefront.

## Problem
Manually managing thousands of electronic components across a distributor (DigiKey) and an e-commerce storefront (Shopify) is unsustainable — pricing changes daily, inventory fluctuates, and product descriptions need SEO optimization.

## Solution
An automated backend that syncs products, manages dynamic pricing, and generates optimized shopping feeds.

### Key Features
- **Product Sync Engine** — Automated catalog sync between DigiKey distributor API and Shopify storefront
- **Dynamic Pricing** — Rule-based pricing engine with configurable markup tiers and margin management
- **SEO Optimization** — Automated product description and metadata generation
- **Google Shopping Feed** — Automated feed generation meeting Google Merchant Center specifications
- **Scheduled Jobs** — Cron-based automation running on Railway for hands-off operation

## Stack
JavaScript · Node.js · Shopify API · DigiKey API · Railway · Google Shopping Feed
