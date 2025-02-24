---
layout: post
title: MAK-E-AT TroubleShooting #3
image: /assets/img/blog/err/err-3-10.png
accent_image: 
  background: url('/assets/img/sidebar/puzzle.jpg') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  flutter_webview_plugin을 Android V2 embedding으로 마이그레이션하기
invert_sidebar: true
---

# [Error] The plugin flutter_webview_plugin uses a deprecated version of the Android embedding.

* toc
{:toc}


```bash
The plugin flutter_webview_plugin uses a deprecated version of the Android embedding.
To avoid unexpected runtime failures, or future build failures, try to see if this plugin supports the Android V2 embedding.r
Otherwise, consider removing it since a future release of Flutter will remove these deprecated APIs.
```

## 상황

flutter_webview_plugin 패키지를 사용해서 네이버 소셜 로그인 페이지를 웹뷰로 띄워주는 과정에서 큰 문제없이 동작은 하지만 위와 같은 에러가 발생했다.


## 에러 분석

네이버의 소셜 로그인 페이지를 웹뷰로 띄우는 과정에서 사용한 `flutter_webview_plugin` 패키지와 관련된 문제로, deprecated(사용 중단)된 Android embedding 버전을 사용하고 있다는 경고이다. 

( Android embedding에 대해 간단히 설명하자면, 플러터 프로젝트의 안드로이드 앱 통합 방식이다. )

기존에 사용하던 Android V1 embedding 방식에서 2019년에 Flutter 1.12와 함께 Android V2 embedding 방식이 도입되었는데,
`flutter_webview_plugin` 패키지는 V2로 마이그레이션이 되지 않아 사용이 중지된 Android V1 embedding 방식을 아직 사용하는 것 같다.

위 에러를 방치하면, 향후 빌드 실패나 런타임 오류가 발생할 위험이 있기 때문에 가능하면 해결하는 것이 좋다고 생각했다.


## 해결 방법

해결을 위해서는, 해당 플러그인을 V2로 직접 마이그레이션하거나 이미 마이그레이션이 완료된 다른 패키지의 사용을 고려해보아야 했고, 내가 택한 방법은 전자였다.

