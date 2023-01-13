# DJANGO Note
DJango Sample Project 
```
source yt: https://www.youtube.com/watch?v=rHux0gMZ3Eg
articles: https://django.fun/
```
### Django Tutorials
[Django NginX Gunicorn Postgres](https://www.digitalocean.com/community/tutorials/how-to-set-up-django-with-postgres-nginx-and-gunicorn-on-ubuntu-20-04)

[Setup Django NginX Gunicorn Postgres](https://arctype.com/blog/install-django-ubuntu/)
```
https://realpython.com/customize-django-admin-python/
https://books.agiliq.com/projects/django-admin-cookbook/en/latest/export.html
https://www.youtube.com/watch?v=fx80N0eQOos&list=PLlM3i4cwc8zBRQOGXuLrCLNfpVOuVLuwZ&index=7
https://medium.com/@jacobtamus/deploying-django-rest-mariadb-gunicorn-supervisor-nginx-on-centos-7-linux-990ca877e72b
https://www.youtube.com/watch?v=lgK238BvuL0
https://preneure.com/the-ultimate-django-cheat-sheet/
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
$mkdir djangoblog
$cd djangoblog
$pipenv shell
$pipenv install django
  - install django in virtual environment
```
### pip files modules generate
```
$pipenv shell
$cd djangoblog
$pipenv run pip freeze requirements.txt
$vi Pipfile - just like package.json where application dependencies are written. django="*" (latest or any version of django)
```
### pip list
```
$pip list - check django installed modules
```
### pipenv list ###
```
$pipenv run pip freeze requirements.txt
```
### Activate Virtual Environment to use python interpreter inside not globally
```
$cd djangoblog
$pipenv shell
 -you always need to do this when accessing the project after exit the project
```
### Install Requirements
```
$pip3 install -r requirements.txt

Note: Manual install the module if conflicting.
$pip3 install <module>
```
### Postgre Client
[Doc](https://www.psycopg.org/install/)

[Failed install psycopg](https://stackoverflow.com/questions/34304833/failed-building-wheel-for-psycopg2-macosx-using-virtualenv-and-pip)
```
// Update if Failed to install
$cd djangoblog
$pip list --outdated
$pip install --upgrade wheel
$pip install --upgrade setuptools
```
```
$sudo apt install python3-dev libpq-dev
$pip install psycopg2
```
```
settings.py
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'OPTIONS': {
            'service': 'my_service',
            'passfile': '.my_pgpass',
        },
    }
}
```
```
pg_service.conf
[my_service]
host=localhost
user=USER
dbname=NAME
port=5432
```
```
.my_pgpass
localhost:5432:NAME:USER:PASSWORD
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
$cd djangoblog
$django-admin startproject djangoblog .
  -dot (.) means it will the use existing folder and will not create new storefront folder.
  
 
 settings.py
 INSTALLED_APPS = [
  djangoblog //Created Apps are Added here
 ]
```
### Run Django Project
```
$cd djangoblog
$python manage.py runserver <custom port number; default 8000>
```
### Check Pipe python interpreter path
```
$cd djangoblog
$pipenv --venv
   -can be used in vscode to setup the python interpreter (vscode used the default python interpreter installed globally)
   result: /root/.local/share/virtualenvs/djangoblog-6hn45Vis
   to add in vscode: /root/.local/share/virtualenvs/djangoblog-6hn45Vis/bin/python
```
### Creating New App (Take Note Django is a collection of App like modular in mind)
```
$cd djangoblog
$python manage.py startapp blogpost
```
### Django Debug Toolbar
```
https://django-debug-toolbar.readthedocs.io/en/latest/installation.html

$pipenv install django-debug-toolbar
$cd djangoblog
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
### Django Static Files Deployment
```
settings.py
INSTALLED_APPS = [
  'django.contrib.staticfiles'
]
STATIC_URL = '/staticflies/'
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, 'staticfiles/bootstrap_album') #mapping location of directories
]
STATIC_ROOT = os.path.join(BASE_DIR, "staticfiles") #set where collectstatic copy and put the files
```
```
templating
{% load static %}

<link href="{% static 'bootstrap.min.css' %}" rel="stylesheet">
```
```
$cd djangoblog
$mkdir staticflies
$python manage.py collectstatic
```
### Django Media Files
```
settings.py
MEDIA_URL = '/uploaded_files/'
MEDIA_ROOT = os.path.join(BASE_DIR, "")

TEMPLATES = [
    {
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.media' #To access media files {{MEDIA_URL}}
            ],
        },
    },
]
```
```
templating
<img width="100%" height="225" src="{{ MEDIA_URL }}{{post.thumbnail }}">
```
```
main application urls.py

