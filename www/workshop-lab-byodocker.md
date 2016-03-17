---
layout: lab
title: BYO Docker
subtitle: Deploy an existing docker image
html_title: BYO Dockerfile
categories: [lab, developers, docker]
---

## Bring your own Docker
It's easy to get started with OpenShift whether that be using our app templates or bringing your existing Docker assets.  In this quick lab we will deploy app using an exisiting Docker image.  OpenShift will create an image stream for the image as well as deploy and manage containers based on that image.  And we will dig into the details to show how all that works.

### Let's point OpenShift to an existing built docker image
> <i class="fa fa-terminal"></i> Goto the terminal and type the following:

{% highlight csh %}
$ oc new-app kubernetes/guestbook
{% endhighlight %}


The output will show:

{% highlight csh %}
--> Found Docker image a49fe18 (17 months old) from Docker Hub for "kubernetes/guestbook"
    * An image stream will be created as "guestbook:latest" that will track this image
    * This image will be deployed in deployment config "guestbook"
    * Port 3000/tcp will be load balanced by service "guestbook"
--> Creating resources with label app=guestbook ...
    ImageStream "guestbook" created
    DeploymentConfig "guestbook" created
    Service "guestbook" created
--> Success
    Run 'oc status' to view your app.
{% endhighlight %}


### We can browse our project details with the command line
> <i class="fa fa-terminal"></i> Try typing the following to see what is available to 'get':

{% highlight csh %}
$ oc get
{% endhighlight %}

> <i class="fa fa-terminal"></i> Now let's look at what our image stream has in it

{% highlight csh %}
$ oc get is
{% endhighlight %}
{% highlight csh %}
$ oc describe is/guestbook
{% endhighlight %}

<i class="fa fa-info-circle"></i> An image stream can be used to automatically perform an action, such as updating a deployment, when a new image, such as a new version of the guestbook image, is created.

> <i class="fa fa-terminal"></i> The app is running in a pod, let's look at that

{% highlight csh %}
$ oc describe pods
{% endhighlight %}

### We can see those details using the web console too
Let's look at the image stream.  Hover over "Browse", then click "Image Streams", and then click on the guestbook image stream.  You should see something similar to this:

<img src="{{ site.baseurl }}/www/screenshots/ose-guestbook-is.png" width="600"/><br/>


### Does this guestbook do anything?
Good catch, your service is running but there is no way for users to access it yet.  We can fix that with the web console or the command line, you decide which you'd rather do from the steps below.

> To expose via the web console, click on "Overview" to get to this view:

<img src="{{ site.baseurl }}/www/screenshots/ose-guestbook-noroute.png" width="600"/><br/>

Notice there is no exposed route 

> Click on the "Create Route" link

<img src="{{ site.baseurl }}/www/screenshots/ose-guestbook-createroute.png" width="600"/><br/>

This is where you could specify route parameters, but we will just use the defaults.

> Click "Create"

Alternatively, you could've done this via the terminal.

> <i class="fa fa-terminal"></i> If you didn't use the web console do this:

{% highlight csh %}
$ oc expose service guestbook
{% endhighlight %}


### Test out the guestbook webapp
Notice that in the web console overview, you now have a URL in the service box.  There is no database setup, but you can see the webapp running by clicking the route you just exposed.

> Click the link in the service box


You should see:
<img src="{{ site.baseurl }}/www/screenshots/ose-guestbook-app.png" width="600"/><br/>


### Good work, let's clean this up
> <i class="fa fa-terminal"></i> Let's clean up all this to get ready for the next lab:

{% highlight csh %}
$ oc delete all --all
{% endhighlight %}


## Summary
TBD