우선 `pub.dev`에 가서 내가 사용한 버전(^0.4.0)이 최신 버전이며, [flutter_webview_plugin](https://pub.dev/packages/flutter_webview_plugin)의 최신 업데이트가 22개월 전이라는 사실을 확인했다.

해당 플러그인의 [공식 깃허브 저장소 - fluttercommunity/flutter_webview_plugin](https://github.com/fluttercommunity/flutter_webview_plugin)를 살펴보니, 예상대로 많은 사람들이 deprecated version에 대해 이슈들을 생성한 것을 볼 수 있었고, 직접 문제점을 해결하려고 시도하신 분들도 간간히 보였다. 


### 마이그레이션 방법은 아래 문서들을 주로 참고했다.

[Supporting the new Android plugins APIs](https://docs.flutter.dev/release/breaking-changes/plugin-api-migration)

[Upgrading pre 1.12 Android projects](https://github.com/flutter/flutter/wiki/Upgrading-pre-1.12-Android-projects)


### 우선 두 방식의 차이점에 대해서 알아보았다.

1. **Android V1 embedding** 방식

- `io.flutter.app.FlutterActivity` 클래스를 사용한다.

- `android.app.Activity`를 직접 상속한다.

- `FlutterView`를 사용하여 플러터 엔진을 호스팅하고 렌더링한다.

- `PluginRegistry`를 사용하여 플러그인을 등록하고 관리한다.
    
2. **Android V2 embedding** 방식

- `io.flutter.embedding.android.FlutterActivity` 클래스를 사용한다.

- `androidx.appcompat.app.AppCompatActivity`를 상속한다.

- `FlutterEngine` 클래스를 사용하여 플러터 엔진을 관리하고 `FlutterView`를 사용하여 렌더링한다.

- `FlutterEngine`을 사용하여 플러그인을 등록하고 관리하며, 각 플러그인은 `io.flutter.embedding.engine.plugins.FlutterPlugin` 인터페이스를 구현해야 한다.
    

## 마이그레이션 진행 단계

### 플러그인 (공식) 레포지토리 포크 및 클론

[레포지토리 포크 - hardy716/flutter_webview_plugin](https://github.com/hardy716/flutter_webview_plugin)

```bash
git clone https://github.com/hardy716/flutter_webview_plugin.git
```

### 안드로이드 프로젝트 설정 업데이트 ( `android/build.gradle` )

1. 안드로이드 V2 임베딩은 최소 API 레벨 16(Android 4.1, Jelly Bean) 이상에서 작동하므로 minSdkVersion(최소 지원 SDK 버전)을 16으로 설정했다.

2. 컴파일 SDK 버전 및 대상 SDK 버전은 마이그레이션에 직접적인 영향을 주지는 않지만 최신 안드로이드 플랫폼과의 호환성 및 최신 API와 보안패치의 적용을 위해 30 이상으로 설정했다.

![err-3-1](/assets/img/blog/err/err-3-1.png){: width="60%" height="60%"}


### AndroidX 마이그레이션

- 프로젝트가 AndroidX 라이브러리를 사용하도록 설정했다.

`android.useAndroidX=true`

- jetifier를 활성화해서 Android Support Library를 사용하는 의존성을 자동으로 AndroidX로 변환한다.

`android.enableJetifier=true`

![err-3-2](/assets/img/blog/err/err-3-2.png){: width="60%" height="60%"}


### 플러그인 등록 코드 수정

![err-3-3](/assets/img/blog/err/err-3-3.png){: width="60%" height="60%"}

Android V1 embedding 방식이 사용하는 `io.flutter.app.FlutterActivity` 클래스를 검색해보니 `MainActivity.java`에서 사용 중인 것으로 확인된다.

해당 파일의 코드를 Android V2 embedding 방식의 코드로 교체한다.

![err-3-4](/assets/img/blog/err/err-3-4.png){: width="60%" height="60%"}


### 플러그인 코드 수정

- `io.flutter.plugin.common.MethodChannel` 클래스를 사용하는 코드를 찾아 필요하다면, Android V2 embedding 방식으로 업데이트를 진행했다.

![err-3-5](/assets/img/blog/err/err-3-5.png){: width="60%" height="60%"}

- `io.flutter.plugin.common.EventChannel` 클래스를 사용하는 코드를 찾아 필요하다면, Android V2 embedding 방식으로 업데이트를 진행했다. 

![err-3-6](/assets/img/blog/err/err-3-6.png){: width="60%" height="60%"}

- `io.flutter.plugin.common.PluginRegistry` 클래스를 사용하는 코드를 찾아 Android V2 embedding 방식으로 업데이트를 진행했다. 

![err-3-7](/assets/img/blog/err/err-3-7.png){: width="60%" height="60%"}


(참고) 일반적으로 MethodChannel과 EventChannel 클래스가 사용된 코드는 V2 embedding 방식에서도 동일하게 사용하지만, 필요하다면 플러그인의 초기화 및 액티비티 관련 코드를 수정해야 하기 때문에, 1, 2번도 진행했다.


### 기존 플러그인 대신 적용(테스트)

기존 플러그인을 사용하던 프로젝트에서 테스트를 해보았다.

먼저 마이그레이션한 플러그인의 경로와 기존 플러그인을 사용하던 프로젝트의 경로를 확인한다.

```bash
cd flutter_webview_plugin
pwd
```
**/Users/hyeono/desktop/flutter_webview_plugin**

```bash
cd makeat_fe
pwd
```
**/Users/hyeono/desktop/Frontend/makeat_fe**


앱 프로젝트의 pubspec.yaml 파일에서 아래와 같이 마이그레이션한 플러그인을 참조했다. path에는 위에서 확인한 플러그인 디렉토리의 절대 경로와 앱 프로젝트 디렉토리의 절대 경로를 비교해서 상대 경로를 입력했다.

![err-3-8](/assets/img/blog/err/err-3-8.png){: width="60%" height="60%"}


### 실행 결과

기존 플러그인의 경우 디버깅을 시작하면 아래와 같이 콘솔에 경고 문구가 찍힌다.

![err-3-9](/assets/img/blog/err/err-3-9.png)

V2로 마이그레이션한 플러그인을 적용한 모습이다. 경고문구가 사라진 것을 확인할 수 있다.

![err-3-10](/assets/img/blog/err/err-3-10.png)


### 변경 사항 반영 

V2로 마이그레이션한 플러그인의 변경사항을 반영하기 위해 플러그인 공식 레포지토리에 [풀리퀘스트](https://github.com/fluttercommunity/flutter_webview_plugin/pull/962#issue-1667425531)를 진행했다.

deprecated version 및 migration 관련 최근 이슈에도 내가 [마이그레이션한 플러그인을 소개](https://github.com/fluttercommunity/flutter_webview_plugin/issues/960)해서 PR이 병합되기 전에도 다른 분들이 쓸 수 있도록 조치했다.
