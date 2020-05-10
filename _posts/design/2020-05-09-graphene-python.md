---
layout: page
# sidebar: left
subheadline: 
title: "Graphene"
teaser: "Django and graphene."
breadcrumb: true
tags:
    - django
    - health database
    - infectious disease
    - health
    - article
categories:
    - tutorial
header:
    image_fullwidth: "/"
show_meta: true
comments: true
---

This tutorial builds off of the django healthsite application created as part of a [previous post]().


You'll need to install 
```conda install -c conda-forge django-filter```

If you get the error message: ```AssertionError: Setting 'Meta.model' without either 'Meta.fields' or 'Meta.exclude' has been deprecated since 0.15.0 and is now disallowed. Add an explicit 'Meta.fields' or 'Meta.exclude' to the DiseaseFilterSet class``` remember to add the line filter_fields = '__all__' .



# Why combine Django + GraphQL + Relay ?


# Master Filtering in Graphene_Django
- https://stackoverflow.com/questions/40381998/graphene-django-how-to-filter

# Django Model Properties in Graphene
- https://stackoverflow.com/questions/42963703/graphene-django-and-model-properties


# Customizing my Graphine-Django output
- https://stackoverflow.com/questions/51762817/get-query-to-return-list-of-values-instead-of-objects-in-graphene-django

# Keeping my Django Primary Key (UUID) in GraphQL
https://stackoverflow.com/questions/54328681/enable-pk-based-filtering-in-django-graphene-relay-while-retaining-global-ids




![installed_apps settings]({{site.baseurl}}/images/installed-apps-settings.webp)


{% highlight ruby %}
python manage.py migrate
{% endhighlight %}



## Other Modeling Posts
{: .t60 }
{% include list-posts tag='modeling' %}
