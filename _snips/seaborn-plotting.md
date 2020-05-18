---
layout: page-fullwidth
subheadline: Overlapping histograms
title:  "Advanced Plotting in Seaborn"
teaser: "An example of generating multiple/overlaying subplots using Seaborn in python "
breadcrumb: true
tags:
    - python
    - seaborn
categories:
    - code help
header:
    image_fullwidth: '/hists_title.jpg'
---

{% highlight ruby %}
fig = plt.figure(figsize=(18,13))
BINS=30

for mn in range(1,13):
    ax = plt.subplot(4,3, int(mn))
    dataset_1 = np.random.normal(size=350)
    dataset_2 = np.random.uniform(-2, 2, size=350)
    
    plt.hist(dataset_1, bins=BINS, density=True, label='Normal dist', color='hotpink')
    sns.distplot(dataset_2, bins=BINS, norm_hist=True, kde=False, label='Uniform dist', color='yellow')
    
    plt.xlabel(f'Month - {mn}')
    plt.ylabel('Density')
    
    if mn>9:
        ax.set_xlabel('LABEL', size=14)
    if mn ==1:
        plt.legend(loc='upper left')
        
    plt.tight_layout()
    
fig.suptitle('Histograms of each month', size=16, y=1.04)

fig.savefig(f'histograms.jpg')
{% endhighlight %}

![l-moment smoothing]({{site.baseurl}}/images/histograms.jpg)