---
layout: post
title: LeetCode Curated SQL 70 - Easy #2
image: /assets/img/blog/leetcode.jpeg
accent_image: 
  background: url('/assets/img/sidebar/bricks.jpg') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  LeetCode에서 제공하는 Curated-SQL-70 - Easy #2 입니다. 
invert_sidebar: true
---

# Curated SQL 70 - Easy #2

* toc
{:toc}



### [1075. Project Employees I](https://leetcode.com/problems/project-employees-i/description/)
```sql
SELECT A.project_id,
    ROUND(SUM(B.experience_years)/COUNT(*), 2) AS average_years
FROM Project A
JOIN Employee B ON A.employee_id = B.employee_id
GROUP BY A.project_id
```

### [1251. Average Selling Price](https://leetcode.com/problems/average-selling-price/description/)
```sql
SELECT
    Prices.product_id, 
    ROUND(SUM(Prices.price * UnitsSold.units) / SUM(UnitsSold.units), 2) as average_price
FROM Prices
INNER JOIN UnitsSold
ON (
    UnitsSold.purchase_date BETWEEN Prices.start_date AND Prices.end_date
    AND Prices.product_id = UnitsSold.product_id 
) 
GROUP BY Prices.product_id
```

### [1280. Students and Examinations]()
```sql
SELECT 
    A.student_id,
    A.student_name,
    B.subject_name,
    COUNT(C.subject_name) as attended_exams
FROM Students as A
JOIN Subjects as B
LEFT JOIN Examinations as C
ON (
    A.student_id = C.student_id 
    AND B.subject_name = C.subject_name
)
GROUP BY A.student_id, B.subject_name
ORDER BY student_id, subject_name;
```

### [1327. List the Products Ordered in a Period](https://leetcode.com/problems/list-the-products-ordered-in-a-period/description/)
```sql
SELECT product_name, unit
FROM (
    SELECT
        A.product_name,
        SUM(B.unit) as unit
    FROM
        Products A
    INNER JOIN
        Orders B ON A.product_id = B.product_id
    WHERE 
        MONTH(B.order_date) = 2
    GROUP BY product_name
) C
WHERE unit >= 100
```

### [1378. Replace Employee ID With The Unique Identifier](https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier/description/)
```sql
SELECT
    CASE WHEN A.id = B.id THEN B.unique_id
        ELSE null
    END as unique_id,
    A.name
FROM 
    Employees A
LEFT JOIN
    EmployeeUNI B
ON A.id = B.id
```

### [1484. Group Sold Products By The Date](https://leetcode.com/problems/group-sold-products-by-the-date/description/)
```sql
SELECT
    sell_date, 
    COUNT( DISTINCT product ) as num_sold ,
    GROUP_CONCAT( 
        DISTINCT product ORDER BY product ASC separator ',' 
    ) as products
FROM Activities 
GROUP BY sell_date 
ORDER BY sell_date ASC;
```

### [1517. Find Users With Valid E-Mails](https://leetcode.com/problems/find-users-with-valid-e-mails/description/)
```sql
SELECT 
    *
FROM 
    users
WHERE 
    mail REGEXP '^[A-Za-z]+[A-Za-z0-9\\._\\-]*@leetcode\\.com$';
```
