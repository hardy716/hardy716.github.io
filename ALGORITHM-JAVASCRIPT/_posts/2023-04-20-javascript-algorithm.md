---
layout: post
title: Javascript - Algorithm
image:
accent_image: 
  background: url('/assets/img/sidebar-bg3.jpg') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  자바스크립트를 사용하여 알고리즘 문제를 풀고 기록합니다.
invert_sidebar: true
---

# Javascript - Algorithm

* toc
{:toc}

## [프로그래머스 코딩테스트 고득점 Kit](https://school.programmers.co.kr/learn/challenges?tab=algorithm_practice_kit)

코딩테스트에는 어떤 알고리즘/자료구조가 출제될까요?
사람들은 어떤 문제를 어려워할까요? 국내에서 코딩테스트를 가장 많이 운영해온 프로그래머스 팀이 코딩테스트 결과를 분석해서 만든 고득점 Kit. 코딩테스트에 자주 나오는 유형, 사람들이 많이 틀리는 유형을 간추렸습니다.


### 해시

#### [폰켓몬](https://school.programmers.co.kr/learn/courses/30/lessons/1845)

```javascript
/* redefine(재정의) */

// input : nums(폰켓몬의 종류 번호가 담긴 1차원 Array)
// return : N/2마리의 폰켓몬을 선택하는 방법 중, 최대로 가질 수 있는 포켓몬 종류 수

// condition : N은 짝수 -> N/2는 항상 정수(parseInt 생략 가능)

// algorithm : 해시 - set




/* solution(구현) */

function solution(nums) {
    
    const N = nums.length;           // nums의 길이
    const nums_set = new Set(nums);  // 폰켓몬의 종류 set

    //  nums_set의 size는 폰켓몬 종류 수
    //  (폰켓몬 종류 수 >= 폰켓몬 개수) ? 폰켓몬 개수 : 폰켓몬 종류 수
    answer = Math.min(nums_set.size, N/2);
    
    return answer;
}




/* check(검증) - Big O Notation */

// time complexity  : O(1)
// space complexity : O(n)
```

#### [위장](https://school.programmers.co.kr/learn/courses/30/lessons/42578)

```javascript
/* redefine(재정의) */

// input : clothes(스파이 의상 2차원 Array)
// return : 서로 다른 옷의 조합 수

// condition1 : 의상의 수는 [1,30]
// condition2 : 의상의 이름은 유일
// condition3 : 문자열 길이 [1,20]
// condition4 : 최소 한 개의 의상을 입어야 함

// algorithm : 해시 - object

// logic(psuedo) :
// 1. clothType을 키로 하는 해시 테이블을 구현한다. {A:a, B:b, C:c, D:d}
// 2. 해시 테이블 생성과 동시에 키 리스트(clothesType)도 생성한다. {A, B, C, D}
// 3. clothesType의 요소를 순회하면서 경우의 수를 구한다(키가 존재하지 않는다면 값에 0 대입). ->  (a+1)*(b+1)*(c+1)*(d+1) - 1




/* solution(구현) */

function solution(clothes) {
    let clothesDict = {};
    let clothesType = [];
    
    let answer = 1;
    
    for (let [clothName, clothType] of clothes) {
        if (!clothesDict[clothType]) {
            clothesDict[clothType] = 0
            clothesType.push(clothType);
        }
        clothesDict[clothType] += 1
    }

    for (let k of clothesType) {
        answer *= clothesDict[k] + 1
    }
    
    
    return answer - 1;
}




/* check(검증) - Big O Notation */

// time complexity  : O(n)
// space complexity : O(n)
```

#### [완주하지 못한 선수](https://school.programmers.co.kr/learn/courses/30/lessons/42576)

```javascript
/* redefine(재정의) */

// input1 : participant(마라톤 참여한 선수들 이름이 담긴 Array)
// input2 : completion(마라톤 완주한 선수들 이름이 담긴 Array)
// return : 마라톤을 완주하지 못한 선수들의 이름을 문자열로 return

// condition1 : 참가자 이름은 알파벳 소문자(20자내)
// condition2 : 참가자 동명이인 가능
// condition3 : 완주 못 한 참가자는 1명
// condition4 : participant.length <= 100,000

// algorithm : 해시 - object

// logic(psuedo) : 
// 1. 참가자 명을 키로 하는 해시 테이블을 구현한다.
// 2. 참가 +1, 완주 -1 하며 값을 계속 갱신한다
// 3. 순회하면서 값이 0을 초과하는 키를 반환한다.




/* solution(구현) */

function solution(participant, completion) {
    
    const participantDict = {};

    for (let i in participant) {
        if (!participantDict[participant[i]]) {
            participantDict[participant[i]] = 0;
        }
        participantDict[participant[i]] += 1
        if (!participantDict[completion[i]]) {
            participantDict[completion[i]] = 0;
        }
        participantDict[completion[i]] -= 1
    }

    for (let k of Object.keys(participantDict)) {    // Object.keys : O(n)
        if (participantDict[k] > 0) {
            return k;
        }
    }
}




/* check(검증) - Big O Notation */

// time complexity  : O(n^2)
// space complexity : O(n)




/* improvements(개선점) */
// completion 배열의 길이가 participant 배열의 길이보다 1 작기 때문에,
// 마지막 n번째 순회 시 의도하지 않은 키-값 쌍(undefined: -1)이 participantDict에 추가된다.
// participantDict[k] > 0을 만족하지 않아 문제 풀이에 큰 영향은 없지만 useless code이므로 예외처리(82)

function solution(participant, completion) {
    
    const participantDict = {};

    for (let i in participant) {
        if (!participantDict[participant[i]]) {
            participantDict[participant[i]] = 0;
        }
        participantDict[participant[i]] += 1
        if (!participantDict[completion[i]]) {
            participantDict[completion[i]] = 0;
        }
        participantDict[completion[i]] -= 1
    }

    delete participantDict.undefined;    // 예외 처리 : participantDict의 프로퍼티 키가 Undefined인 속성 delete(O(1))

    for (let k of Object.keys(participantDict)) {
        if (participantDict[k] > 0) {
            return k;
        }
    }
}




/* recheck(검증) - Big O Notation */

// time complexity  : O(n^2)
// space complexity : O(n)
```

### 탐욕법

#### [구명보트](https://school.programmers.co.kr/learn/courses/30/lessons/42885)

```javascript
/* redefine(재정의) */

// input1 : people(사람 몸무게를 담은 1차원 Array)
// input2 : limit(최대 하중 Number)
// return : 필요한 구명보트 개수의 최솟값 Number

// condition1 : people 길이 : [1, 50000]
// condition2 : people 요소 크기 : [40, 240]
// condition3 : limit 크기 : [40,240]
// condition4 : people 요소 크기 최댓값 < limit 
// condition5 : 구명보트 최대 탑승인원 2인

// <condition5> : people은 비정렬 상태

// algorithm : 그리디, 큐?

// logic(psuedo) : 
// 1. 오름차순 정렬
// 2. 만약, 가장 가벼운 사람 + 기장 무거운 사람 <= left++, right-- (2인 탑승)
// 2. 만약, 가장 가벼운 사람 + 가장 무거운 사람 > right-- (1인: 가장 무거운 사람 탑승)
// 3. 예외 처리
//    마지막에 남은 인원이 모두 탑승한 경우(2인 탑승) 구명보트 추가 X

/* solution(구현) */

function solution(people, limit) {
    
    let cnt = 1;                   // 구명보트 개수 1로 초기화

    let left = 0;
    let right = people.length-1;

    people.sort((a, b) => a - b);  // people 내림차순 정렬

    while (left < right) {   
        if (people[left] + people[right] <= limit) { 
            left++;
            if (left === right) cnt--;
        }
        right--;
        cnt++;  // 다음 구명보트 준비
    }
    
    return cnt;
}

/* 결과 */
// 정확성  테스트
// 테스트 1 〉    통과 (1.94ms, 35.5MB)
// 테스트 2 〉    통과 (1.07ms, 33.6MB)
// 테스트 3 〉    통과 (1.16ms, 33.7MB)
// 테스트 4 〉    통과 (1.11ms, 33.6MB)
// 테스트 5 〉    통과 (0.76ms, 33.6MB)
// 테스트 6 〉    통과 (0.42ms, 33.7MB)
// 테스트 7 〉    통과 (0.60ms, 33.6MB)
// 테스트 8 〉    통과 (0.16ms, 33.6MB)
// 테스트 9 〉    통과 (0.20ms, 33.7MB)
// 테스트 10 〉 통과 (1.86ms, 33.6MB)
// 테스트 11 〉 통과 (1.79ms, 33.6MB)
// 테스트 12 〉 통과 (0.91ms, 33.7MB)
// 테스트 13 〉 통과 (1.08ms, 33.6MB)
// 테스트 14 〉 통과 (1.25ms, 33.8MB)
// 테스트 15 〉 통과 (0.21ms, 33.7MB)
// 효율성  테스트
// 테스트 1 〉    통과 (14.94ms, 38.3MB)
// 테스트 2 〉    통과 (12.88ms, 38.2MB)
// 테스트 3 〉    통과 (62.95ms, 37.8MB)
// 테스트 4 〉    통과 (11.53ms, 38.5MB)
// 테스트 5 〉    통과 (10.42ms, 38.1MB)




/* check(검증) - Big O Notation */

// time complexity  : O(nlogn)
// space complexity : O(1)

// 위 코드의 시간 복잡도는 O(nlogn) 이다.
// 이 코드는 먼저 people 배열을 내림차순으로 정렬하기 위해 sort() 함수를 사용하는데 이는 시간 복잡도가 O(nlogn) 이다. 
// 그리고 while문에서는 left와 right 포인터를 이용하여 인덱스를 이동하며 구명보트를 결정하는데 이는 O(n) 이다.
// 그리고 공간 복잡도는 O(1) 이다.
// 코드는 people 배열만을 사용하고 정렬된 people 배열을 저장하는 공간을 추가로 사용하지 않기 때문에, 추가적인 메모리 공간을 사용하지 않는다.
```

