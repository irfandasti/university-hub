# Task 8: API Contract Sketch (proposed)
All requests use HTTPS and JSON. Error body: `{"error": {"code": "...", "message": "..."}}`

## 1. POST /api/auth/login (FR-02, NFR-04)
Authentication: none.

Request:
```json
{ "email": "student@example.com", "password": "<password>" }
```
200 OK:
```json
{ "token": "<jwt>", "user": { "id": 12, "fullName": "Test Student", "role": "student" } }
```
| Status | Meaning |
|---|---|
| 400 | Missing or invalid field |
| 401 | Wrong login details or inactive account (same message for both) |
| 429 | Too many attempts |
| 500 | Server error, no private details |

## 2. POST /api/assignments (FR-04, FR-06, NFR-03, NFR-04)
Header: `Authorization: Bearer <jwt>`. Only a teacher linked to the class.

Request (teacher ID comes from the token, never from the body):
```json
{
  "title": "ER Diagram",
  "description": "Draw the ER diagram for the project.",
  "classId": 3,
  "deadline": "2026-12-10T23:59:00+05:00",
  "instructions": "Optional"
}
```
Required: title, description, classId, deadline (in the future). The server sets createdAt.

201 Created:
```json
{ "id": 45, "title": "ER Diagram", "classId": 3, "deadline": "2026-12-10T23:59:00+05:00", "createdAt": "2026-11-27T10:00:00+05:00" }
```
| Status | Meaning |
|---|---|
| 400 | Invalid or missing field; nothing saved |
| 401 | Not logged in or token invalid |
| 403 | Not a teacher, inactive account, or not linked to this class |
| 500 | Assignment could not be saved |

If the assignment is saved but notification creation fails, still return 201 and log the error.
A repeated request can create a duplicate; the form should disable Submit while sending.
