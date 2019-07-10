---
title : linux mysql 설치 & 비밀번호 설정하기(우분투)
date : 2019-06-26
categories:
 - linux
---



> VMware 
>
> ubuntu-18.04



## 설치

- 윈도우 용 우분투 bash를 사용하고 있었는데, 그 환경에서는 에러가 나서 설치를 하지 못했다
- 그래서 VMware 가상환경에다가 우분투를 설치한 뒤에, 해당 환경에서 mysql 설치를 진행했다!!

- 설치하기

  ```shell
  $ sudo apt update
  $ sudo apt install mysql-server
  ```

  



## root 비밀번호 설정

- mysql-server-5.7 이상의 버전을 설치할 때 root 비밀번호 설정하기가 까다롭다고 한다

### 방법 1

- mysql_secure_installation
- root 비밀번호를 설정하고 또 변경할 수도 있다. 
- validate password plugin 은 보안을 위해 비밀번호를 강화하는 plugin인데, 비밀번호를 설정하는 규칙이 복잡해서 비밀번호를 설정하는데 까다롭다
  - 해당 여부를 묻는 질문에 no 를 추천..!!!
- 그외 설정들은 읽어보고 선택하기

![mysql password]({{site.url}}{{site.baseurl}}/assets/images/mysql-1.png)



### 방법 2

- mysql.user 직접 변경하기 (mysql에 접속한 뒤에 가능!)

  ```shell
  $ mysql -u root -p
  ```

  ```shell
  $ sudo mysql -u root -p
  ```

- 방법 1을 실행해도 root 비밀번호 창이 생기지 않는다면 방법 2를 실행하기

- 아래 명령어로 root의 인증모드를 보고, auth_socket 이라면, 이를 변경해준다

  ```shell
  >> SELECT user,plugin,host FROM mysql.user;
  ```

- 비밀번호 인증 모드로 변경

  ```shell
  >> ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password you want';
  ```

  - password you want 의 내용에 원하는 비밀번호를 작성하면 된다

- 바로 적용하기

  ```shell
  >> FLUSH PRIVILEGES;
  ```

  

![mysql]({{site.url}}{{site.baseurl}}/assets/images/mysql-2.png)



## 실행하기

- mysql 실행하기

  ```shell
  $ service mysql start
  ```

- 로그인 하기

  ```shell
  $ mysql -u root -p
  ```

- 상태 보기

  ```shell
  $ service mysql status
  ```

- 실행 종료하기

  ```shell
  $ service mysql stop
  ```

  