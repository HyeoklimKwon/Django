## Q.1

```python
is_staff = models.BooleanField(
        _("staff status"),
        default=False,
        help_text=_("Designates whether the user can log into this admin site."),
    )
    is_active = models.BooleanField(
        _("active"),
        default=True,
        help_text=_(
            "Designates whether this user should be treated as active. "
            "Unselect this instead of deleting accounts."
        ),
    )
```

## Q.2

```python
 username = models.CharField(
        _("username"),
        max_length=150,
        unique=True,
        help_text=_(
            "Required. 150 characters or fewer. Letters, digits and @/./+/-/_ only."
        ),
        validators=[username_validator],
        error_messages={
            "unique": _("A user with that username already exists."),
        },
    )
정답은 150
```

## Q.3

auth_login



## Q.4

```python
(a)- AuthenticationForm
(b) - login
(c) - user

```



## Q.5

```python
boolean
```



## Q.6

 PBKDF2 알고리즘 사용

```html
PASSWORD_HASHERS = [
    'django.contrib.auth.hashers.PBKDF2PasswordHasher',
    'django.contrib.auth.hashers.PBKDF2SHA1PasswordHasher',
    'django.contrib.auth.hashers.Argon2PasswordHasher',
    'django.contrib.auth.hashers.BCryptSHA256PasswordHasher',
    'django.contrib.auth.hashers.BCryptPasswordHasher',
]
```

## Q.7

현재 로그인이 되어있는지 확인 작업이 없다.

```python
def logout(request):
    if request.user.is_authenticated:
        auth_logout(request)
    return redirect('accounts:login')
```

