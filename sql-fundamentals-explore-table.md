## ⚡ SQL Fundamentals: Explore a Data Table

## Task
In this project, I'm exploring a table of restaurants called `nomnom` and trying to find out more about these NYC restaurants. This is the schema of that table:
![image](https://github.com/elizabeth-gj/codecademy-bi-data-analyst-path/assets/64903268/b2ae2f1f-4a3a-428c-b004-5802e8951ad9)

***

## Questions and Solutions

**1. Firstly, I'll get a feel of what the table looks like:**

```sql
SELECT COUNT(*)
FROM nomnom;
```

```sql
SELECT *
FROM nomnom
LIMIT 10;
```

**Steps:**
- I like to first have a feel of the size of the table, and then of what the first X rows look like.

**Output:**
I know there are 53 rows in the table and understand what kind of data i can find in there.

![image](https://github.com/elizabeth-gj/codecademy-bi-data-analyst-path/assets/64903268/4b4e9804-9f89-46be-ac0f-c276b18c84f9)

![image](https://github.com/elizabeth-gj/codecademy-bi-data-analyst-path/assets/64903268/53dcb979-6baf-435e-80f5-b2ff79fe100c)
***
**2. I want to understand more about the ranges of cuisine and neighborhood that this table covers:**

```sql
SELECT DISTINCT neighborhood
, COUNT(*) AS restaurant_count
FROM nomnom
GROUP BY 1
ORDER BY 2 DESC;
```

```sql
SELECT DISTINCT cuisine
, COUNT(*) AS restaurant_count
FROM nomnom
GROUP BY 1
ORDER BY 2 DESC;
```

**Steps:**
- I use the SELECT DISTINCT clause and then the COUNT() rows to understand how each value of neighborhood and cuisine are distributed among our restaurants
- I also prefer to ORDER BY DESC to understand very clearly what are the most represented and least represented values, it helps if there are quite a diversity of values such as for our cuisine dimension.

**Output:**
Downtown and Brooklyn are largely the most represented neighborhoods:
![image](https://github.com/elizabeth-gj/codecademy-bi-data-analyst-path/assets/64903268/4a9a3c56-6d6c-4bac-b946-716780fb0736)

And among the most represented cuisines, there is Chinese, American and then Italian. Some cuisines have only 1 restaurant represented such as Mexican.
![image](https://github.com/elizabeth-gj/codecademy-bi-data-analyst-path/assets/64903268/2baeae84-0bf3-48fe-8ee6-9b03badf5bbe)

***

**3. To clean and complete this data in the future, I want to be aware of any blindspots:**

```sql
SELECT *
FROM nomnom
WHERE (health IS NULL OR review IS NULL);
```

**Steps:**
- I am focusing on looking wether there are some restaurants with their health grade or review still pending by using the WHERE clause and IS NULL

**Output:**
There are indeed 2 American restaurants without a review yet and 5 restaurants without a health grade:
![image](https://github.com/elizabeth-gj/codecademy-bi-data-analyst-path/assets/64903268/c3c8c352-f7f5-4463-81cf-cf84348d5130)

***

**5. I want to create a top of the best restaurants:**

```sql
SELECT *
FROM nomnom
ORDER BY review DESC
LIMIT 10;
```

**Steps:**
- I choose `review` as the dimension on which to base my top 10

**Output:**
Here are the Top 10 restaurants based on reviews. There are 3 restaurants on the top spot with 4.6 stars/5: Bunna Cafe, Russ & Daughters and Lighthouse:
![image](https://github.com/elizabeth-gj/codecademy-bi-data-analyst-path/assets/64903268/fca37bec-5e24-4474-b835-3f15bad6de78)

***
