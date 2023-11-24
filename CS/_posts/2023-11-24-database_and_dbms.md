---
layout: post
title: 데이터베이스와 DBMS
image: /assets/img/blog/cs/db/dbs.png
accent_image: 
  background: url('/assets/img/sidebar/reference-room.jpg') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  데이터베이스와 DBMS에 대해 공부한 내용을 정리했습니다.
invert_sidebar: true
---

# [CS - 데이터베이스] 데이터베이스와 DBMS

* toc
{:toc}


## 🔋 데이터베이스와 DBMS

> 데이터베이스는 전자적으로 저장되고 체계적인 데이터 모음입니다. 여기에는 단어, 숫자, 이미지, 비디오 및 파일을 포함한 모든 유형의 데이터가 포함될 수 있습니다. DBMS (데이터베이스 관리 시스템) 라는 소프트웨어를 사용하여 데이터를 저장, 검색 및 편집할 수 있습니다. 컴퓨터 시스템에서 _데이터베이스라는_ 단어는 모든 DBMS, 데이터베이스 시스템 또는 데이터베이스와 관련된 응용 프로그램을 나타낼 수도 있습니다.
> [aws - 데이터베이스란 무엇입니까?](https://aws.amazon.com/ko/what-is/database/)

#### 데이터베이스, DB

데이터베이스(DataBase, DB)는 여러 사람이 공유하여 사용할 목적으로 통합 관리되는 데이터 모음이다.

1950년대에 군사적 목적으로 '데이터의 기지'라는 뜻으로 미국에서 처음 사용되었으며, 이후 1963년 시스템 디벨로프사가 개최한 심포지엄에서 이를 차용하였다고 한다.

#### 데이터베이스 관리 시스템, DBMS

![file_system](/assets/img/blog/cs/db/file_system.png){: width="80%"}

> [데이터베이스 관리 시스템의 등장 배경, 한라대학교 ICT융합공학부 (파일 다운로드)](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwjA9rq3j9uCAxWSa_UHHYr0BnkQFnoECA0QAQ&url=https%3A%2F%2Fict.halla.ac.kr%2Fbbs%2Fict%2F258%2F28843%2Fdownload.do&usg=AOvVaw3thxu9W5Enw4Gj2f312u_Q&opi=89978449)

DBMS가 등장하기 전까지는 운영체제상의 파일에 각종 데이터들을 저장하는 `파일 시스템`을 사용했다.

파일 시스템은 (저장공간의 낭비)와 (데이터 일관성과 무결성을 유지하기 어렵다는 점), (응용 프로그램이 데이터 파일에 종속적이라는 점) 등 여러 문제점과 한계가 존재했고, DBMS는 이를 해결하기 위해 제시되었다고 한다.

데이터베이스 관리 시스템(DataBase Management System, DBMS)은 데이터베이스를 조작 및 관리하는 별도의 소프트웨어 도구의 모음으로, 다수의 사용자나 응용 프로그램들이 데이터베이스를 공유하고, 접근할 수 있는 환경을 제공한다.

DBMS와 관련해서 참고할 만한 좋은 블로그 글이 있어서 아래에 소개하고자 한다.

[마케터 루시씨 블로그 - 데이터베이스 뽀개기 (1) DBMS란 무엇이고 왜 등장했는가?](https://lucy-the-marketer.kr/ko/growth/what-is-database/)


## 🛢️ DBMS의 종류

![dbms](/assets/img/blog/cs/db/dbms.png){: width="80%"}

> [한빛 미디어 - 데이터베이스 이해하기](https://hongong.hanbit.co.kr/데이터베이스-이해하기-databasedb-dbms-sql의-개념/)

DBMS의 유형은 계층형(Hierarchical), 망형(Network), 관계형(Relational), 객체지향형(Object-Oriented), 객체관계형(Object-Relational) 등으로 분류된다. 

현재 사용되는 DBMS 중에는 관계형 DBMS가 가장 많은 부분을 차지하며, MySQL도 관계형 DBMS에 포함된다.

계층형 DBMS와 망형 DBMS는 현재 거의 사용하지 않는 형태이다.

#### 관계형 데이터베이스 관리 시스템, RDBMS

> 관계형 데이터베이스는 데이터가 하나 이상의 열과 행의 테이블(또는 '관계')에 저장되어 서로 다른 데이터 구조가 어떻게 관련되어 있는지 쉽게 파악하고 이해할 수 있도록 사전 정의된 관계로 데이터를 구성하는 정보 모음입니다. 관계는 이러한 테이블 간의 상호작용을 기반으로 설정되는 여러 테이블 간의 논리적 연결입니다.
> [Google Cloud - 관계형 데이터베이스란 무엇인가요?](https://cloud.google.com/learn/what-is-a-relational-database?hl=ko)

관계형 데이터베이스 관리 시스템(Relational DataBase Management System, RDBMS)의 데이터베이스는 테이블(table)이라는 최소 단위로 구성되며, 테이블은 하나 이상의 열(column)과 행(row)으로 이루어져 있다.

즉, RDBMS는 데이터를 테이블 형태(열 & 행)로 저장한다고 생각하면 된다.

#### 구조적 쿼리 언어, SQL

구조적 쿼리 언어(Structured Query Language, SQL)는 관계형 데이터베이스에서 정보를 저장하고 처리하기 위한 프로그래밍 언어이다.

SQL 문을 사용하여 데이터베이스에서 정보를 저장, 업데이트, 제거, 검색 등을 수행할 수 있으며, 데이터베이스 성능을 유지 관리하고 최적화하는 데 사용할 수도 있다.

![sql](/assets/img/blog/cs/db/sql.png){: width="80%"}

SQL의 종류는 크게 DML, DDL, DCL로 구분할 수 있으며, DCL에서의 COMMIT, ROOLBACK, SAVEPOINT를 TCL로 따로 분류하는 문서도 있다.

SQL에 대해 더 자세히 알고 싶다면 아래 글을 참고하는 것을 추천한다.

[aws - SQL(구조적 쿼리 언어)이란 무엇인가요?](https://aws.amazon.com/ko/what-is/sql/)


## 🗞️ 비관계형 데이터베이스 및 NoSQL

> 비관계형 데이터베이스는 대부분의 전형적인 데이터베이스 시스템에서 찾을 수 있는 행과 열로 이루어진 테이블 형식 스키마를 사용하지 않는 데이터베이스입니다. 대신 비관계형 데이터베이스는 저장되는 데이터 형식의 특정 요구 사항에 맞게 최적화된 스토리지 모델을 사용합니다. 예를 들어, 데이터는 단순 키/값 쌍, JSON 문서 또는 모서리와 꼭짓점으로 이루어진 그래프로 저장될 수 있습니다.
> [Microsoft - 비관계형 데이터 및 NoSQL](https://learn.microsoft.com/ko-kr/azure/architecture/data-guide/big-data/non-relational-data)

> NoSQL이라는 용어는 비관계형 데이터베이스 유형을 가리키며 이 데이터베이스는 관계형 테이블과는 다른 형식으로 데이터를 저장합니다. 그러나 NoSQL 데이터베이스는 언어마다 관습화된 API, 선언적 구조의 쿼리 언어, 쿼리별 언어를 사용하여 질의할 수 있습니다. 이 데이터베이스가 not only SQL 데이터베이스라고 불리는 이유가 바로 이것이죠.
> [oracle - NoSQL이란 무엇인가?](https://www.oracle.com/kr/database/nosql/what-is-nosql/)

NoSQL(Not only SQL)은 SQL만을 사용하지 않는 데이터베이스 관리 시스템을 지칭하는 단어, 즉 비관계형 데이터베이스를 지칭한다. 

2000년 후반으로 넘어오면서 인터넷이 활성화되고 소셜네트워크 서비스 등이 등장하면서 관계형 데이터(또는 정형데이터)가 아닌 비정형 데이터들을 처리해야 할 필요성이 늘어났고, 이에 따라 NoSQL이 각광을 받게 되었다고 한다.

NoSQL 데이터베이스는 작업을 진행하는 동시에 데이터를 정의하는 방식으로 빠르게 데이터를 작성하고 반복할 수 있는 능력이 있으며, 신속한 수평적 확장 능력을 기반으로 높은 트래픽을 처리할 수 있다고 한다.

NoSQL은 높은 확장성과 가용성을 바탕으로 실시간 웹 애플리케이션 및 빅데이터 처리에 널리 사용된다.

NoSQL에 대해 더 자세히 알고 싶다면 아래 글을 참고하는 것을 추천한다.

[oracle - NoSQL이란 무엇인가?](https://www.oracle.com/kr/database/nosql/what-is-nosql/)
