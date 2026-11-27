# Task 7: Observer Pattern (FR-04, FR-06, NFR-03, QA-03)
**Problem:** creating an assignment must trigger notifications, but AssignmentService should not depend on how they are made.

**Pattern:** AssignmentService is the subject. NotificationObserver implements AssignmentObserver and is registered when the server starts. The service saves the assignment first, then calls each observer. It catches and logs each observer's error (including awaited async errors), so a failure does not undo or hide the saved assignment.

**Why it is not over-engineering:** it is one small interface and a list, with no message broker. It separates saving from a side task the SRS requires to fail safely. An email observer could be added later without changing the assignment rules. If notifications stayed the only reaction forever, a direct injected call would also work; that is the trade-off.

**Limit:** Observer alone does not retry. A notification lost because of an error or server crash stays lost unless a retry is added.

The class diagram with the pattern is the "After" diagram in 05-class-design.md.
