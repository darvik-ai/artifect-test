Application API endpoints:

- **Create a new user**:
  - URL: `POST http://localhost:5000/users`
  - Body:
    ```json
    {
      "name": "John Doe",
      "email": "john@example.com",
      "password": "password123"
    }
    ```

- **Create a new todo**:
  - URL: POST
    ```http://localhost:5000/todos```
  - Body:
    ```json
    {
      "userId": "User's ObjectId",
      "title": "Sample Todo",
      "description": "This is a sample todo item",
      "completed": false
    }
    ```

- **Fetch all todos for a specific user**:
  - URL: `GET http://localhost:5000/todos/:userId`

- **Fetch a specific todo**:
  - URL: `GET http://localhost:5000/todos/:userId/:todoId`

- **Update a todo**:
  - URL: `PUT http://localhost:5000/todos/:userId/:todoId`
  - Body: (only include the fields you want to update)
    ```json
    {
      "title": "Updated Todo",
      "completed": true
    }
    ```

- **Delete a todo**:
  - URL: `DELETE http://localhost:5000/todos/:userId/:todoId`

This is a basic setup. You can expand it by adding more features, validation, authentication, etc.
