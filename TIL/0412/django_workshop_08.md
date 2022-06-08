```python
from django.shortcuts import render, redirect
from django.contrib.auth.forms import (
    UserCreationForm, 
    AuthenticationForm,
    UserChangeForm,
)
from django.contrib.auth import login as auth_login
from django.contrib.auth import logout as auth_logout


def signup(request):
  
    if request.method == 'POST':
        form = UserCreationForm(request.POST)
        if form.is_valid():
            form.save()            
            return redirect('accounts:login')
    else:
        form = UserCreationForm()
    
    context = {
        'form': form
    }
    return render(request, 'accounts/signup.html', context)


def login(request):
    
    if request.method == 'POST':
        form = AuthenticationForm(request, request.POST)
        if form.is_valid():
            user = form.get_user()
            auth_login(request, user)
            return redirect('articles:index')
    else:
        form = AuthenticationForm()
    context = {
        'form': form,
    }
    return render(request, 'accounts/login.html', context)


def logout(request):
    if request.user.is_authenticated:
        auth_logout(request)
    return redirect('accounts:login')


def delete(request):
    if request.user.is_authenticated:
        request.user.delete()
    return redirect('accounts:signup')


def update(request):
    
    if request.method == 'POST':
        pass
    else:
        
        form = UserChangeForm(instance=request.user)
    context = {
        'form': form
    }
    return render(request, 'accounts/update.html', context)
```

