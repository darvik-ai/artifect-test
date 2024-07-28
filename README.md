Here's a structured overview of the application API endpoints for managing users and todos, formatted for clarity and ease of use.

## API Endpoints Overview

### User Management

#### **Create a New User**
- **Method**: **POST**
- **URL**: 
  ```
  http://localhost:5000/users
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

#### **Create a New Todo**
- **Method**: **POST**
- **URL**: 
  ```
  http://localhost:5000/todos
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

#### **Fetch All Todos for a Specific User**
- **Method**: **GET**
- **URL**: 
  ```
  http://localhost:5000/todos/:userId
  ```

#### **Fetch a Specific Todo**
- **Method**: **GET**
- **URL**: 
  ```
  http://localhost:5000/todos/:userId/:todoId
  ```

#### **Update a Todo**
- **Method**: **PUT**
- **URL**: 
  ```
  http://localhost:5000/todos/:userId/:todoId
  ```
- **Request Body** (only include the fields you want to update):
  ```json
  {
    "title": "Updated Todo",
    "completed": true
  }
  ```

#### **Delete a Todo**
- **Method**: **DELETE**
- **URL**: 
  ```
  http://localhost:5000/todos/:userId/:todoId
  ```
