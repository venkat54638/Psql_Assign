# Psql_Assign
minfy_db=> CREATE TABLE students(
minfy_db(> student_id INTEGER,
minfy_db(> first_name VARCHAR(50),
minfy_db(> last_name VARCHAR(50),
minfy_db(> email VARCHAR(100),
minfy_db(> date_of_birth DATE );
CREATE TABLE
minfy_db=> \\dt

minfy_db=> \d students
                         Table "public.students"
    Column     |          Type          | Collation | Nullable | Default
---------------+------------------------+-----------+----------+---------
 student_id    | integer                |           |          |
 first_name    | character varying(50)  |           |          |
 last_name     | character varying(50)  |           |          |
 email         | character varying(100) |           |          |
 date_of_birth | date                   |           |          |


minfy_db=> ALTER TABLE students ADD COLUMN enrollment_date DATE;
ALTER TABLE
minfy_db=> \d students
                          Table "public.students"
     Column      |          Type          | Collation | Nullable | Default
-----------------+------------------------+-----------+----------+---------
 student_id      | integer                |           |          |
 first_name      | character varying(50)  |           |          |
 last_name       | character varying(50)  |           |          |
 email           | character varying(100) |           |          |
 date_of_birth   | date                   |           |          |
 enrollment_date | date                   |           |          |


minfy_db=> ALTER TABLE students ADD COLUMN phone_number VARCHAR(20);
ALTER TABLE
minfy_db=> ALTER TABLE students DROP COLUMN phone_number VARCHAR(20);
ERROR:  syntax error at or near "VARCHAR"
LINE 1: ALTER TABLE students DROP COLUMN phone_number VARCHAR(20);
                                                      ^
minfy_db=> ALTER TABLE students DROP COLUMN phone_number;
ALTER TABLE
minfy_db=> INSERT INTO students (student_id, first_name, last_name, email, dob)
minfy_db-> VALUES (1, 'Alice', 'Smith', 'alice.smith@example.com', '2003-05-15');
ERROR:  column "dob" of relation "students" does not exist
LINE 1: ...NTO students (student_id, first_name, last_name, email, dob)
                                                                   ^
minfy_db=>
minfy_db=> INSERT INTO students (student_id, first_name, last_name, email, dob)
minfy_db-> VALUES (2, 'Bob', 'Johnson', 'bob.johnson@example.com', '2002-08-22'),
minfy_db->        (3, 'Charlie', 'Brown', 'charlie.brown@example.com', '2003-01-10');
ERROR:  column "dob" of relation "students" does not exist
LINE 1: ...NTO students (student_id, first_name, last_name, email, dob)
                                                                   ^
minfy_db=> INSERT INTO students (student_id, first_name, last_name, email, dob)
minfy_db-> VALUES (1, 'Alice', 'Smith', 'alice.smith@example.com', '2003-05-15');
ERROR:  column "dob" of relation "students" does not exist
LINE 1: ...NTO students (student_id, first_name, last_name, email, dob)
                                                                   ^
minfy_db=> INSERT INTO students (student_id, first_name, last_name, email, date_of_brith)
minfy_db-> VALUES (1, 'Alice', 'Smith', 'alice.smith@example.com', '2003-05-15');
ERROR:  column "date_of_brith" of relation "students" does not exist
LINE 1: ...udents (student_id, first_name, last_name, email, date_of_br...
                                                             ^
minfy_db=> INSERT INTO students (student_id, first_name, last_name, email, date_of_birth)
minfy_db-> VALUES (1, 'Alice', 'Smith', 'alice.smith@example.com', '2003-05-15');
INSERT 0 1
minfy_db=> INSERT INTO students (student_id, first_name, last_name, email, date_of_birth)
minfy_db-> VALUES (2, 'Bob', 'Johnson', 'bob.johnson@example.com', '2002-08-22'),
minfy_db->        (3, 'Charlie', 'Brown', 'charlie.brown@example.com', '2003-01-10');
INSERT 0 2
minfy_db=> INSERT INTO students (student_id, first_name, last_name, email, date_of_birth)
minfy_db-> INSERT INTO students (student_id, first_name, last_name, email, date_of_birth)
minfy_db-> VALUES (3, 'Charlie', 'Brown', 'charlie.brown@example.com', '2003-01-10');
ERROR:  syntax error at or near "INSERT"
LINE 2: INSERT INTO students (student_id, first_name, last_name, ema...
        ^
minfy_db=> INSERT INTO students (student_id, first_name, last_name, email, date_of_birth)
minfy_db-> VALUES (3, 'Charlie', 'Brown', 'charlie.brown@example.com', '2003-01-10');
INSERT 0 1
minfy_db=> \d students
                          Table "public.students"
     Column      |          Type          | Collation | Nullable | Default
-----------------+------------------------+-----------+----------+---------
 student_id      | integer                |           |          |
 first_name      | character varying(50)  |           |          |
 last_name       | character varying(50)  |           |          |
 email           | character varying(100) |           |          |
 date_of_birth   | date                   |           |          |
 enrollment_date | date                   |           |          |


minfy_db=> SELECT first_name, last_name, email FROM students;
 first_name | last_name |           email
------------+-----------+---------------------------
 Alice      | Smith     | alice.smith@example.com
 Bob        | Johnson   | bob.johnson@example.com
 Charlie    | Brown     | charlie.brown@example.com
 Charlie    | Brown     | charlie.brown@example.com
(4 rows)


minfy_db=> SELECT * FROM students;
 student_id | first_name | last_name |           email           | date_of_birth | enrollment_date
------------+------------+-----------+---------------------------+---------------+-----------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15    |
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22    |
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10    |
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10    |
(4 rows)


minfy_db=> INSERT INTO students (student_id, first_name, last_name, dob) VALUES (4, 'Diana', 'Prince', '2001-11-01');
ERROR:  column "dob" of relation "students" does not exist
LINE 1: ...INTO students (student_id, first_name, last_name, dob) VALUE...
                                                             ^
minfy_db=> INSERT INTO students (student_id, first_name, last_name, date_of_birth) VALUES (4, 'Diana', 'Prince', '2001-11-01');
INSERT 0 1
minfy_db=> SELECT *
minfy_db-> FROM students
minfy_db-> WHERE student_id = 2.33;
 student_id | first_name | last_name | email | date_of_birth | enrollment_date
------------+------------+-----------+-------+---------------+-----------------
(0 rows)


minfy_db=> SELECT *
minfy_db-> FROM students
minfy_db-> WHERE birthdate < '2003-01-01';
ERROR:  column "birthdate" does not exist
LINE 3: WHERE birthdate < '2003-01-01';
              ^
minfy_db=> SELECT *
minfy_db-> FROM students
minfy_db-> WHERE date_of_birth < '2003-01-01';
 student_id | first_name | last_name |          email          | date_of_birth | enrollment_date
------------+------------+-----------+-------------------------+---------------+-----------------
          2 | Bob        | Johnson   | bob.johnson@example.com | 2002-08-22    |
          4 | Diana      | Prince    |                         | 2001-11-01    |
(2 rows)


minfy_db=> SELECT *
minfy_db-> FROM students
minfy_db-> WHERE first_name LIKE 'B%' OR first_name LIKE 'C%';
 student_id | first_name | last_name |           email           | date_of_birth | enrollment_date
------------+------------+-----------+---------------------------+---------------+-----------------
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22    |
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10    |
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10    |
(3 rows)


minfy_db=> SELECT *
minfy_db-> FROM students
minfy_db-> WHERE email LIKE '%@example.com';
 student_id | first_name | last_name |           email           | date_of_birth | enrollment_date
------------+------------+-----------+---------------------------+---------------+-----------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15    |
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22    |
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10    |
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10    |
(4 rows)


minfy_db=> SELECT *
minfy_db-> FROM students
minfy_db-> WHERE email IS NULL OR email = '';
 student_id | first_name | last_name | email | date_of_birth | enrollment_date
------------+------------+-----------+-------+---------------+-----------------
          4 | Diana      | Prince    |       | 2001-11-01    |
(1 row)


minfy_db=>
minfy_db=> UPDATE students
minfy_db-> SET email = 'alices@example.net'
minfy_db-> WHERE student_id = 1;
UPDATE 1
minfy_db=> UPDATE students
minfy_db-> SET first_name = 'Robert', email = 'robert.j@example.com'
minfy_db-> WHERE student_id = 2;
UPDATE 1
minfy_db=>
minfy_db=> SELECT * FROM students WHERE student_id IN (1,2);
 student_id | first_name | last_name |        email         | date_of_birth | enrollment_date
------------+------------+-----------+----------------------+---------------+-----------------
          1 | Alice      | Smith     | alices@example.net   | 2003-05-15    |
          2 | Robert     | Johnson   | robert.j@example.com | 2002-08-22    |
(2 rows)


minfy_db=> UPDATE students
minfy_db-> SET birthdate = '2003-02-15'
minfy_db-> WHERE first_name = 'Charlie' AND last_name = 'Brown';
ERROR:  column "birthdate" of relation "students" does not exist
LINE 2: SET birthdate = '2003-02-15'
            ^
minfy_db=> UPDATE students
minfy_db-> SET date_of_birth = '2003-02-15'
minfy_db-> WHERE first_name = 'Charlie' AND last_name = 'Brown';
UPDATE 2
minfy_db=> UPDATE students
minfy_db-> SET email = 'diana.prince@example.org'
minfy_db-> WHERE student_id = 4;
UPDATE 1
minfy_db=> SELECT *
minfy_db-> SELECT * FROM students
minfy_db->
minfy_db-> WHERE student_id = 4;
ERROR:  syntax error at or near "SELECT"
LINE 2: SELECT * FROM students
        ^
minfy_db=> SELECT * FROM students;
 student_id | first_name | last_name |           email           | date_of_birth | enrollment_date
------------+------------+-----------+---------------------------+---------------+-----------------
          1 | Alice      | Smith     | alices@example.net        | 2003-05-15    |
          2 | Robert     | Johnson   | robert.j@example.com      | 2002-08-22    |
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-02-15    |
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-02-15    |
          4 | Diana      | Prince    | diana.prince@example.org  | 2001-11-01    |
(5 rows)


minfy_db=> SELECT *
minfy_db-> FROM students
minfy_db-> ORDER BY birthdate ASC
minfy_db-> LIMIT 2;
ERROR:  column "birthdate" does not exist
LINE 3: ORDER BY birthdate ASC
                 ^
minfy_db=> SELECT *
minfy_db-> FROM students
minfy_db-> ORDER BY birthdate ASC
minfy_db-> LIMIT 2;
ERROR:  column "birthdate" does not exist
LINE 3: ORDER BY birthdate ASC
                 ^
minfy_db=> ORDER BY date_of_birth ASC
minfy_db-> SELECT *
minfy_db-> SELECT *
minfy_db->
minfy_db-> SELECT *
minfy_db->
minfy_db->
minfy_db-> ORDER BY birthdate ASC
minfy_db-> SELECT *
minfy_db-> FROM students
minfy_db-> ORDER BY birthdate ASC
minfy_db-> LIMIT 2;
ERROR:  syntax error at or near "ORDER"
LINE 1: ORDER BY date_of_birth ASC
        ^
minfy_db=> SELECT *
minfy_db-> FROM students
minfy_db-> ORDER BY birthdate ASC
minfy_db-> LIMIT 2;
ERROR:  column "birthdate" does not exist
LINE 3: ORDER BY birthdate ASC
                 ^
minfy_db=> SELECT *FROM studentsORDER BY date_of_birth ASCLIMIT 2;
ERROR:  syntax error at or near "date_of_birth"
LINE 1: SELECT *FROM studentsORDER BY date_of_birth ASCLIMIT 2;
                                      ^
minfy_db=> SELECT *
minfy_db-> FROM students
minfy_db-> ORDER BY date_of_birth ASC
minfy_db-> LIMIT 2;
 student_id | first_name | last_name |          email           | date_of_birth | enrollment_date
------------+------------+-----------+--------------------------+---------------+-----------------
          4 | Diana      | Prince    | diana.prince@example.org | 2001-11-01    |
          2 | Robert     | Johnson   | robert.j@example.com     | 2002-08-22    |
(2 rows)


minfy_db=> SELECT *
minfy_db-> FROM students
minfy_db-> ORDER BY student_id
minfy_db-> OFFSET 1
minfy_db-> LIMIT 2;
 student_id | first_name | last_name |           email           | date_of_birth | enrollment_date
------------+------------+-----------+---------------------------+---------------+-----------------
          2 | Robert     | Johnson   | robert.j@example.com      | 2002-08-22    |
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-02-15    |
(2 rows)


minfy_db=> SELECT DISTINCT birthdate
minfy_db-> FROM students
minfy_db-> ORDER BY birthdate;
ERROR:  column "birthdate" does not exist
LINE 1: SELECT DISTINCT birthdate
                        ^
minfy_db=> SELECT DISTINCT birthdate
minfy_db-> FROM students
minfy_db-> ORDER BY date_of_birth;
ERROR:  column "birthdate" does not exist
LINE 1: SELECT DISTINCT birthdate
                        ^
minfy_db=> SELECT DISTINCT date_of_birth
minfy_db-> FROM students
minfy_db-> ORDER BY date_of_birth;
 date_of_birth
---------------
 2001-11-01
 2002-08-22
 2003-02-15
 2003-05-15
(4 rows)


minfy_db=> SELECT DISTINCT EXTRACT(YEAR FROM date_of_birth) AS birth_year
minfy_db-> FROM students
minfy_db-> ORDER BY birth_year;
 birth_year
------------
       2001
       2002
       2003
(3 rows)


minfy_db=> SELECT COUNT(*) AS total_students
minfy_db-> FROM students;
 total_students
----------------
              5
(1 row)


minfy_db=> SELECT MIN(date_of_birth) AS earliest_birthdate
minfy_db-> FROM students;
 earliest_birthdate
--------------------
 2001-11-01
(1 row)


minfy_db=> SELECT COUNT(DISTINCT last_name) AS distinct_last_names
minfy_db-> FROM students;
 distinct_last_names
---------------------
                   4
(1 row)


minfy_db=> SELECT * FROM students
minfy_db-> SELECT * FROM students;
ERROR:  syntax error at or near "SELECT"
LINE 2: SELECT * FROM students;
        ^
minfy_db=> SELECT * FROM students;
 student_id | first_name | last_name |           email           | date_of_birth | enrollment_date
------------+------------+-----------+---------------------------+---------------+-----------------
          1 | Alice      | Smith     | alices@example.net        | 2003-05-15    |
          2 | Robert     | Johnson   | robert.j@example.com      | 2002-08-22    |
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-02-15    |
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-02-15    |
          4 | Diana      | Prince    | diana.prince@example.org  | 2001-11-01    |
(5 rows)


minfy_db=> SELECT student_id, first_name, last_name, email, date_of_birth, COUNT(*)
minfy_db-> FROM students
minfy_db-> GROUP BY student_id, first_name, last_name, email, date_of_birth
minfy_db-> HAVING COUNT(*) > 1;
 student_id | first_name | last_name |           email           | date_of_birth | count
------------+------------+-----------+---------------------------+---------------+-------
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-02-15    |     2
(1 row)


minfy_db=> WITH duplicates AS (
minfy_db(>   SELECT ctid,
minfy_db(>          ROW_NUMBER() OVER (
minfy_db(>            PARTITION BY student_id, first_name, last_name, email, date_of_birth
minfy_db(>            ORDER BY ctid
minfy_db(>          ) AS rn
minfy_db(>   FROM students
minfy_db(> )
minfy_db-> DELETE FROM students
minfy_db-> WHERE ctid IN (
minfy_db(>   SELECT ctid FROM duplicates WHERE rn > 1
minfy_db(> );
DELETE 1
minfy_db=> SELECT * FROM students;
 student_id | first_name | last_name |           email           | date_of_birth | enrollment_date
------------+------------+-----------+---------------------------+---------------+-----------------
          1 | Alice      | Smith     | alices@example.net        | 2003-05-15    |
          2 | Robert     | Johnson   | robert.j@example.com      | 2002-08-22    |
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-02-15    |
          4 | Diana      | Prince    | diana.prince@example.org  | 2001-11-01    |
(4 rows)


minfy_db=> - Count the number of students for each distinct `last_name`.
minfy_db->
minfy_db-> count ;
ERROR:  syntax error at or near "-"
LINE 1: - Count the number of students for each distinct `last_name`...
        ^
minfy_db=> SELECT last_name, COUNT(*) AS student_count
minfy_db-> FROM students
minfy_db-> GROUP BY last_name
minfy_db-> ORDER BY student_count DESC;  -- optional: order by count, largest first
 last_name | student_count
-----------+---------------
 Smith     |             1
 Johnson   |             1
 Prince    |             1
 Brown     |             1
(4 rows)


minfy_db=> SELECT EXTRACT(YEAR FROM date_of_birth) AS birth_year, COUNT(*) AS student_count
minfy_db-> FROM students
minfy_db-> GROUP BY birth_year
minfy_db-> ORDER BY birth_year;
 birth_year | student_count
------------+---------------
       2001 |             1
       2002 |             1
       2003 |             2
(3 rows)


minfy_db=> SELECT first_name, COUNT(*) AS student_count
minfy_db-> FROM students
minfy_db-> GROUP BY first_name
minfy_db-> ORDER BY student_count DESC;  -- optional: show the most common names first
 first_name | student_count
------------+---------------
 Robert     |             1
 Alice      |             1
 Charlie    |             1
 Diana      |             1
(4 rows)


minfy_db=> DROP TABLE IF EXISTS students;
DROP TABLE
minfy_db=> CREATE TABLE students (
minfy_db(>     student_id SERIAL PRIMARY KEY,
minfy_db(>     first_name VARCHAR(50) NOT NULL,
minfy_db(>     last_name VARCHAR(50) NOT NULL,
minfy_db(>     email VARCHAR(100) UNIQUE,
minfy_db(>     date_of_birth DATE,
minfy_db(>     enrollment_date DATE
minfy_db(> );
CREATE TABLE
minfy_db=> INSERT INTO students (first_name, last_name, email, date_of_birth)
minfy_db-> VALUES ('Alice', 'Smith', 'alice@example.com', '2003-05-15');
INSERT 0 1
minfy_db=> INSERT INTO students (student_id, first_name, last_name, email, date_of_birth)
minfy_db-> VALUES (2, 'Another', 'User', 'test@test.com', '2001-01-01');
INSERT 0 1
minfy_db=> INSERT INTO students (student_id, first_name, last_name, email, date_of_birth, enrollment_status)
minfy_db-> VALUES (2, 'Another', 'User', 'another@test.com', '2001-01-01', 'pending');
ERROR:  column "enrollment_status" of relation "students" does not exist
LINE 1: ..._id, first_name, last_name, email, date_of_birth, enrollment...
                                                             ^
minfy_db=> DROP TABLE IF EXISTS students;
DROP TABLE
minfy_db=>
minfy_db=> CREATE TABLE students (
minfy_db(>     student_id SERIAL PRIMARY KEY,
minfy_db(>     first_name VARCHAR(50) NOT NULL,
minfy_db(>     last_name VARCHAR(50) NOT NULL,
minfy_db(>     email VARCHAR(100) UNIQUE,
minfy_db(>     date_of_birth DATE
minfy_db(> );
CREATE TABLE
minfy_db=> INSERT INTO students (first_name, last_name, date_of_birth)
minfy_db-> VALUES ('Emily', 'Clark', '2004-03-20');
INSERT 0 1
minfy_db=> INSERT INTO students (first_name, last_name, email, date_of_birth)
minfy_db-> VALUES ('Mark', 'Taylor', 'emily@example.com', '2003-07-15');
INSERT 0 1
minfy_db=> INSERT INTO students (last_name, email, date_of_birth)
minfy_db-> VALUES ('Davis', 'davis@example.com', '2002-12-01');
ERROR:  null value in column "first_name" of relation "students" violates not-null constraint
DETAIL:  Failing row contains (3, null, Davis, davis@example.com, 2002-12-01).
minfy_db=> SELECT * FROM students ORDER BY student_id;
 student_id | first_name | last_name |       email       | date_of_birth
------------+------------+-----------+-------------------+---------------
          1 | Emily      | Clark     |                   | 2004-03-20
          2 | Mark       | Taylor    | emily@example.com | 2003-07-15
(2 rows)


minfy_db=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
minfy_db-> VALUES ('Alice', 'Smith', 'alice.smith@example.com', '2003-05-15', 'enrolled');
ERROR:  column "dob" of relation "students" does not exist
LINE 1: ...SERT INTO students (first_name, last_name, email, dob, enrol...
                                                             ^
minfy_db=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
minfy_db-> VALUES ('Robert', 'Johnson', 'robert.j@example.com', '2002-08-22', 'enrolled');
ERROR:  column "dob" of relation "students" does not exist
LINE 1: ...SERT INTO students (first_name, last_name, email, dob, enrol...
                                                             ^
minfy_db=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
minfy_db-> VALUES ('Charlie', 'Brown', 'charlie.brown@example.com', '2003-01-10', 'pending');
ERROR:  column "dob" of relation "students" does not exist
LINE 1: ...SERT INTO students (first_name, last_name, email, dob, enrol...
                                                             ^
minfy_db=> INSERT INTO students (first_name, last_name, email, date_of_birth, enrollment_status)
minfy_db-> VALUES ('Alice', 'Smith', 'alice.smith@example.com', '2003-05-15', 'enrolled');
ERROR:  column "enrollment_status" of relation "students" does not exist
LINE 1: ...nts (first_name, last_name, email, date_of_birth, enrollment...
                                                             ^
minfy_db=>
minfy_db=> INSERT INTO students (first_name, last_name, email, date_of_birth, enrollment_status)
minfy_db-> VALUES ('Robert', 'Johnson', 'robert.j@example.com', '2002-08-22', 'enrolled');
ERROR:  column "enrollment_status" of relation "students" does not exist
LINE 1: ...nts (first_name, last_name, email, date_of_birth, enrollment...
                                                             ^
minfy_db=>
minfy_db=> INSERT INTO students (first_name, last_name, email, date_of_birth, enrollment_status)
minfy_db-> VALUES ('Charlie', 'Brown', 'charlie.brown@example.com', '2003-01-10', 'pending');
ERROR:  column "enrollment_status" of relation "students" does not exist
LINE 1: ...nts (first_name, last_name, email, date_of_birth, enrollment...
                                                             ^
minfy_db=> INSERT INTO students (first_name, last_name, email, date_of_birth, enrollment_status)
minfy_db-> VALUES ('Charlie', 'Brown', 'charlie.brown@example.com', '2003-01-10', 'pending');
ERROR:  column "enrollment_status" of relation "students" does not exist
LINE 1: ...nts (first_name, last_name, email, date_of_birth, enrollment...
                                                             ^
minfy_db=> INSERT INTO students (first_name, last_name, email, date_of_birth)
minfy_db-> VALUES ('Charlie', 'Brown', 'charlie.brown@example.com', '2003-01-10');
INSERT 0 1
minfy_db=> VALUES ('Robert', 'Johnson', 'robert.j@example.com', '2002-08-22');
 column1 | column2 |       column3        |  column4
---------+---------+----------------------+------------
 Robert  | Johnson | robert.j@example.com | 2002-08-22
(1 row)


minfy_db=> INSERT INTO students (first_name, last_name, email, date_of_birth)
minfy_db-> VALUES ('Robert', 'Johnson', 'robert.j@example.com', '2002-08-22');
INSERT 0 1
minfy_db=> INSERT INTO students (first_name, last_name, email, date_of_birth)
minfy_db-> VALUES ('Alice', 'Smith', 'alice.smith@example.com', '2003-05-15');
INSERT 0 1
minfy_db=> SELECT * FROM students;
 student_id | first_name | last_name |           email           | date_of_birth
------------+------------+-----------+---------------------------+---------------
          1 | Emily      | Clark     |                           | 2004-03-20
          2 | Mark       | Taylor    | emily@example.com         | 2003-07-15
          4 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          5 | Robert     | Johnson   | robert.j@example.com      | 2002-08-22
          6 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
(5 rows)


minfy_db=> CREATE TABLE courses (
minfy_db(>     course_id SERIAL PRIMARY KEY,
minfy_db(>     course_name VARCHAR(100) NOT NULL UNIQUE,
minfy_db(>     credits INTEGER CHECK (credits > 0 AND credits < 10) -- Example of CHECK
minfy_db(> );
CREATE TABLE
minfy_db=>
minfy_db=> INSERT INTO courses (course_name, credits) VALUES ('Introduction to SQL', 3);
INSERT 0 1
minfy_db=> INSERT INTO courses (course_name, credits) VALUES ('Database Design', 4);
INSERT 0 1
minfy_db=> INSERT INTO courses (course_name, credits) VALUES ('Web Development', 3);
INSERT 0 1
minfy_db=> INSERT INTO courses (course_name, credits) VALUES ('Data Structures', 4);
INSERT 0 1
minfy_db=> CREATE TABLE enrollments (
minfy_db(>     enrollment_id SERIAL PRIMARY KEY,
minfy_db(>     student_id INTEGER NOT NULL,
minfy_db(>     course_id INTEGER NOT NULL,
minfy_db(>     enrollment_date DATE DEFAULT CURRENT_DATE, -- Sets default if not specified
minfy_db(>     grade CHAR(1) CHECK (grade IN ('A', 'B', 'C', 'D', 'F', 'W', NULL)), -- W for withdraw, NULL if not graded
minfy_db(>
minfy_db(>     -- Foreign Key constraint for student_id
minfy_db(>     CONSTRAINT fk_student
minfy_db(>         FOREIGN KEY (student_id)
minfy_db(>         REFERENCES students(student_id)
minfy_db(>         ON DELETE CASCADE, -- If a student is deleted, their enrollments are also deleted.
minfy_db(>                            -- Other options: ON DELETE RESTRICT, ON DELETE SET NULL, ON DELETE SET DEFAULT
minfy_db(>
minfy_db(>     -- Foreign Key constraint for course_id
minfy_db(>     CONSTRAINT fk_course
minfy_db(>         FOREIGN KEY (course_id)
minfy_db(>         REFERENCES courses(course_id)
minfy_db(>         ON DELETE RESTRICT, -- (Default if not specified) Prevent deleting a course if students are enrolled.
minfy_db(>
minfy_db(>     -- Ensure a student cannot enroll in the same course multiple times (if semester isn't a factor)
minfy_db(>     UNIQUE (student_id, course_id)
minfy_db(> );
CREATE TABLE
minfy_db=> SELECT * FROM courses
minfy_db-> SELECT * FROM courses ;
ERROR:  syntax error at or near "SELECT"
LINE 2: SELECT * FROM courses ;
        ^
minfy_db=> SELECT * FROM courses;
 course_id |     course_name     | credits
-----------+---------------------+---------
         1 | Introduction to SQL |       3
         2 | Database Design     |       4
         3 | Web Development     |       3
         4 | Data Structures     |       4
(4 rows)


minfy_db=> SELECT * FROM enrollments;
 enrollment_id | student_id | course_id | enrollment_date | grade
---------------+------------+-----------+-----------------+-------
(0 rows)


minfy_db=> INSERT INTO enrollments (student_id, course_id, grade) VALUES (1, 1, 'A');
INSERT 0 1
minfy_db=> INSERT INTO enrollments (student_id, course_id) VALUES (1, 2);
INSERT 0 1
minfy_db=> SELECT * FROM enrollments;
 enrollment_id | student_id | course_id | enrollment_date | grade
---------------+------------+-----------+-----------------+-------
             1 |          1 |         1 | 2025-05-30      | A
             2 |          1 |         2 | 2025-05-30      |
(2 rows)


minfy_db=> INSERT INTO enrollments (student_id, course_id, grade) VALUES (999, 1, 'A');
ERROR:  insert or update on table "enrollments" violates foreign key constraint "fk_student"
DETAIL:  Key (student_id)=(999) is not present in table "students".
minfy_db=> -- Expected: ERROR: insert or update on table "enrollments" violates foreign key constraint
minfy_db=> -- student_id 999 does not exist
minfy_db=> INSERT INTO enrollments (student_id, course_id, grade)
minfy_db-> VALUES (999, 1, 'A');
ERROR:  insert or update on table "enrollments" violates foreign key constraint "fk_student"
DETAIL:  Key (student_id)=(999) is not present in table "students".
minfy_db=> -- 🔴 Expected error: violates foreign key constraint "fk_student"
minfy_db=> -- course_id 999 does not exist
minfy_db=> INSERT INTO enrollments (student_id, course_id, grade)
minfy_db-> VALUES (1, 999, 'A');
ERROR:  insert or update on table "enrollments" violates foreign key constraint "fk_course"
DETAIL:  Key (course_id)=(999) is not present in table "courses".
minfy_db=> -- 🔴 Expected error: violates foreign key constraint "fk_course"
minfy_db=> INSERT INTO enrollments (student_id, course_id, grade)
minfy_db-> VALUES (1, 1, 'A');  -- Introduction to SQL
ERROR:  duplicate key value violates unique constraint "enrollments_student_id_course_id_key"
DETAIL:  Key (student_id, course_id)=(1, 1) already exists.
minfy_db=>
minfy_db=> INSERT INTO enrollments (student_id, course_id)
minfy_db-> VALUES (1, 2);       -- Database Design, grade = NULL
ERROR:  duplicate key value violates unique constraint "enrollments_student_id_course_id_key"
DETAIL:  Key (student_id, course_id)=(1, 2) already exists.
minfy_db=> INSERT INTO enrollments (student_id, course_id, grade)
minfy_db-> VALUES (2, 1, 'B');  -- Introduction to SQL
INSERT 0 1
minfy_db=> SELECT * FROM students WHERE student_id = 1;
 student_id | first_name | last_name | email | date_of_birth
------------+------------+-----------+-------+---------------
          1 | Emily      | Clark     |       | 2004-03-20
(1 row)


minfy_db=> SELECT * FROM enrollments WHERE student_id = 1;
 enrollment_id | student_id | course_id | enrollment_date | grade
---------------+------------+-----------+-----------------+-------
             1 |          1 |         1 | 2025-05-30      | A
             2 |          1 |         2 | 2025-05-30      |
(2 rows)


minfy_db=> DELETE FROM students WHERE student_id = 1;
DELETE 1
minfy_db=> SELECT * FROM students WHERE student_id = 1;
 student_id | first_name | last_name | email | date_of_birth
------------+------------+-----------+-------+---------------
(0 rows)


minfy_db=> SELECT * FROM enrollments WHERE student_id = 1;
 enrollment_id | student_id | course_id | enrollment_date | grade
---------------+------------+-----------+-----------------+-------
(0 rows)
