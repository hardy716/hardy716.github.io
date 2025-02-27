---
layout: post
title: MAK-E-AT TroubleShooting #1
image: /assets/img/blog/err/err-1.png
accent_image: 
  background: url('/assets/img/sidebar/puzzle.jpg') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  Flutter 최신 버전 업그레이드 후, 모든 flutter 명령어가 실행되지 않는 현상 
invert_sidebar: true
---

# [ERROR] Failed to start the Dart CLI isolate. Could not resolve DartDev snapshot or kernel.

* toc
{:toc}


```bash
Building flutter tool...
Failed to start the Dart CLI isolate. Could not resolve DartDev snapshot or kernel.
(null).
Error: Unable to 'pub upgrade' flutter tool. Retrying in five seconds... (9 tries left)
Failed to start the Dart CLI isolate. Could not resolve DartDev snapshot or kernel.
(null).
Error: Unable to 'pub upgrade' flutter tool. Retrying in five seconds... (8 tries left)
Failed to start the Dart CLI isolate. Could not resolve DartDev snapshot or kernel.
(null).
Error: Unable to 'pub upgrade' flutter tool. Retrying in five seconds... (7 tries left)
Failed to start the Dart CLI isolate. Could not resolve DartDev snapshot or kernel.
(null).
Error: Unable to 'pub upgrade' flutter tool. Retrying in five seconds... (6 tries left)
Failed to start the Dart CLI isolate. Could not resolve DartDev snapshot or kernel.
(null).
Error: Unable to 'pub upgrade' flutter tool. Retrying in five seconds... (5 tries left)
Failed to start the Dart CLI isolate. Could not resolve DartDev snapshot or kernel.
(null).
Error: Unable to 'pub upgrade' flutter tool. Retrying in five seconds... (4 tries left)
Failed to start the Dart CLI isolate. Could not resolve DartDev snapshot or kernel.
(null).
Error: Unable to 'pub upgrade' flutter tool. Retrying in five seconds... (3 tries left)
Failed to start the Dart CLI isolate. Could not resolve DartDev snapshot or kernel.
(null).
Error: Unable to 'pub upgrade' flutter tool. Retrying in five seconds... (2 tries left)
Failed to start the Dart CLI isolate. Could not resolve DartDev snapshot or kernel.
(null).
Error: Unable to 'pub upgrade' flutter tool. Retrying in five seconds... (1 tries left)
Command 'pub upgrade' still failed after 10 tries, giving up.
```

## 상황

Flutter 최신 버전 업그레이드 후, 모든 flutter 명령어가 인식되지 않고 실행되지 않는 현상 발생.


## 에러 분석

이 에러는 Dart CLI가 실행되지 않고 종료될 때 발생할 수 있으며, DartDev 스냅샷 또는 커널 파일을 찾을 수 없을 때 발생한다.

- Dart CLI
    - Dart 언어를 사용하여 개발된 명령줄 도구
    - 코드 빌드, 디버스, 테스트 등을 수행

- DartDev 스냅샷
    - Dart 언어 컴파일러의 한 형태
    - Dart 코드를 네이티브 코드로 컴파일하는데 사용
    
- 커널 형식
    - Dart 언어의 AOT 컴파일러에서 사용되는 중간 형식
    - Dart 코드를 바이너리 형식으로 컴파일하는데 사용

Dart CLI는 DartDev 스냅샷을 사용하여 Dart 코드를 실행하고, Dart AOT 컴파일러는 Dart 코드를 커널 파일로 컴파일한다. 쉽게 말해, DartDev 스냅샷과 커널 파일은 Dart CLI와 함께 사용되는 도구로 Dart 코드를 실행하는 데에 사용된다.
### 가능성 있는 에러 발생 원인으로는...

1. Dart SDK 업그레이드
    Dart SDK 업그레이드를 수행하는 과정에서 기존에 설치된 DartDev 스냅샷 또는 커널 파일이 새 버전과 호환되지 않는 경우

2. 파일 권한 문제
    파일 권한 문제로 인해 DartDev 스냅샷 또는 커널 파일에 액세스할 수 없는 경우

3. 캐시 불일치
    DartDev 스냅샷 또는 커널 파일과 관련된 캐시가 불일치하는 경우

4. 손상된 파일
    DartDev 스냅샷 또는 커널 파일이 손상된 경우
    
5. 환경 변수 문제
    환경 변수가 올바르게 설정되어 있지 않거나 잘못된 경우


Flutter 또는 Dart SDK의 버전 업데이트나 설치 이후에 이러한 문제가 종종 발생하는 것으로 보이는데, 일반적으로 flutter/bin/cache 디렉터리 안의 모든 항목을 제거하면 대부분 해결된다고 한다.


## 해결 방법

내 경우에도 캐시 불일치가 주요 원인이었고, (Stack Overflow에서) [Basil Mariano가 작성한 해결 방법](https://stackoverflow.com/questions/69193256/failed-to-start-the-dart-cli-isolate-null-in-mac)을 적용했다.


나는 아래와 같은 단계로 문제를 해결했다.

- `which flutter`
    
    Flutter를 설치한 경로를 불러온다.
    
- `sudo rm -r {flutter_direcotry}/bin/cache`
    
    캐시 내 항목들을 관리자 권한으로 제거한다.
    (직접 해당 위치로 이동해서 캐시 내 항목들을 제거해도 상관없다.)

- `flutter doctor -v`
    
    최신 Flutter SDK 버전을 로컬 환경에 다시 다운로드하고, 필요한 플랫폼 도구가 설치되어 있는지 확인하는 작업을 수행한다.


## 기타 참고 링크
[Terry님 블로그 - (Flutter) Failed to start the Dart CLI isolate(null). 에러](https://terry1213.github.io/flutter/flutter-failed-to-start-the-dart-cli-isolate-null/)