#### [조이스틱](https://school.programmers.co.kr/learn/courses/30/lessons/42860)

```javascript
/* redefine(재정의) */

// input : name(만들고자 하는 이름 String)
// return : 조이스틱 조작 횟수의 최솟값(Number)

// condition1 : name은 모두 알파벳 대문자(65~)
// condition2 : name 길이 : [1,20]

// algorithm : 그리디


/* solution(구현) */

function solution(name) {
    let cnt = 0;
    
    let start = "A".charCodeAt();    // A의 아스키코드 
    let end = "Z".charCodeAt() + 1;  // B의 아스키코드 + 1
    let center = (start + end) / 2;  // 중간
    
    let move = name.length - 1;      // 좌우 초기값 설정
    
    for (let i = 0; i < name.length; i++) {
        
        let charCode = name.charCodeAt(i);    // 위/아래 조작 방향 선택하기
        (charCode < center) ? cnt += charCode - start : cnt += end - charCode
        
        let indexNotA = i + 1;    // 다음 커서부터 조작해야하는 문자 찾기
        while (indexNotA < name.length && name[indexNotA] == 'A') { indexNotA++; }
        
        move = Math.min(
            move,                               // 이전 값
            (i * 2) + name.length - indexNotA,  // 정방향 -> 역방향 
            (name.length - indexNotA) * 2 + i   // 역방향 -> 정방향
        )
    }

    return cnt + move;
}


/* 결과 */
// 정확성
// 테스트 1 〉    통과 (0.06ms, 33.4MB)
// 테스트 2 〉    통과 (0.06ms, 33MB)
// 테스트 3 〉    통과 (0.06ms, 33.1MB)
// 테스트 4 〉    통과 (0.07ms, 33.4MB)
// 테스트 5 〉    통과 (0.07ms, 33.4MB)
// 테스트 6 〉    통과 (0.06ms, 33.5MB)
// 테스트 7 〉    통과 (0.07ms, 33.4MB)
// 테스트 8 〉    통과 (0.06ms, 33.4MB)
// 테스트 9 〉    통과 (0.08ms, 33.4MB)
// 테스트 10 〉 통과 (0.15ms, 33.4MB)
// 테스트 11 〉 통과 (0.15ms, 33.5MB)
// 테스트 12 〉 통과 (0.15ms, 33.4MB)
// 테스트 13 〉 통과 (0.15ms, 33.4MB)
// 테스트 14 〉 통과 (0.15ms, 33.4MB)
// 테스트 15 〉 통과 (0.16ms, 33.5MB)
// 테스트 16 〉 통과 (0.06ms, 33.4MB)
// 테스트 17 〉 통과 (0.06ms, 32.8MB)
// 테스트 18 〉 통과 (0.14ms, 32.8MB)
// 테스트 19 〉 통과 (0.07ms, 33.4MB)
// 테스트 20 〉 통과 (0.15ms, 33.4MB)
// 테스트 21 〉 통과 (0.06ms, 33.4MB)
// 테스트 22 〉 통과 (0.15ms, 33.4MB)
// 테스트 23 〉 통과 (0.21ms, 33.4MB)
// 테스트 24 〉 통과 (0.07ms, 33.4MB)
// 테스트 25 〉 통과 (0.16ms, 33.5MB)
// 테스트 26 〉 통과 (0.14ms, 33.5MB)
// 테스트 27 〉 통과 (0.14ms, 33.4MB)



/* check(검증) - Big O Notation */

// time complexity  : O(n^2)
// space complexity : O(1)
```

#### [체육복](https://school.programmers.co.kr/learn/courses/30/lessons/42862)

```javascript
/* redefine(재정의) */

// input1 : n(전체 학생들의 수)
// input2 : lost(체육복을 도난당한 학생들의 번호(Number)가 담긴 1차원 Array)
// input3 : reserve(여벌옷을 가지고 있는 학생들의 번호(Number)가 담긴 1차원 Array)
// return : 체육 수업을 들을 수 있는 학생들의 수(Number)

// condition1 : 전체 학생 수 : [2,30]
// condition2 : lost, reserve 모두 length : [1,n], 중복X
// condition3 : 여벌 옷을 가지고 온 학생들도 도난(두 개 중 하나만)당할 수 있음

// algorithm : 그리디

// logic(psuedo) : 잎 반호의 학생을 우선적으로 탐색




/* solution(구현) */

function solution(n, lost, reserve) {
    
    const studentClothes = new Array(n).fill(1);             // 기본 값 설정(1) 
     
    lost.map(num => {studentClothes[num - 1] = 0});      // 도난 옷 갱신(-1)
    reserve.map(num => {studentClothes[num - 1] += 1});  // 여벌 옷 갱신(+1)

    let cnt = n;
    for(let num=0; num < n; num++) {
        
        if (studentClothes[num] === 0) {               // 해당 번호의 학생이 체육복이 없다면,             
            studentClothes[num] = 1;                   // 여벌의 옷을 받는다고 가정(+1)
            
            if (studentClothes[num - 1] === 2) {       // 앞 번호의 학생에게 여벌 옷이 있다면,
                studentClothes[num - 1] = 1;           // 앞 번호의 학생 1로 초기화(-1)
            }
            else if (studentClothes[num + 1] === 2) {  // 뒤 번호의 학생에게 여벌 옷이 있다면,
                studentClothes[num + 1] = 1;           // 뒤 번호의 학생 1로 초기화(-1)
            }
            else {                                     // 앞, 뒤 번호의 학생 모두 여벌 옷이 없다면,
                studentClothes[num] = 0;               // 현재 번호의 학생 0으로 초기화
                cnt--;                                 // 체육 수업을 듣는 학생 수 감소(1)
            }
        }
    }
    
    return cnt;
}


/* 결과 */
// 정확성
// 테스트 1 〉    통과 (0.08ms, 33.4MB)
// 테스트 2 〉    통과 (0.17ms, 33.6MB)
// 테스트 3 〉    통과 (0.16ms, 33.4MB)
// 테스트 4 〉    통과 (0.08ms, 33.4MB)
// 테스트 5 〉    통과 (0.15ms, 33.5MB)
// 테스트 6 〉    통과 (0.07ms, 33.4MB)
// 테스트 7 〉    통과 (0.16ms, 33.4MB)
// 테스트 8 〉    통과 (0.07ms, 33.4MB)
// 테스트 9 〉    통과 (0.08ms, 33.4MB)
// 테스트 10 〉 통과 (0.17ms, 33.4MB)
// 테스트 11 〉 통과 (0.08ms, 33.4MB)
// 테스트 12 〉 통과 (0.07ms, 33.5MB)
// 테스트 13 〉 통과 (0.08ms, 33.4MB)
// 테스트 14 〉 통과 (0.08ms, 33.4MB)
// 테스트 15 〉 통과 (0.07ms, 33.4MB)
// 테스트 16 〉 통과 (0.07ms, 33.5MB)
// 테스트 17 〉 통과 (0.07ms, 33.5MB)
// 테스트 18 〉 통과 (0.07ms, 33.4MB)
// 테스트 19 〉 통과 (0.07ms, 33.5MB)
// 테스트 20 〉 통과 (0.07ms, 33.6MB)
// 테스트 21 〉 통과 (0.07ms, 33.1MB)
// 테스트 22 〉 통과 (0.07ms, 33.5MB)
// 테스트 23 〉 통과 (0.07ms, 33.4MB)
// 테스트 24 〉 통과 (0.07ms, 33.4MB)
// 테스트 25 〉 통과 (0.07ms, 33.4MB)



/* check(검증) - Big O Notation */

// time complexity  : O(n)
// space complexity : O(n)
```

#### [큰 수 만들기](https://school.programmers.co.kr/learn/courses/30/lessons/42883)

