---
title: github Pages 'jekyll serve' 문제 해결하기  (minimal-mistakes)
date : 2019-04-15
tags:
 - tutorial
categories:
 - Github_Pages

---



github pages 에 `commit`하기 전에 `ruby`와 `jekyll serve`를 통해서 로컬에서 홈페이지를 올려서 살펴볼 수 있다! 쓸데없고 귀찮게 커밋을 여러번 하지 않기 위함이기도 하고, 간혹 문제가 생겨서 포스팅이 올라가지 않을 때 jekyll serve로 살펴보면 쉽게 문제를 해결할 수 있다.



간혹 github pages 빌드에러라며 아예 홈페이지에 들어가지지 않는 경우가 있는데, jekyll serve로 띄워보면 에러메시지가 나와서, 문제를 좀 더 쉽게 파악하고 해결할 수 있다.



## 0) Ruby + Devkit & Jekyll 설치

[다운로드 홈페이지](https://rubyinstaller.org/downloads/) 다운받은 후, ruby prompt를 열어 `gem install jekyll bundler`라고 입력해주면 설치가 진행 된다.



설치를 완료한 후에 `jekyll -v`로 설치 잘 되었는지 확인하면 된다. 



![ruby prompt]({{site.url}}{{site.baseurl}}/assets/images/ruby.png){: .align-center}







## 1) gemfile 수정하기

gemfile이 문제라는 메시지가 나오면, 해당 메시지에서 말하는 gem이 뭔지를 살펴보면 문제를 해결할 수 있다!



문제를 해결하는 법은 아래 둘 중에 하나를 하면 된다. [(참고)](<https://github.com/mmistakes/minimal-mistakes/issues/1937>)

+ 해당 gem 을 주석처리해서 없애기
+ 문제가 있다고 말하는 부분을 `Gemfile`에 추가해주고, `_config.yml`파일의 `plugins:`부분에도 추가하기



내가 봤던 에러는 `jekyll-include-cache` 와 `jemoji`가 관련이 있어 보였는데, 아래와 같이 `Gemfile`과 `_config.yml`파일을 수정했더니 문제가 해결됐다.



>  `error: cannot load such file -- jekyll-include-cache` 
>
> `error: cannot load such file -- jemoji`





**Gemfile**

```gem
source "https://rubygems.org"

gem "json"
gem "jekyll"
gem "jekyll-sitemap"
gem "jekyll-feed"
gem "jekyll-paginate"
gem "jekyll-gist"

gem 'jekyll-include-cache' # 추가
```





**_config.yml**

```yml
# Plugins (previously gems:)
plugins:
  - jekyll-paginate
  - jekyll-sitemap
  - jekyll-gist
  - jekyll-feed
  #- jemoji 			  # 주석처리
  - jekyll-include-cache  # 추가

# mimic GitHub Pages with --safe
whitelist:
  - jekyll-paginate
  - jekyll-sitemap
  - jekyll-gist
  - jekyll-feed
  #- jemoji			      # 주석처리
  - jekyll-include-cache  #추가
```





## 2) 'bundle exec jekyll serve' 사용하기

jekyll serve를 하려고 할 때, 계속 bundle 에러가 나는 경우가 있다. 이럴 때, `bundle exec jekyll serve` 명령어를 이용하면 쉽게 해결되기도 한다. 어떻게 해야 하는 지 알려주기 때문에 창에 나오는 대로 따라하면 된다.

bundle이 설치되지 않았다고 `bundle install` 혹은 `bundle update`를 하라는 메시지가 나오는데, 그대로 따라서 설치해 주면 된다.





## 3) 윈도우 : chcp 65001 을 입력해보자

위에 하라는 대로 다했는데도 안되는 경우가 있다...!!! 으으!!

`Invalid CP949 character "\xEC"` 에러메시지가 나는 경우,  이건 윈도우에서의 인코딩 문제일 수 있다.  



터미널에 `chcp 65001` 이라고 입력하면, `Active code page : 65001`로 넘어가는 걸 볼 수 있다. 그리고 다시 `bundle exec jekyll serve`를 입력하면 된다.



> 만약 UTF-8 인코딩을 사용한다면, 문서 안에 `BOM` 헤더를 사용하지 않아야 합니다. 그렇지 않으면 Jekyll 에 아주, 아주 안 좋은 일이 벌어집니다. 이는 특히, 윈도우즈에서 Jekyll 을 사용하는 것에 연관된 문제입니다.
>
> 
>
> 참고 : [jekyll 공식 홈페이지](<https://jekyllrb-ko.github.io/docs/windows/>)





## 성공?!

만약 문제 없이 성공한다면 아래 `Server address: http://127.0.0.1:4000/` 주소로 들어가면 홈페이지가 뜨는 것을 볼 수 있다!! :)



```
  Jekyll Feed: Generating feed for posts
                    done in 9.4 seconds.
  Please add the following to your Gemfile to avoid polling for changes:
    gem 'wdm', '>= 0.1.0' if Gem.win_platform?
 Auto-regeneration: enabled for 'C:/Users/Desktop/ychaeeun.github.io'
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
      Regenerating: 1 file(s) changed at 2019-04-15 09:18:57
```



