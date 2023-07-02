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

#### [1000 / A+B](https://www.acmicpc.net/problem/1000)

```swift
if let input = readLine() {

    let numbers = input.split(separator: " ").compactMap { Int($0) }
    let sum = numbers.reduce(0, +)
    
    print(sum)
}
```

if let 바인딩(강제 언래핑(!)에 비해 안전한 방식)을 사용해서 nil 체크와 값 추출을 동시에 수행했다.
입력이 `nil`인 경우 블록 내부의 코드가 실행되지 않으므로, 런타임 오류를 방지할 수 있다.

`compactMap`은 `map`과 유사하게 배열의 각 요소를 변환하여 새로운 배열을 생성하지만, 변환 작업 후에 `nil`인 요소를 제거한다는 것에 차이가 있다.
`compactMap`을 사용함으로써, 변환 작업 후에 유효하지 않은 요소들을 제거하고 유효한 정수 값들로만 이루어진 배열을 얻을 수 있다.

`reduce`는 배열의 모든 요소를 합하는 기능을 제공한다.

![1000](/assets/img/blog/algorithm/1000.png){: width="100%" height="100%"}


#### [2739 / 구구단](https://www.acmicpc.net/problem/2739)

```
if let input = readLine(), let n = Int(input) {
    Array(1...9).forEach { print("\(n) * \($0) = \(n * $0)") }
}
```

콤마(,)를 통해 두 개의 옵셔널 바인딩을 동시에 수행했다.

`1...9` 범위를 사용하여 1부터 9까지의 숫자를 나타내는 배열을 생성했다. `forEach` 메서드를 사용하여 배열의 각 요소에 대해 클로저를 반복적으로 실행했다. 추후에 스위프트의 클로저와 자바스크립트의 클로저를 비교해서 정리할 때, 더 자세히 다뤄볼 예정이다.

![1000](/assets/img/blog/algorithm/2739.png){: width="100%" height="100%"}


#### [2753 / 윤년](https://www.acmicpc.net/problem/2753)

```
if let input = readLine(), let num = Int(input) {
    if (num % 400 == 0) || (num % 4 == 0 && num % 100 != 0) {
        print("1")
    } else {
        print("0")
    }
}
```

주어진 연도가 윤년인 경우는 아래 두 가지 조건 중 하나를 만족할 때이다.
조건 1 `(num % 400 == 0)` : 400의 배수일 때
조건 2 `(num % 4 == 0 && num % 100 != 0)` : 4의 배수이면서 100의 배수가 아닐 때

![1000](/assets/img/blog/algorithm/2753.png){: width="100%" height="100%"}
