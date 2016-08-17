# Architecture

Good architecture allows us to create scalable applications.

## Docker

### About

Have you heard about docker? Not yet? Really? Well, then this would [help you][1]

In few words, it is something similar to virtual machine, but it is much more easy to set up and run, clone, create your own image and it also shares a lot of resources. One of the most important advantage is sharing images in public repositories and docker support by major cloud providers.

Do you want to create twenty fully set-up and working MySQL databases on your localhost (or at any other place)? Run one-line command twenty times and it is done. You dont even need powerful computer to do it, 2GB RAM (on debian) and few GB of space is enough. Now try to run twenty virtual machines...

### Everything is container

The instances are called _containers_, if we have our application to deploy, we just put it into the container, based on some setting, it is built, run and it is everything you need to do.

When new version of application comes into play, you just create new container and kill the old one. The end-user does not see nothing, reverse proxy just routes new connection to new container. Where no connection to the old container exist, you kill it. No downtime with minimum set-up time.

## Node.js

This is node.js cookbook, I assume you expect (and you are right) we are working in node.js and javascript. Still it is good to mention it.

### About

Node.js is powerful technology, which appeared at 2009 and started to grow exponencially, especially after 2013. Using javascript language allowed lot of modules to be shared - both on frontend and on backend. Today, the npm repository is by far the biggest repository in the world.

![Image][image-1]

[1]:    http://lmgtfy.com/?q=what+is+docker

### What node gave us

The same you can read on internet, when you are looking for it. Easy and fast developed applications with huge support from open-source world through many well-managed npm packages. Also requiring minimum time to get into this technology and its minimalistic Express framework.

### But but, what about dynamic typing

It has advantages and disadvantages at the same time. The biggest disadvantage is lack of static compiler options, if you are using right variables with right types, which can help a lot. The biggest advantage is sometimes the same - lack of static compiler possibility. You do not have to extend your object to just add one more field or new method, if you need it. Change requests are sometimes much less painfull than with Java or similar languages.

However, you are much more responsible for quality of code, its _clearness_ and understandability. Because you can do almost anything in Javascript, you are (can be) your own worst enemy.

### Does Node.js should be used for everything

Huge monoliths with ten thousands of work or more are not good use-case for node.js, this is where i.e. Java is shining (however do you really want to write huge monolith these days...?). Also some specific tasks can be handled by Python or Scala even better. It is always up to you.

## Microservices

It is also 

[image-1]: https://github.com/libor-vilimek/cookbook/raw/master/raw/Module-counts.png "https://quartetfs.com/blog/journey-gwt-react/"