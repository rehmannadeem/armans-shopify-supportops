# Day 1 Test Report

| Test | Expected | Actual | Result |
|---|---|---|---|
| Token request | Token, scope, expiry returned | Returned successfully | PASS |
| Product query | Store and target product JSON | Returned successfully | PASS |
| Invalid handle | Empty `edges` without API failure | Not yet recorded | PENDING |
| Missing scope | GraphQL access-denied error | Not yet tested | PENDING |
| Secret audit | No real secrets in export/repository | Check before commit | PENDING |
