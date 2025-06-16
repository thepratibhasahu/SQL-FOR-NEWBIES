# PROJECT_1
In this project, you will create your own friends table and add/delete data from it!

The instructions provided are a general guideline. Feel free to add more columns, insert more data, and create more tables.


**1. Create a table named `friends` with three columns:**                                    
* `id` that stores `INTEGER`                                    
* `name` that stores `TEXT`                                       
* `birthday` that stores `DATE`
```SQL
CREATE TABLE friends (
   id INTEGER,
   name TEXT,
   birthday DATE
);
```
📝 The `CREATE TABLE` statement is used to create a new table in the database:
📝 Don’t forget the `;` at the end!

### 🟩 Output
```SQL
  Database Schema
     friends
name	     type
id	    INTEGER
name	     TEXT
birthday     DATE
```
**2.Beneath your current code, add Ororo Munroe to `friends`.**                       
* Her birthday is May 30th, 1940.
```SQL
INSERT INTO friends (id, name, birthday) 
VALUES (1, 'Ororo Munroe', '1940-05-30');
```
📝 The INSERT INTO statement is used to insert new records into a table.                          
📝 For the `DATE` data type, the format is YYYY-MM-DD.

**3.Let’s make sure that Ororo has been added to the database:**                       
Check for two things:                                
* Is ~friends` table created?
* Is Ororo Munroe added to it?
```SQL
SELECT * FROM friends;
```
📝 `SELECT *` indicates that we want to select all columns.                           
📝 `FROM friends` indicates the table we are interested in.
* The result should have three columns (`id`, `name`, `birthday`) and one row.
### 🟩 Output
```SQL
          friends
id	   name	        birthday
1	Ororo Munroe	1940-05-30
```
**4.Let’s move on!**             
* Add two of your friends to the table.                           
* Insert an `id`, `name`, and `birthday` for each of them.
```SQL
INSERT INTO friends (id, name, birthday)
VALUES (2, 'Pratibha sahu', '2006-10-06');

INSERT INTO friends (id, name, birthday)
VALUES (3, 'Bulbul sahu', '2003-10-06');
```
### 🟩 Output
```SQL
id	name	         birthday
1	Ororo Munroe    1940-05-30
2	Pratibha sahu	2006-10-06
3	Bulbul sahu	2003-10-06
```
**5.Ororo Munroe just realized that she can control the weather and decided to change her name. Her new name is “Storm”.**      Update her record in `friends`.
```SQL
UPDATE friends
SET name = 'Storm'
WHERE id = 1;
```
### 🟩 Output
```SQL
id	name	         birthday
1	Storm    	1940-05-30
2	Pratibha sahu	2006-10-06
3	Bulbul sahu	2003-10-06
```
**6.Add a new column named `email`.**
```SQL
ALTER TABLE friends 
ADD COLUMN email TEXT; 
```
### 🟩 Output
```SQL
id	name	         birthday     emails
1	Storm	        1940-05-30	∅
2	Pratibha sahu	2006-10-06	∅
3	Bulbul sahu	2003-10-06	∅
```
**7.Update the email address for everyone in your table.**                       
* Storm’s email is `storm@codecademy.com`.
```SQL
UPDATE friends
SET email = 'storm@codecademy.com'
WHERE id = 1;

UPDATE friends 
SET emails = 'thepratibhasahu@gmail.com'
WHERE id = 2;

UPDATE friends 
SET emails = 'bulbulsahu@gamil.com'
WHERE id = 3;
```
📝 do the same for both of your friends.
### 🟩 Output
```SQL
id	name	         birthday	      emails
1	Storm	        1940-05-30	storm@codecademy.com
2	Pratibha sahu	2006-10-06	thepratibhasahu@gmail.com
3	Bulbul sahu	2003-10-06	bulbulsahu@gamil.com
```

**8.Wait, Storm is fictional…                      
Remove her from `friends`.**
```SQL
DELETE FROM friends
WHERE id = 1;
```
**9.Great job! Let’s take a look at the result one last time:**
```SQL
SELECT * FROM friends;
```
### 🟩 Final Output
```SQL
id	    name	 birthday	       emails
2	Pratibha sahu	2006-10-06	thepratibhasahu@gmail.com
3	Bulbul sahu	2003-10-06	bulbulsahu@gamil.com
```














