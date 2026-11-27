# University Hub: Docs and Traceability
| Task | File |
|---|---|
| 1 Quality attributes | architecture/01-quality-attributes.md, srs/ |
| 2 Styles | architecture/02-architectural-styles.md |
| 3 Diagrams | architecture/03-diagrams.md |
| 4 ADRs | adr/ |
| 5 Cohesion and coupling | design/05-class-design.md |
| 6 SOLID | design/06-solid.md |
| 7 Observer | design/07-observer-pattern.md |
| 8 API contracts | design/08-api-contract.md |
| 9 AI use | design/09-ai-use.md |
| 10 GitHub and traceability | this docs folder and the table below |

## Decisions linked to SRS IDs
| Decision | SRS IDs |
|---|---|
| Client-server | FR-02 to FR-05, NFR-04 |
| Layered monolith (ADR-0001) | FR-01 to FR-07, NFR-06, NFR-08 |
| MySQL (ADR-0002) | FR-01, FR-03 to FR-06, NFR-03, NFR-09 |
| Repository interface | FR-04, NFR-06 |
| Split User responsibilities | FR-01, FR-02, FR-07 |
| Observer | FR-04, FR-06, NFR-03 |
| API contracts | FR-02, FR-04, FR-06, NFR-03, NFR-04 |
| Deployment sketch | NFR-04, NFR-09 |

FR-01 Accounts, FR-02 Login, FR-03 Announcements, FR-04 Assignments, FR-05 Events and societies, FR-06 Notifications, FR-07 Admin panel.
NFR-01 Speed, 02 Ease of use, 03 Reliability, 04 Security, 05 Availability, 06 Maintenance, 07 Compatibility, 08 Growth, 09 Backup.
