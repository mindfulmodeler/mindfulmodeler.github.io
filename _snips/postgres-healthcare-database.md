---
layout: page
# sidebar: left
subheadline: Condensed guide to creating a new database 
title: "Making a database with postgres"
teaser: "Basic shell commands for starting a postgres database in Windows."
breadcrumb: true
tags:
    - postgres
    - database
    - infectious disease
    - health
    - article
categories:
    - tutorial
header:
    image_fullwidth: "/db-unsplash.jpg"
show_meta: true
comments: true
---

# Install postgres
[These step-by-step instructions with screenshots](https://www.postgresqltutorial.com/install-postgresql/) are very easy to follow. Just make sure you **remember the password** that you create, as you'll need it later. 

![postgres installation]({{site.baseurl}}/images/easy-postgres-installation.jpg)

## Create a new database
Navigate to the SQL shell (in Windows, search for 'psql'). Once there, type in the authentication information (you can hit 'enter' for everthing except the password). 

![create database from psql shell]({{site.baseurl}}/images/sql-shell.jpg)

Finally, create a new database called 'healthdb' for our disease modeling project using this simple command: 
{% highlight ruby %}
CREATE DATABASE healthdb;
{% endhighlight %}



## You might also like:
{: .t60 }
{% include list-posts tag='SQL' %}
