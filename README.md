# Django_tutorial
- - -
## Day 1



## **파이썬 가상 환경 생성하기**


+ 전체 구조

DjangoProjects

|

mysite

|

config

   ㄴ__init.py
   
   ㄴ__pycache__
   
         ㄴasgi.py
         
         ㄴsetting.py
         
         ㄴurls.py
         
         ㄴwsgi.py
         
|

db.sqlite3

|

manage.py

|

venv_web

   ㄴbin
   
   ㄴ ...
   


+ 가상환경 생성과정

1. 초기 폴더 DjangoProjects에서 가상환경 생성

```:DjangoProjects$ python3 -m venv venv_web```


2. 가상환경 활성화

```:venv_web/bin$ source ./activate```

* 비활성화 하려면 ```deactivate``` 명령 실행



## **가상환경 내에 장고 설치**

1. pip install 을 통해 장고 설치. (가상환경이 활성화된 상태에서 설치)

```(venv_web) :DjangoProjects$ pip install django```

2. pip 최신 버전 설치 (선택)

```python3 -m pip install --upgrade pip```



## **장고 프로젝트 생성**

1. ```:DjangoProjects/mysite$ django-admin startproject config .```

   - 마침표(.)는 현재 디렉터리를 장고 프로젝트로 설정하는 옵션

   - manage.py 파일이 생성되었다면 성공
   
   
   
## **서버 구동**

1. ```:mysite$ python3 manage.py runserver'''

```Watching for file changes with StatReloader

Performing system checks...

 

System check identified no issues (0 silenced).

 

You have 18 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.

Run 'python manage.py migrate' to apply them.

September 18, 2020 - 09:16:29

Django version 3.1.1, using settings 'config.settings'

Starting development server at http://127.0.0.1:8000/

Quit the server with CONTROL-C.```

+ 위와 같은 메시지가 뜨면 성공

+ 서버 구동 확인 : 브라우저에서 "http://127.0.0.1:8000" 또는 "http://localhost:8000/ 으로 이동



## **언어, 시간 설정**

   - settings.py 에서
      ```LANGUAGE_CODE = 'ko-kr'
      TIME_ZONE = 'Asia/Seoul'
      로 변경
