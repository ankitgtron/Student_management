
### **Project: Simple Student Database Management System**

#### **Objective:**
Create a basic **Student Database** management system that can store and retrieve student information using **Node.js** and **MySQL**. The system will support basic CRUD (Create, Read, Update, Delete) operations on student records.

---

### **Steps to Complete the Project:**

#### 1. **Set Up the Project:**

1. **Create a new directory** for the project:

   ```bash
   mkdir student-db
   cd student-db
   ```

2. **Initialize the project** and install dependencies:

   ```bash
   npm init -y
   npm install express mysql2
   ```

#### 2. **Create the MySQL Database:**

Create the database and the **Students table**.

```sql
CREATE DATABASE StudentDB;
USE StudentDB;

-- Create Students Table
CREATE TABLE Students (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    age INT,
    email VARCHAR(100)
);
```

#### 3. **Create the Node.js Backend:**

1. **Create `index.js` file** to set up the backend:

```js
const express = require('express');
const mysql = require('mysql2');

// Set up the Express app
const app = express();
app.use(express.json());

// Create a MySQL connection pool
const pool = mysql.createPool({
    host: 'localhost',
    user: 'root',       // Replace with your MySQL user
    password: '',       // Replace with your MySQL password
    database: 'StudentDB'
});

const promisePool = pool.promise();

// Start the server
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
    console.log(`Server is running on port ${PORT}`);
});
```

#### 4. **Create CRUD Routes:**

Here are the basic routes to handle the CRUD operations.

- **Create a new student:**

```js
app.post('/students', async (req, res) => {
    const { name, age, email } = req.body;
    try {
        const [result] = await promisePool.query(
            'INSERT INTO Students (name, age, email) VALUES (?, ?, ?)',
            [name, age, email]
        );
        res.status(201).json({ student_id: result.insertId });
    } catch (err) {
        res.status(500).json({ error: err.message });
    }
});
```

- **Get all students:**

```js
app.get('/students', async (req, res) => {
    try {
        const [rows] = await promisePool.query('SELECT * FROM Students');
        res.status(200).json(rows);
    } catch (err) {
        res.status(500).json({ error: err.message });
    }
});
```

- **Get a specific student by ID:**

```js
app.get('/students/:id', async (req, res) => {
    const { id } = req.params;
    try {
        const [rows] = await promisePool.query(
            'SELECT * FROM Students WHERE id = ?',
            [id]
        );
        if (rows.length > 0) {
            res.status(200).json(rows[0]);
        } else {
            res.status(404).json({ message: 'Student not found' });
        }
    } catch (err) {
        res.status(500).json({ error: err.message });
    }
});
```

- **Update a student's information:**

```js
app.put('/students/:id', async (req, res) => {
    const { id } = req.params;
    const { name, age, email } = req.body;
    try {
        const [result] = await promisePool.query(
            'UPDATE Students SET name = ?, age = ?, email = ? WHERE id = ?',
            [name, age, email, id]
        );
        if (result.affectedRows > 0) {
            res.status(200).json({ message: 'Student updated successfully' });
        } else {
            res.status(404).json({ message: 'Student not found' });
        }
    } catch (err) {
        res.status(500).json({ error: err.message });
    }
});
```

- **Delete a student:**

```js
app.delete('/students/:id', async (req, res) => {
    const { id } = req.params;
    try {
        const [result] = await promisePool.query(
            'DELETE FROM Students WHERE id = ?',
            [id]
        );
        if (result.affectedRows > 0) {
            res.status(200).json({ message: 'Student deleted successfully' });
        } else {
            res.status(404).json({ message: 'Student not found' });
        }
    } catch (err) {
        res.status(500).json({ error: err.message });
    }
});
```

#### 5. **Testing the Application:**

1. **Start the server** by running:

   ```bash
   node index.js
   ```

2. **Test the API using Postman** or **cURL**:

   - `POST /students` to add a new student.
   - `GET /students` to get all students.
   - `GET /students/:id` to get a student by ID.
   - `PUT /students/:id` to update a student's information.
   - `DELETE /students/:id` to delete a student.

#### 6. **Example API Requests:**

- **Add a student:**

   ```json
   POST /students
   {
       "name": "John Doe",
       "age": 22,
       "email": "johndoe@example.com"
   }
   ```

- **Get all students:**

   ```json
   GET /students
   ```

- **Get a student by ID:**

   ```json
   GET /students/1
   ```

- **Update a student:**

   ```json
   PUT /students/1
   {
       "name": "Johnathan Doe",
       "age": 23,
       "email": "johnnyd@example.com"
   }
   ```

- **Delete a student:**

   ```json
   DELETE /students/1
   ```

---

### **Conclusion:**

This project is a simple but useful backend system that allows students to:

- Perform **basic CRUD operations** on a database using **Node.js** and **MySQL**.
- Understand how to interact with a database through **Node.js** using the `mysql2` package.
- Set up and test a simple **RESTful API**.
