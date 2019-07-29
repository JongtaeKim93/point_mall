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

>?

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

