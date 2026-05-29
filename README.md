# 💳 Distributed Wallet Simulator (Core Java)

A self-contained, high-performance Core Java simulation of a digital wallet ecosystem. This project was built to demonstrate foundational backend engineering concepts, including **concurrency control**, **deadlock prevention**, **transaction management**, and **extensible architectural patterns**.

While this iteration runs entirely in-memory without external framework dependencies (like Spring or Hibernate), it is structurally designed to be easily adapted into a distributed microservice.

## ✨ Key Features & Technical Highlights

* **Thread-Safe Transactions & Deadlock Prevention:** * Implements account-to-account transfers using `ReentrantLock`.
* Avoids classic deadlocks during concurrent transfers by universally ordering lock acquisition (lexicographical sorting of wallet IDs).


* **Extensible Routing Architecture (Strategy Pattern):**
* **Payment Gateway Router:** Dynamically routes deposits to different payment providers (e.g., Stripe, Razorpay) without modifying core business logic.
* **Notification Router:** Supports multi-channel alerting (Email, SMS) using a pluggable channel architecture.


* **Domain-Driven Design (DDD):**
* Clear separation of concerns across `Controller`, `Service`, `Repository`, and `Domain` layers.


* **Financial Data Integrity:**
* Uses minor units (e.g., cents) for all financial calculations to prevent floating-point precision errors.
* Supports wallet lifecycle management (Active, Suspended, Closed).


* **Account Statements:** Generates time-bounded transaction histories filtered by UTC timestamps.

## 🏗️ Project Structure
```
├── controller/        # Entry points simulating REST/API handlers (Wallet, Transaction, Admin)
├── service/           # Core business logic, distributed lock interfaces, and external routers
│   ├── gateway/       # Payment provider abstractions and routing
│   └── notification/  # Notification channel abstractions
├── repository/        # Data access layer (Interfaces + In-Memory Implementations via ConcurrentHashMap)
├── domain/            # Core entities (User, Wallet, Transaction, Enums)
└── main/              # Application entry point & simulation runner
```

## 🚀 Getting Started

This project is built using standard Core Java and requires **no external dependencies** (no Maven, Gradle, or external databases required to run the simulation).

### Prerequisites

* Java Development Kit (JDK) 11 or higher installed.

### How to Run (Command Line)

1. Clone the repository and navigate to the root directory: 
```git clone https://github.com/bibhuprashad32/syncpay.git && cd syncpay```
2. Compile all Java files: 
```javac controller/*.java domain/*.java main/*.java repository/*.java repository/impl/*.java service/*.java service/gateway/*.java service/notification/*.java```
3. Execute the simulation: 
```java main.DigitalWalletSimulation```

### Expected Output

The simulation will automatically run through a standard user journey:

1. Creating users and wallets.
2. Initiating and completing a deposit via a mock payment gateway callback.
3. Performing a secure transfer between two users.
4. Initiating a withdrawal.
5. Generating an account statement.
6. Simulating admin actions (suspending an account and verifying transaction rejection).

## 🛣️ Roadmap to Production

This project serves as a foundational architecture. To adapt this into a production-ready system, the following infrastructure swaps are designed into the current abstractions:

* [ ] **Database Integration:** Swap `ConcurrentHashMap` repositories with a relational database (e.g., PostgreSQL) using JDBC/JPA. Implement ACID database transactions.
* [ ] **Distributed Locking:** Swap standard Java `ReentrantLock` in `LockService` with a Redis-based distributed lock (e.g., Redisson) to support multi-node deployment safely.
* [ ] **API Layer:** Wrap controllers in a web framework (Spring Boot, Javalin, or Quarkus) to expose real RESTful endpoints.
* [ ] **Real Integrations:** Implement actual API clients for the `PaymentGatewayProvider` (Stripe) and `NotificationChannel` (Twilio/SendGrid).

## 👨‍💻 Author

Built to showcase clean backend architecture and concurrency management in Java.
Feel free to reach out or open an issue if you'd like to discuss the architecture!
