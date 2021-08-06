---
title:  WARNING NOTE getNode()
date: "2020-03-16"
tags: [warning]
thumbnail : ./getNodeImage.png
---



# Warning

React-native 0.62 버전으로 업데이트를 진행되면서 getNode() 코드가 사용되지 않게 되었다. 하지만 0.62 이전 버전을 기준으로 작성 된 패키지 라이브러리들은 해당 부분을 반영하여 수정이 되어야 하지만 그렇지 않을경우 위와 같이 Warning이 출력이 된다.



```
//react-native-scrollble-tab-view/index.js

goToPage(pageNumber) {
    if (Platform.OS === 'ios') {
      const offset = pageNumber * this.state.containerWidth;
      if (this.scrollView) {
        this.scrollView.getNode().scrollTo({x: offset, y: 0, animated: !this.props.scrollWithoutAnimation, });
      }
    } else {
      if (this.scrollView) {
        if (this.props.scrollWithoutAnimation) {
          this.scrollView.getNode().setPageWithoutAnimation(pageNumber);
        } else {
          this.scrollView.getNode().setPage(pageNumber);
        }
      }
    }
```

내가 사용하는 라이브러리를 열어보니 이렇게 사용되고 있었다. 해당 부분을 지우면 문제를 해결을 할 수 있다.

https://reactnative.dev/blog/2020/03/26/version-0.62

```
App.js
import  {  LogBox  }  from  "react-native" ;
LogBox.ignoreLogs(['getNode()']);
```

LogBox를 사용하여 해당 라이브러리가 업데이트 될 때까지 임시로 Warning 출력을 막는 방법도 있다.



### 2020-03-17 추가

Git master merged 가 되었지만 배포가 되지 않은 상태..