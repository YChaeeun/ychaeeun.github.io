---
title: github Pages "jekyll serve Error YAML Exception reading" 등등 에러 해결하기
date: 2019-04-15
tags:
 - tutorial
categories:
 - Github_Pages
---





jekyll serve 가 잘 동작하는 것 같다가도, 시뻘건 에러메시지를 왕창 쏟아낼 때가 있다. (ㅠㅠ) 나의 경우 대부분 `jekyll serve Error: YAML Exception reading` 로 시작하는 에러 메시지들이었는데, jekyll이 포스트를 읽어오기 위해 가장 중요한 `YAML`에서 오류가 있을 경우에 여러 에러 메시지가 나온다.



## 1) did not find expected key while parsing a block mapping at ~

 

제목을 작성하다보면 들어가는 **특수문자**들이 있을 때 이 에러 메시지가 자주 나왔다. 예를 들어 아래와 같이 제목을 작성한다면 에러가 난다.  [ ] {} 괄호와 : 쌍점 때문에....

만약 해당 에러메시지가 나온다면, `YAML`에서 쓰지 말아야 하는 특수문자를 사용한 것일 수도 있으니 이리저리 바꿔보면 문제가 해결될 것이다.

```yml
title: [github_pages] "Error : YAML Exception reading"  #에러!

title: github_pages "Error YAML Exception readinf"  # 문제가 있는 특수문자들을 빼주면 된다
```





## 2)  could not find expected ':' while scanning a simple key at ~

이 에러는 : 쌍점 뒤에 **띄어쓰기**를 안했을 때 등장한 에러였다.

```yml
date:2019-04-15  # 에러!

date: 2019-04-15  # : 뒤를 한 칸 비우면 된다.
```





## 3)  found character that cannot start any token while scanning for the next token at ~ 

해결하고도 조금 어이가 없었던 에러...!!!!! 이 에러는 tags나 categories를 작성할 때, `tab`을 사용했을 때 나온 에러였다. jekyll은 tab을 인식하지 못하는 모양... `space`를 이용해줘야 한다.

물론 본문을 작성할 때는 상관없었고, `YAML`파일의 경우에 문제가 있었다!!

```yml
tags:
     - tutorial			# tab을 사용하면 에러가 난다
categories:
	- Github_Pages
	
	
tags:
 - tutorial				# space 사용하기~
categories:
 - Github_Pages
```





## 4) 사이트 깨져 보임



![page_broken]({{site.url}}{{site.baseurl}}/assets/images/broken.png){: .full}



baseurl을 잘못 설정했을 때 다음과 같은 화면 깨짐이 나타났다. 특별하게 사용할 일이 없을 경우에는 그냥 "" 로 비워두는 게 좋을 것 같다. 이와 관련해서 자세하게 보고싶다면... [(참고)](http://downtothewire.io/2015/08/15/configuring-jekyll-for-user-and-project-github-pages/)

```yml
baseurl : "/"   # 이렇게 했다가 에러가 났었음

baseurl : ""
```





## 5) 기타 등등

그 외에 jekyll serve 에는 나오지 않는 데 git push를 하고 나니 나오는 것들도 있었다. 처음에는 에러인 줄 알아서 이리저리 검색을 하고 답이 나오지 않아 멘붕 했던 기억이 있다. 이유를 알 수 없고 검색해도 잘 모르겠다면 그냥 push한 다음에 적용된 github pages를 살펴보면 해결 될 수도 있다!



나의 경우에는

+  favicon을 설정할 때

+ `date: 9999-12-31` 로 설정했을 때 

jekyll serve에서는 나오지 않았지만 실제 페이지에 적용했을 때는 잘 나오던 것을 확인 할 수 있었다.



> date의 경우, serve할 때 --future 을 붙이면 된다는 글을 본 적이 있다!



