## Q.1

1) F 외래키 참조

2) F 직접참조를 할 수 없고 채comment_set manger를 사용

3) T 데이터 무결성을 위해서 매우 중요한 설정

4) F 아니여도된다. 유일한 값이면 됨.



## Q.2

컬럼 이름: Question_id

테이블 이름: Question



## Q.3

answer.comment_set.all()



## Q.4

1) delete 함수에서 유저가 로그인 된 상태인지 아닌지를 확인하지 않는다. 

2) ```python
   @login_required
   @require_POST
   def delete(request, pk):
       article = get_object_or_404(Article, pk=pk)
       if request.user.is_authenticated:
           if request.user == article.user:
               article.delete()
       return redirect('articles:index')
   
   ```

3) 