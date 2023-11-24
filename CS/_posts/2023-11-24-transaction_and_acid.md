---
layout: post
title: 트랜잭션과 ACID
image: /assets/img/blog/cs/db/acid.png
accent_image: 
  background: url('/assets/img/sidebar/reference-room.jpg') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  트랜잭션과 ACID에 대해 공부한 내용을 정리했습니다.
invert_sidebar: true
---

# [CS - 데이터베이스] 트랜잭션과 ACID 속성

* toc
{:toc}


## 📥 트랜잭션

> A transaction is a unit of work that you want to treat as "a whole." It has to either happen in full or not at all.
> A classical example is transferring money from one bank account to another. To do that you have first to withdraw the amount from the source account, and then deposit it to the destination account. The operation has to succeed in full. If you stop halfway, the money will be lost, and that is Very Bad.
> In modern databases transactions also do some other things - like ensure that you can't access data that another person has written halfway. But the basic idea is the same - transactions are there to ensure, that **no matter what happens, the data you work with will be in a sensible state**. They guarantee that there will NOT be a situation where money is withdrawn from one account, but not deposited to another.
> [What is a database transaction?](https://stackoverflow.com/questions/974596/what-is-a-database-transaction)

데이터베이스와 데이터 스토리지 시스템이라는 맥락에서 트랜잭션이란, 논리적으로 한 단위의 작업으로 취급되는 모든 작업을 말한다.

트랜잭션은 모든 작업이 성공할 때만 성공하는 데이터베이스 읽기 및 쓰기 작업 그룹이다.

## 🗝️ ACID 속성

ACID는 트랜잭션을 정의하는 4가지 중대한 속성을 가리키는 약어로, 다음과 같이 구성되어 진다.

> A - Atomicity : 원자성
> C - Consistency : 일관성
> I - Isolation : 격리성
> D - Durability : 영속성

![file_system](/assets/img/blog/cs/db/acids.png){: width="80%"}

#### 원자성 (Atomicity)

원자성은 '모두 또는 아무것도 없는 규칙'이라고 할 수 있다.

즉, 모든 데이터 조작 작업은 성공하거나 실패할 때까지 적용되지 않거나 롤백 한다.

트랜잭션은 하나의 논리적인 작업 단위로 간주되며, 부분적으로 발생하지 않는다.

#### 일관성 (Consistency)

일관성은 데이터베이스가 트랜잭션 전후에 일관성이 있도록 무결성 제약을 유지해야 한다는 것을 의미한다.

#### 격리성 (Isolation)

동시에 여러 트랜잭션이 발생할 때, 각 트랜잭션이 서로 간섭 없이 독립적으로 이루어진다는 것을 의미한다.

다시 말해, 특정 트랜잭션에 발생하는 변경 사항은 해당 트랜잭션의 특정 변경 사항이 메모리에 기록되거나 커밋될 때까지 다른 트랜잭션에서 볼 수 없다.

이러한 격리성은 어떤 트랜잭션의 작업이 동시에 발생한 다른 트랜잭션에게 영향을 미치지 않도록 보장한다.

#### 지속성 (Durability)

지속성은 트랜잭션이 완료되면 데이터베이스에 대한 업데이트 및 수정 사항이 영구적으로 저장되어야 한다는 것을 의미한다.

어떠한 상황일지라도(시스템 오류가 발생해도) 트랜잭션의 결과는 영구화되고 비휘발성 메모리에 저장되어 그 효과가 결코 사라지지 않도록 해야 한다.


전체적으로 ACID 속성은 각 트랜잭션이 단일 단위로 작동하고, 일관된 결과를 생성하고, 다른 작업과 분리되어 작동하며, 업데이트가 영구적으로 저장되는 방식으로 데이터베이스의 정확성과 일관성을 보장하는 메커니즘을 제공한다.


#### 참고한 문서들

[geeksforgeeks - ACID Properties in DBMS](https://www.geeksforgeeks.org/acid-properties-in-dbms/)

[MongoDB - What are ACID Properties in Database Management Systems?](https://www.mongodb.com/basics/acid-transactions)

[redis - ACID Transactions](https://redis.com/glossary/acid-transactions/)

[databricks - ACID 트랜잭션](https://www.databricks.com/kr/glossary/acid-transactions)