```javascript
/* redefine(재정의) */

// input : number(문자열 형식의 숫자 String)
// return : k(제거할 개수)

// condition1 : number 길이 : [2,1000000]
// condition2 : k 크기 : [1, number 길이)

// algorithm : 그리디

// logic(psuedo) : 부분배열에서 최댓값을 구하고 필요없는 값들은 제거하는 방식을 반복




/* solution(구현) - 시간초과(10, 12) */

function solution(number, k) {
    let answer = '';
    let numList = [...number];
    let startIdx = 0;
    let delCnt = 0;
    
    let ord = 0;
    while (k - delCnt > 0) {
        ord++;
        let maxIdx = 0;
        let maxNum = -1;
        
        for (let i = startIdx; i < startIdx + k - delCnt + 1; i++) {
            if (numList[i] > maxNum) {
                maxNum = numList[i];
                maxIdx = i;
                if (maxNum === 9) break;  // 예외 처리
            }
        }

        answer += maxNum;
        startIdx = maxIdx + 1;
        delCnt = startIdx - ord;

    }
    
    if (startIdx - 1 < number.length) { answer += number.substr(startIdx) }
    
    return answer;
}


/* 결과 */
// 정확성
// 테스트 1 〉    통과 (0.06ms, 33.4MB)
// 테스트 2 〉    통과 (0.15ms, 33.3MB)
// 테스트 3 〉    통과 (0.16ms, 33.4MB)
// 테스트 4 〉    통과 (0.18ms, 33.4MB)
// 테스트 5 〉    통과 (0.51ms, 33.4MB)
// 테스트 6 〉    통과 (82.85ms, 36.8MB)
// 테스트 7 〉    통과 (168.04ms, 37.3MB)
// 테스트 8 〉    통과 (1290.72ms, 38.1MB)
// 테스트 9 〉    통과 (5.32ms, 38.5MB)
// 테스트 10 〉 실패 (시간 초과)
// 테스트 11 〉 통과 (0.08ms, 33.4MB)
// 테스트 12 〉 실패 (시간 초과)



/* check(검증) - Big O Notation */

// time complexity  : O(n^2)
// space complexity : O(n)




/* improvements(개선점) */

// 1. numList = [...number]을 생성하지 말고 charAt()을 이용하여 문자열에서 문자 추출
//   -> 시간복잡도 개선 X(유의미한 차이가 없음)
// 2. 스택 자료구조 이용

function solution(number, k) {
    const arr = [];
    // 반복문을 통해 number의 길이만큼 반복
    for (let i = 0; i < number.length; i++) {
        // arr의 길이가 0보다 크고, 
        // arr의 마지막 요소가 number[i]보다 작고, 
        // k가 0보다 클 때
        while (
            arr.length > 0 
            && arr[arr.length - 1] < number[i] 
            && k > 0
        ) {
            // k를 1 감소
            k--;
            // arr의 마지막 요소를 제거
            arr.pop();
        }
        // number[i]를 arr에 추가
        arr.push(number[i]);
    }
    // arr의 길이에서 k를 뺀 값만큼 제거
    arr.splice(number.length - k);
    // arr를 join 해서 문자열로 반환
    return arr.join("");
}



/* 결과 */
// 정확성
// 테스트 1 〉    통과 (0.05ms, 33.4MB)
// 테스트 2 〉    통과 (0.14ms, 33.5MB)
// 테스트 3 〉    통과 (0.14ms, 33.5MB)
// 테스트 4 〉    통과 (0.23ms, 33.6MB)
// 테스트 5 〉    통과 (0.28ms, 33.6MB)
// 테스트 6 〉    통과 (7.23ms, 37.2MB)
// 테스트 7 〉    통과 (7.40ms, 38.6MB)
// 테스트 8 〉    통과 (10.04ms, 39.9MB)
// 테스트 9 〉    통과 (29.42ms, 54.6MB)
// 테스트 10 〉 통과 (32.01ms, 49.6MB)
// 테스트 11 〉 통과 (0.05ms, 33.6MB)
// 테스트 12 〉 통과 (0.05ms, 33.5MB)   


/* check(검증) - Big O Notation */

// time complexity  : O(n^2)
// space complexity : O(n)
```

### 정렬

#### [H-Index](https://school.programmers.co.kr/learn/courses/30/lessons/42747)

```javascript
/* redefine(재정의) */

// input : citations(발표한 논문 n편의 인용 횟수를 담은 1차원 Array)
// return : H-Index

// condition1 : 논문의 수 N : [1, 1000]
// condition1 : 논문별 인용 횟수(citations[i]) : [1, 1000]

// algorithm : 정렬(내림차순) : sort((a,b) => b - a)




/* solution(구현) */

function solution(citations) {
    let answer = 0;
    citations.sort((a, b) => b - a);    // 공간복잡도 O(n/2)    
    
    while (true) {
        if (citations[answer] >= Math.max(answer + 1, citations.length - answer)) {
            answer++;
        } else {
           return answer;
        }
    }
}


/* 결과 */
// 정확성
// 테스트 1 〉    통과 (0.27ms, 33.4MB)
// 테스트 2 〉    통과 (0.35ms, 33.5MB)
// 테스트 3 〉    통과 (0.33ms, 33.6MB)
// 테스트 4 〉    통과 (0.32ms, 33.5MB)
// 테스트 5 〉    통과 (0.36ms, 33.3MB)
// 테스트 6 〉    통과 (0.39ms, 33.5MB)
// 테스트 7 〉    통과 (0.22ms, 33.5MB)
// 테스트 8 〉    통과 (0.14ms, 33.2MB)
// 테스트 9 〉    통과 (0.15ms, 33.5MB)
// 테스트 10 〉 통과 (0.24ms, 33.5MB)
// 테스트 11 〉 통과 (0.41ms, 33.5MB)
// 테스트 12 〉 통과 (0.16ms, 33.5MB)
// 테스트 13 〉 통과 (0.38ms, 33.4MB)
// 테스트 14 〉 통과 (0.36ms, 33.4MB)
// 테스트 15 〉 통과 (0.39ms, 33.5MB)
// 테스트 16 〉 통과 (0.05ms, 33.5MB)




/* check(검증) - Big O Notation */

// time complexity  : O(n)
// space complexity : O(n/2)




/* improvements(개선점) - 가독성 개선 */

function solution(citations) {
    let answer = 0;
    let flag = true;
    
    citations.sort((a, b) => b - a);      
    
    while (flag) {   
        citations[answer] >= Math.max(answer + 1, citations.length - answer)
        ? answer++
        : flag = false
    }
    
    return answer;
}


/* 결과 */
// 정확성
// 테스트 1 〉    통과 (0.27ms, 33.6MB)
// 테스트 2 〉    통과 (0.36ms, 33.5MB)
// 테스트 3 〉    통과 (0.39ms, 33.7MB)
// 테스트 4 〉    통과 (0.32ms, 33.5MB)
// 테스트 5 〉    통과 (0.36ms, 33.7MB)
// 테스트 6 〉    통과 (0.42ms, 33.5MB)
// 테스트 7 〉    통과 (0.22ms, 33.6MB)
// 테스트 8 〉    통과 (0.14ms, 33.6MB)
// 테스트 9 〉    통과 (0.16ms, 33.5MB)
// 테스트 10 〉 통과 (0.24ms, 33.6MB)
// 테스트 11 〉 통과 (0.42ms, 33.6MB)
// 테스트 12 〉 통과 (0.17ms, 33.6MB)
// 테스트 13 〉 통과 (0.41ms, 33.6MB)
// 테스트 14 〉 통과 (0.37ms, 33.6MB)
// 테스트 15 〉 통과 (0.39ms, 33.6MB)
// 테스트 16 〉 통과 (0.05ms, 33.5MB)




/* check(검증) - Big O Notation */

// time complexity  : O(nlogn)
// space complexity : O(1)
```

#### [K번째수](https://school.programmers.co.kr/learn/courses/30/lessons/42748)

```javascript
/* redefine(재정의) */

// input1 : array(1차원 Array)
// input2 : commands([i,j,k]를 요소로 가지는 2차원 Array)
// return : command별 연산 결과가 담긴 1차원 Array

// condition1 : array 길이 : [1,100]
// condition2 : array 원소 값 : [1,100]
// condition3 : commands 길이 : [1,50]

// algorithm : 정렬(오름차순) : sort((a, b) => a - b)

// logic(psuedo) : 




/* solution(구현) */

function solution(array, commands) {
    let answer = [];
    for ([i, j, k] of commands) {
        segArray = array.slice(i - 1, j).sort((a, b) => a - b);    // 공간복잡도 O(n/2)
        answer.push(segArray[k - 1]);
    }
    return answer;
}


/* 결과 */
// 정확성
// 테스트 1 〉    통과 (0.08ms, 33.4MB)
// 테스트 2 〉    통과 (0.11ms, 33.4MB)
// 테스트 3 〉    통과 (0.07ms, 33.4MB)
// 테스트 4 〉    통과 (0.08ms, 33.5MB)
// 테스트 5 〉    통과 (0.09ms, 33.4MB)
// 테스트 6 〉    통과 (0.07ms, 33.4MB)
// 테스트 7 〉    통과 (0.08ms, 33.4MB)




/* check(검증) - Big O Notation */

// time complexity  : O(n^3*logn)
// space complexity : O(n)
```

#### [가장 큰 수](https://school.programmers.co.kr/learn/courses/30/lessons/42746)

```javascript
/* redefine(재정의) */

// input : numbers(0 또는 양의 정수가 담긴 1차원 Array)
// return : 순서 재배치 결과, 가장 큰 수(String)

// condition1 : numbers 길이 : [1,100000]
// condition2 : numbers 원소 값 : [1,1000]

// algorithm : 정렬(비교연산 - 내림차순) : sort((n1, n2) => (n2 + n1) - (n1 + n2))

// logic(psuedo) : 
// 1. numbers 원소 타입을 문자열로 형변환
// 2. (n2+n1) (n1+n2) 비교 연산을 적용한 내림차순 정렬
// 3. 배열을 문자열로 변환(join)
// 4. 예외 처리("00...0" -> "0")




/* solution(구현) */

function solution(numbers) {
    let answer = numbers
        .map((num) => String(num))
        .sort((n1, n2) => (n2 + n1) - (n1 + n2))    // 공간복잡도 O(n/2)
        .join('');

    return Number(answer) === 0 ? '0' : answer;
}


/* 결과 */
// 정확성
// 테스트 1 〉    통과 (134.70ms, 42.9MB)
// 테스트 2 〉    통과 (63.72ms, 42.1MB)
// 테스트 3 〉    통과 (169.54ms, 44.9MB)
// 테스트 4 〉    통과 (24.57ms, 37.1MB)
// 테스트 5 〉    통과 (104.43ms, 44.7MB)
// 테스트 6 〉    통과 (91.92ms, 44MB)
// 테스트 7 〉    통과 (0.14ms, 33.4MB)
// 테스트 8 〉    통과 (0.13ms, 33.6MB)
// 테스트 9 〉    통과 (0.13ms, 33.4MB)
// 테스트 10 〉 통과 (0.13ms, 33.4MB)
// 테스트 11 〉 통과 (0.15ms, 33.4MB)
// 테스트 12 〉 통과 (0.06ms, 33.4MB)
// 테스트 13 〉 통과 (0.06ms, 33.5MB)
// 테스트 14 〉 통과 (0.06ms, 33.4MB)
// 테스트 15 〉 통과 (0.06ms, 33.4MB)




/* check(검증) - Big O Notation */

// time complexity  : O(n^3*logn)
// space complexity : O(n)
```


