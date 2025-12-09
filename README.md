# 24Krafts API Documentation

Complete Swagger/OpenAPI documentation for the 24Krafts backend API.

## Files

- `index.html` - Swagger UI webpage with custom styling
- `swagger.yaml` - OpenAPI 3.0 specification
- `.env` - Environment configuration template

## Quick Start

### Option 1: Open Directly (Local)

Simply open `index.html` in your browser. Note: Some browsers may block local file access for YAML files. Use a local server instead.

### Option 2: Local Server (Recommended)

Using Python:
```bash
cd swagger_docs
python -m http.server 8080
# Open http://localhost:8080
```

Using Node.js:
```bash
npx serve swagger_docs
# Or
npx http-server swagger_docs
```

### Option 3: Deploy to Vercel

1. Create a new Vercel project
2. Upload this folder as the project root
3. Deploy - Vercel will serve the static files automatically

### Option 4: Deploy to Netlify

1. Drag and drop the `swagger_docs` folder to Netlify
2. Or connect your GitHub repo and set the publish directory to `swagger_docs`

### Option 5: Deploy to GitHub Pages

1. Push to a GitHub repository
2. Go to Settings > Pages
3. Set source to the `swagger_docs` folder
4. Access at `https://yourusername.github.io/reponame/`

## API Base URL

**Production:** `https://24-krafts-backend.vercel.app/api`

## Authentication

The API uses JWT Bearer authentication for all authenticated endpoints:

### JWT Bearer Authentication
Used for all authenticated endpoints (users, profiles, posts, projects, chat, schedules, uploads)
```
Authorization: Bearer <jwt_token>
```

## Getting Started Flow

### For New Users

1. **Send OTP** - `POST /auth/send-otp`
   - Sends a 6-digit OTP to the provided phone number

2. **Verify OTP** - `POST /auth/verify-otp`
   - Returns `isNewUser: true` if the user needs to complete signup
   - Returns `isNewUser: false` with JWT token for existing users

3. **Complete Signup** (for new users) - `POST /auth/signup`
   - Use the same OTP from step 1 along with user details
   - The OTP remains valid even after verification in step 2
   - Returns JWT token upon successful registration

4. **Use JWT Token** - Include the JWT token in subsequent authenticated requests

### For Existing Users

1. **Send OTP** - `POST /auth/send-otp`
2. **Verify OTP** - `POST /auth/verify-otp` (returns `isNewUser: false` with JWT token)
3. **Use JWT Token** - Include the JWT token in subsequent authenticated requests

---

## Sample cURL Commands

### Health Check
```bash
curl -X GET "https://24-krafts-backend.vercel.app/api/health"
```

### Send OTP
```bash
curl -X POST "https://24-krafts-backend.vercel.app/api/auth/send-otp" \
  -H "Content-Type: application/json" \
  -d '{"phone": "9876543210"}'
```

### Verify OTP
```bash
curl -X POST "https://24-krafts-backend.vercel.app/api/auth/verify-otp" \
  -H "Content-Type: application/json" \
  -d '{"phone": "9876543210", "otp": "123456"}'
```

### Complete Signup (for new users)
```bash
curl -X POST "https://24-krafts-backend.vercel.app/api/auth/signup" \
  -H "Content-Type: application/json" \
  -d '{
    "phone": "9876543210",
    "otp": "123456",
    "firstName": "John",
    "lastName": "Doe",
    "email": "john.doe@example.com",
    "gender": "male",
    "department": "Acting",
    "state": "Maharashtra",
    "city": "Mumbai",
    "role": "Talent",
    "aadharNumber": "123456789012"
  }'
```

### List Profiles
```bash
curl -X GET "https://24-krafts-backend.vercel.app/api/profiles?limit=20" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN"
```

### Get Profile by ID
```bash
curl -X GET "https://24-krafts-backend.vercel.app/api/profiles/PROFILE_UUID" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN"
```

