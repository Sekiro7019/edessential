# 📊 ARCHITECTURE OVERVIEW

## System Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                    EDSSENTIALS FULL STACK                       │
└─────────────────────────────────────────────────────────────────┘

┌──────────────────────────────────┐
│     FRONTEND (React)             │
│  http://localhost:3000           │
├──────────────────────────────────┤
│ - Pages (Dashboard, Learning etc)│
│ - Components (UI elements)       │
│ - Services (api.js - API client) │ ← NEW
│ - State Management               │
└──────────────┬───────────────────┘
               │
      HTTP + JWT Token
      (Automatic attachment)
               │
        CORS Protected
               │
               ▼
┌──────────────────────────────────┐
│   BACKEND (Node.js + Express)    │
│   http://localhost:5000          │
├──────────────────────────────────┤
│ Routes (27 endpoints)            │
│   ├─ Auth (5 endpoints)          │
│   ├─ Learning Paths (6 endpoints)│
│   ├─ Resources (5 endpoints)     │
│   ├─ Assessments (5 endpoints)   │
│   └─ Jobs (6 endpoints)          │
│                                  │
│ Middleware                       │
│   ├─ JWT Authentication          │
│   └─ Error Handling              │
│                                  │
│ Controllers (Business Logic)     │
│   └─ 5 controllers for modules   │
│                                  │
│ Models (Schemas)                 │
│   ├─ User                        │
│   ├─ LearningPath                │
│   ├─ Assessment                  │
│   ├─ Resource                    │
│   └─ JobAlert                    │
└──────────────┬───────────────────┘
               │
        TCP/IP Connection
        Authentication
               │
               ▼
┌──────────────────────────────────┐
│    DATABASE (MongoDB)            │
│   Local or MongoDB Atlas         │
├──────────────────────────────────┤
│ Collections (5)                  │
│   - users                        │
│   - learningpaths                │
│   - assessments                  │
│   - resources                    │
│   - jobalerts                    │
│                                  │
│ Indexes for Performance          │
│ Relationships via References     │
└──────────────────────────────────┘
```

## Data Flow Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│              USER REGISTRATION & LOGIN FLOW                     │
└─────────────────────────────────────────────────────────────────┘

1. USER REGISTERS
   ┌──────────────┐
   │ React Form   │
   └──────┬───────┘
          │ Sends: firstName, lastName, email, password
          ▼
   ┌──────────────────────────┐
   │ POST /api/auth/register  │
   └──────┬───────────────────┘
          │ Express validates
          │ Password hashing
          ▼
   ┌──────────────────────────┐
   │ MongoDB - User Created   │
   └──────┬───────────────────┘
          │ Response: user + JWT token
          ▼
   ┌──────────────────────────┐
   │ React stores token       │
   │ in localStorage          │
   └──────┬───────────────────┘
          │ Redirect to Dashboard
          ▼
   ┌──────────────────────────┐
   │ Dashboard displays       │
   │ user information         │
   └──────────────────────────┘

2. USER LOGIN
   ┌──────────────┐
   │ React Form   │
   └──────┬───────┘
          │ Sends: email, password
          ▼
   ┌──────────────────────────┐
   │ POST /api/auth/login     │
   └──────┬───────────────────┘
          │ Find user in MongoDB
          │ Compare password
          ▼
   ┌──────────────────────────┐
   │ Generate JWT token       │
   │ Valid for 7 days         │
   └──────┬───────────────────┘
          │ Response: user + token
          ▼
   ┌──────────────────────────┐
   │ Store in localStorage    │
   │ Attach to all requests   │
   └──────────────────────────┘

3. ACCESSING PROTECTED RESOURCE
   ┌──────────────┐
   │ React calls: │
   │ getProfile() │
   └──────┬───────┘
          │
   ┌──────▼──────────────────────┐
   │ Axios Interceptor:          │
   │ Add Authorization header:   │
   │ "Bearer <token>"            │
   └──────┬───────────────────────┘
          │
   ┌──────▼──────────────────────┐
   │ Backend Middleware:         │
   │ Verify JWT token            │
   └──────┬───────────────────────┘
          │
   ┌──────▼──────────────────────┐
   │ If valid:                   │
   │ Execute controller          │
   │ Query MongoDB               │
   │ Return data                 │
   └──────┬───────────────────────┘
          │
   ┌──────▼──────────────────────┐
   │ React receives data         │
   │ Updates component state     │
   │ Renders to user             │
   └──────────────────────────────┘
```

