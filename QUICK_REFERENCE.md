# ⚡ QUICK REFERENCE GUIDE

## 🚀 Start Your Application (30 Seconds)

### Terminal 1: Backend
```bash
cd backend
npm install
npm run dev
```

### Terminal 2: Frontend  
```bash
npm start
```

### Result
✅ Backend: http://localhost:5000
✅ Frontend: http://localhost:3000
✅ MongoDB: Running

---

## 📱 Test Registration/Login

1. Go to http://localhost:3000
2. Click "Sign Up"
3. Fill form:
   ```
   First Name: John
   Last Name: Doe
   Email: john@test.com
   Password: password123
   ```
4. Click "Create Account"
5. ✅ Account created in MongoDB
6. ✅ Auto-login and see dashboard

---

## 🔗 API Endpoints Quick Reference

### Auth Endpoints
```
POST   /api/auth/register        - Create account
POST   /api/auth/login           - Login
GET    /api/auth/profile         - Get profile (auth)
PUT    /api/auth/profile         - Update profile (auth)
GET    /api/auth/users           - List users (auth)
```

### Learning Paths
```
GET    /api/learning-paths       - List paths
GET    /api/learning-paths/:id   - Get path
POST   /api/learning-paths       - Create (auth)
PUT    /api/learning-paths/:id   - Update (auth)
DELETE /api/learning-paths/:id   - Delete (auth)
POST   /api/learning-paths/:id/enroll - Enroll (auth)
```

### Resources
```
GET    /api/resources            - List
GET    /api/resources/:id        - Get one
POST   /api/resources            - Create (auth)
POST   /api/resources/:id/save   - Save (auth)
GET    /api/resources/saved/my-resources - My saved (auth)
```

### Assessments
```
GET    /api/assessments          - List
GET    /api/assessments/:id      - Get one
POST   /api/assessments          - Create (auth)
POST   /api/assessments/:id/submit - Submit (auth)
GET    /api/assessments/results/my-results - Results (auth)
```

### Jobs
```
GET    /api/jobs                 - List jobs
GET    /api/jobs/:id             - Get job
POST   /api/jobs                 - Create (auth)
POST   /api/jobs/:id/save        - Save job (auth)
POST   /api/jobs/:id/apply       - Apply (auth)
GET    /api/jobs/saved/my-jobs   - My jobs (auth)
```

---

## 💻 React Component Integration

### Import API Service
```javascript
import { authAPI, learningPathAPI, resourceAPI } from '../services/api';
```

### Use in Component
```javascript
// Get data
const response = await learningPathAPI.getAllPaths();
const paths = response.data.data;

// Create data
await authAPI.updateProfile({ firstName: 'Jane' });

// Login
const { token, user } = (await authAPI.login({...})).data.data;
localStorage.setItem('token', token);
```

### In useEffect
```javascript
useEffect(() => {
  learningPathAPI.getAllPaths()
    .then(res => setPaths(res.data.data))
    .catch(err => setError(err.message))
    .finally(() => setLoading(false));
}, []);
```

---

## 🗄️ MongoDB Commands

### Connect to MongoDB
```bash
# Local
mongo

# Atlas CLI
mongosh "mongodb+srv://..."
```

### Query Users
```javascript
use edssentials;
db.users.find();
db.users.find({ email: 'john@test.com' });
db.users.countDocuments();
```

### Query Learning Paths
```javascript
db.learningpaths.find();
db.learningpaths.find({ category: 'Web Development' });
```

---

## 🧪 Testing with Postman

### 1. Register
```
POST http://localhost:5000/api/auth/register
Body:
{
  "firstName": "John",
  "lastName": "Doe",
  "email": "john@test.com",
  "password": "password123",
  "role": "student"
}
```

### 2. Login
```
POST http://localhost:5000/api/auth/login
Body:
{
  "email": "john@test.com",
  "password": "password123"
}

Response: { token: "...", user: {...} }
```

### 3. Protected Request
```
GET http://localhost:5000/api/auth/profile
Headers:
  Authorization: Bearer <token_from_login>
```

---

## 🐛 Troubleshooting Commands

### Backend Issues
```bash
# Restart backend
cd backend
npm run dev

# Clear node_modules and reinstall
rm -rf node_modules package-lock.json
npm install

# Check MongoDB connection
mongod

# Check port 5000
netstat -ano | findstr :5000
```

### Frontend Issues
```bash
# Clear cache and restart
npm start

# Clear all node_modules
rm -rf node_modules
npm install
npm start

# Check port 3000
netstat -ano | findstr :3000
```

### Database Issues
```bash
# Check MongoDB status
mongod --version

# Connect to MongoDB
mongo

# List databases
show databases;

# Switch to edssentials
use edssentials;
```

---

## 📝 Environment Variables

