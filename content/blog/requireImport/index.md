---
title: require vs import ???
date: "2020-03-14"
tags: [es6]
thumbnail : ./typography.png

---



자바스크립트를 이용하여 프로젝트를 작성하다가 파일이나 패키지를 불러올 때 import, require를 접할 수 있다.

require는 CommonJs의 키워드이고, import는 es6에서 사용되고 있는 키워드이기 때문에 es6가 지원하지 않는 브라우저에서는 babel 같은 트랜스파일러를 이용하여 해결을 할 수 있다.

## CommonJs

```
//가져오기
var A = require('./color')

//내보내기
module.export = A
```



## ES6

```
import A from './color'
import { red, yellow } from './color'

//내보내기
export default A
export { A }
```

이렇게만 보면 기능으로 차이가 없다고 생각할 수도 있지만 가장 큰 차이점은 최적화에 있다. require는 모듈의 모든 것을 가져오게 되지만 import의 **import { red, yellow } from './color' ** 모듈의 해당 부분은 프로덕션 빌드에서 webpack의 설정으로 필요 없는 것은 쉐이킹하여 최적화할 수 있다



참고자료: https://ui.toast.com/weekly-pick/ko_20180716