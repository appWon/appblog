---
title: 도커 명령어
date: "2021-08-05"
tags: [docker]
thumbnail : ../../assets/docker.png
---

<br><br>

## 도커 이미지

<hr>

##### 생성

```
docker build -t {이미지명} .
//Dockerfile을 사용하여 image 생성(파일 경로 기준)
```



##### 리스트

```
docker images
//이미지 리스트(전역)
```



##### 이미지만 다운

```
docker pull 이미지 이름
```



##### 삭제

```
docker rmi -f 이미지id
```



<br><br>

## 도커 컨테이너

<hr>

##### 생성

```
docker create {옵션} 이미지 이름
```



##### 리스트

```
docker ps
//실행 중인 컨테이너 리스트(전역)

docker ps -a
//생성된 전체 컨테이너 리스트(전역)
```



##### 시작

````
docker start 컨테이너 이름
//시작
docker restart 컨테이너 이름
//재시작
````



#### 정지

```
docker stop 컨네이너 이름
// 정지
docker stop $(docker ps -aq)
// 컨테이너 전체 정지
docker system prune -a
// 사용x 컨테이너, 이미지 전체 삭제
```



##### 삭제

```
docker rm 컨테이너 name
```



<br><br>

## docker-compose 실행

<hr>

```
docker-compose up
//docker-compose 파일 실행(파일 경로 기준)
```

