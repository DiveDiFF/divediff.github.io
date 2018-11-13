---
title: "Callback function of setState in React"
date: 2018-11-13 18:53:13 -0400
categories: React SetState
comments: true
---

# React 상태 관리의 필수 메소드 setState()


리액트에서 상태를 관리하는 방법은 state, props 두가지다. 부모 컴포넌트와 자식 컴포넌트는 이를 이용해 상태를 주고 받을 수 있다. 이 중에서 내용을 변경할 수 있는 것이
state인데 state의 직접 변경은 react가 감지하여 DOM의 rerender를 하지 못할 수 있기 때문에 일반적으로 금지된다.


```javascirpt

this.state.id = 13

```
> 직접 state의 id를 13으로 변경하고 있음. __금지!__

<br><br>
이럴 때 사용하는 메소드가 setState()다. setState 메소드를 이용해서 state를 재설정 해 주는 방식으로만 state 상태를 변화시켜야 React는 이를 감지하여 View를
변화시킨다.(구체적인 React의 setState 작동은 다루지 않는다.) 

```javascirpt

this.setState({id: 13})
```
> setState 메소드로 id를 13으로 변경하고 있음. __권장!__

<br><br>

## setState의 작동은 비동기

setState 메소드는 가능한 가장 마지막에 실행시킨다. 다시 말하면 setState 이후에 다른 작동을 코딩하지 않는다. 왜냐하면 setState 자체가 비동기 메소드이기 때문이다.
비동기 메소드라는 것은 실행 순서를 보장하지 않는다는 말이고, 이는 setState로 변경된 state를 전달하거나 함수를 실행하거나 하는 행위가 제대로 작동하지 않을 가능성이
크다는 것을 의미한다.

```javascript

this.setState({id: 13})
this.props.onChange(this.state.id)
```
> setState 이후에 onChange props에 state 전달

<br><br>

## setState 이후의 정상 작동을 위한 코딩

이를 해결하기 위한 방법으로 두가지 정도를 생각한다. 

1. setState에 callback 함수로 실행
2. Life Cycle 메소드를 이용

setState의 두번째 인자로 callback 함수를 작성하여 실행하면, 정상적으로 setState가 된 이후에 실행이 보장된다. 대부분의 커뮤니티나 강좌에서 이러한 방법을 권장하고
있을 만큼 원하는 결과를 얻을 수 있으리라 믿는다.

```javascript

this.setState({id: 13}, () => {this.props.onChange(this.state.id)})
```
> callback으로 state 전달 (1번 방법)

<br><br>

두번째 방법은 React의 LifeCycle 메소드를 활용하여, state가 바뀐 이후에 실행될 부분을 넣어준다.

```javascript
componentDidUpdate (prevProps, prevState) { 
  if (this.state.id !== prevState.id) { 
    this.props.onChange(this.state.id)
  } 
}
```
> componentDidUpdate 메소드 활용한 방법(2번방법)

비교해 보면 실행 코드가 간단하다면 LifeCycle 메소드를 활용하는 것도 가능할 것이나, 여러 함수에서 setState를 호출하는 경우 등 복잡해 졌을 때를 생각하면 개인적으로
1번 방법을 활용하는 것이 바람직 하다 생각한다.


