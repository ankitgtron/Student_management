---

# **Simple Student Database Management System**

## **Project Overview:**
This project is a simple backend application that allows the management of student records using **Node.js** and **MySQL**. The application supports basic **CRUD** (Create, Read, Update, Delete) operations on student data and can be accessed through RESTful API endpoints.

## **Technologies Used:**
- **Node.js** – Server-side JavaScript environment
- **Express.js** – Web framework for Node.js
- **MySQL** – Relational database management system
- **mysql2** – MySQL client for Node.js

---

## **Folder Structure:**
```plaintext
student-db/
│
├── node_modules/                 # Dependencies installed by npm
│
├── public/                        # Static files (if needed in the future)
│   └── index.html                 # A sample HTML file (optional)
│
├── routes/                        # Separate folder for routes
│   └── students.js                # Routes related to student management
│
├── database/                      # Database-related files (e.g., database setup)
│   └── db.js                      # MySQL connection setup
│
├── .gitignore                     # To exclude files from git
├── index.js                       # Entry point of the application
├── package.json                   # Project configuration
└── README.md                      # Project overview and instructions
```

---

## **Setup Instructions:**

### 1. **Install Dependencies:**
Make sure you have **Node.js** and **npm** installed on your system. Then, navigate to your project folder and run the following command to install the required dependencies:

```bash
npm install
```

This will install:
- **express**: Web framework for building APIs.
- **mysql2**: MySQL client for Node.js.

### 2. **Create the MySQL Database and Table:**
Before running the application, you need to create the **StudentDB** and the **Students** table in MySQL.

1. Open MySQL and create a database:

   ```sql
   CREATE DATABASE StudentDB;
   USE StudentDB;
   ```

2. Create the **Students** table:

   ```sql
   CREATE TABLE Students (
       id INT AUTO_INCREMENT PRIMARY KEY,
       name VARCHAR(100),
       age INT,
       email VARCHAR(100)
   );
   ```

### 3. **Run the Application:**
Once the database is set up, you can start the server:

```bash
node index.js
```

This will start the application on **http://localhost:3000**.

---

## **API Endpoints:**

The application exposes the following RESTful API endpoints for managing students:

### **1. `POST /students`** – Create a New Student
This endpoint allows you to add a new student to the database.

#### **Request Body:**
- `name`: The name of the student.
- `age`: The age of the student.
- `email`: The email of the student.

#### **Response:**
- `student_id`: The ID of the newly created student.

### **2. `GET /students`** – Get All Students
This endpoint retrieves all students in the database.

#### **Response:**
- A list of all students, including their `id`, `name`, `age`, and `email`.

### **3. `GET /students/:id`** – Get a Student by ID
This endpoint retrieves a student by their unique **ID**.

#### **Response:**
- Details of the student with the requested `id`, including `name`, `age`, and `email`.

### **4. `PUT /students/:id`** – Update Student Information
This endpoint allows you to update the information of an existing student.

#### **Request Body:**
- `name`: The new name of the student (optional).
- `age`: The new age of the student (optional).
- `email`: The new email of the student (optional).

#### **Response:**
- A success message indicating that the student was updated.

### **5. `DELETE /students/:id`** – Delete a Student
This endpoint deletes a student by their unique **ID**.

#### **Response:**
- A success message indicating that the student was deleted.

---

## **File Descriptions:**

### **1. `index.js`**
This is the main entry point of the application, where the Express server is set up and the routes are initialized.

- **Sets up the Express app** to handle HTTP requests.
- **Connects to MySQL** using the `mysql2` package.
- **Registers routes** to handle CRUD operations for the students.

### **2. `routes/students.js`**
Contains the logic for handling the following CRUD routes for students:

- **POST /students** – Add a new student.
- **GET /students** – Get all students.
- **GET /students/:id** – Get a student by ID.
- **PUT /students/:id** – Update a student.
- **DELETE /students/:id** – Delete a student.

Each route uses the **MySQL connection** to interact with the database.

### **3. `database/db.js` (Optional)**
This file contains the **MySQL connection pool** that is used across the application for querying the database. It is modularized to allow the connection to be reused throughout the app.

### **4. `.gitignore`**
This file is used to exclude certain files and directories from being tracked by Git.

```plaintext
node_modules/
.env
```

### **5. `README.md`**
This file contains the **project documentation**, including setup instructions, API endpoints, and usage information. It helps developers and other users to understand and use the project easily.

---

## **Example Usage:**

### 1. **Create a New Student:**

- **Endpoint:** `POST /students`
- **Request Body:**
  - `name`: Name of the student
  - `age`: Age of the student
  - `email`: Email of the student

- **Response:**
  - `student_id`: The ID of the newly created student.

### 2. **Get All Students:**

- **Endpoint:** `GET /students`
- **Response:**
  - A list of all students, including their `id`, `name`, `age`, and `email`.

### 3. **Update a Student's Information:**

- **Endpoint:** `PUT /students/:id`
- **Request Body:**
  - `name`: New name of the student (optional).
  - `age`: New age of the student (optional).
  - `email`: New email of the student (optional).

- **Response:**
  - A success message indicating that the student was updated.

### 4. **Delete a Student:**

- **Endpoint:** `DELETE /students/:id`
- **Response:**
  - A success message indicating that the student was deleted.

---

## **Conclusion:**

This project provides a **simple backend system** for managing student data using **Node.js** and **MySQL**. It covers the essentials of building a **RESTful API** and interacting with a **MySQL database**. This project is great for students to practice **CRUD operations** and understand the flow of data between the client and server in a full-stack application.

--- 