### 스택 & 큐

#### [같은 숫자는 싫어](https://school.programmers.co.kr/learn/courses/30/lessons/12906)

```javascript
/* redefine(재정의) */

// input : arr(0부터 9까지의 숫자로 이루어진 1차원 Array)
// return  연속된 숫자를 제거한 1차원 배열

// condition1 : arr의 길이 : [1,1000000]
// condition2 : arr 원소 값 : [0, 9]

// algorithm : 스택

// logic(psuedo) : 




/* solution(구현) */

function solution(arr)
{
    let answer = [];
    let lastNum = -1;    // 0 ~ 9에 포함되지 않도록 초기값(-1) 설정

    for (let num of arr) {
        if (num !== lastNum) {    // 연속된 숫자가 아니라면,
            lastNum = num;        // lastNum 갱신
            answer.push(num);     // 스택에 push
        }
    }
    
    return answer;
}


/* 결과 */
// 정확성
// 테스트 1 〉    통과 (0.06ms, 33.6MB)
// 테스트 2 〉    통과 (0.18ms, 33.5MB)
// 테스트 3 〉    통과 (0.19ms, 33.4MB)
// 테스트 4 〉    통과 (0.17ms, 33.4MB)
// 테스트 5 〉    통과 (0.22ms, 33.6MB)
// 테스트 6 〉    통과 (0.16ms, 33.4MB)
// 테스트 7 〉    통과 (0.17ms, 33.5MB)
// 테스트 8 〉    통과 (0.20ms, 33.4MB)
// 테스트 9 〉    통과 (0.13ms, 33.6MB)
// 테스트 10 〉 통과 (0.18ms, 33.5MB)
// 테스트 11 〉 통과 (0.15ms, 33.4MB)
// 테스트 12 〉 통과 (0.16ms, 33.6MB)
// 테스트 13 〉 통과 (0.13ms, 33.5MB)
// 테스트 14 〉 통과 (0.14ms, 33.4MB)
// 테스트 15 〉 통과 (0.13ms, 33.5MB)
// 테스트 16 〉 통과 (0.14ms, 33.5MB)
// 테스트 17 〉 통과 (0.04ms, 33.5MB)
// 효율성
// 테스트 1 〉    통과 (27.29ms, 91.2MB)
// 테스트 2 〉    통과 (30.33ms, 90.8MB)
// 테스트 3 〉    통과 (29.95ms, 91.4MB)
// 테스트 4 〉    통과 (56.42ms, 90.9MB)




/* check(검증) - Big O Notation */

// time complexity  : O(n)
// space complexity : O(n)
```

#### [기능개발](https://school.programmers.co.kr/learn/courses/30/lessons/42586)

```javascript
/* redefine(재정의) */

// input : progresses(작업의 진도가 담긴 1차원 Array), speeds(작업의 개발 속도가 담긴1차원 Array)
// return : 배포별 배포되는 기능 수가 담긴 1차원 Array

// condition1 : input 배열들의 길이 : [1,100]
// condition2 : 작업 진도 및 속도 : [1,100]

// algorithm : 스택

// logic(psuedo) : 




/* solution(구현) */

function solution(progresses, speeds) {
    
    let answer = [];
    let endDay = [];

    for (let i=0; i<progresses.length; i++) {
        end = Math.ceil((100 - progresses[i]) / speeds[i]);  // 작업 잔여일 구하기
        endDay.push(end);                                    // 작업 잔여일 리스트에 push
    }

    let cnt = 0;             // 배포되는 기능 수
    let maxDay = endDay[0];  // 배포별 기준일 (첫 작업 잔여일로 초기화)
    
    for (let day of endDay) {
        if (day > maxDay) {    // 다음 배포일에 속한다면,  
            maxDay = day;      // 배포별 기준일 갱신 
            answer.push(cnt)   // 배포되는 기능 수 anwer 리스트에 push
            cnt = 1;           // 배포되는 기능 수 초기화(1)
        }
        else {
            cnt++;             // 같은 배포일에 속한다면 cnt++
        }
    }
    if (cnt > 0) answer.push(cnt);  // 마지막 배포되는 기능 수가 있는지 확인하고, 있으면 push
    
    return answer;
}


/* 결과 */
// 정확성
// 테스트 1 〉    통과 (0.07ms, 33.4MB)
// 테스트 2 〉    통과 (0.18ms, 33.5MB)
// 테스트 3 〉    통과 (0.18ms, 33.4MB)
// 테스트 4 〉    통과 (0.17ms, 33.5MB)
// 테스트 5 〉    통과 (0.07ms, 33.1MB)
// 테스트 6 〉    통과 (0.07ms, 33.1MB)
// 테스트 7 〉    통과 (0.18ms, 33.5MB)
// 테스트 8 〉    통과 (0.07ms, 33.4MB)
// 테스트 9 〉    통과 (0.18ms, 33.3MB)
// 테스트 10 〉 통과 (0.18ms, 33.4MB)
// 테스트 11 〉 통과 (0.07ms, 33.5MB)



/* check(검증) - Big O Notation */

// time complexity  : O(n)
// space complexity : O(n)
```
#### [다리를 지나는 트럭](https://school.programmers.co.kr/learn/courses/30/lessons/42583)

```javascript
/* redefine(재정의) */

// input1 : bridge_length(최대 올라갈 수 있는 트럭 수 Number)
// input2 : weight(견딜 수 있는 최대 하중 Number)
// input3 : truck_weights(대기 중인 트럭별 하중이 담긴 1차원 Array)
// return : 모든 트럭이 다리를 건너는데 걸리는 최소시간(초) Number

// condition1 : bridge_length : [1,10000]
// condition2 : weight : [1,10000]
// condition3 : truck_weights : [1,10000]
// condition4 : truck 속도 : 1

// algorithm : 큐

// logic(psuedo) : 




/* solution(구현) */

function solution(bridge_length, weight, truck_weights) {
    let answer = 0;
    let weightSum = 0;
    let bridge = new Array(bridge_length).fill(0);
  
    do {
        answer++;
        weightSum -= bridge.shift();
      
        (truck_weights.length > 0 && weightSum + truck_weights[0] <= weight)
        ? nextWeight = truck_weights.shift()
        : nextWeight = 0
      
        weightSum += nextWeight;
        bridge.push(nextWeight);
    }
    while (weightSum > 0);
  
    return answer;
}


/* 결과 */
// 정확성
// 테스트 1 〉    통과 (0.61ms, 33.6MB)
// 테스트 2 〉    통과 (7.73ms, 37.4MB)
// 테스트 3 〉    통과 (0.14ms, 33.5MB)
// 테스트 4 〉    통과 (5.15ms, 37.4MB)
// 테스트 5 〉    통과 (29.79ms, 37.9MB)
// 테스트 6 〉    통과 (9.77ms, 38MB)
// 테스트 7 〉    통과 (0.51ms, 33.5MB)
// 테스트 8 〉    통과 (0.27ms, 33.5MB)
// 테스트 9 〉    통과 (4.46ms, 36.6MB)
// 테스트 10 〉 통과 (0.19ms, 33.5MB)
// 테스트 11 〉 통과 (0.14ms, 33.5MB)
// 테스트 12 〉 통과 (0.22ms, 33.4MB)
// 테스트 13 〉 통과 (0.46ms, 33.5MB)
// 테스트 14 〉 통과 (0.22ms, 33.4MB)


/* check(검증) - Big O Notation */

// time complexity  : O(n^2)
// space complexity : O(n)
```
#### [문제]()

```javascript

```
#### [문제]()

```javascript

```

### BFS & DFS

#### [올바른 괄호](https://school.programmers.co.kr/learn/courses/30/lessons/12909)

```javascript
/* redefine(재정의) */

// input : s( '(' , ')' 로만 이루어진 문자열 s)
// return : 괄호가 바르게 짝지었는지에 따른 boolean 값

// condition : s의 길이 : [1,100000]

// algorithm : 

// logic(psuedo) :
// 1. left < right가 된다면, return false
// 2. left/right 갱신이 끝난 후, left === right 조건을 만족하지 않으면, return false




/* solution(구현) */

function solution(s){
    let left = 0;   // 왼쪽 괄호('(')의 개수
    let right = 0;  // 오른쪽 괄호(')')의 개수

    for (let c of s) { 
        
        (c === '(') ? left++ : right++    // 괄호 모양에 따라 left, right 갱신

        if (left < right) return false;   // logic1 : left < right가 된다면, return false
    }    
    
    if (left === right) { return true } 
    else { return false }                 // logic2 : left === right 조건을 만족하지 않으면, return false
}


/* 결과 */
// 정확성
// 테스트 1 〉    통과 (0.04ms, 33.5MB)
// 테스트 2 〉    통과 (0.04ms, 33.4MB)
// 테스트 3 〉    통과 (0.04ms, 33.4MB)
// 테스트 4 〉    통과 (0.05ms, 33.4MB)
// 테스트 5 〉    통과 (0.05ms, 33.5MB)
// 테스트 6 〉    통과 (0.04ms, 33.4MB)
// 테스트 7 〉    통과 (0.04ms, 33.6MB)
// 테스트 8 〉    통과 (0.04ms, 33.5MB)
// 테스트 9 〉    통과 (0.05ms, 33.4MB)
// 테스트 10 〉 통과 (0.07ms, 33.5MB)
// 테스트 11 〉 통과 (0.07ms, 33.4MB)
// 테스트 12 〉 통과 (0.13ms, 33.4MB)
// 테스트 13 〉 통과 (0.13ms, 33.4MB)
// 테스트 14 〉 통과 (0.13ms, 33.4MB)
// 테스트 15 〉 통과 (0.13ms, 33.4MB)
// 테스트 16 〉 통과 (0.13ms, 33.4MB)
// 테스트 17 〉 통과 (0.13ms, 33.4MB)
// 테스트 18 〉 통과 (0.14ms, 33.4MB)
// 효율성
// 테스트 1 〉    통과 (9.30ms, 38MB)
// 테스트 2 〉    통과 (5.40ms, 38.2MB)




/* check(검증) - Big O Notation */

// time complexity  : O(n)
// space complexity : O(1)




/* improvements(개선점 - 가독성 향상) */

function solution(s){
    let left = 0
    let right = 0;

    for (let c of s) { 
        
        (c === '(') ? left++ : right++

        if (left < right) return false;
    }    
    
    return (left === right) ? true : false;
}


/* 결과 */
// 정확성
// 테스트 1 〉    통과 (0.04ms, 33.5MB)
// 테스트 2 〉    통과 (0.06ms, 33.5MB)
// 테스트 3 〉    통과 (0.04ms, 33.5MB)
// 테스트 4 〉    통과 (0.04ms, 33.4MB)
// 테스트 5 〉    통과 (0.04ms, 33.4MB)
// 테스트 6 〉    통과 (0.05ms, 33.4MB)
// 테스트 7 〉    통과 (0.05ms, 33.5MB)
// 테스트 8 〉    통과 (0.04ms, 33.4MB)
// 테스트 9 〉    통과 (0.05ms, 33.5MB)
// 테스트 10 〉 통과 (0.07ms, 33.4MB)
// 테스트 11 〉 통과 (0.04ms, 33.5MB)
// 테스트 12 〉 통과 (0.16ms, 33.4MB)
// 테스트 13 〉 통과 (0.13ms, 33.4MB)
// 테스트 14 〉 통과 (0.14ms, 33.4MB)
// 테스트 15 〉 통과 (0.18ms, 33.6MB)
// 테스트 16 〉 통과 (0.14ms, 33.4MB)
// 테스트 17 〉 통과 (0.13ms, 33.4MB)
// 테스트 18 〉 통과 (0.19ms, 33.4MB)
// 효율성
// 테스트 1 〉    통과 (5.41ms, 38.4MB)
// 테스트 2 〉    통과 (6.65ms, 38.3MB)



/* check(검증) - Big O Notation */

// time complexity  : O(n)
// space complexity : O(1)
```

