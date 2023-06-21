---
layout: post
title: Clean Agile - Back to Basics
image: /assets/img/blog/doc/a-survey-of-augmented-reality.png
accent_image: 
  background: url('/assets/img/sidebar-bg3.jpg') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  Ronald T. Azuma 의  'A Survey of Augmented Reality' 을 읽고 정리한 글입니다.
invert_sidebar: true
---

# A Survey of Augmented Reality


AR에 관심이 있거나 이 분야에 종사하는 사람이라면 한번쯤은 보았을 조사 논문 이다.

1997년에 발표된 논문이지만, Ronald T. Azuma가 구체화한 증강현실(AR)의 개념은 아직까지도 널리 사용되고 있다.

[A Survey of Augmented Reality](https://www.cs.unc.edu/~azuma/ARpresence.pdf) 를 읽고 AR에 대한 기본적인 지식을 습득하고자 했다.

아래는 논문의 일부를 인용한 글이다.


### 💡 AR이란? - 1

> In contrast, AR allows the user to see the real world, with virtual objects superimposed upon or composited with the real world. Therefore, AR supplements reality, rather than completely replacing it. Ideally, it would appear to the user that the virtual and real objects coexisted in the same space,

대조적으로, AR은 사용자가 실제 세계에 가상 물체를 겹치거나 합성하여 실제 세계를 볼 수 있도록 합니다. 따라서 AR은 현실을 완전히 대체하는 것이 아니라 현실을 보완합니다. 이상적으로, 사용자에게 가상의 물체와 실제 물체가 같은 공간에 공존하는 것처럼 보일 것입니다.


### 💡 AR이란? - 2

> AR can be thought of as the "middle ground" between VE (completely synthetic) and telepresence (completely real).

AR은 VE(완전한 합성)와 telepresence(완전한 실제) 사이의 "중간 지점"으로 생각할 수 있습니다.


### 💡 AR의 정의 (3요소)

> <aside>
💡 To avoid limiting AR to specific technologies, this survey defines AR as systems that have the following three characteristics:

1) Combines real and virtual 

2) Interactive in real time

3) Registered in 3-D
</aside>

AR을 특정 기술로 제한하지 않기 위해 이 설문 조사에서는 AR을 다음과 같은 세 가지 특성을 가진 시스템으로 정의합니다:

1) 실제와 가상을 결합 
2) 실시간으로 상호 작용(대화형 미디어)
3) 3-D로 등록됨


### 💡 AR의 유용성

> Why is combining real and virtual objects in 3-D useful? Augmented Reality enhances a user's perception of and interaction with the real world. The virtual objects display information that the user cannot directly detect with his own senses. The information conveyed by the virtual objects helps a user perform real-world tasks. AR is a specific example of what Fred Brooks calls Intelligence Amplification (IA): using the computer as a tool to make a task easier for a human to perform.

실제 물체와 가상 물체를 3D로 결합하는 것이 왜 유용합니까? 증강 현실은 사용자의 현실 세계에 대한 인식과 상호 작용을 향상시킵니다. 가상 개체는 사용자가 직접 감지할 수 없는 정보를 표시합니다. 가상 객체가 전달하는 정보는 사용자가 실제 작업을 수행하는 데 도움이 됩니다. AR은 프레드 브룩스가 지능 증폭(IA)이라고 부르는 것의 구체적인 예입니다. 컴퓨터를 도구로 사용하여 인간이 작업을 더 쉽게 수행할 수 있도록 하는 것입니다.


### 💡 AR의 잠재력 - 1

> Besides adding objects to a real environment, Augmented Reality also has the potential to remove them. Current work has focused on adding virtual objects to a real environment. However, graphic overlays might also be used to remove or hide parts of the real environment from a user.

증강 현실은 실제 환경에 객체를 추가하는 것 외에도 객체를 제거할 수 있는 잠재력을 가지고 있습니다. 현재 작업은 실제 환경에 가상 개체를 추가하는 데 초점을 맞추고 있습니다. 그러나 그래픽 오버레이를 사용하여 실제 환경의 일부를 사용자로부터 제거하거나 숨길 수도 있습니다.


### 💡 AR의 잠재력 - 2

> Augmented Reality might apply to all senses, not just sight.

증강 현실은 시각뿐만 아니라 모든 감각에 적용될 수 있습니다.


