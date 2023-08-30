# SQL Dojo - Mastering SQL Skills

Welcome to the SQL Dojo, your ultimate destination to master SQL skills, conquer data manipulation challenges, and prepare for interviews in the realm of data management and analysis. Whether you're a seasoned SQL samurai or a novice ninja, this repository is your training ground to enhance your SQL proficiency.


## Table of Contents

- [About](#about)
- [Key Features](#keyfeatures)
- [Contributing](#contributing)
- [WorkingArea](#workingArea)

## About <a name = "about"></a> 🚀 

SQL Dojo is a comprehensive resource designed to address a wide range of SQL-related questions and challenges, drawing inspiration from the thought-provoking queries presented at [Datalemur](datalemur.com). Our mission is to empower you with the knowledge and skills required to efficiently navigate and manipulate data using SQL.


## Key Features <a name = "keyfeatures"></a> 🌟

<b>Extensive Question Bank:</b> SQL Dojo houses a diverse set of SQL challenges sourced from DataLemur, ensuring you're exposed to a variety of scenarios encountered in the field.

<b>Detailed Answers:</b> Each question comes with a detailed and well-explained answer. We believe that understanding the solution is as important as solving the problem.

<b>Progressive Difficulty:</b> The questions are categorized based on difficulty levels, allowing you to gradually enhance your skills from basic SELECT statements to advanced JOIN operations, subqueries, and more.

<b>Interview Preparation:</b> Apart from the DataLemur-inspired questions, SQL Dojo also offers a dedicated section for interview preparation. Here, you'll find commonly asked SQL interview questions with expert-approved answers.


## Contributing <a name = "contributing"></a>

We welcome contributions from the SQL community. If you've come across an interesting SQL challenge, a better solution to an existing question, or want to improve the overall structure of SQL Dojo, feel free to submit a pull request.

<b>Note:</b> This repository is meant for personal learning and practice purposes. The challenges are inspired by real-world scenarios, and the solutions provided here are intended to serve as educational references.

## Work Area <a name = "workingArea"></a>

 Navigate through the list of SQL questions in the <b>Q&A</b> listed below. Each question presents a unique challenge, from fundamental queries to more intricate data manipulations.

### Q&A

❓ Assume you're given two tables containing data about Facebook Pages and their respective likes (as in "Like a Facebook Page").

Write a query to return the IDs of the Facebook pages that have zero likes. The output should be sorted in ascending order based on the page IDs.

pages Table:
<table>
<tr><td>Column Name</td><td>Type</td></tr>
<tr><td>page_id</td>	<td>integer</td></tr>
<tr><td>page_name</td>	<td>varchar</td></tr>
</table>
pages Example Input:
<table>
<tr><td>page_id	<td>page_name
<tr><td>20001	<td>SQL Solutions
<tr><td>20045	<td>Brain Exercises
<tr><td>20701	<td>Tips for Data Analysts
</table>
page_likes Table:
<table>
<tr><td>Column Name	<td>Type
<tr><td>user_id	<td>integer
<tr><td>page_id	<td>integer
<tr><td>liked_date	<td>datetime
</table>
page_likes Example Input:
<table>
<tr><td>user_id	<td>page_id	<td>liked_date
<tr><td>111	<td>20001	<td>04/08/2022 00:00:00
<tr><td>121	<td>20045	<td>03/12/2022 00:00:00
<tr><td>156	<td>20001	<td>07/25/2022 00:00:00
</table>
Example Output:
<table>
<tr><td>page_id
<tr><td>20701
</table>
<br>
🛠️ DIFFICULTY : <span style="color:green"><b>Easy</b></span> 

``` sql 
SELECT P.page_id FROM pages P LEFT JOIN page_likes PL ON P.page_id=PL.page_id where PL.user_id is NULL ORDER BY P.page_id;
```
Explainations:

To find the Facebook pages that do not possess any likes, we can use the EXCEPT operator. This operator allows us to subtract the rows from one result set that exist in another result set.

Step 1: Retrieve all Facebook page IDs

In this step, we select all the page IDs from the pages table which gives us the initial set of Facebook pages to consider.

Run the following query to obtain an overview of the data:

SELECT page_id
FROM pages;
Step 2: Retrieve Facebook page IDs with likes

Here, we select the page IDs from the page_likes table, representing the set of Facebook pages that have received likes.

Execute the following query to get an overview of the data:

SELECT page_id
FROM page_likes;
Step 3: Find Facebook page IDs without likes

Using the EXCEPT operator, we subtract the page IDs with likes from the initial set of all page IDs. The resulting query will give us the IDs of the Facebook pages that do not possess any likes.

SELECT page_id
FROM pages
EXCEPT
SELECT page_id
FROM page_likes;
Additionally, here are alternative methods to solve the problem:

Method #2: Using LEFT OUTER JOIN

In this method, a LEFT OUTER JOIN is performed between the pages and page_likes tables.

The LEFT OUTER JOIN selects all rows from the left table (pages) and the matching rows from the right table (page_likes).

By checking for NULL values in the likes.page_id column, we can identify the Facebook pages that do not possess any likes.

SELECT pages.page_id
FROM pages
LEFT OUTER JOIN page_likes AS likes
  ON pages.page_id = likes.page_id
WHERE likes.page_id IS NULL;
Method #3: Using NOT IN` clause

SELECT page_id
FROM pages
WHERE page_id NOT IN (
  SELECT page_id
  FROM page_likes
  WHERE page_id IS NOT NULL
);
Method #4: Using NOT EXISTS clause

This method utilizes the NOT EXISTS clause to check for the non-existence of matching records in the page_likes table. It efficiently identifies the Facebook pages without any likes.

SELECT page_id
FROM pages
WHERE NOT EXISTS (
  SELECT page_id
  FROM page_likes AS likes
  WHERE likes.page_id = pages.page_id
;)
