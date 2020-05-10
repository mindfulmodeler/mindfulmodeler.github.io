---
layout: page-fullwidth
breadcrumb: true
header:
    image_fullwidth: '/great-nonfiction-books-title.jpg'
title: Automatically convert images to .jpg format
subheadline: Improve your website's SEO
teaser: A useful powershell script for optimizing entire directories of images into .jpg format. 
fig-caption:
tags: [search engine optimization, code help, jekyll, optimization]
categories: [Tutorial]
---

This is a quick post on how you can easily convert a batch of images into .jpg format, from you command line. Webp is an image format promoted by Google for making images load faster (and thus improving your SEO ranking). There are online tools that will do this file conversion for you for free in your browser - just drag, drop, and download - so why bother with the command line at all? 

Many of these free conversion tools do indeed work - you'll see a "Success! Image converted to .jpg!" popup and then pat yourself on the back for avoiding a lot of unncessary work (at least that's what I did when I first started out). But then when you actually go to use that image - for instance in your WordPress or Jekyll blog - you'll be pulling your hair out wondering why your shiny new .jpg images aren't actually rendering in the browser! I can't speak to exactly why some of these free conversion tools don't work exactly right - but I can say that skipping them altogether in favor of the script below has ended up saving me a lot of headaches. 

# Convert a directory of .jpg images to .jpg
As an example, here is a directory containing front cover images of some of my favorite nonfiction books. 

![great nonfiction books]({{site.baseurl}}/images/great-nonfiction-books.jpg)

From their file extensions, you can see that they are all .jpgs. So let's get to converting them!

### Step 1: Download the Webp libraries from Google
You can download the precompilied utilities from this the [Google Developers page](https://developers.google.com/speed/webp/faq) - 
https://storage.googleapis.com/downloads.webmproject.org/releases/webp/index.html 

![google webp image conversion]({{site.baseurl}}/images/download-google-webp.jpg)

Save and extract the download to some location, for instance your Desktop. Remember this location as you'll need the path to it later!

### Step 2: Copy and paste the filepath to your image directory
Here, I'm copying the entire path to my book images, which are saved in a folder called "sample_images".

![copy image filepath]({{site.baseurl}}/images/copy-image-filepath.jpg)

### Step 3: Open up a new Powershell Prompt window
From the search bar on your Windows computer, you can search "powershell" in order to open up a new Powershell Prompt window. 

![windows cmd prompt]({{site.baseurl}}/images/powershell-prompt-window.jpg)

### Step 4: paste the filepath in the variable ```$loc```
After the blinking cursor in the prompt window, paste in this line (replacing the path location shown below with the path you copied in Step 1).

    $loc = "C:\mindfulmodeler\Documents\sample_images"

### Step 5: Look through all files
Finally, paste the following code into the powershell window. If you want more options into how the images are converted, feel free to check out https://developers.google.com/speed/webp/docs/cwebp for all the options available and edit the last line of this code block to your needs. 

{% highlight ruby %}
# get all files in the loc directory
$images = Get-ChildItem $loc

# loop through every images
foreach ($img in $images) {
  # output file will have .jpg extension instead of old extension
  $outputName = $img.DirectoryName + "\" + $img.BaseName + ".jpg"

  # copy-paste the path to where you extracted the cwebp program 
  C:\Desktop\libwebp-0.4.1-windows-x64\bin\cwebp.exe $img.FullName -o $outputName
}
{% endhighlight %}

![successfull webp image powershell]({{site.baseurl}}/images/powershell-webp.jpg)

![successfull webp images created]({{site.baseurl}}/images/successful-webp-conversion.jpg)


## You might also like:
{: .t60 }
{% include list-posts tag='health database' %}