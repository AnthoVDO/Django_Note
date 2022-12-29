# Django_Note  
## Create  
### Create .env  
```py<version> -m venv .env```
### Go to .env
```source .env/scripts/activate```
### Install Django  
```pip install django==<version>```
### Add requirement.txt  
```pip freeze > requirements.txt```  
### Check requirements file  
```cat requirements.txt```   
### Install dependecy from requirements.txt  
```pip install -r requirements.txt```
### Create project  
```djando-admin startproject <folder name>```
### Rename folder to src
```
|- website/  
  |- .env  
  |- src/  
    |- website/  
    |- manage.py  
```  
### Run server  
```cd src```
```python manage.py runserver```
### Create app   
```
```

## Database  
### Migration  
### Create migration  
```python manage.py makemigrations <app name>```  
```python manage.py makemigrations #For all the apps```  
### See the SQL migration  
This is only to see what will happen to the database  
```python manage.py sqlmigrate <app name> <migration name without extension>```  
### Apply migration  
```python manage.py migrate #For all the apps```  
```python manage.py migrate <app name>```  
### Difference between blank and null  
```with blank= false => possible to keep it empty with python and not a form ```  
```with null= false => not possible to keep it empty because it is acting on the database side```  

## APP  
### Create an app  
```python manage.py startapp <app name>```

## SHELL  
### Move to the shell that know django info  
```python manage.py shell```  
### Import a model  
```from <app>.models import <model name>```  
Can also add the informations with a software like table plus, ...  
## Queries  
Ref: [Django making queries](https://docs.djangoproject.com/en/4.1/topics/db/queries/)



