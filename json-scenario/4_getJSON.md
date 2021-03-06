Now that the table is ready, we can insert the data sets from the first step. We need to create an entry for both John
and Mary.

Let's start by opening the JSON-file for Johns grades:

`grades_john.json`{{open}}

The file has already been populated with values, but feel free to adjust the grades and maybe even add classes. **Please
don't remove the '*Database II*' entry since we're going to use it in the next step!**

Same goes for Marys grades: `grades_mary.json`{{open}}

# Inserting data

If you are done manipulating the grade files to your liking, we can start inserting the two data points into the table.
To retrieve the JSON content from the files, we are using a temporary variable and the command-line tool `cat`. Since
our primary key *user_id* is generated automatically, we don't need to specify it.

```postgresql
\set grades_john `cat /root/grades_john.json`

INSERT INTO students (first_name, last_name, password, grades)
VALUES ('John', 'Doe', 'admin', :'grades_john');
```{{execute}}

Let's do the same for Mary:

```postgresql
\set grades_mary `cat /root/grades_mary.json`

INSERT INTO students (first_name, last_name, password, grades)
VALUES ('Mary', 'Poppins', 'umbrella1234', :'grades_mary');
```{{execute}}

# Retrieving JSON

To retrieve the data and handle it in your application of choice, you can use a simple `SELECT` statement:

`SELECT grades FROM students WHERE user_id=2;`{{execute}}

Executing this statement will print the JSON of Marys grades.
