# 🚀 Backend API Integration Guide

This guide explains the complete backend setup and integration with the frontend.

## ⏱️ Complete Setup (10 minutes)

### Prerequisites
- ✅ Node.js v14+
- ✅ MongoDB or MongoDB Atlas account
- ✅ Terminal/Command Prompt

---

## 📦 Backend Installation & Setup

### Step 1: Install Backend Dependencies
```bash
cd backend
npm install
```

### Step 2: Configure Environment Variables
Backend `.env` file is already created at `backend/.env`

Update if needed:
```env
MONGODB_URI=mongodb://localhost:27017/edssentials
PORT=5000
NODE_ENV=development
JWT_SECRET=your_jwt_secret_key_change_this_in_production
JWT_EXPIRE=7d
FRONTEND_URL=http://localhost:3000
```

### Step 3: Start Backend Server
```bash
npm run dev
```

Expected output:
```
✓ MongoDB Connected: localhost
🚀 Server running on http://localhost:5000
📝 Environment: development
```

---

## 🎯 Frontend Environment Setup

### Step 1: Create Frontend `.env` File
Create `.env` in frontend root directory:
```env
REACT_APP_API_URL=http://localhost:5000/api
REACT_APP_ENV=development
```

### Step 2: Install Frontend Dependencies (if needed)
```bash
npm install
```

### Step 3: Start Frontend
```bash
npm start
```

Expected output:
```
Compiled successfully!
Localhost: http://localhost:3000
```

---

## 🔗 API Service Integration

### Updated Files
- `src/services/api.js` - ✓ NEW Centralized API client
- `src/pages/Login.js` - ✓ UPDATED to use backend
- `src/pages/Register.js` - ✓ UPDATED to use backend

### How It Works

1. **API Client** (`src/services/api.js`)
   - Axios instance with baseURL
   - Automatic JWT token attachment
   - Request/response interceptors
   - Error handling

2. **Authentication Flow**
   ```
   User Registration → Backend creates user + returns token
   → Token stored in localStorage
   → Token attached to all future requests
   ```

3. **Protected Routes**
   - All protected endpoints require valid JWT
   - Automatic token verification
   - Redirect to login if unauthorized

---

## 📡 Available API Methods

### Authentication
```javascript
import { authAPI } from '../services/api';

// Register
authAPI.register({
  firstName: 'John',
  lastName: 'Doe',
  email: 'john@example.com',
  password: 'password123'
})

// Login
authAPI.login({
  email: 'john@example.com',
  password: 'password123'
})

// Get Profile (requires token)
authAPI.getProfile()

// Update Profile
authAPI.updateProfile({
  firstName: 'Jane',
  bio: 'Learning developer',
  skills: ['React', 'Node.js']
})
```

### Learning Paths
```javascript
import { learningPathAPI } from '../services/api';

learningPathAPI.getAllPaths()
learningPathAPI.getPathById(id)
learningPathAPI.createPath(data)  // requires auth
learningPathAPI.updatePath(id, data)  // requires auth
learningPathAPI.deletePath(id)  // requires auth
learningPathAPI.enrollUser(id)  // requires auth
```

### Resources
```javascript
import { resourceAPI } from '../services/api';

resourceAPI.getAllResources({ category: 'web', type: 'video' })
resourceAPI.getResourceById(id)
resourceAPI.createResource(data)  // requires auth
resourceAPI.saveResource(id)  // requires auth
resourceAPI.getUserSavedResources()  // requires auth
```

### Assessments
```javascript
import { assessmentAPI } from '../services/api';

assessmentAPI.getAllAssessments()
assessmentAPI.getAssessmentById(id)
assessmentAPI.createAssessment(data)  // requires auth
assessmentAPI.submitAssessment(id, answers)  // requires auth
assessmentAPI.getUserResults()  // requires auth
```

### Jobs
```javascript
import { jobAPI } from '../services/api';

jobAPI.getAllJobs()
jobAPI.getJobById(id)
jobAPI.createJobAlert(data)  // requires auth
jobAPI.saveJob(id)  // requires auth
jobAPI.applyForJob(id)  // requires auth
jobAPI.getUserSavedJobs()  // requires auth
```

---

## 🧪 Testing the API

### Using Postman or Insomnia

1. **Test Health Check**
   ```
   GET http://localhost:5000/api/health
   
   Response:
   { "success": true, "message": "Backend is running" }
   ```

2. **Register New User**
   ```
   POST http://localhost:5000/api/auth/register
   Content-Type: application/json
   
   {
     "firstName": "John",
     "lastName": "Doe",
     "email": "john@example.com",
     "password": "password123",
     "role": "student"
   }
   ```

3. **Login**
   ```
   POST http://localhost:5000/api/auth/login
   
   {
     "email": "john@example.com",
     "password": "password123"
   }
   
   Response includes JWT token
   ```

4. **Use Token for Protected Routes**
   ```
   GET http://localhost:5000/api/auth/profile
   Authorization: Bearer {token_from_login}
   ```

---

## 🗄️ Database Collections

### Users
```javascript
{
  _id: ObjectId,
  firstName: String,
  lastName: String,
  email: String (unique),
  password: String (hashed),
  role: 'student' | 'mentor' | 'admin',
  profileImage: String,
  bio: String,
  skills: [String],
  learningPaths: [ObjectId],
  completedAssessments: [ObjectId],
  isActive: Boolean,
  createdAt: Date,
  updatedAt: Date
}
```

