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
### Import  
```from blog.models import Blog```
### Create  
```
    b = Blog(name="test", content="test content")
    b.save();
```  
or  
```Blog.objects.create(name="test", content="test content")```  
No need to use save() with object method  
### Get all  
```Blog.objects.all()```  
### Get one (return error if more than 1 or not found)  
```Blog.objects.get(name="test") #Can add multiple fields``` 
Note: As is should be unique, it's better to use the primary key (pk=). If the primary key is that same as id, we can use id=  
### Get all object according to filter  
```Blog.objects.filter(published=True)```  
or  
```Blog.objects.filter(date_year="2022").filter(published=True)```  
or  
```Blog.objects.filter(date_year="2022", published=True)```  
or  
```Blog.objects.filter(date_year="2022").exclude(published=True)```  
### Modify  
Get the row in a variable, modify it (ex: ```b.content = "some text"```) and save   
### Delete all  
```Blog.objects.all().delete()```  
### Delete one  
```Blog.objects.all()[0].delete() # Delete at first position```  
```Blog.objects.all()[5:10].delete() #Delete from 5 to article number 10```  
```Blog.objects.get(pk=1).delete()```



