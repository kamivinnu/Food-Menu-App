In this hands-on course, you will learn how to build complex web applications from scratch using Django.

The course will teach you Django, right from scratch from a very basic level and will gradually move towards advanced topics like authentication. 

The entire course is divided into 17 major sections.

Here is a brief description of what you will learn in each section of the course:

## Section 1: Introduction and installing required software.

In this section we will learn what Django is and why it is used. We will also install the tools you will need to start making Django web apps.

## Section 2: Setting up Django project:

In this section we will learn about setting up the Django project, using the development server.

## Section 3: Views & URL patterns in Django.

We learn about what the MVT (model-view-template) architecture by starting off by creating views in Django, we will also learn what URL patters are and how they help us to setup routes for our website.

## Section 4: Database & Models:

This section covers content about how to create models in Django and how models help us to create database tables.

## Section 5: Templates:

In this section will learn about templates in Django and how we can pass data from the database to Django templates.

## Section 6: Static Files & Site design:

This section will teach you how to use static content in your site such as static images, JavaScript etc and how to use these static elements to style up your web-page.

## Section 7: Forms.

Every Django app needs to submit data to the back-end, this section covers how to create forms in Django which allow us to perform basic CRUD operations i.e. create, read, update & delete.

## Section 8: Authentication in Django:

Every web-app needs to make sure that it provides a registration and login feature, in this section we learn exactly how to authenticate users on our site and log them in.

We will also learn how to password-protect certain webpages in Django.

## Section 9: Django signals, Class based views in Django:

This section covers Django signals and class based views in Django, which is an alternative to creating function based views.

## Section 10: REST APIs

In this section we will learn Django Rest Framework which helps us to create a REST API using Django for any Django web application.

## Section 11: Pagination, Search & User permissions.

Every modern web app needs advanced features like pagination, & search. We learn how to paginate out webpages and how to add search functionality to our webpages in Django. We also learn how to add user permissions to our Django models so that only a certain set of users on our app have access to certain models.



# Food-Menu-App

# 1 Create and Setup Django Project:
  1. Create Virtual env: For Windows : py -m venv env
  2. Activate ENV: .\env\Scripts\Activate
  3. Install Django: pip install django
  4. Start Project : django-admin startproject project_name . (mysite)
  5. Run Server : python manage.py runserver
  6. Create App : python manage.py startapp appname (food)

# Step 2: views and urls 
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

# Step 3: Databases and Models
### Models:
  1. Models are the blueprint where allows us to create database tables.
  2. Models are the Classes of python.
class Item(models.Model):
    item_name = models.CharField(max_length = 200)
    item_desc = models.CharField(max_length = 200)
    item_price = models.IntegerField()
  3. Configure Apps in -Installed Apps- in settings file - 'food.apps.FoodConfig'

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

# Step 4:  Templates
Templates allows us to create HTML
Template - Simple HTML File
## 4.1 Django Templates
  1. Django Template Engine
  2. Open Setting.py and you can see templates
  3. create templates directory in food app
  4. Inside templates directory - create food directory
  5. Inside Food Directory - create HTML file as index.html
  6. In index.html - body -> <h1>This is my template</h1>
  7. open views.py - from django.template import loader
  8. In user def -     template = loader.get_template('food/index.html')
  9. def index(request):
      item_list = Item.objects.all()
      template = loader.get_template('food/index.html')
      context = {

      }
      return HttpResponse(template.render(context, request))
## 4.2 Passing Context to Template
  1. context = {
        'item_list':item_list, (comma compulsory)
    }
  2. clear index.html and add
  3.   {% for item in item_list %}
        {{ item.id }} -- {{ item.item_name }}
      {% endfor %}
  4. The above is uneasy, instead we use
  5. {% for item in item_list %}
    
      <ul>
        <li>
            {{ item.id }} -- {{ item.item_name }}
        </li>
      </ul>
      {% endfor %}
  6. change - return HttpResponse(template.render(context, request))
  7. update - return render(request, 'food/index.html', context)
  8. using render function is very efficient

## 4.3 Creating the detail view
  1. whenever we click on pizza, it has to open a new page in detail.
  2. to do that we have to open views file and create def detail.
  3. def detail(request,item_id):
      return HttpResponse(f"This is Item no/id : {id}")
  4. In urls of app, add
  5. def detail(request,item_id):
      return HttpResponse(f"This is Item no/id : {item_id}")
## 4.4 Completing the detail view
  1. create detail.html in templates\food
  2. In detail.html
  3. <h1>{{ item.item_name }}</h1>
      <h2>{{ item.item_desc }}</h2>
      <h3>{{ item.item_price }}</h3>
  4. open and add render func for efficient purpose
  5. def detail(request,item_id):
        item = Item.objects.get(pk = item_id)
        context = {
          'item':item,
        }
        return render(request, 'food/detail.html', context)
  6. Now we create hyper links to dirctly access the page
  7. open index.html and add
  8. {% for item in item_list %}
    
      <ul>
        <li>
            
            <a href="/food/{{ item.id }}">{{ item.id }} -- {{ item.item_name }}</a>
        </li>
      </ul>
    {% endfor %}

## 4.5 Django Template Language
  1. Template engine? - Jinja2 - templating engine; Django's Default engine - Django Template Language[DTL]

## 4.6 Removing Hardcoded URLS
  1. In indx.html commit
  2. {% for item in item_list %}
    
      <ul>
        <li>
            
            <!-- <a href="/food/{{ item.id }}">{{ item.id }} -- {{ item.item_name }}</a> -->
            
            <a href="{% url 'detail' item.id %}">{{ item.id }} -- {{ item.item_name }}</a>
        </li>
      </ul>
      {% endfor %}

## 4.7 NameSpacing
  1. Multiple apps with same views name.
  2. To avoid confusion , we have to define namespacing for each apps used in urls
  3. app_name = 'food'
      urlpatterns = [ ]
  4. open index.html and add
  5. <a href="{% url 'food:detail' item.id %}">{{ item.id }} -- {{ item.item_name }}</a>

# 5. Static files and Site Design

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
