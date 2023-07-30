const express = require('express');
const mysql = require('mysql2');
const bodyParser = require('body-parser');

const app = express();
const PORT = 8080;

// Database connection
const connection = mysql.createConnection({
  host: 'localhost',
  user: 'root',
  password: 'Pokemon09*',
  database: 'university',
});

connection.connect((err) => {
  if (err) {
    console.error('Error connecting to MySQL database: ', err);
    return;
  }
  console.log('Connected to MySQL database');
});

// Middleware to parse incoming JSON data
app.use(bodyParser.json());

// GET - /teacher/{id} - Get a specific teacher record by ID.
app.get('/teacher/:id', (req, res) => {
  const teacherId = req.params.id;
  const sql = 'SELECT * FROM teacher WHERE teacher_id = ?';
  connection.query(sql, [teacherId], (err, result) => {
    if (err) {
      console.error('Error fetching teacher: ', err);
      return res.status(500).json({ error: 'Failed to fetch teacher' });
    }
    if (result.length === 0) {
      return res.status(404).json({ message: 'Teacher not found' });
    }
    res.json(result[0]);
  });
});

// GET - /teacher - Get a list of teachers based on filters.
app.get('/teacher', (req, res) => {
  let query = 'SELECT * FROM teacher WHERE 1';

  const { name, is_active, designation } = req.query;

  if (name) {
    query += ' AND name LIKE ' + connection.escape(`%${name}%`);
  }

  if (is_active) {
    query += ' AND is_active = ' + connection.escape(is_active);
  }

  if (designation) {
    query += ' AND designation LIKE ' + connection.escape(`%${designation}%`);
  }

  connection.query(query, (err, rows) => {
    if (err) {
      console.error('Error fetching teachers: ', err);
      return res.status(500).json({ error: 'Failed to fetch teachers' });
    }
    res.json(rows);
  });
});

// POST - /teacher - Create a new teacher record using the JSON payload
app.post('/teacher', (req, res) => {
  const { name, is_active, designation } = req.body;
  const sql = 'INSERT INTO teacher (name, is_active, designation) VALUES (?, ?, ?)';
  connection.query(sql, [name, is_active, designation], (err, result) => {
    if (err) {
      console.error('Error creating teacher: ', err);
      return res.status(500).json({ error: 'Failed to create teacher' });
    }
    res.status(201).json({ teacher_id: result.insertId, name, is_active, designation });
  });
});

// ...

// GET - /course - Get a list of courses based on filters
app.get('/course', (req, res) => {
  let query = 'SELECT * FROM course WHERE 1';

  const { name, start_date, end_date, is_active } = req.query;

  if (name) {
    query += ' AND name LIKE ' + connection.escape(`%${name}%`);
  }

  if (start_date) {
    query += ' AND start_date >= ' + connection.escape(start_date);
  }

  if (end_date) {
    query += ' AND end_date <= ' + connection.escape(end_date);
  }

  if (is_active) {
    query += ' AND is_active = ' + connection.escape(is_active);
  }

  connection.query(query, (err, rows) => {
    if (err) {
      console.error('Error fetching courses: ', err);
      return res.status(500).json({ error: 'Failed to fetch courses' });
    }
    res.json(rows);
  });
});



// POST - /course - Create a new course record using the JSON payload
app.post('/course', (req, res) => {
  const { course_id, course_mentor, name, start_date, end_date, description, is_active } = req.body;
  const sql = 'INSERT INTO course (course_id, course_mentor, name, start_date, end_date, description, is_active) VALUES (?, ?, ?, ?, ?, ?, ?)';
  connection.query(sql, [course_id, course_mentor, name, start_date, end_date, description, is_active], (err, result) => {
    if (err) {
      console.error('Error creating course: ', err);
      return res.status(500).json({ error: 'Failed to create course' });
    }
    res.status(201).json({ course_id, course_mentor, name, start_date, end_date, description, is_active });
  });
});

// GET - /course/{id} - Get a specific course record by ID
app.get('/course/:id', (req, res) => {
  const courseId = req.params.id;
  const sql = 'SELECT * FROM course WHERE course_id = ?';
  connection.query(sql, [courseId], (err, result) => {
    if (err) {
      console.error('Error fetching course: ', err);
      return res.status(500).json({ error: 'Failed to fetch course' });
    }
    if (result.length === 0) {
      return res.status(404).json({ message: 'Course not found' });
    }
    res.json(result[0]);
  });
});

// Starting the server
app.listen(PORT, () => {
  console.log(`JSON API server is running on http://localhost:${PORT}`);
});
