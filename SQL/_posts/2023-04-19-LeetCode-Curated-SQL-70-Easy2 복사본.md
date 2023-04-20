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
