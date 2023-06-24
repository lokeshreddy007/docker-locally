
# Commands

## Database

#### List available databases:

```mysql
show databases;
```

#### Creating database:

```mysql
CREATE DATABASE database_name;
```

#### Drop database

```mysql
CREATE DATABASE soap_store;
```

#### Select database would like to use

```mysql
use database_name
```

#### See currently using database

```mysql
SELECT database();
```

## Tables

#### Create Table

```mysql
 CREATE TABLE cats
    (
        cat_id INT NOT NULL AUTO_INCREMENT,
        name VARCHAR(100) NOT NULL,
        age INT NOT NULL,
        PRIMARY KEY (cat_id)
    );

create table employees
    (
        id int not null auto_increment primary key,
        first_name varchar(50) not null,
        last_name varchar(50) not null,
        middle_name varchar(50),
        age int not null,
        current_status varchar(50) not null default 'employed'
    )
```

#### Create Table with Setting Default Values

```mysql
CREATE TABLE cats
  (
    name VARCHAR(20) NOT NULL DEFAULT 'no name provided',
    age INT NOT NULL DEFAULT 99
  );

```

#### To see tables

```mysql
SHOW TABLES;
```

#### To see column from table

DESC - describe

```mysql
SHOW COLUMNS FROM tablename;

DESC tablename;
```

#### Dropping Tables

```mysql
DROP TABLE tablename;
```

#### Inserting Data

```mysql
INSERT INTO table_name(column_name) VALUES (data);

INSERT INTO cats(name, age) VALUES ("Blue", 2);
```

#### Multiple Insert Data

```mysql
INSERT INTO table_name (column_name, column_name)
            VALUES (value, value), (value, value), (value, value);
INSERT INTO cats (name,age) VALUES ("Neo",1), ("Robo", 4);
```

#### Selecting Data

```
SELECT * FROM table_name;
```

#### View Warning

```mysql
SHOW WARNINGS;
```

#### Where Clause

```mysql
SELECT cat_id as ID,name,age from cats WHERE age = 4;
SELECT * from cats WHERE cat_id = age;
```

#### Updating Data

```mysql
UPDATE cats set age = 12 WHERE breed = "Maine Coon"
```

#### Deleting Data

```mysql
DELETE FROM cats WHERE name='egg';
```

#### Delete entire table data

```mysql
DELETE FROM cats;
```

#### Load SQL

```mysql
source books.sql
```

#### CONCAT

```mysql
select concat(author_fname," ",author_lname) as Author_Name from books;
select concat_ws(" ",author_fname,author_lname) as Author_Name from books;
select concat_ws("-",author_fname,author_lname) as Author_Name from books;

```

#### Substring

Index start from 1 not from 0 as other programming languages

```mysql
select substring("hello world",1,4) // hell
select substr("hello world",1,4) // hell
select substring("hello world",7) // world
select substring("hello world",-4) // orld
select substring(title, 1, 10) as short_title from books;
select concat(substring(title, 1, 10),'...') as 'short title' from books;

```

#### Replace

Replaces all the occurance

```mysql
select replace('hello world','hell','lleh') // lleho world
```

#### Reverse

```mysql
select reverse("hello world") // dlrow olleh
```

#### String Length

```mysql
select char_length("hello world")
select concat(author_fname,' is ', char_length(author_fname),' Characters long') as Description from books;
```

#### Upper & Lower String

```mysql
SELECT UPPER('Hello World');
SELECT LOWER('Hello World');
SELECT CONCAT('MY FAVORITE BOOK IS ', LOWER(title)) FROM books;
```

#### Combination Query

```mysql
select concat(substring(title,1,10),'...') as 'short title', concat(author_lname,',',author_fname) as author, concat(stock_quantity,' in stock') as quantity from books;
--
short title	author	quantity
0	The Namesa...	Lahiri,Jhumpa	32 in stock
1	Norse Myth...	Gaiman,Neil	43 in stock
```

#### Distinct

```mysql
select distinct author_lname,author_fname from books;
```

#### Order by Sorting the result

Ascending by default in oder by

```mysql
select distinct released_year from books order by released_year;
select distinct released_year from books order by released_year desc;
SELECT author_fname, author_lname FROM books ORDER BY author_lname, author_fname;
SELECT author_lname, title FROM books ORDER BY 2; -- here 2 means index of select order i.e title
```

#### Limit

limit start index from 0

```mysql
select title,released_year from book order by released_year desc limit 5
select title,released_year from book order by released_year desc limit 0,5 -- same as above
-- top 3rd row only
select title,released_year from books order by released_year desc limit 2,1
-- here the row start from 0. So if we want the 3rd on use index of 2 and limit to 1 row
```

#### Like with wildcard

Like use pattern to search

