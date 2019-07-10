---
title: python anaconda 미니콘다 가상환경 설정하기
date: 2019-05-21
categories:
 - python
---



## 콘다 conda

- 파이썬 가상환경 (virtual environment) 설정을 돕는 도구

  (비슷한 도구로는 Venv가 있다)

- 콘다는 아나콘다라는 파이썬 배포판 안에 포함되어 있는데, 콘다만 따로 설치할 수도 있다 -> [미니콘다 다운로드](https://conda.io/miniconda.html)

  - 이때 "Add Anaconda to my PATH environment variable" 옵션은 선택하지 않는다!!

  - (우분투) Linux-64-bit (bash installer)를 다운받은 뒤, 다운로드 한 해당 경로로 이동한 뒤 아래 명령어를 적는다 [[참고\]](https://ychae-leah.tistory.com/78)

    ```
    bash Miniconda3-latest-Linux-x86_64.sh
    ```

  - conda list 명령어를 작성했을 때 설치된 패키지들의 리스트가 나열된다면 성공!

- 가상환경 : 여러 프로젝트 끼리 설정 및 패키지 버전 충돌을 막기위해 해당 프로젝트를 위한 독립된 공간을 따로 만들어 주는 기능이다

- 실행경로 추가하기

  ```shell
  export PATH=$HOME/miniconda3/bin:$PATH
  ```

  



## 콘다 가상환경 설정하기

- Anaconda prompt 창 사용 (윈도우에서 검색하기)

- git bash



### 1) 콘다 버전 확인 및 업데이트

```bash
# 버전 확인
conda --version

# 업데이트
conda update conda
```



### 2) 가상환경 생성하기 create

```bash
conda create --name <name> python=3.7
```

```bash
conda create --name miniFlask python=3.7
```

- miniFlask 라는 이름의 가상환경을 만들었다
- Proceed ([y]/n) 이 나오면 y 를 누르면 됨



### 3) 생성한 가상환경 활성화

```bash
source activate <name>
```

```bash
source activate ychaenFlask
```



### 4) 가상환경 비활성화

```bash
conda deactivate
```

- source deactivate 명령어를 적었더니 DeprecationWarning이 떴다! (더이상 사용되지 않는다는 의미)



### 5) 가상환경 리스트 확인하기

```bash
conda env list
```



### 6) 가상환경 삭제하기

```bash
conda remove --name <name> --all
```

- 가상환경 생성할 때 실수로 `conda create --name <envname>`만 적고 뒤에 `python=3.7'을 안적은 게 있었는데 얘는 자꾸 PackagesNotFoundError 가 나면서 삭제가 안됐다
- 그래서 conda install -n <envname> python=3.7 해서 패키지를 설치하고, 그 다음에 remove 명령어를 쓰니까 삭제됐다 !!





### 7) 패키지 설치하고 설치 리스트 확인하기

```bash
conda install <packagename>
pip install <packagename>
```

```bash
conda list
```

