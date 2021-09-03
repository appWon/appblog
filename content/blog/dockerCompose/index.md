---
title: "[ docker-compose ]"
date: "2021-08-06"
tags: [docker]
thumbnail : ../../assets/compose.png
---

<br><br>

## docker-compose.yml

Compose는 다중 컨테이너를 생성 및 실행하기 위한 도구입니다.

```shell
//실행 명령어
docker-compose up
```



```
//docker-compose.yml
version: '3'
services:
  web:
    build: ./frontend
    volumes:
      - ./frontend:/home/node/app
    ports:
      - "3000:3000"
  server:
    build: ./backend
    volumes:
    	- ./backend:/usr/src/app
    ports:
      - "8000:8000"
  db:
    build: ./database
    ports: "3306:3306"
    environment:
      DB_HOST: mysql
      DB_USER: root
      DB_PASSWORD: secret
      DB_SCHEMA: todos
```

<br>

> build : Dockerfile 위치 경로
>
> volumes : 마운트할 호스트 컴퓨터 폴더 : 컨테이너 내 마운트 위치
>
> port : 외부 포트 : 내부 포트
>
> environment : 설정을 위한 변수

<br>

volume  :  컨테이가 종료 or 재시작이 될 경우 `데이터가 사라진다`. 호스트의 폴더가 도커의 폴더에 마운트가 되어 컨테이너가 종료 or 재시작이 되더라도 데이터들은 호스트 폴더에 저장이 되어 있기 때문에 시스템을 유지할 수 있다.

<br>

port : 접속 포트를 변경할 수 있다. 1234 : 8000 로 설정을 하면 호스트 컴퓨터에서 1234 접속하면 컨테이너에서는 8000으로 접속을 할 수있다.

<br>

<br>
