# Task 6: SOLID Violations (in the naive version)

## 1. Single Responsibility Principle: User (FR-01, FR-02, FR-07)
The naive User class changes whenever login, posting or admin rules change. Keep only user data in User, and move login to AuthService and role management to UserAdminService, while posting goes to content services.

## 2. Dependency Inversion Principle: AssignmentService (FR-04, NFR-06)
The naive AssignmentService depends directly on a MySQL connection and runs SQL itself. Make it depend on the AssignmentRepository interface, with MySqlAssignmentRepository supplying the database code and a fake repository used in tests.

Plain JavaScript has no interfaces: pass in any object with the same methods (or use TypeScript).