### Backend (.env)
```env
MONGODB_URI=mongodb://localhost:27017/edssentials
PORT=5000
NODE_ENV=development
JWT_SECRET=your_secret_key_here
JWT_EXPIRE=7d
FRONTEND_URL=http://localhost:3000
```

### Frontend (.env)
```env
REACT_APP_API_URL=http://localhost:5000/api
REACT_APP_ENV=development
```

---

## 📂 Project Structure Quick Map

```
edssentials-app/
├── backend/              ← Node.js + Express
│   ├── server.js         ← Start here
│   ├── models/           ← 5 DB schemas
│   ├── controllers/      ← 5 controllers
│   ├── routes/           ← 5 route files
│   ├── package.json      ← npm install this
│   └── .env              ← Configuration
├── src/                  ← React app
│   ├── services/api.js   ← API client
│   ├── pages/
│   │   ├── Login.js      ← Updated ✓
│   │   ├── Register.js   ← Updated ✓
│   │   └── ...
│   └── ...
├── START_HERE.md         ← Read first
├── ARCHITECTURE.md       ← System design
└── ...
```

---

## 🎯 Common Tasks

### Update a User Profile
```javascript
const response = await authAPI.updateProfile({
  firstName: 'Jane',
  bio: 'Learning enthusiast',
  skills: ['React', 'Node.js']
});
```

### Fetch Learning Paths with Filters
```javascript
// Get all paths
const allPaths = await learningPathAPI.getAllPaths();

// Get by ID
const onePath = await learningPathAPI.getPathById('path_id');

// Enroll user
await learningPathAPI.enrollUser('path_id');
```

### Save a Resource
```javascript
// Get all resources
const resources = await resourceAPI.getAllResources({
  category: 'web',
  type: 'video'
});

// Save a resource
await resourceAPI.saveResource('resource_id');

// Get saved resources
const saved = await resourceAPI.getUserSavedResources();
```

### Submit Assessment
```javascript
const answers = ['option1', 'option2', 'option3'];
const result = await assessmentAPI.submitAssessment('assessment_id', {
  answers
});

// Result: { score: 85, totalPoints: 100 }
```

### Apply for Job
```javascript
// Get all jobs
const jobs = await jobAPI.getAllJobs();

// Save job
await jobAPI.saveJob('job_id');

// Apply for job
await jobAPI.applyForJob('job_id');

// Get saved jobs
const savedJobs = await jobAPI.getUserSavedJobs();
```

---

## 📊 Development Workflow

```
1. START
   │
   ├─ Terminal 1: npm run dev (backend)
   ├─ Terminal 2: npm start (frontend)
   │
2. DEVELOP
   │
   ├─ Make changes
   ├─ Auto-reload (nodemon)
   ├─ Test in browser
   ├─ Check Network tab
   │
3. DEBUG
   │
   ├─ Browser DevTools (F12)
   ├─ Network tab
   ├─ Console logs
   ├─ Backend logs in terminal
   │
4. TEST
   │
   ├─ Manual testing
   ├─ Postman for APIs
   ├─ Check MongoDB
   │
5. DEPLOY
   │
   ├─ npm run build (frontend)
   ├─ Push to hosting
   └─ Monitor logs
```

---

## ✅ Pre-Launch Checklist

- [ ] npm install in backend folder
- [ ] .env files configured
- [ ] MongoDB running
- [ ] Backend starting without errors
- [ ] Frontend starting without errors
- [ ] Can register new user
- [ ] User appears in MongoDB
- [ ] Can login successfully
- [ ] Token in localStorage
- [ ] Dashboard loads
- [ ] No console errors
- [ ] API requests working
- [ ] Ready for feature development

---

## 📚 Documentation Map

| Document | Purpose |
|----------|---------|
| START_HERE.md | Overview & quick start |
| ARCHITECTURE.md | System design & flow |
| backend/README.md | API reference |
| BACKEND_INTEGRATION.md | Code examples |
| FRONTEND_BACKEND_SETUP.md | Setup guide |
| FILES_CREATED.md | What was built |
| QUICK_REFERENCE.md | This file |

---

## 🚀 Performance Tips

1. **Use API Caching** - Cache responses locally
2. **Pagination** - Load data in chunks
3. **Lazy Loading** - Load components on demand
4. **Database Indexing** - Already set up
5. **Minimize Renders** - Use useCallback, useMemo
6. **Code Splitting** - React.lazy for routes
7. **Environment Vars** - Never hardcode secrets

---

## 🎓 Learning Resources

- Express: https://expressjs.com/
- MongoDB: https://docs.mongodb.com/
- React: https://react.dev/
- JWT: https://jwt.io/
- Axios: https://axios-http.com/

---

**Everything you need in one quick reference! 🎉**

Bookmark this page for quick access while developing.
