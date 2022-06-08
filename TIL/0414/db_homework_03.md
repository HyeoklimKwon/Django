```python
from django.db import models
from django.conf import settings

# Create your models here.
class Convenient(models.Model):
    conv_name = models.CharField(max_length=10)
    owner = models.CharField(max_length=10)
    region = models.CharField(max_length=10)
    updated_at = models.DateTimeField(auto_now=True)
    
    def __str__(self):
        return self.conv_name


class Product(models.Model):
    product_name = models.CharField(max_length=200)
    price = models.IntegerField()
    number_left = models.IntegerField()
    benefit = models.IntergerField()
    updated_at = models.DateTimeField(auto_now=True)

    def __str__(self):
        return self.content
```

각 편의점 지점별 사장, 이름, 지점, 그리고 정보가 업데이트된 fields를 가지고, 

그 편의점 지점별로 상품들의 재고, 이름, 가격 그리고 편의점 이익과 마찬가지로 정보가 업데이트된 fields를 가지게 한다.