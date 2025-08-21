# 📌 Architectural Decisions

Records major design choices and reasoning. Only add entries when something meaningful changes.

---

## ADR 001 – Full-Stack Technology Selection
**Date:** July 2025  
**Status:** Accepted  

### Context
Needed to choose technology stack for a modern group coordination platform that could handle real-time data and scale well.

### Decision
- **Backend:** Spring Boot 3.5.4 with Java 21
- **Frontend:** Next.js 15 with TypeScript
- **Database:** PostgreSQL with JPA/Hibernate
- **Styling:** Tailwind CSS

### Consequences
- ✅ Modern, industry-standard stack
- ✅ Strong typing throughout (Java + TypeScript)
- ✅ Excellent ecosystem and community support
- ✅ Good performance and scalability potential
- ⚠️ Learning curve for Next.js 15 App Router (newer paradigm)

---

## ADR 002 – State Management with React Context
**Date:** August 2025  
**Status:** Accepted  

### Context
Needed centralized state management for user data, groups, and availability across the application.

### Decision
Chose **React Context API** over Redux/Zustand for MVP phase.

### Consequences
- ✅ Simpler setup, no external dependencies
- ✅ Perfect for MVP scale and team size
- ✅ Direct integration with Next.js App Router
- ✅ Easier to understand and maintain
- ⚠️ May need migration to more robust solution if app complexity grows
- ⚠️ Re-render optimization requires careful context splitting

---

## ADR 003 – API Design Pattern
**Date:** August 2025  
**Status:** Accepted  

### Context
Needed consistent API structure that could handle complex relationships (users, groups, events) while being easy to consume.

### Decision
- **RESTful endpoints** with clear resource hierarchy
- **DTO pattern** for clean separation between entities and API responses
- **Global exception handling** for consistent error responses
- **Comprehensive validation** with Jakarta Validation

### Consequences
- ✅ Clean, predictable API surface
- ✅ Frontend can easily consume and cache responses
- ✅ Good separation between internal models and external contracts
- ✅ Consistent error handling across all endpoints
- 📝 Note: Working well for MVP, scalable for future features

---

## ADR 004 – Database Relationship Strategy
**Date:** July 2025  
**Status:** Accepted  

### Context
Complex many-to-many relationships between users, groups, and events with additional metadata requirements.

### Decision
- **JPA entities** with proper cascade operations
- **Join tables** for many-to-many relationships
- **Lazy loading** for performance
- **UUID tokens** for invitation system

### Consequences
- ✅ Clean database design with proper normalization
- ✅ JPA handles complex queries automatically
- ✅ Good performance with lazy loading
- ✅ Secure invitation system with UUID tokens
- ⚠️ Future consideration: May need EventAttendance entity for RSVP status

---

## ADR 005 – Repository Visibility Strategy
**Date:** August 2025  
**Status:** Accepted  

### Context
Want to showcase full-stack development skills while protecting intellectual property during MVP phase.

### Decision
- **Public repository** for portfolio visibility
- **Comprehensive README** showcasing architecture and features
- **Documentation structure** showing professional practices
- **Source code available** upon request for qualified opportunities

### Consequences
- ✅ Professional portfolio presence
- ✅ Demonstrates documentation and organization skills
- ✅ Protects work while showing capabilities
- ✅ Creates engagement opportunities with recruiters
- 📝 Note: Can open-source later if desired

---

## 📝 ADR Template
```
## ADR XXX – [Decision Title]
**Date:** [Date]  
**Status:** [Proposed/Accepted/Deprecated/Superseded]  

### Context
[What situation led to this decision?]

### Decision
[What was decided?]

### Consequences
[What are the positive and negative outcomes?]
- ✅ [Positive consequence]
- ⚠️ [Negative consequence or trade-off]
- 📝 [Neutral note or future consideration]
```
