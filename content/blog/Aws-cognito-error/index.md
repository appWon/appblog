---
title: "[ aws Cognito-identity error 400 ]"
date: "2021-10-07"
tags: [aws,cognito,identitym,error,400]
thumbnail : ../../assets/aws.png
---

<br>

<br>

![](https://images.velog.io/images/app235/post/20e6b2cd-aecc-437c-940b-29bdc05678d3/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-10-07%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2012.45.40.png)

<br>

<br>

Cognito의 userPool, identity 을 프로젝트에 새로 만들고 수정을 여러번하면서 발생이 되었다.

위의 에러가 발생하고 나서는 권한을 통한 데이터 조작이 불가능하였다. 혼자서 원인을 못 찾아 구글링을 통해서 알게되었다. 

<br>

<br>

![](https://images.velog.io/images/app235/post/ec39b60e-8b6e-4aa2-b188-099bcdf65f7c/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-10-07%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2012.48.58.png)

> 원인은 .. 코그니토 자격증명의 ID와 자격증명에 설정한 역할(IAM role) 의 신뢰 데이터 설정이 다르기 때문에 위와 같은 에러가 발생하였다.

<br>

<br>

![](https://images.velog.io/images/app235/post/7f18ade2-3858-414d-828c-0767d61db797/image.png)

> 가장 먼저!! 코그니토 자격증명 풀 설정하는 화면에서 자격 증명 풀 ID를 기억하자!!!
>
> 그리고 자신이 설정한 인증된 역할(IAM role) 설정 화면으로 이동하자



![](https://images.velog.io/images/app235/post/e10a812c-0804-4cd0-bfa5-933c3ff55d1c/image.png)

> 위 페이지에서 신뢰 관계 편집버튼을 누르면 수정하는 화면이 나올 것이다.
>
> ```
> {
>   "Version": "2012-10-17",
>   "Statement": [
>     {
>       "Effect": "Allow",
>       "Principal": {
>         "Federated": "cognito-identity.amazonaws.com"
>       },
>       "Action": "sts:AssumeRoleWithWebIdentity",
>       "Condition": {
>         "StringEquals": {
>           "cognito-identity.amazonaws.com:aud": "여기에 자격증명 ID 설정"
>         },
>         "ForAnyValue:StringLike": {
>           "cognito-identity.amazonaws.com:amr": "authenticated"
>         }
>       }
>     }
>   ]
> }
> ```
>
> "cognito-identity.amazonaws.com:aud" 이 부분에 자신의 코그니토 자격증명 Id로 변경시켜주면 에러를 해결할 수 있을 것이다.

