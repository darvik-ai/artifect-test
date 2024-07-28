Sure, I'll guide you through creating a simple Node.js application called TO-APP that stores data into MongoDB. We'll use the `mongoose` library to interact with MongoDB. We'll create a new database `todoapp` with two collections: `todos` and `users`.

Here's a step-by-step guide:

### Step 1: Set Up the Project

1. **Initialize the Node.js project**:
   ```bash
   mkdir TO-APP
   cd TO-APP
   npm init -y
   ```

2. **Install dependencies**:
   ```bash
   npm install express mongoose body-parser
   ```

### Step 2: Create the `server.js` File

Create a `server.js` file in the root directory of your project:

```javascript
const express = require('express');
const mongoose = require('mongoose');
const bodyParser = require('body-parser');

const app = express();

// Middleware
app.use(bodyParser.json());

// Connect to MongoDB
mongoose.connect('mongodb://localhost/todoapp', { useNewUrlParser: true, useUnifiedTopology: true })
  .then(() => console.log('MongoDB connected...'))
  .catch(err => console.log(err));

// Define schemas
const UserSchema = new mongoose.Schema({
  name: String,
  email: String,
  password: String
});

const TodoSchema = new mongoose.Schema({
  userId: mongoose.Schema.Types.ObjectId,
  title: String,
  description: String,
  completed: Boolean
});

// Create models
const User = mongoose.model('User', UserSchema);
const Todo = mongoose.model('Todo', TodoSchema);

// Routes
app.get('/', (req, res) => {
  res.send('Welcome to TO-APP');
});

// Users routes
app.post('/users', (req, res) => {
  const newUser = new User(req.body);
  newUser.save()
    .then(user => res.json(user))
    .catch(err => res.status(400).json(err));
});

// Todos routes
app.post('/todos', (req, res) => {
  const newTodo = new Todo({
    userId: req.body.userId,
    title: req.body.title,
    description: req.body.description,
    completed: req.body.completed
  });
  newTodo.save()
    .then(todo => res.json(todo))
    .catch(err => res.status(400).json(err));
});

// Fetch all todos for a specific user
app.get('/todos/:userId', (req, res) => {
  Todo.find({ userId: req.params.userId })
    .then(todos => res.json(todos))
    .catch(err => res.status(400).json(err));
});

// Fetch a specific todo
app.get('/todos/:userId/:todoId', (req, res) => {
  Todo.findOne({ userId: req.params.userId, _id: req.params.todoId })
    .then(todo => res.json(todo))
    .catch(err => res.status(400).json(err));
});

// Update a todo
app.put('/todos/:userId/:todoId', (req, res) => {
  Todo.findOneAndUpdate(
    { userId: req.params.userId, _id: req.params.todoId },
    req.body,
    { new: true }
  )
    .then(todo => res.json(todo))
    .catch(err => res.status(400).json(err));
});

// Delete a todo
app.delete('/todos/:userId/:todoId', (req, res) => {
  Todo.findOneAndDelete({ userId: req.params.userId, _id: req.params.todoId })
    .then(() => res.json({ success: true }))
    .catch(err => res.status(400).json(err));
});

// Start server
const PORT = process.env.PORT || 5000;
app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

### Step 3: Run the Application

1. **Start MongoDB** (make sure MongoDB is running on your machine):
   ```bash
   mongod
   ```

2. **Run your Node.js application**:
   ```bash
   node server.js
   ```

Your application should now be running, and you can use tools like Postman to test the API endpoints:

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
  - URL: `POST http://localhost:5000/todos`
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
