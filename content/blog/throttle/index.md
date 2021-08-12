---
title: React 최적화 - throttle
date: "2021-07-04"
tags: [최적화]
thumbnail : 


---



# Browser resize 이벤트

```javascript
useEffect(()=>{
        const handleReSize = () => {
            console.log('브라우저 높이 = ', window.innerHeight)
            if( number ){
                let browserHeight = window.innerHeight;
                //브라우저 높이

                const countOfHeight = (browserHeight - 80) / 130 >> 0;
                //브라우저 높이기준 나타낼 수 있는 개수

                let heightSize = number * 130;
                //폴더의 위치 * 폴더 크기 = 총 길이
            
                let xCnt = 0;
                //바탕화면 위치 x - 좌표
                let yCnt = 0;
                //바탕화면 위치 y - 좌표

                if(countOfHeight){
                    while(heightSize >= 130 * countOfHeight){
                      xCnt++;
                      heightSize = heightSize - (130 * countOfHeight);
                    };
              
                    while ( heightSize >= 130 ){
                      yCnt++;
                
                      if ( countOfHeight === yCnt ){
                        yCnt = 0;
                        xCnt = xCnt + 1;
                      };
                
                      heightSize = heightSize - 130;
                    }
                }
                setPosition({xCnt, yCnt})
            }
        };

        handleReSize();
        //초기 화면 사이즈 세팅

        window.addEventListener("resize", handleReSize);
        // Dom View 상태변경에 대한 이벤트 추가

        return () => window.removeEventListener("resize", handleReSize);
        // removeEventListener 이벤트 삭제
    },[]);
```

브라우저의 화면에 따른 UI에 있는 아이템들이 동적으로 움직이게 작성하였다.



`dispaly : flex` 로 같은 기능을 구현을 할 수 있지만 `react-Rnd` 를 사용하면서 <br/> `css !important , <Tag>`에 직접적으로 넣어주어도 사용을 할 수 없어 직접 기능을 구현해보았다.



<br/><br/>

# console.log(window.innerHeight)

![](https://images.velog.io/images/app235/post/1d42736e-ece3-4e82-aef2-7180a76999bd/%E1%84%8C%E1%85%A5%E1%86%AB.gif)

사용자 인터페이스 이벤트 중 `resize` 를 이용하여 Browser 창 크기가 변했을 때 아이템들의 좌표가 수정이 되도록 구현을 해보았다.



그런데 현재는 3개의 아이템 모두에게 똑같이 `resize` 이벤트가 발생하여 성능적으로 문제가 있었다.

`resize event 발생 => (item개수 * item 좌표등록 함수) * resize 이벤트`



<br/><br/>

# { throttle } from lodash

```javascript
import { throttle } from lodash;

useEffect(()=>{
  ...
    window.addEventListener("resize", throttle(handleReSize, 300));
    // Dom View 상태변경에 대한 이벤트 추가

    return () => window.removeEventListener("resize", throttle(handleReSize, 300));
    // removeEventListener 이벤트 삭제
},[]);
```

성능 개선을 위한 `throttle , debounce`에 대해서 알게 되었다.



`Throttle` :  입력 중 설정 시간이 지나면 출력을 한다.

`Debounce` : 이벤트가 멈추고 설정 시간이 지났을 때 호출, 하지만 설정 시간이 지나기전에 다시 호출이 된다면 호출이 되지 않는다.



`resize` 이벤트는 브라우저 크기가 변하는 도중에 이벤트가 발생을 해야하니 `Throttle`을 사용하여 개선을 해보았다.

![](https://images.velog.io/images/app235/post/58c4e2dd-69a1-4f32-985a-5573811da580/%E1%84%92%E1%85%AE.gif)

`throttle`을 적용 후 정말 많은 이벤트가 줄어 들었다!!!! 이 함수만 사용해도 성능을 크게 올릴 수 있다.

하지만 `resize` 이벤트가 발생할 때 마다 좌표등록 함수가 각각 발생하는 문제에 대해서 개선이 필요해 보인다.

