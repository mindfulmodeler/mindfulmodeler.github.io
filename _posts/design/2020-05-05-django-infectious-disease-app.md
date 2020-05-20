---
layout: page
# sidebar: left
subheadline: 
title: "Creating a Web Application for Infectious Disease Modeling"
teaser: "Django makes it easy to create a seemingly complex web application with minimal setup."
breadcrumb: true
tags:
    - django
    - infectious disease
    - health
    - article
    - python
categories:
    - tutorial
header:
    image_fullwidth: "/covid-unsplash.jpg"
show_meta: true
comments: true
---
In this tutorial, we'll be building an infectious diesease web application from scratch. Doing this in the python framework Django is advantageous for many reasons: 
  1. Python is a powerful, easy-to-learn language. If you're new to programming, Python is an awesome general-purpose language that can allow you do everything from machine learning and data science to building custom web applications. 
  2. The combination of Python's enormous StackOverflow support community and Django's extensive documentation means you'll be able to google answers to virtually any problem you run into.
  3. Anything you read about Django will mention its "parts included" or "out-of-the-box functionality". What this means for you is that you can start seemingly small projects that are going to include cool features like security and authorization, and over time you're project will scale really well. 

<div class="panel radius" markdown="1">
**Table of Contents**
{: #toc }
*  TOC
{:toc}
</div>

#### Tools I'll be using:
1. <span style="color:hotpink">**Anaconda**</span>. Not only is conda a user-friendly package manager, it also makes it very easy to create and work with virtual environments.  
2. <span style="color:hotpink">**PostgreSQL**</span>. Some people prefer to stick with the lightweight SQLite for simple web applications. I prefer to start with postgres here because of its powerful ability to scale out projects over time and for its useful geospatial extensions. 
3. <span style="color:hotpink">**Django**</span>. While more heavyweight than alternative python frameworks like Flask, I feel more comfortable with Django's robustness and supporting tools for complex tasks. 
4. <span style="color:hotpink">**GraphQL**</span>. Most Django tutorials will naturally lead you into creating a REST API Framework, but this tutorial provides an alternative GraphQL endpoint using the django_graphene package. 

Also, please note that I'm writing this from the perspective of a Windows 10 user. Other OS's will have slightly different commands. 

![get started in django quickly]({{site.baseurl}}/images/lets-do-this.jpg) 

# Create a New Conda Virtual Environment
Begin by opening a new Anaconda Prompt window. If you haven't already installed anaconda on your local machine, now is a good time to do so (I have a post on [Getting Started With Python ASAP]({{site.baseurl}}/snips/easy-peasy-conda-jupyter-setup/) for more details). 

![open new anaconda prompt]({{site.baseurl}}/images/new-anaconda-prompt.jpg){: .shadow}

Inside the new prompt, you'll see your current environment and working directory, something like: ```(base) C:\Users\mindfulmodeler```. The most basic way of creating a new conda environment is by following this syntax:

{% highlight ruby %}
conda create --name djangoenv
{% endhighlight %}

This synatx tells conda that we want to create a new environment with the name *djangoenv*. Keep in mind that you can name your environment <span style="color:hotpink">**anything you want**</span>, so feel free to replace *djangoenv* with your own variation. 

After creating an environment, the next step is to install all the packages you want inside of that environment. You can do that in two separate steps, but it's often nice to create the environment with it's packages all in one go:

{% highlight ruby %}
conda create --name djangoenv pandas numpy django psycopg2
{% endhighlight %}

![activate new conda environment]({{site.baseurl}}/images/activate-new-conda-env.jpg)


And then we can activate the newly created environment as the instructions tell us:

{% highlight ruby %}
conda activate djangoenv
{% endhighlight %}

If there are any additional packages we forgot to install earlier, it's easy enough to do using `conda install <insert-packagename>`.

<!-- {% highlight ruby %}
conda install psycopg2
{% endhighlight %} -->

We also need to add the package [graphene-django](https://docs.graphene-python.org/projects/django/en/latest/). In this case, however, we also need to add a `-c conda-forge` prefix before the package name, which indicates that we're getting it from an alternative source. This happens sometimes, as a subset of packages (like graphene-django) aren't available via the default anaconda channel.

{% highlight ruby %}
conda install -c conda-forge graphene-django
{% endhighlight %}

The [anaconda documentation](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-with-commands) is a great, easy-to-read reference for more commands related to virtual environment setup and package installation. And remember - if you're unsure about what channel you should install an anaconda package from, just Google it! If a package really isn't available anywhere in conda though, you can always use `pip install` instead (yes you can use pip inside a conda environment, but I'd advise only doing it as a last resort to avoid conflicts).

![conda-forge install package]({{site.baseurl}}/images/conda-install-package.jpg)


## Creating a Django project
I'm going to create a new django project by loosely following the official tutorial. You can checkout the [official Django documentation](https://docs.djangoproject.com/en/3.0/intro/tutorial01/) or follow along with this condensed example to create your own web application. 

{% highlight ruby %}
#1. Start a new project called "healthsite"
django-admin startproject healthsite     

#2. Change directory into the newly created project
cd healthsite   

#3. Inside of this project, create a new app "diseaseapp"
python manage.py startapp diseaseapp  

#4. Runserver in order to verify that the setup worked!
python manage.py runserver  
{% endhighlight %}

In just four steps we have created a new project called 'healthsite' which will contain the infectious disease-related apps. Inside the new project, we've also created an app called 'diseaseapp' that we'll use for tracking infectious diseases. 

From here, we can navigate to the localhost (`http://127.0.0.1:8000/`) in our browser and verify that the setup worked as expected. If so, we'll see this page:

![web app landing page]({{site.baseurl}}/images/successful-django-setup.jpg)

## The essential Django components of our diseaseapp
The most important components for working in Django are our (1) views, (2) urls, and (3) models. 

### 1. Views
Views are types of web pages that usually have a specific purpose and template. 

<p style="text-align:right;"><i>diseaseapp/views.py</i></p>
{% highlight ruby %}
from django.http import HttpResponse

def index(request):
    return HttpResponse("Welcome to the disease app index.")
{% endhighlight %}

Now if you navigate to `http://127.0.0.1:8000/index` and you should see a page with the text "Welcome to the disease app index". Clearly, this is the most minimal possible view we could have created - Django is capable of so much more. If you want to start diving into all the functionalities available in Django views, I recommend checking out [this page]().  

### 2. URLs
Whenever you create a view in Django, you'll also need to configure a URL. You can easily do this using the `path()` function. For instance, a url configuration for AboutMe page might look like: `path('about/', views.about)`. This example has two main parts: (1) the url request to 'about/' and the view that it is routed to. 

![project-level urls file]({{site.baseurl}}/images/healthsite-urls-directory-levels.jpg)

#### A urls.py for the diseaseapp
Create a NEW urls.py **inside** of the diseaseapp directory. 

<p style="text-align:right;"><i>diseaseapp/urls.py</i></p>
{% highlight ruby %}
from django.urls import path

from . import views

urlpatterns = [
    path('', views.index, name='index'),
{% endhighlight %}


#### A urls.py for the healthsite project
Navigate back to the main project folder, where you'll see an existing urls.py file. Use this to point to the app-specific url we just created. This project-wide urls.py file will include pointers to all of the urlpatterns created within this project. 

<p style="text-align:right;"><i>healthsite/urls.py</i></p>
{% highlight ruby %}
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('diseaseapp/', include('diseaseapp.urls')),
    path('admin/', admin.site.urls)
]
{% endhighlight %}

The reason that Django creates a project-level urls.py automatically but does not create app-level urls.py for you is that there might be situations where you don't want to have public views that can be reached via url request. Therefore, Django lets you make this decision on an app-by-app basis by yourself. 


## How to Setup a Database in postgreSQL
If you've never used postgres before, check out [this short post](/tutorial/postgres-healthcare-database/) that will get you to a newly created database in minutes. 
- I like postgres because it scales really well. SQLite is easier with Django right out of the gate but if you start with postgres from the beginning and get really comfortable with it, it will help you get to a production-quality result at the end. 
- Also, I often find myself working on projects that involve complex maps. The postgreSQL extension postGIS is a natural extension that lets you generate geospatial databases. 

# Connecting Django to your postgres database 
Navigate to the settings file, __healthsite/settings.py__, which contains a lot of boilerplate admin. We just need to change the DATABASE settings so that they point to our newly-created postgres database instead of the default SQLite. 

#### Before - default sqlite settings:

![django settings default sqlite3]({{site.baseurl}}/images/sqlite-django-settings.jpg)

#### After - set to postgres backend:

![django settings default postgres]({{site.baseurl}}/images/postgres-django-settings.jpg)

And one more thing about the settings file (while we're here). Add this line inside of the INSTALLED_APPS : `'diseaseapp.apps.DiseaseappConfig'`. This lets the django healthsite *project* know about our infectious disease *app*.

![installed_apps settings]({{site.baseurl}}/images/installed-apps-settings-add.jpg)

Once the database is properly connected, use the following command:

{% highlight ruby %}
python manage.py migrate
{% endhighlight %}

![migrate django database]({{site.baseurl}}/images/migrate-disease-app.jpg)


# Models (i.e database tables)
In this section, we'll create the **models** that define the relationships for our infectious disease web application. 
<!-- To learn more about the structure of this schema, I recommend checking out this post on [UML diagrams](). -->

<p style="text-align:right;"><i>diseaseapp/models.py</i></p>
{% highlight ruby %}
from django.db import models

# Create your models here.
class Symptoms(models.Model):
    name = models.CharField(max_length=40)
    description = models.TextField()
    system = models.CharField(max_length=40)

    def __str__(self):
        return self.name

class PathogenType(models.Model):
    name = models.CharField(max_length=40)
    description = models.TextField()

    def __str__(self):
        return self.name

class Pathogen(models.Model):
    common_name = models.CharField(max_length=40)
    scientific_name = models.CharField(max_length=40)
    pathogen_type = models.ForeignKey(PathogenType, 
                        on_delete=models.PROTECT)
    description = models.TextField()

    def __str__(self):
        return self.common_name

class Prevention(models.Model):
    measure = models.CharField(max_length=80)
    description = models.TextField()
    rel_cost_pp = models.CharField(max_length=5)

    def __str__(self):
        return self.measure

class Disease(models.Model):
    name = models.CharField(max_length=40)
    description = models.TextField()
    pathogen = models.ForeignKey(Pathogen,
                         on_delete=models.PROTECT)
    symptoms = models.ManyToManyField(Symptoms)
    r0 = models.IntegerField(default=1)
    b = models.IntegerField(default=1)
    discovered = models.DateField('date discovered')
    prevention = models.ManyToManyField(Prevention)

    def __str__(self):
        return self.name
{% endhighlight %}

In this example database, I've tried to include a variety of different types of fields you're likely to encouter. For example: Integer, Character, Text, DateTime, ForeignKey and ManyToMany relationships. 


# Populating the database
### Using the Django admin site
Now, we're going to take advantage of the Django admin interface to populate our database. First, we'll generate a superuser (keep in mind the login information you create). Then, navigate to the development server. 

{% highlight ruby %}
python manage.py createsuperuser

    Username: diseaseapp_user
    Email address: diseaseapp@example.com
    Password: diseaseapp_pwd
    Password (again): diseaseapp_pwd

python manage.py runserver
{% endhighlight %}

With the server running, navigate in your browser to `http://127.0.0.1:8000/admin/` and login with the superuser information you created.

![django admin]({{site.baseurl}}/images/django-admin.jpg)
<!-- ![makemigrations database]({{site.baseurl}}/images/makemigrations-disease-app.jpg) -->


### Register a model in Django admin
The Django admin interface will be pretty empty until we connect it with our models in the backend. We can easily register a single model (e.g. the "Disease" model below) with a few lines in the app's `admin.py` file. 

<p style="text-align:right;"><i>diseaseapp/admin.py</i></p>
{% highlight ruby %}
from django.contrib import admin
from .models import Disease

admin.site.register(Disease)
{% endhighlight %}

We can do this for every one of our models. There is a shortcut though, which I like to use to automatically register all models in the admin.py file.

### Shortcut: register *ALL* models in Django admin
Instead of registering our models one-by-one, we can use this shortcut to register any model that hasn't already been registerd (via a try/except statement).

<p style="text-align:right;"><i>diseaseapp/admin.py</i></p>
{% highlight ruby %}
from django.contrib import admin
from django.apps import apps

models = apps.get_models()

for model in models:
    try:
        admin.site.register(model)
    except admin.sites.AlreadyRegistered:
        pass
{% endhighlight %}

Now, the admin page will show you a list of all the models we created. Each of these can be clicked on and populated using this built-in Django interface.

![django admin model interface]({{site.baseurl}}/images/django-admin-models.jpg)


## Populating the data
The Django admin interface is a real user-friendly way to insert data into our models. 

![django populate data]({{site.baseurl}}/images/add-new-disease-django-admin.jpg)

Continue adding data to each table until there is a satisfying amount of data to work with. The next part is to add data to our database tables. We can do this in a number of different ways, but my favorite is by using the API and <span style="color:hotpink">**fixtures**</span>. 

## Downloading the data as fixtures
Once the data is in the database, we can download the stored information as a fixture (data dump).

![data dump fixtures]({{site.baseurl}}/images/data-dump-fixture.jpg)

The four parts of this command are:
1. The Django `dumpdata` command 
2. optional formatting statements
3. The data to download - this can be just one model or the entire app as shown here
4. The path to/name of the fixture

The result is a json file that  be loaded into the database, serving as a great backup to the data entry work you've done so far. But you don't have to download the entire project into a massive fixture - it's just as easy to dump data for a single model:

{% highlight ruby %}
python manage.py dumpdata diseaseapp.disease > diseasefixture.json
{% endhighlight %}


![fixtures database dump]({{site.baseurl}}/images/fixtures-dump.jpg)

One of the nice things about having fixtures is that you can always revert back to this 'fresh load'. I often mess up my databases, especially when migrating or changing things around, and it's nice to know I can go back to this clean set of data. We can load the content from our database dumps into the database using:  

{% highlight ruby %}
manage.py loaddata diseasefixture.json
{% endhighlight %}

Now we have a fresh copy of the disease data for our database. This is great for when you want to run tests on your data - inserting, deleting, trying to break things - and knowing you can always revert back to this version of the data. 

## What's next?
In the next post, I'll cover building effective API endpoints and using the python package Graphene for advanced querying and mutation. Stay tuned!



<!-- NOTES TO SELF
1. Come up with UML diagram for this new django project. 
- remember to have at least one M:M, 1:M, for use in graphql later. 
2. Finish UML post
3. Actually create the django project. Make it something that is interesting and potentially useful. 
4. LATER: could make graphs of each disease spread, do a separate whole post/series on the visualization part of it. 


Create a Python database-access API for accessing Disease and Pathogen objects.
 -->


<!-- I cover fixture creation in [this post], but once you have the fixtures you can simply do this command to load them into your database:

`python manage.py loaddata...` -->




<!-- ## Other Modeling Posts
{: .t60 }
{% include list-posts tag='modeling' %} -->
