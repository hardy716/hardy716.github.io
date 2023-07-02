---
layout: post
title: Swift - Algorithm
image: /assets/img/blog/swift.png
accent_image: 
  background: url('/assets/img/sidebar-bg3.jpg') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  스위프트를 사용하여 알고리즘 문제를 풀고 기록합니다.
invert_sidebar: true
---

# Swift - Algorithm

* toc
{:toc}

## 📈 [백준](https://www.acmicpc.net/problemset?sort=ac_desc&algo=124)

백준 - 알고리즘 분류 - 수학


### 🔢 수학

#### [A+B](https://www.acmicpc.net/problem/1000)

```swift
if let input = readLine() {
    let numbers = input.split(separator: " ").compactMap { Int($0) }
    let sum = numbers.reduce(0, +)
    print(sum)
}
```

if let 바인딩을 사용해서 nil 체크와 값 추출을 동시에 수행했다.(강제 언래핑(!)에 비해 안전한 방식)
입력이 `nil`인 경우 블록 내부의 코드가 실행되지 않으므로, 런타임 오류를 방지할 수 있다.

`compactMap`은 `map`과 유사하게 배열의 각 요소를 변환하여 새로운 배열을 생성하지만, 변환 작업의 결과가 `nil`이 아닌 요소들로 이루어진 새로운 배열을 생성한다는 것에 차이가 있다.
`compactMap`을 사용함으로써, 변환 작업 후에 유효하지 않은 요소들을 제거하고 유효한 정수 값들로만 이루어진 배열을 얻을 수 있다.

![1000](/assets/img/blog/algorithm/1000.png){: width="100%" height="100%"}
