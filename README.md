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
#### Apply migration  
```python manage.py migrate```  
## APP  
### Create an app  
```python manage.py startapp <app name>```

  
