---
layout: post
title: Programmers SQL High Score Kit - SUM, MAX, MIN
image: /assets/img/blog/programmers.jpg
accent_image: 
  background: url('/assets/img/sidebar/bricks.jpg') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  프로그래머스 스쿨에서 제공하는 SQL 고득점 Kit : SUM, MAX, MIN 입니다. 
invert_sidebar: true
---

# SQL 고득점 Kit - SUM, MAX, MIN

나이가 가장 많은 사람은 누구일까? 테이블을 뒤져 통계를 내어봅시다.

* toc
{:toc}


## SUM, MAX, MIN

- LV.1
    - [가장 비싼 상품 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/131697)
    ```sql
    SELECT MAX(PRICE) AS MAX_PRICE
    FROM PRODUCT
    ```
    - [최댓값 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/59415)
    ```sql
    SELECT MAX(DATETIME) AS 시간
    FROM ANIMAL_INS    
    ```

- LV.2
    - [가격이 제일 비싼 식품의 정보 출력하기](https://school.programmers.co.kr/learn/courses/30/lessons/131115)
    ```sql
    SELECT PRODUCT_ID, PRODUCT_NAME, PRODUCT_CD, CATEGORY, PRICE
    FROM FOOD_PRODUCT
    ORDER BY PRICE DESC
    LIMIT 1
    ```
    ```sql
    SELECT *
    FROM FOOD_PRODUCT
    WHERE PRICE IN (SELECT MAX(PRICE) FROM FOOD_PRODUCT)
    ```
    - [최솟값 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/59038)
    ```sql
    SELECT MIN(DATETIME) AS 시간
    FROM ANIMAL_INS
    ```
    - [동물 수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/59406)
    ```sql
    SELECT COUNT(*) AS count
    FROM ANIMAL_INS
    ```
    - [중복 제거하기](https://school.programmers.co.kr/learn/courses/30/lessons/59408)
    ```sql
    SELECT COUNT(DISTINCT NAME) AS count 
    FROM ANIMAL_INS;
    ```
