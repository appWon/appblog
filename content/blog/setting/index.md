---
title: react + webpack5 + babel7 세팅
date: "2021-06-14"
tags: [babel, webpack]
thumbnail : '../../assets/rwb.png'
---



# 개발환경구축

<hr>

```
npm init -y
npm i react react-dom
//개발에만 사용하도록 -D 옵션 추가
```

웹 프론트 개발환경을 구축하기 위해서 react, react-dom을 설치하고 개발을 진행하면서 사용한 ` js,css파일 등을 하나의 파일로 만들어 주는 모듈 번들러` 이다.



```javascript
//src/index.js
import reactDom from 'react-dom';
import App from './App';

reactDom.render(<App/>,document.getElementById('root'))
```



```jsx
//src/app.js
const App = () => {
    return (
        <div>App 페이지</div>
    )
}

export default App;
```



```
//public/index.html
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <div id='root'></div>
  <script src='./dist/main.js'></script>
</body>
</html>
```

<br/><br/><br/>

## webpack

<hr>

```
npm i -D webpack webpack-cli
```

```javascript
//webpack.config.js
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
    mode: 'development',
    entry: './src/index.js',
    output: {
        filename: 'main.js',
        path: path.resolve(__dirname + '/public/dist/')
    },
    module: {
        rules: [
            {
                test: /\.(js|jsx)$/,
                exclude: /nodeModules/,
                loader: 'babel-loader',
            }
        ]
    },
    resolve: {
        extensions: ['.js', '.jsx']
    },
    plugins: [
		new HtmlWebpackPlugin({
			template: './public/index.html'
		})
	]
}
```

`Webpack.config.js` 에서 webpack의 설정을 다룬다. entry를 기준으로 import 된 파일을 들어가고 또 들어가서 하나의 파일로 묶어지게 되고, output에서 설정된 경로에 main.js 이라는 파일이 생성이 된다.

그리고 index.html 파일에서 main.js파일을 불러서 사용면 된다.

이렇게 세팅된 파일들을 npx webpack을 확인해보면

```
You may need an appropriate loader to handle this file type, currently no loaders are configured to process this file. See https://webpack.js.org/concepts#loaders
| import App from './App';
| 
> reactDom.render(<App/>,document.getElementById('root'))
```

jsx 문법으로 작성된 App파일을 처리하기 위해서는 babel-load를 설치와 설치된 babel-load를 사용할 수 있게 webpack을 세팅해야한다.

<br/>

## babel

<hr>

공식문서에는 babel은 자바스크립트 컴파일러라고 하며, es2015코드를 이전 버전의 자바스크립트로 변환하는데 사용하는 도구라고 한다.

```
npm i -D babel-loader
```

```javascript
//webpack.config.js
module.exports = {
	...
    module:{
        rules: [
            {
                test: /\.(js|jsx)$/,
                exclude: /nodeModules/,
                loader: 'babel-loader',
            }
        ]
    }
}
```

이렇게 세팅 후 다시 npx webpack 명령어를 입력 후 확인을 해본다

![](https://images.velog.io/images/app235/post/7640b94f-e225-47e8-b2aa-efb35f1535f9/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-07-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%204.18.06.png)

jsx 문법을 인식을 할 수 없어 error가 발생하였다. 에러 표시에 따라 @babel/preset-react를 설치 후 위와 같이webpack.config.js에 설정하거나, .babelrc 파일을 생성하여 세팅을 해주면 bable이 자동으로 설정이 된다.



##### @babel/preset-react

Jsx 문법으로 작성된 코드를  `React.CreateElement`  문법으로 변환시켜준다.

```
npm i -D @babel/preset-react
```

```
//webpack.config.js
module.exports = {
...
  {
    test: /\.(js|jsx)$/,
    exclude: /nodeModules/,
    loader: 'babel-loader',
    options: {
      presets: ['@babel/preset-react']
    }
  }
...
}

or

//.babelrc (webpack.config.js에서 options 부분 삭제)
{
    "presets": [
        ["@babel/preset-react"]
    ]
}
```



##### @babel/preset-env

바벨에서 `es6 코드를 변환`하기 위해서 사용이 된다.

```
npm i -D @babel/preset-env
```

```
//.babelrc
{
    "presets": [
        ["@babel/preset-react"],
        [
        	"@babel/preset-env",
	        {
          	    "modules": false,
	        	"targets": "> 0.25%, not dead"
	        }
        ]
    ]
}

or

//package.json
{
  "private": true,
  "dependencies": {
		....
  },
  "browserslist": [
		"> 0.25%",
		"not dead"
  ]
}
```

`"target: "> 0.25%, not dead"`  옵션을 보면 대상을 시장 점유율 0.25% AND 업데이트가 계속 되는 브라우저를 대상으로 한다

> modules: 성능 최적화를 위한 Tree shaking의 목적으로 false 설정을 하여야 import, export 문법이 require,modules.exports로 바뀌지 않는다.

<br/><br/>

<br/>

### Webpack-dev-server 설정

<hr>

cors error: 프록시  설정 https://joshua1988.github.io/webpack-guide/devtools/webpack-dev-server.html#webpack-dev-server

```
//package.json
{
	...
	"scripts": {
		start: "webpack serve"
	}
	...
}
```

```
//webpack.config.json
module.exports = {
...
  devServer: {
    port: 3000,
...
}
```

<br/><br/>

### plugins

<hr>

```
npm i -D html-webpack-plugin
```

번들화된 파일을 index.html에서 따로 세팅 하지 않아도 적용이 된다.

```
 npm i -D webpack-bundle-analyzer
```

웹팩으로 번들링된 모듈을 시각적으로 나타내준다.

```
//webpack.config.json
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.export = {
	...
	plugins: [
		new HtmlWebpackPlugin({
			template: './public/index.html'
		})
	]
	...
}
```

<br/>



>참고
>
>https://ui.toast.com/weekly-pick/ko_20180910
>
>https://tech.kakao.com/2020/12/01/frontend-growth-02/