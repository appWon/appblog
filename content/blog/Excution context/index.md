---
title: 실행 컨텍스트
date: "2021-06-26"
tags: [js]
thumbnail : ../../assets/js.png
---

<br><br>

자바스크립트를 공부하면서 `호이스팅` , `스코프 체인` , `this` 이해하기 힘든 용어가 많이 나온다. 실행 컨텍스트를 알게 된다면 좀더 이해하기 쉬울거 같다.

>1. 동기식으로 작동한다.
>2. 단일 스레드로 작동한다.
>
>>1) 단일 스레드이기 때문에 하나의 Global Context 를 가진다.
>>2) Function context는 여러가지를 가진다.

<br>

```
// 실행컨텍스트 스택 단계
function func1(){
  function func2(){}
  func2();
}
func1();
```

위 코드를 예를 들어서 실행과정을 스택으로 표현해 보았습니다.

<br>

<br>

<img src='https://images.velog.io/images/app235/post/8ecda208-f358-4f80-b484-633d6be21656/KakaoTalk_Photo_2021-08-22-19-32-50.png' style='width:750px'/>

<br>

<br>

> 자바스크립트가 실행이 되면 가장 먼저 `전역 실행 컨텍스트` 가 스택에 쌓이고  차례대로 `각각의 함수 컨텍스트` 가. 만들어 지고, LIFO 의 구조를 가진다.
>
> 전역 컨텍스트는 JS가 종료될 때 없어진다.

<br>

<br>

### 실행 컨텍스트 생성 과정

<br>

<img src='https://images.velog.io/images/app235/post/e0c360a7-f568-4b75-a015-af0f886e5629/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-08-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%208.02.21.png'>

> 전역 컨텍스트 및 함수 컨텍스트는 2가지의 과정을 거쳐서 만들어진다.
>
> 1. 생성 단계 - Creation Phase
>
>    > 스코프 내에 함수선언을 하고 메모리에 저장을 한다.
>    >
>    > 변수를 선택하고 undefined 를 할당 한다. `hoisting 호이스팅`
>
> 2. 실행 단계 - Execution Phase
>
>    > 변수에 값 할당
>    >
>    > 함수 실행

이 과정을 거쳐서 실행 컨텍스트가 생성이 됩니다. 그러면 이번에 위 코드를 예를 들어 보겠습니다.



1. 전역 컨텍스트 ( 생성 및 실행 )

```javascript
GlobalContextCreation = {
  VariableObject :{
    func1: function
  },
  ScopeChain: [],
  this: window
}
```

2. func1 ( 생성 단계 )

```javascript
Func1ContextCreation = {
  VariableObject :{
    arguments: {
      length: 0
    },
    Text1: undefined,
    Text2: undefined,
    func2: function
  },
  ScopeChain: [Gloval VO],
  this: window
}
```

3. func1 ( 실행 단계 )

```javascript
Func1ContextCreation = {
  VariableObject :{
    arguments: {
      length: 0
    },
    Text1: '변수 1번',
    Text2: '변수 2번',
    func2: function
  },
  ScopeChain: [Gloval VO],
  this: window
}
```

4. func2 ( 생성 단계 )

```javascript
Func2ContextCreation = {
  VariableObject :{
    arguments: {
      length: 0
    },
    Text3: undefined,
  },
  ScopeChain: [func1 VO,Gloval VO],
  this: window
}
```

5. func2 ( 실행 단계 )

```javascript
Func2ContextCreation = {
  VariableObject :{
    arguments: {
      length: 0
    },
    Text3: '변수 3번',
  },
  ScopeChain: [func1 VO,Gloval VO],
  this: window
}
```

>이렇게 함수가 실행 되면서 ScopeChain 이 차례대로 생성이 된다.
>
>this는 함수 호출 방식에 따라 달라지고 bind를 사용하여 함수 호출방식에 상관없이 대상을 고정할 수있지만 기본적으로는 전역 컨텍스트를 따라 window를 가르키고 있다.

