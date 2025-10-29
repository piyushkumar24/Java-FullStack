# 📘 Chapter 4: IRCTC Ticket Booking App — Low Level Design (LLD)

---

## 🌟 Overview
In this chapter, we will learn how to design the **Low-Level Design (LLD)** of an **IRCTC Ticket Booking Application** using **Java and OOP principles**.  
We’ll identify entities, their relationships, and how they interact — laying the foundation for a scalable backend system.  
Implementation details and advanced features will be explored in upcoming chapters.

---

## 🧭 Concept Map
```text
IRCTC Ticket Booking System
│
├── Entity Layer
│   ├── User
│   ├── Train
│   ├── Ticket
│
└── Service Layer
    ├── UserBookingService
    ├── TrainService
```


---

## 🧩 Entities and Attributes

### 👤 Entity: User
- **String name**  
- **String hashedPassword**  
- **String userId**  
- **List<Ticket> bookedTickets**  

> Represents a registered user who can book and cancel tickets.

---

### 🚂 Entity: Train
- **String trainId**  
- **String trainNumber**  
- **String source**  
- **String destination**
- **DateTime DepartTime**
- **DateTime ArrivalTime**   
- **List <List< Boolean>> Seats**  

> Represents a train with details about route and available seats.
> Tickets will be stored in a 2D Boolean matrix, where 0's will tell empty seats and 1's will tell occupied seats.

---

### 🎫 Entity: Ticket
- **String ticketId**  
- **String userId**
- **String source**
- **String destination**
- **DateTime dateOfTravel**
- **Train train**    

> Represents a ticket booked by a user for a specific train.

---

## ⚙️ Service Layer

### 🧠 UserBookingService
Handles ticket booking, cancellation, and displaying user bookings, user registration and authentication.  
- `registerUser(String name, String password, String email)`  
- `login(String email, String password)` 
- `bookTicket(User user, Train train, int seatCount)`  
- `cancelTicket(int ticketId)`  
- `fetchBookings(User user)`  

---

### 🚉 TrainService
Handles train management operations.  
- `addTrain(Train train)`  
- `getAvailableTrains(String source, String destination)`  
- `updateAvailability(Train train, int seats)`  

---


## 🔗 Relationships Between Entities
| Relationship | Description |
|---------------|-------------|
| **User → Ticket** | One user can have multiple tickets. |
| **Ticket → Train** | Each ticket is associated with one train. |
| **Train → Ticket** | One train can have multiple tickets booked. |

---

## 💡 Design Highlights
✅ Uses **Encapsulation** — all data protected inside classes.  
✅ Shows **Has-A relationships** using Composition (`User` has `Ticket`, `Ticket` has `Train`).  
✅ Uses **Service Layer abstraction** for modular logic.  
✅ Simple foundation for future extensions (payments, waitlist, etc.).

---


## 🧠 Interview Preparation Tips

### 💬 Possible Questions & Answers:

1. **Explain the LLD of your IRCTC app.**  
   → The system follows an *Entity-Service* architecture. Entities like `User`, `Train`, `Ticket`, and `Booking` represent data, while Service classes like `BookingService` and `PaymentService` handle business logic such as seat allocation and cancellation.

2. **How does composition differ from inheritance here?**  
   → Composition is used instead of inheritance — for example, a `User` *has a* list of `Ticket` objects rather than inheriting from them. This increases flexibility and reusability.

3. **Why use a Service Layer instead of directly coding logic in entities?**  
   → It separates **business logic** from **data representation**, promoting cleaner code, easier testing, and better scalability.

4. **How would you make this system multi-threaded for concurrent bookings?**  
   → Use **synchronized blocks** or **locks** to manage seat booking operations, ensuring only one thread updates train seat availability at a time.

5. **How would you persist data to a database (JDBC, Hibernate, etc.)?**  
   → Use JDBC for manual SQL handling or Hibernate ORM to map entities (`@Entity` classes) directly to tables and manage CRUD operations automatically.

6. **What are the key entities and their relationships?**  
   → Entities: `User`, `Train`, `Ticket`, `Booking`.  
     - `User` ↔ `Ticket` — One-to-Many  
     - `Train` ↔ `Ticket` — One-to-Many  
     - `Booking` combines both with additional details like payment and status.

7. **How would you ensure data consistency when multiple users book at once?**  
   → Use **transaction management** and **synchronized seat updates** to prevent double booking. Implement atomic operations at the service layer with rollback mechanisms.


---

## ⚠️ Common Mistakes
🚫 Mixing business logic inside entity classes.  
🚫 Forgetting to handle seat availability correctly.  
🚫 Skipping encapsulation (directly accessing class fields).  
🚫 Not modularizing design into service and entity layers.  
🚫 Ignoring validation or error handling in user input.

---

## 🧰 Tooling & IDE Integration
- **IntelliJ IDEA / VS Code:** Best suited for modular Java backend development.  
- **Java 17+ Recommended:** Supports modern syntax and strong typing.  
- **JUnit:** For testing service layer methods.  
- **GitHub README Preview:** Renders markdown code and diagrams neatly.  
- **Gradle / Maven:** For dependency management and build automation.

---

## 🧩 Advanced Notes
Can extend this project to include:
- 🚀 Dynamic pricing logic  
- 🪑 Waitlist management  
- 🔢 PNR generation and tracking  
- 💾 Database persistence (using JDBC / Hibernate ORM)  
- 🧱 Integration with REST APIs for frontend communication  

---

## 📘 Glossary

| **Term** | **Meaning** |
|-----------|-------------|
| **LLD (Low Level Design)** | Focuses on class structure, attributes, and method-level details for implementation. |
| **Encapsulation** | Bundling data and related methods inside a single class to protect internal state. |
| **Composition** | Represents a *“Has-A”* relationship between objects (e.g., `User` has `Ticket`). |
| **Service Layer** | Responsible for implementing business logic using entity classes. |
| **Entity** | A class representing a real-world object or concept with identifiable attributes (e.g., `User`, `Train`, `Ticket`). |
| **Functional Requirement** | A specific action or capability that the system must support (e.g., login, booking, cancellation). |
| **UUID** | Universally Unique Identifier used to assign unique IDs to entities. |
| **JDBC** | Java Database Connectivity — API for connecting and executing queries with databases. |
| **Hibernate** | ORM tool that maps Java objects to database tables for persistence. |

---