#### [프린터](https://school.programmers.co.kr/learn/courses/30/lessons/42587)

```javascript
/* redefine(재정의) */

// input : priorities(문서의 중요도가 담긴 1차원 Array), location(인쇄를 요청한 문서의 위치 Number)
// return : 인쇄를 요청한 문서의 인쇄 순서(Number)

// condition1 : 중요도 : [1,9]
// condition2 : priorities 길이 : [1,100]

// algorithm : 큐

// logic(psuedo) : 




/* solution(구현) */

function solution(priorities, location) {
    let answer = 0;
    let flag = false;
    
    while(true) {
          maxPriority = Math.max(...priorities);
        
        let priority = priorities.shift();
        
        (priority === maxPriority) 
        ? ((location === 0) ? flag = true : answer++)
        : priorities.push(priority)
        
        if (flag) return (answer + 1);
        
        (location > 0) ? location-- : location = priorities.length - 1
    }
}


/* 결과 */
// 정확성
// 테스트 1 〉    통과 (0.15ms, 33.4MB)
// 테스트 2 〉    통과 (0.35ms, 33.5MB)
// 테스트 3 〉    통과 (0.18ms, 33.5MB)
// 테스트 4 〉    통과 (0.15ms, 33.4MB)
// 테스트 5 〉    통과 (0.05ms, 33.4MB)
// 테스트 6 〉    통과 (0.16ms, 33.5MB)
// 테스트 7 〉    통과 (0.16ms, 33.6MB)
// 테스트 8 〉    통과 (0.26ms, 33.5MB)
// 테스트 9 〉    통과 (0.14ms, 33.5MB)
// 테스트 10 〉 통과 (0.18ms, 33.4MB)
// 테스트 11 〉 통과 (0.24ms, 33.5MB)
// 테스트 12 〉 통과 (0.14ms, 33.5MB)
// 테스트 13 〉 통과 (0.23ms, 33.6MB)
// 테스트 14 〉 통과 (0.05ms, 33.4MB)
// 테스트 15 〉 통과 (0.06ms, 33.5MB)
// 테스트 16 〉 통과 (0.15ms, 33.4MB)
// 테스트 17 〉 통과 (0.30ms, 33.5MB)
// 테스트 18 〉 통과 (0.17ms, 33.5MB)
// 테스트 19 〉 통과 (0.37ms, 33.5MB)
// 테스트 20 〉 통과 (0.15ms, 33.4MB)


/* check(검증) - Big O Notation */

// time complexity  : O(n^2)
// space complexity : O(1)
```


## [코딩테스트 연습](https://school.programmers.co.kr/learn/challenges?order=recent)


### LV.2

#### [무인도 여행](https://school.programmers.co.kr/learn/courses/30/lessons/154540)

```javascript
/* redefine(재정의) */

// input1 : maps(각 행의 식량정보(String)를 요소로 갖는 1차원 Array)
// return : 각 섬에서 머무를 수 있는 최대 일수(Number)를 담은 1차원 Array

// condition1 : maps의 행, 열 크기(서로 다를 수 있음) : [3,100]
// condition2 : maps[i]는 'X' 또는 [1, 9]
// condition3 : 섬이 없다면 -1 반환

// algorithm : BFS, Queue

// logic(psuedo) :
// 1. 섬 노드인 경우만 BFS 진행
// 2. 큐에 출발 노드 삽입
// 3. 방문/섬/인덱스 범위 유효 여부 검사하면 BFS 진행
// 4. BFS 완료 후, 식량 여부 검사(있다면 반환 값 갱신)
// 5. 예외 처리(섬이 하나도 없는 경우) 및 반환 값 조건 만족



/* solution(구현) */

function solution(maps) {
    
    let days = [];                                 // 반환 값 세팅

    const n = maps.length;                         // n(행)
    const m = maps[0].length;                      // m(열)

    const dx = [0, 0, -1, 1];                      // 방향 설정
    const dy = [1, -1, 0, 0];                      // 상/하/좌/우
    
    let visited = new Array(n*m).fill(false);      // 방문 배열(false)

    
    for (let i=0; i<n; i++) {                      // 모든 노드 탐색                  
        for (let j=0; j<m; j++) {
            if (maps[i][j] === "X") { continue; }  // 섬 여부 검사("X": 바다)
            
            let route = [[i, j]];                  // route 세팅(Queue)
            let cnt = 0;                           // 식량 수(총계) 초기화          

            
            while(route.length > 0) {                                   // BFS 시작   

                const [x, y] = route.shift();                           // 노드 설정
    
                if (visited[x * m + y] === true) continue;              // 방문 여부 검사
                visited[x * m + y] = true;                              // 방문 처리
                
                cnt = Number(cnt) + Number(maps[x][y]);                 // 식량 수(총계) 갱신
                
                
                for (let j=0; j<4; j++) {                               // 상/하/좌/우 탐색
                    const nx = x + dx[j];                               // 다음 노드 x좌표 설정
                    const ny = y + dy[j];                               // 다음 노드 y좌표 설정
                    
                    if (nx < 0 | nx >= n | ny < 0 | ny >= m) continue;  // 인덱스 범위 유효 검사(index range)
                    if (maps[nx][ny] === 'X') continue;                 // 섬 여부 검사("X": 바다)
                    
                    route.push([nx, ny]);                               // 다음 레벨 노드를 큐에 삽입
                }

            }

            if (cnt > 0) {days.push(cnt)}                               // 식량 여부 검사, 있다면 push
        }           
    }

    // (섬이 있다면) ? 오름차순 정렬된 days 반환 : [-1] 반환
    return (days.length > 0) ? days.sort((a,b) => a-b) : [-1];
}


/* 결과 */
// 정확성
// 테스트 1 〉    통과 (0.14ms, 33.6MB)
// 테스트 2 〉    통과 (0.25ms, 33.6MB)
// 테스트 3 〉    통과 (0.30ms, 33.5MB)
// 테스트 4 〉    통과 (0.38ms, 33.5MB)
// 테스트 5 〉    통과 (1.33ms, 34MB)
// 테스트 6 〉    통과 (1.95ms, 34.3MB)
// 테스트 7 〉    통과 (1.18ms, 33.9MB)
// 테스트 8 〉    통과 (3.27ms, 34.6MB)
// 테스트 9 〉    통과 (9.70ms, 38.2MB)
// 테스트 10 〉 통과 (4.83ms, 37.4MB)
// 테스트 11 〉 통과 (4.71ms, 37.4MB)
// 테스트 12 〉 통과 (10.86ms, 38.4MB)
// 테스트 13 〉 통과 (10.69ms, 38.5MB)
// 테스트 14 〉 통과 (18.53ms, 38.7MB)
// 테스트 15 〉 통과 (18.41ms, 38.7MB)
// 테스트 16 〉 통과 (18.67ms, 38.8MB)
// 테스트 17 〉 통과 (0.59ms, 33.7MB)
// 테스트 18 〉 통과 (18.61ms, 38.8MB)
// 테스트 19 〉 통과 (18.75ms, 38.8MB)
// 테스트 20 〉 통과 (0.77ms, 33.6MB)
// 테스트 21 〉 통과 (0.71ms, 33.7MB)
// 테스트 22 〉 통과 (0.31ms, 33.5MB)
// 테스트 23 〉 통과 (9.82ms, 38.4MB)
// 테스트 24 〉 통과 (10.82ms, 38.6MB)
// 테스트 25 〉 통과 (0.42ms, 33.6MB)


/* check(검증) - Big O Notation */

// time complexity  : O(NM)
// 모든 노드(NxM 크기)를 탐색하므로

// space complexity : O(NM)
// visited 배열 크기(NxM)
```

