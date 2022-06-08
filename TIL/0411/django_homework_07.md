```python
## Q.1

class User(AbstractUser):
    """
    Users within the Django authentication system are represented by this
    model.
    Username and password are required. Other fields are optional.
    """

    class Meta(AbstractUser.Meta):
        swappable = "AUTH_USER_MODEL"
        
## Q.2
from django.contrib.auth.forms import UserCreationForm

## Q.3
(a) django_session
(b) session_key
```

