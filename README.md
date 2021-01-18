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
