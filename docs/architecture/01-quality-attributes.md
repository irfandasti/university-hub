# Task 1: Top Three Quality Attributes
Also added to the SRS as section 14.10. Targets are proposed and **not yet tested**.

| Rank | Attribute | One-line reason | Measurable scenario | SRS IDs |
|---|---|---|---|---|
| 1 | Security (QA-01) | Accounts and university data need role-based protection. | When a logged-in student sends admin or notice-change requests on the test server, the API refuses them: 100% get 403 and no data changes. | NFR-04, FR-07 |
| 2 | Ease of Use (QA-02) | Some users are not good with computers. | At least 4 of 5 first-time students, logged in on a phone, find a given assignment deadline within 60 seconds without help. | NFR-02, FR-04 |
| 3 | Reliability (QA-03) | A post must not be lost when a notification fails. | In 20 of 20 forced notification failures, the saved post stays visible and the error is logged. | NFR-03, FR-06 |

Full scenario tables (source, stimulus, artifact, environment, response, measure) are in SRS 14.10.
