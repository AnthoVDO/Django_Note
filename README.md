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
### Create super user  
```python manage.py createsuperuser```
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
### Link many to one  
First import the classes  
Assign the field with the foreign key with the object (we assign an author to a blogpost here)
```
my_blog_post = BlogPost.objects.get(pk=1)
my_user = User.objects.get(pk=1)
my_blog_post.author = my_user
my_blog_post.save()
```  
### Link many to many  
First import the classes  
Use the set method to assign a list of value (we assign multiple category for an article here)  
```
my_blog_post = BlogPost.objects.get(pk=1)  
cat_python = Category.objects.get(slug="python")
cat_django = Category.objects.get(slug="django")
my_blog_post.category.set([cat_python, cat_django])
```
Note: Set with erase the other data, to keep them and add one, use add instead of set  
```my_blog_post.category.add([cat_javascript])```  
Note2: with add and set, no need to use save();  
Note3: Can use remove to remove one or more and clear to remove all
## Models  
### Overload the save method  
Used to make operation while saving. Here, we create the slug according to the title  
```
from django.db import models
from django.utils.text import slugify


# Create your models here.
class BlogPost(models.Model):
    title = models.CharField(max_length=100)
    slug = models.SlugField()
    published = models.BooleanField(default=False)
    date = models.DateField(blank=True, null=True)
    content = models.TextField()
    description = models.TextField()  
    
    # Used to avoid to put the () in the end example: BlogPost.published_string instead of BlogPost.published_string()
    @property # It says that it's a property instead of a method  
    def published_string(self):
        if self.published:
            return "The article is published"  
        return "The article isn't published" 

    def save(self, *args, **kwargs): # Overload the save method

        if not self.slug:
            self.slug = slugify(self.title)

        super().save(*args, **kwargs)
 ```
### Many to One  
```author = models.ForeignKey(User, on_delete=models.SET_NULL, null=True)```  
Need to use the ForeignKey method and in this method, need to add the class with the relation (User here) and specify the action if a user is deleted (Set to null here so also need to set null to True)  
### Many to Many  
```category = models.ManyToManyField(Category)```  
### Example  
```
class BlogPost(models.Model):
    author = models.ForeignKey(User, on_delete=models.SET_NULL, null=True) # Set a user foreign key. The on_delete is present to inform how to manage the article if the user is deleted. Here, we decided to set it to NULL
    category = models.ManyToManyField(Category) # Set the possibility to add multiple categories to a BlogPost
    title = models.CharField(max_length=100)
    slug = models.SlugField()
    published = models.BooleanField(default=False)
    date = models.DateField(blank=True, null=True)
    content = models.TextField()
    description = models.TextField()  
    
    # Used to avoid to put the () in the end example: BlogPost.published_string instead of BlogPost.published_string()
    @property # It says that it's a property instead of a method  
    def published_string(self):
        if self.published:
            return "The article is published"  
        return "The article isn't published" 

    def save(self, *args, **kwargs): # Overload the save method

        if not self.slug:
            self.slug = slugify(self.title)

        super().save(*args, **kwargs)
```


