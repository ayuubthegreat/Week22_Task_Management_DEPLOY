# TaskManager

## What This API Is
This is an API specifically designed to help you manage and execute your tasks. 

## Base URL
```
http://localhost:3000
```

## Authentication
Most endpoints require authentication via JWT token. Include the token in the `Authorization` header as `Bearer <token>`.

Obtain a token by registering or logging in via the auth endpoints.

## All Available Endpoints

### Authentication Endpoints

#### POST /api/auth/register
Register a new user.

**Request Body:**
```json
{
  "email": "user@example.com",
  "password": "password123",
  "name": "User Name"
}
```

**Response (201):**
```json
{
  "success": true,
  "message": "User registered successfully",
  "data": {
    "id": "user-id",
    "email": "user@example.com",
    "name": "User Name",
    "token": "jwt-token"
  }
}
```

**Error Responses:**
- 400: User already exists
- 500: Server error

#### POST /api/auth/login
Log in an existing user.

**Request Body:**
```json
{
  "email": "user@example.com",
  "password": "password123"
}
```

**Response (200):**
```json
{
  "success": true,
  "message": "Login successful",
  "data": {
    "user": {
      "id": "user-id",
      "email": "user@example.com",
      "name": "User Name"
    },
    "token": "jwt-token"
  }
}
```

**Error Responses:**
- 400: Invalid email or password
- 500: Server error

#### GET /api/auth/me
Get current user profile. Requires authentication.

**Response (200):**
```json
{
  "success": true,
  "data": {
    "id": "user-id",
    "email": "user@example.com",
    "name": "User Name"
  }
}
```

**Error Responses:**
- 401: Unauthorized (invalid/missing token)
- 500: Server error

### Task Endpoints
All task endpoints require authentication.

#### GET /api/tasks
Get all tasks for the authenticated user.

**Response (200):**
```json
{
  "success": true,
  "count": 2,
  "data": [
    {
      "id": "task-id",
      "title": "Task Title",
      "description": "Task Description",
      "status": "pending",
      "priority": "high",
      "dueDate": "2025-12-31T23:59:59.000Z",
      "assignedTo": null,
      "createdAt": "2025-12-23T00:00:00.000Z",
      "updatedAt": "2025-12-23T00:00:00.000Z",
      "userId": "user-id"
    }
  ]
}
```

**Error Responses:**
- 401: Unauthorized
- 500: Server error

#### GET /api/tasks/:id
Get a specific task by ID.

**Response (200):**
```json
{
  "success": true,
  "data": {
    "id": "task-id",
    "title": "Task Title",
    "description": "Task Description",
    "status": "pending",
    "priority": "high",
    "dueDate": "2025-12-31T23:59:59.000Z",
    "assignedTo": null,
    "createdAt": "2025-12-23T00:00:00.000Z",
    "updatedAt": "2025-12-23T00:00:00.000Z",
    "userId": "user-id"
  }
}
```

**Error Responses:**
- 401: Unauthorized
- 404: Task not found
- 500: Server error

#### POST /api/tasks
Create a new task.

**Request Body:**
```json
{
  "title": "New Task",
  "description": "Task description",
  "status": "pending",
  "priority": "medium",
  "dueDate": "2025-12-31T23:59:59.000Z"
}
```

**Response (201):**
```json
{
  "success": true,
  "data": {
    "id": "new-task-id",
    "title": "New Task",
    "description": "Task description",
    "status": "pending",
    "priority": "medium",
    "dueDate": "2025-12-31T23:59:59.000Z",
    "assignedTo": null,
    "createdAt": "2025-12-23T00:00:00.000Z",
    "updatedAt": "2025-12-23T00:00:00.000Z",
    "userId": "user-id"
  }
}
```

**Error Responses:**
- 400: Bad request
- 401: Unauthorized
- 500: Server error

#### PUT /api/tasks/:id
Update an existing task.

**Request Body:**
```json
{
  "title": "Updated Task",
  "status": "in_progress"
}
```

**Response (200):**
```json
{
  "success": true,
  "data": {
    "id": "task-id",
    "title": "Updated Task",
    "description": "Task description",
    "status": "in_progress",
    "priority": "medium",
    "dueDate": "2025-12-31T23:59:59.000Z",
    "assignedTo": null,
    "createdAt": "2025-12-23T00:00:00.000Z",
    "updatedAt": "2025-12-23T00:00:00.000Z",
    "userId": "user-id"
  }
}
```

**Error Responses:**
- 400: Bad request
- 401: Unauthorized
- 404: Task not found
- 500: Server error

#### DELETE /api/tasks/:id
Delete a task.

