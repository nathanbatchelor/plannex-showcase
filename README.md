# Group Planner 📅

A full-stack group coordination platform that helps friends, families, and teams plan activities by combining personal availability, group calendars, and event planning tools.

## 🌟 Overview

Group Planner makes it easy to coordinate with your people - whether you're planning spontaneous hangouts or organizing big events. The platform combines personal availability tracking, group calendars, and event management in one seamless experience.

### Current Status: MVP Development Phase
This showcase demonstrates the core functionality of the platform, including user management, group coordination, availability tracking, and basic event planning.

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

## 🛠️ Tech Stack

### Backend
- **Java 21** with Spring Boot 3.5.4
- **PostgreSQL** for data persistence
- **Spring Data JPA** for database operations
- **Maven** for dependency management
- **OpenAPI/Swagger** for API documentation

### Frontend
- **Next.js 15** with App Router
- **React 19** with TypeScript
- **Tailwind CSS** for styling
- **Axios** for API communication
- **Lucide React** for icons

## 🚦 Getting Started

### Prerequisites
- Java 21+
- Node.js 18+
- PostgreSQL 12+
- Maven 3.6+

### Backend Setup
1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd group-planner/backend
   ```

2. **Configure Database**
   ```properties
   # src/main/resources/application.properties
   spring.datasource.url=jdbc:postgresql://localhost:5432/groupplanner
   spring.datasource.username=your_username
   spring.datasource.password=your_password
   ```

3. **Run the Application**
   ```bash
   mvn spring-boot:run
   ```
   
   The API will be available at `http://localhost:8080`
   Swagger UI: `http://localhost:8080/swagger-ui.html`

### Frontend Setup
1. **Install Dependencies**
   ```bash
   cd group-planner/frontend
   npm install
   ```

2. **Configure Environment**
   ```bash
   # .env.local
   NEXT_PUBLIC_API_URL=http://localhost:8080/api/v1
   ```

3. **Run Development Server**
   ```bash
   npm run dev
   ```
   
   The application will be available at `http://localhost:3001`

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

## 🧪 Testing

### Backend Testing
```bash
mvn test
```

### Frontend Testing
```bash
npm run test  # When tests are added
npm run lint  # ESLint checks
```

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

## 🔗 Links

- **Live Demo**: Coming Soon
- **API Documentation**: Available at `/swagger-ui.html` when running locally
- **Project Repository**: [GitHub Link]

---

**Built with ❤️ using Spring Boot & Next.js**

*This project showcases modern full-stack development practices, clean architecture, and user-centered design.*
