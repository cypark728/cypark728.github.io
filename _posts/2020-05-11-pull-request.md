---
title:  "pull request"
excerpt: "pull request를 시나리오를 통해 배우자..."

categories:
  - git
tags:
  - git
---

오늘은 한 시나리오를 가지고 실습을 할 것입니다. 만약 협업을 하는 팀원이 무언가를 수정했을때 이 것을 내 repository에도 업데이트 해야 합니다. 
이를 하는 방법을 오늘 실습하도록 하곘습니다. 

# 1.fork
먼저 팀원의 remoet repository를 포크합니다. 
그리고 포크한 remote repository를 로컬 저장소에 클론합니다. 
![image](https://user-images.githubusercontent.com/48200520/81566124-63ce4100-93d5-11ea-9121-5d26157d6b37.png)

# 2.remote
현재 연결되어 있는 remote repository는 팀원의 remote repository이다. 이제 로컬저장소와 내 remote repository를 연결해야 한다.
![image](https://user-images.githubusercontent.com/48200520/81566197-81030f80-93d5-11ea-8769-71ecf692548b.png)
이렇게 하면 origin 이라는 기존 remote repositiory와, abc라는 원본 remote repository가 연결된다. 

# 3.branch
branch를 하나 만들어 원본은 살려두고 새로운 branch에서 pull request를 보낸다. 

# 4. add,commit,push
작업이 완료된 후 다시 내 remote repository로 push 합니다. 

# 5. pull request
push후 내 remote repository에 Compare&pull request 라는 버튼이 생깁니다. 이 버튼을 클릭해서 pull request를 보냅니다. 

# 6. merge
이제 pull request 가 승락되고 원본에 merge가 되면 내 저장소에 pull 합니다.


