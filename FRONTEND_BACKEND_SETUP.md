# Frontend Setup Guide - Backend Integration

## 📋 Prerequisites

- Node.js (v14 or higher)
- npm or yarn
- Backend server running on `http://localhost:5000`

## 🚀 Frontend Installation

### 1. Navigate to frontend folder

```bash
cd ../  # Go back from backend folder
# Or from root: cd Frontend/edssentials-app
```

### 2. Install dependencies (if not already installed)

```bash
npm install
```

### 3. Create `.env` file in frontend root

Create a `.env` file in the root of your frontend project:

```env
# Backend API URL
REACT_APP_API_URL=http://localhost:5000/api

# Environment
REACT_APP_ENV=development
```

### 4. Start the frontend development server

```bash
npm start
```

Frontend will run on `http://localhost:3000`

## 🔄 Frontend-Backend Communication

### How It Works

1. **API Service** (`src/services/api.js`)
   - Centralized API client using axios
   - Automatic JWT token handling
   - CORS-enabled for backend communication
   - Request/response interceptors

2. **Authentication Flow**
   - User logs in → Token stored in localStorage
   - Token automatically attached to all requests
   - If token expires, user redirected to login

3. **Data Storage**
   - `localStorage.getItem('token')` - JWT token
   - `localStorage.getItem('user')` - User data

### Using API in Components

```javascript
import { authAPI, learningPathAPI } from '../services/api';

// Login example
const handleLogin = async (email, password) => {
  try {
    const response = await authAPI.login({ email, password });
    const { token, user } = response.data.data;
    localStorage.setItem('token', token);
    localStorage.setItem('user', JSON.stringify(user));
  } catch (error) {
    console.error('Login failed:', error.message);
  }
};

// Get learning paths
const getPaths = async () => {
  try {
    const response = await learningPathAPI.getAllPaths();
    console.log(response.data.data);
  } catch (error) {
    console.error('Error fetching paths:', error.message);
  }
};
```

## 📡 Updated API Methods

### Authentication
- `authAPI.register(userData)` - Register new user
- `authAPI.login(credentials)` - Login user
- `authAPI.getProfile()` - Get current user profile
- `authAPI.updateProfile(data)` - Update user profile
- `authAPI.getAllUsers()` - Get all users (admin)

### Learning Paths
- `learningPathAPI.getAllPaths()` - Get all paths
- `learningPathAPI.getPathById(id)` - Get specific path
- `learningPathAPI.createPath(data)` - Create path
- `learningPathAPI.updatePath(id, data)` - Update path
- `learningPathAPI.deletePath(id)` - Delete path
- `learningPathAPI.enrollUser(id)` - Enroll in path

### Resources
- `resourceAPI.getAllResources(params)` - Get resources with filters
- `resourceAPI.getResourceById(id)` - Get specific resource
- `resourceAPI.createResource(data)` - Create resource
- `resourceAPI.saveResource(id)` - Save resource
- `resourceAPI.getUserSavedResources()` - Get saved resources

### Assessments
- `assessmentAPI.getAllAssessments()` - Get all assessments
- `assessmentAPI.getAssessmentById(id)` - Get assessment
- `assessmentAPI.createAssessment(data)` - Create assessment
- `assessmentAPI.submitAssessment(id, answers)` - Submit assessment
- `assessmentAPI.getUserResults()` - Get my results

### Jobs
- `jobAPI.getAllJobs()` - Get all job alerts
- `jobAPI.getJobById(id)` - Get job details
- `jobAPI.createJobAlert(data)` - Create job alert
- `jobAPI.saveJob(id)` - Save job
- `jobAPI.applyForJob(id)` - Apply for job
- `jobAPI.getUserSavedJobs()` - Get saved jobs

## ⚙️ Environment Configuration

The frontend automatically:
- ✅ Reads API URL from `.env` file
- ✅ Handles CORS requests
- ✅ Manages JWT authentication
- ✅ Redirects to login if token expires
- ✅ Formats error responses

## 🔍 Debugging

### Check Network Requests
1. Open Chrome DevTools (F12)
2. Go to Network tab
3. Look for API requests starting with `/api`
4. Check response status and data

### Common Issues

**Issue: CORS Error**
- ❌ Backend not running
- ❌ `FRONTEND_URL` not set correctly in backend `.env`
- ✅ Solution: Start backend and verify CORS config

**Issue: 401 Unauthorized**
- ❌ JWT token expired
- ❌ Token not being sent
- ✅ Solution: Clear localStorage and login again

**Issue: API not found**
- ❌ Backend URL incorrect in `.env`
- ❌ Backend route not created
- ✅ Solution: Verify `REACT_APP_API_URL` and backend routes

**Issue: Database connection failed**
- ❌ MongoDB not running
- ❌ `MONGODB_URI` incorrect
- ✅ Solution: Check MongoDB setup in backend

## 📊 Project Structure

```
Frontend/edssentials-app/
├── src/
│   ├── pages/
│   │   ├── Login.js         ✓ Updated to use backend API
│   │   ├── Register.js      ✓ Updated to use backend API
│   │   ├── Dashboard.js     - Can be updated for real data
│   │   ├── LearningPaths.js - Can be updated for real data
│   │   ├── Assessments.js   - Can be updated for real data
│   │   ├── JobAlerts.js     - Can be updated for real data
│   │   └── ...
│   ├── services/
│   │   └── api.js           ✓ New - Centralized API service
│   ├── components/
│   │   └── ...
│   └── ...
├── .env                      - Create this file
└── ...

Backend/
├── server.js                 - Entry point
├── config/
├── controllers/
├── models/
├── routes/
├── middleware/
├── utils/
├── package.json
├── .env                      - Already configured
└── README.md
```

## 🚀 Full Startup Procedure

### Terminal 1 - Backend
```bash
cd backend
npm run dev
# Output: 🚀 Server running on http://localhost:5000
```

### Terminal 2 - Frontend
```bash
npm start
# Output: Compiled successfully!
# Localhost: http://localhost:3000
```

### Browser
1. Navigate to `http://localhost:3000`
2. Go to Register page to create account
3. Or Login with demo credentials
4. Backend will handle authentication

## ✅ Verification Checklist

- [ ] Backend running on port 5000
- [ ] Frontend running on port 3000
- [ ] MongoDB connected
- [ ] `.env` files configured
- [ ] Can register new user
- [ ] Can login successfully
- [ ] Can view dashboard
- [ ] Network requests show `/api/` URLs
- [ ] No CORS errors in console
- [ ] Token stored in localStorage

## 📝 Next Steps

1. Update other pages (Dashboard, LearningPaths, etc.) to use real API data
2. Add error boundaries and loading states
3. Implement user profile page with API integration
4. Add file upload for resources
5. Create admin panel for content management

## 🆘 Troubleshooting

If you encounter any issues:

1. **Check logs** - Look at both backend and browser console
2. **Verify `.env`** - Ensure all variables are set
3. **Restart services** - Kill and restart both backend and frontend
4. **Clear cache** - Clear browser cache and localStorage
5. **Check ports** - Ensure ports 3000 and 5000 are available

## 📚 Additional Resources

- [Backend API Documentation](./backend/README.md)
- [Express.js Docs](https://expressjs.com/)
- [React Hooks](https://react.dev/reference/react)
- [MongoDB Documentation](https://docs.mongodb.com/)
- [Axios Documentation](https://axios-http.com/)