#### [호텔 대실](https://school.programmers.co.kr/learn/courses/30/lessons/155651)

```javascript
/* redefine(재정의) */

// input : book_time(["HH:MM", "HH:MM"]) 형태로 입실 시간과 퇴실 시간이 담긴 2차원 Array)
// return : 예약 손님이 모두 입실하기 위해 필요한 최소 객실의 수 Number

// condition1 : book_time 길이 : [1,1000]
// condition2 : 입실 및 퇴실 시간(24시간 표기법) : ["00:00","23:59"]
// condition3 : 입실 시간 < 퇴실 시간

// algorithm : 정렬, 스택, 그리디?

// logic(psuedo) :
// 1. input 데이터 가공(분으로 환산하여 Number 형으로) : [입실 시간(분):Number, 퇴실 시간(분):Number]
// 2. 대실 시작 시간을 기준으로 오름차순 정렬
// 3. 객실마다 입실 여부를 검사
// 4. 입실이 가능하다면, 해당 객실(room[i]) 값 갱신
// 5. 입실이 불가능하다면, 새로운 객실(room[room.length + 1])에 push
// 6. 모든 예약 손님들의 입실이 끝나면, room.length 반환


/* solution(구현) */

function solution(book_time) {
    
    const bookTime = book_time.map(function([start, end]) {
        
        [sh, sm] = start.split(":").map(Number);  // "(sh):(sm)"
        [eh, em] = end.split(":").map(Number);    // "(eh):(em)"
        
        return [sh * 60 + sm, eh * 60 + em];      // minute(분)으로 환산
    });
    
    bookTime.sort((a, b) => a[0] - b[0]);  // 대실 시작 시간을 기준으로 오름차순 정렬
    
    let room = [0];
    for (let [start, end] of bookTime) {         // 현재 손님의 [입실시간, 퇴실 시간] 세팅
        
        let flag = false;                        // 입실 가능/불가능 표시
        
        for (let i=0; i<room.length; i++) {      // 객실(room[i])마다 탐색
            if (start >= room[i] + 10) {         // 현재 손님의 입실 시간 >= 이전 손님의 퇴실 시간+10 이면
                room[i] = end;                   // 해당 객실에 손님 입실
                flag = true;                     // 입실 가능 표시
                break;                           // break
            }
        }
        if (flag === false) { room.push(end); }  // 만약 입실하지 못했으면, 새로운 객실을 만들어 push
    }
    return room.length;
}


/* 결과 */
// 정확성
// 테스트 1 〉    통과 (0.55ms, 33.5MB)
// 테스트 2 〉    통과 (1.59ms, 33.6MB)
// 테스트 3 〉    통과 (8.66ms, 37.6MB)
// 테스트 4 〉    통과 (7.80ms, 37.1MB)
// 테스트 5 〉    통과 (0.12ms, 33.4MB)
// 테스트 6 〉    통과 (8.54ms, 37.4MB)
// 테스트 7 〉    통과 (7.06ms, 37.6MB)
// 테스트 8 〉    통과 (1.60ms, 33.8MB)
// 테스트 9 〉    통과 (1.93ms, 33.6MB)
// 테스트 10 〉 통과 (8.41ms, 37.4MB)
// 테스트 11 〉 통과 (9.80ms, 37.6MB)
// 테스트 12 〉 통과 (9.55ms, 37.5MB)
// 테스트 13 〉 통과 (1.69ms, 33.7MB)
// 테스트 14 〉 통과 (6.78ms, 37.5MB)
// 테스트 15 〉 통과 (9.67ms, 37.6MB)
// 테스트 16 〉 통과 (2.72ms, 33.7MB)
// 테스트 17 〉 통과 (6.16ms, 37.5MB)
// 테스트 18 〉 통과 (5.54ms, 37.4MB)
// 테스트 19 〉 통과 (6.85ms, 38.5MB)



/* check(검증) - Big O Notation */

// time complexity  : O(n^2)
// 이중 for 문으로 탐색

// space complexity : O(n)
// room의 최대 크기 <= n
```

#### [뒤에 있는 큰 수 찾기](https://school.programmers.co.kr/learn/courses/30/lessons/154539)

```javascript
/* redefine(재정의) */

// input : numbers(정수로 이루어진 1차원 Array) 
// return : 모든 원소에 대한 뒷 큰 수들을 차례로 담은 1차원 Array

// condition1 : numbers 길이 : [4, 1000000]
// condition2 : numbers[i] : [1, 1000000]

// algorithm : 우선순위 큐

// logic(psuedo) : 




/* solution(구현) */

function solution(numbers) {
    
    var answer = [];
    
    for (let i = 0; i < numbers.length; i++) {          // index 0부터 모든 노드 탐색
        let bigNum = -1;                                // bigNum : 뒷 큰 수 세팅(-1)
        
        for (let j = i + 1; j < numbers.length; j++) {
            if (numbers[j] > numbers[i]) {              // 만약, 뒷 큰 수를 찾으면
                bigNum = numbers[j];                    // bigNum 갱신
                break;                                  // 탐색을 멈추고
            }
        }
        answer.push(bigNum);                            // answer에 push
    }
    
    return answer;
}


/* 결과 */
// 정확성
// 테스트 1 〉    통과 (0.11ms, 33.4MB)
// 테스트 2 〉    통과 (0.06ms, 33.4MB)
// 테스트 3 〉    통과 (0.16ms, 33.3MB)
// 테스트 4 〉    통과 (0.13ms, 33.4MB)
// 테스트 5 〉    통과 (0.40ms, 33.6MB)
// 테스트 6 〉    통과 (3.04ms, 37.9MB)
// 테스트 7 〉    통과 (2.30ms, 38MB)
// 테스트 8 〉    통과 (4.23ms, 42.1MB)
// 테스트 9 〉    통과 (3.60ms, 42.1MB)
// 테스트 10 〉 통과 (5.66ms, 46.7MB)
// 테스트 11 〉 통과 (6.66ms, 46.8MB)
// 테스트 12 〉 통과 (10.10ms, 56.1MB)
// 테스트 13 〉 통과 (11.07ms, 56.2MB)
// 테스트 14 〉 통과 (29.47ms, 77.3MB)
// 테스트 15 〉 통과 (94.46ms, 142MB)
// 테스트 16 〉 통과 (88.20ms, 142MB)
// 테스트 17 〉 통과 (85.91ms, 142MB)
// 테스트 18 〉 통과 (81.09ms, 142MB)
// 테스트 19 〉 통과 (66.23ms, 142MB)
// 테스트 20 〉    실패 (시간 초과)
// 테스트 21 〉    실패 (시간 초과)
// 테스트 22 〉    실패 (시간 초과)
// 테스트 23 〉    실패 (시간 초과)


/* check(검증) - Big O Notation */

// time complexity  : O(n^2)
// for loop(n)^2

// space complexity : O(n)




/* improvements(개선점) - 우선순위 큐를 사용하여 시간 복잡도 개선(n^2 => nlogn) */

function solution(numbers) {
    const answer = [];
    
    const pq = []; // 우선순위 큐 세팅
    
    for (let i = numbers.length - 1; i >= 0; i--) {                             // 역순으로 순회
        
        while (pq.length > 0 && pq[pq.length - 1] <= numbers[i]) { pq.pop(); }  // 우선순위 큐 갱신
        
        answer[i] = (pq.length > 0) ? pq[pq.length - 1] : -1;                   // answer 갱신()
        
        pq.push(numbers[i]);                                                    // 우선순위 큐 삽입
    }
    
    return answer;
}


// 테스트 1 〉    통과 (0.05ms, 33.4MB)
// 테스트 2 〉    통과 (0.05ms, 33.5MB)
// 테스트 3 〉    통과 (0.13ms, 33.6MB)
// 테스트 4 〉    통과 (0.14ms, 33.5MB)
// 테스트 5 〉    통과 (0.30ms, 33.7MB)
// 테스트 6 〉    통과 (3.20ms, 38.2MB)
// 테스트 7 〉    통과 (3.30ms, 38.2MB)
// 테스트 8 〉    통과 (7.17ms, 42.3MB)
// 테스트 9 〉    통과 (6.92ms, 42.5MB)
// 테스트 10 〉 통과 (12.41ms, 47MB)
// 테스트 11 〉 통과 (12.11ms, 47MB)
// 테스트 12 〉 통과 (34.04ms, 55.9MB)
// 테스트 13 〉 통과 (25.24ms, 55.8MB)
// 테스트 14 〉 통과 (55.62ms, 77.3MB)
// 테스트 15 〉 통과 (110.82ms, 137MB)
// 테스트 16 〉 통과 (115.39ms, 137MB)
// 테스트 17 〉 통과 (106.52ms, 137MB)
// 테스트 18 〉 통과 (129.07ms, 137MB)
// 테스트 19 〉 통과 (122.90ms, 137MB)
// 테스트 20 〉 통과 (117.40ms, 134MB)
// 테스트 21 〉 통과 (100.29ms, 133MB)
// 테스트 22 〉 통과 (86.16ms, 104MB)
// 테스트 23 〉 통과 (113.67ms, 127MB)


/* check(검증) - Big O Notation */

// time complexity  : O(nlogn)
// for loop(n) * priorityQueue(logn)

// space complexity : O(n)
```

#### [숫자 변환하기](https://school.programmers.co.kr/learn/courses/30/lessons/154538)

