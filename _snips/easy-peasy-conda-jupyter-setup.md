---
layout: page-fullwidth
subheadline: Zero to Python Hero
title:  "Easy Peasy Python for Beginners"
teaser: "A condensed step-by-step guide for getting started with Python + Anaconda in Windows."
breadcrumb: true
tags:
    - python
    - anaconda
    - jupyter
    - ipython
    - conda environment
    - covid-19
categories:
    - code help
header:
    image_fullwidth: '/python-conda-setup-title2.jpg'
---

This is a short tutorial for anyone interested in getting Python up and running on their Windows machine as quickly and painlessly as possible. By the end of this tutorial, you'll have the following: 

1. A working Anaconda distribution. 
2. The ability to download python packages. 
3. The interactive Jupyter notebook where you can run your python scripts from and immediately see the output. 
4. An example test script of to get your on your way!


<div class="panel radius" markdown="1">
**Table of Contents**
{: #toc }
*  TOC
{:toc}
</div>

# Installing Python via Anaconda
There are many tutorials avaialable to show you how to install python, but I recommend following the steps outlined on the site [problemsolvingwithpython.com](https://problemsolvingwithpython.com/01-Orientation/01.03-Installing-Anaconda-on-Windows/). This site gives you Windows-specific instructions along with easy-to-understand screenshots, without any of the extra fluff you don't need to know about right now. 

##### Highlights of the installation process:
1. Install Anaconda for "Just Me" - it's not necessary to install it for "All Users"
2. You shouldn't need to install it as an Administrator
3. Don't add Anaconda to your PATH, unless you have a good reason to. 
4. Register Anaconda as your default for Python. 
5. If you're not sure you did everything correctly, [Anaconda has a page](https://docs.anaconda.com/anaconda/install/verify-install/) where you can verify that the installation worked. 

![all the anaconda features]({{site.baseurl}}/images/anaconda-gui.jpg) 


# I came here for Python - so what is Anaconda and why did I just install it?
Whatever it is you want to do with python, I've got to stop you and say that someone has probably already figured out a way to do it. Those brilliant people create python **packages** to share the code they created with the rest of us, so that we don't have to write those same functions from scratch. Anaconda makes just about anything related to handling python packages easier.

### 1. Anaconda is a superior package manager
There are zillions of packages out there, ready to help you [scrape Twitter data](https://pypi.org/project/twitterscraper/0.2.7/) or make [interactive world maps](https://docs.bokeh.org/en/latest/index.html) or almost anything else you can think of. Having a **package manager** allows you to find and install the package you want to use in seconds. 

The default package manager for Python is **pip**, which automatically comes with Python. You can use pip to get new python packages off of the internet just by using the command `pip install <whatever-packagename>`. So if you're only interested in using a certain package, something like Pandas or Numpy, you can just use pip to install them without needing Anaconda at all. But Anaconda brings additional benefits beyond what pip can do!

### 2. Conda virtual environments
Anaconda makes it easy to create **conda virtual environments**, which is useful if you might be using two different versions of the same package on your computer for different projects. Having separate environments avoids the problem of version conflicts between the two projects (e.g. one new, one legacy). You can even use conda to have both Python 2 and Python 3 running on your system if you need to. Pip does not have the abiliy to create virtual environments, so you'll need something else (e.g. `virtualenv`) to have that ability. 

One place I find conda environments to be extremely useful is when working with the package **Django** to [create dynamic web applications](tutorial/django-infectious-disease-app/). I always start with a fresh conda environment for Django apps and it's simple to switch between environments when I need to.

### 3. Conda checks package dependencies for you
The **pip install** command will essentially download whatever package you tell it to. But one advantage of **conda install** is that it is smart enough to first check if installing that package is actually a good idea. With pip, you can run into package dependencies getting broken behind the scenes, since pip doesn't have the ability to fix conflicting relationships. Conda, however, will take the time to prevent you from creating messed-up environments, which can save you a lot of headache down the road. 


## Create a New Conda Virtual Environment
Begin by opening a new Anaconda Prompt window. If you don't know where to find this, just use the Windows task bar to search for it: 

![new conda prompt]({{site.baseurl}}/images/new-conda-prompt.jpg)

Inside the new prompt, you'll see your current environment and working directory, something like: ```(base) C:\Users\mindfulmodeler```. The most basic way of creating a new conda environment is with the command ```conda create --name <somename>```.

![new conda prompt]({{site.baseurl}}/images/new-conda-env-commands.jpg)


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

## Installing packages with conda
If there are any additional packages we would like to install, it's easy enough to do using the `conda install <some-packagename>` command.

{% highlight ruby %}
conda install pandas
{% endhighlight %}


We also need to add the Jupyter notebook package. In this case, however, we also need to add a `-c conda-forge` prefix before the package name, which indicates that we're getting it from an alternative source. This happens sometimes, as a subset of packages (like notebook) aren't available via the default anaconda channel.

{% highlight ruby %}
conda install -c conda-forge notebook
{% endhighlight %}

The [anaconda documentation](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-with-commands) is a great, easy-to-read reference for more commands related to virtual environment setup and package installation. And remember - if you're unsure about what channel you should install an anaconda package from, just Google it! If a package really isn't available anywhere in conda though, you can always use `pip install` instead (yes you can use pip inside a conda environment, but I'd advise only doing it as a last resort to avoid conflicts).

![conda-forge install package]({{site.baseurl}}/images/conda-install-package.jpg)


A final helpful command is ```conda env list```, which will show you all of your available environments. Simply use ```conda activate <whatever-name>``` to switch to a different environment. 


# Jupyter - The interactive ipython notebook
Now, let's start doing some python! Begin by starting up Jupyter notebook by typing the following simple command into your Anaconda Prompt. This command which will automatically open a new Jupyter session in your browser:

{% highlight ruby %}
jupyter notebook
{% endhighlight %}

And you should see your internet browser appear with a blank Jupyter session, where you can create a new Python noebook to work in. 

![start new jupyter notebook]({{site.baseurl}}/images/new-jupyter-notebook.jpg)


# Your first package - Pandas!
The first thing to do in our new python notebook is to import the package(s) of interest, in this case Pandas:

![begin working in jupyter notebook]({{site.baseurl}}/images/begin-jupyter.jpg)

To show the features of Pandas, we'll need an example spreadsheet to work with. Let's get some test data from Colorado's [open data portal](https://data-cdphe.opendata.arcgis.com/search?tags=covid19) of COVID-19 cases. This site lets us filter by county and metric of interest, and then download that filtered data as a spreadsheet. 

![COVID-19 sample dataset]({{site.baseurl}}/images/sample-co-covid-data.jpg)

The easiest place to save this spreadsheeet of COVID-19 data would be in the same directory as this python notebook. However, it's fine if you want to save it somewhere else - you simply have to provide pandas with the full path to the file, rather than just the filename. 

To read in the spreadsheet, use the pandas command in your notebook:

{% highlight ruby %}
# Provide the name of the csv file
df = pd.read_csv("Community_Testing_Sites.csv")

# Or using full path:
df = pd.read_csv(r"C:/User/MindfulModeler/Documents/Community_Testing_Sites.csv")
{% endhighlight %}

Then, use the shortcut `SHIFT + ENTER` to execute the contents of the current cell. You should have no problem getting pandas to read in your csv, but if you do - just Google your error message! One of the best things about Python (and Pandas in particular) is the enormous user community and the wide range of help available on [StackOverflow](https://stackoverflow.com/questions/tagged/pandas). 

![COVID-19 pandas dataframe]({{site.baseurl}}/images/first-pandas-df-covid.jpg)

The first thing you should do after creating a dataframe is preview it to make sure its contents are what you expect! Simply use the command `df.head()` to get a snapshot of the first five rows of your data. Other commonly used summary commands are:
* `df.tail()`: to get the last five rows
* `df.info()`: to get information on the column datatype, number of rows in the dataframe
* `df.sample(5)`: to preview 5 random rows

![preview COVID-19 dataframe]({{site.baseurl}}/images/df-head-covid.jpg)

### Many more commands available in Pandas
Now that you've got your data as a pandas dataframe, you can easily edit, reshape, merge, rename, compute, and adjust this information to your heart's content! This tutorial is not intended to cover all that pandas can do, but I encourage you to keep playing with your sample dataset and check with StackOverflow whenever you have a question. 

![more pandas dataframe functions]({{site.baseurl}}/images/more-pandas-fns.jpg)

## You Might Also Like...
{: .t60 }
{% include list-posts tag='python' %}