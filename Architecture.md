# Architecture

Good architecture allows us to create scalable applications.

## Docker

### About

Have you heard about docker? Not yet? Really? Well, then this would [help you][1]

In a few words, it is something similar to a virtual machine, but it is much easier to set it up and run, clone, create your own images. One of the most important advantages is sharing it's images in public repositories and support by major cloud providers.

Do you want to create twenty fully set-up and working MySQL databases on your localhost (or at any other place)? Run one-line command twenty times and it is done. You dont even need powerful computer to do it, 2GB RAM (with debian) and few GB of space is enough. Now try to run twenty virtual machines with same settings... Or set up twenty independent MySQL databases on your localhost, how long does it take?

### Everything is container

The instances are called _containers_. You can create i.e. container with MySQL, Tomcat, Node.js... And to run any of these technologies, you just run one-line command, because fully working images already exist in public repositories.

__Deployment? No problem anymore!__
When new version of application comes into play, you just create new container. After it succesfully loads, you just stop the old one. The end-user does not see anything, reverse proxy just routes new connection to new container. Where no connection to the old container exist, you remove it. No downtime with minimum set-up time.

### Cost

Free. Opensource. Enjoy :).

## Node.js

This is Node.js cookbook, I assume you expect (and you are right _clever boy_) us to work with Node and Javascript.

### About

Node.js is powerful technology, which appeared at 2009 and started to grow exponencially, especially after 2013. Using Javascript language serverside allowed a lot of modules to be shared - for both frontend and backend. Today, the npm repository is by far the biggest repository in the world.

![Image][image-1]

### What Node gave us

The same you can read on internet almost everywhere. Easy and fast developed applications with huge support from open-source world through many well-managed npm packages. Also requiring minimum time to get into this technology and its minimalistic Express framework.

### But but, what about dynamic typing

It has advantages and disadvantages at the same time. The biggest disadvantage is lack of static compiler options. The biggest advantage is sometimes the same - lack of predefined types allows much easier modifications. You do not have to extend your object to just add one more field or new method, if you need it. Change requests are often less painfull than with Java or similar languages.

However, you are more responsible for the code quality, its _clearness_ and understandability. Because you can do almost anything in Javascript, you are your own worst enemy.

### Does Node.js should be used for everything

Huge monoliths with ten thousands of work or more are not good use-case for Node, this is where i.e. Java is shining (however do you really want to write huge monolith these days...?). Also some specific tasks can be handled by Python or Scala even better. It is always up to you.

## Microservices

![Image][image-2]

### About

Microservices are getting more popular each day, especially thanks to docker, which allowed to use them as easy and fully functional as possible. In past, programmers tried to implement _separation of concerns_ in different ways, based on what current technology was offering them. Starting with object oriented languages to separate responsiblity. Then frameworks and separating layers (MVC, MVVP) comes into play and then it continues with creating Service Oriented Architecture. Finally, the level of infrastructure worldwide, powered by cloud technology, allowed microservice architecture to become more efficient.

### Advantages

With microservices, you can assign more developers to the same project at the same time without interfering with each other's work (which is costly), because they work on different microservices. You can easily deploy and scale microservices (i.e. parsing statistics is not fast enough? Lets run five instances of it) and much more!

This is the future. We are the future. Ackee. (No, it is not official motto, it is my brain producing awesome ideas. This is why I get IT money for writing cookbook!)

### Disadvantages

You have to handle communication. Basically only one (serious) disadvantage, but the important one. You have to handle all the possible scenarios that can happen.

Also, similar to any other previous technologies, if you do not use it _right_, it does not help you.

## MongoDB

### About

It is perfect match for Node. If you have dynamic-typed language (Javascript) it is good to use it with _schemaless_ database. Aside from that, Mongo is also much faster for many database tasks.

### Why we use it

For similar reason as we adopted Node. Easy to use, easy to set-up or deploy, does not require pre-defined types (as Node.js), have a lot of support these days.

### Do we have to use it

Sure not! We do have projects, that use only MySQL or even both at the same time, MySQL and MongoDB, it always depends on the purpose. MongoDB lacks one of the best feature that MySQL has - transactions. The complexity of relational databases are the best and the worst they can offer. For gathering a lot statistics data, MongoDB is your friend. To handle critical banking service, maybe you would rather use relational database with transaction.

## MySQL/MariaDB

### About
MySQL is relational database owned by Oracle, which every single person who is reading this probably know with one great advantage...

![Image][image-3]

### Why we use it

As you probably saw above, it is free and well-developed database, which is running on such beast as youtube, facebook or twitter. Talking about relational databases and MySQL would be uninteresting for most of us, therefore I would not write more about it.

### MariaDB
We prefer to use MariaDB as it is maintened by core developers of previous MySQL.

### Knex & Bookshelf ORM

We have tried several frameworks to connect our Node applications with MySQL. Need to say - most of them are not mature enough (or they were not at the end of 2015). The one we are using and we can recommend is Knex - a powerful SQL querybuilder, supporting both callbacks and Promises/A+.

Knex provides great, but low-level interface to the storage. For working with models, there is a Bookshelf ORM library, allowing you  to define models and relations between them. Bookshelf is built on top of Knex, so anytime you can just fall back to Knex interface if ORM queries are too heavy, clumsy, or just hard to write.

This Knex-Bookshelf symbiosis is very nice to work with and we have not discovered any crucial limitations of Knex yet, which are the main reasons we use it.

## Push notifications

We were using Parse for long time and we were very satisfied with it. However Parse announced end of its services and we have to look for alternatives. We thought about using our own Parse server, because with this announcement, Facebook released Parse as open source. However we were not confident, if the community would be able to handle it in next years.

We decided to use Firebase, because google announced Firebase Cloud Messages and we were already using Firebase for real-time data. However the REST API we needed to use from our servers was not strong enough to our needs. We end up with our own - as simple as possible - push server, which is handling the requests.

But hey, we got microservice! (One meanlingess point to Ackee for using the TOP technology _paradigm_!)

## Elasticsearch

### About
Elasticsearch is open-source search engine, built on top of Apache Lucene. Due to its popularity there are a lot services connected to it generating additional value.

### Why use it
For searching of course. The API allows highly customizable searches that can be extremely fast and it doesn't put additional load on the database.

We use it usually to access data _fast_, but keep in mind Elasticsearch is search engine, not a database engine. That is why we keep important data also somewhere else, syncing those we search to Elastic, so we can look them up easily, as for complicated queries, it is usually much faster than to query large data sets in database directly.

### Kibana
Next service we are using is Kibana. It is built on elastic search and serves as logging service. Easy to set up and use, with a variety of options to visualize data.

[1]:    http://lmgtfy.com/?q=what+is+docker

[image-1]: https://github.com/AckeeCZ/nodejs-cookbook/raw/master/raw/Module-counts.png "https://quartetfs.com/blog/journey-gwt-react/"
[image-2]: https://github.com/AckeeCZ/nodejs-cookbook/raw/master/raw/63918150.jpg
[image-3]: https://github.com/AckeeCZ/nodejs-cookbook/raw/master/raw/yes-free-stuff.jpg