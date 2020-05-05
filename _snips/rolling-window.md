---
layout: page-fullwidth
breadcrumb: true
header:
    image_fullwidth: '/lmoments.png'
title: Moving Window Function
date: 2020-05-02
teaser: An example moving or rolling window function that can be used for statistical smoothing operations.
fig-caption:
tags: [statistics, code help, python]
categories: [Tutorial]
---

The following is a python function for a moving window that can be used for a variety of statistical operations. 

### Rolling window function

{% highlight ruby %}
def rolling_window(A, win_shape=(3,3)):
    """
    This function creates a rolling window of dimensions 'winshape' to move over an input array (A). 
    A second array (W) of the same size as (A) is used to calculate the weights.
    
        A = The input array
        W = the weight array e.g.e elvation or max annual precip (A nd W should have the same dimensions)
        win_shape = the shape of the rolling window. Note that the win_shape should not be even-numbered ebcause the 
        calculattion uses the center cell of each moving window to determine the distance (i.e. absolute difference)
        to the other cells in the window.
    """
    for i in win_shape:
        assert (i % 2 ==1)  #"window dimensions must be odd-numbered (e.g. (3,3))"
        
    a_list = []
    for i in range(A.shape[0]):
        for j in range(A.shape[1]):
            min_row = i-int(floor(win_shape[0]/2))
            max_row = i+int(floor(win_shape[0]/2))
            min_col = j-int(floor(win_shape[0]/2))
            max_col = j+int(floor(win_shape[0]/2))
            
            #Resize edge windows
            if min_row < 0:
                min_row = 0
            if min_col < 0:
                min_col = 0
            if max_row > A.shape[0]:
                max_row = A.shape[0]
            if max_col > A.shape[1]:
                max_col = A.shape[1]
            
            #Create window(s)
            sub_A = A[min_row:max_row+1, min_col:max_col+1]
            sub_W = A[min_row:max_row+1, min_col:max_col+1] #same size window
                            
            #Get abs difference of center cell to surrounding cells
            diff = abs(sub_W - A[i,j])
                            
            #Get max distance in subarray
            max_sub = np.max(diff)
                            
            #Normalize subarray
            weights = (1-diff/max_sub)
            weights = weights/(sum(weights))
                            
            out = (sub_A*weights)
            a_list.append(np.sum(out))
               
    f = np.reshape(np.array(a_list),(A.shape[0], A.shape[1]))
    return f                 
{% endhighlight %}

![l-moment smoothing]({{site.baseurl}}/images/movingwindow2.png)

### Plot original versus smoothed data
{% highlight ruby %}
window_shape = (5, 5)
moving_window = rolling_window(A = data, W=weight_var, win_shape=window_shape)

#Display figures
fig, ax = plt.subplots(ncols=3, nrows = 3, sharex=Ture, sharey=True, figsize=(16, 10))

plt.subplot(1, 2, 1)
plt.imshow(data, origin = "lower left" )
plt.title('Original Data')

plt.subplot(1, 2, 2)
plt.imshow(moving_window, origin = "lower left" )
plt.title('Smoothed using {} '.format(window_shape)+' window')
{% endhighlight %}

