# PDS
PDS subject of 4th course on Software Engineering in UDC
```mermaid
erDiagram
    SPORTS_CENTER {
        int id PK
        string name
        string address
        string phone
        boolean isHeadquarters
    }

    USER {
        int id PK
        string firstName
        string lastName
        string email
        string password
        string phone
        date registrationDate
        int registeredCenterId FK
        int membershipTypeId FK
    }

    MEMBERSHIP_TYPE {
        int id PK
        string name
        decimal price
        boolean includesClasses
        boolean includesPhysiotherapy
        int freePhysiotherapySessions
    }

    PAYMENT {
        int id PK
        int userId FK
        int membershipTypeId FK
        datetime paymentDate
        decimal amount
        string paymentMethod
    }

    ACCESS {
        int id PK
        int userId FK
        int sportsCenterId FK
        datetime accessTime
        string accessMethod
    }

    BOOKING {
        int id PK
        int userId FK
        int classId FK
        int roomId FK
        int physiotherapySessionId FK
        datetime startTime
        datetime endTime
        string status
    }

    CLASS {
        int id PK
        string name
        int instructorId FK
        int sportsCenterId FK
        int roomId FK
        int maxCapacity
        datetime classTime
        int duration
    }

    ROOM {
        int id PK
        string name
        int sportsCenterId FK
        int maxCapacity
    }

    STAFF {
        int id PK
        string firstName
        string lastName
        string email
        string phone
        int sportsCenterId FK
        string role
    }

    ADMINISTRATOR {
        int id PK
    }

    MAINTENANCE_WORKER {
        int id PK
        string shift
    }

    PHYSIOTHERAPIST {
        int id PK
        string certification
    }

    INSTRUCTOR {
        int id PK
        string specialty
        boolean canRotateCenters
    }

    PHYSIOTHERAPY_SESSION {
        int id PK
        int physiotherapistId FK
        int sportsCenterId FK
        datetime sessionTime
        decimal cost
    }

    OCCUPANCY_REPORT {
        int id PK
        int roomId FK
        date reportDate
        float occupancyRate
    }

    USER }|--|| SPORTS_CENTER : registers_at
    USER ||--o{ ACCESS : can_enter
    USER }|--|| MEMBERSHIP_TYPE : has
    USER ||--o{ PAYMENT : makes
    USER ||--o{ BOOKING : makes

    STAFF ||--|{ INSTRUCTOR : is_a
    STAFF ||--|{ PHYSIOTHERAPIST : is_a
    STAFF ||--|{ ADMINISTRATOR : is_a
    STAFF ||--|{ MAINTENANCE_WORKER : is_a

    INSTRUCTOR ||--o{ CLASS : teaches
    CLASS ||--|| ROOM : takes_place_in
    CLASS ||--o{ BOOKING : requires

    PHYSIOTHERAPIST ||--o{ PHYSIOTHERAPY_SESSION : provides
    PHYSIOTHERAPY_SESSION ||--o{ BOOKING : requires

    ADMINISTRATOR ||--o{ CLASS : manages

    ROOM ||--o{ OCCUPANCY_REPORT : generates
    ROOM ||--o{ BOOKING : requires

    MEMBERSHIP_TYPE ||--o{ PAYMENT : changes_monthly
    MEMBERSHIP_TYPE }|--|| PHYSIOTHERAPY_SESSION : defines_price

    PAYMENT }|--|| MEMBERSHIP_TYPE : corresponds_to

```
