# ✈️ Airline Management System (Microservices Backend)

## 📌 Project Overview

This repository acts as the **central documentation hub** for the Airline Management System backend.  

It does not contain service code. Instead, it provides:

- System architecture explanation  
- Design decisions  
- Request lifecycle overview  
- Links to all individual microservice repositories  

The system is built using a **Microservices Architecture** with a focus on scalability, modularity, and clean backend design principles.

Currently, the APIs are tested using **Postman** (no frontend integrated yet).

---

## 🏗️ System Architecture

The project follows a **Microservices + API Gateway pattern** where:

- The **API Gateway** is the only publicly exposed service.
- All other services remain internal.
- Communication between services is secure and controlled.
- Asynchronous operations are handled via **RabbitMQ**.

### Core Architectural Concepts Used:

- API Gateway Pattern  
- Service Isolation  
- JWT-based Authentication  
- Asynchronous Messaging (Message Queue)  
- Clear Internal vs External Service Boundaries  

Only the API Gateway is accessible to the client.

---

## 🔁 Request Lifecycle (High-Level Flow)

1. Client (Postman) sends signup/login request to **Auth Service**
2. Auth Service returns a **JWT token**
3. Client sends protected requests to **API Gateway** with JWT
4. API Gateway:
   - Verifies token
   - Applies rate limiting
   - Routes request to appropriate service (Booking / Flight Search)
5. Booking Service:
   - Executes core booking logic
   - Communicates internally with Flight Service, Auth Service, and Reminder Service
6. Internal services respond back through Booking Service

⚠️ Internal microservices are never directly exposed to clients.

---

## 🚪 API Gateway

The API Gateway acts as the controlled entry layer of the system.

### Responsibilities:

- Central request routing  
- JWT validation  
- Authorization enforcement  
- Rate limiting  
- Blocking direct access to internal services  

Currently, it routes traffic to:

- Booking Service  
- Flight & Search Service  

🔗 Repository:  
https://github.com/ujzzzwall/Airline_API_Gateway

---

## 🧩 Microservices Breakdown

### 🔐 Auth Service

Handles user authentication and identity management.

**Responsibilities:**
- User registration  
- Login  
- JWT token generation  
- Stateless authentication  

🔗 Repository:  
https://github.com/ujzzzwall/Auth_Service

---

### 📦 Booking Service

Acts as the main business logic orchestrator.

**Responsibilities:**
- Flight booking workflow  
- Seat reservation logic  
- Booking status handling  
- Communication with Flight Service  
- Event publishing to Reminder Service via RabbitMQ  

🔗 Repository:  
https://github.com/ujzzzwall/FlightsAirTicketBookingService

---

### ✈️ Flight & Search Service

Manages flight data and search capabilities.

**Responsibilities:**
- Flight creation and management  
- Seat availability tracking  
- Flight search with filters  
- Internal service communication  

This service is internal-only and not publicly exposed.

🔗 Repository:  
https://github.com/ujzzzwall/FLigthsAndSearchService

---

### 🔔 Reminder / Notification Service

Handles asynchronous notifications and scheduled tasks.

**Responsibilities:**
- Booking confirmation emails  
- Flight notifications 
- Message queue consumption (RabbitMQ)  

This service operates independently using event-driven architecture.

🔗 Repository:  
https://github.com/ujzzzwall/REMINDER_SERVICE

---

## 🛠️ Tech Stack

- **Node.js**
- **Express.js**
- **MySQL**
- **Sequelize ORM**
- **JWT Authentication**
- **RabbitMQ**
- **Postman (API Testing)**

---

## 🔒 Security & Design Considerations

- JWT-based stateless authentication  
- Authorization enforced at API Gateway  
- Internal services hidden from public access  
- Strict separation of responsibilities  
- Rate limiting implemented at Gateway level  

---

## 🚀 Current Implementation Status

- Core backend services completed  
- API Gateway routing functional  
- Internal service communication established  
- Message queue integration implemented  
- Tested using Postman  
- No frontend integration yet  

---

## ▶️ Running the Project (High-Level Steps)

1. Clone each microservice repository  
2. Configure environment variables for each service  
3. Start services in order:
   - Auth Service  
   - API Gateway  
   - Booking Service  
   - Flight & Search Service  
   - Reminder Service  
4. Use Postman to test APIs  

---

## 👤 Author

**Ujjwal Singh**  

Backend Developer | 

---

## 📝 Final Note

This project focuses entirely on backend system design and microservice communication patterns.  
It demonstrates real-world architecture practices including gateway routing, service isolation, authentication handling, and event-driven workflows.
