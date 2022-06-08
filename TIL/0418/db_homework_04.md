## Q.1

1)  T - M:N 관계에서는 모델링에 한계가 있기 때문에 중개 모델을 생성해주는 ManyToManytField를 사용한다.
2)  F - 중개 테이블 이름은 `앱 이름_ManyToManyField를 쓴 클래스_ManyToMnayField를 참조한 인스턴스 이름`
3) T 



## Q.2

(a) user

(b) article.like_user.all



## Q.3

(a) user_pk

(b) followers 

(c) filter

(d) remove

(e) add



## Q.4

form에서 meta 설정을 해주지 않았기 때문에

```python
class Meta:
       model = get_user_model()
       fields = ('username', 'email')
```

forms.py form class안에 추가해준다.



## Q.5

참조되는 테이블이 참조하는 테이블의 데이터를 가져오고 싶을 때 사용하는 이름'을 정의하는 것



## Q.6

(a) followings

(b) followers



(c) user 

(d) person

(e) person.pk