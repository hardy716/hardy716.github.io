---
layout: post
title: LeetCode Curated SQL 70 - Easy #2
image: /assets/img/blog/leetcode.jpeg
accent_image: 
  background: url('/assets/img/sidebar-bg3.jpg') center/cover
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
