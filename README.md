# DJANGO Note
DJango Sample Project 
```
source yt: https://www.youtube.com/watch?v=rHux0gMZ3Eg
```
### Django Tutorials
```
https://realpython.com/customize-django-admin-python/
https://books.agiliq.com/projects/django-admin-cookbook/en/latest/export.html
https://www.digitalocean.com/community/tutorials/how-to-set-up-django-with-postgres-nginx-and-gunicorn-on-ubuntu-18-04#step-3-creating-a-python-virtual-environment-for-your-project
```
## DJango Project
### Install basic requirements
### Check python version
```
check python version
$python3 --version
```
### Install pip3
```
$pip3 install pipenv
  - dependency management tool to install python dependencies in 
               virtual environment to prevent clash with other dependencies.
```
### Install django in the project
```
$mkdir storefront
$cd storefront
$pipenv install django
  - install django in virtual environment
```
### pip3 files
```
$cd storefront
$vi Pipfile - just like package.json where application dependencies are written. django="*" (latest or any version of django)
```
### Activate Virtual Environment to use python interpreter inside not globally
```
$cd storefront
$pipenv shell
 -you always need to do this when accessing the project after exit the project
```
### MySQL Client
```
$pip install pymysql

Edit __init__.py in main application

import pymysql
pymysql.install_as_MySQLdb()

Edit settings.py in main application

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'djangoblog',
        'USER': 'django',
        'PASSWORD': 'Iamdjangouser23',
        'HOST': 'localhost',
        'PORT': '3306'
    }
}
```
### Start django new project
```
$cd storefront
$django-admin startproject storefront .
  -dot (.) means it will the existing folder and will not create new storefront folder.
```
### Run Django Project
```
$cd storefront
$python manage.py runserver <custom port number; default 8000>
```
### Check Pipe python interpreter path
```
$cd storefront
$pipenv --venv
   -can be used in vscode to setup the python interpreter (vscode used the default python interpreter installed globally)
   result: /root/.local/share/virtualenvs/storefront-6hn45Vis
   to add in vscode: /root/.local/share/virtualenvs/storefront-6hn45Vis/bin/python
```
### Creating New App (Take Note Django is a collection of App like modular in mind)
```
$cd storefront
$python manage.py startapp playground
```
### Django Debug Toolbar
```
https://django-debug-toolbar.readthedocs.io/en/latest/installation.html

$pipenv install django-debug-toolbar
$cd storefront
$vi settings.py
    INSTALLED_APPS = [
      'debug_toolbar'
    ]
    MIDDLEWARE = [
      'debug_toolbar.middleware.DebugToolbarMiddleware'
    ]
    INTERNAL_IPS = [
    # ...
      "127.0.0.1",
    # ...
    ]
$vi urls.py
    from django.urls import path, include
    import debug_toolbar
    urlpatterns = [
      path('_debug_/', include(debug_toolbar.urls))
    ]
```
### Django Models and Migrations
```
After  editing models.py
$python manage.py makemigrations
  - this will run latest migrations
$python manage.py migrate
  - this will apply latest migrations

```
### Django Create Super User
```
$python manage.py createsuperuser
   - this will create admin account fro django default admin login form
```