**Response (200):**
```json
{
  "success": true,
  "data": {
    "id": "task-id",
    "title": "Task Title",
    "description": "Task Description",
    "status": "pending",
    "priority": "high",
    "dueDate": "2025-12-31T23:59:59.000Z",
    "assignedTo": null,
    "createdAt": "2025-12-23T00:00:00.000Z",
    "updatedAt": "2025-12-23T00:00:00.000Z",
    "userId": "user-id"
  }
}
```

**Error Responses:**
- 401: Unauthorized
- 404: Task not found
- 500: Server error

### Subtask Endpoints
All subtask endpoints require authentication.

#### GET /api/tasks/:taskId/subtasks
Get all subtasks for a specific task.

**Response (200):**
```json
{
  "success": true,
  "count": 1,
  "data": [
    {
      "id": "subtask-id",
      "title": "Subtask Title",
      "description": "Subtask Description",
      "completed": false,
      "taskId": "task-id",
      "createdAt": "2025-12-23T00:00:00.000Z",
      "updatedAt": "2025-12-23T00:00:00.000Z"
    }
  ]
}
```

**Error Responses:**
- 401: Unauthorized
- 404: Task not found or access denied
- 500: Server error

#### GET /api/subtasks/:id
Get a specific subtask by ID.

**Response (200):**
```json
{
  "success": true,
  "data": {
    "id": "subtask-id",
    "title": "Subtask Title",
    "description": "Subtask Description",
    "completed": false,
    "taskId": "task-id",
    "createdAt": "2025-12-23T00:00:00.000Z",
    "updatedAt": "2025-12-23T00:00:00.000Z"
  }
}
```

**Error Responses:**
- 401: Unauthorized
- 404: Subtask not found or access denied
- 500: Server error

#### POST /api/tasks/:taskId/subtasks
Create a new subtask for a task.

**Request Body:**
```json
{
  "title": "New Subtask",
  "description": "Subtask description",
  "completed": false
}
```

**Response (201):**
```json
{
  "success": true,
  "data": {
    "id": "new-subtask-id",
    "title": "New Subtask",
    "description": "Subtask description",
    "completed": false,
    "taskId": "task-id",
    "createdAt": "2025-12-23T00:00:00.000Z",
    "updatedAt": "2025-12-23T00:00:00.000Z"
  }
}
```

**Error Responses:**
- 400: Bad request
- 401: Unauthorized
- 404: Task not found or access denied
- 500: Server error

#### PUT /api/subtasks/:id
Update a subtask.

**Request Body:**
```json
{
  "title": "Updated Subtask",
  "completed": true
}
```

**Response (201):**
```json
{
  "success": true,
  "data": {
    "id": "subtask-id",
    "title": "Updated Subtask",
    "description": "Subtask description",
    "completed": true,
    "taskId": "task-id",
    "createdAt": "2025-12-23T00:00:00.000Z",
    "updatedAt": "2025-12-23T00:00:00.000Z"
  }
}
```

**Error Responses:**
- 400: Bad request
- 401: Unauthorized
- 404: Subtask not found or access denied
- 500: Server error

#### DELETE /api/subtasks/:id
Delete a subtask.

**Response (200):**
```json
{
  "success": true,
  "data": {
    "id": "subtask-id",
    "title": "Subtask Title",
    "description": "Subtask Description",
    "completed": false,
    "taskId": "task-id",
    "createdAt": "2025-12-23T00:00:00.000Z",
    "updatedAt": "2025-12-23T00:00:00.000Z"
  }
}
```

**Error Responses:**
- 401: Unauthorized
- 404: Subtask not found or access denied
- 500: Server error

## Data Models

### User
```json
{
  "id": "string",
  "email": "string",
  "password": "string (hashed)",
  "name": "string",
  "createdAt": "DateTime",
  "updatedAt": "DateTime"
}
```

### Task
```json
{
  "id": "string",
  "title": "string",
  "description": "string",
  "status": "pending | in_progress | completed | cancelled",
  "priority": "low | medium | high | urgent",
  "dueDate": "DateTime | null",
  "assignedTo": "string | null",
  "createdAt": "DateTime",
  "updatedAt": "DateTime",
  "userId": "string"
}
```

### Subtask
```json
{
  "id": "string",
  "title": "string",
  "description": "string",
  "completed": "boolean",
  "taskId": "string",
  "createdAt": "DateTime",
  "updatedAt": "DateTime"
}
```

## Error Handling
All errors follow this format:
```json
{
  "success": false,
  "message": "Error description",
  "error": "Detailed error (only in development)"
}
```

Common HTTP status codes:
- 200: Success
- 201: Created
- 400: Bad Request
- 401: Unauthorized
- 404: Not Found
- 500: Internal Server Error
