###                  Company Managment System
## User-API
# UML
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
class Level{
<<enumeration>>
Fresh
Junior
Senior
Lead
}
class UserHistory{
-userId:long
-recordId:long
-managerId:long
-title: string
-level:Leve
-role: strin
-departmentId: long
-salaryGross: float
}
class UserRepository{
<<interface>>
+getuserHistory():List<User>
+findUserById():User
+addUser():void
+deleteUser():void
+ updateUser(): void
+findUserById():UserProjection
}
class EmployeeService{
+findUserById():UserProjection
}
class ManagerService{
+findUserById():User
+addUser():void
+deleteUser():void
+ updateUser(): void
+ viewEmployeeHistory():List<User>
}
class EmployeeController{
+findUser():UserProjection
+getUserHistory():List<User>
}
class ManagerController{
+createUser(): User
+ updateUser(): void
+ deletUser(): void
+viewEmployeeHistory(): List<User>
}
ManagerService o-- UserRepository
EmployeeService o-- UserRepository
ManagerController o-- ManagerService
EmployeeController o-- EmployeeService


```
# ERD

```mermaid
erDiagram
User {
        long id PK
        string name
        long managerId FK
        string title
        int level
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
          string name
    }
    UserHistory{
        long id pk
        long recordId pk
       long managerId FK
        string title
        int level
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
# UML 
```mermaid
classDiagram
class Team {
  -teamId: long
  -teamManagerId: long
  -members: List
}

class UserDto {
  +name: String 
  +id: long
  +department: String
}

class TeamRepository {
  <<interface>>
  +createTeam(): void 
  +assignManager(): void
  +addMember(): void
  +getTeamById(): Team
  +removeMemberFromTeam(): void
  +getAllTeams(): List<Team>
}

class TeamService {
  +getUserById(): UserDto
  +getTeamById(): Team
  +getAllTeams(): List<Team>
  +addMember(): void
  +assignManager(): void
  +removeMember(): void
}

class TeamController {
  +getUserById(): UserDto
  +getTeamById(): Team
  +getAllTeams(): List<Team>
  +addMember(): void
  +assignManager(): void
  +removeMember(): void
}

TeamService o-- TeamRepository
TeamController o-- TeamService

```
# ERD
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
## Evaluation API 
# UML
```mermaid
classDiagram
class Cycle{
<<singleton>>
-startDate: DateTime
-duration: int 
-ratings:List<float>
-cycleMembers:List<User>
-cycleState:CycleState
+addMember(): void
+openCycle(): void
+closeCycle(): void
}
class objective{ 
-title: String
-description:String
-deadline:DateTime
-taskId:Long
-employeeId:long
}
class Rating{ 
-cycleId:long
-id: long 
-userId: long
-finalRating: float
-KPIs:List<int>
-weights:List<float>
}
class CycleState{ 
<<enumeration>> 
Open
Passed 
Closed
}
class CycleRepository{
<<interface>>
+openCycle
+closeCycle
+viewCycle():Cycle
}
class RatingsRepository{
<<interface>>
+ evaluateMember():void
}
class ObjectiveRepository{
<<interface>>
+assignObjective():void
+viewObjectives():List<Objective>
}
class UserService{
+ evaluateMember():void
+ viewCycle():Cycle
+viewObjectives():List<objective>

}
class CompanyManagerService{
+openCyclr():void
+closeCycle():void
+defineWeghts():void
}
class TeamManagerService{
+addTeamToCycle():void
+addMemberToCycle():void
+assignObjective():void
}
class UserController{
+ evaluateMember():void
+ viewCycle():void
+viewObjectives():List<objectives>
}
class CompanyManagerController{
+openCyclr():void
+closeCycle():void
+defineWeghts():void
}
class TeamManagerController{
+defineWeghts():void
+addMemberToCycle():void
+assignTask():void
}

UserController <|--CompanyManagerController
UserController <|--TeamManagerController
CompanyManagerService o-- CompanyManagerController
UserService o-- UserController
TeamManagerService o-- TeamManagerController
CycleRepository o-- UserService
RatingsRepository o-- UserService
ObjectiveRepository o-- UserService
ObjectiveRepository o-- TeamManagerService
CycleRepository o-- CompanyManagerService
CompanyManagerService ..>Cycle



```

# ERD
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
```mermaid
classDiagram
class AttendanceStatus{
<<enumeration>>
Absent
Remote
On-site
}
class AttendanceService{
+ setDailyStatus() Void
+ getDailyStatus() Attendance
+ getWeeklyStatus() List<Attendance>
}
class UserDTO{
-userId: int
-name: String
-department: String 
}
class AttendanceResponseDTO{
-userDto: UserDTO
-attendanceList: List<Attendance>
}
class AttendanceController{
+ setDailyStatus () Attendance
+ getDailyStatus () Attendance
+ getWeeklyStatus() List<Attendance>
}
class AttendanceRepository{
<<interface>>
+ findByUserIdAndDate Attendance
+ findByUserIdAndDateBetween Attendance
}

class Attendance{
-userId: int
-date: DateTime
-status: AttendanceStatus 
}

class Vacation{
-id: int
-userId: int
-startDate: DateTime
-endDate: DateTime
-status: VacationStatus
}
class VacationStatus{
<<enumeration>>
Pending
Approved
Rejected 
}
class VacationService{
+requestVacation(): void
+approveVacation(): void
+rejectVacation(): void
+getTeamVacations(): List<VacationRequest>
}
AttendanceController o-- AttendanceService
AttendanceService o-- AttendanceRepository

```
# ERD
```mermaid
erDiagram
VacationRequest{
long requestId pk
long userId
long TeamId
DateTime start
DateTime end
string statusType "ENUM('Pending', 'Approved', 'Rejected')"
}
Attendance{
long UserId pk 
Date attendance_date pk
Time arrival
Time departure 
String location "ENUM (Absent, 'Remote', 'On-site')"
}
```
## Hiring API
# UML
```mermaid
classDiagram
    class JobOpening {
        +Long jobId
        +String title
        +String department
        +String location
        +String description
        +String requirements
        +Long createdBy
        +LocalDateTime createdAt
        +JobStatus status
    }

    class JobApplication {
        +Long applicationId
        +JobOpening job
        +Long userId
        +String cvFile
        +LocalDateTime submittedAt
    }

    class JobStatus {
        <<enumeration>>
        OPEN
        CLOSED
    }

    class JobOpeningRepository {
        <<interface>>
        +createJob(): void
        +getJobs(): List<JobOpening>
        +getJobById(): JobOpening
        +updateJob(): void
        +deleteJob(): void
    }

    class JobApplicationRepository {
        <<interface>>
        +applyForJob(): void
        +getApplications(): List<JobApplication>
        +deleteApplication(): void
        +getCvFile(): File
    }

    class JobService {
        +createJob(): JobOpening
        +getJobs(): List<JobOpening>
        +getJobById(): JobOpening
        +updateJob(): JobOpening
        +deleteJob(): void
        +applyForJob(): JobApplication
        +getApplications(): List<JobApplication>
        +deleteApplication(): void
        +getCvFile(): File
    }

    class JobController {
        +createJob(): JobOpening
        +getJobs(): List<JobOpening>
        +getJobById(): JobOpening
        +updateJob(): JobOpening
        +deleteJob(): void
        +applyForJob(): JobApplication
        +getApplications(): List<JobApplication>
        +deleteApplication(): void
        +downloadCV(): Resource
    }

    JobOpening "1" --> "0..*" JobApplication : has
    JobOpening --> JobStatus : uses
    JobService o-- JobOpeningRepository
    JobService o-- JobApplicationRepository
    JobController o-- JobService
```
# ERD
```mermaid
erDiagram
    JOB_OPENINGS ||--o{ JOB_APPLICATIONS : "has"
    JOB_OPENINGS {
        bigint job_id PK
        varchar title
        varchar department
        varchar location
        text description
        text requirements
        bigint created_by
        timestamp created_at
        enum status
    }
    JOB_APPLICATIONS {
        bigint application_id PK
        bigint job_id FK
        bigint user_id
        varchar cv_file
        timestamp submitted_at
    }
```
