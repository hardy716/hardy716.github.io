---
layout: post
title: LeetCode Curated SQL 70 - Easy #1
image: /assets/img/blog/sql/leetcode.jpeg
accent_image: 
  background: url('/assets/img/sidebar/question.jpg') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  LeetCode에서 제공하는 Curated-SQL-70 - Easy #1 입니다. 
invert_sidebar: true
---

# Curated SQL 70 - Easy #1

* toc
{:toc}



### [586. Customer Placing the Largest Number of Orders](https://leetcode.com/problems/customer-placing-the-largest-number-of-orders/)
```sql
SELECT customer_number
FROM (
    SELECT customer_number, COUNT(*) AS order_count
    FROM Orders
    GROUP BY customer_number
) OrderCnt
ORDER BY order_count DESC
LIMIT 1
```
### [607. Sales Person](https://leetcode.com/problems/sales-person/)
```sql
SELECT name
FROM SalesPerson
WHERE sales_id NOT IN (
    SELECT a.sales_id
    FROM Orders a
    JOIN Company b ON a.com_id = b.com_id
    WHERE b.name = "RED"
)
```
### [1050. Actors and Directors Who Cooperated At Least Three Times](https://leetcode.com/problems/actors-and-directors-who-cooperated-at-least-three-times/)
```sql
SELECT actor_id, director_id
FROM (
    SELECT actor_id, director_id, COUNT(*) AS count
    FROM ActorDirector
    GROUP BY actor_id, director_id
) meetCnt
WHERE count >= 3
```
### [1084. Sales Analysis III](https://leetcode.com/problems/sales-analysis-iii/)
```sql
SELECT p.product_id, p.product_name
FROM Product p, Sales s
WHERE p.product_id = s.product_id
GROUP BY s.product_id
HAVING MIN(s.sale_date) >= '2019-01-01' AND MAX(s.sale_date) <= '2019-03-31';
```
### [511. Game Play Analysis I](https://leetcode.com/problems/game-play-analysis-i/)
```sql
SELECT player_id, min(event_date) as first_login
FROM Activity
GROUP BY player_id
```
### [1141. User Activity for the Past 30 Days I](https://leetcode.com/problems/user-activity-for-the-past-30-days-i/)
```sql
SELECT activity_date AS day, count(*) AS active_users
FROM (
    SELECT activity_date, count(*) AS active_count
    FROM Activity
    GROUP BY activity_date, user_id
) ActivityCount
GROUP BY activity_date
HAVING DATE_FORMAT(day,"%Y-%m-%d") BETWEEN "2019-06-28" AND "2019-07-27"
```
### [1148. Article Views I](https://leetcode.com/problems/article-views-i/)
```sql
SELECT author_id AS id
FROM Views
WHERE author_id = viewer_id
GROUP BY author_id
ORDER BY id ASC
```
### [1407. Top Travellers](https://leetcode.com/problems/top-travellers/)
```sql
SELECT a.name, IFNULL(b.travelled_distance, 0) AS travelled_distance
FROM Users a
LEFT JOIN (
    SELECT user_id, sum(distance) AS travelled_distance
    FROM Rides
    GROUP BY user_id
) b ON a.id = b.user_id
ORDER BY travelled_distance DESC, name ASC
```
### [610. Triangle Judgement](https://leetcode.com/problems/triangle-judgement/description/)
```sql
SELECT x, y, z,
    CASE WHEN x + y <= z OR x + z <= y OR y + z <= x THEN 'No'
    ELSE 'Yes' 
    END AS triangle
FROM Triangle
```
### [1068. Product Sales Analysis I](https://leetcode.com/problems/product-sales-analysis-i/description/)
```sql
SELECT B.product_name, A.year, A.price
FROM Sales A
JOIN Product B ON A.product_id = B.product_id
```