## File Organization

```
FRONTEND
  edssentials-app/
  ├── src/
  │   ├── services/
  │   │   └── api.js ........................ API Client (CENTRALIZED)
  │   │       ├── authAPI
  │   │       ├── learningPathAPI
  │   │       ├── resourceAPI
  │   │       ├── assessmentAPI
  │   │       └── jobAPI
  │   ├── pages/
  │   │   ├── Login.js ..................... ✅ UPDATED
  │   │   ├── Register.js ................. ✅ UPDATED
  │   │   ├── Dashboard.js ................ Ready for integration
  │   │   ├── LearningPaths.js ............ Ready for integration
  │   │   └── ...
  │   └── components/
  │       └── ...
  │
  ├── public/
  ├── .env .............................. REACT_APP_API_URL
  ├── package.json
  └── ...

BACKEND (NEW)
  backend/
  ├── server.js ......................... Express server entry
  ├── package.json ..................... Dependencies
  ├── .env ............................. Config (MONGODB, JWT, etc)
  ├── README.md ........................ API documentation
  │
  ├── config/
  │   ├── database.js .................. MongoDB connection
  │   └── cors.js ..................... CORS configuration
  │
  ├── models/ (5 MongoDB schemas)
  │   ├── User.js
  │   ├── LearningPath.js
  │   ├── Assessment.js
  │   ├── Resource.js
  │   └── JobAlert.js
  │
  ├── controllers/ (5 business logic)
  │   ├── authController.js
  │   ├── learningPathController.js
  │   ├── resourceController.js
  │   ├── assessmentController.js
  │   └── jobController.js
  │
  ├── routes/ (5 API route files)
  │   ├── authRoutes.js
  │   ├── learningPathRoutes.js
  │   ├── resourceRoutes.js
  │   ├── assessmentRoutes.js
  │   └── jobRoutes.js
  │
  ├── middleware/
  │   ├── auth.js ..................... JWT verification
  │   └── errorHandler.js ............ Error handling
  │
  └── utils/
      ├── jwt.js ..................... Token utilities
      └── response.js .............. Response formatting

DOCUMENTATION (6 files)
  START_HERE.md ........................ Quick overview
  BACKEND_SETUP_COMPLETE.md ........... Complete guide
  BACKEND_INTEGRATION.md .............. Integration examples
  FRONTEND_BACKEND_SETUP.md ........... Setup guide
  FILES_CREATED.md ................... What was built
  backend/README.md .................. API reference
```

## Request/Response Cycle

