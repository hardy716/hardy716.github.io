---
layout: post
title: Programmers SQL High Score Kit - GROUP BY
image: /assets/img/blog/programmers.jpg
accent_image: 
  background: url('/assets/img/sidebar-bg2.jpg') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  프로그래머스 스쿨에서 제공하는 SQL 고득점 Kit : GROUP BY 입니다. 
invert_sidebar: true
---

# SQL 고득점 Kit - GROUP BY

나랑 이름이 같은 사람은 몇 명일까요? 데이터를 묶고 평균값을 계산해보세요.

* toc
{:toc}


## GROUP BY

- LV.2
    - [진료과별 총 예약 횟수 출력하기](https://school.programmers.co.kr/learn/courses/30/lessons/132202)
    ```sql
    SELECT MCDP_CD AS '진료과 코드', COUNT(*) AS '5월예약건수'
    FROM APPOINTMENT
    WHERE APNT_YMD LIKE '2022-05%'
    GROUP BY MCDP_CD
    ORDER BY COUNT(*) ASC, MCDP_CD ASC
    ```
    - [성분으로 구분한 아이스크림 총 주문량](https://school.programmers.co.kr/learn/courses/30/lessons/133026)
    ```sql
    SELECT ICECREAM_INFO.INGREDIENT_TYPE, SUM(FIRST_HALF.TOTAL_ORDER) AS TOTAL_ORDER
    FROM FIRST_HALF JOIN ICECREAM_INFO
    ON FIRST_HALF.FLAVOR = ICECREAM_INFO.FLAVOR
    GROUP BY INGREDIENT_TYPE
    ORDER BY SUM(FIRST_HALF.TOTAL_ORDER)
    ```
    - [자동차 종류 별 특정 옵션이 포함된 자동차 수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/151137)
    ```sql
    SELECT CAR_TYPE, COUNT(*) AS CARS
    FROM CAR_RENTAL_COMPANY_CAR
    WHERE  OPTIONS REGEXP '통풍시트|열선시트|가죽시트'
    GROUP BY CAR_TYPE
    ORDER BY CAR_TYPE ASC
    ```
    - [고양이와 개는 몇 마리 있을까](https://school.programmers.co.kr/learn/courses/30/lessons/59040)
    ```sql
    SELECT ANIMAL_TYPE, COUNT(*) AS count
    FROM ANIMAL_INS
    GROUP BY ANIMAL_TYPE
    ORDER BY ANIMAL_TYPE ASC
    ```
    - [동명 동물 수 찾기](https://school.programmers.co.kr/learn/courses/30/lessons/59041)
    ```sql
    SELECT NAME, COUNT(NAME) AS COUNT
    FROM ANIMAL_INS 
    GROUP BY NAME 
    HAVING COUNT(NAME) > 1 
    ORDER BY NAME ASC
    ```
    - [입양 시각 구하기(1)](https://school.programmers.co.kr/learn/courses/30/lessons/59412)
    ```sql
    SELECT HOUR(DATETIME) AS HOUR, COUNT(DATETIME) AS COUNT
    FROM ANIMAL_OUTS
    WHERE HOUR(DATETIME) BETWEEN 9 AND 19
    GROUP BY HOUR 
    ORDER BY HOUR ASC
    ```
    - [가격대 별 상품 개수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/131530)
    ```sql
    SELECT FLOOR(PRICE/10000)*10000 AS PRICE_GROUP, COUNT(*) AS PRODUCTS
    FROM product
    GROUP BY PRICE_GROUP
    ORDER BY PRICE_GROUP ASC
    ```

- LV.3
    - [대여 횟수가 많은 자동차들의 월별 대여 횟수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/151139)
    ```sql
    WITH RENTAL_DATA AS (
        SELECT CAR_ID, MONTH(START_DATE) AS MONTH, COUNT(*) AS RECORDS
        FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
        WHERE YEAR(START_DATE) = 2022 AND MONTH(START_DATE) >= 8 AND MONTH(START_DATE) <= 10
        GROUP BY CAR_ID, MONTH(START_DATE)
    )
    SELECT MONTH, CAR_ID, RECORDS
    FROM RENTAL_DATA
    WHERE CAR_ID IN (SELECT CAR_ID FROM RENTAL_DATA GROUP BY CAR_ID HAVING SUM(RECORDS) >= 5)
    ORDER BY MONTH, CAR_ID DESC
    ```
    - [카테고리 별 도서 판매량 집계하기](https://school.programmers.co.kr/learn/courses/30/lessons/144855)
    ```sql
    SELECT b.CATEGORY, SUM(bs.SALES) AS TOTAL_SALES
    FROM BOOK b
    JOIN BOOK_SALES bs
    ON b.BOOK_ID = bs.BOOK_ID
    WHERE bs.SALES_DATE LIKE '2022-01%'
    GROUP BY b.CATEGORY
    ORDER BY b.CATEGORY ASC
    ```
    - [즐겨찾기가 가장 많은 식당 정보 출력하기](https://school.programmers.co.kr/learn/courses/30/lessons/131123)
    ```sql
    SELECT FOOD_TYPE, REST_ID, REST_NAME, FAVORITES
    FROM REST_INFO
    WHERE (FOOD_TYPE, FAVORITES) IN (SELECT FOOD_TYPE, MAX(FAVORITES) FROM REST_INFO GROUP BY FOOD_TYPE)
    ORDER BY FOOD_TYPE DESC
    ```
    - [자동차 대여 기록에서 대여중 / 대여 가능 여부 구분하기](https://school.programmers.co.kr/learn/courses/30/lessons/157340)
    ```sql
    SELECT CAR_ID,
    (CASE WHEN CAR_ID IN (
        SELECT CAR_ID
        FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
        WHERE '2022-10-16' BETWEEN DATE_FORMAT(START_DATE, '%Y-%m-%d') AND DATE_FORMAT(END_DATE, '%Y-%m-%d'))
    THEN '대여중'
    ELSE '대여 가능'
    END) AS 'AVAILABILITY'
    FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
    GROUP BY CAR_ID
    ORDER BY CAR_ID DESC
    ```

- LV.4
    - [식품분류별 가장 비싼 식품의 정보 조회하기](https://school.programmers.co.kr/learn/courses/30/lessons/131116)
    ```sql
    SELECT CATEGORY, PRICE AS MAX_PRICE, PRODUCT_NAME
    FROM FOOD_PRODUCT
    WHERE (CATEGORY, PRICE) IN (
        SELECT CATEGORY, MAX(PRICE) 
        FROM FOOD_PRODUCT
        WHERE CATEGORY IN ("과자", "국", "김치", "식용유")
        GROUP BY CATEGORY
    )
    ORDER BY PRICE DESC
    ```
    - [저자 별 카테고리 별 매출액 집계하기](https://school.programmers.co.kr/learn/courses/30/lessons/144856)
    ```sql
    SELECT A.AUTHOR_ID
         , A.AUTHOR_NAME
         , B.CATEGORY
         , SUM(BS.SALES * B.PRICE) AS TOTAL_SALES
    FROM AUTHOR A
    INNER JOIN BOOK B ON A.AUTHOR_ID = B.AUTHOR_ID
    INNER JOIN BOOK_SALES BS ON B.BOOK_ID = BS.BOOK_ID
    WHERE BS.SALES_DATE LIKE "2022-01%"
    GROUP BY A.AUTHOR_ID, A.AUTHOR_NAME, B.CATEGORY
    ORDER BY A.AUTHOR_ID ASC, B.CATEGORY DESC
    ```
    - [년, 월, 성별 별 상품 구매 회원 수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/131532)
    ```sql
    SELECT YEAR(OS.SALES_DATE) AS YEAR, MONTH(OS.SALES_DATE) AS MONTH, UI.GENDER, COUNT(DISTINCT OS.USER_ID) AS USERS
    FROM ONLINE_SALE OS
    JOIN USER_INFO UI
    ON OS.USER_ID = UI.USER_ID
    WHERE GENDER IS NOT Null
    GROUP BY YEAR(OS.SALES_DATE), MONTH(OS.SALES_DATE), UI.GENDER
    ORDER BY YEAR ASC, MONTH ASC, GENDER ASC
    ```
    - [입양 시각 구하기(2)](https://school.programmers.co.kr/learn/courses/30/lessons/59413)
    ```sql
    SET @HOUR = -1;
    SELECT (@HOUR := @HOUR +1) AS HOUR,
        (SELECT COUNT(HOUR(DATETIME)) 
        FROM ANIMAL_OUTS 
        WHERE HOUR(DATETIME)=@HOUR) AS COUNT 
        FROM ANIMAL_OUTS
    WHERE @HOUR < 23;
    ```
