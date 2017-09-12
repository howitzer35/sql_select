1.
 
mysql> select first_name, last_name from student;
+------------+-----------+
| first_name | last_name |
+------------+-----------+
| Eric       | Ephram    |
| Greg       | Gould     |
| Adam       | Ant       |
| Howard     | Hess      |
| Charles    | Caldwell  |
| James      | Joyce     |
| Doug       | Dumas     |
| Kevin      | Kraft     |
| Frank      | Fountain  |
| Brian      | Biggs     |
+------------+-----------+
10 rows in set (0.00 sec)
 
 
2.
 
mysql> select * 
    -> from 
    -> student
    -> WHERE years_of_experience <8;
+------------+------------+-----------+---------------------+------------+
| student_id | first_name | last_name | years_of_experience | start_date |
+------------+------------+-----------+---------------------+------------+
|          1 | Eric       | Ephram    |                   2 | 2016-03-31 |
|          2 | Greg       | Gould     |                   6 | 2016-09-30 |
|          3 | Adam       | Ant       |                   5 | 2016-06-02 |
|          4 | Howard     | Hess      |                   1 | 2016-02-28 |
|          5 | Charles    | Caldwell  |                   7 | 2016-05-07 |
|          8 | Kevin      | Kraft     |                   3 | 2016-04-15 |
|         10 | Brian      | Biggs     |                   4 | 2015-12-25 |
+------------+-----------
 
 
3.
 
mysql> SELECT
    -> last_name, start_date, student_ID
    -> FROM
    -> student
    -> ORDER BY last_name ASC;
+-----------+------------+------------+
| last_name | start_date | student_ID |
+-----------+------------+------------+
| Ant       | 2016-06-02 |          3 |
| Biggs     | 2015-12-25 |         10 |
| Caldwell  | 2016-05-07 |          5 |
| Dumas     | 2016-07-04 |          7 |
| Ephram    | 2016-03-31 |          1 |
| Fountain  | 2016-01-31 |          9 |
| Gould     | 2016-09-30 |          2 |
| Hess      | 2016-02-28 |          4 |
| Joyce     | 2016-08-27 |          6 |
| Kraft     | 2016-04-15 |          8 |
+-----------+------------+------------+
10 rows in set (0.00 sec)
 
 
4.
 
mysql> SELECT *
    -> FROM student
    -> WHERE first_name IN ("Adam", "James", "Frank")
    -> ORDER BY last_name DESC;  
+------------+------------+-----------+---------------------+------------+
| student_id | first_name | last_name | years_of_experience | start_date |
+------------+------------+-----------+---------------------+------------+
|          6 | James      | Joyce     |                   9 | 2016-08-27 |
|          9 | Frank      | Fountain  |                   8 | 2016-01-31 |
|          3 | Adam       | Ant       |                   5 | 2016-06-02 |
+------------+------------+-----------+---------------------+------------+
3 rows in set (0.00 sec)
 
 
5.
 
mysql> SELECT 
    -> first_name, last_name, start_date
    -> FROM 
    -> student
    -> WHERE start_date BETWEEN "2016-01-01" AND "2016-06-30"
    -> ORDER BY start_date DESC;
+------------+-----------+------------+
| first_name | last_name | start_date |
+------------+-----------+------------+
| Adam       | Ant       | 2016-06-02 |
| Charles    | Caldwell  | 2016-05-07 |
| Kevin      | Kraft     | 2016-04-15 |
| Eric       | Ephram    | 2016-03-31 |
| Howard     | Hess      | 2016-02-28 |
| Frank      | Fountain  | 2016-01-31 |
+------------+-----------+------------+
6 rows in set (0.00 sec)


















MEDIUM

