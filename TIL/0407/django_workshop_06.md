### urls

articles

```python
from django.urls import path
from . import views

app_name = 'articles'
# ~/articiels/
urlpatterns = [
    path('', views.index, name = 'index'),
    
    path('<int:pk>/', views.detail, name='detail'),

    
    path('create/', views.create, name='create'),

    
    path('<int:pk>/update/', views.update, name='update'),

    
    path('<int:pk>/delete/', views.delete, name='delete'),
]


```



crud

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('articles/', include('articles.urls'))
]
```



### Views

```python
from django.shortcuts import render, redirect, get_object_or_404
from .models import Article
from .forms import ArticleForm
# Create your views here.

def index(request):
    articles = Article.objects.order_by('-pk')
    context = {
        'articles' : articles
    }
    return render(request, 'articles/index.html', context)

def detail(request, pk):
    
    article = get_object_or_404(Article, pk=pk)
    context = {
        'article': article,
    }
    return render(request, 'articles/detail.html', context)


def create(request):
    
    if request.method == 'POST':
        form = ArticleForm(request.POST)
        if form.is_valid():
            article = form.save()
            return redirect('articles:detail', article.pk)
    else:
        # form instance <= form class
        form = ArticleForm()
    # POST 쪽에서도 활용할 수 있도록
    context = {
        'form': form
    }
    return render(request, 'articles/create.html', context)


def update(request, pk):
    
    article = get_object_or_404(Article, pk=pk)

    if request.method == 'POST':
        request.POST
        form = ArticleForm(request.POST, instance=article)
        if form.is_valid():
            article = form.save()
            return redirect('articles:detail', article.pk)
    else:
        # form instance 준비
        # 가져온 정보 form class에 넘겨주기
        form = ArticleForm(instance=article)

    context = {
        'form': form
    }
    return render(request, 'articles/update.html', context)


def delete(request, pk):
    
    article = get_object_or_404(Article, pk=pk)
    if request.method == 'POST':
        article.delete()
        return redirect('articles:index')
    return redirect('articles:detail', article.pk)

```



### models

```python
from django.db import models

# Create your models here.
class Article(models.Model):
    title = models.CharField(max_length=10)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add= True)
    updated_at = models.DateTimeField(auto_now= True)

```



### Forms

```python
from django import forms
from .models import Article


class ArticleForm(forms.ModelForm):
    title = forms.CharField(
        label='제목',
        widget=forms.TextInput(
            attrs={
                'class': 'form-control',
                'maxlength': 10,
                'placeholder': '제목을 작성해주세요.',
            }
        )
    )
    content = forms.CharField(
        label='내용',
        widget=forms.Textarea(
            attrs={
                'class': 'form-control',
                'placeholder': '내용을 작성해주세요.',
            }
        )
    )

    class Meta:
        model = Article
        fields = '__all__'
```



### templates

index

```html
{% extends 'base.html' %}

{% block content %}
<h1>Articles</h1>
<a href="{% url 'articles:create'%}">CREATE</a>
<div class="list-group">
  {% for article in articles %}
    <p>글 번호 : {{article.pk }}</p>
    <p>글 제목 : {{article.title }}</p>
    <p>글 내용 : {{article.content }}</p>
    <a href="{% url 'articles:detail' article.pk %}">DETAIL</a>
    <hr>
  {% endfor %}
</div>
{% endblock content %}


```

create

```html
{% extends 'base.html' %}

{% block content %}
<h1>CREATE</h1>

<form method="POST">
  {% csrf_token %}
  <div class="mb-3">
    {{ form.title.errors }}
    {{ form.title.label_tag }}
    {{ form.title }}
  </div>
  <div class="mb-3">
    {{ form.content.errors }}
    {{ form.content.label_tag }}
    {{ form.content }}
  </div>
  <button class="btn btn-outline-primary">작성하기</button>
</form>
{% endblock content %}
```

detail

```html
{% extends 'base.html' %}

{% block content %}
<h1>DETAIL</h1>

<div class="row justify-content-center">
  <div class="card col-8">
    <div class="card-body">
      <h5 class="card-title">{{ article.title }}</h5>
      <p class="card-text">{{ article.content }}</p>
      <hr>
      <p class="fw-light">작성 : {{ article.created_at }}</p>
      <p class="fw-light">수정 : {{ article.updated_at }}</p>
      <a
        href=".."
        class="btn btn-outline-primary"
      >HOME</a>
      <a
        href="{% url 'articles:update' article.pk %}"
        class="btn btn-outline-warning"
      >수정하기</a>
      <form action="{% url 'articles:delete' article.pk %}" method="POST">
        {% csrf_token %}
        <button class="btn btn-outline-danger">삭제하기</button>
      </form>
    </div>
  </div>
</div>
{% endblock content %}
```

update

```python
{% extends 'base.html' %}

{% block content %}
<h1>UPDATE</h1>

<form method="POST">
  {% csrf_token %}
  {{ form }}
  <button>수정하기</button>
</form>
{% endblock content %}
```

