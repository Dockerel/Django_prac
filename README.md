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

<<<<<<< HEAD
- ```python3 manage.py migrate```

   : 앱이 필요로 하는 테이블 생성


## **모델 만들기**

- 질문과 답변에 대한 모델

<pre>
<code>
from django.db import models

# Create your models here.

class Question(models.Model):
    subject = models.CharField(max_length=200)
    content = models.TextField()
    create_date = models.DateTimeField()

class Answer(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    content = models.TextField()
    create_date = models.DateTimeField()
</code>
</pre>


- pybo 앱 등록하기

   - config/settings.py
   - INSTALLED_APPS 항목에 pybo 앱 추가

   <pre>
   <code>
   (... 생략 ...)
   INSTALLED_APPS = [
      'pybo.apps.PyboConfig',
      'django.contrib.admin',
      'django.contrib.auth',
      (... 생략 ...)
   ]
   (... 생략 ...)
   </code>
   </pre>

- migrate로 테이블 생성하기

   - 모델이 생성되거나 변경된 경우 makemigrations 명령을 실행
   <pre>
   <code>
   :mysite$ python3 manage.py makemigrations
   :mysite$ python3 manage.py migrate
   </code>
   </pre>

   - makemigration 명령 수행후 pybo/migrations/0001_initial.py 파일이 생성되는지 확인!

   - 정확히 모델의 속성이 추가되거나 변경된 경우에 실행해야 하는 명령임. 메서드(```__str__```) 등이 추가된 경우에는 하지 않아도 됨


## **데이터 입력, 저장, 조회하기**
---
### 데이터의 입력, 저장

1. 장고 셸 실행

   ```:mysite$ python3 manage.py shell```

2. Question, Answer 모델 임포트

   ```from pybo.models import Question, Answer```

3. ```>>> from django.utils import timezone```

   ```>>> q = Question(subject='q title ex', content='q content ex', create_date=timezone.now())```

   ```>>> q.save()```

   - id가 각 데이터마다 생성시 자동으로 할당됨

   - ```q.id``` 로 데이터의 id값 확인

### **데이터의 조회 - 1**

- Question.objects.all()

```<QuerySet [<Question: Question object (1)>, <Question: Question object (2)>]>```

- ```__str__``` 메서드의 추가로 데이터의 속성값을 보여줄 수 있음

<pre>
<code>
# :mysite/pybo/models.py

def __str__(self):
   return self.subject

# 위 코드 추가
</code>
</pre>

- Question.objects.all()

```<QuerySet [<Question: 'Question example 1'>, <Question: Question example 2>]>```

---
### **데이터의 조회 - 2**

1. filter

   ```Question.objects.filter(id=1)```

   - 제목의 일부를 이용하여 데이터 조회하기

      ```Question.objects.filter(subject__contains='search word')```

2. get : 반드시 1건의 데이터를 반환해야 한다는 특징이 있음

   ```Question.objects.filter(id=1)```

   ---

   - filter, get의 차이

      조건에 맞지 않는 데이터를 함수로 조회하면 get 함수의 경우 오류가 발생하지만, filter 함수의 경우 그저 빈 QuerySet을 반환한다.

---

### **데이터 수정하기**

1. 데이터의 조회
   
   ```q = Question.objects.get(id=2)```

2. subject 속성 수정
   
   ```q.subject = 'Django Model Question'```

3. 수정된 모델 저장

   ```q.save```

### **데이터 삭제**

1. 데이터의 조회
   
   ```q = Question.objects.get(id=2)```

2. 삭제

   ```q.delete()```

---

## **연결된 데이터 알아보기**

1. Answer 모델 데이터 만들기

   <pre>
   <code>
   a = Answer(question=q, content='response example', create_date=timezone.now())

   a.save()
   </code>
   </pre>

2. 연결된 데이터로 조회하기: 답변에 있는 질문 조회하기

   ```a.question```

3. 연결된 데이터로 조회하기: 질문을 통해 답변 찾기

   ```q.answer_set.all()```

   - 질문 1개에는 1개 이상의 답변이 달릴 수 있으므로 질문에 달린 답변은 q.answer_set으로 조회해야 한다.

      - 질문 입장 : q.answer_set

      - 답변 입장 : a.question
---
# 2-3

## **개발 편의를 제공하는 장고 Admin**

```:mysite$ python3 manage.py createsuperuser```

- localhost:8000/admin 으로 접속

- 장고 Admin에서 모델 관리하기
<pre>
<code>
# :mysite$pybo/admin.py에 추가

from django.contrib import admin

from .models import Question


admin.site.register(Question)
</code>
</pre>

- 장고 Admin에 데이터 검색 기능 추가하기
<pre>
<code>
# :mysite$pybo/admin.py에 추가

from django.contrib import admin

from .models import Question

class QuestionAdmin(admin.ModelAdmin):
   search_fields = ['subject']

admin.site.register(Question, QuestionAdmin)
</code>
</pre>
---