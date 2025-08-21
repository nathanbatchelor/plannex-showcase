# Group Planner 📅

A **full-stack group coordination platform** built with Spring Boot and Next.js, featuring real-time availability tracking, smart group management, and seamless event planning.

![Spring Boot](https://img.shields.io/badge/Spring%20Boot-6DB33F?style=for-the-badge&logo=springboot&logoColor=white)
![Next.js](https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=nextdotjs&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-336791?style=for-the-badge&logo=postgresql&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=java&logoColor=white)

> ⚠️ This is a **portfolio showcase repo**. Code is **not fully public** and currently in **MVP development**. Reach out for access or walkthroughs.

## 🔥 Project Overview

This system streamlines group coordination by combining **personal availability tracking**, **smart group management**, and **intuitive event planning**. The platform makes it effortless to see when your group is free, plan events, and coordinate activities - whether it's spontaneous hangouts or major celebrations.

**Portfolio Project Note:** *Currently in MVP development phase - This showcase demonstrates core full-stack development capabilities including RESTful API design, React state management, real-time data synchronization, and responsive UI design.*

## 🚀 Features Implemented (MVP)

### 👤 User Management
- User registration and authentication
- Personal profile management
- Secure password handling

### 👥 Group Coordination
- Create and manage groups
- Join/leave group functionality
- Group invitation system with UUID tokens
- Member management with owner permissions

### 📅 Availability System
- Personal availability calendar
- Mark unavailable dates with intuitive UI
- Group availability visualization
- Real-time availability overlays

### 🎉 Event Planning
- Create events within groups
- Date range validation
- Event ownership and participation
- Group-based event organization

### 🔧 Technical Features
- RESTful API design
- Responsive React UI with Tailwind CSS
- Real-time data synchronization
- Comprehensive error handling
- Type-safe TypeScript implementation

## 🏗️ Architecture

### Backend (Spring Boot)
```
src/main/java/io/github/nathanbatchelor/groupplanner/
├── controller/          # REST API endpoints
├── service/            # Business logic layer
├── repository/         # Data access layer
├── entity/            # JPA entities
├── model/             # DTOs and request models
└── exception/         # Global error handling
```

### Frontend (Next.js 15)
```
src/
├── app/               # App Router pages
├── components/        # Reusable UI components
├── context/          # React Context providers
├── api/              # API client functions
├── types/            # TypeScript definitions
└── lib/              # Utility functions
```

## 🛠️ Technology Stack & Architecture

### **Backend Excellence**
- **Spring Boot 3.5.4** with Java 21 for robust server-side architecture
- **PostgreSQL** with JPA/Hibernate for reliable data persistence
- **RESTful API Design** with comprehensive error handling and validation
- **Maven** for dependency management and build automation

### **Frontend Innovation**  
- **Next.js 15** with App Router for modern React development
- **TypeScript** for type-safe development and better maintainability
- **Tailwind CSS** for responsive, utility-first styling
- **React Context** for sophisticated state management

### **Key Technical Features**
- **Clean Architecture** - Proper separation of concerns across all layers
- **Type Safety** - Full TypeScript coverage from API to UI components  
- **Real-time Sync** - Seamless data flow between frontend and backend
- **Responsive Design** - Mobile-first approach with modern UX patterns

## 🚦 Getting Started

**Note:** This is a portfolio showcase repository. The full source code is available upon request for qualified opportunities.

### Live Demo
- **Frontend Preview**: [Coming Soon]
- **API Documentation**: Available at `/swagger-ui.html` when running locally

### For Recruiters/Interviewers
If you'd like to see the full implementation or discuss the technical details, please feel free to reach out. I'd be happy to walk through:
- Architecture decisions and trade-offs
- Code structure and organization  
- Database design and relationships
- Frontend state management patterns
- API design principles

## 📋 API Endpoints

### Core Endpoints
```
Users:
  POST   /api/v1/users              # Create user
  GET    /api/v1/users/{id}         # Get user profile
  POST   /api/v1/users/login        # User authentication

Groups:
  POST   /api/v1/groups             # Create group
  GET    /api/v1/groups/{id}        # Get group details
  POST   /api/v1/groups/{id}/members/{userId}    # Join group
  DELETE /api/v1/groups/{id}/members/{userId}    # Leave group

Events:
  POST   /api/v1/events             # Create event
  GET    /api/v1/events/{id}        # Get event details
  GET    /api/v1/events/groups/{id} # Get group events

Availability:
  PUT    /api/v1/availability/users/{id}         # Update user availability
  DELETE /api/v1/availability/users/{id}         # Clear user availability
```

## 🎯 Roadmap & Future Features

### Phase 2: Enhanced Planning
- [ ] Complete event planning suite (budget, location, tasks)
- [ ] Ping events for spontaneous hangouts
- [ ] Built-in chat and messaging
- [ ] Photo sharing and albums

### Phase 3: Social & Intelligence
- [ ] Friends network and DMs
- [ ] AI hangout suggestions
- [ ] Advanced analytics and insights
- [ ] Achievement system and leaderboards

### Phase 4: Advanced Features
- [ ] Smart calendar screenshot parsing
- [ ] Weather integration
- [ ] Advanced payment splitting
- [ ] Custom group nicknames and social personas

## 🧪 Current Development Status

**MVP Phase Complete Features:**
- ✅ User authentication and profile management
- ✅ Group creation and member management  
- ✅ Real-time availability calendar
- ✅ Basic event planning and coordination
- ✅ Responsive UI with modern design
- ✅ RESTful API with comprehensive error handling

**Coming in Phase 2:**
- 🔄 Enhanced event planning suite
- 🔄 Spontaneous "ping" events
- 🔄 In-app messaging system
- 🔄 Photo sharing capabilities

## 📊 Key Design Decisions

### Backend Architecture
- **Clean Architecture**: Separation of concerns with distinct layers
- **DTO Pattern**: Separate public and private user data representations
- **Global Exception Handling**: Consistent error responses across all endpoints
- **JPA Relationships**: Proper entity relationships with cascade operations

### Frontend Architecture
- **Context API**: Centralized state management for user, groups, and availability
- **Component Composition**: Reusable components with clear responsibilities
- **Type Safety**: Full TypeScript coverage for better development experience
- **Responsive Design**: Mobile-first approach with Tailwind CSS

### Data Flow
```
Frontend Components → Context Providers → API Layer → Backend Controllers → Services → Repositories → Database
```

## 🐛 Known Limitations (MVP)

- Authentication is basic (no JWT/OAuth implementation)
- No real-time notifications
- Limited event management features
- Basic error handling on frontend
- No comprehensive testing suite
- PostgreSQL configuration hardcoded

## 📈 Performance Considerations

- **Database Indexes**: Strategic indexing on frequently queried fields
- **Lazy Loading**: JPA lazy loading for entity relationships
- **API Efficiency**: DTOs prevent over-fetching of data
- **Frontend Optimization**: Context providers minimize unnecessary re-renders

### Code Quality
- Comprehensive documentation in code
- Consistent naming conventions
- Separation of concerns
- Error handling throughout the stack

## 📝 License

This project is not open source. Codebase available upon request.
---

**Built with ❤️ using Spring Boot & Next.js**

*This project showcases modern full-stack development practices, clean architecture, and user-centered design.*
