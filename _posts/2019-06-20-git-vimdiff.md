---
title : Git vimdiff 사용해서 merge conflict 해결하기
date : 2019-06-20
published : false
categories:
 - vim
 - git
---







- vimdiff 사용하기!!!
- 아래 merge창으로 이동해서 (컨트롤+w로 이동)
  - 차이점들이 많다면 ] c 혹은 [ c 로 이동하면서 볼 수 있음
- 어떤 버전에서 가져올 것인지 생각하기 (창 순서대로 LOCAL BASE REMOTE)
- 컨플릭트 난 곳에 가서`:diffget LO` `:diffget BA` `:diffget RE` 중에 하나 적어주면 해당 부분을 가져옴
  - 각각의 컨플릭트들에 대해 적용하기! 
- 그다음에 `:wqa` 로 파일 전체 저장
- 이후에 git commit 해주면 merge끝!!!
- [링크](<https://stackoverflow.com/questions/14904644/how-do-i-use-vimdiff-to-resolve-a-git-merge-conflict>)
- [git mertool document링크](<https://git-scm.com/docs/git-mergetool>)
- `:diffupdate`로 차이점 보기
- 백업파일을 생성하는게 싫다면 `git config --global mergetool.keepBackup false` 로 설정을 바꿔준다