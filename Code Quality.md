# Code Quality

![Image][image-1]

## Eslint

We have discussed eslint in [Best Practices][1] section, it helps to keep code quality, but of course, only small part of it. The context is not proccesable by the machine.

## Standards

We have implemented few standards, which keeps our Node code (wow a rhyme) readable and consistent. If you get involved into one of our project and adopt the basic structure of application, then you are able to easily switch to any other. Even if you have never seen that project before, you should be able to implement new features or do change requests in reasonable times.

### Node Template

The structure of our projects is based on our __node template__ project. It is well-tested project that can be run and deployed itself. In last few years we have succesfully created a lot of projects, therefore we have identified use-cases which are common in most of them and we have put them into this Template.

#### Basic structure of project

We haven't invented wheel, we used the known approaches that was succesfully invented and tested in many applications.

```
 |->app
 |-->components *Having components like Elasticsearch, Redis for configuring and using it
 |-->controllers *Classic controllers
 |-->errors *Error messages
 |-->facade *Facades for accessing database, email services...
 |-->middleware *Classes and methods for using in middleware
 |-->models *Database models
 |-->routes *Defining routes (basically connecting URL with controllers and middleware methods)
 |-->services *Specialized services like userService for handling more complex user methods
 |->config *Configuration files and setting up the application (i.e. express, passport)
 |server.js *Main file
```

The flow of app



[1]: https://github.com/libor-vilimek/cookbook/blob/master/Best%20Practices.md "Best Practices"
[image-1]: https://github.com/libor-vilimek/cookbook/raw/master/raw/feel_bad_meme.jpg