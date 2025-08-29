# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:
  
<img width="1285" height="730" alt="Screenshot 2025-08-29 222837" src="https://github.com/user-attachments/assets/4148c141-aa91-4493-8feb-1599beeb0439" />

### Entity and Attributes

| Entity              | Attributes (PK, FK)                                                           | Notes                                          |
| ------------------- | ----------------------------------------------------------------------------- | ---------------------------------------------- |
| **Member**          | MemberID (PK), Name, MembershipType, StartDate, Phone, Email                  | Gym members                                    |
| **Program**         | ProgramID (PK), ProgramName, ProgramType (Yoga, Zumba, etc.), Schedule        | Fitness programs offered                       |
| **Trainer**         | TrainerID (PK), Name, Specialization, Phone, Email                            | Trainers at the gym                            |
| **Enrollment**      | EnrollmentID (PK), MemberID (FK), ProgramID (FK), EnrollmentDate              | Tracks which programs a member joins           |
| **TrainerProgram**  | TrainerID (FK), ProgramID (FK) (Composite PK)                                 | Many-to-Many between trainers and programs     |
| **PersonalSession** | SessionID (PK), MemberID (FK), TrainerID (FK), SessionDate, Duration          | 1-on-1 training sessions                       |
| **Attendance**      | AttendanceID (PK), SessionID (FK), Status (Present/Absent)                    | Tracks member attendance                       |
| **Payment**         | PaymentID (PK), MemberID (FK), PaymentType (Membership/Session), Amount, Date | Payments for memberships and personal sessions |


### Relationships and Constraints

| Relationship                 | Cardinality                                                                  | Participation | Notes                                        |
| ---------------------------- | ---------------------------------------------------------------------------- | ------------- | -------------------------------------------- |
| Member – Enrollment          | 1\:M (One member can join many programs)                                     | Partial       | A member may not join a program              |
| Program – Enrollment         | 1\:M (One program can have many enrolled members)                            | Total         | Every enrollment must be linked to a program |
| Trainer – TrainerProgram     | M\:N (Trainer can run multiple programs, program can have multiple trainers) | Total         | Resolved via **TrainerProgram**              |
| Member – PersonalSession     | 1\:M (A member can book multiple personal sessions)                          | Partial       | Some members may not book sessions           |
| Trainer – PersonalSession    | 1\:M (A trainer can conduct many sessions)                                   | Total         | Each session must have a trainer             |
| PersonalSession – Attendance | 1:1 or 1\:M (Each session has attendance records for the member)             | Total         | Tracks session participation                 |
| Member – Payment             | 1\:M (One member makes many payments)                                        | Total         | Each payment must be tied to a member        |


### Assumptions
Members register with name, membership type, and start date.
Each member can join multiple programs (Yoga, Zumba, Weight Training).
Trainers assigned to programs; a program may have multiple trainers.

# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:
  
<img width="1209" height="703" alt="image" src="https://github.com/user-attachments/assets/88bfb37c-37da-45e1-8543-c679df4fbe44" />


### Entities and Attributes

| Entity                | Attributes (PK, FK)                                                                | Notes                                         |
| --------------------- | ---------------------------------------------------------------------------------- | --------------------------------------------- |
| **Member**            | MemberID (PK), Name, Phone, Email, MembershipDate                                  | Library members                               |
| **Book**              | BookID (PK), Title, Author, Category, AvailabilityStatus                           | Books available in library                    |
| **Loan**              | LoanID (PK), MemberID (FK), BookID (FK), LoanDate, ReturnDate, DueDate, FineAmount | Tracks book borrow/return and fines           |
| **Event**             | EventID (PK), EventName, EventDate, RoomID (FK)                                    | Cultural/author events                        |
| **Speaker**           | SpeakerID (PK), Name, Specialization                                               | Authors/speakers in events                    |
| **Room**              | RoomID (PK), RoomName, Capacity, RoomType                                          | Rooms for events/study                        |
| **EventRegistration** | RegID (PK), MemberID (FK), EventID (FK), RegistrationDate                          | Members registering for events                |
| **EventSpeaker**      | EventID (FK), SpeakerID (FK) (Composite PK)                                        | M\:N relationship between events and speakers |


### Relationships and Constraints

| Relationship                   | Cardinality                                                                    | Participation | Notes                              |
| ------------------------------ | ------------------------------------------------------------------------------ | ------------- | ---------------------------------- |
| Member – Loan                  | 1\:M (One member can borrow many books)                                        | Total         | Each loan must belong to a member  |
| Book – Loan                    | 1\:M (One book can be borrowed many times)                                     | Partial       | A book may not always be on loan   |
| Member – EventRegistration     | 1\:M (One member can register for many events)                                 | Partial       | Not all members attend events      |
| Event – EventRegistration      | 1\:M (One event can have many registered members)                              | Total         | Events require members             |
| Event – Room                   | M:1 (Many events can take place in one room)                                   | Total         | Each event must be assigned a room |
| Event – Speaker (EventSpeaker) | M\:N (Many events can have many speakers, and speakers can attend many events) | Total         | Modeled via **EventSpeaker**       |


### Assumptions
Members borrow books, with loan and return dates tracked.  
Each book has title, author, and category.  
Library organizes events; members can register.

---

# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:
  
<img width="757" height="697" alt="image" src="https://github.com/user-attachments/assets/2b397a58-080f-4d41-bc13-8b38490672a4" />


### Entities and Attributes
| Entity          | Attributes (PK, FK)                                                       | Notes                                     |
| --------------- | ------------------------------------------------------------------------- | ----------------------------------------- |
| **Customer**    | CustomerID (PK), Name, Phone, Email                                       | Customers may reserve tables or walk in   |
| **Reservation** | ReservationID (PK), CustomerID (FK), Date, Time, NumGuests, WaiterID (FK) | Links to Customer; served by a waiter     |
| **Waiter**      | WaiterID (PK), Name, Phone                                                | Each reservation is assigned a waiter     |
| **Order**       | OrderID (PK), ReservationID (FK), OrderTime                               | Each reservation can have multiple orders |
| **OrderItem**   | OrderItemID (PK), OrderID (FK), DishID (FK), Quantity                     | Junction between Order and Dish           |
| **Dish**        | DishID (PK), Name, Price, CategoryID (FK)                                 | Menu items belong to categories           |
| **Category**    | CategoryID (PK), CategoryName                                             | Example: Starter, Main, Dessert           |
| **Bill**        | BillID (PK), ReservationID (FK), Amount, ServiceCharge, TotalAmount       | Generated per reservation                 |
### Relationships and Constraints
| Relationship           | Cardinality | Participation                                        | Notes                                                                      |
| ---------------------- | ----------- | ---------------------------------------------------- | -------------------------------------------------------------------------- |
| Customer – Reservation | 1 to M      | Partial (a customer may have 0 or many reservations) | Walk-in customers may not be stored unless they reserve                    |
| Reservation – Order    | 1 to M      | Total (every order must belong to a reservation)     |                                                                            |
| Order – OrderItem      | 1 to M      | Total                                                | OrderItem exists only if linked to an Order                                |
| OrderItem – Dish       | M to 1      | Total                                                | Each OrderItem refers to one Dish                                          |
| Dish – Category        | M to 1      | Total                                                | Every dish belongs to a category                                           |
| Reservation – Bill     | 1 to 1      | Total (each reservation generates one bill)          |                                                                            |
| Reservation – Waiter   | M to 1      | Total                                                | A waiter serves many reservations; each reservation has exactly one waiter |


## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