### Learning Paths
```javascript
{
  _id: ObjectId,
  title: String,
  description: String,
  category: String,
  difficulty: 'beginner' | 'intermediate' | 'advanced',
  duration: String,
  instructor: ObjectId,
  modules: [{title, description, content, resources}],
  enrolledUsers: [ObjectId],
  image: String,
  rating: Number,
  isPublished: Boolean,
  createdAt: Date
}
```

### Assessments
```javascript
{
  _id: ObjectId,
  title: String,
  learningPath: ObjectId,
  questions: [{
    questionText: String,
    type: 'multiple-choice' | 'short-answer' | 'essay',
    options: [String],
    correctAnswer: String,
    points: Number
  }],
  totalPoints: Number,
  createdBy: ObjectId,
  submissions: [{
    userId: ObjectId,
    answers: [String],
    score: Number,
    submittedAt: Date
  }]
}
```

### Resources
```javascript
{
  _id: ObjectId,
  title: String,
  description: String,
  type: 'video' | 'article' | 'book' | 'tutorial' | 'tool' | 'other',
  category: String,
  url: String,
  author: String,
  difficulty: 'beginner' | 'intermediate' | 'advanced',
  tags: [String],
  savedBy: [ObjectId],
  rating: Number,
  uploadedBy: ObjectId,
  createdAt: Date
}
```

### Job Alerts
```javascript
{
  _id: ObjectId,
  title: String,
  company: String,
  location: String,
  jobType: 'full-time' | 'part-time' | 'contract' | 'internship',
  salary: String,
  skills: [String],
  url: String,
  savedBy: [ObjectId],
  appliedBy: [{userId: ObjectId, appliedAt: Date}],
  createdAt: Date
}
```

---

## ⚡ Common Integration Patterns

### Pattern 1: Fetch Data on Component Mount
```javascript
import { useEffect, useState } from 'react';
import { learningPathAPI } from '../services/api';

function LearningPaths() {
  const [paths, setPaths] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchPaths = async () => {
      try {
        const response = await learningPathAPI.getAllPaths();
        setPaths(response.data.data);
      } catch (err) {
        setError(err.message);
      } finally {
        setLoading(false);
      }
    };

    fetchPaths();
  }, []);

  if (loading) return <div>Loading...</div>;
  if (error) return <div>Error: {error}</div>;
  
  return (
    <div>
      {paths.map(path => (
        <div key={path._id}>{path.title}</div>
      ))}
    </div>
  );
}

export default LearningPaths;
```

### Pattern 2: Handle Form Submission
```javascript
const handleSubmit = async (e) => {
  e.preventDefault();
  setLoading(true);

  try {
    const response = await resourceAPI.createResource({
      title: formData.title,
      description: formData.description,
      type: formData.type,
      url: formData.url
    });
    
    console.log('Resource created:', response.data.data);
    // Show success message
  } catch (error) {
    console.error('Error:', error.response?.data?.message);
    // Show error message
  } finally {
    setLoading(false);
  }
};
```

### Pattern 3: Protected Route Check
```javascript
import { useEffect } from 'react';
import { useNavigate } from 'react-router-dom';

function ProtectedPage() {
  const navigate = useNavigate();

  useEffect(() => {
    const token = localStorage.getItem('token');
    if (!token) {
      navigate('/login');
    }
  }, [navigate]);

  // Component code...
}
```

---

## 🔐 Security Features

### JWT Authentication
- Tokens stored in localStorage
- Automatically attached to requests
- 7-day expiration
- Automatic logout on expiration

### Password Security
- Bcryptjs hashing (10 salt rounds)
- Never stored in plain text
- Not returned in API responses

### CORS Protection
- Whitelist origin (frontend URL)
- Credentials allowed
- Specific allowed methods

### Input Validation
- Email format validation
- Password length validation
- Express validator middleware

---

## 🆘 Troubleshooting

| Issue | Solution |
|-------|----------|
| **CORS Error** | Restart backend, check FRONTEND_URL in .env |
| **401 Unauthorized** | Token expired, login again |
| **MongoDB connection failed** | Check MongoDB running, verify MONGODB_URI |
| **Port 5000 in use** | Change PORT in .env or kill process |
| **API returns 404** | Check endpoint URL and method |
| **Cannot register** | Check email unique, password ≥ 6 chars |

---

## 📚 Documentation References

- `backend/README.md` - Complete backend documentation
- `FRONTEND_BACKEND_SETUP.md` - Full setup guide
- Backend API endpoint examples throughout this file

---

## ✅ Verification Checklist

- [ ] MongoDB running
- [ ] Backend installed (`npm install`)
- [ ] Backend `.env` configured
- [ ] Backend started (`npm run dev`)
- [ ] Frontend `.env` created
- [ ] Frontend installed
- [ ] Frontend started (`npm start`)
- [ ] Can register new user
- [ ] Token stored in localStorage
- [ ] Can login successfully
- [ ] Dashboard loads user data

---

## 🎉 You're Ready!

Backend and Frontend are now fully integrated:
- ✅ Smooth data flow
- ✅ Secure authentication
- ✅ Easy to extend
- ✅ Production-ready

Start building features! 🚀
