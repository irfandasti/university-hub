# Task 2: Architectural Styles

## Client-Server
**Why it fits:** students, teachers and the admin use browsers but need the same notices, assignments and events (FR-03, FR-04, FR-05). One server also gives one place to check login and roles (NFR-04, QA-01).
**Cost:** the system needs internet and a hosted server. The server can be a single point of failure.
**Rejected:** peer-to-peer. It would make shared data, backups and role checks much harder.

## Layered Monolith
One Express application with layers: API, service, data access. React is the presentation layer and MySQL is the data source.
**Why it fits:** the team is small and the first version is limited. Separate layers support maintenance and testing (NFR-06) while there is only one server application to deploy.
**Cost:** simple actions need code in several layers. The whole server application is deployed and restarted together, and growth is by scaling all of it (NFR-08).
**Rejected:** microservices. They add service communication, more deployments and harder debugging, which the current requirements do not need.

See ADR-0001. MVC and the repository pattern organize code inside these styles.
