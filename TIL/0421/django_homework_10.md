## Q.1

1) F 반드시는 아니다. 다른 여러 프레임워크들도 사용가능하다. 
2) F Postman 혹은 python anywhere등 사용 가능
3) F DRF에서는 필수적으로 작성해야 해당 view 함수가 정상적으로 동작한다.
4) T Serializers는 Queryset 객체를 JSON 포맷으로 변환 할 수 있는 python 데이터 타입으로 만들어준다



## Q.2

정보의 자원을 표현해야 하는 "URI"와 자원의 대한 행위를 표현하는 "HTTP Method" 라고 할 수 있다.

## Q.3

```python
from rest_framework import status

@api_view(['POST'])
def create_article(request):
 serializer = ArticleSerializer(data=request.data)
 if serializer.is_valid(raise_exception=True):
   serializer.save()
   return Response(serializer.data, status=status.HTTP_201_CREATED)

```

