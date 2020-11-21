---
date: "2020-10-21T06:05:22+06:00"
title: "Customizing authentication in Django"
---

## Intro
The authentication that comes with Django is good enough for most common cases. Django also allows us to customize authentication if the defaults don't match our requirements.

There are multiple approaches we can take to customize the Django authentication system. We can **extend** the default User model, or **substitute** a completely customized model.

---

## Extending the default User model

There are two ways to extend the default User model without substituting our own model.


### 1) Using Proxy Model :

##### What?
A proxy model is just another class that provides a different interface for the same underlying database model without creating a new table in the database.

##### When to use?
When we don’t need to have any change in the database, but we need to change the behaviour a little bit (e.g. default ordering, add new methods, etc)

##### Code Example

```python
# app/models.py
# ----------------

from django.db import models
from django.contrib.auth.models import User


class UserProxy(User):
    class Meta:
        proxy = True
        ordering = ('username', )

    def do_something(self):
        print("doing something")
```

> Note : In the above example, `User.objects.all()` and `UserProxy.objects.all()` will call the same database but they will differ in behaviour (UserProxy will sort the result by username). Also UserProxy can use the new method named *do_something*.



### 2) Using One-To-One Link With a User Model (Profile) :

##### What?
It is a regular Django model that has it’s own database table and holds a One-To-One relationship with the existing User Model. This is often called a profile model.

##### When to use?
When we wish to store additional (non-auth) information related to User.

##### Code Example :

```python
# app/models.py
# ----------------

from django.db import models
from django.contrib.auth.models import User

class Profile(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE)
    bio = models.CharField(max_length=500)
    website = models.CharField(max_length=200)
```

> Note : we can define [signals](https://docs.djangoproject.com/en/3.1/topics/signals/) to automatically create/update the Profile model when we create/update User instances.


---


## Substituting a custom User model

We may have different authentication requirements for our Django project for which Django’s built-in User model may not be appropriate. For instance, we may need to use an email address as the identification token instead of a username.

If we want to use a custom User model for our project, we need to override the default user model by providing a value for the AUTH_USER_MODEL setting that references that custom model:

```python
# settings.py
#-------------

AUTH_USER_MODEL = 'myapp.MyUser'
```

>Notes :
>- It’s highly recommended to set up a custom user model when starting a new project, even if the default User model is sufficient for us. In this way we’ll be able to customize it in the future if the needed. Changing AUTH_USER_MODEL after we've created database tables is significantly more difficult and can’t be done automatically.
>- After changing the AUTH_USER_MODEL setting to a different user model, we should not reference the [**User**](https://docs.djangoproject.com/en/3.1/ref/contrib/auth/#django.contrib.auth.models.User) directly. Instead we should reference the user model with either [`get_user_model()`](https://docs.djangoproject.com/en/3.1/topics/auth/customizing/#django.contrib.auth.get_user_model) or `settings.AUTH_USER_MODEL` to get the currently active user model.
>- Reusable apps shouldn’t implement a custom user model.

There are two ways to create a custom user model in Django : **AbstractUser** and **AbstractBaseUser**

### 1) Custom User Model Extending AbstractUser :

##### What?
It is a new User model that inherit from AbstractUser class. AbstractUser is a full User model, complete with fields. We can inherit from it and add our own profile fields and methods.

##### When to use?
We should use it when we are perfectly happy with the default authentication process of Django and want to keep the default fields in the user model, yet we want to add some extra information directly in the User model without having to create an extra class. We can also change the username to a different field with minimal overhead.

> Note : AbstractUser actually subclasses AbstractBaseUser but provides more default configuration.

##### Code Example

```python
# app/models.py
# --------------

from django.db import models
from django.contrib.auth.models import AbstractUser

class BloggerUser(AbstractUser):
    # The model already has an email field, but we
    # need add here to add the unique=True Paremeter
    email = models.EmailField(unique=True) 
    bio = models.CharField(max_length=500)
    website = models.CharField(max_length=200)

    USERNAME_FIELD = 'email'
    REQUIRED_FIELD = ['website']
```

```python
# settings.py
# ----------------

AUTH_USER_MODEL = 'accounts.BloggerUser'
```

```python
# articles/models..py
# --------------------

from django.conf import settings
from django.db import models

class Article(models.Model):
    author = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.CASCADE,
    )
```

> Note : In the above example, We are still having username field. In most cases, we may want to remove the username field as we are using email as the identifier. This [blog post](https://www.fomfus.com/articles/how-to-use-email-as-username-for-django-authentication-removing-the-username) covers well how to do that. 

### 2) Custom User Model Extending AbstractBaseUser :

##### What?
This one is the most difficult option but gives the highest flexibility too. It is a new User model that inherit from AbstractBaseUser class. AbstractBaseUser only contains the authentication functionality, but no actual fields. We have to supply them when you subclass.

##### When to use?
We should use it when our application will have different requirements than the default authentication process and we want to start from scratch by creating our own, completely new User model.


##### Rules
While we inherit from the AbstractBaseUser, we have to follow some rules. Please follow the [offical doc](https://docs.djangoproject.com/en/3.1/topics/auth/customizing/#specifying-a-custom-user-model) to know more about the rules.

##### Code Example :

```python
# app/managers.py
# -----------------

from django.contrib.auth.base_user import BaseUserManager
from django.utils.translation import ugettext_lazy as _


class CustomUserManager(BaseUserManager):
    """
    Custom user model manager where identifier is the unique identifiers
    for authentication instead of usernames.
    """
    def create_user(self, identifier, password, **extra_fields):
        """
        Create and save a identifier with the given identifier and password.
        """
        if not identifier:
            raise ValueError(_('The identifier must be set'))
        user = self.model(identifier=identifier, **extra_fields)
        user.set_password(password)
        user.save()
        return user

    def create_superuser(self, identifier, password, **extra_fields):
        """
        Create and save a SuperUser with the given identifier and password.
        """
        extra_fields.setdefault('is_staff', True)
        extra_fields.setdefault('is_superuser', True)
        extra_fields.setdefault('is_active', True)

        if extra_fields.get('is_staff') is not True:
            raise ValueError(_('Superuser must have is_staff=True.'))
        if extra_fields.get('is_superuser') is not True:
            raise ValueError(_('Superuser must have is_superuser=True.'))
        return self.create_user(identifier, password, **extra_fields)
```

```python
# app/models.py
# ----------------

from django.contrib.auth.models import AbstractBaseUser
from django.db import models

from .managers import CustomUserManager


class BloggerUser(AbstractBaseUser):
    identifier = models.CharField(max_length=40, unique=True)
    website = models.CharField(max_length=100)
    is_staff = models.BooleanField(default=False)
    is_active = models.BooleanField(default=True)

    USERNAME_FIELD = 'identifier'

    objects = CustomUserManager()
```

```python
# settings.py
# ----------------

AUTH_USER_MODEL = 'app.BloggerUser'
```


## Resources :

- https://simpleisbetterthancomplex.com/tutorial/2016/07/22/how-to-extend-django-user-model.html
- https://medium.com/agatha-codes/options-objects-customizing-the-django-user-model-6d42b3e971a4
- https://testdriven.io/blog/django-custom-user-model/