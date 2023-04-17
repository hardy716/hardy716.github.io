---
layout: post
title: Programmers SQL High Score Kit - IS NULL
image: /assets/img/blog/sql-is_null.jpg
accent_image: 
  background: url('/assets/img/blog/sql.jpg') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  프로그래머스 스쿨에서 제공하는 SQL 고득점 Kit : IS NULL 입니다. 
invert_sidebar: true
---

# SQL 고득점 Kit - IS NULL

값이 없음을 의미하는 NULL. NULL을 처리하는 방법을 배워봅시다.

* toc
{:toc}


## IS NULL

- LV.1
    - [경기도에 위치한 식품창고 목록 출력하기](https://school.programmers.co.kr/learn/courses/30/lessons/131114)
    ```sql
    SELECT WAREHOUSE_ID, WAREHOUSE_NAME, ADDRESS, IFNULL(FREEZER_YN, "N") AS FREEZER_YN
    FROM FOOD_WAREHOUSE
    WHERE ADDRESS LIKE "경기도%"
    ORDER BY WAREHOUSE_ID ASC
    ```
    - [이름이 없는 동물의 아이디](https://school.programmers.co.kr/learn/courses/30/lessons/59039)
    ```sql
    SELECT ANIMAL_ID
    FROM ANIMAL_INS
    WHERE NAME IS NULL
    ORDER BY ANIMAL_ID ASC
    ```
    - [이름이 있는 동물의 아이디](https://school.programmers.co.kr/learn/courses/30/lessons/59407)
    ```sql
    SELECT ANIMAL_ID
    FROM ANIMAL_INS
    WHERE NAME IS NOT NULL
    ORDER BY ANIMAL_ID
    ```
    - [나이 정보가 없는 회원 수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/131528)
    ```sql
    SELECT COUNT(*) AS USERS
    FROM USER_INFO
    WHERE AGE IS NULL
    ```

- LV.2
    - [NULL 처리하기](https://school.programmers.co.kr/learn/courses/30/lessons/59410)
    ```sql
    SELECT ANIMAL_TYPE, IFNULL(NAME, "No name"), SEX_UPON_INTAKE
    FROM ANIMAL_INS
    ```
