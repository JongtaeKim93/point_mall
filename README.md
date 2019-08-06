# django rest_framework 설정 (window)

- **cmd**

```
cd C:\Users\user\Desktop\workspace
pip install django
django-admin startproject django_rest
cd django_rest
python -m venv --copies venv
```



- **settings**

> File->Settings->Build, Execution, Deployment->Console->Python ConsoleEnvironment variables: **DJANGO_SETTINGS_MODULE=django_rest.settings**

> *Starting script에 아래 두 라인 추가*
>
> ```
> import django
> django.setup()
> ```



- **터미널**

```
python -m django --vesion
pip install django
pip install djangorestframework
pip install pygments
pip list
python manage.py runserver
```



- *Run/Debug Configurations*

> Script path: (manage.py 찾아서 지정)
>
> Parameters: runserver 8001



- *app 만들기*

```
python manage.py startapp snippets
```

> django_rest>settings.py
>
> installes_app=[]에
>
> ```python
> 'rest_framework',
> 'snippets.apps.SnippetsConfig',
> ```

추가하기



이후 models.py, serializer.py, views.py, urls.py 작업



---

# 새로 내려받아서 작업한다면

clone 내려받고

**cmd**

> 해당경로로 이동해서

```
python -m venv --copies venv
```



**pycharm**

> File-Settings- 1.Project Interpreter 확인
>                         2.Build,Execution,Deployment-Console-Python Console

> Configurations - runserver 설정

> 패키지 설치
>
> ```
> pip install -r requirements.txt
> ```
>
> 패키지 관리하려면
>
> ```
> pip freeze > requirements.txt
> ```



***

# models, serializers, views, urls 작성요령

**model.py**

```python
from django.db import models

class Item(models.Model):
    title = models.CharField(max_length=100)
    description = models.TextField()
    created = models.DateTimeField(auto_now_add=True)
    price = models.IntegerField(default=0)
    image = models.ImageField(upload_to='uploads/item_images/')
```

> 데이터베이스에 어떤 속성들이 들어갈지 정의

**serializers.py**

```python
from rest_framework import serializers
from .models import Item


class ItemSerializer(serializers.ModelSerializer):
    class Meta:
        model = Item
        fields = ['id', 'title', 'description', 'created', 'price', 'image']
```

> 어떤 값을 보여줄지 정의

**views.py**

```python
from rest_framework import viewsets

from .models import Item
from .serializers import ItemSerializer


class ItemViewSet(viewsets.ModelViewSet):
    queryset = Item.objects.all()
    serializer_class = ItemSerializer
```

> 

**urls.py**

```python
from rest_framework.routers import DefaultRouter
from django.urls import path, include

from item import views


router = DefaultRouter()
router.register('', views.ItemViewSet)

urlpatterns = [
    path('', include(router.urls))
]
```

**root>urls.py**

```python
from django.urls import path, include

urlpatterns = [
    path('items/', include(item.urls')),
]
```