---
title : Git .gitignore 파일 작성하기
date : 2019-06-18
categories:
 - git
---



> 참고 : [git-scm.com/book]([https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-Git-%EA%B8%B0%EC%B4%88](https://git-scm.com/book/ko/v2/시작하기-Git-기초))



## .gitignore 파일이란?

- working directory에 있는 파일들 중에 커밋하고 싶지 않은 파일들, 관리할 필요가 없는 파일들의 패턴을 gitignore에 적어준다

  - 예를 들어서 비밀번호나 개인정보!

- bash창에서 vim으로 작성할 수 있다

  ```c
  $ vim .gitignore
  ```

  



## .gitignore 파일의 규칙

- 아무것도 없는 라인이나, # 로 시작하는 라인은 주석
- 슬래시(/)로 시작하면 하위디렉토리에는 적용되지 않는다
- 전체 디렉토리를 무시하고 싶으면 `디렉토리명` 끝에 슬래시(/)로 표현한다
- 느낌표(!)로 시작하는 파일은 무시하지 않는다
- 표준 Glob패턴을 사용한다 (프로젝트 전체에 적용됨)



### 표준 Glob 패턴?

- 정규표현식을 단순하게 만든 것
- `*`  : 문자가 0개 이상 / `?` : 문자가 1 개
- `[]`  :  괄호안에 있는 문자 중 하나
  - `-`  : 괄호 안 문자들 사이에 있는 문자 하나



## .gitignore 작성 예시

```shell
# 확장자가 .py인 파일 무시
*.py

# .py 파일 중에서 lib.py는 무시하지 말자
!lib.py

# folder 디렉토리에 있는 모든 파일 무시하기 (하위 폴더까지)
folder/
    
# doc/abcd.txt 는 무시해도 doc/folder2/abcd.txt는 무시하지 말자
doc/*.txt

# doc 디렉토리 아래 모든 .pdf 파일을 무시한다
doc/**/*.pdf
```

- **`doc/*.txt`**
  - *.txt는 **슬래시(/)로 시작**했기 때문에
  - 해당 doc 폴더에 있는 모든 .txt는 무시하지만, 하위디렉토리에 있는 .txt 파일들은 무시하지 않는다
- __`doc/**/*.pdf`__
  - `*/` : doc의 모든 하위폴더에 있는
  - `/*.pdf` :  모든 .pdf 파일을 무시한다