mysql> CREATE TABLE `assignment` (
    ->   `assignment_id` int(11) unsigned NOT NULL AUTO_INCREMENT,
    ->   `student_id` int(11) NOT NULL,
    ->   `assignment_nbr` int(11) NOT NULL,
    ->   `grade` varchar(30) DEFAULT NULL,
    ->   `class_id` int(11) DEFAULT NULL,
    ->   PRIMARY KEY (`assignment_id`)
    -> ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
Query OK, 0 rows affected (0.01 sec)

mysql> alter table assignment drop column grade;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> alter table assignment add column grade_id int;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> explain assignment
    -> ;
+----------------+------------------+------+-----+---------+----------------+
| Field          | Type             | Null | Key | Default | Extra          |
+----------------+------------------+------+-----+---------+----------------+
| assignment_id  | int(11) unsigned | NO   | PRI | NULL    | auto_increment |
| student_id     | int(11)          | NO   |     | NULL    |                |
| assignment_nbr | int(11)          | NO   |     | NULL    |                |
| class_id       | int(11)          | YES  |     | NULL    |                |
| grade_id       | int(11)          | YES  |     | NULL    |                |
+----------------+------------------+------+-----+---------+----------------+
5 rows in set (0.00 sec)



mysql> CREATE TABLE grade (
    -> grade_id int PRIMARY KEY
    -> ,
    -> grade_description VARCHAR(50) NOT NULL
    -> );
Query OK, 0 rows affected (0.01 sec)



mysql> explain grade
    -> ;
+-------------------+-------------+------+-----+---------+-------+
| Field             | Type        | Null | Key | Default | Extra |
+-------------------+-------------+------+-----+---------+-------+
| grade_id          | int(11)     | NO   | PRI | NULL    |       |
| grade_description | varchar(50) | NO   |     | NULL    |       |
+-------------------+-------------+------+-----+---------+-------+
2 rows in set (0.00 sec)


mysql> drop table grade;
Query OK, 0 rows affected (0.01 sec)



mysql> CREATE TABLE grade (
    -> grade_id int PRIMARY KEY AUTO_INCREMENT,
    -> grade_description VARCHAR(50) NOT NULL
    -> );
Query OK, 0 rows affected (0.02 sec)



mysql> explain grade
    -> ;
+-------------------+-------------+------+-----+---------+----------------+
| Field             | Type        | Null | Key | Default | Extra          |
+-------------------+-------------+------+-----+---------+----------------+
| grade_id          | int(11)     | NO   | PRI | NULL    | auto_increment |
| grade_description | varchar(50) | NO   |     | NULL    |                |
+-------------------+-------------+------+-----+---------+----------------+
2 rows in set (0.00 sec)



mysql> INSERT INTO grade (grade_description) VALUES (
    -> "incomplete"
    -> );
Query OK, 1 row affected (0.01 sec)


mysql> INSERT INTO grade (grade_description) VALUES ( "complete and unsatisfactory");
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO grade (grade_description) VALUES ( "complete and satisfactory");
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO grade (grade_description) VALUES ( "exceeds expectations");
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO grade (grade_description) VALUES ( "not graded");
Query OK, 1 row affected (0.00 sec)



mysql> explain grade
    -> ;
+-------------------+-------------+------+-----+---------+----------------+
| Field             | Type        | Null | Key | Default | Extra          |
+-------------------+-------------+------+-----+---------+----------------+
| grade_id          | int(11)     | NO   | PRI | NULL    | auto_increment |
| grade_description | varchar(50) | NO   |     | NULL    |                |
+-------------------+-------------+------+-----+---------+----------------+
2 rows in set (0.00 sec)



mysql> select *
    -> from grade;
+----------+-----------------------------+
| grade_id | grade_description           |
+----------+-----------------------------+
|        1 | incomplete                  |
|        2 | complete and unsatisfactory |
|        3 | complete and satisfactory   |
|        4 | exceeds expectations        |
|        5 | not graded                  |
+----------+-----------------------------+
5 rows in set (0.00 sec)



mysql> CREATE INDEX index_grade_id
    -> ON assignment(grade_id);
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0



mysql> ALTER TABLE assignment
    -> ADD CONSTRAINT fk_grade_id
    -> FOREIGN KEY (grade_id) REFERENCES grade(grade_id);
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0



mysql> select *
    -> from grade;
+----------+-----------------------------+
| grade_id | grade_description           |
+----------+-----------------------------+
|        1 | incomplete                  |
|        2 | complete and unsatisfactory |
|        3 | complete and satisfactory   |
|        4 | exceeds expectations        |
|        5 | not graded                  |
+----------+-----------------------------+
5 rows in set (0.00 sec)



mysql> select *
    -> from assignment;
Empty set (0.00 sec)



mysql> explain assignment
    -> ;
+----------------+------------------+------+-----+---------+----------------+
| Field          | Type             | Null | Key | Default | Extra          |
+----------------+------------------+------+-----+---------+----------------+
| assignment_id  | int(11) unsigned | NO   | PRI | NULL    | auto_increment |
| student_id     | int(11)          | NO   |     | NULL    |                |
| assignment_nbr | int(11)          | NO   |     | NULL    |                |
| class_id       | int(11)          | YES  |     | NULL    |                |
| grade_id       | int(11)          | YES  | MUL | NULL    |                |
+----------------+------------------+------+-----+---------+----------------+
5 rows in set (0.00 sec)


mysql> INSERT INTO assignment (student_id, assignment_nbr, class_id, grade_id)
    -> VALUES
    -> (2, 3, 4, 5),                                                                       
    -> (1, 3, 5, 2),
    -> (5, 3, 2, 1),
    -> (4, 2, 1, 3),
    -> (1, 3, 2, 1);
Query OK, 5 rows affected (0.01 sec)
Records: 5  Duplicates: 0  Warnings: 0



mysql> SELECT * FROM assignment
    -> ;
+---------------+------------+----------------+----------+----------+
| assignment_id | student_id | assignment_nbr | class_id | grade_id |
+---------------+------------+----------------+----------+----------+
|             1 |          2 |              3 |        4 |        5 |
|             2 |          1 |              3 |        5 |        2 |
|             3 |          5 |              3 |        2 |        1 |
|             4 |          4 |              2 |        1 |        3 |
|             5 |          1 |              3 |        2 |        1 |
+---------------+------------+----------------+----------+----------+
5 rows in set (0.00 sec)



mysql> explain assignment
    -> ;
+----------------+------------------+------+-----+---------+----------------+
| Field          | Type             | Null | Key | Default | Extra          |
+----------------+------------------+------+-----+---------+----------------+
| assignment_id  | int(11) unsigned | NO   | PRI | NULL    | auto_increment |
| student_id     | int(11)          | NO   |     | NULL    |                |
| assignment_nbr | int(11)          | NO   |     | NULL    |                |
| class_id       | int(11)          | YES  |     | NULL    |                |
| grade_id       | int(11)          | YES  | MUL | NULL    |                |
+----------------+------------------+------+-----+---------+----------------+
5 rows in set (0.00 sec)



mysql> select * from assignment
    -> ;
+---------------+------------+----------------+----------+----------+
| assignment_id | student_id | assignment_nbr | class_id | grade_id |
+---------------+------------+----------------+----------+----------+
|             1 |          2 |              3 |        4 |        5 |
|             2 |          1 |              3 |        5 |        2 |
|             3 |          5 |              3 |        2 |        1 |
|             4 |          4 |              2 |        1 |        3 |
|             5 |          1 |              3 |        2 |        1 |
+---------------+------------+----------------+----------+----------+
5 rows in set (0.00 sec)



mysql> explain grade;
+-------------------+-------------+------+-----+---------+----------------+
| Field             | Type        | Null | Key | Default | Extra          |
+-------------------+-------------+------+-----+---------+----------------+
| grade_id          | int(11)     | NO   | PRI | NULL    | auto_increment |
| grade_description | varchar(50) | NO   |     | NULL    |                |
+-------------------+-------------+------+-----+---------+----------------+
2 rows in set (0.00 sec)



mysql> select * from grade;
+----------+-----------------------------+
| grade_id | grade_description           |
+----------+-----------------------------+
|        1 | incomplete                  |
|        2 | complete and unsatisfactory |
|        3 | complete and satisfactory   |
|        4 | exceeds expectations        |
|        5 | not graded                  |
+----------+-----------------------------+
5 rows in set (0.00 sec)
