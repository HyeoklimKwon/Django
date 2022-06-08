#### Q.1 왜 변수 context는 if else 구문과 동일한 레벨에 작성 되어있는가?

​    코드를 보면 if 구문과 else 구문 모두 form을 정의하는 바가 다르다. if 조건 아래에서는 form이 ArticleForm(request.POST) 로 되어있고, else 조건문 아래에서는 GET 장식의 ArticleForm()으로 정의 되어있다. 두 가지 경우 모두 form을 받고 html에 전달해야하기 때문에 동일한 레벨에 작성하였다.

#### Q.2 왜 request의 http method는 POST 먼저 확인하도록 작성하는가? 

​	request를 받는 과정에서는 크게 GET 방식과 POST 방식으로 나눌 수가 있는데, POST 방식의 경우 외부에서 임의적으로 추가하는 것을 방지하고 url에 정보가 그대로 노출되는 것을 방지하기 위해, csrf token 을 사용하는 부분에서 GET 방식과의 차이가 있다. 따라서 만약에 POST 검사를 먼저 하지 않을 경우 is valid 탈출시 에러메시지 포함한 form을 가져오려는 과정이 미포함이 되기에 POST 검사를 먼저한다. 추가적으로 다른 method들이 들어올때, 따로 더 조건문을 작성하지 않아도 되고 구조가 쉽게 쓸 수 있는 장점이 있다. 