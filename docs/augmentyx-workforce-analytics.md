# Augmentyx workforce analytics

My work for Augmentyx began with MVP discovery, local development setup, and cloud and AI service evaluation. After the scope shifted to HR analytics, the prototype focused on workforce KPIs, department breakdowns, and retention and attrition views. Development included checking metric calculations and data mappings against representative records, exercising filters, and refining how the dashboard handled missing or empty results.

## Where the work connects to this repository

| Augmentyx work | Current implementation |
| --- | --- |
| Workforce KPIs, charts, and reporting filters | **Insights** (`/insights`) shows workforce movement, department comparisons, and continuity measures. Reporting scope includes dates, department, location, and reporting interval. See the [Insights calculation contracts](reference.md#insights-calculation-contracts). |
| Analytics API contracts and data mapping | The early prototype explored a Next.js dashboard backed by FastAPI. In this repository, the Next.js [Insights page](../app/%28workspace%29/insights/page.tsx) calls the [server-side analytics service](../lib/server/hr-analytics.ts) for PostgreSQL-backed metrics. |
| Retention and attrition review | **Attrition** (`/attrition`) presents operational evidence for human review. **Risk Review** (`/risk-review`) supports historical model validation. See the [model card](../backend/MODEL_CARD.md) for training data, evaluation, and limitations. |
| Infrastructure and delivery | [Terraform configuration](../infra/) and the [GitHub Actions workflow](../.github/workflows/production.yml) support the Azure deployment described in the [technical reference](reference.md#deployment). |

## Local walkthrough

1. Follow the [local setup](../README.md#run-locally) with a disposable PostgreSQL database and `SEED_DEMO_DATA=true`.
2. Open `/insights` and note the hires, exits, and net movement for the initial date range. Under **Reporting scope**, narrow the dates and select a department or location. Check that the displayed scope and department comparisons reflect the selection.
3. Try a scope with no matching records, then reset the scope. Check how the dashboard presents empty results and that the previous view can be recovered.
4. Open `/attrition` to inspect the department continuity evidence, then open `/risk-review` to inspect historical model records. Use operational evidence for human review and historical scores for model evaluation.
5. Run `pnpm test:insights` to check the analytics calculations covered by the [workforce insights tests](../tests/workforce-insights.test.ts).
