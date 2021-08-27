---
title: 배열함수
date: "2021-02-05"
tags: [js]
thumbnail : ../../assets/js.png
---

<br>

배열함수를 사용하다가 흔히 사용하지 않는 함수는 잊어먹기 쉬워서 정리하였다.

<br>

###### Includes

배열의 각 항목을 참조하여 `조건이 맞는 항목이 있으면 true 반환 후 즉시 종료`

```javascript
const numberList = [ 1, 2, 3, 4, 5];
numberList.includes(2)
// true
```

<br>

<br>

###### some

배열의 각 항목을 참조하여 `조건이 맞는 항목이 있으면 true 반환 후 즉시 종료`

```javascript
const numberList = [ 1, 2, 3, 4, 5];
numberList.some((num) => {
  return num % 2 === 0;
});
// true ( 2에서 종료 )
```

<br>

###### every

배열의 `전체 값들이` 조건에 맞을 경우 true 반환

```javascript
const numberList = [ 1, 2, 3, 4, 5];
numberList.every((num) => {
  return num % 2 === 0;
});
// false
```

<br>

###### map

배열의 각 항목을 참조하여 `다양한 값들로 반환`을 할 수 있다.

```javascript
const numberList = [ 1, 2, 3, 4, 5];
numberList.map((num) => {
  return num * 10;
});
// [ 10, 20, 30, 40, 50 ]
```

<br>

###### filter

배열의 각 항목을 참조하여 `조건을 주었을 경우 참인 항목을 반환`

```javascript
const numberList = [ 1, 2, 3, 4, 5];
numberList.filter((num) => {
  return num % 2 === 0;
});
// [ 2, 4 ]
```

<br>

###### forEach

배열의 크기 만큼 `callback 함수는 실행 되지만 반환 값은 없다`

```javascript
const numberList = [ 1, 2, 3, 4, 5];
numberList.filter((num) => {
  console.log(num);
});
```

<br>

###### push

배열의 마지막에 `값 추가`

```javascript
const numberList = [ 1, 2, 3, 4, 5];
numberList.push(6);
// [ 1, 2, 3, 4, 5, 6 ]
```

<br>

###### pop

배열의 마지막에 `값 제거`

```javascript
const numberList = [ 1, 2, 3, 4, 5];
numberList.pop();
// [ 1, 2, 3, 4 ]
```

<br>

###### unshift

배열의 앞 부분에 `값 추가`

```javascript
const numberList = [ 1, 2, 3, 4, 5];
numberList.unshift(0);
// [ 0, 1, 2, 3, 4, 5 ]
```

<br>

###### shift

배열의 앞 부분의 `값 삭제`

```javascript
const numberList = [ 1, 2, 3, 4, 5];
numberList.shift();
// [ 2, 3, 4, 5 ]
```

<br>

###### sort

배열을 유니코드 순서로 `정렬`

```javascript
const numberList = [ 'b', 5, 2, 3, 4, 1, 'a' ];
numberList.sort();
// [ 1, 2, 3, 4, 5, "a", "b" ]
```

<br>

###### join

매개변수를 참조하여 stirng 으로 반환

```javascript
const numberList = [ 1, 2, 3, 4, 5];
numberList.join('더하기');
// "1더하기2더하기3더하기4더하기5"
```

<br>

###### toString

배열 값들을 string으로 반환

```javascript
const numberList = [ 1, 2, 3, 4, 5];
numberList.toString();
// "1,2,3,4,5"
```

<br>

###### splice

배열의 매개변수 `1번째꺼 기준`, 매개변수 `2째 만큼` 가져온다. 참조변수 `데이터 손실`

```javascript
const numberList = [ 1, 2, 3, 4, 5];
const getData = numberList.splice(2,2);
// getData = [ 4, 5 ]
// numberList = [ 1, 2, 3]
```

<br>

###### slice

배열의 매개변수 `1번째꺼 기준`, 매개변수 2째 `자리까지` 가져온다. 참조변수 `데이터 유지`

```javascript
const numberList = [ 1, 2, 3, 4, 5];
const getData = numberList.splice(0,2);
// getData = [ 1, 2, 3 ]
// numberList = [ 1, 2, 3, 4, 5]
```

<br>