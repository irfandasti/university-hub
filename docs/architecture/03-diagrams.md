# Task 3: Context, Container and Deployment Diagrams

The deployment sketch matches the context and container diagrams. It shows what runs on which device or server. Hosting is proposed and the provider is not yet chosen.

## Context diagram

```mermaid
flowchart LR
  S([Student]) -->|views content, gets reminders| H[University Hub]
  T([Teacher]) -->|posts assignments and class notices| H
  A([Admin]) -->|manages users, notices, events| H
  H -.->|optional, future| E[External email service]
```

## Container diagram

```mermaid
flowchart TB
  U([Student, Teacher, Admin]) -->|uses| W["Web app: React in browser"]
  W -->|"HTTPS, JSON"| API
  subgraph SERVER["Application server: Node.js"]
    API["API layer: Express routes, controllers, auth and role checks"] --> SV["Service layer: accounts, announcements, assignments, events, notifications, admin"]
    J["Reminder scheduler: node-cron"] --> SV
    SV --> R["Data access: repositories"]
  end
  R -->|SQL| DB[("MySQL database")]
```

## Deployment diagram

```mermaid
flowchart TB
  subgraph DEV["User device: computer or phone"]
    B["Web browser running the React app"]
  end
  subgraph HOST["Hosted server (provider not chosen)"]
    WEB["Web server: React build files, HTTPS entry"]
    APP["Node.js: Express API and scheduler"]
    DB[("MySQL")]
    WEB -->|forwards API requests| APP
    APP -->|SQL| DB
  end
  BK[("Backup storage, separate from the server")]
  B -->|HTTPS| WEB
  DB -.->|scheduled backup| BK
```