```javascript
/* redefine(재정의) */

// input : x, y, n (Number)
// return : 필요한 최소 연산 횟수(Number), 만들 수 없다면 -1

// condition1 : x, y : [1,1000000]
// condition2 : n : [1,y)

// algorithm : BFS & Set

// logic(psuedo) : 




/* solution(구현) */

function solution(x, y, n) {

    if (x === y) { return 0; }
    
    let cnt = 0;                               // 레벨 깊이
    let stack1 = [];                           // 레벨 별 노드를 담을 스택
    let visited = new Array(1000001).fill(0);  // 방문 배열 작성

    stack1.push(x);  // 시작 노드 세팅
    
    while (true) {
        cnt++;         
        let stack2 = [];
        
        while (stack1.length > 0) {    // 레벨 내 노드 유무 검사
            const num = stack1.pop();  // 부모 노드 세팅

            const n1 = num * 2;        // 자식 노드 세팅1
            const n2 = num * 3;        // 자식 노드 세팅2
            const n3 = num + n;        // 자식 노드 세팅3
            
            if (n1===y || n2===y || n3===y) { return cnt; }  // 
            
            if (n1 < y && visited[n1] === 0) {               // n1 < y && 방문X
                stack2.push(num * 2);                        // 임시 스택에 Push
                visited[n1] = 1;                             // 방문 표시
            }
            if (n2 < y && visited[n2] === 0) {               // n2 < y && 방문X
                stack2.push(num * 3);                        // 임시 스택에 Push
                visited[n2] = 1;                             // 방문 표시
            }
            if (n3 < y && visited[n3] === 0) {               // n3 < y && 방문X 
                stack2.push(num + n);                        // 임시 스택에 Push
                visited[n3] = 1;                             // 방문 표시
            }
        }
        if (stack2.length === 0) { return -1; }              // 불가능한 경우, -1 반환
        stack1.push(...stack2);                              // 다음 연산을 위해 push
    }
}


/* 결과 */
// 정확성
// 테스트 1 〉    통과 (6.32ms, 41.2MB)
// 테스트 2 〉    통과 (6.73ms, 41.1MB)
// 테스트 3 〉    통과 (6.48ms, 41.1MB)
// 테스트 4 〉    통과 (6.65ms, 41.2MB)
// 테스트 5 〉    통과 (14.36ms, 46.3MB)
// 테스트 6 〉    통과 (0.07ms, 33.5MB)
// 테스트 7 〉    통과 (18.54ms, 47MB)
// 테스트 8 〉    통과 (6.18ms, 41.3MB)
// 테스트 9 〉        실패 (런타임 에러)
// 테스트 10 〉    실패 (런타임 에러)
// 테스트 11 〉 통과 (19.32ms, 48.3MB)
// 테스트 12 〉 통과 (6.08ms, 41.3MB)
// 테스트 13 〉 통과 (6.19ms, 41.1MB)
// 테스트 14 〉 통과 (7.17ms, 41.3MB)
// 테스트 15 〉 통과 (6.90ms, 41.3MB)
// 테스트 16 〉 통과 (6.42ms, 41.2MB)


/* check(검증) - Big O Notation */

// time complexity  : O()
// space complexity : O()




/* improvements(개선점 - Set 활용) */

function solution(x, y, n) {
    
    if (x === y) { return 0; }
    
    let cnt = 0;            
    let numSet1 = new Set();
    numSet1.add(x);
    
    while(numSet1.size > 0) {
        if(numSet1.has(y)) { return cnt; }
        const numSet2 = new Set();
        for (const num of numSet1.values()) {
            if(num * 2 <= y) { numSet2.add(num * 2); }
            if(num * 3 <= y) { numSet2.add(num * 3); }
            if(num + n <= y) { numSet2.add(num + n); }
        }
        numSet1 = numSet2;
        cnt++;
    }
    return -1;
}


// 정확성
// 테스트 1 〉    통과 (0.07ms, 33.4MB)
// 테스트 2 〉    통과 (0.09ms, 33.4MB)
// 테스트 3 〉    통과 (0.12ms, 33.5MB)
// 테스트 4 〉    통과 (0.09ms, 33.4MB)
// 테스트 5 〉    통과 (43.41ms, 52.2MB)
// 테스트 6 〉    통과 (0.06ms, 33.4MB)
// 테스트 7 〉    통과 (45.59ms, 52.7MB)
// 테스트 8 〉    통과 (0.10ms, 33.4MB)
// 테스트 9 〉    통과 (248.04ms, 88.3MB)
// 테스트 10 〉 통과 (201.50ms, 88.1MB)
// 테스트 11 〉 통과 (61.75ms, 56.7MB)
// 테스트 12 〉 통과 (0.07ms, 33.4MB)
// 테스트 13 〉 통과 (0.07ms, 33.4MB)
// 테스트 14 〉 통과 (1.32ms, 34.1MB)
// 테스트 15 〉 통과 (0.23ms, 33.5MB)
// 테스트 16 〉 통과 (0.50ms, 33.7MB)


/* check(검증) - Big O Notation */

// m은 cnt의 최댓값

// time complexity  : O(3^m * n)
// while 루프에서는 각 레벨에서 만들어지는 새로운 숫자의 수가 O(3) 이고, 각 레벨은 O(n) 의 시간이 걸린다.

// space complexity : O(m)
// 각 레벨에서 새로운 숫자를 저장하기 위해 필요한 Set 개수
```

#### [시소 짝꿍](https://school.programmers.co.kr/learn/courses/30/lessons/152996)

```javascript
/* redefine(재정의) */

// input : weights(사람들의 몸무게가 담긴 1차원 Array)
// return : 시소 짝꿍이 몇 쌍 존재하는지 Number

// condition1 : weights 길이 : [1, 100000]
// condition2 : weights[i] : [100,1000]

// algorithm :

// logic(psuedo) : 




/* solution(구현) */

function solution(weights) {
    let answer = 0;
    
    const people = new Array(1001).fill(0);
    for (let w of weights) { people[w] += 1; }
    
    for (let w of weights) {
        const w1 = w / 2;
        const w2 = w * 2 / 3;
        const w3 = w * 3 / 4;
        const w4 = w;
        const w5 = w * 4 / 3;
        const w6 = w * 3 / 2;
        const w7 = w * 2;
        
        if (w1 % 1 === 0 && w1 < 1001) { answer += people[w1]; }
        if (w2 % 1 === 0 && w2 < 1001) { answer += people[w2]; }
        if (w3 % 1 === 0 && w3 < 1001) { answer += people[w3]; }
        if (w4 % 1 === 0 && w4 < 1001) { answer += (people[w4] - 1); }
        if (w5 % 1 === 0 && w5 < 1001) { answer += people[w5]; }
        if (w6 % 1 === 0 && w6 < 1001) { answer += people[w6]; }
        if (w7 % 1 === 0 && w7 < 1001) { answer += people[w7]; }
    }
    
    return answer/2;
}


/* 결과 */
// 정확성
// 테스트 1 〉    통과 (0.08ms, 33.5MB)
// 테스트 2 〉    통과 (0.09ms, 33.5MB)
// 테스트 3 〉    통과 (0.09ms, 33.6MB)
// 테스트 4 〉    통과 (7.50ms, 38.3MB)
// 테스트 5 〉    통과 (8.83ms, 38.8MB)
// 테스트 6 〉    통과 (12.04ms, 39.5MB)
// 테스트 7 〉    통과 (12.62ms, 39.8MB)
// 테스트 8 〉    통과 (14.19ms, 40.3MB)
// 테스트 9 〉    통과 (16.26ms, 39.3MB)
// 테스트 10 〉 통과 (18.69ms, 39.7MB)
// 테스트 11 〉 통과 (19.87ms, 39.7MB)
// 테스트 12 〉 통과 (15.92ms, 39.8MB)
// 테스트 13 〉 통과 (28.45ms, 39.9MB)
// 테스트 14 〉 통과 (21.51ms, 39.7MB)
// 테스트 15 〉 통과 (19.33ms, 39.8MB)
// 테스트 16 〉 통과 (0.09ms, 33.6MB)
// 테스트 17 〉 통과 (0.11ms, 33.5MB)



/* check(검증) - Big O Notation */

// time complexity  : O(n)
// space complexity : O(1001)
```

#### [마법의 엘리베이터](https://school.programmers.co.kr/learn/courses/30/lessons/148653)

```javascript
/* redefine(재정의) */

// input : storey(엘리베이터가 있는 층을 나타내는 정수)
// return : 0층으로 가기 위해 필요한 마법의 돌의 최소값(Number)

// condition :

// algorithm : dfs

// logic(psuedo) : 




/* solution(구현) */

function solution(storey) {

  let answer = Number.MAX_SAFE_INTEGER;

  const dfs = (num, cnt) => {
    if (cnt >= answer) return;

    if (num === 0) { answer = cnt; }
    else {
      dfs(Math.floor(num / 10), cnt + num % 10);
      dfs(Math.floor(num / 10) + 1, cnt + 10 - num % 10);
    }
  }
  
  dfs(storey, 0);
    
  return answer;
}


/* 결과 */
// 정확성
// 테스트 1 〉    통과 (0.16ms, 33.5MB)
// 테스트 2 〉    통과 (0.06ms, 33.4MB)
// 테스트 3 〉    통과 (0.14ms, 33.4MB)
// 테스트 4 〉    통과 (0.15ms, 33.5MB)
// 테스트 5 〉    통과 (0.15ms, 33.5MB)
// 테스트 6 〉    통과 (0.14ms, 33.5MB)
// 테스트 7 〉    통과 (0.16ms, 33.4MB)
// 테스트 8 〉    통과 (0.16ms, 33.4MB)
// 테스트 9 〉    통과 (0.15ms, 33.4MB)
// 테스트 10 〉 통과 (0.26ms, 33.4MB)
// 테스트 11 〉 통과 (0.22ms, 33.4MB)
// 테스트 12 〉 통과 (0.15ms, 33.4MB)
// 테스트 13 〉 통과 (0.14ms, 33.4MB)



/* check(검증) - Big O Notation */

// time complexity  : O(n)
// space complexity : O(n)
```

#### [유사 칸토어 비트열](https://school.programmers.co.kr/learn/courses/30/lessons/148652)

