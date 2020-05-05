---
layout: page-fullwidth
breadcrumb: true
subheadline: Distribution Fitting with PyStan
title:  "Distribution Fitting with PyStan"
teaser: "Applying the Stan python package for distribution fitting"
breadcrumb: true
tags:
    - stan
    - pystan
    - statistics
categories:
    - code help
header:
    image_fullwidth: '/stan_title.png'
---
With the pystan package, you can either import a .stan file or you can define your stan model directly in the script. The three mandatory parts of the stan model definition are: (1) data; (2) parameters; and (3) model. 

{% highlight ruby %}
stan_model = """
data {
    int<lower=1> N; //Number of observed data
    real Y[N]; //observed data
    int<lower=1> K; //Number of mixture components;
    }
    
parameters
    simplex[K] theta; //mixing proportions for K components
    ordered[K} mu;
    vector<lower=0>[K] sigma; // prior on SD, cant be neg
    }
    
model {
    vector[K] log_theta = log(theta);
    real N2=N;
    //set priors
    mu[1]~normal(-3.4, 4)
    mu[2]~normal(-0.1, 2)
    
    //same prior for each simplex
    sigma~gamma(4,2)
    
    for (n in 1:N){
    vector[K] lps=log_theta;
        for (k in 1:K)
            lps[k] = lps[k] + normal_lpdf(Y[n] | mu[k], sigma[k]);
        target += log_sum_exp(lps);
        }
    }
"""
{% endhighlight %}

After defining the model, the next step is to compile the model. Compiling will take a few minutes - although it is also possible to pickle the model in order to avoid repeat compiling.  

{% highlight ruby %}
sm = pystan.StanModel(model_code=stan_model)
{% endhighlight %}

Finally, we can specify our parameters, including the number of iterations to cycle though. 

{% highlight ruby %}
#set up parameters
NumK = 2
ITER = 2000
NUMCHAIN = 4
{% endhighlight %}

{% highlight ruby %}
#define data and run model
Dat = {'N':len(dataframe), 'Y':dataframe, 'K':NumK}
fit = sm.sampling(data=Dat, n_jobs=1, iter=ITER, chains=NUMCHAIN)
{% endhighlight %}



<!-- ![l-moment smoothing]({{site.baseurl}}/images/histograms.png) -->