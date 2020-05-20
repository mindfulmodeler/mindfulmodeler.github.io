---
layout: page-fullwidth
subheadline: Zero to Python Hero
title:  "Getting Set Up in Python ASAP"
teaser: "A condensed step-by-step guide for installing Python + Anaconda in Windows."
breadcrumb: true
tags:
    - python
    - anaconda
    - jupyter
    - ipython
    - conda environment
categories:
    - code help
header:
    image_fullwidth: '/python-conda-setup-title2.jpg'
---

This is a condensed, step-by-step guide for anyone interested in getting Python up and running on their Windows machine as quick and complete as possible. By the end of this tutorial, you'll have the following: 

1. A working Anaconda distribution. 
2. The ability to download python packages. 
3. The interactive Jupyter notebook where you can run your python scripts from and immediately see the output. 
4. An example test script to get your on your way!

# Installation
Follow the steps outlined on [problemsolvingwithpython.com](https://problemsolvingwithpython.com/01-Orientation/01.03-Installing-Anaconda-on-Windows/), which provides Windows-specific instructions along with easy-to-understand screenshots. Highlights of the installation process:
1. Install for "Just Me" - it's not necessary to install it for "All Users"
2. You shouldn't need to install it as an Administrator
3. Don't add Anaconda to your PATH, unless you have a good reason to. 
4. Register Anaconda as your default for Python. 
5. If you're not sure you did everything correctly, [Anaconda has a page](https://docs.anaconda.com/anaconda/install/verify-install/) where you can verify that the installation worked.  


# I'm here for Python - so what is Anaconda and why did I just install it?
Whatever it is you want to do with python, I'm going to stop you right now and tell you that someone has probably already figured out a way to do it. Those amazing souls create **packages** to share that code with the rest of us, so that we don't have to write those same functions from scratch. There are zillions of packages out there, ready to help you [scrape Twitter data](https://pypi.org/project/twitterscraper/0.2.7/) or make [interactive world maps](https://docs.bokeh.org/en/latest/index.html) or almost anything else you can think of. Having a **package manager** allows you to find and install the package you want to use in seconds. The default package manager for Python is **pip**, which automatically comes with Python (so you should already have it on your machine). You can use pip to get new python packages off of the internet just by using the command `pip install <whatever-packagename>`. So if you're only interested in using a certain package, something like Pandas or Numpy, you can just use pip to install them without needing Anaconda at all. But Anaconda brings additional benefits beyond what pip can do:

1. Virtual environments. Anaconda makes it easy to create **conda virtual environments**, which is useful if you might be using two different versions of the same package on your computer for different projects. Having separate environments avoids the problem of version conflicts between the two projects (e.g. one new, one legacy). You can even use conda to have both Python 2 and Python 3 running on your system if you need to. 

Pip does not have the abiliy to create virtual environments, so you'll need something else (e.g. `virtualenv`) to have that ability. One place I find conda environments to be extremely useful is when working with the package **Django** to [create dynamic web applications](tutorial/django-infectious-disease-app/). I always start with a fresh conda environment for Django apps and it's simple to switch between environments when I need to.

2. Checking dependencies. The **pip install** will essentially download whatever package you tell it to. But one advantage of **conda install** is that it is smart enough to first check if installing that package is actually a good idea. With pip, you can run into package dependencies getting broken behind the scenes, since pip doesn't have the ability to fix these relationships. Conda, however, will take the time to prevent you from creating messed-up environments, which can save you a lot of headache down the road. 





## Create a New Conda Virtual Environment
Begin by opening a new Anaconda Prompt window. If you don't know where to find this, just use the task bar to search for it: 

![new conda prompt]({{site.baseurl}}/images/new-conda-prompt.jpg)

Inside the new prompt, you'll see your current environment and working directory, something like: ```(base) C:\Users\mindfulmodeler```. The most basic way of creating a new conda environment is by following this syntax:

{% highlight ruby %}
conda create --name djangoenv
{% endhighlight %}

This synatx tells conda that we want to create a new environment with the name *djangoenv*. Keep in mind that you can name your environment <span style="color:hotpink">**anything you want**</span>, so feel free to replace *djangoenv* with your own variation. 

After creating an environment, the next step is to install all the packages you want inside of that environment. You can do that in two separate steps, but it's often nice to create the environment with it's packages all in one go:

{% highlight ruby %}
conda create --name djangoenv pandas numpy scipy
{% endhighlight %}

![activate new conda environment]({{site.baseurl}}/images/activate-new-conda-env.jpg)


And then we can activate the newly created environment as the instructions tell us:

{% highlight ruby %}
conda activate djangoenv
{% endhighlight %}

If there are any additional packages we forgot to install earlier, it's easy enough to do using `conda install`.

{% highlight ruby %}
conda install pandas
{% endhighlight %}


We also need to add the Jupyter notebook package. In this case, however, we also need to add a `-c conda-forge` prefix before the package name, which indicates that we're getting it from an alternative source. This happens sometimes, as a subset of packages (like notebook) aren't available via the default anaconda channel.

{% highlight ruby %}
conda install -c conda-forge notebook
{% endhighlight %}

The [anaconda documentation](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-with-commands) is a great, easy-to-read reference for more commands related to virtual environment setup and package installation. And remember - if you're unsure about what channel you should install an anaconda package from, just Google it! If a package really isn't available anywhere in conda though, you can always use `pip install` instead (yes you can use pip inside a conda environment, but I'd advise only doing it as a last resort to avoid conflicts).

![conda-forge install package]({{site.baseurl}}/images/conda-install-package.jpg)


A final helpful command is ```conda env list```, which will show you all of your available environments. Simply use ```conda activate whateverenvname``` to switch to a different environment. 


## Jupyter - The interactive ipython notebook
Now, let's start doing some python! Begin by starting up Jupyter notebook with the following simple command, which will open a new Jupyter session in your browser:

{% highlight ruby %}
jupyter notebook
{% endhighlight %}

![start new jupyter notebook]({{site.baseurl}}/images/new-jupyter-notebook.jpg)


# Your first package - Pandas!
The first thing to do in our new python notebook is to import the package(s) of interest, in this case Pandas:

![begin working in jupyter notebook]({{site.baseurl}}/images/begin-jupyter.jpg)

To show the features of Pandas, we'll need an example spreadsheet to work with. Let's get some test data from Colorado's (open data portal)[https://data-cdphe.opendata.arcgis.com/search?tags=covid19] of COVID-19 cases. This site lets us filter by county and metric of interest, and then download that filtered data as a spreadsheet. 


![COVID-19 sample dataset]({{site.baseurl}}/images/sample-co-covid-data.jpg)


![COVID-19 pandas dataframe]({{site.baseurl}}/images/first-pandas-df-covid.jpg)

![preview COVID-19 dataframe]({{site.baseurl}}/images/df-head-covid.jpg)


![more pandas dataframe functions]({{site.baseurl}}/images/more-pandas-fns.jpg)

## You Might Also Like...
{: .t60 }
{% include list-posts tag='python' %}