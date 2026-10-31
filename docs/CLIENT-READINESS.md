# Client readiness and proposed acceptance plan

**Review basis:** the repository's workflow exports and historical documentation reviewed on 31 October 2026. This is not a live security audit or a new test execution report.

## Work needed before a client pilot

| Priority | Work item | Evidence needed to close it |
| --- | --- | --- |
| 1 | Reproducible environment | Tested setup instructions, dependency versions, database schema and access-policy documentation, synthetic fixtures and a sanitized export. |
| 1 | Strict request validation | Explicit handling of missing body, wrong types, missing fields, invalid categories, oversized input and supported content types. |
| 1 | Duplicate protection | A documented request identifier and storage constraint or equivalent; replaying the same event does not create duplicate tickets. A timestamp alone is insufficient proof. |
| 1 | Failure handling | Controlled database outage, timeout and authentication-failure tests; no false success response; bounded recovery and a visible failed-request record where feasible. |
| 1 | Endpoint protection | A documented access/abuse-control design appropriate to a public form or server integration. CORS alone does not authenticate requests. |
| 1 | Data handling | Required fields, access boundaries, redaction, retention and deletion defined, including what happens to invalid submissions. |
| 2 | Observable operations | Correlation IDs, actionable error reporting and an operator's retry/recovery procedure. |
| 2 | Maintainable handover | Setup/runbook, ownership of accounts and costs, known limits, rollback steps and support boundaries. |
| Later | Supervised order assistance | Authorized read-only order lookup, approved policy sources, draft responses and explicit human approval. |

The reviewed export does not show explicit authentication, request deduplication, rate limits or a database-error branch. Infrastructure outside the export may supply controls; it has not been reviewed here.

## Acceptance cases to execute

Every case below is **NOT RUN in this documentation update**. Desired outcomes for new protections are requirements, not descriptions of the current implementation.

| ID | Scenario | Desired outcome / observation to record |
| --- | --- | --- |
| I01 | Valid synthetic `order_status` request | 201, one new ticket, returned ID matches stored record. |
| I02 | Valid `return`, `product_question` and `other` requests | Each accepted category behaves as specified. Record each execution separately. |
| I03 | Mixed-case email/category and leading `#` on order number | Documented normalization reflected in stored values. |
| I04 | Missing or whitespace-only name | Rejected with the documented validation response. |
| I05 | Malformed email | Rejected without a success response. |
| I06 | Empty message or unknown category | Rejected with a useful, non-sensitive error. |
| I07 | Missing body, malformed JSON or unsupported content type | Controlled request error; no unintended ticket creation. |
| I08 | Arrays, objects or numbers in text fields | Strictly rejected or handled according to an explicit schema; not accidentally accepted by string coercion. |
| I09 | Oversized message or unexpected fields | Enforced documented limits and no unneeded data retention. |
| I10 | Same event delivered twice, including simultaneous delivery | One logical ticket after duplicate protection is implemented. |
| I11 | Database unavailable or invalid database credential | No false 201 success; defined error handling, observability and recovery. |
| I12 | Database timeout followed by retry | Defined behavior even if the first write succeeded but acknowledgement was lost. |
| I13 | Burst of requests | Access/abuse limits behave as designed; legitimate failures are visible. |
| I14 | Unauthorized read of another customer's ticket | Access denied; record both the access policy and the actual test result. |
| I15 | Redaction and retention exercise | No credentials in exports/logs/screenshots; test records can be removed according to the retention design. |

## Evidence record template

For each actual run, record:

- Case ID, UTC timestamp, commit SHA, workflow version and environment.
- Synthetic input or fixture path; never include a real customer's personal data.
- Expected HTTP response and storage outcome.
- Actual HTTP response and storage outcome.
- Redacted execution reference or screenshot.
- PASS, FAIL or BLOCKED, with the reason and any follow-up issue.

Keep a failed run visible until it is resolved. A static review or a screenshot of the canvas does not replace runtime verification.

## Boundaries for a first paid engagement

Offer a scoped assessment or a single intake/integration milestone only when you can demonstrate it and explain its failure modes. Agree on the source system, destination, expected volume, fields, acceptance cases, access needed and handover before quoting implementation.

A first milestone should exclude automatic refunds, payments, inventory changes, customer promises and unsupervised outbound messaging. Additional actions require their own agreed requirements, permissions and acceptance evidence.

Before calling a pilot ready, complete the priority-1 checks, demonstrate the agreed workflow in a test environment, identify who owns operation and recovery, and obtain the client's acceptance of the documented scope. This checklist alone does not certify readiness.
