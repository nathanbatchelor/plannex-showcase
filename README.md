# Plannex 📅 | Full-Stack Group Coordination Platform

![Spring Boot](https://img.shields.io/badge/Spring%20Boot-6DB33F?style=for-the-badge&logo=springboot&logoColor=white)
![Next.js](https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=nextdotjs&logoColor=white)
![Java](https://img.shields.io/badge/Java%2024-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-336791?style=for-the-badge&logo=postgresql&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)

> ⚠️ **Portfolio Showcase:** This repository demonstrates the architecture, documentation, and feature set of the Plannex platform. The full source code is private but is available upon request for review.

---

## 🚀 Live Demo

* **Frontend Application:** [https://plannex.vercel.app](url)
* **Backend API Documentation:** Available via Swagger UI (running on the live backend)

---

## 🔥 Project Overview

Plannex is a full-stack group coordination platform designed to solve the simple but universal problem of "When is everyone free?". It streamlines social planning by combining **personal availability tracking**, **smart group management**, and **intuitive event planning** into one seamless application.

Users can mark their unavailable dates on a personal calendar. This data is then aggregated within their groups, allowing any member to instantly see "availability gaps" and find the perfect time to schedule an event.

The system is built on a modern, decoupled architecture with a **Spring Boot 3.5.6 (Java 24)** backend API and a **Next.js 15 (TypeScript)** frontend.

### Core Problem Solved:

Instead of polling multiple people in a group chat, a user can simply:
1.  Create a group (e.g., "Weekend Hiking").
2.  Invite friends via a unique, secure link.
3.  Instantly see a visual overlay of *all members'* unavailable dates.
4.  Create a "Ping" event for a spontaneous hangout, inviting only those who are marked as "available" today.
5.  Chat with accepted participants in real-time event threads.

---

## Core Concepts Demonstrated

This project serves as a practical demonstration of modern full-stack development principles:

### **Backend Excellence:**
* **RESTful API Design:** Clean, resource-oriented API with comprehensive DTOs (`/api/v1/...`).
* **Security Architecture:** 
    - JWT-based authentication with secure `httpOnly` refresh token cookies
    - Role-based authorization using Spring Security 6
    - Custom `@PreAuthorize` expressions with dedicated `SecurityService`
    - Protection against common vulnerabilities (XSS, CSRF)
* **Data Persistence:** 
    - JPA/Hibernate ORM with optimized queries
    - Custom `@EntityGraph` definitions for N+1 problem prevention
    - Efficient many-to-many relationship management
    - PostgreSQL with proper indexing strategy
* **Architecture:** 
    - Clean, layered architecture (Controller → Service → Repository)
    - DTO pattern for API contract separation
    - Global exception handling with consistent error responses
    - Comprehensive Jakarta Bean Validation
* **Testing Strategy:**
    - **Unit Tests** - Mockito for service layer logic isolation
    - **Integration Tests** - `@DataJpaTest` for repository validation
    - **Controller Tests** - `@SpringBootTest` with MockMvc for full API testing
    - **Custom Test Utilities** - `@WithMockCustomUser` for security context testing
    - **95%+ code coverage** across critical business logic

### **Frontend Excellence:**
* **Modern React:** Built with Next.js 15 App Router and React Server Components.
* **Type Safety:** 100% TypeScript coverage, from API client functions to UI components.
* **State Management:** Centralized, domain-driven state using React Context (for Auth, Groups, Availability, Events), minimizing prop-drilling.
* **UI/UX:** Responsive, mobile-first design using Tailwind CSS with consistent design system.
* **API Integration:** Robust async data fetching with a dedicated API client layer and proper error handling.

### **DevOps & Tooling:**
* **Containerization:** Fully containerized backend with `Dockerfile` and `docker-compose` for consistent development environments.
* **CI/CD:** Automated build and test pipeline using GitHub Actions.
* **Database Management:** Docker Compose setup for PostgreSQL with proper volume management.
* **Documentation:** Comprehensive API documentation via Swagger/OpenAPI.

---

## 🚀 Features Implemented (Current Version)

### 👤 **User Management**
* Secure user registration with BCrypt password hashing
* JWT-based authentication with dual-token system:
    - Short-lived access tokens for API requests
    - Long-lived refresh tokens stored in `httpOnly` cookies
* Automatic token refresh flow
* Personal profile management (edit username, email, password)
* Availability calendar management with date validation

### 👥 **Group Coordination**
* Create, view, and manage groups with proper ownership tracking
* Secure, UUID-based group invitation system with expiration
* Role-based permissions (creator vs. member)
* Member management with join/leave functionality
* Creator-specific protections (cannot leave own group)
* Real-time member availability aggregation

### 📅 **Availability System**
* Personal availability calendar with date range selection
* Business logic validation:
    - Prevents setting availability for past dates
    - Limits on maximum unavailable dates (365 day cap)
    - Date format validation
* Group-level availability view showing aggregated member unavailability
* Efficient backend aggregation using JPA queries
* Smart filtering for "Ping" event invitations

### 🎉 **Event Planning (Ping Events)**
* Create time-limited "Ping" events within groups for spontaneous hangouts
* **Smart Invitation System:**
    - Automatically filters and invites *only* available members
    - Option to include/exclude unavailable members
    - Initiator automatically marked as "accepted"
* **RSVP Management:**
    - Accept/Decline functionality with validation
    - Prevents RSVP changes after event expiration
    - Real-time acceptance count tracking
* **Event Status Logic:**
    - `AWAITING` - Event is active and accepting responses
    - `COMPLETED` - Event expired with ≥2 accepted members
    - `EXPIRED` - Event expired with <2 accepted members
* **Event Messaging:**
    - Real-time chat/message board per event
    - Only accepted members can send messages
    - Message history with timestamp filtering
    - Efficient polling for new messages

### 🔒 **Security Features**
* JWT authentication with secure token rotation
* `@PreAuthorize` method-level security with custom expressions
* Custom `SecurityService` for reusable authorization checks:
    - `isGroupMember(groupId, user)` - Verify group membership
    - `isCreator(groupId, user)` - Verify group ownership
    - `isMemberOfEventsGroup(eventId, user)` - Verify event access
    - `isAcceptedEventMember(eventId, user)` - Verify RSVP status
* Input validation at DTO and service layers
* Proper error handling with informative HTTP status codes
* Protection against common attack vectors

---

## 🏗️ Architecture

The backend follows a classic **3-layer architecture** (Controller → Service → Repository) with additional separation for security and DTOs. The frontend is built with Next.js 15, utilizing the App Router and React Context for state management.

### **Backend Layer Breakdown:**

```
┌─────────────────────────────────────────┐
│          Controllers (REST API)         │
│  - Request handling & validation        │
│  - DTO mapping                          │
│  - Security annotations                 │
└──────────────┬──────────────────────────┘
               ↓
┌──────────────────────────────────────────┐
│            Services (Business Logic)     │
│  - Authorization checks                  │
│  - Complex business rules                │
│  - Transaction management                │
└──────────────┬───────────────────────────┘
               ↓
┌──────────────────────────────────────────┐
│         Repositories (Data Access)       │
│  - JPA/Hibernate queries                 │
│  - Custom @Query methods                 │
│  - @EntityGraph optimizations            │
└──────────────┬───────────────────────────┘
               ↓
         ┌──────────┐
         │PostgreSQL│
         └──────────┘
```

### **Key Design Patterns:**
* **DTO Pattern** - Separation between entities and API contracts
* **Repository Pattern** - Abstraction over data access
* **Service Layer** - Business logic encapsulation
* **Security Service** - Centralized authorization logic
* **Global Exception Handling** - Consistent error responses

*(See the `docs/architecture.md` file for detailed diagrams and data flows.)*

---

## 🛠️ Tech Stack

### **Backend (Spring Boot)**
* **Framework:** Spring Boot 3.5.6 (Java 24)
* **Security:** Spring Security 6 with JWT
* **Data:** Spring Data JPA (Hibernate 6)
* **Database:** PostgreSQL 16
* **Auth:** JSON Web Tokens (jjwt 0.11.5)
* **Testing:** JUnit 5, Mockito 5, H2 (test DB)
* **Build:** Maven 3.9
* **Containerization:** Docker / Docker Compose
* **Documentation:** SpringDoc OpenAPI 3

### **Frontend (Next.js)**
* **Framework:** Next.js 15 (App Router)
* **Language:** TypeScript 5
* **Styling:** Tailwind CSS 3
* **State Management:** React Context API
* **HTTP Client:** Axios
* **Date Handling:** date-fns

---

## 📊 Test Coverage

The project maintains comprehensive test coverage across all layers:

### **Backend Testing:**
* **Controller Tests** (`@SpringBootTest`, `@AutoConfigureMockMvc`)
    - Full integration tests with security context
    - Custom `@WithMockCustomUser` annotation for auth testing
    - Tests for all endpoints (success + error cases)
* **Service Tests** (`@ExtendWith(MockitoExtension.class)`)
    - Unit tests with mocked dependencies
    - Business logic validation
    - Edge case handling
* **Repository Tests** (`@DataJpaTest`)
    - JPA query validation
    - Custom query method testing
    - Entity relationship verification
* **Exception Handler Tests**
    - Global error handling validation
    - Proper HTTP status code verification
    - Error message consistency

### **Test Statistics:**
* **Total Test Classes:** 20+
* **Total Test Methods:** 200+
* **Coverage:** ~95% of critical business logic
* **Test Database:** H2 in-memory for fast execution

---

## 🔐 Security Implementation

### **Authentication Flow:**
1. User logs in with email/password
2. Backend validates credentials against BCrypt hash
3. Server generates:
    - Access token (JWT, 15-minute expiration)
    - Refresh token (JWT, 7-day expiration)
4. Access token returned in response body
5. Refresh token set as `httpOnly` cookie (prevents XSS)
6. Client includes access token in `Authorization: Bearer <token>` header
7. On access token expiration:
    - Client calls `/api/v1/auth/refresh`
    - Backend validates refresh token from cookie
    - New access token issued

### **Authorization Pattern:**
```java
@PreAuthorize("@security.isGroupMember(#groupId, principal)")
public ResponseEntity<GroupInfoDTO> getGroupById(@PathVariable Long groupId) {
    // Only group members can access this endpoint
}
```

---

## 📁 Project Structure

```
plannex/
├── src/main/java/.../plannex/
│   ├── config/                 # Security, JWT, CORS, Jackson config
│   ├── controller/             # REST API endpoints
│   ├── entity/                 # JPA entities
│   ├── exception/              # Global exception handlers
│   ├── model/                  # DTOs (Request/Response)
│   ├── repository/             # Data access layer
│   └── service/                # Business logic layer
├── src/test/java/.../plannex/
│   ├── controllerTests/        # API endpoint tests
│   ├── serviceTests/           # Business logic tests
│   ├── repositoryTests/        # Data layer tests
│   └── exceptionTests/         # Error handling tests
├── docs/
│   ├── architecture.md         # System design documentation
│   ├── decisions.md            # Architectural Decision Records
│   ├── idea.md                 # Feature backlog
│   └── progress.md             # Development log
├── docker-compose.yml          # PostgreSQL container setup
├── Dockerfile                  # Backend containerization
└── pom.xml                     # Maven dependencies
```

---

## 🚦 For Recruiters & Reviewers

This repository is designed to showcase my approach to building a complete, production-ready application. As the source code is private, I encourage you to review the documentation in the `/docs` folder:

* **[`docs/architecture.md`](docs/architecture.md):** High-level diagrams and data flow explanations.
* **[`docs/decisions.md`](docs/decisions.md):** Architectural Decision Records (ADRs) explaining *why* certain technologies were chosen.
* **[`docs/idea.md`](docs/idea.md):** The product backlog and future roadmap for the platform.
* **[`docs/progress.md`](docs/progress.md):** A high-level development log.

### **Key Highlights to Review:**

1. **Security Implementation** - JWT with refresh tokens, method-level authorization
2. **Test Coverage** - Comprehensive test suite with custom testing utilities
3. **Database Design** - Efficient JPA relationships with query optimization
4. **API Design** - Clean REST principles with proper HTTP semantics
5. **Error Handling** - Consistent, informative error responses
6. **Code Organization** - Clear separation of concerns, easy to navigate

**I am happy to provide access to the private source code and do a full code walkthrough upon request.**

---

## 🎯 What Makes This Project Stand Out

* **Production-Ready Architecture** - Not just a toy project, built with scalability and maintainability in mind
* **Comprehensive Testing** - 200+ tests covering edge cases and integration scenarios
* **Security Best Practices** - Proper JWT implementation, method-level authorization, input validation
* **Real-World Problem Solving** - Addresses a genuine coordination challenge with smart features
* **Clean Code** - Consistent naming, proper abstractions, readable and maintainable
* **Professional Documentation** - Architecture decisions recorded, progress tracked, code well-commented

---

## 📞 Contact

For questions, source code access, or to schedule a code walkthrough, please reach out via:
* **GitHub:** [https://github.com/nathanbatchelor](url)
* **LinkedIn:** [https://linkedin.com/in/nathanbatchelor](url)
* **Email:** nathanbatchelor04@gmail.com

---

*Last Updated: October 2025*
