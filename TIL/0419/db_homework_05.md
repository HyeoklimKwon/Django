## Q.1

MVC 디자인 패턴 모델 뷰 컨트롤러 
장고는 MTV 패턴 모델-데이터베이스의 기록을 관리 /템플레이츠- 파일의 구조나 레이아웃을  정의 // 뷰-오전 8:44 2022-03-21 HTTP 요청을 수신하고 응답을 반환 데이터에 접근

## Q.2

(a) articles 

(b) views

(c) views.index, name='index'



## Q.3

(a) settings.py

(b) TEMPLATES

(c) STATIC_URL



## Q.4

1) python manage.py makemigrations
2) python manage.py showmigrations
3) python manage.py sqlmigrate
4) python manage.py migrate



## Q.5

1) F
2) T
3) T
4) T



## Q.6

1. settings.py에 **MEDIA_URL**이라는 값을 추가해 줍니다.

​		\# settings.py MEDIA_URL = "/media/"

2. 다음으로 **MEDIA_ROOT**값을 추가해 줍니다.

​		\# settings.py MEDIA_ROOT = os.path.join(BASE_DIR, "crud/uploaded_files")



## Q.7

1) T
2) F
3) T
4) T
5) T



## Q.8

CASCADE



## Q.9

(a) ManyToManyField

(b) related_name



## Q.10

중개 테이블 이름: accounts_user_followings

컬럼 1 :  from_user_id

컬럼 2:  to_user_id

 