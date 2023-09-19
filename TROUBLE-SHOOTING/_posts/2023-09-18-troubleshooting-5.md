---
layout: post
title: TroubleShooting - Image.network 403 에러
image: /assets/img/blog/err/err-5-0.png
accent_image: 
  background: url('/assets/img/sidebar/puzzle.jpg') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  Flutter의 Image.network 403 에러
invert_sidebar: true
---

# Flutter `Image.network()` 403 에러

* toc
{:toc}


## 상황 🤯

```
======== Exception caught by image resource service ================================================
The following NetworkImageLoadException was thrown resolving an image codec:
HTTP request failed, statusCode: 403, https://image-comic.pstatic.net/webtoon/779632/thumbnail/thumbnail_IMAG21_4048795649913205816.jpg

When the exception was thrown, this was the stack: 
#0      NetworkImage._loadAsync (package:flutter/src/painting/_network_image_io.dart:135:9)
<asynchronous suspension>
Image provider: NetworkImage("https://image-comic.pstatic.net/webtoon/779632/thumbnail/thumbnail_IMAG21_4048795649913205816.jpg", scale: 1.0)
Image key: NetworkImage("https://image-comic.pstatic.net/webtoon/779632/thumbnail/thumbnail_IMAG21_4048795649913205816.jpg", scale: 1.0)
=====================================================
```

이미지 URL이 403 Forbidden 오류를 반환했다는 에러이다.


## 문제 분석 🧐

서버에서 특정 요청을 거부하였음을 의미하는데, Flutter의 `Image.network`가 사용하는 `User-Agent`가 서버에서 차단되었을 가능성을 생각해보았다.


## 해결 방법 😎

Flutter의 Image.network를 사용하여 이미지를 가져올 때 User-Agent 값을 알기 위해 다음과 같이 진행했다.

`image.dart → image_provider.dart → _network_image_web.dart`

파일들을 순회하면서 알게된 사실을 통해 다음과 같이 유추해보았다.

> 1. `NetWorkImage` 클래스의 `headers` 속성은 `Map<String, String>?` 타입이다.
> 2. `Image.network`를 사용할 때 `headers`를 명시적으로 설정하지 않으면, 내부적으로 사용되는 `NetworkImage`의 `headers`는 `null`로 초기화된다.
> → 결론적으로, 초기의 `User-Agent` 값이 `null`이거나 제대로 설정되지 않았기 때문에 문제가 발생했을 것이다.

<br>

그러나 일반적인 이미지 주소는 별도로 헤더를 명시적으로 설정하지 않아도 잘 작동되는 것을 확인할 수 있다.

구글 검색창에 [구글 이미지의 주소](https://www.google.com/images/branding/googlelogo/1x/googlelogo_light_color_272x92dp.png)를 가지고 실험했고, 문제없이 이미지를 잘 받아온다는 것을 확인할 수 있었다.(이미 가능함을 알고 있었지만, 다시 확인해보았다.)

![err-5-1](/assets/img/blog/err/err-5-1.png){: width="30%"}

<br>

따라서 웹툰 썸네일 이미지 주소를 자세히 살펴보았다.

> [https://image-comic.pstatic.net/webtoon/779632/thumbnail/thumbnail_IMAG21_4048795649913205816.jpg](https://image-comic.pstatic.net/webtoon/779632/thumbnail/thumbnail_IMAG21_4048795649913205816.jpg)

[`pstatic.net`](http://pstatic.net) 도메인은 네이버에서 사용하는 CDN(Content Delivery Network) 도메인 중 하나이다.

따라서 위 주소를 네이버 웹툰의 썸네일 이미지를 호스팅하는 서버라고 유추했다.

<br>

예전에 크롤링을 해보다가 알게된 `robots.txt`가 생각나서 혹시나 해서 https://image-comic.pstatic.net/robots.txt 를 확인했다.

![err-5-2](/assets/img/blog/err/err-5-2.png){: width="60%"}

위에서 알 수 있는 정보는, 

> 1. 해당 도메인에서 호스팅되고 있는 서비스가 `nginx` 웹 서버를 사용하고 있으며, 
> 2. 해당 서버에 `robots.txt` 파일이 존재하지 않는다는 것이다.

쉽게 말하면, 영양가 있는 정보가 없다고 할 수 있다.

(참고로 네이버 웹툰의 robots.txt 정보는 아래와 같다.)

```
User-agent: *
Disallow: /

User-agent: Yeti
Disallow: /
Allow: /navercontest/2022/
```

<br>

크롬에서 해당 이미지 주소로 접속 후, 개발자 도구로 자세히 살펴보았다.

![err-5-3](/assets/img/blog/err/err-5-3.png){: width="80%"}
![err-5-4](/assets/img/blog/err/err-5-4.png){: width="80%"}

일반적인 브라우저에서는 이미지가 성공적으로 로드가 되고 있는 상황이기 때문에, 개발자 도구에서 확인한 User-Agent를 사용해보았고 에러를 해결할 수 있었다.

> ![err-5-5](/assets/img/blog/err/err-5-5.png){: width="80%"}
>
> `Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.0.0 Safari/537.36`

## 알게된 사실 🥳

다른 일반적인 이미지 주소와 다르게, 웹툰 썸네일 이미지 주소가 불러와지지 않았던 이유는 서버 간의 정책 차이로 보인다. 에러가 발생했던 네이버 웹툰 서버(정확하게는, 네이버 웹툰의 썸네일 이미지를 호스팅하는 서버)의 경우, 웹툰 콘텐츠의 무단 복제나 스크래핑을 방지하기 위해 `User-Agent` 기반의 접근 제한을 설정하여 일반적인 웹 브라우저에서의 요청만을 허용한 것이 아닐까 생각한다. 결국 `User-Agent`를 일반적인 웹 브라우저의 `User-Agent`로 변경함으로써 문제를 해결하였지만, 이러한 방식은 서버의 정책을 우회하는 행위로 간주될 수 있기 때문에 주의가 필요할 것으로 보인다.

다양한 브라우저의 UA 문자열(User-Agent 값)에 대해 더 알아보고 싶다면, [여기](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/User-Agent) 참고하는 것을 추천한다.
