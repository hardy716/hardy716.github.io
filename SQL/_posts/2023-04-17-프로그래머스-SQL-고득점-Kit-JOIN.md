---
layout: post
title: Programmers SQL High Score Kit - JOIN
image: /assets/img/blog/sql-join.jpg
accent_image: 
  background: url('/assets/img/blog/sql.jpg') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  프로그래머스 스쿨에서 제공하는 SQL 고득점 Kit : JOIN 입니다. 
invert_sidebar: true
---

# SQL 고득점 Kit - JOIN

테이블 사이의 복잡한 관계를 파악해보아요. 이제부터 어렵습니다.

* toc
{:toc}


## JOIN

- LV.2
    - [조건에 맞는 도서와 저자 리스트 출력하기](https://school.programmers.co.kr/learn/courses/30/lessons/144854)
    ```sql
    SELECT B.BOOK_ID, A.AUTHOR_NAME, DATE_FORMAT(B.PUBLISHED_DATE, "%Y-%m-%d") AS PUBLISHED_DATE
    FROM BOOK B
    JOIN AUTHOR A
    ON B.AUTHOR_ID = A.AUTHOR_ID
    WHERE CATEGORY = "경제"
    ORDER BY PUBLISHED_DATE
    ```
    - [상품 별 오프라인 매출 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/131533)
    ```sql
    SELECT P.PRODUCT_CODE, (P.PRICE * SUM(OS.SALES_AMOUNT)) AS SALES
    FROM PRODUCT P
    JOIN OFFLINE_SALE OS
    ON P.PRODUCT_ID = OS.PRODUCT_ID
    GROUP BY OS.PRODUCT_ID
    ORDER BY (P.PRICE * SUM(OS.SALES_AMOUNT)) DESC, P.PRODUCT_CODE ASC
    ```
    
- LV.3
    - [없어진 기록 찾기](https://school.programmers.co.kr/learn/courses/30/lessons/59042)
    ```sql
    SELECT ANIMAL_ID, NAME
    FROM ANIMAL_OUTS
    WHERE ANIMAL_ID NOT IN (
        SELECT ANIMAL_ID
        FROM ANIMAL_INS
    )
    ORDER BY ANIMAL_ID ASC
    ```
    - [있었는데요 없었습니다](https://school.programmers.co.kr/learn/courses/30/lessons/59043)
    ```sql
    SELECT AI.ANIMAL_ID, AI.NAME
    FROM ANIMAL_INS AI
    JOIN ANIMAL_OUTS AO
    ON AI.ANIMAL_ID = AO.ANIMAL_ID
    WHERE AI.DATETIME > AO.DATETIME
    ORDER BY AI.DATETIME ASC
    ```
    - [오랜 기간 보호한 동물(1)](https://school.programmers.co.kr/learn/courses/30/lessons/59044)
    ```sql
    SELECT NAME, DATETIME
    FROM ANIMAL_INS AI
    WHERE ANIMAL_ID NOT IN (
        SELECT ANIMAL_ID
        FROM ANIMAL_OUTS
    )
    ORDER BY DATETIME ASC
    LIMIT 3
    ```

- LV.4
    - [그룹별 조건에 맞는 식당 목록 출력하기](https://school.programmers.co.kr/learn/courses/30/lessons/131124)
    ```sql
    SELECT M.MEMBER_NAME, R.REVIEW_TEXT, DATE_FORMAT(R.REVIEW_DATE, "%Y-%m-%d") AS REVIEW_DATE
    FROM MEMBER_PROFILE M INNER JOIN REST_REVIEW R
    ON M.MEMBER_ID = R.MEMBER_ID
    WHERE M.MEMBER_ID = (
        SELECT MEMBER_ID FROM REST_REVIEW
        GROUP BY MEMBER_ID
        ORDER BY COUNT(*) DESC 
        LIMIT 1
    )
    ORDER BY REVIEW_DATE ASC, REVIEW_TEXT ASC;
    ```
    - [특정 기간동안 대여 가능한 자동차들의 대여비용 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/157339)
    ```sql
    SELECT M.MEMBER_NAME, R.REVIEW_TEXT, DATE_FORMAT(R.REVIEW_DATE, "%Y-%m-%d") AS REVIEW_DATE
    FROM MEMBER_PROFILE M INNER JOIN REST_REVIEW R
    ON M.MEMBER_ID = R.MEMBER_ID
    WHERE M.MEMBER_ID = (
        SELECT MEMBER_ID FROM REST_REVIEW
        GROUP BY MEMBER_ID
        ORDER BY COUNT(*) DESC 
        LIMIT 1
    )
    ORDER BY REVIEW_DATE ASC, REVIEW_TEXT ASC;
    ```
    - [주문량이 많은 아이스크림들 조회하기](https://school.programmers.co.kr/learn/courses/30/lessons/133027)
    ```sql
    SELECT A.FLAVOR
    FROM FIRST_HALF A
    JOIN (SELECT FLAVOR, SUM(TOTAL_ORDER) AS TOTAL_ORDER FROM JULY GROUP BY FLAVOR) B
    ON A.FLAVOR = B.FLAVOR
    ORDER BY (A.TOTAL_ORDER + B.TOTAL_ORDER) DESC
    LIMIT 3
    ```
    - [5월 식품들의 총매출 조회하기](https://school.programmers.co.kr/learn/courses/30/lessons/131117)
    ```sql
    SELECT A.PRODUCT_ID, A.PRODUCT_NAME, (A.PRICE * B.TOTAL_AMOUNT) AS TOTAL_SALES
    FROM FOOD_PRODUCT A
    JOIN (
        SELECT PRODUCT_ID, SUM(AMOUNT) AS TOTAL_AMOUNT
        FROM FOOD_ORDER
        WHERE PRODUCE_DATE LIKE '2022-05%'
        GROUP BY PRODUCT_ID
    ) B
    ON A.PRODUCT_ID = B.PRODUCT_ID
    ORDER BY TOTAL_SALES DESC, PRODUCT_ID ASC
    ```
    - [보호소에서 중성화한 동물](https://school.programmers.co.kr/learn/courses/30/lessons/59045)
    ```sql
    SELECT ANIMAL_ID, ANIMAL_TYPE, NAME
    FROM ANIMAL_INS
    WHERE SEX_UPON_INTAKE LIKE "Intact%"
        AND ANIMAL_ID IN (
            SELECT ANIMAL_ID
            FROM ANIMAL_OUTS
            WHERE SEX_UPON_OUTCOME IN (
                "Spayed Female", "Spayed Male", "Neutered Female", "Neutered Male"
            )
        )
    ORDER BY ANIMAL_ID ASC
    ```

- LV.5
    - [상품을 구매한 회원 비율 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/131534)
    ```sql
    SELECT YEAR, MONTH, COUNT(*) AS PUCHASED_USERS,
        ROUND((COUNT(*) / (SELECT COUNT(*) FROM USER_INFO WHERE YEAR(JOINED) = 2021)), 1) AS PUCHASED_RATIO
    FROM (
        SELECT DISTINCT YEAR(S.SALES_DATE) AS YEAR, MONTH(S.SALES_DATE) AS MONTH, U.USER_ID
        FROM ONLINE_SALE S
        JOIN USER_INFO U ON S.USER_ID = U.USER_ID AND YEAR(JOINED) = 2021
    ) A
    GROUP BY YEAR, MONTH
    ORDER BY YEAR, MONTH
    ```    
