---
title : [Git] 
published : false
date : 
categories:
 - git
---





페이스북 이노베이션 랩에서 이고잉님의 '지옥에서 온 GIT' 수업에서 배운 것들을 정리한 게시물입니다



생활코딩 사이트 및 페이스ㅜ



유명한 분을 (!!) 만나볼 수 있어서 좋았고,

또 git 을 사용하고는 있지만 묻지도 따지지도 않고 주먹구구식으로 찾아보고 사용하고 있어서 

기본부터 다시 알아가고 싶어서 세미나에 참여하게 되었다



새로운 것들을 알 수 있었고 정말 유익...

사실 다른 약속이 있어서 목요일 세션을 참여하지 않으려고 했는데, 화요일 세션을 듣고 나니 정말 유익하고 좋은 기회라 목요일 약속 취소하고 (!!) 목요일 세션을 들으러 왔다



## source tree

cli 환경에서만 하다보니까 정확하게 가시화?하기 힘들다는 생각을 했는데 source tree로 확실하게 보니까 구조화 하기 좋았음!!



물론 cli 환경에서 처리하는 게 편한데, 결과를 보기에는 source tree 넘 조아



<http://hochulshin.com/git-revert-changes/>



토토이즈??



엑셀과 이미지 파일의 차이점도 찾아서 보는 프로그램?플러그인을 활용하면 다양한 직군에서 사용하기 좋은 git

허미...넘 좋네







## 새롭게 배운 점



- git reset --hard HEAD^
  - 지금 head 가 가리키고 있는 커밋의 내용을 삭제
- git reflog
  - 커밋 로그를 간결하게 다 보여줌
  - 좀더 자세하게 보고 싶으면 git log
- git에서 중요한 세가지 공간
  - .git 은 repository 모든 기록들을 담고 있는 공간
  - stage area는 논리적인 공간개념
  - 나머지는 파일들은 working directory 라고 부름
- 화살표 위를 누르면 방금 전에 썼던 명령어를 복사해서 붙여넣어줌 (오올...)
- HEAD
  - 포인터 처럼 커밋 지점을 가리키는?
- 각 노드들은 자신의 부모 정보를 담고 있어서 reset으로 자유롭게 이동 가능!
- cnt + ~ 하면 터미널 창 열림 (visual studio code)



## reset

- **흠 checkout 과 다른 점이 뭐지?!**
- reset ABCD : ABCD 커밋의 상태로 가자
- hard - 지금 선택한 이후 버전들의 commit을 초기화?
- soft - 시점을 이동하고 커밋하지 않은 상태로 파일을 남김
  - git reset --soft HEAD^
  - aHEAD^ : HEAD이전
  - HEAD~2 : HEAD 이전이전(?)
  - 숫자를 붙이면 이동하는 것 같음







## 소스트리에서 브랜치 더블클릭하면 해당 스냅샷으로!

- cli에서는 어떻게 하지?

  - git reset --hard[--soft] 커밋코드?앞자리 4개
  - git reflog 명령어를 실행하면 모든 로그?를 확인할 수 있음

- 원래상태로 돌아오려면 git checkout master

  
  
  