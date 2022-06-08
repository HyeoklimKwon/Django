## url.py

```django
#articles/url.py
from django.urls import path
from . import views

# URL namespace
app_name = 'articles'

urlpatterns = [
    # ~/articles/
    path('', views.index, name='index'),

    # ~/articles/new/ => 새 글 쓰기 페이지 랜더
    path('new/', views.new, name='new'),

    # ~/articles/create/ => 입력받은 정보 DB에 적용
    path('create/', views.create, name='create'),
   
    ]

#crud/url.py
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('articles/', include('articles.urls')),
]

```

## view.py

```django
def index(request):
    articles = Article.objects.order_by('-pk')
    context = {
        'articles': articles
    }   
    return render(request, 'articles/index.html', context)

def new(request):
    return render(request, 'articles/new.html')

def create(request):      
    title = request.POST.get('title')
    content = request.POST.get('content')
    article = Article(title=title, content=content)
    article.save()
    return redirect('articles:index', article.pk)

```

## templates\articles

```django
#index.html
{% extends 'base.html' %}

{% block content %}
<h1>INDEX</h1>

<div class="row row-cols-1 row-cols-md-2 row-cols-lg-4 g-4">
  {% for article in articles %}
    <div class="col">
      <div class="card">
        <a href="{% url 'articles:detail' article.pk %}">
          <div class="card-body">
            <h5 class="card-title">{{ article.pk }}. {{ article.title }}</h5>
            <p class="card-text">{{ article.content }}</p>
          </div>
        </a>
      </div>
    </div>
  {% endfor %}
</div>



{% endblock content %}


#new.html
{% extends 'base.html' %}

{% block content %}
<h1 class="text-center mt-5">NEW</h1>
<div class="row">
  <div class="col-4">
    <form action="{% url 'articles:create' %}" method="POST">
      {% csrf_token %}
      <div class="mb-3">
        <label for="title" class="form-label">TITLE</label>
        <input type="text" name="title" id="title" class="form-control">
      </div>      
      <div class="mb-3">
        <label for="content" class="form-label">CONTENT</label>
        <textarea name="content" id="content" cols="30" rows="10" class="form-control"></textarea>
      </div>    
      <button class="btn btn-primary">작성</button>
    </form>
  </div>
</div>
{% endblock content %}

```

## model.py

```django
class Article(models.Model):
    title = models.CharField(max_length=10)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
	def __str__(self):
        return f'{self.pk}. 제목: {self.title} - 내용: {self.content}'
```



