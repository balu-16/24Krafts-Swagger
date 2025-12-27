# 24Krafts API Swagger Documentation

This folder contains the Swagger/OpenAPI documentation files for the 24Krafts Backend API.

## Files

- **index.html** - Custom Swagger UI interface
- **style.css** - Custom styling for the Swagger UI
- **README.md** - This file

## Accessing the Documentation

The Swagger documentation is automatically generated and available at:

**Production (Vercel):**
- URL: `https://24-krafts-backend.vercel.app/api/docs`
- JSON Spec: `https://24-krafts-backend.vercel.app/api/docs-json`

**Development (Local):**
- URL: `http://localhost:3000/api/docs`
- JSON Spec: `http://localhost:3000/api/docs-json`

## Features

- Interactive API testing
- JWT Bearer token authentication
- Request/Response examples
- Schema definitions
- Endpoint grouping by tags

## Authentication

All protected endpoints require a JWT token. To authenticate:

1. Use the `/api/auth/send-otp` endpoint to send an OTP
2. Use the `/api/auth/verify-otp` endpoint to verify the OTP and get an `access_token`
3. Click the "Authorize" button in Swagger UI
4. Enter: `Bearer <your_access_token>`
5. Click "Authorize" and "Close"

Now you can test all protected endpoints.

## API Tags

- **Health** - Health check endpoints
- **Auth** - Authentication endpoints (OTP, Login, Signup)
- **Users** - User management
- **Profiles** - User profile management
- **Posts** - Posts and project applications
- **Projects** - Project management
- **Chat** - Conversations and messaging
- **Schedules** - Schedule management for projects
- **Uploads** - File uploads
- **Notifications** - Push notification management
- **Admin** - Admin endpoints

## Customization

To customize the Swagger UI:

1. Edit `index.html` to modify the Swagger UI configuration
2. Edit `style.css` to change the visual appearance
3. The OpenAPI specification is generated automatically from code annotations

## Notes

- The Swagger documentation is generated at runtime from NestJS decorators
- All API endpoints are automatically documented using `@ApiTags`, `@ApiOperation`, `@ApiResponse`, etc.
- The documentation reflects the current state of the codebase

