---
title: "Using ref with @withStyles"
date: 2018-11-06 11:21:20 -0400
categories: ref, react
comments: true
---

# Material-UI의 @withStyles 사용이 대상 class의 인스턴스를 이상하게 변화시켜 ref 설정이 깨지는 문제

Material-UI의 customizing 방법으로 편하고 가독성이 좋은 해당 클래스에 withStyles 데코레이터를 붙이는 방식을 이용

```javaScirpt
@withStyles(()=> ({
  root: {},
  title:  {},
  ...
}))
class AnyComponent extends React.Componet {
...
}
```
>@withStyles를 사용한 Component Styling 예시


<br><br>
해당 컴포넌트에 ref가 설정되어 있는 경우 해당 class를 wrapping 하고 있는 @withStyles 데코레이터로 인해 참조가 깨짐

```javaScirpt
...
<AnyComponent ref={ref => this.component = ref} />
...
```
>Component에 ref 참조 설정 예시

<br><br>
withStyles의 클래스를 살펴보면 꾸며지는 Component Class를 받아와 새로운 인스턴스를 만들어 내는 구조임. 개발자도구로 Elements를 살펴보면 추가적인 wrapping이
추가되어 있음을 알 수 있음. ref가 이 외부의 wrapping Elements에 binding 되는 것이 아닌가 추측함. 해결을 위해 뒤지다가 Material-UI 문서에서 innerRef Props 발견.

**ref를 innerRef로 대체하는 것만으로 해당 문제 해결이 가능했다.!!**

```javaScirpt
...
<AnyComponent innerRef={ref => this.component = ref} />
...
```
>ref -> innerRef 로 대체 설정 예시

