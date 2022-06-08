## url.py

### templates/articles/url.py

```django
#detail.html
{% extends 'base.html' %}

{% block content %}
<div class = "container mx-3">
    <h1 class = "fw-bold ">DETAIL</h1>

    <h2>{{ article.title }}</h2>
    <p>{{ article.content }}</p>
    <p>작성일: {{ article.created_at }}</p>
    <p>수정일: {{ article.updated_at }}</p>
    <a class = "text-decoration-none" href="{% url 'articles:edit' article.pk %}">EDIT</a>
    <a class = "text-decoration-none" href="{% url 'articles:delete' article.pk %}" method="POST">
        {% csrf_token %}
        DELETE
    </a>
    <br>
    <a class = "text-decoration-none" href="{% url 'articles:index' %}">BACK</a>
    
</div>

{% endblock content %}
```

```django
#edit.html
{% extends 'base.html' %}


{% block content %}
<div> 
    <h1 class= "fw-bold">EDIT</h1>

    <form action="{% url 'articles:update' article.pk %}" method="POST">
        {% csrf_token %}
        <label for="title" class="form-label">제목</label>
        <input type="text" name="title" id="title" class="form-control" value="{{ article.title }}">
        <label for="content" class="form-label">내용</label>
        <textarea name="content" id="content" cols="30" rows="10" class="form-control">{{ article.content }}</textarea>
        <button>수정</button>
        <a href="{% url 'articles:detail' article.pk %}">BACK</a>
    </form>

</div>
{% endblock content %}
```

```django
#index.html
{% extends 'base.html' %}

{% block content %}
<h1 class = "fw-bold mx-5">INDEX</h1>
<a href="{% url 'articles:new' %}" class = "text-decoration-none mx-5">NEW</a>
<br>
<div class="row row-cols-1 row-cols-md-2 g-4">
    {% for article in articles %}
        <div class = "mx-5">
            
            <br>
            <h2>제목: {{ article.title }}</h2>
            <p>내용: {{ article.content }}</p>
            <br>
            <a href="{% url 'articles:detail' article.pk %}" class = "text-decoration-none">DETAIL</a>
        </div>
    {% endfor %}


{% endblock content %}
```

```dj
#new.html
{% extends 'base.html' %}

{% block content %}
<h1 class = "fw-bold">NEW</h1>

<form action="{% url 'articles:create' %}" method="POST">
    {% comment %} POST 방식에서 필수! {% endcomment %}
    {% csrf_token %}
    <div class="mb-3">
      <label for="title" class="form-label">제목</label>
      <input type="text" name="title" id="title" class="form-control">
    </div>
    <div class="mb-3">
      <label for="content" class="form-label">내용</label>
      <textarea name="content" id="content" cols="30" rows="10" class="form-control"></textarea>
    </div>
    <button class="btn btn-primary">작성</button>
    <a href="{% url 'articles:index' %}" class = "text-decoration-none">BACK</a>
  </form>
{% endblock content %}
```

### crud/urls.py

```python
"""crud URL Configuration

The `urlpatterns` list routes URLs to views. For more information please see:
    https://docs.djangoproject.com/en/3.2/topics/http/urls/
Examples:
Function views
    1. Add an import:  from my_app import views
    2. Add a URL to urlpatterns:  path('', views.home, name='home')
Class-based views
    1. Add an import:  from other_app.views import Home
    2. Add a URL to urlpatterns:  path('', Home.as_view(), name='home')
Including another URLconf
    1. Import the include() function: from django.urls import include, path
    2. Add a URL to urlpatterns:  path('blog/', include('blog.urls'))
"""
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('articles/', include('articles.urls')),
```



## views.py

```python
from django.shortcuts import render

# Create your views here.
from django.shortcuts import render, redirect, get_object_or_404

from .models import Article

def index(request):
    articles = Article.objects.order_by('-pk')
    context = {
        'articles': articles

    }
    return render(request, 'articles/index.html',context)

def new(request):
    return render(request, 'articles/new.html')

def create(request):
    title = request.POST.get('title')
    content = request.POST.get('content')

    article = Article()
    article.title = title
    article.content = content
    article.save()

    return redirect('articles:index')

def detail(request, article_pk):
    article = get_object_or_404(Article, pk=article_pk)

    context = {
        'article': article
    }
    return render(request, 'articles/detail.html', context)

def delete(request, article_pk):
    article = get_object_or_404(Article, pk=article_pk)

    # 2. 삭제
    article.delete()

    return redirect('articles:index')

def edit(request, article_pk):
    article = get_object_or_404(Article, pk=article_pk)
    context = {
        'article': article
    }
    return render(request, 'articles/edit.html', context)

def update(request, article_pk):
    article = get_object_or_404(Article, pk=article_pk)
       
    title = request.POST.get('title')
    content = request.POST.get('content')

    article.title = title
    article.content = content
   
    article.save()

    return redirect('articles:detail', article.pk)
```

## templates/base.html

```django
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">
    <title>Document</title>
</head>
<body>
    {% block content %}

    {% endblock content %}
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-ka7Sk0Gln4gmtz2MlQnikT1wXgYsOg+OMhuP+IlRH9sENBO0LRn5q+8nbTov4+1p" crossorigin="anonymous"></script>
</body>

</html>
```



### model.py

```python
from django.db import models

class Article(models.Model):
    title = models.CharField(max_length=100)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    def __str__(self):
        return f'{self.pk}. {self.title}'

```

