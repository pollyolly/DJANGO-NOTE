## DJANGO REST

### SETUP DJANGO
#### INSTALLATION
```
$mkdir flipbook
$cd flipbook
$pipenv shell
$pipenv install django

$pipenv install djangorestframework
$pipenv install markdown
$pipenv install django-filter

//Create Project
$django-admin startproject flipbook .

//Create Project Base folder
flipbook/flipbook/settings.py
 INSTALLED_APPS = [
  rest_framework,
  flipbook
 ]

//Create app
$python manage.py startapp api
 
flipbook/flipbook/settings.py
INSTALLED_APPS = [
  rest_framework,
  flipbook,
  api
 ]
 

```
