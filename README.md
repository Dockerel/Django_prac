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



### **데이터의 조회**

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

## Day 3 ~ 5

### **Chapter 2**

#### **장고 관련 참고 문서 링크**

- 장고 속성 공식 문서 주소 : docs.djangoprojects.com/en/3.0/ref/models/fields/#field-types

- 장고 공식 문서(데이터 조회 관련) : docs.djangoprojects.com/en/3.0/topics/db/queries

- 장고 admin 기능 관련 : docs.djangoprojects.com/en/3.0/ref/contrib/admin

- 템플릿 장고 공식 문서 주소 : docs.djangoproject.com/en/3.0/topics/templates

- 부트스트랩 다운로드 링크 : getbootstrap.com/docs/4.5/getting-started/download

- 부트스트랩 공식 문서 : getbootstrap.com/docs/4.5/getting-started/introduction

### **각종 오류 해결법**
1. 모델 사용시 object 오류 표시 해결법

   model.py의 해당 모델에

   ```objects = models.Manager()```

   코드 추가

   ex)
   <pre>
   <code>
   class Question(models.Model):
      objects = models.Manager()
      (... 생략 ...)
   </code>
   </pre>

2. static 오류
   <pre>
   <code>
   import os
   (... 생략 ...)
   STATICFILES_DIRS = [
      os.path.join(BASE_DIR, 'static')
   ]
   </code>
   </pre>