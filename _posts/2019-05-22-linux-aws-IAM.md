---
title: inux IAM
published: false
---





- node 설치

  ```
  $ sudo apt-get install nodejs
  ```

  

- npm 설치

  ```
  $ sudo apt-get install npm
  ```

  

- aws cli 설치

  ```
  $ sudo apt install awscli
  ```

  



- 설치 완료 및 버전 확인

  ```
  $ node --version
  $ npm --version
  $ aws --version
  ```



- node 업데이트 (n 모듈을 이용해서 버전 업데이트)

  ```
  $ sudo npm cache clean -f
  $ sudo npm install -g n
  $ sudo n stable
  ```

  ```
  $ sudo n latest
  // 다른 버전을 설치하고 싶다면 sudo n 6.0.0 이런식으로 작성하기
  ```

  - 설치를 완료하고 터미널 창을 종료한 뒤에 다시 시작



```
$ node --version // 8.10.0 이상 필요  
v12.1.0  
$ npm --version // 5.2 이상 필요  
6.9.0  
$ aws --version  
aws-cli/1.16.156 Python/2.7.15 Darwin/18.5.0 botocore/1.12.146  
```





## AWS Amplify CLI 설치



- 다운로드 및 버전 확인

  ```
  $ npm install -g @aws-amplify/cli
  (...)
  
  $ amplify --version
  ```

  

## 유저 생성 IAM

### IAM 이란?

- AWS Identity and Access Management(IAM)는 AWS 리소스에 대한 액세스를 안전하게 제어할 수 있는 웹 서비스입니다. 
-  IAM을 사용하여 리소스를 사용하도록 인증(로그인) 및 권한 부여(권한 있음)된 대상을 제어합니다.



AWS 페이지에 가서 IAM 검색

- 



- AWS Access Key와 Secret Access Key 키를 기억해야 함!!
  - csv 파일 다운로드 하기



### 인라인 정책 추가로 권한 부여

- 실제로 제품을 사용할 때는 모든 리소스에 대한 권한이 아니라 필요한 리소스에 대한 권한을 부여하면 됨





### Default AWS 계정 등록하기

```
$ aws configure
// 네번째 입력인 output에 대한 입력 생략
```



[]



- ap-northeast-2 
  - 서울 리전



```
$ aws configure list
```



[]





[키 관리에 문제가 생겼다면?](<https://docs.aws.amazon.com/ko_kr/IAM/latest/UserGuide/id_credentials_access-keys.html>)