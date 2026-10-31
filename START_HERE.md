# Start here

This repository contains two implemented foundations, historical evidence, and a proposed next increment. Start with the [README](README.md) rather than treating the original Day 1 checklist as the current project status.

## For a potential client

Read the [case study](docs/PORTFOLIO-CASE-STUDY.md), inspect the workflow exports, and review the [remaining readiness work](docs/CLIENT-READINESS.md). These materials demonstrate implementation approach and scope awareness. They do not establish production performance or a completed customer engagement.

## For a technical reviewer

| Review item | Location |
| --- | --- |
| Shopify product-read workflow | [Day 1 export](n8n-workflows/day1-shopify-admin-graphql-Safe.json) |
| Intake, validation, persistence, responses | [Day 2 export](n8n-workflows/D2%20-%20Shopify%20Support%20Intake.json) |
| Recorded Shopify results | [Day 1 test report](test-reports/day1-test-report.md) |
| Recorded intake results | [Day 2 test report](test-reports/test-reports/day2-support-intake-tests.md) |
| Historical setup notes | [Original Day 1 README](docs/history/README-day1.md) |
| Future acceptance cases and evidence template | [Client readiness](docs/CLIENT-READINESS.md) |

## Reproduction prerequisites

The repository is not yet a one-click deployment package. Before a new test run:

1. Use an isolated n8n test environment and a Shopify development store. Record the actual n8n version and relevant node versions used.
2. Review each export before importing it. Replace environment-specific references with your own test configuration; keep workflows inactive until the review is complete.
3. Configure your own Shopify and Supabase credentials outside source control. Do not reuse screenshot values or historical identifiers.
4. Document and provision the `support_tickets` schema and access policies in a test database. The intake export shows field mappings, but does not supply the database definition.
5. Confirm the webhook route, allowed origins, access controls, and data-retention approach for the test environment.
6. Run the proposed acceptance cases with synthetic inputs. Capture the actual HTTP result and database outcome, including failures.
7. Publish a redacted, dated evidence report tied to a commit only after execution. Do not convert proposed outcomes into PASS entries without running them.

The Day 1 Shopify product query and Day 2 intake should be tested independently. Do not imply they form a connected order-support workflow until that connection exists and has been verified.

## Next implementation priority

First make the current intake reproducible and handle duplicate requests and storage failures. Then consider one read-only order-support path with human approval. Adding several integrations before these foundations are verified will make diagnosis and handover harder.
