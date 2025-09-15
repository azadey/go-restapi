# Go REST API

A REST API for event management with user authentication, built with Go, Gin framework, and SQLite database.

## Features

- User registration and authentication with JWT tokens
- Event CRUD operations (Create, Read, Update, Delete)
- Event registration system for users
- Password hashing for security
- SQLite database with auto-created tables
- Protected routes with JWT middleware

## Tech Stack

- **Go** - Programming language
- **Gin** - Web framework
- **SQLite** - Database
- **JWT** - Authentication tokens
- **bcrypt** - Password hashing

## Setup and Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/azadey/go-restapi.git
   cd go-restapi
   ```

2. Install dependencies:
   ```bash
   go mod tidy
   ```

3. Run the application:
   ```bash
   go run main.go
   ```

The server will start on `http://localhost:8080`

## API Endpoints

### Authentication
- `POST /signup` - User registration
- `POST /login` - User login

### Events (Public)
- `GET /events` - Get all events
- `GET /events/:id` - Get single event

### Events (Protected - requires JWT token)
- `POST /events` - Create new event
- `PUT /events/:id` - Update event
- `DELETE /events/:id` - Delete event
- `POST /events/:id/register` - Register for event
- `DELETE /events/:id/register` - Cancel event registration

## Usage Examples

### User Registration
```bash
curl -X POST http://localhost:8080/signup \
  -H "Content-Type: application/json" \
  -d '{"email": "user@example.com", "password": "password123"}'
```

### User Login
```bash
curl -X POST http://localhost:8080/login \
  -H "Content-Type: application/json" \
  -d '{"email": "user@example.com", "password": "password123"}'
```

### Create Event (requires JWT token)
```bash
curl -X POST http://localhost:8080/events \
  -H "Content-Type: application/json" \
  -H "Authorization: YOUR_JWT_TOKEN" \
  -d '{
    "name": "Tech Conference",
    "description": "Annual tech conference",
    "location": "San Francisco",
    "dateTime": "2025-06-15T10:00:00.000Z"
  }'
```

## Project Structure

```
├── main.go              # Application entry point
├── db/                  # Database configuration and setup
├── models/              # Data models (User, Event)
├── routes/              # API route handlers
├── middlewares/         # Authentication middleware
├── utils/               # Utility functions (JWT, password hashing)
├── api-test/            # HTTP test files
└── api.db               # SQLite database file
```

## Database Schema

The application automatically creates the following tables:
- `users` - User accounts with email and hashed passwords
- `events` - Event information with foreign key to users
- `registrations` - Event registrations linking users to events

## Authentication

Protected routes require a JWT token in the `Authorization` header. Tokens expire after 2 hours and are generated upon successful login.
