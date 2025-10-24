# Plannex 📅 | Full-Stack Group Coordination Platform

![Spring Boot](https://img.shields.io/badge/Spring%20Boot-6DB33F?style=for-the-badge&logo=springboot&logoColor=white)
![Next.js](https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=nextdotjs&logoColor=white)
![Java](https://img.shields.io/badge/Java%2024-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-336791?style=for-the-badge&logo=postgresql&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)

> ⚠️ **Portfolio Showcase:** Demonstrates the architecture, documentation, and features of Plannex. Full source code is private but available upon request.

---

## 🚀 Live Demo

* **Frontend:** [https://plannex.vercel.app](url)
* **API Docs:** Available via Swagger UI on the live backend.

---

## 🔥 Project Overview

Plannex is a full-stack group coordination platform solving the common challenge: "When is everyone free?". It simplifies social planning through **personal availability tracking**, **group management**, and **intuitive event scheduling**.

Users mark unavailable dates on a personal calendar, which aggregates within groups to instantly show shared availability, enabling easy scheduling of spontaneous "Ping" events or planned activities. Built with Spring Boot 3.5.6 (Java 24) and Next.js 15 (TypeScript).

### Core Problem Solved:

Eliminates group chat polling. Users can:
1.  Create a group (e.g., "Weekend Hiking").
2.  Invite friends via secure link.
3.  View aggregated member unavailability.
4.  Create "Ping" events, auto-inviting *only* available members.
5.  Chat in real-time within event threads.

---

## Core Concepts Demonstrated

This project showcases modern full-stack development skills:

### **Backend (Spring Boot):**
* **API Design:** Clean RESTful API (`/api/v1/...`) with DTOs.
* **Security:** JWT auth (Access/Refresh tokens, `httpOnly` cookie), Spring Security 6, role-based auth, `@PreAuthorize` with custom `SecurityService`.
* **Data Persistence:** JPA/Hibernate, PostgreSQL, `@EntityGraph` for N+1 prevention, efficient relationship management.
* **Architecture:** Layered (Controller/Service/Repository), global exception handling, Jakarta Bean Validation.
* **Testing:** Comprehensive suite (Unit/Integration/Controller) using Mockito, `@DataJpaTest`, `@SpringBootTest`, MockMvc, custom `@WithMockCustomUser`. **~95% coverage**.

### **Frontend (Next.js):**
* **Modern React:** Next.js 15 App Router, React Server Components.
* **Type Safety:** 100% TypeScript coverage.
* **State Management:** Centralized React Context (Auth, Groups, Availability, Events).
* **UI/UX:** Responsive, mobile-first design with Tailwind CSS.
* **API Integration:** Robust async data fetching (Axios) with error handling.

### **DevOps & Tooling:**
* **Containerization:** `Dockerfile` & `docker-compose` for backend & DB.
* **CI/CD:** Automated build/test pipeline via GitHub Actions.
* **Documentation:** API docs via Swagger/OpenAPI.

---

## 🚀 Features Implemented

### 👤 **User Management**
* Secure Registration (BCrypt) & JWT Authentication (Access/Refresh tokens, `httpOnly` cookie).
* Automatic token refresh flow.
* Profile editing (username, email, password).
* Personal availability calendar management.

### 👥 **Group Coordination**
* Group creation/management with ownership.
* Secure, expiring UUID-based invitation links.
* Role-based permissions (creator vs. member).
* Join/Leave functionality (creator cannot leave).
* Aggregated member availability view.

### 📅 **Availability System**
* Mark personal unavailability (with date validation: no past dates, 365-day limit, format check).
* Group-level availability overlay.
* Efficient backend aggregation via JPA.

### 🎉 **Event Planning (Ping Events)**
* Create time-limited "Ping" events for spontaneous hangouts.
* **Smart Invites:** Auto-invite only available members (optional override). Initiator auto-accepted.
* **RSVP:** Accept/Decline (validation prevents changes after expiration). Real-time count tracking.
* **Status Logic:** `AWAITING` → `COMPLETED` (≥2 accepted) / `EXPIRED` (<2 accepted).
* **Messaging:** Real-time event chat (accepted members only), history with timestamp filtering.

### 🔒 **Security Features**
* JWT authentication with secure token rotation.
* `@PreAuthorize` method security using custom `SecurityService` expressions (`isGroupMember`, `isCreator`, `isMemberOfEventsGroup`, `isAcceptedEventMember`).
* Input validation (DTOs & Service layer).
* Consistent HTTP error responses.

---

## 🏗️ Architecture

Backend uses a **3-layer architecture** (Controller → Service → Repository). Frontend employs Next.js 15 App Router with React Context.

*(See [`docs/architecture.md`](docs/architecture.md) for detailed diagrams and data flows.)*

### **Key Design Patterns:**
* DTO Pattern, Repository Pattern, Service Layer, Security Service, Global Exception Handling.

---

## 🛠️ Tech Stack

### **Backend (Spring Boot)**
* **Framework:** Spring Boot 3.5.6 (Java 24)
* **Security:** Spring Security 6 with JWT
* **Data:** Spring Data JPA (Hibernate 6)
* **Database:** PostgreSQL 16
* **Testing:** JUnit 5, Mockito 5, H2
* **Build:** Maven 3.9
* **Containerization:** Docker / Docker Compose
* **Docs:** SpringDoc OpenAPI 3

### **Frontend (Next.js)**
* **Framework:** Next.js 15 (App Router)
* **Language:** TypeScript 5
* **Styling:** Tailwind CSS 3
* **State:** React Context API
* **HTTP:** Axios
* **Date:** date-fns

---

## 📊 Test Coverage

* **Comprehensive Layers:** Controller (`@SpringBootTest`), Service (Mockito), Repository (`@DataJpaTest`), Exception Handler tests.
* **Custom Utilities:** `@WithMockCustomUser` for security context simulation.
* **Stats:** 20+ Test Classes, 200+ Test Methods, **~95% coverage** of critical logic.
* **DB:** H2 in-memory for fast test execution.

---

## 🔐 Security Implementation

* **Auth Flow:** Login → Validate (BCrypt) → Issue JWT Access (15min) & Refresh (7day, `httpOnly` cookie) → Client uses Access Token → Refresh via `/auth/refresh` on expiry.
* **Authorization:** Method-level via `@PreAuthorize("@security...")`.

```java
// Example Authorization
@PreAuthorize("@security.isGroupMember(#groupId, principal)")
public ResponseEntity<GroupInfoDTO> getGroupById(@PathVariable Long groupId) { /*...*/ }
````

-----

## 📁 Project Structure

```
plannex/
├── src/main/java/.../plannex/ # Main source code (config, controller, entity, etc.)
├── src/test/java/.../plannex/ # Test code (controllerTests, serviceTests, etc.)
├── docs/                      # Architecture, Decisions, Ideas, Progress docs
├── docker-compose.yml         # DB container setup
├── Dockerfile                 # Backend container build instructions
└── pom.xml                    # Maven project config
```

-----

## 🚦 For Recruiters & Reviewers

This repository showcases a production-oriented development approach. Review the `/docs` folder for deeper insights:

  * [`docs/architecture.md`](https://www.google.com/search?q=docs/architecture.md): System design & data flow.
  * [`docs/decisions.md`](https://www.google.com/search?q=docs/decisions.md): ADRs explaining tech choices.
  * [`docs/idea.md`](https://www.google.com/search?q=docs/idea.md): Product backlog & roadmap.
  * [`docs/progress.md`](https://www.google.com/search?q=docs/progress.md): Development log.

### **Key Highlights:**

1.  **Security:** Robust JWT flow & method-level authorization.
2.  **Testing:** Extensive coverage & custom test utilities.
3.  **Database:** Efficient JPA design & query optimization.
4.  **API:** Clean REST principles & error handling.
5.  **Code Quality:** Organized, readable, maintainable.

**Full source code access and code walkthrough available upon request.**

-----

## 🎯 What Makes This Project Stand Out

  * **Production-Ready:** Scalable architecture, comprehensive testing, security best practices.
  * **Real-World Solution:** Addresses a common coordination problem effectively.
  * **Clean Code & Docs:** Demonstrates maintainability and professional practices.
  * **Modern Tech Stack:** Utilizes current industry standards (Java 24, Spring Boot 3.5, Next.js 15).

-----

## 📞 Contact

For questions, source code access, or walkthroughs:

  * **GitHub:** [https://github.com/nathanbatchelor](https://www.google.com/search?q=url)
  * **LinkedIn:** [https://linkedin.com/in/nathanbatchelor](https://www.google.com/search?q=url)
  * **Email:** nathanbatchelor04@gmail.com

-----

*Last Updated: October 2025*
