---
layout: post
title: Programmers SQL High Score Kit - String, Date
image: /assets/img/blog/sql/programmers.jpg
accent_image: 
  background: url('/assets/img/sidebar/question.jpg') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  프로그래머스 스쿨에서 제공하는 SQL 고득점 Kit : String, Date 입니다. 
invert_sidebar: true
---

# SQL 고득점 Kit - String, Date

숫자는 어떻게 쓰는 건지 알겠는데, 글자와 날짜는 어떻게 다루지?

* toc
{:toc}


## String, Date

- LV.1
    - [특정 옵션이 포함된 자동차 리스트 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/157343)
    ```sql
    SELECT *
    FROM CAR_RENTAL_COMPANY_CAR
    WHERE OPTIONS LIKE "%네비게이션%"
    ORDER BY CAR_ID DESC
    ```
    - [자동차 대여 기록에서 장기/단기 대여 구분하기](https://school.programmers.co.kr/learn/courses/30/lessons/151138)
    ```sql
    SELECT 
        HISTORY_ID, 
        CAR_ID, 
        DATE_FORMAT(START_DATE, "%Y-%m-%d") AS START_DATE,
        DATE_FORMAT(END_DATE, "%Y-%m-%d") AS END_DATE,
        CASE WHEN DATEDIFF(END_DATE, START_DATE) >= 29 THEN "장기 대여"
        ELSE "단기 대여" 
        END AS RENT_TYPE
    FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
    WHERE START_DATE LIKE "2022-09%"
    ORDER BY HISTORY_ID DESC;
    ```

- LV.2
    - [자동차 평균 대여 기간 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/157342)
    ```sql
    SELECT ANIMAL_ID, NAME, SEX_UPON_INTAKE
    FROM ANIMAL_INS
    WHERE NAME IN (
        "Lucy", "Ella", "Pickle", "Rogan", "Sabrina", "Mitty"
    )
    ORDER BY ANIMAL_ID
    ```
    - [루시와 엘라 찾기](https://school.programmers.co.kr/learn/courses/30/lessons/59046)
    ```sql
    SELECT ANIMAL_ID, NAME, SEX_UPON_INTAKE
    FROM ANIMAL_INS
    WHERE NAME IN (
        "Lucy", "Ella", "Pickle", "Rogan", "Sabrina", "Mitty"
    )
    ORDER BY ANIMAL_ID
    ```
    - [이름에 el이 들어가는 동물 찾기](https://school.programmers.co.kr/learn/courses/30/lessons/59047)
    ```sql
    SELECT ANIMAL_ID, NAME
    FROM ANIMAL_INS
    WHERE ANIMAL_TYPE = "Dog"
        AND NAME LIKE "%EL%"
    ORDER BY NAME
    ```
    - [중성화 여부 파악하기](https://school.programmers.co.kr/learn/courses/30/lessons/59409)
    ```sql
    SELECT 
        ANIMAL_ID,
        NAME,
        CASE WHEN SEX_UPON_INTAKE LIKE "Intact%" THEN "X"
        ELSE "O"
        END AS "중성화"
    FROM ANIMAL_INS
    ORDER BY ANIMAL_ID
    ```
    - [카테고리 별 상품 개수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/131529)
    ```sql
    SELECT LEFT(PRODUCT_CODE ,2) AS CATEGORY, COUNT(*) AS PRODUCTS
    FROM PRODUCT
    GROUP BY CATEGORY
    ORDER BY CATEGORY ASC
    ```
    - [DATETIME에서 DATE로 형 변환](https://school.programmers.co.kr/learn/courses/30/lessons/59414)
    ```sql
    SELECT ANIMAL_ID, NAME, DATE_FORMAT(DATETIME, "%Y-%m-%d") AS "날짜"
    FROM ANIMAL_INS
    ORDER BY ANIMAL_ID
    ```

- LV.3
    - [조건별로 분류하여 주문상태 출력하기](https://school.programmers.co.kr/learn/courses/30/lessons/131113)
    ```sql
    SELECT ANIMAL_ID, NAME, SEX_UPON_INTAKE
    FROM ANIMAL_INS
    WHERE NAME IN (
        "Lucy", "Ella", "Pickle", "Rogan", "Sabrina", "Mitty"
    )
    ORDER BY ANIMAL_ID
    ```
    - [대여 기록이 존재하는 자동차 리스트 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/157341)
    ```sql
    SELECT DISTINCT CAR_ID
    FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
    WHERE START_DATE LIKE "2022-10%"
        AND CAR_ID IN (
        SELECT CAR_ID
        FROM CAR_RENTAL_COMPANY_CAR
        WHERE CAR_TYPE = "세단"
    ) 
    ORDER BY CAR_ID DESC
    ```
    - [오랜 기간 보호한 동물(2)](https://school.programmers.co.kr/learn/courses/30/lessons/59411)
    ```sql
    SELECT A.ANIMAL_ID, A.NAME
    FROM ANIMAL_INS A
    JOIN ANIMAL_OUTS B
    ON A.ANIMAL_ID = B.ANIMAL_ID
    ORDER BY DATEDIFF(B.DATETIME, A.DATETIME) DESC
    LIMIT 2
    ```

- LV.4
    - [자동차 대여 기록 별 대여 금액 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/151141)
    ```sql
    SELECT 
        HISTORY_ID,
        ROUND(DAILY_FEE * RENTAL_DURATION * PURCHASE_RATE) AS FEE
    FROM (
        SELECT
            A.HISTORY_ID,
            B.DAILY_FEE,
            (DATEDIFF(A.END_DATE, A.START_DATE) + 1) AS RENTAL_DURATION,
            CASE WHEN (DATEDIFF(A.END_DATE, A.START_DATE) + 1) < 7 THEN 1
            WHEN (DATEDIFF(A.END_DATE, A.START_DATE) + 1) < 30 THEN 0.95
            WHEN (DATEDIFF(A.END_DATE, A.START_DATE) + 1) < 90 THEN 0.92
            ELSE 0.85
            END AS PURCHASE_RATE
        FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY A
        JOIN CAR_RENTAL_COMPANY_CAR B
        ON A.CAR_ID = B.CAR_ID
        WHERE B.CAR_TYPE = "트럭"
    ) A
    ORDER BY FEE DESC, HISTORY_ID DESC
    ```
    - [취소되지 않은 진료 예약 조회하기](https://school.programmers.co.kr/learn/courses/30/lessons/132204)
    ```sql
    SELECT 
        A.APNT_NO, 
        B.PT_NAME,
        A.PT_NO, 
        A.MCDP_CD,
        C.DR_NAME,
        A.APNT_YMD
    FROM APPOINTMENT A
    JOIN PATIENT B ON A.PT_NO = B.PT_NO
    JOIN DOCTOR C ON A.MDDR_ID = C.DR_ID
    WHERE A.APNT_CNCL_YN = "N" 
        AND A.APNT_YMD LIKE "2022-04-13%"
    ORDER BY APNT_YMD ASC
    ```
