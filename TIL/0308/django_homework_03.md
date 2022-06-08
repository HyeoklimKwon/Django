## Q.1

migration 작업



## Q.2

```
1) python manage.py migrate 0001
```

```
2) python manage.py sqlmigrate articles 0001
	
	BEGIN;
--
-- Create model Article
--
CREATE TABLE "articles_article" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "title" varchar(140) NOT NULL, "content" text NOT NULL, "created_at" datetime NOT NULL, "updated_at" datetime NOT NULL);
COMMIT;
```



## Q.3

```null
python manage.py shell
```



## Q.4

```
ID
AutoField:	기본 키 필드이며, 자동적으로 증가하는 필드입니다. 주로 ID에 할당
BigAutoField:	1 ~ 9223372036854775807까지 1씩 자동으로 증가
UUIDField:	UUID 전용 필드이며, UUID 데이터 유형만 저장

문자열
CharField:	적은 문자열을 저장하는 문자열 필드
TextField:	많은 문자열을 저장하는 문자열 필드

데이터
BinaryField:	이진 데이터를 저장하는 필드
DecimalField:	Decimal 데이터를 저장하는 필드
IntegerField:	Interger 데이터를 저장하는 필드

날짜 및 시간
DateField:	날짜 데이터를 저장하는 필드
TimeField:	시간 데이터를 저장하는 필드
DateTimeField:	날짜와 시간 데이터를 저장하는 필드
```

