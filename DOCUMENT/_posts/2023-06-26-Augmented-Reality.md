---
layout: post
title: Clean Agile - Back to Basics
image: /assets/img/blog/doc/augmented-reality.png
accent_image: 
  background: url('/assets/img/sidebar-bg3.jpg') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  Dieter Schmalstieg 와  Tobias Hollerer 의  'Augmented Reality: Principles and Practice' 을 읽고 정리한 글입니다.
invert_sidebar: true
---

# Augmented Reality: Principles and Practice

최근에 많이 시청하고 있는 유튜버 ['개발자 옆 디자이너'의 영상](https://www.youtube.com/watch?v=r4dIowyDbgs)을 보고 구매하게 된 책이다.

증강 현실의 기본 원칙과 실천 측면을 꼼꼼히 다룬 책인 것 같아 AR에 관심이 있는 분들이라면 읽어보는 것을 추천한다.



* toc
{:toc}


### 📒 1장 : 증강 현실의 개요

> 먼저 온라인 정보에 대한 접근이 엄청나게 늘어나며 대규모의 정보 소비자들이 생겨났다. 이런 소비자들은 이어서 정보 제조자로 활동하며 서로 대화할 수 있게 되고, 결국 어디에서 어떤 상황에서나 커뮤니케이션을 관리할 수단까지 갖게 됐다. 그럼에도 이 모든 정보가 수집되고 작성되며 커뮤니케이션이 일어나는 물리적 세계는 사용자의 전자적 활동에 연결될 준비를 하지 못했다.

1장에서 가장 기억에 남는 내용이었다. 사실 '증강 현실이 왜 필요한가'에 대해서는 깊게 고민해 본 적이 없었기 때문에 위 문장이 좀 더 크게 다가왔던 것 같다. 이 책에 따르면 증강 현실은 물리 세계에 대해 전자적으로 강화된 단순하고 즉각적인 사용자 인터페이스를 제공함으로써 이러한 상황을 변화시킬 수 있고, 또 그 과정에서 인간의 인식과 인지를 굉장히 새로운 방식으로 확장할 수 있다고 한다.


> AR에 대해 가장 폭넓게 받아들여지는 정의는 1997년 아주마가 논문을 통해 제기했다...

원래 알고있는 내용이었지만 신기했던 점은 이 책이 아주마의 논문이 나온지 20년 뒤의 출판물임에도 불구하고 AR의 3요소에 대한 내용이 서로 완벽하게 일치했다는 점이었다. 

Ronald T.Azuma의 조사 논문 'A Survey of Augmented Reality'를 읽고 작성한 [블로그 글](https://hardy716.github.io/blog/document/2023-06-21-a-survey-of-augmented-reality/#-ar의-정의-3요소)


> 완전한 AR 시스템에는 트래킹, 등록, 시각화라는 최소한 세 가지 컴포넌트가 필요하다. 네 번째 컴포넌트인 공간 모형은 실제 세계와 가상 세계에 대한 정보를 저장한다.

[삼성 SDS 관련 글](https://www.samsungsds.com/kr/insights/augmented-reality-technology.html)에 따르면, 증강현실의 구현 시스템은 '트래킹 시스템(Tracking System), 그래픽 시스템(Graphics System), 디스플레이 시스템(Display System)'의 3가지 요소로 이루어진다고 한다. 책에서 언급한 등록과 시각화는 각각 그래픽 시스템과 디스플레이 시스템과 관련이 있으며, 추후에 더 자세히 다룰 예정이다.


> 사실, '혼합 현실'보다 '증강 현실'이란 용어를 선호하는 이들도 있는데, MR이라는 개념보다 더 폭넓기 때문이다. 이런 관점은 현실부터 가상 현실까지를 아우르는 연속체를 제안하는 밀그램과 키시노에서 유래했다. 둘은 MR의 특징을 다음과 같이 설명한다. (MR은) 완전한 현실의 환경을 완전한 가상의 환경과 연결하는 '가상 연속체'에 따른 실체와 가상 세계에서 나온다.

[정동훈 교수님의 블로그 글](https://www.donghunc.kr/single-post/2017/03/03/가상현실-증강현실-그리고-혼합현실의-이해)에 따르면, 현실과 가상현실 사이에는 가상성의 정도에 따라 현실과 더 가까울 수도 가상현실과 더 가까울 수도 있는데, 이러한 구분을 위해서 제시한 것이 '가상성의 연속성(virtuality continuum)'이다. 가상성이라는 개념은 어느 단계를 구체적으로 단절시킬 수 있는 것이 아니라, 현실에 더해서 가상의 대상물(object)이 얼마나 많이 더해지는가에 따라 가상현실에 가까워진다는 연속체적인 속성을 띈다는 주장을 한 것이다.

![ar1-1](/assets/img/blog/doc/Reality-Virtuality-Continuum.jpg){: width="80%" height="60%"}

밀그램과 키시노가 정의한 증강 현실과 아즈마가 정의한 증강 현실에는 차이가 있다는 점을 주의해야 한다. 쉽게 얘기하면, 밀그램과 키시노의 증강 현실은 현실과 가상 현실 사이에 존재하지만 현실에 좀 더 치우쳐 있지만 아즈마의 증강 현실은 현실과 가상 현실 사이 그 어딘가에 존재한다고 생각하면 된다. 그외에도 다른 차이점이 있지만, 추후에 기회가 된다면 그때 추가로 정리할 예정이다.
