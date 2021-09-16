---
title: "[ aws 웹 앱 만들기 (Serverless) ]"
date: "2021-09-15"
tags: [aws]
thumbnail : ../../assets/aws.png
---

<br>

개발을 진행을 하다보면 프론트엔드도 백엔드의 지식과 개념을 알아야한다. 하지만 사용하는 기술과 언어가 많이 차이가 나면서 런닝커브가 짧지 않기 때문에 단기간에 프로젝트를 구성하기가 쉽지가 않다.

그래서 프론트 개발자가 쉽게 백엔드 프로세스를 알고 쉽게 접근하기 위해서  aws `serverlesss`를 배우게 되었다.

aws serverles 설명문에서는 `서버를 고려하지 않고 앱과 서비스를 구축 및 실행`할 수 있다고 설명하고 있다. 즉 백 엔드 서버를 실행하기 위한 서버 프로비저닝, 관리를 AWS 에서 모두 맡아서 진행하겠다. 라고 나와있다.

<img src="https://images.velog.io/images/app235/post/2636885f-2926-4115-87d7-823760cbdea8/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-09-15%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%208.23.00.png" style='width:100%;'/>

백엔드서버를 AWS로 도식화로 만들어 보면 위와 같이 나타낼수 있고, 아래의 설명과 같이 백엔드 서버를 aws serverless 할 수 있다.

> - AWS S3(Simple Cloud Storage) : 온라인 스토리지로써 유저가 서버에 동영상, 이미지, 문서 같은 비교적 용량인 큰 파일을 저장하고, 검색을 기능을 가지고 있는 AWS의 스토리지 서비스이다.
>
>  
>
> - AWS COGNITO : 웹 , 모바일에서 로그인, 가입, 인증, 복구에 사용하며, 아이뒤와 비밀번호를 입력한 로그인 뿐만 아니라 소셜 로그인도 할 수 있다.
>
>   1. 사용자 풀 (User pool ): 인증(본인 확인)을 위한 pool 이다. 아이뒤, 비밀번호를 통한 로그인을 하거나, SNS 로그인 연동을 할 수 있다. 그리고 로그인을 했을 경우 로그인한 유저에 대한 자격 증명 풀을 프로비저닝한다.
>
>   2. 자격 증명 풀 (Identity Pool) : AWS 서비스에 접근할 수 있는 권한을 준다.
>
>      <img src='https://images.velog.io/images/app235/post/76190979-e1c4-44f8-b40a-b3497c32bc2a/image.png' style='width=100%;'/>
>
> - AWS Gateway : 백 엔드의 엔드포인트의 역할, AWS Lamda 함수와 같은 AWS 서비스 접근할 수 API를 생성할 수있다.
>
>   1. 권한 부여 및 접근 제어
>   2. 성능 모니터링  [AWS X-Ray](https://docs.aws.amazon.com/ko_kr/apigateway/latest/developerguide/apigateway-xray.html)
>
>    [더 보기](https://docs.aws.amazon.com/ko_kr/apigateway/latest/developerguide/welcome.html)
>
>   
>
> - Lambda : AWS 람다 함수라고도 하며, 일박적으로 함수를 작성하고 실행하는 개념과 같다. 하지만 우리가 백엔드 함수를 구현을 한다면 서버 프로비저닝, 관리를 해야 하지만 이 과정들을 모두 AWS에서 맡아서 하기 때문에 Lambda 작성 후 호출만 하면 실행할 수 있다.
>
>   1. 익스텐션을 사용하여 모니터링, 관찰, 보안 및 거버넌스 도구와 함수를 통합할 수 있다.
>   2. 람다 함수에서 `실행 역할` 로 권한을 주어 AWS 서비스에 접근을 할 수 있다.
>
>   [더 보기](https://docs.aws.amazon.com/ko_kr/lambda/latest/dg/gettingstarted-features.html)
>
>   
>
> - DynamoDB : 비관계형 데이터 베이스이며, DB 테이블을 생성만하고 Auto Scaling 설정만 하면 쉽게 사용을 할 수 있는 DB이다.