```mysql
-- matches exactly 'da' it doesn't care before or after what is there
select title, author_fname from books where author_fname like '%da%';

-- matches exactly 'da' it should start with da but doesn't care after what is there
select title, author_fname from books where author_fname like 'da%';

-- matches exactly 'da'
select title, author_fname from books where author_fname like 'da';

-- matching for %
SELECT title FROM books WHERE title LIKE '%\%%'

-- matches _ means 1 char, so it can be anything followed by he and then anything
SELECT title, stock_quantity FROM books WHERE title LIKE '_he%';

-- match for _
SELECT title FROM books WHERE title LIKE '%\_%'

```

#### Group by

```mysql
select count(released_year) from books group by released_year;
```

## Aggregate Functions

#### count

```mysql
select count(*) as 'number of row' from books;
SELECT COUNT(title) FROM `books` where title like '%the%';

```

#### Min & Max

```mysql
SELECT MIN(released_year) FROM books;
SELECT MAX(released_year) FROM books;
select author_fname,author_lname,max(pages) from books group by author_fname,author_lname;
```

#### SUBQUERIES

```mysql
select title,pages from books where pages = (select max(pages)from books);
```

#### Sum

```mysql
select sum(pages) from books;
select author_fname,author_lname,sum(pages) from books group by author_fname,author_lname;
```

#### Average

```mysql
select avg(pages) from books;
select released_year, avg(stock_quantity) from books group by released_year;
```

#### Date, Time & DateTime

```mysql
CURDATE() -- current date
CURTIME() -- current time
NOW()     -- current datetime

INSERT INTO people (name, birthdate, birthtime, birthdt)
VALUES('noq', curdate(), curtime(), now());


SELECT name, birthdate, DAY(birthdate) FROM people; -- -- gives day like number 11

SELECT name, birthdate, DAYNAME(birthdate) FROM people; -- gives day like string friday


SELECT name, birthdate, DAYOFWEEK(birthdate) FROM people; -- gives day of week like number 4

SELECT name, birthdate, DAYOFYEAR(birthdate) FROM people;  -- gives number


SELECT name, birthdt, MONTH(birthdt) FROM people;  -- gives months link numbers

SELECT name, birthdt, MONTHNAME(birthdt) FROM people; -- gives months link strings

SELECT name, birthtime, HOUR(birthtime) FROM people;  -- give hours

SELECT name, birthtime, MINUTE(birthtime) FROM people;  -- give mintues

SELECT CONCAT(MONTHNAME(birthdate), ' ', DAY(birthdate), ' ', YEAR(birthdate)) FROM people;

SELECT DATE_FORMAT(birthdt, 'Was born on a %W') FROM people;

SELECT DATE_FORMAT(birthdt, '%m/%d/%Y') FROM people;

SELECT DATE_FORMAT(birthdt, '%m/%d/%Y at %h:%i') FROM people;
``
```

#### Date Math

```mysql
SELECT DATEDIFF(NOW(), birthdate) FROM people;

SELECT name, birthdate, DATEDIFF(NOW(), birthdate) FROM people;

SELECT birthdt FROM people;

SELECT birthdt, DATE_ADD(birthdt, INTERVAL 1 MONTH) FROM people;

SELECT birthdt, DATE_ADD(birthdt, INTERVAL 10 SECOND) FROM people;

SELECT birthdt, DATE_ADD(birthdt, INTERVAL 3 QUARTER) FROM people;

SELECT birthdt, birthdt + INTERVAL 1 MONTH FROM people;

SELECT birthdt, birthdt - INTERVAL 5 MONTH FROM people;

SELECT birthdt, birthdt + INTERVAL 15 MONTH + INTERVAL 10 HOUR FROM people;

CREATE TABLE tweets(
    content VARCHAR(140),
    username VARCHAR(20),
    created_at TIMESTAMP DEFAULT NOW()
);
```

## Logical Operators

#### Not Equal To

```mysql
SELECT title FROM books WHERE released_year != 2017;
```

#### Not Like

```mysql
SELECT title FROM books WHERE title NOT LIKE 'W%';
```

#### Greater Than

```mysql
SELECT title, stock_quantity FROM books WHERE stock_quantity > 100;
-- Greater than or equal to
SELECT title, stock_quantity FROM books WHERE stock_quantity >= 100;

```

#### Less Than

```mysql
SELECT title, released_year FROM books WHERE released_year < 2000;

SELECT title, released_year FROM books WHERE released_year <= 2000;
```

#### Logical AND

```mysql
-- can use &&
SELECT
    title,
    author_lname,
    released_year FROM books
WHERE author_lname='Eggers'
    AND released_year > 2010;

SELECT *
FROM books
WHERE author_lname='Eggers'
    AND released_year > 2010
    AND title LIKE '%novel%';
```

#### Logical OR

