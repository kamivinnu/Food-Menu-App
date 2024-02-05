# Food-Menu-App

## Create and Setup Django Project:
  1. Create Virtual env: For Windows : py -m venv env
  2. Activate ENV: .\env\Scripts\Activate
  3. Install Django: pip install django
  4. Start Project : django-admin startproject project_name .
  5. Run Server : python manage.py runserver
  6. Create App : python manage.py startapp appname
## Step 2: views and urls 
### Views:
  1. def index(request):
       return HttpResponse("Hello World")
  2. from django.http import HttpResponse
  3. To view this hello world in our browser, we have to create urls.py file in app

### urls in app:
  1. urlpatterns = path['',]
  2. To define views in urls,
  3. from . import views
      from django.urls import path
  4. urlpatterns = path['', views.index, name = 'index']
  5. Add URLS of Project :
       path('food', include('food.urls'),

### Databases and Models
### Models:
  1. Models are the blueprint where allows us to create database tables.
  2. Models are the Classes of python.
class Item(models.Model):
    item_name = models.CharField(max_length = 200)
    item_desc = models.CharField(max_length = 200)
    item_price = models.IntegerField()
  3. Configure Apps in Installed Apps in settings file - 'food.app.FoodConfig'

## Changes to Djnago:
  1. python manage.py makemigrations food
## To create Database Table:
  1. python manage.py sqlmigrate food 0001
  2. python manage.py migrate
## Steps Invovled in adding the data to database
  1. Database Abstruction API - create, update, delete ---- Object
  2. Adding the data to database
  3. python manage.py shell
  4. from food.models import Item
  5. to see the data in the Item - type- Item.objects.all()
  6. a = Item(item_name = 'Pizza', item_desc = 'cheese pizza', item_price = 20)
  7. a.save()
  8. a.id or a.pk
  9. b = Item(item_name = 'Burger', item_desc = 'Cheesy  burger', item_price = 25)
  10. b.save()
  11. b.id or b.pk
  12. Item.objects.all()
  13. to view
  14. def __str__(self):
        return self.item_name
  15. The above should write in models.py file
  16. exit()
  17. This process is time consuming and length to write.
  18. Soo for this django have admin panel - create super user account

## Django Admin Panel- Super User Account
  1. python manage.py createsuperuser
  2. Open the Development Server
  3. Add Admin/
  4. We cannot find a Item Database
  5. To do this, open admin.py file to register models.py
  6. admin.site.register(Item)
  7. from.models import Item
  8. Refresh

## retrieve Data from Database
  1. Open Views.py
  2. from .models import Item
  3. item_list = Item.objects.all() in item user defined function
  4. return HttpResponse(item_list)
  5. open new tab after viewing
  6. In new tab open admin and add data
  7. Come back to previous tab and refresh
  8. To add layout to the page, we use templates

## Templates

# Django Introduction
## What is Django?
Django is a Python framework that makes it easier to create web sites using Python.

Django takes care of the difficult stuff so that you can concentrate on building your web applications.

Django emphasizes reusability of components, also referred to as DRY (Don't Repeat Yourself), and comes with ready-to-use features like login system, database connection and CRUD operations (Create Read Update Delete).

Django is especially helpful for database driven websites.

## How does Django Work?
Django follows the MVT design pattern (Model View Template).

Model - The data you want to present, usually data from a database.
View - A request handler that returns the relevant template and content - based on the request from the user.
Template - A text file (like an HTML file) containing the layout of the web page, with logic on how to display the data.

### Model
The model provides data from the database.

In Django, the data is delivered as an Object Relational Mapping (ORM), which is a technique designed to make it easier to work with databases.

The most common way to extract data from a database is SQL. One problem with SQL is that you have to have a pretty good understanding of the database structure to be able to work with it.

Django, with ORM, makes it easier to communicate with the database, without having to write complex SQL statements.

The models are usually located in a file called models.py.

### View
A view is a function or method that takes http requests as arguments, imports the relevant model(s), and finds out what data to send to the template, and returns the final result.

The views are usually located in a file called views.py.

### Template
A template is a file where you describe how the result should be represented.

Templates are often .html files, with HTML code describing the layout of a web page, but it can also be in other file formats to present other results, but we will concentrate on .html files.

Django uses standard HTML to describe the layout, but uses Django tags to add logic:

<h1>My Homepage</h1>

<p>My name is {{ firstname }}.</p>
The templates of an application is located in a folder named templates.

### URLs
Django also provides a way to navigate around the different pages in a website.

When a user requests a URL, Django decides which view it will send it to.

This is done in a file called urls.py.

## When you have installed Django and created your first Django web application, and the browser requests the URL, this is basically what happens:

  1. Django receives the URL, checks the urls.py file, and calls the view that matches the URL.
  2. The view, located in views.py, checks for relevant models.
  3. The models are imported from the models.py file.
  4. The view then sends the data to a specified template in the template folder.
  5. The template contains HTML and Django tags, and with the data it returns finished HTML content back to the browser.
Django can do a lot more than this, but this is basically what you will learn in this tutorial, and are the basic steps in a simple web application made with Django.
