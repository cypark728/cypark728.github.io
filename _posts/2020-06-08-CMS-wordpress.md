---
title:  "CMS 구축해보기 ver.wordpress"
excerpt: "라즈베리파이에 CMS를 구축해보자......"

---

오늘은 백업과 새로운 CMS인 wordpress를 사용할 것이다. 

# 백업
내가 이때까지 했던것들이 날아가는것은 끔찍한 일이다. 그런 일이 발생하지 않도록 백업을
하자. 백업은 중요한 것이다. 

먼저 super user로 진행한다. 
백업용 디렉토리를 만든다. 

```
# mkdir /backup
# chmod 700 /backup
```
그리고 root 디렉토리에 sh파일을 만든다. 

```
# pwd
/root
# vi backup.sh
# chmod 700 backup.sh
```
![image](https://user-images.githubusercontent.com/48200520/84042700-5f02aa00-a9e0-11ea-940b-c39712bb2714.png)

이제 실행을 해보자
```
# ./backup.sh
ls -l /backup
```

백업을 주기적으로 하기 위해서 cron을 사용할 것이다. 매번 직접 백업을 하는것은
별로 좋은 방법이 아니다. 

```
# crontab -e
```
이 명령어를 입력하면 원하는 에디터를 선택하라고 하고, 마지막 줄에 아래와 같이 추가해준다 
```
0 4 * * * /root/backup.sh 1>dev/null 2>dev/null
```

# Wordpress

Wordpress는 세계에서 가장 유명한 CMS이다. db는 그전에 설정해 놓은 userdb를 사용할 것이다. 
/home/jinu/html 에 다운받고 압축을 풀어준다. 
```
$ wget https://ko.wordpress.org/latest-ko_KR.tar.gz
$ tar -xzvf latest-ko_KR.tar.gz
```

그후 jinu.com/wordpress 에 접속하면 db정보를 입력하는 창이 나온다.
그곳에 알맞은 정보를 입력해주고, 그 후에 나온 wp-config.php를 복사하여
/home/jinu/html/wordpress 에 붙여넣어준다. 

wp를 관리하기 위한 몇가지 설정을 해 줘야 한다. 
이 설정은 super user로 진행한다. 

```
# chgrp -R www-data ~/html/wordpress/wp-content
# chmod -R 775 ~/html/wordpress/wp-content
```

그후 wp-config.php 파일 맨 마지막에 아래와 같이 추가해주면 완성이다.
```
define('FS_METHOD', 'direct);
```



