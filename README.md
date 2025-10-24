# Plannex 📅 | Full-Stack Group Coordination Platform

![Spring Boot](https://img.shields.io/badge/Spring%20Boot-6DB33F?style=for-the-badge&logo=springboot&logoColor=white)
![Next.js](https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=nextdotjs&logoColor=white)
![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=java&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-336791?style=for-the-badge&logo=postgresql&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)

> ⚠️ **Portfolio Showcase:** This repository demonstrates the architecture, documentation, and feature set of the Plannex platform. The full source code is private but is available upon request for review.

---

## 🚀 Live Demo

* **Frontend Application:** `https://plannex.vercel.app` (Coming Soon)
* **Backend API Documentation:** Available via Swagger UI (running on the live backend)

---

## 🔥 Project Overview

Plannex is a full-stack group coordination platform designed to solve the simple but universal problem of "When is everyone free?". It streamlines social planning by combining **personal availability tracking**, **smart group management**, and **intuitive event planning** into one seamless application.

Users can mark their unavailable dates on a personal calendar. This data is then aggregated within their groups, allowing any member to instantly see "availability gaps" and find the perfect time to schedule an event.

The system is built on a modern, decoupled architecture with a **Spring Boot 3 (Java 24)** backend API and a **Next.js 15 (TypeScript)** frontend.

### Core Problem Solved:

Instead of polling multiple people in a group chat, a user can simply:
1.  Create a group (e.g., "Weekend Hiking").
2.  Invite friends via a unique link.
3.  Instantly see a visual overlay of *all members'* unavailable dates.
4.  Create a "Ping" event for a spontaneous hangout, inviting only those who are marked as "available" today.

---

## Core Concepts Demonstrated

This project serves as a practical demonstration of modern full-stack development principles:

* **Backend:**
    * **RESTful API Design:** Clean, resource-oriented API with clear DTOs (`/api/v1/...`).
    * **Security:** Token-based authentication (JWT) with secure `httpOnly` refresh token cookies. Role-based authorization using Spring Security 6 and `@PreAuthorize` annotations.
    * **Data Persistence:** JPA/Hibernate for ORM, featuring custom `@Query` and `@EntityGraph` definitions for optimized data fetching (solving N+1 problems).
    * **Database Management:** PostgreSQL for relational data storage, managed with `docker-compose` for a consistent development environment.
    * **Architecture:** Clean, layered architecture (Controller, Service, Repository) with separation of concerns.
    * **Testing:** Comprehensive test suite including Unit Tests (Mockito), Integration Tests (`@DataJpaTest`), and Controller Tests (`@WebMvcTest`/`@SpringBootTest`).

* **Frontend:**
    * **Modern React:** Built with Next.js 15 App Router and React Server Components.
    * **Type Safety:** 100% TypeScript coverage, from API client functions to UI components.
    * **State Management:** Centralized, domain-driven state using React Context (for Auth, Groups, etc.), minimizing prop-drilling.
    * **UI/UX:** Responsive, mobile-first design using Tailwind CSS.
    * **API Integration:** Robust async data fetching with a dedicated API client layer.

* **DevOps:**
    * **Containerization:** Fully containerized backend with `Dockerfile` and `docker-compose` for production and development.
    * **CI/CD:** Automated build and test pipeline using GitHub Actions.

---

## 🚀 Features Implemented (MVP)

### 👤 User Management
* Secure user registration (BCrypt hashing) and authentication (JWT).
* Access and Refresh token implementation with `httpOnly` cookie storage.
* Personal profile management (edit username, email, password).

### 👥 Group Coordination
* Create, view, and manage groups.
* Secure, token-based group invitation system (UUID tokens).
* Member management (owner permissions, leave group functionality).

### 📅 Availability System
* Personal availability calendar to mark unavailable dates.
* Group-level availability view showing an aggregated overlay of all members' unavailable dates.
* Efficient backend aggregation of member availability.

### 🎉 Event Planning (Ping Events)
* Create "Ping" events within groups for spontaneous hangouts (e.g., "Who is free in the next 3 hours?").
* **Smart Invites:** Automatically filter and invite *only* group members who are marked as "available" on the current day.
* RSVP system (Accept/Decline) for ping events.
* Real-time event chat/message board per event.

---

## 🏗️ Architecture

The backend follows a classic **3-layer architecture** (Controller, Service, Repository). The frontend is built with Next.js 15, utilizing the App Router and React Context for state management.

*(See the `docs/architecture.md` file for a detailed breakdown and diagrams.)*

---

## 🛠️ Tech Stack

### **Backend (Spring Boot)**
* **Framework:** Spring Boot 3.5.4 (Java 24)
* **Security:** Spring Security 6
* **Data:** Spring Data JPA (Hibernate)
* **Database:** PostgreSQL
* **Auth:** JSON Web Tokens (JWT)
* **Build:** Maven
* **Containerization:** Docker / Docker Compose

### **Frontend (Next.js)**
* **Framework:** Next.js 15 (App Router)
* **Language:** TypeScript
* **Styling:** Tailwind CSS
* **State Management:** React Context API

---

## 🚦 For Recruiters & Reviewers

This repository is designed to showcase my approach to building a complete, production-ready application. As the source code is private, I encourage you to review the documentation in the `/docs` folder:

* **[`docs/architecture.md`](docs/architecture.md):** High-level diagrams and data flow explanations.
* **[`docs/decisions.md`](docs/decisions.md):** Architectural Decision Records (ADRs) explaining *why* certain technologies were chosen.
* **[`docs/idea.md`](docs/idea.md):** The product backlog and future roadmap for the platform.
* **[`docs/progress.md`](docs/progress.md):** A high-level development log.

**I am happy to provide access to the private source code and do a full code walkthrough upon request.**