```
1. FRONTEND REQUEST
   ┌─────────────────────────────────┐
   │ React Component                 │
   │ Calls: authAPI.login({...})     │
   └────────────┬────────────────────┘
                │
   ┌────────────▼────────────────────┐
   │ axios instance (api.js)         │
   │ - Set baseURL                   │
   │ - Add content-type              │
   └────────────┬────────────────────┘
                │
   ┌────────────▼────────────────────┐
   │ Request Interceptor             │
   │ - Get token from localStorage   │
   │ - Add Authorization header      │
   │ - "Bearer <token>"              │
   └────────────┬────────────────────┘
                │
   ┌────────────▼────────────────────┐
   │ HTTP Request sent to Backend    │
   │ POST http://localhost:5000/...  │
   └────────────┬────────────────────┘

2. BACKEND PROCESSING
                │
   ┌────────────▼────────────────────┐
   │ Express receives request        │
   └────────────┬────────────────────┘
                │
   ┌────────────▼────────────────────┐
   │ CORS Middleware                 │
   │ - Check origin                  │
   │ - Check methods                 │
   │ - Check headers                 │
   └────────────┬────────────────────┘
                │
   ┌────────────▼────────────────────┐
   │ Body Parser Middleware          │
   │ - Parse JSON body               │
   │ - Validate format               │
   └────────────┬────────────────────┘
                │
   ┌────────────▼────────────────────┐
   │ Router finds route match        │
   │ POST /api/auth/login            │
   └────────────┬────────────────────┘
                │
   ┌────────────▼────────────────────┐
   │ Auth Middleware (if protected)  │
   │ - Extract token from header     │
   │ - Verify JWT signature          │
   │ - Check expiration              │
   │ - Set req.userId                │
   └────────────┬────────────────────┘
                │
   ┌────────────▼────────────────────┐
   │ Controller executes             │
   │ - Validate input                │
   │ - Query database                │
   │ - Process logic                 │
   │ - Generate response             │
   └────────────┬────────────────────┘
                │
   ┌────────────▼────────────────────┐
   │ Format response using utility   │
   │ { success, message, data }      │
   └────────────┬────────────────────┘
                │
   ┌────────────▼────────────────────┐
   │ Error Handler (if error)        │
   │ - Catch exception               │
   │ - Format error response         │
   │ - Send proper status            │
   └────────────┬────────────────────┘

3. FRONTEND RECEIVES
                │
   ┌────────────▼────────────────────┐
   │ Response Interceptor            │
   │ - Check status                  │
   │ - Handle 401 logout             │
   │ - Return data                   │
   └────────────┬────────────────────┘
                │
   ┌────────────▼────────────────────┐
   │ Promise resolved/rejected       │
   │ .then(res => ...)               │
   │ .catch(err => ...)              │
   └────────────┬────────────────────┘
                │
   ┌────────────▼────────────────────┐
   │ Component updates state         │
   │ Component re-renders            │
   │ User sees result                │
   └─────────────────────────────────┘
```

## Technology Stack

```
Frontend Layer:
  - React.js (UI framework)
  - React Router (navigation)
  - Axios (HTTP client)
  - Framer Motion (animations)
  - React Icons (icons)

Backend Layer:
  - Node.js (runtime)
  - Express.js (server framework)
  - Mongoose (MongoDB ODM)
  - JWT (authentication)
  - bcryptjs (password hashing)

Database Layer:
  - MongoDB (document database)
  - Collections (user, paths, assessments, etc)
  - Indexes (performance)

Development Tools:
  - npm (package manager)
  - nodemon (auto-reload)
  - dotenv (configuration)

Communication:
  - RESTful API
  - JSON (data format)
  - HTTP/HTTPS (protocol)
  - CORS (cross-origin)
```

## Security Layers

```
1. TRANSPORT LAYER
   ├─ HTTPS/TLS (in production)
   └─ CORS protection

2. AUTHENTICATION LAYER
   ├─ JWT tokens (7-day expiration)
   ├─ Token storage (localStorage with caution)
   └─ Automatic logout on expiry

3. PASSWORD LAYER
   ├─ bcryptjs hashing (10 salt rounds)
   ├─ Never stored in plain text
   └─ Never returned in responses

4. AUTHORIZATION LAYER
   ├─ Protected routes with middleware
   ├─ Role-based access (student/mentor/admin)
   └─ Request validation

5. DATA VALIDATION LAYER
   ├─ Input validation (express-validator)
   ├─ Type checking (Mongoose schemas)
   └─ Business logic validation

6. ERROR HANDLING LAYER
   ├─ No sensitive info in errors
   ├─ Proper HTTP status codes
   └─ Error logging (ready for implementation)
```

## Scaling Considerations

```
Current Setup (Development):
  - Local MongoDB
  - Single Express server
  - Monolithic structure

Ready to Scale:
  ✓ Database indexing implemented
  ✓ Modular code structure
  ✓ Environment configuration
  ✓ Error handling in place
  ✓ Request validation ready

Future Scaling Options:
  - MongoDB Atlas (cloud)
  - Load balancing
  - Microservices
  - Caching layer (Redis)
  - API versioning
  - Rate limiting
  - Database replication
  - CI/CD pipeline
```

---

This architecture is:
✅ Modular - Easy to extend
✅ Secure - Multiple layers
✅ Scalable - Ready to grow
✅ Maintainable - Clear structure
✅ Production-ready - Best practices followed
