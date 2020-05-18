---
title:  "내 웹서버 만들기 ver.라즈베리파이"
excerpt: "라즈베리파이에 웹 서버를 세팅해보자"

---

이전 글에서는 닷홈이라는 곳을 이용하여 호스팅을 받아
무료로 간단한 나만의 웹 사이트를 만들어 보았다. 이번에는
라즈베리파이에 웹 서비스를 한번 세팅해보자!

# 1. SD카드에 라즈비안 설치하기
먼저 라즈베리파이 공식 홈페이지( https://www.raspberrypi.org/ ) 에
들어가서 라즈비안을 설치 하자.

![image](https://user-images.githubusercontent.com/48200520/82211814-6e945300-994c-11ea-9426-fb59d40689e9.png)

우리는 위 3개중에 몇몇 소프트웨어가 미리 설치되어 있는 Raspbian Buster with desktop and recommended software 를 
사용할 것이다. 

이후 Raspberry Pi Imaer도 자신의 os에 맞게 설치를 하자

![image](https://user-images.githubusercontent.com/48200520/82232987-4b789c00-996a-11ea-8425-4e29add6b148.png)

이제 Operating System 에는 좀전에 설치한 라즈비안 이미지를 두고, 라즈비안 이미지를 설치할 SD card를 선택하고 
설치를 한다. 

## Wi-Fi 설정 및 ssh 설정
sd card의 root에 ssh 라는 이름을 가진 빈 파일을 만든다. 윈도우의 경우 텍스트 파일을 만든 후 확장자를 삭제하면 된다. 
Wi-Fi설정을 위해서 wpa_supplicant.conf라는 파일을 만든후 아래와 같이 입력한다. 

![image](https://user-images.githubusercontent.com/48200520/82233319-ce015b80-996a-11ea-94f1-faf3bc2ac94e.png)

이 후 sd card를 라즈베리파이에 장착 후 부팅을 해준다. 

# 2. 라즈베리 파이에 접속하기
이제는 라즈베리 파이를 부팅시킨 후 라즈베리파이에 접속해보자.
먼저 라즈베리파이가 연결되어 있는 공유기와 같은 공유기로 내 컴퓨터를 연결한 후 power shell을 이용하여 
ping raspberrypi.local 명령어를 사용해준다. 

### 첫번째 오류
원활하게 핑이 보내지면 그 때 얻은 ip주소를 이용해서 ssh로 접속 할 수 있다. 하지만 나는 원활하게 ping 이 보내지지 않았다.

![image](https://user-images.githubusercontent.com/48200520/82233711-61d32780-996b-11ea-8ff8-27a4b92d66c8.png)

이와 같은 오류가 발생 하였다. 보통은 위에서 작성한 wpa_supplicant.conf 파일에 오타가 있어서 연결이 되지 않는 경우들이다. 
하지만 나는 어째서인지 몇번이나 파일을 확인해봐도 틀린곳이 있지 않았기에 유선 연결을 시도하였다. 유선 연결을 하면서 라즈베리파이에
키보드와 모니터를 장착해 주었다. 공유기가 유무선용 이였기에 먼저 유선으로 네트워크에 연결을 해주고 이후 무선 연결로 바꿔주었다. 

![image](https://user-images.githubusercontent.com/48200520/82234137-f9d11100-996b-11ea-928e-af3289967cb8.png)

직접 연결하여서 192.168.100.20 이라는 ip주소를 알아내었다. 첫번째 오류를 해결하였다. 

이제 putty나 shell등을 이용해서 알아낸 ip의 ssh에 접속할 수 있다. 여기서 username은 pi, password는 raspberry로 기본설정되어있다. 
하지만 모니터와 키보드를 사용해서 직접연결할때 비밀번호를 변경하라고 하여서 나는 기존에 변경한 비밀변호로 접속 하였다. 

# 3. 웹 서버 세팅하기
웹 서버를 세팅할때 nginx 또는 Apache 둘중 하나를 자주 사용한다. 이번에 나는 nginx를 사용할 것이다. 
nginx를 설치하기 전에 먼저 "sudo su - "명령어를 사용하여 super user로 root에 들어간다. 그 후 "apt-get update"로 라즈베리 파이 내에 있는 
패키지들을 최신 버전으로 업데이를 해준 후 "apt-get install nginx"를 사용해서 nginx를 설치해 준다. 

### 두번째 오류
나는 여기서 "dpkg was interrupted, you must manually run 'dpkg --configure -a' to correct the problem." 라는 오류가 나왔다. 

![image](https://user-images.githubusercontent.com/48200520/82235110-436e2b80-996d-11ea-8f1c-c2ae20667468.png)

이때는 "rm /var/lib/dpkg/updates/*" 명령어를 사용해서 updates 폴더 안에 있는것들을 삭제해주고 다시 업데이트 및 nginx를 설치 해주면 된다. 
( https://blog.naver.com/dbreoqja/221206207705 사이트 참조) 두번째 오류를 해결하였다. 

# 4. 웹 페이지 작성하기
이제 "service nginx start"명령어로 nginx를 시작하자. 이후 "vi /var/www/html/index.html" 명령어를 사용하여 index.html을 작성하자.
그 후 저장하고 종료한 후 라즈베리파이의 ip주소를 웹 브라우저 주소창에 입력한후 접속해서 결과를 확인한다. 

![image](https://user-images.githubusercontent.com/48200520/82236609-4e29c000-996f-11ea-92dc-cb1acc816341.png)

잘 완료된 것을 볼 수 있다. 

# 5. 결론
이제 호스팅을 따로 받아서 하는 것이 아닌 직접 웹 서버를 세팅해서 웹 페이지를 만들어 보았다. 중간중간 많은 우역곡절들이 있었지만
많은 오류들을 통해서 더 많은 것들을 배울 수 있었던 기회가 되었다. 이제는 내가 직접 세팅한 웹 서버를 통해서 더 많은 일들을 할 수 
있을 것이다. 


