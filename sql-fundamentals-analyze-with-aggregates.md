## 🔎 SQL Fundamentals: Analyze Trends with Aggregates

## Task
In this project, I'm exploring a table name `hacker_news` that contains stories, news posted on [Hacker News](https://news.ycombinator.com/) since its launch in 2007. This data was made publicly available under the MIT license.

## Exploration and Analyzing of Trends

**1. Firstly, I'll get a feel of what the table looks like:**

```sql
SELECT COUNT(*)
FROM hacker_news;
```

```sql
SELECT *
FROM hacker_news
LIMIT 10;
```

**Steps:**
- I like to first have a feel of the size of the table, and then of what the first 10 rows look like.

**Output:**
I understand there are 4000 rows in that table and a few columns: 
- title: title of the post/story
- user: who posted it
- score: that the story got (numeric value)
- timestamp: when it was posted
- url: direct link to the story

![image](https://github.com/elizabeth-gj/codecademy-bi-data-analyst-path/assets/64903268/9e79e11b-4c35-4015-aac3-060b8c410e86)


***
**2. MODERATING: Recent studies have found that online formus tend to be dominated by a small percentage of their users ([1% rule](https://en.wikipedia.org/wiki/1%25_rule)). How true is it for Hacker News?:**

```sql
SELECT SUM(score)
FROM hacker_news
```
→ The outcome here is 6,366. In total, for all of these stories, we have a cumulated score of 6,366 points. Let's keep this in mind to understand the distribution of score in the following exploration.


```sql
SELECT user
     , SUM(score) AS sum_score
     , ROUND(SUM(score)/6366.0*100,2) AS perc_total
FROM hacker_news
GROUP BY user
HAVING sum_score > 150
ORDER BY sum_score DESC

```

**Steps:**
- It's important I SELECT user and GROUP BY it to see the result per individual user/contributor
- I am using the SUM() aggregate to sum each `score` per user
- I also add a calculation of the share of each user's sum of score in the total 6,366 score to get a better feel of the distribution per user
- I also add a HAVING clause because the results table is too long otherwise: there are 3,870 users!
- And to make it even clearer, I like to ORDER BY in descending order to immediatley see my top contributor 

**Output:**
Wow, there is one user 'vxNsr' that cumulatves 517 points, which is +8% of the total score.
Actually, summing up the `perc_total` share of our Top 5 Contributor-users, we have 25.18% of total scores - meanwhile, these 5 users represent a 0.13% (5/3870) of the total users → the 1% rule definitely applies here.

![image](https://github.com/elizabeth-gj/codecademy-bi-data-analyst-path/assets/64903268/e2fa35bd-3ae3-4206-b917-4d035438c8d6)


***
**3. POSTING TIME OPTIMISATION: Is there any best time for posting in regards to scores?:**

```sql
SELECT strftime('%H', timestamp) AS hour
     , ROUND(AVG(score),2) AS average_score
     , COUNT(*) AS count_stories
FROM hacker_news
WHERE hour IS NOT NULL
GROUP BY 1
ORDER BY 2 DESC
```

**Steps:**
- I use the function strftime to only get the Hour from the full timestamp value - this allows me to group scores and count stories per hour of the day
- For more readability: I round the average_score and order by descending average_score
- And finally, I also filter out the NULL hours

**Output:**
There seem to be 2 main trends with best hours of posting: end of afternoon with hours 18-20 and also the early morning on the hour 7. There is a high difference in between these peak times and the rest of the day.
![image](https://github.com/elizabeth-gj/codecademy-bi-data-analyst-path/assets/64903268/ff5c2732-409e-4d88-9b62-f80acb1b4c62)

***
**4. NEWS SOURCES: Most of the stories there redirect users to other websites via links to GitHub, Medium or the New York Times for example. Which of these website is the biggest source for us here?:**

```sql
SELECT CASE
        WHEN url LIKE '%github.%' THEN 'GitHub'
        WHEN url LIKE '%medium.%' THEN 'Medium'
        WHEN url LIKE '%nytimes.%' THEN 'New York Times'
        ELSE 'Other'
       END AS 'Source'
     , COUNT(*)
FROM hacker_news
GROUP BY 1;
```

**Steps:**
- I use the CASE clause and the % as a wildcare to include `url` containing github, medium or nytimes in their url
- There will also be other urls which don't belong to any of these cases so I'll group them under "Other"

**Output:**
GitHub is the #1 source of story among these big 3.
![image](https://github.com/elizabeth-gj/codecademy-bi-data-analyst-path/assets/64903268/2e8eb441-0396-40a1-bb6c-45dc4a7145ee)
