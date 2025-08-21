# 🏗️ System Architecture

High-level overview of the Group Planner platform structure and data flow.

---

## System Overview

```
┌─────────────────────────────────────────────────────────────┐
│                    CLIENT LAYER                             │
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────┐  │
│  │  Dashboard  │  │ Group Pages │  │  Authentication     │  │
│  │   - Stats   │  │ - Calendar  │  │   - Login/Register  │  │
│  │   - Groups  │  │ - Events    │  │   - Profile Mgmt    │  │
│  └─────────────┘  └─────────────┘  └─────────────────────┘  │
│                                                             │
└─────────────────────────────────────────────────────────────┘
                                │
                       ┌────────▼────────┐
                       │   CONTEXT API   │
                       │ - User Context  │
                       │ - Group Context │
                       │ - Availability  │
                       └────────┬────────┘
                                │
                       ┌────────▼────────┐
                       │   API LAYER     │
                       │   (Axios)       │
                       │ - HTTP Client   │
                       │ - Error Handler │
                       └────────┬────────┘
                                │ REST API
═══════════════════════════════════════════════════════════════
                                │
                    ┌───────────▼───────────┐
                    │    BACKEND API        │
                    │                       │
┌─────────────┐     │  ┌─────────────────┐  │     ┌─────────────┐
│   POSTGRES  │◄────┤  │   CONTROLLERS   │  ├────►│   SWAGGER   │
│             │     │  │ - User          │  │     │     UI      │
│ - Users     │     │  │ - Group         │  │     │             │
│ - Groups    │     │  │ - Event         │  │     └─────────────┘
│ - Events    │     │  │ - Availability  │  │
│ - Members   │     │  └─────────────────┘  │
│ - Invites   │     │           │           │
└─────────────┘     │  ┌────────▼────────┐  │
                    │  │    SERVICES     │  │
                    │  │ - Business      │  │
                    │  │   Logic         │  │
                    │  │ - Validation    │  │
                    │  └────────┬────────┘  │
                    │           │           │
                    │  ┌────────▼────────┐  │
                    │  │  REPOSITORIES   │  │
                    │  │ - JPA/Hibernate │  │
                    │  │ - Query Methods │  │
                    │  └─────────────────┘  │
                    └───────────────────────┘
```

---

## Frontend Architecture (Next.js)

### **App Router Structure**
```
src/app/
├── (user)/dashboard/          # Protected user dashboard
├── auth/                      # Login/registration
├── group/[groupid]/          # Dynamic group pages
└── layout.tsx                # Root layout with providers
```

### **Context Providers**
- **UserContext** - Authentication state, user profile, availability
- **GroupManagementContext** - Group operations, member management  
- **AvailabilityContext** - Calendar state, date selection, sync logic

### **Component Structure**
```
src/components/
├── shared/                   # Reusable components
│   ├── Calendar.tsx         # Interactive availability calendar
│   └── Header.tsx           # Navigation header
├── home/                    # Dashboard components
│   ├── GroupsList.tsx       # Group management UI
│   └── UserProfile.tsx      # Profile and availability
└── group/                   # Group-specific components
    ├── GroupHeader.tsx      # Group info display
    └── GroupCalendar.tsx    # Group availability view
```

---

## Backend Architecture (Spring Boot)

### **Layered Architecture**
```
Controllers  →  Services  →  Repositories  →  Database
     ↓             ↓            ↓
   DTOs      Business Logic   JPA Entities
```

### **Core Entities & Relationships**
```
User ──────── owns ────────── Group
  │                            │
  │                         members
  │                            │
  └─── availability ───── Availability
  │
  └─── participates ────── Event
                            │
                         owner
```

### **API Design Patterns**
- **RESTful endpoints** with consistent resource hierarchy
- **DTO pattern** for clean API contracts
- **Global exception handling** for consistent error responses
- **Validation** with Jakarta Bean Validation

---

## Data Flow Examples

### **User Availability Update**
```
1. User clicks calendar date
2. AvailabilityContext updates local state
3. User clicks "Save Changes"  
4. API call: PUT /api/v1/availability/users/{id}
5. Backend validates & persists to database
6. Response updates UserContext
7. UI reflects new state across all components
```

### **Group Creation Flow**
```
1. User submits CreateGroup form
2. GroupManagementContext handles submission
3. API call: POST /api/v1/groups
4. Backend creates Group entity with user as owner
5. Response includes full GroupDTO
6. UserContext updates with new group
7. UI refreshes to show new group
```

---

## Key Technical Decisions

### **State Management**
- React Context API for centralized state
- Separation by domain (User, Groups, Availability)
- Local storage persistence for user sessions

### **Data Synchronization**
- REST API with DTOs for clean contracts
- Context providers handle API integration
- Optimistic updates where appropriate

### **Security Considerations**  
- Password handling on backend only
- UUID-based invitation tokens
- Public/Private DTO separation

---

## 🚀 Future Architecture Considerations

### **Phase 2 Enhancements**
- **Real-time updates** - WebSocket integration for live changes
- **Caching strategy** - Redis for session management
- **File uploads** - Image handling for events and profiles

### **Scalability Patterns**
- **Microservices** - Potential split by domain (User, Group, Event services)
- **Database optimization** - Indexing strategy for larger datasets  
- **CDN integration** - Static asset optimization

---
