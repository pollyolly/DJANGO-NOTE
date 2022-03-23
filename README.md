# storefront
DJango Sample Project 
source yt: https://www.youtube.com/watch?v=rHux0gMZ3Eg
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
$cd python manage.py startapp playground
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
$vi urls.py
    path('_debug_/', include(debug_toolbar.urls))
```
