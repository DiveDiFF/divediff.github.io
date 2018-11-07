---
title: "Ref fire After ComponentDidUpdate Method in React"
date: 2018-10-31 14:26:28 -0400
categories: React Ref
comments: true
---




1. React의 LifeCycle Method가 3rd party library (like M-UI)에서 이상하게 작동하는 문제 발생
  - M-UI의 다이얼로그가 단순히 감춰놓는 식의 방식이 아니라 완전히 DOM을 생성, 제거 하기 때문에 발생하는 문제?로 추정

2. 이로 인해 M-UI로 만들어진 다이얼로그 안에 daumpostcode 인스턴스가 제대로 embed되지 않는 문제 발생.
  - 첫번째는 정상 작동, 닫기(또는 저장) 이후 재실행 시 embed되지 않음

3. M-UI는 생성과 생성 이후의 Component Life Cycle이 다른 것 같음.
  - ComponentDidUpdate는 state(false -> open) 변경 이후 rendering이 끝나 DOM이 생성된 이후에 호출될 줄 알았는데 순서가 이상해짐

4. M-UI Document에서 Enter, Entering, Entered, Exit, Exiting, Exited 등 나름대로의 LifeCycle API가 있음을 발견

5. 다이얼로그 open 후 DOM이 완전히 그려진 후에 daumpostcode 인스턴스가 embed되도록 하기 위해 onEntered API로 props 전달하여 해당 문제 해결
