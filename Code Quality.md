# Code Quality

![Image][image-1]

## Eslint

We have discussed eslint in [Best Practices][1] section, it helps to keep better code quality, but of course, only small part of it. The context is not proccesable by the machine.

## Standards

We have implemented few standards, which keeps our Node code (wow a rhyme) readable and consistent. If you get involved into one of our project and adopt the basic structure of application, then you are able to easily switch to any other. Even if you have never seen that project before, you should be able to implement new features or do change requests in reasonable times.

### Node Template

The structure of our projects is based on our __node template__ project. It is well-tested project that can be run and deployed itself. In last few years we have succesfully created a lot of projects, therefore we have identified use-cases which are common in most of them and we have put them into this Template.

#### Basic structure of project

We haven't invented wheel, we used the known best practicec.

```
 |->app
 |--->components *Having components like Elasticsearch, Redis for configuring and using it
 |--->controllers *Classic controllers
 |----->api *REST API controllers
 |----->forms *Handle forms
 |--->errors *Error messages
 |--->facade *Facades for accessing database, email services...
 |--->middleware *Classes and methods for using in middleware
 |----->fieldChecker *Checks mandatory fields before any controller is hit
 |--->models *Database models
 |----->mongo *Models for mongo
 |----->relation *Models for relational database
 |--->routes *Defining routes (basically connecting URL with controllers and middleware methods)
 |----->crud *Basic routing for CRUD operations
 |--->services *Specialized services like userService for handling more complex user methods
 |->config *Configuration files and setting up the application (i.e. express, passport)
 |--->routes.js *Configurate routes
 |--->express.js *Configurate express
 |server.js *Main file
```

The flow of app is as follows. The Node is started with server.js, it loads all the required configuration in config folders (especially express and routes definition) and starts the server on required port.

The config/routes defines basic structure of all routes with requiring app/routes modules. When request come, it finds path previously defined, it can go through middleware methods and hit function in controller. There it usually works with services or with facade methods. The facade is only file which is connected to database models and create queries for it. After it returns value, it goes all the way back to controller, where it is sent back to user.

## Naming conventions
It is good to use one naming convention for all the variables, functions and classes in the whole application. The camelCase was the one that won, because of simplicity, lack of special characters and fact it is widely used

## Separation of concerns
As mentioned in Architecture section of our cookbook, we try to not our applications to grow "too big" as time need to do anything in big project or get involved in it is huge.

The solution these days are microservices and Docker. If it makes sense and whole project is big enough, it is put into several microservices, which keeps each one of them small and well-arranged.

## Tests and Code coverage
It is described in Best Practices section. The tests and code coverage tools help us keep our code tested and possibly easier to find weak spots.

## JSDoc
There is a convention "how to comment your code", similar to JavaDoc. If you do it right, the tools in IDE are able to tell you, what parameter types are expected, what is returned and description of method. Also having a comment-style convention in all your code make it more readable for developers too.

### Generating JSDoc HTML
Not good :(. We have tried several tools, but none of them was able to generate good results (especially with linking it together). You can specify type in JSDoc (altough Javascript itself is dynamic-typed) and i.e. Webstorm is able to warn you, if you use wrong type. However tools for generating HTML JSDoc are not clever enough, and it gives you almost same insight possibilities as looking into the code itself.

## Merge requests
Also mentioned in Best Practices section. Every single line of code is reviewed by another programmer before it's merged into public branch.

## Const, let
We do not use _var_ anymore as it has unusual behaviour because of [Hoisting][2]. Const is good to declare your variable "unrewritable", therefore you cant by accident remove it and it is also another message just in code saying "this variable is initialized here and nowhere else and we do know about it". (It supplies _final_ statement in Java)

The _let_ behaves (almost) same as if you use it in Java. There is _limited_ Hoisting used, but it does not affect program as much  as _var_ can.

## 

[1]: https://github.com/AckeeCZ/nodejs-cookbook/blob/master/Best%20Practices.md "Best Practices"
[2]: http://www.w3schools.com/js/js_hoisting.asp
[image-1]: https://github.com/AckeeCZ/nodejs-cookbook/raw/master/raw/feel_bad_meme.jpg