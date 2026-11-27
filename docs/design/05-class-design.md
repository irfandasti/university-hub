# Task 5: Cohesion and Coupling (and Task 7 class diagram)
Both diagrams use UML class notation: attributes, operations, visibility and multiplicity. Version 1 is the initial design. Version 2 is the improved design. Content services other than assignments are left out to keep the focus.

| Problem class | Problem in version 1 | Fix in version 2 |
|---|---|---|
| User | Low cohesion: account data, login, posting and admin work in one class | User keeps data; AuthService and UserAdminService take login and admin work. Posting belongs to content services. |
| AssignmentService | Does validation, SQL, notifications and reminders; tightly coupled to MySQL | Uses AssignmentValidator, AssignmentRepository and an observer for notifications. Reminders move to the scheduler job. |

## Before (version 1)

```mermaid
classDiagram
  direction LR
  class User {
    -userId : int
    -fullName : String
    -email : String
    -passwordHash : String
    -role : String
    -status : String
    +register()
    +login()
    +editProfile()
    +postAnnouncement()
    +addAssignment()
    +manageUsers()
    +changeRole()
  }
  class SchoolClass {
    -classId : int
    -name : String
    -subject : String
    -department : String
  }
  class Assignment {
    -assignmentId : int
    -title : String
    -description : String
    -instructions : String
    -createdAt : DateTime
    -deadline : DateTime
  }
  class AssignmentService {
    -db : MySQLConnection
    +create(data)
    +validate(data)
    +runSql(query)
    +createNotifications(a)
    +sendReminders()
  }
  class Announcement {
    -announcementId : int
    -title : String
    -message : String
    -audience : String
    -createdAt : DateTime
    -expiresAt : DateTime
  }
  class Event {
    -eventId : int
    -name : String
    -description : String
    -startsAt : DateTime
    -place : String
    -status : String
  }
  class Society {
    -societyId : int
    -name : String
    -activities : String
    -contact : String
  }
  class Notification {
    -notificationId : int
    -message : String
    -createdAt : DateTime
    -isRead : boolean
  }
  User "0..*" -- "0..*" SchoolClass : linked to
  SchoolClass "1" -- "0..*" Assignment : has
  User "1" -- "0..*" Assignment : teacher posts
  User "1" -- "0..*" Announcement : creates
  User "1" -- "0..*" Event : creates
  Society "0..1" -- "0..*" Event : organizes
  User "1" *-- "0..*" Notification : receives
  AssignmentService ..> Assignment
```

## After (version 2, with Observer pattern)

```mermaid
classDiagram
  direction LR
  class User {
    -userId : int
    -fullName : String
    -email : String
    -passwordHash : String
    -role : String
    -status : String
  }
  class SchoolClass {
    -classId : int
    -name : String
    -subject : String
    -department : String
  }
  class Assignment {
    -assignmentId : int
    -title : String
    -description : String
    -instructions : String
    -createdAt : DateTime
    -deadline : DateTime
  }
  class Announcement {
    -announcementId : int
    -title : String
    -message : String
    -audience : String
    -createdAt : DateTime
    -expiresAt : DateTime
  }
  class Event {
    -eventId : int
    -name : String
    -description : String
    -startsAt : DateTime
    -place : String
    -status : String
  }
  class Society {
    -societyId : int
    -name : String
    -activities : String
    -contact : String
  }
  class Notification {
    -notificationId : int
    -message : String
    -createdAt : DateTime
    -isRead : boolean
  }
  User "0..*" -- "0..*" SchoolClass : linked to
  SchoolClass "1" -- "0..*" Assignment : has
  User "1" -- "0..*" Assignment : teacher posts
  User "1" -- "0..*" Announcement : creates
  User "1" -- "0..*" Event : creates
  Society "0..1" -- "0..*" Event : organizes
  User "1" *-- "0..*" Notification : receives
  class AuthService {
    +register(data)
    +login(email, password)
  }
  class UserAdminService {
    +setRole(userId, role)
    +setStatus(userId, status)
  }
  class AssignmentService {
    +create(teacher, data)
    +subscribe(observer)
    -notifyObservers(a)
  }
  class AssignmentValidator {
    +validate(data)
  }
  class AssignmentRepository {
    <<interface>>
    +create(data)
  }
  class MySqlAssignmentRepository {
    +create(data)
  }
  class AssignmentObserver {
    <<interface>>
    +onAssignmentCreated(a)
  }
  class NotificationObserver {
    +onAssignmentCreated(a)
  }
  AuthService ..> User
  UserAdminService ..> User
  AssignmentService ..> Assignment
  AssignmentService --> AssignmentValidator
  AssignmentService --> AssignmentRepository
  AssignmentRepository <|.. MySqlAssignmentRepository
  AssignmentService "1" o-- "0..*" AssignmentObserver
  AssignmentObserver <|.. NotificationObserver
  NotificationObserver ..> Notification
```