### 💡 가상환경과의 비교

> The overall requirements of AR can be summarized by comparing them against the requirements for Virtual Environments, for the three basic subsystems that they require.

AR의 전반적인 요구 사항은 가상 환경에 대한 요구 사항, 즉 필요한 세 가지 기본 하위 시스템에 대한 요구 사항과 비교하여 요약할 수 있습니다.

> 1) Scene generator: Rendering is not currently one of the major problems in AR. VE systems have much higher requirements for realistic images because they completely replace the real world with the virtual environment. In AR, the virtual images only supplement the real world. Therefore, fewer virtual objects need to be drawn, and they do not necessarily have to be realistically rendered in order to serve the purposes of the application. For example, in the annotation applications, text and 3-D wireframe drawings might suffice. Ideally, photorealistic graphic objects would be seamlessly merged with the real environment (see Section 7), but more basic problems have to be solved first.

1) Scene generator: 렌더링은 현재 AR에서 주요 문제 중 하나가 아닙니다. VE 시스템은 실제 환경을 가상 환경으로 완전히 대체하기 때문에 실제 이미지에 대한 요구 사항이 훨씬 높습니다. AR에서 가상 이미지는 실제 세계를 보완할 뿐입니다. 따라서 더 적은 수의 가상 개체를 그려야 하며, 애플리케이션의 목적에 맞게 현실적으로 렌더링할 필요는 없습니다. 예를 들어 주석 응용프로그램에서는 텍스트 및 3D 와이어프레임 도면으로 충분할 수 있습니다. 이상적으로는 사실적인 그래픽 객체가 실제 환경과 원활하게 통합될 수 있지만(섹션 7 참조), 보다 기본적인 문제를 먼저 해결해야 합니다.

> 2) Display device: The display devices used in AR may have less stringent requirements than VE systems demand, again because AR does not replace the real world. For example, monochrome displays may be adequate for some AR applications, while virtually all VE systems today use full color. Optical see-through HMDs with a small field-of-view may be satisfactory because the user can still see the real world with his peripheral vision; the see-through HMD does not shut off the user's normal field-of-view. Furthermore, the resolution of the monitor in an optical see-through HMD might be lower than what a user would tolerate in a VE application, since the optical see-through HMD does not reduce the resolution of the real environment.

2) 디스플레이 장치: AR에 사용되는 디스플레이 장치는 VE 시스템이 요구하는 것보다 덜 엄격한 요구 사항을 가질 수 있습니다. AR이 실제 세계를 대체하지 않기 때문입니다. 예를 들어, 현재 거의 모든 VE 시스템이 전체 색상을 사용하는 반면, 단색 디스플레이는 일부 AR 애플리케이션에 적합할 수 있습니다. 시야가 작은 광학 시스루 HMD는 사용자가 여전히 주변 시야로 실제 세계를 볼 수 있기 때문에 만족스러울 수 있습니다. 시스루 HMD는 사용자의 일반 시야를 차단하지 않습니다. 또한 광학 시스루 HMD의 모니터 해상도는 사용자가 VE 애플리케이션에서 허용하는 해상도보다 낮을 수 있습니다. 광학 시스루 HMD는 실제 환경의 해상도를 감소시키지 않기 때문입니다.

> 3) Tracking and sensing: While in the previous two cases AR had lower requirements than VE, that is not the case for tracking and sensing. In this area, the requirements for AR are much stricter than those for VE systems. A major reason for this is the registration problem, which is described in the next section.

3) 추적 및 감지: 이전 두 경우에서 AR은 VE보다 요구 사항이 낮았지만 추적 및 감지에는 해당되지 않습니다. 이 영역에서 AR에 대한 요구사항은 VE 시스템에 대한 요구사항보다 훨씬 엄격합니다. 이 문제의 주요 원인은 다음 섹션에서 설명하는 등록 문제입니다.


이외에도 AR 기술을 사용하는 다양한 분야에서의 응용 사례와 AR의 작동 원리 및 핵심 기술에 대해 서술하고 있으나, 비교적 오래된 자료이기 때문에 참고만 했습니다. 위 논문에서 언급되었던 '트래킹'이나 '캘리브레이션', '등록'의 경우 추후에 다른 책을 통해 더 자세하게 살펴보겠습니다.