# ADR-0001: Use a layered, client-server monolith
- **Status:** Proposed (team approval needed)
- **Date:** 2026-11-27
- **Decided by:** ____________ (team fills after approval)
- **Requirements:** FR-01 to FR-07, NFR-04, NFR-06, NFR-08

## Context
Three user roles share one set of data. The team is small, and time and resources are limited.

## Decision
Use a React client and one Node.js/Express server application with API, service and data access layers.

## Alternatives
- Microservices: rejected, too much deployment and communication work for this scope.
- One unlayered codebase: rejected, pages, rules and SQL would become tightly linked.

## Consequences
- Good: one server application to deploy; rules can be tested separately.
- Cost: more files and pass-through code; the application is scaled and restarted as one unit; one server can be a single point of failure.
