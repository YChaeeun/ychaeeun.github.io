## 공부

- reset 시점을 바꿈!

  - --hard : 저장소, stage, working dir 다 없어짐
  - --soft : 저장소에만 지우고 stage에는 올려놓음, 파일이 add 되어 있는 상태로 남아있음
  - --mixed : 저장소, stage에 있는 내용지움. working dir에는 남아있음
  - reset은 push하기 전까지만 가능해!! 다른 사람한테 공유하기 전까지만 reset을 사용할 수 있어

- revert는 되돌리기 (사실은 추가하기)

  - 수정하고 싶다면 새로운 버전을 추가로 만들어서 수정하는 수 밖에 없음
  - 0 +10 을 했는데 앗 10은 더하면 안됐었어 --> 그럼 -10 이라는 새로운 버전을 만들어서 0 +10 -10 원상태로 만드는 게 바로 revert
  - git revert C

- rebase

- github - ssh방식으로 연결하기[참고]([https://git-scm.com/book/ko/v2/Git-%EC%84%9C%EB%B2%84-SSH-%EA%B3%B5%EA%B0%9C%ED%82%A4-%EB%A7%8C%EB%93%A4%EA%B8%B0](https://git-scm.com/book/ko/v2/Git-서버-SSH-공개키-만들기))

  - ssh-keygen : 이 경로에 비밀번호를 저장해줄게! (/c/Users/maisy/.ssh/id_rsa)

  - 해당 경로로 가면 id_rsa라는 파일이 생김

  - .pub는 알려줘도 되지만, id_rsa는 절대절대 알려주면 안돼!! 

  - pub를 복사해서 깃헙에다가 올리면 됨 (파일이 안열릴경우 메모장으로 열기)

  - 리모트 레포의 통신방법을 ssh로 하고

    ```shell
    $ git remote add origin ~ 주소입력
    $ git push -u origin master
    ```

    - origin 리모트의 이름

    - master는 브랜치 이름

    - 즉 다른 브랜치 ex) feature를 적어주면 돼

      ```shell
      $ git push -u origin feature
      ```

    - 만약 다른 원격 저장소를 이용하고 싶다면 다른 remote 이름을 적어주면 됨

      ```shell
      $ git remote add origin2 ~ 주소입력
      $ git push -u origin2 master
      ```

      - origin2 라는 새로운 브랜치 이름, 새로운 주소 입력

  - 이렇게 해도 돼

    $ git remote add origin ~ 주소입력

    git push --set-upstream origin master



- clone

  - git clone 주소 .
  - 끝에 점을 찍으면 현재 디렉토리로 복사해옴 안그러면 디렉토리가 추가로 생긴다음에 거기에다가 복제함
  - 쉽게 전체 정보를 다 가져옴 리모트 정보나 브랜치 정보 등등 다 가져와

- 서로 병렬적으로 같은 걸 작업했을 때 아래와 같은 메시지가 뜸

  ```shell
  Merge branch 'master' of github.com:YChaeeun/practiceGit
  ```

  - 받아와서, 자동으로 3 way merge를 하고 컨플릭트가 없으면 자동으로 커밋함
  - 만약 컨플릭트가 있다면 그걸 해결하면 돼

- git fetch git merge

  - git merge origin/master
  - 원격 저장소가 특별한 것이 아니라 새로운 브랜치 처럼 생각하면 된다!
  - git pull을 하면 합치기까지 같이 해버림 만약 rebase 처럼 전략적으로 merge를 하고 싶다면 fetch를 하고 merge를 해주면 돼



- git 초기설정 

  ```shell
  $ git config --global user.email "youremail"
  $ git config --global user.name "yourname"
  ```

  