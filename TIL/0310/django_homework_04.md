## Q.1

```git
python manage.py makemigrations posts
python manage.py migrate posts 0001
```

## Q.2

#3 Post(title = '제목', content = '내용') 으로 고쳐야 한다.

## Q.3

#2 Post.objects.all()[-10] 인덱스 번호 음수는 적용되지 않는다.

## Q.4

```python
Post.title = '안녕하세요'
Post.content = '반갑습니다'
```

## Q.5

posts = Post.objects.all()



