###                  Company Managment System
## User-API
#UML
```mermaid
classDiagram
class User{
-name: String
-id: long
-managerId: long
-title: String
-level: Level
-role: String
-email: String
-password: String
-phone: String
-company: String
-department: String
-location: String
-salaryNet: float
-salaryGross: float
}
class UserProjetion{
 <<interface>>
+ getName(): String
+ getId():long
+getManagerId():long
+getCompany():String 
+getDepartment(): String
}
```
#ERD

```mermaid
erDiagram
User {
        long id PK
        string name
        long managerId FK
        string title
        string level
        string role
        string mail
        string password
        string phone
        long departmentId fk
        float salaryGross
    }
    Company{
        long id  pk
        String name  
        String Location
        string description
        }
    Department{
          long id pk
          long companyId fk
          string location
    }
    UserHistory{
        long id pk
        long recordId pk
       long managerId FK
        string title
        string level
        string role
        long departmentId fk
        float salaryGross
}
User ||--o{ Department : "belongs to"
Department ||--o{ Company : "belongs to"
User ||--o{ User : "reports to"
UserHistory ||--o{ User : "has"

```
## Team API 
#UML 

#ERD
```mermaid
erDiagram
    TEAM {
        long id PK
        long managerId
    }
    TEAM-MEMBER {
        long userId PK
        long teamId PK, FK
    }
    TEAM ||--o{ TEAM-MEMBER : has
```
##Evaluation API 
#UML

#ERD
```mermaid
erDiagram
Cycle{
long cycleId pk
string name
DateTime startDate
DateTime endDate
CycleState State
}
KPI{
long kpiId pk
long cycleId fk
string name
}
Ratings{
long id pk
long kpiId fk
long submitterId
long ratedpersonId
string feedback
}
Objectives {
    long objectiveId pk
    long cycleId fk
    string title
    string description
    long assignedUserId 
    string deadline
  }
Objectives ||--o{Cycle : "belongs to"
Ratings ||--o{Cycle : "belongs to"
KPI ||--o{Cycle : "belongs to" 
```
## Attendance API 

# UML

#ERD
```mermaid
erDiagram
VacationRequest{
long requestId pk
long userId
long TeamId
DateTime start
DateTime end
string status
}
Attendance{
long UserId pk 
Date day pk
Time arrival
Time departure 
String location
}
```

        
          
