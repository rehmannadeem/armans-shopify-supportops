# Case study: structured ecommerce support intake

**Project type:** self-directed portfolio project using a Shopify development store.  
**Status:** foundational workflows implemented; historical execution records available; current runtime verification pending.  
**Author:** Rehman Nadeem, Armans.AI.

## Business context

An ecommerce support operator needs enough structured information to understand a request and route it correctly. Free-text messages alone can omit essential details, and inconsistent records make follow-up difficult.

This project models that problem using a development store. It does not claim that a paying merchant commissioned the system or that a real merchant's operating metrics improved.

## Implemented scope

The first workflow reads a known test product through Shopify's Admin GraphQL API. The second accepts a support form submission, normalizes its fields, checks required fields and request categories, and attempts to record either a new ticket or a rejected request in Supabase. Successful database writes lead to a 201 or 422 response, depending on validation.

These are separate foundations. The intake workflow does not retrieve order status or automatically answer a customer.

## Design decisions visible in the export

| Decision | Purpose | Remaining concern |
| --- | --- | --- |
| Normalize email, category and order-number formatting | Make records more consistent | String coercion is not strict input-type validation. |
| Explicit allowed request categories | Keep the initial routing scope understandable | Categories do not establish whether a request is safe to automate. |
| Separate valid and rejected records | Make validation outcomes observable | Storing invalid submissions also stores submitted personal information. |
| Store before sending the response | Return success after the storage step | A storage failure needs a deliberate error response and recovery path. |
| Keep product reads separate from intake | Demonstrate each foundation independently | The full support journey remains unimplemented. |

## Evidence available

- [Product-read workflow](../n8n-workflows/day1-shopify-admin-graphql-Safe.json) and [historical report](../test-reports/day1-test-report.md).
- [Support-intake workflow](../n8n-workflows/D2%20-%20Shopify%20Support%20Intake.json) and [historical report](../test-reports/test-reports/day2-support-intake-tests.md).
- [Screenshot directory](../screenshots/).

The Day 2 report records 10/10 acceptance tests, but does not enumerate the cases or include execution evidence. This documentation review has not independently rerun those tests. The next evidence report should record each input, expected result, actual response, database outcome and execution reference.

## Proposed demonstration after verification

1. Explain the support operator's problem and the narrow scope.
2. Submit a synthetic valid request and show the response and stored record.
3. Submit an invalid request and show its actual handling.
4. Replay a request and explain the observed duplicate behavior.
5. Demonstrate a controlled database failure and explain recovery behavior.
6. Show the limitations and the handover checklist.

Steps 4 and 5 are verification targets, not claims that duplicate protection or graceful recovery currently exist.

## Proposed next increment

After the intake passes its readiness checks, add one read-only order-status path. Verify the customer's right to see the order, retrieve only the required fields, draft a response using approved policies, and require a person to approve it. Keep refunds, cancellations, address changes, and other write actions outside the first increment.

## What can honestly be said today

> I built an n8n portfolio project that reads Shopify development-store product data and includes a separate support-intake workflow with validation and database storage. The repository includes historical execution evidence and a clear plan for reproducibility, failure handling and a supervised support-assistant extension.

Do not describe this project as a production AI support platform, a completed merchant deployment, or evidence of measured revenue or time savings.

See [client readiness](CLIENT-READINESS.md) for the proposed acceptance cases and pilot boundaries.
