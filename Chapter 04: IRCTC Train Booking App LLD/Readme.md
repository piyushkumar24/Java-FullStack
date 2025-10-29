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

