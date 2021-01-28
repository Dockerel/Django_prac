# Django_tutorial
- - -
## Day 1



# 1

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

1. ```:mysite$ python3 manage.py runserver```


+ 서버 구동 확인 : 브라우저에서 "http://127.0.0.1:8000" 또는 "http://localhost:8000/ 으로 이동



## **언어, 시간 설정**

   - settings.py 에서
   
      ```LANGUAGE_CODE = 'ko-kr'```
      
      ```TIME_ZONE = 'Asia/Seoul'```
      
     로 변경
- - -
## Day 2



# 2-1

## **pybo 앱 생성하기**

1. (mysite):mysite$ django-admin startapp pybo

2. pybo라는 이름의 디렉터리가 생성되었음을 확인

3. http://localhost:8000/pybo/



## **config/urls.py 수정하기**

- 장고가 사용자의 페이지 요청을 이해할 수 있도록 config/urls.py 파일 수정 : 이를 'URL 매핑을 추가한다; 라고 

- URL 분리하기 : path('pybo/', include('pybo.urls)) - pybo/로 시작되는 페이지 요청은 모두 pybo/urls.py 파일에 있는 URL 매핑을 참고하여 처리하라는 의미

<code>
<pre>
from django.contrib import admin

from django.urls import path, include

from pybo import views


urlpatterns = [
   
   path('admin/', admin.site.urls),
   
   path('pybo/', include('pybo.urls)),
   
]
</code>
</pre>


## **pybo/urls.py 수정하기**

<pre>
<code>
from django.urls import path


from . import views


urlpatterns = [

   path('', views.index),
   
]
</code>
</pre>


## **views함수 추가 : views.py**

<code>
<pre>
from django.http import HttpResponse


def index(request):

   return HttpResponse("안녕하세요 pybo에 오신것을 환영합니다)
</code>
</pre>
   
+ 인식 순서 : config/urls.py -> pybo/urls.py -> views.py


## **데이터를 관리하는 모델**

- migrate
