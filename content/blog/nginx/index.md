---
title: "[ nginx ]"
date: "2021-08-28"
tags: [nginx]
thumbnail : ../../assets/nginx.png

---

<br>

```
worker_processes 4;

events { 
    worker_connections 1024; 
}

http {
    server {
        listen 80;
        root  /usr/share/nginx/html;
    }
}
```

>worker_connections : 하나의 프로세스가 처리할 수 있는 최대 연결 수
>
>> 최대 동접자 수 = worker_processes * worker_connections
>
>root : 요청을  `/usr/share/nginx/html` 폴더로 매핑을 하게 된다.

