# django rest_framework 설정 (window)

---

- *cmd*

```
cd C:\Users\user\Desktop\workspace
pip install django
django-admin startproject django_rest
cd django_rest
python -m venv --copies venv
```

- *settings*

![](C:\Users\user\Desktop\md\django rest_framework 설정\설정1.JPG)

File->Settings->Build, Execution, Deployment->Console->Python ConsoleEnvironment variables: **DJANGO_SETTINGS_MODULE=django_rest.settings**

*Starting script에 아래 두 라인 추가*

```
import django
django.setup()
```

- *터미널*

```
python -m django --vesion
pip install django
pip install djangorestframework
pip install pygments
pip list
python manage.py runserver
```



- *Run/Debug Configurations*

Script path: (manage.py 찾아서 지정)

Parameters: runserver 8001



- *app 만들기*

```
python manage.py startapp snippets
```

django_rest>settings.py

installes_app=[]에

```
'rest_framework',
'snippets.apps.SnippetsConfig',
```

추가하기





이후 models.py, serializer.py, views.py, urls.py 작업