```mysql
SELECT title,
       author_lname,
       released_year,
       stock_quantity
FROM   books
WHERE  author_lname = 'Eggers'
              || released_year > 2010
OR     stock_quantity > 100;
```

#### Between

```mysql
SELECT title, released_year FROM books WHERE released_year >= 2004 && released_year <= 2015;

-- Same as above query using between
SELECT title, released_year FROM books
WHERE released_year BETWEEN 2004 AND 2015;

SELECT title, released_year FROM books
WHERE released_year NOT BETWEEN 2004 AND 2015;


```

#### Cast

- `CAST()` - convert the value to desired data type

```mysql
-- convert string to datatime
SELECT CAST('2017-05-02' AS DATETIME);

SELECT
    name,
    birthdt
FROM people
WHERE
    birthdt BETWEEN CAST('1980-01-01' AS DATETIME)
    AND CAST('2000-01-01' AS DATETIME);

```

#### In And Not In

```mysql
SELECT title, author_lname FROM books
WHERE author_lname IN ('Carver', 'Lahiri', 'Smith');

SELECT title, released_year FROM books
WHERE released_year >= 2000
AND released_year NOT IN
(2000,2002,2004,2006,2008,2010,2012,2014,2016) ORDER BY released_year;

-- same as above query but optimize one
SELECT title, released_year FROM books
WHERE released_year >= 2000 AND
released_year % 2 != 0 ORDER BY released_year;

```

#### Case Statements

```mysql
select title, released_year,
    case
        when released_year >= 2000 then 'Morden List'
        else '20th Century List'
        end as genre
    from books;

SELECT title, stock_quantity,
    CASE
        WHEN stock_quantity <= 50 THEN '*'
        WHEN stock_quantity <= 100 THEN '**'
        ELSE '***'
    END AS STOCK
FROM books;

select title, author_lname,
    case
        when count(*) = 1 then '1 Book'
        else concat(count(*), ' Books')
    end as Count
from books group by author_lname,author_fname;

```

#### Primary Key

```mysql
CREATE TABLE customers(
    id INT not null AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    email VARCHAR(100)
);
```

#### Foregin Key

```mysql
CREATE TABLE orders(
    id INT AUTO_INCREMENT PRIMARY KEY,
    order_date DATE,
    amount DECIMAL(8,2),
    customer_id INT,
    FOREIGN KEY(customer_id) REFERENCES customers(id)  ON DELETE CASCADE
);
```

## Joins

#### Cross Join Craziness

```mysql
SELECT * FROM customers, orders;
```

#### Inner Join

```mysql

SELECT first_name, last_name, order_date, amount
FROM customers
JOIN orders
    ON customers.id = orders.customer_id;


SELECT username,
       Count(*) AS num_likes
FROM   users
       INNER JOIN likes
               ON users.id = likes.user_id
GROUP  BY likes.user_id
HAVING num_likes = (SELECT Count(*)
                    FROM   photos);
```

#### Left Join

```mysql
select first_name, last_name, order_date, sum(amount)
from customers
left join orders
on customers.id = orders.customer_id
group by customers.id

select * from users left join photos on users.id = photos.user_id where photos.id is null;
```

#### Right Join

`IFNULL` - check if the value is null then replace with which mentioned. if not i will just the same value

```mysql
SELECT
    IFNULL(first_name,'MISSING') AS first,
    IFNULL(last_name,'USER') as last,
    order_date,
    amount,
    SUM(amount)
FROM customers
RIGHT JOIN orders
    ON customers.id = orders.customer_id
GROUP BY first_name, last_name;
```

#### Schema

- Below Schema help us to delete other table row if the if delete corresponding row in one table

```mysql
CREATE TABLE orders(
    id INT AUTO_INCREMENT PRIMARY KEY,
    order_date DATE,
    amount DECIMAL(8,2),
    customer_id INT,
    FOREIGN KEY(customer_id)
        REFERENCES customers(id)
        ON DELETE CASCADE
);

-- MANY to MANY

CREATE TABLE reviewers (
    id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(100),
    last_name VARCHAR(100)
);

CREATE TABLE series(
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(100),
    released_year YEAR(4),
    genre VARCHAR(100)
);


CREATE TABLE reviews (
    id INT AUTO_INCREMENT PRIMARY KEY,
    rating DECIMAL(2,1),
    series_id INT,
    reviewer_id INT,
    FOREIGN KEY(series_id) REFERENCES series(id),
    FOREIGN KEY(reviewer_id) REFERENCES reviewers(id)
)
```

#### Mutiple table joins

```mysql
SELECT
    title,
    rating,
    CONCAT(first_name,' ', last_name) AS reviewer
FROM reviewers
INNER JOIN reviews
    ON reviewers.id = reviews.reviewer_id
INNER JOIN series
    ON series.id = reviews.series_id
ORDER BY title;
```
