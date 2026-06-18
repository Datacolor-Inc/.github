**Proactive Data Quality Monitoring for a Global Facilities & Hygiene Services Leader**

**1. Description**

A multinational provider of pest control and hygiene services - operating across thousands of branches and serving millions of customers globally - partnered with Datacolor to implement enterprise-grade data quality observability platform, powered by Datacolor’s AtlasDQ solution, ensuring real-time health monitoring of 30 KPIs across 5 functions.

The AI-driven data quality agent layer was designed to autonomously evaluate this pipeline against a defined set of data quality rules - freshness, validity, variance, and reconciliation - and to surface a single quality score with drill-down explanations, removing the need for analysts to manually trace anomalies back through SQL.

**2. Business Problem**

Before Atlas DQ, the customer's data quality process was entirely reactive:

- A business analyst would notice a number "looked off" in the morning sales report.
- They'd escalate to engineering, who would spend **1–2 hours** running ad hoc SQL to trace the discrepancy back through the pipeline.
- By the time root cause was found, the report had often already been acted on or distributed.

This reactive loop created three compounding problems:

- **Operational risk** - duplicate or mismatched reference data (e.g., employee/sales rep IDs sourced differently across two upstream systems) silently inflated sales figures.
- **Business risk** - KPI-level metrics (sales, revenue, work orders) lacked any automated variance detection, so swings could go unnoticed until a person happened to look.
- **Pipeline risk** - no systematic check existed for source-to-target record integrity or refresh latency across the BigQuery → Power BI pipeline, so broken joins or stale data could pass through undetected.

There was no mechanism to catch any of this **before** a human escalated - and no way to quantify "how good" the data was at any given moment.

**3. Solution Overview**

Datacolor deployed Atlas DQ - a proactive data quality observability platform - directly within the customer's existing GCP environment, with zero changes to their upstream pipeline infrastructure.

Rather than replacing any part of the BigQuery → Power BI stack, Atlas DQ was layered on top as a monitoring and alerting layer. It runs on a configurable daily schedule aligned to the customer's data refresh cycle, automatically evaluating the health of their most critical business report - Daily Sales Performance - against a defined library of data quality rules before the business day begins.

The core shift Atlas DQ enables is from a reactive, human-escalation model to a proactive, automated signal model:

|**Before**|**After**|
|---|---|
|Business analyst notices anomaly|Atlas DQ flags anomaly at 6 AM|
|Escalates to engineering|No escalation required|
|1–2 hrs of ad hoc SQL tracing|Root cause surfaced in the dashboard|
|No visibility into "how good" the data is|Composite DQ score with drill-down|

The platform surfaces a single composite Data Quality Score each morning - covering freshness, validity, metric variance, and source-to-target reconciliation - with drill-down capability so analysts can go from "the score is 98%" to "here is the specific customer segment driving the deviation" without writing a single query.

**Architecture**

![Architecture](/CaseStudies/Picture1.png)

Built-for and integrates with existing data stack

·      GCP-native, containerised -Atlas DQ runs on Cloud Run (Dev → Prod), with CI/CD via GitHub + Cloud Build.

·      Queries BigQuery in-place - SQL pushdown executes directly on Rentokil's existing BigQuery Medallion layers (Gold, Silver, Bronze).

·      Configurable multi-channel integrations - Breaches trigger Pub/Sub → Email (SMTP), Google Chat Space, PagerDuty, and Jira automatically.

|**Before**|**After**|
|---|---|
|Business analyst notices anomaly|Atlas DQ flags anomaly at 6 AM|
|Escalates to engineering|No escalation required|
|1–2 hrs of ad hoc SQL tracing|Root cause surfaced in the dashboard|
|No visibility into "how good" the data is|Composite DQ score with drill-down
  

**4. Results & Business Impact**

Shift from reactive to proactive monitoring:

- **Composite DQ score** computed automatically each morning, with one-click drill-down into gap.
- **Time-to-insight collapsed from 1–2 hours of manual escalation-driven SQL analysis to an automated 6 AM signal** - issues are visible before the business day starts, not after someone notices a problem.
- Reframed the operational model from _"a person has to notice something is wrong"_ to _"the system tells you exactly what's wrong and why,"_ directly addressing the duplicate-reference-data and broken-join risks that previously went undetected.

**Business Impact at a Glance**

- **8x team scaling avoided** - proactive monitoring kept operations running with a 2-person team, eliminating the need to grow to a 15-person function and saving an estimated $1.2Mn annually in analyst headcount.
- **Zero reactive escalations** - issues surfaced automatically at 6 AM before business hours, eliminating a recurring 1–2 hour daily engineering drain that had no end in sight.
- **Trusted Data customer could act on** - clean, reconciled daily sales data gave commercial teams the confidence to pursue upsell and cross-sell opportunities, knowing the numbers reflected reality rather than data artifacts.