from django.conf import settings
from django.conf.urls.static import static
urlpatterns = [
  
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
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
### Django Gunicorn
```
$cd djangoblog
$pipenv shell
$pipenv install gunicorn
Test Gunicorn if works inside pipenv
$gunicorn --bind 0.0.0.0:8000 djangoblog.wsgi:application 
```
### Django NGINX
```
$apt install nginx
```
## Django NGINX Deployment
Gunicorn Service (wsgi)
```
# $touch gunicorn.socket
# /etc/systemd/system/gunicorn.socket
[Unit]
Description=gunicorn socket

[Socket]
ListenStream=/run/gunicorn.sock

[Install]
WantedBy=sockets.target
```
```
# $touch gunicorn.service
#/etc/systemd/system/gunicorn.service

[Unit]
Description=gunicorn daemon
Requires=gunicorn.socket
After=network.target

[Service]
User=root
Group=www-data
WorkingDirectory=/var/www/html/djangoblog
#Path To Virtual Env (pipenv install gunicorn)
ExecStart=/root/.local/share/virtualenvs/djangoblog-B6XojO9L/bin/gunicorn \
          --access-logfile - \
          --workers 3 \
          --bind unix:/run/gunicorn.sock \
          djangoblog.wsgi:application

[Install]
WantedBy=multi-user.target
```
Run gunicorn socket
```
$sudo systemctl start gunicorn.socket
$sudo systemctl enable gunicorn.socket
```
Check Status
```
$sudo systemctl status gunicorn.socket
```
 Check File (Automatically created)
```
$file /run/gunicorn.sock
```
Check activate gunicorn
```
$curl --unix-socket /run/gunicorn.sock localhost

$sudo systemctl status gunicorn
```
Daphne Service (asgi)
```
# $touch daphne.service
#/etc/systemd/system/daphne.service

[Unit]
Description=WebSocket Daphne Service
After=network.target

[Service]
Type=simple
User=root
Group=www-data
WorkingDirectory=/var/www/html/djangoblog
ExecStart=/root/.local/share/virtualenvs/djangoblog-B6XojO9L/bin/python /root/.local/share/virtualenvs/djangoblog-B6XojO9L/bin/daphne -b 0.0.0.0 -p 8991 djangoblog.asgi:application
Restart=on-failure

[Install]
WantedBy=multi-user.target
```
Start/Restart Daphne Service
```
systemctl daemon-reload
systemctl start daphne.service
systemctl status daphne.service
```
```
#/etc/nginx/sites-available/djangoblog
upstream django-websocket {
        server 127.0.0.1:8991;
}

server {
        listen 80;
        listen [::]:80;

        server_name djangoblog.iwebitechnology.xyz *.djangoblog.iwebitechnology.xyz;
        return 301 https://djangoblog.iwebitechnology.xyz$request_uri;
}

server {
        listen 443 ssl;

        server_name djangoblog.iwebitechnology.xyz *.djangoblog.iwebitechnology.xyz;

        #root /var/www/html/djangoblog;
        #index index.html;

        access_log /var/log/nginx/djangoblog_access.log;
        error_log  /var/log/nginx/djangoblog_error.log debug;

        #RSA certificate
        ssl_certificate /etc/letsencrypt/live/djangoblog.iwebitechnology.xyz/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/djangoblog.iwebitechnology.xyz/privkey.pem;


        include /etc/letsencrypt/options-ssl-nginx.conf;

        location /staticfiles/ {
                root /var/www/html/djangoblog;
        }
        location / {
                include proxy_params;
                proxy_pass http://unix:/run/gunicorn.sock;
        }
        location /ws/ {
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header Host $http_host;
                proxy_http_version 1.1;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection "upgrade";
                proxy_pass http://django-websocket;
        }
}
```
