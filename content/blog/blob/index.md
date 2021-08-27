---
title: "[ blob ]"
date: "2021-08-28"
tags: [js]
thumbnail : ../../assets/js.png


---

<br>

websocket 프로젝트를 하면서 onmessage를 통해 `blob`이라는 데이터를 받게 되었고, Blob에 대해서 짧게나마 정리해보려고 한다.

<br>

#### blob : Binary Large Objects

<hr>

이 말을 해석하기 위해서는 우선 `binary` 가 무엇인지 알아야 할거 같다.

Binary는 0과 1만 사용하는 2진법이다. 그리고 0, 1만 사용하는 컴퓨터에게 있어서는 가장 중요한 계념이다.

그렇다면 blob에 대해서 추측하면 0,1로 구성된 binary 타입으로 저장하는 큰 오브젝트로 생각할 수 있을거 같다.

##### 용도

blob는 `그림, 오디오, 멀티미디어` 에 사용이 된다고 하였지만 이번에 websocket를 이용하면서 blob 데이터를 받게 되어보니 `실시간으로 많은 문자 데이터` 를 보낼 때에도 사용하는 거 같다.

<br>

##### Blob 객체

![](https://images.velog.io/images/app235/post/df0bc932-60af-410e-a30f-383a269fff3c/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-08-27%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%207.22.10.png)

<br>

websocket으로 받은 데이터이다. Blob 객체는 `size, type` 속성으로 되어 있다.

`size` 는 `byte` 단위 크기를 가지고 있으며, 지금 blob 객체는 약 1Kb



##### FileReader

이제 이렇게 받은 데이터를 사람들이 이해할 수 있는 데이터로 바꿔주는 작업이 필요할거 같다. 이럴 때는 `fileReader` 를 사용하여서 변화를 주어야 한다.

>FileReader.readAsText() : `텍스트` 형식의 파일을 읽는다.
>
>그외도, readAsArrayBuffer, readAsbinaryString,readAsDataURL 가 있다.
>
>> readAsText( blob [, encoding ]);
>>
>> encoding Optional : default UTF-8
>
><br>
>
>FileReader.onload() : 파일리더는 `비동기` 로 실행이 되기 때문에 unload 함수를 이용하여야한다.



<br>



```javasc
  socket.onmessage = ({ data }: any) => {
    const reader = new FileReader();

    reader.readAsText(data);
    reader.onload = ({ target }: any) => {
      const result = target.result;
      console.log(JSON.parse(result));
    };
  };
```

