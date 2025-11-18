# 🔐 Admin Access Guide - User Data Viewer

## Overview
The user data endpoints are now **protected by admin authentication**. Only admin users with valid credentials can access user information.

---

## 📋 Admin Credentials

**Email:** `admin@edssentials.com`  
**Password:** `admin@123`

> ⚠️ **Important:** Change this password after first login for security!

---

## 🔑 How to Access User Data

### Step 1: Login as Admin
First, login with admin credentials to get an authentication token.

**Endpoint:** `POST http://localhost:5000/api/auth/login`

**Request Body:**
```json
{
  "email": "admin@edssentials.com",
  "password": "admin@123"
}
```

**Response:**
```json
{
  "success": true,
  "message": "Login successful",
  "data": {
    "user": {
      "_id": "...",
      "firstName": "Admin",
      "lastName": "User",
      "email": "admin@edssentials.com",
      "role": "admin",
      "isActive": true
    },
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
  }
}
```

**Copy the `token` from the response** - you'll need it for the next step.

---

### Step 2: Access User Data with Token

Use the token in the `Authorization` header with all data endpoints.

#### Get All Users
**Endpoint:** `GET http://localhost:5000/api/data/users`

**Headers:**
```
Authorization: Bearer <YOUR_TOKEN_HERE>
```

#### Get User Statistics
**Endpoint:** `GET http://localhost:5000/api/data/stats`

**Headers:**
```
Authorization: Bearer <YOUR_TOKEN_HERE>
```

#### Get User by Email
**Endpoint:** `GET http://localhost:5000/api/data/users-by-email/email@example.com`

**Headers:**
```
Authorization: Bearer <YOUR_TOKEN_HERE>
```

#### Get User by ID
**Endpoint:** `GET http://localhost:5000/api/data/users/:id`

**Headers:**
```
Authorization: Bearer <YOUR_TOKEN_HERE>
```

---

## 🛠️ Using cURL or PowerShell

### PowerShell Example:
```powershell
# Step 1: Login and get token
$loginResponse = Invoke-WebRequest -Uri "http://localhost:5000/api/auth/login" `
  -Method POST `
  -Headers @{"Content-Type"="application/json"} `
  -Body '{"email":"admin@edssentials.com","password":"admin@123"}' `
  -UseBasicParsing

$token = ($loginResponse.Content | ConvertFrom-Json).data.token

# Step 2: Access user data with token
$headers = @{
  "Authorization" = "Bearer $token"
  "Content-Type" = "application/json"
}

$usersResponse = Invoke-WebRequest -Uri "http://localhost:5000/api/data/stats" `
  -Headers $headers `
  -UseBasicParsing

$usersResponse.Content | ConvertFrom-Json | ConvertTo-Json -Depth 10
```

---

## 📊 Quick View Script

You can also use the built-in viewer script without authentication:

```bash
node viewUsers.js
```

This script directly connects to MongoDB and displays all users in the database.

---

## 🔒 Security Features

✅ **Token-based Authentication:** All data endpoints require a valid JWT token  
✅ **Role-based Access:** Only users with `admin` role can access data  
✅ **Password Hashing:** Passwords are never returned in API responses  
✅ **7-day Token Expiration:** Tokens expire after 7 days for security  
✅ **CORS Protection:** API has CORS enabled for frontend-backend communication  

---

## ⚡ Available Endpoints

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|----------------|
| GET | `/api/data/users` | Get all users | ✅ Admin |
| GET | `/api/data/stats` | Get user statistics | ✅ Admin |
| GET | `/api/data/users/:id` | Get user by ID | ✅ Admin |
| GET | `/api/data/users-by-email/:email` | Get user by email | ✅ Admin |

---

## 🚀 Testing the Admin Features

1. **Start the backend:**
   ```bash
   node server.js
   ```

2. **Login as admin via Postman/cURL:**
   - Set method to `POST`
   - URL: `http://localhost:5000/api/auth/login`
   - Body (JSON): `{"email":"admin@edssentials.com","password":"admin@123"}`
   - Copy the token from response

3. **Access user data:**
   - Set method to `GET`
   - URL: `http://localhost:5000/api/data/stats`
   - Add header: `Authorization: Bearer <token>`
   - View all users with their details!

---

## 🔄 Creating Additional Admin Users

To create more admin users:

1. Use the register endpoint with `role: "admin"`
2. Or manually create users and update their role to `"admin"` in MongoDB

```javascript
// Example - Update user role to admin
db.users.updateOne(
  { email: "user@example.com" },
  { $set: { role: "admin" } }
)
```

---

## ❓ Troubleshooting

### "No token provided"
- Make sure you included the `Authorization: Bearer <token>` header
- Check that the token is valid and not expired

### "Access denied. Admin role required"
- The token is valid but the user doesn't have admin role
- Login with admin credentials instead

### "Invalid or expired token"
- The token has expired (7 days)
- Login again to get a new token

---

## 📝 Notes

- All user passwords are excluded from API responses for security
- Passwords are hashed using bcryptjs with 10 salt rounds
- The admin user should change their password in production
- Tokens are stored in JWT format with user ID and role