```javascript
/* redefine(재정의) */

// input1 : n (유사 칸토어 비트열 순번: n번째) - Number
// input2 : l (1-base index 시작점) - Number
// input3 : r (1-base index 마침점) - Number
// return : 1-base index 폐구간[l,r] 내의 1의 개수 - Number

// condition1 : n : [1,20]
// condition2 : l,r : [1,5**n]
// condition3 : r : [l,l+10000000)

// algorithm1 : 메모리제이션
// algorithm2 : 수학(5진법)

// logic(psuedo) : 


/* solution(구현) */

function solution(n, l, r) {

    const CantorLike = (preCount) => {
        
        // 0. currCount = preCount;
        const currCount = [...preCount];
        
        // 1. max값 : currCount[currCount.length - 1], arr : preCount 리스트
        let maxCnt = currCount[currCount.length - 1];
        
        // 2. arr을 순회하며 각 (요소 + max) 값을 currCount에 push, max 갱신 : currCount[currCount.length - 1]
        for (let i=0; i<preCount.length; i++) { currCount.push(preCount[i] + maxCnt); }
        maxCnt = currCount[currCount.length - 1];
        
        // 3. 5**(n-1)만큼 max 값을 currCount에 push
        for (let i=0; i<preCount.length; i++) { currCount.push(maxCnt); }
        
        // 4. 2번 단계를 반복
        for (let i=0; i<preCount.length; i++) { currCount.push(preCount[i] + maxCnt); }
        maxCnt = currCount[currCount.length - 1];
        
        // 5. 2번 단계를 반복
        for (let i=0; i<preCount.length; i++) { currCount.push(preCount[i] + maxCnt); }
        
        // 6. currCount 리스트를 return
        return currCount;
    }
    
    let countOne = [1];
    let m = 0;
    while (m < n) {
        m++;
        countOne = CantorLike(countOne);
    }
    
    return countOne[r-1] - countOne[l-1] + 1;
}


/* 결과 */
// 일부 런타임 에러 발생, 토의 필요


/* check(검증) - Big O Notation */

// time complexity  : O(n * 5^(n-1))
// space complexity : O(5^n)




/* improvements(개선점) */

// n번째 = n-1번째 + n-1번째 + '0'.repeat(n-1번째 길이만큼) + n-1번째 + n-1번째

// index -> 5진법 변환 (~0, ~1, ~2, ~3, ~4)
// <경우1> : ~에 2가 포함되어 있지 않은 경우 : 11011 패턴
// <경우2> : ~에 2가 포함되어 있는 경우     : 00000 패턴

// 1이 나오는 경우는 <경우1>에서 끝자리가 2가 아닌 경우, 즉 5진법으로 변환했을때 2가 하나도 없는 경우
// !i.toString(5).match('2')

function solution(n, l, r) {
    let answer = 0;
    for (let i = l - 1; i <=r - 1; i++) {
        if (!i.toString(5).match('2')) answer += 1;
    }
    return answer;
}


/* check(검증) - Big O Notation */

// time complexity  : O(r - l + 1)
// space complexity :  O(1)
```

#### [혼자 놀기의 달인](https://school.programmers.co.kr/learn/courses/30/lessons/131130)

```javascript
/* redifine(재정의) */

// input : cards : number[]
// return : 게임 내 얻을 수 있는 최고 점수 : number

// condition1 : cards 길이 : [2, 100]
// condition2 : cards 요소 : [1, cards.length]

// algorithm : closed graph

// logic(psuedo) : 




/* solution(구현) */

function solution(cards) {
    let group = [];                                     // 각 그룹에 속하는 상자 수 저장                   
    let visited = new Array(cards.length).fill(false);  // 노드 방문 여부 저장
    
    for (let i=0; i<cards.length; i++) {
        if (visited[i]===true) continue;  // 방문한 노드라면 continue
        
        let cnt = 0;                      // 상자 수
        let idx = i;                      // 노드 번호
        
        while (visited[idx]===false) {    // 닫힌 그래프 내 방문 처리가 안된 노드들 순회
            visited[idx] = true;          // 방문 처리
            cnt++;                        // 상자 수++
            idx = cards[idx] - 1;         // 다음 노드 설정
        }
        group.push(cnt);                  // group별 cnt push
    }
    
    group.sort((a, b)=> a - b);           // group 오름차순 정렬
    
    return (group.length === 1) 
        ? 0                                              // 최종 그룹 개수가 1개인 경우
        : group[group.length-1] * group[group.length-2]  // 최대 점수
}


/* 결과 */
// 정확성
// 테스트 1 〉    통과 (0.07ms, 33.5MB)
// 테스트 2 〉    통과 (0.15ms, 33.4MB)
// 테스트 3 〉    통과 (0.16ms, 33.4MB)
// 테스트 4 〉    통과 (0.16ms, 33.5MB)
// 테스트 5 〉    통과 (0.15ms, 33.5MB)
// 테스트 6 〉    통과 (0.16ms, 33.6MB)
// 테스트 7 〉    통과 (0.17ms, 33.4MB)
// 테스트 8 〉    통과 (0.18ms, 33.4MB)
// 테스트 9 〉    통과 (0.16ms, 33.5MB)
// 테스트 10 〉 통과 (0.17ms, 33.4MB)


/* check(검증) - Big O Notation */

// time complexity  : O(nlogn)
// space complexity : O(n)
```

#### [테이블 해시 함수](https://school.programmers.co.kr/learn/courses/30/lessons/147354)

```javascript
/* redefine(재정의) */

// input1 : data : number 타입인 컬럼들(튜플)로 이루어진 테이블
// input2 : col(number)
// input3 : row_begin(number)
// input4 : row_end(number)
// return : 테이블의 해시 값(number)

// condition1 : 1-index 기준
// condition2 : data 길이 : [1, 2500]
// condition3 : data의 원소 길이 : [1, 500]
// condition4 : data[i][j] : [1, 1000000]
// condition5 : col : [1, data의 원소의 길이]
// condition6 : 1 <= row_begin <= row_end <= data의 길이
// condition7 : 튜플의 첫번째 값은 기본키이므로 중복 x

// algorithm : 다중 조건 정렬, bittwise XOR

// logic(psuedo) : 
// 1. 다중 조건 정렬(|| 연산자 사용)
// 2. S_i를 갱신하면서 answer 갱신(^)


/* solution(구현) */

function solution(data, col, row_begin, row_end) {
    let answer = 0;
    let sum = 0;
    
    data.sort((a, b) => a[col-1] - b[col-1] || b[0] - a[0])  // 다중 조건 정렬을 위해 || 연산자 이용
    
    for (let i=row_begin-1; i<row_end; i++) {
        sum = 0;
        data[i].forEach(el => sum += el%(i+1));              // S_i 갱신
        answer = answer ^ sum;                               // bitwise XOR
    }
    
    return answer;
}


/* 참고 링크 */
// https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_XOR


/* 결과 */
// 정확성
// 테스트 1 〉    통과 (0.24ms, 33.4MB)
// 테스트 2 〉    통과 (0.21ms, 33.6MB)
// 테스트 3 〉    통과 (0.21ms, 33.6MB)
// 테스트 4 〉    통과 (0.23ms, 33.7MB)
// 테스트 5 〉    통과 (0.99ms, 37.2MB)
// 테스트 6 〉    통과 (11.42ms, 83.3MB)
// 테스트 7 〉    통과 (7.84ms, 89.1MB)
// 테스트 8 〉    통과 (9.93ms, 88.7MB)
// 테스트 9 〉    통과 (11.10ms, 89.1MB)
// 테스트 10 〉 통과 (11.81ms, 88.5MB)
// 테스트 11 〉 통과 (0.07ms, 33.5MB)


/* check(검증) - Big O Notation */

// time complexity  : O(n*m)
// O(nlogn + (row_end - row_begin + 1) * m)에서 row_end - row_begin + 1의 최대 크기가 n이므로.
```

#### [점 찍기](https://school.programmers.co.kr/learn/courses/30/lessons/140107)

```javascript
/* redefine(재정의) */

// input1 : k(간격 - number)
// input2 : d(원점과의 거리 - number)
// return : 찍히는 점의 총 개수 - number

// condition1 : k : [1,1000000]
// condition2 : d : [1,1000000]

// algorithm : 수학

// logic(psuedo) : 




/* solution(구현) */

function solution(k, d) {
    let answer = 0;
    
    for (let i=0; i<=d; i+=k) {
        if (i > d) break;
        answer += parseInt(Math.sqrt(d**2 - i**2)/k) + 1;
    }
    return answer;
}


/* 결과 */
// 정확성
// 테스트 1 〉    통과 (0.04ms, 33.4MB)
// 테스트 2 〉    통과 (0.04ms, 33.4MB)
// 테스트 3 〉    통과 (0.48ms, 33.7MB)
// 테스트 4 〉    통과 (0.31ms, 33.6MB)
// 테스트 5 〉    통과 (0.63ms, 33.9MB)
// 테스트 6 〉    통과 (0.54ms, 33.9MB)
// 테스트 7 〉    통과 (0.40ms, 33.7MB)
// 테스트 8 〉    통과 (2.97ms, 37.6MB)
// 테스트 9 〉    통과 (0.63ms, 33.8MB)
// 테스트 10 〉 통과 (2.39ms, 37.1MB)
// 테스트 11 〉 통과 (17.80ms, 37.9MB)
// 테스트 12 〉 통과 (0.06ms, 33.4MB)
// 테스트 13 〉 통과 (12.57ms, 37.9MB)
// 테스트 14 〉 통과 (7.88ms, 37.8MB)
// 테스트 15 〉 통과 (0.06ms, 33.6MB)
// 테스트 16 〉 통과 (0.04ms, 33.4MB)



/* check(검증) - Big O Notation */

// time complexity  : O(d/k)
// space complexity : O(1)
```
