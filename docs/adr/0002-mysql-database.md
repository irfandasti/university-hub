# ADR-0002: Use MySQL as the database
- **Status:** Accepted 
- **Date:** 2026-11-27
- **Decided by:** M IRFAN 
- **Requirements:** FR-01, FR-03 to FR-06, NFR-03, NFR-09

## Context
Users, classes, enrollments, assignments, events and notifications are related records.

## Decision
Use MySQL with InnoDB tables, foreign keys, transactions and parameterized queries.

## Alternatives
- MongoDB (document database): rejected. It can model this data, but our data is mainly relational and we want foreign key constraints.
- SQLite: rejected for the hosted version, because it has limited support for many writes at the same time.

## Consequences
- Good: relationships can be enforced by the database; SQL joins fit class-based queries.
- Cost: schema changes need migration scripts; the team must run and back up a database server.
- The notification link to three content types needs a check in the application.
