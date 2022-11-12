## DJANGO REST

### SETUP DJANGO REST
#### INSTALLATION
Create Folder
```
$mkdir flipbook
$cd flipbook
$pipenv shell
$pipenv install django
```
Install Django Rest Framework
```
$pipenv install djangorestframework
$pipenv install markdown
$pipenv install django-filter
```
Create Project
```
$django-admin startproject flipbook .
```
Create Project Base folder
```
flipbook/flipbook/settings.py
 INSTALLED_APPS = [
  rest_framework,
  flipbook
 ]
 ```
 ```
flipbook/flipbook/urls.py
from django.contrib import admin
from django.urls import path, include
urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('api.urls'))
]
```
Create app
```
$python manage.py startapp api
 
flipbook/flipbook/settings.py
INSTALLED_APPS = [
  rest_framework,
  flipbook,
  api
 ]
 ```
 ```
flipbook/api/urls.py
from django.urls import path, include
from . import views
urlpatterns = [
    path('apiOverview/', views.apiOverview, name="apiOverview")
]
```
```
flipbook/api/views.py
from rest_framework.decorators import api_view
from rest_framework.response import Response
@api_view(['GET'])
def apiOverview(request):
    api_url = {
            'Test' : '',
    }
    return Response(api_url)
```
```
flipbook/api/models.py
from django.db import models
class Flipbooks(models.Model):
    filelink = models.CharField(max_length=255)
    updated = models.DateTimeField(auto_now=True)
    created = models.DateTimeField(auto_now_add=True)
    def __str__(self):
        return self.filelink
```
```
$python manage.py makemigrations
  - this will run latest migrations
$python manage.py migrate
  - this will apply latest migrations
```
Setup StaticFiles
```
$cd flipbook
$mkdir staticfiles && chmod 775 staticfiles
```
```
flipbook/flipbook/settings.py
INSTALLED_APPS = [
  'django.contrib.staticfiles'
]
STATIC_URL = '/staticflies/'
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, 'staticfiles/bootstrap_album') #mapping location of directories
]
STATIC_ROOT = os.path.join(BASE_DIR, "staticfiles") #set where collectstatic copy and put the files
```
Collect StaticFiles
```
$cd flipbook
$python manage.py collectstatic
```
Access Rest Framework
```
$cd flipbook
$python manage.py runserver 8585
http://127.0.0.1:8585/apiOverview/
```