### Update Profile
```bash
curl -X PUT "https://24-krafts-backend.vercel.app/api/profiles/PROFILE_UUID" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"first_name": "John", "last_name": "Doe", "bio": "Artist from Mumbai"}'
```

### List Posts
```bash
curl -X GET "https://24-krafts-backend.vercel.app/api/posts?limit=20" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN"
```

### Create Post
```bash
curl -X POST "https://24-krafts-backend.vercel.app/api/posts" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Looking for Actors",
    "description": "We need talented actors for our upcoming film project",
    "department": "Acting",
    "location": "Mumbai",
    "status": "open"
  }'
```

### Get Post by ID
```bash
curl -X GET "https://24-krafts-backend.vercel.app/api/posts/POST_UUID" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN"
```

### Like a Post
```bash
curl -X POST "https://24-krafts-backend.vercel.app/api/posts/POST_UUID/like" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN"
```

### Add Comment
```bash
curl -X POST "https://24-krafts-backend.vercel.app/api/posts/POST_UUID/comment" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"content": "Great opportunity!"}'
```

### Apply to Project
```bash
curl -X POST "https://24-krafts-backend.vercel.app/api/posts/POST_UUID/apply" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"cover_letter": "I am interested in this role", "portfolio_link": "https://myportfolio.com"}'
```

### List Conversations
```bash
curl -X GET "https://24-krafts-backend.vercel.app/api/conversations?profileId=PROFILE_UUID" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN"
```

### Create Conversation
```bash
curl -X POST "https://24-krafts-backend.vercel.app/api/conversations" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"member_ids": ["PROFILE_UUID_1", "PROFILE_UUID_2"], "is_group": false}'
```

### Send Message
```bash
curl -X POST "https://24-krafts-backend.vercel.app/api/conversations/CONVERSATION_UUID/messages" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"content": "Hello!"}'
```

### List Schedules
```bash
curl -X GET "https://24-krafts-backend.vercel.app/api/schedules?limit=20" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN"
```

### Create Schedule (Recruiter Only)
```bash
curl -X POST "https://24-krafts-backend.vercel.app/api/schedules" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "project_id": "PROJECT_UUID",
    "title": "Script Reading Session",
    "date": "2024-12-01",
    "start_time": "10:00",
    "end_time": "12:00",
    "location": "Studio A"
  }'
```

### Upload File
```bash
curl -X POST "https://24-krafts-backend.vercel.app/api/uploads" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -F "file=@/path/to/image.jpg"
```

### Save Push Notification Token
```bash
curl -X POST "https://24-krafts-backend.vercel.app/api/notifications/save-token" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"token": "EXPO_PUSH_TOKEN", "platform": "android", "device_name": "Pixel 6"}'
```

---

## API Categories

| Category | Description | Auth Type |
|----------|-------------|-----------|
| Health | Health check endpoint | None |
| Auth | Authentication | None/JWT |
| Users | User management | JWT |
| Profiles | Profile CRUD | JWT |
| Posts | Posts & applications | JWT |
| Projects | Project management | JWT |
| Chat | Conversations & messages | JWT |
| Schedules | Schedule management | JWT |
| Uploads | File uploads | JWT |
| Notifications | Push notifications | JWT |
| Admin | Admin endpoints | JWT (Admin role) |

---

## Response Codes

| Code | Description |
|------|-------------|
| 200 | Success |
| 201 | Created |
| 400 | Bad Request - Validation error |
| 401 | Unauthorized - Invalid/missing token |
| 403 | Forbidden - Insufficient permissions |
| 404 | Not Found |
| 429 | Too Many Requests - Rate limited |
| 500 | Internal Server Error |

---

## Rate Limits

- **Default:** 100 requests per minute
- **Uploads:** 5 uploads per minute
- **Messages:** 10 messages per second

---

## Support

For API issues, contact the development team.
