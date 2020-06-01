---
title:  "CMS 구축해보기 ver.라즈베리파이"
excerpt: "라즈베리파이에 CMS를 구축해보자......"

---


오늘은 지금까지 이용한 라즈베리파이에 CMS를 구출해보려고 합니다. 그럼 시작하겠습니다.

# CMS란 무엇인가?
우선 CMS가 무엇인지에 대해서 설명을 하곘습니다. CMS는 Contents Management System의 약자로, 웹의 콘텐츠들을 관리하는 시스템이다. 
평버한 CMS시스템은 라즈베리파이에서 실행하기에 무리가 있어 'batflat'이라는 조금 가벼운 CMS를 준비했다.


# batflat 세팅하기
root 권한을 가지고 아래 명령어로 php7.3을 설치하자.

```
apt install software-properties-common
apt update
apt install php7.3-fpm php7.3-common php7.3-mbstring php7.3-xmlrpc php7.3-sqlite3 php7.3-soap php7.3-gd php7.3-xml php7.3-cli php7.3-curl php7.3-zip
```

나는 도메인을 myblog.com이라고 정했기에 이를 세팅하겠다. 아래 명령어를 이용하자.

```
cd /etc/nginx/sites-available
vim myblog.com
cd /etc/nginx/sites-enabled
ln -s /etc/nginx/sites-available/myblog.com myblog.com
nginx -t
service nginx restart
```

이제 본인의 경로에 알맞게 아래 세팅파일을 수정해서 세팅해주자.

```
server {
    listen 80;
    listen [::]:80;

    server_name myblog.com;

    root /home/pcy/html/blog;
    index index.php index.html index.htm;

    client_max_body_size 100M;

    autoindex off;

    location / {
        try_files $uri $uri/ @handler;
    }

    location  /admin {
        try_files $uri $uri/ /admin/index.php?$args;
    }

    location @handler {
        if (!-e $request_filename) { rewrite / /index.php last; }
        rewrite ^(.*.php)/ $1 last;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.3-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```

지금부터는 root계정이 아닌 user계정으로(나같은 경우는 pcy계정을 사용했다) 들어와서 아래와 같이 세팅해주자.

```
cd ~/html
wget https://github.com/sruupl/batflat/archive/master.zip
unzip master.zip
mv batflat-master blog 
cd blog
mkdir ./tmp
mkdir ./admin/tmp
chmod -R 777 ./uploads ./inc/data ./admin/tmp ./tmp
```

이제 로컬컴퓨터의 hosts 파일을 수정한 후 myblog.com에 접속하면 완료된 모습을 볼 수 있다. 

# 웹 페이지 세팅
지금 myblog.com에 들어가서 보는 화면은 기본적으로 설정 되어있는 화면이다. 이제 페이지를 설정해서 나만의 페이지로 만들자.
먼저 myblog.com/admin 에 들어가자. 로그인 화면이 나올텐데 초기 아이디와 비밀호는 admin/admin 이다. 

![image](https://user-images.githubusercontent.com/48200520/83408604-d9b24f00-a44d-11ea-83ef-7a074d8f017d.png)

성공했다면 이러한 화면이 보일 것이다. 이곳에서 내 페이지를 수정 할 수 있고, 글들을 포스팅 할 수도 있다. 

![image](https://user-images.githubusercontent.com/48200520/83409590-acff3700-a44f-11ea-85c0-c49038b8d07a.png)

![image](https://user-images.githubusercontent.com/48200520/83409639-c2746100-a44f-11ea-9d5f-7a41f159ceb7.png)

나 같은 경우는 기존에 git hub블로그에 작성했던 글들을 가져와서 포스팅 해 보았다. 하지만 md형식으로 글들이 작성 되어 있어서 내가 원하는데로
포스팅 되지는 않았다. 오늘 목표는 단순 포스팅 이였기에 이 글들은 차후 수정할 것이다. 

이렇게 오늘 CMS세팅하기 ver.라즈베리파이는 끝났다. 나중에 이글을 따라하는 모든 사람들은 원하는 만큼 잘 성공했으면 좋겠다. 



