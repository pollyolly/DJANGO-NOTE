# storefront
DJango Sample Project
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
```

