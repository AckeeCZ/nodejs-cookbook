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

[1]:    http://lmgtfy.com/?q=what+is+docker
