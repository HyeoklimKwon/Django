## Q.1

T - http request methods는 자원에 대한 행위를 장위하고 주어진 리소스에 수행하길 원하는 행동을 나타낸다.

F - http method에는 GET, POST, PUT, DELETE등이 있다.

F - 마지막에 슬래쉬를 포함하지 않아야하며, 행위또한 나타나지 말아야한다. create



## Q.2

200 : request succeed 성공적으로 불러옴 

400: 응답 상태 코드는 서버가 클라이언트 오류(예: 잘못된 요청 구문, 유효하지 않은 요청 메시지 프레이밍, 또는 변조된 요청 라우팅) 를 감지해 요청을 처리할 수 없거나, 하지 않는다는 것을 의미 

401: client request has not been completed because it lacks valid authentication credentials for the requested resource. 요청 권한 없음

403: server understands the request but refuses to authorize it. 서버에서 권한을 줄 수 없음

404:  server cannot find the requested resource. 서버에서 요청한 자원을 찾을 수 없음

500: the server encountered an unexpected condition that prevented it from fulfilling the request. 특정 조건으로 인해서 요구를 만족하는데 문제가 있음.



## Q.3

```python
class StudentSerializer(serializers.ModelSerializer):

    class Meta:
        model = Student
        fields = '__all__'
```



## Q.4

Queryset 및 Model Instance와 같은 복잡한 데이터를 JSON, XML 등의 유형으로 쉽게 변환 할 수 있는 Python 데이터 타입으로 만들어 줌.

