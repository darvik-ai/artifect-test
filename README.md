Here's a structured overview of the application API endpoints for managing users and todos, formatted for clarity and ease of use.

## API Endpoints Overview

### User Management

#### Create a New User
- **URL**: 
  ```
  POST http://localhost:5000/users
  ```
- **Request Body**:
  ```json
  {
    "name": "John Doe",
    "email": "john@example.com",
    "password": "password123"
  }
  ```

### Todo Management

#### Create a New Todo
- **URL**: 
  ```
  POST http://localhost:5000/todos
  ```
- **Request Body**:
  ```json
  {
    "userId": "User's ObjectId",
    "title": "Sample Todo",
    "description": "This is a sample todo item",
    "completed": false
  }
  ```

#### Fetch All Todos for a Specific User
- **URL**: 
  ```
  GET http://localhost:5000/todos/:userId
  ```

#### Fetch a Specific Todo
- **URL**: 
  ```
  GET http://localhost:5000/todos/:userId/:todoId
  ```

#### Update a Todo
- **URL**: 
  ```
  PUT http://localhost:5000/todos/:userId/:todoId
  ```
- **Request Body** (only include the fields you want to update):
  ```json
  {
    "title": "Updated Todo",
    "completed": true
  }
  ```

#### Delete a Todo
- **URL**: 
  ```
  DELETE http://localhost:5000/todos/:userId/:todoId
  ```

