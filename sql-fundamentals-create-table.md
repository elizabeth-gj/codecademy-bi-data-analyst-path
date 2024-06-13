## ⚡ SQL Fundamentals: Create Table

## Task
In this project, I am creating a `friends` table and adding/deleting data from it.

***

## Questions and Solutions

**1. Create a table named friends with three columns: id, name, birthday:**

```sql
CREATE TABLE friends (
  id INTEGER,
  name TEXT,
  birthday DATE
);
```

**Steps:**
- I use the CREATE TABLE clause and define the name of my table to `friends`
- Next to each column, I specify their data type

**Answer:**
My table has been created!

![image](https://github.com/elizabeth-gj/codecademy-bi-data-analyst-path/assets/64903268/482b645c-f122-45e6-b021-11454ee3fbed)

***
**2. Add a row for your friend Harry:**

```sql
INSERT INTO friends (id, name, birthday)
VALUES (1, 'Harry Potter', '1980-07-31');
```

**Steps:**
- I use the INSERT INTO clause to modify my `friends` table
- I define my new row's values for each of the given columns

**Answer:**
When querying the table, I get to see my new row:

![image](https://github.com/elizabeth-gj/codecademy-bi-data-analyst-path/assets/64903268/4d13b14f-38d0-4090-93ab-8bde12798cd9)

***
**3. Add 2 more friends to the table:**

```sql
INSERT INTO friends (id, name, birthday)
VALUES (2,'Hermione Granger','1979-09-19'),
       (3,'Ron Weasley','1980-03-01');  
```

**Steps:**
- I use the INSERT INTO clause again
- And I add the two new rows at the same time with the VALUES clause
 
**Answer:**

![image](https://github.com/elizabeth-gj/codecademy-bi-data-analyst-path/assets/64903268/2b39e37f-e559-40a8-83f9-a586a62d5513)

***
**4. Hermione's getting married to Ron and changes her name. Update it in the table:**

```sql
UPDATE friends
SET name = 'Hermione Weasley'
WHERE id = 2; 
```

**Steps:**
- This time, I get to use the UPDATE clause
- and I use the variable `id` to identify Hermione
 
**Answer:**

![image](https://github.com/elizabeth-gj/codecademy-bi-data-analyst-path/assets/64903268/46206320-5aee-44a6-b27d-08126cbb6d7e)

***

**5. We'd also like to know which School my friends attended. Add a column to the table:**

```sql
ALTER TABLE friends
ADD COLUMN school TEXT DEFAULT 'Hogwarts';
```

**Steps:**
- With the ALTER TABLE / ADD COLUMN clauses, I add a `school` column
- I can even default its value for all my current rows as I know they attended the same School
 
**Answer:**

![image](https://github.com/elizabeth-gj/codecademy-bi-data-analyst-path/assets/64903268/fce41b16-360e-45f6-b1bf-90c55e0ac641)

***
