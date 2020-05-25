---
title:  "가상 호스트 세팅하기"
excerpt: "가상 호스트를 세팅해보자..."

---

오늘은 가상호스트를 세팅해볼 것이다. 

# 유저 추가하기
오늘은 2개의 가상 호스트를 만들 것이기 때문에 두개의 유저를 만들것이다. 
```
useradd -m <유저이름>
passwd <유저이름> 
```
명령어를 사용해서 유저를 만들어 주자.

![image](https://user-images.githubusercontent.com/48200520/82796922-43ac8080-9eb1-11ea-9fef-664630a261ef.png)

유저가 생성 되었다!!

# 세팅파일 생성

이제 /etc/nginx/sites-available 에 가서 세팅파일을 생성해 주자.
```
server {
        listen 80;
        listen [::]:80;

        server_name pcy.com;

        root /home/pcy/html;
        index index.html;
}
```
세팅파일은 위 내용을 자신의 서버 이름과 주소에 맞게 수정하여 만들어 준다. 

이후 /etc/nginx/sites-enabled 에 /etc/nginx/sites-available/pcy.com pcy.com 링크를 만들어 준다

다 완료되었으면 service nginx restart 해주자.

# 사이트 열기
이제는 아까 만든 유저인 pcy로 접속을 해보자.
pcy로 접속하면 그 안에 아무것도 없을테니 html폴더를 만들고 그 안에 index.html 파일을 만들자
그 후 브라우저에 pcy.com을 들어가면

![image](https://user-images.githubusercontent.com/48200520/82810858-76af3e00-9eca-11ea-829a-e24cfb0c2b33.png)

이렇게 나올것이다! 그러면 정상적으로 호스팅 된 것이다. 

이제는 git hub에 있는 템플릿중 몇개를 호스팅 해볼 것이다. 
나는 ( https://github.com/The-WebOps-Club/personal-website-template ) 를 사용했다. 

저 링크를 fork 해주고 git clone 을 해주면 이렇게 된다.

![image](https://user-images.githubusercontent.com/48200520/82811375-93984100-9ecb-11ea-9efb-82af2c860519.png)

이후 http://pcy.com/personal-website-template/ 에 접속하면 이렇게 보인다. 

![image](https://user-images.githubusercontent.com/48200520/82811446-c2161c00-9ecb-11ea-92ae-915e9a8849e7.png)

이러면 성공 한 것이다. 

# 웹 사이트 수정하기


