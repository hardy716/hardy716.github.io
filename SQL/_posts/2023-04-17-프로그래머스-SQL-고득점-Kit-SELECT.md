---
layout: post
title: Programmers SQL High Score Kit - SELECT
image: /assets/img/blog/programmers.jpg
accent_image: 
  background: url('/assets/img/sidebar-bg3.jpg') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  프로그래머스 스쿨에서 제공하는 SQL 고득점 Kit : SELECT 입니다. 
invert_sidebar: true
---

# SQL 고득점 Kit - SELECT

조건에 맞는 레코드를, 원하는 순서대로. 기본기를 처음부터 탄탄히 다져보세요.

* toc
{:toc}


## SELECT

- LV.1
    - [평균 일일 대여 요금 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/151136)
    ```sql
    SELECT ROUND(SUM(DAILY_FEE) / COUNT(*)) AS AVEARGE_FEE
    FROM CAR_RENTAL_COMPANY_CAR
    WHERE CAR_TYPE = 'SUV'
    ```
    - [강원도에 위치한 생산공장 목록 출력하기](https://school.programmers.co.kr/learn/courses/30/lessons/131112)
    ```sql
    SELECT FACTORY_ID, FACTORY_NAME, ADDRESS
    FROM FOOD_FACTORY
    WHERE ADDRESS LIKE '강원도%'
    ORDER BY factory_id
    ```
    - [12세 이하인 여자 환자 목록 출력하기](https://school.programmers.co.kr/learn/courses/30/lessons/132201)
    ```sql
    SELECT PT_NAME, PT_NO, GEND_CD, AGE, IFNULL(TLNO, 'NONE') AS TLNO
    FROM PATIENT
    WHERE (GEND_CD = 'W') AND (AGE < 13)
    ORDER BY AGE DESC, PT_NAME
    ```
    - [흉부외과 또는 일반외과 의사 목록 출력하기](https://school.programmers.co.kr/learn/courses/30/lessons/132203)
    ```sql
    SELECT DR_NAME, DR_ID, MCDP_CD, DATE_FORMAT(HIRE_YMD, '%Y-%m-%d') AS HIRE_YMD
    FROM DOCTOR
    WHERE MCDP_CD IN ('CS', 'GS')
    ORDER BY HIRE_YMD DESC, DR_NAME
    ```
    - [과일로 만든 아이스크림 고르기](https://school.programmers.co.kr/learn/courses/30/lessons/133025)
    ```sql
    SELECT FIRST_HALF.FLAVOR 
    FROM FIRST_HALF JOIN ICECREAM_INFO 
    ON FIRST_HALF.FLAVOR = ICECREAM_INFO.FLAVOR
    WHERE (TOTAL_ORDER > 3000) AND (INGREDIENT_TYPE = "fruit_based")
    ORDER BY TOTAL_ORDER DESC
    ```
    - [조건에 맞는 도서 리스트 출력하기](https://school.programmers.co.kr/learn/courses/30/lessons/144853)
    ```sql
    SELECT BOOK_ID, DATE_FORMAT(PUBLISHED_DATE, '%Y-%m-%d') AS PUBLISHED_DATE
    FROM BOOK
    WHERE (PUBLISHED_DATE LIKE '2021%') AND (CATEGORY = '인문')
    ORDER BY PUBLISHED_DATE
    ```
    - [인기있는 아이스크림](https://school.programmers.co.kr/learn/courses/30/lessons/133024)
    ```sql
    SELECT FLAVOR
    FROM FIRST_HALF
    ORDER BY TOTAL_ORDER DESC, SHIPMENT_ID
    ```
    - [모든 레코드 조회하기](https://school.programmers.co.kr/learn/courses/30/lessons/59034)
    ```sql
    SELECT *
    FROM ANIMAL_INS
    ORDER BY ANIMAL_ID
    ```
    - [역순 정렬하기](https://school.programmers.co.kr/learn/courses/30/lessons/59035)
    ```sql
    SELECT NAME, DATETIME
    FROM ANIMAL_INS
    ORDER BY ANIMAL_ID DESC
    ```
    - [아픈 동물 찾기](https://school.programmers.co.kr/learn/courses/30/lessons/59036)
    ```sql
    SELECT ANIMAL_ID, NAME
    FROM ANIMAL_INS
    WHERE INTAKE_CONDITION = 'Sick'
    ORDER BY ANIMAL_ID
    ```
    - [어린 동물 찾기](https://school.programmers.co.kr/learn/courses/30/lessons/59037)
    ```sql
    SELECT ANIMAL_ID, NAME
    FROM ANIMAL_INS
    WHERE INTAKE_CONDITION != 'Aged'
    ORDER BY ANIMAL_ID
    ```
    - [동물의 아이디와 이름](https://school.programmers.co.kr/learn/courses/30/lessons/59403)
    ```sql
    SELECT ANIMAL_ID, NAME
    FROM ANIMAL_INS
    ORDER BY ANIMAL_ID
    ```
    - [여러 기준으로 정렬하기](https://school.programmers.co.kr/learn/courses/30/lessons/59404)
    ```sql
    SELECT ANIMAL_ID, NAME, DATETIME
    FROM ANIMAL_INS
    ORDER BY NAME, DATETIME DESC
    ```
    - [상위 n개 레코드](https://school.programmers.co.kr/learn/courses/30/lessons/59405)
    ```sql
    SELECT NAME
    FROM ANIMAL_INS
    ORDER BY DATETIME
    LIMIT 1
    ```
    - [조건에 맞는 회원수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/131535)
    ```sql
    SELECT COUNT(*) AS USERS
    FROM USER_INFO
    WHERE (JOINED LIKE '2021%') AND (AGE BETWEEN 20 AND 29)
    ```

- LV.2
    - [3월에 태어난 여성 회원 목록 출력하기](https://school.programmers.co.kr/learn/courses/30/lessons/131120)
    ```sql
    SELECT MEMBER_ID, MEMBER_NAME, GENDER, DATE_FORMAT(DATE_OF_BIRTH, '%Y-%m-%d') as DATE_OF_BIRTH
    FROM MEMBER_PROFILE
    WHERE (MONTH(DATE_OF_BIRTH) = 3) 
        AND (GENDER = 'W') 
        AND (TLNO IS NOT NULL)
    ORDER BY MEMBER_ID
    ```
    - [재구매가 일어난 상품과 회원 리스트 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/131536)
    ```sql
    SELECT USER_ID, PRODUCT_ID
    FROM ONLINE_SALE
    GROUP BY USER_ID, PRODUCT_ID
    HAVING COUNT(*) > 1
    ORDER BY USER_ID, PRODUCT_ID DESC
    ```
    
- LV.4
    - [서울에 위치한 식당 목록 출력하기](https://school.programmers.co.kr/learn/courses/30/lessons/131118)
    ```sql
    SELECT I.REST_ID, I.REST_NAME, I.FOOD_TYPE, I.FAVORITES, I.ADDRESS, ROUND(SUM(R.REVIEW_SCORE)/COUNT(*), 2) AS SCORE
    FROM REST_INFO I JOIN REST_REVIEW R
    ON I.REST_ID = R.REST_ID
    WHERE I.ADDRESS LIKE '서울%'
    GROUP BY R.REST_ID
    ORDER BY SCORE DESC, I.FAVORITES DESC
    ```
    - [오프라인/온라인 판매 데이터 통합하기](https://school.programmers.co.kr/learn/courses/30/lessons/131537)
    ```sql
    WITH SALES_DATA AS (
        SELECT  SALES_DATE
                , PRODUCT_ID
                , USER_ID
                , SALES_AMOUNT
        FROM    ONLINE_SALE
            UNION ALL 
        SELECT  SALES_DATE
                , PRODUCT_ID
                , NULL AS USER_ID
                , SALES_AMOUNT
        FROM    OFFLINE_SALE
    )
    SELECT  DATE_FORMAT(SALES_DATE, '%Y-%m-%d') AS SALES_DATE
            , PRODUCT_ID
            , USER_ID
            , SALES_AMOUNT
    FROM    SALES_DATA
    WHERE    (YEAR(SALES_DATE) = 2022) AND (MONTH(SALES_DATE) = 3)
    ORDER BY    SALES_DATE ASC, PRODUCT_ID ASC, USER_ID ASC
    ```
